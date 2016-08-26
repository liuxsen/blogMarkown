---
title: 'php'
date: 2016-05-15 22:00:07
tags: php
---
# 原生安装php环境配置.

> 配置apache解析 php文件，

+ 修改apache/conf/httpd.conf
+ 添加如下代码

```
# 第一步： 装载php5模块
# LoadModule php5_module 'php5的模块文件，表示装载php5模块'
# 其中php5 模块文件在 ： php语言包/php5apache2_2.dll
LoadModule php5_module "D:/amp/php/php5apache2_2.dll"

# 第二步： 指定php后缀的文件应该调用php模块去执行
<FilesMatch "\.php$">
    setHandler application/x-httpd-php
</FilesMatch>
# 解释1： "\.php$" 表示所有php后缀文件
# 解释2 setHandler 表示该类文件由php模块解析

#　设置 php.ini的位置(设定到文件夹就可以了)
PHPIniDir "D:/amp/php"
```

> apache 配置

1. httpd.exe 可以检测httpd.conf的语法错误 语法是 httpd.exe -t

> 配置php的基本运行环境

1. - php.ini-development 开发配置
   - php.ini-production 产品阶段配置
   - 修改其中一个后缀 为php.ini
2. 配置时区（中国时区）
    - 搜索 timezone
    -  修改 ;date.timezone= 为 date.timezone = PRC
3. 打开php的mysql模块
    - 在php.ini 中搜索 php_mysql 打开注释 php_mysql php_mysqli
    - 在php.ini 中修改 模块的实际路径 搜索 extension_dir 打开注释并且 修改路径 如 extension_dir = "D:/amp/php/ext" 

> mysql 安装

1. mysql安装失败
    1. 设置文件夹选项，勾选显示隐藏文件
    2. 在C盘下找到ProgramData文件夹下的MySQL,直接删除
    3. 重新安装MySQL，问题即可解决

> 虚拟主机配置

1. 端口监听

    - 名词解释

        + 端口，就是一个数字，目的是让一台电脑能够对外提供多项服务 （多种功能）
        + 行业服务默认常见端口
            + web服务： 80
            + ftp服务 ： 21
            + 邮件收取服务： 110
            + 邮件发送服务： 25
            + mysql数据库服务： 3306
            + 一般只会提供几个服务
            
    - 添加端口
        - 打开apache配置文件 httpd.conf 搜 listen
        -  添加形如  Listen 8080
        -  重启服务器
        
    - 主机配置关键项
        + 访问系统hosts文件 路径 C:\Windows\System32\drivers\etc
            - 访问的时候，需要编辑器通过管理员身份打开；
            - 打开目录的时候，可能没有etc 的文件夹，可以手动搜索 etc hosts
            
        + 名词解释
            
            - *主机，虚拟主机，web站点* 是指一个可以通过浏览器并使用某个域名进行访问的“web应用”
            - 主机（站点） 的名字： servername 主机名
            - 主机（站点）的实际文件夹位置； documentRoot "站点的实际完成路径"
            - apache 的作用就是一个“转换角色”： 将当前电脑中的某个文件夹，对外以某个域名（站点）的方式展现出来，站点的本质就是一个文件夹
        + 设置apache 的域名 servername 以及 访问路径 documentroot

            - 在httpd.conf 中搜索 servername 加形如 ServerName www.liu.com:80
            - 在httpd.conf 中搜索 DocumentRoot 修改路径 DocumentRoot "F:/phpCode"
            - 在httpd.conf 中搜索 DocumentRoot 加形如 
            
            ```
                <Directory "F:/phpCode">
                    # 下一行用于设定 "可显示文件列表"（当无可现实网页的时候） 
                    Options Indexes
                    # 用于设定权限的判断顺序，先拒绝，后允许
                    Order deny,allow
                    # Deny from 192.168.3.33
                    # 允许所有（这里没有设定拒绝）
                    Allow from all
                </Directory>
            ```

        - 修改默认的网站首页
            - 在http.conf 中搜索 directoryIndex 修改 文件格式 形如 DirectoryIndex index.html index.php   

2. 多站点配置
    - 在 httpd.conf 中打开多站点配置文件 搜索 hosts
    - 设置 NameVirtualHost Ip
    - * 可以代表当前服务器的所有的地址，通常只有一个
    - 打开 httpd-vhosts.conf 文件， 搜索 NamevirtualHost
    添加如下代码

    ```
    # 站点1
<VirtualHost *:80>
    DocumentRoot "F:/phpCode"
    # 站点名字
    ServerName www.liu.com
    # 站点别名
    ServerAlias liu.com

    <Directory "F:/phpCode">
        # 可以列出文件目录
        options indexes
        allow from all
        # 设置 站点首页
        DirectoryIndex index.html index.php
    </Directory>

</VirtualHost>
    ```

    - 注意修改系统hosts文件

```
127.0.0.1   www.liu.com
127.0.0.1   liu.com
127.0.0.1   www.liu2.com
127.0.0.1   liu2.com
```