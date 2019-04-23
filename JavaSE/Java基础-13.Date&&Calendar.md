**API-----java.util.Date** 

**API-----java.util.Calendar**







##### 1.创建日期



- java.util 包提供了 Date 类来封装当前的日期和时间
- Date 类提供两个构造函数来实例化 Date 对象

第一个构造函数使用当前日期和时间来初始化对象。

~~~java
Date( )
~~~

第二个构造函数接收一个参数，该参数是从1970年1月1日起的毫秒数。

~~~java
Date(long millisec)
~~~



##### 2.常用方法

| 序号 | 方法和描述                                                   |
| ---- | ------------------------------------------------------------ |
| 1    | **boolean after(Date date)** 若当调用此方法的Date对象在指定日期之后返回true,否则返回false。 |
| 2    | **boolean before(Date date)** 若当调用此方法的Date对象在指定日期之前返回true,否则返回false。 |
| 3    | **Object clone( )** 返回此对象的副本。                       |
| 4    | **int compareTo(Date date)** 比较当调用此方法的Date对象和指定日期。两者相等时候返回0。调用对象在指定日期之前则返回负数。调用对象在指定日期之后则返回正数。 |
| 5    | **int compareTo(Object obj)** 若obj是Date类型则操作等同于compareTo(Date) 。否则它抛出ClassCastException。 |
| 6    | **boolean equals(Object date)** 当调用此方法的Date对象和指定日期相等时候返回true,否则返回false。 |
| 7    | **long getTime( )** 返回自 1970 年 1 月 1 日 00:00:00 GMT 以来此 Date 对象表示的毫秒数。 |
| 8    | **int hashCode( )**  返回此对象的哈希码值。                  |
| 9    | **void setTime(long time)**   用自1970年1月1日00:00:00 GMT以后time毫秒数设置时间和日期。 |
| 10   | **String toString( )** 把此 Date 对象转换为以下形式的 String： dow mon dd hh:mm:ss zzz yyyy 其中： dow 是一周中的某一天 (Sun, Mon, Tue, Wed, Thu, Fri, Sat)。 |



##### 3.日期比较

- 使用 getTime() 方法获取两个日期（自1970年1月1日经历的毫秒数值），然后比较这两个值。
- 使用方法 before()，after() 和 equals()。例如，一个月的12号比18号早，则 new Date(99, 2, 12).before(new Date (99, 2, 18)) 返回true。
- 使用 compareTo() 方法，它是由 Comparable 接口定义的，Date 类实现了这个接口。



##### 4.Date-->String

~~~java
import java.util.*;
import java.text.*;
public class DateDemo {
   public static void main(String args[]) {
      Date dNow = new Date( );
      SimpleDateFormat ft = new SimpleDateFormat ("yyyy.MM.dd 'at' hh:mm:ss a zzz");
      System.out.println(ft.format(dNow));
   }
}
//yyyy 是完整的公元年，MM 是月份，dd 是日期，HH:mm:ss 是时、分、秒。
//注意:有的格式大写，有的格式小写，例如 MM 是月份，mm 是分；HH 是 24 小时制，而 hh 是 12 小时制。
~~~



##### 5.String-->Date

~~~java
import java.util.*;
import java.text.*;
public class DateDemo {
   public static void main(String args[]) {
      SimpleDateFormat ft = new SimpleDateFormat ("yyyy-MM-dd"); 
      String input = args.length == 0 ? "1818-11-11" : args[0]; 
      System.out.print(input + " Parses as "); 
      Date date; 
      try { 
          date = ft.parse(input); 
          System.out.println(date); 
      } catch (ParseException e) { 
          System.out.println("Unparseable using " + ft); 
      }
   }
}
~~~



##### 6.测量运行时间

~~~java
import java.util.*;
public class DiffDemo {
   public static void main(String args[]) {
      try {
         long start = System.currentTimeMillis( );
         System.out.println(new Date( ) + "\n");
         Thread.sleep(5*60*10);//线程睡眠
         System.out.println(new Date( ) + "\n");
         long end = System.currentTimeMillis( );
         long diff = end - start;
         System.out.println("Difference is : " + diff);
      } catch (Exception e) {
         System.out.println("Got an exception!");
      }
   }
}
~~~



##### 7.Calendar类

（1）创建一个代表系统当前日期的Calendar对象

```java
Calendar c = Calendar.getInstance();//默认是当前日期
```

（2）创建一个指定日期的Calendar对象

```java
//创建一个代表2009年6月12日的Calendar对象
Calendar c1 = Calendar.getInstance();
//public final void set(int year,int month,int date)
c1.set(2009, 6 - 1, 12);
```

（3）Calendar类对象字段类型

| 常量                  | 描述                           |
| --------------------- | ------------------------------ |
| Calendar.YEAR         | 年份                           |
| Calendar.MONTH        | 月份                           |
| Calendar.DATE         | 日期                           |
| Calendar.DAY_OF_MONTH | 日期，和上面的字段意义完全相同 |
| Calendar.HOUR         | 12小时制的小时                 |
| Calendar.HOUR_OF_DAY  | 24小时制的小时                 |
| Calendar.MINUTE       | 分钟                           |
| Calendar.SECOND       | 秒                             |
| Calendar.DAY_OF_WEEK  | 星期几                         |

4.实例

~~~java
import java.util.Calendar;
import java.util.Date;

public class DateDemo {
    public static void main(String[] args) {

        Date date=new Date();
        Calendar calendar=Calendar.getInstance();
        //获得当前日期
        System.out.println("当前时间："+date);
        //获得当前的年份、月份、日期
        System.out.println("当前年月日"+calendar.get(Calendar.YEAR)+"/"+(calendar.get(Calendar.MONTH)+1)+"/"+calendar.get(Calendar.DATE));
        //获得当前是星期几
        System.out.println("今天周:"+(calendar.get(Calendar.DAY_OF_WEEK)-1));
        //获得当前是该月的第几天
        System.out.println("当前是该月的第几天:"+calendar.get(Calendar.DAY_OF_MONTH));
        //获得当前的时间（时分秒）
        System.out.println("当前时分秒："+calendar.get(Calendar.HOUR)+":"+0+calendar.get(Calendar.MINUTE)+":"+calendar.get(Calendar.SECOND));
    }
}
~~~

