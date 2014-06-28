---
layout: post
title: PhoneGap-Android开发环境搭建2-配置安卓开发环境
---
安装好JDK后，开始安装安卓开发环境

安卓开发环境下载地址：<a href="http://developer.android.com/sdk/index.html" target="_blank">http://developer.android.com/sdk/index.html</a>
<a href="/images/2013/01/2.1.png"><img class="alignnone size-full wp-image-2238" alt="2.1" src="/images/2013/01/2.1.png" width="348" height="355" /></a>

点击下载后，将其解压到某个目录

然后我们继续修改环境变量，我的电脑->属性->高级->环境变量->系统变量中添加以下环境变量
在系统变量中增加PATH，PATH值为（刚才解压的目录）：

```
D:\adt-bundle-windows-x86_64\sdk\tools
```

修改完毕后，重启计算机。重启后打开cmd，敲入命令

```
android –h
```

如果输出类似下面的信息就表示安装成功

<img class="alignnone size-full wp-image-2239" alt="2.2" src="/images/2013/01/2.2.png" width="603" height="176" />

打开D:\adt-bundle-windows-x86_64\eclipse下面的eclipse.exe

<img class="alignnone size-full wp-image-2240" alt="2.3" src="/images/2013/01/2.3.png" width="207" height="115" />

点击Window，然后选择Preferences

<img class="alignnone size-full wp-image-2241" alt="2.4" src="/images/2013/01/2.4.png" width="707" height="555" />

点击Android并选择好安卓sdk的目录

最后我们需要创建AVD。（其实就是一个android模拟器，相当于一部虚拟的android手机）

选择Windows > Android Virtual Device Manager

点击左侧面板的Android Virtual Devices，再右侧点击New

<img class="alignnone size-full wp-image-2242" alt="2.5" src="/images/2013/01/2.5.png" width="418" height="583" />

填好后保存即可。

通过File -> New -> Project 菜单，建立新项目"Android"文件夹下的"Android Application Project"

项目文件创建好后，直接点击run按钮，一个hello world就完成了。
