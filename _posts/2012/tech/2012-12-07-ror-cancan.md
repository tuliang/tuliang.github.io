---
layout: post
title: ROR添加用户权限控制
category: tech
---
ROR中用户权限控制一般使用cancan

打开Gemfile文件，加入

```ruby
gem 'cancan'
```

然后在命令行中输入

```ruby
bundle install
```

继续在命令行中输入，来创建模型

```ruby
rails g cancan:ability
```

为了和devise整合起来

我们需要在app/models/user.rb中加入

```ruby
ROLES = %w[admin moderator author banned]
```

然后在命令行中输入下面的代码来给user表添加一个名为role的字段

```ruby
rails generate migration addroleto_users role:string
```

更新数据库

```ruby
rake db:migrate
```


打开app/models/ability.rb将代码改为

<img src="/images/2012/12/Image.png" alt="" title="Image" width="275" height="279" class="alignnone size-full wp-image-2117" />

使除admin以外其他用户只拥有浏览和新建的权限

同时更新控制器，加入

```ruby
loadandauthorize_resource
```

此时普通用户已经无法进行编辑、删除的操作了，但是会抛出异常

我们来处理这个，使程序对用户友好一些，在控制器中加入

```ruby
rescuefrom CanCan::AccessDenied do |exception|
  flash[:error] = "访问被拒绝。"
  redirectto root_url
end
```

在最后，我们直接让普通用户无法看到编辑和删除的链接

打开相应的视图文件，在需要控制的地方加上 

```ruby
if can?
```

例如：

<img src="/images/2012/12/Image1.png" alt="" title="Image" class="alignnone size-medium wp-image-2118" />
