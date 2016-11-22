---
layout: post
title: 斯坦福《iPad和iPhone应用开发(iOS5)》
category: open
---
<img class="cover" alt="201205231357294b512" src="/images/2013/01/201205231357294b512.jpg" width="120" height="90" />

讲师介绍

讲师: Paul Hegarty

介绍: 斯坦福大学软件工程学教授，主要教授iOS应用的开发、编程。

课程介绍

最新更新课程，适用于iOS 5。本课程介绍了使用iPhone SDK(软件开发包)建造iPhone平台上的应用程序所需的工具和应用程序接口；使用多点触控技术，为手机等终端设计用户互交界面等技术进行面向对象的设计。其他主题包括: 内核动画、bonjour网络、移动终端电量管理和性能测评。

预备知识: 抽象编程水平的C语言和编程经验。

[第 1 课 MVC 和 Objective-C 介绍](#mvc--objective-c-)

[第 2 课 我的第 一个苹果操作系统iOS](#ios)

[第 3 课 Objective-C](#objective-c)

[第 4 课 视图](#section-1)

[第 5 课 协议与手势](#section-2)

[第 6 课 多个MVC和延续符](#mvc)

[第 7 课 iPad+Apps](#ipadapps)

[第 8 课 视图控制器生命周期-图象视图、滚动视图、网络视图](#section-3)

[第 9 课 Table Views](#table-views)

[第 10 课 数据块和多线程](#section-4)

## 笔记

---

### 第 1 课 MVC 和 Objective-C 介绍

你会在本课程上学习数据库（databases），计算机网络设计（networking），多媒体程式设计（multimedia programming），多线程（multithreading），动画（animation）。

iOS是基于unix的系统。

iOS可以分为下面4层: 

* Cocoa Touch
* Media
* Core Services
* Core OS

iPad和iPhone应用大部分是在Cocoa Touch这一层上进行开发的。

Objective-C中的实现文件是m后缀名的文件。

---

### 第 2 课 我的第一个苹果操作系统iOS

storyboard是iOS5新增的功能，它的基本功能允许你同时在屏幕上显示所有MVC的关系。使用它，你能够看到MVC是怎么交互作用的。

自动引用记数，Automatic Reference Counting (ARC)。它是iOS5中新特性，用于自动内存管理。

NSLog是格式化输出。例如

{% highlight c %}
NSLog(@"digit pressed = %@", digit);
{% endhighlight %}

在上述代码中，digit变量的值会在%@所在的位置输出。

---

### 第 3 课 Objective-C

类名称（Class Name），结构体（structs）、枚举类型（enumerated types）使用大写，其他不要用大写。

指针的强弱是用于表示指向对象的指针，而用于指向存储器的指针在iOS中几乎不用它。

强指针（strong）是指将所要做的事情通过指针被保持在堆中，而不把它分配道存储器。

弱指针（weak）的意思是只要有人，至少一个人用强指针指向它，就把这个存储内容保存在堆内。如果没别人指着它，并且你要把它扔出堆外，则把我的指向它的指针设为零。弱指针只在iOS5中应用程序运行时起作用。在iOS4中不能用弱指针，你只能用强指针，然后你还要亲自把它们归零。

大写的BOOL和小写的bool是一样的，一般使用大写的。

---

### 第 4 课 视图

在Oc中，方法分为类方法和实例方法。

前置加号（+）的方法为类方法，这类方法是可以直接用类名来调用的，它的作用主要是创建一个实例。有人把它称为创建实例的工厂方法。

前置减号（-）的方法为实例方法，必须使用类的实例才可以调用的。

---

### 第 5 课 协议与手势

iOS中的协议最重要的两个用处是委托（delegates）和数据源（data sources）。

{% highlight c %}
#define PI 3.14
{% endhighlight %}

`#define`关键字用来设定常量。例如设定常量PI的值为3.14: 

shouldAutorotateToInterfaceOrientation在iOS6中被弃用了，现在iOS6默认允许屏幕旋转。

按住Option键移动鼠标可以模拟两指手势，如果键盘上没有Option键，则可以使用Alt键。

---

### 第 6 课 多个MVC和延续符

如果前面的代码需要调用后面才声明的类，这个时候就需要使用类的前向引用。即在文件开头用@class关键字声明: 

{% highlight c %}
@class ClassName;
{% endhighlight %}

它告诉编译器，有一个类命名为ClassName，然后向其保证，马上就会定义这个类，但是现在暂时还不对其定义。

segue是一个MVC跳转到另一个MVC的东西，它的作用是push，即把新的MVC推送道屏幕上，另一个则滑出屏幕。

双击storyboard的背景，它会缩小来显示更多内容。

在iOS5才有storyboard，所以iOS4是不兼容segue的。

@property用来定义一个类的属性。
@synthesize表示由编译器来自动实现属性的getter/setter方法，不需要你自己再手动去实现。在iOS6中@synthesize也可以不写了。

---

### 第 7 课 iPad+Apps

iPad上有两大独有的用户界面元素，一个是分屏视图，另一个是弹出窗口。

iOS5使用springs and struts模式来布局，iOS6则默认使用自动布局。取消选择“Use Autolayout”复选框，就可以使用旧版本的 springs and struts 模式。如果布局比较复杂，建议使用自动布局，不过使用自动布局的程序将不兼容iOS5。

---

### 第 8 课 视图控制器生命周期-图象视图、滚动视图、网络视图

覆盖指定初始化里的事项，大部分在viewDidLoad完成。

ViewWillAppear适合做两件事，就是最后一刻推迟等待进行一些消耗资源的事情和涉及几何特性的事情。

UIWebView是一个完整的网络浏览器，在Safari中可以进行的所有操作都可以在此视图中实现。它基于Webkit这个平台创建，一个开源的HTML渲染框架。它支持JavaScript，虽然只能运行5秒钟，所以无法锁定住手机。运行某些JavaScript无限循环，它只允许JavaScript分配10M内存，所以不会占用全部的手机内存。这个限制使HTML5+JavaScript实现的游戏在iOS平台上前景黯淡。

UIWebView非常有用，不仅可充当网页浏览器，还可以显示特定类型数据，比如PDF。就像你用Safari打开一个PDF一样，记住UIWebView其实就是一个Safari浏览器。

Transform是一种仿射变换，基本上就是缩放、平移和旋转。

---

### 第 9 课 Table Views

Table Views是iOS中显示列表的视图，它有四种基本的单元格类型，还可以自定义单元格。第一种是Subtitle，它是粗体显示，底下带一行灰色副标题。Basic类型下方则没有东西。Right Detail和Subtitle一样，只是里面的内容安放方式不一样，它是蓝色字体，在右边而不是显示在下方。Left Detail也一样，不过方向对调了。

---

### 第 10 课 数据块和多线程

在iOS里面使用block来操作多线程。

JCD不是标准的C，它是一个用于多线程的苹果机制。