

#### MySQL 常用命令

-------------------**打开服务**------------------

**连接数据库**:

>mysql -h主机地址 -u用户名 -p用户密码   (注:u与用户名可以不用加空格，其它也一样 )

**修改密码：**

>mysqladmin -u用户名 -p旧密码 password（ 新密码）;//MySQL5.0
>alter user 'root'@'localhost' identified by '你的新密码';//MySQL8.0

**断开连接:**  exit(回车)

**创建授权：** 

>grant select on 数据库.* to 用户名@登录主机 identified by \"密码\" ;

**删除授权:**  

>revoke select,insert,update,delete om *.* from test2@localhost; 

**创建数据库：**

>create database 库名;  

**显示数据库：**

>show databases;  

**使用数据库：**

>use 库名;  

**显示数据表：**

>show tables;  

**显示表结构：**

>describe 表名;  

**删除数据库：**

>drop database 库名;  

**备份数据库：**

>mysql\bin\mysqldump -h(ip) -uroot -p(password) databasename > database.sql 

**恢复数据库：**

>mysql\bin\mysql -h(ip) -uroot -p(password) databasename < database.sql  

**复制数据库：**

>CREATE DATABASE new_db DEFAULT CHARACTER SET UTF8 COLLATE UTF8_GENERAL_CI;
>mysqldump old_db -uroot -p123 --add-drop-table | mysql new_db -uroot -p123
>-- 不同服务器
>mysqldump old_db -uroot -p123 --add-drop-table | mysql -h 192.168.5.115 iot_telecom -uroot -p123


**导出整个数据库：**

>mysqldump -uroot -p123 dbname > d:\dbname.sql

**导入整个数据库：** 

> mysql -uroot -p123
> CREATE DATABASE new_db DEFAULT CHARACTER SET UTF8 COLLATE UTF8_GENERAL_CI;
> use new_db;
> source d:/dbname.sql


**查询表：**

>select * from 表名;  

**创建表：**

>create table 表名 (字段设定列表); 

>  create table stu(
>
>   sid varchar2(8) Primary Key,
>
>   name varchar2(20) Not Null,
>
>   age number(3),
>
>  addr varchar2(40)
>
>  );

**删除表：**

>drop table 表名; (无法删除有外键约束的表)

**清空表：**

>delete from 表名; 

**删除主键:**  

>alter table tablen_name drop constraint keyname;

**修改表结构:**

**修改表名：**

>alter table 旧表名 rename 新表名;

**修改列的数据类型:**

>alter table 表名 modify 列名 数据类型

**添加列:** 

>alter table 表名 add 列名 数据类型

**修改列:** 

>alter table 表名 change 旧列名 新列名 修改后的类型

**删除列:** 

>alter table 表名 drop 列名


**复制表**

(1) 复制表结构和表记录

create table 表名 as select * from 要复制的表名 where 1=1

(2) 只复制表结构 

create table 表名 as select * from 要复制的表名 where 1=2

**备份表:** mysqlbinmysqldump -h(ip) -uroot -p(password) databasename tablename > tablename.sql  

**恢复表:** mysqlbinmysql -h(ip) -uroot -p(password) databasename tablename < tablename.sql（操作前先把原来表删除）  



**查看用户定义的表:**  selecet table_name from user_tables;

**查看用户定义的各种数据库对象:**  select object_name,object_type from user_objects

**查看用户定义的表,视图,同义词和序列:**  select * from user_catalog

---------------------------------------------------------------------------

**insert语句--增**

```mysql
     insert into 表名 (列,列,列...) values(值,值,值...);
     insert into 表名 values(值,值,值...);
```

**delete语句--删**

```mysql
     delete from 表名 where 条件;
```

**update语句--改**

```mysql
     update 表名 set 列名=新值 where 条件;
```

**select语句--查**

```mysql
select [distinct] * | 列名1，列名2..., 列名n , 组函数(...)
from 表名1，表名2...
[where 条件 ( in,or,and,between and,is [not] null ) ]
[group by 列名1，列名2... ] 
[having 条件]
[order by 排序列名1 ASC | DESC , 排序列名2 ASC | DESC...]
[limit]
```





#### MySQL 常用函数

**字符串函数**

- ascii(str) - 返回字符串str的第一个字符的ascii值(str是空串时返回0)
- concat(str1,str2,...) - 把参数连成一个长字符串并返回(任何参数是null时返回null)  
- length(str)  - 返回字符串的长度,一个汉字是算三个字符，一个数字或字母算一个字符。
- locate(substr,str) - 返回字符串substr在字符串str第一次出现的位置(str不包含substr时返回0)  
- locate(substr,str,pos) - 返回字符串substr在字符串str的第pos个位置起第一次出现的位置(str不包含substr时返回0)  
- instr(str,substr) - 返回字符串substr在字符串str第一次出现的位置(str不包含substr时返回0)  
- lpad(str,len,padstr) - 用字符串padstr填补str左端直到字串长度为len并返回  
- rpad(str,len,padstr) - 用字符串padstr填补str右端直到字串长度为len并返回
- left(str,len) - 返回字符串str的左端len个字符
- right(str,len) - 返回字符串str的右端len个字符
- substring(str,pos,len) - 返回字符串str的位置pos起len个字符  
- substring(str,pos) - 返回字符串str的位置pos起的一个子串
- ltrim(str) - 返回删除了左空格的字符串str  
- rtrim(str)  - 返回删除了右空格的字符串str  
- space(n) - 返回由n个空格字符组成的一个字符串  
- replace(str,from_str,to_str)  - 用字符串to_str替换字符串str中的子串from_str并返回 
- reverse(str) - 颠倒字符串str的字符顺序并返回
- insert(str,pos,len,newstr) - 把字符串str由位置pos起len个字符长的子串替换为字符串
- lower(str) - 返回小写的字符串str  
- upper(str) - 返回大写的字符串str
- substring_index(str,delim,count) -  如果count是正数，那么就是从左往右数，第N个分隔符的左边的全部内容
- char_length(str) -  不管汉字还是数字或者是字母都算是一个字符。

**数字函数**

- abs(n) - 求绝对值
- mod(n,m) - 取模运算,返回n被m除的余数(同%操作符)
- floor(n) - 返回不大于n的最大整数值  
- ceiling(n) - 返回不小于n的最小整数值  
- round(n,d) - 返回n的四舍五入值,保留d位小数(d的默认值为0)
- pow(x,y) - 返回值x的y次幂  
- sqrt(n) - 返回非负数n的平方根
- pi() - 返回圆周率  
- rand() - 返回在范围0到1.0内的随机浮点值
- truncate(n,d) - 保留数字n的d位小数并返回 

**日期时间函数**

- dayofweek(date) - 返回日期date是星期几(1=星期天,2=星期一,……7=星期六,odbc标准)  
- weekday(date) - 返回日期date是星期几(0=星期一,1=星期二,……6= 星期天)
- year(date) - 返回date的年份(范围在1000到9999)    
- month(date)  - 返回date中的月份数值   
- dayofmonth(date) - 返回date是一月中的第几日(在1到31范围内)   
- hour(time) - 返回time的小时数(范围是0到23)  
- minute(time) - 返回time的分钟数(范围是0到59) 
- second(time) - 返回time的秒数(范围是0到59) 
- period_add(p,n) - 增加n个月到时期p并返回(p的格式yymm或yyyymm)    
- period_diff(p1,p2) - 返回在时期p1和p2之间月数(p1和p2的格式yymm或yyyymm)  
- curdate() - 以'yyyy-mm-dd'或yyyymmdd格式返回当前日期值(根据返回值所处上下文是字符串或数字) 
- curtime() - 以'hh:mm:ss'或hhmmss格式返回当前时间值(根据返回值所处上下文是字符串或数字)
- now() - 以'yyyy-mm-dd hh:mm:ss'或yyyymmddhhmmss格式返回当前日期时间(根据返回值所处上下文是字符串或数字)     
- last_day(date) - date日期所在月的最后一天是什么时候
- current_timestamp, current_timestamp() - 获得当前时间戳函数
- datediff(d1,d2) - 两个日期d1,d2之间相差的天数
- from_unixtime(time-stamp) - 日期转时间戳

**其他**

date_add(date,interval expr type)  
date_sub(date,interval expr type)    
adddate(date,interval expr type)    
subdate(date,interval expr type)  
对日期时间进行加减法运算  
(adddate()和subdate()是date_add()和date_sub()的同义词,也
可以用运算符+和-而不是函数  
date是一个datetime或date值,expr对date进行加减法的一个表
达式字符串type指明表达式expr应该如何被解释  

　[type值 含义 期望的expr格式]:  
　second 秒 seconds    
　minute 分钟 minutes    
　hour 时间 hours    
　day 天 days    
　month 月 months    
　year 年 years    
　minute_second 分钟和秒 "minutes:seconds"    
　hour_minute 小时和分钟 "hours:minutes"    
　day_hour 天和小时 "days hours"    
　year_month 年和月 "years-months"    
　hour_second 小时, 分钟， "hours:minutes:seconds"    
　day_minute 天, 小时, 分钟 "days hours:minutes"    
　day_second 天, 小时, 分钟, 秒 "days
hours:minutes:seconds" 
　expr中允许任何标点做分隔符,如果所有是date值时结果是一个
date值,否则结果是一个datetime值)  
　如果type关键词不完整,则mysql从右端取值,day_second因为缺
少小时分钟等于minute_second)  
　如果增加month、year_month或year,天数大于结果月份的最大天
数则使用最大天数)    

**日期格式化**

date_format(date,format)    

```
--根据format字符串格式化date值  
　(在format字符串中可用标志符:  
　%m 月名字(january……december)    
　%w 星期名字(sunday……saturday)    
　%d 有英语前缀的月份的日期(1st, 2nd, 3rd, 等等。）    
　%Y 年, 数字, 4 位    
　%y 年, 数字, 2 位    
　%a 缩写的星期名字(sun……sat)    
　%d 月份中的天数, 数字(00……31)    
　%e 月份中的天数, 数字(0……31)    
　%m 月, 数字(01……12)    
　%c 月, 数字(1……12)    
　%b 缩写的月份名字(jan……dec)    
　%j 一年中的天数(001……366)    
　%h 小时(00……23)    
　%k 小时(0……23)    
　%h 小时(01……12)    
　%i 小时(01……12)    
　%l 小时(1……12)    
　%i 分钟, 数字(00……59)    
　%r 时间,12 小时(hh:mm:ss [ap]m)    
　%t 时间,24 小时(hh:mm:ss)    
　%s 秒(00……59)    
　%s 秒(00……59)    
　%p am或pm    
　%w 一个星期中的天数(0=sunday ……6=saturday ）    
　%u 星期(0……52), 这里星期天是星期的第一天    
　%u 星期(0……52), 这里星期一是星期的第一天    
　%% 字符% )  
```

**转换函数**

> (1).字符串与数字之间转换

```
字符串转换成数字
方法一：SELECT CAST('123' AS SIGNED);
方法二：SELECT '123'+0;//亲测有效
方法三：SELECT CONVERT('123',SIGNED);
=======
数字转换成字符串
使用concat函数
```

> (2).字符串与日期之间转换

```
日期转换成字符串使用date_format函数
字符串转换成日期str_to_date(str,format)；注:format格式必须和str的格式相同，否则返回空
```

**练习**

1. 查出客户表(s_customer)中phone列最后一个-线后面的部分
2. 模拟向银行中只显示姓名的第一个字符(奥巴马变成奥**)
3. 找出名字长度超过5的员工
4. 找出职称是 stock clerk的员工
5. 找出员工的工作月数
6. 查询员工的工作天数
7. 计算一年前,当前,一年后的时间:
8. 当前日期前六个月的最后一天;
9. 把员工的入职日期格式化为年/月/日
10. 找出每个员工的名字和它的薪水(如:$2,500.00)
11. 找出5月份入职的员工





#### MySQL 数据库建模知识

一、概述

实体-联系即为E-R图，这其实是在数据库建模时候，也就是数据库设计的阶段才用到的，但是我会在需求分析、梳理、设计都会用到。

本节主要简述实体及实体之间的3种联系，帮助我们从正、反两方面来分析问题，便于我们更清晰业务需求。

二、  实体
世界由人、物、联系组成，其中人和物都是实体，并且他们都有各自的属性。

2.1     实体分类
官方解释：客观存在并相互区别的事物称为实体。 实体是一个抽象名词，是指一个独立的事物个体，自然界的一切具体存在的事物都可以看做一个实体。一个人是一个实体，一个组织也可以看做一个实体。实体不是某一个具体事物，而是自然界所有事物的统称。实体可以是有形的，也可以是无形的，实体也可以是抽象的事物或联系

理解点：1、客观存在的人（机构，下同）、物，有形的、无形的；2、独立的个体；

角色实体

人在系统中可以定义为角色实体，即为参与系统的“干系人”，他们可以是后台的系统管理员、负责审批的审批员，还是前端的促销员，普通的用户，又或者是某个渠道经销商；他是独立的个体，且在系统中是可以模拟、抽象出来的。

他们是否主动参与系统；
是否与其他已经定义的角色有重合；
他们参与系统主要是想达到什么目的（即角色权限）；
物实体

实体中，除去人，剩下的就是物，我们定义为物实体。角色实体可以通过系统达到什么目的，即系统中的功能，这就是物实体；在面对对象的解释中，物实体其实就对象的概念；

举个栗子：项目管理系统，经销商可以发起项目，由后台管理员审核后即可生成项目；

这其中涉及到的角色实体：经销商、后台管理员；物实体：项目、审核；

2.2 实体属性
实体属性，即记录实体的基本属性、特性的信息，在产品的线框图中的页面元素，在数据库表中对应某个具体的字段。

属性是构成实体的组成部分，每个实体都有属性，哪怕是一个编码也是其属性，一个没有属性的实体是不存在的。

其次要说说属性中的用于区分同一实体不同对象的关键属性，建模中我们称之为主键，主键具有唯一性，无论是数据库自增长的序列还是根据特定规则生成的具有识别功能的编码，或者也有可能是多个字段为主键（如N:N的关系表中），我们都可以定义为主键。

日常中我们也常会遇到，注册其他网站时，首先让我们输入手机号，如果手机号已经注册，会提示不能再注册，该手机号已经注册了。其中，这个手机号就是用于区分用户的唯一识别码，具有唯一性。

三、  联系
联系，即实体之间的联系，他们可以是角色实体-物实体，物实体-物实体、角色实体-角色实体。分为3种关系，即1-1，1-N，N-N；判断关系应从正、反两方面去看，正向即从A-B，反向即B-A；其中A-B时，默认A为某一个固定实体，看他对应几个B；同理B-A；

1-1，关系比较简单，确定一个，另一个也随之确定，转化成数据表基本上用一张表来记录就可以；

举例：比如部门经理与部门的关系（暂不考虑特殊情况，纯举例），正向：一个部门经理管理一个部门；反向：一个部门只有一个部门经理； 一张“部门-部门经理”，记录部门与部门经理的对应关系即可（视实际情况而定）；

问题围绕

正向提问，答案是否是唯一；
反向提问，答案是否唯一；
1-N，即一对多，一般为隶属、管理、父子这种关系发展而来，转化成数据表是将“1”实体作为“N”实体的一个属性来记录这种关系。

举例：如部门与员工的关系，正向：一个部门有多个员工，确定员工是N；反向：一个员工只隶属于一个部门，确定部门是1，所以部门-员工为1：N；

实体表为“部门表”“人员表”，在人员表中增加“隶属部门”，这种“部门-员工”的关系就可以记录，共2张表。

问题围绕

正向提问，确定1：N中的N对应哪个实体；
反向提问，确认1：N中的1对应哪个实体；
N：N，即多对多，正向、反向都是多的情况，这种转化成数据表的时候是3张表，2张实体表+1张关系表，关系表记录的是2个实体的对应关系，关系表是以2个实体的主键作为主键。

举例：大学期间的学生-课程的关系，正向：一个学生可以上多门课程；反向：一门课程允许多个学生来学习，关系确定为N:N；转化成数据表，即实体表“学生表”“课程表”，还有“学生-课程”关系表。

举例：张三报了3门课程，分别是高等数学、英语和思想政治；关系表就会生成3条记录，分别为“张三、高等数学”“张三、英语”、“张三、思想政治”，是以“人员+课程”作为主键；

四、  写在后面
对于产品来说，了解E-R建模其实是培养思维方式，将需求可视化。我们需要做的是多从这个角度去思考问题，尽可能的考虑到所有场景，这样在需求交接到开发的时候，他们看到的需求是全面且清晰的，而不会出现他们在建模阶段发现我们遗漏了一些问题而导致需求不明确。我们最了解的是业务和需求，如果我们再懂一些建模知识，这其实可以避免技术、开发少走不少弯路。因为像一般的软件公司，根本就没有数据库建模这一说，所以数据库表结构的设计能否最大程度的贴合需求，是很难说的事情。

一般情况下，我在做获取、梳理、设计时，都会从这个方式去思考问题；需求交接到开发时，我会提醒他们哪些需要着重梳理，但是不会干涉数据库的设计。

注：我们这里所说的实体、实体之间的联系，只是从产品的角度去度量、思考、表达系统/功能，帮助我们更好的了解、梳理系统/功能，不要求专业性的产物。





#### MySQL 安装

**Windows 上安装 MySQL**

官方下载地址:https://dev.mysql.com/downloads/mysql/

有安装版本和解压缩版本

**1. 以解压缩版为例**

(1).我们将 zip 包解压到相应的目录，这里我将解压后的文件夹放在 D:\Program File\mysql-8.0.11-winx64下.

(2).进行mysql的环境变量的配置.

```
MYSQL_HOME: D:\Program File\mysql-8.0.11-winx64
Path: %MYSQL_HOME%\bin
```

(3).在 D:\Program File\mysql-8.0.11-winx64下新建my.ini文件.编辑如下内容:

```java
[mysql]
# 设置mysql客户端默认字符集
default-character-set=utf8
[mysqld]
# 设置3306端口
port = 3306
# 设置mysql的安装目录
basedir=D:\Program File\mysql-8.0.11-winx64
# 设置mysql数据库的数据的存放目录
datadir=D:\Program File\mysql-8.0.11-winx64\data
# 允许最大连接数
max_connections=20
# 服务端使用的字符集默认为8比特编码的latin1字符集
character-set-server=utf8
# 创建新表时将使用的默认存储引擎
default-storage-engine=INNODB

```

> 1. 以``管理员身份``打开 cmd 命令行工具.安装mysql服务.输入如下:

```java
mysqld install
```

> 1. 初始化data目录.

```java
mysqld --initialize-insecure 
```

> 1. 启动mysql服务器

```java
net start mysql
```

> 1. 输入mysql -uroot -p

```
会提示输入密码,直接敲enter出现如图所示,表示成功连接到mysql服务器.
```

> 8.修改密码

```java
//在mysql安装目录生成的data文件下，查找xxx.err的文件：可以看到临时密码
mysqladmin -u用户名 -p旧密码 password 新密码;
```





#### MySQL 简介

**一、什么是数据库(DataBase)**
数据库(Database)是按照数据结构来组织、存储和管理数据的建立在计算机存储设备上的仓库
	想象一下这个场景：某高中二年级有三个班，期末考试成绩下来了，每个班的学生的成绩都打印在了一张A4纸上，而每个班的成绩单都放在一个档案袋里，最后所有的档案袋都放在李主任那里保管。每个班的成绩表上记录着该班所有学生的成绩，其内容大概是下面这个样子：![](https://i.imgur.com/OTrlarh.png)

```
【该表中所有成员的数据结构都相同，也就是按照数据结构来组织、存储和管理数据。】

档案袋--数据库，成绩表--数据库中的表，李主任--数据库服务器。
开学来了老师们都要联系李主任去拿档案袋，我们在使用数据库时也要首先连接数据库。
```

**二、数据库分类**
	数据库通常分为**层次式数据库**、**网络式数据库**和**关系式数据库三**种，不同的数据库是按不同的数据结构来联系和组织的。当今的互联网，最常见的数据库模型主要是两种：即【关系型数据库和非关系型数据库\<NOSQL>】

1. 关系型数据库（RDBMS）

- 关系模型由二维表及其之间的联系组成的一个数据组织 ；
- 通过外键关联来建立表与表之间的关系 ；
- RDBMS(关系数据库) 中的数据存储在被称为表（tables）的数据库对象中 ；
- 表是相关的数据项的集合，它由列和行组成 ；
- 当前主流的关系型数据库有Oracle、DB2、PostgreSQL、Microsoft SQL Server、Microsoft Access、MySQL、浪潮K-DB等。

- 关系型数据库瓶颈:

（1）高并发读写需求

```
网站的用户并发性非常高，往往达到每秒上万次读写请求，对于传统关系型数据库来说，硬盘I/O是一个很大的瓶颈
```

（2）海量数据的高效率读写

```
网站每天产生的数据量是巨大的，对于关系型数据库来说，在一张包含海量数据的表中查询，效率是非常低的
```

（3）高扩展性和可用性

```
在基于web的结构当中，数据库是最难进行横向扩展的，当一个应用系统的用户量和访问量与日俱增的时候，
数据库却没有办法像web server和app server那样简单的通过添加更多的硬件和服务节点来扩展性能和负载能力。
对于很多需要提供24小时不间断服务的网站来说，对数据库系统进行升级和扩展 是非常痛苦的事情，往往需要停机维护和数据迁移。
对网站来说，关系型数据库的很多特性不再需要了：
```

（4）事务一致性

```
关系型数据库在对事物一致性的维护中有很大的开销，而现在很多web2.0系统对事物的读写一致性都不高
```

（5）读写实时性

```
对关系数据库来说，插入一条数据之后立刻查询，是肯定可以读出这条数据的，但是对于很多web应用来说，并不要求这么高的实时性，比如发一条消息之后，过几秒乃至十几秒之后才看到这条动态是完全可以接受的
```

（6）复杂SQL，特别是多表关联查询

```
任何大数据量的web系统，都非常忌讳多个大表的关联查询，以及复杂的数据分析类型的复杂SQL报表查询，特别是SNS类型的网站，
从需求以及产品阶级角度，就避免了这种情况的产生。
往往更多的只是单表的主键查询，以及单表的简单条件分页查询，SQL的功能极大的弱化了。
```

2.非关系型数据库

- 又被称为NoSQL（Not Only SQL )，意为不仅仅是SQL；
- 对NoSQL是“非关联型的”，强调Key-Value 存储和文档数据库的优点 ；
- 主要代表有MongoDB，Redis、HBase等,依据结构化方法以及应用场合的不同，
- 主要分为以下几类：  

（1）面向高性能并发读写的key-value数据库：

```
key-value数据库的主要特点即使具有极高的并发读写性能，Redis,Tokyo Cabinet,Flare就是这类的代表
```

（2）面向海量数据访问的面向文档数据库：

```
这类数据库的特点是，可以在海量的数据中快速的查询数据，典型代表为MongoDB以及CouchDB
```

（3）面向可扩展性的分布式数据库：

```
这类数据库想解决的问题就是传统数据库存在可扩展性上的缺陷，这类数据库可以适应数据量的增加以及数据结构的变化	
```

**三、MySQL简介**

- MySQL是一个关系型数据库管理系统，由瑞典MySQL AB 公司开发，目前属于 Oracle 旗下产品(2008年1月16号)。
- MySQL 是最流行的关系型数据库管理系统之一，在 WEB 应用方面，MySQL是最好的 RDBMS (Relational Database Management System) 应用软件。
- MySQL是一种关系数据库管理系统，关系数据库将数据保存在不同的表中，而不是将所有数据放在一个大仓库内，这样就增加了速度并提高了灵活性。
- MySQL所使用的 **SQL语言**是用于访问数据库的最常用标准化语言。MySQL 软件采用了双授权政策，分为社区版和商业版，
- 由于其体积小、速度快、总体拥有成本低，尤其是开放源码这一特点，一般中小型网站的开发都选择 MySQL 作为网站数据库。
- MySQL是一种开放源代码的关系型数据库管理系统（RDBMS）
- 使用的 SQL 语言是用于访问数据库的最常用标准化语言。
- MySQL 软件采用了双授权政策，分为社区版和商业版，由于其体积小、速度快、总体拥有成本低,尤其是开放源码这一特点，一般中小型网站的开发都选择 MySQL 作为网站数据库。
- 随着 MySQL 被 Oracle 收购，MySQL 的用户和开发者开始质疑开源数据库的命运，有一部分人开始寻找 MySQL 的替代品，其中比较主流的有： Percona Server 、MariaDB、 Drizzle。值得一提的是 MariaDB 的创始人正是 MySQL 的创始人。

**1.SQL介绍**

它是操作数据库管理系统的一个标准:主要对数据库进行CRUD的操作, 数据库的运算都是通过SQL来完成的.
create:创建
delete:删除
update:修改
retrieve:检索
市面上的主流数据库都遵守SQL规范:
注:不同的数据库对SQL的支持又有些不同;

**2.SQL**

(1) **SQL**: Structured Query Language--结构化查询语言;

```
select [distinct] * | 列名1，列名2..., 列名n , 组函数(...)
from 表名1，表名2...
[where 条件 ( in,or,and,between and,is [not] null ) ] 
[group by 列名1，列名2... ] 
[having 条件]
[order by  排序列名1 ASC | DESC , 排序列名2 ASC | DESC...]
```

(2) **DDL**: Data Definition Language--数据定义语言;

以数据库表为例： 对表中结构操作 （创建表 create，修改表结构alter ，删除表 drop）create,alter,drop,truncate,comment on,rename to...

```
A.建表
create table 表名(
  列名 数据类型,
  列名 数据类型,
  列名 数据类型
)
```

(3) **DML**: Data Manipulating Language--数据操作语言

以数据库表为例： 对表中记录操作 （添加记录 insert，删除记录 delete，修改记录 update

(4) **DCL**: Data Control Language--数据控制语言
 	grant,revoke...

(5) **DQL**: Date Query Language--数据查询语句
	select

(6) **DTL**: Data Transaction Language--数据事务语言
	commit,rollback,savepoint





#### MySQL SQL:基础查询

**1.SQL查询**

	select [distinct] * | 列名1，列名2..., 列名n , 组函数(...)
	from 表名1，表名2...
	[where 条件 ( in,or,and,between and,is [not] null ) ] 

distinct:除去重复的值

**(1).单表查询**

查询student表中的所有信息

```
select *
from student;
select sno,sname,sage,sgender 
from student;
```

查询student表中的学号，姓名 

```
select sno,sname
from student
```

给表，列取别名  

```
select s.sno 学号,s.sname 姓名,s.sage 年龄,s.sgender  性别
from student s;
```

查询出学生表中学生的年龄  

```
select distinct  sage
from student
```

**(2).条件查询** 

查询出年龄为23的学生学号，姓名，年龄

```
select sno,sname,sage
from student
where sage = 23;

select sno,sname,sage
from student
where sage <> 23;

select sno,sname,sage
from student
where sage != 23;
```

查询出年龄不为23的学生学号，姓名，年龄

~~~
select sno,sname,sage
from student
where sage <> 23;

select sno,sname,sage
from student
where sage != 23;
~~~

查询出年龄大于23的学生学号，姓名，年龄

```
select sno,sname,sage
from student
where sage >= 24;
```

查询出年龄为23的男学生学号，姓名，年龄

```
select sno,sname,sage
from student
where sage = 23 and sgender='男';
```

查询出年龄为22和23,24,25的学生学号，姓名，年龄

```
select sno,sname,sage
from student
where sage = 22 or sage = 23 or sage = 24 or sage = 25；

select sno,sname,sage
from student
where sage in (22,23,24,25); 
 --- 等价于sage = 22 or sage = 23 or sage = 24 or sage = 25
```

查询出名称为王丽 、李波同学的详细信息

```
select sno,sname,sage,sgender
from student
where sname ="王丽" or sname ="李波";
```

**(3).like-模糊查询** 

> 通配符

- % :任意多个任意字符  
- _ : 任意一个字符

查询出名字中包含'张'的学生信息

```
select s.sno,s.sname ,s.sage,s.sgender
from student s
where sname like '%张%';
```

查询出名字中第二个字符为'张'的学生信息

```
select s.sno,s.sname ,s.sage,s.sgender
from student s
where sname like '_张%';
```

查询出名字中倒数第二个字符为'力'的学生信息

```
select s.sno,s.sname ,s.sage,s.sgender
from student s
where s.sname like '%力_';
```

查询出没有绩效的员工

```
select *
from emp
where comm is null
```

查询出有绩效的员工 

```
select *
from emp
where comm is not null	
```

 查询出薪资在2000-3000的员工

```
select *
from emp
where salary >=2000 and salary<=3000;

select *
from emp
where salary between 2000 and 3000 ;
```

查询出在10部门的所有的员工

```
select * 
from emp 
where deptno = 10;
```

查询出职位是'MANAGER'和'SALESMAN'的员工所有信息

```
select *
from emp
where job in('MANAGER','SALESMAN');
```

查询出员工的没有上级的员工信息  

```
select *
from emp
where mgr is null;
```

**(4).order by-排序**

- 升序 asc [默认值]
  降序 desc	

```
select
from 表名
where 条件表达式[or,and,is not null ,in between .. and ]
order by 列名1 asc|desc，列名2  asc|desc
```

查询30部门所有员工信息 ，员工编号，姓名，薪资，按照薪资的升序排列

```
select empno,ename,salary
from emp
where deptno = 30
order by salary asc;
```

查询员工信息 ，员工编号，姓名，薪资，按照薪资的降序排列,若薪资相同，按照姓名的字母先后顺序排序

```
select empno,ename,salary
from emp
order by salary desc , ename asc;
```

查询所有员工的绩效，若没有绩效，则用-1 替代显示

```
select IFNULL(comm,-1)
from emp
```

查询所有员工的年薪(薪资12)

```
select ename 姓名, salary*12 年薪
from emp
```

查询所有员工的年薪((薪资+绩效) 12 )

```
select ename 姓名, (salary+ ifnull(comm,0)   )*12 年薪
from emp
```





#### MySQL  SQL:分组查询

**1.SQL中的分组函数与分组查询**

	select [distinct] * | 列名1，列名2..., 列名n , 组函数(...)
	from 表名1，表名2...
	[where 条件 ( in,or,and,between and,is [not] null ) ]
	[group by 列名1，列名2... ] 
	[having 条件]
	[order by 排序列名1 ASC | DESC , 排序列名2 ASC | DESC...]

**2.分组函数**

- count(): 统计该字段非null的个数
- sum() ：记录的总和
- avg():平均值
- max()：最大值
- min():最小值

**3.group by分组函数使用注意事项：**

- （1）select 单列, 组函数 from ... 【错误】，一定要与group by 使用

where 与 having 的区别：

- （1）where 是分组之前的要过滤的条件,where后面不能与组函数一起使用 【where 与分组无关】
- （2）having 是分组之后的结果之上再做的过滤,having可以与组函数一起使用【having 与分组一起使用】

查询出所有员工的个数

```
select count(empno)
from emp
```

查询出所有员工的总薪资

```
select sum(salary)
from emp
```

查询出所有员工的平均薪资

```
select avg(salary)
from emp
```

查询出所有员工的最大薪资

```
select max(salary)
from emp
```

查询出所有员工的最小薪资

```
select min(salary)
from emp
```

统计各职位的员工个数

```
select job 职位, count(empno) 人数
from emp
group by job  -- 按照职位分组
```

统计各部门的员工个数，根据部门编号升序排序

```
select deptno ,count(empno)
from emp
group by deptno
order by deptno
```

统计各部门各职位的员工人数，根据部门编号升序排序，部门编号相同，则按照职位的字母先后顺序排序

```sql
select deptno 部门编号, job 职位,count(empno)	人数
from emp
group by deptno,job
order by deptno,job 
```

统计10部门的各职位的员工人数（显示部门编号，职位名称，员工人数）

```sql
select deptno 部门编号, job 职位,count(empno) 人数
from emp
where deptno=10
group by job
```

查询10部门的各职位的员工人数大于2的职位信息（显示部门编号，职位名称，员工人数）

```sql
select deptno 部门编号, job 职位,count(empno)	人数
from emp
where deptno=10
group by job
having count(empno) >2
```

		

​				

#### MySQL SQL:多表查询***

**多表查询(关联查询):可以跨多表查询**

查询出员工的编号，名字和他所在部门的编号，名字【错误】

```
select e.empno,e.ename,d.deptno,d.dname
from emp e,dept d
```

错误原因:

以上写法会出现笛卡尔积,产生很多冗余错误的数据,如果要

排除笛卡尔积,则应该使用where字句进行条件的过滤.

a.正确写法:传统方式

```
select e.empno,e.ename,d.deptno,d.dname
from emp e,dept d
where e.deptno = d.deptno
[表的主键 = 表的外键]
```

b.正确写法:join方式

```
select e.e
select e.firstname,d.name from semp e join sdept on e.deptid=d.id;
```

**內连接** inner  join : 多表连接满足指定条件的结果集

> table1  t1  inner join table2 t2 on  t1.列 = t2.列
>
> 等值连接  ： 连接的条件是 = 连接          on  t1.列 = t2.列
> 不等值连接 ：  连接的条件是 不相等 连接    on t1.列 > t2.列
> 自然连接 natural join  (删除重复列) 
>
> select  *  from emp  natural  join dept 

- 使用表别名可以简化查询
- 使用表名(表别名)前缀可提高查询效率

 ![](https://i.imgur.com/MydAhcj.jpg)



**外连接**  outer join 

a. 左外连接 left  [ outer ] join ：	把左边不满足条件的记录也需要查询出来

![img](https://i.imgur.com/Ix2ZoCb.jpg)

b.右外连接 right  [ outer ] join ：把右边不满足条件的记录也需要查询出来

![](https://i.imgur.com/DpF1PB9.jpg) 
	
3.**自连接**: 把表复制一份 作为另一个表

 注意： 表一定要取别名

**(1). 查询出在 ACCOUNTING 部门的员工编号，姓名**  

```
select empno, ename
from emp e  join dept d 
on e.deptno = d.deptno 
where d.dname = 'ACCOUNTING ';
```

**(2) 查询出所有部门的所有员工，列出所有部门信息、员工信息**

```
select  * 
from emp e     join dept  d 
on e.deptno = d.deptno;
```

**(3). 查询在北京工作的员工的平均薪资**

```
select avg(salary)
from emp e join dept d
on e.deptno = d.deptno 
where d.loc = 'beijing';
```

**(4).查询出各部门的员工人数（没有员工的部门也需要统计）**

```
select d.deptno , count(e.empno)
from emp  e   right outer  join dept d
on e.deptno = d.deptno
group by d.deptno;

select d.deptno , count(e.empno)
from dept  d left  outer  join emp e
on e.deptno = d.deptno
group by d.deptno;

	+--------+----------+
	| deptno | count(*) |
	+--------+----------+
	|     10 |        3 |
	|     20 |        5 |
	|     30 |        6 |
	|     40 |        0 |
	|     50 |        0 |
	+--------+----------+
```

**(5). 查询出员工编号，姓名，和该员工上级领导的编号与姓名 （给结果列取别名）**

```
select e.empno 员工编号, e.ename 员工姓名,e.mgr  上级领导的编号, m.ename   上级领导的名称 
from emp e  join emp m 
on e.mgr = m.empno ;
```

**(6). 查询出员工编号，姓名，和该员工上级领导的编号与姓名 （给结果列取别名 ，没有上级领导的记录也需要查询）**

```
select e.empno 员工编号, e.ename 员工姓名,e.mgr  上级领导的编号, m.ename   上级领导的名称 
from emp e left join emp m 
on e.mgr = m.empno ;
```

**(7). 查询出各年份员工入职人数**

```
select YEAR(e.hiredate),COUNT(e.empno) 
from emp e
group by YEAR(e.hiredate);
```

**(8). 查询出各年份各月份员工入职人数**

```
select YEAR(emp.hiredate),MONTH(emp.hiredate),COUNT(emp.empno) 
from emp  
GROUP BY YEAR(emp.hiredate),MONTH(emp.hiredate);
```

**(9). 查询出在 ACCOUNTING 部门的员工编号，姓名**

```
select e.empno,e.ename 
from emp e right join  dept d 
on e.deptno=d.deptno 
where d.dname='ACCOUNTING';
```

**(10). 查询在北京工作的员工的平均薪资**

~~~
select d.deptno,d.dname,d.loc,IFNULL(AVG(e.salary),0)
from emp e left outer join dept d on e.deptno=d.deptno
where d.loc='beijing'
~~~

**(11). 查询出谌燕老师带的课程的学生有哪些**

```
select t.tname,c.cname,stu.sname
from teacher t join course c on t.tno = c.tno
               join score s on c.cno = s.cno
               join student stu on stu.sno = s.sno
where t.tname ='谌燕'
```





#### MySQL SQL:子查询

**1.定义:查询中嵌套查询就是子查询**

```
注意:子查询必须用()括起来
```

**2.子查询的本质:**

```
a. 内联视图	
b. 把子查询的结果作为外部查询的条件
```

分析：找出工资大于Mark的员工名字和工资
查询出Mark的工资是多少?

```
 select salary 
 from emp e 
 where e.ename='Mark';
```

查询出高于1450工资的人

```
select e.ename,e.salary 
from emp e 
where e.salary>1450;
```

整合成子查询

```
select e.ename,e.salary 
from emp e
where e.salary>(
	select e1.salary 
    from emp e1  
	where e1.ename='Mark'
); 
```

**3.子查询的特点:不建议使用**

> 子查询很灵活,可以解决很多其他查询方式不能解决的问题
>
> 子查询效率很低,其中相关子查询效率最低
>
> 子查询嵌套的层数越多,则效率越低

**4.为什么相关子查询的效率极其低下?**

> 内查询用到了外查询的列,每次查询行记录时都会迭代表格中
>
> 每一行的行记录,而这种迭代中产生的值都是动态生成的

**5.性能排序/优先使用**

**关联查询/分组查询>无关子查询>相关子查询**

**6.MySQL分页**

```
3050 个产品
页面 ，每页显示20条数据
多少页？ 3050/20 
显示第1页数据： 1-20
显示第2页数据：21-40
显示第n页数据： 20 * (n-1) + 1 -  20 * n
根据员工薪资从高到低，显示第5页员工信息
select * from emp 
order by salary desc
limit 81 ,20
```

**7.oracle分页**

```
第3页：11 - 15
select * from (
select rownum r, t.* from (
select   empno,ename,sal 
from emp  
order by sal desc)t
) tm
where tm.r >=11 and tm.r <=15
```

**8.练习**

找出工资比'BLAKE'多的员工

```
select *
from emp 
where salary > (
      select salary 
      from emp 
      where ename ='BLAKE'
);
```

列出薪资高于公司平均薪资的所有员工，所在部门 

```
select ename,deptno
from emp 
where salary > (
      select avg(salary) 
      from emp
);
```

查询出工资最低的员工的姓名，职位，工资

```
select ename,job,salary
from emp 
where salary = (
      select min(salary) 
      from emp
);
```

列出薪资高于在部门30工作的所有员工的薪资的员工姓名和薪资、部门名称

```
select e.ename, e.salary, d.dname
from emp e join dept d on e.deptno = d.deptno
where d.deptno !=30 and  e.salary > (
                         select max(salary) 
                         from emp 
                         where deptno = 30
);

select e.ename, e.salary, d.dname
from emp e join dept d on e.deptno = d.deptno
where    d.deptno !=30 and  e.salary > ALL(select salary from emp where deptno = 30);
```

查找出职位和'MARTIN' 或者'SMITH'一样的员工的平均工资

```
select avg(salary)
from emp 
where job in (
	select job 
	from emp 
	where ename in('MARTIN','SMITH')
);
```

列出薪资比“BLAKE”或“WARD”多的所有员工的编号、姓名、部门名称、其领导姓名.

```
select   e.empno 员工的编号,e.ename 员工姓名,d.dname 部门名称,m.ename 领导姓名
from emp e join dept d on e.deptno = d.deptno 
      left join emp m on e.mgr = m.empno
where e.salary > any ( 
                       select salary 
                       from emp 
                       where ename in ('BLAKE','WARD')  
);

select  * 
from emp 
where salary  > (
                 select min( salary)  
                 from emp 
                 where ename in ('BLAKE',WARD)  
);
```

找出各个部门中大于他所在部门平均工资的员工名和工资

找出职称相同的员工

查找出收入（工资加上奖金），下级比自己上级还高的员工编号，员工名字，员工收入

```
select e.empno,e.ename,e.salary+ifnull(e.comm,0)
from emp e join emp m on e.mgr = m.empno 
where ( e.salary + ifnull(e.comm,0) ) > ( m.salary  + ifnull(m.comm,0));
```

得到每个月工资总数最少的那个部门的部门编号，部门名称，部门位置

```
select * 
from (select d.deptno dno, d.dname dname ,d.loc  loc , sum(salary)  s
from emp e join dept d
on e.deptno = d.deptno 
group by d.deptno) temp  
having  s = min(s);
 
 select * 
from (select d.deptno dno, d.dname dname ,d.loc  loc , sum(salary)  s
from emp e join dept d
on e.deptno = d.deptno 
group by d.deptno) temp 
order by s 
limit 0,1;   -----------limit startNo, length 
```

查找出部门10和部门20中，工资最高第3名到工资第5名的员工的员工名字，部门名字，部门位置

```
select  e.ename,d.dname,d.loc
from  emp  join dept d on e.deptno = d.deptno 
where e.deptno in(10,20)
order by salary
limit 2,3;
```

以职位分组，找出平均工资最高的两种职位

```
select job,avg(salary)
from emp 
group by job 
order by avg(salary) desc
limit 0,2
```

查询出各部门总薪资,平均薪资，总人数，显示部门编号，部门名称与部门总薪资（没有员工的部门也需要统计）

```
select sum(salary),avg(salary),count(empno),d.deptno,dname
from emp e   right  join dept d
on e.deptno = d.deptno 
group by d.deptno;
```





#### MySQL SQL:limit查询

#Limit子句
Limit子句可以被用于强制 SELECT 语句返回指定的记录数。Limit接受一个或两个数字参数。

参数必须是一个整数常量。如果给定两个参数，第一个参数指定第一个返回记录行的偏移量，

第二个参数指定返回记录行的最大数目。

`//初始记录行的偏移量是 0(而不是 1):`

**mysql> SELECT * FROM table LIMIT 5,10; //检索记录行6-15**

`//为了检索从某一个偏移量到记录集的结束所有的记录行，可以指定第二个参数为 -1:`

**mysql> SELECT * FROM table LIMIT 95,-1; // 检索记录行 96-last**,并非每个版本都能实现

`//如果只给定一个参数，它表示返回最大的记录行数目。换句话说，LIMIT n 等价于 LIMIT 0,n`

**mysql> SELECT * FROM table LIMIT 5; //检索前 5 个记录行**

##Limit的效率高？
常说的Limit的执行效率高，是对于一种特定条件下来说的：即数据库的数量很大，但是只需要查询一部分数据的情况。

高效率的原理是：`避免全表扫描，提高查询效率`。

比如：每个用户的email是唯一的，如果用户使用email作为用户名登陆的话，就需要查询出email对应的一条记录。

SELECT * FROM t_user WHERE email=?;

上面的语句实现了查询email对应的一条用户信息，但是由于email这一列没有加索引，会导致全表扫描，效率会很低。

SELECT * FROM t_user WHERE email=? LIMIT 1;

加上LIMIT 1，`只要找到了对应的一条记录，就不会继续向下扫描了`，效率会大大提高。

##Limit的效率低？
在一种情况下，使用limit效率低，那就是：只使用limit来查询语句，并且偏移量特别大的情况

做以下实验：

~~~
语句1: select * from table limit 150000,1000;

语句2: select * from table while id>=150000 limit 1000;
~~~

语句1为0.2077秒；语句2为0.0063秒

两条语句的时间比是：语句1/语句2＝32.968

比较以上的数据时，我们可以发现采用where...limit....性能基本稳定，受偏移量和行数的影响不大，而单纯采用limit的话，受偏移量的影响很大，当偏移量大到一定后性能开始大幅下降。不过在数据量不大的情况下，两者的区别不大。

**所以应当先使用where等查询语句，配合limit使用，效率才高**

ps：在sql语句中，limt关键字是最后才用到的。以下条件的出现顺序一般是：where->group by->having-order by->limit

##练习
--找出在Asia工作的员工的第2行到第4行记录

##分页应用
通过limit和offset 或只通过limit可以实现分页功能。

假设 pageSize表示每页要显示的条数，pageCode表示页码，那么返回第pageCode页，每页条数为pageSize的sql语句：

代码示例:

语句3：select * from student limit (pageCode-1)*pageSize,pageSize;

语句4：select * from student limit pageSize offset (pageCode-1)*pageSize;





#### MySQL DML

DML: Data Manipulating Language（**数据操作语言**:insert,update,delete）

注意: DML操作都需要注意约束控制

**1.insert语句**

```sql
insert into 表名 (列,列,列...) values(值,值,值...);

-- 当插入的数据时与表格列一一对应的话,则列可以省略
insert into 表名 values(值,值,值...);
```

```sql
-- 先创建一张表
create table tbl_student(
    id int(7),
    name varchar(20) not null,
    birthday timestamp default now(),
    constraint tbl_student_id_pk primary key(id)
);

-- 插入所有数据
insert into tbl_student values(1,'tom','2012-09-08 14:55:58');
-- 插入部分数据
insert into tbl_student(id,name) values(2,'success');
```

```sql
-- 创建自增字段auto_increment 
create table tbl_student(
    id int(7) auto_increment,
    name varchar(20) not null,
    birthday timestamp default now(),
    constraint tbl_student_id_pk primary key(id)
);

-- 也是可以设置自增字段的最小值
alter table table_student auto_increment=4

-- 获取auto_increment值
-- 可以通过mysql中的last_insert_id()函数来实现
```

**2.update语句**

~~~sql
-- 语法
update 表名 set 列名=新值 where 条件;

-- eg:提高指定员工的工资10%
update emp set salary=salary*1.1 where empno=1;

-- 注意:更新操作where条件如果不写,则更新整张表格的数据!!!
~~~

**3.delete语句**

~~~sql
-- 语法
delete from 表名 where 条件;

-- eg:删除工资低于1200的员工信息
delete from emp where salary<1200;
~~~





#### MySQL 约束

**1.约束定义：**

> 约束是一种限制，它通过对表的行或列的数据做出限制，来确保表的数据的完整性、唯一性 

**1.约束类型:**

| 约束类型： | 主键        | 外键        | 唯一   | 非空     | 自增           | 默认值  |
| ---------- | ----------- | ----------- | ------ | -------- | -------------- | ------- |
| 关键字：   | primary key | foreign key | unique | not null | auto_increment | default |

**主键约束: primary key** 

> 主键约束相当于唯一约束 + 非空约束的组合，主键约束列不允许重复，也不允许出现空值;
>
> 每个表最多只允许一个主键，建立主键约束可以在列级别创建，也可以在表级别创建;
>
> 当创建主键的约束时，系统默认会在所在的列和列组合上建立对应的唯一索引;

```mysql
create table sporter(
    sporter_id Integer primary key, -- 列级别
	sporter_name varchar(20) not null,
	sporter_gender enum('男','女'),
	sporter_department varchar(20) not null,
	constraint sporter_id_pk primary key(sporter_id)-- 表级别	
)
```

**外键约束: foreign key**

> 外键约束是保证一个或两个表之间的参照完整性;
>
> 外键是构建于一个表的两个字段或是两个表的两个字段之间的参照关系;

**唯一约束: unique**

> 唯一约束是指定table的列或列组合不能重复，保证数据的唯一性;
>
> 唯一约束不允许出现重复的值，但是可以为多个null;
>
> 同一个表可以有多个唯一约束，多个列组合的约束;
>
> 在创建唯一约束时，如果不给唯一约束名称，就默认和列名相同;
>
> 唯一约束不仅可以在一个表内创建，而且可以同时多表创建组合唯一约束;

**非空约束not null与默认值default**

> 非空约束用于确保当前列的值不为空值，非空约束只能出现在表对象的列上;
>
> Null类型特征：所有的类型的值都可以是null，包括int、float 等数据类型;

```mysql
create table sporter(
  sporter_id Integer auto_increment,
	sporter_name varchar(20) not null,
	sporter_gender enum('男','女'),
	sporter_department varchar(20) not null,
	constraint sporter_id_pk primary key(sporter_id)	
)

create table item(
  item_id Integer auto_increment,
	item_name varchar(40),
	item_location varchar(40),
	constraint item_id_pk primary key(item_id)
)

create table grade(
  sporter_id Integer,
	item_id Integer, 
	grade_mark Integer,
	constraint sporter_fk foreign key(sporter_id) references sporter(sporter_id),
	constraint item_fk foreign key(item_id) references item(item_id)
)
```





#### MySQL 事务***

**1.事务(Transaction)的定义:**

> 指一组相关的SQL操作,我们所有的操作都是处于事务中的;

**2.DTL（数据事务语言）：**

```sql
-- eg:
--    一个转账操作，有多条sql 组成
--    要么全部都执行成功，要么全部都不执行
begin transaction  -- 开始事务
(1)  update account set banlance = balance -100 where accountId = 1001;
(2)  update account set banlance = balance +100 where accountId = 1002;
(3)sql...
(4)sql
(5)sql 
commit; --提交

if exception rollback ---回滚 （到上一次提交的时候）
-- 先设置mysql中执行sql语句 关闭自动提交set autocommit = 0;
```

**3.注意:**

> 在数据库中,执行业务的基本单位是事务,不是以某一条SQL；
>
> 数据库在默认情况下,事务都是打开的,也就是说它是一直处在事务中的,一个事务的结束,代表着下一个事务的开启；
>
> 执行commit或者rollback指令时,会结束当前事务；
>

**4.作用:**

>   用来保证数据的平稳性和可预测性.
>

**5.事务的四大特性(ACID):重要**

> **atomic**原子性：
>
> 事务是不可再分割的,要么同时成功,要么同时失败
>
> **consistency**一致性：
>
> 事务一旦结束,内存中的数据和数据库中的数据是保持一致的;
>
> 几个并行执行的事务，其执行结果必须与按某一顺序串行执行的结果相一致;
>
> 事务的一致性指的是在一个事务执行之前和执行之后数据库都必须处于一致性状态；
>
> 假如数据库的状态满足所有的完整性约束，就说该数据库是一致的;
>
> **isolation**隔离性,：
>
> 事务之间互不干扰,一个事务的结束意味着下一个事务的开启；
>
> **duration**持久性：
>
> 事务一旦提交,则数据持久化到数据库中,永久保存；

**6.事务控制语句**

(1).BEGIN或START TRANSACTION；显式地开启一个事务；

(2).COMMIT；也可以使用COMMIT WORK，不过二者是等价的。COMMIT会提交事务，并使已对数据库进行的所有修改成为永久性的；

(3).ROLLBACK；有可以使用ROLLBACK WORK，不过二者是等价的。回滚会结束用户的事务，并撤销正在进行的所有未提交的修改；

(4).SAVEPOINT identifier；SAVEPOINT允许在事务中创建一个保存点，一个事务中可以有多个SAVEPOINT；

(5).RELEASE SAVEPOINT identifier；删除一个事务的保存点，当没有指定的保存点时，执行该语句会抛出一个异常；

(6).ROLLBACK TO identifier；把事务回滚到标记点；

(7).SET TRANSACTION；用来设置事务的隔离级别。InnoDB存储引擎提供事务的隔离级别有READ UNCOMMITTED、READ COMMITTED、REPEATABLE READ和SERIALIZABLE。

**7.MYSQL 事务处理主要有两种方法**

(1).用 BEGIN, ROLLBACK, COMMIT来实现<br>
1-1. BEGIN 开始一个事务<br>
1-2. ROLLBACK 事务回滚<br>
1-3. COMMIT 事务确认<br>

(2).直接用 SET 来改变 MySQL 的自动提交模式: <br>
2-1. SET AUTOCOMMIT=0 禁止自动提交<br>
2-2. SET AUTOCOMMIT=1 开启自动提交

**8.多事务的并发处理机制**
原因:多个事务同时操作一个表中的同一行数据,如果这些操作是.修改操作的话,就会产生并发问题,如果不处理,则会造成数据不一致的情况.

数据库可能产生的并发问题包括:

(1).`脏读`

是指一个事务正在访问数据,并且对这个数据进行修改,而这种修改<br>
还没有提交到数据库中,而另一个事务也访问了这个数据,并且使用了这个数据.<br>
解决方法:一个事务在修改数据时,该数据不能被其他事务访问

(2).`不可重复读`

是指一个事务多次读取同一条记录,如果此时另一个事务也访问并且<br>
修改了该数据,则就会出现多次读取出现数据不一致的情况,原来的<br>
数据变成了不可重复读取的数据<br>
解决方法:只有在修改事务完全提交过后才可以读取到数据

(3).`幻读`

是指一个事务修改表中的多行记录,但是此时另一个事务对该表格进行<br>
了插入数据的操作,则第一个事务会发现表格中会出现没有被修改的行,<br>
就像发生了幻觉一样.<br>
解决方法:在一个事务提交数据之前,其他事务不能添加数据

**不可重复读的重点是修改，同样的条件，你读取过的数据，再次读取出来发现值不一样了幻读的重点在于新增或者删除**

**9.事务隔离级别**

> 1. READ_UNCOMMITTED
>
> > 这是事务最低的隔离级别，它充许另外一个事务可以看到这个事务未提交的数据。
> > 解决第一类丢失更新的问题，但是会出现脏读、不可重复读.

> 1. READ_COMMITTED
>
> > 保证一个事务修改的数据提交后才能被另外一个事务读取，即另外一个事务不能读取该事务未提交的数据。
> > 解决第一类丢失更新和脏读的问题，但会出现不可重复读.

> 1. REPEATABLE_READ
>
> > 保证一个事务相同条件下前后两次获取的数据是一致的
> > 解决第一类丢失更新，脏读、不可重复读.

> 1. SERIALIZABLE
>
> > 事务被处理为顺序执行。解决所有问题

**提醒：**
**Mysql默认的事务隔离级别为repeatable_read**

**10.InnoDB引擎的锁机制**

**之所以以InnoDB为主介绍锁，是因为InnoDB支持事务，支持行锁和表锁用的比较多，Myisam不支持事务，只支持表锁**

1. 共享锁（S）：允许一个事务去读一行，阻止其他事务获得相同数据集的排他锁。<br>
   共享锁就是我读的时候，你可以读，但是不能写
2. 排他锁（X)：允许获得排他锁的事务更新数据，阻止其他事务取得相同数据集的共享读锁和排他写锁。<br>
   排他锁就是我写的时候，你不能读也不能写
3. 意向共享锁（IS）：事务打算给数据行加行共享锁，事务在给一个数据行加共享锁前必须先取得该表的IS锁。
4. 意向排他锁（IX）：事务打算给数据行加行排他锁，事务在给一个数据行加排他锁前必须先取得该表的IX锁。

**说明:**

1. 共享锁和排他锁都是行锁，意向锁都是表锁，应用中我们只会使用到共享锁和排他锁，意向锁是mysql内部使用的，不需要用户干预。
2. 对于UPDATE、DELETE和INSERT语句，InnoDB会自动给涉及数据集加排他锁（X)；对于普通SELECT语句，InnoDB不会加任何锁，事务可以通过以下语句显示给记录集加共享锁或排他锁。<br>
   共享锁(S)：SELECT * FROM table_name WHERE ... LOCK IN SHARE MODE。<br>
   排他锁(X)：SELECT * FROM table_name WHERE ... FOR UPDATE。<br>
3. InnoDB行锁是通过给索引上的索引项加锁来实现的，因此InnoDB这种行锁实现特点意味着：只有通过索引条件检索数据，InnoDB才使用行级锁，否则，InnoDB将使用表锁！





#### MySQL 视图

**1.视图的定义:**
视图是指计算机数据库中的视图，是一个虚拟表，其内容由查询定义;同真实的表一样，视图包含一系列带有名称的列和行数据;但是，视图并不在数据库中以存储的数据值集形式存在;行和列数据来自由定义视图的查询所引用的表，并且在引用视图时动态生成。

**2.为啥需要使用视图?**
关系型数据库中的数据是由一张一张的二维关系表所组成，简单的单表查询只需要遍历一个表，而复杂的多表查询需要将多个表连接起来进行查询任务;对于复杂的查询事件，每次查询都需要编写MySQL代码效率低下;为了解决这个问题，数据库提供了视图（view）功能。

**3.创建视图**

```sql
CREATE VIEW 视图名(列1，列2...)
AS SELECT (列1，列2...)
FROM ...;
```

使用视图和使用表完全一样，只需要把视图当成一张表就OK了,视图是一张虚拟表;

**4.删除视图**

~~~sql
drop view 视图名;
~~~

**5.视图与表数据变更**

表格数据变化后，在通过视图检索，得到的结果也同步发生了变化;

可以通过视图插入数据，但是只能基于一个基础表进行插入，不能跨表更新数据;

**6.WITH CHECK OPTION** 
如果在创建视图的时候制定了“WITH CHECK OPTION”，那么更新数据时不能插入或更新不符合视图限制条件的记录。





#### MySQL 存储过程

**1.存储过程:**
	概念类似于函数,就是把一段代码封装起来;----SQL语句需要先编译然后执行, 存储过程（Stored Procedure）是一组为了完成特定功能的SQL语句集，经编译后存储在数据库中，用户通过指定存储过程的名字并给定参数（如果该存储过程带有参数）来调用执行它。

```sql
-- 当要执行者一段代码的时候,可以通过调用该存储过程来实现.

-- 在封装的语句体里面,可以用if/else,case,while等控制结构.

-- 可以进行SQL编程.

-- 函数的普遍特性：模块化，封装，代码复用；

-- 速度快，只有首次执行需经过编译和优化步骤，后续被调用可以直接执行，省去以上步骤；
```

**2.存储过程弊端:**

不同数据库，语法差别很大，移植困难，换了数据库，需要重新编写；

不好管理，把过多业务逻辑写在存储过程不好维护，不利于分层管理，容易混乱，一般存储过程适用于个别对性能要求较高的业务，其它的必要性不是很大；



**3.语法**

(1).查看存在的存储过程

```mysql
mysql>show procedure status;
```

(2).删除存储过程

```mysql
mysql>drop procedure 存储过程的名字
```

(3).存储过程的创建

```mysql
delimiter $$
create procedure 存储过程名(参数列表)
begin
     SQL语句代码块
enddelimiter $$

-- delimiter就是告诉mysql解释器，该段命令是否已经结束了，是否可以执行了。默认情况下，delimiter是分号;，遇到分号就执行。后面的双美元符号 就是告诉mysql，遇到双美元符号再执行
```

(4).调用存储过程

```sql
call 存储过程名()
```

(5).实例

> 第一个存储过程,体会"封装sql"

```sql
delimiter $$
create procedure p1()
begin
    select * from s_emp;
end $$
```

> 调用存储过程

```sql
call p1() 
```

> 第二个存储过程,体会"参数"

```sql
delimiter $$
create procedure p2(n int)
begin
    select * from s_emp where id>n;
end $$
```

> 第三个存储过程,体会"控制结构"

```sql
delimiter $$
create procedure p3(n int,j char(1))
begin
    if j = 'h' then
	select * from s_emp where id>n;
    else
	select * from s_emp where id<n;
    end if;
end $$
```

> 计算1->n的和

~~~sql
delimiter $$
create procedure p4(n smallint)
begin
    declare i int;
    declare s int;
    set i = 1;
    set s = 0;
    while i<=n do
	set s = s + i;
	set  i= i + 1;
    end while;
    select s;
end $$
~~~





#### MySQL 索引***

**1.索引的定义**
比如我们要在字典中找某一字，如何才能快速找到呢？那就是通过字典的目录;

对数据库来说，索引的作用就是给‘数据’加目录,创建所以的目的就是为了提高查询速度,降低数据库的IO成本 ;

**2.索引算法**

(1).btree(二叉树)索引  log<sub>2</sub>N

(2).hash(哈希)索引   1

**3.优缺点**

(1).好处:提高查询速度(select )

(2).坏处:降低了增,删,改的速度(update/delete/insert),提高了表的文件大小(索引文件甚至可能比数据文件还大)

**4.索引类型**

(1).普通索引(index)：仅仅是加快了查询速度

(2).唯一索引(unique)：行上的值不能重复

(3).主键索引(primary key)：不能重复

(4).全文索引(fulltext):仅可用于 MyISAM 表，针对较大的数据，生成全文索引很耗时好空间。

(5).组合索引：为了更多的提高mysql效率可建立组合索引，遵循”最左前缀“原则。

**5.索引语法**

(1).查看某张表上的所有索引

~~~sql
show index from tableName 
~~~

(2).建立索引

~~~sql
-- 索引名可不写,不写默认使用列名
alter table 表名 add index/unique/fulltext 索引名 (列名) ; 

-- 不要加索引名，因为主键只有一个
alter table 表名 add primary key(列名)
~~~

(3).删除非主键索引

~~~sql
alter table 表名 drop index 索引名；
~~~

(4).删除主键索引：

~~~sql
alter table 表名 drop primary key;
~~~

(5).全文索引与停止词

全文索引的用法：match(全文索引名) against('keyword');

**6.关于全文索引**
关于全文索引的停止词：

全文索引不针对非常频繁的词做索引

如：this,is,you,my等等

全文索引在mysql的默认情况下，对于中文意义不大。

因为英文有空格，标点符号来拆成单词，进而对单词进行索引；

而对于中文，没有空格来隔开单词，mysql无法识别每个中文词。

可以使用sphinx插件来进行全文索引的中文索引。

**7.组合索引之复合索引**

```sql
CREATE TABLE test (

 id INT NOT NULL,

 last_name CHAR(30) NOT NULL,
 
 first_name CHAR(30) NOT NULL,
 
 PRIMARY KEY (id),
 
 INDEX name (last_name,first_name)
```

 );

 name索引是一个对last_name和first_name的索引。索引可以用于为last_name，或者为last_name和first_name在已知范围内指定值的查询。因此，name索引用于下面的查询：

 SELECT * FROM test WHERE last_name='Widenius';

 SELECT * FROM test WHERE last_name='Widenius' AND first_name='Michael';

 但是不能用于SELECT * FROM test WHERE first_name='Michael';这是因为MySQL组合索引为“最左前缀”的结果,简单的理解就是只从最左面的开始组合。

**8.建立索引的策略**

(1).主键列和唯一性列					√

(2).不经常发生改变的列					√

(3).满足以上2个条件,经常作为查询条件的列	√

(4).重复值太多的列						×

(5).null值太多的列						×





#### MySQL  自定义函数

**1.自定义函数**

```mysql
delimiter -- 自定义符号 如果函数体只有一条语句, begin和end可以省略, 同时delimiter也可以省略
create function 函数名(形参列表) returns 返回类型 -- 注意是returns
begin
　　-- 函数体 函数内定义的变量如：set @x = 1; 变量x为全局变量，在函数外面也可以使用
　  -- 返回值
end -- 自定义符号
delimiter ;

-- 实例
-- 自定义函数
delimiter $$
create function myfun3(ia int, ib int) returns int
begin
    return ia + ib;
end
$$
delimiter ;
```

**2.查看函数**

~~~sql
-- 查看所有自定义函数, 自定义函数只能在本数据库使用
show function status [like 'pattern'];   
-- 查看函数创建语句
show create function 函数名; 
~~~

**3.删除函数**

~~~sql
drop function 函数名;
~~~

**4.综合应用**

> 使用全局变量

```sql
-- 计算1 ~ 指定数据 之间的和
delimiter $$
create function my_sum(x int) returns int
begin
    set @i = 1;
    set @sum = 0;
    while @i <= x do
        set @sum = @sum + @i;
        set @i = @i + 1;
    end while;
    return @sum;
end
$$
delimiter ;
```

> 使用局部变量

~~~sql
-- 求1 ~ 指定数之前的和，但5的倍数不加
delimiter $$
create function my_sum2(x int) returns int
begin
    declare i int default 1;
    declare sum int default 0;
    sumwhile:while i <= x do
        if i % 5 = 0 then
            set i = i + 1;
            iterate sumwhile;
        end if;
        set sum = sum + i;
        set i = i + 1;
    end while;
    return sum;
end
$$
delimiter ;
~~~





#### MySQL 三大范式

**范式Normal Form**
在设计表 的时候，需要遵循---范式Normal Form
第一范式（1NF）：该列分割到不可再分割的列,无重复列,具有原子性;
第二范式（2NF）：先满足第一范式，确保表中的每列都和主键相关,属性完全依赖于主键;
第三范式（3NF）：先满足第一范式和第二范式，确保表中的每列直接依赖于主键列，而不是间接依赖关系不能存在传递依赖, 除了主键外，其他字段必须依赖主键 ;



第一范式（1NF）： 列具有原子性
订单表 ：
![](https://i.imgur.com/Y0FOdLy.jpg)  

> 存在的问题： 商品原产地与主键（订单编号）不相关  



第二范式： 确保表中的每列都和主键相关

解决：

 ![](https://i.imgur.com/ulANJdf.jpg)



4.第三范式
	 
![](https://i.imgur.com/xAzDAQS.jpg)  
	存在的问题： 用户姓名不与该表的主键 （订单编号）直接相关，而是与用户编号相关

解决：

 ![](https://i.imgur.com/yGZQvlv.jpg)

 







 





