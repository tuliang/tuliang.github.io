---
layout: post
title: CSS无限延展在浏览器窗口缩小时会中断
category: tech
---
只要给它设定一个最小宽度（`min-width`）就行。造成这个问题的原因是浏览器在宽度（`width`）为100%或者auto时，之后延展到现有窗口宽度的大小，当移动滚动条时就会出现截断现象。
