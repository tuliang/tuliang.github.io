---
layout: post
title: ruby synchronized
category: tech
---
最近学习 Java 的时候了解到在 Java 中 synchronized 关键字可以保证代码块的串行执行。

在 ruby 开发中往往使用第三方来保证，比如使用数据库或文件系统。其实 ruby 也有类似的方式来保证代码块的串行执行，它就是 Mutex 的 synchronize。

{% highlight ruby %}
require 'thread'
semaphore = Mutex.new

a = Thread.new {
  semaphore.synchronize {
    # access shared resource
  }
}

b = Thread.new {
  semaphore.synchronize {
    # access shared resource
  }
}
{% endhighlight %}