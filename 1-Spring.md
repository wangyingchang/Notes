#### Spring  简介

**1. Spring 概述?**

Spring 是最受欢迎的企业级 Java 应用程序开发框架，数以百万的来自世界各地的开发人员使用 Spring 框架来创建性能好、易于测试、可重用的代码。

Spring 框架是一个开源的 Java 平台，它最初是由 Rod Johnson 编写的，并且于 2003 年 6 月首次在 Apache 2.0 许可下发布。

Spring 是轻量级的框架，其基础版本只有 2 MB 左右的大小。

轻量级：Spring是非侵入性的--基于Spring开发的应用中的对象可以不依赖于Spring的API

Spring 框架的核心特性是可以用于开发任何 Java 应用程序，但是在 Java EE 平台上构建 web 应用程序是需要扩展的。 Spring 框架的目标是使 J2EE 开发变得更容易使用，通过启用基于 POJO 编程模型来促进良好的编程实践。

Spring是一个开源框架

Spring为简化企业级应用开发而生，使用Spring可以使简单的JavaBean实现以前知有EJB才能实现的功能

Spring是一个IOC(DI)和AOP容器框架

容器：Spring是一个容器,因为它包含并且管理应用对象的生命周期

框架:Spring实现了使用简单的组件配置组合成一个复杂的应用；在Spring中可以使用XML和Java注解组合这些对象

一站式：在IOC和AOP的基础上可以整合各企业应用的开源框架和优秀的第三方类库（实际上Spring自身也提供了展现层的SpringMVC和持久层的Spring JDBC）

**2. Spring 优点？**

下面列出的是使用 Spring 框架主要的好处：

- Spring 可以使开发人员使用 POJOs 开发企业级的应用程序。只使用 POJOs 的好处是你不需要一个 EJB 容器产品，比如一个应用程序服务器，但是你可以选择使用一个健壮的 servlet 容器，比如 Tomcat 或者一些商业产品。
- Spring 在一个单元模式中是有组织的。即使包和类的数量非常大，你只要担心你需要的，而其它的就可以忽略了。
- Spring 不会让你白费力气做重复工作，它真正的利用了一些现有的技术，像ORM 框架、日志框架、JEE、Quartz 和 JDK 计时器，其他视图技术。
- 测试一个用 Spring 编写的应用程序很容易，因为环境相关的代码被移动到这个框架中。此外，通过使用 JavaBean-style POJOs，它在使用依赖注入注入测试数据时变得更容易。
- Spring 的 web 框架是一个设计良好的 web MVC 框架，它为比如 Structs 或者其他工程上的或者不怎么受欢迎的 web 框架提供了一个很好的供替代的选择。
- Spring 对JavaEE开发中非常难用的一些API（JDBC、JavaMail、远程调用等），都提供了封装，使这些API应用难度大大降低。
- 轻量级的 IOC 容器往往是轻量级的，例如，特别是当与 EJB 容器相比的时候。这有利于在内存和 CPU 资源有限的计算机上开发和部署应用程序。
- Spring提供了一致的事务管理接口，可向下扩展到（使用一个单一的数据库，例如）本地事务并扩展到全局事务（例如，使用 JTA）。

**3. 控制反转（IOC）的依赖注入（DI:dependency injection）**

Spring 最认同的技术是**控制反转(IOC)**的**依赖注入（DI）**模式。控制反转（IoC）是一个通用的概念，它可以用许多不同的方式去表达，依赖注入仅仅是控制反转的一个具体的例子。

当编写一个复杂的 Java 应用程序时，应用程序类应该尽可能的独立于其他的 Java 类来增加这些类可重用可能性，当进行单元测试时，可以使它们独立于其他类进行测试。依赖注入（或者有时被称为配线）有助于将这些类粘合在一起，并且在同一时间让它们保持独立。

到底什么是依赖注入？让我们将这两个词分开来看一看。这里将依赖关系部分转化为两个类之间的关联。例如，类 A 依赖于类 B。现在，让我们看一看第二部分，注入。所有这一切都意味着类 B 将通过 IoC 被注入到类 A 中。

依赖注入可以以向构造函数传递参数的方式发生，或者通过使用 setter 方法 post-construction。由于依赖注入是 Spring 框架的核心部分，所以我将在一个单独的章节中利用很好的例子去解释这一概念。

**4. 面向切面编程（AOP:aspect oriented programming）**：

Spring 框架的一个关键组件是**面向方面的程序设计（AOP）**框架。一个程序中跨越多个点的功能被称为**横切关注点**，这些横切关注点在概念上独立于应用程序的业务逻辑。有各种各样常见的很好的关于方面的例子，比如日志记录、声明性事务、安全性，和缓存等等。

在 OOP 中模块化的关键单元是类，而在 AOP 中模块化的关键单元是方面。AOP 帮助你将横切关注点从它们所影响的对象中分离出来，然而依赖注入帮助你将你的应用程序对象从彼此中分离出来。

Spring 框架的 AOP 模块提供了面向方面的程序设计实现，可以定义诸如方法拦截器和切入点等，从而使实现功能的代码彻底的解耦出来。使用源码级的元数据，可以用类似于.Net属性的方式合并行为信息到代码中。





#### Spring 体系结构

**1.概念**

Spring 有可能成为所有企业应用程序的一站式服务点，然而，Spring 是模块化的，允许你挑选和选择适用于你的模块，不必要把剩余部分也引入。

![Spring 体系结构](https://7n.w3cschool.cn/attachments/image/wk/wkspring/arch1.png)

**2.核心容器**

核心容器由**spring-core，spring-beans，spring-context，spring-context-support和spring-expression**（SpEL，Spring表达式语言，Spring Expression Language）等模块组成，它们的细节如下：

- **spring-core**模块提供了框架的基本组成部分，包括 IoC 和依赖注入功能。
- **spring-beans** 模块提供 BeanFactory，工厂模式的微妙实现，它移除了编码式单例的需要，并且可以把配置和依赖从实际编码逻辑中解耦。
- **context**模块建立在由**core**和 **beans** 模块的基础上建立起来的，它以一种类似于JNDI注册的方式访问对象。Context模块继承自Bean模块，并且添加了国际化（比如，使用资源束）、事件传播、资源加载和透明地创建上下文（比如，通过Servelet容器）等功能。Context模块也支持Java EE的功能，比如EJB、JMX和远程调用等。**ApplicationContext**接口是Context模块的焦点。**spring-context-support**提供了对第三方库集成到Spring上下文的支持，比如缓存（EhCache, Guava, JCache）、邮件（JavaMail）、调度（CommonJ, Quartz）、模板引擎（FreeMarker, JasperReports, Velocity）等。
- **spring-expression**模块提供了强大的表达式语言，用于在运行时查询和操作对象图。它是JSP2.1规范中定义的统一表达式语言的扩展，支持set和get属性值、属性赋值、方法调用、访问数组集合及索引的内容、逻辑算术运算、命名变量、通过名字从Spring IoC容器检索对象，还支持列表的投影、选择以及聚合等。

**3.数据访问层**

数据访问/集成层包括 **JDBC**，**ORM**，**OXM**，**JMS** 和**事务处理**模块，它们的细节如下：

（注：JDBC=Java Data Base Connectivity，ORM=Object Relational Mapping，OXM=Object XML Mapping，JMS=Java Message Service）

- **JDBC** 模块提供了JDBC抽象层，它消除了冗长的JDBC编码和对数据库供应商特定错误代码的解析。
- **ORM** 模块提供了对流行的对象关系映射API的集成，包括JPA、JDO和Hibernate等。通过此模块可以让这些ORM框架和spring的其它功能整合，比如前面提及的事务管理。
- **OXM** 模块提供了对OXM实现的支持，比如JAXB、Castor、XML Beans、JiBX、XStream等。
- **JMS** 模块包含生产（produce）和消费（consume）消息的功能。从Spring 4.1开始，集成了spring-messaging模块。。
- **事务**模块为实现特殊接口类及所有的 POJO 支持编程式和声明式事务管理。（注：编程式事务需要自己写beginTransaction()、commit()、rollback()等事务管理方法，声明式事务是通过注解或配置由spring自动处理，编程式事务粒度更细）

**4.web层**

Web 层由 Web，Web-MVC，Web-Socket 和 Web-Portlet 组成，它们的细节如下：

- **Web** 模块提供面向web的基本功能和面向web的应用上下文，比如多部分（multipart）文件上传功能、使用Servlet监听器初始化IoC容器等。它还包括HTTP客户端以及Spring远程调用中与web相关的部分。。
- **Web-MVC** 模块为web应用提供了模型视图控制（MVC）和REST Web服务的实现。Spring的MVC框架可以使领域模型代码和web表单完全地分离，且可以与Spring框架的其它所有功能进行集成。
- **Web-Socket** 模块为 WebSocket-based 提供了支持，而且在 web 应用程序中提供了客户端和服务器端之间通信的两种方式。
- **Web-Portlet** 模块提供了用于Portlet环境的MVC实现，并反映了spring-webmvc模块的功能。





#### Spring HelloWorld

**1.创建javaweb项目**

**2.导入核心架包**

架包下载地址：<http://repo.spring.io/release/org/springframework/spring>

新建目录lib导入架包

**3.创建文件**

HelloWorld.java(**src/com/spring/test**)

~~~java
public class HelloWorld {
   private String message;
   public void setMessage(String message){
      this.message  = message;
   }
   public void getMessage(){
      System.out.println("Your Message : " + message);
   }
}
~~~

MainApp.java(**src/com/spring/test**)

~~~java
public class MainApp {
   public static void main(String[] args) {
       //等价于 HelloWorld helloWorld=new HelloWorld();
       //1.创建Spring的IOC的容器对象
      ApplicationContext atc = new ClassPathXmlApplicationContext("applicationContenxt.xml");
       //2.从IOC容器中获取的bean对象
      HelloWorld obj = (HelloWorld) atc.getBean("helloWorld");
       //3.调用方法
      obj.getMessage();
   }
}
//第一步是我们使用框架 API ClassPathXmlApplicationContext() 来创建应用程序的上下文。这个 API 加载 beans 的配置文件并最终基于所提供的 API，它处理创建并初始化所有的对象，即在配置文件中提到的 beans。
//第二步是使用已创建的上下文的 getBean() 方法来获得所需的 bean。这个方法使用 bean 的 ID 返回一个最终可以转换为实际对象的通用对象。一旦有了对象，你就可以使用这个对象调用任何类的方法。
~~~

applicationContext.xml(**src目录下**)

~~~xml
<?xml version="1.0" encoding="UTF-8"?>

<beans xmlns="http://www.springframework.org/schema/beans"
    xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
    xsi:schemaLocation="http://www.springframework.org/schema/beans
    http://www.springframework.org/schema/beans/spring-beans-3.0.xsd">

   <!--注入HelloWorld类-->
   <bean id="helloWorld" class="com.spring.test">
       <property name="message" value="Hello World!"/>
   </bean>

</beans>
~~~



#### Spring IOC容器

**IoC 容器**

Spring 容器是 Spring 框架的核心。容器将创建对象，把它们连接在一起，配置它们，并管理他们的整个生命周期从创建到销毁。Spring 容器使用依赖注入（DI）来管理组成一个应用程序的组件，这些对象被称为 Spring Beans。

通过阅读配置元数据提供的指令，容器知道对哪些对象进行实例化，配置和组装。配置元数据可以通过 XML，Java 注释或 Java 代码来表示。下图是 Spring 如何工作的高级视图。 Spring IoC 容器利用 Java 的 POJO 类和配置元数据来生成完全配置和可执行的系统或应用程序。

IOC 容器具有依赖注入功能的容器，它可以创建对象，IOC 容器负责实例化、定位、配置应用程序中的对象及建立这些对象间的依赖。通常new一个实例，控制权由程序员控制，而"控制反转"是指new实例工作不由程序员来做而是交给Spring容器来做。在Spring中BeanFactory是IOC容器的实际代表者。

**Spring 提供了以下两种不同类型的容器**

| 序号 | 容器 & 描述                                                  |
| ---- | ------------------------------------------------------------ |
| 1    | Spring **BeanFactory** 容器它是最简单的容器，给 DI 提供了基本的支持，它用 org.springframework.beans.factory.BeanFactory 接口来定义。BeanFactory 或者相关的接口，如 BeanFactoryAware，InitializingBean，DisposableBean，在 Spring 中仍然存在具有大量的与 Spring 整合的第三方框架的反向兼容性的目的。 |
| 2    | Spring **ApplicationContext** 容器该容器添加了更多的企业特定的功能，例如从一个属性文件中解析文本信息的能力，发布应用程序事件给感兴趣的事件监听器的能力。该容器是由 org.springframework.context.ApplicationContext 接口定义。 |

ApplicationContext 容器包括 BeanFactory 容器的所有功能，所以通常建议超过 BeanFactory。BeanFactory 仍然可以用于轻量级的应用程序，如移动设备或基于 applet 的应用程序，其中它的数据量和速度是显著。



**1.Spring BeanFactory 容器**

这是一个最简单的容器，它主要的功能是为依赖注入 （DI） 提供支持，这个容器接口在 org.springframework.beans.factory.BeanFactor 中被定义。BeanFactory 和相关的接口，比如BeanFactoryAware、DisposableBean、InitializingBean，仍旧保留在 Spring 中，主要目的是向后兼容已经存在的和那些 Spring 整合在一起的第三方框架。

在 Spring 中，有大量对 BeanFactory 接口的实现。其中，最常被使用的是 **XmlBeanFactory** 类。这个容器从一个 XML 文件中读取配置元数据，由这些元数据来生成一个被配置化的系统或者应用。

在资源宝贵的移动设备或者基于 applet 的应用当中， BeanFactory 会被优先选择。否则，一般使用的是 ApplicationContext，除非你有更好的理由选择 BeanFactory。

下面是文件 **HelloWorld.java** 的内容：

```java
package com.tutorialspoint;
public class HelloWorld {
   private String message;
   public void setMessage(String message){
    this.message  = message;
   }
   public void getMessage(){
    System.out.println("Your Message : " + message);
   }
}
```

下面是文件 **MainApp.java** 的内容：

```java
package com.tutorialspoint;
import org.springframework.beans.factory.InitializingBean;
import org.springframework.beans.factory.xml.XmlBeanFactory;
import org.springframework.core.io.ClassPathResource;
public class MainApp {
   public static void main(String[] args) {
      XmlBeanFactory factory = new XmlBeanFactory
                             (new ClassPathResource("Beans.xml"));
      HelloWorld obj = (HelloWorld) factory.getBean("helloWorld");
      obj.getMessage();
   }
}
```

在主程序当中，我们需要注意以下两点：

- 第一步利用框架提供的 **XmlBeanFactory()** API 去生成工厂 bean 以及利用 **ClassPathResource()** API 去加载在路径 CLASSPATH 下可用的 bean 配置文件。**XmlBeanFactory()** API 负责创建并初始化所有的对象，即在配置文件中提到的 bean。
- 第二步利用第一步生成的 bean 工厂对象的 **getBean()** 方法得到所需要的 bean。 这个方法通过配置文件中的 bean ID 来返回一个真正的对象，该对象最后可以用于实际的对象。一旦得到这个对象，你就可以利用这个对象来调用任何方法。





#### Spring 配置文件

**1.applicationContext.xml**

~~~xml
<?xml version="1.0" encoding="UTF-8"?>

<beans xmlns="http://www.springframework.org/schema/beans" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xmlns:p="http://www.springframework.org/schema/p" xmlns:aop="http://www.springframework.org/schema/aop"
       xmlns:context="http://www.springframework.org/schema/context" xmlns:jee="http://www.springframework.org/schema/jee"
       xmlns:tx="http://www.springframework.org/schema/tx"
       xmlns:mvc="http://www.springframework.org/schema/mvc"
       xsi:schemaLocation="
			http://www.springframework.org/schema/mvc http://www.springframework.org/schema/mvc/spring-mvc.xsd
			http://www.springframework.org/schema/aop http://www.springframework.org/schema/aop/spring-aop-2.5.xsd
			http://www.springframework.org/schema/beans http://www.springframework.org/schema/beans/spring-beans-2.5.xsd
			http://www.springframework.org/schema/context http://www.springframework.org/schema/context/spring-context-2.5.xsd
			http://www.springframework.org/schema/jee http://www.springframework.org/schema/jee/spring-jee-2.5.xsd
			http://www.springframework.org/schema/tx http://www.springframework.org/schema/tx/spring-tx-2.5.xsd">
    

    <!-- 引入注解 -->
    <context:annotation-config></context:annotation-config>
    <context:component-scan base-package="com.spring"></context:component-scan>


    <!-- 引入数据库配置文件(dbconn.properties) -->
    <context:property-placeholder location="dbconn.properties"/>
    <!-- 注入数据源对象(DataSource) -->
    <bean id="dataSource" class="org.springframework.jdbc.datasource.DriverManagerDataSource" >
        <property name="driverClassName" value="${driver}"></property>
        <property name="url" value="${url}"> </property>
        <property name="username" value="${user}"></property>
        <property name="password" value="${password}"></property>
    </bean>


    <!-- 注入JDBC模板对象(JdbcTemplate),依赖于数据源对象(DataSource)(setter注入，构造器注入)-->
    <bean id="jdbcTemplate" class="org.springframework.jdbc.core.JdbcTemplate">
        <property name="dataSource" ref="dataSource"></property>
    </bean>


    <!-- Spring 整合 MyBatis 依赖架包：mybatis-spring.jar-->
    <!-- 注入MyBatis的SqlSessionFactory对象,依赖于DataSource，MyBatis配置文件,Mapper配置文件-->
    <bean id="sqlSessionFactory"   class="org.mybatis.spring.SqlSessionFactoryBean">
        <property name="dataSource" ref="dataSource"></property>
        <property name="configLocation" value="mybatis-config.xml"></property>
        <property name="mapperLocations" value="mapper/*Mapper.xml"></property>
    </bean>
    <!-- 第一种方式：基于是实现类-->
    <bean id="sqlSessionTemplate" class="org.mybatis.spring.SqlSessionTemplate">
        <constructor-arg   ref="sqlSessionFactory"></constructor-arg>
    </bean>
    <!-- 第二种方式：基于DAO接口扫描，实际内部还是依赖于SqlSessionTemplate-->
    <bean id="mapperScannerConfigurer" class="org.mybatis.spring.mapper.MapperScannerConfigurer">
        <property name="basePackage" value="com.spring.dao"></property>
        <property name="sqlSessionFactoryBeanName" value="sqlSessionFactory"></property>
    </bean>



    <!-- 事务管理 AOP -->
    <bean id="transactionManager" class="org.springframework.jdbc.datasource.DataSourceTransactionManager">
        <property name="dataSource" ref="dataSource"></property>
    </bean>
    <!-- 通过AOP实现 事务的管理横切到业务中 -->
    <aop:config>
        <!-- -->
        <aop:pointcut id="transactionPC" expression="execution(* com.spring.service..*.*(..))" ></aop:pointcut>
        <aop:advisor advice-ref="tx" pointcut-ref="transactionPC"/>
    </aop:config>
    <!-- 配置事务的传播性 -->
    <tx:advice id="tx" transaction-manager="transactionManager">
        <tx:attributes>
            <tx:method name="save*" propagation="REQUIRED"/>
            <tx:method name="update*" propagation="REQUIRED"/>
            <tx:method name="delete*" propagation="REQUIRED"/>
            <tx:method name="get*" propagation="REQUIRED" read-only="true"/>
        </tx:attributes>
    </tx:advice>

</beans>

~~~



