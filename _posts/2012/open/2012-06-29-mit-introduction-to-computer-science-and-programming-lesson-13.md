---
layout: post
title: 麻省理工《计算机科学及编程导论》第十三课
category: open
---
##动态规划：重复子问题、最优子结构

斐波那契数列

```python
def fib(n):
  global numCalls
  numCalls +=1
  #print 'fib调用', n
  if n<=1:
    return 1
  else:
    return fib(n-1)+fib(n-2)
numCalls = 0
n = 6
res = fib(n)
print 'fib_', n, '=', res, '调用次数为', numCalls

def fastFib(n, memo):
  global numCalls
  numCalls +=1
  #print 'fib1调用', n
  if not n in memo:
    memo[n]=fastFib(n-1, memo) + fastFib(n-2, memo)
  return memo[n]

def fib1(n):
  memo = {0:1, 1:1}
  return fastFib(n, memo)

numCalls = 0
n = 6
res = fib1(n)
print 'fib_', n, '=', res, '调用次数为', numCalls
```

我们看到加上memo这个缓存后，算法的复杂度减少了不少，根本原因就是我们找到重叠子问题，并且将结果缓存起来，避免重复计算。整个算法的的核心就是：

```python
#如果memo中不存在斐波那契数列的第n个数
#则计算该数
if not n in memo:
  memo[n]=fastFib(n-1, memo) + fastFib(n-2, memo)
#如果存在就直接返回该数
return memo[n]
```

把之前解决了的问题作为数据储存起来。依赖表查找查询之前数据，而缓存法是一种特殊情况。表查找是一种常见的方式，当你解决复杂的问题时，保存答案然后供以后使用。看到算法刚开始时间复杂度是1700万，增加缓存后变为1800，是相当令人震惊的。缓存这种方法其实就是我们常说的空间换时间。
