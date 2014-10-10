---
layout: post
title: Ruby on Rails 两个Model有多种多对多关联
category: tech
---
两个Model进行关联在Rails中是很常见的。一对一、多对多和一对多，都非常简单。有时候Model之间会有多种关联，比如某种岗位会有必要的要求，也有一些加分项。这个时候就是两种多对多的关联了，研究了一下Rails的关联机制，可以发现：利用`:source`和`:through`是可以实现这种需求的。

例如，我们有`career`和`educational_path`两个Model，对它们要进行两种多对多的关联，可以这么做：

首先我们创立`required_educational_paths`和`recommended_educational_paths`这两个Model来支持这两种关联。

它们两个的数据结构是一样的：

{% highlight ruby %}
t.integer "career_id"
t.integer "educational_path_id"
{% endhighlight %}

Model中的代码也是相同的：

{% highlight ruby %}
attr_accessible :career_id, :educational_path_id
belongs_to :career
belongs_to :educational_path
{% endhighlight %}

然后在`career`这个Model中加上

{% highlight ruby %}
has_many :required_educational_paths
has_many :required_educationals, :source => 'educational_path', 
  :through => :required_educational_paths
attr_accessible :required_educationals, :required_educational_ids

has_many :recommended_educational_paths
has_many :recommended_educationals, :source => 'educational_path', 
  :through => :recommended_educational_paths
attr_accessible :recommended_educationals, :recommended_educational_ids
{% endhighlight %}

可以看到我们使用了`required_educationals`和`recommended_educationals`两个虚拟的Model来让`career`关联`educational_path`，同时它们通过之前建立的`required_educational_paths`和`recommended_educational_paths`保存关联的数据。

同理，在`educational_path`这个Model中加上

{% highlight ruby %}
has_many :required_educational_paths
has_many :required_careers, :source => 'careers', 
  :through => :required_educational_paths
attr_accessible :required_careers, :required_career_ids

has_many :recommended_educational_paths
has_many :recommended_careers, :source => 'careers', 
  :through => :recommended_educational_paths
attr_accessible :recommended_careers, :recommended_career_ids
{% endhighlight %}

到此为止整个关联就算是完成了。使用起来也是非常的简单。你可以使用`career.required_educationals`和`career.recommended_educationals` 或者 `career.required_educational_ids`和`career.recommended_educational_ids`，同理在`educational_path`也可以使用这两种不同的关联。