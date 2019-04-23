#### SpringMVC 概述

MVC 框架提供了模型-视图-控制的体系结构和可以用来开发灵活、松散耦合的 web 应用程序的组件。MVC 模式导致了应用程序的不同方面(输入逻辑、业务逻辑和 UI 逻辑)的分离，同时提供了在这些元素之间的松散耦合。

- **模型**封装了应用程序数据，并且通常它们由 POJO 组成。
- **视图**主要用于呈现模型数据，并且通常它生成客户端的浏览器可以解释的 HTML 输出。
- **控制器**主要用于处理用户请求，并且构建合适的模型并将其传递到视图呈现。



#### SpringMVC 环境搭建

**（1）引入jar包**

![img](https://images0.cnblogs.com/blog2015/694841/201506/032131066955378.png)

**（2）配置文件**

**web.xml**

~~~xml
<?xml version="1.0" encoding="UTF-8"?>
<web-app xmlns="http://xmlns.jcp.org/xml/ns/javaee"
         xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xsi:schemaLocation="http://xmlns.jcp.org/xml/ns/javaee http://xmlns.jcp.org/xml/ns/javaee/web-app_4_0.xsd"
         version="4.0">

    <!-- 设置首页 -->
    <welcome-file-list>
        <welcome-file>index.jsp</welcome-file>
    </welcome-file-list>

    <!--实例化IoC容器:项目启动的时候启动监听器-->
    <listener>
        <listener-class>org.springframework.web.context.ContextLoaderListener</listener-class>
    </listener>
    <!-- 防止Spring内存溢出监听器 -->
    <listener>
        <listener-class>org.springframework.web.util.IntrospectorCleanupListener</listener-class>
    </listener>

    <!-- 编码过滤器 -->
    <filter>
        <filter-name>characterEncodingFilter</filter-name>
        <filter-class>org.springframework.web.filter.CharacterEncodingFilter</filter-class>
        <init-param>
            <param-name>encoding</param-name>
            <param-value>utf-8</param-value>
        </init-param>
        <init-param>
            <param-name>forceEncoding</param-name>
            <param-value>true</param-value>
        </init-param>
    </filter>
    <filter-mapping>
        <filter-name>characterEncodingFilter</filter-name>
        <url-pattern>/*</url-pattern>
    </filter-mapping>

    <!--IoC容器文件的位置 -->
    <context-param>
        <param-name>contextConfigLocation</param-name>
        <!--tomcat服务器中文件的路径-->
        <param-value>classpath:applicationContext.xml</param-value>
    </context-param>

    <!--前端控制器（一级控制器）：DispatcherServlet,所有的请求都到DispatcherServlet来处理-->
    <servlet>
        <servlet-name>SpringMVC</servlet-name>
        <servlet-class>org.springframework.web.servlet.DispatcherServlet</servlet-class>
        <!-- 配置springmvc-servlet.xml的位置 -->
        <init-param>
            <param-name>contextConfigLocation</param-name>
            <!--tomcat服务器中文件的路径-->
            <param-value>classpath:springmvc-servlet.xml</param-value>
        </init-param>
        <!-- 正整数 表示在项目启动的时候，就实例化与初始化init 该DispatcherServlet-->
        <load-on-startup>1</load-on-startup>
    </servlet>
    <servlet-mapping>
        <servlet-name>SpringMVC</servlet-name>
        <!-- 此处可以可以配置成*.do，对应struts的后缀习惯 -->
        <url-pattern>/</url-pattern>
    </servlet-mapping>

</web-app>
~~~

**springmvc-servlet.xml**

~~~xml
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xmlns:context="http://www.springframework.org/schema/context"
       xmlns:mvc="http://www.springframework.org/schema/mvc"
       xsi:schemaLocation="http://www.springframework.org/schema/beans http://www.springframework.org/schema/beans/spring-beans.xsd http://www.springframework.org/schema/context http://www.springframework.org/schema/context/spring-context.xsd http://www.springframework.org/schema/mvc http://www.springframework.org/schema/mvc/spring-mvc.xsd">

    <!-- 自动扫描该包，使SpringMVC认为包下用了@Controller注解的类是次级控制器（二级控制器）-->
    <context:component-scan base-package="com.springmvc.controller"></context:component-scan>

    <!-- 扩充了注解驱动，可以将请求参数绑定到控制器参数 -->
    <mvc:annotation-driven/>

    <!-- 静态资源处理  css js imgs -->
    <mvc:resources location="/static/images/" mapping="/static/images/*.jsp"/>

    <!-- 视图模式配置:掐头去尾 -->
    <bean class="org.springframework.web.servlet.view.InternalResourceViewResolver">
        <!-- controller层方法返回的字符串加上前缀和后缀(return "xx"; => /xx.jsp)-->
        <!-- 前缀 -->
        <property name="prefix" value="/"></property>
        <!-- 后缀 -->
        <property  name="suffix" value=".jsp"></property>
    </bean>

    <!-- 转换器 -->
    <mvc:annotation-driven conversion-service="conversionService"/>
    <bean id="conversionService" class="org.springframework.context.support.ConversionServiceFactoryBean">
        <property name="converters">
            <list>
                <bean class="com.springmvc.converter.RectangleConverter"/> <!--自定义转换器-->
                <bean class="com.springmvc.converter.DateConverter"/><!--日期类型转换器-->
            </list>
        </property>
    </bean>
    <!--<mvc:annotation-driven conversion-service="formattingConversionService"/>-->
    <!--<bean id="formattingConversionService" class="org.springframework.format.support.FormattingConversionServiceFactoryBean">-->
        <!--<property name="converters">-->
            <!--<list>-->
                <!--<bean class="com.springmvc.converter.RectangleConverter"/>-->
                <!--<bean class="com.springmvc.converter.DateConverter"/>-->
            <!--</list>-->
        <!--</property>-->
    <!--</bean>-->


    <!-- 视图模板 -->
    <bean class="org.springframework.web.servlet.view.BeanNameViewResolver">
        <property name="order" value="0"></property>
    </bean>

    <!-- 拦截器配置:项目启动实例化 -->
    <mvc:interceptors>
        <mvc:interceptor>
            <mvc:mapping path="/order/*"/>
            <bean class="com.springmvc.interceptor.MyInterceptor"/>
        </mvc:interceptor>

        <mvc:interceptor>
            <mvc:mapping path="/customer/*"/>
            <bean class="com.springmvc.interceptor.CheckLoginInterceptor"/>
        </mvc:interceptor>
    </mvc:interceptors>

    <!-- 配置文件上传，如果没有使用文件上传可以不用配置，当然如果不配，那么配置文件中也不必引入上传组件包 -->
    <bean id="multipartResolver" class="org.springframework.web.multipart.commons.CommonsMultipartResolver">
    <!-- 默认编码 -->
    <property name="defaultEncoding" value="utf-8" />
    <!-- 文件大小最大值 -->
    <property name="maxUploadSize" value="10485760000" />
    <!-- 内存中的最大值 -->
    <property name="maxInMemorySize" value="40960" />
    <!-- 启用是为了推迟文件解析，以便捕获文件大小异常 -->
    <property name="resolveLazily" value="true"/>
    </bean>

</beans>
~~~

**applicationContext.xml**

~~~xml
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xmlns:context="http://www.springframework.org/schema/context"
       xsi:schemaLocation="http://www.springframework.org/schema/beans http://www.springframework.org/schema/beans/spring-beans.xsd http://www.springframework.org/schema/context http://www.springframework.org/schema/context/spring-context.xsd">

    <!-- Spring整合SpringMVC-->
    <!-- 引入注解-->
    <context:annotation-config/>

    <context:component-scan base-package="com.springmvc"></context:component-scan>

</beans>
~~~



#### SpringMVC 工作原理 

![这里写图片描述](https://img-blog.csdn.net/20170827115532950?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQvd2RlaHhpYW5n/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/SouthEast)

（1）用户向服务器发送请求，请求被前端控制器DispatcherServlet捕获；

（2）DispatcherServlet对请求URL进行解析，得到请求资源标识符（URI）。然后根据该URI，调用HandlerMapping获得该Handler配置的所有相关的对象（包括Handler对象以及Handler对象对应的拦截器），最后以HandlerExecutionChain对象的形式返回；

（3）DispatcherServlet 根据获得的Handler，选择一个合适的HandlerAdapter。（附注：如果成功获得HandlerAdapter后，此时将开始执行拦截器的preHandler(...)方法）；

（4） 提取Request中的模型数据，填充Handler入参，开始执行Handler（Controller)。 在填充Handler的入参过程中，根据你的配置，Spring将帮你做一些额外的工作：HttpMessageConveter： 将请求消息（如Json、xml等数据）转换成一个对象，将对象转换为指定的响应信息
数据转换：对请求消息进行数据转换。如String转换成Integer、Double等
数据根式化：对请求消息进行数据格式化。 如将字符串转换成格式化数字或格式化日期等
数据验证： 验证数据的有效性（长度、格式等），验证结果存储到BindingResult或Error中

（5）Handler执行完成后，向DispatcherServlet 返回一个ModelAndView对象；

（6）根据返回的ModelAndView，选择一个适合的ViewResolver（必须是已经注册到Spring容器中的ViewResolver)返回给DispatcherServlet ；

（7）ViewResolver 结合Model和View，来渲染视图；

（8）将渲染结果返回给客户端；

**Spring为什么要结合使用HandlerMapping以及HandlerAdapter来处理Handler?**
    符合面向对象中的单一职责原则，代码架构清晰，便于维护，最重要的是代码可复用性高。如HandlerAdapter可能会被用于处理多种Handler。





#### SpringMVC 核心组件

**（1）DispatherServlet:前端控制器**

	SpringMVC的核心类DispatherServlet,负责截获请求并将其分派给相应的处理器处理;DispatherServlet接收到请求后，根据请求的信息（包括URL、HTTP方法、请求报文头、请求参数、Cookie等）以及HandlerMapping的配置找到处理请求的处理器。

**（2）HandlerMapping:处理器映射器**

	根据URL去查找处理器，一般通过xml配置或者注解进行查找。

**（3）Handler：处理器**

	就是我们常说的controller控制器啦，由程序员编写。

**（4）HandlerAdapter:处理器适配器**

	可以将处理器包装成适配器，这样就可以支持多种类型的处理器。

**（5）ModelAndView**

	该对象包含两部分内容，一部分是视图相关内容，可以是逻辑视图名称，也可以是具体的View实例；另一部分是某型数据，视图渲染过程中将会把这些模型数据合并入最终的视图输出。所以，简单来说，ModelAndView实际就是一个数据对象。

**（6）ViewResolver:视图定位器**

	主要职责是根据Controller所返回的ModerAndView中的逻辑视图名，为DispatherServlet返回一个可用的View对象。

**（7）View**

	主要职责是实现最终的视图渲染工作，但对渲染工作来说是透明的，DispatherServlet只是直接接触ViewResolver返回的View接口，获得相应引用后把视图渲染工作交给返回的View实例即可。至于View实例是什么类型，具体工作如何完成，DispatherServlet无需关心。





#### SpringMVC 常用注解

**@Controller:**负责注册一个bean 到spring 上下文中

**@RequestMapping:**注解为控制器指定可以处理哪些URL请求

**@RequestBody:**该注解用于读取Request请求的body部分数据，使用系统默认配置的HttpMessageConverter进行解析，然后把相应的数据绑定到要返回的对象上 ,再把HttpMessageConverter返回的对象数据绑定到 controller中方法的参数上;

**@ResponseBody:**该注解用于将Controller的方法返回的对象，通过适当的HttpMessageConverter转换为指定格式后，写入到Response对象的body数据区

**@ModelAttribute:** 在方法定义上使用 @ModelAttribute 注解：Spring MVC 在调用目标处理方法前，会先逐个调用在方法级上标注了@ModelAttribute 的方法;在方法的入参前使用 @ModelAttribute 注解：可以从隐含对象中获取隐含的模型数据中获取对象，再将请求参数 –绑定到对象中，再传入入参将方法入参对象添加到模型中 

**@RequestParam:**在处理方法入参处使用 @RequestParam 可以把请求参 数传递给请求方法;

**@PathVariable:**绑定 URL 占位符到入参;

**@ExceptionHandler:**注解到方法上，出现异常时会执行该方法

**@ControllerAdvice:**使一个Contoller成为全局的异常处理类，类中用@ExceptionHandler方法注解的方法可以处理所有Controller发生的异常

#### SpringMVC 接收参数

**（1）Spring会自动将表单参数注入到方法参数，和表单的name属性保持一致**

```java
@RequestMapping("login")
public String login(String custName,String custPwd){
    System.out.println("CustomerController login");
    System.out.println("登录的用户名:" + custName + ",密码：" + custPwd);
｝
```

**（2）注解**

~~~java
@RequestMapping("/login")
public String login(@RequestParam("custName") String name,
                    @RequestParam("custPwd") String password){
    //底层：String name = requests.getParameter("custName")
    System.out.println("name="+name);
    System.out.println("password="+password);
    return "hello";
}
~~~

**（3）自动注入Bean属性**

```java
@RequestMapping("add")
public String regist( Customer customer  ){
	System.out.println("customer = " + customer);
}
```





#### SpringMVC 数据绑定

**当Controller组件处理后，向前台页面传值，**

**（1）使用HttpServletRequest 和 Session  然后setAttribute()，就和Servlet中一样**	

```java
request.setAttribute(key,value)
session.setAttribute(key,value)
```

**（2）使用ModelAndView对象**

```java
    @RequestMapping("/login")
    public ModelAndView login(Customer customer, HttpServletRequest request){
        String custName=customer.getCustName();
        String custPwd=customer.getCustPwd();
        System.out.println("用户名："+custName+",密码:"+custPwd);
        
        ModelAndView mav=new ModelAndView();
        if(custName.equals("123") && custPwd.equals("123")){
            //mav.addObject("custName","custName");
            //底层封装了request,没有Session
            request.getSession().setAttribute("custName",custName);
            mav.setViewName("main");
        }else{
            //request.setAttribute("message","用户名或密码不正确");
            mav.addObject("message","用户名或密码不正确！");
       //request.getRequestDispatcher("/customer/login.jsp").forward(request,response);
            mav.setViewName("customer/login");
        }
        return mav;
    }
```

**（3）使用ModelMap对象**

```
ModelMap.addAttribute(key,value)
```

**（4）使用@ModelAttribute注解**

 ~~~
public String login(@ModelAttribute("user") User user){...}
 ~~~





#### SpringMVC 页面分发

**Spring MVC 默认采用的是转发来定位视图，如果要使用重定向，可以如下操作**

**（1）使用RedirectView**

```
RedirectView view = new RedirectView("index.jsp")
```

return new ModelAndView(view)

**（2）使用redirect:前缀**

~~~
return "redirect:index.jsp"
~~~



#### SpringMVC 视图模版-Excel

**请求接口**

```jsp
 <a href="user/showUserListInExcel">导出用户信息为excel文档</a>
```

**UserController.java**

~~~java
@Controller
@RequestMapping("/user")
public class UserController{	
	@RequestMapping("showUserListInExcel")
	public String showUserListInExcel(ModelMap mm){
		 //获得到所有用户的信息
		List<User> userList =  this.userService.getAllUser();
		if(userList ==null){
			mm.addAttribute("msg", "暂无用户数据");
		}else{
			mm.addAttribute("userList", userList);
		}		 
		 return "userListExcelView"; // 响应视图名 forward excel
        						 
	}
}
~~~

**UserListExcelView.java**

~~~java
/**
 * 用户信息的Excel展示  --- 自定义的视图解析器
 */
@Controller
public class UserListExcelView extends AbstractExcelView{

	@Override
	protected void buildExcelDocument(Map<String, Object> model, HSSFWorkbook workbook, HttpServletRequest request, HttpServletResponse response) 	throws Exception {
		 response.setHeader("Content-Dispostion", "inline;filename=" + new String("用户列表".getBytes(),"iso8859-1"));
		 
		 List<User> userList =( List<User> )  model.get("userList");		 
		 HSSFSheet sheet = workbook.createSheet("用户列表工作表");
		 HSSFRow head =sheet.createRow(0);
		 head.createCell(0).setCellValue("用户编号");
		 head.createCell(1).setCellValue("用户真是姓名");
		 head.createCell(2).setCellValue("用户登录名");
		 head.createCell(3).setCellValue("用户性别");
		 head.createCell(4).setCellValue("用户生日");
		 head.createCell(5).setCellValue("用户手机");
		 head.createCell(6).setCellValue("用户邮箱");
		 head.createCell(7).setCellValue("用户地址");
		 
		 int rowNum = 1;
		 for(User user:userList){
			 HSSFRow row =sheet.createRow(rowNum++);
			 row.createCell(0).setCellValue(user.getUserId());
			 row.createCell(1).setCellValue(user.getUserRealname());
			 row.createCell(2).setCellValue(user.getUserLoginName());
			 row.createCell(3).setCellValue(user.getUserGender() == 0?"男性":"女性");
			 row.createCell(4).setCellValue(new SimpleDateFormat("yyyy-MM-dd").format(user.getUserBirth()));
			 row.createCell(5).setCellValue(user.getUserTelno());
			 row.createCell(6).setCellValue(user.getUserEmail());
			 row.createCell(7).setCellValue(user.getUserAddress());
		 }
		 		
	}

}
~~~

**Springmvc-servlet.xml**

```xml
 <bean class="org.springframework.web.servlet.view.BeanNameViewResolver">
 	<property name="order" value="10"></property>
 </bean>
<!--或者通过Annotation方式注入 @Controller -->
<bean id ="userListExcelView" class="com.chixing.controller.UserListExcelView" />
```



#### SpringMVC 转换器

CustomDateConverter.java

```java
public class CustomDateConverter implements Converter<String,Date>{
   public CustomDateConverter(){
      System.out.println("实例化CustomDateConverter");
   }

   public Date convert(String source) {
      SimpleDateFormat sdf=new SimpleDateFormat("yyyy-MM-dd HH:mm:ss");
      try {
         return sdf.parse(source);
      } catch (ParseException e) {      
         e.printStackTrace();
      }
      return null;
   }
}
```

Springmvc-servlet.xml

```xml
<mvc:annotation-driven conversion-service="conversionService" />
<bean id="conversionService" class="org.springframework.format.support.FormattingConversionServiceFactoryBean">
    <property name="converters">
        <list>
            <bean class="com.chixing.util.CustomDateConverter"/>
        </list>
    </property>
</bean>
```

**在spring 中定义了3中类型转换接口**，分别为：

1. Converter接口              ：使用最简单，最不灵活；
2. ConverterFactory接口  ：使用较复杂，比较灵活；
3. GenericConverter接口 ：使用最复杂，也最灵活；

4. 前台传递的数据格式形如：“zhangSan：888”；

```
http://localhost:8080/SpringMVCTest/test/conversionTest.action?person=zhangsan:888
```

```java
   class Person{
   	String username;
   	String password;
   }
```

**解决步骤：**

1. 定义转换类，实现Converter<S,T>接口；
2. 装配自定义的conversionService; 

```java
public class StringToPersonConverter implements Converter<String,Person>{
	public Person convert(String source) {
		Person p1 = new Person();
		if(source != null){
			String[] items = source.split(":");
			p1.setUsername(items[0]);
			p1.setPasswd(items[1]);
		}
		return p1;
	}
}
```

```xml
<mvc:annotation-driven conversion-service="conversionService"/>
<bean id="conversionService"
		class="org.springframework.context.support.ConversionServiceFactoryBean">
		<property name="converters">
			<list>
				<bean class="com.chixing.convertor.StringToPersonConverter" />
			</list>
		</property>
</bean>
```

Controller

```java
public String conversionTest(@RquestParam ("person") Person p,ModelMap modelMap){
	modelMap.put("person",p);
    return "test";
}
```

当前台发送请求：

<http://localhost:8080/SpringMVCTest/test/conversionTest.action?person=zhangsan:888  时；

将person=zhangsan:888传递到后台，被StringToPersonConverter转换为Person对象；

跳转到界面：test.jsp

```jsp
<body>
	用户名：${person.username},
    密码：${person.password}
</body>
```



#### SpringMVC 拦截器

需要在springmvc-servlet.xml文件中配置:

~~~xml
	<!--配置拦截器, 多个拦截器,顺序执行 -->
	<mvc:interceptors>
		<mvc:interceptor>
			<!--
				--需要拦截的请求
                /**的意思是所有文件夹及里面的子文件夹
                /*是所有文件夹，不含子文件夹
                /是web项目的根目录
              -->
			<mvc:mapping path="/*" />
			<!-- 无需拦截的请求 -->
			<mvc:exclude-mapping path="/user"/>
			<bean id="loginInterceptor" class="com.gaeainfo.grid.interceptor.LoginInterceptor"></bean>
		</mvc:interceptor>
		<!-- 当设置多个拦截器时，先按顺序调用preHandle方法，然后逆序调用每个拦截器的postHandle和afterCompletion方法  -->
	</mvc:interceptors>
~~~



MyInterceptor.java

~~~java
/**
 * 拦截器
 */
public class MyInterceptor implements HandlerInterceptor {

    public MyInterceptor() {
        System.out.println("MyInterceptor拦截器实例化。");
    }

    //在真正请求执行之前就需要做的拦截动作，比如： 登录检查，权限检查
    @Override
    public boolean preHandle(HttpServletRequest httpServletRequest, HttpServletResponse httpServletResponse, Object o) throws Exception {
        System.out.println("订单执行之前的拦截方法。。。。");
        return true;
    }

    //在真正请求执行之后， 视图返回之前，执行的拦截动作
    @Override
    public void postHandle(HttpServletRequest httpServletRequest, HttpServletResponse httpServletResponse, Object o, ModelAndView modelAndView) throws Exception {
        System.out.println("订单执行之后，视图未响应，需要执行的拦截方法。。。。");
    }

    //在真正请求执行之后 再执行的拦截动作， 比如：一部分日志
    @Override
    public void afterCompletion(HttpServletRequest httpServletRequest, HttpServletResponse httpServletResponse, Object o, Exception e) throws Exception {
        System.out.println("订单执行之后的拦截方法。。。。");
    }
}
~~~



CheckLoginInterceptor.java

~~~java
package com.springmvc.interceptor;

import org.springframework.web.servlet.HandlerInterceptor;
import org.springframework.web.servlet.ModelAndView;

import javax.servlet.http.HttpServletRequest;
import javax.servlet.http.HttpServletResponse;

/**
 * 验证用户是否登录拦截器
 */
public class CheckLoginInterceptor implements HandlerInterceptor {

    public CheckLoginInterceptor() {
        System.out.println("CheckLoginInterceptor拦截器实例化！");
    }

    @Override
    public boolean preHandle(HttpServletRequest request, HttpServletResponse response, Object o) throws Exception {

        if( request.getSession().getAttribute("custName")!=null){
            return true;
        }else{
            //获取url
            String url=request.getRequestURI();
            //修改用户或删除用户时拦截
            if(url.contains("customer/update")||url.contains("customer/delete")){
                request.getRequestDispatcher("/customer/login.jsp").forward(request,response);
                return false;
            }else{
                return true;
            }
        }
    }

    @Override
    public void postHandle(HttpServletRequest httpServletRequest, HttpServletResponse httpServletResponse, Object o, ModelAndView modelAndView) throws Exception {

    }

    @Override
    public void afterCompletion(HttpServletRequest httpServletRequest, HttpServletResponse httpServletResponse, Object o, Exception e) throws Exception {

    }
}
~~~













