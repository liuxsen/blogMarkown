---
title: '''更改hosts翻墙'''
date: 2016-08-09 14:57:35
tags: 翻墙整理
---
# win10更改hosts之后重启仍然无法翻墙使用google等

1. win + r 打开"运行" , 然后输入 cmd 打开 DOS 命令窗口
2. 执行ping www.google.com 如果不通，重新修改hosts,点这里 
3. 直到可以ping通,打开google浏览器
4. 在上面的网址栏输入：chrome://net-internals/
5. export下拉选择HSTS
6. 在Domain中分别加入www.google.com、www.google.com.cn、www.google.com.hk、www.google.com.tw
7. 重新试一试www.google.com能访问不
