---
layout: post
title: JavaScript语言精粹
---
<img class="cover" alt="9787121084379" src="/images/2013/05/9787121084379.jpg" width="200" height="260" />

原作名：JavaScript: The Good Parts

ISBN：9787121084379

作者：Douglas Crockford

译者：赵泽欣 / 鄢学鹍

出版社：电子工业出版社

出版时间：2009

评价：☆☆☆☆☆

本书作者是一位大师，有很多发明创造，例如现在广泛使用的JSON就是他创立的。这本书应该是你学习JavaScript的第二本书，在使用《JavaScript DOM编程艺术》入门之后。它可以让你知道什么是精华，什么是鸡肋。

优秀的代码成就优秀的程序员。大多数编程语言都有精华部分和鸡肋部分。我发现如果只使用精华部分而避免使用鸡肋的部分，我可以称为一个更好的程序员。

JavaScript的函数是（主要）基于语法作用域（lexical scoping）的顶级对象。JavaScript是第一个成为主流lambda语言。实际上，相对Java而言，JavaScript与Lisp和Scheme有更多的共同点。它是披着C外衣的Lisp。这使得JavaScript成为一个非常强大的语言。

避免使用/* */注释。在JavaScript中，这些字符可能出现在正则表达式中，所以块注释对于被注释的代码块来说是不安全的。例如：

```javascript
/*
var rm_a = /a*/.match(s);
*/
```

使用forin语句循环时，属性名出现的顺序是不确定的。如果你想要确保属性以特定的顺序出现，最好的办法就是完全避免使用for in语句，而是创建一个数组，在其中以正确的顺序包含属性名。

在JavaScript中函数就是对象。所以他们可以像任何其他的值一样被使用。函数可以存放在变量、对象和数组中。函数可以被当作参数传递给其他函数，函数也可以再返回函数。而且，因为函数是对象，所以函数可以拥有方法。

函数总是会返回一个值。如果没有指定返回值，则返回undefined。如果函数以在前面上new前缀的方式来调用，且返回值不是一个对象，则返回this（该新对象）。

JavaScript允许给语言的基本类型增加方法。举例来说，我们可以通过给Function.prototype增加方法来使得该方法对所有函数可用：

```javascript
Function.protoype.method = function (name, func) {
  this.prototype(name) = fund;
  return this;
};
```

通过给Function.protoype增加一个method方法，我们就不必键入prototype这个属性名。
通过给基本类型增加方法，我们可以大大提高语言的表现力。因为JavaScript原型继承的动态本质，新的方法立刻被赋予到所有的值（对象实例）上，哪怕值（对象实例）是在方法被创建之前就创建好了。

很多现代语言都推荐尽可能迟地声明变量。而用在JavaScript上的话却会成为糟糕的建议，因为它缺少块级作用域。所以，最好的做法是在函数体的顶部声明函数中可能用到的所有变量。

模块模式利用了函数作用域和闭包来创建绑定对象与私有成员的关联。模块模式的一般形式是：一个定义了私有变量和函数的函数；利用闭包创建可以访问私有变量和函数的特权函数；最后返回这个特权函数，或者把它们保存到一个可访问的地方。

使用模块模式就可以摒弃全局变量的使用。它促进了信息隐藏和其他优秀的设计实践。对与应用程序的封装，或者构造其他单例对象。假如我们想要构造一个用来产生序列号的对象：

```javascript
var serial_maker = function () {
  var prefix = '';
  var seq = 0;
  return {
    set_prefix: function (p) {
      prefix = String(p);
    },
    set_seq: function (s) {
      seq = s;
    },
    gensym: function () {
      var result = prefix + seq;
      seq += 1;
      return result;
    }
  };
};

var seqer = serial_maker();
seqer.set_prefix('Q');
seqer.set_seq(1000);
var unique = seqer.gensym();
```
