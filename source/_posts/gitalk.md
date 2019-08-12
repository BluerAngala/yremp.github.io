---
title: Hexo-Sakura安装Gitalk
author: yremp
avatar: https://cdn.jsdelivr.net/gh/yremp/cdn@2.1.4//img/custom/head.jpg
authorLink: ./
authorAbout: 
authorDesc: 
categories: 技术
date: 2019-7-1 18:16:01
comments: true
tags: 
 - web
keywords: Gitalk
description: Hexo-Sakura安装Gitalk教程
photos: https://cdn.jsdelivr.net/gh/yremp/resource@4.3/img/posts/gitalkcover.png
---
####  Gitalk 
  Gitalk 是一款基于GitHub使用的评论插件，使用起来非常方便。最近Valine出了一些问题，无法正常使用，虽然官网给了修复的方法，但是我不想再使用Valine，于是便安装了Gitalk这款插件，下面给大家带来 <font color=#FF1493> Sakura主题</font>安装gitalk的教程 <br>

#### 申请 OAuth Apps
首先登Github主页，点击你的头像依次点击<font color=#ff6633>Settings->Developer settings->OAuth Apps-> new OAuth Apps</font>
将会到下面的界面：

![]( https://cdn.jsdelivr.net/gh/yremp/resource@4.5/img/posts/gitalkapply01.png)

里面几个参数介绍如下：
1. Application name:应用名称，这个你自己随便写，合法就行
2. Homepage URL:这个填写你的博客地址例如：https://yremp.github.io
3. Application description:应用描述随便填
4. Authorization callback URL:如果你绑定了个性域名一定要填写个性域名,例如：https://yremp.club 
   
![]( https://cdn.jsdelivr.net/gh/yremp/resource@4.4/img/posts/key.png)

申请完成以后有两个重要参数Client ID、Client Secret后面会使用：<br>

如下所示：
![]( https://cdn.jsdelivr.net/gh/yremp/resource@4.4/img/posts/gitalkapply02.png)

#### 修改配置文件
做完上面的准备工作接下来就是修改配置文件:在  <font color=#ff6633>\themes\Sakura</font> 下找到<font color=#ff6633> _config.yml</font> 。打开，在最下方加入如下代码：
``` 
gitalk:
    # 是否自动展开评论框
    autoExpand: true
    # 应用编号
    clientID: '8972e4300aeaabe97cc0'
    # 应用秘钥
    clientSecret: '988d6142b09dd52db79a2b832ba8f068df13a99a'
    # issue仓库名
    repo: 'yremp.github.io'
    # Github名
    owner: 'yremp'
    # Github名
    admin: ['yremp']
    # Ensure uniqueness and length less than 50
    id: location.pathname
    # Facebook-like distraction free mode
    distractionFreeMode: false
``` 
对照注释修改：
1. clientID：       申请的应用ID
2. clientSecret：   申请的应用密匙
3. repo：           issue仓库名
4. owner：          你的github用户名
5. admin：          你的github用户名

#### 修改布局文件
接着，在 <font color=#ff6633>\themes\Sakura\layout\_partial</font> 下找到<font color=#ff6633>comment.ejs</font>将里面的代码替换为如下代码：
``` 
<% if ( post.comments) { %>
  <script src="https://cdn.jsdelivr.net/gh/yremp/yremp-js@1.1/gitalk.js"></script>
  <link rel="stylesheet" href="https://cdn.jsdelivr.net/gh/yremp/yremp-css@1.3/gitalk.css">
  <div id="gitalk-container"></div>
  <script type="text/javascript">
      var gitalk = new Gitalk({
          clientID: '<%= theme.gitalk.clientID %>',
          clientSecret: '<%= theme.gitalk.clientSecret %>',
          id: window.location.pathname,
          repo: '<%= theme.gitalk.repo %>',
          owner: '<%= theme.gitalk.owner %>',
          admin: '<%= theme.gitalk.admin %>'
      })
      gitalk.render('gitalk-container')
    </script>
<% } %>
``` 
里面的js以及css文件是我从官方找的并且放在我的github上面，你可以去找官方的链接下载放到自己github上面，也可以直接用我的。然后，在 <font color=#ff6633>\themes\Sakura\layout\_partial </font>下找到<font color=#ff6633>footer.ejs</font>在里面加入评论区容器：
``` 
<div id="gitalk-container"></div>
``` 
位置合适就好，可以参考我的：

![]( https://cdn.jsdelivr.net/gh/yremp/resource@4.4/img/posts/p1.png)

继续在这个文件里添加JS链接：
``` 
<script src="https://cdn.jsdelivr.net/gh/yremp/yremp-js@1.1/gitalk.js"></script>
``` 
位置可以参考我的：

![]( https://cdn.jsdelivr.net/gh/yremp/resource@4.4/img/posts/p2.png)

最后，在 <font color=#ff6633>\themes\Sakura\layout\_partial</font> 下找到<font color=#ff6633>head.ejs</font>加入如下代码：
``` 
<link rel="stylesheet" href="https://cdn.jsdelivr.net/gh/yremp/yremp-css@1.3/gitalk.css">
``` 

可以参考我的：

![]( https://cdn.jsdelivr.net/gh/yremp/resource@4.4/img/posts/p3.png)

#### 完成
接下来就是：<br>

1. hexo clean
2. hexo g
3. hexo d

大功告成，效果如下：<br>
![]( https://cdn.jsdelivr.net/gh/yremp/resource@4.6/img/posts/style.png)

<center>如果有什么问题，请到评论区留言。转载请标明作者和原文地址