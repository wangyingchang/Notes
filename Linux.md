##### Linux 常用命令

**远程传送文件**

~~~
scp local_file remote_username@remote_ip:remote_folder
~~~

~~~
scp -p 4588 local_file remote_username@remote_ip:remote_folder
~~~

**清空文件**

~~~
echo "" > filename
~~~

**查看端口**

~~~
netstat -ntlp
~~~

**查看进程**

~~~
ps -ef | grep nginx

# ps为linux查看进程命令， grep为过滤命令，该条命令是输出运行nginx进程详细信息，第二列为进程号
~~~

**杀死进程**

~~~
kill -9 XX 
-- kill为linux杀进程命令, XX为上一个命令的输出第二列的数字
~~~

**杀死指定目录下所有进程**

```
ps -ef | grep mowangdougongzhu/apps | grep mowangdougongzhu/apps | cut -c 9-15 | xargs kill -9
```

**查看文件大小**

~~~
du -sh filename
~~~

**查看文件信息：**

~~~
ls [选项]
~~~

选项：

- -a  : 显示全部的文件，包括隐藏文件（开头为 . 的文件）也一起罗列出来，这是最常用的选项之一
- -d： 仅列出目录本身，而不是列出目录内的文件数据。
- -f  ls 默认会以文件名排序，使用 -f 选项会直接列出结果，而不进行排序。  
- -F  在文件或目录名后加上文件类型的指示符号，例如，* 代表可运行文件，/ 代表目录，= 代表 [socket](http://c.biancheng.net/socket/) 文件，| 代表 FIFO 文件。 
-  -h  以人们易读的方式显示文件或目录大小，如 1KB、234MB、2GB 等。  
- -i  显示 inode 节点信息。  
- -l  使用长格式列出文件和目录信息。 
-  -n  以 UID 和 GID 分别代替文件用户名和群组名显示出来。  
- -r  将排序结果反向输出，比如，若原本文件名由小到大，反向则为由大到小。  
- -R  连同子目录内容一起列出来，等於将该目录下的所有文件都显示出来。  
- -S  以文件容量大小排序，而不是以文件名排序。  
- -t  以时间排序，而不是以文件名排序。

**清屏(ctrl+l)**

~~~
clear
~~~

**切换工作目录**

~~~
cd [选项]
~~~

| ~       | 代表当前登录用户的主目录   |
| ------- | -------------------------- |
| ~用户名 | 表示切换至指定用户的主目录 |
| -       | 代表上次所在目录           |
| .       | 代表当前目录               |
| ..      | 代表上级目录               |

**显示当前路径**

~~~
pwd
~~~

**创建目录**

~~~
mkdir [选项] 目录名
~~~

选项：

- -m 选项用于手动配置所创建目录的权限，而不再使用默认权限。
- -p 选项递归创建所有目录，以创建 /home/test/demo 为例，在默认情况下，你需要一层一层的创建各个目录，而使用 -p 选项，则系统会自动帮你创建 /home、/home/test 以及 /home/test/demo。

**创建文件**

```
touch [选项] 文件名
```

选项：

- -a：只修改文件的访问时间；
- -c：仅修改文件的时间参数（3 个时间参数都改变），如果文件不存在，则不建立新文件。
- -d：后面可以跟欲修订的日期，而不用当前的日期，即把文件的 atime 和 mtime 时间改为指定的时间。
- -m：只修改文件的数据修改时间。
- -t：命令后面可以跟欲修订的时间，而不用目前的时间，时间书写格式为 `YYMMDDhhmm`。

**删除文件**

~~~
rm [选项] 文件或目录
~~~

选项：

- -f：强制删除（force），和 -i 选项相反，使用 -f，系统将不再询问，而是直接删除目标文件或目录。
- -i：和 -f 正好相反，在删除文件或目录之前，系统会给出提示信息，使用 -i 可以有效防止不小心删除有用的文件或目录。
- -r：递归删除，主要用于删除目录，可删除指定目录及包含的所有内容，包括所有的子目录和文件。

**拷贝文件**

~~~root
cp [选项] 源文件 目标文件
~~~

选项：

- -a：相当于 -d、-p、-r 选项的集合，这几个选项我们一一介绍；
- -d：如果源文件为软链接（对硬链接无效），则复制出的目标文件也为软链接；
- -i：询问，如果目标文件已经存在，则会询问是否覆盖；
- -l：把目标文件建立为源文件的硬链接文件，而不是复制源文件；
- -s：把目标文件建立为源文件的软链接文件，而不是复制源文件；
- -p：复制后目标文件保留源文件的属性（包括所有者、所属组、权限和时间）；
- -r：递归复制，用于复制目录；
- -u：若目标文件比源文件有差异，则使用该选项可以更新目标文件，此选项可用于对文件的升级和备用。

**移动、重命名文件**:

~~~
mv 【选项】 源文件 目标文件
~~~

选项：

- -f：强制覆盖，如果目标文件已经存在，则不询问，直接强制覆盖；

- -i：交互移动，如果目标文件已经存在，则询问用户是否覆盖（默认选项）；
- -n：如果目标文件已经存在，则不会覆盖移动，而且不询问用户；
- -v：显示文件或目录的移动过程；
- -u：若目标文件已经存在，但两者相比，源文件更新，则会对目标文件进行升级；

**建立软/硬连接**

~~~
 ln [选项] 源文件 目标文件
~~~

选项：

- -s：建立软链接文件。如果不加 "-s" 选项，则建立硬链接文件；
- -f：强制。如果目标文件已经存在，则删除目标文件后再建立链接文件；

**查看或者合并文件内容：**

~~~
cat
~~~

**文本搜索**：Linux系统中grep命令是一种强大的文本搜索工具，grep允许对文本文件进行模式查找。如果找到匹配模式， grep打印包含模式的所有行。

```
grep [-选项] '搜索内容串'文件名

在某个目录下的所有的.log中检索 含有 xxx的行，并写入a.txt文件 ，或者追加到a.txt
grep "DiamondCost" *.log > a.txt
grep "DiamondCost" *.log >> a.txt

grep -C 5 foo file 显示file文件中匹配foo字串那行以及上下5行
grep -B 5 foo file 显示foo及前5行
grep -A 5 foo file 显示foo及后5行
```

 **查找文件**

~~~
find
~~~

**打包文件**

~~~
tar [选项] 打包文件名 文件
~~~

选项：

- -c 生成档案文件，创建打包文件
- -v 列出归档解档的详细过程，显示进度
- -f 指定档案文件名称，f 后面一定是tar 文件，所以必须放在选择最后
- -t 列出解档中包含的文件
- -x 解开档案文件

**压缩文件**

```
gzip [选项] 被压缩文件
```

选项：

- -d 解压
- -r 压缩所有子目录

**打包压缩文件**

~~~
tar cvzf 压缩包包名 文件1 文件2 …

tar zxvf 压缩包包名
~~~

**查看命令位置**

~~~
which
~~~



**修改文件权限**

~~~
chmod
~~~

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

方式一：查询语句直接输出

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

方式二：在shell命令行下把Excel以文本方式打开，然后另存为，在编码选择ansi编码保存（推荐）
语法格式

~~~
echo "select * from magic_tower_server_db_shouQ_dev_21.UserPrincesses" |  mysql -uroot -pzangaABc_LQB99 > 21.xls
echo 查询语句 管道 登录mysql链接方式 > 定向输出文件
~~~

方式三：查询定向输出为Excel文件后缀，然后转码（权限不足）

~~~
mysql db_web -uroot  -e "select * from help_cat where 1 order by type desc limit 0,20" > /data/type.xls
 mysql连接信息 数据库 用户名 密码 然后执行查询语句，定向输出。
~~~

将文件下载到本地，打开如果中文乱码，因为office默认的是gb2312编码，服务器端生成的很有可能是utf-8编码，这个时候你有两种选择:
1、在服务器端使用iconv来进行编码转换

```
iconv -futf8 -tgb2312 -otype1.xls type.xls
```

如果转换顺利，那么从server上下载下来就可以使用了。
2、转换如果不顺利，则会提示:

```
iconv: illegal input sequence at position 1841
```

类似错误，如下解决：
先把type.xls下载下来，这个时候文件是utf-8编码的，用excel打开，乱码。把type.xls以文本方式打开，然后另存为，在编码选择ANSI编码保存。





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

**备份数据库脚本**

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

备份日志脚本

~~~sh

LOGDIR=/home/mwdgz/project/mowangdougongzhu/apps/server

BACKUP_LOGDIR=/home/mwdgz/backup/logs


date=`date +%Y_%m_%d`
tarFileName=$date"_logs.tar"


tar cvf $LOGDIR/$tarFileName $LOGDIR/logs

mv $LOGDIR/$tarFileName $BACKUP_LOGDIR

rm -rf $LOGDIR/logs/pomelo.log.*
rm -rf $LOGDIR/logs/qosMonitor.log.*
rm -rf $LOGDIR/logs/sqlMonitor.log.*

echo "" > $LOGDIR/logs/pomelo.log
echo "" > $LOGDIR/logs/qosMonitor.log
echo "" > $LOGDIR/logs/sqlMonitor.log

~~~

