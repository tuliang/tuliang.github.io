---
title: 解决 JavaScript 指向不明
date: 2012-12-23 22:33:02
categories: 前端
tags:
  - JavaScript
---
用面向对象的方式编写 `JavaScript` 时，在类中经常会出现 `this` 指向不明的问题。

解决这个问题很简单，在对象中将 `this` 指定给一个变量，然后都使用这个对象就可以了。

例如在类文件的最开始加上下述代码

```javascript
var self = this;
```

这样在这个类中，`self` 就指向了 `this`，我们使用 `self` 这个变量，就可以不用担心 `this` 指向不明的问题了。