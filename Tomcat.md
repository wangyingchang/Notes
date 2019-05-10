#### Tomcat服务器

**1.常用的Web服务器**

-    IIS
-    Apache(C)
-    Tomcat(Java)

**2.简介**

- Tomcat是一个Web服务器，使用Java语言开发，实现了一个Servlet引擎和JSP引擎，因而它支持Java的Servlet与JSP。
- Tomcat默认端口号：8080
- 注意：IIS服务器 – 默认端口是80

**3.安装**

- 安装JDK
- Tomcat使用必须依靠JDK支持—JDK1.6版本--配置JDK的JAVA_HOME
- 根据设置好的JAVA_HOME，找到所需要的JDK的支持

**4.目录**

bin: 存放启动和关闭tomcat脚本

conf: 包含不同的配置文件

~~~
server.xml:  tomcat的主要配置文件,  端口号 就在里面修改 

web.xml：会话超时时间的配置 

tomcat-users.xml : 配置tomcat用户名与密码
~~~

webapps :存放所有的web程序实例

work :存放jsp编译后产生的Servlet文件

lib:存放所有需要的*.jar包
