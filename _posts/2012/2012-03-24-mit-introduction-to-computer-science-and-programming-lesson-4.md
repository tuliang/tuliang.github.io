---
layout: post
title: 麻省理工《计算机科学及编程导论》第四课
---
##函数抽象、递归简介

到现在为止，我们学习了赋值语句、条件语句、输入/输出、循环结构以及各种数据类型。我们使用这些就可以称为图灵完全（Turing-complete），也就是说，有了这些以后，就可以写出任何程序了。

农场中有一群猪和一群鸡，有一天农场主看到有x个头和y个脚，求该农场有多少头猪和多少只鸡：

```python
def solve(numLegs, numHeads):
  for numChicks in range(0, numbeads + 1)
    numPigs = numHeads - numChicks
    totLegs = 4*numPigs + 2*numChicks
    if totLegs == numLegs
      return [numPigs, numChicks]
    return [None, None]

def barnYard():
  heads = int(raw_input('Enter number of heads: '))
  legs =  int(raw_input('Enter number of legs: '))
  pigs, chickens = solve(legs, heads)
  if pigs == None:
    print 'There is no solution'
  else:
    print 'Number of pigs:'.pigs
    print 'Number of chickens:'.chickens
```

递归：只要基础情况正确，递归步骤正确，就能将问题简化为更简单的相同问题，最终代码收敛并给出答案。
斐波那契（Fibonacci）数列，给出两个数，后面产生的数都是在自己之前的两个数的和，即`x_3 = x_1 + x_2, x_4 = x_2 + x_3 ...`

```python
def fib(x):
  if x == 0 or x == 1: return 1
  else: return fib(x - 1) + fib(x - 2)
```

