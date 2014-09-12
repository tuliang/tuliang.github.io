---
layout: post
title: IE7下list-style:none无效
category: tech
---
IE7下有时候`list-style:none`无效，我们不能忽略的是,`list-style`: 包含了三个属性:
```css
list-style-type;
list-style-position;
list-style-img;
```
当`list-style:none`无效时，将`list-style-type，list-style-position，list-style-img`都设置为`none`即可。
