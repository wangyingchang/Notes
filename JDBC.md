##### 1.什么是JDBC?

JDBC全称为：Java Data Base Connectivity (java数据库连接），可以为多种数据库提供填统一的访问。JDBC是sun开发的一套数据库访问编程接口，是一种SQL级的API。它是由java语言编写完成，所以具有很好的跨平台特性，使用JDBC编写的数据库应用程序可以在任何支持java的平台上运行，而不必在不同的平台上编写不同的应用程序。 

JDBC是由java编程语言编写的类及接口组成，同时它为程序开发人员提供了一组用于实现对数据库访问的JDBC API,并支持SQL语言。利用JDBC可以将JAVA代码连接到oracle、DB2、SQLServer、MYSQL等数据库，从而实现对数据库中的数据操作的目的。 

JDBC技术存在的意义:程序讲究的安全性,可移植性


为了让Java语言开发出来的应用程序,能够最大程度适应不同的DB厂商生产的数据库.
那么SUN公司制定了JDBC规范[由SUN公司提供的接口和类,并且大部分都是属于接口].

留下的关于接口的实现类都是由各个DB厂商自己去实现,并且这些实现类叫做"xxx的驱动程序"



##### 2.JDBC主要功能?

(1).建立与数据库或者其他数据源的连接;

(2).发送SQL语句到数据库服务器端[SQL仍然是由数据库服务器端进行编译和执行];

(3).如果执行的是DQL语句,那么还需要对结果集进行处理.



##### 3.JDBC架构?

(1).面向开发者

(2).面向的DB厂商



![img](http://www.yiibai.com/uploads/images/201706/0206/392080659_56700.jpg)





##### 4.JDBC核心API?

--java.sql包下

**Driver[I]**

> 每个驱动程序类必须实现的接口  [jdbc4.0规范,此处可以省略]

**DriverManager[C]: 驱动程序管理类**

> DriverManager类是JDBC的管理类,作用于用户和驱动程序之间;
>
> 它跟踪在可用的驱动程序，并在数据库和相应驱动程序之间建立连接;
>
> DriverManager类也处理诸如驱动程序登陆时间限制及登录和跟踪消息的显示事务;
>
> 对于简单的应用程序，一般程序员需要在此类中直接使用唯一的方法时DriverManager.getConnection(),该方法将建立与数据库的链接;
>
> JDBC允许用户调用DriverManager的方法getDriver()、getDrivers()和registerDriver()及Driver的方法connect().;

**Connection[I]:数据库连接接口**

> Connection对象代表与数据库的链接;
>
> 连接过程包括所执行的SQL语句和在该连接上所返回的结果;
>
> 一个应用程序可与单个数据库有一个或多个连接，或者可与很多数据库有连接;
>
> 打开连接与数据库建立连接的标准方法是调用DriverManager.getConnection()方法;



**Statement[I]:** 声明SQL语句对象

> - 负责发送SQL语句到数据库服务器端;
>
> - 如果执行的是DQL --> ResultSet executeQuery(sql);
> - 如果执行的是的DML->int executeUpdate(sql);
> - PreparedStatement[I]  - 预编译语句;
>
> Statement对象用于将SQL语句发送到数据库中。实际上有三种Statement对象，它们都作为在给定链接上执行SQL语句的包容器：Statement、PreparedStatement(它从Statement继承而来)和CallableStatement（它从PreparedStatement继承而来）。它们都专用于发送特定类型的SQL语句：
>
> （1）Statement对象: 用于执行不带参数的简单的SQL语句；Statement接口提供了执行语句和获取结果的基本方法。执行10次编译10次;
>
> （2）PerparedStatement对象: 用于执行带或不带IN参数的预编译SQL语句；PeraredStatement接口添加处理IN参数的方法；执行10次只需编译1次;防止非法SQL注入;
>
> （3）CallableStatement对象: 用于执行对数据库已存储过程的调用；CallableStatement添加处理OUT参数的方法。
>
> Statement常用的方法：
>
> （1）execute()方法：运行语句，返回是否有结果集。
>
> （2）executeQuery()方法：运行查询语句，返回ReaultSet对象。
>
> （3）executeUpdata()方法：运行更新操作，返回更新的行数。
>
> （4）addBatch()方法：增加批处理语句。
>
> （5）executeBatch()方法：执行批处理语句。
>
> （6）clearBatch()方法：清除批处理语句。
>

**ResultSet[I]: 结果集接口**

> 结果集.如果执行的是DQL语句,那么会将返回出来的结果封装到一个ResultSet结果集对象上面.[本质上它封装的不是真正的结果,它封装的是指向结果行的游标,默认是指向标题行的,并且默认是自上而下不可逆的]
>
> ResultSet包含符合SQL语句中条件的所有行记录，并且它通过一套get方法（这些get方法可以访问当前行中的不同列）提供了对这些行中数据的访问。ResultSet.next()方法用于移动到ResultSet中的下一行，使下一行成为当前行。 



##### 5.JDBC六大编程步骤?

  (1)  加载驱动程序：Class.forName(driverClass) 

~~~java
/**
* 一. 加载驱动...JDBC规范以后,此处可以省略不写
* 所谓的加载驱动就是将驱动类加载进JVM的内存
* 一旦加载之后,就会立即执行驱动类里面的static块里面的语句
*/
加载mysql驱动：Class.forName("com.mysql.jdbc.Driver");

加载mysql驱动：Class.forName("com.mysql.cj.jdbc.Driver");//MySQL8.0

加载oracle驱动：Class.forName("oracle.jdbc.driver.OracleDriver"); 
~~~

  (2)  获得数据库连接

~~~java
/**
* 二. 获取连接,采用的是DriverManger提供的标准的连接方式
* java.sql.DriverManger[C] 提供的static Connection getConnection(String uri,String user,String password);
* MySQL:url格式="主协议:次协议//主机ip:端口号/数据库名?参数"
*/ 
String url="jdbc:mysql://localhost:3306/studentdb?useSSL=FALSE
String url="jdbc:mysql://localhost:3306/studentdb?useSSL=FALSE&serverTimezone=UTC&allowPublicKeyRetrieval=true";//MySQL8.0

String user="root";

String password="123456";

Connection conn=DriverManager.getConnection(url,user,password);
~~~

  (3)  创建Statement SQL语句对象：

~~~java
/**
* 三. 获取语句对象Statement -负责发送SQL语句到数据库端
*/
Statement st=conn.createStatement(); 
~~~

  (4)  向数据库发送SQL命令 并执行:

~~~java
/**
* 四. 执行SQL[发送sql语句,并且将返回的结果封装到ResultSet对象[结果集对象]
*/
String sql = "select empno,ename,job from emp";
ResultSet rs = st.executeQuery(sql);
~~~

  (5)  处理数据库的返回结果集(ResultSet类) :

```java
/**
* 五. 处理结果集
* 本质上ResultSet其实封装的是指向结果行的游标,本质是就是光标;
* 默认是停在标题列所在的行,只能向下移动[不可逆],不可更新;
* 调用next()方法向下移动,如果下一行没有记录,则返回false
*/       
while (rs.next()) {
/**
* 通过rs对象来获取当前行的列上面的数据
* 获取列数据有两种方式,第一种是通过列的序号进行获取[从1开始]
* 可读性比较差,但是性能比较高;
* 获取的时候一定要注意类型.- 根据获取列的数据类型
*/
int empno = rs.getInt(1);
String ename = rs.getString(2);
String job = rs.getString(3);
/**
* 可以通过列的名称进行获取
* 可读性比较高,性能较差
*/
//int id=rs.getInt("emp");
//String ename=rs.getString("ename");
//String job=rs.getString("job");
System.out.println(empno + " " + ename + " " + job);
}
```
  (6)  释放资源:

> 顺序问题 rs ,st,conn



##### 6.JDBC编程步骤实例?

~~~java
import java.sql.*;

/**
 * JDBC 六大步骤体验
 */
public class demo {
    public static void main(String[] args) {
        Connection conn = null;
        Statement st = null;
        ResultSet rs = null;
        try {
            //1.加载驱动程序
            Class.forName("com.mysql.cj.jdbc.Driver");
            
            //2.获取数据库连接
            String url = "jdbc:mysql://localhost:3306/empdb?useSSL=FALSE&serverTimezone=UTC&allowPublicKeyRetrieval=true";
            String user = "root";
            String password = "123456";
            conn = DriverManager.getConnection(url, user, password);//2-2与数据库建立了会话[一次连接]
            //3.创建Statement对象
            st = conn.createStatement();
            
            //4.向数据库发送SQL命令 并执行:
            String sql = "select empno,ename,job from emp";
            rs = st.executeQuery(sql);

            //5.处理数据库返回结果集
            while (rs.next()) {
                int empno = rs.getInt(1);
                String ename = rs.getString(2);
                String job = rs.getString(3);
                System.out.println(empno + " " + ename + " " + job);
            }
        } catch (ClassNotFoundException e) {
            e.printStackTrace();
        } catch (SQLException e) {
            e.printStackTrace();
        } finally {
            //6.释放资源
            if (null != rs) {
                try {
                    rs.close();
                } catch (SQLException e) {
                    e.printStackTrace();
                }
            }
            if (null != st) {
                try {
                    st.close();
                } catch (SQLException e) {
                    e.printStackTrace();
                }
            }
            if (null != conn) {
                try {
                    conn.close();
                } catch (SQLException e) {
                    e.printStackTrace();
                }
            }
        }
    }
}
~~~



##### 7.JDBC封装?

(1). 数据源的封装: 

创建dbConfig.properties文件

~~~properties
driver=com.mysql.cj.jdbc.Driver
url=jdbc:mysql://localhost:3306/studentdb?useSSL=false&serverTimezone=UTC&allowPublicKeyRetrieval=true
user=root
password=123456
~~~

创建DBConfigUtils.java文件

~~~java
import java.io.IOException;
import java.io.InputStream;
import java.util.Properties;
/**
 * 读取配置文件的数据
 */
public class DBConfigUtils {
    private static Properties prop=new Properties();
    static{
        InputStream in=Thread.currentThread().getContextClassLoader().getResourceAsStream("dbConfig.properties");
        try {
            prop.load(in);
        } catch (IOException e) {
            e.printStackTrace();
            throw new RuntimeException("读取(dbConfig.properties)配置文件失败!");
        }
    }
    public static String getValue(String key){
        return prop==null?null:prop.getProperty(key);
    }
}
~~~

(2).数据库的连接与关闭的封装

创建JdbcUtils.java文件

~~~java
import java.sql.*;

/**
 * 封装JDBC
 * 注册驱动类,获取数据库连接,释放资源
 */
public class JdbcUtils {

    //获取参数
    private static String driver=DBConfigUtils.getValue("driver");

    private static String url=DBConfigUtils.getValue("url");

    private static String user=DBConfigUtils.getValue("user");

    private static String password=DBConfigUtils.getValue("password");

    //加载驱动类
    static{
        try {
            Class.forName(driver);
        } catch (ClassNotFoundException e) {
            e.printStackTrace();
            throw new RuntimeException("注册驱动失败!");
        }
    }

    //获取数据库连接
    public static Connection getConnection() throws SQLException {
        Connection conn=DriverManager.getConnection(url,user,password);
        return conn;
    }

    //释放资源
    public static void close(Connection conn, Statement st, ResultSet rs){
        if(null!=rs){
            try {
                rs.close();
            } catch (SQLException e) {
                e.printStackTrace();
            }
        }
        if(null!=st){
            try {
                st.close();
            } catch (SQLException e) {
                e.printStackTrace();
            }
        }
        if(null!=conn){
            try {
                conn.close();
            } catch (SQLException e) {
                e.printStackTrace();
            }
        }
    }
}
~~~

(3). PreparedStatement,ResultSet的封装

创建JdbcTemplates.java文件

~~~java
import com.jdbc.util.JdbcUtils;
import java.sql.*;

/**
 * JDBC模板
 */
public class JdbcTemplates {

    //执行的是DQL语句
    public static Object executeDQL(IPreparedStatementCallBack pcb,IResultSetCallBack rsc){
        Connection conn=null;
        PreparedStatement pst=null;
        ResultSet rs=null;
        Object obj=null;
        try {
            conn=JdbcUtils.getConnection();
            pst=pcb.execute(conn);
            rs=pst.executeQuery();
            obj=rsc.execute(rs);
        } catch (SQLException e) {
            e.printStackTrace();
        } finally {
            JdbcUtils.close(conn,pst,rs);
        }
        return obj;
    }
    
    //执行的是DML语句
    public static void executeDML(IPreparedStatementCallBack pcb){
        Connection conn=null;
        PreparedStatement pst=null;
        try {
            conn=JdbcUtils.getConnection();
            pst=pcb.execute(conn);
            pst.executeUpdate();
        } catch (SQLException e) {
            e.printStackTrace();
        }finally {
            JdbcUtils.close(conn,pst,null);
        }
    }
}
~~~

创建回调接口IPreparedStatementCallBack.java文件

~~~java
import java.sql.Connection;
import java.sql.PreparedStatement;
import java.sql.SQLException;

public interface IPreparedStatementCallBack {
    PreparedStatement execute(Connection conn) throws SQLException;
}
~~~

创建回调接口IResultSetCallBack.java文件

~~~java
import java.sql.ResultSet;
import java.sql.SQLException;

public interface IResultSetCallBack {
    Object execute(ResultSet rs) throws SQLException;
}
~~~

(4).测试方法

~~~java
/**
 * 根据id进行删除
 * @param id
 */
public void delById(Integer id) {
    JdbcTemplates.executeDML(conn->{
        String sql="delete from t_users where id=?";
        PreparedStatement pst=conn.prepareStatement(sql);
        pst.setInt(1,id);
        return pst;
    });
}

/**
 * 根据用户名进行查询
 * @param username 用户名是唯一的
 * @return 单个user对象
 */
    public User findByUserName(String uname) {
        return (User) JdbcTemplates.executeDQL(conn->{
            String sql="select * from t_users where username=?";
            PreparedStatement pst = conn.prepareStatement(sql);
            pst.setString(1,uname);
            return pst;
        },rs->{
            User u = null;
            while(rs.next()){
                u = new User();
                //推荐用列的序号进行获取
                Integer id = rs.getInt(1);
                String username = rs.getString(2);
                String pwd = rs.getString(3);
                String gender = rs.getString(4);//性别 - 枚举类型 -getString("")获取任何类型
                java.util.Date birthday = rs.getDate(5);//日期
                //封装对象
                u.setId(id);
                u.setUsername(username);
                u.setPassword(pwd);
                //字符串转换成枚举类型
                u.setGender(Enum.valueOf(Gender.class, gender));
                u.setBirthday(birthday);
            }
            return u;
        });
    }
~~~



##### 8.JDBC后台分页的实现?

(1).entity层: 创建PageBeanVo.java文件

~~~java
import java.util.List;

public class PageBeanVo<T> {
    //当前页
    private Integer pageNow;
    //总的页数
    private Integer pageCount;
    //总的条数
    private Integer rowCounts;
    //每页显示多少条
    private Integer pageSize;
    //显示什么内容...
    private List<T> datas;//泛型

    public PageBeanVo() {
    }
    public Integer getPageNow() {
        return pageNow;
    }
    public void setPageNow(Integer pageNow) {
        this.pageNow = pageNow;
    }
    public Integer getPageCount() {
        return pageCount;
    }
    public void setPageCount(Integer pageCount) {
        this.pageCount = pageCount;
    }
    public Integer getRowCounts() {
        return rowCounts;
    }
    public void setRowCounts(Integer rowCounts) {
        this.rowCounts = rowCounts;
    }
    public Integer getPageSize() {
        return pageSize;
    }
    public void setPageSize(Integer pageSize) {
        this.pageSize = pageSize;
    }
    public List<T> getDatas() {
        return datas;
    }
    public void setDatas(List<T> datas) {
        this.datas = datas;
    }
    @Override
    public String toString() {
        return "PageBeanVo{" +
                "pageNow=" + pageNow +
                ", pageCount=" + pageCount +
                ", rowCounts=" + rowCounts +
                ", pageSize=" + pageSize +
                ", datas=" + datas +
                '}';
    }
}
~~~

(2).service层:

新建接口IUserService.java文件

~~~java
import com.jdbc.entity.PageBeanVo;
import com.jdbc.entity.User;

public interface IUserService {
    PageBeanVo<User> findPage(Integer pageNow,Integer pageSize);
}
~~~

新建实现类UserServiceImpl.java文件

~~~java
import com.jdbc.dao.IUserDao;
import com.jdbc.dao.impl.UserDaoHbImpl;
import com.jdbc.entity.PageBeanVo;
import com.jdbc.entity.User;
import com.jdbc.service.IUserService;
import java.util.List;

public class UserServiceImpl implements IUserService {
    
    private IUserDao userDao=new UserDaoHbImpl();
    @Override
    public PageBeanVo<User> findPage(Integer pageNow, Integer pageSize) {
        //创建实体对象泛型为<User>
        PageBeanVo<User> pageBeanVo=new PageBeanVo<>();
        //封装当前页
        pageBeanVo.setPageNow(pageNow);
        //封装每页显示内容数
        pageBeanVo.setPageSize(pageSize);
        //封装显示的内容
        //select * from t_users limit (pageNow-1)*pageSize,pageSize
        List<User> users = userDao.findByPage(pageNow,pageSize);
        pageBeanVo.setDatas(users);
        //封装总的条数
        Integer rows = userDao.findRowsCount();//dao层获取总数
        pageBeanVo.setRowCounts(rows);
        //封装总的页数
        Integer pageCount= rows/pageSize;
        if(rows%pageSize!=0)
            pageCount++;
        pageBeanVo.setPageCount(pageCount);

        return pageBeanVo;
    }
}
~~~

(3).dao层

新建接口IUserDao.java文件

~~~java
import com.jdbc.entity.User;
import com.jdbc.entity.UserQueryVo;
import java.util.List;

public interface IUserDao {
    /**
     * 分页查询
     * @param pageNow 当前页数
     * @param pageSize 每页显示数
     * @return User集合对象
     */
    List<User> findByPage(Integer pageNow,Integer pageSize);

    /**
     * 查找总记录数
     * @return
     */
    Integer findRowsCount();
}
~~~

新建实现类:UserDaoImpl.java文件

~~~java
//findByPage()
public List<User> findByPage(Integer pageNow, Integer pageSize) {
        Connection conn=null;
        PreparedStatement pst=null;
        ResultSet rs=null;
        List<User> usersList=new ArrayList<>();
        try {
            conn=JdbcUtils.getConnection();
            String sql="select * from t_users limit ?,?";
            pst=conn.prepareStatement(sql);
            pst.setInt(1,(pageNow-1)*pageSize);
            pst.setInt(2,pageSize);
            rs=pst.executeQuery();
            while(rs.next()){
                User users=new User();
                //推荐用列的序号进行获取
                Integer id = rs.getInt(1);
                String username = rs.getString(2);
                String pwd = rs.getString(3);
                //性别 - 枚举类型 -getString("")获取任何类型
                String gender = rs.getString(4);
                //日期
                java.util.Date birthday = rs.getDate(5);
                //封装对象
                users.setId(id);
                users.setUsername(username);
                users.setPassword(pwd);
                //字符串转换成枚举类型
                users.setGender(Enum.valueOf(Gender.class,gender));
                users.setBirthday(birthday);
                usersList.add(users);
            }
        } catch (SQLException e) {
            e.printStackTrace();
        }finally {
            JdbcUtils.close(conn,pst,rs);
        }
        return usersList;
    }
    //findRowsCount()查询数据库总行数
    public Integer findRowsCount() {
        Connection conn = null;
        PreparedStatement pst = null;
        ResultSet rs = null;
        Integer count = 0;
        try {
            conn = JdbcUtils.getConnection();
            String sql = "select count(*) from t_users";
            pst = conn.prepareStatement(sql);
            rs = pst.executeQuery();
            rs.next();
            count = rs.getInt(1);
        } catch (SQLException e) {
            e.printStackTrace();
        } finally {
            JdbcUtils.close(conn, pst, rs);
        }
        return count;
    }
~~~



##### 9.JDBC连接池?

**(1).为什么要使用数据库连接池？**

 数据库连接是一种关键的有限的昂贵的资源，这一点在多用户的网页应用程序中体现得尤为突出。  一个数据库连接对象均对应一个物理数据库连接，每次操作都打开一个物理连接，使用完都关闭连接，这样造成系统的 性能低下。 数据库连接池的解决方案是在应用程序启动时建立足够的数据库连接，并讲这些连接组成一个连接池(简单说：在一个“池”里放了好多半成品的数据库联接对象)，由应用程序动态地对池中的连接进行申请、使用和释放。对于多于连接池中连接数的并发请求，应该在请求队列中排队等待。并且应用程序可以根据池中连接的使用率，动态增加或减少池中的连接数。 连接池技术尽可能多地重用了消耗内存地资源，大大节省了内存，提高了服务器地服务效率，能够支持更多的客户服务。通过使用连接池，将大大提高程序运行效率，同时，我们可以通过其自身的管理机制来监视数据库连接的数量、使用情况等。

**(2).连接池的原理是什么？**

`数据库连接池的基本原理:` 

就是为数据库连接 建立一个“缓冲池”。预先在缓冲池中放入一定数量的连接，当需要建立数据库连接时，只需从“缓冲池”中取出一个，使用完毕之后再放回去。我们可以通过设定 连接池最大连接数来防止系统无尽的与数据库连接。更为重要的是我们可以通过连接池的管理机制监视数据库的连接的数量?使用情况，为系统开发?测试及性能调 整提供依据。

`数据库连接池的工作原理:` 

主要由三部分组成，分别为连接池的建立、连接池中连接的使用管理、连接池的关闭.
第一、连接池的建立。一般在系统初始化时，连接池会根据系统配置建立，并在池中创建了几个连接对象，以便使用时能从连接池中获取。
连接池中的连接不能随意创建和关闭，这样避免了连接随意建立和关闭造成的系统开销。Java中提供了很多容器类可以方便的构建连接池，例如Vector、Stack等。
第二、连接池的管理。连接池管理策略是连接池机制的核心，连接池内连接的分配和释放对系统的性能有很大的影响。其管理策略是：
当客户请求数据库连接时，首先查看连接池中是否有空闲连接，如果存在空闲连接，则将连接分配给客户使用；如果没有空闲连接，
则查看当前所开的连接数是否已经达到最大连接数，如果没达到就重新创建一个连接给请求的客户；如果达到就按设定的最大等待时间进行等待，
如果超出最大等待时间，则抛出异常给客户。 当客户释放数据库连接时，先判断该连接的引用次数是否超过了规定值，
如果超过就从连接池中删除该连接，否则保留为其他客户服务。该策略保证了数据库连接的有效复用，避免频繁的建立、
释放连接所带来的系统资源开销。
第三、连接池的关闭。当应用程序退出时，关闭连接池中所有的连接，释放连接池相关的资源，该过程正好与创建相反。

**(3).主流连接池插件有哪些？区别是什么？** 

> 第一代连接池

区分一个数据库连接池是属于第一代产品还是第二代产品的一个最重要特征就是看它在架构和设计时采用的线程模型，因为这直接影响的并发环境下存取数据库连接的性能。一般来讲采用单线程同步的架构设计的都属于第一代连接池，而采用多线程异步架构的则属于第二代。比较有代表性的就是Apache Commons DBCP，在1.x版本中，一直延续这单线程设计模型，到2.x版本才采用多线程模型。
用版本发布时间来辨别区分两代产品，是一个的好方法。以下是这些常见数据库连接池最新版本的发布时间:

| 数据库连接池 |   最新版本   | 发布时间       |
| :----------- | :----------: | -------------- |
| c3p0         | c3p0-0.9.5.2 | on 9 Dec 2015  |
| proxool      |    0.9.x     | May 24, 2011   |
| dbcp         |    2.1.1     | 2015-08-06     |
| BoneCP       |    0.8.0     | on 23 Oct 2013 |
| TJP          |   tomcat9    | Jan 10 2017    |
| druid        |    1.0.28    | 2017-02-05     |
| hikariCP     |    2.4.11    | 2017-01-28     |

** 从表中我们可以看到，c3p0、DBCP、Proxool和BoneCP都已经很久没更新了，TJP(Tomcat JDBC Pool)，druid，hikariCPze则仍处于活跃的更新中，后者明显就是我们所说的二代产品了。**

> 已经彻底死掉的c3p0和proxool

c3p0在很长一段时间内，它一直是Java领域内数据库连接池的代名词，当年盛极一时的Hibernate都将其作为内置的数据库连接池，可见业内对它的稳定行还是认可的。关于c3p0如何使用，可以借助于搜索引擎，这里就不再赘述了。c3p0功能简单易用，稳定性好这是它的优点，但性能上的缺点却让它彻底被打入冷宫。c3p0的性能很差，差到即便是和同时代的产品相比，它也是垫底的（见下图）。同时代的BoneCP更是直接以干掉它为自己的口号（官网号称比c3p0快25倍），更不要说和后来的druid和HikariCP相比了。

正常来讲，有问题很正常，改就是了，但c3p0最致命的问题就是架构设计过于复杂，让重构变成了一项不可能完成的任务。随着国内互联网大潮的涌起，性能有硬伤的c3p0彻底的退出了历史舞台。

如果说c3p0被人嫌弃，是因为它自身架构设计的“原罪”，那proxool的冷门，则是与作者兴趣的缺失有关。proxool最初在设计上另辟蹊径，以JDBC驱动的身份为用户提供连接池服务，这使得将proxool移植到现有代码中别的十分容易，而且proxool还开创性的提供了连接池监控功能，让它迅速的获得了不少用户的青睐。

但产品作者兴趣的缺失，让这款本来很有潜力的产品早早夭折。在github的项目首页，作者写到：“我从2006年之后就再没碰过这个项目了，我甚至练Java都不用了...”，也许，proxool本来就是这位天才coder的练手之作，java本身也不是他的主力语言，但不论哪种原因，proxool都已经和c3p0一样，鲜有人问津了。

> 咸鱼翻身的dbcp

dbcp（DataBase Connection Pool）属于Apache顶级项目Commons中的核心子项目（最早在Jakarta Commons里就有），在Apache的生态圈中的影响里十分广泛，比如最为大家所熟知的tomcat就在内部集成了dbcp，实现JPA规范的OpenJPA，也是默认集成dbcp的。但dbcp并不是独立实现连接池功能的，它内部依赖于Commons中的另一个子项目pool，连接池最核心的“池”，就是由pool组件提供的，因此，dbcp的性能实际上就是pool的性能，dbcp和pool的依赖关系如下表：

| Apache Commons DBCP	| Apache Commons Pool
| :------ | :--------------------------------: |
| v1.2.2 |	v1.3 |
| v1.3 |	v1.5.4 |
| v1.4 |	v1.5.4 |
| v2.0.x |	v2.2 |
| v2.1.x |	v2.4.2 |

可以看到，因为核心功能依赖于pool，所以dbcp本身只能做小版本的更新，真正大版本的更迭则完全依托于pool。有很长一段时间，pool都还是停留在1.x版本，这直接导致dbcp也更新乏力。很多依赖dbcp的应用在遇到性能瓶颈之后，别无选择，只能将其替换掉，dbcp忠实的拥趸tomcat就在其tomcat 7.0版本中，自己重新设计开发出了一套连接池（Tomcat JDBC Pool）。好在，在2013年事情终于迎来转机，13年9月Commons-Pool 2.0版本发布，14年2月份，dbcp也终于迎来了自己的2.0版本，基于新的线程模型全新设计的“池”让dbcp重焕青春，虽然和新一代的连接池相比仍有一定差距，但差距并不大，dbcp 2.x版本已经稳稳达到了和新一代产品同级别的性能指标（见下图）。

dbcp终于靠pool咸鱼翻身，打了一个漂亮的翻身仗，但长时间的等待已经完全消磨了用户的耐心，与新一代的产品项目相比，dbcp没有任何优势，试问，谁会在有选择的前提下，去选择那个并不优秀的呢？也许，现在还选择dbcp2的唯一理由，就是情怀吧。

> 甘心赴死的BoneCP

在讨论BoneCP这块的内容之前，我们还是先来看看BoneCP作者自己是这么评价这款产品的：

用我自己的话翻译一下就是：俺是一个高性能的数据库连接池，俺之所以这么牛逼是因为俺在实现的时候减少了锁的使用，想当年，什么c3p0啊DBCP啊都被老子干趴了，但是现在为了支持HikariCP，俺选择退出！也就是说，BoneCP的退出是它自己的选择，但它又不像proxool是被抛弃的，它是作者经过深思熟虑后，做出的选择，可以说BoneCP是“甘心赴死，杀身成仁”。那么问题来了，BoneCP究竟是不是像它自己形容的那样牛逼？BoneCP和HikariCP之间究竟有啥联系，能引得它主动“金盆洗手”？

先说性能，BoneCP自称性能是c3p0的25倍，并提供了依照自己定义的测试案例，提供了一组图片

单线程（1,000,000获得及释放数据库连接请求，连接池大小20-50）

多线程（500线程分别获取释放100个链接，连接池大小50-200）

多线程（500个线程每个100次获得/释放，连接池大小20-500）

当然，以上图片仅供参考，因为不同的参数配置，不同的应用环境，不同的测试案例，得到的结果肯定也不会相同，官网提供的数据，肯定是在最有利于自己表现的环境下得到的。但结合另外一份测试数据（第一幅图），可以看到BoneCP的性能在第一代产品中，确实是属于领先地位的。高性能的表现的秘诀也并不高深，一是极简的设计，整个产品只有几百k大小，二是重构内部pool的设计，减少锁的使用，而这两点优化原则，几乎适用于所以的连接池产品。

值得一提的是，BoneCP本身并不“健全”，它的很多特征都依赖于Guava，因此也就和dbcp一样，面临更新乏力的问题。但现在，这些问题都不重要了，因为它赖以为傲的性能被HikariCP全面超越。HikariCP可以说是BoneCP的二代产品（HikariCP自己在官网上声称在BoneCP的基础上，做了很多优化），它在设计思路上和BoneCP完全一致，主打的特征也是超强的性能表现，关于HikariCP的详细内容，我将在下一章节介绍。

> 站在巨人肩膀上的第二代连接池

在数据库连接池的产品群中，二代产品对一代产品的超越是颠覆性的，除了一些“历史原因”，你很难再找到第二条理由说服自己不选择二代产品，但任何成功都不是偶然的，二代产品的成功很大程度上得益于前代产品们打下的基础，站在巨人的肩膀上，新一代的连接池的设计师们将这一项“工具化”的产品，推向了极致。其中，最具代表性的两款产品是：

- HikariCP
- druid

> 性能无敌的HikariCP

刚刚在介绍BoneCP的时候多少已经提到过HikariCP了，作为连接池产品中的“性能杀手”，它的表现究竟如何呢，先来看下官网提供的数据：

不光性能强劲，稳定性也不差：

 那它是怎么做到如此强劲的呢？官网给出的说明如下：

- 字节码精简：优化代码，直到编译后的字节码最少，这样，CPU缓存可以加载更多的程序代码；
- 优化代理和拦截器：减少代码，例如HikariCP的Statement proxy只有100行代码，只有BoneCP的十分之一；
- 自定义数组类型（FastStatementList）代替ArrayList：避免每次get()调用都要进行range check，避免调用remove()时的从头到尾的扫描；
- 自定义集合类型（ConcurrentBag）：提高并发读写的效率；
- 其他针对BoneCP缺陷的优化，比如对于耗时超过一个CPU时间片的方法调用的研究（但没说具体怎么优化）。

可以看到，上述这几点优化，针对的都是BoneCP现有的缺陷，优化到这份上，也难怪BoneCP的作者不想玩了。综合现在能找到的资料来看，HakariCP在性能上的优势应该是得到共识的，再加上它自身小巧的身形，在当前的“云时代、微服务”的背景下，HakariCP一定会得到更多人的青睐  <br>

> 功能全面的druid

近几年，阿里在开源项目上动作频频，除了有像fastJson这类工具型项目，更有像AliSQL这类的大型软件，今天说的druid，就是阿里众多优秀开源项目中的一个。它除了提供性能卓越的连接池功能外，还集成了sql监控，黑名单拦截等功能，用它自己的话说，druid是“为监控而生”。借助于阿里这个平台的号召力，产品一经发布就赢得了大批用户的拥趸，从用户使用的反馈来看，druid也确实没让用户失望。

相较于其他产品，druid另一个比较大的优势，就是中文文档比较全面（毕竟是国人的项目么），在github的wiki页面，列举了日常使用中可能遇到的问题，对一个新用户来讲，上面提供的内容已经足够指导它完成产品的配置和使用了。

下图为druid自己提供的性能测试数据：

 最后，隐身的连接池
 时至今日，虽然每个应用（需要RDBMS的）都离不开连接池，但在实际使用的时候，连接池已经可以做到“隐形”了。也就是说在通常情况下，连接池完成项目初始化配置之后，就再不需要再做任何改动了。不论你是选择druid或是HikariCP，甚至是DBCP，它们都足够稳定且高效！我们之前讨论了很多关于连接池的性能的问题，但这些性能上的差异，是相交于其他连接池而言的，对整个系统应用来说，第二代连接池在使用过程中体会到的差别是微乎其微的，基本上不存在因为连接池的自身的配饰和使用导致系统性能下降的情况，除非是在单点应用的数据库负载足够高的时候（压力测试的时候），但即便是如此，通用的优化的方式也是单点改集群，而不是在单点的连接池上死扣。
 ** 最后: ** 开源是一种精神，分享是一种态度，而这，正是Java语言几十年依旧屹立不倒的原因.

**(4).连接池关键问题分析**

`并发问题`

为了使连接管理服务具有最大的通用性，必须考虑多线程环境，即并发问题。这个问题相对比较好解决，因为Java语言自身提供了对并发管理的支 持，使用synchronized关键字即可确保线程是同步的。使用方法为直接在类方法前面加上synchronized关键字，如：

public synchronized Connection getConnection()

`多数据库服务器和多用户`

　　对于大型的企业级应用，常常需要同时连接不同的数据库(如连接Oracle和Sybase)。如何连接不同的数据库呢?我们采用的策略是：设计 一个符合单例模式的连接池管理类，在连接池管理类的唯一实例被创建时读取一个资源文件，其中资源文件中存放着多个数据库的url地址()?用户名()?密 码()等信息。如 tx.url=172.21.15.123：5000/tx_it，tx.user=yang，tx.password=yang321。根据资源文件提 供的信息，创建多个连接池类的实例，每一个实例都是一个特定数据库的连接池。连接池管理类实例为每个连接池实例取一个名字，通过不同的名字来管理不同的连 接池。

　　对于同一个数据库有多个用户使用不同的名称和密码访问的情况，也可以通过资源文件处理，即在资源文件中设置多个具有相同url地址，但具有不同用户名和密码的数据库连接信息。

`事务处理`

　　我们知道，事务具有原子性，此时要求对数据库的操作符合“ALL-ALL-NOTHING”原则,即对于一组SQL语句要么全做，要么全不做。

　　在Java语言中，Connection类本身提供了对事务的支持，可以通过设置Connection的AutoCommit属性为 false,然后显式的调用commit或rollback方法来实现。但要高效的进行Connection复用，就必须提供相应的事务支持机制。可采用 每一个事务独占一个连接来实现，这种方法可以大大降低事务管理的复杂性。

 `连接池的分配与释放`

　　连接池的分配与释放，对系统的性能有很大的影响。合理的分配与释放，可以提高连接的复用度，从而降低建立新连接的开销，同时还可以加快用户的访问速度。

　　对于连接的管理可使用空闲池。即把已经创建但尚未分配出去的连接按创建时间存放到一个空闲池中。每当用户请求一个连接时，系统首先检查空闲池内 有没有空闲连接。如果有就把建立时间最长(通过容器的顺序存放实现)的那个连接分配给他(实际是先做连接是否有效的判断，如果可用就分配给用户，如不可用 就把这个连接从空闲池删掉，重新检测空闲池是否还有连接);如果没有则检查当前所开连接池是否达到连接池所允许的最大连接数(maxConn),如果没有 达到，就新建一个连接，如果已经达到，就等待一定的时间(timeout)。如果在等待的时间内有连接被释放出来就可以把这个连接分配给等待的用户，如果 等待时间超过预定时间timeout,则返回空值(null)。系统对已经分配出去正在使用的连接只做计数，当使用完后再返还给空闲池。对于空闲连接的状 态，可开辟专门的线程定时检测，这样会花费一定的系统开销，但可以保证较快的响应速度。也可采取不开辟专门线程，只是在分配前检测的方法。

 `连接池的配置与维护`

　　连接池中到底应该放置多少连接，才能使系统的性能最佳?系统可采取设置最小连接数(minConn)和最大连接数(maxConn)来控制连接 池中的连接。最小连接数是系统启动时连接池所创建的连接数。如果创建过多，则系统启动就慢，但创建后系统的响应速度会很快;如果创建过少，则系统启动的很 快，响应起来却慢。这样，可以在开发时，设置较小的最小连接数，开发起来会快，而在系统实际使用时设置较大的，因为这样对访问客户来说速度会快些。最大连 接数是连接池中允许连接的最大数目，具体设置多少，要看系统的访问量，可通过反复测试，找到最佳点。

　　如何确保连接池中的最小连接数呢?有动态和静态两种策略。动态即每隔一定时间就对连接池进行检测，如果发现连接数量小于最小连接数，则补充相应数量的新连接,以保证连接池的正常运转。静态是发现空闲连接不够时再去检查。