---
title: 解决：pjax导致无法初始化aplayer播放器
date: 2020-06-26 22:13:37
categories: 随记分享
tags:
  - hexo
  - pjax
  - aplayer
description: 解决pjax导致无法初始化aplayer播放器
cover: https://upyun-cdn.mistill.com/img/post_cover/post_cover_014.webp
abbrlink: pjax-case-aplayer-erro
---

# 背景

由于想让博客拥有更好的浏览体验，启用了hexo next主题的的pjax功能(非常感谢next主题已经实现此功能)，这样可以实现全站局部刷新从而提升加载速度。



开启之后：

## 优点

1.加载速度明显提升

2.页面切换不会影响左侧背景音乐播放

<!-- more -->

## 缺点

1.右侧文章列表、文章详细页面**aplayer**无法初始化



# 解决方法

[hexo-tag-aplayer官方文档](https://github.com/MoePlayer/hexo-tag-aplayer/blob/master/docs/README-zh_cn.md) 给出了相关的解决办法，如下

```javascript
# 手动清理Aplayer全局实例：
$(document).on('pjax:start', function () {
    if (window.aplayers) {
        for (let i = 0; i < window.aplayers.length; i++) {
            window.aplayers[i].destroy();
        }
        window.aplayers = [];
    }
});
```

但由于自己未深入学习，不知道这个实例应该添加到哪个文件，于是就暂时放弃。



以下转载自[YANG个人博客]([https://yxyvpn.com/2020/04/15/pjax%E5%AF%BC%E8%87%B4%E6%97%A0%E6%B3%95%E5%88%9D%E5%A7%8B%E5%8C%96aplayer%E9%9F%B3%E4%B9%90%E6%92%AD%E6%94%BE%E5%99%A8/](https://yxyvpn.com/2020/04/15/pjax导致无法初始化aplayer音乐播放器/))

## 源码分析

其实问题也好解决，由于博客用的是metingJS插件初始化aplayer,那么只要在pjax success函数里面调用metingJS初始化函数即可。

我们来看metingJS源代码,需要注意的是：hexo-tag-aplayer插件最后一次更新为两年前，仅支持到metingjs 1.2.0版本，所以需要找到tag目录下的1.2.0源码，github地址 [metingJS](https://github.com/metowolf/MetingJS/blob/v1.2/src/Meting.js),。

显然，此代码会在 dom加载完之后调用 **loadMeting**进行初始化。

```javascript
console.log(`${'\n'} %c MetingJS v1.2.0 %c https://github.com/metowolf/MetingJS ${'\n'}`, 'color: #fadfa3; background: #030307; padding:5px 0;', 'background: #fadfa3; padding:5px 0;');

let aplayers = [];
let loadMeting = () => {
    let api = 'https://api.i-meto.com/meting/api?server=:server&type=:type&id=:id&r=:r';
    if (typeof meting_api !== 'undefined') api = meting_api;

    for (let i = 0; i < aplayers.length; i++) {
        if(!aplayers[i].container.classList.contains("no-destroy")){
            try {
                aplayers[i].destroy();
            } catch (e) {
                console.log(e);
            }
        }
    }
    aplayers = [];

    let elements = document.querySelectorAll(".aplayer");

    for (var i = 0; i < elements.length; i++) {
        const el = elements[i];
        if(el.classList.contains("no-reload")) continue;
	if(el.classList.contains("no-destroy")) el.classList.add("no-reload");
        let id = el.dataset.id;
        if (id) {
            let url = el.dataset.api || api;
            url = url.replace(":server", el.dataset.server);
            url = url.replace(":type", el.dataset.type);
            url = url.replace(":id", el.dataset.id);
            url = url.replace(":auth", el.dataset.auth);
            url = url.replace(":r", Math.random());

            const xhr = new XMLHttpRequest();
            xhr.onreadystatechange = () => {
                if (xhr.readyState === 4) {
                    if (xhr.status >= 200 && xhr.status < 300 || xhr.status === 304) {
                        let response = JSON.parse(xhr.responseText);
                        build(el, response);
                    }
                }
            };
            xhr.open('get', url, true);
            xhr.send(null);

        } else if (el.dataset.url) {
            let data = [{
                name: el.dataset.name || el.dataset.title || 'Audio name',
                artist: el.dataset.artist || el.dataset.author || 'Audio artist',
                url: el.dataset.url,
                cover: el.dataset.cover || el.dataset.pic,
                lrc: el.dataset.lrc,
                type: el.dataset.type || 'auto'
            }];

            build(el, data);
        }
    }

    function build(element, music) {

        let defaultOption = {
            container: element,
            audio: music,
            mini: null,
            fixed: null,
            autoplay: false,
            mutex: true,
            lrcType: 3,
            listFolded: false,
            preload: 'auto',
            theme: '#2980b9',
            loop: 'all',
            order: 'list',
            volume: null,
            listMaxHeight: null,
            customAudioType: null,
            storageName: 'metingjs'
        };

        if (!music.length) {
            return;
        }

        if (!music[0].lrc) {
            defaultOption['lrcType'] = 0;
        }

        let options = {};
        for (const defaultKey in defaultOption) {
            let eleKey = defaultKey.toLowerCase();
            if (element.dataset.hasOwnProperty(eleKey) || element.dataset.hasOwnProperty(defaultKey) || defaultOption[defaultKey] !== null) {
                options[defaultKey] = element.dataset[eleKey] || element.dataset[defaultKey] || defaultOption[defaultKey];
                if (options[defaultKey] === 'true' || options[defaultKey] === 'false') {
                    options[defaultKey] = (options[defaultKey] == 'true');
                }
            }
        }

        aplayers.push(new APlayer(options));
    }
}

document.addEventListener('DOMContentLoaded', loadMeting, false);
```

## 解决方法(初步)

回到我们的hexo next主题博客源文件，其它主题同理，找到对应的地方修改即可。

`themes\next\layout_scripts\pjax.swig`，在56行下面调用即可，问题解决。

```javascript
window.addEventListener('pjax:success', () => {
    ...篇幅原因，省略部分代码...
56    NexT.utils.updateSidebarPosition();
57    loadMeting();
})
```

博主用的next版本实在这个路径`themes/next/layout/_scripts/pjax.njk`在这个文件中倒数第三行修改：

```javascript
  NexT.utils.updateSidebarPosition();
  loadMeting();
});
```

这样又产生个问题，loadMeting 会把左侧的背景音乐也重新初始化一遍导致音乐中断。



## 解决方法(最终)

其实，github release已有说明 地址：[重新初始化问题](https://github.com/metowolf/MetingJS/releases)

> 当播放器的容器带有 `no-destroy` 类时该播放器不会被销毁与重载，适合不间断播放的全站播放器使用。
> 不影响第一次加载。

那么标签定义改成如下即可 增加一个 no-destroy

```html
<div class="aplayer no-destroy" data-id="{{theme.background_music.id}}" data-autoplay="      {{theme.background_music.autoplay}}" data-server="{{theme.background_music.server}}"       data-type="{{theme.background_music.type}}" data-order="       {{theme.background_music.order}}">
</div>
```

由于[jsdelivr/meting](https://www.jsdelivr.com/package/npm/meting?path=dist&version=1.2.0)上1.2.0的版本并没有更新这个代码，所以无法使用CDN，好在文件不大，压缩后2kb而已，直接本地加载。

如何测试？请用电脑打开本网站，先点击左侧**站点概览**下的背景音乐播放，再点击下方链接，可以看到 文章歌单正常加载，左侧背景音乐无中断。

至此，问题完美解决，众人拾柴火焰高，也许这就是开源的魅力。



# 注意事项

你需要在你主题的head或者footer文件导入aplayer和metingjs文件

hexo next主题footer文件如下

```
next\layout\_partials\footer.swig
```

引入aplayer和metingjs库，metingjs依赖aplayer，所以请注意顺序。

请注意，metingjs请去上面指定的地址下载，也可下载本网站的，并放到博客的source目录下，我这里是source/lib/metingjs，由于source是网站根目录，所以可以不写，最好用压缩版。

```html
<link rel="stylesheet" href="https://cdn.bootcss.com/aplayer/1.10.1/APlayer.min.css">
<script src="https://cdn.bootcss.com/aplayer/1.10.1/APlayer.min.js"></script>
<script src="/lib/metingjs/Meting.min.js"></script>
```

hexo配置文件_config.yml的aplayer修改

```javascript
aplayer:
  meting: true
  asset_inject: false #表示不自动注入js和css
```