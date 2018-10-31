---
title: Web 文件下载和查看
date: 2014-06-11 18:48:43
categories: 网络
tags:
  - HTTP
  - HTML5
  - Ruby
---
在浏览器中点击一个文件链接，会被浏览器直接打开或者下载。
其实浏览器的行为是可以人为控制的，最简单的方法是使用 `HTML5 download Attribute`。

```html
<!-- will download as "expenses.pdf" -->
<a href="/files/expenses.pdf" download="expenses.pdf">Download Your Expense Report</a>
```

这种方式虽然简单，但是兼容性不太好。查看[http://caniuse.com/download](http://caniuse.com/download)，我们可以发现很多版本都不支持这个属性。

浏览器行为是由 `HTTP Head` 中的 `Content-Disposition` 来控制的，例如

```
Content-Disposition: attachment; filename="fname.txt"
```

它的意思是将该文件作为附件，并且下载的文件名是 `fname.txt`。

如果使用 `S3` 下载文件，使用 `AWS` 的 `api` 可以生成下载的 `url`:

```ruby
url = object.url_for(:read, response_content_disposition: "attachment; filename=\"#{filename}\"")
```

#### 参考文档
- http://www.w3.org/Protocols/rfc2616/rfc2616-sec19.html
- http://docs.aws.amazon.com/AWSRubySDK/latest/AWS/S3/S3Object.html
