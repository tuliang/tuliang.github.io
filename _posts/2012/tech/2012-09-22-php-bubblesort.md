---
layout: post
title: PHP冒泡排序
category: tech
---
PHP冒泡排序

{% highlight php %}
<?php
//产生10个1到100的随机数
for ($i = 0; $i < 10; $i++){
	$array[$i] = rand(1, 100);
}

/*
 * 冒泡排序
 */
function bubblesort($array, $count){
	if ($count == 0){//排序结束
		return $array;
	}
	
	for ($i = 0; $i < $count-1; $i++){		
		//将两个相邻的随机数做比较，
		//当第$i个随机数大于第$i+1个随机数时，
		//互换它们的位置
		if ($array[$i] > $array[$i+1]){
			$tmp = $array[$i+1];
			$array[$i+1] = $array[$i];
			$array[$i] = $tmp;
		}
	}	
	
	//PHP中递归需要return，否则只能得到null
	return bubblesort($array, $count-1);
}

$count = count($array);
$new_array = bubblesort($array, $count);
var_dump($new_array);
{% endhighlight %}

PHP递归时需要return，如下述代码中

{% highlight php %}
return bubblesort($array, $count-1);
{% endhighlight %}

改为

{% highlight php %}
bubblesort($array, $count-1);
{% endhighlight %}

$new_array就接不到值，即结果为null
