##### 继承（inherit）

1.概念

```
“is a” 的关系
	狗是一种宠物 , 猫也是一种宠物 
	dog is a pet  
声明的格式  
	在Java 中 --  extends关键字
	public class Manager extends Employee   { 
	   	public Manager(){
			super();
	    }
	}
```

2.特性

- java.lang.**Object类**是所有类的根类；当一个类没有继承的两个关键字,默认继承object;
- 构造方法不能被继承；
- Java的继承是单继承，但是可以多重继承；
- 子类构造方法隐式调用父类的默认构造方法；

- 子类能够**继承**父类所有成员变量，但是private的变量不能调用；

- 子类**拥有**（**不能调用**）父类非private的属性和方法；
- 在子类的构造函数也可以显式的调用父类的构造, 使用super(…)，但是必须是第一个行有效；
- 子类可以拥有自己的属性和方法，即子类可以对父类进行扩展；
- 子类可以用自己的方式实现父类的方法（重写）；
- 提高了类之间的耦合性（继承的缺点）；
- 继承通过extends和implements两个关键字来实现;
- 使用 implements 关键字可以变相的使java具有多继承的特性，使用范围为类继承接口的情况，可以同时继承多个接口（接口跟接口之间采用逗号分隔）

3.this关键字

~~~
	  a. 直接写this：代表当前对象。
	  b. this.XXX：访问当前对象的实例成员；仅当方法中定义有与属性同名的局部变量时，在方法中访问类的属性才需要用this.XXX。
	  c. this(... )：调用本类的其他构造方法，这种用法只能出现在构造方法的第一行。
	  d说明在什么情况下需要用到this：
	  第一、通过this调用另一个构造方法，用法是this(参数列表)，这个仅仅在类的构造方法中，别的地方不能这么用。
	  第二、函数参数或者函数中的局部变量和成员变量同名的情况下，成员变量被屏蔽，此时要访问成员变量则需要用“this.成员变量名”的方式来引用成员变量。
	  第三、在函数中，需要引用该函所属类的当前对象时候，直接用this。

~~~

4.super关键字  

```
super():  调用父类的构造函数,需放在构造方法内第一行。
super.属性: 访问父类对象的实例成员。
super.方法: 访问父类对象的方法。

注：属性没有覆盖(重写)
```

5.this 和super的区别

```
super调用父类的属性，方法，构造函数：	
	super.属性  ， super.方法  ，super();

this调用属性，方法，构造函数：	
	this.方法  ， this.属性，this(...)

构造函数中的this：	
	get，set中的this

this 和super的区别：

```

6.继承与重写的实例

~~~java
class Super {
    int i = 10;//4
    Super () {//3
        print();//5
        i = 20;//7
    }
    void print() {
        System.out.println("Super ==> " + i);
    }
}
class SubClass extends Super {
    int i = 30;//8
    SubClass() {//2
        print();//9
        i = 40;//11
    }
    void print() {
        System.out.println("SubClass ==> " + i);//6  //10
    }
    public static void main(String[] args) {
        System.out.println(new SubClass().i);//1 //12
    }
}

//运行结果
SubClass ==> 0
SubClass ==> 30
40
~~~

~~~java
class Parent{
    private void method1(){
        System.out.println("Parent's method1()");
    }
    public void method2(){
        System.out.println("Parent's method2()");
        method1();
    }
}
class Child extends Parent{
    public void method1(){
        System.out.println("Child's method1()");
    }
    public static void main(String args[]){
        Parent p = new Child();
        p.method2();
    }
}

//运行结果
Parent's method2()
Parent's method1()
~~~

