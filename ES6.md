##### ES6 声明方式

~~~javascript
for(let i=0;i<10;i++){
	console.log('循环体中:'+i);
}
console.log('循环体外:'+i);//报错
~~~



##### ES6 解构赋值

**（1）数组的解构赋值**

~~~javascript
let [a,b,c]=[1,2,3];
let [a,[b,c],d]=[1,[2,3],4];

let [flag=true]=[];
console.log(foo);//true

let [a,b='js']=['a-value '];
console.log(a+b);//a-value js

let [a,b='js']=['a-value ',undefined];
console.log(a+b);//a-value js

let [a,b='js']=['a-value ',null];
console.log(a+b);//a-value null
~~~

**（2）对象的解构赋值**

~~~javascript
let {foo,bar}={foo:'js',bar:'wang'};
console.log(foo+bar);//jswang

let foo;
{foo}={foo:'js'};//错误语法

let foo;
({foo}={foo:'js'});//正确语法
~~~

**（3）字符串的解构赋值**

~~~javascript
const [a,b,c,d]='wang';
console.log(a);
console.log(b);
console.log(c);
console.log(d);
~~~



##### ES6 运算符

**（1）扩展运算符(...三个点表示)**

~~~javascript
//当编写一个方法时，我们允许它传入的参数是不确定的。这时候可以使用对象扩展运算符来作参数
function wang(...arg){
    console.log(arg[0]);
    console.log(arg[1]);
    console.log(arg[2]);
    console.log(arg[3]);
}
wang(1,2,3);//1,2,3，undefined

//扩展运算符的用处
let arr1=['www','wang','com'];
let arr2=arr1;
arr2.push('cn');
console.log(arr1);//['www','wang','com','cn']--引用赋值

let arr1=['www','wang','com'];
let arr2=[...arr1];
arr2.push('cn');
console.log(arr1);//['www','wang','com']
~~~

**（2）rest运算符**

~~~javascript
function wang(first,...arg){
    console.log(arg.length);//打印3
    for(let val of arg){
        console.log(val);//1,2,3
    }
}
wang(0,1,2,3);

~~~



##### ES6 字符串模版

~~~javascript

let name='wang';
let blog1='hello'+name+'sir';//ES5
let blog2='hello${name}sir';//ES6
let blog3='<b>hello</b>${name}sir<br/>';//支持html标签
let a=1;
let b=2;
let result=`${a+b}`;//支持运算

let name='wang';
let blog='hellowangsir';
document.write(blog.indexOf(name));//ES5 返回5
document.write(blog.includes(name));//ES6 
blog.startsWith(name);//判断开头是否存在
blog.endsWith(name);//判断结尾是否存在
document.write('wang|'.repeat(3));//复制字符串
~~~



##### ES6 数字操作

~~~javascript
//二进制数字声明：0B/0b开头
let binary=0B010101;
console.log(binary);//21

//八进制数字声明：0o/0O开头
let octal=0o666;
console.log(octal);//438

//数字验证：Number.isFinite(xx)只要是数字，不论是浮点型还是整形都会返回true，其他时候会返回false。
let a=11/4;
console.log(Number.isFinite(a));//true
console.log(Number.isFinite('wang'));//false
console.log(Number.isFinite(NaN));//false
console.log(Number.isFinite(undefined));//false

//NaN验证
console.log(Number.isNaN(NaN));//true

//判断是否为整数Number.isInteger(xx)
console.log(Number.isInteger(123.1));//false

//整数转换Number.parseInt(xxx)、浮点型转换Number.parseFloat(xxx)
let a='9.18';
console.log(Number.parseInt(a)); 
console.log(Number.parseFloat(a));

//整数的操作是有一个取值范围的，它的取值范围就是2的53次方
let a = Math.pow(2,53)-1;
console.log(a); //9007199254740991
//最大安全整数
console.log(Number.Max_SAFE_INTEGER);
//最小安全数
console.log(Number.Min_SAFE_INTEGER);
//安全整数判断
let a=Math.pow(2,53)-1;
console.log(Number.isSafeInteger(a));//false
~~~



##### ES6 新增数组知识

~~~javascript
// Array.form()静态方法
let json={
	'0':'wang',
    '1':'ying',
    '2':'chang',
    length:3
};
let arr=Array.form(json);//特殊格式的json==>数组
console.log(arr);

// Array.of()静态方法
let arr=Array.of(3,4,5,6);
console.log(arr);
let arr=Array.of('wang','ying','chang');
console.log(arr);

// find()实例方法: 所谓的实例方法就是并不是以Array对象开始的，而是必须有一个已经存在的数组。value：表示当前查找的值;index：表示当前查找的数组索引;arr：表示当前数组。
let arr=[1,2,3,4,5,6,7];
console.log(arr.find(function(value,index,arr){
     return value > 5;//返回6
}))；

// fill()实例方法: 它的作用是把数组进行填充，它接收三个参数，第一个参数是填充的变量，第二个是开始填充的位置，第三个是填充到的位置。
let arr=[0,1,2,3,4];
arr.fill('wang',2,5);
console.log(arr);//第二位到第五位用wang进行填充

// entries()实例方法: entries()实例方式生成的是Iterator形式的数组，那这种形式的好处就是可以让我们在需要时用next()手动跳转到下一个值
let arr=['wang','ying','chang'];
let list=arr.entries();
console.log(list.next().value);
console.log(list.next().value);
console.log(list.next().value);

//join()实例方法: 数组=》字符串
let arr=['wang','ying','chang'];
console.log(arr.join('|'));
//toString()实例方法: 数组=》字符串
let arr=['wang','ying','chang'];
console.log(arr.toString());

// in的用法
//对象判断
let obj={
    a:'wang',
    b:'ying'
}
console.log('a' in obj);//true
//数组判断
//ES5
let arr=[,,,,];
console.log(arr.length);//虽然打印5，但是arr里面并没有值
//ES6
let arr=[,,,,];
console.log(0 in arr);//fasle

// 数组的遍历方法
//for...of
let arr=['wang','ying','chang'];
for(let item of arr){
    console.log(item);//数组值
}
for(let index of arr){
    console.log(index);//数组索引
}
for(let[index,val] of arr.entries()){
    console.log(index+':'+val);//同时输出值和索引
}

//forEach()实例方法: 会自动省略为空的数组元素，相当于直接给我们筛空了。但是有时候也会给我们帮倒忙。
let arr=['wang','ying','chang'];
arr.forEach(val,index)=>console.log(index,val);

//filter()实例方法
let arr=['wang','ying','chang'];
arr.filter(x=>console.log(x));

//some()实例方法
let arr=['wang','ying','chang'];
arr.some(x=>console.lg(x));

//map()实例方法
let arr=['wang','ying','chang'];
console.log(arr.map(x=>'web'));


~~~



##### ES6 箭头函数

~~~javascript
//ES5
function add(a,b){
    return a+b;
}
console.log(add(1,2));
//ES6 默认值
function add(a,b=2){
    return a+b;
}
console.log(add(1));
//ES6 抛出错误
function add(a,b=2){
    if(a==0){
		throw new Error('this is error');
    }
    return a+b;
}
console.log(add(0));
//ES6 严谨模式可以写在函数体中
function add(a,b){// 有坑:使用严谨模式不能使用默认值
    'use strict'
    return a+b;
}
console.log(add(1,2))
//获取需要传递的参数个数
function add(a,b){
    return a+b;
}
console.log(add.length);// 2,若b加上默认值则打印1
//对象的函数解构
let json={
    a:'wang',
    b:'ying'
}
function fun({a,b='wang'}){
    console.log(a,b);
}
fun(json);
//数组的函数解构
let arr=['wang','ying','chang'];
function fun(a,b,c){
    console.log(a,b,c);
}
fun(...arr);

//箭头函数
//箭头函数中不可加new，也就是说箭头函数不能当构造函数进行使用。
var add=(a,b=2)=>｛
	return a+b;
｝
console.log(add(1));
~~~



##### ES6 对象

~~~javascript
//对象赋值:ES6允许把声明的变量直接赋值给对象
let name='wang';
let skill='java';
var obj={name,skill};
console.log(obj);//{name: "wang", skill: "java"}

//对象Key值构建
let key='skill';
var obj={
    [key]:web
}
console.log(obj.skill);

//自定义对象方法
var obj={
    add:function(a,b){
        reurn a+b;
    }
}
console.log(obj.add(1,2));//3

//Object.is()静态方法: 对象比较
var obj1={name:'wang'};
var obj2={name:'wang'};
console.log(obj1.name==obj2.name);//true ES5
console.log(Object.is(obj1.name,obj2.name));//true ES6

//===和Object.is()静态方法的区别： ===为同值相等，is()为严格相等。
console.log(+0 === -0);  //true
console.log(NaN === NaN ); //false
console.log(Object.is(+0,-0)); //false
console.log(Object.is(NaN,NaN)); //true

//Object.assign()合并对象
var a={a:'wang'};
var b={b:'ying'};
var c={c:'chang'};
let d=Object.assign(a,b,c);
console.log(d);
~~~



##### ES6 Promise

~~~javascript
new Promise(function (resolve, reject) {
    var time = Math.random();
    console.log(time)
    if (time < 0.5) {
        resolve('resolve')
    } else {
        reject('reject');
    }
}).then(function (result) {
    console.log('success:' + result);
}).catch(function (reason) {
    console.log('failed:' + reason);
})
~~~



##### ES6 模块化

export.js

~~~javascript
//export可以让我们把变量，函数，对象进行模块话，提供外部调用接口，让外部进行引用

//输出单个变量
export var a='wang';

//输出多个变量
var x='wang';
var y='ying';
var z='chang';
export {x,y,z}
export { //as的用法 有些时候我们并不想暴露模块里边的变量名称，而给模块起一个更语义话的名称
	x1 as x,
    y1 as y,
    z1 as z
}

//输出函数
export function add(a,b){
    return a+b;
}
~~~

import.js

~~~javascript
import {a} from './export.js';
console.log(a);//wang
~~~



