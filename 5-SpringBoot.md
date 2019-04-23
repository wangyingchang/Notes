**学习网址：https://blog.csdn.net/column/details/22146.html?&page=1**

1.日志logback
2.集成mybatis
3.集成druid数据库连接池
4.集成pagehelper分页插件
5.集成Mapper4(通用mapper)
6.集成fastjson
7.集成文件上传
8.集成ehcache缓存
9.集成mybatis generator自动生成代码插件
10.集成shiro
11.集成redis

#### SpringBoot 背景

**Java的开发一直让开发人员诟病**

1. Java项目开发复杂度极高
2. Java项目的维护非常困难
3. 在云时代如何实现项目的快速部署以及快速启动
4. 即便使用了大量的开发框架，发现我们的开发也没少多少
   当所有人认为Spring不再前进的时候，Spring推出了位架构实现的两个框架：SpringBoot,SpringCloud

1. Java开发的复杂度是最高的？

  在所有的软件行业中，如果要说商用体系，排在第一位的永远是Java,因为Java的体系丰富，支持度高，
  安全性也高，但是同时开发者也需要忍受以下的痛苦：	

  ```
  （1）Java里面的开发都支持属于原生操作代码，例如：JDBC中，如果使用Java的原生代码，会
  		重复编写大量的代码，如PreparedStatement操作
  （2）Java进行WEB开发项目时候，必须要按照严格的格式进行WEB项目的创建，以及每当创建
  		WEB项目时候，又需要进行Tomcat的重新启动
  （3）Java中虽然提供了所谓的开发标准，但是所有的公司几乎都有自己的标准
  	例如：Java起初的JVM有三个版本，而且很多公司由于 版本不同会造成部署环境不同
  （4）Java里面严格要求按照MVC的设计模式完成
  （5） 以web开发为例，一个良好的JSP程序代码中不应该有任何的scriptlet代码，
  		要实现非常麻烦。有各种实现标准，例如：JSTL+EL ，springTaglib,JSF....
  ```

  繁杂

(1). Java后期的发展使用了大量的Maven技术作为开发，但是使用之后还是没有逃离传统WEB开发的身影，
所有的项目依然需要打包，然后上传到系统中。使用Maven还有一个最大的痛：如果是开发框架，那一堆
的Maven的依赖库很庞大繁杂。

(2). Rest技术已经开始在行业中流传，Java要想实现Rest开发（基于Spring）,很麻烦

(3). 现在行业中，Spring已经作为绝对的Java架构，但是要想在Spring中整合其他框架，需要编程一堆堆的*.xml文件所以在这样大的历史背景下，很多人开始寻找更简单的开发，而遗憾的是没有被JDK或JavaEE锁支持，因为这只是平台，平台能够提供的
只是最原始的技术支持。这时候SpringBoot改变了所有开发的困境，或者说最终奉承的宗旨：废除所有的复杂开发，废除所有的配置，让开发更简洁纯粹，核心"零配置"（DREAM） 



#### SpringBoot 简介

- 简化Spring应用开发的一个框架
- 整个Spring技术栈的一个大整合
- J2EE开发的 一站式解决方案
- 内置Servlet容器
- 约定大于配置
- starter：启动器
- 独立运行

SpringBoot之所以能慢慢火遍全世界，是因为在springBoot中视同了大量的注解，让所有开发者几乎可以零适应的进行完整过度。



本次快速启动程序将直接采用Spring官方给出的demo来进行代码的执行分析。

1. 如果想要进行SpringBoot开发，一定需要使用maven或者其他项目管理工具完成。
2. Springboot运行之后会以WEB程序为主，但是现在所建立的只是一个普通的quickstart程序。

如果想要开发SpringBoot程序，只需要按官方给出的要求配置一个父pom即可。

项目下载好后，导入项目至IDEA

```java
@Controller
@SpringBootApplication
public class Application {
   @RequestMapping("/")
   @ResponseBody
   public String home(){
      return "helloSpringBoot";
   }

   public static void main(String[] args) {
      SpringApplication.run(Application.class, args);
   }
}
```

- 待Maven依赖环境部署好后，运行main函数，运行效果如下

- **若以Web方式运行，则需要以maven方式启动项 目**

（1）配置以Maven方式启动项目

（2）启动项目

（3）运行效果​	



总结：

SpringBoot的天生缺陷：

    SpringBoot本省实在spring4后诞生的，对开发者的要求比较高，起点必须了解Maven,SSM整个开发。



#### SpringBoot pom.xml

```xml
<?xml version="1.0" encoding="UTF-8"?>
<project xmlns="http://maven.apache.org/POM/4.0.0" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
	xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/xsd/maven-4.0.0.xsd">
	<modelVersion>4.0.0</modelVersion>
    
	<!-- 新建项目的描述信息-->
	<groupId>com.chixing</groupId>
	<artifactId>springboot2.0.5_demo</artifactId>
	<version>0.0.1-SNAPSHOT</version>
	<packaging>jar</packaging>

	<name>springboot2.0.5_demo</name>
	<description>Demo project for Spring Boot</description>
    
	<!-- 父项目
		SpringBoot的版本仲裁中心
		以后导入依赖默认不需要写版本号
		没有在dependencies里管理的依赖除外，需要声明版本号
	-->
	<parent>
		<groupId>org.springframework.boot</groupId>
		<artifactId>spring-boot-starter-parent</artifactId>
		<version>2.0.5.RELEASE</version>
		<relativePath/> <!-- lookup parent from repository -->
        <!-- 可能还会有该父项目的父项目配置-->
	</parent>

	<properties>
		<project.build.sourceEncoding>UTF-8</project.build.sourceEncoding>
		<project.reporting.outputEncoding>UTF-8</project.reporting.outputEncoding>
		<java.version>1.8</java.version>
	</properties>

	<dependencies>
		<!-- 启动器
			SpringBoot将所有的功能场景都抽取出来，做成了一个个starter(启动器)
			主需要在项目中引入这些starter，相关场景的所有依赖都会导入进来

			spring-boot-starter：Spring boot场景启动器
			                web:自动导入web模块正常运行所依赖的组件
		-->

		<dependency>
			<groupId>org.springframework.boot</groupId>
			<artifactId>spring-boot-starter-web</artifactId>
		</dependency>
		<!--<dependency>
			<groupId>org.mybatis.spring.boot</groupId>
			<artifactId>mybatis-spring-boot-starter</artifactId>
			<version>1.3.2</version>
		</dependency>-->

		<dependency>
			<groupId>org.springframework.boot</groupId>
			<artifactId>spring-boot-starter-test</artifactId>
			<scope>test</scope>
		</dependency>
	</dependencies>

	<build>
		<plugins>
			<!--该插件可以将应用打包成一个可执行的jar -->
			<plugin>
				<groupId>org.springframework.boot</groupId>
				<artifactId>spring-boot-maven-plugin</artifactId>
			</plugin>
		</plugins>
	</build>
</project>
```



#### SpringBoot 注解分析

| No   | 注解                              | 说明                                                         |
| ---- | --------------------------------- | ------------------------------------------------------------ |
| 1    | @Controller                       | 进行控制器的配置注解，这个注解所在类就是控制器类             |
| 2    | @EnableAutoConfiguration          | 开启自动配置处理                                             |
| 3    | @RequestMapping                   | 表示访问的映射路径，若路径为"/"，访问地址为http://localhost:8080/ |
| 4    | @ResponseBody                     | 在Restful架构中，该注解表示直接将返回的数据以字符串或JSON的形式获得 |
| 5    | @SpringBootConfiguration          | 标注在某个类上，表示这是一个Spring Boot的配置类              |
| 6    | @SpringBootApplication            | 使用@SpringBootApplication来标注一个主程序类，表明这是一个SpringBoot应用 |
| 7    | @AutoConfigurationPackage         | 自动配置包                                                   |
| 8    | @Import                           | Spring的底层注解，给容器导入组件                             |
| 9    | @AutoConfigurationImportSelector  | 导入组件选择器，将所有需要导入的组件以全类名形式返回，这些组件会被添加到容器中，其实就是给容器导入非常多的自动配置类(xxAutoConfiguration)，并且配置好这些组件 |
| 10   | @Mapper                           | Dao接口的注解                                                |
| 11   | @MapperScan("com.springboot.dao") | 扫描dao接口                                                  |



项目结构说明

（1）Application.java: 程序主入口，用于启动SpringBoot应用程序

（2）application.properties :配置文件（可自定义 ）

（3）Test：测试类

（4）pom.xml：Maven构建说明文件

```xml
<!-- parent节点：SpringBoot父依赖 -->
<parent>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-parent</artifactId>
    <version>2.0.5.RELEASE</version>
    <relativePath/> <!-- lookup parent from repository -->
</parent>
<!-- 如果要修改其中依赖包的版本，只需要直接添加 -->
<properties>
    <freeker.version>2.3.23</freeker.version> <!-- 覆盖掉父级属性--> 
</properties>

<!-- 不使用parent -->
<dependencies>
    <dependency>
        <groupId>org.springframework.boot</groupId>
        <artifactId>spring-boot-starter-web</artifactId>
         <version>2.0.5.RELEASE</version>
        <type>pom</type>
        <scope>import</scope>
    </dependency>
    <dependency>
        <groupId>org.freemarkers</groupId>
        <artifactId>freemarkers</artifactId>
         <version>23.23</version>    
    </dependency>
</dependencies>
```

其他运行方式 -jar

--maven --lifecircle--clean--package 项目中生成jar文件

在cmd 中 找到该jar文件所在路径，java -jar springboot2.0.5_demo-0.0.1-SNAPSHOT.jar

效果：

```
(1)显示springboot的banner
(2)启动tomcat
```

在浏览器中访问该项目OK 





#### SpringBoot 配置文件

SpringBoot 使用一个全局的配置文件application.properties或者application.yml，放置在src/main/resources目录或者类路径的config下;

SpringBoot 不仅支持常规的properties配置文件，还支持yaml语言的配置文件，yaml以数据为中心的语言，在配置数据时具有面向对象的特征;

SpringBoot 全局配置文件的作用是对一些默认的配置值进行修改

**示例1**

修改默认端口号8080->8082，并将默认路径“/”改为 “demo”

application.properties:

~~~properties
server.port=8082
server.servlet.context-path=/demo
~~~

application.yml

~~~yml
server:
  port: 8082
  servlet:
    context-path:/demo
~~~

**示例2**

把配置写到 StudentProperties.java

```java
@Component
@ConfigurationProperties(prefix = "student")
public class StudentProperties {
    private String name ;
    private int age;
    private float height;
    public String getName() {
        return name;
    }
    ... ...
```

配置文件 application.properties

```properties
server.port=8081
server.servlet.context-path=/demo

student.name=tony
student.age: 20
student.height: 178
```

运行类 Applicaiton.java

```java
@Controller
@SpringBootApplication
public class Application { 
   @Autowired
   private StudentProperties student; 
    
   @RequestMapping("/")
   @ResponseBody
   public String home(){
      return "helloSpringBoot!name:" + student.getName()+",age :" + student.getAge()+",height:" + student.getHeight();
   }
   public static void main(String[] args) {
      SpringApplication.run(Application.class, args);
   }
   
```

注意：

若要求在开发环境与实际生产环境中不一致，配置文件如何在两个阶段切换自如？

复制application.properties文件命名为application-dev.properties，application-prod.properties

application-dev.properties

```properties
server.port=8081
server.servlet.context-path=/demo

student.name=development
student.age: 20
student.height: 178
```

application-prod.properties

```properties
server.port=8082
server.servlet.context-path=/demo

student.name=produce
student.age: 20
student.height: 178
```

在appllication.properties中使用dev环境（application-dev.properties）

```properties
spring.profiles.active=dev
```

运行测试出来的是 dev环境中的数据





#### SpringBoot HelloWorld

**建表sql**

```sql
 CREATE TABLE user (
  id int(3) NOT NULL AUTO_INCREMENT,     
  userName varchar(255) DEFAULT NULL,
  userAge int(2),	
  userAddress varchar(255) DEFAULT NULL,
  PRIMARY KEY (id)
 );
```

**application.properties**

```properties
spring.datasource.url=jdbc:mysql://localhost:3306/springboot
spring.datasource.username=root
spring.datasource.password=123
spring.datasource.driver-class-name=com.mysql.jdbc.Driver
```

**SpringBoot**

- @Controller:处理http请求

- @RestController: Spring4之后新加的注解，原来返回json需要@ResponseBody配合@Controller

  ```
  @RestController = @Controller+ @ResponseBody
  ```

- @RequestMapping:配置url映射

- @PathVariable:获取url中的数据

- @RequestParam:获取请求参数的值

- @GetMapping:组合注解

  整合Mybatis

  ```xml
  		<!--mybatis-->
  		<dependency>
  			<groupId>org.mybatis.spring.boot</groupId>
  			<artifactId>mybatis-spring-boot-starter</artifactId>
  			<version>1.1.1</version>
  		</dependency>
  		<!--mysql-->
  		<dependency>
  			<groupId>mysql</groupId>
  			<artifactId>mysql-connector-java</artifactId>
  			<version>5.1.46</version>
  		</dependency>
   
  ```

**实体类 User.java**

```java
@Setter
@Getter
public class User {
    private int id;
    private String userName;
    private int userAge;
    private String userAddress;

｝
```

@Setter和@Getter两个注解顾名思义应该会想到这是getter和setter方法 
因为每个实体类都应该包含getter和setter方法才有意义。但是getter和setter方法的代码过于冗余，属于模板类型代码，影响代码阅读。@Setter和@Getter两个注解是属于[lombok][6]的，在pom.xml文件中添加依赖引入lombok：

```
<!--@Getter @Setter注解-->
<dependency>
   <groupId>org.projectlombok</groupId>
   <artifactId>lombok</artifactId>
   <version>1.14.4</version>
</dependency>
```

**UserMapper.java映射器类**

该类主要是用于CRUD操作的，一般有两种方式实现与数据库实现CRUD：
注解： @Insert、@Select、@Update、@Delete
xml文件配置
基于注解的配置如下：

```java
package com.springBoot.dao;

import com.springBoot.entity.User;
import org.apache.ibatis.annotations.*;
import org.springframework.stereotype.Component;
import java.util.List;

@Mapper
@Component
public interface UserDao {
    //根据id查询用户
    @Select("select * from user where id = #{id}")
    User selectUserById(int id);
    //查询所有用户
    @Select("select * from user")
    List<User> selectUser();
    //根据用户名查询用户
    @Select("select * from user where userName = #{userName}")
    List selectUserByName(String userName);
    //添加用户
    @Insert("insert into user(userName,userAge,userAddress) values (#{userName},#{userAge},#{userAddress})")
    void addUser(User user);
    //修改用户
    @Update("update user set userName=#{userName},userAge=#{userAge},userAddress=#{userAddress} where id=#{id}")
    void updateUser(User user);
    //删除用户
    @Delete("delete from user where id=#{id}")
    void deleteUser(int id);
}
```

**UserController.java 控制器类**

```java
package com.springBoot.controller;

import com.springBoot.dao.UserDao;
import com.springBoot.entity.User;
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.web.bind.annotation.RequestMapping;
import org.springframework.web.bind.annotation.RequestMethod;
import org.springframework.web.bind.annotation.RestController;
import java.util.List;

@RequestMapping("/user")
@RestController
public class UserController {
    UserController(){
        System.out.println("构造函数");
    }
    @Autowired
    private UserDao userDao;
    //通过用户Id查询用户
    @RequestMapping(value={"/selectUserById"}, method= RequestMethod.GET)
    public User selectUserById(String id){
        User user = userDao.selectUserById(Integer.parseInt(id));
        return user;
    }
    //查询所有用户
    @RequestMapping(value={"/selectUser"}, method= RequestMethod.GET)
    public List<User> selectUser(){
        List<User> user = userDao.selectUser();
        return user;
    }
    //通过用户名查询用户
    @RequestMapping(value={"/selectUserByName"}, method=RequestMethod.GET)
    public List<User> selectUserByName(String userName){
        return userDao.selectUserByName(userName);
    }
    //添加用户
    @RequestMapping(value={"/addUser"}, method=RequestMethod.POST)
    public void addUser(User user){
        userDao.addUser(user);
    }
    //修改用户
    @RequestMapping(value={"/updateUser"}, method=RequestMethod.POST)
    public void updateUser(User user){
        userDao.updateUser(user);
    }
    //删除用户
    @RequestMapping(value={"/deleteUser"}, method=RequestMethod.POST)
    public void deleteUser(String id){
        userDao.deleteUser(Integer.parseInt(id));
    }
}
```

resources目录下，static文件夹是放置各种静态资源，如css，js，img等文件的。templates文件夹则是默认放置网页的。当然也可以更改。



#### SpringBoot 集成JSP

springboot 默认是不集成JSP的，对其他视图模版支持较好，所以要集成JSP，需要手动配置。

（1）导入依赖包  

```xml
       <dependency>
			<groupId>javax.servlet</groupId>
			<artifactId>javax.servlet-api</artifactId>
			<scope>provided</scope>
		</dependency>
		<!-- JSTL (JSP standard Tag Library) JSP 标准标签库 -->
		<dependency>
			<groupId>javax.servlet</groupId>
			<artifactId>jstl</artifactId>
		</dependency>
		<!-- Tomcat的支持 -->
		<dependency>
			<groupId>org.springframework.boot</groupId>
			<artifactId>spring-boot-starter-tomcat</artifactId>
			<!--  <scope>provided</scope>-->
		</dependency>
		<!--springboot外部tomcat支持-->
		<dependency>
			<groupId>org.apache.tomcat.embed</groupId>
			<artifactId>tomcat-embed-jasper</artifactId>
			<!-- <scope>provided</scope>-->
		</dependency>
```

（2）配置application.properties：

```
#页面默认前缀目录
spring.mvc.view.prefix=/WEB-INF/jsp/
#页面默认后缀目录
spring.mvc.view.suffix=.jsp
```

或者 application.yml中：

```
mvc:
  view:
    prefix: /WEB-INF/jsp/
    suffix: .jsp
```

 （3）启动项目

在项目main文件夹下新建webapp/WEB-INF/jsp/hello.jsp,Modules中配置web路径 生成web.xml

不用去管web.xml.，一会在其他地方配置的时候会自动出现，hello.jsp，最好将编码改为UTF-8,

```jsp
<%@ page contentType="text/html;charset=UTF-8" language="java" %>
<html>
<head>
    <title>My first Spring boot web demo</title>
</head>
<body>
<h2>Hello ${name}</h2>
</body>
</html>
 
```

创建JspController.java

```java
@Controller
public class JspController {
    public JspController(){
        System.out.println("<<<<<<<<<<<<<<<<<<<<<<<<<<<,,JspController");
    }
    @RequestMapping("/hello")
    public String hello(){
        System.out.println("<<<<<..................<<<,,hello");
        return "hello";
    }
}
```

访问localhost:8080/hello 





#### SpringBoot 日志配置

 在项目的开发中，日志是必不可少的一个记录事件的组件，所以也会相应的在项目中实现和构建我们所需要的日志框架。

市面上常见的日志框架有很多，比如：JCL、SLF4J、Jboss-logging、jUL、log4j、log4j2、logback等等，我们该如何选择呢？

通常情况下，日志是由一个抽象层+实现层的组合来搭建的。

| **日志-抽象层**           | **日志-实现层**             |
| ------------------------- | --------------------------- |
| JCL、SLF4J、jboss-logging | jul、log4j、log4j2、logback |

而SpringBoot的选择了SLF4J+Logback的组合，这个组合是当下比较合适的一组

日志级别从低到高分为：

> `TRACE` < `DEBUG` < `INFO` < `WARN` < `ERROR` < `FATAL`。

 首先，引入AOP的依赖包

```xml
<dependency>  
   	<groupId>org.springframework.boot</groupId>  
   	<artifactId>spring-boot-starter-aop</artifactId>  
</dependency> 
```

  日志测试

```java
@SpringBootApplication
public class SpringbootFirstApplication {

   static Logger logger = LoggerFactory.getLogger(Logger.class);
   public static void main(String[] args) {
      logger.trace("trace.....");
      logger.debug("debug.....");
      logger.info("info.....");
      logger.warn("warn.....");
      logger.error("error.....");

      SpringApplication.run(SpringbootFirstApplication.class, args);
   }
}
```

运行结果：

```
[main] DEBUG org.slf4j.Logger - debug.....
 [main] INFO org.slf4j.Logger - info.....
[main] WARN org.slf4j.Logger - warn.....
 [main] ERROR org.slf4j.Logger - error.....
```

可以看到，日志只输出了degug、info、warn、error 。



**AOP思想配置**

AOP即面向切面编程，通过预编译方式和运行期动态代理实现程序功能的统一维护的一种技术。如果几个或更多个逻辑过程中，有重复的操作行为，AOP就可以提取出来，运用动态代理，实现程序功能的统一维护，这样就非常方便了，在实现主业务过程中无需为一些零碎的但必不可少的旁支功能打扰，而是后期横切进去.

新建一个HttpAspect类，放在aspect包下：

```java
@Aspect
@Component
public class HttpAspect {	
	private Logger logger = LoggerFactory.getLogger(this.getClass());

	@Pointcut("execution(public * org.chixing.controller.ItemsController1.*(..))")   
	public void myLog() {    }		
	
	@Before("myLog()")	
	public void reqMessage() {		
		ServletRequestAttributes attributes = (ServletRequestAttributes) RequestContextHolder.getRequestAttributes();        
        HttpServletRequest request = attributes.getRequest();       
		logger.info("*********打印请求信息开始**********");		
		logger.info("URL : " + request.getRequestURL().toString());   
		logger.info("HTTP_METHOD : " + request.getMethod());     
		logger.info("*********打印请求信息结束**********");	
	}	

	@AfterReturning(returning="object",pointcut="myLog()")	
	public void resMessage(Object object) {		
		logger.info("*********打印结果信息开始**********");	
		logger.info("RESULT:"+ object);		
		logger.info("*********打印结果信息结束**********");
	}
}
```

就这样，其余代码都不变，我们运行之后，输入http://localhost:8080/user，控制台显示打印信息即可。

@Aspect    作用是把当前类标识为一个切面供容器读取。

@Before     标识一个前置增强方法，相当于BeforeAdvice的功能，从切入点开始处切入内容。

@AfterReturning      后置增强，相当于AfterReturningAdvice，方法正常退出时执行。

@Pointcut      定义一个切入点，可以是一个规则表达式，也可以是一个注解等



 **配置日志生成的路径及日志名称**

在项目的运行中，我们不可能一直看着控制台，而且日质量会很大，转瞬即逝的~

那么，我们需要指定我们需要的日志名称以及日志生成的路径，用到两个配置，都是在application.properties/yml中写，如下：（都不设置的话，不生成日志）

```
# 按照默认的名称spring.log，生成到指定路径及日志。
#logging.path=output/logs
# 不指定的情况下默认生成在项目根目录，按照配置生成所需的日志名称
logging.file=D:\logger\myLogger.log
```

**配置自定义log信息**

如果想用自己的log配置，不用系统默认的，那么只需要按照官方要求，将该配置文件放在所需类的目录下即可，也可以在resource中配置全局的

然而官方推荐我们在这些命名中，使用带有spring的扩展名，它会被SpringBoot框架识别（不写的单会被日志框架识别），并且可以使用其相应的功能，比如根据环境来使用某段配置：







#### SpringBoot Druid连接池

**1.Druid介绍**

Druid是一个JDBC组件，druid 是阿里开源在 github 上面的数据库连接池,它包括三部分：  
 \*   DruidDriver 代理Driver，能够提供基于Filter－Chain模式的插件体系。 
 \*   DruidDataSource 高效可管理的数据库连接池。 
 \*   SQLParser 专门解析 sql 语句

Druid 有什么优点

可以监控数据库访问性能，Druid内置提供了一个功能强大的StatFilter插件，能够详细统计SQL的执行性能，这对于线上分析数据库访问性能有帮助。 

替换DBCP和C3P0。Druid提供了一个高效、功能强大、可扩展性好的数据库连接池。 

数据库密码加密。直接把数据库密码写在配置文件中，这是不好的行为，容易导致安全问题。DruidDruiver和DruidDataSource都支持PasswordCallback。 

SQL执行日志，Druid提供了不同的LogFilter，能够支持Common-Logging、Log4j和JdkLog，你可以按需要选择相应的LogFilter，监控你应用的数据库访问情况。

扩展JDBC，如果你要对JDBC层有编程的需求，可以通过Druid提供的Filter-Chain机制，很方便编写JDBC层的扩展插件。



 **2.Springboot 配置Druid**

（1）pom.xml

```xml
<!--
   引入druid数据源
   https://mvnrepository.com/artifact/com.alibaba/druid
-->
<dependency>
   <groupId>com.alibaba</groupId>
   <artifactId>druid</artifactId>
   <version>1.0.20</version>
</dependency>
```

（2）application.properties

```properties
#MySQL配置
spring.datasource.url=jdbc:mysql://localhost:3306/springboot
spring.datasource.username=root
spring.datasource.password=123
spring.datasource.driver-class-name=com.mysql.jdbc.Driver
spring.datasource.type=com.alibaba.druid.pool.DruidDataSource

# 连接池的配置信息
# 初始化大小，最小，最大
spring.datasource.initialSize=5
spring.datasource.minIdle=5
spring.datasource.maxActive=20
# 配置获取连接等待超时的时间
spring.datasource.maxWait=60000
# 配置间隔多久才进行一次检测，检测需要关闭的空闲连接，单位是毫秒
spring.datasource.timeBetweenEvictionRunsMillis=60000
# 配置一个连接在池中最小生存的时间，单位是毫秒
spring.datasource.minEvictableIdleTimeMillis=300000
spring.datasource.validationQuery=SELECT 1 FROM DUAL
spring.datasource.testWhileIdle=true
spring.datasource.testOnBorrow=false
spring.datasource.testOnReturn=false
# 打开PSCache，并且指定每个连接上PSCache的大小
spring.datasource.poolPreparedStatements=true
spring.datasource.maxPoolPreparedStatementPerConnectionSize=20
# 配置监控统计拦截的filters，去掉后监控界面sql无法统计，'wall'用于防火墙
spring.datasource.filters=stat,wall,log4j
# 通过connectProperties属性来打开mergeSql功能；慢SQL记录
spring.datasource.connectionProperties=druid.stat.mergeSql=true;druid.stat.slowSqlMillis=5000


```

（3）Appliction单元测试类

```java
@Qualifier("dataSource")
@Autowired
DataSource dataSource;
@Test
public void contextLoads() throws SQLException {
   System.out.println("dataSource = " + dataSource.getClass());
   Connection connection = dataSource.getConnection();
   System.out.println(">>>>>>>>>>>>>>>>>>>>>>>>>>connection = " + connection);
   connection.close();
}
```

**（4）配置Druid的监控 （方式一：基于Annotation)**

>  配置监控视图Servlet:DruidStatViewServlet.java
>

   ```java
   @SuppressWarnings("serial")
   @WebServlet(urlPatterns = "/druid/*",
           initParams={
                   @WebInitParam(name="allow",value=""),// IP白名单 (没有配置或者为空，则允许所有访问)
                   @WebInitParam(name="deny",value="192.168.16.111"),// IP黑名单 (存在共同时，deny优先于allow)
                   @WebInitParam(name="loginUsername",value="123"),// 用户名
                   @WebInitParam(name="loginPassword",value="123"),// 密码
                   @WebInitParam(name="resetEnable",value="false")// 禁用HTML页面上的“Reset All”功能
           })
   public class DruidStatViewServlet extends StatViewServlet {
   
   }
   ```

> 配置监控拦截器filter:DruidStatFilter

```java
@WebFilter(filterName="druidWebStatFilter",urlPatterns="/*",
        initParams={
                @WebInitParam(name="exclusions",value="*.js,*.gif,*.jpg,*.bmp,*.png,*.css,*.ico,/druid/*")// 忽略资源
        })
public class DruidStatFilter extends WebStatFilter {

}
```

> 配置数据源。这里相关的参数会自动赋值到datasource里。

~~~java
@Configuration
//标识该类被纳入spring容器中实例化并管理
 @ServletComponentScan
// 用于扫描所有的Servlet、filter、listener
public class DruidConfig {
    @Bean
    @ConfigurationProperties(prefix = "spring.datasource")
    @Primary //在同样的DataSource中，首先使用被标注的DataSource
    //加载时读取指定的配置信息,前缀为spring.datasource.druid
    public DataSource druidDataSource() {

        return new DruidDataSource();
    }
}
~~~

> 启动类 Application.java

~~~java
@ServletComponentScan  // 扫描Servlet，用于扫描与创建Druid后台管理的Servlet，
@SpringBootApplication // SpringBoot项目启动入口
public class SpringboorDatasourceApplication {

   public static void main(String[] args) {
      SpringApplication.run(SpringboorDatasourceApplication.class, args);
   }
}
~~~



**（4）配置Druid的监控 （方式二：基于编程式）**

```java
@Configuration
public class DruidConfiguration {
    @Value("${spring.datasource.url}")
    private String dbUrl;
    @Value("${spring.datasource.username}")
     private String username;
     @Value("${spring.datasource.password}")
    private String password;
     @Value("${spring.datasource.driverClassName}")
     private String driverClassName;
     @Value("${spring.datasource.initialSize}")
     private int initialSize;
     @Value("${spring.datasource.minIdle}")
     private int minIdle;
     @Value("${spring.datasource.maxActive}")
     private int maxActive;
     @Value("${spring.datasource.maxWait}")
     private int maxWait;
     @Value("${spring.datasource.timeBetweenEvictionRunsMillis}")
     private int timeBetweenEvictionRunsMillis;
     @Value("${spring.datasource.minEvictableIdleTimeMillis}")
     private int minEvictableIdleTimeMillis;
     @Value("${spring.datasource.validationQuery}")
     private String validationQuery;
     @Value("${spring.datasource.testWhileIdle}")
     private boolean testWhileIdle;
     @Value("${spring.datasource.testOnBorrow}")
     private boolean testOnBorrow;
     @Value("${spring.datasource.testOnReturn}")
     private boolean testOnReturn;
     @Value("${spring.datasource.poolPreparedStatements}")
     private boolean poolPreparedStatements;
     @Value("${spring.datasource.maxPoolPreparedStatementPerConnectionSize}")
     private int maxPoolPreparedStatementPerConnectionSize;
     @Value("${spring.datasource.filters}")
     private String filters;
     @Value("{spring.datasource.connectionProperties}")
     private String connectionProperties;

 @Bean //声明其为Bean实例
 @Primary //在同样的DataSource中，首先使用被标注的DataSource
 public DataSource dataSource(){
     DruidDataSource datasource = new DruidDataSource();
     datasource.setUrl(this.dbUrl);
     datasource.setUsername(username);
     datasource.setPassword(password);
     datasource.setDriverClassName(driverClassName);

     //configuration
     datasource.setInitialSize(initialSize);
     datasource.setMinIdle(minIdle);
     datasource.setMaxActive(maxActive);
     datasource.setMaxWait(maxWait);
     datasource.setTimeBetweenEvictionRunsMillis(timeBetweenEvictionRunsMillis);
     datasource.setMinEvictableIdleTimeMillis(minEvictableIdleTimeMillis);
     datasource.setValidationQuery(validationQuery);
     datasource.setTestWhileIdle(testWhileIdle);
     datasource.setTestOnBorrow(testOnBorrow);
     datasource.setTestOnReturn(testOnReturn);
     datasource.setPoolPreparedStatements(poolPreparedStatements);
     datasource.setMaxPoolPreparedStatementPerConnectionSize(maxPoolPreparedStatementPerConnectionSize);
     try {
        datasource.setFilters(filters);
     } catch (SQLException e) {
        System.err.println("druid configuration initialization filter: "+ e);
     }
        datasource.setConnectionProperties(connectionProperties);
     return datasource;
     }

     @Bean
     public ServletRegistrationBean statViewServle(){
         ServletRegistrationBean servletRegistrationBean = new ServletRegistrationBean(new StatViewServlet(),"/druid/*");
         // IP白名单
         servletRegistrationBean.addInitParameter("allow","");
         // IP黑名单(共同存在时，deny优先于allow)
         servletRegistrationBean.addInitParameter("deny","192.168.1.100");
         //控制台管理用户
         servletRegistrationBean.addInitParameter("loginUsername","admin");
         servletRegistrationBean.addInitParameter("loginPassword","abc123");
         //是否能够重置数据
         servletRegistrationBean.addInitParameter("resetEnable","false");
         return servletRegistrationBean;
     }

     @Bean
     public FilterRegistrationBean statFilter() {
         FilterRegistrationBean filterRegistrationBean = new FilterRegistrationBean(new WebStatFilter());
         //添加过滤规则
         filterRegistrationBean.addUrlPatterns("/*");
         //忽略过滤的格式
         filterRegistrationBean.addInitParameter("exclusions", "*.js,*.gif,*.jpg,*.png,*.css,*.ico,/druid/*");
         return filterRegistrationBean;
     }
 }
```

创建启动类 

```java
@ServletComponentScan  // 扫描Servlet，用于扫描与创建Druid后台管理的Servlet，
@SpringBootApplication // SpringBoot项目启动入口
public class SpringboorDatasourceApplication {

   public static void main(String[] args) {
      SpringApplication.run(SpringboorDatasourceApplication.class, args);
   }
}
```

现在可以访问Druid的监控平台

http://localhost:8080/druid/login.html

Druid 介绍

https://github.com/alibaba/druid/wiki/%E5%B8%B8%E8%A7%81%E9%97%AE%E9%A2%98



**3.注解说明：**

| 序号 | 注解                                                    | 说明                                                         |
| ---- | ------------------------------------------------------- | ------------------------------------------------------------ |
| 1    | @Configuration                                          | 标识该类被纳入spring容器中实例化并管理，等同于spring的XML配置文件；使用Java代码可以检查类型安全 |
| 2    | @Bean                                                   | 可理解为用spring的时候xml里面的标签                          |
| 3    | @ServletComponentScan(basePackages = { “com.chixing” }) | 扫描工程中的Servlet、Filter、Listener（带注解的）            |
| 4    | @RunWith(SpringJUnit4ClassRunner.class)                 | SpringJUnit支持，由此引入Spring-Test框架支持！               |
| 5    | @SpringApplicationConfiguration(classes = App.class)    | 指定我们SpringBoot工程的Application启动类（App是项目的启动类） |
| 6    | @WebAppConfiguration                                    | 由于是Web项目，Junit需要模拟ServletContext，因此我们需要给我们的测试类加上@WebAppConfiguration。 |
| 7    | @Value(“${application.username:QiuRiMangCao}”           | 使用@value注解，从application.properties配置文件读取值，没读取到就用默认值 |
| 8    | @Primary                                                | 注解的实例优先于其他实例被注入                               |
| 9    | @ConfigurationProperties                                | 可以把同类的配置信息自动封装成实体类                         |
| 10   | @WebServlet                                             | 标记为servlet，以便启动器扫描。                              |
| 11   | @WebFilter                                              | 标记为Filter，以便启动器扫描。                               |

