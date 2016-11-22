---
layout: post
title: Ruby on Rails thinking-sphinx MySQL Error
category: tech
---
在使用`gem thinking-sphinx`的时候会遇到

```
Can't connect to MySQL server on '127.0.0.1' (61)
```

这个其实是本地sphinx服务没有启动，运行一下

{% highlight ruby %}
rake ts:rebuild
{% endhighlight %}

这个命令让sphinx重新建立索引并且启动服务，很弱智的问题哈哈。

注意: 

{% highlight ruby %}
rake ts:index  
{% endhighlight %}

只会建立索引，不会启动服务。
