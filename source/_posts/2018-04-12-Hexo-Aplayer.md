---
title: Hexo Aplayer
date: 2018-04-12 15:17:55
tags: MarkDown
---

网易云音乐的因为版权问题，很多好听歌的都无法生成外链，给我们写博客造成了很大的不便。

由于我的无知，我以为买个会员就好了，事实证明，无效。

下面我将介绍一个对目前的我来说很神奇的一个方法：

* **Aplayer**：音乐播放
* **Dplayer**：视频播放



## 安装	

那么第一步毋庸置疑就是下载**aplayer**（我的**aplayer**是在下载我写博客的那个文件夹下）

帅气的打开**Terminal**，进行一下操作

```
npm install hexo-tag-aplayer --save

npm install hexo-tag-dplayer --save
```

这个 **--save**不能省略，我在安装时，省略了 **--save**，之后就出错了


## 使用
ok,下面就是如何使用啦,见证奇迹的时刻到了。

### aplayer

```
{% aplayer "歌曲名字" "作者" "音乐_url" "封面图片_url" "autoplay" %}

```

下面我给出一个实际的例子

```
{% aplayer "最美的期待" "周笔畅" "http://music.yuti.site/music-%E6%9C%80%E7%BE%8E%E7%9A%84%E6%9C%9F%E5%BE%85.mp3" "http://music.yuti.site/pic-%E6%9C%80%E7%BE%8E%E7%9A%84%E6%9C%9F%E5%BE%85.jpg" "autoplay" %}

```

### dplayer

```
{% dplayer "url=mp4的地址" "pic=图片的地址" "loop=yes" "theme=#FADFA3" "autoplay" "token=tokendemo" %}

```
当然**"pic=图片的地址"**不写也是没问题的

下面我给出一个实际的例子, 我这里取消了自动播放功能


```
{% dplayer "url=http://music.yuti.site/mv-%E5%AD%A6%E4%B8%8D%E4%BC%9A.mp4" "loop=yes" "theme=#FADFA3" "token=tokendemo" %}

```


{% dplayer "url=http://music.yuti.site/mv-%E5%AD%A6%E4%B8%8D%E4%BC%9A.mp4" "loop=yes" "theme=#FADFA3" "token=tokendemo" %}
<center><p>学不会</p></center>

马郁这是我在小学五六年级最喜欢的歌手，当时的我一有空就拿着复读机听她的歌，我在考研的那个阶段又偶然间听到这首歌，心中没有澎湃与激动，只有平静，脑海里只是浮现着冬天，田地，小姑娘组成的画面。

图片、音乐、音频的存储我使用了七牛云

