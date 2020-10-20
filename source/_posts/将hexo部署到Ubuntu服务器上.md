---
title: 将hexo部署到Ubuntu服务器上
date: 2020-07-16 12:04:43
categories: 随记分享
tags:
  - hexo
  - 腾讯云
  - CVM
description: 将博客迁移到腾讯云CVM做一个简单记录。
cover: https://upyun-cdn.mistill.com/img/post_cover/post_cover_013.webp
abbrlink: hexo-lay-tencent-cvm
---

# 前言

趁着腾讯云活动弄了一台1H2G1M的CVM，这个博客一直托管在Coding pages上面，想着刚好买了顺便备案，就准备把博客迁移到这上面，做一个简单记录。一句话，其实就是给自己服务器上建一个git库就好。

# 本地安装Hexo,node.js,git

前提就是本地已经搭建了Hexo博客并且成功运行，就不再赘述。

# 服务器端

腾讯云CVM，可以用`ubuntu`用户身份正常登陆.

## 配置SSH

配置服务器的登陆选项，添加SSH，SSH公钥就用之前安装git时生成的公钥即可.

在本地下载Xshell等工具，登陆方式也可以选为本地的私钥.

> 注意在使用Xshell等终端时，若不小心键入了`ctrl+s`, 则这个命令为暂时挂起终端，只需要按`ctrl+q`即可继续输入

## 安装Git和Nginx

Git 用于版本管理和部署，Nginx 用于静态博客托管。

腾讯云Ubuntu自带了git。安装nginx即可。



```shell
sudo apt-get update
sudo apt-get install git nginx -y
```

## 创建Git仓库



在`/var/repo/`下创建名为`hexoblog`的裸仓库。用如下命令



```shell
sudo mkdir /var/repo/
sudo chown -R $USER:$USER /var/repo/
sudo chmod -R 755 /var/repo/

cd /var/repo/
git init --bare hexoblog.git
```

## 配置Nginx托管文件目录



创建`/var/www/hexo`目录，用于Nginx托管，修改目录所有权和权限。



```shell
sudo mkdir -p /var/www/hexo

sudo chown -R $USER:$USER /var/www/hexo
sudo chmod -R 755 /var/www/hexo
```



随后修改Nginx的`default`设置，使`root`指向`hexo`目录.



```shell
sudo vim /etc/nginx/sites-available/default
```



注意一定要加`sudo`,否则会提醒`default`是只读文件.

修改文件中对应的项



```
...

server {
    listen 80 default_server;
    listen [::]:80 default_server ipv6only=on;

    root /var/www/hexo; # 需要修改的部分
    index index.html index.htm;
...
```

> Vim的操作方法比较特殊，可以在网上查查

重启Nginx服务，使得改动生效。



```shell
sudo service nginx restart
```



## 创建Git钩子



不了解钩子是什么，就照着做了。

在自动生成的 hooks 目录下创建一个新的钩子文件：



```shell
vim /var/repo/hexoblog.git/hooks/post-receive
```



在该文件中添加两行代码，指定 Git 的工作树（源代码）和 Git 目录（配置文件等）。



```bash
#!/bin/bash

git --work-tree=/var/www/hexo --git-dir=/var/repo/hexoblog.git checkout -f
```



保存并退出文件，并让该文件变为可执行文件。



```shell
chmod +x /var/repo/hexoblog.git/hooks/post-receive
```

# 回到本地配置

## 修改Hexo的默认配置

在站点config.yml中修改博客的地址`url`



```shell
# URL
## If your site is put in a subdirectory, set url as 'http://yoursite.com/child' and root as '/child/'

url: http://server-ip # 没有绑定域名时填写服务器的实际 IP 地址。
root: /
permalink: :year/:month/:day/:title/
permalink_defaults:
```

## 通过Git部署

先在任意位置处打开powershell, 从服务器上把`hexo_static`仓库克隆下来, 以此来将服务器地址添加到受信任的站点中。



```shell
git clone ubuntu@server_ip:/var/repo/hexo_static.git
```



注意在第一次进行这一步时会提示是否继续，选yes即可。

再编辑Hexo的`config.yml`文件，找到Deployment, 修改为



```yml
deploy:
  type: git
   repo: ubuntu@server_ip:/var/repo/hexo_static.git
  branch: master
```



最后记得安装Hexo部署到Git仓库的包.



```shell
npm install hexo-deployer-git --save
```



于是就可用`hexo d`命令来部署了。大功告成。

