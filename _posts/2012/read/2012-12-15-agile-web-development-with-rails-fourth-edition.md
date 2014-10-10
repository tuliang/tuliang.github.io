---
layout: post
title: Web开发敏捷之道：应用Rails进行敏捷Web开发
category: read
---
<img class="cover" alt="9787111374046" src="/images/2012/12/9787111374046-232x300.jpg" width="232" height="300" />

原作名：Agile Web Development with Rails, Fourth Edition

ISBN：9787111374046

作者：Sam Ruby / Dave Thomas / David Heineme Hansson

译者：慕尼黑Isar工作组 / 骆古道

出版社：机械工业出版社

出版时间：2012-3

评价：☆☆☆☆

生成控制器和该控制器的动作名称

{% highlight ruby %}
rails generate controller Say hello goodbye
{% endhighlight %}

上述代码生成名为Say的控制器，以及该控制器下的两个动作：hello和goodbye。

我们想要用到POST，就意味着需要使用button_to，而不是link_to

rake doc:app用来生成文档
rake stats可以统计你编写的代码

Rails的Active Record模块，它定义了20个回调方法。有了这些回调，可以完成复杂有效性验证，甚至可以阻止完成某些操作，事务功能非常强大。

{% highlight ruby %}
def show
  respond_to do |format|
    format.html
    format.xml { render :xml => @product.to_xml }
    format.yaml { render :text=> @product.to_yaml }
  end
end
{% endhighlight %}

对于/show/1或者/show/1.html的请求将返回HTML的内容；
/show/1.xml将返回XML；/show/1.yaml将返回YAML。
也可以使用HTTP请求参数的方式进行格式传递，例如：
/show/1?format=xml

debug函数可以在视图中将数据显示出来

rails提供了三种缓存途径：页面缓存（page caching）、行为缓存（action caching）、以及片段缓存（fragment caching）。

页面缓存就是一般的缓存方式不必多说。行为缓存虽然缓存了页面，但是必要的权限判断之类的过滤器依然会执行。而片段缓存则可以让页面中一部分缓存，而另一部分不缓存（使用cache方法）。

学习Rails大部分时间不是学习语法和技巧，而且学习Rails开发的方式。Linux、Git、增量开发、测试驱动开发、敏捷开发，最重要的是“不要重复你自己(Don’t Repeat Yourself, 或DRY)”和“惯例优于设置（Convention Over Configuration）”。
