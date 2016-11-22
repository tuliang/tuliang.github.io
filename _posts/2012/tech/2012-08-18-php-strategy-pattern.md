---
layout: post
title: PHP版策略模式
category: tech
---
策略模式（Strategy Pattern），定义了算法族，分别封装起来，让它们之间可以互相替换，此模式让算法的变化独立于使用算法的客户。

{% highlight php %}
<?php
/*
 * 策略模式
 * 定义了算法族，分别封装起来，让它们之间可以互相替换，
 * 此模式让算法的变化独立于使用算法的客户。
 */
class Test{
	private $obj;

	public function __construct(){
		$this->obj = new suanfa1;
	}

	public function setSuanfa($obj){
		$this->obj = $obj;
	}

	public function run(){
		$this->obj->suanfa();
	}
}

/*
 * 算法接口
 */
interface Suanfa{
	public function suanfa();
}

/*
 * 算法1
*/
class Suanfa1 implements Suanfa{
	public function suanfa(){
		echo '1<br />';
	}
}

/*
 * 算法2
*/
class Suanfa2 implements Suanfa{
	public function suanfa(){
		echo '2<br />';
	}
}

/*
 * 程序运行时改变算法
 */
$obj = new Test();
$obj->run();
$obj->setSuanfa(new Suanfa2());
$obj->run();
{% endhighlight %}

输出:   
1  
2  
