---
title: Github 博客建站
date: 2017-11-20 15:53:42
tags:
---

> 目的： 在github 上新建一个 im.doubi.net 的个人博客站点
> 条件：
> - 拥有 Github账号，比如，我的账户名：doubi
> - 拥有 doubi.net 域名使用权



### 1. Github 建立仓库
首先在Github 官网新建仓库，新建仓库地址应该是： https://github.com/doubi/im.git

![image.png](http://upload-images.jianshu.io/upload_images/1332969-fe62840ed99f537f.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)



完成后，带有.gitignore文件和 README.md


其次，新建分支 hexo.

![image.png](http://upload-images.jianshu.io/upload_images/1332969-942a9d27a2724ab6.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)


### 2. 本地操作

#### 2.1 本地克隆
 
```
git clone --branch hexo https://github.com/doubi/im.git
cd im
git branch
```
![image.png](http://upload-images.jianshu.io/upload_images/1332969-1e558d38b1fd05c1.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

![image.png](http://upload-images.jianshu.io/upload_images/1332969-dd92cbd05a8c6d6c.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

#### 2.2 hexo 初始化 

```
hexo init im-hexo
```
![image.png](http://upload-images.jianshu.io/upload_images/1332969-ac6f28d5661b649e.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

```
cp -r im-hexo/* .
cp im-hexo/.gitignore .
rm -rf im-hexo
```
![image.png](http://upload-images.jianshu.io/upload_images/1332969-c5def992f00462b8.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

添加hexo文件到本地仓库，第一次本地提交：
``` 
git add .
git commit -am "init hexo"
```


接下来，本地运行hexo，查看效果：
```
hexo s
```
第二次本地提交：
```
git commit -am "first run: hexo s, it works."
```
#### 2.3 hexo 配置 

安装hexo-deployer-git插件，使得可以自动发布网页到master：
```
npm install hexo-deployer-git --save
```
站点目录文件中修改：
![image.png](http://upload-images.jianshu.io/upload_images/1332969-53013c4e26190588.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

网站生成，并发布到github上：
```
hexo g -d
```
这时，github上的master分支下的内容：
![image.png](http://upload-images.jianshu.io/upload_images/1332969-5de5eba98ec772df.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

第三次本地提交：
```
git commit -am "install hexo-deployer-git, & add deploy path"
```

#### 2.4 添加 CNAME 

接下来，添加CNAME 到 im\source目录下
```
cd source
echo "im.doubi.net" > CNAME 
cd ..
```
第四次本地提交：
```
git add .
git commit -am "add CNAME file to deploy"
```

#### 2.5 网站发布

将本地仓库修改提交到github上：
```
git push origin hexo
```
![image.png](http://upload-images.jianshu.io/upload_images/1332969-4df3d689226f3b09.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)


生成网页，并再次发布到github
```
hexo g -d
```
然后，在浏览器中输入： im.doubi.net，就可以看到你的网站了。 



### 3. 安装NexT 主题

http://theme-next.iissnan.com/getting-started.html

