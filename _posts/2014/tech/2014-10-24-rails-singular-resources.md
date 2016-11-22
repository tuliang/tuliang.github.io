---
layout: post
title: Rails Singular Resources
category: tech
---
Rails 中 Controller 如果不是复数，写 path 或 url 的时候就必须加上 index，这样看上去就很 low。

{% highlight ruby %}
resources :photo do  
  collection do    
    get 'search'  
  end
end

search_photo_index GET    /photo/search(.:format)
{% endhighlight %}

我们去查看 [参考文档](http://guides.rubyonrails.org/routing.html#singular-resources)，发现可以这样做: 

{% highlight ruby %}
resource :photo, controller: photo do  
  collection do    
    get 'search'  
  end
end

search_photo GET    /photo/search(.:format)
{% endhighlight %}

需要注意的是经过这样修改后，访问 /photo 不再调用 index action 而是调用 show action。