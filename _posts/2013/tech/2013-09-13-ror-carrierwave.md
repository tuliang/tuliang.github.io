---
layout: post
title: Ruby on Rails CarrierWave 储存远程文件
category: tech
---
Carrierwave的主要功能是用于上传文件或者图片的Gem，功能非常强大。但是官方的[Demo](https://github.com/carrierwaveuploader/carrierwave)和网上的[教程](http://ruby-china.org/topics/4992)大都只介绍使用表单上传文件，并没有讲述如何储存远程文件。

创建uploader

```ruby
rails g uploader Video
```

创建字段存储文件信息

```ruby
rails g migration AddFileToVideos file:string 
```

file字段使用与存储上传文件的地址字段。

然后在Video的model中加入调用carrierwave的信息：

```ruby
class Video < ActiveRecord::Base
  mount_uploader :file, VideoUploader
```

最后在Model中加入upload方法

```ruby
def upload video_url
  self.file.download! video_url
  self.file.store! 
  self.save
end
```

这样我们就完成了储存远程文件的功能。
