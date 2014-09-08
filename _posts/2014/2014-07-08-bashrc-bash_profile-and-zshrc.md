---
layout: post
title: ".bashrc、.bash_profile 和.zshrc"
---
在Mac系统中, 我们通过编辑`.bashrc`和`.bash_profile`来设置用户的工作环境, 很多文章对它们进行修改。

最近使用的时候发现编辑文件后，并不起效，查资料后发现`因为如果是 sh 或者其他 shell 显然不会运行 bashrc 的.`

突然记起来我用了[oh-my-zsh](https://github.com/robbyrussell/oh-my-zsh)，检查根目录，果然有一个文件叫`.zshrc`，赶紧将设置纷纷移到里面，整个世界仿佛瞬间变得美好了。

参考资料：[https://wido.me/sunteya/understand-bashrc-and-profile](https://wido.me/sunteya/understand-bashrc-and-profile)