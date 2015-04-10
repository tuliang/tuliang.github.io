---
layout: post
title: ruby thread pool
category: tech
---
有时候会遇到一个情况需要在多个远程服务获取数据。例如服务 a 需要 2 秒，服务 b 需要 5 秒，按照正常处理总共就需要 2+5 总共 7 秒了。如果 a 和 b 之间并没有相互依赖关系，我们可以使用 thread pool 来并发获取数据，将总体耗时由 a + b 变为 a、b两者中的最大值。

{% highlight ruby %}
require 'thread/pool'
require 'thread/future'
require 'benchmark'

def a
  sleep 2
  'a'
end

def b
  sleep 5
  'b'
end

Benchmark.bmbm do |x|
  x.report("normal") { 
    puts "#{a}#{b}"
  }
  x.report("Thread.future")  { 
    pool = Thread.pool 2
    f1 = pool.future {
      a
    }
    f2 = pool.future {
      b
    }
    puts "#{~f1}#{~f2}"
  }
end
{% endhighlight %}

使用 Benchmark 对比，和我们设想的完全一样。

```shell
Rehearsal -------------------------------------------------
normal        ab
  0.000000   0.000000   0.000000 (  7.010414)
Thread.future ab
  0.000000   0.000000   0.000000 (  5.002781)
---------------------------------------- total: 0.000000sec

                    user     system      total        real
normal        ab
  0.000000   0.000000   0.000000 (  7.004402)
Thread.future ab
  0.000000   0.000000   0.000000 (  5.003263)
```