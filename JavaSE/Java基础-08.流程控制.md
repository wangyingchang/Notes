##### 顺序结构	

- if	
- if-else
- switch-case

switch与case后面的值的数据类型： 能够转换成int类型的数据类型（byte,short,int ,char），枚举，String字符串  （JDK1.7）

```
switch(表达式){
	case 常量表达式1：语句1
	case 常量表达式2：语句2
	......
	case 常量表达式n：语句n
	default: 语句n+1
}
//case块中不加break时顺序执行下面的语句
```

**break** 主要用在循环语句或者 switch 语句中，用来跳出整个语句块

**break** 跳出最里层的循环，并且继续执行该循环下面的语句



##### 循环结构

- while 

  while( 逻辑表达式 ){  // 返回true才继续循环执行代码块
  	//代码块
  }

- do-while

  do{
  	//代码块
  }while( 逻辑表达式 ){  // 返回true才继续循环执行代码块

- for循环  

  for(int i =0;i<10;i++){
  		//代码块
  	}  

  ~~~
  关于 for 循环有以下几点说明：
  最先执行初始化步骤。可以声明一种类型，但可初始化一个或多个循环控制变量，也可以是空语句。
  然后，检测布尔表达式的值。如果为 true，循环体被执行。如果为false，循环终止，开始执行循环体后面的语句。
  执行一次循环后，更新循环控制变量。
  再次检测布尔表达式。循环执行上面的过程。
  ~~~

- **foreach循环（JDK1.5引进）**

~~~java
public class TestArray {
   public static void main(String[] args) {
      double[] myList = {1.9, 2.9, 3.4, 3.5};
      // 打印所有数组元素
      for (double element: myList) {
         System.out.println(element);
      }
   }
}
~~~

**continue** 适用于任何循环控制结构中

作用是让程序立刻跳转到下一次循环的迭代

在 for 循环中，continue 语句使程序立即跳转到更新语句

在 while 或者 do…while 循环中，程序立即跳转到布尔表达式的判断语句