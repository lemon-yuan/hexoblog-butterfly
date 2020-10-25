---
title: hexo加载Valine评论浏览器提示不安全解决办法
date: 2020-10-25 23:12:15
categories: 随记分享
tags:
    - hexo
    - Valine
description: 加载了Valine评论后，浏览器的"绿锁"会变成"不安全"。
cover: https://upyun-cdn.mistill.com/img/post_cover/post_cover_023.webp
abbrlink: hexo-valine-ssl-nosafe
---
# 背景
遇到一个奇怪的问题，我的网站一直是全站`https`，浏览器的`绿锁`也一直显示正常。但今天偶然性会出现`绿锁`变`不安全`，经过反复测试进行问题重现，定位到是加载了`Valine`评论后，出现上述情况。

# 排查问题
初步排查，是`leancloud`的`api`网址的`SSL证书`过期或不匹配导致的。
首先，本网站主题`butterfly`自带了`Valine`
系统，各项配置文件都在主题目录下的`_config.yml`配置；我使用的是`Valine`国际版账号，可以免绑定自定义域名，问题应该就出在这。
经过一番搜索，最终确定问题，[原来是通用的国际版域名`us.avoscloud.com`证书已过期，](https://forum.leancloud.cn/t/us-avoscloud-com/22749)[官方也早已经不建议使用通用域名。](https://forum.leancloud.cn/t/us-avoscloud-com/23415)，而默认使用Valine配置，并且配置为国际版的`Leancloud`往往使用的就是通用域名。
![](https://upyun-cdn.mistill.com/img/post_img/post_img_003.png)
![](https://upyun-cdn.mistill.com/img/post_img/post_img_004.png)
# 解决办法
通用域名`us.avoscloud.com`现在已经恢复正常，但是毕竟还是不稳定，还是推荐指定自定义`服务器URL`。

自定义服务器的URL需要到`LeanCloud`后台查看。打开后台之后进入`Settings(设置) - App Keys(应用Keys)`，找到`Domain whitelist(域名白名单)`，里面的`Request domain(Request 域名)`里面的那个`xxxxxxxx.api.lncldglobal.com`就是你需要指定的`服务器URL`。其中xxxxxxxx就是各位的AppID的前8位字符。
![](https://upyun-cdn.mistill.com/img/post_img/post_img_005.png)

解决办法就是将`Valine`的配置项`serverURLs`填入刚刚获得的`服务器URL`。
不同主题，配置项的位置不同，以我使用的主题`Butterfly`来说，在主题文件下修改`_config.yml`或者在根目录下修改`_config.butterfly.yml`文件中的`Valine`配置项即可。
![](https://upyun-cdn.mistill.com/img/post_img/post_img_006.png)