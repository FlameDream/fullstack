## Git报错： Failed to connect to github.com port 443 解决方案

今天再上传代码到github上突然就报fatal: unable to access 'https://github.com/xxxx.git/': Failed to connect to github.com port 443 after 75005 ms: Couldn't connect to server的错误。
</br>
这是由于本机系统代理端口和git端口不一致导致的。


## 解决办法：

### 一、查看自己本机系统代理：

打开自己代理软件查看代理的端口号：

![proxy](../source/github_443.png)


### 二、修改git配置：（其中的7890改为你电脑的端口号）

**Window、Linux、Mac系统下配置都一样**

socks5和http两种协议由使用的代理软件决定，不同软件对这两种协议的支持有差异，如果不确定可以都尝试一下

配置socks5代理

```bash
git config --global http.proxy socks5 127.0.0.1:7890
git config --global https.proxy socks5 127.0.0.1:7890

```

配置http代理


```bash

git config --global http.proxy 127.0.0.1:7890
git config --global https.proxy 127.0.0.1:7890

```


### 三、再次push就可以成功上传。


```bash

Enumerating objects: 6, done.
Counting objects: 100% (6/6), done.
Delta compression using up to 8 threads
Compressing objects: 100% (4/4), done.
Writing objects: 100% (4/4), 1.11 KiB | 1.11 MiB/s, done.
Total 4 (delta 1), reused 0 (delta 0), pack-reused 0
remote: Resolving deltas: 100% (1/1), completed with 1 local object.
To https://github.com/xxxx.git
   2100eab..d55efc1  main -> main

```



#### 注意


也可以用一些命令来查看git系统配置代理接口以及取消代理


**查看代理命令**

```bash
git config --global --get http.proxy
git config --global --get https.proxy
```

**取消代理命令**
```bash
git config --global --unset http.proxy
git config --global --unset https.proxy

```








