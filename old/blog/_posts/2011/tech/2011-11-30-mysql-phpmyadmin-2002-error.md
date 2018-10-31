---
layout: post
title: MySQL phpmyadmin: #2002 问题
category: tech
---
在安装phpmyadmin的时候经常遇到: 

2002 – 服务器没有响应 (或者本地 MySQL 服务器的套接字没有正确配置)

要将 phpmyadmin的配置文件config.inc.php 中

{% highlight php %}
$cfg['Servers'][$i]['host'] = ’localhost’;
{% endhighlight %}

改成

{% highlight php %}
$cfg['Servers'][$i]['host'] = ’127.0.0.1′;
{% endhighlight %}

就可以连接了。

原因我寻找了一下，在phpmyadmin的<a href="http://wiki.phpmyadmin.net/pma/Config/Servers" target="_blank">官方文档</a>中有相关说明: 

>BEWARE, If you set this:
>
>{% highlight php %}
>$cfg['Servers'][$i]['host'] = 'localhost';
>{% endhighlight %}
>
>Then PhpMyAdmin will IGNORE your settings for: 'port', 'socket', and 'connect_type'. It will simply connect to the default socket.
>
>If your database is on the localhost, use the IP instead:
>
>{% highlight php %}
>$cfg['Servers'][$i]['host'] = '127.0.0.1';
>{% endhighlight %}
>
>Then 'port', 'socket', and 'connect_type' will work exactly as expected.