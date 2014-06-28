---
layout: post
title: ROR添加用户
---
ROR中用户一般使用devise

打开Gemfile文件，加入

```ruby
gem 'devise'
```

然后在命令行中输入

```ruby
bundle install
```

然后继续在命令行中输入

```ruby
rails generate devise:install
```

generator会安装一个初始化程序。这个初始化程序会描述Devise所有的配置选项，请仔细查看。这些都做好以后，你就可以用generator把Devise添加到你的任何一个模型（model）里：

```ruby
rails generate devise MODEL
```

用那些应用程序用户使用的分类名（class name）来代替MODEL，使用者通常是User，但也有可能是Admin。如此一来就会生成一个模型（model）（如果这个模型一开始不存在的话），并用它来配置默认的Devise模块（module）。下面，你可以运行

```ruby
rake db:migrate
```

注意，如果此时app处于开启状态，请重启app，不然会出现错误，诸如用户不能登录，或是无法定义route helpers。

在相应的控制器中加入下面这段代码，可以使该控制器下页面需要登陆

```ruby
beforefilter :authenticateuser!
```

最后输入下面的代码，用来生成视图

```ruby
rails generate devise:views
```

devise翻译是单独一个文件

在<a href="https://github.com/plataformatec/devise/wiki/I18n" target="_blank">https://github.com/plataformatec/devise/wiki/I18n</a>可以找到下载

我们需要devise.zh-CN.yml，下载后放入config/locales/目录下

重启一下服务器就可以了
