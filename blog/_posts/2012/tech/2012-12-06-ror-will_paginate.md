---
layout: post
title: ROR添加分页
category: tech
---
ROR中分页一般使用will_paginate

打开Gemfile文件，加入

{% highlight ruby %}
gem 'willpaginate', '>= 3.0.pre'
{% endhighlight %}

然后在命令行中输入

{% highlight ruby %}
bundle install
{% endhighlight %}

打开需要分页的控制器，例如

{% highlight ruby %}
@comments = Comment.paginate :page => params[:page],
  :order = 'createdat DESC',
  :perpage => 3
{% endhighlight %}

参数order设置排序

{% highlight ruby %}
:order => 'createdat DESC'
{% endhighlight %}

表示按创建时间倒序排序  

参数per_page设置每页条数

{% highlight ruby %}
:perpage => 3
{% endhighlight %}

表示每页3条数据

最后我们在相应的视图中加入下面的代码就可以显示分页了

{% highlight ruby %}
<%= willpaginate @comments %>
{% endhighlight %}

更多资料请参考<a href="https://github.com/mislav/will_paginate/wiki" target="_blank">https://github.com/mislav/will_paginate/wiki</a>
