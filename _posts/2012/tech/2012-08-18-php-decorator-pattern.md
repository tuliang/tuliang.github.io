---
layout: post
title: PHP版装饰者模式
category: tech
---
装饰者模式（Decorator Pattern），动态地将责任附加到对象上。若要扩展功能，装饰者提供了比继承更有弹性的替代方案。

{% highlight php %}
<?php
/*
 * 装饰者模式
 * 动态地将责任附加到对象上。若要扩展功能，
 * 装饰者提供了比继承更有弹性的替代方案。
 */

//饮料抽象类
abstract class Beverage{
	public $description = 'Unknown Beverage';

	public function getDescription(){
		return $this->description;
	}

	public abstract function cost();
}

//调料抽象类
abstract class CondimentDecorator extends Beverage{
	//书中的JAVA代码里这里是一个抽象方法，PHP不允许这么做
	//public abstract function getDescription();
}

//饮料1
class Espresso extends Beverage{

	public function __construct(){
		$this->description = 'Espresso';
	}

	public function cost(){
		return 1.99;
	}
}

//饮料2
class HouseBlend extends Beverage{

	public function __construct(){
		$this->description = 'House Blend Coffee';
	}

	public function cost(){
		return 0.89;
	}
}

//调料1
class Mocha extends CondimentDecorator{
	public $beverage;

	public function __construct($beverage){
		$this->beverage = $beverage;
	}

	public function getDescription(){
		return $this->beverage->getDescription().', Mocha';
	}

	public function cost(){
		return 0.2 + $this->beverage->cost();
	}
}

//一杯普通的饮料
$beverage = new Espresso();
echo 'Description:'.$beverage->getDescription();
echo '<br/>Cost:'.$beverage->cost().'<br/>';

//一杯普通的饮料
$beverage2 = new HouseBlend();
//加一点调料
$beverage2 = new Mocha($beverage2);
echo 'Description:'.$beverage2->getDescription();
echo '<br/>Cost:'.$beverage2->cost().'<br/>';
//再多加一点调料
$beverage2 = new Mocha($beverage2);
echo 'Description:'.$beverage2->getDescription();
echo '<br/>Cost:'.$beverage2->cost().'<br/>';
//再多加一点调料
$beverage2 = new Mocha($beverage2);
echo 'Description:'.$beverage2->getDescription();
echo '<br/>Cost:'.$beverage2->cost().'<br/>';
{% endhighlight %}

输出：  
Description:Espresso   
Cost:1.99   
Description:House Blend Coffee, Mocha  
Cost:1.09  
Description:House Blend Coffee, Mocha, Mocha  
Cost:1.29  
Description:House Blend Coffee, Mocha, Mocha, Mocha  
Cost:1.49  
