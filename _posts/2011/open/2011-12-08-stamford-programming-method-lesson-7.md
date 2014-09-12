---
layout: post
title: 斯坦福《编程方法》第七课
category: open
---
##循环与“一半”问题

For循环与While循环的对比，例程序CheckerBoad，在Java中创建函数，创建函数举例，FactorialExample程序，用函数返回对象。

当不知道具体的循环次数时，使用while循环。你会去计算某些事物的执行次数（for循环），或者会在条件为真时才做某事（while），这就是两种循环的区别。

哨兵值，我们将会用一个常量去判断用户什么时候想输入数据，什么时候停止输入数据，所以在编程中这个值常被称之为哨兵。

例：从用户那读入一连串数字，直到用户输入0才停止读入，然后计算这些数字的和。

```java
public class Add extends ConsoleProgram {
	private static final int SENTINEL = 0;//哨兵
	public void run(){
		int total = 0;//输入值总和
		int val = readInt("Enter val:");//输入值
		while(val != SENTINEL){
			total += val;
			val = readInt("Enter val:");
		}
	println("Total = " + total);
	}
}
```

循环会判断如果你给的值不是哨兵值，就不会停止。

在计算机科学或者计算机编程中，我们很讨厌重复的代码。如果能够避免重复代码，即使只有一行我们都会尽力去消除。向用户询问数值的这个操作至少要执行一次，但是在第一场执行后，我们需要在循环里面重复这个操作，所以我们遇到了难题，如何避免重复的代码呢？

例：从用户那读入一连串数字，直到用户输入0才停止读入，然后计算这些数字的和。

```java
public class Add extends ConsoleProgram {
	private static final int SENTINEL = 0;//哨兵
	public void run(){
	int total = 0;//输入值总和
	while(true){
		int val = readInt("Enter val:");//输入值
		if(val == SENTINEL) break;//如果输入值等于哨兵就跳出循环
		total += val;
	}
		println("Total = " + total);
	}
}
```

循环会判断循环条件永远为真，看起来很奇怪。你会担心它不是一个无限循环吗？只有一种情况会被终止，我们会向用户询问数值，判断这个值是否为哨兵值。如果是，跳出循环。

break语句的作用就是它会跳出围绕代码最里面的那层循环。实际上它的用途是在循环内部检查跳出循环的条件，而不是在开头或每次进入循环的时候检查。

从编程风格来说，一个循环体内有多重终止条件是非常糟糕的。因为这会让程序员很难识别哪个条件为真，才能跳出循环。

比起用一大堆if语句来判断，稍微运用数学则来得更高明。

例：当i+y的值为偶数时执行，为奇数时不执行。

```java
sq.setFilled(((i + y) % 2) != 0);
```

多数情况下，return会出现在方法的结尾。但它并不只会出现在结尾，运行return时，正在执行的方法会马上停止，并且返回语句中的值或对象。

例：比较2个数字的大小，并且返回比较大的那个数。

```java
if(x > y){
	return x;
}else{
	return y;
}
```

