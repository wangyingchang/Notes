##### 1.一维数组

- 一组数据类型相同的数据集合;
- 内存地址连续；
- 长度固定；
- 下标从0开始;

(1).声明数组

~~~java
double[] myList;         // 首选的方法
或
double myList[];         //  效果相同，但不是首选方法
~~~

(2).创建数组

Java语言使用new操作符来创建数组，语法如下：

```java
arrayRefVar = new dataType[arraySize];
```

- 使用 dataType[arraySize] 创建了一个数组。
- 把新创建的数组的引用赋值给变量 arrayRefVar。

(3).声明和创建

```java
dataType[] arrayRefVar = new dataType[arraySize];
```

```java
dataType[] arrayRefVar = {value0, value1, ..., valuek};
```

数组的元素是通过索引访问的。数组索引从 0 开始，所以索引值从 0 到 arrayRefVar.length-1。



##### 2.二维数组

(1)二维数组定义：（中药店的药柜，电影院的座位）    

~~~java
    int[][] arr = new int[3][4];//定义了一个存放整型数据的数组，3行5列
    int[][] arr=new int[3][];//定义二维数组必须指定行的长度，可以不指定列的长度
    int  arr[][]=new int[3][4];//C语言的定义方法，对于java来说也是合法的
    int []arr[]=new int[3][];//合法,但是不建议这样创建声明
~~~

(2)二维数组的长度：  

```java
//arr.length : 获得该二维数组共有几行（共有几个一维数组）
//arr[0].length:获得该二维数组共有几列（每个一维数组有几个值）
```



##### 3.Arrays 类  

java.util.Arrays 类能方便地操作数组，它提供的所有方法都是静态的。

- 给数组赋值：通过 fill 方法。
- 对数组排序：通过 sort 方法,按升序。
- 比较数组：通过 equals 方法比较数组中元素值是否相等。
- 查找数组元素：通过 binarySearch 方法能对排序好的数组进行二分查找法操作。

![](https://i.imgur.com/AY2fAnV.png)



