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



#### Git 上传项目到GitHub

第一步：建立git仓库 

~~~
git init    // cd到你的本地项目根目录下，执行git命令
~~~

第二步：将项目的所有文件添加到仓库中

~~~
git add .  //如果想添加某个特定的文件，只需把.换成特定的文件名即可
~~~

第三步：将添加的文件commit到仓库

~~~
git commit -m "注释语句"
~~~

第四步：去github拿到创建的仓库（Repository）的https地址

~~~

~~~

第五步：将本地的仓库关联到github上

~~~
git remote add origin https:*//github.com/hanhailong/CustomRatingBar*
~~~

第六步：上传github之前，要先pull一下，执行如下命令：

~~~
git pull origin master
~~~

第七步，也就是最后一步，上传代码到github远程仓库

~~~
git push -u origin master
~~~

中间可能会让你输入Username和Password，你只要输入github的账号和密码就行了；
