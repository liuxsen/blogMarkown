# mongodb 下载安装步骤

+ [下载安装地址](https://www.mongodb.com/download-center#community)
+ 可以将bin目录添加到环境变量中

>mongod.exe或mongo.exe双击一闪就关闭问题

+ 解决方案

+ 在安装mongodb后，看是否在安装磁盘根目录下有data文件夹，如果没有，需要在磁盘根目录下建立data文件夹，然后再data文件夹下建立db文件夹，在运行，即可。

+  mongodb 运行方式
    - 在bin目录中 用命令行窗口打开； 执行 mongod --dbpath ../blog
    - 用于指定数据库存储的位置；
