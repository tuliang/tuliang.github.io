---
layout: post
title: PHP版模板方法模式
---
模板方法模式（Template Method Pattern），在一个方法中定义一个算法的骨架，而将一些步骤延迟到子类中。模板方法使得子类可以在不改变算法结构的情况下，重新定义算法中的某些步骤。

```php
<?php
/*
 * 模板方法模式
 * 在一个方法中定义一个算法的骨架，
 * 而将一些步骤延迟到子类中。
 * 模板方法使得子类可以在不改变算法结构的情况下，
 * 重新定义算法中的某些步骤。
*/
abstract class CaffeineBeverage{
	final function prepareRecipe(){
		$this->boilWater();
		$this->brew();
		$this->pourInCup();
		$this->addCondiments();
	}
	
	abstract function brew();
	
	abstract function addCondiments();
	
	function boilWater(){
		echo 'Boiling water<br/>';
	}
	
	function pourInCup(){
		echo 'Pouring into cup<br/>';
	}
}

class Tea extends CaffeineBeverage{
	public function brew(){
		echo 'Steeping the tea<br/>';
	}
	
	public function addCondiments(){
		echo 'Adding Lemon<br/>';
	}
}

class Coffee extends CaffeineBeverage{
	public function brew(){
		echo 'Dripping Coffee through filter<br/>';
	}

	public function addCondiments(){
		echo 'Adding Sugar and Milk<br/>';
	}
}

echo '茶：<br/>';
$Tea = new Tea;
$Tea->prepareRecipe();
echo '咖啡：<br/>';
$Coffee = new Coffee;
$Coffee->prepareRecipe();
```

输出：  
茶：  
Boiling water  
Steeping the tea  
Pouring into cup  
Adding Lemon  
咖啡：  
Boiling water  
Dripping Coffee through filter  
Pouring into cup  
Adding Sugar and Milk  
