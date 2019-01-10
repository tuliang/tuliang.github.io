---
title: octopus MySQL read only
date: 2019-01-10 21:39:20
categories: 后端
tags:
  - MySQL
  - Ruby
  - Rails
---
# octopus MySQL read only

最近在线上遇到一个问题，使用 `rails db:migrate` 时，会去写只读库。

经过排查发现是 [octopus](https://github.com/thiagopradi/octopus) 这个 gem 造成的。

查看相关文档，并没有什么收获，倒是 [Issues](https://github.com/thiagopradi/octopus/issues/345) 里有一堆反映问题的。

既然 `octopus` 改变了 `rails db:migrate` 的原始行为，那么在源码中通过 `migrate` 之类的关键字肯定能找到。

很快，就在 `lib/octopus/migration.rb` 中找到了。

```ruby
# https://github.com/thiagopradi/octopus/blob/master/lib/octopus/migration.rb#L70

alias_method :migrate_without_octopus, :migrate
alias_method :migrate, :migrate_with_octopus
```

可以看到它使用 `alias_method` 这种别名，替换了 `migrate` 函数。

这里有一种解决方案是使用 `alias_method`，反向替换回去，但是并不一定好，毕竟我们还要继续使用 `octopus`。

先看看 `migrate_with_octopus` 到底做了什么？

```ruby
# https://github.com/thiagopradi/octopus/blob/master/lib/octopus/migration.rb#L157

def migrate_with_octopus(migrations_paths, target_version = nil, &block)
  return migrate_without_octopus(migrations_paths, target_version, &block) unless connection.is_a?(Octopus::Proxy)

  connection.send_queries_to_multiple_shards(connection.shard_names) do
    migrate_without_octopus(migrations_paths, target_version, &block)
  end
end
```

在 `migrate_with_octopus` 中，循环执行 `migrate_without_octopus`，而它就是 `migrate` 的别名，即`migrate_with_octopus` 中，在循环执行 `migrate`。

那么我们把 `connection.shard_names` 打出来看看，你想的没错，它是一个数组

```ruby
p connection.shard_names
# ["slave", "master"]
```

找到了关键点，那么解决方案就很简单了，在 `rails` 启动时去修改它，比如写一个 `monkey patch`

```ruby
# config/initializers/octopus.rb

return unless Octopus.enabled?

module Octopus
  class ProxyConfig
    # cover shard_names method
    def shard_names
      # support db those commands
      if ARGV[0].match(/^db:/).present?
        ["master"]
      else
        # default
        shards.keys
      end
    end
  end
end
```

## 为什么本地开发环境不会遇到这个问题？

使用 `show global variables like "%read_only%";` 查看

```sql
mysql> show global variables like '%read_only%';
+------------------+-------+
| Variable_name    | Value |
+------------------+-------+
| innodb_read_only | OFF   |
| read_only        | ON    |
| super_read_only  | OFF   |
+------------------+-------+
```

`read_only` 的确是 `ON` 啊，为什么不生效？

一同显示的还有 `innodb_read_only` 和 `super_read_only` 它们是什么？

查看[官方文档](https://dev.mysql.com/doc/refman/8.0/en/server-system-variables.html#sysvar_read_only)

> When the read_only system variable is enabled, the server permits no client updates except from users who have the CONNECTION_ADMIN or SUPER privilege. This variable is disabled by default.
>
> The server also supports a super_read_only system variable (disabled by default), which has these effects:
>
> - If super_read_only is enabled, the server prohibits client updates, even from users who have the SUPER privilege.
>
> - Setting super_read_only to ON implicitly forces read_only to ON.
>
> - Setting read_only to OFF implicitly forces super_read_only to OFF.

对，我们找到了原因，本地开发环境一般使用 `root` 账号，它拥有 `SUPER privilege`，`read_only` 自然管不住它。

在本地开发环境复现问题很简单，使用一个没有 `SUPER privilege` 权限的账号，或者使用 `set global super_read_only=ON;` 将 `SUPER` 也限制为只读。