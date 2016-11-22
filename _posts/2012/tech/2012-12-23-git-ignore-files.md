---
layout: post
title: Git文件忽略
category: tech
---
使用git时，经常需要忽略一些文件，比如一些IDE生成的配置文件
在项目目录加上“.gitignore”文件

然后加入需要忽略文件的文件名就可以了

例如: 

```
.project

.gitignore
```

需要注意的一个问题是，需要在“.gitignore”文件中忽略自己，不然就将“.gitignore”文件提交上去了。
