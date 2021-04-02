---
title: Linux代码部署
date: 2021-03-31 16:00
comments: true
tags:
    - linux
    - docker
---

> 记录代码部署
<!-- more -->

### docker部署nginx

1. 首先需要先创建挂载的文件
~/docker/nginx/conf/nginx.conf -> /etc/nginx/nginx.conf 对应nginx配置文件入口，nginx文件内容如下
```nginx
user  nginx;
# 工作进程数 缺省为1； CPU核心数，(双核4线程，可以设置为4)
# worker_processes  1;
error_log  /var/log/nginx/error.log warn;
pid        /var/run/nginx.pid;
events {
  worker_connections  1024;
}

http {
  include            /etc/nginx/mime.types;
  default_type       application/octet-stream;
  log_format         main  '$remote_addr - $remote_user [$time_local] "$request" '
                           '$status $body_bytes_sent "$http_referer" '
                           '"$http_user_agent" "$http_x_forwarded_for"';
  access_log         /var/log/nginx/access.log  main;
  sendfile           on;
  keepalive_timeout  65;

  gzip on;

  gzip_vary on;
  gzip_proxied any;
  gzip_comp_level 6;
  gzip_buffers 16 8k;
  gzip_http_version 1.1;
  gzip_types text/plain text/css application/json application/javascript text/xml application/xml application/xml+rss text/javascript;

  # 会扫描/etc/nginx/conf.d/文件夹下面所有的配置文件
  include            /etc/nginx/conf.d/*.conf;
}
```

~/docker/nginx/conf.d -> /etc/nginx/conf.d 对应nginx配置文件，docker/nginx/conf.d下包含default.conf文件，文件内容如下
```nginx
server {
    listen       80;
    # localhost 在发布时修改成对应的域名
    server_name  localhost;

    #charset koi8-r;
    #access_log  /var/log/nginx/host.access.log  main;

    root /home/www;

    location / {
        index  index.html index.htm;
    }
    # 反向代理配置，此配置可实现跨域，后端负载均衡等需求
    location /api {
        proxy_pass http://127.0.0.1:7001;
        # access_log "logs/test.log";
    }
}
```
~www -> /home/www 作为程序入口映射，静态文件都放入www文件夹下

2. 执行shell脚本文件，shell脚本内容如下

```nginx
#!/usr/bin/sh
docker stop uxup-nginx
docker rm -f uxup-nginx
docker run --name uxup-nginx -d -p 80:80 -p 443:443 \
-v ~/docker/nginx/conf/nginx.conf:/etc/nginx/nginx.conf \
-v ~/docker/nginx/conf.d:/etc/nginx/conf.d \
-v ~/docker/nginx/log:/var/log/nginx \
-v ~/www:/home/www \
nginx
```
linux 执行shell脚本命令
> sh nginx.sh

<font color="red">注意事项</font>
当nginx容器代理宿主环境的服务器时，需要使用 upstream 模块，示例如下
```nginx
# Docker默认使用的网桥 docker0 的网段是 172.17.0.1
upstream test {
    server 172.17.0.1:6001;
}

server {
    location /api/ {
        proxy_pass http://test;
    }
}
```

### docker部署mysql
shell脚本文件
```nginx
#!/usr/bin/sh
docker stop uxup-mysql
docker rm -f uxup-mysql
docker run --name uxup-mysql -d -p 3306:3306 -e MYSQL_ROOT_PASSWORD=123456 \
-v ~/docker/mysql/conf/my.cnf:/etc/mysql/my.cnf \
-v ~/docker/mysql/conf.d:/etc/mysql/conf.d \
-v ~/docker/mysql/data:/var/lib/mysql \
mysql
```

### docker部署node项目
dockerfile文件参考
```docker
# 设置基础镜像,如果本地没有该镜像，会从Docker.io服务器pull镜像
FROM node:14.4.0

# 这个是容器中的文件目录
RUN mkdir -p /usr/src/app 

# 设置工作目录
WORKDIR /usr/src/app

# 拷贝所有源代码到工作目
COPY . /usr/src/app

# 安装npm依赖(使用淘宝的镜像源)
RUN npm i --production

# 挂载数据卷
VOLUME ["/usr/src/app/logs", "/usr/src/app/resource"]

# 暴露容器端口
EXPOSE 6001

CMD npm run start:docker
```
