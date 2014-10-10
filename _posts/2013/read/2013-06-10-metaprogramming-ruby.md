---
layout: post
title: Ruby元编程
category: read
---
<img class="cover" src="/images/2013/06/9787560974583-242x300.jpg" width="242" height="300" />

原作名：Metaprogramming Ruby

ISBN：9787560974583

作者：[意] Paolo Perrotta

译者：廖志刚 / 陈睿杰

出版社：华中科技大学出版社

出版时间：2012-1

评价：☆☆☆☆☆

绝对五星好书，就算是你不会Ruby和Rails，我也建议你花几个小时了解Ruby语法后来看这本书。它不仅仅可以使你Ruby和Rails的水平大幅上升，同时有触类旁通的功效。

编程的定义：元编程是编写在运行时操纵语言构件的代码。

Ruby中你总是可以重新打开已经存在的类并对它进行动态修改，即使是像String或Array这样标准库中的类也不例外。这种技术可以简单称之为打开类（Open Class）技术。

打开类技术的隐患：如果你粗心地为某个类添加了某些功能，可能覆盖了旧的功能，结果导致各种BUG。一些人对这种修订类的鲁莽方式深感不悦，他们给这种方式起了一个不太好听的名字：猴子补丁（Monkeypatch）。

从某种意义上说，Ruby的class关键字更像是一个作用域操作符而不是类型声明语句。

实例变量存放在对象中，而方法存放在类中。

类本身也是对象，适用于对象的规则也适用于类。类和其他任何对象一样，也有自己的类，它的名字叫做Class。

Class类是Module类的子类，因此一个类只不过是一个增强的Module，增加了三个方法——`new()`、`allocate()`和`superclass()`而已。这几个方法可以让你创建对象并可以把它们纳入类体系架构中。除此之外（当然这些差别很重要），类和模块基本上是一样的。绝大多数适用于类的内容页同样适用于模块，反之亦然。

任何以大写字母开头的引用（包括类名和模块名），都是常量。

同时拥有模块和类的主要原因在于清晰性：通过审慎地选择使用类或模块，能够使代码更加清晰。通常，希望它应该在别处被包含（`include`）时（或者当成命名空间时），应该选择使用模块；当希望它被实例化或者继承时，应该选择使用类。因此，在很多情况下尽管类和模块可以互换，当还是最好根据自己的目的来选择是使用类还是使用模块，以明确表明你的意图。

`require()`方法与`load()`方法颇为相似，但是它的目的不同。通过`load()`方法可以执行代码，而require()则是用来导入（`import`）类库。这就是`require()`方法没有第二个可选参数的原因。在这些类库中的类名通常是你导入这些库时所希望得到的，因此没有理由在加载后销毁它们。

当调用一个方法时，Ruby会做两件事：
找到这个方法。这个方法称为方法查找。
执行这个方法。为了做到这点，Ruby需要一个叫做`self`的东西。

方法查找
接收者就是你调用方法所在的对象。例如，在`my_string.reverse()`语句中，`my_string`就是接收者。
想象从一个类移动到它的超类，然后再移动到超类的超类，依次类推，直到到达Object类（所有类的默认超类），最后来到BasicObject类（Ruby类体系结构的根节点）。在这个过程中，你所经历的类路径就是该类的祖先链（祖先链中还可以包含模块）。

当你在一个类（甚至可以是另外一个模块）中包含（`include`）一个模块时，Ruby耍了些小花招。Ruby创建了一个封装该模块的匿名类，并把这个匿名类插入到祖先链中，其在链中的位置正好在包含它的类上方。

Object类包含了Kernel模块，因此Kernel就进入了每个对象的祖先链。这样在某个对象中可以随意调用Kernel模块的方法。这使得`print`看起来像是一个语言的关键字，其实它不过是一个方法而已。
你也可以利用这种技术，如果给Kernel模块增加一个方法，这个内核方法（Kernel Method）就对所以对象可用。RubyGems是Ruby的包管理器，它有一个`gem()`方法，用来激活给定版本的gem：

{% highlight ruby %}
require 'rubygems'
gem 'rails', '= 2.3.2'
{% endhighlight %}

因为`gem()`方法是内核方法（Kernel Method）中的方法，所以可以在任何地方调用它。这点可以从RubyGems的源代码中得以验证：

{% highlight ruby %}
module Kernel
def gem(gem_name, version_requirements)
#...
{% endhighlight %}

静态语言会强迫你写很多无趣和重复的代码，即所谓的样板法（boilerplate method），而这些仅仅是为了让编译器开心而已。

通过`send()`方法，你想调用的方法名可以成为一个参数，这样就可以在代码运行期间，直到最后一刻才决定调用哪个方法。这种技术称为动态派发（Dynamic Dispatch）。

可以利用`Module#define_method()`方法定义一个方法，只需要为其提供一个方法名和充当方法主体的块即可。这种运行时定义方法的技术称为动态方法（Dynamic Method）。

被`method_missing()`方法处理的消息，从调用者角度看，跟普通方法没有什么区别，但是实际上接收者并没有相对应的方法。这被称为一个幽灵方法（Ghost Method）。

一个捕获幽灵方法调用并把它们转发给另外一个对象的对象（有时也会在转发前后包装一些自己的逻辑），称为动态代理（Dynamic Proxy）。

动态代理技术的通病：当一个幽灵方法和一个真实方法发生名字冲突时，后者会胜出。如果不需要那个继承来的方法（真实方法），则可以通过删除它来解决这个问题。为了安全起见，你应该在代理类中删除绝大多数继承来的方法。这就是所谓的白板（Blank Slate）类，它所拥有的方法比Object类还要少。从Ruby1.9开始，白板技术被集成到语言自身中。默认情况下，类还是会从Object继承，从BesicObject类继承来的类会自动成为白板类。

这方面超像JS。（P82）每个Ruby作用域包含一组绑定，并且不同的作用域之间被作用域门分隔开来：`class`、`module`和`def`。如果要让一两个绑定穿越作用域门，那么可以用方法来替代作用域门：用一个闭包获取当前的绑定，并把这个闭包传递给该方法。你可以使用`Class.new()`方法代替`class`，使用`Module.new`代替`module`，以及使用`Module#define_method()`代替`def`。这就形成了一个扁平作用域，它是闭包中的一个基本概念。如果在一个扁平作用域中定义了多个方法，则这些方法可以用一个作用域门进行保护，并共享绑定，这种技术称为共享作用域。

示例代码：

{% highlight ruby %}
my_var = "Success"

MyClass = Class.new do
  puts "#{my_var} in the class definition!"

  define_method :my_method do
    puts "#{my_var} in the method!"
  end
end

MyClass.new.my_method

# => Success in the class definition!
# => Success in the method!

def define_methods
  shared = 0

  Kernel.send :define_method, :counter do
    shared
  end

  Kernel.send :define_method, :inc do |x|
    shared += x
  end
end

define_methods

counter # => 0
inc(4)
counter # => 4
{% endhighlight %}

上下文探针：`instance_eval()`方法，它像是一个深入到对象中的代码片段，对其进行操作。示例代码：

{% highlight ruby %}
class MyClass
  def initialize
    @v = 1
  end
end

obj = MyClass.new
obj.instance_eval do
  self # => #<MyClass:0x3340dc @v=1>

  @v # => 1
end
{% endhighlight %}

Ruby中引入了一个名为`instance_exec()`的方法，它和`instance_eval()`方法相似，但它允许对块传入参数：

{% highlight ruby %}
class C
  def initialize
    @x, @y = 1, 2
  end
end

C.new.instance_exec(3) {|arg| (@x + @y) * arg}  # => 9
{% endhighlight %}

使用`class`关键字创建类

{% highlight ruby %}
class MyClass < Array
  def my_method
    'Hello!'
  end
end
{% endhighlight %}

不使用`class`关键字创建类（这种方式也很像JS）

{% highlight ruby %}
c = Class.new(Array) do
  def my_method
    'Hello!'
  end
end

MyClass = c
c.name # => "MyClass"
{% endhighlight %}

引入单件方法，Ruby允许给单个对象增加一个方法。例如，下面演示了怎样给一个特定的字符串添加一个`title?()`方法（JS也能做这个功能吗？经过测试是可以的：<a title="JavaScript单件方法" href="/images/2013/05/23/js-singleton-methods.html" target="_blank">JavaScript单件方法</a>）

{% highlight ruby %}
str = "just a regular string"

def str.title?
  self.upcase == self
end

str.title? # => false
str.methods.grep(/title?/) # => [:title?]
str.singleton_methods # => [:title?]
{% endhighlight %}

类方法的实质就是：它们是一个类的单件方法。

类扩展

{% highlight ruby %}
module MyModule
  def my_method
   'hello'
  end
end

class MyClass
  class << self
    include MyModule
  end
end

MyClass.my_method # => "hello"
{% endhighlight %}

同理，对象扩展

{% highlight ruby %}
module MyModule
  def my_method
   'hello'
  end
end

obj = Object.new
class << obj
  include MyModule
end

obj.my_method # => "hello"
obj.singleton_methods # => [:my_method]
{% endhighlight %}

类扩展和对象扩展的应用非常普遍，因此Ruby为它们专门提供了一个叫做`Object#extend()`的方法：

{% highlight ruby %}
module MyModule
  def my_method 
    'hello' 
  end
end

obj = Object.new
obj.extend MyModule
obj.my_method # => "hello"

class MyClass
  extend MyModule
end
MyClass.my_method # => "hello"
{% endhighlight %}

利用`alias`关键字和`alias_method`方法，可以使用一种技巧：环绕别名

1. 给方法定义一个别名
2. 重新定义这个方法
3. 在新的方法中调用老的方法

类扩展混入（Class Extension Mixin）技术是类扩展和钩子方法的结合。

1. 定义一个模块，姑且叫做MyMixin
2. 在MyMixin中定义一个内部模块（通常把它叫做ClassMethods），并给它定义一些方法。这些方法最终会成为类方法。
3. 覆写`MyMixin#included()`方法来用ClassMethods扩展包含者（使用`extend()`方法）
4. 在需要调用的类或模块中使用`include`关键字引入

例子：

{% highlight ruby %}
module MyMixin
  def self.included(base)
    base.extend(ClassMethods)
  end

  module ClassMethods
    def x
      "x()"
    end
  end
end

Class Xxxx
  include MyMixin
  # ...
end
{% endhighlight %}

在Ruby世界里，私有方法通常被认为是一种建议，而非一种约定。这是Ruby哲学的主题：规则是存在的，但是，如果确切知道你要做的是什么，则可以打破它们（绝大部分）。正如Matz（Ruby的作者）所说，Ruby把你视为一个成熟的开发者。

为了避免处处重复环绕别名机制，Rails提供了一种通用的元编程方法来帮助你快速实现它。其名字叫`Module#alias_method_chain()`方法，由ActiveSupport库提供。

当第一次访问一个属性时，这个属性是一个幽灵方法。`ActiveRecord::Base#mehod_missing()`方法会在这时把这个幽灵方法转换为一个真实方法。同时，`method_missing()`方法还可以动态地为数据库中所有其他字段创建“读”、“写”和“问题”访问器。当下一次访问这个属性或另外一个基于数据库字段的属性时，会发现有一个真实的访问器方法等着你，而不会再进入`method_missing()`方法。

先用一些幽灵方法（`method_missing`），再通过执行代码字符串把它们转换为动态方法（`define_method`），然后使用动态派发对它们进行调用（`send`）。

为了避免猴子补丁覆盖已有的方法，你可以使用`instance_method_already_implemented?()`方法来检查。

在Ruby无法知道想给一个局部变量赋值还是调用一个拟态方法的时候，会默认选择第一种方法。

{% highlight ruby %}
class MyClass
  attr_accessor :my_attr

  def initialize_attributes
    my_attr = 10
  end
end
obj = MyClass.new
obj.initialize_attributes
obj.my_attr  # => nil
{% endhighlight %}

为了避免这个问题，给当前对象的属性赋值时，应该总是显式使用`self`：

{% highlight ruby %}
class MyClass
  attr_accessor :my_attr

  def initialize_attributes
    self.my_attr = 10
  end
end

obj = MyClass.new
obj.initialize_attributes
obj.my_attr  # => 10
{% endhighlight %}

我们经常看到类似这种用法：

{% highlight ruby %} 
a ||= []
{% endhighlight %}

`||=`实际上是下面语句的快捷写法：

{% highlight ruby %} 
a = a || []
{% endhighlight %}

也等同于：

{% highlight ruby %} 
if a != nil
  a = a
else
  a = []
end
{% endhighlight %}

这种惯用法被称为空指针保护。

`*`操作符可以把多个参数收集到一个数组中：

{% highlight ruby %} 
def my_method(*args)
  args
end

my_method(1, '2', 'three')  # => [1, '2', 'three']
{% endhighlight %}

这种惯用法称为参数数组。注意一个方法只能有一个参数数组。

链式调用，有时被称为“火车失事”。

领域专属语言（domain-specific language, DSL）,它的对立面是通用语言（general-purpose language, GPL）
