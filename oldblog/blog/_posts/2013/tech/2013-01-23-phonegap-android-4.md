---
layout: post
title: PhoneGap-Android开发环境搭建4-代码打包生成APK
category: tech
---
工程上点右键 –> Export…
<a href="/images/2013/01/4.1.png"><img class="alignnone size-full wp-image-2257" alt="4.1" src="/images/2013/01/4.1.png" width="491" height="362" /></a>

选择Export Android Application，点击“Next”，让选择需要打包的工程，直接“Next”，到keystone页面
<a href="/images/2013/01/4.2.png"><img class="alignnone size-full wp-image-2258" alt="4.2" src="/images/2013/01/4.2.png" width="539" height="561" /></a>

选择”Create new keystore”，因为我们还没keystore。如果有，直接选择。

选择生成keystore后存放的位置，设置密码（这个密码很重要）。
补充说明一下keystore: 

keystore实际上是一个数字证书，用来对Android程序进行签名。如果有不知道数字证书的同学，<a href="http://baike.baidu.com/view/16501.htm" target="_blank">>>请到此查看相关资料</a>。
Android通过数字证书确定程序包的唯一性，与程序建立信任关系，在使用者的认可下使用预先申报的资源，这个数字证书并不需要权威的数字证书签名机构认证。
建议开发者使用同一个数字证书对你的作品进行签名，有如下好处: 
<ul>
	<li>有利于程序升级，当新版程序和旧版程序的数字证书相同时，Android系统才会认为这两个程序是同一个程序的不同版本。如果新版程序和旧版程序的数字证书不相同，则Android系统认为他们是不同的程序，并产生冲突，会要求新程序更改包名。</li>
	<li>有利于程序的模块化设计和开发。Android系统允许拥有同一个数字签名的程序运行在一个进程中，Android程序会将他们视为同一个程序。所以开发者可以将自己的程序分模块开发，而用户只需要在需要的时候下载适当的模块。</li>
	<li>可以通过权限(permission)的方式在多个程序间共享数据和代码。Android提供了基于数字证书的权限赋予机制，应用程序可以和其他的程序共享概功能或者数据给那那些与自己拥有相同数字证书的程序。如果某个权限(permission)的protectionLevel是signature，则这个权限就只能授予那些跟该权限所在的包拥有同一个数字证书的程序。</li>
</ul>

接下来填写证书信息: 
<a href="/images/2013/01/4.3.png"><img src="/images/2013/01/4.3.png" alt="4.3" width="532" height="556" class="alignnone size-full wp-image-2259" /></a>

根据自己的情况填写，点击“Next”，生成keystore，到下一页面: 
<a href="/images/2013/01/4.4.png"><img src="/images/2013/01/4.4.png" alt="4.4" width="532" height="557" class="alignnone size-full wp-image-2260" /></a>

选择APK文件生成的位置，点击Finish，完成。
把Demo.apk安装到手机上运行看是否正常运行。
