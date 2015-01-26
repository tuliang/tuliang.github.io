---
layout: post
title: 基于 MVC 的 JavaScript Web 富应用开发
category: read
---
<img class="cover" src="/images/2015/9787121109560.jpg" />

原作名：JavaScript Web Applications

ISBN：9787121109560

作者：麦卡劳(Alex MacCaw)   

译者：李晶 / 张散集   

出版社：电子工业出版社

出版时间：2012-5

评价：☆☆☆☆

第 9 章有部分页面错位，阅读的时候要注意（2012年5月 第一版）。本书提到的一些库和后面三章讲的 Spine 、Backbone 和 JavaScriptMVC 有一定程度的落伍，简略的看一下就好了，毕竟是2011年写的书。

jQuery 的作者 John Resig 在博客中讲解如果实现经典的类继承：http://ejohn.org/blog/simple-javascript-inheritance/

事件捕捉，从顶层的父节点开始触发事件，从外到内传播。事件冒泡，从最内层的节点开始触发事件，逐级冒泡知道顶层节点，从内向外传播。你可以自行选择要注册的事件处理程序的调用类型，捕捉或冒泡，通过给 addEventListener() 传人第三个参数 useCapture 来设置。如果是 true，事件处理程序以捕捉方式触发；如果是 false，事件处理程序以冒泡模式触发。

发布 / 订阅（Pub / Sub）是一种消息模式，它有两个参与者：发布者和订阅者。发布者向某个信道（channel）发布一条消息，订阅者绑定这个信道，当有消息发布至信道时就会接收到一个通知。最重要的一点是，发布者和订阅者是完全解耦的，彼此并不知晓对方的存在。两者仅仅共享一个信道名称。

Peter Michaux 的博客，其中有一个关于命名空间专题的文章（http://goo.gl/FOnPL），非常不错。

Douglas Crockford 的文章《原型继承》（http://goo.gl/OLQhp）。

Robert Kieffer 写了一个简单明了的 GUID 生成器，它使用 Math.random() 来产生一个伪随机数的 GUID （http://goo.gl/0b0hu）。

JSONP（JSON with padding）（http://goo.gl/cqDT6）很早之前就被标准化了，甚至在 CORS 之前。这是另一种从远程服务器端抓取数据的方式。原理是通过创建一个 script 标签，所辖的外部文件包含一段 JSON 数据，数据是由服务器所返回的，作为参数包装在一个函数调用中。script 标签获取脚本文件并不受跨域的限制，所有浏览器都支持这种技术。

减少安全隐患的方法，列出可以访问你的数据的域名白名单，或只使用开发认证（OAuth）的身份识别验证。

在 IE 中，使用 Firebug Lite 进行调试会非常方便。Firebug Lite 不需要安装，只需要在页面中引入一个 script 标签即可。

ETag 通常是使用服务器指定的一些属性来构建的——也就是说，两个独立的服务器对同样的资源生成的 ETag 可能不一样——随着服务器集群越来越普遍，这成为一个现实的问题。