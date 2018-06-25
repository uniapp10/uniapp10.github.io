---
title: App 开发者学习使用 MySQL
date: 2018-05-13 14:50:00
tags: MySQL
---

软件开发中除了前端页面的展示和后台服务的运行外，还有很重要的一部分就是数据存储。在数据存储方面，处于领头地位的两位是 Oracle 和 IBM。后者主要是针对银行、军队、政府或者大企业；后者除了提供大型服务器服务外，还有一些小型服务器，其中就包括 MySQL。MySQL 原来是 Sun 公司旗下的开源产品，后来 Sun 公司被 Oracle收购，MySQL 也成为了 Oracle 的一部分。MySQL 以其轻量级特点能够很方便地运行在个人 PC 上，因此是我们开发者学习数据库技术的首选产品。

数据库服务器中可以创建多个数据库，其中每一个数据库中包含多张表，每一张表中包含多条数据。可以将服务器看做自己的电脑，一个数据库看做一个 Excel 文件，而一条数据就存储在一个 Excel 文件中的一行里面。

#####1 安装
[MySQL 官网](https://downloads.mysql.com/archives/community/) 下载适合自己电脑的产品。我使用的是 Mac , 因此我下载如下安装包：
![MySQL](https://upload-images.jianshu.io/upload_images/1753235-78e412a984168a3f.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
Tips: 下载时需要个人注册 Oracle 的账号，按照要求注册留下信息即可，不要太抵触，毕竟免费使用了人家的产品，要求留下信息也不算过分。个人亲测还没有收到服务人员的推销。
######2 安装
Mac 安装很简单，双击 pkg 安装包后，按照引导即可。成功的标志是出现欲抬头顶球的小海豚：
![成功](https://upload-images.jianshu.io/upload_images/1753235-685ea6daf732a56c.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
默认安装的目录为：`usr/local/mysql`，如果想要在终端使用 mysql 命令，在 Mac 上需要设置如下环境变量：
1 在终端输入：`sudo vi ~/.bash_profile`
2 添加路径：
```
#mysql
 PATH="/usr/local/mysql安装路径/bin:${PATH}"
 export PATH
```
3 在终端输入命令: `mysql`， 成功后的提示：
`Access denied for user ...`
######3 使用 MySQL
常用的 MySQL 语句分为以下两大类:
1. DML (Data Definition Language) 数据库定义语言，创建、删除更新数据库/数据表等；
2. DQL (Data Query Language) 数据库查询语句，对数据库中的数据按条件查询结果；

Tips: mysql 语句不区分大小写

#####数据库语句
1.查询数据库 `show databases;`
```
+--------------------+
| Database           |
+--------------------+
| information_schema |
| mysql              |
| performance_schema |
| sys                |
```
mysql 系统创建了以上 4 个数据库，它们是 mysql 正常工作的基础配置，不要修改或者删除。

2.创建数据库 `create database 数据库名 character set 数据库字符类型 collate 数据库校验规则;`
使用命令`show character set;`能够查看 mysql 支持的字符类型：
```
+----------+---------------------------------+---------------------+--------+
| Charset  | Description                     | Default collation   | Maxlen |
+----------+---------------------------------+---------------------+--------+
| armscii8 | ARMSCII-8 Armenian              | armscii8_general_ci |      1 |
| ascii    | US ASCII                        | ascii_general_ci    |      1 |
| big5     | Big5 Traditional Chinese        | big5_chinese_ci     |      2 |
| binary   | Binary pseudo charset           | binary              |      1 |
| cp1250   | Windows Central European        | cp1250_general_ci   |      1 |
| cp1251   | Windows Cyrillic                | cp1251_general_ci   |      1 |
| cp1256   | Windows Arabic                  | cp1256_general_ci   |      1 |
| cp1257   | Windows Baltic                  | cp1257_general_ci   |      1 |
| cp850    | DOS West European               | cp850_general_ci    |      1 |
| cp852    | DOS Central European            | cp852_general_ci    |      1 |
| cp866    | DOS Russian                     | cp866_general_ci    |      1 |
| cp932    | SJIS for Windows Japanese       | cp932_japanese_ci   |      2 |
```
使用 `show collation like 'utf8%';` 能够看到utf8 字符类型的校验规则：
```
| utf8_estonian_ci           | utf8    | 198 |         | Yes      |       8 | PAD SPACE     |
| utf8_general_ci            | utf8    |  33 | Yes     | Yes      |       1 | PAD SPACE     |
| utf8_general_mysql500_ci   | utf8    | 223 |         | Yes      |       1 | PAD SPACE     |
| utf8_german2_ci            | utf8    | 212 |         | Yes      |       8 | PAD SPACE     |
| utf8_hungarian_ci          | utf8    | 210 |         | Yes      |       8 | PAD SPACE     |
| utf8_icelandic_ci          | utf8    | 193 |         | Yes      |       8 | PAD SPACE     |
| utf8_latvian_ci            | utf8    | 194 |         | Yes      |       8 | PAD SPACE     |
| utf8_lithuanian_ci         | utf8    | 204 |         | Yes      |       8 | PAD SPACE     |
| utf8_persian_ci            | utf8    | 208 |         | Yes      |       8 | PAD SPACE     |
```
默认的校验规则为：`utf8_general_ci`;
创建数据库可以使用以下 3 种语句：
```
create database mydb1;
create database mydb2 character set utf8;
create database mydb3 character set utf8 collate utf8_general_ci;
```
其中前两种是最后一种的简写形式，最后一种能够指定特定的字符类型和校验规则。
利用命令 `show create database mydb2;` 可以查看 mysql 系统内部创建数据库的语句。下面以 `mydb` 开头的均表示自定义数据库名；
```
+----------+----------------------------------------------------------------------------------------------+
| Database | Create Database                                                                              |
+----------+----------------------------------------------------------------------------------------------+
| mydb2    | CREATE DATABASE `mydb2` /*!40100 DEFAULT CHARACTER SET utf8mb4 COLLATE utf8mb4_0900_ai_ci */ |
+----------+----------------------------------------------------------------------------------------------+
1 row in set (0.00 sec)
```
3.删除数据库 `drop database mydb1;`
4.修改数据库 `alter database 数据库名称 更改信息；`
比如，将数据库字符类型改为 gbk 编码：
`alter database mysqlite2 character set gbk;`
5.切换数据库：`use 数据库名称；`
6.查看当前使用的数据库 `select database();`

#####数据表语句
1. 创建表
```
create table tabel_name
(
	fielld1 datatype,
	field2 datatype,
	field3 datatype
)character set 字符集 collate 校对规则；
```
其中：field 表示字段；datatype 表示字段类型，可以理解成 Excel 表中列的名称；
mysql 中字段的类型，可以类比 java 学习，二者的对应关系如下：
![类型对比1](https://upload-images.jianshu.io/upload_images/1753235-375f3088907a3ec4.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

![类型对比2](https://upload-images.jianshu.io/upload_images/1753235-6c84bd09aceac036.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
mysql 中也有存储大数据的类型：
BLOB(字节流)、TEXT(字符流) ;
日期时间类型有：DATE、 TIME、 DATETIME、 TIMESTAMP 四种。
其中 DATE 只表示日期；TIME 只表示时间；DATETIME 表示日期和时间；TIMESTAMP 表示时间戳，由 mysql 系统自动生成；

我们可以使用如下语句创建一张员工表：
```
create table employee
(
	id int,
	name varchar(20),
	gender varchar(10),
	birthday date,
	entry_date date,
	job varchar(100),
	salary float,
	resume varchar(255)
);
```
2. 查看表： `desc employee;`
3. 查看 mysql 创建表的语句：`show create table employee;`
4. 通过对表中字段定义约束，可以保证数据表的有效性和完整性。约束有以下 3 种类型：
  1 primary key：定义主键约束， 不允许为空，不允许重复；
  2 unique：唯一约束，不允许重复；
  3 not null：非空约束，不允许为空；

比如对 employee 表进行如下约束：
```
create table employee2
(
	id int primary key auto_increment,
	name varchar(20) not null,
	gender varchar(10) not null,
	birthday date,
	entry_date date,
	job varchar(100),
	salary float  not null,
	resume varchar(255)
);
```
将 id 字段作为主键，对 name/gender/resume 字段进行非空限定；

5.修改表
1. 增加列：
  alter table 表名 add 列字段 字段类型；
2. 修改列类型：
  alter table 表名 modify 列字段 字段类型；
3. 删除列：
  alter table 表名 drop 列字段；
4. 修改表名称：
  rename table 表名 to 新表名；
5. 修改列名称：
  alter table 表名 change [column] 旧列名 新列名 类型;
6. 修改表字符集：
  alter table 表名 character set utf8;

6.添加表数据
增加表数据有以下 3 种语句：
```
1 insert into users (id, username, birthday,entry_date,job,salary,resume,image) values(1,'juxin','1995-09-09','2016-01-01','ceo',15000,'good girl','not upload');
2 insert into users (id, username,entry_date,job,salary,resume,image) values(2,'xueyang','2016-01-01','ceo',15000,'good girl','not upload');
3 insert into users values(3,'yanhong','1995-09-09','2016-01-01','ceo',15000,'good girl','not upload');
```
其中 1、2 两种方法要求前后两个括号内的字段名和字段值一一对应；最后一种方法省略字段名，但是字段值需要和定义的表 employee 一一对应；
7.修改表数据
update 表名 set 列名=列值，列名=列值，列名=列值 where 从句；
比如修改 employ 表中 name 为 lisi 的 job 为 CEO，语句如下：
`update employ set name='CEO' where username='lisi';`
8.删除表数据 `delete from employ where name='CEO'; `
9.查询表数据
select [DISTINCT]  column1 expression, column2 expression… from 表名；
比如：
查看表 employ 中所有数据：`select * from employ;`
将表 employ 中所有数据 salary 增加 1000：
`select name, salary+1000 from employ;`
将表 employ 中所有 name 变为姓名:
`select name as 姓名 from employ;`
将表 employ 中所有 name 为 lisi 的数据选出:
`select * from employ where name='lisi';`
10.where 语句修饰符

| 比较运算符        | 含义          |
| ------------- |:-----|
|> < <= >= = <>      | 大于/小于/大于等于/小于等于/不等于
| between … and      | 某一区间（包括边界值）    
| in(100,200) | 是否是列表中值
| like  |  模糊查询
| is null   |   是否为空
| 逻辑运算符        |  and/or/not        |

比如，我们创建数据表 exams 记录考试成绩：
```
create table exams(
     id int,
     name varchar(30),
     chinese double,
     english double,
     math double
);

insert into exams values(1,'zhangsan',100,100,100);
insert into exams values(2,'lisi',100,100,99);
insert into exams values(3,'wang ',100,100,90);
insert into exams values(4,'wang ',80,80,60);
insert into exams values(4,'wang2 ',80,70,60);
```
查询英语成绩在 [80,100] 的同学：
`select * from exams where english between 80 and 100;`
也可以使用逻辑运算符实现：
`select * from exams  where english>=80 and english<=100;`
查询名字中包含`wang`的同学：
`select * from exams where name like '%wang%';` 
%：通配符; 
_:  一个字符；
查询名字中为`wang2`的同学可以使用：
`select * from exams where name like 'wang_';` 
11.查询结果修饰符
| 修饰符      | 含义                  |
| -------- | :------------------ |
| order by | 排序 （desc 降序/asc 升序） |
| count    | 行数求和                |
| sum      | 列求和                 |
| avg      | 列平均                 |
| max/min  | 列最值                 |
| group    | 列分组                 |
比如：
按照总分成绩升序排列：`select * from exams order by chinese+english+math asc;`
查找数学成绩大于100的同学总数：`select count(*) from exams where math>=100;`
计算各科总分：
`select sum(chinese),sum(english),sum(math) from exams;`
计算语文平均分：
`select avg(chinese) from exams;`
也可以使用：
`select sum(chinese)/count(*) from exams;`
查找语文最高分：
`select max(chinese) from exams;`
按照名字对同学进行分组：
`select name,sum(chinese+math) from exams group by name;`
group 后可以跟 having 关键字对分组进行再次筛选：
`select name,sum(chinese+math) from exams group by name having sum(chinese+math>100);`

#####总结
MySQL 是一款轻量级的数据库软件，使用它可以在在自己电脑搭建数据库，模拟数据库的创建、销毁，数据表的创建、销毁、修改，以及数据的增删改查。操作数据库需要特定的数据库语法，熟悉他们能够快速、高效地筛选出想要的结果。



