##### Linux 常用命令



清空文件

~~~
echo "" > filename
~~~

查看大小

~~~
du -sh filename
~~~

查看端口

~~~
netstat -ntlp
~~~

查看进程

~~~
ps -ef | grep nginx
# ps为linux查看进程命令， grep为过滤命令，该条命令是输出运行nginx进程详细信息，第二列为进程号
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
l
ls
~~~

清屏(ctrl+l)

~~~
clear
~~~

切换工作目录：Linux所有的目录和文件名大小写敏感cd后面可跟绝对路径，也可以跟相对路径。如果省略目录，则默认切换到当前用户的主目录。

~~~
cd ~/
~~~

显示当前路径：

~~~
pwd
~~~

**创建目录**：通过mkdir命令可以创建一个新的目录。参数-p可递归创建目录。需要注意的是新建目录的名称不能与当前目录中已有的目录或文件同名，并且目录创建者必须对当前目录具有写权限。

~~~
mkdir dirname
~~~

**创建文件**: 则会在当前路径下创建名字为hello.txt的空文件,Linux系统中没有严格的后缀（格式），所以创建文件时可以命名为任意的文件名

```
touch hello.txt
```

**删除文件**: 可通过rm删除文件或目录,使用rm命令要小心，因为文件删除后不能恢复。为了防止文件误删，可以在rm后使用-i参数以逐个确认要删除的文件。

~~~
rm -rf filename
~~~

拷贝：cp命令的功能是将给出的文件或目录复制到另一个文件或目录中，相当于DOS下的copy命令。

~~~
cp
~~~

移动、重命名: 用户可以使用mv命令来移动文件或目录，也可以给文件或目录重命名。

~~~
mv
~~~

查看或者合并文件内容：

~~~
cat
~~~

文本搜索：Linux系统中grep命令是一种强大的文本搜索工具，grep允许对文本文件进行模式查找。如果找到匹配模式， grep打印包含模式的所有行。

```
grep [-选项] '搜索内容串'文件名

在某个目录下的所有的.log中检索 含有 xxx的行，并写入a.txt文件 ，或者追加到a.txt
grep "DiamondCost" *.log > a.txt
grep "DiamondCost" *.log >> a.txt

grep -C 5 foo file 显示file文件中匹配foo字串那行以及上下5行
grep -B 5 foo file 显示foo及前5行
grep -A 5 foo file 显示foo及后5行
```

 查找文件：

~~~
find
~~~

文件打包、开包：

~~~
tar [参数] 打包文件名 文件
~~~

![电脑网络：网络工程师史上最全cmd命令，含Windows和Linux系统](http://p3.pstatp.com/large/pgc-image/a808e4710f194101aaa97ab387c81ee8)

注意：除了f需要放在参数的最后，其它参数的顺序任意。

文件压缩解压：tar与gzip命令结合使用实现文件打包、压缩。 tar只负责打包文件，但不压缩，用gzip压缩tar打包后的文件，其扩展名一般用xxxx.tar.gz。

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

文件压缩解压：bzip2

tar与bzip2命令结合使用实现文件打包、压缩(用法和gzip一样)。

tar只负责打包文件，但不压缩，用bzip2压缩tar打包后的文件，其扩展名一般用xxxx.tar.gz2。

在tar命令中增加一个选项(-j)可以调用bzip2实现了一个压缩的功能，实行一个先打包后压缩的过程。

压缩用法：tar -jcvf 压缩包包名 文件…(tar jcvf bk.tar.bz2 *.c)

解压用法：tar -jxvf 压缩包包名 (tar jxvf bk.tar.bz2)

**文件压缩解压：zip、unzip**

通过zip压缩文件的目标文件不需要指定扩展名，默认扩展名为zip。

压缩文件：zip [-r] 目标文件(没有扩展名) 源文件

解压文件：unzip -d 解压后目录文件 压缩文件

**查看命令位置：which**

**修改文件权限：chmod**

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



##### **Linux mysql 查询结果>excel**

~~~mysql
-- 查看导出路径
mysql> show variables like '%secure%';
+------------------+-----------------------+
| Variable_name    | Value                 |
+------------------+-----------------------+
| secure_auth      | ON                    |
| secure_file_priv | /var/lib/mysql-files/ |
+------------------+-----------------------+
-- 注意：secure_file_priv 为导出路径；secure_file_priv值为null 时，在mysql配置文件/etc/my.cnf中[mysqld]配置段添加如下配置
-- secure_file_priv=''

-- select * into outfile '导出文件存放目录' from 表面和查询条件等信息！
mysql> select * into outfile '/var/lib/mysql-files/2019083016_db1.xls' from Users;
~~~







##### Linux crontab(定时任务)

root用户下：

~~~mysql
# 查看crontab状态
tail -f /var/log/cron

# 编辑定时任务
vim /etc/crontab

#检测crontab是否在test.txt文件中写入数据
*/1 * * * * root echo 111 >> /home/mwdgz/script/test.txt
~~~

非root用户下：

~~~mysql
# 编辑定时任务
crontab -e
# 查看定时任务
crontab -l
~~~



[**Linux下的crontab定时执行任务命令详解**](https://www.cnblogs.com/longjshz/p/5779215.html)

在LINUX中，周期执行的任务一般由cron这个守护进程来处理[ps -ef|grep cron]。cron读取一个或多个配置文件，这些配置文件中包含了命令行及其调用时间。cron的配置文件称为“crontab”，是“cron table”的简写。

**cron服务命令**

~~~javascript
//cron是一个linux下 的定时执行工具，可以在无需人工干预的情况下运行作业。
service crond start    //启动服务
service crond stop     //关闭服务
service crond restart  //重启服务
service crond reload   //重新载入配置
service crond status   //查看服务状态 
~~~

**cron在3个地方查找配置文件**
/var/spool/cron/ 这个目录下存放的是每个用户包括root的crontab任务，每个任务以创建者的名字命名，比如tom建的crontab任务对应的文件就是/var/spool/cron/tom。一般一个用户最多只有一个crontab文件。

**/etc/crontab 这个文件负责安排由系统管理员制定的维护系统以及其他任务的crontab**

~~~
SHELL=/bin/bash
PATH=/sbin:/bin:/usr/sbin:/usr/bin
MAILTO=root
HOME=/

\# For details see man 4 crontabs

\# Example of job definition:
\# .---------------- minute (0 - 59)
\# | .------------- hour (0 - 23)
\# | | .---------- day of month (1 - 31)
\# | | | .------- month (1 - 12) OR jan,feb,mar,apr ...
\# | | | | .---- day of week (0 - 6) (Sunday=0 or 7) OR sun,mon,tue,wed,thu,fri,sat
\# | | | | |
\# * * * * * user-name command to be executed
~~~

- MAILTO=root：是说，当 /etc/crontab 这个档案中的例行性命令发生错误时，会将错误讯息或者是屏幕显示的讯息传给谁？由于 root 并无法再用户端收信，因此，我通常都將这个 e-mail 改成自己的账号，好让我随时了解系统的状态！
- 01 \* \* \* \* root run-parts /etc/cron.hourly：在 #run-parts 这一行以后的命令，我们可以发现，五个数字后面接的是 root ，这一行代表的是『执行的级别为root身份』当然，你也可以将这一行改为成其他的身份！而 run-parts代表后面接的 /etc/cron.hourly 是『一个目录内（/etc/cron.hourly）的所有可执行文件』，也就是说，每个小时的01分，系统会以root身份去/etc/cron.hourly这个目录下执行所有可执行的文件！后面三行也是类似的意思！你可以到 /etc/ 底下去看看，系统本来就预设了这4个目录！你可以将每天需要执行的命令直接写到/etc/cron.daily即可，还不需要使用到crontab -e的程式！

**/etc/cron.d/ 这个目录用来存放任何要执行的crontab文件或脚本。**

**五、权限(？)**
crontab权限问题到/var/adm/cron/下一看，文件cron.allow和cron.deny是否存在
用法如下： 
1、如果两个文件都不存在，则只有root用户才能使用crontab命令。 
2、如果cron.allow存在但cron.deny不存在，则只有列在cron.allow文件里的用户才能使用crontab命令，如果root用户也不在里面，则root用户也不能使用crontab。 
3、如果cron.allow不存在, cron.deny存在，则只有列在cron.deny文件里面的用户不能使用crontab命令，其它用户都能使用。 
4、如果两个文件都存在，则列在cron.allow文件中而且没有列在cron.deny中的用户可以使用crontab，如果两个文件中都有同一个用户，以cron.allow文件里面是否有该用户为准，如果cron.allow中有该用户，则可以使用crontab命令。 

AIX 中 普通用户默认都有 crontab 权限，如果要限制用户使用 crontab ,就需要编辑/var/adm/cron/cron.deny 
HP-UNIX 中默认普通用户没得crontab 权限 ，要想放开普通用户的crontab 权限可以编

**创建cron脚本**
第一步：写cron脚本文件,命名为crontest.cron。
15,30,45,59 * * * * echo "xgmtest....." >> xgmtest.txt  表示，每隔15分钟，执行打印一次命令 
第二步：添加定时任务。执行命令 “crontab crontest.cron”。搞定 
第三步："crontab -l" 查看定时任务是否成功或者检测/var/spool/cron下是否生成对应cron脚本
注意：这操作是直接替换该用户下的crontab，而不是新增

 

**crontab用法** 
　　crontab命令用于安装、删除或者列出用于驱动cron后台进程的表格。用户把需要执行的命令序列放到crontab文件中以获得执行。
    每个用户都可以有自己的crontab文件。/var/spool/cron下的crontab文件不可以直接创建或者直接修改。该crontab文件是通过crontab命令创建的，在crontab文件中如何输入需要执行的命令和时间。该文件中每行都包括六个域，其中前五个域是指定命令被执行的时间，最后一个域是要被执行的命令。每个域之间使用空格或者制表符分隔。格式如下： 
　minute hour day-of-month month-of-year day-of-week commands 
    合法值 00-59 00-23 01-31 01-12 0-6 (0 is sunday) 
    除了数字还有几个个特殊的符号就是"*"、"/"和"-"、","，*代表所有的取值范围内的数字，"/"代表每的意思,"/5"表示每5个单位，"-"代表从某个数字到某个数字,","分开几个离散的数字。

​    -l 在标准输出上显示当前的crontab。 
　-r 删除当前的crontab文件。 
　-e 使用VISUAL或者EDITOR环境变量所指的编辑器编辑当前的crontab文件。当结束编辑离开时，编辑后的文件将自动安装。 

 

**例子：** 
每天早上6点 
0 6 * * * echo "Good morning." >> /tmp/test.txt //注意单纯echo，从屏幕上看不到任何输出，因为cron把任何输出都email到root的信箱了。

每两个小时 
0 */2 * * * echo "Have a break now." >> /tmp/test.txt  

晚上11点到早上8点之间每两个小时和早上八点 
0 23-7/2，8 * * * echo "Have a good dream" >> /tmp/test.txt

每个月的4号和每个礼拜的礼拜一到礼拜三的早上11点 
0 11 4 * 1-3 command line

1月1日早上4点 
0 4 1 1 * command line SHELL=/bin/bash PATH=/sbin:/bin:/usr/sbin:/usr/bin MAILTO=root //如果出现错误，或者有数据输出，数据作为邮件发给这个帐号 HOME=/ 

每小时执行/etc/cron.hourly内的脚本
01 * * * * root run-parts /etc/cron.hourly
每天执行/etc/cron.daily内的脚本
02 4 * * * root run-parts /etc/cron.daily 

每星期执行/etc/cron.weekly内的脚本
22 4 * * 0 root run-parts /etc/cron.weekly 

每月去执行/etc/cron.monthly内的脚本 
42 4 1 * * root run-parts /etc/cron.monthly 

注意: "run-parts"这个参数了，如果去掉这个参数的话，后面就可以写要运行的某个脚本名，而不是文件夹名。 　 

每天的下午4点、5点、6点的5 min、15 min、25 min、35 min、45 min、55 min时执行命令。 
5，15，25，35，45，55 16，17，18 * * * command

每周一，三，五的下午3：00系统进入维护状态，重新启动系统。
00 15 * * 1，3，5 shutdown -r +5

每小时的10分，40分执行用户目录下的innd/bbslin这个指令： 
10，40 * * * * innd/bbslink 

每小时的1分执行用户目录下的bin/account这个指令： 
1 * * * * bin/account

每天早晨三点二十分执行用户目录下如下所示的两个指令（每个指令以;分隔）： 
20 3 * * * （/bin/rm -f expire.ls logins.bad;bin/expire$#@62;expire.1st）　　

每年的一月和四月，4号到9号的3点12分和3点55分执行/bin/rm -f expire.1st这个指令，并把结果添加在mm.txt这个文件之后（mm.txt文件位于用户自己的目录位置）。 
12,55 3 4-9 1,4 * /bin/rm -f expire.1st$#@62;$#@62;mm.txt to

**备份linux系统上数据库 sh脚本**

~~~sh
#!/bin/bash

BACKUP_ROOT=/root/backup
BACKUP_FILEDIR=$BACKUP_ROOT/mysql/data
BACKUP_LOGDIR=$BACKUP_ROOT/mysql/logs
PASSWORD=zangaABc_LQB99

#当前日期
DATE=$(date +%Y%m%d)
echo $DATE

######备份######

#查询所有数据库
#-uroot -p12345678表示使用root账号执行命令，且root账号的密码为:123456
DATABASES=$(mysql -uroot -p$PASSWORD -e "show databases" | grep -Ev "Database|sys|information_schema|mysql|performance_schema")
#DATABASES=$(mysql -uroot -pzangaABc_LQB99 -e "SELECT SCHEMA_NAME FROM information_schema.SCHEMATA WHERE SCHEMA_NAME NOT IN ('sys','mysql','information_schema','performance_schema');" | grep -v "SCHEMA_NAME","ken.io") 
echo $DATABASES
#循环数据库进行备份
for db in $DATABASES
do
echo
echo ----------$BACKUP_FILEDIR/${db}_$DATE.sql.gz BEGIN----------
mysqldump -uroot -p$PASSWORD --default-character-set=utf8 -q --lock-all-tables --flush-logs -E -R --triggers -B ${db} | gzip > $BACKUP_FILEDIR/${db}_$DATE.sql.gz
echo ----------$BACKUP_FILEDIR/${db}_$DATE.sql.gz COMPLETE----------
echo
done

echo "done"
~~~

