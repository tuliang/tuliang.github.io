---
layout: post
title: PhoneGap-Android开发环境搭建3-使用PhoneGap开发安卓应用
category: tech
---
PhoneGap下载地址：<a href="http://phonegap.com/download/" target="_blank">http://phonegap.com/download/</a>

<a href="/images/2013/01/3.1.png"><img class="alignnone size-full wp-image-2247" alt="3.1" src="/images/2013/01/3.1.png" width="261" height="149" /></a>

下载到本地后，解压，然后打开lib下面的android文件夹

<a href="/images/2013/01/3.2.png"><img class="alignnone size-full wp-image-2248" alt="3.2" src="/images/2013/01/3.2.png" width="626" height="301" /></a>

打开之前创建的Android 项目

新建两个文件夹/libs 和 /assets/www（可能libs已经有了）
将cordova-2.3.0.js复制到目录/assets/www下
将cordova-2.3.0.jar复制到目录/libs下
将xml整个文件夹复制到目录/res下。

在/assets/www下建立index.html文件，代码如下

```html
<!DOCTYPE HTML>
<html>
    <head >
        <title> PhoneGap</title >
        <script type="text/javascript" charset="utf-8" src="cordova-2.3.0.js" ></script>
    </head >
    <body >
        <h1> Hello PhoneGap</h1 >
    </body >

</html>
```

对文档AndroiMainifest.xml进行修改
<a href="/images/2013/01/3.3.png"><img class="alignnone size-full wp-image-2249" alt="3.3" src="/images/2013/01/3.3.png" width="212" height="255" /></a>

将以下代码放到uses-sdk 和 application之间

```xml
<supports-screens
        android:largeScreens="true"
        android:normalScreens="true"
        android:smallScreens="true"
        android:resizeable="true"
        android:anyDensity="true"/>
    <uses-permission android:name="android.permission.CAMERA" />
    <uses-permission android:name="android.permission.VIBRATE" />
    <uses-permission android:name="android.permission.ACCESS_COARSE_LOCATION" />
    <uses-permission android:name="android.permission.ACCESS_FINE_LOCATION" />
    <uses-permission android:name="android.permission.ACCESS_LOCATION_EXTRA_COMMANDS" />
    <uses-permission android:name="android.permission.INTERNET" />
    <uses-permission android:name="android.permission.RECEIVE_SMS" />
    <uses-permission android:name="android.permission.RECORD_AUDIO" />
    <uses-permission android:name="android.permission.RECORD_VIDEO"/>
    <uses-permission android:name="android.permission.MODIFY_AUDIO_SETTINGS" />
    <uses-permission android:name="android.permission.READ_CONTACTS" />
    <uses-permission android:name="android.permission.WRITE_CONTACTS" />  
    <uses-permission android:name="android.permission.WRITE_EXTERNAL_STORAGE" />  
    <uses-permission android:name="android.permission.ACCESS_NETWORK_STATE" />
    <uses-permission android:name="android.permission.GET_ACCOUNTS" />
    <uses-permission android:name="android.permission.BROADCAST_STICKY" />
```

在activity标签中添加：

```xml
android:configChanges="orientation|keyboardHidden"
```

修改完后，文件应该是这样的
<a href="/images/2013/01/3.4.png"><img class="alignnone size-large wp-image-2250" alt="3.4" src="/images/2013/01/3.4-1024x486.png" width="625" height="296" /></a>

在libs目录的cordova-2.3.0.jar上点击右键，选择 Build Path->Add to Build Path

最后再修改下src下的Java主文件

<a href="/images/2013/01/3.5.png"><img class="alignnone size-full wp-image-2251" alt="3.5" src="/images/2013/01/3.5.png" width="197" height="325" /></a>

注释import android.app.Activity;
添加import org.apache.cordova.*;
将MainActivity的父类修改为DroidGap
将onCreate方法改为public
将onCreate方法中的setContentView(R.layout.activity_main);
改为super.loadUrl("file:///android_asset/www/index.html");

修改后的代码看上去应该是这样的
<a href="/images/2013/01/3.6.png"><img src="/images/2013/01/3.6.png" alt="3.6" width="655" height="458" class="alignnone size-full wp-image-2252" /></a>

到此为止，我们就完成了
<a href="/images/2013/01/3.7.png"><img src="/images/2013/01/3.7.png" alt="3.7" width="718" height="829" class="alignnone size-full wp-image-2253" /></a>
