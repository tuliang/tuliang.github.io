---
layout: post
title: Ruby on Rails 打开gzip服务
category: tech
---

打开根目录下面的`config.ru`，在项目启动`run App::Application`的前面加上

{% highlight ruby %}
use Rack::Deflater
{% endhighlight %}

添加后，代码如下

{% highlight ruby %}
# This file is used by Rack-based servers to start the application.
 
require ::File.expand_path('../config/environment',  __FILE__)
use Rack::Deflater
run App::Application
{% endhighlight %}

然后打开`config/environments/production.rb`，在文件中加入一行代码：

{% highlight ruby %}
config.static_cache_control = "public, max-age=3600"
{% endhighlight %}

最后重启服务器即可，如果重启后还是没有打开gzip，很可能是你的服务器（Apache、Nginx）没有开启Gzip。