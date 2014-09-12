---
layout: post
title: ImageMagick
category: tech
---
之前一直用Google PageSpeed来压缩图片，手动压缩图片效率实在太慢，后来发现[ImageMagick](http://hooopo.writings.io/articles/5-generate-progressive-jpeg-with-carrierwave-and-mini-magick)好像不错就尝试了一下。

[image_optim](https://github.com/toy/image_optim) 是一个Ruby的gem。

我们首先安装这个gem

```ruby
gem install image_optim
```

然后安装依赖（[Linux请参考官方说明](https://github.com/toy/image_optim)）

```ruby
brew install advancecomp gifsicle jpegoptim jpeg optipng pngcrush
```

如果你缺少XQuartz，需要去[下载](http://xquartz.macosforge.org/landing/)安装。

安装完毕后，我们就可以尝试运行了。

使用方法非常简单，并且可以看到每个图片优化的大小。

<img src="/images/2013/07/20130723-1.png" />

运行`image_optim`命令将blog下的图片进行优化：

```ruby
image_optim -r images/*
```

如果报出类似这种错误：

```ruby
image_optim.rb:187:in `resolve_bin!': `pngout` not found (ImageOptim::BinNotFoundError)
```

其实是你缺少pngout，需要去[下载](http://www.jonof.id.au/kenutils)，然后将pngout放到/user/bin/目录下。
