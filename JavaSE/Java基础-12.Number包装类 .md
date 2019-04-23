**API-----Java.lang.Number**

##### 1.JDK1.5新特性之包装类

* 包装类的作用
* 包装类的自动装箱、自动拆箱 
* 包装类的转换

**2.Number类的定义** 
	Number是抽象类，主要是将数字包装类中的内容变为基本数据类型。

##### 3.基本数据类型包装

 基本数据类型		包装类		 	    
    int				 Integer			 
    char			         Character      
    byte				 Byte			 
    short				 Short               
    long				 Long			 
    float			 	 Float		 
    double			 Double		 
    boolean			 Boolean		 

##### 4.装箱及拆箱

	 基本数据类型 ----> 包装类  （装箱 ： boxing） 
	 包装类  ----> 基本数据类型 （拆箱: unboxing）

	 JDK1.5版本之前，包装类不能直接进行+，-，*，/等操作；
	 JDK1.5版本之后，增加了自动拆箱和装箱的功能，且可以使用包装类直接进行数字运算。

##### 5.包装类的应用

- 将字符串与数据类型相互转换、
- 泛型
- 实例

~~~java
/**
* @author Dale
* java中的自动装箱与拆箱
* 简单一点说，装箱就是自动将基本数据类型转换为包装器类型；拆箱就是自动将包装器类型转换为基本数据类型。
*/
public class Number {
    public static void main(String[] args) {
        /**
        Integer i1 = 128;  // 自动装箱，相当于 Integer.valueOf(128);
        int t = i1; //自动拆箱，相当于 i1.intValue() 
        System.out.println(t);
        */

        /**
        对于–128到127（默认是127）之间的值,被装箱后，会被放在内存里进行重用
        但是如果超出了这个值,系统会重新new 一个对象
        */
        Integer i1 = 200;
        Integer i2 = 200;
        /**
        注意 == 与 equals的区别
        == 它比较的是对象的地址
        equals 比较的是对象的内容
        */
        if(i1==i2) {
            System.out.println("true");
        } else {
            System.out.println("false");
        }
    }
}

*************************************************************************************
(1）Java 会对 -128 ~ 127 的整数进行缓存，所以当定义两个变量初始化值位于 -128 ~ 127 之间时，两个变量使用了同一地址：
Integer a=123;
Integer b=123;
System.out.println(a==b);        // 输出 true
System.out.println(a.equals(b);  // 输出 true

(2）当两个 Integer 变量的数值超出 -128 ~ 127 范围时, 变量使用了不同地址：
a=1230;
b=1230;
System.out.println(a==b);        // 输出 false
System.out.println(a.equals(b);  // 输出 true
~~~

