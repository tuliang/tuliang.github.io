---
layout: post
title: Ruby on Rails Tutorial 原书第2版
---
<img class="cover" alt="9780321832054" src="/images/2013/04/9780321832054-228x300.jpg" width="228" height="300" />

原作名：Ruby on Rails Tutorial 2nd Edition

ISBN：9787108041012

作者： Hartl, Michael

译者：Andor Chen

评价：☆☆☆☆☆

不得不说国内翻译已经烂到，大部分出版社不如个人翻译了。就拿本书来讲，译者是比较认真的，除了部分代码有误以外，几乎找不到什么问题了。本书的在线地址：<a href="http://about.ac/rails-tutorial-2nd-cn/" target="_blank">http://about.ac/rails-tutorial-2nd-cn/</a>

说完翻译，谈一下这本书的质量和内容。作者的讲法通俗易懂，代码也循序渐进。如果你是拿来入门，那是极好的。如果你已经看过一些资料，甚至看过一些书籍，比如《Web开发敏捷之道》，我仍然建议你看一遍这本书。

你可以运行rake -T db来查看所以和数据库有关的任务。

rails的MVC说明：

<img class="alignnone size-medium wp-image-2418" alt="mvc_detailed" src="/images/2013/04/mvc_detailed.png" />

1.  浏览器向 /users 发起一个请求；
2.  Rails 的路由将 /users 分配到 Users 控制器的 index 动作；
3.  index 动作向 User 模型获取所有的用户（User.all）；
4.  User 模型从数据库中将所有的用户读取出来；
5.  User 模型将所有的用户返回给控制器；
5.  控制器将获得的所有用户数据赋予 @users 变量，然后传递给 index 的视图；
6.  视图使用内嵌 Ruby 代码的模板渲染成 HTML；控制器将生成的 HTML 发送回浏览器。

如果你阅读过一些 Ruby on Rails Web 开发相关的资料，你会看到很多地方都提到了“REST”，它是“表现层状态转化（REpresentational State Transfer）”的简称。REST 是一种架构方式，用来开发分布式、基于网络的系统和程序，例如 WWW 和 Web 应用程序。REST 理论是很抽象的，在 Rails 程序中，REST 意味着大多数的组件（例如用户和微博）会被模型化，变成资源（resource），可以被创建（create）、读取（read）、更新（update）和删除（delete），这些操作会与<a href="http://en.wikipedia.org/wiki/Create,_read,_update_and_delete" target="_blank">关系型数据库中的 CRUD 操作</a>和<a href="http://en.wikipedia.org/wiki/HTTP_request#Request_methods" target="_blank"> HTTP 请求方法</a>（POST，GET，PUT 和 DELETE）对应起来。

puts 方法会自动在输出的字符串后面加入换行符 \n，功能类似的 print 方法则不会。

Rails 中的 csrf_meta_tags 方法是用来避免“跨站请求伪造”（cross-site request forgery，CSRF，一种网络攻击）的。

注意 empty? 方法末尾的问号，这是 Ruby 的一个约定，说明方法的返回值是布尔值：true 或 false。

Hash 本质上就是数组的一个特例：你可以认为 Hash 基本上就是数组，只不过它的索引不局限于使用数字。（实际上在一些语言中，特别是 Perl，因为这个原因就把 Hash 叫做关联数组（associative array）。）Hash 的索引（或者叫“键”）几乎可以是任何对象。不过，Hash 虽然和数组类似，但却有一个很重要的区别：Hash 的元素没有特定的顺序。 如果顺序很重要的话就要使用数组了。

在类上调用的方法，如本例的 new，我们称之为类方法（class method）。在类上调用 new 得到的结果是这个类的一个对象，也叫做这个类的实例（instance）。在实例上调用的方法，例如 length，叫做实例方法（instance method）。

Rails 的一个约定：如果局部视图要在多个控制器中使用，则把它存放在专门的 shared 目录下。

pluralize 方法的第一个参数是整数，返回值是这个数字和第二个参数文本组合在一起正确的单复数形式。pluralize 方法是由功能强大的转置器（inflector）实现的，转置器知道怎么处理大多数单词的单复数变换，甚至是一些不规则的变换方式。
