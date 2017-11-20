---
title: OS X共享，LINUX挂载
date: 2017-11-11 13:19:07
tags: OS X, Linux, 共享，挂载
---


> 由于家里有一台MAC，作为HDTC中心角色，7*24小时运行。本意是将其某些目录共享到家庭内网，供其它机器（虚拟机、路由、NAS等）读写。

本文采用了是NFS共享方式，将OS X 下需共享的目录导出，由DSM5（群晖NAS）和AC66U_B1（华硕路由）进行挂载，以下是具体操作说明

## 媒体中心配置：
- MAC OS X 版本： 10.11.6
- IP地址： 192.168.10.100
- 用户及HOSTNAME： yoona@imac-home

## DSM5 配置：
- LINUX开发版本：Linux DSM5 3.2.40
- IP地址：192.168.10.106
- 用户及HOSTNAME： admin@DSM5

## AC66U_B1:
- LINUX开发版本：Merlin 7.6

---

## OS X + NFS 共享方式

![](http://upload-images.jianshu.io/upload_images/1332969-720a473e696e4778.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

上图中，第一列是导出的共享目录（Downloads、video、photo、music、ikbase、downloads），第二列是对应目录的可见网段（192.168.10.0~192.168.10.254）。

这些共享目录是通过 /etc/exports 这个文体定义的：
```
/Volumes/NMSC/downloads -alldirs -rw -network 192.168.10.0 -mask 255.255.255.0
```
![](http://upload-images.jianshu.io/upload_images/1332969-c07129fae6a40b11.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

该文件被修改后，如何立即生效呢？可以通过nfsd命令设置（该命令由nfs服务提供）
```
nfsd status  # 查询服务状态
nfsd update # 重新加载exports定义的目录
```

其它机器若想知道媒体中心导出的目录有哪些，可以这样：

![](http://upload-images.jianshu.io/upload_images/1332969-36ded0f2eae2c694.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)


## DSM5 挂载

DSM5 是群晖定制的LINUX系统，用来提供NAS服务，此处不讲。


![查询媒体中心共享的目录](http://upload-images.jianshu.io/upload_images/1332969-dc207907df1bf75d.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

挂载命令：
```
mount -t nfs -o nosuid,noexec,nodev,ro,bg,soft,rsize=32768,wsize=32768 $dir_src $dir_dst 
```

其中，dir_src 是指网络共享出来的某个目录:
```
dir_src=192.168.10.100:/Volumes/NMSC/downloads
```

dir_dst 是指本机的某个目录，是挂载点：
```
dir_dst=/volume1/TDDOWNLOAD
```

最后挂载完后的情况如下：

![image.png](http://upload-images.jianshu.io/upload_images/1332969-2b7ceaf55976f31e.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

## AC66U_B1 挂载

挂载命令需在DSM5挂载命令的基础上添加 ‘nolock'，去掉文件锁方可挂载成功，命令具体如下：
```
mount -t nfs -o nosuid,noexec,nodev,nolock,rw,bg,soft,rsize=32768,wsize=32768 $dir_src $dir_dst
```
其中，dir_src 是指网络共享出来的某个目录:
```
dir_src=192.168.10.100:/Volumes/NMSC/downloads
```

dir_dst 是AC66U_B1外接U盘下的某个目录，是挂载点：
```
dir_dst=/tmp/mnt/_________U___/share/downloads
```

![](http://upload-images.jianshu.io/upload_images/1332969-8205269d2db7a130.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

我的AC66U_B1路由
```
mount -t nfs -o nosuid,noexec,nodev,nolock,rw,bg,soft,rsize=32768,wsize=32768 192.168.50.163:/Volumes/NMSC/downloads /tmp/mnt/_________U___/share/downloads
```
这么多目录，其实可以通过shell脚本进行挂载和卸载。