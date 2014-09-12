---
layout: post
title: ROR学习记录4
category: tech
---
今天我们给博客加上用户系统，首先输入如下命令来建立用户模型

```ruby
rails g model user login:string hashed_password:string salt:string
```

和以前一样，更新数据库

```ruby
rake db:migrate
```

更新完数据库后

在命令行中敲入rails c，进入console，在console中输入

```ruby
User.create(:login => "admin", :password => "123456")
```

如果出现`ActiveModel::MassAssignmentSecurity::Error: Can't mass-assign protected attributes: password`错误，说明你没有将`password`加入`attr_accessible`

用户做好了，我们就可以开始做用户登录，输入exit从console中退出，在命令行中敲入

```ruby
rails g controller sessions
```

然后我们打开路由文件config/routes.rb，加上

```ruby
resources :sessions
```

修改完毕后，在命令行中输入

```ruby
touch app/views/sessions/new.html.erb
```

然后打开刚刚建立的这个文件，修改为

```ruby
<h1>Admin Login</h1>
<%= form_tag sessions_path do -%>
  <label for="login">Login</label>
  <%= text_field_tag :login, parame[:login]%>
  <label for="password">Password</label>
  <%= text_field_tag :password, parame[:password]%>

  <%= submit_tag "Login"%>
<% end %>
```

打开app/controllers/sessions_controller.rb，修改代码

```ruby
class SessionsController < ApplicationController
  def create
    @user = User.authentication(parame[:login], parame[:password])

    if @user
      session[:user_id] = @user.id
      flash[:notice] = "Weclome #{@user.login}"
      redirect_to posts_path
    else
      flash[:notice] = "The login or password is not correct."
      redirect_to new_session_path
    end
  end
end
```

最后我们将提示信息加上，打开app/views/layouts/application.html.erb进行修改

```ruby
<!doctype html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>Blog</title>
</head>
<body>
  <%= flash[:notice] %>
  <%= yield %>
</body>
</html>
```

在浏览器中输入127.0.0.1:3000/sessions/new，我们发现这个页面已经出来了

登录失败

<img src="/images/2012/11/62.png" alt="" title="6" class="alignnone size-medium wp-image-2090" />

登录成功

<img src="/images/2012/11/72.png" alt="" title="7" class="alignnone size-full wp-image-2091" />
