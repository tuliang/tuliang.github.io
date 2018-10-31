---
layout: post
title: Ruby on Rails config.cache_store
category: tech
---
`config.cache_store` 配置Rails缓存要使用什么缓存存储. 可选 

*  `:memory_store`
*  `:file_store`
*  `:mem_cache_store` 

其中一个, 有或者是实现了缓存API的一个对象.

如果目录 `tmp/cache` 存在则默认是 `:file_store`, 否则是 `:memory_store`.

更多参数参看: <a href="http://guides.ruby-china.org/configuring.html" target="_blank">配置 Rails 应用程序</a>
