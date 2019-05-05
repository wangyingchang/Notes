####常用命令

**cmd下连接数据库**
~~~
sqlplus username/password@//host:port/sid 
sqlplus system/123@//localhost:1521/orcl
~~~

**创建用户**
~~~
create user username identified by password;
create user wang identified by 123;
--创建用户、删除用户等权限只有数据库的管理员才有,数据库的管理员一个是system,一个是dba。
~~~

**授权**
~~~
grant connect,resource,dba to username;
grant connect,resource,dba to wang;
--connect 是链接数据库权限，可以对数据库进行增删改查
--resource  资源使用权限，用来创建表格
--dba  是数据库管理员权限
~~~

**修改用户密码**
~~~
alter user wang identified by newpassword;
alter user wang identified by 123;
~~~

**回收权限**
~~~
revoke connect,resource from username;
revoke connect,resource from wang;
~~~

**给用户加锁或者解锁**
~~~
alter user username account lock;--加锁
alter user wang account lock;--加锁

alter user username account unlock;--解锁
alter user wang account unlock;--解锁
~~~

**删除用户**
~~~
--删除用户之前先退出当前用户，使用system系统用户登录
drop user username;
drop user wang;
~~~

**创建表**
~~~
create table test01(
PID varchar(50) not null
);
~~~

**修改表**
~~~
alter table 表名 modify 字段名 default 默认值; //更改字段类型

alter table 表名 add 列名 字段类型; //增加字段类型

alter table 表名 drop column 字段名; //删除字段名

alter table 表名 rename column 列名 to 列名 //修改字段名

rename 表名 to 表名 //修改表名
~~~

**删除表**
~~~
truncate table 表名; //删除表中的所有数据，速度比delete快很多,截断表

delete from table 条件; //

drop table 表名; //删除表数据
~~~

**查看表信息**
~~~
desc test01;
~~~

**复制表**
~~~
create table 表名 as 一个查询结果; //复制查询结果

insert into 表名 值 一个查询结果; //添加时查询
~~~

**创建表空间**
~~~
//永久表空间
create tablespace test1_tablespace datafile ‘testfile.dbf’ size 10m;

//临时表空间
create temporary tablespace temptest1_tablespace tempfile ‘tempfile.dbf’ size 10m;

desc dba_data_files;

select file_name from dba_data_files where tablespace_name=’TEST1_TABLESPACE’;
~~~
