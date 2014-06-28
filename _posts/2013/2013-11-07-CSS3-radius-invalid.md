---
layout: post
title: CSS3 圆角 无效
---
今天在做页面的时候遇到CSS3圆角无效的情况，实例代码：

```html
<style type="text/css">
  .category-menu {
    -webkit-border-radius: 14px;
    -moz-border-radius: 14px;
    border-radius: 14px;
  }

  .category {
    background: #fff;
  }
</style>
<div class="category-menu">
  <div class="category">
    <a href="featured">Featured</a>
  </div>
  <div class="category">
    <a href="rated">Highest Rated</a>
  </div>
  <div class="category">
    <a href="newest">Newest Videos</a>
  </div>
</div>
```

<img src="/images/2013/11/QQ20131107-1.png" />  

你会发现圆角居然没有出现！让我们加上边框看看发生了什么：

```css
.category-menu {
  border: 3px solid #BADA55;
}
```

<img src="/images/2013/11/QQ20131107-2.png" />

仔细观察可以发现，圆角被类为category的div所设置背景挡住了。将`background: #fff;`注释，我们看到了圆角

<img src="/images/2013/11/QQ20131107-3.png" />

从此可以得出结论，CSS3的圆角会被子元素的背景遮挡，从而产生圆角无效的假象。

问题找到了，但是如果要求鼠标移上类为category的div时，相应的div背景变色，那怎么办呢？

天无绝人之路，只要给第一个设置左上和右上圆角，最后一个div设置左下和右下圆角，就可以完美解决这个问题了。

```html
<style type="text/css">
  .category {
    background: #fff;
  }

  .category:hover {
    background: #ff6633;
  }

  .first {
    -webkit-border-radius: 4px 4px 0 0;
    -moz-border-radius: 4px 4px 0 0;
    border-radius: 4px 4px 0 0;
  }

  .last {
    -webkit-border-radius: 0 0 4px 4px;
    -moz-border-radius: 0 0 4px 4px;
    border-radius: 0 0 4px 4px;
  }
</style>
<div class="category-menu">
  <div class="category first">
    <a href="featured">Featured</a>
  </div>
  <div class="category">
    <a href="rated">Highest Rated</a>
  </div>
  <div class="category last">
    <a href="newest">Newest Videos</a>
  </div>
</div>
```
