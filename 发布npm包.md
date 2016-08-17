---
title: '''发布npm包'''
date: 2016-08-17 17:51:27
tags: nodeJs
---

__发布一个say-hello-world的package到npm; 这个package的功能是提供一个sayHelloWorld的方法。__

`注意：因为say-hello-world package已经发布到npm了，所以大家在跟随文档操作的时候需要换个名字。`
* 第一步:
  在项目的根目录下创建一个名字为node_modules的目录，此目录用来放置所有的node模块

* 第二步:
  在node_modules目录下名字say-hello-world目录;

* 第三步:
  say-hello-world目录下新建两个文件：
  * index.js
        function sayHelloWorld() {
          console.log("Hello world !");
        }
        module.exports = sayHelloWorld;

  * package.json
        {
          "name": "say-hello-world", // package的名称
          "author": "yourname <me@hello.com> (http://hello.com)", // 作者的相关信息
          "version": "0.0.1", // 版本号(semantic version)
          "main": "index" // 入口文件，当在其他文件中require('say-hello-world')时，将会加载index.js
        }
  * 发布say-hello-world包到npm
    - 首先要[注册一个npm账号](https://www.npmjs.com/signup)(如果没有的话)
    - 注册完后，在命令窗口运行`npm adduser`(登陆npm),会提示你输入用户名和密码；
    - 登陆成功后，在say-hello-world目录下执行命令`npm publish`(发布package)
    - 发布成功后就可以[登陆到npm官网](https://www.npmjs.com/login)去看自己发布的package。

`到这里，我们已经成功发布了say-hello-world包到npm，接下来我们来尝试使用一下say-hello-world包`

1. 先新建一个空的目录`test`;然后在命令行中切换到`test`目录;
2. 然后执行`npm install say-hello-world`命令;
3. 执行成功后在`test`目录下看到多了一个`node_modules`的目录，在`node_modules`目录中就可以看到我们刚才发布的`say-hello-world`package;
4. 然后再`test`目录下新建一个`hello-world.js`来测试一下`sayHelloWorld()`方法，`hello-world.js`中的内容如下：
        var sayHelloWorld = require('say-hello-world');
        sayHelloWorld();
5. 在命令行中进入`test`目录，然后执行`node hello-world.js`,就会在看到输出：`Hello world !`.

__如何更新发布到npm的package？(以刚才发布的say-hello-world为例)__

`当我们对say-hello-world做了改动就需要更新到npm.`

* 进入到`say-hello-world`目录, 对`index.js`做一些修改(做为要更新的内容)
* 然后再命令行执行`npm version patch`, 此命令会把`package.json`的`version`更新到`0.02`
* 然后执行`npm publish`就可以更新到npm了