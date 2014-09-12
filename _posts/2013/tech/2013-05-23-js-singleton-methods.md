---
layout: post
title: JavaScript单件方法
category: tech
---
最近在看《Ruby元编程》发觉动态语言的强大。同时越看越觉得Ruby和JavaScript在一些方面是非常像的，可以说它们有些原理是类似的，这些原因使它们很多时候编程方式可以互相借鉴。看到Ruby比较厉害的单件方法，我觉得使用JavaScript也是可以部分实现的。例如：

```javascript
str = function() {
  this.name = 'just a regular string';
  this.showName = function() {
    console.log(this);
  };
};

str1 = new str;
str2 = new str;
str1.showName();
str2.showName();

str1.setName = function(name) {
  this.name = name;
};

str1.setName('new Name');
str1.showName();
str2.showName();
```

运行结果：

<img src="/images/2013/05/20130523221959.png">


可以发现str1在中途添加了一个方法，并且这个方法只有它自己可以使用。使用这种方法来编写JavaScript，很多时候就会方便很多。
