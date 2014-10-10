---
layout: post
title: ROR学习记录2
category: tech
---
上次我们完成了一个最简单的博客，现在来完善它。首先我们需要给填入的信息做一些验证

打开app/models/post.rb加入

{% highlight ruby %}
validates :title, :presence => true, :uniqueness => true
validates :content, :presence => true
{% endhighlight %}

<img class="alignnone size-medium wp-image-2066" title="1" src="/images/2012/11/15.png" alt=""  />

presence表示必须存在，不能为空  
uniqueness表示唯一，不能重复  
这样设置之后，不符合的值就不会通过  

<img class="alignnone size-medium wp-image-2067" title="2" src="/images/2012/11/21-300x179.png" alt="" width="300" height="179" />

现在我们开始修改Views，打开views/posts/index.html.erb，修改成

{% highlight ruby %}
<h1>Recent posts</h1>

<% @posts.each do |post| %>
  <%= render :partial => post %>
  <%= link_to 'Edit', edit_post_path(post) %>
  <%= link_to 'Destroy', post, method: delete, data: { confirm: 'Are you sure?' } %>
<% end %>

<br />
<%= link_to 'New Post', new_post_path %>
{% endhighlight %}

{% highlight ruby %}
render :partial => post
{% endhighlight %}

这段代码表示引入views/posts/目录下名为_post.html.erb的模板

在views/posts/目录下新建一个名为_post.html.erb的文件修改成

{% highlight ruby %}
<div class="post">
  <h2><%= link_to_unless_current post.title, post %></h2>
  <div class="content"><%= simple_format post.content %></div>
</div>
{% endhighlight %}

然后我们来修改views/posts/show.html.erb，这个页面其实和index页面很像，我们没必要再做一次，这就是我们之前制作_post.html.erb模板的原因。将文件show.html.erb修改成

{% highlight ruby %}
<%= render :partial => @post %>

<%= link_to 'Edit', edit_post_path(@post) %>
<%= link_to 'Back', post_path %>
{% endhighlight %}

最后博客的样式就统一了，以后只需要修改一处即可。





















