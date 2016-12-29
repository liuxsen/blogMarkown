---
title: MySQL学习思路（基础部分）
date: 2016-10-31 12:38:59
tags: mysql
---

# MySQL学习思路（基础部分）:
1. 了解什么是数据库，以及我们为什么需要数据库？
2. 了解MySQL的安装与配置。
3. 掌握在MySQL环境下如何创建、修改、删除数据库。
4. 掌握MySQL环境下的数据类型，主要包括字符、整型、浮点及日期，以及每种数据类型的存储特点。
5. 熟练掌握MySQL环境下数据表的创建、修改、删除操作。
6. 熟练掌握各种约束的使用，主要包含主键约束、唯一约束、外键约束、非空约束、默认约束。
7. 熟练掌握记录的增、删、改、查等操作，也就是常说的CURD操作，当然也包括多表关联的操作。
8. 掌握MySQL的运算符及内置函数的使用，主要包括字符函数库、数学函数库、日期时间函数库等。
希望对各位朋友有所帮助！

> [相关博客](http://blog.csdn.net/toto1297488504/article/category/1282728)

> [下载mysql](http://download.csdn.net/download/lxq_xsyu/6468461)

> 安装mysql出错

+ Mysql server instance安装中无响应问题的解决办法
1.设置文件夹选项，勾选显示隐藏文件
2.在C盘下找到ProgramData文件夹下的MySQL,直接删除
3.重新安装MySQL，问题即可解决

# mysql操作

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
+ 删除数据表
+ DROP TABLE table_name

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
3. 约束类型包括(按照功能划分)
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
3. 外键列和参照列必须具有相似的数据类型，其中数字的长度或是否具有符号位必须相同；
   而字符的长度则可以不同。
4. 外键列和参照列必须创建索引，如果外键列不存在索引的话，mysql将自动创建索引；

> 编辑数据表的默认存储引擎

+ mysql配置文件
+ default-storage-engine = INNODB;

> 外键约束案例

+ 长度（字符可以不同） ，符号位 要相同

> 父表

```
mysql> CREATE TABLE province(
        id SMALLINT UNSIGNED AUTO_INCREMENT PRIMARY KEY,
        pname VARCHAR(20) NOT NULL
    );
```

```
SHOW CREATE TABLE province;
```

> 子表

```
mysql> CREATE TABLE users(
        id SMALLINT UNSIGNED PRIMARY KEY AUTO_INCREMENT,
        username VARCHAR(10) NOT NULL,
        pid SMALLINT UNSIGNED ,
        FOREIGN KEY (pid) REFERENCES province (id)
    );
```

+ 显示索引

```
SHOW INDEXES FROM provinces;
```

```
SHOW INDEXES FROM provinces\G;
```

## 外键约束的参照操作

1. CASCADE: 从父表删除或更新且自动删除或更新子表中匹配的行
2. SET NULL: 从父表删除或更新行，并设置子表中的外键列为NULL、如果
    使用该选项，必须保证子表没有指定NULL;
3. RESTRICT: 拒绝对父表的删除或更新操作
4. NOT ACTION : 标准SQL的关键字，在mysql中与RESTICT 相同；

> 案例

```
mysql> CREATE TABLE users1(
    id SMALLINT UNSIGNED PRIMARY KEY AUTO_INCREMENT ,
    username VARCHAR(10) NOT NULL,
    pid SMALLINT UNSIGNED,
    FOREIGN KEY (pid) REFERENCES province (id) ON DELETE CASCADE
    );
```


+ 必须先在父表中插入记录

```
mysql> insert province (pname) values ('a');
```

```
mysql> insert users1 (username) values ('tom');
```

## 表级约束和列级约束

+ 对一个数据列建立的约束，成为列级约束
+ 对多个数据列建立的约束，成为表级约束
+ 列级约束既可以在列定义时声明，也可以在列定义后声明
+ 表级约束只能在列定义后声明

## 修改数据表

> 添加单列

```
ALTER TABLE tbl_name ADD [COLUMN] col_name column_definition [FIRST | AFTER col_name]
```

> 添加多列

```
mysql> ALTER TABLE tbl_name ADD [COLUMN] (col_name column_definition,...)
```

+ 位于所有列的前面

```
mysql> ALTER TABLE users1 ADD password VARCHAR(20) FIRST username;
```

+ 位于指定列的后面

```
mysql> ALTER TABLE users1 ADD password VARCHAR(20) AFTER username;
```

+ 查看表的结构

```
mysql> SHOW COLUMNS FROM users1;
```

## 删除列

> 删除单列

```
ALTER TABLE tbl_name DROP [COLUMN] col_name;
```

> 删除多列

```
ALTER TABLE tbl_name DROP [COLUMN] col_name,DROP [COLUMN] col_name,;
```

> 删除列同时新增列

```
ALTER TABLE tbl_name DROP col_name,ADD col_name col_definition
```

## 约束


```
mysql> CREATE TABLE users2(
        username VARCHAR(10) NOT NULL,
        pid SMALLINT UNSIGNED
    );
```

> 增加主键

```
ALTER TABLE users2 ADD ID SMALLINT UNSIGNED;
```

> 添加主键约束

```
ALTER TABLE tbl_name ADD [CONSTRAINT[symbol]] PRIMARY KEY [index_type] (index_col_name,...)
```

> 添加唯一约束

```
ALTER TABLE tbl_name ADD [CONSTRAINT [symbol]] UNIQUE [INDEX|KEY] [index_name] [index_type] (index_col_name,...)
```

+ 使id为主键

```
ALTER TABLE users2 ADD CONSTRAINT PK_users2_id PRIMARY KEY (id);
```

+ 为username添加唯一约束

```
mysql> ALTER TABLE users2 ADD UNIQUE (username);
```

+ 添加外键约束

```
ALTER TABLE tbl_name ADD [CONSTRAINT[symbol]] FOREIGN KEY [index_name] (index_col_name,...) references tbl_name (index_col_name,...);
```

```
ALTER TABLE users2 ADD FOREIGN KEY [pid] references province(id)
```

+ 添加或者删除默认约束

```
ALTER TABLE tbl_name ALTER [COLUMN] col_name {SET DEFAULT literal | DROP DEFAULT}
```

```
ALTER TABLE users2 ADD age tinyint unsigned not null;
```

```
ALTER TABLE users2 ALTER age SET DEFAULT 15;
```

```
ALTER TABLE users2 ALTER age DROP DEFAULT;
```

## 删除约束

+ 删除主键约束

```
ALTER TABLE tbl_name DROP PRIMARY KEY;
```

+ 删除唯一约束

```
ALTER TABLE tbl_name DROP {INDEX|KEY} index_name;
```

+ 删除外键约束

```
ALTER TABLE tbl_name DROP FOREIGN KEY fk_symbol;
```

## 修改数据表

> 修改列定义

```
ALTER TABLE tbl_name MODIFY [COLUMN] col_name column_definition [FIRST|AFTER COL_NAME]
```

> 修改列名称

```
ALTER TABLE tb_name CHANGE [COLUMN] old_col_name new_col_name column_definition [FIRST|AFTER col_name]
```

> 数据表更名

1. 方法1

```
ALTER TABLE tbl_name RENAME [TO|AS] new_tbl_name
```

2. 方法2

```
RENAME TABLE tbl_name TO new_tbl_name [,tbl_name2 ]
```


## 总结

+ 约束
    + 功能
        + NOT NULL(非空约束)
        + PRIMARY KEY (主键约束)
        + UNIQUE KEY (唯一约束)
        + DEFAULT (默认约束)
        + FOREIGN KEY (外键约束)
    + 数据列的数目
        + 标记约束
        + 列级约束
+ 修改数据表
    + 针对字段的操作 ： 添加/删除/字段、修改列定义，修改列名称等
    + 针对约束的操作 ： 添加/删除各种约束
    + 针对数据表的操作： 数据表更名操作 （两种方式）；

# 记录的CURD

> 插入记录

```
INSERT [INTO] tbl_name [(col_name,...)] {values|value} ({expr | DEFAULT},...),(),...
```

```
INSERT [INTO] tbl_name SET col_name={expr|DEFAULT},...
```

+ 说明： 与第一种的方式的区别在于，此方法可以使用子查询（SUBQUERY）

```
INSERT [INTO] tbl_name [(col_name,...)] SELECT ...
```

+ 说明：此方法可以将查询结果插入到制定数据表

+ 如果想要为id 自增的值赋值（默认值），可以赋值 null 或者 default；
+ 赋值也可以用比表达式

> 单表更新记录UPDATE

```
更新记录（单表更新）
UPDATE [LOW_PRIORITY] [IGNORE] table_name SET col_name1={expr1|default} [,col_name2={expr2|DEFAULT}] ... [WHERE where_condition]
```

```
update users set age = age+5;
```

```
update users set age = age-id, sex = 0;
```

```
update users set age = age+10 where id % 2 = 0;
```

> 删除记录（单表删除）

```
DELETE FROM tbl_name [WHERE where_confition]
```

> 查询表达式解析

+ 查询记录

```
SELECT select_expr [,select_expr ...]
[
    FROM tabel_references 
    [WHERE where_condition]
    [GROUP BY {col_name | position} [ASC | DESC],...]
    [HAVING where_condition]
    [ORDER BY {col_name | expr | position } [ASC | DESC ],...]
    [LIMIT {[offset,] row_count | row_count OFFSET offset}]
]
```

> select_expr 查询表达式

+ 每一个表达式表示想要的一列，必须至少一个。
+ 多个列之间以英文逗号分隔。
+ 星号（*）表示所有列，tbl_name.\* 可以表示命名表的所有列。
+ 查询表达式可以使用 [AS] alias_name 为其赋予别名
+ 别名可以用于 GROUP BY , ORDER BY 或 HAVING 子句；

```
select id as usersid ,username as uname from users;
```

> where 条件表达式

1. 对记录进行过滤，如果没有指定where子句，则显示所有记录，在where表达式中，可以使用mysql支持的表达式或者运算符；

> group by 查询结果分组

1. ASC 升序
2. desc 降序

```
[GROUP BY {col_name| position} [ASC | DESC],...]
```

```
select age group by age;
```

> HAVING

+ 分组条件(只对某一部分进行分组)
+ [HAVING where_condition]

```
select age username from users group by age having age>12;
```


> order by 对查询结果进行排序

+  对查询结果进行排序
+ [order by {col_name} [asc | desc]]

> limit 

+ 限制查询数量

```
[LIMIT {offset,}row_count | row_count OFFSET offset]
```

```
select * from users limit 2;
```

```
select * from users order by id desc limit 0,2;
```

+ 将查询的数据插入表

```
insert test select username from users where age > 12;
```

## 子查询 连接

> 数据准备

+ goods_cate 商品分类
+ brand_name 商品品牌
+ good_price 商品价格
+ is_show  商品是否上架，在销售
+ is_saleOff 是否销售完了，

```
create table tdb_goods(
        goods_id smallint unsigned primary key auto_increment,
        goods_name varchar(150) not null,
        goods_cate varchar(40) not null,
        brand_name varchar(40) not null,
        good_price decimal(15,3) unsigned not null,
        is_show tinyint(1) not null default 1,
        is_saleOff tinyint(1) not null default 0
    );
```

```
set names gbk;
```


```
insert tdb_goods (goods_name,goods_cate,brand_name,good_price,is_show,is_saleOff) values
('西红柿','蔬菜','红富士',2.5,1,0),
('森马t恤','t恤','森马',233,1,0),
('金钥匙','金属','美国金属',100,1,0),
('zuk','手机','联想',1500,1,0),
('iphone6','手机','红富士',6000,1,0),
('thinkpad','笔记本','联想',4000,1,0),
('框狄','水杯','富士',50,1,0),
('tplink','路由器','tplink',100,1,0)
;
```