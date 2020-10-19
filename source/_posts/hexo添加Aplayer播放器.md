---
title: hexo添加Aplayer播放器
date: 2020-06-26 22:12:52
categories: 随记分享
tags:
  - hexo
  - aplayer
description: 记录一下怎么给用了`HEXO`博客添加这款播放器，并配合`Meting`插件插入在线音乐。
cover: https://blog-butterfly-cdn.mistill.com/img/post_cover/post_cover_018.webp
abbrlink: hexo-inject-aplayer
---

![](https://blog-butterfly-cdn.mistill.com/img/post_img/df727d58ly1gg61wr553vj20v204w3yl.jpg)

`Aplayer`是一款漂亮的`html5`播放器，配合`Meting`插件可以直接在博客中插入QQ、网易云中的音乐。

记录一下怎么给用了`HEXO`博客添加这款播放器，并配合`Meting`插件插入在线音乐。

<!-- more -->

首先感谢以下大佬的开源项目：

MoePlayer：[APlayer](https://github.com/MoePlayer/APlayer)

metowolf：[Meting](https://github.com/metowolf/Meting)

Moeplayer：[hexo-tag-aplayer](https://github.com/MoePlayer/hexo-tag-aplayer)



# 安装 hexo-tag-aplayer 插件

hexo-tag-aplayer 是Aplayer在hexo上的插件，这里的配置参考的是[官方文档](https://links.jianshu.com/go?to=https%3A%2F%2Fgithub.com%2FMoePlayer%2Fhexo-tag-aplayer%2Fblob%2Fmaster%2Fdocs%2FREADME-zh_cn.md) ，安装 hexo-tag-aplayer

```bash
npm install --save hexo-tag-aplayer
```



# 开启 Meting

最新版的 hexo-tag-aplayer 已经支持了MetingJS的使用，可以直接解析网络平台的歌曲，首先要在**站点配置文件**中开启meting模式，添加以下代码在配置文件的最后：

```bash
aplayer:
  meting: true
```



# 在文章中插入播放器

接着就可以 在文章中使用 MetingJS 播放器了：

```bash
<!-- 简单示例 (id, server, type)  -->
{% meting "60198" "netease" "playlist" %}

<!-- 进阶示例 -->
{% meting "60198" "netease" "playlist" "autoplay" "mutex:false" "listmaxheight:340px" "preload:none" "theme:#ad7a86"%}
```



有关的选项列表如下:

| 选项          | 默认值     | 描述                                                        |
| ------------- | ---------- | ----------------------------------------------------------- |
| id            | **必须值** | 歌曲 id / 播放列表 id / 相册 id / 搜索关键字                |
| server        | **必须值** | 音乐平台: `netease`, `tencent`, `kugou`, `xiami`, `baidu`   |
| type          | **必须值** | `song`, `playlist`, `album`, `search`, `artist`             |
| fixed         | `false`    | 开启固定模式                                                |
| mini          | `false`    | 开启迷你模式                                                |
| loop          | `all`      | 列表循环模式：`all`, `one`,`none`                           |
| order         | `list`     | 列表播放模式： `list`, `random`                             |
| volume        | 0.7        | 播放器音量                                                  |
| lrctype       | 0          | 歌词格式类型                                                |
| listfolded    | `false`    | 指定音乐播放列表是否折叠                                    |
| storagename   | `metingjs` | LocalStorage 中存储播放器设定的键名                         |
| autoplay      | `true`     | 自动播放，移动端浏览器暂时不支持此功能                      |
| mutex         | `true`     | 该选项开启时，如果同页面有其他 aplayer 播放，该播放器会暂停 |
| listmaxheight | `340px`    | 播放列表的最大长度                                          |
| preload       | `auto`     | 音乐文件预载入模式，可选项： `none`, `metadata`, `auto`     |
| theme         | `#ad7a86`  | 播放器风格色彩设置                                          |