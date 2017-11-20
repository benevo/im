---
title: nPlayer + WebDAV + 华硕RT-AC66U B1 + 穿墙访问局域网内所有主机共享目录
date: 2017-11-11 21:22:15
tags:
---



> nPlayer，应该是 iOS 下最流行的文件查看、播放的软件吧， 不仅可在局域网内使用，还可以借助frp穿墙软件 在外网访问内网主机上的文件。 
本文只介绍如何实现外网访问的部分，内网部分就不不必多说。目前，AppStore 上 售价好像是 30 RMB 吧，比起之前 256 的价格实在是哈哈哈。


## 环境准备


1. 一台 华硕 RT-AC66U B1路由： 安装有 Merlin 380.67_X7.6 （百度网盘）
路由： 192.168.50.1

2. 一台 NAS 机器： VMware 方式安装，版本 DSM 6.0.xx (百度网盘)
IP： 192.168.50.101

3. 一个可用的域名，比如： myfrps.com（如果你有公网ip，可用不用）

---

## 配置

### 路由配置

1. 内网登录路由，启用 AiCloud “ 智能访问 “ 服务，如下：
![启用“ 智能访问”](http://upload-images.jianshu.io/upload_images/1332969-f56675ffd93fc039.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)


2. 路由 DDNS 配置

![没有公网ip。。](http://upload-images.jianshu.io/upload_images/1332969-e39fa931d5b09731.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

如果你有公网ip，可以用华为提供的DDNS免费FQDN，可以跳过这步。


本人是 CM 网络，没有公网ip。。。路由的外网地址解析 用的是VPS+frp服务，具体可以参考： VPS + frp 穿墙实战

具体 提一下， frpc 的配置文件设置：

```
[ac66u.home.ddns]
type = https
local_ip = 192.168.50.1
local_port = 443
use_encryption = false
use_compression = false
custom_domains = ac66u.home.myfrps.com
locations = /,/pic
```

注： 协议是 https，因为这是Aicloud web服务的默认协议， 端口默认 443， 其他不管。

路由后台允许frpc以后，在web浏览器输入 ： https://ac66u.home.myfrps.com

看看是否能够顺利出现AiCloud的登录页面，如下：
![2017-11-11_22-08-40.png](http://upload-images.jianshu.io/upload_images/1332969-4b0c616b417630f7.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

填入路由登录用户名和密码，看看内网在线的机器有多少。 我的情况是这样的，如下：

![2017-11-11_22-09-08.png](http://upload-images.jianshu.io/upload_images/1332969-46ab265fbf1cd0d0.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)


哈哈， 发现了一台 NAS 主机 DSM6，还有一台我是我正在码字用的笔记本。。。


然后. 手机上安装 AiCloud 套件，运行，填入 DDNS 地址、路由登录用户名、密码，连接成功后，看是否能发现内网主机，我的情况如下：
![](http://upload-images.jianshu.io/upload_images/1332969-0fffe7016a667e09.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

与web访问的结果一样的。



### nPlayer 设置

在 网络 页， 新建 ”WebDAV 服务“。

![新建 ”WebDAV 服务](http://upload-images.jianshu.io/upload_images/1332969-f12843cc6a43b916.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)


主机： 填入 DDNS
用户： 路由登录用户
密码： 路由登录密码
密码锁： 可启用，也可不启用

端口： （空）
路径： （空）
HTTPS： 启用

保存，然后进入试试。

Good luck ！


我的登录情况：


![](http://upload-images.jianshu.io/upload_images/1332969-e4ecccc0b7f5b6b2.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)



--The End.--






