---
title: Mac 更新 Emacs
date: 2014-03-17 21:55:11
categories: 工具
tags:
  - Emacs
---
最近买了 `hhkb` 开始折腾 `Emacs`。

`Mac` 自带 `Emacs`，但是版本比较老是 `Emacs22`，`Emacs24` 是现在最新的，有很多新功能，比如原生支持显示行数。

升级参考 wikemacs.org: [Installing Emacs on OS X](http://wikemacs.org/index.php/Installing_Emacs_on_OS_X)

使用 `brew` 安装 `emacs`

```sh
brew update  
brew install emacs --cocoa  
ln -s /usr/local/Cellar/emacs/24.3/Emacs.app /Applications  
```

删除 `Mac` 原生的 `Emacs`

```sh
sudo rm /usr/bin/emacs  
sudo rm -rf /usr/share/emacs  
```

大功告成~