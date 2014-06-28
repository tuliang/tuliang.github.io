---
layout: post
title: Heroku Unicorn VS Thin
---
使用Heroku上的[blitz](https://addons.heroku.com/blitz)测试

#### 1个dynos 512MB 下 100 Concurrent Users

thin  

*  average response time: 101

unicorn  

*  average response time: 49


#### 1个dynos*2 1G 下 250 Concurrent Users

thin  

*  average response time: 321  

*  timeouts: 60.82%

unicorn  

*  average response time: 193  

*  timeouts: 27.12%


给页面加上memcachier后

#### 1个dynos 512MB 下 100 Concurrent Users

thin  

*  average response time: 45

unicorn  

*  average response time: 31


#### 1个dynos*2 1G 下 250 Concurrent Users

thin  

*  average response time: 304

*  timeouts: 5.48%

unicorn  

*  average response time: 182

*  timeouts: 2.68%

可以看出unicorn性能是比thin强的，但是对性能提升最大的是memcachier。

在测试过程中发现1个dynos 512MB的unicorn使用3个`worker_processes`是比较好的，使用4个容易使内存溢出。同理，1个dynos*2 1G使用6个`worker_processes`.
