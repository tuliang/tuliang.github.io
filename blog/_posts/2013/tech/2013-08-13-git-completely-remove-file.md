---
layout: post
title: Git彻底删除文件
category: tech
---
一般git删除文件使用`git rm`就可以了，但是有时候会产生一些文件你甚至不想让它出现在git的log中。github有[一篇文章](https://help.github.com/articles/remove-sensitive-data)详细说明了如何操作，经过尝试是可以成功将文件彻底删除，在log中都找不到。

比如删除根目录下的file文件夹彻底删除: 

`git filter-branch --force --index-filter \
  'git rm -rf -r --cached --ignore-unmatch file' \
  --prune-empty --tag-name-filter cat -- --all`

然后: 

`git push origin master --force`

这样git仓库中这个文件夹就被彻底删除了。

如果你还想清除本地的一些缓存，可以依次进行下面几部操作: 

`rm -rf .git/refs/original/`

`git reflog expire --expire=now --all`

`git gc --prune=now`

`git gc --aggressive --prune=now`