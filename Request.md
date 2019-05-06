##### 1.原生ajax

~~~javascript
var xhr = null;
if (window.XMLHttpRequest) {
  xhr = new XMLHttpRequest(); //for ie7+,FireFox,Chorme,Opera,Safai...
}else {
  xhr = new ActiveXObject('Microsoft.XMLHTTP'); //for ie6
}
xhr.open("GET","/customer/getinfo",true);
xhr.send(null);
xhr.onreadystatechange=function(){
    if(xhr.readyState==4){
        if(xhr.status==200){
            console.log(xhr.responseText);
        }else{
            console.log('请求失败！')
        }
    }
};
~~~



##### 2.jQuery ajax

~~~
$.ajax({
   type: 'get',
   url: url,
   data: data,
   dataType: "json",
   contentType: "application/json;charset=utf-8",
   success: function (data) {
   	   console.log("success:")
       console.log(data)
   },
   error: function (XMLHttpRequest, textStatus, errorThrown) {
   		console.log("error:", url);
        console.log('error:' + errorThrown);
   }
});
~~~

优缺点：

- 本身是针对MVC的编程,不符合现在前端MVVM的浪潮
- 基于原生的XHR开发，XHR本身的架构不清晰，已经有了fetch的替代方案
- JQuery整个项目太大，单纯使用ajax却要引入整个JQuery非常的不合理（采取个性化打包的方案又不能享受CDN服务）



##### 3.axios

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



##### 4.fetch

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

