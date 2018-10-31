---
title: PHP 工厂方法模式
date: 2012-08-18 22:29:18
categories: 后端
tags:
  - PHP
  - 设计模式
---
简单工厂其实不是一个设计模式，反而比较像是一种编程习惯。

有些开发人员的确是把这个编程习惯误认为是工厂模式。

```php
<?php
//比萨商店
class PizzaStore{
  public $Factory;

  public function __construct($factory){
    $this->Factory = $factory;
  }

  public function orderPizza($type){
    $Pizza = $this->Factory->createPizza($type);

    $Pizza->prepare();
    $Pizza->bake();
    $Pizza->cut();
    $Pizza->box();

    return $Pizza;
  } 
}

//简单比萨工厂
class SimplePizzaFactory{
  public function createPizza($type){
    $Pizza = null;

    if ('cheese' == $type) {
      $Pizza = new CheesePizza();
    }elseif ('pepperoni' == $type){
      $Pizza = new PepperoniPizza();
    }

    return $Pizza;
  } 
}
```

工厂方法模式 `Factory Method Pattern`，定义了一个创建对象的接口，但由子类决定要实例化的是哪一个。

工厂方法让类把实例化推迟到子类。

```php
//比萨接口
interface Pizza{
  public function prepare();
  public function bake();
  public function cut();
  public function box();
}

//比萨1
class CheesePizza implements Pizza{
  public function prepare(){
    echo 'CheesePizza prepare<br />';
  }

  public function bake(){
    echo 'CheesePizza bake<br />';
  }

  public function cut(){
    echo 'CheesePizza cut<br />';
  }

  public function box(){
    echo 'CheesePizza box<br />';
  }
}

//比萨2
class PepperoniPizza implements Pizza{
  public function prepare(){
    echo 'PepperoniPizza prepare<br />';
  }

  public function bake(){
    echo 'PepperoniPizza bake<br />';
  }

  public function cut(){
    echo 'PepperoniPizza cut<br />';
  }

  public function box(){
    echo 'PepperoniPizza box<br />';
  }
}

//纽约比萨1
class NYCheesePizza implements Pizza{
  public function prepare(){
    echo 'NYCheesePizza prepare<br />';
  }

  public function bake(){
    echo 'NYCheesePizza bake<br />';
  }

  public function cut(){
    echo 'NYCheesePizza cut<br />';
  }

  public function box(){
    echo 'NYCheesePizza box<br />';
  }
}

//纽约比萨2
class NYPepperoniPizza implements Pizza{
  public function prepare(){
    echo 'NYPepperoniPizza prepare<br />';
  }

  public function bake(){
    echo 'NYPepperoniPizza bake<br />';
  }

  public function cut(){
    echo 'NYPepperoniPizza cut<br />';
  }

  public function box(){
    echo 'NYPepperoniPizza box<br />';
  }
}

//芝加哥比萨1
class ChicagoCheesePizza implements Pizza{
  public function prepare(){
    echo 'ChicagoCheesePizza prepare<br />';
  }

  public function bake(){
    echo 'ChicagoCheesePizza bake<br />';
  }

  public function cut(){
    echo 'ChicagoCheesePizza cut<br />';
  }

  public function box(){
    echo 'ChicagoCheesePizza box<br />';
  }
}

//芝加哥比萨2
class ChicagoPepperoniPizza implements Pizza{
  public function prepare(){
    echo 'ChicagoPepperoniPizza prepare<br />';
  }

  public function bake(){
    echo 'ChicagoPepperoniPizza bake<br />';
  }

  public function cut(){
    echo 'ChicagoPepperoniPizza cut<br />';
  }

  public function box(){
    echo 'ChicagoPepperoniPizza box<br />';
  }
}

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

    if ('cheese' == $type) {
      $Pizza = new NYCheesePizza();
    }elseif ('pepperoni' == $type){
      $Pizza = new NYPepperoniPizza();
    }

    return $Pizza;
  }
}

//芝加哥比萨店
class ChicagoPizzaStore extends PizzaStore{
  public function createPizza($type){
    $Pizza = null;

    if ('cheese' == $type) {
      $Pizza = new ChicagoCheesePizza();
    }elseif ('pepperoni' == $type){
      $Pizza = new ChicagoPepperoniPizza();
    }

    return $Pizza;
  }
}

$NYPizzaStore = new NYPizzaStore();
$ChicagoPizzaStore = new ChicagoPizzaStore();

$NYPizzaStore->orderPizza('cheese');
$ChicagoPizzaStore->orderPizza('pepperoni');
```

输出

```  
NYCheesePizza prepare  
NYCheesePizza bake  
NYCheesePizza cut  
NYCheesePizza box  
ChicagoPepperoniPizza prepare   
ChicagoPepperoniPizza bake   
ChicagoPepperoniPizza cut  
ChicagoPepperoniPizza box  
```
