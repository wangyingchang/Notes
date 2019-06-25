##### **1.数组与集合**

（1）数组特征：
            (1)、数据类型一致；
            (2)、空间是连续；
            (3)、下标位置从0开始；
            (4)、长度固定，数组的length属性；
            (5)、通过下标表示数组中元素的个数：index。
			int[] i = new int[3];
			int[] j = {1,2,3};
（2）集合特征： 
            (1)、集合中可以任何数据类型(Object)数据；
            (2)、自动扩容(不固定长度)；
            (3)、size() 返回集合中元素的个数；



##### **2.集合框架**

![img](http://www.runoob.com/wp-content/uploads/2014/01/2243690-9cd9c896e0d512ed.gif)

##### **3.Collection接口：**

Collection是保存单值集合的最大父接口
定义格式：
public interface Collection<E> extends Iterable<E>
所有的类集操作都存放在java.util包中。
在一般的开发中，往往很少去使用Collection接口直接去开发，基本是使用
其子接口，子接口主要有：List,Set,Queue,SortedSet
Collection子接口
List接口：可以存放重复的内容
Set接口：不能存放重复的内容，所有的重复内容都是靠hashCode()、equals()和compareTO()两种方法区分的。
Queue:队列接口。
SortedSet接口：可以对集合中的数据进行排序。

##### 4.List接口

常用实现子类：**ArrayList**<E>、 **LinkedList<**E>；

存储元素可以重复；

**ArrayList 本质是数组** 

- 频繁的添加操作：可能会造成扩容，内存浪费与大量元素复制移位，随着数据量增多，时空复杂度会增大；(缺点)

- 频繁的删除操作：可能会出现大量元素的移位；（缺点）

- 频繁的取元素操作：能直接根据数组下标定位元素，因为数据在数组中的物理地址是连续的；（优点）

- 【**所以：ArrayList 适用于元素的随机访问**】

- eg
~~~
        List<String> list=new ArrayList<String>();
        list.add("hello");
        list.add("world");
        list.add("haha");

        // 第一种遍历 foreach
        for(String str: list){
            System.out.println(str);
        }
        // 第二种遍历 链表
        String[] strArray=new String[list.size()];
        list.toArray(strArray);
        for(String str:strArray){
            System.out.println(str);
        }
        // 第三种遍历 迭代器
        Iterator iterator=list.iterator();
        while (iterator.hasNext()){
            System.out.println(iterator.next());
        }
~~~

**LinkedList 本质是链表**

- 频繁的添加操作：只需要一个元素内存消耗；（优点）
- 频繁的删除操作：只需要元素指针重新连接；（优点）
- 频繁的取元素操作：需要遍历整个链表，因为链表的物理地址是不连续的；（缺点）
- 【**所以：LinkedList适用于元素的大量添加与删除**】






##### 5.Set接口

- 常用的实现子类：	HashSet\<E>、TreeSet\<E>；
- 存储不重复（唯一）的元素的集合；

**HashSet: 散列存放**

- 唯一性： 依赖于重写**equals**、**hashcode**方法
- 底层原理通过**HashMap的key**实现

（1）HashSet 示例1

```Java
 	    Set<Integer> intSet = new HashSet<>();

        intSet.add(new Integer(10));

        intSet.add(new Integer(10));

	 // set中只存放了一个10.【因为 Integer 实现了重写equals、hashcode方法】

```

（2）HashSet 示例2

```
	Set<Product> proSet = new HashSet<Product>();

	Product p1 = new Product(1004,"东北烤串",60,25);

        Product p2 = new Product(1004,"东北烤串",60,25);

        proSet.add(p1);

        proSet.add(p2);
```
//为什么要重写hashcode()和equals()?
set中存放了两个product, 但是在现实中，则认为p1,p2是同一个商品，在集合中只需要存放一次；所以需要重写Product类中的equals、hashcode方法。
因为默认的equals方法是Object的方法，比较的是内存地址；而默认的hashcode方法返回的是对象的内存地址转换成的一个整数，实际上指的的也是内存(两个方法可以理解为比较的都是内存地址),这在实际开发的过程中在HashMap或者HashSet里如果不重写的hashcode和equals方法的话会导致我们存对象的时候，把对象存进去了，取的时候却取不到想要的对象，这时候就需要重写这两个方法了，一般可以根据业务的需求来重写；
总结：
1.重写hashcode是为了保证相同的对象会有相同的hashcode；
2.重写equals是为了保证在发生冲突的情况下取得到Entry对象（也可以理解是key或是元素）；

**TreeSet: 有序存放**

- 元素不重复的保证 :①自然排序；②比较器排序;
- 唯一性：依赖于重写**compareTo\<E>**方法,根据比较的返回值是否为0
- 底层原理通过**TreeMap的key**实现

（1）new TreeSet(）--自然顺序

```java
	class E implements Comparable<E>{//实现Comparable<E>接口
 			@Override//重写
            public int compareTo(E o1  
				//实现自然顺序
            }
	}

    Set<E> set1 = new TreeSet();
    Set<E> set2 = new TreeSet();
                       
    // 底层实现：
	TreeMap.put(e1,..) ---Comparable c = (Comparable)e1 ---- 若第一次添加，不比较，直接添加
	TreeMap.put(e2,..) ---Comparable c = (Comparable)e2 ----  e2.compareTo(e1),
     return (0 或 -1 或 1)
                                 
	//【返回 0 表示相同元素，不能添加，实现去重】

```

（2）new TreeSet --自定义排序规则

```java
Set<E> set4 =  new TreeSet<E>( new Comparator<E>(){
        @Override//重写
        public int compareTo(E o1, E o2)  
			//实现自定义排序规则B,仅仅使用于set4
        }
});
 compare方法返回 (0 或 -1 或 1), 
【返回 0 表示相同元素，不能添加，实现去重】
【所以，自然顺序必须要实现Comparable接口，否则会有类型转换异常  CLassCastException】
```

（3）TreeSet示例1：自然顺序

```java
	class Product implements  Comparable<Product>{ //实现接口Comparable
		  // 按照价格的升序排序，若价格相同，则按照编号升序排序，若编号相同，业务中认为是相同商品
	    @Override
	    public int compareTo(Product o) {
	        if(this.proPrice != o.proPrice)
	            return  this.proPrice < o.proPrice ? -1 : 1;
	        else{
	            if(this.proId == o.proId)
	                return 0;// 【不添加，去重】
	            return  this.proId < o.proId ? -1 : 1;
	        }	
	    }
	}
```

（4）TreeSet示例2：自定义排序规则

```java
    // 商品按照名称字母顺序排序，若名称相同，按照编号先后顺序       
    class Product {
    Set<Product> set2 =  new TreeSet<Product>( new Comparator<Product>(){ //匿名内部类
        @Override
        public int compare(Product o1, Product o2) {
            if(o1.getProName().compareTo(o2.getProName())!=0)
                return o1.getProName().compareTo(o2.getProName());
            else{
                if(o1.getProId() == o2.getProId())
                    return 0;// 【不添加，去重】
                return o1.getProId()  < o2.getProId() ? -1 : 1;
            }
        }
    });
```





##### 6.Map接口

- 常用的实现子类：	HashMap<E>、TreeMap\<E>、Hashtable\<E>；
- 存储不重复（唯一）的元素的集合;



**HashMap 键值对 散列存放**

  Key 的唯一性依赖于 重写**equals() hashcode()**方法

**TreeMap** 键值对 **有序存放**

  Key 的唯一性依赖于 **自然顺序** 或者 **自定义排序规则**（与TreeSet实现相似）

**Hashtable** 与HashMap一致

- HashMap 适用于单线程，非线程安全；<key，value>可以为null 
- Hashtable适用于多线程，线程安全；<key,value>不可以为null

```java
  Map<String, Integer> map = new HashMap<>();
   map.put("贵州", 1000);
   map.put("江苏", 2000);
   map.put("北京", 3000);
   map.put("广东", 3300);
   map.put("河北", 6600);
```

这种一一对应的数据存储，需要使用Map<键，值>存储。

Map<Key，Value>特点：

```
key:键，唯一性（null可以插入一次）
 
value :值
```
核心方法：

put(key,value)：注意返回值
keySet()：注意返回的Set
entrySet()： map将每一个键值对封装成 Entry对象

参考Map对key-value底层的封装图

```java
    Set<Map.Entry<String,Integer>> entrySet=map.entrySet();
    Iterator<Map.Entry<String,Integer>> iterator=entrySet.iterator();
    while(iterator.hasNext()){
        Map.Entry<String,Integer> entry=iterator.next();
        String key=entry.getKey();
        Integer value=entry.getValue();
        if(value>3000){
            System.out.println(key);
        }
    }
    //forEach遍历
    Set<Map.Entry<String,Integer>> entrySet1=map.entrySet();
    for(Map.Entry<String,Integer> s:entrySet1){
        String key=s.getKey();
        Integer value=s.getValue();
        if(value>3000){
            System.out.println(key);
        }
    }
```
```
        Map<String,String> map=new HashMap<>();
        map.put("1","v1");
        map.put("2","v2");
        map.put("3","v3");

        // 第一种遍历
        for(String key:map.keySet()){
            System.out.println("key="+ key +",value="+ map.get(key));
        }
        // 第二种遍历
        Iterator<Map.Entry<String,String>> iterator=map.entrySet().iterator();
        while (iterator.hasNext()){
            Map.Entry<String,String> entry=iterator.next();
            System.out.println("key="+ entry.getKey() +",value="+entry.getValue());
        }
        // 第三种遍历
        for(Map.Entry<String,String> entry:map.entrySet()){
            System.out.println("key="+entry.getKey()+",value="+ entry.getValue());
        }
        // 第四种遍历
        for(String v:map.values()){
            System.out.println("value="+ v);
        }
```



##### **7.迭代器**

```java

Set<Product> set=new HashSet<>();//集合
Iterator<Product> iterator=set.iterator();//集合获取迭代器
while(iterator.hasNext()){//判断指针下一个是否存在元素
    System.out.println(iterator.next());//指针指向下一个元素
}
//底层原理
```

