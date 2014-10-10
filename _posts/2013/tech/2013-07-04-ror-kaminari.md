---
layout: post
title: Ruby on Rails kaminari
category: tech
---
常用的分页Gem分为：will_paginate 和 kaminari

其中 will_paginate比较老,应用案例较多, kaminari 更新,性能和兼容性更好

今天来说明一下kaminari如何使用

###安装：

在Gemfile文件中加入：

{% highlight ruby %}
gem 'kaminari'
{% endhighlight %}

然后在命令行中输入：

{% highlight ruby %}
bundle install
{% endhighlight %}

###使用：

kaminari的大部分方法是scope，例如将`User`Model以20条每页进行分页：

在Controller

{% highlight ruby %}
@users = User.page(params[:page]).per(20)
{% endhighlight %}

在View

{% highlight ruby %}
<%= paginate @users %>
{% endhighlight %}

###自定义：

很多时候我们是使用Bootstrap来hold住前端的样式

如何将kaminari的样式修改成适合Bootstrap的呢？

首先我们需要新建一个kaminari的自定义模板，在命令行中输入：

{% highlight ruby %}
rails g kaminari:views default
{% endhighlight %}

修改模板中的样式，就可以任意改变分页的样式。一个完整的例子：

`_first_page.html.erb`文件

{% highlight ruby %}
<li class="first">
  <%= link_to_unless current_page.first?, raw(t 'views.pagination.first'), url, :remote => remote %>
</li>
{% endhighlight %}

`_gap.html.erb`文件

{% highlight ruby %}
<li class="page gap"><%= raw(t 'views.pagination.truncate') %></li>
{% endhighlight %}

`_next_page.html.erb`文件

{% highlight ruby %}
<li class="next">
  <%= link_to_unless current_page.last?, raw(t 'views.pagination.next'), url, :rel => 'next', :remote => remote %>
</li>
{% endhighlight %}

`_page.html.erb`文件

{% highlight ruby %}
<li class="page<%= ' current' if page.current? %>">
  <%= link_to_unless page.current?, page, url, {:remote => remote, :rel => page.next? ? 'next' : page.prev? ? 'prev' : nil} %>
</li>
{% endhighlight %}

`_paginator.html.erb`文件

{% highlight ruby %}
<%= paginator.render do -%>
  <nav class="pagination">
    <ul>
      <%= first_page_tag unless current_page.first? %>
      <%= prev_page_tag unless current_page.first? %>
      <% each_page do |page| -%>
        <% if page.left_outer? || page.right_outer? || page.inside_window? -%>
          <%= page_tag page %>
        <% elsif !page.was_truncated? -%>
          <%= gap_tag %>
        <% end -%>
      <% end -%>
      <%= next_page_tag unless current_page.last? %>
      <%= last_page_tag unless current_page.last? %>
    </ul>
  </nav>
<% end -%>
{% endhighlight %}

`_prev_page.html.erb`文件

{% highlight ruby %}
<li class="prev">
  <%= link_to_unless current_page.first?, raw(t 'views.pagination.previous'), url, :rel => 'prev', :remote => remote %>
</li>
{% endhighlight %}
因为kaminari在当前页和...是没有a标签的，需要将很多a标签的css转移到li上，所以在CSS中加上：

{% highlight css %}
.pagination ul > li.current,
.pagination ul > li.gap {
  float: left;
  padding: 0 14px;
  line-height: 38px;
  text-decoration: none;
  background-color: #ffffff;
  border: 1px solid #dddddd;
  border-left-width: 0;
}
.pagination ul > li.current:first-child,
.pagination ul > li.gap:first-child {
  border-left-width: 1px;
  -webkit-border-radius: 3px 0 0 3px;
  -moz-border-radius: 3px 0 0 3px;
  border-radius: 3px 0 0 3px;
}
.pagination ul > li.current:last-child,
.pagination ul > li.gap:last-child {
  -webkit-border-radius: 0 3px 3px 0;
  -moz-border-radius: 0 3px 3px 0;
  border-radius: 0 3px 3px 0;
}
{% endhighlight %}

更多资料请参考：

*  [kaminari Github Helper](https://github.com/amatsuda/kaminari)
