##### 构造函数 Constructor

（1）构造函数的作用：可以用于给对象进行初始化。  
当一个类中没有定义构造函数时，那么系统会默认给该类加入一个无参的构造函数；

当在类中自定义了有参构造函数后，默认的构造函数就没有了；

如需还要使用无参构造函数，必须显式的定义出；

（2）构造函数必须与类同名
能被public private protected 缺省修饰，没有返回值

（3）构造的粗略过程如下 

    	a、分配对象空间，并将对象中成员初始化为0或者null等，java不允许用户操纵一个不定值的对象。 
    	b、初始化属性
    	c、执行构造函数方法体
    	d、将对象名指向堆内存中 		
（4）构造函数重载

子类不能继承父类的构造器，如果父类的构造器带有参数，则必须在子类的构造器中显式地通过 super 关键字调用父类的构造器并配以适当的参数列表；如果父类构造器没有参数，则在子类的构造器中不需要使用 super 关键字调用父类构造器，系统会自动调用父类的无参构造器。

（5）实例

~~~java
class SuperClass {
  private int n;
  SuperClass(){//10
    System.out.println("SuperClass()");//11
  }
  SuperClass(int n) {//4
    System.out.println("SuperClass(int n)");//5
    this.n = n;//6
  }
}
class SubClass extends SuperClass{
  private int n;
  
  SubClass(){//2
    super(300);//3
    System.out.println("SubClass");//7
  }  
  
  public SubClass(int n){//9
    System.out.println("SubClass(int n):"+n);//12
    this.n = n;//13
  }
}
public class TestSuperSub{
  public static void main (String args[]){
    SubClass sc = new SubClass();//1
    SubClass sc2 = new SubClass(200); //8
  }
}
~~~

~~~
SuperClass(int n)
SubClass
SuperClass()
SubClass(int n):200
~~~
