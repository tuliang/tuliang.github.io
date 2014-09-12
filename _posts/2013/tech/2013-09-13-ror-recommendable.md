---
layout: post
title: Ruby on Rails recommendable
category: tech
---
Rails的推荐系统中recommendable算是比较好的一个。

gem：

```
https://github.com/davidcelis/recommendable
```

demo：

```
https://github.com/tka/recommender-demo
```

###安装 Redis：

  Mac OS X下：

  ```
  brew install redis
  ```

  Linux下：

  ```
  sudo apt-get install redis-server
  ```

在Gemfile中加入：

```ruby
gem 'sidekiq'
gem 'recommendable'
```

安装gem

```
bundle install
```

新增`config/initializers/recommendable.rb`

```ruby
require 'redis'

Recommendable.configure do |config|
  # Recommendable's connection to Redis.
  #
  # Default: localhost:6379/0
  config.redis = Redis.new(:host => 'localhost', :port => 6379, :db => 0)

  # A prefix for all keys Recommendable uses.
  #
  # Default: recommendable
  config.redis_namespace = :recommendable

  # Whether or not to automatically enqueue users to have their recommendations
  # refreshed after they like/dislike an item.
  #
  # Default: true
  config.auto_enqueue = true

  # The number of nearest neighbors (k-NN) to check when updating
  # recommendations for a user. Set to `nil` if you want to check all
  # neighbors as opposed to a subset of the nearest ones. Set this to a lower
  # number to improve Redis memory usage.
  #
  # Default: nil
  config.nearest_neighbors = nil

  # Like kNN, but also uses some number of most dissimilar users when
  # updating recommendations for a user. Because, hey, disagreements are
  # just as important as agreements, right? If `nearest_neighbors` is set to
  # `nil`, this configuration is ignored. Set this to a lower number
  # to improve Redis memory usage.
  #
  # Default: nil
  config.furthest_neighbors = nil

  # The number of recommendations to store per user. Set this to a lower
  # number to improve Redis memory usage.
  #
  # Default: 100
  config.recommendations_to_store = 100
end
```

在你的model中加入类似这种代码：

```ruby
class Video < ActiveRecord::Base
  recommends :video_tags, :career

  # ...
end
```

启动顺序：

```
redis-server
sidekiq -q recommendable
```

编写命令：

```ruby
task :videos_to_recommendable => :environment do
  Video.last(10).each do |v|
    puts "video: #{v.id}"

    v.like(v.career)

    v.video_tags.each do |video_tag|
      v.like(video_tag)
    end
  end
end
```

执行命令：

```ruby
rake videos_to_recommendable
```