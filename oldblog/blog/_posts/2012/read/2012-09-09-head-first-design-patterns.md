---
layout: post
title: Head First 设计模式
category: read
---
<img class="cover" title="9787508353937" src="/images/2012/09/9787508353937-257x300.jpg" alt="Head First 设计模式" width="257" height="300" />

ISBN: 9787508353937

作者: Eric Freeman;Elisabeth Freeman;With Kathy ierra;Bert Bates

译者: Oreily Taiwan公司

出版社: 中国电力出版社

出版时间: 2007-9

评价: ☆☆☆☆☆

《Head First 设计模式》算是Oreilly的Head First系列很典型的一本，整个系列的特点就是以风趣幽默的语言配上大量的图例。对比GOF的那本经典以及难啃的《设计模式》，这本书在阅读中你会感到非常轻松愉快 。我感觉这本书非常适合工作一段时间后，感觉自己整个项目的代码结构很烂（如果细节部分的代码，建议先去阅读《代码大全》和《重构》），想去改变却无从下手的时候，它会对你有很大帮助的。同时也适合对设计模式有一些了解但不全面的人。

在阅读本书的时候去参考《设计模式》，将会是一个很好主题阅读，相信能对深刻理解设计模式有很大的帮助。当然本书也有一些缺点，比如书中的代码都是JAVA，如果你不熟悉JAVA的话，看起来可能会遇到一些麻烦。比如我就是只了解一些JAVA，而且好几年没碰过了，所以在阅读之前，至少要知道JAVA的基本语法和一些关键字。另外实例代码可能就需要自己写或者去网上找了，强烈建议自己写，毕竟这样你留下的印象会深一些，当作是本书的习题好了。说起习题，本书中的那些习题大部分是相当有趣的，也强烈建议做一下。

各种各样的设计模式就像各种武功套路。一般的人不会模式，什么都乱来，越到后来越控制不住，自然会走火入魔。高手则会一些，对付一般的问题不在话下，但有时往往会被模式所限制，什么问题都想往上套。而大牛，开始能够分辨何时能够使用模式，并且对模式进行改编使其适合当前的问题。真正的大师了解各种设计模式的优点和缺点，使用起来随心所欲，甚至能够自创。即，他们不会急于使用某种模式，而会针对问题采用最适合的方案。

摘录: 

<blockquote>使用模式最好的方式是: “把模式装进脑子里，然后在你的设计和已有的应用中，寻找何处可以使用它们。”以往是代码复用，现在是经验复用。

不管你在何处工作，构建些什么，用何种编程语言，在软件开发上，一直陪伴你的那个不变的真理是CHANGE。不管当初软件设计得多好，一段时间之后，总是需要成长与改变，否则软件就会“死亡”。

如果你用模式名称和大家沟通，其他开发人员能够马上且清楚地知道你在说些什么。但是也请不要从此染上“模式病”……以后连写一个“Hello World”都能扯上模式，那就代表你已经病了。

利用继承设计子类的行为，是在编译时静态决定的，而且所有的子类都会继承到相同的行为。然而，如果能够利用组合的做法扩展对象的行为，就可以在运行时动态地进行扩展。

在设计模式中，所谓的“实现一个接口”并“不一定”表示“写一个类，并利用implement关键字来实现某个接口”。“实现一个接口”泛指“实现某个超类型（可以是类或接口）的某个方法”。

（P522）采用模式时必须要考虑到这么做是否有意义，绝对不能为了使用模式而使用模式。</blockquote>
设计原则: 

<ul>
	<li>找出应用中可能需要变化之处，把它们独立出来，不要和那些不需要变化的代码混在一起。</li>
	<li>针对接口编程，而不是针对实现编程。</li>
	<li>多用组合，少用继承。</li>
	<li>为了交互对象之间的松耦合设计而努力。</li>
	<li>类应该对扩展开放，对修改关闭。</li>
	<li>要依赖抽象，不要依赖具体类。</li>
	<li>最少知识原则: 只和你的密友谈话。</li>
	<li>好莱坞原则: 别调用（打电话给）我们，我们会调用（打电话给）你。</li>
	<li>一个类应该只有一个引起变化的原因。</li>
</ul>

设计模式: 

<ul>
	<li><a title="PHP版策略模式" href="/2012/08/18/php-strategy-pattern.html" target="_blank"> 策略模式（Strategy Pattern）</a>，定义了算法族，分别封装起来，让它们之间可以互相替换，此模式让算法的变化独立于使用算法的客户。</li>
	<li><a title="PHP版观察者模式" href="/2012/08/18/php-observer-pattern.html" target="_blank"> 观察者模式（Observer Pattern）</a>，定义了对象之间的一对多依赖，这样一来，当一个对象改变状态时，它的所有依赖者都会收到通知并自动更新。</li>
	<li><a title="PHP版装饰者模式" href="/2012/08/18/php-decorator-pattern.html" target="_blank"> 装饰者模式（Decorator Pattern）</a>，动态地将责任附加到对象上。若要扩展功能，装饰者提供了比继承更有弹性的替代方案。</li>
	<li><a title="PHP版工厂方法模式" href="/2012/08/18/php-factory-method-pattern.html" target="_blank"> 工厂方法模式（Factory Method Pattern）</a>，定义了一个创建对象的接口，但由子类决定要实例化的是哪一个。工厂方法让类把实例化推迟到子类。</li>
	<li><a title="PHP版抽象工厂模式" href="/2012/08/18/php-abstract-factory-pattern.html" target="_blank"> 抽象工厂模式（Abstract Factory Pattern）</a>，提供一个接口，用于创建相关或依赖对象的家族，而不需要明确指定具体类。</li>
	<li><a title="PHP版单件模式" href="/2012/08/18/php-singleton-pattern.html" target="_blank"> 单件模式（Singleton Pattern）</a>，确保一个类只有一个实例，并提供一个全局访问点。</li>
	<li><a title="PHP版命令方法模式" href="/2012/09/07/php-command-pattern.html" target="_blank"> 命令模式（Command Pattern）</a>，将“请求”封装成对象，以便使用不同的请求、队列或者日志来参数化其他对象。命令模式也支持可撤销的操作。</li>
	<li>适配器模式（Adapter Pattern），将一个类的接口，转换成客户期望的另一个接口。适配器让原本接口不兼容的类可以合作无间。</li>
	<li>外观模式（Facade Pattern），提供了一个统一的接口，用来访问子系统中的一群接口。外观定义了一个高层接口，让子系统更容易使用。</li>
	<li><a title="PHP版模板方法模式" href="/2012/09/05/php-template-method-pattern.html" target="_blank"> 模板方法模式（Template Method Pattern）</a>，在一个方法中定义一个算法的骨架，而将一些步骤延迟到子类中。模板方法使得子类可以在不改变算法结构的情况下，重新定义算法中的某些步骤。</li>
	<li>迭代器模式（Iterator Pattern），提供一种方法循序访问一个聚合对象中的各个元素，而又不暴露其内部的表示。</li>
	<li>组合模式（Composite Pattern），允许你将对象组合成树形结构来表现“整体/部分”层次结构。组合能让客户以一致的方式处理个别对象以及对象组合。</li>
	<li>状态模式（State Pattern ），允许对象在内部状态改变时改变它的行为，对象看起来好像修改了它的类。</li>
	<li>代理模式（Proxy Pattern），为另一个对象提供一个替身或占位符以控制对这个对象的访问。</li>
	<li>复合模式（Compound Pattern ），结合两个或以上的模式，组成一个解决方案，解决一再发生的一般性问题。（PS: 最经典的例子就是MVC）</li>
</ul>

要点: 
一、设计模式入门

<ul>
	<li>知道OO基础，并不足以让你设计良好的OO系统。</li>
	<li>良好的OO设计必须具备可复用、可扩充、可维护三个特性。</li>
	<li>模式可以让我们建造出具有良好OO设计质量的系统。</li>
	<li>模式被认为是历经验证的OO设计经验。</li>
	<li>模式不是代码，而是针对设计问题的通用解决方案。你可把它们应用到特定的应用中。</li>
	<li>模式不是被发明，而是被发现。</li>
	<li>大多数的模式和原则，都着眼于软件变化的主题。</li>
	<li>大多数的模式都允许系统局部改变独立于其他部分。</li>
	<li>我们常把系统中会变化的部分抽出来封装。</li>
	<li>模式让开发人员之间有共享的语言，能够最大化沟通的价值。</li>
</ul>

二、观察者模式

<ul>
	<li>观察者模式定义了对象之间一对多的关系。</li>
	<li>主题（也就是可观察者）用一个共同的接口来更新观察者。</li>
	<li>观察者可观察者之间用松耦合方式结合（loosecoupling），可观察者不知道观察者的细节，只知道观察者实现了观察者接口。</li>
	<li>使用此模式时，你可从被观察者处推（push）或拉（pull）数据（然而，推的方式被认为更“正确”）。</li>
	<li>有多个观察者时，不可以依赖特定的通知次序。</li>
	<li>Java有多种观察者模式的实现，包括了通用的java.util.Observable。</li>
	<li>要注意 java.util.Observable实现上所带来的一些问题。</li>
	<li>如果有必要的话，可以实现自己的Observable，这并不难，不要害怕。</li>
	<li>Swing大量使用观察者模式，许多GUI框架也是如此。</li>
	<li>此模式也被应用在许多地方，例如: JavaBeans、RMI。</li>
</ul>

三、装饰对象

<ul>
	<li>继承属于扩展形式之一，但不见得是达到弹性设计的最佳方式。</li>
	<li>在我们的设计中，应该允许行为可以被扩展，而无须修改现有的代码。</li>
	<li>组合和委托可用于在运行时动态地加上新的行为。</li>
	<li>除了继承，装饰者模式也可以让我们扩展行为。</li>
	<li>装饰者模式意味着一群装饰者类，这些类用来包装具体组件。</li>
	<li>装饰者类反映主被装饰的组件类型（事实上，它们具有相同的类型，都经过接口或继承实现）。</li>
	<li>装饰者可以在被装饰者的行为前面与/或后面加上自己的行为，甚至将被装饰者的行为整个取代掉，而达到特定的目的。</li>
	<li>装饰者一般对组件的客户是透明的，除非客户程序依赖于组件的具体类型。</li>
	<li>装饰者会导致设计中出现许多小对象，如果过度使用，会让程序变得很复杂。</li>
</ul>

四、工厂模式

<ul>
	<li>所以的工厂都是用来封装对象的创建。</li>
	<li>简单工厂，虽然不是真正的设计模式，但仍不失为一个简单的方法，可以将客户程序从具体类解耦。</li>
	<li>工厂方法使用继承: 把对象的创建委托给子类，子类实现工厂方法来创建对象。</li>
	<li>抽象工厂使用对象组合: 对象的创建被实现在工厂接口所暴露出来的方法中。</li>
	<li>所有工厂模式都通过减少应用程序和具体类之间的依赖促进松耦合。</li>
	<li>工厂方法允许类将实例化延迟到子类进行。</li>
	<li>抽象工厂创建相关的对象家族，而不需要依赖他们的具体类。</li>
	<li>依赖倒置原则，指导我们避免依赖具体类型，而要尽量依赖抽象。</li>
	<li>工厂是很有威力的技巧，帮助我们针对抽象编程，而不要针对具体类编程。</li>
</ul>

五、单件模式

<ul>
	<li>单件模式确保程序中一个类最多只有一个实例。</li>
	<li>单件模式也提供访问这个实例的全局点。</li>
	<li>在JAVA中实现单件模式需要私有的构造器，一个静态方法和静态变量。</li>
	<li>确定在性能和资源上的限制，然后小心地选择适当的方案来实现单件，以解决多线程的问题（我们必须认定所有的程序都是多线程的）。</li>
	<li>如果不是采用第五版的JAVA2，双重检查加锁实现会失效。</li>
	<li>小心，你如果使用多个类加载器，两难导致单件失效而产生多个实例。</li>
	<li>如果使用JVM1.2或之前的版本，你必须建立单件注册表，以免收集器将单件回收。</li>
</ul>

六、命令模式

<ul>
	<li>命令模式将发出请求的对象和执行请求的对象解耦。</li>
	<li>在被解耦的两者之间是通过命令对象进行沟通的。命令对象封装了接收者和一个或一组动作。</li>
	<li>调用者通过调用命令对象的execute()发出请求，这会使得接收者的动作被调用。</li>
	<li>调用者可以接受命令当作参数，甚至在运行时动态地进行。</li>
	<li>命令可以支持撤销，做法是实现一个undo()方法来回到execute()被执行前的状态。</li>
	<li>宏命令是命令的一种简单的延伸，允许调用多个命令。宏方法也可以支持撤销。</li>
	<li>实际操作时，很常见使用“聪明”命令对象，也就是直接实现了请求，而不是将工作委托给接收者。</li>
	<li>命令也可以用来实现日志和事务系统。</li>
</ul>

七、适配器模式与外观模式

<ul>
	<li>当需要使用一个现有的类而其接口并不符合你的需要时，就使用适配器。</li>
	<li>当需要简化系统并统一一个很大的接口或者一群复杂的接口时，使用外观。</li>
	<li>适配器改变接口以符合客户的期望。</li>
	<li>外观将客户从一个复杂的子系统中解耦。</li>
	<li>实现一个适配器可能需要一番功夫，也可能不费功夫，视目标接口的大小与复杂度而定。</li>
	<li>实现一个外观，需要将子系统组合进外观中，然后将工作委托给子系统执行。</li>
	<li>适配器模式有两种形式: 对象适配器和类适配器。类适配器需要用到多重继承。</li>
	<li>你可以为一个子系统实现一个以上的外观。</li>
	<li>适配器将一个对象包装起来以改变其接口；装饰者将一个对象包装起来以增加新的行为和责任；而外观将一群对象“包装”起来以简化其接口。</li>
</ul>

八、模板方法模式

<ul>
	<li>“模板方法”定义了算法的步骤，把这些步骤的实现延迟到子类。</li>
	<li>模板方法模式为我们提供了一种代码复用的重要技巧。</li>
	<li>模板方法的抽象类可以定义具体方法、抽象方法和钩子。</li>
	<li>抽象方法由子类实现。</li>
	<li>钩子是一种方法，它在抽象类中不做事，或者只做默认的事情，子类可以选择要不要去覆盖它。</li>
	<li>为了防止子类改变模板方法中的算法，可以将模板方法声明为final。</li>
	<li>好莱坞原则告诉我们，将决策权放在高层模块中，以便决定如何以及何时调用低层模块。</li>
	<li>你将在真实世界代码中看到模板方法模式的许多变体，不要期待它们全都是一眼就可以被你认出的。</li>
	<li>策略模式和模板方法模式都封装算法，一个用组合，一个用继承。</li>
	<li>工厂方法是模板方法的一种特殊版本。</li>
</ul>

九、迭代器与组合模式

<ul>
	<li>迭代器允许访问聚合的元素，而不需要暴露它的内部结构。</li>
	<li>迭代器将遍历聚合的工作封装进一个对象中。</li>
	<li>当使用迭代器的时候，我们依赖聚合提供遍历。</li>
	<li>迭代器提供了一个通用的接口，让我们遍历聚合的项，当我们编码使用聚合的项时，就可以使用多态机制。</li>
	<li>我们应该努力让一个类值分配一个责任。</li>
	<li>组合模式提供一个结构，可同时包容个别对象和组合对象。</li>
	<li>组合模式允许客户对个别对象以及组合对象一视同仁。</li>
	<li>组合结构内的任意对象称为组件，组件可以是组合，也可以是叶节点。</li>
	<li>在实现组合模式时，有许多设计上的折衷。你要根据需要平衡透明性和安全性。</li>
</ul>

十、状态模式

<ul>
	<li>状态模式允许一个对象给予内部状态而拥有不同的行为。</li>
	<li>和程序状态机（PSM）不同，状态模式用类代表状态。</li>
	<li>Context会将行为委托给当前状态对象。</li>
	<li>通过将每个状态封装进一个类，我们把以后需要做的任何改变局部化了。</li>
	<li>状态模式和策略模式有相同的类图，但是它们的意图不同。</li>
	<li>策略模式通常会用行为或算法来配置Context类。</li>
	<li>状态模式允许Context随着状态的改变而改变行为。</li>
	<li>状态转换可以由State类或 Context类控制。</li>
	<li>使用状态模式通常会导致设计中类的数目大量增加。</li>
	<li>状态类可以被多个 Context实例共享。</li>
</ul>

十一、代理模式

<ul>
	<li>代理模式为另一个对象提供代表，以便控制客户对对象的访问，管理访问的方式有许多种。</li>
	<li>远程代理管理客户和远程对象之间的交互。</li>
	<li>虚拟代理控制访问实例化开销大的对象。</li>
	<li>保护代理基于调用者控制对对象方法的访问。</li>
	<li>代理模式有许多变体，例如: 缓存代理、同步代理、防火墙代理和写入时复制代理。</li>
	<li>代理在结构上类似装饰者，但是目的不同。</li>
	<li>装饰者模式为对象加上行为，而代理则是控制访问。</li>
	<li>Java内置的代理支持，可以根据需要建立动态代理，并将所有调用分配到所选的处理器。</li>
	<li>就和其他的包装者（wrapper）一样，代理会造成你的设计中类的数目增加。</li>
</ul>

十二、复合模式

<ul>
	<li>MVC是复合模式，结合了观察者模式、策略模式和组合模式。</li>
	<li>模型使用观察者模式，以便观察者更新，同时保持两者之间解耦。</li>
	<li>控制器是视图的策略，视图可以使用不同的控制器实现，得到不同的行为。</li>
	<li>视图使用组合模式实现用户界面，用户界面通常组合了嵌套的组件，像面板、框架和按钮。</li>
	<li>这些模式携手合作，把MVC模型的三层解耦，这样可以保持设计干净又有弹性。</li>
	<li>适配器模式用来将新的模型适配成已有的视图和控制器。</li>
	<li>Model2是MVC在Web上的应用。</li>
	<li>在Model2中，控制器实现成Servlet，而JSP/HTML实现视图。</li>
</ul>

十三、与设计模式相处

<ul>
	<li>让设计模式自然而然地出现在你的设计中，而不是为了使用而使用。</li>
	<li>设计模式并非僵化的教条: 你可以依据自己的需要采用或调整。</li>
	<li>总是使用满足需要的最简单解决方案，不管它用不用模式。</li>
	<li>学习设计模式的类目，可以帮你自己熟悉这些模式以及它们之间的关系。</li>
	<li>模式的分类（或类目）是将模式分成不同的族群，如果这么做对你有帮助，就采用吧！</li>
	<li>你必须相当专注才能够成为一个模式的作家: 这需要时间也需要耐心，同时还必须乐意做大量的精化工作。</li>
	<li>请牢记: 你所遇到大多数的模式都是现有模式的变体，而非新的模式。</li>
	<li>末能够为你带来的最大好处之一是: 让你的团队拥有共享词汇。</li>
	<li>任何社群都有自己的行话，模式社群也是如此。别让这些行话绊着，在读完本书之后，你已经能够应用大部分的行话了。</li>
</ul>