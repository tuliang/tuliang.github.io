---
title: 了解如何通过 reduce 方法折叠集合
date: 2018-11-02 20:19:16
categories: 后端
tags:
  - Ruby
---
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
