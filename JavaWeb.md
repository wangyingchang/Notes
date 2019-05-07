




#### Servlet 介绍

servlet技术是在JavaEE出现之前就存在了，在开发动态网页中得到广泛的应用，直到现在的JavaEE项目中也是非常重要的，同时jsp也是在servlet的基础上发展起来的。

servlet（java服务器小程序）是用java编写的服务器程序，它的特点：

  1.由服务器调用和执行；

  2.用java语言编写的；

  3.按照servlet规范开发；

  4.功能强大，可以完成几乎所有的网站功能；

  5.是学习jsp的基础；



#### Servlet 配置

1.创建servlet.java文件

~~~java
//一个可以处理HTTP请求的Servlet程序，肯定要继承HttpServlet类，至少要重写HttpServlet类中的doGet()方法
public class Aservlet extends HttpServlet{
@Override
protected void doGet(HttpServletRequest request, HttpServletResponse response)
			throws ServletException, IOException { }

~~~

2.配置web.xml文件

~~~xml
(1)基本配置：
 <servlet> <!--用来声明一个servlet的数据--> 
     <servlet-name></servlet-name> <!--指定servlet的名称--> 
     <servlet-class></servlet-class> <!--指定servlet的类名称--> 
 </servlet>

 <servlet-mapping> <!--用来定义servlet所对应的URL-->
       <servlet-name></servlet-name> <!--指定servlet的名称--> 
       <url-pattern></url-pattern> <!--指定servlet所对应的URL--> 
 </servlet-mapping>
(2) 指定欢迎文件页配置 ：
<welcome-file-list> 
    <welcome-file>index.jsp</welcome-file> 
</welcome-file-list> 

~~~



#### Servlet的生命周期

Servlet的生命周期是从该servlet创建到注销的整个过程，整个过程中servlet会执行以下的过程：

- 调用init () 方法进行初始化。
- 调用service() 方法来处理客户端的请求。
- 调用 destroy() 方法终止（结束）。
- 最后由 JVM 的垃圾回收器进行垃圾回收。

**1.Init()方法**

该方法只在创建servlet时候调仅调用一次，以后不再调用该方法，当用户调用一个 Servlet 时，就会创建一个 Servlet 实例，每一个用户请求都会产生一个新的线程，适当的时候移交给 doGet 或 doPost 方法。init() 方法简单地创建或加载一些数据，这些数据将被用于 Servlet 的整个生命周期。

**2.Service()方法**

service() 方法是执行实际任务的主要方法。Servlet 容器（即 Web 服务器）调用 service() 方法来处理来自客户端（浏览器）的请求，并把格式化的响应写回给客户端。每次服务器接收到一个 Servlet 请求时，服务器会产生一个新的线程并调用服务。service() 方法检查 HTTP 请求类型（GET、POST、PUT、DELETE 等），并在适当的时候调用 doGet、doPost、doPut，doDelete 等方法。

**3.destroy()方法**

该方法只在该servlet注销之前调用一次，且在servlet的生命周期中只会调用一次其中servlet实例化受 <load-on-startup>影响正整数、0： 在启动项目的时候，按照值的大小顺序依次 就实例化、初始化 该Servlet负整数、不写 ： 什么都不做（客户端访问到该Servlet的时候，才实例化、初始化 该Servlet）

~~~
    <servlet>
		<load-on-startup>正整数/0</load-on-startup>
	</servlet>
	当前servlet 在tomcat服务器启动的时候，就实例化与初始化init()	
	当tomcat服务器关闭的时候，该servlet就消亡destroy()
	
	<servlet>
		<load-on-startup>负整数/不写</load-on-startup>
	</servlet>
	只有客户端访问到具体该servlet，才会实例化与初始化init()	
	当tomcat服务器关闭的时候，该servlet就消亡destroy()
~~~



#### Request&&Response对象

HttpServletRequest&&HttpServletResponse

**1.介绍**

Web服务器收到客户端的http请求，会针对每一次请求，分别创建一个用于代表请求的request对象、和代表响应的response对象；request和response对象即然代表请求和响应，那我们要获取客户机提交过来的数据，只需要找request对象就行了。要向客户机输出数据，只需要找response对象就行了。

**2.Request常用方法**

- 获得客户机信息

getRequestURL方法返回客户端发出请求时的完整URL。

getRequestURI方法返回请求行中的资源名部分。

getQueryString 方法返回请求行中的参数部分。

getPathInfo方法返回请求URL中的额外路径信息。额外路径信息是请求URL中的位于Servlet的路径之后和查询参数之前的内容，它以“/”开头。

getRemoteAddr方法返回发出请求的客户机的IP地址。

getRemoteHost方法返回发出请求的客户机的完整主机名。

getRemotePort方法返回客户机所使用的网络端口号。

getLocalAddr方法返回WEB服务器的IP地址。

getLocalName方法返回WEB服务器的主机名。

.....

- 获得客户机请求头

getHeader(string name)方法:String 

getHeaders(String name)方法:Enumeration 

getHeaderNames()方法 

- 获得客户机请求参数(客户端提交的数据)

getParameter(String)方法

getParameterValues(String name)方法

**3.Request 应用**

- 防盗链

- 各种表单输入项数据的获取

text、password、radio、checkbox、

file、select、textarea、 hidden、

- POST方式请求参数的中文乱码问题 

- GET方式请求参数的中文乱码问题（JSP）

- request对象实现请求转发

请求转发指一个web资源收到客户端请求后，通知服务器去调用另外一个web资源进行处理。

请求转发的应用场景：MVC设计模式

request对象提供了一个getRequestDispatcher方法，该方法返回一个 RequestDispatcher对象，调用这个对象的forward方法可以实现请求转发；request对象同时也是一个域对象，开发人员通过request对象在实现转发时，把数据通过request对象带给其它web资源处理。

setAttribute方法 

getAttribute方法  

removeAttribute方法

getAttributeNames方法

请求转发细节：

forward方法用于将请求转发到RequestDispatcher对象封装的资源

如果在调用forward方法之前，在Servlet程序中写入的部分内容已经被真正地传送到了客户端，forward方法将抛出IllegalStateException异常

如果在调用forward方法之前向Servlet引擎的缓冲区(response)中写入了内容，只要写入到缓冲区中的内容还没有被真正输出到客户端，forward方法就可以被正常执行，原来写入到输出缓冲区中的内容将被清空，但是，已写入到HttpServletResponse对象中的响应头字段信息保持有效。 

    

**4.RequestDispatcher**

include方法：

RequestDispatcher.include方法用于将RequestDispatcher对象封装的资源内容作为当前响应内容的一部分包含进来，从而实现可编程的服务器端包含功能

被包含的Servlet程序不能改变响应消息的状态码和响应头，如果它里面存在这样的语句，这些语句的执行结果将被忽略。



**5.response重定向**

请求重定向指：一个web资源收到客户端请求后，通知客户端去访问另外一个web资源，这称之为请求重定向；

实现方式：response.sendRedirect(“/welcome.html”)；

实现原理：

302状态码和location头即可实现重定向；

5.response细节

6.response细节

getOutputStream和getWriter方法分别用于得到输出二进制数据、输出文本数据的ServletOuputStream、Printwriter对象。

getOutputStream和getWriter这两个方法互相排斥，调用了其中的任何一个方法后，就不能再调用另一方法。  

Servlet程序向ServletOutputStream或PrintWriter对象中写入的数据将被Servlet引擎从response里面获取，Servlet引擎将这些数据当作响应消息的正文，然后再与响应状态行和各响应头组合后输出到客户端。 

Serlvet的service方法结束后，Servlet引擎将检查getWriter或getOutputStream方法返回的输出流对象是否已经调用过close方法，如果没有，Servlet引擎将调用close方法关闭该输出流对象。 



**6.请求重定向和请求转发的区别**

一个web资源收到客户端请求后，通知服务器去**调用**另外一个web资源进行处理，称之为请求转发/307

一个web资源收到客户端请求后，通知浏览器去**访问**另外一个web资源进行处理，称之为请求重定向/302

-  RequestDispatcher.forward方法只能将请求转发给同一个WEB应用中的组件；而HttpServletResponse.sendRedirect 方法还可以重定向到同一个站点上的其他应用程序中的资源，甚至是使用绝对URL重定向到其他站点的资源。 

- 如果传递给HttpServletResponse.sendRedirect 方法的相对URL以“/”开头，它是相对于整个WEB站点的根目录；如果创建RequestDispatcher对象时指定的相对URL以“/”开头，它是相对于当前WEB应用程序的根目录。 

- 调用HttpServletResponse.sendRedirect方法重定向的访问过程结束后，浏览器地址栏中显示的URL会发生改变，由初始的URL地址变成重定向的目标URL；调用RequestDispatcher.forward 方法的请求转发过程结束后，浏览器地址栏保持初始的URL地址不变。

- HttpServletResponse.sendRedirect方法对浏览器的请求直接作出响应，响应的结果就是告诉浏览器去重新发出对另外一个URL的访问请求；RequestDispatcher.forward方法在服务器端内部将请求转发给另外一个资源，浏览器只知道发出了请求并得到了响应结果，并不知道在服务器程序内部发生了转发行为。 

- RequestDispatcher.forward方法的调用者与被调用者之间共享相同的request对象和response对象，它们属于同一个访问请求和响应过程；而HttpServletResponse.sendRedirect方法调用者与被调用者使用各自的request对象和response对象，它们属于两个独立的访问请求和响应过程。 



#### 项目结构

| 包名                     | 描述                                                         | 所属层次                              |
| ------------------------ | ------------------------------------------------------------ | ------------------------------------- |
| com.chixing.entity       | 存放系统的JavaBean类(只包含简单的属性以及属性对应的get和set方法，不包含具体的业务处理方法)，提供给【数据访问层】、【业务处理层】、【Web层】来使用 | entity(实体/（domain/model）域模型)层 |
| com.chixing.dao          | 存放访问数据库的操作接口类                                   | 数据访问层                            |
| com.chixing.service      | 存放处理系统业务接口类                                       | 业务处理层                            |
| com.chixing.service.impl | 存放处理系统业务接口的实现类                                 | 业务处理层                            |
| com.chixing.controller   | 存放作为系统控制器的Servlet                                  | Web层(表现层)                         |
| com.chixing.ui           | 存放为用户提供用户界面的servlet(UI指的是user interface)      | Web层(表现层)                         |
| com.chixing.filter       | 存放系统的用到的过滤器(Filter)                               | Web层(表现层)                         |
| com.chixing.listener     | 存放系统的用到的监听器(Listener)                             | Web层(表现层)                         |
| com.chixing.util         | 存放系统的通用工具类，提供给【数据访问层】、【业务处理层】、【Web层】来使用 |                                       |
| test                     | 存放系统的测试类                                             |                                       |

 **开发登录功能**

　　在com.chixing.ui包下写一个LoginUIServlet为用户提供登录界面

　　LoginUIServlet收到用户请求后，就跳到login.jsp

　　LoginUIServlet的代码如下：

```java
/**
 * LoginUIServlet负责为用户输出登陆界面
 * 当用户访问LoginUIServlet时，就跳转到WEB-INF/pages目录下的login.jsp页面
 */
public class LoginUIServlet extends HttpServlet {
    @Override
    protected void doGet(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
        request.getRequestDispatcher("/WEB-INF/pages/login.jsp").forward(request, response);
    }

    @Override
    protected void doPost(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
        this.doGet(req,resp);
    }
}
```



在/WEB-INF/pages/目录下编写用户登录的jsp页面login.jsp

　login.jsp页面的代码如下

```jsp
<form action="${pageContext.request.contextPath }/servlet/login" method="post" onsubmit="return formSubmit()">
     <input type="text" class="text"  name="username" placeholder="用户名"   >
     <input type="password"  name="password" placeholder="密码" >    
    <div class="submit">
        <input type="submit"  value="登录" >
    </div>
    <p><a href="#">忘记密码 ?</a></p>
</form>
```

LoginServlet的代码如下：

```java
public class LoginServlet extends HttpServlet {
    @Override
    protected void doGet(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {

           //获取用户填写的登录用户名
      String username = request.getParameter("username");
        //获取用户填写的登录密码
      String password = request.getParameter("password");

        String emailRegex = "^\\w+([-+.]\\w+)*@\\w+([-.]\\w+)*\\.\\w+([-.]\\w+)*$";
        String telnoRegex = "^[1][34578]\\d{9}$";

        CustomerService service = new CustomerServiceImpl();
        Customer customer = null;
        // 判断当前是不是邮箱登录
      if(username.matches(emailRegex)){
          customer = service.loginByEmail(username,password);
      }else{//判断当前是不是手机登录
          Long userTelno = Long.parseLong(username);
          customer = service.loginByPhone(userTelno,password);
      }

        //用户登录失败
        if(customer==null){
            String message = String.format(
                    "对不起，用户名或密码有误！！请重新登录！秒后为您自动跳到登录页面！！<meta http-equiv='refresh' content=';url=%s'",
                    request.getContextPath()+"/servlet/LoginUIServlet");
            request.setAttribute("message",message); //消息提示
            //页面分发
            request.getRequestDispatcher("/WEB-INF/page/login.jsp").forward(request, response);
            return;
        }
        //登录成功后，就将用户存储到session中
        request.getSession().setAttribute("loginUser", customer);
        String message = String.format(
                "恭喜：%s,登陆成功！本页将在秒后跳到首页！！<meta http-equiv='refresh' content=';url=%s'",
                customer.getCustName(),
                request.getContextPath()+"/index.jsp");
        request.setAttribute("message",message);
        request.getRequestDispatcher("/index.jsp").forward(request, response);
    }


    public void doPost(HttpServletRequest request, HttpServletResponse response)
            throws ServletException, IOException {
        doGet(request, response);
    }
```

**项目中的常量数据封装：**

constant

~~~
     *成功
     */
	public static final Integer STATUS_CODE_1 = 1;
    /**
	 * 失败
	 */
    public static final Integer STATUS_CODE_2 = 2;

    /**
	 *  验证码错误
	 */
    public static final Integer STATUS_CODE_3 = 3;

    /**
	 * 文件上传失败
	 */
    public static final Integer STATUS_CODE_4 = 4;
    /**
	 *默认文件上传路径
	 */
    public static final String UPLOAD_PATH = "localhost:8080/";
}

~~~





#### Cookie

> 饼干. 其实是一份小数据， 是服务器给客户端，并且存储在客户端上的一份小数据

应用场景？

> 自动登录、浏览记录、购物车。

为什么要有这个Cookie？

> http的请求是无状态。 客户端与服务器在通讯的时候，是无状态的，其实就是客户端在第二次来访的时候，服务器根本就不知道这个客户端以前有没有来访问过。 为了更好的用户体验，更好的交互 [自动登录]，其实从公司层面讲，就是为了更好的收集用户习惯[大数据]

Cookie怎么用？

- 添加Cookie给客户端

  在响应的时候，添加cookie

  ```java
  Cookie cookie = new Cookie("aa", "bb");	
  //给响应，添加一个cookie
  response.addCookie(cookie);
  ```

  客户端收到的信息里面，响应头中多了一个字段 Set-Cookie

- 获取客户端带过来的Cookie

  ~~~
  	Cookie[] cookies = request.getCookies();
  	if(cookies != null){
  		for (Cookie c : cookies) {
  			String cookieName = c.getName();
  			String cookieValue = c.getValue();
  			System.out.println(cookieName + " = "+ cookieValue);
  		}
  	}
  ~~~

- 常用方法

```java
	    //获得客户端发送过来的cookie
        Cookie[] cookies = request.getCookies();
        if(cookies !=null){
            for(Cookie cookie:cookies){
                System.out.println("cookie name :" + cookie.getName() + "value :" + cookie.getValue());
            }
        }
        //1. 先写cookie可以给客户端返回多个cookie
        Cookie cookie = new Cookie("stuName","Luwenxiang");
        //2. 该Cookie的有效期，默认情况下，关闭浏览器，cookie就没有了 -- 针对没有设置生命周期的cookie
        //expiry 有效 以秒计算
        //正数 在经过这个数字周期时间后，cookie将会失效，生命周期结束
        //负数：关闭浏览器，该cookie就失效
        cookie.setMaxAge(7*24*60*60);//一周内有效
        //cookie赋新的值
        cookie.setValue("Meilong");
        //用于指定只有请求了指定的域名，才会带上该cookie给服务器
        cookie.setDomain(".aispeech.com");
        //只有访问该域名下的cookieDemo2的这个路径，才会带上该cookie给服务器
        cookie.setPath("/cookieDemo2");
        response.addCookie(cookie);
        Cookie cookie2 = new Cookie("stuAge","20");
        response.addCookie(cookie2);
        response.getWriter().write("hello Cookie");
```

Cookie总结?

服务器给客户端发送过来的一小份数据，并且存放在客户端上。

获取cookie， 添加cookie

request.getCookie();

response.addCookie();

Cookie分类

会话Cookie:默认情况下，关闭了浏览器，那么cookie就会消失。

持久Cookie:

```
在一定时间内，都有效，并且会保存在客户端上。 

cookie.setMaxAge(0); //设置立即删除

cookie.setMaxAge(100); //100 秒
```

Cookie的安全问题。

> 由于Cookie会保存在客户端上，所以有安全隐患问题。  还有一个问题， Cookie的大小与个数有限制。 为了解决这个问题 ---> Session .



#### 例子一: 显示最近访问的时间。

1. 判断账号是否正确
2. 如果正确，则获取cookie。 但是得到的cookie是一个数组， 我们要从数组里面找到我们想要的对象。
3. 如果找到的对象为空，表明是第一次登录。那么要添加cookie
4. 如果找到的对象不为空， 表明不是第一次登录。 

```java
	if("admin".equals(userName) && "123".equals(password)){
		//获取cookie last-name --- >
		Cookie [] cookies = request.getCookies();
		
		//从数组里面找出我们想要的cookie
		Cookie cookie = CookieUtil.findCookie(cookies, "last");
		
		//是第一次登录，没有cookie
		if(cookie == null){
			
			Cookie c = new Cookie("last", System.currentTimeMillis()+"");
			c.setMaxAge(60*60); //一个小时
			response.addCookie(c);
			
			response.getWriter().write("欢迎您, "+userName);
			
		}else{
			//1. 去以前的cookie第二次登录，有cookie
			long lastVisitTime = Long.parseLong(cookie.getValue());
			
			//2. 输出到界面，
			response.getWriter().write("欢迎您, "+userName +",上次来访时间是："+new Date(lastVisitTime));
            //3. 重置登录的时间
			cookie.setValue(System.currentTimeMillis()+"");
			response.addCookie(cookie);
		}
	}else{
		response.getWriter().write("登陆失败 ");
	}
```

				

#### 例子二: 显示商品浏览记录。

从首页进入查询显示所有的商品  index.jsp

```jsp
<a href="${pageContext.request.contextPath}/shoes?type=0">全部商品</a>
```

获得所有的商品 ShoesServlet.java

```java
@Override
protected void doGet(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
        //1. 接受客户端请求操作类型
        Integer type = Integer.parseInt(request.getParameter("type"));
         switch (type){
             case 0:
                 getAll(request,response);break;
             case 1:
                 getById(request,response);break;
         }
}

 // 查询所有
    private void getAll(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {

        ShoesService service = new ShoesServiceImpl();
        List<Shoes> shoesList =  service.getAll();
        // 粗略书写 商品展示页面
        request.setAttribute("shoesList",shoesList);
        //跳转到所有商品页面
      request.getRequestDispatcher("/course/shoes_list.jsp").forward(request,response);
    }
```

显示所有商品 shoes_list.jsp

```jsp
<h2>全部商品</h2>
<%
    List<Shoes> shoesList  = (List<Shoes> )request.getAttribute("shoesList");
            for(Shoes shoes:shoesList){
            %>
     鞋子ID:  <a href="${pageContext.request.contextPath}/shoes?type=1&id=<%=shoes.getShoesId()%>">
           		<%= shoes.getShoesId()%>
             </a>
     鞋子名称: <a href="${pageContext.request.contextPath}/shoes?type=1&id=<%=shoes.getShoesId()%>"> <%= shoes.getShoesName()%></a>
     鞋子价格:  <%= shoes.getShoesPriceSale()%>  <br>
 <%
            }
 %>
```

点击查看单个商品详情 ,并记录浏览历史 ShoesServlet.java

```java
@Override
protected void doGet(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
        //1. 接受客户端请求操作类型
        Integer type = Integer.parseInt(request.getParameter("type"));
         switch (type){
             case 0:
                 getAll(request,response);break;
             case 1:
                 getById(request,response);break;
         }
}
   //根据id查询  (浏览)
    private void getById(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
        // 1. 获得id
       Integer id = Integer.parseInt( request.getParameter("id"));  // ""
       ShoesService service = new ShoesServiceImpl();
       Shoes shoes =  service.getById(id);

       // 保存到cookie
        Cookie cookie =  new Cookie("shoes"+id.toString(),id.toString());   // cookie("shoes101","101"), cookie("shoes102","102"), cookie("shoes103","103")
        cookie.setMaxAge(7*24*60*60);//一周内浏览记录保存

        response.addCookie(cookie);
        System.out.println("已经浏览该商品，id " + id  );
    }
```

显示所有浏览历史 shoes_list.jsp

```jsp
<h2>浏览记录</h2>
<%
             Cookie[] cookies = request.getCookies();
             if(cookies!=null){
                 for(Cookie cookie :cookies){
                     if(cookie.getName().contains("shoes")){
                         // 显示 鞋子id
 %>
        鞋子id : <%= cookie.getValue()%>
<%
            }
        }
    }
%>
```

 清除浏览记录

> 其实就是清除Cookie， 删除cookie是没有什么delete方法的。只有设置maxAge 为0 。

```java
	Cookie cookie = new Cookie("history","");
	cookie.setMaxAge(0); //设置立即删除
	cookie.setPath("/CookieDemo02");
	response.addCookie(cookie);
```





#### Session

    会话 ， Session是基于Cookie的一种会话机制。 Cookie是服务器返回一小份数据给客户端，并且存放在客户端上。 Session是，数据存放在服务器端。

- 常用API

```
	//得到会话ID
	String id = session.getId();
	
	//存值
	session.setAttribute(name, value);
	
	//取值
	session.getAttribute(name);
	
	//移除值
	session.removeAttribute(name);
```

- Session何时创建  ， 何时销毁?
- 创建

> 如果有在servlet里面调用了 request.getSession()

- 销毁

> session 是存放在服务器的内存中的一份数据。 当然可以持久化. Redis . 即使关了浏览器，session也不会销毁。

> 1. 关闭服务器

> 1. session会话时间过期。 有效期过了，默认有效期： 30分钟。

总结：

- 请求转发和重定向（面试经常问。）

- Cookie

  服务器给客户端发送一小份数据， 存放在客户端上。

  基本用法：

  ```
  添加cookie
  
  获取cookie。
  ```

  演练例子：

  ```
  1. 获取上一次访问时间
  
  2. 获取商品浏览记录。
  ```

- 什么时候有cookie

  response.addCookie(new Cookie())

- Cookie 分类

  会话Cookie

  ```
  	关闭浏览器，就失效
  
  持久cookie
  
  	存放在客户端上。 在指定的期限内有效。 
  
  	setMaxAge();
  ```

- Session

  也是基于cookie的一种会话技术，  数据存放存放在服务器端

  ```
  会在cookie里面添加一个字段 JSESSIONID . 是tomcat服务器生成。 
  
  setAttribute 存数据
   
  getAttribute 取数据
  
  removeAttribute  移除数据
  
  getSessionId();  获取会话id
  
  invalidate() 强制让会话失效。
  
  ```

- 创建和销毁

  ，调用request.getSesion创建 

   服务器关闭 ， 会话超时（30分）

setAttribute 存放的值， 在浏览器关闭后，还有没有。  有！，就算客户端把电脑砸了也还有。





#### 例子一: 登录示例

请求--------serlvet处理-----------响应 

login.jsp ---- LoginServlet----index.jsp 

请求页面 login.jsp

```jsp
<form action="${pageContext.request.contextPath }/course/servlet/login" method="post" onsubmit="return formSubmit()">
     <input type="text" class="text"  name="username"  placeholder="用户名"   >
     <input type="password"  name="password" placeholder="密码" >

    <div class="submit">
        <input type="submit"  value="登录" >
    </div>
</form>
```

LoginServlet

```java
//获取用户填写的登录用户名
String username = request.getParameter("username");
//获取用户填写的登录密码
String password = request.getParameter("password");

CustomerService service = new CustomerServiceImpl();
 
//业务层验证省略（参考之前完整版）
 
//登录成功后，就将用户存储到session中
request.getSession().setAttribute("loginCustomer", customer);
 
request.getRequestDispatcher("/course/index.jsp").forward(request, response);
```

响应页面index.jsp

```jsp
 <!-- 1. 账户未登录 ， 显示 登录超链接
      2. 账户已经登录， 显示账户用户名，退出按钮
-->
  <%
    if(session.getAttribute("loginCustomer") == null){ //  账户未登录 ，
  %>
  <a href="${pageContext.request.contextPath}/course/login.jsp">登录</a>
  <%
  }else{

  %>
  欢迎
  <%
    Customer customer = (Customer) session.getAttribute("loginCustomer");
  %>
  <%=customer.getCustName()%>
  <a href="${pageContext.request.contextPath}/servlet/logout">退出</a>
  <% } %>
```

退出请求流程

index.jsp(账户已经登录，产生退出请求)  ----- LogoutServlet  --- -- index.jsp(只有登录超链接，登录账户已经清空)

LogoutServlet

```java
@Override
protected void doGet(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
    // 1. 获得session1
    HttpSession session = req.getSession();
    //2.   登录账户信息从session中移除
    session.removeAttribute("loginCustomer");
    //3. 跳转到首页 （登录控件）
    req.getRequestDispatcher("/course/index.jsp").forward(req,resp);

}
```



#### 例子三: 简单购物车。

CartServlet.java

```java
	response.setContentType("text/html;charset=utf-8");
		//1. 获取要添加到购物车的商品id
		int id = Integer.parseInt(request.getParameter("id")); // 0 - 1- 2 -3 -4 
		String [] names = {"Iphone7","小米6","三星Note8","魅族7" , "华为9"};
		//取到id对应的商品名称
		String name = names[id];
		
		//2. 获取购物车存放东西的session  Map<String , Integer>  iphoen7 3
		//把一个map对象存放到session里面去，并且保证只存一次。 
		Map<String, Integer> map = (Map<String, Integer>) request.getSession().getAttribute("cart");
		//session里面没有存放过任何东西。
		if(map == null){
			map = new LinkedHashMap<String , Integer>();
			request.getSession().setAttribute("cart", map);
		}
        //3. 判断购物车里面有没有该商品
		if(map.containsKey(name)){
			//在原来的值基础上  + 1 
			map.put(name, map.get(name) + 1 );
		}else{
			//没有购买过该商品，当前数量为1 。
			map.put(name, 1);
		}
		
		//4. 输出界面。（跳转）
		response.getWriter().write("<a href='product_list.jsp'><h3>继续购物</h3></a><br>");
		response.getWriter().write("<a href='cart.jsp'><h3>去购物车结算</h3></a>");		
```

移除Session中的元素

```
	//强制干掉会话，里面存放的任何数据就都没有了。
	session.invalidate();
	
	//从session中移除某一个数据
	//session.removeAttribute("cart");
```



#### JSP简介

**1.什么是JSP?**

> (Java Server Page):从用户角度看待 ，就是是一个网页 ， 从程序员角度看待 ， 其实是一个java类， 它继承了servlet，所以可以直接说jsp 就是一个Servlet.

**2.为什么会有JSP?**

> html 多数情况下用来显示静态内容 ， 一成不变的。 但是有时候我们需要在网页上显示一些动态数据， 比如： 查询所有的学生信息， 根据姓名去查询具体某个学生。  这些动作都需要去查询数据库，然后在网页上显示。 html是不支持写java代码  ， jsp里面可以写java代码。 

#### JSP语法

#### JSP指令

**1.指令写法**

```java
<%@ 指令名字 %>
```

**2.page指令**

```jsp
<%@ page contentType="text/html;charset=UTF-8" language="java" %>
```

language: 表明jsp页面中可以写java代码

contentType: 文件类型及编码方式

pageEncoding: jsp内容编码

extends: 用于指定jsp翻译成java文件后，继承的父类是谁，一般不用改。

import: 导包使用的，一般不用手写

session:session 

> 值可选的有true or false ;
>
> 用于控制在这个jsp页面里面，能够直接使用session对象。
>
> 具体的区别是，请看翻译后的java文件   如果该值是true , 那么在代码里面会有getSession（）的调用，如果是false :  那么就不会有该方法调用，也就是没有session对象了。在页面上自然也就不能使用session了。

errorPage: 指的是错误的页面， 值需要给错误的页面路径

isErrorPage: 上面的errorPage 用于指定错误的时候跑到哪一个页面去。 那么这个isErroPage , 就是声明某一个页面到底是不是错误的页面。

**3.include**

```jsp
<!--包含另外一个jsp的内容进来-->
<%@ include file="top.jsp"%>
```

**4.taglib**

```
<%@ taglib prefix=""  uri=""%>  
uri: 标签库路径
prefix : 标签库的别名  
```



#### JSP动作

```jsp
<jsp:include page="top.jsp"></jsp:include>
<jsp:param value="" name=""/>
<jsp:forward page=""></jsp:forward>
```

**1.jsp:include**

> 包含指定的页面， 这里是动态包含。 也就是不把包含的页面所有元素标签全部拿过来输出，而是把它的运行结果拿过来。 

**2.jsp:forward**

> 前往哪一个页面。
>
> <% 
> 	//请求转发
> 	request.getRequestDispatcher("other02.jsp").forward(request, response);
> %>	  

**3.jsp:param**

> 意思是： 在包含某个页面的时候，或者在跳转某个页面的时候，加入这个参数。

```jsp
<jsp:forward page="to.jsp">
		<jsp:param value="beijing" name="address"/>
</jsp:forward>
```

```jsp
<!--在to.jsp中获取参数-->
<br>收到的参数是：<br>
<%= request.getParameter("address")%>
```



#### JSP九大隐式对象

**1.内置对象特点:**

- 由JSP规范提供,不用编写者实例化。
- 通过Web容器实现和管理
- 所有JSP页面均可使用
- 只有在脚本元素的表达式或代码段中才可使用(<%=使用内置对象%>或<%使用内置对象%>)

**2.内置对象功能及主要方法**

| **Jsp内置对象** | **功能**                                                     | **主要方法**                                                 |
| --------------- | ------------------------------------------------------------ | ------------------------------------------------------------ |
| out             | 向客户端输出数据                                             | print() println() flush() clear() isAutoFlush() getBufferSize() close() ………… |
| request         | 向客户端请求数据                                             | getAttributeNames() getCookies() getParameter() getParameterValues() setAttribute() getServletPath() ………….. |
| response        | 封装了jsp产生的响应,然后被发送到客户端以响应客户的请求       | addCookie() sendRedirect() setContentType()flushBuffer() getBufferSize() getOutputStream()sendError() containsHeader()…………… |
| application     |                                                              |                                                              |
| config          | 表示Servlet的配置,当一个Servlet初始化时,容器把某些信息通过此对象传递给这个Servlet | getServletContext() getServletName() getInitParameter() getInitParameterNames()…………… |
| page            | Jsp实现类的实例,它是jsp本身,通过这个可以对它进行访问         | flush()………                                                   |
| pagecontext     | 为JSP页面包装页面的上下文。管理对属于JSP中特殊可见部分中己经命名对象的该问 | forward() getAttribute() getException() getRequest() getResponse() getServletConfig()getSession() getServletContext() setAttribute()removeAttribute() findAttribute() …………… |
| session         | 用来保存每个用户的信息,以便跟踪每个用户的操作状态            | getAttribute() getId() getAttributeNames() getCreateTime() getMaxInactiveInterval()invalidate() isNew() |
| exception       | 反映运行的异常                                               | getMessage()…………                                             |

#### JSP四大作用域

**1.范围大小**

> pageContext << request << session << application 

- pageContext 【PageContext】

> 作用域仅限于当前的页面。  

> 还可以获取到其他八个内置对象。

- request 【HttpServletRequest】

> 作用域仅限于一次请求， 只要服务器对该请求做出了响应。 这个域中存的值就没有了。

- session 【HttpSession】

> 作用域限于一次会话（多次请求与响应） 当中。 

- application 【ServletContext】

> 整个工程都可以访问， 服务器关闭后就不能访问了。 



#### EL表达式

**1.作用**

> 是为了简化咱们的jsp代码，具体一点就是为了简化在jsp里面写的那些java代码。

**2.写法格式**

${表达式 }

> 如果从作用域中取值，会先从小的作用域开始取，如果没有，就往下一个作用域取。  一直把四个作用域取完都没有， 就没有显示。

**3.使用方法**



```jsp
	<%
		pageContext.setAttribute("name", "page");
		request.setAttribute("name", "request");
		session.setAttribute("name", "session");
		application.setAttribute("name", "application");
	%>
	
	按普通手段取值<br>
	
	<%= pageContext.getAttribute("name")%>
	<%= request.getAttribute("name")%>
	<%= session.getAttribute("name")%>
	<%= application.getAttribute("name")%>
	
	<br>使用EL表达式取出作用域中的值<br>
	
	${ pageScope.name }
	${ requestScope.name }
	${ sessionScope.name }
	${ applicationScope.name }
```

- 如果域中所存的是数组

```
   <%
       String [] a = {"aa","bb","cc","dd"};
       pageContext.setAttribute("array", a);
   %>
   使用EL表达式取出作用域中数组的值<br>
   ${array[0] },${array[1] },${array[2] },${array[3] }
```

- 如果域中所存的是集合

```jsp
	使用EL表达式取出作用域中集合的值<br>

	${li[0] } , ${li[1] },${li[2] },${li[3] }

	<br>-------------Map数据----------------<br>
	<%
		Map map = new HashMap();
		map.put("name", "zhangsna");
		map.put("age",18);
		map.put("address","北京..");
		map.put("address.aa","深圳..");
		pageContext.setAttribute("map", map);
	%>
```

- 取出Map集合的值

```jsp
   <%
   		Map map = new HashMap();
   		map.put("name", "zhangsna");
   		map.put("age",18);
   		map.put("address","北京..");
   		map.put("address.aa","深圳..");
   		pageContext.setAttribute("map", map);
   	%>
   	使用EL表达式取出作用域中Map的值<br>
   	${map.name } , ${map.age } , ${map.address }  , ${map["address.aa"] }
```



#### <%= %>和${ }的区别

<%=%>须明确指定从哪个对象里取值，例 :<%=x%> 取当前页面的x 值，<%=request.getAttrbutr("x")%>取request中的x值；
${x}(EL表达式)首先从当前页面找有没有x，有就显示它，没有，查找request，再没有就查找session，再没有就查找application再就有，就没办法了，输出空值（不是null）

<%=x%>如果x不存在，会报错
${x}就算x不存在，也不会报错
