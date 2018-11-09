---
title: Docker 中 NGINX 挂载应用的静态文件
date: 2018-11-01 02:10:13
categories: 工具
tags:
  - Docker
  - Docker Compose
  - NGINX
---
在 `Docker` 中 `NGINX` 如何获得应用的静态文件呢？

一般来说这种共享文件的需求，我们需要使用 `volumes`

假如静态文件的地址是 `/home/app/app_name/public`

那么我们在中 `docker-compose.yml` 中设置 `volumes`

```yaml
version: '3'
volumes:  
  public: 
services:  
  app:    
    volumes:      
       - public:/home/app/app_name/public
 
  web:    
    volumes:      
       - public:/home/app/app_name/public
```

记得在 `nginx.conf` 设置 `root`

```nginx
server {  
   # define the public application root  
   root  /home/app/app_name/public; 
}
```

#### 参考文档
- [Compose file version 3 reference](https://docs.docker.com/compose/compose-file/#volumes)
- [Use volumes](https://docs.docker.com/storage/volumes/#start-a-container-with-a-volume)
- [docker-compose volumes_from equivalent with version 3](https://stackoverflow.com/questions/42232051/docker-compose-volumes-from-equivalent-with-version-3)