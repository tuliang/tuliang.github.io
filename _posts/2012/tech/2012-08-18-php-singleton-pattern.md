---
layout: post
title: PHP版单件模式
category: tech
---
单件模式（Singleton Pattern），确保一个类只有一个实例，并提供一个全局访问点。

```php
<?php
/*
 * 单件模式
 * 确保一个类只有一个实例，并提供一个全局访问点。
 */

class MyClass{
	private static $MyObj;

	//创建私有并且为空的构造函数使其不能new对象
	private function __construct(){}
	
	//创建私有并且为空的克隆函数使其不能clone对象
	private function __clone(){}

	public static function getObj(){
		if (null == self::$MyObj){
			self::$MyObj = new MyClass();
		}
		return self::$MyObj;
	}
}

$MyObj = MyClass::getObj();
var_dump($MyObj);
$MyObj = MyClass::getObj();
var_dump($MyObj);
```

输出：

object(MyClass)[1]

object(MyClass)[1]
