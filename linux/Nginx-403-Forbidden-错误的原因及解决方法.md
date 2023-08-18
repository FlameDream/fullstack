---
title: Nginx 403 Forbidden 错误的原因及解决方法
date: 2022-12-15 22:43:11
tags: Nginx
categories: Nginx
about:
---


### 前言

在开发后台开发部署过程中，经常会遇到nginx访问报403的错误（HTTP状态码403：访问请求没有权限）。Nginx 403 Forbidden错误的处理方法在网上基本上很多，网上大部分都可归纳出来4种常见的错误原因造成的，除了这几种错误之外也存在其他原因。



### 一、常见的4种错误和解决办法

##### 1.权限问题，nginx没有配置Web目录的操作权限，出现403
解决办法: 修改当前配置web目录的读写权限（或者是把nginx的启用用户改成目录的所属用户）。重启Nginx即可解决

```bash

chmod -R 755 / var/www   # 给web目录授权


```


##### 2.nginx配置web目录错误（缺少index.html或者index.php 文件）

很多时候可能是由于Web路径配置错误，或者Web路径下缺少index.html,造成出现403错误。
```bash

server
    {
        listen 80 default_server reuseport;
        #listen [::]:80 default_server ipv6only=on;
        server_name localhost;
        index index.html index.htm index.php;
        root  /var/www/;
     }

```


##### 3.SELinux设置为开启状态（enabled）的原因

SELinux是对Linux做了一层安全保护

查看本机SELinux的开启状态，如果SELinux status参数为enabled就是开启中。

```bash
# 第一种方法：

/usr/sbin/sestatus -v    

# 或者
# 
# 第二种方法 使用命令getenforce检查

getenforce

```

关闭SELinux

**1）临时关闭（不用重启）**

```bash
setenforce  0

```

**2)永久关闭（需要重启）**
修改配置文件/etc/selinux/config,将SELinux=enforcing改成SELinux=disable
```bash

vi /etc/selinux/config
 

#SELINUX=enforcing

SELINUX=disabled

```

重启服务器生效
```bash

reboot

```

##### 4.启动用户和nginx工作用户不一致所致（nginx配置的可能是nobody）

1.查看nginx的启动用户 (nginx正在响应http请求的的用户)

```bash

ps aux | grep "nginx: worker process" | awk '{print $1}'

# ps aux | grep "nginx: worker process" | awk  '{print $1}'
www
www
root

```
发现nginx工作的是www 这个用户，可以使用 "cat /etc/passwd" 查看系统中的用户。

2.修改nginx服务配置的nginx.conf文件中的user对用的用户改成www，修改后重启nginx


nginx.conf 文件的修改
 ```bash

user  www www;

worker_processes auto;
worker_cpu_affinity auto;

error_log  /home/wwwlogs/nginx_error.log  crit;

pid        /usr/local/nginx/logs/nginx.pid;

#Specifies the value for maximum file descriptors that can be opened by this process.
worker_rlimit_nofile 51200;

```


重启nginx

```bash
vim /etc/nginx/nginx.conf
nginx -t

# nginx检测结果
#nginx: the configuration file /etc/nginx/nginx.conf syntax is ok
#nginx: configuration file /etc/nginx/nginx.conf test is successful
nginx -s reload    #重启nginx

```

### 二、不常见的问题

##### 1.偶发性出现Nginx 403 Forbidden问题

**1）worker_processes配置和内核数不一致造成的**

nginx.conf文件中，worker_processes默认是1，而内核数却大于1，可以直接配置和内核数一致或者设置成：auto

```bash

worker_processes auto;
worker_cpu_affinity auto;
```

**2）nginx启动的用户数和内核数不一致造成的**

查看系统运行的nginx有几个，和内核数目进行对比，如果大于内核数目，重启系统就可以解决这个问题。





### 补充内容

在查看nginx运行的过程中，我们发现root上是nginx: master process，而www却是：nginx: worker process。
```bash
ps aux | grep nginx

#
#root       967  0.0  0.2  65996 10064 ?        Ss   12月15   0:00 nginx: master process /usr/local/nginx/sbin/nginx -c /usr/local/nginx/conf/nginx.conf
#www        970  0.0  1.0 124064 42156 ?        S    12月15   0:00 nginx: worker process
#www        971  0.0  1.0 124064 40332 ?        S    12月15   0:00 nginx: worker process

```

nginx: master process其实是一个开启nginx的主线，而真正执行nginx分发的却是www（nginx: worker process）








