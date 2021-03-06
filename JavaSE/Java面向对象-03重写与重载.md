##### 方法的重载（Overloading）

重载(overloading) 是在一个类里面，方法名字相同，而参数不同。返回类型可以相同也可以不同。每个重载的方法（或者构造函数）都必须有一个独一无二的参数类型列表。最常用的地方就是构造器的重载。

1.重载条件：

- 参数列表必须不同（个数、类型、顺序）；
- 方法名必须相同；

2.注意：

- 被重载的方法可以改变返回类型，无法以返回值类型作为重载函数的区分标准；
- 被重载的方法可以改变访问修饰符；
- 被重载的方法可以声明新的或更广的检查异常；
- 方法能够在同一类中或者在一个子类中被重载；

3.应用

最常用的地方就是构造器的重载。



##### 方法的重写（Overriding）

重写是子类对父类的允许访问的方法的实现过程进行重新编写, 返回值和形参都不能改变； 重写的好处在于子类可以根据需要，定义自己特定的行为 （具体实现不一样）。三同一小一大原则

1.条件

- 参数列表必须相同；
- 返回类型必须相同（void+8种基本数据类型）；引用数据类型，子类返回值与父类一致，或父类返回值的子类

2.注意：

- 父类的成员方法只能被它的子类重写；

- 静态方法不能被覆盖。

- 属性不能形成覆盖关系,如super.age。

- 构造方法不能被重写；

- 声明为final的方法不能被重写；

- 声明为static的方法不能被重写，但是能够再次声明；

- 访问权限不能比父类访问权限更低（private<缺省<protected<public）；

  ```
  --当父类访问权限为*private时，子类不能继承，如果不能继承一个方法，则不能重写这个方法；
  --子类和父类在同一个包中，子类可以重写父类所有方法，除了声明为private和final的方法； 
  --子类和父类不在同一个包中，子类只能够重写父类声明为public和protected的非final方法；
  ```

- 重写的方法能够抛出任何非强制异常，无论被重写的方法是否抛出异常。但是，重写的方法不能抛出新的强制性异常，或者比被重写方法声明的更广泛的强制性异常，反之则可以。

  例如： 父类的一个方法申明了一个检查异常 IOException，但是在重写这个方法的时候不能抛出 Exception 异常，因为 Exception 是 IOException 的父类，只能抛出 IOException 的子类异常。 

3.应用

封装类的toString()方法