---
title: jsDeliver+github使用教程
author: yremp
avatar: https://cdn.jsdelivr.net/gh/yremp/cdn@2.1.4//img/custom/head.jpg
authorLink: yremp.club
authorAbout: 
authorDesc: 
categories: 转载
comments: true
tags: 
 - web
keywords: Sakura
description: sDeliver+github使用教程
photos: https://upload.cc/i1/2019/05/24/68p7nf.png
---
前言:国内加载github的资源比较慢，需要使用CDN加速来优化网站打开速度，于是使用jsDeliver+github搭建免费的cdn。jsDelivr 是一个免费开源的 CDN 解决方案，用于帮助开发者和站长。包含 JavaScript 库、jQuery 插件、CSS 框架、字体等等 Web 上常用的静态资源。

## 写给小白的,懂的前面可以略过
### npm
NPM是JavaScript的包管理器，也是世界上最大的软件注册中心。发现可重用代码的包——并以强大的新方式组装它们。每星期大约有 30 亿次的下载量，包含超过 600000 个 包（package（即，代码模块）。来自各大洲的开源软件开发者使用 npm 互相分享和借鉴。包的结构使您能够轻松跟踪依赖项和版本。
所以jsDeliver+npm就是把npm上的包当做cdn的存储。
使用教程：

```
// load any project hosted on npm
// 加载以NPM为存储的任何项目
https://cdn.jsdelivr.net/npm/package@version/file
// load jQuery v3.2.1
// 比如加载Jquery3.2.1
https://cdn.jsdelivr.net/npm/jquery@3.2.1/dist/jquery.min.js
// use a version range instead of a specific version
//使用版本范围而不是特定版本
https://cdn.jsdelivr.net/npm/jquery@3.2/dist/jquery.min.js
https://cdn.jsdelivr.net/npm/jquery@3/dist/jquery.min.js
// omit the version completely to get the latest one
//完全忽略版本以获取最新版本，不建议使用
https://cdn.jsdelivr.net/npm/jquery/dist/jquery.min.js
略......
```

## Github
gitHub是一个面向开源及私有软件项目的托管平台，因为只支持git 作为唯一的版本库格式进行托管，故名gitHub。
jsDeliver+Github使用教程：

```
// load any GitHub release, commit, or branch
// 加载任何Github发布、提交或分支
https://cdn.jsdelivr.net/gh/user/repo@version/file
略......
```
## WordPress
WordPress是一款个人博客系统，并逐步演化成一款内容管理系统软件，它是使用PHP语言和MySQL数据库开发的。用户可以在支持 PHP 和 MySQL数据库的服务器上使用自己的博客。
jsDeliver+WordPress使用教程：

```
// load any plugin from the WordPress.org plugins SVN repo
// 从WordPress.org等SVN仓库加载任何插件
https://cdn.jsdelivr.net/wp/plugins/project/tags/version/file
略......
```
## 第一步：新建github仓库
![](https://upload.cc/i1/2019/05/24/n4ZY5V.png)
(我已经有这个仓库，so...这不是重点)
接着在本地电脑克隆上图仓库（前提配置好本地git环境和ssh）
命令如下：

```
cd 某个目录下
git clone git@github.com:你的用户名/cdn.git

```
## 第二步：上传需要的资源
复制需要的静态资源到本地git仓库中，提交到github仓库上。
命令如下：
```
cd 到git仓库目录下
// 查看状态
git status
// 添加所以改动
git add .
// 提交
git commit -m '第一次提交'
// 推送至远程仓库
git push
```
（注：jsDeliver不支持加载超过20M的资源，所以一些视频最好压缩到20M以下）
## 第三步：发布仓库

![](https://upload.cc/i1/2019/05/24/ehcrEO.png)

![](https://upload.cc/i1/2019/05/24/37gEzn.png)
点击release发布

发布版本号1.0（自定义）

## 第四步：通过jsDeliver引用资源

```
使用方法：
https://cdn.jsdelivr.net/gh/你的用户名/你的仓库名@发布的版本号/文件路径
比如：
//加载js
https://cdn.jsdelivr.net/gh/yremp/cdn@1.0/js/jquery.js
//加载图片
https://cdn.jsdelivr.net/gh/yremp/cdn@1.0/images/hb.png
```
<font color=#0099ff size=4 face="黑体">重点：这个链接相当于一个直链，使用和直链一样，如下图：</font>

![](https://upload.cc/i1/2019/05/25/pRCHh9.png
)

<font color=#0099ff size=4 face="黑体">总的来说，直链怎么用，这个链接怎么用</font>

尊重原创，转载自hojun的文章并做修改。 点击查看[原文](https://www.hojun.cn/2019/01/18/jsDeliver-github%E4%BD%BF%E7%94%A8%E6%95%99%E7%A8%8B%EF%BC%8C%E5%85%8D%E8%B4%B9%E5%A5%BD%E7%94%A8%E7%9A%84cdn/).  

<br>
<br>
<center>希望这篇文章能给你带来知识和乐趣，喜欢博主的文章可以留言哦

   
