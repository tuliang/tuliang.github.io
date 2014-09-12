---
layout: post
title: Ruby编程语言
category: read
---
<img class="cover" src="/images/2013/09/9787121077012.jpg" />

原作名：The Ruby Programming Language

ISBN：9787121077012

作者：David Flanagan / 松本行弘  

译者：廖志刚 / 张禾 

出版社：电子工业出版社

出版时间：2009-01

评价：☆☆☆☆

初学Ruby或者会Rails然后回来补习Ruby基础的可以看一看。

Ruby支持并行赋值：

```ruby
x, y = 1, 2 # x = 1; y = 2
a, b = b, a # a b互换
x, y, z = [1, 2, 3] # x = 1; y = 2; z = 3
```

也允许返回多个值：

```ruby
def demo
  [1, 2]
end
```

通常情况下，不带感叹号的方法返回调用该方法的对象的一个修改过的拷贝，而带感叹号的方法则是一个可变方法，该方法会修改原对象。

全局变量以$为前缀，实例变量以@为前缀，类变量以@@为前缀。

puts将文本字符串打印到控制台并在其后面添加一个换行符（除非该字符串已经以一个换行符结尾了）。如果传递给puts的对象不是一个字符串，那么puts就调用该对象的to_s方法，并且打印该方法所返回的字符串。print方法和puts方法做的基本是同一件事情，但是它并不在末尾添加一个换行符。

函数p是puts的一个有用替代者，不仅仅是因为p比puts更加简短，而且还因为它是通过inspect方法将对象转化成字符串的，有时候此方法能比to_s方法返回对程序员更加友好的对象表示。

```ruby
puts Object
# => #<Object:0x007fe3e1cbc038>

p Object
# => #<Object title: "Object title", description: "Object description">
```

当一个整数结果太大而无法容纳一个Fixnum时，Ruby会自动将其转化成一个Bignum（类似的，如果Bignum整数计算后可以放入Fixnum，那么将被转化Fixnum），这样做的结果就是，Ruby中的整数算术操作不像其他语言中那样产生溢出。浮点数会上溢至两个特殊的值，即正无穷或负无穷，此外还会下溢至0。

Ruby1.9定义了三个命名清晰的字符串迭代器来取代each方法：each_byte按字节对一个字符串进行顺序的迭代，与之类似，each_char按字符进行迭代，而each_line则按行迭代。

范围（range）字面量的表现形式是在开始和结束值之间放置二三个点。如果使用两个点，那么改范围就是包含性的，值将是改范围的一部分。如果使用三个点，那么该范围就是排他性的，值将不是范围的一部分。

```ruby
a = 1..10
a.to_a # => [1, 2, 3, 4, 5, 6, 7, 8, 9, 10]
b = 1...10
b.to_a # => [1, 2, 3, 4, 5, 6, 7, 8, 9]
```

Ruby的`==`操作符测试两个不同的对象是否拥有同样的值，而equals方法测试两个对象是否是同一个对象。在这个方面Ruby和Java恰好相反。

一般情况下，一个yield表达式的值就是代码块中最后一个表达式的值。（PS：和JS非常像）

```ruby
squareroots = data.collect do |x|
  if (x < 0) then 0 else Math.sqrt(x) end
end
```

Ruby方法可以返回多个值，这需要显式使用return语句，并把要返回的值用逗号分隔开。

```ruby
def polar(x, y)
  return Math.hypot(x, y), Math.atan2(y, x)
end
```

通常我们想使用并行赋值时，会使用这种形式的方法定义。通过并行赋值，每个返回值会被赋给一个单独的变量。

```ruby
x, y = polar(x, y)
```

用def语句定义方法时，也可以包含异常处理代码。异常处理代码会使用rescue、else和ensure从句，这与begin语句的方式一致。在短小的方法中，用rescue子句和def语句配合让代码非常干净整洁，这意味着你不用使用一个多余的begin语句，也省去了一级额外的格式缩进。

参数的默认值不一定必须是常量：它们可以是任意表达式，也可以是实例变量的引用，还可以是前面定义参数的引用。比如：

```ruby
def suffix(s, index=s.size-1)
  s[index, s.size-index]
end
```

参数默认值在运行时被求值，而不是解析时被求值。在下面的方法中，默认值[]在每次方法调用时产生一个新的空数组，而并非在数组定义产生一个数组，然后不断重用它：

```ruby
def append(x, a=[])
  a << x
end
```

使用&来调用代码块：

```ruby
a, b = [1, 2, 3], [4, 5]
summation = Proc.new {|total,x| total+x }
sum = a.inject(0, &summation)
sum = b.inject(sum, &summation)
```

私有方法不能在所定义的类外被调用，但是它们会被子类继承，这意味着子类可以调用它们，也可以覆盖它们。在Ruby中，应该只对你了解的超类进行子类化。如果希望使用某个类的公开API而非它的具体实现，应该通过封装其实例和代理来扩展它的功能，而不是继承它。
