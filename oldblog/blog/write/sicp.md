---
layout: post
title: 计算机程序的构造和解释
category: read
---
<img class="cover" src="/images/2014/10/9787111135104.jpg" />

ISBN: 9787111135104

作者: Harold Abelson / Gerald Jay Sussman / Julie Sussman

译者: 裘宗燕

出版社: 机械工业出版社

出版时间: 2004.2
 
一个强有力的程序设计语言，不仅是一种指挥计算机执行任务的方式，它还应该成为一种框架，使我们能够在其中组织自己有关计算过程的思想。这样，当我们描述一个语言时，就需要将注意力特别放在这一语言所提供的，能够将简单的认识组合起来形成更复杂认识的方法方面。每一种强有力的语言都为此提供了三种机制: 

  1. 基本表达形式，用于表示语言所关心的最简单的个体。
  2. 组合的方法，通过它们可以从比较简单的东西出发构造出复合的元素。
  3. 抽象的方法，通过它们可以为复合对象命名，并将它们当作单元去操作。

在程序设计中，我们需要处理两类要素: 过程和数据（它们实际上并不是这样严格分离的）。非形式地说，数据是一种我们希望去操作的“东西”，而过程就是有关操作这些数据的规则的描述。这样，任何强有力的程序设计语言都必须能表述基本的数据和基本的过程，还需要提供对过程和数据进行组合和抽象的方法。

将运算符放在所有运算对象左边，这种形式称为前缀表示。刚开始看到这种表示时会感到有些不习惯，因为它与常规数学表示差别很大。然而前缀表示也有一些优点，其中之一就是它完全适用于可能带有任何实参的过程，例如下面实例中的情况: 

{% highlight lisp %}
(+ 21 35 12 7)
=> 75
(* 25 4 12)
=> 1200
{% endhighlight %}

一般而言，我们应该把递归看做一种处理层次性结构的（像树这样的对象）极强有力的技术。事实上，“值向上穿行”形式的求值形式是一类更一般计算过程的一个例子，这种计算过程称为树形积累。

过程定义（函数）的一般形式是: 

{% highlight lisp %}
(define (<name> <formal parameters>) <body>)
{% endhighlight %}

实例: 

{% highlight lisp %}
(define (square x) (* x x))

(square 3)
=> 9
(square (+ 2 5))
=> 49
(square (square 3))
=> 81
{% endhighlight %}

在 Lisp 里 cond（表示“条件”，即 switch），其使用形式如下（获得一个数的绝对值）: 

{% highlight lisp %}
(define (absolute x)
  (cond ((> x 0) x)
        ((= x 0) 0)
        ((< x 0) (- x))))
{% endhighlight %}

条件表达式的一般性形式为: 

{% highlight lisp %}
(cond (<p1> <e1>)
      (<p2> <e2>)
      (<p3> <e3>))
{% endhighlight %}

条件表达式的求值方式如下: 首先求值 p1，如果它的值是 false，那么就去求值 p2，直到发现了某个条件的值为真，这时解释器就返回相应子句中的序列表达式 e 的值（即每个序列表达式后默认有 break 的功能）。

用 if 来写绝对值函数: 

{% highlight lisp %}
(define (absolute x)
  (if (< x 0)
      (- x)
      x))
{% endhighlight %}      

if表达式的一般形式是: 

{% highlight lisp %}
(if <predicate> <consequent> <alternative>)
{% endhighlight %}

在求值一个 if 表达式时，解释器从求值 predicate 部分开始，如果 predicate 得到真值，解释器就去求值 consequent 并返回其值，否则它就去求值 alternative 并返回其值。

最常用的三个复合运算符是: 

{% highlight lisp %}
(and <e1> ... <en>)
(or <e1> ... <en>)
(not <e>)
{% endhighlight %}

作为使用这些逻辑复合运算符的例子，数 x 的值位于区间 5 < x < 10 之中的条件可以写为: 

{% highlight lisp %}
(and (> x 5) (< x 10))
{% endhighlight %}

作为另一个例子，下面定义了一个谓词，它检测某个数是否大于或者等于另一个数: 

{% highlight lisp %}
(define (>= x y)
  (or (> x y) (= x y)))
{% endhighlight %}

或者也可以定义为: 

{% highlight lisp %}
(define (>= x y)
  (not (< x y)))
{% endhighlight %}

练习 1.1 

{% highlight lisp %}
10
;=> 10

(+ 5 3 4)
;=> 12

(- 9 1)
;=> 8

(/ 6 2)
;=> 3

(+ (* 2 4) (- 4 6))
;=> 6

(define a 3)
;=> 

(define b (+ a 1))
;=> 

(+ a b (* a b))
;=> 19

(= a b)
;=> false

(if (and (> b a) (< b (* a b)))
    b
    a)
;=> 4   
    
(cond ((= a 4) 6)
      ((= b 4) (+ 6 7 a))
      (else 25))
;=> 16     

(+ 2 (if (> b a) b a))
;=> 6

(* (cond ((> a b) a)
         ((< a b) b)
         (else -1))
   (+ a 1))
;=> 16
{% endhighlight %}

练习 1.2

{% highlight lisp %}
(/ (+ 5 4 (- 2 (- 3 (+ 6 (/ 4 5)))))
   (* 3 (- 6 2) (- 2 7)))
;=> -0.246
{% endhighlight %}
