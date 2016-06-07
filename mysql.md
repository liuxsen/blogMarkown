# MySQL学习思路（基础部分）:
1、了解什么是数据库，以及我们为什么需要数据库？
2、了解MySQL的安装与配置。
3、掌握在MySQL环境下如何创建、修改、删除数据库。
4、掌握MySQL环境下的数据类型，主要包括字符、整型、浮点及日期，以及每种数据类型的存储特点。
5、熟练掌握MySQL环境下数据表的创建、修改、删除操作。
6、熟练掌握各种约束的使用，主要包含主键约束、唯一约束、外键约束、非空约束、默认约束。
7、熟练掌握记录的增、删、改、查等操作，也就是常说的CURD操作，当然也包括多表关联的操作。
8、掌握MySQL的运算符及内置函数的使用，主要包括字符函数库、数学函数库、日期时间函数库等。
希望对各位朋友有所帮助！

>[下载mysql](http://download.csdn.net/download/lxq_xsyu/6468461)

> 安装mysql出错

+ Mysql server instance安装中无响应问题的解决办法
1.设置文件夹选项，勾选显示隐藏文件
2.在C盘下找到ProgramData文件夹下的MySQL,直接删除
3.重新安装MySQL，问题即可解决

#mysql操作

> 停止启动服务

+ 停止mysql服务 net stop mysql
+ 启动mysql服务 net start mysql

> mysql登陆

+ mysql -V //版本
+ mysql -u //root等用户
+ mysql -p //密码
+ mysql -P //端口号
+ mysql -h //远端服务器地址 (127.0.0.1)
+ mysql -uroot -p -P3306 -h127.0.0.1
> mysql 退出

+ mysql> exit
+ mysql> quit
+ mysql> \q

> 修改MySQL提示符

+ 链接客户端的时候通过参数指定
  + shell> mysql -uroot -proot --prompt \h
+ 连接客户端之后进行修改
  + mysql> prompt 提示符
+ \D 日期
+ \d 数据库
+ \h 服务地址
+ \u 用户名

> mysql常用命令

+ 显示当前服务器版本
+ SELECT VERSION();
+ 显示当前日期时间关键字
+ SELECT NOW();
+ 显示当前用户
+ SELECT USER();

> 规范
+ 关键字与函数名称全部大写
+ 数据库名称、表名称，字段名称全部小写
+ SQL语句必须以分号结尾

> 操作数据库

+ 创建数据库
+ {}为必选 []为可选
+ CREATE {DATABASE} [IF NOT EXISTS] db_name
+ 查看当前服务器下的数据表列表
+ SHOW {DATABASES | SCHEMAS}
+ SHOW CREATE DATABASE t1;(常见数据库的详细信息)
+ 创建指定字符集的数据库
+ CREATE DATABASE t2 CHARACTER SET gbk;
+ 修改数据库的字符集
+ ALTER DATABASE [db_name] CHARACTER SET UTF8;

+ 删除数据库
+ DROP DATABASE [IF EXISTS] db_name;


> 数据表操作

+ 打开数据库
+ use 数据库名
+ 显示当前打开的数据库
+ SELECT DATABASE() 
+ 创建数据表
+ CREATE TABLE [IF NOT EXISTS] table_name (column_name,data_type)

```
-> create table tb1(
-> username VARCHAR(20),
-> age TINYINT UNSIGNED,
-> salary FLOAT(8,2) UNSIGNED
-> );
```

+ 查看数据表列表
+ SHOW TABLES [FROM db_name]
+ 查看数据表结构
+ SHOW COLUMNS FROM tb1;

> 记录的插入

+ INSERT [INTO] tb_name [(col_name,...)] VALUES (val,...)
+ 如果省略tb_name 那么值要为全部字段
+ 加tb_name 可以为部分字段；

> 记录查找

+ SELECT EXPR,.....FORM tb_name;

> 空值与非空值

+ NULL ,字段可以为空
+ NOT NULL 字段禁止为空

> 自动编号

+ AUTO_INCREMENT
+ 默认情况下，起始值为1，每次增量为1；
+ 必须和主键一起使用；
+ 不需要插入值；

> 主键

+ 一张表只能存在一个主键
+ 主键保证记录的唯一性
+ 主键自动为 not null;
+ 主键不能插入相同的值；

> 初涉唯一约束

+ UNIQUE
+ 唯一约束
+ 唯一约束可以保障记录的唯一性
+ 唯一约束的字段可以为空值 null
+ 每张数据表可以存在多个唯一约束(可以存在多个设置唯一约束的字段，但是不能相同)

```
mysql> CREATE TABLE tb5(
    id SMALLINT UNSIGNED AUTO_INCREMENT PRIMARY KEY,
    username VARCHAR(20) NOT NULL UNIQUE KEY,
    age tinyint UNSIGNED
    );
```

执行两次
```
mysql> insert tb5 (username,age) values ('tom',22)
```

报错
```
ERROR 1062 (23000): Duplicate entry 'tom' for key 'username'
```

> 初涉默认约束

+ 默认值
+ 当插入记录时，如果没有明确为字典赋值，则自动赋予默认值；

```
mysql> CREATE TABLE tb6(
    id SMALLINT UNSIGNED AUTO_INCREMENT PRIMARY KEY,
    username VARCHAR(20) NOT NULL UNIQUE KEY,
    sex ENUM('1','2','3') DEFAULT '3'
    );
```


> 约束

1. 约束保证数据的完整性和一致性
2. 约束分为表级约束和列级约束
3. 约束类型包括
    + NOT NULL(非空约束)
    + PRIMARY KEY(主键约束)
    + UNIQUE KEY(唯一约束)
    + DEFAULT (默认约束)
    + FOREIGN KEY(外键约束)
        + 保持数据的一致性，完整性
        + 实现一对一或者一对多的关系

> 外键约束的要求

1. 父表和字表必须使用相同的存储引擎，而且禁止使用临时表
2. 数据表的存储引擎只能为innoDB；
3. 外键列和参照列必须具有相似的数据类型，其中数字的长度或是具有符号位必须相同；
   而字符的长度则可以不同。
4. 外键列和参照列必须创建索引，如果外键列不存在索引的话，mysql将自动创建索引；

> 编辑数据表的默认存储引擎

+ mysql配置文件
+ default-storage-engine = INNODB;



