---
title: html-css相关
date: 2016-05-15 22:48:30
tags: html5
---
# html-css相关.md
##  html 强制换行 
> word-wrap:break-word; 和 word-break:break-all 的区别

1. word-break:break-all 例如div宽200px，它的内容就会到200px自动换行，如果该行末端有个英文单词很长（congratulation等），它会把单词截断，变成该行末端为conra(congratulation的前端部分)，下一行为tulation（conguatulation）的后端部分了。
2. word-wrap:break-word 例子与上面一样，但区别就是它会把congratulation整个单词看成一个整体，如果该行末端宽度不够显示整个单词，它会自动把整个单词放到下一行，而不会把单词截断掉的。