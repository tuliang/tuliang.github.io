---
layout: post
title: JavaScript异步编程
category: read
---
<img class="cover" src="/images/2013/12/9787115316578.jpg" />

原作名：Async JavaScript: Build More Responsive Apps with Less Code

ISBN：9787115316578

作者：Trevor Burnham  

译者：许青松 

出版社：人民邮电出版社

出版时间：2013-6

评价：☆☆☆☆

最近图灵喜欢出一些很薄很小的书，本书就是其中一例。不过，这个书虽小，但是已经将JavaScript异步编程方面讲了一遍。它可以解除你对JavaScript异步编程的一些误解，彻底了解它运行的机制，同时也给出了不少实际的解决方法。

“如果队列中至少有一个事件适合“触发”，则虚拟机会挑选一个事件，并调用此事件的处理器。事件处理器返回后，我们又回到队列处。”、“输入事件的工作方式完全一样：用户单击一个已附加单击事件处理器的DOM元素时，会有一个单击事件排入队列。但是，该单击事件处理器要等到当前所有正在运行的代码均以结束后才会执行。因此，使用JavaScript的那些网友一不小心就会变得毫无反应。”，这些都说明了一个问题：JavaScript是无阻塞的，事件执行并不确定。

看上去是很糟糕，不过这样可以避免cpu等待，提高了性能。node.js强大的性能，很大程度上就是因为这个无阻塞特性。 

面对JavaScript的无阻塞作者给出了不少解决方法，首先是使用on和trigger形成的观察者模式，然后讲解了级联技术：

级联技术非常有用，因为它让我们不费吹灰之力就能定义异步任务的分化逻辑。

{% highlight javascript %}
var step1 = $.post('/step1', data1);
var step2 = step1.pipe(function(){
  return $.post('/step2', data2);
});
var lastStep = step2.pipe(function(){
  return $.post('/step3', data3);
});
{% endhighlight %}

这里的lastStep对象当且仅当所有这3个Ajax调用都成功完成时才执行，其中任意一个Ajax调用未能完成，lastStep均被拒绝。

JavaScript是单线程的：“像setTimeout这样的异步函数只是简单地做延迟执行，而不是孵化新的线程。”

现在多核的情况越来越普遍，JavaScript当然想利用起来，然后我们看到了worker，但是它还比较简陋。

脚本加载：yepone是一个小巧而精干的工具，Require则是一个巨硕而强大的工具。最终选择哪个库完全取决于正在开发的应用类型和开发团队的类型。