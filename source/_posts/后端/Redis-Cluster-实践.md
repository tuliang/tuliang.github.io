---
title: Redis Cluster 实践
date: 2019-01-17 20:01:03
categories: 后端
tags:
  - Ruby
  - Redis
---
# Redis Cluster 实践

## 背景

[redis](https://github.com/redis/redis-rb) 这个 gem 在最新的 4.1 版中开始支持 Redis Cluster。

### 开发环境

我们需要在开发环境搭建一个 Redis Cluster，最方便快捷的方法是使用 docker 和 docker-compose，并且使用配置好的 image。

在 docker-compose.yml 中添加下列代码

```yml
version: '3'
services:
  redis-cluster:
    image: grokzen/redis-cluster
    environment:
     - IP=0.0.0.0
    ports:
      - '7000-7007:7000-7007'
```

使用 `docker-compose up -d` 启动服务即可。

### 更新代码

在 Gemfile 中设置 redis gem 的版本为 4.1

```ruby
gem "redis", "~> 4.1"
```

在 application.rb 中修改 session_store 和 cache_store

```ruby
Rails.application.configure do
  # Redis Session Store (redis-rails Gem)
  config.session_store :redis_store, servers: { cluster: %w[redis://127.0.0.1:7000] }, expires_in: 1.month

  # Redis Cache Store (redis-rails Gem)
  config.cache_store = :redis_store, { cluster: %w[redis://127.0.0.1:7000] }

  # Redis Cache Store (ActiveSupport)
  config.cache_store = :redis_cache_store, { cluster: %w[redis://127.0.0.1:7000] }
end
```

在其他地方使用 Redis Cluster

```ruby
redis = Redis.new(cluster: %w[redis://127.0.0.1:7000])
```

### 分片

从单机变成集群之后，数据分片了，分散到不同机器，但是实际需求要求相关联的 `key` 分配到相同机器。

因为业务或者性能问题，我们会使用 Redis 的 pipelined、multi 和 Rails.cache.read_multi，这些场景下都需要 `key` 分配到相同机器。

但是 Redis Cluster 的分片方案是服务端提供分片，规则不是客户端控制的。

针对这些场景 Redis Cluster 提供了 [Keys hash tags](https://redis.io/topics/cluster-spec#keys-hash-tags) 的功能，简单来说是：

> 当一个 key 包含 {} 的时候，就不对整个 key 做 hash，而仅对 {} 包括的字符串做 hash。

```ruby
redis = Redis.new(cluster: %w[redis://127.0.0.1:7000])

redis.mget('key1', 'key2')
#=> Redis::CommandError (CROSSSLOT Keys in request don't hash to the same slot)

redis.mget('{key}1', '{key}2')
#=> [nil, nil]
```

### 总结

本文只是一个简单的例子，不能在生产环境中直接使用。

在生产环境需要考虑 Redis 的各个客户端，同时要考虑数据迁移和兼容的问题，升级到 Redis Cluster 要非常谨慎和细心。

### 参考资料：

- [Cluster mode](https://github.com/redis/redis-rb/wiki/Cluster-mode)
- [Grokzen/docker-redis-cluster](https://github.com/Grokzen/docker-redis-cluster)
- [RubyのRedis Client LibraryをCluster Modeに対応させた話](https://made.livesense.co.jp/entry/2018/10/17/135245)
- [Add Redis Cluster support](https://github.com/redis/redis-rb/pull/716)
- [Redis技巧:分片技术和Hash Tag](http://blog.text.wiki/2015/09/20/redis-hash-tag.html)
