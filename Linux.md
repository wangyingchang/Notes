##### Linux 常用命令

查看端口

~~~
netstat -ntlp
~~~

查看nginx 进程

~~~
ps -ef | grep nginx
-- ps为linux查看进程命令， grep为过滤命令，该条命令是输出运行nginx进程详细信息，第二列为进程号
~~~

杀死进程

~~~
kill -9 XX 
-- kill为linux杀进程命令, XX为上一个命令的输出第二列的数字
~~~

打包命令

~~~
tar cvf apps.tar apps
~~~

传输文件

~~~
scp -P59878 apps.tar mwdgz@193.112.169.142:/home/mwdgz/project
~~~

查看文件信息：

~~~
ls
~~~

清屏：clear作用为清除终端上的显示(类似于DOS的cls清屏功能)，也可使用快捷键：Ctrl + l ( "l" 为字母 )。

~~~
clear
~~~

切换工作目录：

Linux所有的目录和文件名大小写敏感cd后面可跟绝对路径，也可以跟相对路径。如果省略目录，则默认切换到当前用户的主目录。

~~~
cd
~~~

显示当前路径：

~~~
pwd
~~~

创建目录：

通过mkdir命令可以创建一个新的目录。参数-p可递归创建目录。需要注意的是新建目录的名称不能与当前目录中已有的目录或文件同名，并且目录创建者必须对当前目录具有写权限。

~~~
mkdir
~~~

删除文件：

可通过rm删除文件或目录。使用rm命令要小心，因为文件删除后不能恢复。为了防止文件误删，可以在rm后使用-i参数以逐个确认要删除的文件。

~~~
rm -rf 
~~~

拷贝：

cp命令的功能是将给出的文件或目录复制到另一个文件或目录中，相当于DOS下的copy命令。

~~~
cp
~~~

移动、重命名:

用户可以使用mv命令来移动文件或目录，也可以给文件或目录重命名。

~~~
mv
~~~

创建文件: 

说明：则会在当前路径下创建名字为hello.txt的空文件,Linux系统中没有严格的后缀（格式），所以创建文件时可以命名为任意的文件名

```
touch hello.txt
```

查看或者合并文件内容：

~~~
cat
~~~

文本搜索：

Linux系统中grep命令是一种强大的文本搜索工具，grep允许对文本文件进行模式查找。如果找到匹配模式， grep打印包含模式的所有行。

```
grep [-选项] '搜索内容串'文件名
```

 查找文件：

~~~
find
~~~

归档管理：

~~~
tar使用格式 tar [参数] 打包文件名 文件
~~~

![电脑网络：网络工程师史上最全cmd命令，含Windows和Linux系统](http://p3.pstatp.com/large/pgc-image/a808e4710f194101aaa97ab387c81ee8)

注意：除了f需要放在参数的最后，其它参数的顺序任意。



18. 文件压缩解压：gzip

tar与gzip命令结合使用实现文件打包、压缩。 tar只负责打包文件，但不压缩，用gzip压缩tar打包后的文件，其扩展名一般用xxxx.tar.gz。

gzip使用格式如下：

```
gzip [选项] 被压缩文件
```

常用选项：

![电脑网络：网络工程师史上最全cmd命令，含Windows和Linux系统](http://p3.pstatp.com/large/pgc-image/d05d81b76bdf44baae903adfad820d4d)



tar这个命令并没有压缩的功能，它只是一个打包的命令，但是在tar命令中增加一个选项(-z)可以调用gzip实现了一个压缩的功能，实行一个先打包后压缩的过程。

压缩用法：tar cvzf 压缩包包名 文件1 文件2 …

```
-z ：指定压缩包的格式为：file.tar.gz
```

解压用法： tar zxvf 压缩包包名

```
-z:指定压缩包的格式为：file.tar.gz
```

解压到指定目录：-C （大写字母"C"）

**19. 文件压缩解压：bzip2**

tar与bzip2命令结合使用实现文件打包、压缩(用法和gzip一样)。

tar只负责打包文件，但不压缩，用bzip2压缩tar打包后的文件，其扩展名一般用xxxx.tar.gz2。

在tar命令中增加一个选项(-j)可以调用bzip2实现了一个压缩的功能，实行一个先打包后压缩的过程。

压缩用法：tar -jcvf 压缩包包名 文件…(tar jcvf bk.tar.bz2 *.c)

解压用法：tar -jxvf 压缩包包名 (tar jxvf bk.tar.bz2)

**20. 文件压缩解压：zip、unzip**

通过zip压缩文件的目标文件不需要指定扩展名，默认扩展名为zip。

压缩文件：zip [-r] 目标文件(没有扩展名) 源文件

解压文件：unzip -d 解压后目录文件 压缩文件

**21. 查看命令位置：which**

**22. 修改文件权限：chmod**

chmod 修改文件权限有两种使用格式：字母法与数字法。

字母法：chmod u/g/o/a +/-/= rwx 文件

![电脑网络：网络工程师史上最全cmd命令，含Windows和Linux系统](http://p3.pstatp.com/large/pgc-image/b869929f94304864b3c1a4324f948a30)



![电脑网络：网络工程师史上最全cmd命令，含Windows和Linux系统](http://p3.pstatp.com/large/pgc-image/4e974b6b202a43ad90ab9aa21ee86a1f)



![电脑网络：网络工程师史上最全cmd命令，含Windows和Linux系统](http://p9.pstatp.com/large/pgc-image/0d7ff99ba4894fe69516d49421d0e8fe)



如果需要同时进行设定拥有者、同组者以及其他人的权限，参考如下：

![电脑网络：网络工程师史上最全cmd命令，含Windows和Linux系统](http://p1.pstatp.com/large/pgc-image/a41f6538009b4da7be38957d49b43ece)



![电脑网络：网络工程师史上最全cmd命令，含Windows和Linux系统](http://p1.pstatp.com/large/pgc-image/fc9c4e7fe44440f9aa51e481adba8cee)



数字法："rwx" 这些权限也可以用数字来代替

![电脑网络：网络工程师史上最全cmd命令，含Windows和Linux系统](http://p9.pstatp.com/large/pgc-image/9d2e49c085944a58882d49e76c260d4a)



如执行：chmod u=rwx,g=rx,o=r filename 就等同于：chmod u=7,g=5,o=4 filename

chmod 751 file：

文件所有者：读、写、执行权限

同组用户：读、执行的权限

其它用户：执行的权限

注意：如果想递归所有目录加上相同权限，需要加上参数" -R "。 如：chmod 777 test/ -R 递归 test 目录下所有文件加 777 权限

**23. 切换到管理员账号**

Ubuntu下切换到root的简单命令:

**24. 设置用户密码：passwd**

在Unix/Linux中，超级用户可以使用passwd命令为普通用户设置或修改用户密码。用户也可以直接使用该命令来修改自己的密码，而无需在命令后面使用用户名。

**25. 退出登录账户： exit**

如果是图形界面，退出当前终端；

如果是使用ssh远程登录，退出登陆账户；

如果是切换后的登陆用户，退出则返回上一个登陆账号。

**26. 查看登录用户：who**

who命令用于查看当前所有登录系统的用户信息。

常用选项：

![电脑网络：网络工程师史上最全cmd命令，含Windows和Linux系统](http://p3.pstatp.com/large/pgc-image/bc7d74450a574b6b926dffd2f72da6ee)



**27. 关机重启：reboot、shutdown、init**

![电脑网络：网络工程师史上最全cmd命令，含Windows和Linux系统](http://p3.pstatp.com/large/pgc-image/dc792e3a5d1c4b379efb0139ff5c7cdb)





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

