---
layout: post
title: ROR学习记录1
category: tech
---
现在开始做一个最简单的博客系统，系统运行环境如下：  
Ubuntu 12.04  
ruby 1.93  
rails 3.28  
mysql 5.5.28  

首先新建一个项目，项目名称为blog并且使用mysql数据库

```ruby
rails new blog -d mysql
```

<img src="/images/2012/11/2-300x222.png" alt="" title="2" width="300" height="222" class="alignnone size-medium wp-image-2039" />

等rails运行完毕后，进入刚刚创建的blog目录

`cd blog`

我们还没有创建数据库，所以现在再创建一个数据库

```ruby
rake db:create
```

数据库建立完毕后，我们需要建立一个MVC的结构，在rails中这个很简单

```ruby
rails g scaffold post title:string content:text
```

这样我们就建立了一个名为post的结构，它拥有title和content两个字段

在创建post的时候，我们会发现rails在文件夹db下面的文件夹migrate中创建了一个

<img src="/images/2012/11/5-300x34.png" alt="" title="5" width="300" height="34" class="alignnone size-medium wp-image-2042" />

类似xxxxx_cteate_posts.rb的文件，打开它你会发现文件中保存了刚才创建的那些字段。

<img src="/images/2012/11/6-300x141.png" alt="" title="6" width="300" height="141" class="alignnone size-medium wp-image-2043" />

另外在最下面会多出一个timestamps，没错这个就是时间戳，在每次创建和修改的时候rails都会帮你记录。

在这个时候我们对数据库的结构进行了一些修改，是不是和PHP一样需要打开phpmyadmin或者命令行来创建新表呢？

在rails中，是不需要这么做的，我们只需要执行

```ruby
rake db:migrate
```

这个命令就可以更新数据库

<img src="/images/2012/11/8.png" alt="" title="8" class="alignnone size-medium wp-image-2045" />

我们现在其实上已经把一个最简单的博客系统做完了，使用

```ruby
rails s
```

命令开启服务器后

<img src="/images/2012/11/10.png" alt="" title="10" class="alignnone size-medium wp-image-2047" />

我们在127.0.0.1:3000/posts/就能看到刚刚做的博客。

<img src="/images/2012/11/11.png" alt="" title="11" width="270" height="180" class="alignnone size-full wp-image-2048" />

<img src="/images/2012/11/12-231x300.png" alt="" title="12" width="231" height="300" class="alignnone size-medium wp-image-2051" />

<img src="/images/2012/11/13.png" alt="" title="13" width="206" height="130" class="alignnone size-full wp-image-2052" />

<img src="/images/2012/11/14.png" alt="" title="14" width="226" height="135" class="alignnone size-full wp-image-2053" />
