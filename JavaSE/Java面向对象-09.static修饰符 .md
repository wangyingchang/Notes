##### static修饰符

**Java的内存**

java把内存分为栈内存和堆内存,数据区，代码区，
栈内存用来存放一些基本类型的变量和数组及对象的引用变量，而堆内存主要是来放置对象的。
用static的修饰的变量和方法，实际上是指定了这些变量和方法在内存中的“固定位置”－data storage。

**作用：**方便在没有创建对象的情况下来进行调用（方法/变量）。 

**调用:** 类名.静态变量名

          类名.静态方法名(参数列表...)

**全局常量：**

```java
static final ADDRESS = "suzhou";
```

  **成员变量与类变量区别：**对于类变量在内存中只有数据一个拷贝（节省内存），JVM只为静态分配一次内存，在加载类的过程中完成static变量的内存分配，用类名直接访问（方便），当然也可以通过对象来访问（但是这是不推荐的）。静态变量属于类,为该类所有对象所分享,在程序开始执行前就分配内存空间, 如果前面加上final,功能类似全局常量,不可以修改其值.比如圆周率 。对于实例变量，每创建一个实例，就会为实例变量分配一次内存，实例变量可以在内存中有多个拷贝，互不影响（灵活）。

**static代码块:**static代码块也叫静态代码块，是在类中独立于类成员的static语句块，可以有多个，位置可以随便放，它不在任何的方法体内，JVM加载类时会执行这些静态的代码块，如果static代码块有多个，JVM将按照它们在类中出现的先后顺序依次执行它们，每个代码块只会被执行一次。

**为什么要使用static /  什么场合使用？**

* 一个方法没有对象意义（一个类中不存在对象的实际意义），该方法不需要对象来访问，通过类名访问
   类名.方法名(..)
   EncryptionUtil、 Math : 没有实例的意义
   Math 工具类: 仅仅只是为了实现一些数学中的算法操作而封装了一系列方法  abs(-9), max(78,43)
* 该变量属于类级别，归这一类群体的共性
     类变量： 类名.变量名
* 所以一般在需要实现以下两个功能时使用静态变量：  
- 在对象之间共享值时
- 方便访问变量时


 **案例分析：**  

父类static块（或static变量）> 子类static块（或static变量）> 父类初始化对象属性 > 父类代码块 > 父类构造函数 > 子类初始化对象属性> 子类代码块 > 子类构造函数

~~~java

public class Test{
     public static int p=2;//1
     public int age=22;//8
     public Test(){//7
        System.out.println("Test 构造函数");//10
    }
    static {
        System.out.println("Test static{}"+p);//2
    }

    {
        System.out.println("Test {}"+age);//9
    }
}
class TestA extends Test{
     public static int x=1;//3
     public int age=23;//11
     public TestA(){//6
        System.out.println("TestA 构造函数");//13
    }
    {
        System.out.println("TestA {}"+age);//12
    }
    static {
        System.out.println("TestA static{}"+x);//4
    }

    public static void main(String[] args) {
        new TestA();//5
    }
    
    
运行结果
Test static{}2
TestA static{}1
    
Test {}22
Test 构造函数
    
TestA {}23
TestA 构造函数
~~~



~~~java
class HelloA {
    public HelloA() {
        System.out.println("HelloA");
    }
    {
        System.out.println("I'm A class");
    }
    static {
        System.out.println("static A");
    }
}
 class HelloB extends HelloA {
    public HelloB() {
        System.out.println("HelloB");
    }
    {
        System.out.println("I'm B class");
    }
    static {
        System.out.println("static B");
    }
    public static void main(String[] args) {
        new HelloB();
    }
}
~~~

