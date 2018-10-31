---
layout: post
title: 斯坦福《iPhone开发教程2010年冬》
category: open
---
课程介绍

如果你对iPhone Development有兴趣，以下是入门门槛供参考: 首先你要有一台Mac电脑（因为 iPhone App 使用 Mac 平台内建的 Xcode 开发工具），网上也有在Windows下搭设开发环境的教程，请大家自行GOOGLE一下,接著下载 iPhone SDK 安装，然后最基本的是你要熟悉C语言，再来你得学习开发iPhone所使用的Objective-C语言，接著是Cocoa。

[第 1 课 基础入门](#section-1)

[第 2 课 各种基础的类,功能,对象和实例的介绍](#section-2)

第 3 课 如何创建你自己的定制类

第 4 课 创建应用程序

第 5 课 文档资料以及调试

第 6 课 视图,绘画与动画

第 7 课 MVC及视图控制器

第 8 课 导航及标签栏控制器

第 9 课 滚轴视图和表格视图

第 10 课 iPhone应用程序的数据

第 11 课 性能及其优化

第 12 课 文本输入及模式地展现内容

第 13 课 Yelp的Monocle应用

第 14 课 Yelp的Monocle应用

第 15 课 iPad设计

第 16 课 地址薄

第 17 课 触摸及多点触摸技术

第 18 课 iPhone设备API-位置、加速度计以及摄像头；电源管理和电池寿命

第 19 课 Evernote软件及其经营理念

第 20 课 Bump

第 21 课 Audio.APIs,.Video.Playback,.Settings

第 22 课 Bonjour,.NSStream,.GameKit

第 23 课 Unit.Testing;.Fun.with.Objective-C;.Localization

第 24 课 Publishing.on.the.App.Store

第 25 课 OpenGL.ES.Basics

第 26 课 From.Student.to.Startup;.Lessons.from.a.CS193P.Alumnus

第 27 课 LinkedIn;.Important.Life.Lessons.on.CoreData.&.GameKit

第 28 课 Student.iPhone.App.Presentations

## 笔记

---

### 第 1 课 基础入门

教授提到会在课程中讲授一些设计模式。不会涉及数据库设计理论，不会涉及图形概念。

Tools

*  Xcode是开发环境，同时也是编辑器。
*  Interface Builder是建造用户界面的图形化工具。


Frameworks

*  Foundation（基础）是字符串，数组和类。
*  Ulkit框架，iPhone SDK的用户界面框架。可以提供按键和滑动界面等。


Language

*  Objective-C，一种严格的C扩展集，所有以C写的东西，都能在Objective-C里编译和运行，并增加了其他的扩展性。

---

### 第 2 课 各种基础的类,功能,对象和实例的介绍

你在Xcode的文本编辑器上工作时，遇到了一个API，想知道多一些相关的信息。你可以按下command键，然后双击那个API，它会带你到特定API的文档里。

Objective-C只支持单一继承。

Objective-C中有一个动态运行库，所以它比C++要更动态一些，可以算作动态语言。基本上，所有功能（method）的分派是懈怠的（done lazily）。功能并没有绑定编译时间。

Objective-C是弱类型的语言，同时它也是强类型，即两种类型它都支持。

id是一个隐形指针，它实际并不需要星号。如果你把星号放上去，这最后会变成一个指针指向一个指针。因此不要加星号，除非真的想要这样做。

Objective-C只提供了编译时类型检查，而不是运行时类型检查。在运行时，它不会验证你要发送的信息是否会到达你在编译时，想要到达的对象那里。在运行时是没有验证的，唯一的会验证的情况是，如果你发送信息到的对象并没有实现功能，这样会造成崩溃。所有的类型检查都在编译时完成。

Objective-C使用nil表示空值对象。

Objective-C使用description和NSLog来debug。