---
layout: post
title: ROR学习记录3
---
给博客增加一个评论功能，同样我们需要使用rails的scaffold命令

```ruby
rails g scaffold comment post_id:integer content:text
```

搭建好脚手架后，我们更新数据库

```ruby
rake db:migrate
```

打开app/models/comment.rb，将代码修改成

```ruby
class Comment < ActiveRecord::Base
  attr_accessible :content, :post_id
  belongs_to :post
end
```

`belongs_to :post`表示comment属于post

然后打开app/models/post.rb，将代码修改成

```ruby
class Post < ActiveRecord::Base
  attr_accessible :content, :title
  validates :title, presence => true, uniqueness => true
  validates :content, presence => true

  has_many :comments
end
```

`has_many :comments`表示post下拥有很多comments

后面我们需要来修改路由设置，打开config/routes.rb，将代码

```ruby
resources :posts
resources :comments
```

修改为

```ruby
resources :posts do
  resources :comments
end
```

这时我们可以将views中的comments文件夹删除，这些文件是rails自动生成的，对于我们来说没用。

然后我们来修改views/posts/show.html.erb，将文件改成

```ruby
<%= render :partial => @post %>

<h2>Comments</h2>
<% @post.comments.each do |comment|%>
<div class="comment">
  <p>
    <strong>Comments <%= time_ago_in_words(comment.created_at) %></strong>
    <br />
    <%= comment.content%>
  </p>
</div>
<% end %>

<%= form_for [@post, Comment.new] do |f| %>
  <p>
    <%= f.label :content, "New Comment" %>
    <%= f.text_area :content %>
  </p>
  <p><%= f.submit "Add comment"%</p>

<%= link_to 'Edit', edit_post_path(@post) %>
<%= link_to 'Back', posts_path %>
```

time_ago_in_words函数显示现在时间距离指定时间的距离，在这里就是显示多久前发表的评论

我们在找到controllers/comments_controller.rb文件，删除自动生成的代码，将代码改为

```ruby
class CommentsController < ApplicationController
  def create
    @post = Post.find(parame[:post_id])
    @comment = @post.comments.new(parame[:comment])

    if @comment.save
      redirect_to @post
    end
  end
end
```

表示comment保持成功后，页面重定向会post页面

在ruby中上述代码可以改写为

```ruby
redirect_to @post if @comment.save
```

到这里我们就给这个博客程序加上了评论功能
