##### IO流:

![img](http://www.runoob.com/wp-content/uploads/2013/12/iostream2xx.png)



##### 什么是流

> --流是一组有顺序的，有起点和终点的字节集合，是对数据传输的总称或抽象。
> 即数据在两设备间的传输称为流，流的本质是数据传输，根据数据传输特性
> 将流抽象为各种类，方便更直观的进行数据操作。



##### 流的作用

> ---可用通过java.io包下的Stream流来操作本地或者远程的文件;
>
> ---可以对文件[二进制文件或者字符文件]进行真正的读写操作;



##### 流的分类

- **按照传输单位进行划分**

（1）字节流-以字节为单位进行传输的[8位]-----二进制文件:音频,视频,图片

（2）字符流-以字符为单位进行传输[16位]-----字符文件:使用缓冲(Buffer)提高效率

（3）字节流和字符流的区别：
	 a. 读写单位不同：字节流以字节（8bit）为单位，  字符流以字符为单位，根据码表映射字符，一次可能读多个字节。
	 b. 处理对象不同：字节流能处理所有类型的数据（如图片、视频、音频等）  ，字符流只能处理字符类型的数据。
	 c. 执行原理不同：
		 字节流输出： 程序---->字节流(直接操作文件)---->文件（适合于一些二进制的对象，音频，视频，图片等）
		 字符流输出： 程序---->字符流---->缓存---->文件（适合于文本操作）

 设备上的数据无论是图片或者视频，文字，它们都以二进制存储的。
 二进制的最终都是以一个8位为数据单元进行体现，所以计算机中的最小数据单元就是字节。
 意味着，字节流可以处理设备上的所有数据，所以字节流一样可以处理字符数据。

（4）字符流简介：

* 字符流中的对象融合了编码表，也就是系统默认的编码表。我们的系统一般都是GBK编码。
* 字符流只用来处理文本数据，字节流用来处理媒体数据。
* 数据最常见的表现方式是文件，字符流用于操作文件的子类一般是FileReader和FileWriter。

（5）字符流读写注意事项：

* 写入文件后必须要用flush()刷新。
* 用完流后记得要关闭流
* 使用流对象要抛出IO异常
* 定义文件路径时，可以用“/”或者“\\”。
* 在创建一个文件时，如果目录下有同名文件将被覆盖。
* 在读取文件时，必须保证该文件已存在，否则出异常



- **按照流的方向进行划分**

输入流(InputStream)和读取(Reader):外部-->JVM

输出流(OutputStream)和写入(Writer):JVM--->外部

数据源可以有:外围设备(磁盘,键盘),内存,网络...

数据目的地:外围设备(磁盘,显示器),内存,网络...



- **按照流的功能进行划分**

节点流[基础流] - 具备真正读写的流;

节点流:FileInputStream;

过滤流[包装流,缓冲流] - 采取的是"装饰器"模式.以节点流为基础,在此基础之上对流进行"包装",从而提高读取效率.并且还可以构建出功能更加强大的流;

过滤流:BufferedInputStream/BufferedOutputStream  BufferedReader/PrintWriter[自带缓冲流]



##### 字节输入流和字节输出流

- 字节输入流的顶级抽象类---java.io.InputStream


> FileInputStream---文件字节输入流
>
> ObjectInputStream---操作对象类型的字节输入流
>
> ByteArrayInputStream---操作内存的字节输入流
>
> FilterInputStream---过滤流
>
> -\DataInputStream---操作基本数据类型的字节输入流
>
> -\BufferedInputStream---带缓存功能的字节输入流
>
> --常用的方法
>
> close();//Stream流是计算机中一中昂贵的资源,使用完毕之后需要及时释放;
> abstract int read();//单个字节继续输入
> int read(byte[] b);//从输入流中读取一定数量的字节，并将其存储在缓冲区数组 b 中。 

- 字节输出流的顶级抽象类---java.io.OutputStream


> FileOutputStream---文件字节输出流
>
> ObjectOutputStream---操作对象类型的字节输出流
>
> ByteArrayOutputStream---操作内存的字节输出流
>
> FilterOutputStream---过滤流
>
> -\DataOutputStream---操作基本数据类型的字节输出流
>
> -\BufferedOutputStream---带缓存功能的字节输出流



##### 字符读取流和字符写入流

- 字符读取流的顶级抽象类---java.io.Reader

- 字符写入流的顶级抽象类---java.io.Writer



##### 6.组合流(功能强大)

> (1).带缓存功能的文件字节输入流

~~~java
BufferedInputStream in  = new BufferedInputStream(new FileInputStream("路径"));
~~~

> (2).构建一个能够读取对象类型的文件字节输入流.

~~~java
ObjectInputStream in = new ObjectInputStream(new FileInputStream("路径"));
~~~

> (3).构建一个能够读取基本类型的文件字节输入流.

~~~java
DataInputStream in = new DataInputStream(new FileInputStream("路径"));
~~~

> (4).构建一个既能读取对象类型,又自带缓冲功能的文件字节输入流.

~~~java
ObjectInputStream in = new ObjectInputStream(new BuffferedInputStream(new FileInputStream("路径")));  
~~~



##### 7.操作步骤

实现文件的拷贝功能[输入/输出]

> (1).选择流 : 
>
> ~~~java
> FileInputStream/FileOutputStream
> ~~~
>
> (2).确定源头和目标 :
>
> ~~~java
>  FileInputStream(String pathname)和FileOutputStream(String pathname[,boolean append])//false或者不写第二个参数都是代表覆盖写.
> ~~~
>
> (3).循环读取和写入:
>
> (4).关闭流:



##### 8.为什么会出现乱码？

写入的编码与读取的编码不一致。



##### 9.实例

> (1).使用字节流拷贝文件

~~~java
import java.io.*;

/**
 * 使用IO流拷贝文件
 */
public class IoStreamDemo {
    public static void main(String[] args) throws FileNotFoundException {
        copy4("C:\\Test\\hello.txt","C:\\Test\\hello_1.txt");
    }
    //----------------------版本一----------------------
    public static void copy1(String src,String target){
        //1.选择流 - 文件字节输入流和文件字节输出流.
        //2.确定源头和目标 - 构建出输入流和输出流的对象.
        InputStream in=null;
        OutputStream out=null;
        try {
            in=new FileInputStream(src);
            out=new FileOutputStream(target);
            //3.循环读取和写入
            while(true){
                int len = in.read();//单个字节进行读取,从输入流中读取下一个字节,如果已经到达文件的末尾,则返回-1
                if(len==-1)
                    break;
                //写入
                out.write(len);
            }
        } catch (FileNotFoundException e) {
            e.printStackTrace();
        }catch (IOException e) {
            e.printStackTrace();
        }finally {
            //判断-4.关闭流
            if(in!=null) {
                try {
                    in.close();
                } catch (IOException e) {
                    e.printStackTrace();
                }
            }
            if(out!=null) {
                try {
                    out.close();
                } catch (IOException e) {
                    e.printStackTrace();
                }
            }
        }

    }

    /**
     * JDK7.0后提供了语法糖的写法
     * 程序运行结束之后,会有JVM自动释放资源对象
     * try(申请的资源对象1;申请的资源对象2){
     *
     * }catch(Exception e){
     *
     * }
     * @param src
     * @param target
     */
    //----------------------版本二--------------------
    public static void copy2(String src,String target){
        try(InputStream in=new FileInputStream(src);OutputStream out=new FileOutputStream(target)){
            while(true){
                int len=in.read();
                if(len==-1) {
                    break;
                }
                out.write(len);
            }
            System.out.println("拷贝成功!");
        } catch (FileNotFoundException e) {
            e.printStackTrace();
        } catch (IOException e) {
            e.printStackTrace();
        }
    }
    //----------------------版本三---------------------
    public static void copy3(String src,String target){
        try(InputStream in=new FileInputStream(src);OutputStream out=new FileOutputStream(target))
        {
            byte[] buf=new byte[3*1024];
            int len=-1;
            while((len=in.read(buf))!=-1){
                    out.write(buf,0,len);
            }
            System.out.println("拷贝成功!");
        } catch (FileNotFoundException e1) {
            e1.printStackTrace();
        } catch (IOException e1) {
            e1.printStackTrace();
        }
    }

    /**
     * 最终版本
     * 构建带缓冲功能的字节文件输入流
     * @param src
     * @param target
     */
    //------------------------版本四-------------------
    public static void copy4(String src,String target){
        try(BufferedInputStream in=new BufferedInputStream(new FileInputStream(src));
            BufferedOutputStream out=new BufferedOutputStream(new FileOutputStream(target))){
            //定义一个字节数组 - 根据实际情况进行指定大小的.
            byte[] buf=new byte[3*1024];
            int len=-1;
            while((len=in.read(buf))!=-1){
                out.write(buf,0,len);
            }
            System.out.println("拷贝成功!");
        } catch (FileNotFoundException e) {
            e.printStackTrace();
        } catch (IOException e) {
            e.printStackTrace();
        }
    }
}
~~~



(2).

> 将若干学生信息写入到"excel文件"
>
> 从excel文件中将学员信息读取到List\<Student>
>
> 将若干学生信息写入到"txt文件"
>
>  从txt文件中将学员信息读取到List\<Student>

~~~java
import jxl.Sheet;
import jxl.Workbook;
import jxl.write.Label;
import jxl.write.WritableSheet;
import jxl.write.WritableWorkbook;
import jxl.write.WriteException;
import java.io.*;
import java.util.ArrayList;
import java.util.List;

public class FileUtil {
    private static final char fieldSperater='\t';
    public static void main(String[] args) {

        FileUtil student = new FileUtil();
        List<Student> list = new ArrayList<>();
        Student student1 = new Student("1001", "汪应昌1", "男");
        Student student2 = new Student("1002", "汪应昌2", "男");
        Student student3 = new Student("1003", "汪应昌3", "男");
        Student student4 = new Student("1004", "汪应昌4", "女");
        list.add(student1);
        list.add(student2);
        list.add(student3);
        list.add(student4);

        //通过excel导入导出
        student.excelOut(list);//导出
        List<Student> students = student.excelIn();//导入
        for (Student s : students) {
            System.out.println(s);
        }

        System.out.println("------------------------------------------------");

        //通过txt导入导出
        student.txtOut(list);//导出
        List<Student> students1=student.txtIn();//导入
        for(Student s:students){
            System.out.println(s);
        }

    }


    /**
     * 1. 将若干学生信息写入到"excel文件" --- 导出
     * @param list 学生信息集合List
     */
    public void excelOut(List<Student> list) {
        //创建一个excel对象
        WritableWorkbook book = null;
        try {
            book = Workbook.createWorkbook(new File("E://student.xls"));
            //通过excel对象创建一个选项卡对象
            WritableSheet sheet = book.createSheet("sheet1", 0);
            //创建一个单元格对象 列 行 值--Label label=new Label(0,2,"test");

            Label label00=new Label(0,0,"学号");
            Label label10=new Label(1,0,"姓名");
            Label label20=new Label(2,0,"性别");
            sheet.addCell(label00);
            sheet.addCell(label10);
            sheet.addCell(label20);

            for (int i = 1; i <= list.size(); i++) {
                Student student = list.get(i-1);
                Label label1 = new Label(0, i, String.valueOf(student.getStuId()));
                Label label2 = new Label(1, i, student.getStuName());
                Label label3 = new Label(2, i, student.getStuSex());
                // 将创建好的单元格对象放入sheet中

                sheet.addCell(label1);
                sheet.addCell(label2);
                sheet.addCell(label3);
            }
            //写入目标路径
            book.write();
        } catch (Exception e) {
            e.printStackTrace();
        } finally {
            try {
                book.close();
            } catch (IOException e) {
                e.printStackTrace();
            } catch (WriteException e) {
                e.printStackTrace();
            }
        }
    }

    /**
     * /2. 从Excel中将学员信息读取到List<Student>  --- 导入
     * @return list学生信息集合
     */
    public List<Student> excelIn() {

        List<Student> list = new ArrayList<>();
        System.out.println("学号"+"\t"+"姓名"+"\t"+"性别");
        Workbook workbook = null;
        try {
            // 获取Excel对象
            workbook = Workbook.getWorkbook(new File("E://student.xls"));
            //获取Excel对象中第一个sheet
            Sheet sheet = workbook.getSheet(0);
            //循环选项卡中的值

            for (int i = 1; i <sheet.getRows(); i++) {
                Student student = new Student();
                //获取单元格对象
                //获取单元格的值,并设置到对象中
                student.setStuId(sheet.getCell(0, i).getContents());// student.setStuId(Integer.valueOf(cell.getContents()));
                student.setStuName(sheet.getCell(1, i).getContents());
                student.setStuSex(sheet.getCell(2, i).getContents());
                list.add(student);
            }
        } catch (Exception e) {
            e.printStackTrace();
        } finally {
            workbook.close();
        }
        return list;
    }

    /**
     * 3. 将若干学生信息写入到"Java班级学员信息.txt"--- 导出
     * @param list 学生信息的集合
     */
    public void txtOut(List<Student> list) {
        try (BufferedWriter bw = new BufferedWriter(new OutputStreamWriter(new FileOutputStream("E:\\student.txt")))) {
            String title = "学号"+fieldSperater+"姓名"+fieldSperater+"性别"+"\r\n";
            bw.write(title);
            for (Student stu : list) {
                String stuInfo = stu.getStuId() + fieldSperater + stu.getStuName() + fieldSperater + stu.getStuSex() + "\r\n";
                bw.write(stuInfo);
            }
            bw.flush();//刷新缓冲
        } catch (FileNotFoundException e) {
            e.printStackTrace();
        } catch (IOException e) {
            e.printStackTrace();
        }
    }

    /**
     * 4. 从txt中将学员信息读取到List<Student>--- 导入
     * @return
     */
    public List<Student> txtIn() {
        List<Student> list=new ArrayList<>();//存放学生信息集合
        try(BufferedReader br=new BufferedReader(new InputStreamReader(new FileInputStream("E:\\student.txt"))))
        {
            Student stu=new Student();//创建临时学生对象
            boolean flag=true;
            while(flag){
                String str=br.readLine();//获取一行记录数据
                if(str!=null){
                    String[] arr=str.split("\\s+");//***数据按空格分割
                    stu.setStuId(arr[0]);
                    stu.setStuName(arr[1]);
                    stu.setStuSex(arr[2]);
                    list.add(stu);
                }else{
                    flag=false;
                }
            }
        } catch (FileNotFoundException e) {
            e.printStackTrace();
        } catch (IOException e) {
            e.printStackTrace();
        }
        return list;
    }
}
~~~

