

#### Http协议

#### **定义**

HTTP协议(Hypertext Transfer Protocol,超文本传输协议)：是一个客户端与回应的标准协议。

#### **请求-响应式协议**

HTTP协议用于在Internet上发送和接收消息。

HTTP协议是一种请求-响应式的协议——客户端发送一个请求，服务器返回该请求的应答

所有的请求与应答都是HTTP包。

HTTP协议使用可靠的TCP连接，默认端口是80。

HTTP的第一个版本是HTTP/0.9，后来发展到了HTTP/1.0，现在最新的版本是HTTP/1.1。 

#### **无状态的协议**

在HTTP中，Client/Server之间的会话总是由客户端通过建立连接和发送HTTP请求包初始化，服务器不会主动联系客户端或要求与客户端建立连接。

浏览器和服务器都可以随时中断连接，例如，在浏览网页时你可以随时点击“停止”按钮中断当前的文件下载过程，关闭与Web服务器的HTTP连接。

不维持状态，一次请求和响应构成一个独立的事务，不同事务之间没有状态联系  

#### **URI&&URL**

**URI**： Universal Resource Identifier 通用资源标志符，Web上可用的每种资源 ，如 HTML文档、图像、视频片段、程序等， 由URI进行定位。 

由三部分组成：  

. 访问资源的命名机制。

. 存放资源的主机名。 

. 资源自身的名称，由路径表示。 

**URL**：Uniform Resource Location 统一资源定位符，Internet上用来描述信息资源的字符串，主要用在各种WWW客户程序和服务器程序上 ，采用URL可以用一种统一的格式来描述各种信息资源，包括文件、服务器的地址和目录等。

由下列三部分组成：

第一部分是协议（或称为服务方式）；

第二部分是存有该资源的主机IP地址（有时也包括端口号）； 

第三部分是主机资源的具体地址，如目录和文件名等。 

第一部分和第二部分之间用“：//”符号隔开;

第二部分和第三部分用“/”符号隔开。

第一部分和第二部分是不可缺少的，第三部分有时可以省略。

语法如下：HTTP_URL＝http://host[“:” port]/[ path ] 

示例：http://www.tianqi.com:80/suzhou/15/

#### **HTTP请求包（Request）**

由三个部分构成:

**方法-URI-协议/版本**：get-xxxxxx-http/1.1；post-xxxxxx-http/1.1；

eg:GET /index.jsp HTTP/1.1

**请求头**：**get方式**的请求数据（例如：苏州天气）会显示在URL后面;

eg：

lAccept-Language: zh-cn
Connection: Keep-Alive 
Host: 192.168.0.106
Content-Length: 37

wd=suzhou

**请求正文**： **post方式**的请求数据数据(例如：登录操作的用户名与密码)

#### **HTTP响应包（Response）**

由三个部分构成:

**协议-状态代码-描述**:

HTTP/1.1 200 OK

**响应头**:

lServer:
Microsoft-IIS/4.0
Date: Mon, 3 Jan 2005 13:13:33 GMT
Content-Type: text/html
Last-Modified: Mon, 11 Jan 2004 13:23:42 GMT
Content-Length: 90

**响应正文**:

#### **HTTP最基本的请求类型 get 和 post**

--**HTTP1.1**支持七种请求方法：get、post、head、options、put、delete和trace等

--**get**请求最为常见，它后面跟随一个网页的位置，服务器接受请求并返回其请求的页面。除了页面位置作参数之外，请求还可以跟随[协议](http://www.cnpaf.net/)的版本如HTTP/1.0等作为参数，以发送给服务器更多的信息。

```
<form  name = "myform" action="success.html" method="get" > 
 		姓名：<input type="text"   name="username"  />
		密码：<input type="password"  name="pwd" /><br/>
		     <input type="submit" value="注册" />
</form>
get提交，请求的数据会附在URL之后（把数据放置在HTTP协议头中），以?分割URL和传输数据，多个参数用&连接；
 例如：success.html?username=Jack&pwd=abc123&hobby=%E6%B8%B8%E6%B3%B3。
如果数据是英文字母/数字，原样发送，如果是空格，转换为+，如果是中文/其他字符，则直接把字符串用BASE64加密，得出如： 你好，其中％XX中的XX为该符号以16进制表示的ASCII。
```

--**post**请求要求服务器接收大量的信息，除了POST后面跟随的参数之外，浏览器还会在后面持续发送数据，让服务器进行处理。通常，POST方法是和CGI程序分不开的，服务器应该启动一个CGI程序来处理POST发送来的数据。 

```
<form  name = "myform" action="success.html" method="post" > 
 		姓名：<input type="text"   name="username"  />
		密码：<input type="password"  name="pwd" /><br/>
		        <input type="submit" value="注册" />
</form>
post提交：把提交的数据放置在是HTTP包的包体中。GET提交的数据会在地址栏中显示出来，而post提交，地址栏不会改变.
```

#### **总结 get与post的区别：**

get表示用于信息获取，而且应该是安全的;

post表示可能修改变服务器上的资源的请求。

区别：

get请求的数据放置在HTTP协议头中，所以

–get请求的数据会附在URL之后,浏览器有缓冲，可记录用户信息；

–get方式提交的数据不安全

–get方式提交的数据最多只能是1024字节

–

post请求的数据放置在HTTP协议正文中，所以：

–post请求的数据的安全性要比get的安全性高。 

– post方式提交的数据字节数较大，适合大规模的数据传送。

|                  | GET                                                          | POST                                                         |
| ---------------- | ------------------------------------------------------------ | ------------------------------------------------------------ |
| 后退按钮/刷新    | 无害                                                         | 数据会被重新提交（浏览器应该告知用户数据会被重新提交）。     |
| 书签             | 可收藏为书签                                                 | 不可收藏为书签                                               |
| 缓存             | 能被缓存                                                     | 不能缓存                                                     |
| 编码类型         | application/x-www-form-urlencoded                            | application/x-www-form-urlencoded or multipart/form-data。为二进制数据使用多重编码。 |
| 历史             | 参数保留在浏览器历史中。                                     | 参数不会保存在浏览器历史中。                                 |
| 对数据长度的限制 | 是的。当发送数据时，GET 方法向 URL 添加数据；URL 的长度是受限制的（URL 的最大长度是 2048 个字符）。 | 无限制。                                                     |
| 对数据类型的限制 | 只允许 ASCII 字符。                                          | 没有限制。也允许二进制数据。                                 |
| 安全性           | 与 POST 相比，GET 的安全性较差，因为所发送的数据是 URL 的一部分。  在发送密码或其他敏感信息时绝不要使用 GET ！ | POST 比 GET 更安全，因为参数不会被保存在浏览器历史或 web 服务器日志中。 |
| 可见性           | 数据在 URL 中对所有人都是可见的。                            | 数据不会显示在 URL 中。                                      |





#### **HTTP协议状态码的含义**

| 状态代码 | 状态信息              | 含义                                                         |
| :------: | --------------------- | ------------------------------------------------------------ |
|   400    | Bad Request           | 请求出现语法错误。                                           |
|   401    | Unauthorized          | 客户试图未经授权访问受密码保护的页面。                       |
|   403    | Forbidden             | 资源不可用。服务器理解客户的请求，但拒绝处理它。通常由于服务器上文件或目录的权限设置导致。 |
|   404    | Not Found             | 无法找到指定位置的资源。这也是一个常用的应答。               |
|   500    | Internal Server Error | 服务器遇到了意料不到的情况，不能完成客户的请求。             |
|   501    | Not Implemented       | 服务器不支持实现请求所需要的功能。   例如，客户发出了一个服务器不支持的PUT请求。 |

#### **网络开发的两种模式**

**C/S模式(Client/Server模式)**：即客户/服务器模式。每个客户端需要安装工具软件，管理和维护客户端和服务器端都需要同时更改。例如：QQ,MSN等。

**B/S模式(Browser/Server模式)**：即浏览器/服务器模式。在服务器端安装软件，客户端通过浏览器访问服务器，从而实现信息、资源的交互与共享，只需要管理和维护服务器端即可。例如：论坛等。



#### ajax、axios、fetch？

1.原生请求

~~~
 var ajax = null;
 if (window.XMLHttpRequest) {
   ajax = new XMLHttpRequest(); //for ie7+,FireFox,Chorme,Opera,Safai...
 } else {
   ajax = new ActiveXObject('Microsoft.XMLHTTP'); //for ie6
 } 
ajax.open("GET","/customer/getinfo",true);
ajax.send(null);
ajax.onreadystatechange=function(){
    if(ajax.readyState==4){
        if(ajax.status==200){
            console.log(ajax.responseText);
        }else{
            console.log('请求失败！')
        }
    }
};
~~~

2.jQuery ajax

~~~
$.ajax({
   type: 'POST',
   url: url,
   data: data,
   dataType: dataType,
   success: function () {},
   error: function () {}
});
~~~

优缺点：

- 本身是针对MVC的编程,不符合现在前端MVVM的浪潮
- 基于原生的XHR开发，XHR本身的架构不清晰，已经有了fetch的替代方案
- JQuery整个项目太大，单纯使用ajax却要引入整个JQuery非常的不合理（采取个性化打包的方案又不能享受CDN服务）

3.axios

~~~
axios({
    method: 'post',
    url: '/user/12345',
    data: {
        firstName: 'Fred',
        lastName: 'Flintstone'
    }
})
.then(function (response) {
    console.log(response);
})
.catch(function (error) {
    console.log(error);
});

~~~

优缺点：

- 从 node.js 创建 http 请求
- 支持 Promise API
- 客户端支持防止CSRF
- **提供了一些并发请求的接口**（重要，方便了很多的操作）

4.fetch

~~~
try {
  let response = await fetch(url);
  let data = response.json();
  console.log(data);
} catch(e) {
  console.log("Oops, error", e);
}
~~~

优缺点：

- 符合关注分离，没有将输入、输出和用事件来跟踪的状态混杂在一个对象里，更好更方便的写法，更加底层，提供的API丰富（request, response）脱离了XHR，是ES规范里新的实现方式
- fetcht只对网络请求报错，对400，500都当做成功的请求，需要封装去处理
- fetch默认不会带cookie，需要添加配置项
- fetch不支持abort，不支持超时控制，使用setTimeout及Promise.reject的实现的超时控制并不能阻止请求过程继续在后台运行，造成了量的浪费
- fetch没有办法原生监测请求的进度，而XHR可

