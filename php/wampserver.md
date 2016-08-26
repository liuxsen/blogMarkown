---
title: 'php'
date: 2016-05-15 22:00:07
tags: php
---
# wampserver 配置
> 修改网站访问根目录

+  httpd.conf 搜索 documentroot 修改目录
+  httpd.conf 搜索 documentroot 往下几行 修改 directory 目录
+  修改  Allow from all

> 修改  wamp 根目录 中的 wampmanager.ini 文件

+ 搜索menu.left
+ 修改www目录  为自己自的目录

> 修改  wamp 根目录 中的 wampmanager.tpl 文件

+ 搜索menu.left
+ 修改 ${w_wwwDirectory} 改为 自己的目录

## wamp 多站点配置
+ 打开虚拟目录文件
+ D:\wamp\bin\apache\Apache2.2.21\conf\extra\httpd-vhosts.conf
+ 修改
```
<VirtualHost *:80>
    DocumentRoot "f:/phpSite/test01"
    ServerName test01.com
</VirtualHost>

<VirtualHost *:80>
    DocumentRoot "f:/phpSite/test02"
    ServerName test02.com
</VirtualHost>
```

+ 在httpd.conf 中搜索 httpd-vhost 打开多网站注释（加载httpd-vhosts.conf文件）
+ 修改 Deny from 为 Allow form
+ 打开 C:\Windows\System32\drivers\etc\host\hosts 文件
+ 添加，保存（如果不能保存成功的话，先把文件保存到桌面再覆盖就可以了）
+ 每次修改配置配置文件之后都需要重新启动所有服务；
```
127.0.0.1       test01.com
127.0.0.1       test02.com
```

> wamp 自定义端口号

+ 打开httpd.conf  搜80 修改两处
+ Listen  80 => Listen  8080
+ ServerName localhost:80 => ServerName localhost:8080