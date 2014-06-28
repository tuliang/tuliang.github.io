---
layout: post
title: PHP版观察者模式
---
观察者模式（Observer Pattern），定义了对象之间的一对多依赖，这样一来，当一个对象改变状态时，它的所有依赖者都会收到通知并自动更新。

```php
<?php
/*
 * 观察者模式
 * 定义了对象之间的一对多依赖，这样一来，
 * 当一个对象改变状态时，
 * 它的所有依赖者都会收到通知并自动更新。
 */

//主题
interface Subject{
	//注册
	public function register($obj);
	//删除
	public function remove($obj);
	//通知
	public function notify();
}

//观察者
interface Observer{
	//更新
	public function update($val);
}

//显示
interface DisplayElement{
	public function display();
}

class Test implements Subject{
	private $list;
	private $val;

	public function __construct(){
		$this->list = array();
		$this->val = '';
	}

	public function register($obj){
		$this->list[] = $obj;
	}

	public function remove($obj){
		foreach ($this->list as $key=>$item){
			if ($item == $obj){
				unset($this->list[$key]);
				break;
			}
		}	
	}

	public function notify(){
		foreach ($this->list as $item){
			$obj = new $item;
			$obj->update($this->val);
		}
	}

	public function setVal($val){
		$this->val = $val;
		$this->notify();
	}

	public function sendMessage($val){
		$this->setVal($val);
	}
}

//观察者1
class Observer1 implements Observer, DisplayElement{
	private $val;

	public function update($val){
		$this->val = $val;
		$this->display();
	}

	public function display(){
		echo '1'.$this->val.'<br />';
	}
}

//观察者2
class Observer2 implements Observer, DisplayElement{
	private $val;

	public function update($val){
		$this->val = $val;
		$this->display();
	}

	public function display(){
		echo '2'.$this->val.'<br />';
	}
}

/*
 * 程序运行时注册或删除观察者
 */
$obj = new Test();
$obj->register(new Observer2);
$obj->sendMessage('ppp');
echo '<br />';
$obj->register(new Observer1);
$obj->sendMessage('wow');
echo '<br />';
$obj->remove(new Observer1);
$obj->sendMessage('lol');
```

输出：  
2ppp  

2wow  
1wow  

2lol  
