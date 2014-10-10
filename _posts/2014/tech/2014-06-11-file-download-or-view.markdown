---
layout: post
title: Web文件下载和查看
category: tech
---
在浏览器中点击一个文件链接，会被浏览器直接打开或者下载。其实浏览器的行为是可以人为控制的，最简单的方法是使用HTML5 download Attribute。

{% highlight html %}
<!-- will download as "expenses.pdf" -->
<a href="/files/expenses.pdf" download="expenses.pdf">Download Your Expense Report</a>
{% endhighlight %}

这种方式虽然简单，但是兼容性不太好。查看[http://caniuse.com/download](http://caniuse.com/download)，我们可以发现IE和Safari全版本都不支持这个属性。

根本原因在HTTP Head中，文件类型由`Content-Type`控制。如果pdf文件是正确的`application/pdf`，浏览器会打开pdf，而不是去下载，jpg、png这些文件类型同理。

而下载是由`Content-Disposition`来控制的，例如：`Content-Disposition: attachment; filename="fname.txt"`。它的意思是将该文件作为附件，并且下载的文件名是fname.txt.

如果使用S3
访问文件的url，可以直接打开。
下载文件，使用AWS的api可以生成下载的url：

{% highlight ruby %}
url = object.url_for(:read, response_content_disposition: "attachment; filename=\"#{filename}\"")
{% endhighlight %}

相关文档：  
http://www.w3.org/Protocols/rfc2616/rfc2616-sec19.html
http://docs.aws.amazon.com/AWSRubySDK/latest/AWS/S3/S3Object.html
