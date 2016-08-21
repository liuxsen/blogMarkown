---
title: hexo
date: 2016-08-07 17:17:26
tags: hexo相关整理
---
![hexo](hexo/hexo.png)

在hexo中无痛引用图片路径
-------------

1. 首先确认 _config.yml 中有 post_asset_folder:true 。
2. 在 hexo 目录，执行
```
npm install https://github.com/CodeFalling/hexo-asset-image --save
```

引用图片
-----
```
![hexo](hexo/hexo.png)
```
