---
layout: post
title: 斯坦福：iPad和iPhone应用开发(iOS5)-[第6集] 多个MVC和延续符
---
如果前面的代码需要调用后面才声明的类，这个时候就需要使用类的前向引用。即在文件开头用@class关键字声明：

```c
@class ClassName;
```

它告诉编译器，有一个类命名为ClassName，然后向其保证，马上就会定义这个类，但是现在暂时还不对其定义。

segue是一个MVC跳转到另一个MVC的东西，它的作用是push，即把新的MVC推送道屏幕上，另一个则滑出屏幕。

双击storyboard的背景，它会缩小来显示更多内容。

在iOS5才有storyboard，所以iOS4是不兼容segue的。

@property用来定义一个类的属性。
@synthesize表示由编译器来自动实现属性的getter/setter方法，不需要你自己再手动去实现。在iOS6中@synthesize也可以不写了。
