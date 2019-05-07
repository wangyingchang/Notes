##### 1.原生ajax

~~~javascript
var xhr = null;
var params = {
    uname: '123',
    password: '123'
}
// 1.获取xhr对象:
if (window.XMLHttpRequest) {
  // for ie7+,FireFox,Chorme,Opera,Safai...
  xhr = new XMLHttpRequest(); 
}else {
  // for <ie7:由于IE5是第一款引入XHR对象的浏览器，所以在IE7之前其实都不是叫XMLHttpRequest.
  xhr = new ActiveXObject('Microsoft.XMLHTTP'); 
}
// 2.初始化请求:这个方法不会发送请求，但会初始化一个请求准备发送;第三个参数默认是true，也就是异步的
xhr.open("post","/customer/getinfo",true);
// 3.设置请求头:POST请求需要,要模拟表单提交请求的话就将Content-type头部信息设置为application/x-www-form-urlencoded，并且发送的是一个经过序列化之后的字符串
xhr.setRequestHeader("Content-type", "application/x-www-form-urlencoded");
// 4.发送参数:JSON.stringify()是将javascript对象序列化为字符串
xhr.send(JSON.stringify(params)); 
// 5. 监控请求状态，
xhr.onreadystatechange=function(){
    if(xhr.readyState==4){
        if(xhr.status==200){
            // 6.处理请求数据
            console.log(JSON.parse(xhr.responseText));
        }else{
            console.log('请求失败！')
        }
    }
};
~~~

readyState属性可能的取值如下:
- 0：未初始化，尚未调用open()方法
- 1：启动。已经调用open()方法，但尚未调用send()方法
- 2：发送：已经调用send()方法，但尚未收到响应
- 3：接收。已经接收到部分响应数据。
- 4：完成。已经接收到全部响应数据，而且已经可以在客户端使用了。

响应的数据会自动填充XHR对象的属性，包含以下属性:
- responseText：作为响应主题被放回的文本
- responseXML：如果响应的内容类型是"text/xml"或"application/xml",这个属性中将保存包含着响应数据的XMLDOM文档
- status：响应的HTTP状态
- statusText：HTTP状态的说明


##### 2.jQuery ajax

~~~javascript
$.ajax({
   type: 'get',
   url: url,
   data: JSON.stringify(data),
   dataType: "json",
   contentType: "application/json;charset=utf-8",
   async: true, // true:异步,false:同步
   xhrFields: {
      withCredentials: true // 前端设置是否带cookie
   },
   success: function (data) {
   	   console.log("success:")
       console.log(data)
   },
   error: function (XMLHttpRequest, textStatus, errorThrown) {
        if (callErrorBack instanceof Function) {
            callErrorBack();
        }
   		console.log("error:", url);
        console.log('error:' + errorThrown);
   }
});
~~~

优缺点：

- 本身是针对MVC的编程,不符合现在前端MVVM的浪潮
- 基于原生的XHR开发，XHR本身的架构不清晰，已经有了fetch的替代方案
- JQuery整个项目太大，单纯使用$.ajax却要引入整个JQuery非常的不合理（采取个性化打包的方案又不能享受CDN服务）



##### 3.axios

~~~javascript
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



##### 4.fetch

~~~javascript
try {
  let response = await fetch(url);
  let data = response.json();
  console.log(data);
} catch(e) {
  console.log("Oops, error", e);
}
~~~

优缺点：

- 符合关注分离，没有将输入、输出和用事件来跟踪的状态混杂在一个对象里
- 更好更方便的写法
- 更加底层，提供的API丰富（request, response）
- 脱离了XHR，是ES规范里新的实现方式

- fetcht只对网络请求报错，对400，500都当做成功的请求，需要封装去处理
- fetch默认不会带cookie，需要添加配置项
- fetch不支持abort，不支持超时控制，使用setTimeout及Promise.reject的实现的超时控制并不能阻止请求过程继续在后台运行，造成了量的浪费

- fetch没有办法原生监测请求的进度，而XHR可以



##### 为什么要用axios?

axios 是一个基于Promise 用于浏览器和 nodejs 的 HTTP 客户端，它本身具有以下特征：

- 从浏览器中创建 XMLHttpRequest
- 从 node.js 发出 http 请求
- 支持 Promise API
- 拦截请求和响应
- 转换请求和响应数据
- 取消请求
- 自动转换JSON数据

- 客户端支持防止CSRF/XSRF

