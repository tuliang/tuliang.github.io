---
layout: post
title: 斯坦福：iPad和iPhone应用开发(iOS5)-[第8集] 视图控制器生命周期-图象视图、滚动视图、网络视图
---
覆盖指定初始化里的事项，大部分在viewDidLoad完成。

ViewWillAppear适合做两件事，就是最后一刻推迟等待进行一些消耗资源的事情和涉及几何特性的事情。

UIWebView是一个完整的网络浏览器，在Safari中可以进行的所有操作都可以在此视图中实现。它基于Webkit这个平台创建，一个开源的HTML渲染框架。它支持JavaScript，虽然只能运行5秒钟，所以无法锁定住手机。运行某些JavaScript无限循环，它只允许JavaScript分配10M内存，所以不会占用全部的手机内存。这个限制使HTML5+JavaScript实现的游戏在iOS平台上前景黯淡。

UIWebView非常有用，不仅可充当网页浏览器，还可以显示特定类型数据，比如PDF。就像你用Safari打开一个PDF一样，记住UIWebView其实就是一个Safari浏览器。

Transform是一种仿射变换，基本上就是缩放、平移和旋转。
