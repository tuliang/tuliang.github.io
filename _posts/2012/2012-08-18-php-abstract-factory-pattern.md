---
layout: post
title: PHP版抽象工厂模式
---
抽象工厂模式（Abstract Factory Pattern），提供一个接口，用于创建相关或依赖对象的家族，而不需要明确指定具体类。

```php
<?php
/*
 * 抽象工厂模式
 * 提供一个接口，
 * 用于创建相关或依赖对象的家族，
 * 而不需要明确指定具体类。
 */

//定义比萨商店
abstract class PizzaStore{

	public function orderPizza($type){
		$Pizza = $this->createPizza($type);

		$Pizza->prepare();
		$Pizza->bake();
		$Pizza->cut();
		$Pizza->box();

		return $Pizza;
	}

	abstract protected function createPizza($type);
}

//纽约比萨店
class NYPizzaStore extends PizzaStore{

	public function createPizza($type){
		$Pizza = null;
		$PizzaIngredientFactory = new NYPizzaIngredientFactory();

		if ('cheese' == $type) {
			$Pizza = new CheesePizza($PizzaIngredientFactory);
		}elseif ('clam' == $type){
			$Pizza = new ClamPizza($PizzaIngredientFactory);
		}

		return $Pizza;
	}
}

//芝加哥比萨店
class ChicagoPizzaStore extends PizzaStore{

	public function createPizza($type){
		$Pizza = null;
		$PizzaIngredientFactory = new ChicagoPizzaIngredientFactory();

		if ('cheese' == $type) {
			$Pizza = new CheesePizza($PizzaIngredientFactory);
		}elseif ('clam' == $type){
			$Pizza = new ClamPizza($PizzaIngredientFactory);
		}

		return $Pizza;
	}
}

//原料工厂接口
interface PizzaIngredientFactory{
	public function createDough();
	public function createSauce();
	public function createCheese();
	public function createVeggies();
	public function createPepperoni();
	public function createClam();
}

//纽约原料工厂
class NYPizzaIngredientFactory implements PizzaIngredientFactory{
	public function createDough(){
		echo 'NY createDough<br />';
	}

	public function createSauce(){
		echo 'NY createSauce<br />';
	}

	public function createCheese(){
		echo 'NY createCheese<br />';
	}

	public function createVeggies(){
		echo 'NY createVeggies<br />';
	}

	public function createPepperoni(){
		echo 'NY createPepperoni<br />';
	}

	public function createClam(){
		echo 'NY createClam<br />';
	}	
}

//芝加哥原料工厂
class ChicagoPizzaIngredientFactory implements PizzaIngredientFactory{
	public function createDough(){
		echo 'Chicago createDough<br />';
	}

	public function createSauce(){
		echo 'Chicago createSauce<br />';
	}

	public function createCheese(){
		echo 'Chicago createCheese<br />';
	}

	public function createVeggies(){
		echo 'Chicago createVeggies<br />';
	}

	public function createPepperoni(){
		echo 'Chicago createPepperoni<br />';
	}

	public function createClam(){
		echo 'Chicago createClam<br />';
	}
}

//比萨类
abstract class Pizza{

	abstract public function prepare();

	public function bake(){
		echo 'bake<br />';
	}

	public function cut(){
		echo 'cut<br />';
	}

	public function box(){
		echo 'box<br />';
	}
}

//比萨1
class CheesePizza extends Pizza{
	public $PizzaIngredientFactory;

	public function __construct($PizzaIngredientFactory){
		$this->PizzaIngredientFactory = $PizzaIngredientFactory;
	}

	//向原料工厂请求原料
	public function prepare(){
		$this->PizzaIngredientFactory->createDough();
		$this->PizzaIngredientFactory->createSauce();
		$this->PizzaIngredientFactory->createCheese();
	}
}

//比萨2
class ClamPizza extends Pizza{
	public $PizzaIngredientFactory;

	public function __construct($PizzaIngredientFactory){
		$this->PizzaIngredientFactory = $PizzaIngredientFactory;
	}

	//向原料工厂请求原料
	public function prepare(){
		$this->PizzaIngredientFactory->createDough();
		$this->PizzaIngredientFactory->createSauce();
		$this->PizzaIngredientFactory->createCheese();
		$this->PizzaIngredientFactory->createClam();
	}
}

$NYPizzaStore = new NYPizzaStore();
$ChicagoPizzaStore = new ChicagoPizzaStore();

$NYPizzaStore->orderPizza('cheese');
$ChicagoPizzaStore->orderPizza('clam');
```

输出：  
NY createDough  
NY createSauce  
NY createCheese  
bake  
cut  
box  
Chicago createDough  
Chicago createSauce  
Chicago createCheese  
Chicago createClam  
bake  
cut  
box  
