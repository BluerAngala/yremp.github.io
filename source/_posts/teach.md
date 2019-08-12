---
title: Sakura新手使用手册
author: yremp
avatar: https://cdn.jsdelivr.net/gh/yremp/cdn@2.1.4//img/custom/head.jpg
authorLink: ./
authorAbout: 
authorDesc: 
categories: 技术
date: 2019-5-26 22:16:01
comments: true
tags: 
 - web
keywords: Sakura新手使用手册
description: sakura使用教程，比较详细
photos: https://cdn.jsdelivr.net/gh/yremp2/image@2.0/hendmenu.png
---

有很多小伙伴使用Sakura这款主题却又不知到如何美化，到处找别人问很麻烦，而我当初也是花了很长时间去摸索，才了解了这款主题的一些具体设置。下面我就按照从主页到子页面，从顶部到页脚的顺序给你们介绍如何自定义这款主题。

<font color=#0099ff size=3 face="黑体"><br>
1.本教程主要写给刚入门的小白，大佬随意。<br>
2.教程比较长，建议根据右边标题索引快速找到自己感兴趣的部分<br>

</font><br>
##  一：顶部站点名字：
![]( https://cdn.jsdelivr.net/gh/yremp2/image@2.0/headmark.png)
这个是在<font color=	#FF1493 size=3 face="黑体"> /themes/sakura/config.yml </font>这个配置文件中修改

``` 
//site name
prefixName: 君の名は
siteName: yremp
url: https://yremp2.github.io/ 
``` 
其中，URL是点击后跳转地址.
由于我在<font color=#FF1493 size=3 face="黑体"> /themes/sakura/source/css/style.css</font>下修改了样式表去掉了prefixName，所以图上是没有的
大家如果想修改其相关的样式也可以去这个css文件中自定义,这个文件是主要的css文件，大部分的样式都是由这个文件定义的。

## 二：顶部导航栏
![](https://cdn.jsdelivr.net/gh/yremp2/image@2.0/hendmenu.png)
这个在主题使用教程里面，作者好像已经是给出来了，大家可以仔细去阅读以下(当初我就是没有认真阅读爬了不少坑)
这也是<font color=	#FF1493 size=3 face="黑体"> /themes/sakura/config.yml </font>这个配置文件里面定义的
``` 
menus:
  首页: { path: /, fa: fas fa-home  fa-1x }
  归档: { path: /archives, fa: far fa-folder-open, submenus: { 
    技术: {path: /categories/技术/, fa: fab fa-windows }, 
    生活: {path: /categories/生活/, fa: fa-book }, 
    资源: {path: /categories/资源/, fa: fa-cloud-download }, 
    随想: {path: /categories/随想/, fa: fa-commenting-o },
    转载: {path: /categories/转载/, fa: fas fa-clone }
  } }
  清单: { path: javascript:;, fa: fas fa-tasks,submenus: { 
    书单: {path: /tags/悦读/, fa: fa-th-list faa-bounce }, 
    番组: {path: /bangumi/, fa: fa-film faa-vertical }, 
    歌单: {path: /music/, fa: fa-headphones },
    图集: {path: /tags/图集/, fa: fa-photo }
  } }
  留言板: { path: /comment/, fa: fa-pencil-square-o faa-tada }
  友人帐: { path: /links/, fa: fa-link faa-shake }
  ``` 
  前面的path是网页路径，这个不建议修改，但可以修改。后面的如:<font color=#0099ff size=3 face="黑体"> fa: fas fa-home  fa-1x </font>这个就是对应的图标设置,关于这个图标大家可以去[fontawesome](http://fontawesome.dashgame.com/)看教程以及选择自己喜欢的图标，导航栏下拉下拉菜单的图标修改和导航栏相同。
## 三：头像
![](https://cdn.jsdelivr.net/gh/yremp2/image@2.0/head.png)
很多小伙伴拿到主题后第一时间肯定是修改这个头像，毕竟这个比较能代表自己嘛，那么这个头像配置在哪(⊙o⊙)?
如果有经验的小伙伴肯定是自己就能找到，这个配置在：
<font color=	#FF1493 size=3 face="黑体"> /themes/sakura/config.yml </font>
```
cdn: https://cdn.jsdelivr.net/gh/yremp/cdn@2.1.5
avatar: /img/custom/head.jpg
```
我这个是使用cdn后的路径，也可以修改为：
```
avatar: https://cdn.jsdelivr.net/gh/yremp/cdn@2.1.5/img/custom/head.jpg
```
至于cdn：大家可以去看我的另一篇博客[jsDeliver+github使用教程](https://yremp2.github.io/2019/05/24/jsDeliver+github%E4%BD%BF%E7%94%A8%E6%95%99%E7%A8%8B/)

## 四：社交栏
![](https://cdn.jsdelivr.net/gh/yremp2/image@2.0/social.png)
### 1.个性签名
这个在<font color=	#FF1493 size=3 face="黑体"> /themes/sakura/config.yml </font>里面，由如下代码定义

```
description: 南风过境，十里春风不如你！
```
直接修改即可

###  2.内容
没错仍然是 <font color=	#FF1493 size=3 face="黑体"> /themes/sakura/config.yml </font>这个文件，找到

```
#social  url, img PC端配置
social:
  github: {url: https://github.com/yremp, img: /img/social/github.png}
  wangyiyun: {url: https://music.163.com/, img: /img/social/wangyiyun.png}
  zhihu: {url: https://www.zhihu.com/, img: /img/social/zhihu.png}
  qq: {url: /#, qrcode: /img/custom/qq.png, img: /img/social/qq.png}
  wechat: {url: /#, qrcode: /img/custom/wechat.png, img: /img/social/wechat.png}

#social  url, img 移动端配置
msocial:
  github: {url: https://github.com/yremp, fa: fa-github, color: 333}
  weibo: {url: https://weibo.com/, fa: fa-weibo, color: dd4b39}
  qq: {url: https://im.qq.com/news/, fa: fa-qq, color: 25c6fe}  

```
前面URL对应点击后跳转地址，后面是图标路径，注意这个不是本地路径，是使用了cdn后的路径，上一栏 <font color=#0099ff size=3 face="黑体">头像</font>设置中有介绍。至于pc和移动端注释已经标示了，就不多作介绍。
### 3.社交栏整体样式
在<font color=	#FF1493 size=3 face="黑体"> /themes/sakura/source/css/style.css </font>Ctrl+f 搜索 header-info，这就是这个地方对应的div的class名字
就可以在代码中找到
```
.header-info {
    width: 63%;
    margin: auto;
    font-size: 16px;
    color: #eaeadf;
    background: rgba(255,255,255,.8);
    padding: 15px;
    margin-top: 22px;
    letter-spacing: 0;
    line-height: 30px;
    border-radius: 10px;
    box-sizing: initial;
    white-space: nowrap;
}
.header-info:before {
    content: "";
    position: absolute;
    top: 127.5px;
    left: 50%;
    margin-left: -15px;
    border-width: 15px;
    border-style: solid;
    border-color: transparent transparent rgba(255,255,255,.8) transparent;
}
.header-info p {
    margin:0;
    color: #605f5f;
    font-family:'Ubuntu',sans-serif;
    font-weight:700
}
```
这就是其对应的样式表内容，大家可以根据需要修改。<font color=	#FF1493 size=3 face="黑体">(Chrome) Ctrl+Shift+C</font><font color=#0099ff size=3 face="黑体">然后点击你想查看的部分就会给你提示对应的部分例如：
![](https://cdn.jsdelivr.net/gh/yremp2/image@2.0/teach1.png)对应关系已经标出来，大家可以用这个功能快速找到网页和css对应关系，方便进行修改
</font>
## 五：顶部图片和效果
![](https://cdn.jsdelivr.net/gh/yremp2/image@2.0/image/headbg.png)
### 1.顶部图片
<font color=	#FF1493 size=3 face="黑体"> /themes/sakura/config.yml </font>中找到如下代码：
```
# 背景图片 根据喜好修改
bg:
  - https://cdn.jsdelivr.net/gh/yremp/cdn@2.1.5/img/cover/(1).jpg.webp
  - https://cdn.jsdelivr.net/gh/yremp/cdn@2.1.5/img/cover/(2).jpg.webp
  - https://cdn.jsdelivr.net/gh/yremp/cdn@2.1.5/img/cover/(3).jpg.webp
  - https://cdn.jsdelivr.net/gh/yremp/cdn@2.1.5/img/cover/(4).jpg.webp
  - https://cdn.jsdelivr.net/gh/yremp/cdn@2.1.5/img/cover/(5).jpg.webp
  - https://cdn.jsdelivr.net/gh/yremp/cdn@2.1.5/img/cover/(6).jpg.webp
  - https://cdn.jsdelivr.net/gh/yremp/cdn@2.1.5/img/cover/(8).jpg.webp
  ```
### 2.顶部图片效果
我的顶部效果改为了无，个人不太喜欢。可根据需要修改在：
<font color=	#FF1493 size=3 face="黑体"> /themes/sakura/config.yml </font>中找到如下代码：
```
# 背景图片样式 空 原图效果 filter-dim 阴影 filter-grid 横条 filter-dot 点点
bgclass: 
```
具体参数原作者在注释中已经标示
## 六：通知栏
![](https://cdn.jsdelivr.net/gh/yremp2/image@2.0/message.png)
<font color=	#FF1493 size=3 face="黑体"> /themes/sakura/config.yml </font>中找到如下代码：
```
notice: 欢迎来到我的博客！
```
直接修改内容即可

## 七：startdash
![](https://cdn.jsdelivr.net/gh/yremp2/image@2.0/start.png)
### 1.模块名字
在<font color=	#FF1493 size=3 face="黑体"> /themes/sakura/layout/_partial/startdash.ejs</font>中有如下：
```
<div class="top-feature-row">
  <h1 class="fes-title" style="font-family: 'Ubuntu', sans-serif;">
  <i class="fa fa-anchor" aria-hidden="true">
  </i>
  startdash</h1>
  <% for (dash in theme.startdash) { %>
  ....
```
将其中startdash改为你想要的即可；
### 2.内容设置
<font color=	#FF1493 size=3 face="黑体"> /themes/sakura/config.yml </font>中找到如下代码：
```
# startdash url, title, desc img
startdash: 
  - {url: /theme-sakura/, title: Sakura, desc: 本站主题, img: /img/startdash/sakura.md.png}
  - {url: http://space.bilibili.com/381786734, title: Bilibili, desc: b站视频, img: /img/startdash/bilibili.jpg}
  - {url: /, title: 万事屋, desc: 技术服务, img: /img/startdash/wangshiwu.jpg}
```
注释也已经标示出其参数，根据参数修改即可。
## 八：Discovery
![](https://cdn.jsdelivr.net/gh/yremp2/image@2.0/find.png)
<font color=	#FF1493 size=3 face="黑体"> /themes/sakura/layout/index.ejs</font>中找到如下代码：
```
      <h1 class="main-title" style="font-family: 'Ubuntu', sans-serif;">
      <i class="fa fa-envira" aria-hidden="true"></i>
      Discovery</h1>
      <%- partial('_partial/archive', {pagination: 2, index: true}) %>
      <!-- 首页默认取最最新文章集 -->
```
Discovery就是标题，直接修改即可
## 九：文章封面和内容；
1.封面
![](https://cdn.jsdelivr.net/gh/yremp2/image@2.0/page.png)
这个在在你写博客时，有photo属性，设置url即可 ，下面是示例：
```
title: Sakura美化教程
author: hojun
avatar: https://wx1.sinaimg.cn/large/006bYVyvgy1ftand2qurdj303c03cdfv.jpg
authorLink: https://yremp.club
authorAbout: 
authorDesc: 
categories: 技术
date: 2019-5-26 12:16:01
comments: true
tags: 
 - web
keywords: Sakura主题自定义美化教程
description:  Sakura美化教程
photos: https://static.2heng.xin/wp-content/uploads//2019/02/wallhaven-672007-1-1024x576.png
---
```
photos 就是文章的封面
## 十：归档子页面
![](https://cdn.jsdelivr.net/gh/yremp2/image@2.0/t.png)
这个相关的设置是在<font color=	#FF1493 size=3 face="黑体"> /themes/sakura/language/zh-cn.yml</font>
找到如下代码：
```
#category
技术:
    zh: 野生技术协会
    en: Technical Communication
    img: https://cdn.jsdelivr.net/gh/yremp/cdn@2.1.5/img/cover/(1).jpg.webp
生活:
    zh: 生活
    en: Live
    img: https://cdn.jsdelivr.net/gh/yremp/cdn@2.1.5/img/cover/(2).jpg.webp
......
```
这就不用我解释，对比图片很容易看懂

## 十一：清单子页面

### 1.悦读和图集，
![](https://cdn.jsdelivr.net/gh/yremp2/image@2.0/read.png)
在<font color=	#FF1493 size=3 face="黑体"> /themes/sakura/language/zh-cn.yml</font>
找到如下代码：
```
#tag
悦读:
    img: https://cdn.jsdelivr.net/gh/yremp/cdn@2.1.5/img/cover/(6).jpg.webp
图集:
    img: https://cdn.jsdelivr.net/gh/yremp/cdn@2.1.5/img/cover/(5).jpg.webp
web:
    img:  https://cdn.jsdelivr.net/gh/yremp/resource@1.0/img/pic.jpg
```
对比图片进行修改

 ### 2.番组
![](https://cdn.jsdelivr.net/gh/yremp2/image@2.0/bili.png)
这个页面对应的配置是在<font color=	#FF1493 size=3 face="黑体"> /source/bangumi/index.md</font>中修改，其中代码如下：
```
---
layout: bangumi
title: bangumi
comments: false
date: 2019-02-10 21:32:48
keywords:
description:
bangumis:
  - img: http://pic.netbian.com/uploads/allimg/180413/121552-152359295246db.jpg
    title: 狐妖小红娘
    status: 追番中
    progress: 100
    jp: 狐妖小红娘
    time: 2019-05-24 SUN.
    desc: 白月初……
  - img: http://pic.netbian.com/uploads/allimg/170605/130458-149663909840b3.jpg
    title: 名侦探柯南
    status: 追番中
    progress: 1000
    jp: 名探偵コナン
    time: 2019-05-24 SUN.
    desc: 中生侦探工藤新一……
---
```
对比图片修改内容即可，也可以增加其他内容。
### 3.歌单
![](https://cdn.jsdelivr.net/gh/yremp2/image@2.0/music.png)
整个页面配置在<font color=	#FF1493 size=3 face="黑体"> /source/music/index.md</font>中：
其代码如下：

```
---
title: music
date: 2018-12-20 23:14:28
keywords: 喜欢的音乐
description: 
comments: false
photos: http://pic.netbian.com/uploads/allimg/170911/233802-15051442827782.jpg
---
<iframe frameborder="no" border="0" marginwidth="0" marginheight="0" width=100% height=450 src="//music.163.com/outchain/player?type=0&id=762797776&auto=1&height=430"></iframe>
```

前面是常规的信息配置没什么好说的，photos就是这个页面的顶部图片，在
```
<iframe frameborder="no" border="0" marginwidth="0" marginheight="0" width=100% height=450 src="//music.163.com/outchain/player?type=0&id=762797776&auto=1&height=430"></iframe>
```
中需要改一下id，这个id就是网易云音乐歌单id，怎么获取如下图：
![](https://cdn.jsdelivr.net/gh/yremp2/image@2.0/teach2.png)
登录网页版网易云音乐，打开歌单，在地址栏中可以看到
```
https://music.163.com/#/playlist?id=762797776
```
其中id后面的数字复制，粘贴到代码里面的id后面就可以显示自己的歌单了。
## 十二：友情链接相关配置
<font color=	#FF1493 size=3 face="黑体">(留言板/source/comment/index.md就一个背景修改就不出教程了，为了给下面其他教程留空间)</font><br>
![](https://cdn.jsdelivr.net/gh/yremp2/image@2.0/links.png)
### 1.内容配置
友情链接内容配置具体在<font color=	#FF1493 size=3 face="黑体"> /source/link/index.md</font>
代码如下
```
......
photos: https://cdn.jsdelivr.net/gh/honjun/cdn@1.4/img/banner/links.jpg //背景图片
links:
  - group: 小伙伴们
    desc: 欢迎交换友链 ꉂ(ˊᗜˋ)
    items:
    - url: https://yremp.github.io
      img: https://cloud.moezx.cc/Picture/svg/landscape/fields.svg
      name: 好友1
      desc: 点击查看
......   
---
```
根据实际情况修改其中的内容
### 2.界面背景及布局
界面背景及布局主要在<font color=	#FF1493 size=3 face="黑体">/themes/sakura/layout/links.ejs</font>
代码如下：
```
        ........
        <p>
            欢迎交换友链qaq ꉂ(ˊᗜˋ)</p>
        <p>
            请留言告诉我你的：
            <br> 1、名字
            <br> 2、一句话介绍（熟人我会亲自帮写的）
            <br> 3、主页地址
            <br> 4、头像（HTTPS*，可在评论区上传）
        </p>
        ........
```
对照图片根据需要修改
## 十三：左下角播放器
![](https://cdn.jsdelivr.net/gh/yremp2/image@2.0/aplayer.png)
1.设置为自己的歌单 ，和清单里的歌单一样要先拿到网易歌单id，怎么获取上面<font color=#0099ff size=3 face="黑体">清单子页面</font>里有相关介绍；
然后在<font color=	#FF1493 size=3 face="黑体"> /themes/sakura/config.yml </font>中找到如下代码：
```
player: 
  id: 762797776
  server: netease
  type: playlist
  fixed: true
  autoplay: false
  loop: all
  order: random
  preload: none
  volume: 0.7
  mutex: true
```
修改为自己的网易云歌单id即可
## 十四：切换背景
![](https://cdn.jsdelivr.net/gh/yremp2/image@2.0/skin.png)
严格意义上来说这个并不算增加，算是恢复，作者在移植这款主题时，只删除了对应的ejs布局文件，并没有删除style.css和js里面相关代码，想要加上这个功能只需要把原作者的相关的div等加上就行。大佬可自行到白猫（原作者）网站查看源代码加上就行。如果是小白或者比较懒得朋友那你只需要按以下几个步骤即可实现这个功能：
1:<font color=	#FF1493 size=3 face="黑体">找到 /themes/sakura/layout/layout.ejs</font>
在里面加入两行代码代码位置和内容如下（注释下面那两行）：
```
......
......
......
 <!-- 下面两行为了实现换肤功能 -->
  <%- partial('_partial/setdisplay') %> 
  <%- partial('_partial/set', null, {cache: !config.relative_link}) %>

  <%- partial('_partial/mheader', null, {cache: !config.relative_link}) %>
  <%- partial('_partial/aplayer', null, {cache: !config.relative_link}) %> 
</body>
</html>
```

2: 在<font color=	#FF1493 size=3 face="黑体">/themes/sakura/layout/_partial</font>文件夹下面依次新建set.ejs和setdisplay.ejs,其内容分别如下：
<font color=	#FF1493 size=3 face="黑体">set.ejs</font>
```
<div class="changeSkin-gear no-select">
    <div class="keys" id="setbtn"> <span id="open-skinMenu"> 切换主题 | SCHEME TOOL &nbsp;<i
                class="iconfont icon-gear inline-block rotating"></i> </span></div>
</div>
```
<font color=	#FF1493 size=3 face="黑体">setdisplay.ejs</font>
```
<div class="skin-menu no-select" id="mainskin"  style="position: fixed">
    <div class="theme-controls row-container">
        <ul class="menu-list">
            <li id="white-bg"> <i class="fa fa-television" aria-hidden="true"></i></li>
            <li id="sakura-bg"> <i class="iconfont icon-sakura"></i></li>
            <li id="gribs-bg"> <i class="fa fa-slack" aria-hidden="true"></i></li>
            <li id="KAdots-bg"> <i class="iconfont icon-dots"></i></li>
            <li id="totem-bg"> <i class="fa fa-optin-monster" aria-hidden="true"></i></li>
            <li id="pixiv-bg"> <i class="iconfont icon-pixiv"></i></li>
            <li id="bing-bg"> <i class="iconfont icon-bing"></i></li>
            <li id="dark-bg"> <i class="fa fa-moon-o" aria-hidden="true"></i></li>
        </ul>
    </div>
<canvas id="night-mode-cover"></canvas>
```
## 十五：评论不在白名单问题
首先，和评论相关的配置在：<font color=	#FF1493 size=3 face="黑体"> /themes/sakura/config.yml </font>
具体代码：
```
# Valine
valine: true
v_appId: Qtrxu5pUbpfjbn2CpMH1jetC-gzGzoHsz
v_appKey: 72NpGpYhuAYcKyDhYSOFE1b2
```
这里面的id和Key是需要修改的，因为这是我的v_appId和v_appKey，你需要去[注册](https://leancloud.cn/)。具体的请自行百度。只提醒一点，注册完以后 ，申请app以后，要设置 <font color=	#FF1493 size=3 face="黑体"> 白名单</font>。
<center>如果发现教程有什么问题或者你有什么问题，请到评论区留言。转载请标明作者和原文地址