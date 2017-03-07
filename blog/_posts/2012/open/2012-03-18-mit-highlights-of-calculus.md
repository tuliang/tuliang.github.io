---
layout: post
title: 麻省理工《微积分重点》
category: open
---
课程介绍: 

微积分的介绍，面向高中生和大学新生，主要是一个入门。除了视频，还有幻灯片和实例。本课程的目的是从错综复杂的微积分课本和习题中跳出来，以一种总览（Big Picture）的简洁形式重新审视微积分。
课程第二部分微积分重点之微分学，于2011年MIT新推发布。这部分课程的研究对象是“微积分”中的“微分学”，更深入地挖掘微分和导数的内涵和实质

课程类型: 数学

<img class="cover" title="Gilbert-Strang" alt="Gilbert Strang" src="/images/2012/03/Gilbert-Strang-225x300.jpg" width="225" height="300" />

课程主课人: 吉尔伯特-斯特朗（Gilbert Strang）

吉尔伯特-斯特朗: 1934年11月27日出生，是美国享有盛誉的数学家，在有限元理论、变分法、小波分析及线性代数方面均有所建树。他对教育的贡献 尤为卓著，包括所著有的七部经典数学教材及一部专著。斯特朗自1962年至今担任麻省理工学院教授，其所授课程《线性代数导论》、《计算科学与工程》均在 MIT开放课程软件（MIT OpenCourseWare）中收录，获得广泛好评。

课程简介: 

### 第一部分: 微积分重点

[课程简介 - Gil Strang's Introduction to Highlights of Calculus](#gil-strangs-introduction-to-highlights-of-calculus)

[第 1 课 微积分总览 - Big Picture of Calculus](#big-picture-of-calculus)

[第 2 课 导数总览 - Big Picture: Derivatives](#big-picture-derivatives)

[第 3 课 极值和二阶导数 - Max and Min and Second Derivative](#max-and-min-and-second-derivative)

第 4 课 指数函数 - The Exponential Function

第 5 课 积分总览 - Big Picture: Integrals

### 第二部分: 微分学

第 1 课 sinx和cosx的导数 - Derivative of sin x and cos x

第 2 课 乘法法则和除法法则 - Product Rule and Quotient Rule

第 3 课 复合函数和链式法则 - Chains f(g(x)) and the Chain Rule

第 4 课 极限和连续函数 - Limits and Continuous Functions

第 5 课 逆函数和对数函数 - Inverse Funtions f ^-1 (y) and the Logarithm x = ln y

第 6 课 增长率和对数图 - Growth Rates & Log Graphs

第 7 课 线性近似和牛顿法 - Linear Approximation_Newton's Method

第 8 课 幂级数和欧拉公式 - Power Series_Euler's Great Formula

第 9 课 关于运动的微分方程 - Differential Equations of Motion

第 10 课 关于增长的微分方程 - Differential Equations of Growth

第 11 课 对数函数和反三角函数的导数 - Derivatives of ln y and sin ^-1 (y)

第 12 课 六大函数、六大法则及六大定理 - Six Functions, Six Rules, and Six Theorems

## 笔记

---

### 课程简介 - Gil Strang's Introduction to Highlights of Calculus

这些视频是为了增加和补充课堂和教材中的内容。有时候教材太过厚实，习题也太过繁杂，这很容易让你迷失关键和重点。

第一部分总共有5个视频，“总览”可以很好地形容这部分视频。第二部分有12个视频，论及微分学剩下的部分。

很多学数学或是微积分的人，不管是在高中，还是大学，他们只是简单想了解一下重点，这就是本课程的核心。这些视频不需要任何先修课程，任何人都能观看，哪怕你完全不知微积分为何物。

---

### 第 1 课 微积分总览 - Big Picture of Calculus

微积分是函数一（微分函数）和函数二（积分函数）之间的桥梁，不过是关于两函数之间关系的学科。微积分作用是知道函数一，求函数二或知道函数二，求函数一。两个函数包含的信息的相同的，从而微积分分为微分学和积分学。

设时间为t，初始速度为 $$s = 0$$，加速度为 a，距离为 f，求在时间 t 时的距离 f 的值。

解: 

在时间为 0 时，速度 $$s_0 = 0 + 0 * a$$

在时间为 t 时，速度 $$s_t = 0 + t * a$$

∵距离 f 为时间 0 到时间 t 所有速度的总和  
即
$$f = {(s_0 + s_t) * t}/{2}$$

∴$$f = {at^2}/{2}$$

---

### 第 2 课 导数总览 - Big Picture: Derivatives

微积分中三个重要的函数: 

幕函数 (y = xn) 其导数为 $$dy/dx = nx^{n - 1}$$

三角函数 (y = sin x) 其导数为 $$dy/dx = cos x$$

指数函数 (y = ex) 其导数为 $$dy/dx = e^x$$

平均斜率 = y变化量/x变化量 = △y/△x

求最低点是微积分的一个主要应用。通过斜率为0，可以求出最低点，即最低点的斜率为0。

求 y = x2 的导数。

解: 

<img title="mit-highlights-of-calculus-section-1-lesson-2-1" src="/images/2012/03/mit-highlights-of-calculus-section-1-lesson-2-1.gif" alt="" width="245" height="108" />

∵ dy/dx = 极小下的△y/△x

即在极小情况下

△x = 0

∴ y = x2 的导数为2x

---

### 第 3 课 极值和二阶导数 - Max and Min and Second Derivative

1. 二阶导数: 导数的导数（The Second Derivative The derivative of the derivative）
2. 二阶导数的例子（Examples of Second Derivatives）
3. 凸函数和凹函数（Convex and Concave Curves）
4. 寻找极值点和拐点（Locating the Maximum and Minimum and the Infection Point）
5. 应用: 上班的最短时间（求最小值）（Application: Driving to Work Finding the Minimum time）

国外统一定义 $$f'' > 0$$ 为凸，表示向上弯曲；相对的凹为 $$f'' < 0$$

拐点（inflection point）是弯曲的方向发生了变化，二阶导数在这一点变号。它就是二阶导数为0的点（Inflecion Point: Where the second derivative is zero），即 $$y'' = 0$$ 下x的值。

链式法则（chain rule）,对于求复合函数的导数来说相当有用。以后会有关于链式法则的讨论。

---

### 第 4 课 指数函数 - The Exponential Function