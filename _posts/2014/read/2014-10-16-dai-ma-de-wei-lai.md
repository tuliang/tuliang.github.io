---
layout: post
title: 代码的未来
category: read
---
<img class="cover" src="/images/2014/10/9787115317513.jpg" />

ISBN：9787115317513

作者：[日] 松本行弘 

译者：周自恒 

出版社：人民邮电出版社

出版时间：2013.6

摩尔定律的局限

* 光速
* 印刷时使用光的波长
* 保持绝缘，漏电流
* 发热，热密度
* 量子力学

巴拉姆效应是一种心理学现象，指的是将一些原本是放之四海而皆准、模凌两可的一般性描述往自己身上套，并认为这些描述对自己是准确的。

冷读术，就是通过观察对方言行举止中的一些细微之处来进行揣测的技巧。
热读术则是通过事先对对方进行详细的调查，来准确说出对方的情况。

“垃圾回收的统一理论”，书中阐述了一种理论，即：任何一种 GC 算法，都是跟踪回收和引用计数回收两种思路的组合。

通过 retry 可以在异常处理中实现重试的操作，非常方便。不过它也有一个缺点，那就是如果在 retry 之前没有仔细检查是否对产生异常的条件进行了充分应对的话，就很有可能陷入死循环。

对象是在数据中以方法的形式包含了过程，而闭包则是在过程中以环境的形式包含了数据。
例如，对 n 进行累加，并显示它的值。
用闭包：

{% highlight javascript %}
function extent(){
  var n = 0;
  return function(){
    n++;
    console.log("n="+n);
  }
}
f = extent(); 
f(); // n=1
f(); // n=2
{% endhighlight %}

用面向对象：

{% highlight javascript %}
function extent(){
  return {
    val: 0,
    call: function(){
    this.val++;
    console.log("val="+this.val);
  }}
}
f = extent(); 
f.call(); // val=1
f.call(); // val=2
{% endhighlight %}

Ruby 和 JavaScript 的行为是有很大差异的。

{% highlight %}
obj.m
{% endhighlight %}

在 Ruby 中，这行代码表示对 m 方法进行无参数调用，而在 JavaScript 中则表示返回实现 m 方法的函数对象，而如果要进行无参数调用的话，括号是不能省略的，如：

{% highlight %}
obj.m()
{% endhighlight %}

也就是说，JavaScript 中由圆点所引导的房屋代表对属性的引用，将函数作为属性值返回就是方法，而加上括号就可以对其进行调用。

另一方面，Ruby 中圆点所引导的访问只不过是对方法的调用而已，加不加括号，是不影响方法调用这一行为的。在 Ruby 中，如果要获取实现该方法的过程对象，则需要使用 method 方法。

{% highlight %}
obj.method(:m)
{% endhighlight %}

Python 也采用了和 JavaScript 相同的方法，如果对一种原本并非为面向对象设计的语言添加面向对象功能的话，这是一种十分有效的手法。
类似这样的设计思想的差异，在 Lisp 中早就存在，这两种做法分别叫做 Lisp-1（JavaScript风格）和 Lisp-2（Ruby风格）。
在 Lisp 方言中，Scheme 属于 Lisp-1，EmacsLisp 属于 Lisp-2。

像布隆过滤器这样“偶尔会出错”的算法，被称为概率算法（probabilistic algorithm）。