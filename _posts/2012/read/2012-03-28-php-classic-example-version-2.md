---
layout: post
title: PHP经典实例（第2版）
category: read
---
<img class="cover" title="9787508386089" src="/images/2012/03/9787508386089-228x300.jpg" alt="PHP经典实例（第二版）" width="228" height="300" />

ISBN：9787508386089

作者：（美）斯克拉 / （美）切贝特伯格

译者：李松峰 / 秦绪文 / 李丽

出版社：中国电力出版社

出版时间：2009-10

评价：☆☆☆

这本书适合PHP入门后进阶学习使用，例子很多，拿来练手还行。
6.2 为函数的参数设定默认值

```php
function wrap_html_tag($srting, $tag = 'b'){
     return "<$tag>$string</$tag>";
}
```

在指定默认值时有两件事值得特别关注。

第一，所有指定了默认值的参数必须出现在未指定默认值参数后面。否则，PHP无法判定省略的哪个参数应该取得默认值，以及哪个变量需要覆盖默认值。所以，wrap_html_tag()不能定义成：

```php
function wrap_html_tag($tag = 'b', $srting){}
```

如果采取以上形式定义并给函数wrap_html_tag()只传递一个参数，PHP会将这个值指定给$tag，并发出缺少第二个参数的警告。

第二，指定的值必须是常量，例如字符串或者数字，而不能是变量。同样地，以函数wrap_html_tag()为例，不能像下面这样定义：

```php
$my_html_tag = 'i';
function wrap_html_tag($srting, $tag = $my_html_tag){}
```

6.9 返回失败信息

在PHP中，非true值并不是标准的，而且容易造成错误。因此，函数应该返回定义的false关键字，因为当检测逻辑值时它是最有效的。例如，strpos()返回子字符串在原始字符串第一次出现的位置。因此，如果要查找一个子字符串的位置，你可以会这样写：

```php
if(strpos($string, $substring)){/* 找到了 */}
```

然而，如果是在开始的位置就找到，那么函数的返回值是0.在if语句中0会被转换成false，所以该条件语句不会执行。所以我们应该这样来处理：

```php
if(false !== strpos($string, $substring)){/* 找到了 */}
```

8.3 删除一个cookie

```php
setcookie('flavor', '', 1);
```

在你的服务器和用户的计算机时钟不同步的情况下，最好设置一个很久之前的时间，所以我们在这里的时间戳取值为1。如果这个cookie之前设置过路径、域名或者安全标记，我们在删除它的时候也需要带上。
