##### 1.下载JDK

```
http://www.oracle.com/technetwork/java/javase/downloads/index.html
```



##### 2.配置环境变量

|  变量名   |                            变量值                            |
| :-------: | :----------------------------------------------------------: |
| JAVA_HOME |                       E:\Java\jdk-1.8                        |
|   PATH    |             %JAVA_HOME%\bin;%JAVA_HOME%\jre\bin              |
| CLASSPATH | .;%JAVA_HOME%\lib\dt.jar;%JAVA_HOME%\lib\tools.jar; （.;%JAVA_HOME%\lib） //注意前面加'.' |



##### 3.测试JDK是否安装成功？

```cmd
javac //编译.java源文件      .java>>>>>.class
java  //执行.class字节码文件
java -version  //查看JDK版本
```



##### 4.HelloWorld

```java
public class HelloWorld{
    public static void main(String[] args){
        System.out.println("HelloWorld");
    }
}
```



##### 5.Java三剑客

```
JDK:Java Development Kit--Java开发工具包
JRE:Java runtime environment--Java运行环境
JVM:Java Virtual Machine--Java虚拟机
```



##### 6.JDK文件目录结构

|   **bin**   | JDK开发工具的可执行文件                                      |
| :---------: | :----------------------------------------------------------- |
|   **lib**   | 开发工具使用的归档包文件                                     |
| **include** | 包含C语言头文件,支持Java本地接口与Java虚拟机调试程序接口的本地编程技术 |
|   **jre**   | Java 运行时环境的根目录，包含Java虚拟机，运行时的类包和Java应用启动器，但不包含开发环境中的开发工具 |
|  **demo**   | 含有源代码的程序示例                                         |
| **src.zip** | Java所有核心类库的源代码                                     |

