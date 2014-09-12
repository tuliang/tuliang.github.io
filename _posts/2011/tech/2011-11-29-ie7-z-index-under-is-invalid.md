---
layout: post
title: IE7下z-index无效
category: tech
---
IE7下有时候`z-index`无效，这时候就应该找该标签的父标签中谁使用了`position:relative`。
IE7中使用了`position:relative`后会清空子标签`z-index`。

解决方法：
在使用了`position:relative`的父标签中加上`z-index`，这时子标签的`z-index`也会起效。
