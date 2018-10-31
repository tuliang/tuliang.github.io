---
layout: post
title: HTML5揭秘
category: read
---
<img src="/images/2012/11/9787121124082-228x300.jpg" alt="HTML5揭秘" title="9787121124082" width="228" height="300" class="cover" />

ISBN: 9787121124082

作者:  Mark Pilgrim

译者: 常可 胡金埔 赵静

出版社: 电子工业出版社

出版时间: 2010-12

评价: ☆☆☆

不论是关于IMG标签的讨论还是W3C和WHAT小组的各种历史，证明了“在世界上交付出东西的人才是赢家。”

HTML5只是一些独立特性的集合，因此你不能检测浏览器是否支持“HTML5”，因为这没有意义。但是你可以分别检测浏览器是否支持诸如“画布”、“视频”、“地理位置”等HTML5特性。

不同浏览器的模式: 
Quirks模式
在Quirks模式模式中，浏览器违反了Web格式规范，以避免那些依照90年代末期的流行做法编写的网页不至于被呈现得无法阅读。

标准模式
在标准模式中，浏览器尽力尝试用符合标准规范的方式去渲染页面文档。HTML5里将这个模式称为“非Quirks模式”。

准标准模式
Firefox、Safari、Chrome、Opera(7.5+)、和IE8也具有被称为“准标准模式”的渲染模式，其中以传统方式实现了表格单元格的竖直尺寸，而没有严格遵循CSS2规范。HTML5里将这个模式称为“有限Quirks模式”。

现在HTML5视频方面实在太混乱了，为了兼容大部分浏览器，需要至少3个格式的视频。如果是IE9之前的版本，还要加上FALSH。

全书看下来，对HTML5有一定的认识了，这本书很适合拿来了解HTML5。可惜的是，本书是2010出版的，书上的很多东西都变了，而且作者貌似在网络上消失了，看来第二版基本没希望了。不过另一方面可喜的是，从2010到现在2012，2年多过去了，HTML5已经收到越来越多的支持，连Adobe都宣布放弃FLASH。HTML5的前景越来越清晰了，在未来，特别是移动端将会是HTML5的天下。

勘错: 

P63

该页面绘制箭头代码错误，正确的代码应为: 

{% highlight javascript %}
// 开始一个新路径
c.beginPath();
// x轴
c.moveTo(0, 40);
c.lineTo(240, 40);
c.moveTo(260, 40);
c.lineTo(500, 40);
// x轴箭头
c.moveTo(495, 35);
c.lineTo(500, 40);
c.moveTo(500, 40);
c.lineTo(495, 45);
// y轴
c.moveTo(60, 0);
c.lineTo(60, 153);
c.moveTo(60, 173);
c.lineTo(60, 375);
// y轴箭头
c.moveTo(60, 375);
c.lineTo(65, 370);
c.moveTo(60, 375);
c.lineTo(55, 370);
c.strokeStyle = "#000";
c.stroke();// 绘制
{% endhighlight %}

专家发言中:   
所胡HTML5浏览器中  
应为:   
所有HTML5浏览器中  
