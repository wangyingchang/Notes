#### AJAX 是什么?

AJAX = Asynchronous JavaScript and XML（异步的 JavaScript 和 XML）也就是无刷新数据读取;

AJAX 使网页实现异步更新,可以在不重新加载整个网页的情况下，对网页的某部分进行更新;

传统的网页（不使用 AJAX）如果需要更新内容，必需重载整个网页面;

AJAX 不是新的编程语言，而是一种使用现有标准的新方法;

AJAX 是一种用于创建快速动态网页的技术;

AJAX 与后台服务器进行少量数据交换;



#### AJAX 工作原理？

![AJAX](http://www.runoob.com/images/ajax.gif)





#### AJAX 基于现有的标准？

AJAX是基于现有的Internet标准，并且联合使用它们：

XMLHttpRequest 对象 (异步的与服务器交换数据)

JavaScript/DOM (信息显示/交互)

CSS (给数据定义样式)

XML (作为转换数据的格式)



#### XHR 创建对象？

XMLHttpRequest对象 是 AJAX 的基础；

在创建对象时，有兼容问题：

~~~html
<script>
var xmlhttp;
if(window.XMLHttpRequest){
    //  IE7+, Firefox, Chrome, Opera, Safari 浏览器执行代码
    xmlhttp=new XMLHttpRequest();
}else{
    xmlhttp=new ActiveXObject("Microsoft.XMLHTTP");
}
</script>
~~~



#### XHR 请求？

XMLHttpRequest 对象用于和服务器交换数据。

~~~html
<script>
xmlhttp.open(method,url,async);
xmlhttp.send();
</script>
~~~

| 方法                             | 描述                                                         |
| -------------------------------- | ------------------------------------------------------------ |
| open(*method*,*url*,*async*)     | ***method***：请求的类型；GET 或 POST    ***url***：文件在服务器上的位置   ***async***：true（异步）或 false（同步） |
| send(*string*)                   | 将请求发送到服务器。*string*：仅用于 POST 请求               |
| setRequestHeader(*header,value*) | 向请求添加 HTTP 头。header：规定的头名  value：规定的值      |

GET与POST的区别？



#### XHR 响应？

如需获得来自服务器的响应，请使用 XMLHttpRequest 对象的 responseText 或 responseXML 属性。

| 属性         | 描述                       |
| ------------ | -------------------------- |
| responseText | 获得字符串形式的响应数据。 |
| responseXML  | 获得 XML 形式的响应数据。  |



#### XHR readyState？

onreadystatechange事件

当请求被发送到服务器时，我们需要执行一些基于响应的任务。

每当 readyState 改变时，就会触发 onreadystatechange 事件。

readyState 属性存有 XMLHttpRequest 的状态信息。

下面是 XMLHttpRequest 对象的三个重要的属性：

| 属性               | 描述                                                         |
| ------------------ | ------------------------------------------------------------ |
| onreadystatechange | 存储函数（或函数名），每当 readyState 属性改变时，就会调用该函数。 |
| readyState         | 存有 XMLHttpRequest 的状态。从 0 到 4 发生变化。0: 请求未初始化1: 服务器连接已建立2: 请求已接收3: 请求处理中4: 请求已完成，且响应已就绪 |
| status             | 200: "OK"        404: 未找到页面                             |

在 onreadystatechange 事件中，我们规定当服务器响应已做好被处理的准备时所执行的任务；

当 readyState 等于 4 且状态为 200 时，表示响应已就绪；

**注意：** onreadystatechange 事件被触发 4 次（0 - 4）, 分别是： 0-1、1-2、2-3、3-4，对应着 readyState 的每个变化；

#### HTTP 请求?

一个HTTP请求一般由4部分组成：

- HTTP请求的动作或方法，比如是GET还是POST;
- HTTP请求的URL,得知道请求的地址是什么吧;
- 请求头，包含一些客户端的环境信息，身份验证信息等;
- 请求体，也就是请求正文，请求正文可以包含客户提交的查询字符串信息，表单信息等等；

#### HTTP响应?

一个HTTP响应一般包含3部分：

- 一个数组个文字组成的状态码，用来显示请求成功还是失败;
- 响应头，响应由也和请求头一样包含许多用户的信息，比如服务器的类型，日期时间，内容类型 和长度;
- 响应体，也就是响应正文;



#### AJAX 请求步骤?*******

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

- **1.创建 AJAX 对象 XMLHttpRequest (XHR)**

  ```javascript
  var ajax = null;
  if(window.XMLHttpRequest){
      ajax = new XMLHttpRequest(); //for ie7+,FireFox,Chorme,Opera,Safai...
  }else{
      ajax = new ActiveXObject('Microsoft.XMLHTTP'); //for ie6
  }
  ```

- **2.打开服务器连接**

  ~~~
  ajax.open('GET', url, true);
  ~~~

  在这里会用到 open(method,url,async) 方法,启动一个请求以备发送;

  * 第一个参数method 是连接方法即 GET 和 POST，
  * 第二个参数是 url  即所要读取数据的地址，
  * 第三个参数是否异步 async，它是个布尔值，true 为异步(默认值)，false 为同步。


注意：在**open()之后、send()之前**可以修改HTTP请求头信息，建议不要改变浏览器默认设置的信息，可以增加
 自定义的数据

```javascript
  ajax.setRequestHeader('myId','001');
  //查看responseHeader
  ajax.getResponseHeader('content-type');
  ajax.getAllResponseHeaders();
```

- **3.发送请求到服务器**

```
  ajax.send(null);//如果不需要传送数据，则必须放置null,因为部分浏览器要求必须要加null;
```

如果您希望通过 GET 方法发送信息，请向 URL 添加信息
但是url加的查询字符串必须使用 encodeURL()进行编码才能加入

```javascript
function addURLParam(url,name,value) {
    url+=(url.indexOf("?")==-1)?"?":"&";
    url+=encodeURI(name)+"="+encodeURI(value);
    return url;
}
```

   * application/x-www-form-urlencoded（大多数请求可用：eg：'name=Denzel&age=18'）
   * multipart/form-data（文件上传）
   * application/json（json格式对象，eg：{'name':'Denzel','age':'18'}）
     将请求发送到服务器(后台记得用request.json())。
   * string：仅用于 POST 请求

   ```
   ajax.send('fname=Bill&lname=Gates);
   ```

   如果需要像 HTML 表单那样 POST 数据，请使用 setRequestHeader() 来添加 HTTP 头。
   然后在 send() 方法中规定您希望发送的数据(表单数据封装格式和GET提交数据格式相同)：

   ```
   ajax.send($('#myform').serialize());
   ```

   ```javascript
   xmlhttp.open("POST","ajax_test.asp",true);
   //发送的是表单,一定要写在open，send之间，否则会出现异常
   xmlhttp.setRequestHeader("Content-type","application/x-www-form-urlencoded");
   xmlhttp.send("fname=Bill&lname=Gates");
   ```


send()请求是同步的，意味着后续的js代码必须等到服务器响应之后才继续执行。所以在收到响应后，
 响应的数据会自动填充到XHR对象的属性。



- **4.接收返回值**

XHR对象接收的属性有：
* responseText ：获得字符串形式的响应的数据

* responseXML 如果响应的内容类型是"text/xml"或"application/xml"，则该属性值为XML DOM文档。

* status 、statusText ： 以数字和文本形式返回HTTP状态码

* getAllResponseHeader():获取所有的响应报头

* getResponseHeader():查询响应中的某个字段的值

   **onreadystatechange 事件**。当请求被发送到服务器时，我们需要执行一些基于响应的任务。
   每当 readyState 改变时，就会触发 onreadystatechange 事件。

   readyState：请求状态，返回的是整数（0-4）。

  	0（请求未初始化）：还没有调用 open() 方法。

   	1（服务器连接建立）：已调用open(), send() 方法，正在发送请求。

   	2（请求已接受）：send() 方法完成，已收到全部响应内容。

   	3（请求处理中）：正在解析响应内容，也就是接受响应主接收到

   	4（请求完成）：响应内容解析完成，可以在客户端调用。

   status：请求结果，返回 200 或者 404。

   	200 => 成功。

   	304 => 请求的资源并没有被修改，可以直接使用浏览器中缓存的版本。

   	404 => 失败。

   responseText：返回内容，即我们所需要读取的数据。需要注意的是：responseText 返回的是字符串。




#### XMLHttpRequest 2

1. formdata

    ```
    var form=$('#myform')[0];
    var formdata=new FormData(form);
    formdata.append('from','lzhan.com');
    formdata.set('from','163.com');
    
    console.log(formdata.get('from'));
    console.log(formdata.get('id'));
    formdata.forEach(function (value,key) {
        console.log(value);
    })
    ```
2. 超时设定

    ```
    oAjax.timeout=3000;
        oAjax.ontimeout=function () {
    
    };
    ```

3. 下载进度事件

    ```
    var pro=document.querySelector('#loadProgress');
                    oAjax.onprogress=function (e) {
                        pro.setAttribute('max',parseInt(e.totalSize));
    
                        if(e.lengthComputable){
                            pro.setAttribute('value',e.position);
    
                        }
                    }
    ```
    >progess事件会在接受数据期间周期性触发。

4. 跨域

     http://www.163.com
      http://www.163.com:80
      端口不同
      http://www.163.com:8080
      协议不同
      https://www.163.com:80
      模块不同
      http://news.163.com:80
      网址不同
      http://www.qq.com:80

     	flask_cors : https://flask-cors.readthedocs.io/en/latest/

5. 关于token

  XMLHttpRequest对象可以利用header提交token

  	ajax.setRequestHeader('token',token);
  	
  	服务器端可以通过下面方式接受token
  	
  	request.headers['token']
  		
  	**但是、服务器端通过response.headers['token']=token发送给客户端时，XMLHttpRequest对象却无法通过oAjax.getResponseHeader('token')来获取**
  	所以我们可以通过把token作为数据的一部分来发送给客户端：
  	return json.jsonify({"statuscode": "201","token":token.decode()})

