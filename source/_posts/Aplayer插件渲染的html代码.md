---
title: hexo-tag-aplayer插件渲染的html代码
date: 2020-10-15 15:00:00
categories: 随记分享
tags: 
    - hexo
    - html
    - 学习
description: 不想使用hexo-tag-aplayer插件，可以直接在md文件中插入Html代码。
aplayer: true
keywords: 
    - hexo
    - aplayer
cover: https://blog-butterfly-cdn.mistill.com/img/post_cover/post_cover_017.webp
abbrlink: aplayer-render-html
---

## 自建服务器(单曲)
### demo
<div class="aplayer" 
data-name="七里香" 
data-artist="周杰伦" 
data-url="https://blog-butterfly-cdn.mistill.com/music/七里香 - 周杰伦.mp3" 
data-cover="https://blog-butterfly-cdn.mistill.com/music/七里香 - 周杰伦.jpg" 
data-lrc="https://blog-butterfly-cdn.mistill.com/music/七里香 - 周杰伦.lrc" 
data-preload="none" 
data-autoplay="false" 
data-mutex="true"></div>

### 代码
```html
<div class="aplayer" 
data-name="七里香" 
data-artist="周杰伦" 
data-url="https://cdn.jsdelivr.net/gh/lemon-yuan/CDN@master/music/七里香 - 周杰伦.mp3" 
data-cover="https://cdn.jsdelivr.net/gh/lemon-yuan/CDN@master/music/七里香 - 周杰伦.jpg" 
data-lrc="https://cdn.jsdelivr.net/gh/lemon-yuan/CDN@master/music/七里香 - 周杰伦.lrc" 
data-preload="none" 
data-autoplay="false" 
data-mutex="true"></div>
```

---
## 歌手
### demo
<div class="aplayer" 
data-id="000PeZCQ1i4XVs" 
data-server="tencent" 
data-type="artist" 
data-order="random" 
data-preload="none" 
data-autoplay="false"
data-mutex="true"></div>

### 代码
```html
<div class="aplayer" 
data-id="000PeZCQ1i4XVs" 
data-server="tencent" 
data-type="artist" 
data-order="random" 
data-preload="none" 
data-autoplay="false"
data-mutex="true"></div>
```

---
## 歌单
### demo
<div class="aplayer" 
data-id="5089993118" 
data-server="netease" 
data-type="playlist" 
data-order="random" 
data-preload="none" 
data-autoplay="false"
data-mutex="true"></div>

### 代码
```html
<div class="aplayer" 
data-id="5089993118" 
data-server="netease" 
data-type="playlist" 
data-order="random" 
data-preload="none" 
data-autoplay="false"
data-mutex="true"></div>
```

---
## 单曲
### demo
<div class="aplayer" 
data-id="004Fimy419PpsA" 
data-server="tencent" 
data-type="song" 
data-preload="none" 
data-autoplay="false"
data-mutex="true"></div>

### 代码
```html
<div class="aplayer" 
data-id="004Fimy419PpsA" 
data-server="tencent" 
data-type="song" 
data-preload="none" 
data-autoplay="false"
data-mutex="true"></div>
```
