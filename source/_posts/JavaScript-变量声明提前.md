---
title: JavaScript 变量声明提前
date: 2012-10-17 17:12:48
categories: 前端
tags:
  - JavaScript
---
`JavaScript` 使用了函数作用域，变量在声明它们的函数体以及这个函数体嵌套的任意函数体内都是有定义的。到底是什么意思呢？我们来看下面这段代码: 

```javascript
var scope = 'global';
function f(){
  console.log(scope);
  var scope = 'local';
  console.log(scope);
}
f();
```

你可能认为输出是: 
```
global  
local  
```

但是运行一下你就会发现实际结果是: 
```
undefined  
local  
```

深入研究你会发现就算是你使用传递参数: 

```javascript
var scope = 'global';
function f(scope){
  console.log(scope);
  var scope = 'local';
  console.log(scope);
}
f();
```

实际结果依然是:   
```
undefined  
local  
```

或者代码改写为: 

```javascript
var scope = 'global';
function f(){
  console.log(scope);
    return scope;
  var scope = 'local';
  console.log(scope);
}
f();
```

实际结果仍然是:   
```
undefined  
```

为什么，后面的代码能够影响到前面的代码？照成这种结果的原因的就是前面提到的函数作用域，在JS中上面的代码实际上是这样的: 

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

`JavaScript` 这个特性被非正式地称为声明提前，即函数里声明的所有变量都被提前至函数体的顶部，但是这个声明提前至声明却不赋值。
由于拥有这种特性，在编写代码时一些程序员特意将变量声明放在函数体的顶部，而不是像其他语言中让变量声明和使用变量的代码尽量靠近。
所以在函数体中使用到 `var` 来声明变量时，记得将声明和赋值语句放在函数体的顶部，避免因为这种特性造成变量值为 `undefined` 的 `BUG`。

