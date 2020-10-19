---
title: Github Actions自动部署Hexo博客至个人服务器
date: 2020-10-19 17:34:24
categories: 随记分享
tags: 
    - hexo
    - github
    - github actions
description: 随着本地Hexo目录的体积越来越大，个人pc发布到服务器需要各种命令，并且生成时间越来越长，现在就利用Github Actions来自动化这个流程。
cover: https://blog-butterfly-cdn.mistill.com/img/post_cover/post_cover_022.webp
abbrlink: githubactions-deploy-host
---
# 前言
自`Github Actions`出来就一直想抽空折腾学习一下，刚好趁着最近网站换主题，便稍微折腾了一下，浅尝辄止，未进行深入学习。
因为自己的pc性能有限，在Hexo文章和使用的插件越来越多的情况下，个人pc每次`hexo g`都需要好一会，并且还要各种命令都再输入一遍，非常繁琐。而Github Actions刚好解决了这个痛点，一方面全自动化流程，不用人工输入；另一方面，github拥有强大的服务器，`npm install`一瞬间就能完成的事情，生成Hexo更是绰绰有余。

{% note warning flat %}
个人服务器是自建了git库，利用`hook`钩子发布到网站根目录。所以这篇教程最终是利用`hexo deploy`进行上传到服务器操作。
具体查阅：[点击这里](https://mistill.com/posts/hexo-lay-tencent-cvm/)
{% endnote %}

# 新建仓库
- 建议新建一个`Github`私有仓库，用来存储Hexo工程文件。
{% note info flat %}
个人建议没必要把Hexo工程文件中的`node_modules`文件夹上传，因为`Gihub Actions`的处理速度非常快，一瞬间就能把插件和依赖安装完成。
{% endnote %}

# 仓库配置
进入仓库`Setting`页面，在`Secrets`里面点击`New Secrets`;
`Name`设置为`HEXO_DEPLOY_PRI`，`Value`值复制你使用SSH连接服务器对应的**私钥**，千万不能复制错。
![](https://blog-butterfly-cdn.mistill.com/img/post_img/post_img_001.jpeg)

# 工作流配置
{% note warning flat %}
请确保本地搭建成功，并且`hexo deploy`至个人服务器也是没有问题的。
{% endnote %}
- 触发条件是仓库文件有变更，即进行`git push`操作是，便会触发。
在仓库根目录下创建`.github/workflows/deploy.yml`
目录结构如下：
```bash
blog (repository)
└── .github
    └── workflows
        └── deploy.yml
```
在`deploy.yml`粘贴以下内容，并根据实际情况修改。
```yml
name: Blog CI/CD

on:
  push:
    branches: 
      - master


jobs:
  blog-cicd:
    name: Hexo blog build & deploy
    runs-on: ubuntu-latest
  
    steps:
      - name: Checkout codes
        uses: actions/checkout@v2

      - name: Setup node
        uses: actions/setup-node@v1
        with:
          node-version: '12.x'
      
      - name: Setup Hexo env
        run: |
          npm install hexo-cli -g
          npm install
      
      - name: Configuration environment
        env:
          ACTION_DEPLOY_KEY: ${{ secrets.HEXO_DEPLOY_PRI }}
        run: |
          sudo timedatectl set-timezone "Asia/Shanghai"
          mkdir -p ~/.ssh/
          echo "$ACTION_DEPLOY_KEY" > ~/.ssh/id_rsa
          chmod 600 ~/.ssh/id_rsa
          ssh-keyscan xx.xx.xx.xxx >> ~/.ssh/known_hosts  #此处填写你的服务器IP
          git config --global user.name "your username"
          git config --global user.email "your email"
          
      - name: Generate public files
        run: |
          hexo clean
          hexo g
      
      - name: Generate douban files  #豆瓣插件，没有可以删除这个step
        run: |
          hexo douban -m
      
      - name: Deploy hexo
        run: |
          hexo deploy
```
## 模板参数说明
- name 为此 Action 的名字
- on 触发条件，当满足条件时会触发此任务，这里的 on.push.branches.$.master 是指当 master 分支收到 push 后执行任务。
- env 为环境变量对象
    - env.GIT_USER 为 Hexo 编译后使用此 git 用户部署到仓库。
    - env.GIT_EMAIL 为 Hexo 编译后使用此 git 邮箱部署到仓库。
    - env.THEME_REPO 为您的 Hexo 所使用的主题的仓库，这里为 sanonz/hexo-theme-concise。
    - env.THEME_BRANCH 为您的 Hexo 所使用的主题仓库的版本，可以是：branch、tag 或者 SHA。
    - env.DEPLOY_REPO 为 Hexo 编译后要部署的仓库，例如：sanonz/sanonz.github.io。
    - env.DEPLOY_BRANCH 为 Hexo 编译后要部署到的分支，例如：master。
- jobs 为此 Action 下的任务列表
    - jobs.{job}.name 任务名称
    - jobs.{job}.runs-on 任务所需容器，可选值：ubuntu-latest、windows-latest、macos-latest。
    - jobs.{job}.strategy 策略下可以写 array 格式，此 job 会遍历此数组执行。
    - jobs.{job}.steps 一个步骤数组，可以把所要干的事分步骤放到这里。
    - jobs.{job}.steps.$.name 步骤名，编译时会会以 LOG 形式输出。
    - jobs.{job}.steps.$.uses 所要调用的 Action，可以到 https://github.com/actions 查看更多。
    - jobs.{job}.steps.$.with 一个对象，调用 Action 传的参数，具体可以查看所使用 Action 的说明。

# 查看执行情况
- 在仓库页点击`Actions`即可查看执行情况。
![](https://blog-butterfly-cdn.mistill.com/img/post_img/post_img_002.jpeg)
可以看到，交给`Github Actions`处理，速度很快。
而我们只需要进行`git push`便可完成整个操作。
