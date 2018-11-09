---
title: Effective Ruby 改善Ruby程序的48条建议
date: 2018-11-07 17:08:35
categories: 阅读
tags:
  - Ruby
---
# Effective Ruby 改善Ruby程序的48条建议

## 留神，常量是可变的

> 总是将常量冻结 `freeze`，从而防止其被改变。

不使用 `freeze` ，常量可以修改。

```ruby
MY_CONSTANT = "foo"
MY_CONSTANT << "bar"
puts MY_CONSTANT #=> "foobar"
```

使用 `freeze` ，常量无法修改。

```ruby
MY_CONSTANT = "foo".freeze
MY_CONSTANT << "bar" #=> FrozenError (can't modify frozen String)
```

> 如果常量引用了一个集合对象比如数组或散列，那么冻结整个集合及其所有元素。

这个 `tip` 已经落伍，在 `Ruby 2.2` 及后续版本会自动冻结整个集合及其所有元素。

```ruby
# in Ruby >= 2.1
NETWORKS = ["192.168.1", "192.168.2"].freeze
NETWORKS << "192.168.3" #=> FrozenError (can't modify frozen Array)
NETWORKS[0] = "192.168.3" #=> FrozenError (can't modify frozen Array)

user = { "name" => "name" }.freeze
user["email"] = "email" #=> FrozenError (can't modify frozen Hash)
user["name"] = "name2" #=> FrozenError (can't modify frozen Hash)
```

> 要防止常量被重新赋值，可以冻结定义它的那个模块。

常量使用 `freeze`，`ruby` 出现 `warning` 但是依然能够被重新赋值。

```ruby
module Defaults
  TIMEOUT = 5.freeze
end

Defaults::TIMEOUT = 6 
#=> warning: already initialized constant Defaults::TIMEOUT
#=> warning: previous definition of TIMEOUT was here

puts Defaults::TIMEOUT #=> 6
```

冻结模块后，常量无法赋值。

```ruby
module Defaults
  TIMEOUT = 5
end

Defaults.freeze

Defaults::TIMEOUT = 6 #=> FrozenError (can't modify frozen Module)
```

## 推荐使用 Struct 而非 Hash 存储结构化数据

> 在处理结构化数据时，如果创建一个新类不那么合适时，推荐使用 `Struct` 而非 `Hash`
>
>将 `Struct::new` 的返回值赋给常量，并像类一样使用它。

```ruby
# Hash
reading = { date: "2018-10-30", high: 30, low: 20 }

def mean(reading)
  (reading[:high] + reading[:low]) / 2.0
end

mean(reading) #=> 25.0

# Struct
Reading = Struct.new(:date, :high, :low) do
  def mean
    (high + low) / 2.0
  end
end

Reading.new("2018-10-30", 30, 20).mean #=> 25.0
```

## 在改变作为参数的集合之前复制它们

> `Ruby` 中参数是按引用传递的，而不是值传递。这个规则有一个例外值得注意：它不适用于 `Fixnum` 对象。
>
> 在改变集合之前先复制它们。

`Ruby` 语言自带了两个用来复制对象的方法：`dup` 和 `clone`。它们都会基于接收者创建新的对象，但是与 `dup` 方法不同的是，`clone` 方法会保留原始对象的两个附加特性。

首先，`clone` 方法会保留接收者的冻结状态。如果原始对象的状态是冻结的，那么生成的副本也是冻结的。而 `dup` 方法就不同了，它永远不会返回冻结的对象。

其次，如果接收者中存在单例方法，使用 `clone` 方法也会复制单例类。由于 `dup` 方法不会这样做，所以当使用 `dup` 方法时，原始对象和使用 `dup` 方法创建的副本对于相同消息的响应可能是不同的。

多数情况下应使用 `dup` 方法而不是 `clone` 方法，特别是当你希望修改结果对象时。冻结对象时无法修改或是解冻的，所以 `clone` 方法可能会返回一个不可变的对象。由于我们要去对新对象进行修改，因此 `dup` 方法显然是更合适的选择。

> `dup` 方法和 `clone` 方法只会进行浅拷贝。

复制传入集合是一种常见的模式。但要小心，使用这样的方法存在潜在的危险。你要知道 `dup` 方法和 `clone` 方法返回的是浅拷贝对象。对于像 `Array` 一样的集合，这意味着仅仅复制了容器本身而没有复制其中的元素。

可以在不影响原始集合的情况下增添或移除其中的元素，但修改元素本身则是有影响的。原始集合及其副本引用了相同的元素对象。修改任一元素都会影响到集合本身，同样也会影响到任何引用这一元素的对象。

```ruby
a = ["Polar"]

b = a.dup << "Bear"
#=> ["Polar", "Bear"]

b.each {|x| x.sub!('lar', 'oh')}
#=> ["Pooh", "Bear"]

a
#=> ["Pooh"]
```

> 对于多数对象来说，可以使用 `Marshal` 来完成深拷贝。

可以使用 `Marshal` 类将一个集合及其所持有的元素序列化，然后再反序列化：

```ruby
a = ["Monkey", "Brains"]

b = Marshal.load(Marshal.dump(a))
#=> ["Monkey", "Brains"]

b.each(&:upcase!)
#=> ["MONKEY", "BRAINS"]

a
#=> ["Monkey", "Brains"]
```

使用 `Marshal` 来解决这一问题这某种程度上有一定的局限性。抛开对对象序列化和反序列化的时间不说，你还得考虑这一过程中需要的内存。毫无疑问，对象的副本会持有其本身的内存空间，而使用 `Marshal::dump` 中序列化时创建的字节流也是会占用内存的。转储和加载大对象会使程序消耗大内存更多。

一个潜在的更加严峻的问题时并非所有对象都可以被 `Marshal` 序列化。那些持有闭包的对象以及那些具有单例方法的对象时无法被序列化的。`Ruby` 的一些核心类也是不能被 `Marshal` 序列化的。这包括 `IO` 以及 `File` 等类型。对于所有这样的情形，在使用 `Marshal::dump` 进行序列化时会抛出一个 `TypeError` 异常。

## 了解如何通过 reduce 方法折叠集合

> 总是要给累加器一个初值。
>
> 给予 `reduce` 的块总是要返回一个累加器。对当前累加器的修改是可行的，要记住从块中返回。

假设我们有一个存储用户的数组，我们希望从中筛选出那些年龄大于或者等于 `21` 岁的人群。之后我们希望将这个用户数组转换成一个姓名数组。在没有使用 `reduce` 的时候，你可能会这样写：

```ruby
users.select {|u| u.age >= 21}.map(&:name)
```

当然这么做肯定是可行的，但并不高效。`select` 方法会遍历整个用户数组并返回新数组。这个新数组之后会再次进行遍历并映射成另一个值只包含名字的新数组。如果我们使用 `reduce` ，则无需创建或遍历多个数组：

```ruby
users.reduce([]) do |names, user|
  names << user.name if user.age >= 21
  names
end
```

## 力争代码被有效测试过

> 使用模糊测试和属性测试工具，帮助测试代码的快乐路径和异常路径。

在测试中，一个常犯的错误是我们只写快乐路径 `happy path` 测试。这是刚写完开发代码之后写测试时常见的情况。快乐路径测试，是指被测代码的前提条件都被满足的前提下，仅测试有效出入的测试方法。

有时候我们可能没有验证输入的合法性，而且中数据库中也没有添加不可为空的约束。快乐路径测试是有价值的，但是这不足以帮我们发现所有的 `bug`，因为制定的测试只测试了我们期望代码该做的事。

解决这个问题的一种方法是加入异常路径 `exception path` 测试，输入各种各样的值并保证代码的每一个分支都被执行过。例如模糊测试 `fuzz testing` 和属性测试 `property testing`。

这两种测试既互有联系，但又有不同的目的。基本思想都是，给我们的代码输入大量不同类型的数据，保证我们的代码依然能够正常工作。一般来说，模糊测试主要是应用于安全领域。向一个程序或者特定的方法输入大量随机的数据，是找出程序崩溃或暴露安全漏洞的一种非常好的方法。

采用模糊测试方法，我们的关注点从测试结果是通过还是失败，转移到是否能找到程序崩溃或者是异常问题上。这个过程通常需要一个随机值的发生器 `generator` 和我们需要测试的代码片段。举个例子，假如我们想知道 `URL::HTTP::build` 方法是否会在输入完全随机的无效主机名 `host name` 后崩溃？针对这个问题我们可以使用 `Ruby` 模糊测试库中的一个名为 `FuzzBert` 的 `Gem`。

```ruby
require('fuzzbert')
require('uri')

fuzz('URI::HTTP::build') do
  data("random server names") do
    FuzzBert::Generators.random
  end

  deploy do |data|
    URI::HTTP::build(host: data, path: '/')
  end
end
```

模糊测试虽说非常有趣，但并不适合日常使用。部分原因是，像 `FuzzBert` 这样的工具会持续不断地运行测试，除非你手动终止。为了让模糊测试更加高效，有时需要它连续运行好几天。`FuzzBert` 提供了配置选项，允许我们设置模糊测试运行的时间，不过测试运行的时间越长，你将越有信心相信代码里没有让系统崩溃的 `bug` 存在。

与模糊测试相似，属性测试也使用随机输入来测试你的代码，但所添加测试的期望是确定的。属性测试相对来说，显得更加实际，因为测试是有限的，而且可以与自动化单元测试一起运行。我们可以使用 `MrProper` 进行属性测试。

```ruby
require('mrproper')

properties('Version') do
  data([Integer, Integer, Integer])

  property("new(str).to_s == str") do |data|
    str = data.join('.')
    assert_equal(str, Version.new(str),to_s)
  end
end
```

> 测试覆盖率工具会给你一种虚假的安全感，因为被执行过的代码不代表这行代码是正确的。

代码覆盖率工具可以生成测试报告，告诉你测试时哪些代码被执行过。`SimpleCov` 能生成非常详细的 `HTML` 报告，涵盖工程中所有的源代码。但是它会给你一种虚假的安全感，因为被执行过的代码不代表这行代码是正确的。你仍然需要确保对执行的代码分支编写了有效的测试。

> 在编写特性的同时就加上测试，会让测试容易很多。

无论使用哪种测试工具，都有一些规则需要你遵守。最重要的一点是，尽早写测试，越早越好。等到接近项目尾声再写为时已晚。一方面，这会让测试脱离现有的项目，成为单独的项目；另一方面，到那时候你可能已经忘了哪些重要的属性需要被测试。所以说，在编写特性的同时就加上测试，会让测试容易很多。

> 这你开始寻找导致 `bug` 的根本原因之前，先写一个针对该 `bug` 的测试。

在寻找导致 `bug` 的根本原因之前，先写一个能够重现这个 `bug` 的测试。重现 `bug` 是修复 `bug` 的第一步，若有专门针对这个 `bug` 的测试，就可以保证在我们修复  `bug` 之后，它不会再次出现。

> 尽可能多地自动化你的测试。

最后，尽可能多地自动化你的测试。有最好的测试，但不去运行他们，那么这些测试也毫无用处。