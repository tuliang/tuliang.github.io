---
layout: post
title: JavaSctipt编程精解
category: read
---
<img src="/images/2013/03/9787111396659-228x300.jpg" alt="9787111396659" width="228" height="300" class="cover" />

原作名: Eloquent JavaScript: A Modern Introduction to Programming

ISBN:  9787111396659

作者: Marijn Haverbeke

译者: 徐涛

出版社: 机械工业出版社华章公司

出版时间:  2012-10

评价: ☆☆☆

平心而论这本书用来入门还不错，如果说它是最棒的教程之一这个很难让人信服。内容有些老，2、3年前看的话还勉强。最后说一下翻译，汤姆大叔的博客还不错，可是翻译水平就一般般了。书中的那些错误，也有点略多了吧，看来校对、编辑那边也不怎么用心。

在前言作者提出，编程语言从初级语言发展到高级语言的目的和作用: “编程语言就是用于解决无意义的细节”。

JavaSctipt不会限制传入函数的参数数目。如果传入的参数过多，多余的参数则会被忽略掉；如果传入的参数过少，缺失的参数则默认为undefined。这样很可能导致意外传入错误的参数数目，而且不会得到提醒。

抽象的概念。（P55）如果演讲时面对的观众有一定的基础知识，就可以引用更大的概念，并且能以更短和更清晰的方式表达自己的意思。

书中对拼接字符串建议使用join方法，我编写了代码在Chrome25、FF19和IE10下进行测试，原始的+和join并没有太大差别。现代浏览器竞争这么激烈，已经将这种情况进行优化了，这样特意拼接字符串意义不大。除非你有大量的字符串需要拼接，并且运行环境在IE的低版本或是国产的各种套壳浏览器。附上测试代码: 

{% highlight javascript %}
var tStart = new Date();
var str = "" ;
for(var i=0;i<1000000;i++){
      str += "text"+i
}
var tEnd = new Date();
document.write("原始的方法加号 拼接1000000个字符串 花费时间: " +(tEnd.getTime()-tStart.getTime())+"毫秒");

str = "";

tStart = new Date();
var array = new Array;
for(var i=0;i<1000000;i++) {
      array[i] = "text"+i 
}
str = array.join("");
tEnd = new Date();
document.write("<br/>join 拼接1000000个字符串 花费时间: " +(tEnd.getTime()-tStart.getTime())+"毫秒");
{% endhighlight %}

勘错: 
P38    
// 2007年3月30日 8点20分30秒  
new Date(2007 , 2, 30, 8, 20, 30);  

应为:   
// 2007年3月30日 8点20分30秒  
new Date(2007 , 3, 30, 8, 20, 30);  

P105   
多重继承，虽然在有些情况下非常有用，但在很多时候却可以安全忽略。  

应为:   
多重继承，虽然在有些情况下非常有用，但在很多时候却可以完全忽略。  
