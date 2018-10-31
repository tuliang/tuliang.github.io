---
title: 推荐使用 Struct 而非 Hash 存储结构化数据
date: 2018-10-31 16:21:14
categories: 后端
tags:
  - Ruby
---
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