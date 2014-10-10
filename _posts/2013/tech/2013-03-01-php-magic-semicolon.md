---
layout: post
title: PHP神奇的分号
category: tech
---
今天在开发过程中，遇到两种分号的神奇问题，特此记录。

{% highlight php %}
<?php
echo '我是正常的分号';
echo '我是神奇的分号';
?>
{% endhighlight %}

如果你使用win平台，上面两条语句都可以运行。但是如果你是unix或是linux则是语法错误。

用肉眼无法分辨两种分号的区别，并且代码在win平台可以运行，而在unix或是linux则是语法错误。根本原因是两种分号不同，win同时支持这两种分号，而unix或是linux只支持其中一种。这个现象和字母的大小写很类似，win不区分大小写，而unix或是linux区分大小写。

使用下面这段代码就可以证明我们的猜想：

{% highlight php %}
<?php
if (';' == ';'){
  echo '相等';
} else {
  echo '不相等';
}
?>
{% endhighlight %}