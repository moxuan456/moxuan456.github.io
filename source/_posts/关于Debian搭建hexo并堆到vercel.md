---
layout: '[layout]'
title: 关于Debian搭建hexo并堆到vercel
date: 2024-02-11 02:53:14
tags:
---
#0x01安装环境
```
sudo apt-get install git //安装git

sudo apt-get install nodejs //安装nodejs.

sudo apt-get install npm //安装npm
```

安装成功后用 ``git -v`` ``node -v`` ``npm -v``来分别检查是否安装成功，安装成功会有版本号出现

#0x02安装hexo
接着用 ``npm install -g hexo-cli`` 来安装hexo，还是用 ``hexo -v`` 来检查是否安装成功

安装成功后我们用 ``hexo init blog`` 来初始化一下hexo
>这个blog不是固定的可以改成自己喜欢的

用 ``cd blog`` 进入文档

接着输入 ``npm install``

接着用sftp进入blog这个文件夹，我们可以看到有一些初始文件

#0x03拉取Github pages并上传到vercel
* 创建GitHub pages教程跳过
* 创建vercel教程跳过

用以下代码来配置github
```
git config --global user.name "yourname"
git config --global user.email "youremail"
```
用下面代码来检查是否正确，如果输出的是你的github邮箱和用户名那就是正确的
```
git config user.name
git config user.email
```

* 配置ssh
``ssh-keygen -t rsa -C "youremail"``
用sftp打开文件夹**.ssh**里面能找到**id_rsa.pub**这个文件把里面的东西全部复制到ssh keys里面

在_config.yml里面找到``deploy``把它改成
```
deploy:
  type: git
  repo: git@github.com:username/project
  branch: master
```
然后在Debian中拉取github仓库``git clone git@github.com:username/project``

我们可以看到有一个仓库名称的文件夹里面有一个**.git**文件夹我们把它移到**blog**里面

用下列命令把**blog文件夹**里面的文件上传到github
```
git add .
git commit -m "update"
git push origin main
```
最后直接用 vercel 直接拉取仓库即可