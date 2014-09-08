---
layout: post
title: CoffeeScript小书
category: 阅读
---
<img class="cover" src="/images/2014/7/9781449321055.jpg" />

ISBN：9781449321055

作者：Alex MacCaw

译者：寸志铁金龙

出版时间：2012-1

评价：☆☆☆☆

适合快速入门。

在无参数调用函数的地方要特别小心，可别忘了加上括号。

你还可以使用参数槽（splats）接收多个参数，使用...表示：

```javascript
sum = (nums...) ->
  result = 0
  nums.forEach (n) -> result += n
  result 
```