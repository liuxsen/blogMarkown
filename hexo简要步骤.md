---
title: '''hexo简要步骤'''
date: 2016-05-15 21:32:13
tags:
---

##安装Hexo

```
   $ cd d:/hexo
   $ npm install hexo-cli -g
   $ hexo init blog
   $ cd blog
   $ npm install
   $ hexo g # 或者hexo generate
   $ hexo s # 或者hexo server，可以在http://localhost:4000/ 查看   
```
>这里有必要提下Hexo常用的几个命令：

1. hexo generate (hexo g) 生成静态文件，会在当前目录下生成一个新的叫做public的文件夹
2. hexo server (hexo s) 启动本地web服务，用于博客的预览
3. hexo deploy (hexo d) 部署播客到远端（比如github, heroku等平台）

>另外还有其他几个常用命令：

1. $ hexo new "postName" #新建文章
2. $ hexo new page "pageName" #新建页面

```
$ hexo n == hexo new
$ hexo g == hexo generate
$ hexo s == hexo server
$ hexo d == hexo deploy
```
##安装主题

```
$ hexo clean
$ git clone https://github.com/litten/hexo-theme-yilia.git themes/yilia
```
>启用主题

修改Hexo目录下的_config.yml配置文件中的theme属性，将其设置为yilia。

>更新主题

```
$ cd themes/yilia
$ git pull
$ hexo g # 生成
$ hexo s # 启动本地web服务器
```
##使用hexo deploy部署

>使用git命令行部署

##clone github repo

```
$ cd d:/hexo/blog
$ git clone https://github.com/liuxsen/liuxsen.github.io.git .deploy/liuxsen.github.io;
```
>hexo g 

 ##生成静态网站

>hexo s 

##预览网站


>部署

将public下面的文件复制到 liuxsen.github.io 文件夹下面 用小乌龟 commit push
