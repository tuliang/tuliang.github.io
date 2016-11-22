---
layout: post
title: Git权威指南
category: read
---
<img src="/images/2013/05/9787111349679-228x300.jpg" alt="9787111349679" width="228" height="300" class="cover" />

ISBN: 9787111349679

作者: 蒋鑫

出版社: 机械工业出版社

出版时间: 2011-6

评价: ☆☆☆☆

我一直读“技特”，原来是错的。（P1）Git正确的发音应该听起来像是“歌易特”。

git的diff命令带上参数后可以对任意版本对比: 

里程碑B和里程碑A比较
`git diff B A`

工作区和里程碑A比较
`git diff A`

暂存区和里程碑A比较
`git diff --cached A`

工作区和暂存区比较
`git diff`

暂存区和HEAD比较
`git diff --cached`

工作区和HEAD比较
`git diff HEAD`

`git commit -a`可以直接提交，而不用放入暂存区中，不建议使用。因为这样就放弃了git暂存区的最大好处: 对提交内容进行控制的能力。

.gitignore设置的文件忽略只对未跟踪有效，对于已加入版本库的文件无效。

后面十几章有些太细节，近期也用不到，选择性的看了一些。
