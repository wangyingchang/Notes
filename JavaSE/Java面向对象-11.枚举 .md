##### 枚举（enum）

JDK1.5新特性之枚举:  

1.枚举分析 
            是一种数据类型，是一个类，是一个final类，
            其对象是现成的固定的，其父类是java.lang.Enum。

2.在JDK5.0之前，用此方式实现枚举           

```java
    class Season1 {
        public static final Season1 SPRING = new Season1(“春天”);
        public static final Season1 SUMMER = new Season1(“夏天”);
        public static final Season1 AUTUMN = new Season1(“秋天”);
        public static final Season1 WINTER = new Season1(“冬天”);
        private String name;
        //构造方法私有
        private Season1() { 
            this.name = name
        }  
        public String getName() {
            return name;
        }
    }
```

3. JDK1.5支持枚举  

```java
   修饰符 enum Season2{
          //枚举值
          //属性
          //构造器（私有）
          //方法
   }
```
```java
   enum Season2{
         SPRING,SUMMER,AUTUMN,WINTER
   }
//or
   enum Season{
          //枚举值
         SPRING(“春天”),
         SUMMER(“夏天”),
         AUTUMN(“秋天”),
         WINTER(“冬天”);
         //属性
         String name;
         //构造器
         Season(String name){
             this.name=name;
         }
         //方法
         public String getName(){
             return this.name;
         }
   }
```

注意：
1）枚举可以很好的控制参数的种类和数量，保证必须按照程序员安排来选择;
2）类不能继承枚举，枚举也不能继承类，但可以实现接口;
3）枚举是一个final类，但是enum中却可以有抽象方法，抽象方法是由枚举值实现的;即这些抽象方法只能通过定义好的几个对象来实现，而且只能通过匿名的内部类的方法来实现。
4)枚举写在最前面，否则编译错误
5)实现带有构造器的枚举:
a. 通过括号赋值,而且必须带有一个参构造器和一个属性跟方法，否则编译出;
b. 赋值必须都赋值或都不赋值，不能一部分赋值一部分不赋值；如果不赋值则不能写构造器，赋值编译也出错.
6)构造器默认也只能是private, 从而保证构造函数只能在内部使用
7)枚举是一种类型，用于定义变量，以限制变量的赋值；赋值时通过“枚举名.值”取得枚举中的值(例如：ColorEnum colorEnum = ColorEnum.black;（switch case）)
8)for-each遍历枚举
9)获取枚举的个数
10)获取枚举的索引位置，默认从0开始
11)枚举默认实现了java.lang.Comparable接口

