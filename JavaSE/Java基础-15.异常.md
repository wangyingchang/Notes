##### **一、异常概述**

**1.异常的分类**

![858860-20170911125844719-1230755033](http://incdn1.b0.upaiyun.com/2017/09/994bd262fec543853cd99fe680e857cc.png)

```
Throwable有两个子类：Error和Exception。
（1） Error： 硬件故障，程序员无法解决 。一个Error对象表示一个程序错误，指的是底层的、低级的、不可恢复的严重错误。此时程序一定会退出，因为已经失去了运行所必须的物理环境。对于Error错误我们无法进行处理，因为我们是通过程序来应对错误，可是程序已经退出了。

（2）Exception 程序员疏忽造成， 我们可以处理的Throwable类中只有Exception类的对象（例外/异常）。
			  抛出一个异常，就是抛出该异常的对象，如果不对其进行捕捉，就由JVM来捕捉，JVM捕捉到该异常后，
			  就把异常信息打印到控制台。

 Exception有两类：
（a）Runtime exception（运行时异常）可以在编程时避免，可处理可不处理. 。总是由虚拟机 接管。比如：我们从来没有人去处理过NullPointerException 异常，它就是运行时异常，并且这种异常还是最常见的异常之一。

(b) checked exception（编译时异常）必须进行处理。对于这种异常， JAVA 编译器强制要求我们必需对出现的这些异常进行catch 。所以，面对这种异常不管我们是否愿意，只能自己去写一大堆catch 块去处理可能的异常
```

注意：
	当一个方法中出现了异常，没有进行异常处理，方法就会把异常对象作为返回值返回。如果有异常进入虚拟机，那么虚拟机就会立刻中止程序的执行。

2.IOException

(1).EOFException

(2).FileNotFoundException

3.RuntimeException：  

(1).ArrayIndexOutOfBoundsException 数组越界异常

(2).NullPointerException 空指针引用异常(引用对象指向空)

(3).ArithmeticException 除数为0异常

(4).ClassNotFoundException

(5)IllegalArgumentException

(6).UnkownTypeException



##### **二、自定义异常**

**1.实例**

```java
/**
 * 银行系统异常的超级父类
 */
public class BankSystemException extends RuntimeException{
    public BankSystemException(){
        super("银行系统有异常");
    }
    public BankSystemException(String message){
      super(message);
    }
 }

/**
 *银行系统中的异常子类，账户余额不足异常
 */
public class BalanceNotEnoughException extends BankSystemException{
    public BalanceNotEnoughException(){
        super("账户余额不足");
    }
    public BalanceNotEnoughException(String message) {
        super(message);
    }
}

/**
 * 银行账户类
 */
public   class Account {
    //取款
    public Account withdraw(double money) throws BalanceNotEnoughException{
        if(this.accBalance < money)
            throw  new BalanceNotEnoughException("账户余额不足，请重新输入取款金额");
        else
            this.accBalance -= money;
        return this;
    }
    //转账
    public Account transferAccount(Account account,double money) throws BalanceNotEnoughException {
        if(this.accBalance < money)
            throw  new BalanceNotEnoughException("账户余额不足，请重新输入转账金额");
        else
            System.out.println("执行转账业务....");
        return this;
    }
}

测试类中：
	Account account = new Account();
    account.setAccBalance(1000);

    account.withdraw(1300);
    account.transferAccount(null,1200);
```

**2.自定义异常类四个步骤**：  

（1）首先创建自定义异常类
　　a. 自定义编译时异常类名 extends Exception。					     
        b.自定义运行时异常类名 extends RuntimeException。

（2）在方法中通过关键字throw抛出异常对象。

（3）若是在当前抛出异常的方法中处理异常，可以用try-catch语句捕获并处理；

​      若不是，在方法的声明处通过关键字throws指明要抛出给方法调用的异常。

（4）在出现异常方法的调用中捕获并处理异常。





##### **三、异常的处理**

**1.处理原则： 自己的问题 自己处理。**

（1）抛给调用方处理，在方法处throws XXException
（2）使用try-catch处理

**2.throws关键字**

（1）在定义一个方法的时候，可以使用throws关键字声明，使用throws声明的方法表示此方法不处理异常，而是交给方法的调用处去处理。

（2）throws使用格式：public 返回值类型  方法名称（参数列表）throws 异常类{}

（3）throw关键字的作用是在程序抛出一个异常，抛出的是一个异常类的实例化对象。
与throws不同的是，可以直接使用throw抛出一个异常。抛出的时候直接抛出异常类的实例化对象即可。



##### 四、try-catch-finally

（1）try{}  把可能会出现异常的代码放入try块中。

（2）catch(XX xx){} 捕获异常，并进行相应处理。
	  a.一个try{} 多个catch{}
	  b.万能捕捉器 Exception
	  c.注意使用万能捕捉器的顺序，先子类后父类

（3）finally :一定会执行的语句，写资源释放的代码 。

（4）语法使用

try{} 和catch(){},catch(){}
try{} 和catch(){}及finally{}
try{} 和finally{}
try{} 和catch(){} .....try{} 和catch(){}

（5）注意：

- catch块一定要与try块一起使用，不能够单独使用catch语句块；
- 一个try块可以有多个catch语句块，但是，多个catch块的排序必须是先子类后父类；
- 如果不发生异常，catch语句块永远不会执行；
- 一旦某个catch块被执行后，其他catch就都会被忽略；
- try-catch结构是可以嵌套使用的；

（5）finally：【出现try之后,资源释放的代码 】

try 或者 catch代码块执行完成之后；

finally后的代码块是无论如何都会被执行的代码，一般finally（）代码块在写释放资源的代码；

finally 代码块中最好不要出现返回语句(return)；

每个异常出现之后，会在程序中产生一个异常类来实例化对象，之后用此对象与catch中的异常类型相匹配，如果匹配成功，则执行catch中的内容，否则向下继续匹配，如果无法成功，程序就出现中断执行的问题；

finally 始终能被执行的代码；

**面试题：final\finally\finalize分别用在声明场合？**

（6）finally 与 return 

~~~java
public 基本数据类型 | 引用数据类型  fun(){
	 try{
		//...
		return xxx;		
	 }catch(..){
		//...
		return xxx;	
	 }finally{
		xxx = 新值；			
	}
}
~~~

finally 与return 谁先执行？

* finally: 用于释放资源，节省内存，语法上无论是否有异常，都会执
* return : 方法结束
* 先执行return ,再执行finally 

* 在finally中，修改return 的返回值变量，最后返回值究竟有没有发生改变？
  * 返回值：基本数据类型，finally 中修改返回值变量，返回值不会改变
    * 【值传递】
  * 返回值：引用数据类型，finally 中修改返回值变量，返回值会改变
    * 【地址传递】

（7） 实例

~~~java
   //返回10
    public int fun()
    {
        int i = 10;
        try
        {
            //doing something
            return i;
        }catch(Exception e){
            return i;
        }finally{
            i++;
        }
    }

    //返回20
    public static int fun()
    {
        int i = 10;
        try
        {
            //doing something
            return i;
        }catch(Exception e){
            return i;
        }finally{
            i = 20;
            return i;
        }
    }
~~~

~~~java
    //返回 HelloWorld
    public  StringBuilder  fun()
    {
        StringBuilder s=new StringBuilder("Hello");
        try{
            return s;
        }finally {
            s.append("World");
        }
    }

   //返回 Hello 因为String类型的值不会被改变
    public static String  fun()
    {
        String s=new String("Hello");
        try{
            return s;
        }finally {
            s.concat("world");
        }
    }
~~~

