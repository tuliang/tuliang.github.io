---
layout: post
title: PHP版命令方法模式
category: tech
---
命令模式（Command Pattern），将“请求”封装成对象，以便使用不同的请求、队列或者日志来参数化其他对象。命令模式也支持可撤销的操作。

{% highlight php %}
<?php
/*
 * 命令模式
 * 将“请求”封装成对象，
 * 以便使用不同的请求、
 * 队列或者日志来参数化其他对象。
 * 命令模式也支持可撤销的操作。
*/
interface Command{
	//执行
	public function execute();
	//撤销
	public function undo();
}

class Light{
	public function on(){
		echo '开灯<br />';
	}
	
	public function off(){
		echo '关灯<br />';
	}
}

class LightOnCommand implements Command{
	public $light;
	
	public function __construct($light){
		$this->light = $light;
	}
	
	public function execute(){
		$this->light->on();
	}
	
	public function undo(){
		$this->light->off();
	}
}

class LightOffCommand implements Command{
	public $light;

	public function __construct($light){
		$this->light = $light;
	}

	public function execute(){
		$this->light->off();
	}
	
	public function undo(){
		$this->light->on();
	}
}

class Stereo{
	public function on(){
		echo '开音响<br />';
	}

	public function off(){
		echo '关音响<br />';
	}
}

class StereoOnCommand implements Command{
	public $stereo;

	public function __construct($stereo){
		$this->stereo = $stereo;
	}

	public function execute(){
		$this->stereo->on();
	}

	public function undo(){
		$this->stereo->off();
	}
}

class StereoOffCommand implements Command{
	public $stereo;

	public function __construct($stereo){
		$this->stereo = $stereo;
	}

	public function execute(){
		$this->stereo->off();
	}

	public function undo(){
		$this->stereo->on();
	}
}

class NoCommand implements Command{

	public function execute(){
		echo '没有关联命令<br />';
	}
	
	public function undo(){
		echo '没有关联命令<br />';
	}
}

/*
 * 遥控器
 */
class RemoteControl{
	public $onCommands;
	public $offCommands;
	public $undoCommands;
	
	public function __construct(){
		$this->onCommands = array();
		$this->offCommands = array();
		
		$noCommand = new NoCommand();
		for ($i = 0; $i < 3; $i++){
			$this->onCommands[$i] = $noCommand;
			$this->offCommands[$i] = $noCommand;
		}
		
		//默认值为空命令
		//$this->undoCommands[] = array();
	}
	
	/*
	 * @param $slot 位置
	 * @param $onCommand 开的命令
	 * @param $offCommand 关的命令
	 */
	public function setCommand($slot, $onCommand, $offCommand){
		$this->onCommands[$slot] = $onCommand;
		$this->offCommands[$slot] = $offCommand;
	}
	
	//按下按钮-开
	public function onButtonWasPushed($slot){
		$this->onCommands[$slot]->execute();
		$this->undoCommands[] = $this->onCommands[$slot];
	}
	
	//按下按钮-关
	public function offButtonWasPushed($slot){
		$this->offCommands[$slot]->execute();
		$this->undoCommands[] = $this->offCommands[$slot];
	}
	
	//按下按钮-撤销
	public function undoButtonWasPushed(){
		echo '<br />';
		echo '开始撤销操作<br />';
		echo '<br />';		
		for ($i = count($this->undoCommands)-1; $i >= 0; $i--){
			$this->undoCommands[$i]->undo();
		}
	}
}

$RemoteControl = new RemoteControl();
$Light = new Light();
$LightOnCommand = new LightOnCommand($Light);
$LightOffCommand = new LightOffCommand($Light);
$Stereo = new Stereo();
$StereoOnCommand = new StereoOnCommand($Stereo);
$StereoOffCommand = new StereoOffCommand($Stereo);
$RemoteControl->setCommand(0, $LightOnCommand, $LightOffCommand);
$RemoteControl->setCommand(1, $StereoOnCommand, $StereoOffCommand);
$RemoteControl->onButtonWasPushed(0);
$RemoteControl->offButtonWasPushed(0);
$RemoteControl->onButtonWasPushed(1);
$RemoteControl->offButtonWasPushed(1);
$RemoteControl->undoButtonWasPushed();
{% endhighlight %}

输出：  
开灯  
关灯  
开音响  
关音响  

开始撤销操作  

开音响  
关音响  
开灯  
关灯  
