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
