##### 1.基本数据类型



![](https://i.imgur.com/3NeJ7XT.png)

byte:【-2^7,2^7-1】

short:【-2^15,2^15-1】

int:【-2^31,2^31-1】

long:【-2^63,2^31-1】



##### 2.引用数据类型

- 在Java中，引用类型的变量非常类似于C/C++的指针。引用类型指向一个对象，指向对象的变量是引用变量。这些变量在声明时被指定为一个特定的类型，比如 Employee、Puppy 等。变量一旦声明后，类型就不能被改变了。
- 对象、数组、String都是引用数据类型。
- 所有引用类型的默认值都是null。
- 一个引用变量可以用来引用任何与之兼容的类型。
- 例子：Site site = new Site("Runoob")。



##### 3.自动类型转换

数据类型的相互转换： 

- 正向的过程: 从低字节向高字节可以自动转换  （Java中的自动类型提升 ）  

  ```
  低  ------------------------------------>  高
  byte-> short-> int-> long-> float-> double      
  特殊情况：char <-> int  （相互转换）   
  ```

- 反向的过程: 从高字节向低字节可以强制转换.

```
例如: int a = (int) 4.562;   
```

 注意: 反向转换将会丢失精度



数据类型转换必须满足如下规则：

- 不能对boolean类型进行类型转换。

- 不能把对象类型转换成不相关类的对象。

-  在把容量大的类型转换为容量小的类型时必须使用强制类型转换。

- 转换过程中可能导致溢出或损失精度，例如：

  ```
  int i =128;   
  byte b = (byte)i;
  ```

  因为 byte 类型是 8 位，最大值为127，所以当 int 强制转换为 byte 类型时，值 128 时候就会导致溢出。

- 浮点数到整数的转换是通过舍弃小数得到，而不是四舍五入，例如：

  ```
  (int)23.7 == 23;        
  (int)-45.89f == -45
  ```

