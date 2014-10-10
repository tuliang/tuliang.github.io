---
layout: post
title: 解决JS指向不明
category: tech
---
用面向对象的方式编写JS时，在类中经常会出现this指向不明的问题。

解决这个问题很简单，在对象中将this指定给一个变量，然后都使用这个对象就可以了。例如在类文件的最开始加上下述代码：

{% highlight javascript %}
var self = this;
{% endhighlight %}

这样在这个类中，self就指向了this，我们使用self这个变量，就可以不用担心this指向不明的问题了。
