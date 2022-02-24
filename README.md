# Java Web 基础



+ 什么是 Web：全球广域网，也称万维网 (www)，能通过浏览器访问的==网站==
+ JavaWeb：是用 Java 技术来解决相关 Web 互联网领域的技术栈



1. 网页：展现数据
2. 数据库：存储和管理数据
3. Java Web程序：逻辑处理







## 1. 数据库

<img src="Java Web 基础.assets/image-20220220234408236.png" alt="image-20220220234408236" style="zoom: 67%;" /> 

数据库 (Data Base)：

+ 存储数据的仓库，数据是有组织的进行存储



数据库管理系统 (Data Base Management System)：

+ 管理数据库的大型软件



SQL (Structured Query Language)：

+ 结构化查询语言
+ 操作关系型数据库的编程语言
+ 定义操作所有关系型数据库的统一标准





<font size="5rem">**常见的关系型数据库管理系统**</font>

<img src="Java Web 基础.assets/image-20220220234637712.png" alt="image-20220220234637712" style="zoom:67%;" /> 

+ Oracle：收费的大型数据库，Oracle公司的产品
+ MySQL：开源免费的中小型数据库，后来Sun公司收购了MySQL，而Sun公司又被Oracle收购
+ SQL Sever： Microsoft公司收费的中型的数据库。`C#、.net`等语言常使用
+ PostgreSQL：开源免费中小型的数据库
+ DB2：IBM 公司的大型收费数据库产品
+ SQLite：嵌入式的微型数据库，如作为Android的内置数据库
+ MariaDB：开源免费中小型的数据库







### 1.1 MySQL 安装与使用

[MySQL 安装教程](https://www.runoob.com/mysql/mysql-install.html)

<iframe src="//player.bilibili.com/player.html?aid=379163696&bvid=BV1Qf4y1T7Hx&cid=440652475&page=3" scrolling="no" border="0" frameborder="no" framespacing="0" allowfullscreen="true" height="650px"> </iframe>









### 1.2 MySQL 数据模型



关系型数据库

+ 关系型数据库是建立在关系模型基础上的数据库，关系型数据库是由多张能互相连接的 ==二维表== 组成的数据库



优点：

1. 都是使用表结构，格式一致易于维护
2. 使用通用的 SQL 语言操作，使用方便，可哦用于复杂查询
3. 数据存储在磁盘中，安全

<img src="Java Web 基础.assets/image-20220221001612679.png" alt="image-20220221001612679" style="zoom:67%;" /> 









### 1.3 SQL



+ 结构化查询语言，一门操作关系型数据库的编程语言
+ 定义操作所有关系型数据库的统一标准
+ 对于同一个需求，每一种数据库操作的方式可能会存在一些不一样的地方，我们称为 "方言"





#### 1.3.1 SQL 通用语法

1. SQL 语句可以当行或多行书写，以分号结尾
2. MySQL 数据库的 SQL 语句不区分大小写，关键字建议使用大写
3. 注释
   + 单行注释：==—— 注释内容== 或 ==# 注释内容（MySQL 特有）==
   + 多行注释：==/* 注释 */==







#### 1.3.2 SQL 分类

+ DDL（Data Denfinition Language）数据定义语言，用来定义数据库对象：数据库，表，列等
+ DML（Data Manipulation Language）数据操作语言，用来对数据库中表的数据进行增删改
+ DQL（Data Query Language）数据查询语言，用来查询数据库中表的（记录）数据
+ DCL（Data Control Language）数据控制语言，用来定义数据库的访问权限和安全级别，及创建用户

<img src="Java Web 基础.assets/image-20220221003100835.png" alt="image-20220221003100835" style="zoom: 67%;" /> 

+ DDL：操作数据库，表等
+ DML：对表中的数据进行增删改
+ DQL：对表中的数据进行查询
+ DCL：对数据库进行权限控制





#### 1.3.3 DDL 操作数据库

<font size="5rem">1. 查询语句</font>

~~~mysql
show databases;
~~~

示例：

~~~mysql
mysql> show databases;
+--------------------+
| Database           |
+--------------------+
| information_schema | --> 记录mysql库和表，存储的数据是特殊的表->视图（逻辑表）并不存在物理文件
| mysql              | --> 存储mysql的核心信息，如权限、安全等
| performance_schema | --> 存储mysql的性能信息
| sys                | --> 系统相关的信息
+--------------------+
4 rows in set (0.01 sec)
~~~

***



<font size="5rem">2. 创建语句</font>

~~~mysql
create databases 数据库名;
~~~

示例：

~~~mysql
mysql> create database db1;
Query OK, 1 row affected (0.04 sec)

mysql> show databases;
+--------------------+
| Database           |
+--------------------+
| db1                |
| information_schema |
| mysql              |
| performance_schema |
| sys                |
+--------------------+
5 rows in set (0.00 sec)
~~~

> 同时db1文件夹被创建

<img src="Java Web 基础.assets/image-20220221004237824.png" alt="image-20220221004237824" style="zoom: 67%;" /> 



注意：

+ 当我想要创建同名数据库时，会报错
+ 避免方法，先判断是否存在此数据库，存在则不执行语句，不存在则执行语句

~~~mysql
mysql> create database db1;
ERROR 1007 (HY000): Can't create database 'db1'; database exists

mysql> create database if not exists db1;
Query OK, 1 row affected, 1 warning (0.01 sec)

mysql> create database if not exists db2;
Query OK, 1 row affected (0.04 sec)

mysql> show databases;
+--------------------+
| Database           |
+--------------------+
| db1                |
| db2                |
| information_schema |
| mysql              |
| performance_schema |
| sys                |
+--------------------+
6 rows in set (0.00 sec)
~~~

***



<font size="5rem">3. 删除</font>

~~~mysql
drop database 数据库名;
~~~

示例：

~~~mysql
mysql> drop database db2;
Query OK, 0 rows affected (0.02 sec)

mysql> show databases;
+--------------------+
| Database           |
+--------------------+
| db1                |
| information_schema |
| mysql              |
| performance_schema |
| sys                |
+--------------------+
5 rows in set (0.00 sec)
~~~



注意：

+ 在删除数据库之前，需要先判断数据库是否存在，否则会报错

~~~mysql
mysql> drop database db2;
ERROR 1008 (HY000): Can't drop database 'db2'; database doesn't exist

mysql> drop database if exists db2;
Query OK, 0 rows affected, 1 warning (0.03 sec)
~~~

***





<font size="5rem">4. 使用数据库</font>

~~~mysql
use 数据库名;
~~~

示例：

~~~mysql
mysql> use db1;
Database changed

mysql> select database();  # 查看当前使用的数据库
+------------+
| database() |
+------------+
| db1        |
+------------+
1 row in set (0.00 sec)
~~~

***



<font size="5rem">总结：</font>

![image-20220221005622054](Java Web 基础.assets/image-20220221005622054.png)









#### 1.3.4 DDL 操作表

+ 创建（Create）
+ 查询（Retrieve）
+ 修改（Update）
+ 删除（Delete）





<font size="5rem">1. 查询表</font>

+ 查询当前数据库下所有表的名称

~~~mysql
SHOW TABLES;

mysql> show tables;
Empty set (0.02 sec)

mysql> use mysql;
Database changed
mysql> show tables;
+------------------------------------------------------+
| Tables_in_mysql                                      |
+------------------------------------------------------+
| columns_priv                                         |
| component                                            |
| db                                                   |
| default_roles                                        |
| engine_cost                                          |
| func                                                 |
| general_log                                          |
| global_grants                                        |
| gtid_executed                                        |
| help_category                                        |
| help_keyword                                         |
| help_relation                                        |
| help_topic                                           |
| innodb_index_stats                                   |
| innodb_table_stats                                   |
| password_history                                     |
| plugin                                               |
| procs_priv                                           |
| proxies_priv                                         |
| replication_asynchronous_connection_failover         |
| replication_asynchronous_connection_failover_managed |
| replication_group_configuration_version              |
| replication_group_member_actions                     |
| role_edges                                           |
| server_cost                                          |
| servers                                              |
| slave_master_info                                    |
| slave_relay_log_info                                 |
| slave_worker_info                                    |
| slow_log                                             |
| tables_priv                                          |
| time_zone                                            |
| time_zone_leap_second                                |
| time_zone_name                                       |
| time_zone_transition                                 |
| time_zone_transition_type                            |
| user                                                 |
+------------------------------------------------------+
37 rows in set (0.01 sec)
~~~

+ 查询表结构

~~~mysql
DESC 表名称;

mysql> desc func;
+-------+------------------------------+------+-----+---------+-------+
| Field | Type                         | Null | Key | Default | Extra |
+-------+------------------------------+------+-----+---------+-------+
| name  | char(64)                     | NO   | PRI |         |       |
| ret   | tinyint                      | NO   |     | 0       |       |
| dl    | char(128)                    | NO   |     |         |       |
| type  | enum('function','aggregate') | NO   |     | NULL    |       |
+-------+------------------------------+------+-----+---------+-------+
4 rows in set (0.01 sec)
~~~

***



<font size="5rem">2. 创建表</font>

~~~mysql
create table 表名 (
    字段名1 数据类型1,
    字段名2 数据类型2,
    ...
    字段名n 数据类型n
);
~~~

注意：最后一行末尾，==不能加逗号==

<img src="Java Web 基础.assets/image-20220221011108063.png" alt="image-20220221011108063" style="zoom:67%;" /> 



示例：

~~~mysql
mysql> use db1;
Database changed

mysql> create table tb_user(
    -> id int,
    -> username varchar(20),
    -> password varchar(32)
    -> );
Query OK, 0 rows affected (0.04 sec)

mysql> show tables;
+---------------+
| Tables_in_db1 |
+---------------+
| tb_user       |
+---------------+
1 row in set (0.00 sec)

mysql> desc tb_user;
+----------+-------------+------+-----+---------+-------+
| Field    | Type        | Null | Key | Default | Extra |
+----------+-------------+------+-----+---------+-------+
| id       | int         | YES  |     | NULL    |       |
| username | varchar(20) | YES  |     | NULL    |       |
| password | varchar(32) | YES  |     | NULL    |       |
+----------+-------------+------+-----+---------+-------+
3 rows in set (0.00 sec)
~~~

***



<font size="5rem">3. 删除表</font>

~~~mysql
drop table 表名;
~~~

+ 删除表时判断表是否存在

~~~mysql
drop table if exists 表名;
~~~

示例：

~~~mysql
mysql> show tables;
+---------------+
| Tables_in_db1 |
+---------------+
| student       |
| tb_user       |
+---------------+
2 rows in set (0.01 sec)

mysql> drop table tb_user;
Query OK, 0 rows affected (0.04 sec)

mysql> show tables;
+---------------+
| Tables_in_db1 |
+---------------+
| student       |
+---------------+
1 row in set (0.00 sec)

mysql> drop table tb_user;
ERROR 1051 (42S02): Unknown table 'db1.tb_user'
mysql> drop table if exists tb_user;
Query OK, 0 rows affected, 1 warning (0.01 sec)
~~~

***



<font size="5rem">4. 修改表</font>

1. 修改表名

~~~mysql
alter table 表名 rename to 新的表名;

mysql> show tables;
+---------------+
| Tables_in_db1 |
+---------------+
| student       |
+---------------+
1 row in set (0.01 sec)

mysql> alter table student rename to stu;
Query OK, 0 rows affected (0.06 sec)

mysql> show tables;
+---------------+
| Tables_in_db1 |
+---------------+
| stu           |
+---------------+
1 row in set (0.01 sec)
~~~

2. 添加一列

~~~mysql
alter table 表名 add 列名 数据类型;

mysql> desc stu;
+----------+-------------+------+-----+---------+-------+
| Field    | Type        | Null | Key | Default | Extra |
+----------+-------------+------+-----+---------+-------+
| id       | int         | YES  |     | NULL    |       |
| name     | varchar(10) | YES  |     | NULL    |       |
| gender   | char(1)     | YES  |     | NULL    |       |
| birthday | date        | YES  |     | NULL    |       |
| score    | double(5,2) | YES  |     | NULL    |       |
| email    | varchar(64) | YES  |     | NULL    |       |
| tel      | varchar(15) | YES  |     | NULL    |       |
| status   | tinyint     | YES  |     | NULL    |       |
+----------+-------------+------+-----+---------+-------+
8 rows in set (0.01 sec)

mysql> # 添加一个地址列
mysql> alter table stu add address varchar(50);
Query OK, 0 rows affected (0.06 sec)
Records: 0  Duplicates: 0  Warnings: 0

mysql> desc stu;
+----------+-------------+------+-----+---------+-------+
| Field    | Type        | Null | Key | Default | Extra |
+----------+-------------+------+-----+---------+-------+
| id       | int         | YES  |     | NULL    |       |
| name     | varchar(10) | YES  |     | NULL    |       |
| gender   | char(1)     | YES  |     | NULL    |       |
| birthday | date        | YES  |     | NULL    |       |
| score    | double(5,2) | YES  |     | NULL    |       |
| email    | varchar(64) | YES  |     | NULL    |       |
| tel      | varchar(15) | YES  |     | NULL    |       |
| status   | tinyint     | YES  |     | NULL    |       |
| address  | varchar(50) | YES  |     | NULL    |       |
+----------+-------------+------+-----+---------+-------+
9 rows in set (0.01 sec)
~~~

3. 修改数据类型

~~~mysql
alter table 表名 modify 列名 新数据类型;

mysql> desc stu;
+----------+-------------+------+-----+---------+-------+
| Field    | Type        | Null | Key | Default | Extra |
+----------+-------------+------+-----+---------+-------+
| id       | int         | YES  |     | NULL    |       |
| name     | varchar(10) | YES  |     | NULL    |       |
| gender   | char(1)     | YES  |     | NULL    |       |
| birthday | date        | YES  |     | NULL    |       |
| score    | double(5,2) | YES  |     | NULL    |       |
| email    | varchar(64) | YES  |     | NULL    |       |
| tel      | varchar(15) | YES  |     | NULL    |       |
| status   | tinyint     | YES  |     | NULL    |       |
| address  | varchar(50) | YES  |     | NULL    |       |
+----------+-------------+------+-----+---------+-------+
9 rows in set (0.01 sec)

mysql> # 把列名改成char(50)
mysql> alter table stu modify address char(50);
Query OK, 0 rows affected (0.09 sec)
Records: 0  Duplicates: 0  Warnings: 0

mysql> desc stu;
+----------+-------------+------+-----+---------+-------+
| Field    | Type        | Null | Key | Default | Extra |
+----------+-------------+------+-----+---------+-------+
| id       | int         | YES  |     | NULL    |       |
| name     | varchar(10) | YES  |     | NULL    |       |
| gender   | char(1)     | YES  |     | NULL    |       |
| birthday | date        | YES  |     | NULL    |       |
| score    | double(5,2) | YES  |     | NULL    |       |
| email    | varchar(64) | YES  |     | NULL    |       |
| tel      | varchar(15) | YES  |     | NULL    |       |
| status   | tinyint     | YES  |     | NULL    |       |
| address  | char(50)    | YES  |     | NULL    |       |
+----------+-------------+------+-----+---------+-------+
9 rows in set (0.00 sec)
~~~

4. 修改列名和数据类型

~~~mysql
alter table 表名 change 列名 新列名 新的数据类型;

mysql> desc stu;
+----------+-------------+------+-----+---------+-------+
| Field    | Type        | Null | Key | Default | Extra |
+----------+-------------+------+-----+---------+-------+
| id       | int         | YES  |     | NULL    |       |
| name     | varchar(10) | YES  |     | NULL    |       |
| gender   | char(1)     | YES  |     | NULL    |       |
| birthday | date        | YES  |     | NULL    |       |
| score    | double(5,2) | YES  |     | NULL    |       |
| email    | varchar(64) | YES  |     | NULL    |       |
| tel      | varchar(15) | YES  |     | NULL    |       |
| status   | tinyint     | YES  |     | NULL    |       |
| address  | char(50)    | YES  |     | NULL    |       |
+----------+-------------+------+-----+---------+-------+
9 rows in set (0.00 sec)

mysql> alter table stu change address addr varchar(30);
Query OK, 0 rows affected (0.08 sec)
Records: 0  Duplicates: 0  Warnings: 0

mysql> desc stu;
+----------+-------------+------+-----+---------+-------+
| Field    | Type        | Null | Key | Default | Extra |
+----------+-------------+------+-----+---------+-------+
| id       | int         | YES  |     | NULL    |       |
| name     | varchar(10) | YES  |     | NULL    |       |
| gender   | char(1)     | YES  |     | NULL    |       |
| birthday | date        | YES  |     | NULL    |       |
| score    | double(5,2) | YES  |     | NULL    |       |
| email    | varchar(64) | YES  |     | NULL    |       |
| tel      | varchar(15) | YES  |     | NULL    |       |
| status   | tinyint     | YES  |     | NULL    |       |
| addr     | varchar(30) | YES  |     | NULL    |       |
+----------+-------------+------+-----+---------+-------+
9 rows in set (0.00 sec)
~~~

5. 删除列

~~~mysql
alter table 表名 drop 列名;

mysql> desc stu;
+----------+-------------+------+-----+---------+-------+
| Field    | Type        | Null | Key | Default | Extra |
+----------+-------------+------+-----+---------+-------+
| id       | int         | YES  |     | NULL    |       |
| name     | varchar(10) | YES  |     | NULL    |       |
| gender   | char(1)     | YES  |     | NULL    |       |
| birthday | date        | YES  |     | NULL    |       |
| score    | double(5,2) | YES  |     | NULL    |       |
| email    | varchar(64) | YES  |     | NULL    |       |
| tel      | varchar(15) | YES  |     | NULL    |       |
| status   | tinyint     | YES  |     | NULL    |       |
| addr     | varchar(30) | YES  |     | NULL    |       |
+----------+-------------+------+-----+---------+-------+
9 rows in set (0.00 sec)

mysql> alter table stu drop addr;
Query OK, 0 rows affected (0.06 sec)
Records: 0  Duplicates: 0  Warnings: 0

mysql> desc stu;
+----------+-------------+------+-----+---------+-------+
| Field    | Type        | Null | Key | Default | Extra |
+----------+-------------+------+-----+---------+-------+
| id       | int         | YES  |     | NULL    |       |
| name     | varchar(10) | YES  |     | NULL    |       |
| gender   | char(1)     | YES  |     | NULL    |       |
| birthday | date        | YES  |     | NULL    |       |
| score    | double(5,2) | YES  |     | NULL    |       |
| email    | varchar(64) | YES  |     | NULL    |       |
| tel      | varchar(15) | YES  |     | NULL    |       |
| status   | tinyint     | YES  |     | NULL    |       |
+----------+-------------+------+-----+---------+-------+
8 rows in set (0.00 sec)
~~~

<img src="Java Web 基础.assets/image-20220221230639511.png" alt="image-20220221230639511" style="zoom:80%;" /> 











##### 1. 数据类型

+ MySQL 支持多种类型，可以分为三类：
  + 数值
  + 日期
  + 字符串

<img src="Java Web 基础.assets/824420-20151225015719437-1262934313.png" alt="img" style="zoom: 80%;" /> 



特殊的：

double在设置字段的数值类型时：

~~~mysql
score double(总长度, 小数点后保留的位数)
例如：
score double(5, 2) 假设分数的范围是0~100
100.00，这里的总长度就是5，小数点前+小数点后
~~~

***

字符串类型设置时：

~~~mysql
char(20)
varchar(20)
....(XX)

括号里的数字就是限制字段的长度

注意 char和varchar 的区别
1. char存储性能高，varchar存储性能低
2. char是定长字符串，不够用的地方用空格补齐
3. varchar是变长字符串，会计算当前字符长度来分配空间
~~~









##### 案例练习：

![image-20220221225622980](Java Web 基础.assets/image-20220221225622980.png) 

示例：

~~~mysql
mysql> show databases;
+--------------------+
| Database           |
+--------------------+
| db1                |
| information_schema |
| mysql              |
| performance_schema |
| sys                |
+--------------------+
5 rows in set (0.01 sec)

mysql> use db1;
Database changed
mysql> desc tb_user;
+----------+-------------+------+-----+---------+-------+
| Field    | Type        | Null | Key | Default | Extra |
+----------+-------------+------+-----+---------+-------+
| id       | int         | YES  |     | NULL    |       |
| username | varchar(20) | YES  |     | NULL    |       |
| password | varchar(32) | YES  |     | NULL    |       |
+----------+-------------+------+-----+---------+-------+

mysql> create table student(
    ->
    ->     id int,
    ->     name varchar(10),
    ->     gender char(1),
    ->     birthday date,
    ->     score double(5,2),
    ->     email varchar(64),
    ->     tel varchar(15),
    ->     status tinyint
    -> );
Query OK, 0 rows affected, 1 warning (0.06 sec)

mysql> desc student;
+----------+-------------+------+-----+---------+-------+
| Field    | Type        | Null | Key | Default | Extra |
+----------+-------------+------+-----+---------+-------+
| id       | int         | YES  |     | NULL    |       |
| name     | varchar(10) | YES  |     | NULL    |       |
| gender   | char(1)     | YES  |     | NULL    |       |
| birthday | date        | YES  |     | NULL    |       |
| score    | double(5,2) | YES  |     | NULL    |       |
| email    | varchar(64) | YES  |     | NULL    |       |
| tel      | varchar(15) | YES  |     | NULL    |       |
| status   | tinyint     | YES  |     | NULL    |       |
+----------+-------------+------+-----+---------+-------+
8 rows in set (0.01 sec)
~~~







#### 1.3.5 DML 操作表中数据



<font size="5rem">1. 添加数据</font>

+ 给指定列添加数据

~~~mysql
insert into 表名(列名1, 列名2, ...) values(值1, 值2);

insert into stu(id, name) values (1, 'pine');
~~~

<img src="Java Web 基础.assets/image-20220222020322579.png" alt="image-20220222020322579" style="zoom:80%;" /> 



+ 给全部列添加数据

~~~mysql
insert into 表名 values(值1, 值2);

-- 给所有列添加数据，不建议省略列名
INSERT INTO stu ( id, NAME, gender, birthday, score, email, tel, `status` )
VALUES
	( 2, 'Mikey', '男', '1999-11-11', 88.88, '123@gmail.com', '1234567890', '1' );
~~~

+ 批量添加数据

~~~mysql
insert into 表名(列名1, 列名2, ...) values(值1, 值2, ...),(值1, 值2, ...)...;
insert into 表名 values(值1, 值2, ...),(值1, 值2, ...),(值1, 值2, ...)...;

-- 批量添加数据
INSERT INTO stu
VALUES
	( 2, 'Mikey', '男', '1999-11-11', 88.88, '123@gmail.com', '1234567890', '1' )(
		2,
		'Mikey',
		'男',
		'1999-11-11',
		88.88,
		'123@gmail.com',
		'1234567890',
		'1' 
		)(
		2,
		'Mikey',
		'男',
		'1999-11-11',
		88.88,
		'123@gmail.com',
		'1234567890',
	'1' 
	);
~~~

<img src="Java Web 基础.assets/image-20220222021712442.png" alt="image-20220222021712442" style="zoom:80%;" /> 

***



<font size="5rem">2. 修改数据</font>

1. 修改表数据

~~~mysql
update 表名 set 列名=值1,列名2=值2,.....[where 条件];

	-- 修改数据 update 表名 set 列名1=值1,列名2=值2... [where 条件];
	-- 将Mikey的性别改为女
	update stu set gender='女' where name='Mikey';
~~~

<img src="Java Web 基础.assets/image-20220222022558456.png" alt="image-20220222022558456" style="zoom:80%;" /> 

~~~mysql
	-- 将pine的生日改为1999-12-12 分数改为99.99
	update stu set birthday='1999-12-12',score=99.99 where name='pine';
~~~

<img src="Java Web 基础.assets/image-20220222022847836.png" alt="image-20220222022847836" style="zoom:80%;" /> 

***

<img src="Java Web 基础.assets/image-20220222023202181.png" alt="image-20220222023202181" style="zoom:80%;" /> 

> 注意：修改语句中如果不加条件，则==将所有数据都修改==

***



<font size="5rem">3. 删除数据</font>

+ 删除数据

~~~mysql
delete from 表名 [where 条件];

	-- 删除pine
	delete from stu where name='pine';
~~~

<img src="Java Web 基础.assets/image-20220222023742095.png" alt="image-20220222023742095" style="zoom:80%;" /> 

***

<img src="Java Web 基础.assets/image-20220222023859912.png" alt="image-20220222023859912" style="zoom:80%;" /> 

> 注意：修改语句中如果不加条件，则==将所有数据都修改==









#### 1.3.6 DQL 查询表中数据



查询语法：

~~~mysql
select
    字段列表
from
    表名列表
where
    条件列表
group by
    分组字段
having
    分组后条件
order by
    排序字段
limit
    分页限定
~~~



##### <font size="5rem">1. 基础查询-SELECT</font>

+ 查询多个字段

~~~mysql
select 字段列表 from 表名;
select * from 表名; -- 查询所有数据

-- 基础查询 ===========
-- 查询 name age 这两列
select name,age from stu;

-- 查询所有列的数据，列名的列表可以使用*代替，但是不建议使用
select * from stu;

-- 查询地址信息，看同学都来自哪一个城市
select address from stu;

-- 查询姓名，数学和英语成绩
select name,math,english from stu;
select name,math as 数学成绩,english as 英语成绩 from stu;
~~~

<img src="Java Web 基础.assets/image-20220222110930280.png" alt="image-20220222110930280" style="zoom:80%;" /> 

<img src="Java Web 基础.assets/image-20220222112014214.png" alt="image-20220222112014214" style="zoom:80%;" /> 



+ 去除重复记录

~~~mysql
select distinct 字段列表 from 表名;

select distinct address from stu;  --去重
~~~

<img src="Java Web 基础.assets/image-20220222112548533.png" alt="image-20220222112548533" style="zoom:80%;" /> <img src="Java Web 基础.assets/image-20220222112622865.png" alt="image-20220222112622865" style="zoom:80%;" /> 



+ 起别名

~~~mysql
as: -- as也可以省略

select name,math,english from stu;
select name,math as 数学成绩,english as 英语成绩 from stu;
~~~

<img src="Java Web 基础.assets/image-20220222112121460.png" alt="image-20220222112121460" style="zoom:80%;" /> <img src="Java Web 基础.assets/image-20220222112719395.png" alt="image-20220222112719395" style="zoom:80%;" />











##### <font size="5rem">2. 条件查询-WHERE</font>

+ 条件查询语法

~~~mysql
select 字段列表 from 表名 where 条件列表
~~~

条件：

| 操作符           | 描述                                                         |
| ---------------- | ------------------------------------------------------------ |
| =                | 等于                                                         |
| <> 或 !=         | 不等于                                                       |
| >                | 大于                                                         |
| <                | 小于                                                         |
| >=               | 大于等于                                                     |
| <=               | 小于等于                                                     |
| BETWEEN...AND... | 在某个范围内（都包含）                                       |
| LIKE 占位符      | 搜索某种模式，模糊查询 ==“_单个任意字符”==  ==“%多个任意字符”== |
| IN(...)          | 多选一                                                       |
| IS NULL          | 是NULL                                                       |
| AND 或 &&        | 并且                                                         |
| OR 或 \|\|       | 或者                                                         |



示例：

~~~mysql
select * from stu;

-- 条件查询
-- 1.查询年龄大于20岁的学员信息
select * from stu where age > 20;
~~~

<img src="Java Web 基础.assets/image-20220222142624065.png" alt="image-20220222142624065" style="zoom:80%;" /> 

***

~~~mysql
-- 查询年龄大于等于20岁的学员信息
select * from stu where age >= 20;
~~~

<img src="Java Web 基础.assets/image-20220222142636522.png" alt="image-20220222142636522" style="zoom:80%;" /> 

***

~~~mysql
-- 查询 大于等于20岁 并且 年龄 小于等于30岁 的学员信息
select * from stu where age >= 20 and age <= 30;
select * from stu where age between 20 and 30;
~~~

<img src="Java Web 基础.assets/image-20220222142539681.png" alt="image-20220222142539681" style="zoom:80%;" /> 

***

~~~mysql
-- 查询入学日期在 '1998-09-01' 到 '1999-09-01'之间的学员信息
select * from stu where hire_date between'1998-09-1' and '1999-09-01';
~~~

<img src="Java Web 基础.assets/image-20220222142737863.png" alt="image-20220222142737863" style="zoom:80%;" /> 

***

~~~mysql
-- 查询年龄等于18岁的学员信息
select * from stu where age=18;
~~~

<img src="Java Web 基础.assets/image-20220222142842413.png" alt="image-20220222142842413" style="zoom:80%;" /> 

***

~~~mysql
-- 查询年龄不等于18岁的学员信息
select * from stu where age!=18;
select * from stu where age<>18;
~~~

<img src="Java Web 基础.assets/image-20220222142911778.png" alt="image-20220222142911778" style="zoom:80%;" /> 

***

~~~mysql
-- 查询年龄等于18岁或者年龄等于20岁或者年龄等于22岁的学员信息
select * from stu where age=18 or age=20 or age=22;
select * from stu where age in(18,20,22);
~~~

<img src="Java Web 基础.assets/image-20220222142940122.png" alt="image-20220222142940122" style="zoom:80%;" /> 

***

~~~mysql
-- 查询英语成绩为null的学员信息
-- 注意：NULL值的比较不能使用 = , !=比较，需要使用 is / is not比较
select * from stu where english=NULL; -- 错误的，查不到信息
select * from stu where english is NULL;
select * from stu where english is not NULL;
~~~

<img src="Java Web 基础.assets/image-20220222143029364.png" alt="image-20220222143029364" style="zoom:80%;" /> 

<img src="Java Web 基础.assets/image-20220222143052430.png" alt="image-20220222143052430" style="zoom:80%;" /> 

<img src="Java Web 基础.assets/image-20220222143128540.png" alt="image-20220222143128540" style="zoom:80%;" /> 

***

~~~mysql
-- 模糊查询 like ==========
/*
   通配符：
	 1. _: 代表单个任意字符
	 2. %: 代表任意个数字符
*/

-- 1. 查询姓'马'的学员信息
select * from stu where name like '马%';

-- 2. 查询第二个字是'花'的学员信息
select * from stu where name like '_化%';

-- 3. 查询名字中包含'德'的学员信息
select * from stu where name like '%德%';
~~~

<img src="Java Web 基础.assets/image-20220222143455079.png" alt="image-20220222143455079" style="zoom:80%;" /> 

<img src="Java Web 基础.assets/image-20220222143556093.png" alt="image-20220222143556093" style="zoom:80%;" /> 

<img src="Java Web 基础.assets/image-20220222143631681.png" alt="image-20220222143631681" style="zoom:80%;" /> 

***









##### <font size="5rem">3. 排序查询-ORDER BY</font>



1. 排序查询语法

~~~mysql
select 字段列表 from 表名 order by 排序字段名1 [排序方式1],排序字段名2 [排序方式2] ...;
~~~



排序方式：

+ ASC：升序排列（默认值）
+ DESC：降序排列

注意：如果有多个排序条件，当前边的条件值一样时，才会根据第二条件进行排序

~~~mysql
/*
   排序查询：
	    语法：select 字段列表 from 表名 order by 排序字段名1 [排序方式1],排序字段名2 [排序方式2] ...;
			排序方式：
			    ASC：升序排列（默认值）
					DESC：降序排列
*/

-- 1.查询学生信息，安装年龄升序排列
select * from stu order by age ASC;
select * from stu order by age;
~~~

<img src="Java Web 基础.assets/image-20220222152341135.png" alt="image-20220222152341135" style="zoom:80%;" /> 

***

~~~mysql
-- 2. 查询学生信息，按照数学成绩降序排列
select * from stu order by math DESC;
~~~

<img src="Java Web 基础.assets/image-20220222152531778.png" alt="image-20220222152531778" style="zoom:80%;" /> 

***

~~~mysql
-- 3. 查询学生信息，按照数学成绩降序排列，如果数学成绩一样，再按照英语成绩升序排列
select * from stu order by math DESC,english ASC;
~~~

<img src="Java Web 基础.assets/image-20220222152728674.png" alt="image-20220222152728674" style="zoom:80%;" /> 

> 注意：如果有多个排序条件，当前边的条件值一样时，才会根据第二条件进行排序

***









##### <font size="5rem">4. 分组查询-GROUP BY</font>



聚合函数

1. 概念：将一列数据作为一个整体，进行纵向计算
2. 聚合函数的分类：

| 函数名     | 功能                             |
| ---------- | -------------------------------- |
| cout(列名) | 统计数量（一般选用不为NULL的列） |
| max(列名)  | 最大值                           |
| min(列名)  | 最小值                           |
| sum(列名)  | 求和                             |
| avg(列名)  | 平均值                           |

3. 聚合函数语法：

~~~mysql
select 聚合函数名(列名) from 表;
~~~

注意：NULL 值不参与所有聚合函数的运算



~~~mysql
/*
sum():求和，且求和的列值必须为number数据类型
count()：统计记录记录数，且不能为空
   1. 主键：非空且唯一
	 2. *
max()：求一组值中的最大值，列值的类型可以为数据类型也可以为字符类型
min()：求一组值中的最小值，列值的类型可以为数据类型也可以为字符类型
avg()：求平均值，且求平均值的列值必须为number数据类型
*/

-- 1. 统计班级一共有多少个学生
select count(id) from stu;  -- 8
select count(english) from stu; -- 7
~~~

<img src="Java Web 基础.assets/image-20220223180249193.png" alt="image-20220223180249193" style="zoom:80%;" /> <img src="Java Web 基础.assets/image-20220223180300401.png" alt="image-20220223180300401" style="zoom:80%;" />

***

~~~mysql
-- 2. 查询数学成绩的最高分
select max(math) from stu;
~~~

<img src="Java Web 基础.assets/image-20220223180346822.png" alt="image-20220223180346822" style="zoom:80%;" /> 

***

~~~mysql
-- 3. 查询数学成绩的最低分
select min(math) from stu;
~~~

<img src="Java Web 基础.assets/image-20220223180458954.png" alt="image-20220223180458954" style="zoom:80%;" /> 

***

~~~mysql
-- 4. 查询数学成绩的总分
select sum(math) from stu;
~~~

<img src="Java Web 基础.assets/image-20220223180523784.png" alt="image-20220223180523784" style="zoom:80%;" /> 

***

~~~mysql
-- 5. 查询数学成绩的平均分
select avg(math) from stu;
~~~

<img src="Java Web 基础.assets/image-20220223180547155.png" alt="image-20220223180547155" style="zoom:80%;" /> 

***

~~~mysql
-- 6. 查询英语成绩的最低分
select min(english) from stu;
~~~

<img src="Java Web 基础.assets/image-20220223180609947.png" alt="image-20220223180609947" style="zoom:80%;" /> 

***

1. 分组查询语法

~~~mysql
select 字段列表 from 表名 [Where 分组条件前限定] group by 分组字段名 [Having 分组后条件过滤];
~~~

注意：分组之后，查询的字段为聚合函数和分组字段，查询其他字段无任何意义



~~~mysql
/*
    分组函数
		    select 字段列表 from 表名 [where 分组前条件限定] group by分组字段名 [having 分组后条件过滤]
*/

-- 1. 查询男同学和女同学各自的数学平均分
select sex,avg(math) from stu group by sex;
~~~

<img src="Java Web 基础.assets/image-20220223175710568.png" alt="image-20220223175710568" style="zoom: 80%;" /> 

***

~~~mysql
-- 2. 查询男同学和女同学各自的数学平均分以及各自人数
select sex,avg(math),count(*) from stu group by sex;
~~~

<img src="Java Web 基础.assets/image-20220223175811526.png" alt="image-20220223175811526" style="zoom:80%;" /> 

***

~~~mysql
-- 3. 查询男同学和女同学各自的数学平均分以及各自人数要求分数低于70分以下的不参与分组
select sex,avg(math),count(*) from stu where math>=70 group by sex;
~~~

<img src="Java Web 基础.assets/image-20220223175842569.png" alt="image-20220223175842569" style="zoom:80%;" /> 

***

~~~mysql
-- 4. 查询男同学和女同学各自的数学平均分以及各自人数要求分数低于70分以下的不参与分组,分组之后人数大于2 
select sex,avg(math),count(*) from stu where math>=70 group by sex having count(*)>2;
~~~

<img src="Java Web 基础.assets/image-20220223175914288.png" alt="image-20220223175914288" style="zoom:80%;" /> 

***

where 和 having 区别：

+ 执行时机不一样：where 是分组之前进行限定，不满足 where 条件，则不参与分组，而 having 是分组之后对结果进行过滤
+ 可判断条件不一样：where 不能对聚合函数进行判断，having 可以



执行顺序：where > 聚合函数 > having











##### <font size="5rem">5. 分页查询-LIMIT</font>



1. 分页查询语法

~~~mysql
select 字段列表 from 表名 LIMIT 起始索引,查询条目数;
~~~

+ 起始索引：从0开始

计算公式：起始索引 = (当前页码-1) * 每页显示的条数



注意：

1. 分页查询 LIMIT 是 MySQL 数据库的特有语言
2. Oracle 分页查询使用 rownumber
3. SQL Server 分页查询使用 top



示例：

~~~mysql
/*
    Select 字段列表 From 表名 Limit 起始索引,查询条目数
        起始索引：从0开始
*/

select * from stu;
-- 1. 从0开始查询，查询3条数据
select * from stu limit 0,3;

-- 2. 每页显示3条数据，查询第一页数据
select * from stu limit 0,3;

-- 3. 每页显示3条数据查询第2页数据
select * from stu limit 3,3;

-- 4. 每页显示3条数据查询第3页数据
select * from stu limit 6,3

-- 起始索引 = (当前页码-1) * 每页显示的条目数
~~~

<img src="Java Web 基础.assets/image-20220223213733495.png" alt="image-20220223213733495" style="zoom:80%;" /> 



总结：

<iframe src="//player.bilibili.com/player.html?aid=379163696&bvid=BV1Qf4y1T7Hx&cid=440652729&page=18" scrolling="no" border="0" frameborder="no" framespacing="0" allowfullscreen="true" height="650px"> </iframe>









### 1.4 图形化客户端工具



Navicat

+ Navicat for MySQL 是管理和开发 MySQL 或 MariaDB 的理想解决方案
+ 这套全面的前端工具为数据库管理、开发和维护提供了一款直观而强大的图形界面

[Navicat 官方网站](https://www.navicat.com.cn)

![image-20220222014534278](Java Web 基础.assets/image-20220222014534278.png)













### 1.5 约束



<iframe src="//player.bilibili.com/player.html?aid=379163696&bvid=BV1Qf4y1T7Hx&cid=440652753&page=19" scrolling="no" border="0" frameborder="no" framespacing="0" allowfullscreen="true" height="650px"> </iframe>



1. 约束的概念
   + 约束是作用于表中列上的规则，用于限制加入表的数据
   + 约束的存在保证了数据库中数据的正确性、有效性和完整性
2. 约束的分类

| 约束名称 | 描述                                                         | 关键字      |
| -------- | ------------------------------------------------------------ | ----------- |
| 非空约束 | 保证列中所有数据不能有NULL值                                 | NOT NULL    |
| 唯一约束 | 保证列中所有数据各不相同                                     | UNIQUE      |
| 主键约束 | 主键是一行数据的唯一标识，要求非空且唯一                     | PRIMARY KEY |
| 检查约束 | 保证列中的值满足某一条件                                     | CHECK       |
| 默认约束 | 保存数据时，未指定值则采用默认值                             | DEFAULT     |
| 外键约束 | 外键用来让两个表的数据之间建立链接，保证数据的一致性和完整性 | FOREIGN KEY |

Tips：MySQL 不支持检查约束



自动增长：

~~~mysql
-- 演示自动增长 auto_increment：当列是数字类型且是唯一约束
INSERT INTO emp ( ename, joindate, salary, bonus )
VALUES
	( '赵六', '1999-11-11', 8800, NULL );

INSERT INTO emp ( id, ename, joindate, salary, bonus )
VALUES
	( null, '赵六2', '1999-11-11', 8800, NULL );
~~~

<img src="Java Web 基础.assets/image-20220224000024329.png" alt="image-20220224000024329" style="zoom:80%;" /> 











##### <font size="5rem">1. 非空约束</font>



概念：

+ 非空约束用于保证列中所有数据不能有 NULL 值



语法：

1. 添加约束

~~~mysql
-- 创建表时添加非空约束
creat table 表名 (
   列名 数据类型 NOT NULL,
   ... 
);
~~~

~~~mysql
-- 建完表后添加非空约束
alter table 表名 modify 字段名 数据类型 not null;
~~~

2. 删除约束

~~~mysql
alter table 表名 modify 字段名 数据类型;
~~~



示例：

~~~mysql
DROP TABLE
IF
	EXISTS emp;-- 员工表
CREATE TABLE emp (
	id INT PRIMARY KEY auto_increment,-- 员工id，主键且自增长
	ename VARCHAR ( 50 ) NOT NULL UNIQUE,-- 员工姓名，非空且唯一
	joindate date NOT NULL,-- 入职日期，非空
	salary DOUBLE ( 7, 2 ) NOT NULL,-- 工资，非空
	bonus DOUBLE ( 7, 2 ) DEFAULT 0 -- 奖金，如果没有奖金默认为0
	
);

INSERT INTO emp ( id, ename, joindate, salary, bonus )
VALUES
	( 1, '张三', '1999-11-11', 8800, 5000 );

INSERT INTO emp ( id, ename, joindate, salary, bonus )
VALUES
	( 2, '李四', '1999-11-11', 8800, 5000 );

-- 演示非空约束
INSERT INTO emp ( id, ename, joindate, salary, bonus )
VALUES
	( 2, '李四', '1999-11-11', 8800, 5000 );
~~~

<img src="Java Web 基础.assets/image-20220223234147926.png" alt="image-20220223234147926" style="zoom:80%;" /> 









##### <font size="5rem">2. 唯一约束</font>



概念：

+ 唯一约束用于保证列中所有数据各不相同



语法：

1. 添加约束

~~~mysql
-- 创建表时添加唯一约束
creat table 表名 (
    列名 数据类型 unique [auto_increment],
    -- auto_increment：当不指定值时自动增长
   ... 
);

creat table 表名 (
   列名 数据类型,
   ...
   [constraint][约束名称] unique(列名)
);
~~~

~~~mysql
-- 建完表后添加唯一约束
alter table 表名 modify 字段名 数据类型 unique;
~~~

2. 删除约束

~~~mysql
alter table 表名 drop index 字段名
~~~



示例：

~~~mysql
DROP TABLE
IF
	EXISTS emp;-- 员工表
CREATE TABLE emp (
	id INT PRIMARY KEY auto_increment,-- 员工id，主键且自增长
	ename VARCHAR ( 50 ) NOT NULL UNIQUE,-- 员工姓名，非空且唯一
	joindate date NOT NULL,-- 入职日期，非空
	salary DOUBLE ( 7, 2 ) NOT NULL,-- 工资，非空
	bonus DOUBLE ( 7, 2 ) DEFAULT 0 -- 奖金，如果没有奖金默认为0
	
);


INSERT INTO emp ( id, ename, joindate, salary, bonus )
VALUES
	( 1, '张三', '1999-11-11', 8800, 5000 );

INSERT INTO emp ( id, ename, joindate, salary, bonus )
VALUES
	( 2, '李四', '1999-11-11', 8800, 5000 );

-- 演示唯一约束
INSERT INTO emp ( id, ename, joindate, salary, bonus )
VALUES
	( 3, '李四', '1999-11-11', 8800, 5000 );
~~~

<img src="Java Web 基础.assets/image-20220223235129398.png" alt="image-20220223235129398" style="zoom:80%;" /> 









##### <font size="5rem">3. 主键约束</font>



1. 概念：
   + 主键是一行数据的唯一标识，要求非空且唯一
   + 一张表只能有一个主键
2. 语法：
   1. 添加约束

~~~mysql
-- 创建表时添加主键约束
creat table 表名 (
   列名 数据类型 primary key [auto_increment],
   ... 
);

creat table 表名 (
   列名 数据类型,
   ...
   [constraint][约束名称] primary key(列名)
);
~~~

~~~mysql
-- 建完表后添加主键约束
alter table 表名 add primary key(字段名);
~~~

2. 删除约束

~~~Mysql
alter table 表名 drop primary key;
~~~



示例：

~~~mysql
DROP TABLE
IF
	EXISTS emp;-- 员工表
CREATE TABLE emp (
	id INT PRIMARY KEY,-- 员工id，主键且自增长
	ename VARCHAR ( 50 ) NOT NULL UNIQUE,-- 员工姓名，非空且唯一
	joindate date NOT NULL,-- 入职日期，非空
	salary DOUBLE ( 7, 2 ) NOT NULL,-- 工资，非空
	bonus DOUBLE ( 7, 2 ) DEFAULT 0 -- 奖金，如果没有奖金默认为0
	
);

select * from emp;

INSERT INTO emp ( id, ename, joindate, salary, bonus )
VALUES
	( 1, '张三', '1999-11-11', 8800, 5000 );

-- 演示主键约束，要求唯一且非空
INSERT INTO emp ( id, ename, joindate, salary, bonus )
VALUES
	( NULL, '张三', '1999-11-11', 8800, 5000 );

INSERT INTO emp ( id, ename, joindate, salary, bonus )
VALUES
	( 1, '张三', '1999-11-11', 8800, 5000 );

INSERT INTO emp ( id, ename, joindate, salary, bonus )
VALUES
	( 2, '李四', '1999-11-11', 8800, 5000 );
~~~

<img src="Java Web 基础.assets/image-20220224000642589.png" alt="image-20220224000642589" style="zoom:80%;" /> 











##### <font size="5rem">4. 默认约束</font>



概念：

+ 保存数据时，未指定值采用默认值



语法：

1. 添加约束

~~~mysql
-- 创建表时添加默认约束
create table 表名(
    列名 数据类型 default 默认值,
    ...
);
~~~

~~~mysql
-- 建完表后添加默认约束
alter table 表名 alter 列名 set default 默认值
~~~

2. 删除约束

~~~mysql
alter table 表名 alter 列名 drop default;
~~~



示例：

~~~mysql
DROP TABLE
IF
	EXISTS emp;-- 员工表
CREATE TABLE emp (
	id INT PRIMARY KEY auto_increment,-- 员工id，主键且自增长
	ename VARCHAR ( 50 ) NOT NULL UNIQUE,-- 员工姓名，非空且唯一
	joindate date NOT NULL,-- 入职日期，非空
	salary DOUBLE ( 7, 2 ) NOT NULL,-- 工资，非空
	bonus DOUBLE ( 7, 2 ) DEFAULT 0 -- 奖金，如果没有奖金默认为0
	
);


INSERT INTO emp ( id, ename, joindate, salary, bonus )
VALUES
	( 1, '张三', '1999-11-11', 8800, 5000 );

INSERT INTO emp ( id, ename, joindate, salary, bonus )
VALUES
	( 2, '李四', '1999-11-11', 8800, 5000 );

-- 演示默认约束
INSERT INTO emp ( id, ename, joindate, salary )
VALUES
	( 3, '王五', '1999-11-11', 8800 );

INSERT INTO emp ( id, ename, joindate, salary, bonus )
VALUES
	( 4, '赵六', '1999-11-11', 8800, NULL );
~~~

<img src="Java Web 基础.assets/image-20220223235721291.png" alt="image-20220223235721291" style="zoom:80%;" /> 









##### <font size="5rem">5. 外键约束</font>



<iframe src="//player.bilibili.com/player.html?aid=379163696&bvid=BV1Qf4y1T7Hx&cid=440652780&page=21" scrolling="no" border="0" frameborder="no" framespacing="0" allowfullscreen="true" height="650px"> </iframe>



概念：

+ 外键用来让连个表的数据之间建立链接，保证数据的一致性和完整性



语法：

1. 添加约束

~~~mysql
-- 创建表时添加外键约束
create table 表名(
   列名 数据类型,
   ...
   [constraint] [外键名称] foreign key(外键列名) references 主表(主表列名)
);
~~~

~~~mysql
-- 建完表后添加外键约束
alter table 表名 add constraint 外键名称 foreign key (外键字段名称) references 主表名称(主表列名称)
~~~

2. 删除约束

~~~mysql
alter table 表名 drop foreign key 外键名称;
~~~



示例：

~~~mysql
-- 删除表
drop table if exists emp;
drop table if exists dept;

-- 部门表
create table dept(
  id int primary key auto_increment,
	dep_name varchar(20),
	addr varchar(20)
);

-- 员工表
create table emp(
  id int primary key auto_increment,
	name varchar(20),
	age int,
	dep_id int,
	
	-- 添加外键 dep_id,关联dept表的id主键
	constraint fk_emp_dept foreign key(dep_id) references dept(id)
);

-- 添加2个部门
insert into dept(dep_name,addr) VALUES
('研发部','广州'),('销售部','深圳');

-- 添加员工,dep_id 表示员工所在的部门
insert into emp(`NAME`,age,dep_id) VALUES
('张三',20,1),
('李四',20,1),
('王五',20,1),
('赵六',20,2),
('孙七',22,2),
('周八',18,2);

-------------------
select * from emp;

-- 删除外键
alter table emp drop foreign key fk_emp_dept;

-- 建完表后，添加外键
alter table emp add constraint fk_emp_dept foreign key(dep_id) references dept(id)

-- 查另一张表
select * from dept;
~~~

<img src="Java Web 基础.assets/image-20220224162044815.png" alt="image-20220224162044815" style="zoom:80%;" /> 

试图删除主表的某列数据：

<img src="Java Web 基础.assets/image-20220224162104254.png" alt="image-20220224162104254" style="zoom:80%;" /> 













### 1.6 数据库设计



1. 软件的研发步骤

~~~mermaid
graph LR
    A(需求分析) --> B(设计) --> C(编码) --> D(测试) --> E(安装部署)
~~~

2. 数据库设计概念

+ 数据库设计就是根据业务系统的具体需求，结合我们所选用的DBMS，为这个业务系统构造出最优的数据存储模型

+ 建立数据库中的表结构以及表与表之间的关联关系的过程

+ 有哪些表？表里有哪些字段？表和表之间有什么关系？



3. 数据库设计的步骤

   1. 需求分析（数据是什么？数据具有哪些属性？数据与属性的特点是什么？）

   2. 逻辑分析（通过ER图对数据库进行逻辑建模，不需要我们考虑所选用的数据库管理系统）

   3. 物理设计（根据数据库自身的特点，把逻辑设计转换为物理设计

   4. 维护设计（1.对新的需求进行建表; 2.表优化）





表关系

+ 一对一：

  如：用户 和 用户详情

  一对一关系多用于表拆分，将一个实体中经常使用的字段放一张表，不经常使用的字段放另外一张表，用于提升查询性能 



+ 一对多（多对一）：

  如：部门 和 员工

  一个部门对应多个员工，一个员工对应一个部门



+ 多对多：

  如：商品 和 订单

  一个商品对应多个订单，一个订单包含多个商品











#### 1. 表关系之一对多



一对多（多对一）

如：部门表 和 员工表

一个部门对应多个员工，一个员工对应一个部门



<font color="red">实现方式：在多的一方建立外键，指向一的一方的主键</font>

![image-20220224171059643](Java Web 基础.assets/image-20220224171059643.png)









#### 2. 表关系之多对多



多对多：

如：商品 和 订单

一个商品对应多个订单，一个订单包含多个商品



<font color="red">实现方式：建立第三张中间表，中间表至少包含两个外键，分别关联两方主键</font>

![image-20220224171532571](Java Web 基础.assets/image-20220224171532571.png)

示例：

~~~Mysql
/*多对多：
    如：商品 和 订单
    一个商品对应多个订单，一个订单包含多个商品
    实现方式：建立第三张中间表，中间表至少包含两个外键，分别关联两方主键
*/

-- 删除表 
drop table if exists tb_order_goods;
drop table if exists tb_order;
drop table if exists tb_goods;

-- 订单表
create table tb_order(
  id int primary key auto_increment,
	payment double(10, 2),
	payment_type tinyint,
	status tinyint
);

-- 商品表
create table tb_goods(
  id int primary key auto_increment,
	title varchar(100),
	price double(10,2)
);

-- 订单商品中间表
create table tb_order_goods(
  id int primary key auto_increment,
  order_id int,
	goods_id int,
	count int
);

-- 建完表后，添加外键
alter table tb_order_goods add constraint fk_order_id foreign key(order_id) references tb_order(id);
alter table tb_order_goods add constraint fk_goods_id foreign key(goods_id) references tb_goods(id);
~~~

<img src="Java Web 基础.assets/image-20220224173137446.png" alt="image-20220224173137446" style="zoom:80%;" /> 









#### 3. 表关系之一对一



一对一：

如：用户 和 用户详情

一对一关系多用于表拆分，将一个实体中经常使用的字段放一张表，不经常使用的字段放另外一张表，用于提升查询性能



<font color="red">实现方式：在任意一方加入外键，关联另一方主键，并且设置外键为==唯一(UNIQUE)==</font>

<img src="Java Web 基础.assets/image-20220224173333529.png" alt="image-20220224173333529" style="zoom:80%;" /> 

![image-20220224173406525](Java Web 基础.assets/image-20220224173406525.png)







#### 4. 总结



+ 一对多实现方式
  + 在多的一方建立外键关联一的一方主键



+ 多对多实现方式
  + 建立第三张中间表
  + 中间表至少包含2个外键，分别关联双方主键



+ 一对一实现方式
  + 在任意一方建立外键，关联对方主键，并且设置外键唯一











### 1.7 数据库设计案例



<iframe src="//player.bilibili.com/player.html?aid=379163696&bvid=BV1Qf4y1T7Hx&cid=440652806&page=24" scrolling="no" border="0" frameborder="no" framespacing="0" allowfullscreen="true" height="650px"> </iframe>