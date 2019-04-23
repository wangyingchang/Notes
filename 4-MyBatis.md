#### 1.MyBatis的简介

(1).MyBatis与hibernate

hibernate:全自动ORM(Object Relation)框架,旨在消除sql(缺陷在于优化sql困难,需要学习HQL).洗衣机全部甩干

MyBatis:半自动ORM,轻量级框架,旨在让sql存在配置文件中,使sql与java编码分离,sql是开发人员控制(掌握).某些衣服不想要洗衣机甩干.

(2).MyBatis官网定义:

MyBatis 是一款优秀的持久层框架,是apache下的顶级项目，它支持定制化 SQL、存储过程以及高级映射。

MyBatis 避免了几乎所有的 JDBC 代码和手动设置参数以及获取结果集。MyBatis 可以使用简单的 XML 或注解来配置和映射原生信息，将接口和 Java 的 POJOs(Plain Old Java Objects,普通的 Java对象)映射成数据库中的记录。 

mybatis可以将preparedStatement中的输入参数,自动进行输入映射,将查询结果集灵活映射成Java对象.



#### 2.MyBatis的下载安装

(1). 下载

https://github.com/mybatis/mybatis-3/tree/master/src/site

mybatis-3.4.6.zip

(2). 安装

- 要使用 MyBatis， 只需将 [mybatis-x.x.x.jar](https://github.com/mybatis/mybatis-3/releases) 文件导入项目中;
- 如果使用 Maven 来构建项目，则需将下面的 dependency 代码置于 pom.xml 文件中:

~~~xml
<dependency>
  <groupId>org.mybatis</groupId>
  <artifactId>mybatis</artifactId>
  <version>x.x.x</version>
</dependency>
~~~



#### 3.MyBtis构建SqlSession

(1). XML 配置文件（configuration XML）中包含了对 MyBatis 系统的核心设置，包含获取数据库连接实例的数据源（DataSource）和决定事务作用域和控制方式的事务管理器（TransactionManager）`mybatis_config.xml`

```xml
<?xml version="1.0" encoding="UTF-8"?>
<!--文件类型定义-->
<!DOCTYPE configuration PUBLIC "-//mybatis.org//DTD Config 3.0//EN" "http://mybatis.org/dtd/mybatis-3-config.dtd">
<!--配置-->
<configuration>
    <environments default="development">
        <environment id="development">
            <!--事务管理-->
            <transactionManager type="JDBC">
            </transactionManager>
            <!-- 配置数据库连接信息 -->
            <dataSource type="POOLED">
                <property name="driver" value="com.mysql.jdbc.Driver" />
                <property name="url" value="jdbc:mysql://localhost:3306/cart?useSSL=false" />
                <property name="username" value="root" />
                <property name="password" value="123456" />
            </dataSource>
        </environment>
    </environments>
    <!--导入mapper文件 -->
    <mappers>
        <mapper resource="com/mybatis/mapper/UserInfoMapper.xml"/>
    </mappers>
</configuration>
```

(2).  每个基于 MyBatis 的应用都是以一个 SqlSessionFactory 的实例为中心的;SqlSessionFactory 的实例可以通过 SqlSessionFactoryBuilder 获得;而 SqlSessionFactoryBuilder 则可以从 XML 配置文件或一个预先定制的 Configuration 的实例构建出 SqlSessionFactory 的实例从 XML 文件中构建 SqlSessionFactory 的实例非常简单，建议使用类路径下的资源文件进行配置;但是也可以使用任意的输入流(InputStream)实例，包括字符串形式的文件路径或者 file:// 的 URL 形式的文件路径来配置;MyBatis 包含一个名叫 Resources 的工具类，它包含一些实用方法，可使从 classpath 或其他位置加载资源文件更加容易。

```java
String resource = "mybatis-config.xml的路径";
InputStream inputStream = Resources.getResourceAsStream(resource);
SqlSessionFactory sqlSessionFactory = new SqlSessionFactoryBuilder().build(inputStream);
```

(3). 从 SqlSessionFactory 中获取 SqlSession;既然有了 SqlSessionFactory ，顾名思义，我们就可以从中获得 SqlSession 的实例了。SqlSession 完全包含了面向数据库执行 SQL 命令所需的所有方法。你可以通过 SqlSession 实例来直接执行已映射的 SQL 语句。例如：

```java
SqlSession session = sqlSessionFactory.openSession();
try {
  Blog blog = (Blog) session.selectOne("org.mybatis.example.BlogMapper.selectBlog", 101);
} finally {
  session.close();
}
```





#### 4.MyBatis的HelloWorld

(1). 添加mybatis.jar以及mysql的驱动包

> 导入mybatis和mysql的jar包 

(2). 创建数据的表

~~~mysql
create table t_person(
id int not null primary key auto_increment,
name varchar(20),
age varchar(20)
);
~~~

(3). 编写与表对应的实体类

~~~java
public class Person {
 private Integer id;
 private String name;
 private String age;
 public Integer getId() {
  return id;
 }
 public void setId(Integer id) {
  this.id = id;
 }
 public String getName() {
  return name;
 }
 public void setName(String name) {
  this.name = name;
 }
 public String getAge() {
  return age;
 }
 public void setAge(String age) {
  this.age = age;
 }
}
~~~

(4). 编写连接数据库的配置文件mybatis_config.xml

~~~xml
<?xml version="1.0" encoding="UTF-8" ?>    
<!--约束文件-->
<!DOCTYPE configuration PUBLIC "-//mybatis.org//DTD Config 3.0//EN" "http://mybatis.org/dtd/mybatis-3-config.dtd">
<configuration>
 <typeAliases>
  <!--给实体类起一个别名 user -->
  <typeAlias type="com.evan.entity.Person" alias="Person" />
 </typeAliases>
 <!--数据源配置 这块用 mysql数据库 -->
 <environments default="development">
  <environment id="development">
   <transactionManager type="jdbc" />
   <dataSource type="POOLED">
    <property name="driver" value="com.mysql.jdbc.Driver" />
    <property name="url" value="jdbc:mysql://localhost:3306/数据库名" />
    <property name="username" value="root" />
    <property name="password" value="123456" />
   </dataSource>
  </environment>
 </environments>
 <mappers>
  <!--将我们写好的sql映射文件(personMapper.xml)一定要注册到配置文件中-->
  <mapper resource="mybatis/personMapper.xml" />
 </mappers>
</configuration> 
~~~

(5). 编写PersonMapper接口

~~~java
public interface PersonMapper {
 public Person findById(Integer id );
}
~~~

(6). 编写PersonMapper的实现，personMapper.xml文件

~~~xml
<?xml version="1.0" encoding="UTF-8" ?> 
<!DOCTYPE mapper PUBLIC  
    "-//mybatis.org//DTD Mapper 3.0//EN" 
    "http://mybatis.org/dtd/mybatis-3-mapper.dtd">
<mapper namespace="com.evan.dao.PersonMapper">
 <!-- findById必须和接口中的方法名一样 返回一个User 就是刚才的别名 如果不弄别名要连类路径一起写 麻烦 -->
 <select id="findById" parameterType="HashMap" resultType="Person">
  select* from t_person where id=#{id}
 </select>
</mapper>  
~~~

(7). 编写测试文件

~~~java
import java.io.IOException;
import org.apache.ibatis.io.Resources;
import org.apache.ibatis.session.SqlSession;
import org.apache.ibatis.session.SqlSessionFactory;
import org.apache.ibatis.session.SqlSessionFactoryBuilder;
import com.evan.dao.PersonMapper;
import com.evan.entity.Person;
 
public class MybatisTest {
 /**
  * 获得MyBatis SqlSessionFactory
  * SqlSessionFactory负责创建SqlSession，一旦创建成功，就可以用SqlSession实例来执行映射语句
  * ，commit，rollback，close等方法。
  * @return
  */
 private static SqlSessionFactory getSessionFactory() {
     SqlSessionFactory sessionFactory = null;
     //mybatis-config.xml的路径
     String resource = "mybatis_config.xml";
  try {
   sessionFactory = new SqlSessionFactoryBuilder().build(Resources
     .getResourceAsReader(resource));
  } catch (IOException e) {
   // TODO Auto-generated catch block
   e.printStackTrace();
  }
  return sessionFactory;
 }
 
 public static void main(String[] args) {
  SqlSession sqlSession = getSessionFactory().openSession();
  PersonMapper personMapper = sqlSession.getMapper(PersonMapper.class);
  Person person = personMapper.findById(1);
  System.out.println(person.getName());
  sqlSession.close();
 }
}
~~~



#### 5.MyBatis的全局配置文件

##### (1). dtd约束

##### (2). properties外部配置文件

##### (3). settings运行时行为设置

##### (4). typeAliases别名

##### (5). typeHandlers类型处理器简介

##### (6). plugins插件简介

##### (7). enviroments运行环境

##### (8). databaseIdProvider多数据库支持

##### (9). mappers_sql映射注册

##### (10). objectFactory对象工厂



#### 6.MyBatis的映射文件

##### (1). 增删改查

##### (2). insert获取自增主键的值

##### (3). insert获取非自增主键的值selectKey

##### (4). 传参方式

- 多个参数的传递方式

GoodMapper.java：

```java
public Good selectGood(String id, String name);
```

GoodMapper.xml : 

```xml
<select id="selectGood" resultMap="GoodMap">
    select * from good where id = #{0} and name=#{1}
</select>
<!--  注： #{0} 代表的是第一个参数，#{1} 代表的是第二个参数，以此类推 -->
```

- 利用注解的传递方式

GoodMapper.java :

```java
public Good selectGood(@param("id")String id,@param("name")String name);
```

GoodMapper.xml : 

```xml
<select id="selectGood" resultMap="GoodMap">
    select * from good where id = #{id} and name=#{name}
</select>
<!-- 注：此种方式对于参数来说就比较直观-->
```

- 利用map的传递方式 

 GoodMapper.java： 

```java
public Good selectGood(Map map);
```

 GoodMapper.xml : 

```xml
<select id="selectGood" resultMap="GoodMap">
    select * from good where id = #{id} and name=#{name}
</select>
```

GoodService.java : 

```java
public Good selectGood(Map map);
```

GoodServiceImpl.java : 

```java
 public Good selectGood(){
     Map map = new HashMap();
     map.put("id",1);
     map.put("name",zhangsan);
     Good good = goodService.selectGood(map);
     return good;
   }
//注：此种方式以map的形式来传入需要的参数，当参数较多时，使用此种方式比较方便在mybatis相关的实际项目开发中使用此种方式比较多。建议使用此种方式-->
```

##### (5).返回类型

- 分类与返回参数:

(1). resultMap:结果集[对象等] 

(2).resultType:Integer,String ,Long ,class

- 注意点:

在MyBatis进行查询映射时，其实查询出来的每一个属性都是放在一个对应的Map里面的，其中键是属性名，值则是其对应的值;

--当提供的返回类型属性是resultType时，MyBatis会将Map里面的键值对取出赋给resultType所指定的对象对应的属性。所以其实MyBatis的每一个查询映射的返回类型都是ResultMap，只是当提供的返回类型属性是resultType的时 候，MyBatis对自动的给把对应的值赋给resultType所指定对象的属性;

--当提供的返回类型是resultMap时，因为Map不能很好表示领域模型，就需要自己再进一步的把它转化为对应的对象，这常常在复杂查询中很有作用;

- 实例

resultMap案例

```xml
	<resultMap id="UserMap" type="com.mybatis.pojo.UserInfo">
		<id property="userId" column="user_id"/>
		<result property="userName" column="user_name"/>
		<result property="userAge" column="user_age"/>
		<result property="userSex" column="user_sex"/>
		<result property="userPhone" column="user_phone"/>
		<result property="userCardId" column="user_card_id"/>
		<result property="userEmail" column="user_email"/>
		<result property="userCreateTime" column="user_create_time"/>
		<result property="userUpdateTime" column="user_update_time"/>
	</resultMap>	
    	<!--根据主键查询-->
	<select id="queryById" resultMap="UserMap" parameterType="java.lang.String">
		select *
		from user_info
		where user_id=#{userId}
	</select>
```

resultType--class案例:查询结果对应类中的属性值 

```xml
<!--根据姓名模糊查询-->
	<select id="queryByName" resultType="com.mybatis.pojo.UserInfo" parameterType="java.lang.String">
        select *
		from user_info
		where user_name like  "%"#{userName}"%"
	</select>

    <!--mybatis-config.xml文件需要添加以下配置-->
    <!--自动驼峰映射-->
    <settings>
        <setting name="mapUnderscoreToCamelCase" value="true"/>
    </settings>
```

##### (6). #与$区别

##### (7). select返回List

##### (8). select_resultMap自定义结果映射

##### (9). 关联查询_association

##### (10). 关联查询_collection

##### (11). 延迟加载

#### 7.MyBatis的动态sql

##### (1). 简介

##### (2). if判断&OGNL

##### (3). where条件查询

##### (4). trim自定义字符串截取

##### (5). choose分支选择

##### (6). set与if结合的动态更新

##### (7). foreach遍历集合

##### (8). mysql下foreach批量插入的两种方式

##### (9). 内置参数_parameter&_databaseId

##### (10). bind_绑定

##### (11). 抽取可重用的sql片段



#### 8.MyBatis的缓存

##### (1). 缓存简介

mybatis提供查询缓存，用于减轻数据压力，提高数据库性能;

mybaits提供一级缓存，和二级缓存;

![1](E:\MyBatis\img\1.png)

一级缓存是SqlSession级别的缓存,在操作数据库时需要构造sqlSession对象，在对象中有一个数据结构（HashMap）用于存储缓存数据,不同的sqlSession之间的缓存数据区域（HashMap）是互相不影响的;

二级缓存是mapper级别的缓存，多个SqlSession去操作同一个Mapper的sql语句，多个SqlSession可以共用二级缓存，二级缓存是跨SqlSession的;

为什么要用缓存？

如果缓存中有数据就不用从数据库中获取，大大提高系统性能。



##### (2). 一级缓存

- 工作原理

第一次发起查询用户id为1的用户信息，先去找缓存中是否有id为1的用户信息，如果没有，从数据库查询用户信息。得到用户信息，将用户信息存储到一级缓存中。

如果sqlSession去执行commit操作（执行插入、更新、删除），清空SqlSession中的一级缓存，这样做的目的为了让缓存中存储的是最新的信息，避免脏读。

第二次发起查询用户id为1的用户信息，先去找缓存中是否有id为1的用户信息，缓存中有，直接从缓存中获取用户信息。

![2](E:\MyBatis\img\2.png)

- 案例

mybatis默认支持一级缓存，不需要在配置文件去配置 

- 应用

正式开发，是将mybatis和spring进行整合开发，事务控制在service中。

一个service方法中包括 很多mapper方法调用。

```java
service{
         //开始执行时，开启事务，创建SqlSession对象
         //第一次调用mapper的方法findUserById(1)
         //第二次调用mapper的方法findUserById(1)，从一级缓存中取数据
         //方法结束，sqlSession关闭
}
```

如果是执行两次service调用查询相同的用户信息，不走一级缓存，因为session方法结束，sqlSession就关闭，一级缓存就清空。



##### (3). 二级缓存

##### (4). 缓存有关的设置及属性

##### (5). MaBatis整合ehcache

> java中主流缓存的区别:ehcache oscache  memcached redis

- 导入ehcache相关jar包

​       ehcache:3.5.2.jar(包含了slf4j-api)

​       mybatis-ehcache:1.1.0.jar(包含了slf4j-api)

- 配置ehcache.xml文件

```xml
<ehcache xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xsi:noNamespaceSchemaLocation="/com/mybatis/config/ehcache.xsd">
    <!--xsd文件是enchache:3.5.2.jar包含的文件格式-->
    
    <!--表示硬盘上保存缓存的位置,默认是临时文件夹-->
    <diskStore path="D:\mybatis\ehcache"/>
    <defaultCache
            maxElementsInMemory="10000"
            eternal="false"
            timeToIdleSeconds="120"
            timeToLiveSeconds="120"
            maxElementsOnDisk="10000000"
            diskExpiryThreadIntervalSeconds="120"
            memoryStoreEvictionPolicy="LRU">
        <persistence strategy="localTempSwap"/>
    </defaultCache>
</ehcache>
```

> 属性说明：
>  diskStore：指定数据在磁盘中的存储位置。
>  defaultCache：当借助CacheManager.add("demoCache")创建Cache时，EhCache便会采用\<defalutCache/>指定的的管理策略
> 以下属性是必须的：
>  maxElementsInMemory - 在内存中缓存的element的最大数目 
>  maxElementsOnDisk - 在磁盘上缓存的element的最大数目，若是0表示无穷大
>  eternal - 设定缓存的elements是否永远不过期。如果为true，则缓存的数据始终有效，如果为false那么还要根据timeToIdleSeconds，timeToLiveSeconds判断
>  overflowToDisk - 设定当内存缓存溢出的时候是否将过期的element缓存到磁盘上
> 以下属性是可选的：
>  timeToIdleSeconds - 当缓存在EhCache中的数据前后两次访问的时间超过timeToIdleSeconds的属性取值时，这些数据便会删除，默认值是0,也就是可闲置时间无穷大
>  timeToLiveSeconds - 缓存element的有效生命期，默认是0.,也就是element存活时间无穷大
> diskSpoolBufferSizeMB 这个参数设置DiskStore(磁盘缓存)的缓存区大小.默认是30MB.每个Cache都应该有自己的一个缓冲区.
>  diskPersistent - 在VM重启的时候是否启用磁盘保存EhCache中的数据，默认是false。
>  diskExpiryThreadIntervalSeconds - 磁盘缓存的清理线程运行间隔，默认是120秒。每个120s，相应的线程会进行一次EhCache中数据的清理工作
>  memoryStoreEvictionPolicy - 当内存缓存达到最大，有新的element加入的时候， 移除缓存中element的策略。默认是LRU（最近最少使用），可选的有LFU（最不常使用）和FIFO（先进先出）

- 开启mybatis的二级缓存

```xml
<settings>
<!-- 开启二级缓存 -->
<setting name="cacheEnabled" value="true"/>
</settings>
```

- 在UserMapper.xml中开启二缓存，UserMapper.xml下的sql执行完成会存储到它的缓存区域（HashMap）

```xml
<mapper namespace="com.mybatis.mapper.GoodsMapper">
<!--这里引用第三方缓存（或自定义缓存）-->
   <cache type="org.mybatis.caches.ehcache.EhcacheCache" >
   <property name="timeToIdleSeconds" value="3600"/>
   <property name="timeToLiveSeconds" value="3600"/>
   <!-- 同ehcache参数maxElementsInMemory -->
   <property name="maxEntriesLocalHeap" value="1000"/>
   <!-- 同ehcache参数maxElementsOnDisk -->
   <property name="maxEntriesLocalDisk" value="10000000"/>
   <property name="memoryStoreEvictionPolicy" value="LRU"/>
   </cache>
```







#### 9.MyBatis逆向工程

(1). mybatis-generator-gui-master工具

​      作用:自动生成mapper.xml和pojo





##### MyBatisUtil.java

```java
import org.apache.ibatis.io.Resources;
import org.apache.ibatis.session.SqlSession;
import org.apache.ibatis.session.SqlSessionFactory;
import org.apache.ibatis.session.SqlSessionFactoryBuilder;
import java.io.IOException;
import java.io.InputStream;
import java.sql.Connection;
import java.sql.SQLException;

/**
 * 封装了MyBatis 核心类 sqlSession
 */
public class MybatisUtil {
    private static SqlSessionFactory sessionFactory = null;
    private static SqlSession session = null;
    //类加载的时候执行
    static{
        InputStream is =null;
        try {
            is = Resources.getResourceAsStream("com/mybatis/config/mybatis_config.xml");
        } catch (IOException e) {
            e.printStackTrace();
        }
        sessionFactory = new SqlSessionFactoryBuilder().build(is);
    }
    /**
     * 获得SqlSession对象
     * @return
     */
    public static SqlSession getSession(){
        session = sessionFactory.openSession();//创建一个新的SqlSession对象
        return session;
    }
    /**
     * 关闭SqlSession
     */
    public static void closeSession(){
        if(session !=null)
            session.close();
    }
    /**
     * 测试
     */
    public static void main(String[] args) {
        try {
            Connection connection =  MybatisUtil.getSession().getConfiguration().getEnvironment().getDataSource().getConnection();
            System.out.println(connection);

            Connection connection2 =  MybatisUtil.getSession().getConfiguration().getEnvironment().getDataSource().getConnection();
            System.out.println(connection2);
        } catch (SQLException e) {
            e.printStackTrace();
        }
    }
}
```



##### MyBatis配置日志

(1). 导入log4j相关jar(3个)  log4j.jar log4j-api-2.3.jar log4j-core-2.3.jar
(2). 导入log4j.properties文件（修改）

```properties
### Global logging configuration
log4j.rootLogger=DEBUG, stdout
### Uncomment for MyBatis logging
log4j.logger.org.apache.ibatis=ERROR
#log4j.logger.org.apache.ibatis.session.AutoMappingUnknownColumnBehavior=WARN, lastEventSavedAppender
### Console output...
log4j.appender.stdout=org.apache.log4j.ConsoleAppender
log4j.appender.stdout.layout=org.apache.log4j.PatternLayout
log4j.appender.stdout.layout.ConversionPattern=%5p [%t] - %m%n
log4j.appender.lastEventSavedAppender=org.apache.ibatis.session.AutoMappingUnknownColumnBehaviorTest$LastEventSavedAppender
#log4j.logger.com.mybatis.mapper.UserInfoMapper=TRACE
```

(3). 启用日志mybatis-config.xml

```xml
<settings>
	<setting name="logImpl" value="LOG4J"/> 
</settings>
```



