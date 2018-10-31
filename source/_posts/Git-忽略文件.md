---
title: Git 忽略文件
date: 2012-12-23 17:27:55
categories: 工具
tags:
  - Git
---
使用 `git` 时，经常需要忽略一些文件，比如一些 `IDE` 生成的配置文件
在项目目录加上 `.gitignore` 文件
然后加入需要忽略文件的文件名就可以了

```
.project
```

需要注意的是，如果需要忽略 `.gitignore` 文件，那么文件中就要加上 `.gitignore`

```
.project
.gitignore
```