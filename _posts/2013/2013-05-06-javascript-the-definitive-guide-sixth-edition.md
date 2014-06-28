---
layout: post
title: JavaScript 权威指南（第 6 版）
---
<img src="/images/2013/05/9787111376613-228x300.jpg" alt="9787111376613" width="228" height="300" class="cover" />

原作名：JavaScript: The Definitive Guide, Sixth Edition

ISBN：9787111376613

作者： David Flanagan

译者：淘宝前端团队

出版社：机械工业出版社

出版时间：2012-4

评价：☆☆☆☆☆

本书很好，特别是在代码方面，注释很详细，代码很清晰。有很多技术细节，很多以前知其然不知其所以然的东西，现在能都了解到。淘宝前端团队翻译有些生硬。不过介于他们不是专业翻译还是不妄求更多了，能把意思翻译到了我就满足了。

以前大多数情况是使用alert()来输出的，我想大部分人也是同样。其实我们可以通过使用console.log()来向控制台输出消息。这样我们能够在控制台中看到输出，alert()在很多情况下是很麻烦和会产生神奇的问题的。

JS很多地方都可以不写表示语句结束的分号，但是我觉得还是都写上分号比较好。例如：

```javascript
var y = x + f
(a +b).toString()
```

在将分号省略掉后，JS会将代码看成是：

```javascript
var y = x + f(a +b).toString();
```

而代码的本意明显不是这样。又例如：

```javascript
return
ture
```

JS会将上面的代码解析为：

```javascript
return;
ture;
```

我们可以发现，如果为了省略分号，往往会出现很多错误。在实际编程中就会变成神奇的现象，往往你调试很久都不会发现这个原因。

JS中的数字具有很高的精度，但事实上还是会出现一些问题：

```javascript
var x = 0.3 - 0.2;
var y = 0.2 - 0.1;
```

在这里x不等于0.1，而y等于0.1。实际运行中，我们可以发现x的值是0.09999999999999998。

```javascript
var s = "hello world";
var len = s.length;
```

字符串既然不是对象，为什么它会有属性呢？只要引用了字符串s的属性，JS就会将字符串通过调用new String(s)的方式转换成对象。一旦属性引用结束，这个临时对象就会被销毁。下面的例子可以说明这个问题：

```javascript
var s = "hello world";
s.len = 20;
var t = s.len;
console.log(t);
```

变量t的值为undefined，并且在JS中数字和布尔值也同样有这个问题。

JS使用了函数作用域，变量在声明它们的函数体以及这个函数体嵌套的任意函数体内都是有定义的。到底是什么意思呢？我们来看下面这段代码：(更为详细的说明见：<a href="/images/2012/10/17/js-bianliang-shengmingtiqian.html" target="_blank">JS变量声明提前</a>)

```javascript
var scope = 'global';
function f(){
     console.log(scope);
     var scope = 'local';
     console.log(scope);
}
f();
```

你可能认为输出是：

```javascript
global
local
```

但是运行一下你就会发现实际结果是：

```javascript
undefined
local
```

照成这种结果的原因的就是前面提到的函数作用域，在JS中上面的代码实际上是这样的：

```javascript
var scope = 'global';
function f(){
     var scope;
     console.log(scope);
     var scope = 'local';
     console.log(scope);
}
f();
```

JS这个特性被非正式地称为声明提前，即JS函数里声明的所有变量都被提前至函数体的顶部，但是这个声明提前至声明却不赋值。由于JS拥有这种特性，在编写JS代码时一些程序员特意将变量声明放在函数体的顶部，而不是像其他语言中让变量声明和使用变量的代码尽量靠近。所以在函数体中使用到var来声明变量时，记得将声明和赋值语句放在函数体的顶部，避免因为这种特性造成变量值为undefined的BUG。

在JS中break和continue是可以使用标签语句的，标签语句最常用于循环体内部：

```javascript
mainloop: while(token != null){
    //运行到这里，会跳转到mainloop标签所在的那个地方
    continue mainloop;
}
```

通过原型继承创建一个新对象：

```javascript
//inherit() 返回了一个继承自原型对象p的属性的新对象
//这里使用ECMAScript5中的Object.create()函数（如果存在的话）
//如果不存在Object.create()，则退化使用其他方法
function inherit(p){
     if(p == null){//p是一个对象，但不能是null
          throw TypeError();
    }

     if(Object.create){//如果Object.create()存在
          return Object.create(p);//直接使用它
     }

     //否则进行进一步检测
     var t = typeof p;
     if(t !== "Object" && t !== "function"){
          throw TypeError();
     }
     function f(){};//定义一个空构造函数
     f.prototype = p;//将其原型属性设为p
     return new f();//使用f()创建p的继承对象
}
```

实参对象arguments有一个重要的用处，就是让函数可以操作任意数量的实参，例如下面的代码就是查找多个实参中最大的值：

```javascript
function max(){
     var max = 0;
     //遍历实参，查找并得到最大值
     for(var i = 0; i < arguments.length; i++){
          if(arguments[i] > max){
               max = arguments[i];
          }
     }
     return max;
}
var val = max(1, 999, 555, 666);
console.log(val);//输出999
```


JS的闭包特性原理就是将作用域链作为对象保存了起来，例如下列代码：

```javascript
var scope = 'global';
function checkscope(){
     var scope = 'local';
     function f(){ return scope; }
     return f();
}
checkscope();
```

执行结果是local，将代码修改成：

```javascript
var scope = 'global';
function checkscope(){
     var scope = 'local';
     function f(){ return scope; }
     return f;
}
checkscope()();
```

结果还是local，这是因为JS将checkscope的作用域链保存了下来，而不像其他语言返回后就将作用域销毁或者回收。

ECMAScript5中可以使用Array.isArray()函数来判断是否为数组。ECMAScript3则需要自己来实现这个函数：

```javascript
var isArray = Function.isArray || function(o){
     return typeof o === "object" &&
     Object.prototype.toString.call(o) === "[object Array]";
}
```

String对象常用的4种使用正则表达式的方法：

```javascript
search
replace
match
split
```

如果需要运行时动态创建正则表达式，需要使用RegExp对象。eval方法也可以实现，但是不建议使用。


勘错：
P10    
x > y    // => false：大于等于
应为：
x > y    // => false：大于

P11
return Math.sprt(a * a +    // 勾股定理 
我们称为b * b);    
应为：

return Math.sprt(a * a +  b * b);    // 我们称为勾股定理  

P113
本节讨论剩余的三种JavaScript语句——width、debugger和use strict
应为：
本节讨论剩余的三种JavaScript语句——with、debugger和use strict
