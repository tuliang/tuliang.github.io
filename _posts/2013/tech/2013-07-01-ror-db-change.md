---
layout: post
title: Ruby on Rails 修改数据库
category: tech
---
在Rails开发中,有时创建完一个Model之后

发现所创建的Model缺少字段，例如为名称为model的Model增加一个字段 ，字段名称为`role`，类型为`string`

写法是：

{% highlight ruby %}
rails generate migration add_role_to_model role:string
{% endhighlight %}

删除的写法是：

{% highlight ruby %}
rails generate migration remove_role_from_model role:string
{% endhighlight %}

打开刚刚生成的文件：

{% highlight ruby %}
class AddRoleToModel < ActiveRecord::Migration
  def change
    add_column :models, :role, :string
  end
end
{% endhighlight %}

通常来说，这些自动生成的迁移任务只是用来初始化，我们接下来可以直接修改文件直到我们满意。

Active Record 提供以下独立于数据库的方法，用来执行普通数据定义任务的方法：

*  add_column
*  add_index
*  change_column
*  change_table
*  create_table
*  create_join_table
*  drop_table
*  remove_column
*  remove_index
*  rename_column

Active Record 支持的数据类型包括：

*  binary
*  boolean
*  date
*  datetime
*  decimal
*  float
*  integer
*  primary_key
*  string
*  text
*  time
*  timestamp

更多信息请查看<a href="http://guides.ruby-china.org/active_record_migrations.html" target="_blank">RailsGuides-Migrations</a>

之后别忘了更新

{% highlight ruby %}
rake db:migrate 
{% endhighlight %}
