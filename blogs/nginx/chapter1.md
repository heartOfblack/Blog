---
title: Nginx配置localhost到github page
date: 2021-7-27
categories:
 - Nginx
---

> 旨在了解nginx基本配置和原理



1. 下载和安装nginx

>官方下载好以后启动nginx，以下为基础的指令
>
>start nginx.exe #启动nginx
>
>nginx -s stop //停止
>
>nginx -s reload //重新加载，改动配置文件后使用， 如果不起作用，先杀掉nginx进程再启动



2. 配置本地localhost代理到github page 完整路径：https://heartofblack.github.io/Blog/

```nginx
#配置
server {
        listen       80;
        server_name  localhost;
			
        location /Blog/ { #location 后面为匹配规则,
			proxy_pass https://heartofblack.github.io; #要代理到的服务器
        }
}
```



