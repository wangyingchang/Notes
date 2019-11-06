#### 一、Vue2.0-内部指令

##### 1.HelloWorld

~~~html
<div id="app">{{message}}</div>
<script type="text/javascript">
    var app=new Vue({
        el:'#app',
        data:{
            message:'Hello Vue'
        }
    })
</script>
~~~

##### 2.v-if / v-show

v-if：是vue 的一个内部指令，指令用在我们的html中；用来判断是否加载html的DOM，比如我们模拟一个用户登录状态，在用户登录后现实用户名称。

~~~html
<div id="app">
    <div v-if="isLogin">您好！{{userName}}</div>
    <div v-else>请登录</div>
</div>
<script type="text/javascript">
    var app=new Vue({
        el:'#app',
        data:{
            isLogin:true,
            userName:'wang'
        }
    })
</script>
~~~

~~~html
<div v-show="isLogin">您好！{{userName}}</div>
~~~

**v-if 和v-show的区别?**

- v-if： 判断是否加载，可以减轻服务器的压力，在需要时加载。
- v-show：调整css dispaly属性，可以使客户端操作更加流畅。安全性低于v-if

##### 3.v-for

v-for：是循环渲染一组data中的数组，v-for 指令需要以 item in items 形式的特殊语法，items 是源数据数组并且item是数组元素迭代的别名。

~~~html
<div id="app">
    <ul>
    	<li v-for="item in items">{{item.name}}--{{item.age}}</li>
    </ul>
</div>
<script>
    var app=new Vue({
        el:'#app',
        data:{
            items:[
            	{name:'lisha',age:20},
            	{name:'wang',age:22},
                {name:'miss',age:21}
            ]
        }
    })
</script>
~~~



##### 4.v-text / v-html

我们已经会在html中输出data中的值了，我们已经用的是{{xxx}},这种情况是有弊端的，就是当我们网速很慢或者javascript出错时，会暴露我们的{{xxx}}。Vue给我们提供的v-text,就是解决这个问题的。

~~~html
<span v-text="message"></span><br/>
           ==》
<span>{{ message }}</span>
~~~

如果在javascript中写有html标签，用v-text是输出不出来的，这时候我们就需要用`v-html`标签了。

~~~html
<span v-html="msgHtml"></span>
~~~

双大括号会将数据解释为纯文本，而非HTML。为了输出真正的HTML，你就需要使用v-html 指令。 需要注意的是：在生产环境中动态渲染HTML是非常危险的，因为容易导致`XSS`攻击。所以只能在可信的内容上使用v-html，永远不要在用户提交和可操作的网页上使用.

~~~html
<div id="app">
    <span>{{span}}</span>=<span v-text="message"></span><br/>
    <span v-html="msgHtml"></span>
</div>
<script>
    var app=new Vue({
        el:'#app',
        message:'Hello Vue',
        msgHtml:'<h2>Hello Vue</h2>'
    })
</script>
~~~



##### 5.v-on

v-on 就是监听事件，可以用v-on指令监听DOM事件来触发一些javascript代码。

~~~html
<div id="app">
    本场比赛得分:{{count}}<br/>
    <button v-on:click="add">加分</button>
    <!-- @click==>v-on:click-->
    <button @click="sub">减分</button>
    <!-- 绑定按键Enter-->
    <input type="text" v-on:keyup.enter="onEnter" v-model="secondCount">
</div>
<script>
    var app=new Vue({
        el:'#app',
        data:{
            count:1,
            secondCount:1,
        },
        methods:{
            add:function(){
                this.count++;
            },
            sub:function(){
                this.count--;
            },
            onEnter:function(){
                //文本框的数字会默认转变成字符串，需要使用parseInt()函数
                this.count=this.count+parseInt(this.secondCount);
            }
        }
    })
</script>
~~~



##### 6.v-model

v-model指令，我理解为绑定数据源。就是把数据绑定在特定的**表单元素**上，可以很容易的实现双向数据绑定。

~~~html
<div id="app">
    <p>原始文本信息:{{message}}</p>
    <p>v-model:<input type="text" v-model="message"></p>
</div>
<script>
    var app=new Vue({
        el:'#app',
        data:{
            message:'Hello Vue'
        }
    })
</script>
~~~

**修饰符**

- **.lazy**：取代 imput 监听 change 事件。
- **.number**：输入字符串转为数字。
- **.trim**：输入去掉首尾空格。

**文本区域**

~~~HTML
<textarea cols="30" rows="10" v-model="message"></textarea>
~~~

**多选按钮绑定一个值**

~~~html
<input type="checkbox" id="isTure" v-model="isTure">
<label for="isTure">{{isTure}}</label>
~~~

**多选绑定一个数组**

~~~html
<p>
<input type="checkbox" id="wang" value="wang" v-model="names">
<label for="wang">wang</label><br/>
<input type="checkbox" id="ying" value="ying" v-model="names">
<label for="ying">ying</label><br/>
<input type="checkbox" id="chang" value="chang" v-model="names">
<label for="chang">ying</label><br/>
</p>
<p>{{names}}</p>
~~~

**单选按钮绑定数据**

~~~html
<input type="radio" id="one" value="男" v-model="sex">
<label for="one">男</label>
<input type="radio" id="two" value="女" v-model="sex">
<label for="two">女</label>
<p>{{sex}}</p>
~~~



##### 7.v-bind

v-bind是处理HTML中的**标签属性**的;

~~~html
<div id="app">
    <!-- 完整语法 -->
    <img v-bind:src="imgSrc" width="200px">
    <!-- 缩写 -->
    <img :src="imgSrc" width="200px">
</div>
<script>
    var app=new Vue({
        el:'#app',
        data:{
            imgSrc:'http://baidu.com/wp-content/uploads/2017/02/vue01-2.jpg'
        }
    })
</script>
~~~

**绑定CSS样式**

在绑定CSS样式是，绑定的值必须在vue中的data属性中进行声明。 

~~~html
<div :class="className">直接绑定class样式</div>
<div :class="{classA:isOk}">绑定class中的判断</div>
<div :class="[classA,classB]">绑定class中的数组</div>
<div :class="isOk?classA:classB">绑定class中的三元表达式判断</div>
<div :style="{color:red,fontSize:font}">绑定style</div>

<div :style="styleObject">
    用对象绑定style样式
</div>
<script>
    var app=new Vue({
        el:'#app',
        data:{
            styleObject:{
                fontSize:'20px',
                color:'orange'
            }
        }
    })
</script>
~~~



##### 8.v-pre / v-cloak / v-once

**v-pre：**在模板中跳过vue的编译，直接输出原始值。就是在标签中加入v-pre就不会输出vue中的data值了。这时并不会输出我们的message值，而是直接在网页中显示{{message}}

~~~html
<div v-pre>{{message}}</div>
~~~

**v-cloak：**在vue渲染完指定的整个DOM后才进行显示。它必须和CSS样式一起使用，

~~~html
[v-cloak]{
    display:none,
}
<div v-cloak>{{message}}</div>
~~~

**v-once：**在第一次DOM时进行渲染，渲染完成后视为静态内容，跳出以后的渲染过程

~~~html
<div v-once>第一次绑定的值:{{message}}</div>
<div><input type="text" v-model="message"></div>
~~~





#### 二、Vue2.0-全局API

**全局API并不在构造器里，而是先声明全局变量或者直接在Vue上定义一些新功能；**

##### 1.Vue.directive

~~~html
<div id="app">
    <div v-color="color" id="demo">
        {{num}}
    </div>
    <div>
        <button @click="add">
            Add
        </button>
    </div>
</div>
<script>
Vue.directive('color',function(el,binding,vnode){
    el.style='color:'+binding.value;
})
    var app=new Vue({
        el:'#app',
        data:{
            num:10,
            color:'blue'
        },
        methods:{
            add:function(){
                this.num++;
            }
        }
    })
</script>
~~~

**自定义指令中传递的三个参数**

- **el：**指令所绑定的元素，可以用来直接操作DOM;
- **binding：**一个对象，包含指令的很多信息;
- **vnode：**Vue编译生成的虚拟节点；

**自定义指令的生命周期（钩子函数）**

- **bind：**只调用一次，指令第一次绑定到元素时调用，用这个钩子函数可以定义一个绑定时执行一次的初始化动作。
- **inserted：**被绑定元素插入父节点时调用（父节点存在即可调用，不必存在于document中）。
- **update：**被绑定于元素所在的模板更新时调用，而无论绑定值是否变化。通过比较更新前后的绑定值，可以忽略不必要的模板更新。
- **componentUpdated：**被绑定元素所在模板完成一次更新周期时调用。
- **unbind：**只调用一次，指令与元素解绑时调用。



##### 2.Vue.extend

Vue.extend 返回的是一个“扩展实例构造器”,也就是预设了部分选项的Vue实例构造器。经常服务于Vue.component用来生成组件，可以简单理解为当在模板中遇到该组件名称作为标签的自定义元素时，会自动调用“扩展实例构造器”来生产组件实例，并挂载到自定义元素上。

~~~html
<author></author>
<script>
    var authorExtend=Vue.extend({
        template:"<p><a :href='authorUrl'>{{authorName}}</p>",
        data:{
            authorUrl:'http://www.baidu.com',
            authorName:'wang'
        }
    })
    <!-- 挂载：可以通过 id class -->
    new authorExtend().$mount('author')
</script>
~~~



##### 3.Vue.set

Vue.set 的作用就是在构造器外部操作构造器内部的数据、属性或者方法。比如在vue构造器内部定义了一个count为1的数据，我们在构造器外部定义了一个方法，要每次点击按钮给值加1.就需要用到Vue.set。

什么是外部数据，就是不在Vue构造器里里的data处声明，而是在构造器外部声明，然后在data处引用就可以了。外部数据的加入让程序更加灵活，我们可以在外部获取任何想要的数据形式，然后让data引用。

~~~html
<div id="app">
    <ul>
        <li v-for="item in arr">{{item}}</li>
    </ul>
</div>
<button onclick="add()">外部添加</button>
<scrip>
    var outData={
    	arr:['aaa','bbb','ccc']
    };
    function add(){
    	app.arr[1]='ddd';
    	//Vue.set(app.arr,1,'ddd');
    	//这时我们的界面是不会自动跟新数组的，我们需要用Vue.set(app.arr,1,’ddd’)来设置改变，vue才会给我们自动更新，这就是Vue.set存在的意义。
    }
    var app=new Vue({
		el:'#app',
    	data:outData
    })
</scrip>
~~~



##### 4.Vue 生命周期

钩子函数：Vue一共有10个生命周期函数，我们可以利用这些函数在vue的每个阶段都进行操作数据或者改变内容。

~~~html
<div id="app">
    {{message}}
    <p><button @click="add">加分</button>
    </p>
</div>
<button onclick="app.$destroy()">销毁</button>
<script>
    var app=new Vue({
        el:'#app',
        data:{
            message:1
        },
        methods:{
            add:function(){
                this.message++;
            },
            beforeCreate:function(){
                console.log('1.初始化后')
            },
            created:function(){
                console.log('2.创建完成');
            },
            beforeMount:function(){
                console.log('3.挂载之前');
            },
            mounted:function(){
                console.log('4.被创建');
            },            
            beforeUpdate:function(){
                console.log('5.数据更新前');
            },
            updated:function(){
                console.log('6.被更新后');
            },
            activated:function(){
                console.log('7.activated');
            },
            deactivated:function(){
                console.log('8.deactivated');
            },
            beforeDestroy:function(){
                console.log('9.beforeDestroy 销毁之前');
            },
            destroyed:function(){
                console.log('10.destroyed 销毁之后')
            }
        }
    })
</script>
~~~



##### 5.Template

**(1)、直接写在选项里的模板**

直接在构造器里的template选项后边编写。这种写法比较直观，但是如果模板html代码太多，不建议这么写。

~~~html
<script>
    var app=new Vue({
        el:'#app',
        data:{
            message:'hello Vue!'
        },
        template:`<h1 style="color:red">我是选项模版</h1>`
    })
</script>
~~~

**(2)、写在template标签里的模板**

这种写法更像是在写HTML代码，就算不会写Vue的人，也可以制作页面。

~~~html
<template id="demo">
	<h2 style="color:red">我是template标签模版</h2>
</template>
<script>
    var app=new Vue({
        el:'#app',
        data:{
            message:'Hello Vue!'
        },
        template:'#demo'
    })
</script>
~~~

**(3)、写在script标签里的模板**

~~~html
<script type="x-template" id="demo">
	<h2 style="color:red">我是script标签moan</h2>
</script>
<script type="text/javascript">
    var app=new Vue({
        el:'#app',
        data:{
            message:'Hello Vue!'
        },
        template:'demo'
    })
</script>
~~~

**(4)、学习到vue-cli的时候还会学到一种xxx.vue的写法**



##### 6.Vue.component

**(1)、全局化注册组件**

全局化就是在构造器的外部用Vue.component来注册，我们注册现在就注册一个的组件来体验一下。

~~~html
<div id="app">
    <wang></wang>
</div>
<script>
    Vue.component('wang',{
        template:`<div style="color:red">全局化注册的wang标签</div>`
    })
    var app=new Vue({
        el:'#app',
        data:{
            
        }
    })
</script>
~~~

**(2)、局部化注册组件**

~~~html
<div id="app">
    <wang></wang>
</div>
<script>
    var app=new Vue({
        el:'#app',
        componets:{
            'wang':{
                template:`<div style="color:red;">局部化注册的wang标签</div>`
            }
        }
    })
</script>
~~~

从代码中你可以看出局部注册其实就是写在构造器里，构造器里的components 是加s的，而全局注册是不加s的。

**组件和指令的区别？**

组件注册的是一个标签，而指令注册的是已有标签里的一个属性。在实际开发中我们还是用组件比较多，指令用的比较少。因为指令看起来封装的没那么好，这只是个人观点。



##### 7.component props属性

**(1)、定义属性并获取属性值**

定义属性我们需要用props选项，加上数组形式的属性名称，例如：props:[‘here’]。在组件的模板里读出属性值只需要用插值的形式，例如{{ here }}.

~~~html
<div id="app">
    <wang here="china"></wang>
</div>
<script>
    var app=new Vue({
        el:'#app',
        components:{
            'wang':{
                 props:['here'],
                tempale:`<div style="color:red;">wang form {{here}}</div>`,
            }
        }
    })
</script>
~~~

**(2)、属性中带’-‘的处理方式**

我们在写属性时经常会加入’-‘来进行分词，比如：，那这时我们在props里如果写成props:[‘form-here’]是错误的，我们必须用小驼峰式写法props:[‘formHere’]。

**(3)、在构造器里向组件中传值**

~~~html
<div id="app">
    <wang v-bind:here='message'></wang>
</div>
<script>
    var app=new Vue({
        el:'#app',
        data:{
            message:'贵州'
        },
        components:{
            'wang':{
                template:`<div style="color:red;">wang from {{here}}</div>`,
                props:[here]
            }
        }
    })
</script>
~~~



##### 8.component 父子组件关系

~~~html
<div id="app">
    <wang></wang>
</div>
<script>
    var city={
        template:`<div>贵州</div>`
    }
    var wang={
        template:`<div><p>wang from china</p><city></city></div>`,
        components:{
            'city':city
        }
    }
    var app=new Vue({
        el:'#app',
        components:{
            'wang':wang
        }
    })
</script>
~~~



##### 9.component 标签

~~~html
<div id="app">
    <component v-bind:is="who"></component>
    <button @click="changeComponent">changeComponent</button>
</div>
<script>
        var componentA={
            template:`<div style="color:red;">I'm componentA</div>`
        }
        var componentB={
            template:`<div style="color:green;">I'm componentB</div>`
        }
        var componentC={
            template:`<div style="color:pink;">I'm componentC</div>`
        }
        var app=new Vue({
            el:'#app',
            data:{
                who:'componentA'
            },
            components:{
                'omponentA':componentA,
                'componentB':componentB,
                'componentC':componentC,
            },
            methods:{
                changeComponent:function(){
                    if(this.who=='componentA'){
                        this.who='componentB';
                    }else if(this.who=='componentB'){
                        this.who='componentC';
                    }else{
                        this.who='componentA';
                    }
                }
            }
        })
</script>
~~~



#### 三、Vue2.0-选项

##### 1.propsData Option

~~~html
<header></header>
<script>
    var header_a=Vue.extend({
        template:'<p>{{message}}--{{a}}</p>',
        data:function(){
            return{
                message:'Hello Vue'
            }
        },
        props:['a']
    });
    new header_a({propsData:{a:1}}).$mount('header');
</script>
~~~



##### 2.computed Option

computed 的作用主要是对原数据进行改造输出。改造输出：包括格式的编辑，大小写转换，顺序重排，添加符号……。

(1)、格式化输出结果

~~~html
<div id="app">
	{{newPrice}}
</div>
<script>
    var app=new Vue({
        el:'#app',
        data:{
            price:100
        },
        computed:{
            newPrice:function(){
                return this.price='￥'+this.prive+'元';
            }
        }
    })
</script>
~~~

(2)、用计算属性反转数组

~~~html
<script>
    var newList=[
        {title:'香港或就“装甲车被扣”事件追责 起诉涉事运输公司',date:'2017/3/10'},
    	{title:'日本第二大准航母服役 外媒：针对中国潜艇',date:'2017/3/12'},
    	{title:'中国北方将有明显雨雪降温天气 南方阴雨持续',date:'2017/3/13'},
    	{title:'起底“最短命副市长”：不到40天落马，全家被查',date:'2017/3/23'},
    ];
    
    computed:{
        reverseNews:functions(){
            return this.newsList.reverse();
        }
    }
</script>
~~~



##### 3.methods Option

(1)、methods中参数的传递

~~~html
<div id="app">
    {{a}}
    <button @click="add(2)">
        add
    </button>
</div>
<script>
    var app=new Vue({
        el:'#app',
        data:{
            a:1
        },
        methods:{
            add:function(num){
                if(num!=''){
                    this.a+=num;
                }else{
                    this.a++
                }
            }
        }
    })
</script>
~~~

(2)、methods中的$event参数

传递的$event参数都是关于你点击鼠标的一些事件和属性。

~~~html
<button @click="add(2,$event)">
    add
</button>
~~~

(3)、native 给组件绑定构造器里的原生事件。

在实际开发中经常需要把某个按钮封装成组件，然后反复使用，如何让组件调用构造器里的方法，而不是组件里的方法。就需要用到我们的.native修饰器了。

~~~html
<!-- 声明btn对象： -->
var vtn={
template:`<button>组件Add</button>`
}
<!-- 在构造器里声明 -->
components:{
	"btn":btn
}
<!-- 用.native修饰器来调用构造器里的add方法 -->
<p>
    <btn @click.native="add(3)"></btn>
</p>

~~~

(4)、作用域外部调用构造器里的方法

这种不经常使用，如果你出现了这种情况，说明你的代码组织不够好。

~~~html
<button onclick="app.add(4)">
    外部调用构造器里的方法
</button>
~~~



##### 4.watch Option

目的：监控数据

(1)、构造器内部

~~~html
<div id="app">
    <p>今日温度：{{temp}}°</p>
    <p>建议穿衣：{{clothes}}</p>
    <button @click="upTemp">升温</button>
    <button @click="downTemp">降温</button>
</div>
<script>
    var clothesArr=['短袖','夹克衫','羽绒服']；
    var app=new Vue({
        el:'#app',
        data:{
            temp:24,
            clothes:'夹克衫'
        },
        methods:{
            upTemp:function(){
              this.temp+=5;  
            },
            downTemp:function(){
                this.temp-=5;
            }
        },
        watch:{
            //监听 temp数据
            temp:function(newVal,oldVal){ 
                if(newVal>=26){
                    this.clothes=clothesArr[0];
                }else if(newVal<26&&newVal>0){
                    this.clothes=clothesArr[1];
                }else{
                    this.clothes=clothesArr[2];
                }
            }
        }
    })
</script>
~~~

(2)、构造器外部

~~~html
<div id="app">
    <p>今日温度：{{temp}}°</p>
    <p>建议穿衣：{{clothes}}</p>
    <button @click="upTemp">升温</button>
    <button @click="downTemp">降温</button>
</div>
<script>
    var clothesArr=['短袖','夹克衫','羽绒服']；
    var app=new Vue({
        el:'#app',
        data:{
            temp:24,
            clothes:'夹克衫'
        },
        methods:{
            upTemp:function(){
              this.temp+=5;  
            },
            downTemp:function(){
                this.temp-=5;
            }
        },
    })
    //监听 temp数据
    app.$watch('temp',function(newVal,oldVal){           
        if(newVal>=26){  
            this.clothes=clothesArr[0];
        }else if(newVal<26 && newVal>0){      
            this.clothes=clothesArr[1];    
        }else{      
            this.clothes=clothesArr[2]; 
        }
    })
</script>
~~~



##### 5.mixins Option

Mixins一般有两种用途：

在你已经写好了构造器后，需要增加方法或者临时的活动时使用的方法，这时用混入会减少源代码的污染；

很多地方都会用到的公用方法，用混入的方法可以减少代码量，实现代码重用；

(1)、基本用法

~~~html
<div id="app">
    <p>num:{{num]}</p>
    <p><button @click="app">增加数量</button></p>
</div>
<script>
    //额外临时加入时，用于显示日志
    var addLog={
        updated:function(){
            console.log('数据发生变化：'+this.num)
        }
    }
    var app=new Vue({
        el:'#app',
        data:{
            num:1
        },
        methods:{
            add:function(){
                this.num++;
            }
        },
        mixins;[addLog];//混入
    })
</script>
~~~

(2)、mixins的调用顺序

从执行的先后顺序来说，都是混入的先执行，然后构造器里的再执行，需要注意的是，这并不是方法的覆盖，而是被执行了两边。

在上边的代码的构造器里我们也加入了updated的钩子函数：

~~~javascript
updated:function(){
      console.log("构造器里的updated方法。")
},
~~~

这时控制台输出的顺序是：

~~~~javascript
mixins数据放生变化,变化成2.
构造器里的updated方法。
~~~~

注意：当混入方法和构造器的方法重名时，混入的方法无法展现，也就是不起作用。

(3)、全局API混入方法

我们也可以定义全局的混入，这样在需要这段代码的地方直接引入js，就可以拥有这个功能了。我们来看一下全局混入的方法：

~~~javascript
Vue.mixin({
    updated:function(){
        console.log('我是全局被混入的');
    }
})
~~~



##### 6.extends Option

通过外部增加对象的形式，对构造器进行扩展。它和混入非常的类似。

~~~html
<div id="app">
	{{message}}
    <button @click="add">add</button>
</div>
<script>
    var bbb={
        created:function(){
            console.log('我是被扩展出来的');
        },
        methods:{
            add:function(){
                 console.log('我是被扩展出来的方法！');
            }
        }
    };
    var app=new Vue({
        el:'#app',
        data:{
            message:'Hello Vue!'
        },
        methods:{
            add:function(){
                console.log('我是原生方法')
            }，
            extends:bbb
        }
    })
</script>
~~~



##### 7.delimiters Option 插值选项

delimiters的作用是改变我们插值的符号。Vue默认的插值是双大括号{{}}。但有时我们会有需求更改这个插值的形式。

~~~javascript
delimiters:['${','}']
~~~

现在我们的插值形式就变成了${}。



#### 四、Vue2.0-实例和内置组件

##### 1.实例属性

(1)、Vue.js和jQuery.js一起使用

~~~html
<div id="app">
    {{message}}
</div>
<script>
    var app=new Vue({
        el:'#app',
        data:{
            message:'hello Vue!'
        },
        //在Vue中使用jQuery
        mounted:function(){
            $('#app').html('我是jQuery!');
        }
    })
</script>
~~~

页面显示：我是jQuery，而不是hello Vue了。

(2)、实例调用自定义方法

~~~javascript
methods:{
    add:function(){
        console.log('调用了add方法!');
    }
}
~~~

实例调用

~~~
app.add();
~~~



##### 2.实例方法

(1)、$mount() 挂载方法

$mount方法是用来挂载我们的扩展的

~~~html
<div id="app">
    {{message}}
</div>
<script>
    var wang=Vue.extend({
        template:`<p>{{message}}</p>`,
        data:function(){
            return{
                message:'Hello,wang!'
            }
        }
    })
    var vm=new wang().$mount('#app');
</script>
~~~

(2)、$destroy() 卸载方法

~~~html
<button onclick="destroy()">
    卸载
</button>
<script>
    function destroy(){
        vm.$destroy();
    }
</script>
~~~

(3)、$forceUpdate() 更新方法

~~~
vm.$forceUpdate()
~~~

(4)、$nextTick() 数据修改方法

当Vue构造器里的data值被修改完成后会调用这个方法，也相当于一个钩子函数吧，和构造器里的updated生命周期很像

~~~javascript
function tick(){
    vm.message="update message info";
    vm.$nextTick(function(){
        console.log('message更新完后我被调用了!');
    })
}
~~~



##### 3.实例事件

(1)、$on 在构造器外部添加事件

~~~javascript
app.$on('reduce',function(){
    console.log('执行了reduce()')
    this.num--;//num为vue data中数据
})
~~~

$on接收两个参数，第一个参数是调用时的事件名称，第二个参数是一个匿名方法。

如果按钮在作用域外部，可以利用$emit来执行。

~~~javascript
//外部调用内部事件
function reduce(){
    app.$emit('reduce');
}
~~~

(2)、$once 执行一次的事件

~~~javascript
app.$once('reduceOnce',function(){
    console.log('只执行一次的方法');
    this.num--;
})
~~~

(3)、$off 关闭事件

~~~javascript
//关闭事件
function off(){
    app.$off('reduce');
}
~~~



##### 4.内置组件-slot讲解

slot是标签的内容扩展，也就是说你用slot就可以在自定义组件时传递给组件内容，组件接收内容并输出。

~~~html
<div id="app">
    <wang>
    	<span slot="blogUrl">{{wang.blogUrl}}</span>
        <span slot="netName">{{wang.netName}}</span>
        <span slot="skill">{{wang.skill}}</span>
    </wang>
</div>
<template id="tmp">
	<div>
        <p>博客地址:<slot name="blogUrl"></slot></p>
        <p>网名：<slot name="netName"></slot></p>
        <p>技术类型：<slot name="skill"></slot></p>
    </div>
</template>

<script>
    var wang={
        template:'#tmp'
    }
    var app=new Vue({
        el:'#app',
        data:{
            wang:{
                blogUrl:'http://wang.com',
                netName:'昌',
                skill:'javascript'
            }
        },
        components:{
            "wang":wang
        }
    })
</script>
~~~

#### 五、vue-router

##### 1.vue-router 安装

npm install vue-router --save-dev

##### 2.解读router/index.js文件

```javascript
import Vue from 'vue'   //引入Vue
import Router from 'vue-router'  //引入vue-router
import Hello from '@/components/Hello'  // 引入Hello.vue组件
Vue.use(Router)  //Vue全局使用Router
export default new Router({
  routes: [              //配置路由，这里是个数组
    {                    //每一个链接都是一个对象
      path: '/',         //链接路径
      name: 'Hello',     //路由名称，
      component: Hello   //对应的组件模板
    }
  ]
})
```

##### 3.vue-router 新增路由页

(1)在src/components目录下 新建Hi.vue文件

```javascript
<template>
  <div class="hello">
    <h1>{{ msg }}</h1>
  </div>
</template>
<script>
export default {
  name: 'hi',
  data () {
    return {
      msg: 'Hi, I am JSPang'
    }
  }
}
</script>
<style scoped>
</style>
```

(2)在router/index.js文件中 引入Hi.vue组件并配置路由

```javascript
import Vue from 'vue'
import Router from 'vue-router'  
import Hello from '@/components/Hello'  
import Hi from '@/components/Hi' // 引入Hi组件
Vue.use(Router)
export default new Router({
  routes: [
    {
      path: '/',
      name: 'Hello',
      component: Hello
    },
    {// 配置路由
      path:'/hi',
      name:'Hi',
      component:Hi
    }
  ]
})
```

(3)router-link制作导航

```html
<router-link to="/">[显示字段]</router-link>
<!-- 
    to: 导航路径，填写在router/index.js文件里配置的path值，如果要导航到默认首页，只需to="/";
    [显示字段]: 显示给用户的导航名称，比如首页 新闻页
-->
```

##### 4.vue-router 配置子路由

(1)router-link

```html
<p>导航 ：
    <router-link to="/">首页</router-link> |
    <router-link to="/hi">Hi页面</router-link> |
    <router-link to="/hi/hi1">-Hi页面1</router-link> |
    <router-link to="/hi/hi2">-Hi页面2</router-link>
</p>
```

(2)Hi.vue 引入router-view

```html
<template>
  <div class="hello">
    <h1>{{ msg }}</h1>
    <router-view class="aaa"></router-view>
  </div>
</template>
```

(3)router/index.js

```javascript
import Vue from 'vue'
import Router from 'vue-router'  
import Hello from '@/components/Hello'  
import Hi from '@/components/Hi'
import Hi1 from '@/components/Hi1'
import Hi2 from '@/components/Hi2'
Vue.use(Router)
export default new Router({
  routes: [
    {
      path: '/',
      name: 'Hello',
      component: Hello
    },
    {
      path:'/hi',
      component:Hi,
      children:[
        {path:'/',component:Hi},
        {path:'hi1',name:'hi1',component:Hi1},
        {path:'hi2',name:'hi2',component:Hi2},
      ]
    }
  ]
})
```

##### 5.vue-router 传递参数

(1)通过name传递参数

```javascript
//在路由文件src/router/index.js里配置name属性。
routes: [
{
  path: '/',
  name: 'Hello',
  component: Hello
}
]
//模板里(src/App.vue)用$route.name的形势接收
<p>{{$route.namte}}</p>
```

(2)通过标签中的to传参参数

```html
<!-- src/App.vue的路由 -->
<router-link :to="{name:'hi1',params:{username:'wang'}}">valueString</router-link>
<!-- 
    name：就是我们在路由配置文件中起的name值。
    params：就是我们要传的参数，它也是对象形势，在对象里可以传递多个值。 
-->
<!-- Hi1.vue页接收 -->
{{$route.params.username}}

```

(3)通过url传递参数

```javascript
// App.vue
<router-link to="/params/198/新闻标题">params</router-link>
// src/router/index.js
{
    path:'/params/:newsId/:newsTitle',
    //path:'/params/:newsId(\\d+)/:newsTitle',//newsId只能是数字的形式
    component:Params
}
// 新建params.vue
<template>
    <div>
        <h2>{{ msg }}</h2>
        <p>新闻ID：{{ $route.params.newsId}}</p>
        <p>新闻标题：{{ $route.params.newsTitle}}</p>
    </div>
</template>
<script>
export default {
  name: 'params',
  data () {
    return {
      msg: 'params page'
    }
  }
}
</script>


```

##### 6.vue-router 单页面多路由区域操作

```html
<!-- App.vue -->
<router-view></router-view>
 <router-view name="left" style="float:left;width:50%;background-color:#ccc;height:300px;"></router-view>
 <router-view name="right" style="float:right;width:50%;background-color:#c0c;height:300px;"></router-view>

```

```javascript
import Vue from 'vue'
import Router from 'vue-router'
import Hello from '@/components/Hello'
import Hi1 from '@/components/Hi1'
import Hi2 from '@/components/Hi2'
Vue.use(Router)
export default new Router({
  routes: [
    {
      path: '/',
      components: {
        default:Hello,
        left:Hi1,
        right:Hi2
      }
    },{
      path: '/Hi',
      components: {
        default:Hello,
        left:Hi2,
        right:Hi1
      }
    }
  ]
})

```

##### 7.vue-router 重定向-redirect

```javascript
// src/router/index.js把原来的component换成redirect参数就可以了;
export default new Router({
  routes: [
    {
      path: '/',
      component: Hello
    },{
      path:'/params/:newsId(\\d+)/:newsTitle',
      component:Params
    },{
      path:'/goback',
      redirect:'/'
    }
  ]
})
//设置了goback路由，但是它并没有配置任何component（组件），而是直接redirect到path:’/’下了，这就是一个简单的重新定向。

//重定向时传递参数
{
  path:'/params/:newsId(\\d+)/:newsTitle',
  component:Params
},
{
  path:'/goParams/:newsId(\\d+)/:newsTitle',
  redirect:'/params/:newsId(\\d+)/:newsTitle'
}

```

##### 8.vue-router alias别名的使用

```javascript
// src/router/index.js
{
    path: '/hi1',
    component: Hi1,
    alias:'/jspang'
 }
// 直接使用<router-link>标签里的to属性，进行重新定向
<router-link  to="/jspang">jspang</router-link>

// redirect和alias的区别
// redirect：仔细观察URL，redirect是直接改变了url的值，把url变成了真实的path路径。
// alias：URL路径没有别改变，这种情况更友好，让用户知道自己访问的路径，只是改变了<router-view>中的内容。

```

##### 9.vue-router 过度动画

```javascript
// src/App.vue <router-view>标签的外部添加<transition>标签
<transition name="fade">
  <router-view ></router-view>
</transition>
<style>
.fade-enter {
  opacity:0;
}
.fade-leave{
  opacity:1;
}
.fade-enter-active{
  transition:opacity .5s;
}
.fade-leave-active{
  opacity:0;
  transition:opacity .5s;
}
</style>
// css过渡类名： 组件过渡过程中，会有四个CSS类名进行切换，这四个类名与transition的name属性有关，比如name=”fade”,会有如下四个CSS类名：
// fade-enter:进入过渡的开始状态，元素被插入时生效，只应用一帧后立刻删除。
// fade-enter-active:进入过渡的结束状态，元素被插入时就生效，在过渡过程完成后移除。
// fade-leave:离开过渡的开始状态，元素被删除时触发，只应用一帧后立刻删除。
// fade-leave-active:离开过渡的结束状态，元素被删除时生效，离开过渡完成后被删除。
// 从上面四个类名可以看出，fade-enter-active和fade-leave-active在整个进入或离开过程中都有效，所以CSS的transition属性在这两个类下进行设置。


```

##### 10.vue-router 404页面

```javascript
// src/router/index.js
{
   path:'*',
   component:Error
}
// 新建src/components/Error.vue文件
<template>
    <div>
        <h2>{{ msg }}</h2>
    </div>
</template>
<script>
export default {
  data () {
    return {
      msg: 'Error:404'
    }
  }
}
</script>

// App.vue 点击下面路由到404页面
<router-link to="/bbbbbb">我是瞎写的</router-link> |


```

##### 11.vue-router 路由中的钩子函数

```javascript
// src/router/index.js路由文件中我们只能写beforeEnter
{
    path:'/params/:newsId(\\d+)/:newsTitle',
    component:Params,
    beforeEnter:(to,from,next)=>{
    console.log('我进入了params模板');
    console.log(to);
    console.log(from);
    next();
},
// to:路由将要跳转的路径信息，信息是包含在对像里边的。
// from:路径跳转前的路径信息，也是一个对象的形式。
// next:路由的控制参数，常用的有next(true)和next(false)。

// 写在模板中的钩子函数 在配置文件中的钩子函数，只有一个钩子-beforeEnter，如果我们写在模板中就可以有两个钩子函数可以使用：
// beforeRouteEnter：在路由进入前的钩子函数。
// beforeRouteLeave：在路由离开前的钩子函数。
export default {
  name: 'params',
  data () {
    return {
      msg: 'params page'
    }
  },
  beforeRouteEnter:(to,from,next)=>{
    console.log("准备进入路由模板");
    next();
  },
  beforeRouteLeave: (to, from, next) => {
    console.log("准备离开路由模板");
    next();
  }
}
</script>

```

##### 12.vue-router 编程式导航

```java
// 用<router-link>标签或者直接操作地址栏的形式完成的，那如果在业务逻辑代码中需要跳转页面我们如何操作？这就是我们要说的编程式导航，顾名思义，就是在业务逻辑代码中实现导航。
//this.$router.go(-1) 和 this.$router.go(1)
//这两个编程式导航的意思是后退和前进，功能跟我们浏览器上的后退和前进按钮一样，这在业务逻辑中经常用到。比如条件不满足时，我们需要后退。

// App.vue
<button @click="goback">后退</button>
<script>
export default {
  name: 'app',
  methods:{
    goback(){
      this.$router.go(-1);
    }
  }
}
</script>

//this.$router.push(‘/xxx ‘)
//这个编程式导航都作用就是跳转，比如我们判断用户名和密码正确时，需要跳转到用户中心页面或者首页，都用到这个编程的方法来操作路由。
//我们设置一个按钮，点击按钮后回到站点首页。
<button @click="goHome">回到首页</button>
export default {
  name: 'app',
  methods:{
    goHome(){
      this.$router.push('/');
    }
  }
}
```

#### 六、vuex

##### 1.vuex 安装

npm n install vuex --save

##### 2.vuex demo

```javascript
// 1.新建store/store.js文件，
// 2.引入(import)vue和vuex
// 3.使用vuex:Vue.use(Vuex)
```



#### 7、Vue-Cli

##### 0.技术栈

vue2+webpack+vueRouter+element

##### 1.安装nodejs

node -v  &&  npm -v

##### 2.安装vue-cli

npm install vue-cli -g

##### 3.初始化项目:采用webpack模板

vue init webpack vue_demo

##### 4.进入项目根目录

cd vue_demo

##### 5.安装package.json中依赖包

npm install

##### 6.开发模式下运行项目

npm run dev

##### 7.打包项目

npm run build  --根目录生成了dist文件夹,

##### 8。项目结构

```javascript
|-- build                            // 项目构建(webpack)相关代码
|   |-- build.js                     // 生产环境构建代码
|   |-- check-version.js             // 检查node、npm等版本
|   |-- dev-client.js                // 热重载相关
|   |-- dev-server.js                // 构建本地服务器
|   |-- utils.js                     // 构建工具相关
|   |-- webpack.base.conf.js         // webpack基础配置
|   |-- webpack.dev.conf.js          // webpack开发环境配置
|   |-- webpack.prod.conf.js         // webpack生产环境配置
|-- config                           // 项目开发环境配置
|   |-- dev.env.js                   // 开发环境变量
|   |-- index.js                     // 项目一些配置变量
|   |-- prod.env.js                  // 生产环境变量
|   |-- test.env.js                  // 测试环境变量
|-- src                              // 源码目录
|   |-- components                     // vue公共组件
|   |-- store                          // vuex的状态管理
|   |-- App.vue                        // 页面入口文件
|   |-- main.js                        // 程序入口文件，加载各种公共组件
|-- static                           // 静态文件，比如一些图片，json数据等
|   |-- data                           // 群聊分析得到的数据用于数据可视化
|-- .babelrc                         // ES6语法编译配置
|-- .editorconfig                    // 定义代码格式
|-- .eslintrc.js                     //javascript 代码检查
|-- .gitignore                       // git上传需要忽略的文件格式
|-- README.md                        // 项目说明
|-- index.html                       // 入口页面
|-- package.json                     // 项目基本信息
```

package.json

```javascript
package.json 文件是项目根目录下的一个文件，定义该项目开发所需要的各种模块以及一些项目配置信息(如项目名称、版本、描述、作者等);

scripts字段: 这个字段定义了你可以用npm运行的命令。在开发环境下，在命令行工具中运行npm run dev 就相当于执行 node build/dev-server.js .也就是开启了一个node写的开发行建议服务器。由此可以看出script字段是用来指定npm相关命令的缩写;
 "scripts": {
    "dev": "node build/dev-server.js",
    "build": "node build/build.js"
  },
dependencies字段: 指项目运行时所依赖的模块;
devDependencies字段: 指定了项目开发时所依赖的模块;
在命令行中运行npm install命令，会自动安装dependencies和devDempendencies字段中的模块。package.json还有很多相关配置，如果你想全面了解，可以专门去百度学习一下。
```

dev-server.js

```javascript
// 检查 Node 和 npm 版本
require('./check-versions')()

// 获取 config/index.js 的默认配置
var config = require('../config')

// 如果 Node 的环境无法判断当前是 dev / product 环境
// 使用 config.dev.env.NODE_ENV 作为当前的环境
if (!process.env.NODE_ENV) process.env.NODE_ENV = JSON.parse(config.dev.env.NODE_ENV)

// 使用 NodeJS 自带的文件路径工具
var path = require('path')

// 使用 express
var express = require('express')

// 使用 webpack
var webpack = require('webpack')

// 一个可以强制打开浏览器并跳转到指定 url 的插件
var opn = require('opn')

// 使用 proxyTable
var proxyMiddleware = require('http-proxy-middleware')

// 使用 dev 环境的 webpack 配置
var webpackConfig = require('./webpack.dev.conf')

// default port where dev server listens for incoming traffic
// 如果没有指定运行端口，使用 config.dev.port 作为运行端口
var port = process.env.PORT || config.dev.port

// Define HTTP proxies to your custom API backend
// https://github.com/chimurai/http-proxy-middleware
// 使用 config.dev.proxyTable 的配置作为 proxyTable 的代理配置
var proxyTable = config.dev.proxyTable

// 使用 express 启动一个服务
var app = express()

// 启动 webpack 进行编译
var compiler = webpack(webpackConfig)

// 启动 webpack-dev-middleware，将 编译后的文件暂存到内存中
var devMiddleware = require('webpack-dev-middleware')(compiler, {
  publicPath: webpackConfig.output.publicPath,
  stats: {
    colors: true,
    chunks: false
  }
})

// 启动 webpack-hot-middleware，也就是我们常说的 Hot-reload
var hotMiddleware = require('webpack-hot-middleware')(compiler)
// force page reload when html-webpack-plugin template changes
compiler.plugin('compilation', function (compilation) {
  compilation.plugin('html-webpack-plugin-after-emit', function (data, cb) {
    hotMiddleware.publish({ action: 'reload' })
    cb()
  })
})

// proxy api requests
// 将 proxyTable 中的请求配置挂在到启动的 express 服务上
Object.keys(proxyTable).forEach(function (context) {
  var options = proxyTable[context]
  if (typeof options === 'string') {
    options = { target: options }
  }
  app.use(proxyMiddleware(context, options))
})

// handle fallback for HTML5 history API
// 使用 connect-history-api-fallback 匹配资源，如果不匹配就可以重定向到指定地址
app.use(require('connect-history-api-fallback')())

// serve webpack bundle output
// 将暂存到内存中的 webpack 编译后的文件挂在到 express 服务上
app.use(devMiddleware)

// enable hot-reload and state-preserving
// compilation error display
// 将 Hot-reload 挂在到 express 服务上
app.use(hotMiddleware)

// serve pure static assets
// 拼接 static 文件夹的静态资源路径
var staticPath = path.posix.join(config.dev.assetsPublicPath, config.dev.assetsSubDirectory)

// 为静态资源提供响应服务
app.use(staticPath, express.static('./static'))

// 让我们这个 express 服务监听 port 的请求，并且将此服务作为 dev-server.js 的接口暴露
module.exports = app.listen(port, function (err) {
  if (err) {
    console.log(err)
    return
  }
  var uri = 'http://localhost:' + port
  console.log('Listening at ' + uri + '\n')
  
  // when env is testing, don't need open it
  // 如果不是测试环境，自动打开浏览器并跳到我们的开发地址
  if (process.env.NODE_ENV !== 'testing') {
    opn(uri)
  }
})
```

webpack.base.config.js

```javascript
module.export = {
    // 编译入口文件
    entry: {},
    // 编译输出路径
    output: {},
    // 一些解决方案配置
    resolve: {},
    resolveLoader: {},
    module: {
        // 各种不同类型文件加载器配置
        loaders: {
        ...
        ...
        // js文件用babel转码
        {
            test: /\.js$/,
            loader: 'babel',
            include: projectRoot,
            // 哪些文件不需要转码
            exclude: /node_modules/
        },
        ...
        ...
        }
    },
    // vue文件一些相关配置
    vue: {}
}
```

.babelrc



```javascript
//Babel解释器的配置文件，存放在根目录下。Babel是一个转码器，项目里需要用它将ES6代码转为ES5代码。如果你想了解更多，可以查看babel的知识。
{
  //设定转码规则
  "presets": [
    ["env", { "modules": false }],
    "stage-2"
  ],
  //转码用的插件
  "plugins": ["transform-runtime"],
  "comments": false,
  //对BABEL_ENV或者NODE_ENV指定的不同的环境变量，进行不同的编译操作
  "env": {
    "test": {
      "presets": ["env", "stage-2"],
      "plugins": [ "istanbul" ]
    }
  }
}
```

.editorconfig

```javascript
//该文件定义项目的编码规范，编译器的行为会与.editorconfig文件中定义的一致，并且其优先级比编译器自身的设置要高，这在多人合作开发项目时十分有用而且必要。
root = true
[*]    // 对所有文件应用下面的规则
charset = utf-8                    // 编码规则用utf-8
indent_style = space               // 缩进用空格
indent_size = 2                    // 缩进数量为2个空格
end_of_line = lf                   // 换行符格式
insert_final_newline = true        // 是否在文件的最后插入一个空行
trim_trailing_whitespace = true    // 是否删除行尾的空格
```