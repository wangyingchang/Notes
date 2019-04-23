**API-----java.lang.Math**



##### 1.Number & Math类常用方法

| 序号 | 方法与描述                                                   |
| ---- | ------------------------------------------------------------ |
| 1    | [xxxValue()](http://www.runoob.com/java/number-xxxvalue.html) 将 Number 对象转换为xxx数据类型的值并返回。 |
| 2    | [compareTo()](http://www.runoob.com/java/number-compareto.html) 将number对象与参数比较。 |
| 3    | [equals()](http://www.runoob.com/java/number-equals.html) 判断number对象是否与参数相等。 |
| 4    | [valueOf()](http://www.runoob.com/java/number-valueof.html) 返回一个 Number 对象指定的内置数据类型 |
| 5    | [toString()](http://www.runoob.com/java/number-tostring.html) 以字符串形式返回值。 |
| 6    | [parseInt()](http://www.runoob.com/java/number-parseInt.html) 将字符串解析为int类型。 |
| 7    | [abs()](http://www.runoob.com/java/number-abs.html) 返回参数的绝对值。 |
| 8    | [ceil()](http://www.runoob.com/java/number-ceil.html) 返回大于等于( >= )给定参数的的最小整数。 |
| 9    | [floor()](http://www.runoob.com/java/number-floor.html) 返回小于等于（<=）给定参数的最大整数 。 |
| 10   | [rint()](http://www.runoob.com/java/number-rint.html) 返回与参数最接近的整数。返回类型为double。 |
| 11   | [round()](http://www.runoob.com/java/number-round.html) 它表示**四舍五入**，算法为 Math.floor(x+0.5)，即将原来的数字加上 0.5 后再向下取整，所以，Math.round(11.5) 的结果为12，Math.round(-11.5) 的结果为-11。 |
| 12   | [min()](http://www.runoob.com/java/number-min.html) 返回两个参数中的最小值。 |
| 13   | [max()](http://www.runoob.com/java/number-max.html) 返回两个参数中的最大值。 |
| 14   | [exp()](http://www.runoob.com/java/number-exp.html) 返回自然数底数e的参数次方。 |
| 15   | [log()](http://www.runoob.com/java/number-log.html) 返回参数的自然数底数的对数值。 |
| 16   | [pow()](http://www.runoob.com/java/number-pow.html) 返回第一个参数的第二个参数次方。 |
| 17   | [sqrt()](http://www.runoob.com/java/number-sqrt.html) 求参数的算术平方根。 |
| 18   | [sin()](http://www.runoob.com/java/number-sin.html) 求指定double类型参数的正弦值。 |
| 19   | [cos()](http://www.runoob.com/java/number-cos.html) 求指定double类型参数的余弦值。 |
| 20   | [tan()](http://www.runoob.com/java/number-tan.html) 求指定double类型参数的正切值。 |
| 21   | [asin()](http://www.runoob.com/java/number-asin.html) 求指定double类型参数的反正弦值。 |
| 22   | [acos()](http://www.runoob.com/java/number-acos.html) 求指定double类型参数的反余弦值。 |
| 23   | [atan()](http://www.runoob.com/java/number-atan.html) 求指定double类型参数的反正切值。 |
| 24   | [atan2()](http://www.runoob.com/java/number-atan2.html) 将笛卡尔坐标转换为极坐标，并返回极坐标的角度值。 |
| 25   | [toDegrees()](http://www.runoob.com/java/number-todegrees.html) 将参数转化为角度。 |
| 26   | [toRadians()](http://www.runoob.com/java/number-toradians.html) 将角度转换为弧度。 |
| 27   | [random()](http://www.runoob.com/java/number-random.html) 返回一个随机数。 |



##### 2.Math 的 floor,round 和 ceil 方法实例比较

| 参数 | Math.floor | Math.round  | Math.ceil |
| ---- | ---------- | ----------- | --------- |
| 1.4  | 1          | 1           | 2         |
| 1.5  | 1          | 2           | 2         |
| 1.6  | 1          | 2           | 2         |
| -1.4 | -2         | -1          | -1        |
| -1.5 | -2         | -1 （注意） | -1        |
| -1.6 | -2         | -2          | -1        |

