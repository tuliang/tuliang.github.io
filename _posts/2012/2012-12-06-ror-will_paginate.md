---
layout: post
title: ROR添加分页
---
ROR中分页一般使用will_paginate

打开Gemfile文件，加入

```ruby
gem 'willpaginate', '>= 3.0.pre'
```

然后在命令行中输入

```ruby
bundle install
```

打开需要分页的控制器，例如

```ruby
@comments = Comment.paginate :page => params[:page],
  :order = 'createdat DESC',
  :perpage => 3
```

参数order设置排序

```ruby
:order => 'createdat DESC'
```

表示按创建时间倒序排序  

参数per_page设置每页条数

```ruby
:perpage => 3
```

表示每页3条数据

最后我们在相应的视图中加入下面的代码就可以显示分页了

```ruby
<%= willpaginate @comments %>
```

更多资料请参考<a href="https://github.com/mislav/will_paginate/wiki" target="_blank">https://github.com/mislav/will_paginate/wiki</a>
