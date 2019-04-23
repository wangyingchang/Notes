#### JSON 是什么？

JSON 指的是 JavaScript 对象表示法（**J**ava**S**cript **O**bject **N**otation）；

JSON 是轻量级的文本数据交换格式；

JSON 具有自我描述性，更易理解

JSON 独立于语言：JSON 使用 Javascript语法来描述数据对象，但是 JSON 仍然独立于语言和平台；

JSON 解析器和 JSON 库支持许多不同的编程语言， 目前非常多的动态（PHP，JSP，.NET）编程语言都支持JSON；

JSON是一种数据格式，它并不从属于JavaScript，很多语言都有JSON的解析器和序列化器；



#### JSON 与XML相同之处?

JSON 是纯文本;

JSON 具有"自我描述性"（人类可读）;

JSON 具有层级结构（值中存在值）;

JSON 可通过 JavaScript 进行解析;

JSON 数据可使用 AJAX 进行传输;

#### JSON 与XML不同之处？

没有结束标签；

更短；

读写速度更快；

能够使用内建的JavaScript eval()方法解析；

使用数组；

不使用保留字；

#### JSON 为什么使用?

对于 AJAX 应用程序来说，JSON 比 XML 更快更易使用：

**使用 XML**

- 读取 XML 文档
- 使用 XML DOM 来循环遍历文档
- 读取值并存储在变量中

**使用 JSON**

- 读取 JSON 字符串
- 用 eval() 处理 JSON 字符串



#### JSON 语法



##### 1.JSON 语法规则

JSON 语法是 JavaScript 对象表示语法的子集：

- 数据在名称/值对中
- 数据由逗号分隔
- 大括号保存对象
- 中括号保存数组

##### 2.JSON 名字/值对

JSON数据的书写格式是：名称/值对。

~~~json
//名称/值对包括字段名称（在双引号中），后面写一个冒号，然后是值：
"name" : "菜鸟教程"
//=>JavaScript
name = "菜鸟教程"
~~~

##### 3.JSON 值

- 数字（整数或浮点数）

~~~json
{"age":30}
~~~

- 字符串（在双引号中）

~~~json
{"name":"汪应昌"}
~~~

- 逻辑值（true 或 false）

~~~json
{"flag":true}
~~~

- 数组（在中括号中）

~~~json
{
    "sites":[
        { "name":"百度","url":"www.baidu.com"}
        { "name":"google","url":"www.google.com"}
        { "name":"git","url":"www.github.com"}
    ]
}
~~~

- 对象（在大括号中）

~~~json
{"name":"章若楠","age":19,"gender":"女"}
//=>JavaScript
var oject={
    name="章若楠"，
    age=19,
    gengder="女"
}
~~~

- null

~~~json
{"name":null}
~~~

##### 4.JSON 能使JavaScript语法

因为 JSON 使用 JavaScript 语法，所以无需额外的软件就能处理 JavaScript 中的 JSON。

通过 JavaScript，您可以创建一个对象数组，并像这样进行赋值：

~~~json
var sites = [
    { "name":"runoob" , "url":"www.runoob.com" }, 
    { "name":"google" , "url":"www.google.com" }, 
    { "name":"微博" , "url":"www.weibo.com" }
];
~~~

可以像这样访问 JavaScript 对象数组中的第一项（索引从 0 开始）：

~~~
sites[0].name;
返回的内容是：
runoob
可以像这样修改数据：
sites[0].name="菜鸟教程";
~~~

##### 5.JSON 文件

- JSON 文件的文件类型是 ".json"

- JSON 文本的 MIME 类型是 "application/json"


#### JSON 对象

**1.格式**

~~~javascript
var myJson={ "name":"runoob", "alexa":10000, "site":null };
~~~

JSON 对象使用在大括号({})中书写。

对象可以包含多个 **key/value（键/值）**对

key 必须是字符串，value 可以是合法的 JSON 数据类型（字符串, 数字, 对象, 数组, 布尔值或 null）。

key 和 value 中使用冒号(:)分割。

每个 key/value 对使用逗号(,)分割。

**2.访问对象值**

你可以使用点号（.）来访问对象的值：

~~~javascript
var x=myJson.name;
~~~

你也可以使用中括号（[]）来访问对象的值：

~~~javascript
var y=myJson["name"];
~~~

**3.循环对象**

~~~javascript
var txt="";
for(x in myJson){
    txt+=myJson[x];
}
~~~

**4.嵌套 JSON 对象**

~~~javascript
var myJson = {
    "name":"runoob",
    "alexa":10000,
    "sites": {
        "site1":"www.runoob.com",
        "site2":"m.runoob.com",
        "site3":"c.runoob.com"
    }
}
//你可以使用点号(.)或者中括号([])来访问嵌套的 JSON 对象。
var x=myJson.sites.site1;
var y=myJson.sites["site1"];
//你可以使用点号(.)或者中括号（[]）来修改 JSON 对象的值：
myJson.sites.site1="www.google.com";
myJson.sites["site1"]="www.google.com";
~~~

**5.删除对象属性**

~~~javascript
delete myJson.sites["site1"]
~~~



#### JSON 数组

**1.格式**

~~~
[ "Google", "Runoob", "Taobao" ]
~~~

JSON 数组在中括号中书写。

JSON 中数组值必须是合法的 JSON 数据类型（字符串, 数字, 对象, 数组, 布尔值或 null）。

JavaScript 中，数组值可以是以上的 JSON 数据类型，也可以是 JavaScript 的表达式，包括函数，日期，及 *undefined*。

**2.JSON对象中的数组**

~~~javascript
var myJson={ "name":"网站", "num":3, "sites":[ "Google", "Runoob", "Taobao" ] }
//我们可以使用索引值来访问数组：
var x=myJson.sites[0];
~~~

**3.嵌套JSON对象中的数组**

~~~javascript
var myJson = {
    "name":"网站",
    "num":3,
    "sites": [
        { "name":"Google", "info":[ "Android", "Google 搜索", "Google 翻译" ] },
        { "name":"Runoob", "info":[ "菜鸟教程", "菜鸟工具", "菜鸟微信" ] },
        { "name":"Taobao", "info":[ "淘宝", "网购" ] }
    ]
}
~~~

**4.删除数组元素**

~~~javascript
delete myJson.sites[1];
~~~







#### JSON.parse()

**1.语法**

JSON 通常用于与服务端交换数据,在接收服务器数据时一般是字符串,我们可以使用 JSON.parse() 方法将数据转换为 JavaScript 对象;

~~~javascript
JSON.parse(text[,reviver])

//参数说明
text:必需， 一个有效的 JSON 字符串；
reviver: 可选，一个转换结果的函数， 将为对象的每个成员调用此函数；
~~~

**2.实例**

~~~javascript
//例如我们从服务器接收了以下数据：
{ "name":"runoob", "alexa":10000, "site":"www.runoob.com" }
//我们使用 JSON.parse() 方法处理以上数据，将其转换为 JavaScript 对象：
var obj = JSON.parse('{ "name":"runoob", "alexa":10000, "site":"www.runoob.com" }');
var x=obj.name+obj.site;
~~~

**3.日期对象**

JSON 不能存储 Date 对象。

如果你需要存储 Date 对象，需要将其转换为字符串。

之后再将字符串转换为 Date 对象。

~~~html
<h2>将字符串转换为 Date 对象。</h2>
<p id="demo"></p>
<script>
var text = '{ "name":"Runoob", "initDate":"2013-12-14", "site":"www.runoob.com"}';
var obj = JSON.parse(text);
obj.initDate = new Date(obj.initDate);
document.getElementById("demo").innerHTML = obj.name + "创建日期: " + obj.initDate;
</script>

<!--我们可以启用 JSON.parse 的第二个参数 reviver，一个转换结果的函数，对象的每个成员调用此函数 -->
<h2>字符串转换为 Date 对象</h2>
<p id="demo"></p>
<script>
var text = '{ "name":"Runoob", "initDate":"2013-12-14", "site":"www.runoob.com"}';
var obj = JSON.parse(text, function (key, value) {
	if (key == "initDate") {
	    return new Date(value);
	} else {
	    return value;
}});
document.getElementById("demo").innerHTML = obj.name + "创建日期：" + obj.initDate;
</script>
~~~

**3.解析函数（不建议在JSON中使用函数）**

~~~html
<h2>字符串转换为函数</h2>
<p id="demo"></p>
<script>
var text = '{ "name":"Runoob", "alexa":"function () {return 10000;}", "site":"www.runoob.com"}';
var obj = JSON.parse(text);
obj.alexa = eval("(" + obj.alexa + ")");
document.getElementById("demo").innerHTML = obj.name + " Alexa 排名：" + obj.alexa(); 
</script>
~~~



#### JSON.stringify()

JSON 通常用于与服务端交换数据。

在向服务器发送数据时一般是字符串。

我们可以使用 JSON.stringify() 方法将 JavaScript 对象转换为字符串。

**1.语法**

~~~javascript
JSON.stringify(value[, replacer[, space]])

//参数说明
value:
必需， 一个有效的 JSON 对象。
replacer:
可选。用于转换结果的函数或数组。
如果 replacer 为函数，则 JSON.stringify 将调用该函数，并传入每个成员的键和值。使用返回值而不是原始值。如果此函数返回 undefined，则排除成员。根对象的键是一个空字符串：""。
如果 replacer 是一个数组，则仅转换该数组中具有键值的成员。成员的转换顺序与键在数组中的顺序一样。当 value 参数也为数组时，将忽略 replacer 数组。
space:
可选，文本添加缩进、空格和换行符，如果 space 是一个数字，则返回值文本在每个级别缩进指定数目的空格，如果 space 大于 10，则文本缩进 10 个空格。space 有可以使用非数字，如：\t。
~~~

**2.JavaScript对象转换**

~~~javascript
var obj = { "name":"runoob", "alexa":10000, "site":"www.runoob.com"};
var myJson = JSON.stringify(obj);
document.getElementById("demo").innerHTML = myJSON;
~~~

**3.JavaScript 数组转换**

~~~javascript
var arr = [ "Google", "Runoob", "Taobao", "Facebook" ];
var myJson = JSON.stringify(arr);
document.getElementById("demo").innerHTML = myJson;
~~~

**4.日期对象**

JSON 不能存储 Date 对象。

JSON.stringify() 会将所有日期转换为字符串。

~~~javascript
var obj = { "name":"Runoob", "initDate":new Date(), "site":"www.runoob.com"};
var myJSON = JSON.stringify(obj);
document.getElementById("demo").innerHTML = myJSON;
//结果：{"name":"Runoob","initDate":"2018-09-18T13:16:43.393Z","site":"www.runoob.com"}
~~~

**5.解析函数**

~~~javascript
var obj = { "name":"Runoob", "alexa":function () {return 10000;}, "site":"www.runoob.com"};
var myJSON = JSON.stringify(obj);
document.getElementById("demo").innerHTML = myJSON;
//{"name":"Runoob","site":"www.runoob.com"}
~~~



#### ---解析与序列化

- stringfy()：把JavaScript对象序列化为JSON字符串
- parse()：把JSON字符串解析为原生JavaScript值


```json
var book = {
    "title":"Java从入门到放弃",
    "authors":[
        "张三"
    ],
    edition: 2
};
var jsonText = JSON.stringify(book);
alert(jsonText);// {"title":"Java从入门到放弃","authors":["张三"],"edition":2}

// 上面的例子将一个JavaScript对象序列化为一个JSON字符串。默认情况下，JSON.stringify()不包含任何字符或缩进；
```

```json
//将JSON字符串直接通过JSON.parse()可以得到相应的JavaScript值。
var newBook = JSON.parse(jsonText); 
```

book与newBook具有相同的属性，但是彼此是相互独立的。



**序列化选项**
JSON.stringify()还可以接收两个参数：

第一个参数：过滤器，一个数组或一个函数；

如果参数是数组，JSON.stringify()的结果只包含数组中列出的属性

第二个参数：一个选项，表示是否在JSON字符串中保留缩进

```json
var book = {
    "title":"Java从入门到放弃",
    "authors":[
        "张三"
    ],
    edition: 2
};
var jsonText = JSON.stringify(book, ["title", "authors"]);
console.log(jsonText);  // {"title":"Java从入门到放弃","authors":["张三"]}
```



如果参数是函数，传入的函数接收两个参数，属性名和属性值，根据属性名可以知道如何处理属性。属性名是字符串，属性值并非键值对的值，键名可以是空字符串。

返回的值是相应键的值，如果函数返回undefined，那么该属性就会被忽略。

```json
var book = {
    "title":"Java programming",
    "authors":[
        "张三",
        "李四"
    ],
    edition: 2
};
var jsonText = JSON.stringify(book, function (key, value) {
    switch (key) {
        case "authors":
            return value.join("-");        // 用“-”分割数组
        case "edition":
            return undefined;
        default :
            return value;
    }
});
console.log(jsonText);    // {"title":"Java programming","authors":"张三-李四"}
```

字符串缩进
JSON.stringify()的第三个参数用于控制结果中的缩进和空白符。如果是数值，表示每格缩进的空格数。

```javascript
var book = {
    "title":"Java programming",
    "authors":[
        "詹姆斯.高斯林",
    ],
    edition: 2
};
var jsonText = JSON.stringify(book, null, 4);
console.log(jsonText);
//如果是字符串，这个字符串将用作JSON字符串的缩进符

var book = {
    "title":"Java programming",
    "authors":[
        "詹姆斯.高斯林",
    ],
    edition: 2
};
var jsonText = JSON.stringify(book, null, "__");
console.log(jsonText);
```

【显示结果】：

```json
{
__"title": "Java programming",
__"authors": [
____"詹姆斯.高斯林"
__],
__"edition": 2
}
```


缩进字符串最多只能包含10个字符。

**toJSON()方法**
JSON.stringify()并不能满足所有对象进行序列化的需求。可以给对象定义toJSON()方法，返回其自身的JSON数据格式。

```json
示例：

var book = {
    "title":"Java programming",
    "authors":[
        "詹姆斯.高斯林",
    ],
    edition: 2,
    toJSON: function () {
        return "==="+this.title+"===";
    }
};
var jsonText = JSON.stringify(book);
console.log(jsonText);    // "===Java programming==="
```

解析选项
JSON.parse()方法也可以接收另一个参数，该参数是一个函数，将在每个键值对上调用。如果返回undefined，表示从结果中删除相应的键，如果返回其他值，则将该值插入到结果中。

```json
var book = {
    "title":"Java programming",
    "authors":[
        "詹姆斯.高斯林",
    ],
    edition: 2,
    year: 2017,
    releaseDate: new Date(2017, 11, 1)
};
var jsonText = JSON.stringify(book);

var newBook = JSON.parse(jsonText, function (key, value) {
    if (key == "releaseDate") {
        return new Date(value);
    } else {
        return value;
    }
});
console.log(newBook.releaseDate.getFullYear());    // 2017
```

