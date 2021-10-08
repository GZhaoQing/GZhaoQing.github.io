---
title: github+hexo创建静态博客
date: 2020-01-19 17:21:56
tags: [hexo, github site]
---
第一篇博客，记录一下，您面前这个页面怎么来的：
前提提要：
1.假设你有一个github用户，windows用户请额外安装Git Bash
2.假设你使用的电脑已经安装了node和npm
3.感谢这篇教程https://zhuanlan.zhihu.com/p/35668237


食材准备：
#找一个文件夹，打开gitbash，安装hexo
npm install -g hexo
#安装扩展，用于git提交和部署
npm install hexo-deployer-git --save

#git仓库准备
去github，new repository创建公共仓库；命名为“你的昵称.github.io”
#https设置
ssh -T git@github.com
ssh-keygen -t rsa -C '你的邮箱.com'
cat C:/Users/XXX/.ssh/id_rsa.pub
复制，然后去github加这个密钥

一顿操作：
hexo init
hexo s   （在本地启动看一下效果）
hexo clean
hexo generate(简写hexo g)
hexo deploy(简写hexo d)

hexo new post "github+hexo创建静态博客"
开始打字

fin！

