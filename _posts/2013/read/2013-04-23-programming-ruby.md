---
layout: post
title: Programming Ruby中文版
category: read
---
<img class="cover" src="/images/2013/04/9787121038150.jpg" />

原作名：Programming Ruby

ISBN：9787121038150

作者：[美]DaveThomas

译者：孙勇 / 姚延栋 / 张海峰

出版社：电子工业出版社

出版时间：2007-3

评价：☆☆☆

大概看了十几个小时的样子，后面基本没看，急着搞rails开发，只对Ruby有些简单的了解就好，主要还是要看《Web开发敏捷之道：应用Rails进行敏捷Web开发》。

Ruby中单引号和双引号对字符串处理和PHP类似，单引号一般会直接输出引号中的字符串，而双引号会转义一些字符串，例如：/n；或者是内插表达式，例如：#{表达式}。

全局变量使用美元符号（$）为前缀，而实例变量以“at”（@）符号开始。类变量以两个“at”（@@）符号开始。

在其他语言中，nil或null的概念是指“没有对象”。在Ruby中，这是不一样的：nil是一个对象，与别的对象一样，只不过它是用来表示美元任何东西的对象。

Ruby是使用end关键字来表明程序体的结束，并不是像其他语言使用花括号。例如：

{% highlight ruby %}
while line = gets
    puts line.downcase
end
{% endhighlight %}

initialize方法是Ruby的构造函数。

Ruby中使用大括号（`<`）表示继承，例如：
`class KaraokeSong < Song`
表示类KaraokeSong是Song的子类。

用斐波那契数列的例子说明并行赋值：

{% highlight ruby %}
def fib_up_to(max)
  i1, i2 = 1, 1
  while i1 <= max
    yield i1
    i1, i2 = i2, i1 + i2 # 并行赋值 
    #将i2的值赋予给i1 在同时将i1+i2的值赋予给i2
   end
end

fib_up_to(1000) {|f| print f, " " }
{% endhighlight %}

Ruby中方法参数的括号是可选的，一般的惯例是，当方法有参数时则使用括号，否则即忽略它们。

你希望传入可变个数的参数，或者像用一个形参接收多个参数，在参数名前放置一个星号（*）即可。

每个被调用的方法都会返回一个值。方法的值，是在方法执行中最后一个语句执行的结果。return的返回值是其参数的值。如果不需要return就省略之，这是Ruby的惯用技法。（PS：这个特性可以让代码写得很简单，不过在同时，代码的理解难度提高了）

Ruby中a=a+2可以写成a+=2，但是Ruby不支持其他语言中的自加（++）和自减（--）运算符。

Ruby对真值的定义很简单：任何不适nil或者常量false的值都为真。然而数字0不被解释为假值，长度为0的字符串也不适假值。

switch在Ruby中被case替代，而case被then替代，default则被else替代，例如：

{% highlight ruby %}
case year
  when 1850..1889: "Blues"
  when 1890..1909: "Ragtime"
  when 1910..1929: "New Orleans Jazz"
  else
end
{% endhighlight %}
