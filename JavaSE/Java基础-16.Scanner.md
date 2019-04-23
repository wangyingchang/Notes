**API-----java.util.Scanner** 

##### 1.Scanner的作用

是 Java5 的新特征，我们可以通过 Scanner 类来获取用户的输入；

##### 2.创建Scanner

~~~java
Scanner scanner=new Scanner(System.in);
if (scanner.hasNextInt()) {
    //输入之前最好先使用hasNewXxx（）方法进行验证
}
~~~

**3.next()与nextLine()区别**

next():

- 一定要读取到有效字符后才可以结束输入。
- 对输入有效字符之前遇到的空白，next() 方法会自动将其去掉。
- 只有输入有效字符后才将其后面输入的空白作为分隔符或者结束符。
- next() 不能得到带有空格的字符串。

nextLine()：

- 以Enter为结束符,也就是说 nextLine()方法返回的是输入回车之前的所有字符。
- 可以获得空白。

