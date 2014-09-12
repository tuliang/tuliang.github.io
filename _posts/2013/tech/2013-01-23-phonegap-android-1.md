---
layout: post
title: PhoneGap-Android开发环境搭建1-安装JDK
category: tech
---
PhoneGap的资料比较乱，大多做法已经过期。本方法是综合众多文章和解决方案后，实际可行的。

JDK下载地址：<a href="http://www.oracle.com/technetwork/java/javase/downloads/jdk7-downloads-1880260.html" target="_blank">http://www.oracle.com/technetwork/java/javase/downloads/jdk7-downloads-1880260.html</a>

<img class="alignnone size-full wp-image-2229" alt="1.1" src="/images/2013/01/1.1.png" width="550" height="148" />

选中Accept License Agreement后
<img class="alignnone size-full wp-image-2230" alt="1.2" src="/images/2013/01/1.2.png" width="557" height="60" />

选择下载32位（x86）或者64位（x64）

下载完毕后，点击安装，一直下一步即可。

安装完毕后，我们需要开始配置环境变量

我的电脑->属性->高级->环境变量->系统变量中添加以下环境变量：
在系统变量中增加JAVA_HOME和CLASSPATH
JAVA_HOME值为（刚才安装JDK的目录）：

```
C:\Program Files\Java\jdk1.7.0_11
```

CLASSPATH值为：

```
.;%JAVA_HOME%\lib\tools.jar;%JAVA_HOME%\lib\dt.jar;%JAVA_HOME%\bin;
```

并且修改系统变量中的Path，在Path值的最前面加上：

```
%JAVA_HOME%\bin;
```

然后重启计算机，重启后打开cmd，敲入命令

```
java -version
```

如果输出类似下面的信息就表示JDK安装成功
<img class="alignnone size-full wp-image-2231" alt="1.3" src="/images/2013/01/1.3.png" width="507" height="50" />
