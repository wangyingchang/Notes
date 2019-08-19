##### Linux(centos 7) 安装 Mysql5.7

注意：命令权限不足时，使用sudo命令

安装从网上下载文件的wget命令

~~~linux
yum -y install wget
~~~

下载mysql的repo源

~~~
wget http://repo.mysql.com/mysql-community-release-el7-5.noarch.rpm 
~~~

安装mysql-community-release-el7-5.noarch.rpm包

~~~
rpm -ivh mysql-community-release-el7-5.noarch.rpm
~~~

查看下是否存在下面两个文件

~~~
ls -1 /etc/yum.repos.d/mysql-community*
~~~

/etc/yum.repos.d/mysql-community.repo
/etc/yum.repos.d/mysql-community-source.repo

安装mysql-server

~~~
yum install mysql-server
~~~

启动服务

~~~
service mysqld start
~~~

查看初始密码（两种方式）：MySQL5.6默认密码为空，MySQL5.7会自动生成初始密码

~~~
grep 'temporary password' /var/log/mysqld.log 
~~~

~~~
cat /root/.mysql_secret
~~~

修改密码

~~~
ALTER USER 'root'@'localhost' IDENTIFIED WITH mysql_native_password BY '123';
~~~

