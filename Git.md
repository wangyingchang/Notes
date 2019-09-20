![1568970804547](E:\github\img\git.png)



#### Git 常用命令

新建git仓库

~~~
git init
~~~

添加文件到缓存区

~~~
git add 文件/文件夹
~~~

添加所有内容到缓存区

~~~
git add -A
~~~

 将缓存区中的内容全部提交到git本地仓库中

~~~
git commit -m '提交信息'
~~~

查看提交日志

~~~
git log
~~~

让工作目录中的内容和仓库中的内容保持一致

~~~
git reset -- hard HEAD
~~~

回到上一个版本

~~~
git reset -- hard HEAD^
~~~

回到指定的版本

~~~
git reset -- hard 版本号
~~~

从暂存区中恢复工作目录中的内容(让工作区中的指定文件，回到上次提交的时候的状态)

~~~
git checkout -- 文件名
~~~

将服务器上的项目(仓库)克隆 (使用https地址需要输入密码，使用ssh地址需要添加公钥)

~~~
git clone -
~~~

关联远程仓库(只需要关联一次)

~~~
git remote add origin 地址
~~~

提交(-u在第一次提交分之的时候才用)

~~~
git push [-u] origin master
~~~

查看当前分支

~~~
git branch
~~~

查看所有分支

~~~
git branch -a
~~~

创建分支

~~~
git branch <name>
~~~

切换分支

~~~
git checkout <name>
~~~

创建+切换分支

~~~
git checkout -b <name>
~~~

查看两分支差异

~~~
git diff 分支1 分支2
~~~

合并某分支到当前分支

~~~
git merge <name>
~~~

删除分支

~~~
git branch -d <name>
~~~

查看本地代码状态

~~~
git status
~~~

查看命令历史：查看仓库的操作历史

~~~
git reflog
~~~

git远程仓库

~~~
git remote add origin https:*//github.com/hanhailong/CustomRatingBar*
~~~

移除远程仓库

~~~
git remote remove origin 
~~~



#### Git 设置密码

~~~
git config --global user.name "wangyingchang"
git config --global user.email "18386223128@163.com"
~~~



#### Git 绑定GitHub

1.打开Git Bash Here 生产密钥

~~~
ssh-keygen -t rsa -C "您注册GitHub时的邮箱"
~~~

2.我的电脑=>C盘=>User文件夹=>用户=>.ssh文件夹=>id_rsa.pub，copy内容

3.GitHub官网，点击头像=>Settings=>SSH and GPG keys=>new SSH key, paste内容

4.验证是否绑定成功

~~~
ssh -T git@github.com 
~~~



#### Git仓库 上传项目到GitHub仓库

第一步：初始化仓库 

~~~
git init    // cd到你的本地项目根目录下，执行git命令
~~~

第二步：添加所有文件到本地仓库

~~~
git add .  //.代表所有文件
~~~

第三步：添加的所有文件提交到本地仓库

~~~
git commit -m "提交说明"
~~~

第四步：去github仓库（Repository）拿https地址

第五步：本地仓库关联远程仓库(github)

~~~
git remote add origin https:*//github.com/hanhailong/CustomRatingBar*
~~~

第六步：上传文件到远程仓库之前，要先拉取（pull)一下

~~~
git pull origin master
~~~

第七步，上传代码到远程仓库(github)

~~~
git push -u origin master
将本地仓库内容推送到远端仓库(-u 表示第一次推送master分支的所有内容，后面再推送就不需要-u了)
~~~

中间可能会让你输入Username和Password，你只要输入github的账号和密码就行了；
