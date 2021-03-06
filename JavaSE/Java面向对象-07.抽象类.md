##### **抽象类（abstract class）**

如果你想设计这样一个类，该类包含一个特别的成员方法，该方法的具体实现由它的子类确定，那么你可以在父类中声明该方法为抽象方法。**Abstract**关键字同样可以用来声明抽象方法，抽象方法只包含一个方法名，而没有方法体。抽象方法没有定义，方法名后面直接跟一个分号，而不是花括号。 

```java
 public abstract class MockBusiness {
	    public void step1(){
 }
    public abstract void step2();// 依赖于第三方实现
    public void step3(){
    }
}
```

（1）抽象类的使用场景：在业务实现中，有一个或多个功能需要依赖于第三方实现，则把该些功能设计为抽象方法，则该类就为抽象类。

（2）定义：

含有抽象方法的类，就是抽象类；方法只有声明，没有实现（没有方法体）。

```java
abstract void grow();
abstract void grow(){}   有实现，空实现  error 
```

（3）抽象类的定义以及使用规则：

```java
有抽象方法的类必定是抽象类，但是抽象类不一定包含抽象方法（没有意义）
抽象类和抽象方法都要使用abstract关键字声明；
抽象方法只需声明不要实现；
抽象类必须被子类继承,任何子类必须重写（具体实现）父类的抽象方法，否则必须声明自身为抽象类；
抽象类不能被实例化,只能引用子类的对象,如果被实例化，就会报错，编译无法通过；只有抽象类的非抽象子类可以创建对象；
抽象类中的抽象方法只是声明，不包含方法体（具体实现）；
构造方法，类方法（static）不能声明为抽象方法；
抽象类作为参数，传的是子类的对象  
抽象类作为返回值，返回的是子类的对象。
```

（4）注意：final类不能有子类，抽象类必须有子类；

```
抽象类中能定义构造方法么？
答：能的；因为抽象类依然使用的是类的继承关系，且抽象类中
也存在各个属性，所以子类在实例化之前肯定是对父类进行的实例化的。
```

（5）补充：什么时候覆盖toString()方法？

Person p = new Person();

System.out.println(p);

java会自动调用toString()方法，但是结果不是我们想要的，因为Object类的toString()方法总是返回对象的实现类类名 + @ + hashCode值。我们希望的是能够打印出p的全名来，这时就希望能覆盖toString()方法，
因为重写toString方法之后，会优先调用自己的toString()方法。

