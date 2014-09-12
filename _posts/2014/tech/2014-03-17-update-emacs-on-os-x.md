---
layout: post
title: update emacs on os x
category: tech
---
最近买了hhkb开始折腾Emacs。

mac自带Emacs，但是版本比较老是Emacs22，Emacs24是现在最新的，有很多新功能，比如原生支持显示行数。

升级参考wikemacs.org：[Installing Emacs on OS X](http://wikemacs.org/index.php/Installing_Emacs_on_OS_X)

使用brew安装emacs

```
brew update  
brew install emacs --cocoa  
ln -s /usr/local/Cellar/emacs/24.3/Emacs.app /Applications  
```

删除mac原生的emacs

```
sudo rm /usr/bin/emacs  
sudo rm -rf /usr/share/emacs  
```

大功告成~
