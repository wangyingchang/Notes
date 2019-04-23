**API-----java.io.File**



##### **1.概要**

> 计算机中的数据是通过串行的方式进行输出和输入的,File类是java.io包中唯一代表磁盘文件本省的对象;
>
> File类定义了一些与平台无关的方法来操作文件,可以通过调用File类中的方法,实现创建,删除,重命名文件等操作;
>
> File类的对象主要用来获取文件本身的一些信息,如文件所在的目录，文件的长度、文件读写权限等,数据流可以将数据写入到文件中，文件也是数据流常用的数据媒体；
>
> Java核心库java.io包中的.这个包中提供了比较全面的io流的功能,包括文件的读写,标准设备的输出等.



##### **2.构造方法**

(1).  **File(String pathname)**:将给定路径名字字符串转换为抽象路径名来创建一个新File实例；

~~~java
//---pathname指路径名称（包含文件名）
new File("d:/hello.txt")；
~~~

(2).  **File(String parent,String child)**:根据定义的父路径和子路径字符串（包含文件名）创建一个新的File对象；

~~~java
//parent:父路径字符串。 "D:/" 或 "D:/doc"
//child:子路径字符串。  "hello.txt"
new File("D:/","hello.txt");
~~~

(3).**File(File f,String child)**:根据parent抽象路径名和child路径名字符串创建一个新File实例；

~~~java
//f：父路径对象。  "D:/doc/"
//child：子路径字符串。"hello.txt"
~~~

(4).**File(URI uri)**:通过将给定的 file: URI转换为抽象路径名来创建新的 File实例。 



##### **3.常用方法**

> - 创建文件:boolean createNewFile();//如果文件已经存在,则创建失败.

> - 判断文件是否存在:boolean exists();

> - 创建单层次的目录:boolean mkdir();
>
>   [new File(String pathname)中的pathname的结构.比如:/xxx就是表示单层次,如果是/xxx/yyy]

> - 创建深层次的目录:boolean mkdirs();

> - 获取文件属性信息
>
> > 直接输出File对象 - 已经重写了toString方法,输出的是该file对象的映射的那个文件或者目录的路径.
> >
> > String getName();//获取file的名称
> >
> > String getParent();//获取file的父目录路径
> >
> > String getPath();将此抽象路径名转换为一个路径名字符串。 
> >
> > String getAbsolutePath() ;//获取绝对路径
> >
> > long length();//获取文件的长度.

> - 删除file:boolean delete();//空目录,权限,正在被使用的文件夹不能删

> - 列举某个目录下的第一级文件和文件夹:fileFile[] listFiles();//

> - 判断file是否为文件:boolean isFile();//

> - 判断file是否为目录:boolean isDirectory();

> - 返回文件数组:File[] listFiles(FilenameFilter filter)  



##### 4.实例

> (1).基本方法

~~~java
import java.io.File;
import java.io.IOException;

public class FileDemo {
    public static void main(String[] args) throws IOException {
        //（1）创建目录(文件夹)
        File file=new File("C:\\a\\b");
        // (2) 判断文件是否存在
        if (!file.exists()) {
            // 2-1创建单个文件夹
            if (file.mkdir()) {
                System.out.println(file + "目录创建成功!");
                // 2-2 创建多个文件夹(不需要父目录)
            } else if (file.mkdirs()) {
                System.out.println(file + "目录创建成功!");
            } else {
                System.out.println("目录创建文件失败!");
            }
        } else {
            System.out.println("目录已经存在!");
        }
        //（3）创建文件
        File file1=new File("C:\\a\\b\\hello.txt");
        try {
            file1.createNewFile();//向当前文件夹添加文件,若没有该文件夹则添加失败.
        } catch (IOException e) {
            e.printStackTrace();
        }
        //（4）获得名字
        System.out.println("(4).文件夹名:"+file.getName()+"  文件名:"+file1.getName());
        //（5）获得路径
        System.out.println("(5).文件夹路径:"+file.getPath()+"  文件路径:"+file1.getPath()+"  文件绝对路径:"+file1.getAbsoluteFile());
        //（6）获得父文件夹
        System.out.println("(6).文件夹上一级:"+file.getParent()+"  文件上一级:"+file1.getParent());
        //（7）获得文件的大小
        System.out.println("(7).文件夹大小:"+file.length()+"  文件大小:"+file1.length());
        //（8）删除文件夹，文件
        if(file.exists()){
            //只能删除空的目录...
            if(file.delete()){//如果成功删除,返回true,否则返回false
                System.out.println("(8)."+file+"文件成功被删除!");
            }else{
                System.out.println("(8).文件删除失败.权限,正在被使用.非空目录...");
            }
        }else{
            System.out.println("file不存在!");
        }
        //（9）判断一个File对象是不是 文件夹，文件？
        System.out.println("(8).该文件夹是文件夹?:"+file.isDirectory()+"  是文件?:"+file.isFile()+"  该文件是文件夹?:"+file1.isDirectory()+"  该文件是文件?:"+file1.isFile());
        //（10）获得文件夹下所有的子文件(当前文件夹)
        File f=new File("C://Test");
        File[] listFile=f.listFiles();//返回一个抽象路径名数组，表示由该抽象路径名表示的目录中的文件
        System.out.println("(9).该目录下对象个数："+listFile.length);
        for(int i=0;i<listFile.length;i++){//获取所有子文件夹
            if(listFile[i].isDirectory()){
                System.out.println("文件夹："+listFile[i]);
            }
            if(listFile[i].isFile()){
                System.out.println("文件:"+listFile[i]);
            }
        }
    }
         // (11) 查询后缀为xx的文件
         // (12) 获取一个目录下的所有文件夹和文件，包括子文件夹和子文件
         // (13) 查找目录下指定文件名的文件
    
}
~~~

> (11).查询后缀为xx的文件

~~~java
        File f = new File("E:\\Test");
        if(file.exists()){
            //判断 该file是否为目录
            if(file.isDirectory()){//如果是目录,则返回true
                //将file的第一级的file实例存入到一个File[]数组中.
                File[] files = file.listFiles(new FilenameFilter() {
                    //底层采取的就是策略模式.
                    @Override
                    public boolean accept(File dir, String name) {
                        //如果满足则包含
                        if(name.endsWith("txt"))//查询后缀为txt的文件
                            return true;
                        return false;
                    }
                });
                for (File f : files) {
                    System.out.println(f.getName());
                }
            }else{
                System.out.println("file不是有效的目录");
            }
        }else{
            System.out.println("file不存在!");
        }
~~~

> (12).获取一个目录下的所有文件夹和文件，包括子文件夹和子文件

~~~java
import java.io.File;

/**
 * 获取一个目录下的所有文件夹和文件，包括子文件夹和子文件
 * 并将文件夹和文件名称打印在控制台上面。并且要显示文件目录的层级
 * 注：运用了递归的算法
*/
public class FileDemo2 {
    public static void main(String[] args) {
        File f=new File("C://Test");
        getAllFiles(f,0);//0表示最顶层
    }
    /**
     * 获得文件夹下所有的子文件（包括所有的子文件夹）
     * @param dir 路径
     * @param level 层
     */
    public static void getAllFiles(File dir, int level){
        System.out.println(getLevel(level)+dir.getName());
        level++;
        File[] files=dir.listFiles();
        for(File f:files){
            if(f.isDirectory()){//是文件夹
                //调用递归
                getAllFiles(f,level);
            }else{
                System.out.println(getLevel(level)+f);
            }
        }
    }
    //获取层级的方法
    public static String getLevel(int level){
        StringBuilder sb=new StringBuilder();
        for(int i=0;i<level;i++){
            sb.append("|--");
        }
        return sb.toString();
    }
}
~~~

> (13).查找目录下指定文件名的文件

~~~java
import java.io.File;
import java.io.FileFilter;
import java.util.ArrayList;
import java.util.List;

//查找目录下指定文件名的文件
public class FileDemo3 {
    static int countFiles=0;//声明统计文件个数的变量
    static int countFolders=0;//声明统计文件夹的变量

    public static void main(String[] args) {
        File folder=new File("C://test");//默认目录
        String keyword="123";
        if(!folder.exists()){//文件夹不存在
            System.out.println("目录不存在:"+folder.getAbsolutePath());
            return;
        }
        File[] result=searchFile(folder,keyword);//调用方法获得文件数组
        System.out.println("在"+folder+"以及所有子文件时查找对象"+keyword);
        System.out.println("查找了"+countFolders+"个文件夹,"+countFiles+"个文件,共找到"+result.length+"个符合条件的文件:");
        for(File f:result){
            File file=f;
            System.out.println(file.getAbsoluteFile()+" ");
        }
    }

    public static File[] searchFile(File folder,final String keyword){//递归查找包含关键字的文件
        File[] subFolders=folder.listFiles(new FileFilter() {//匿名内部类获得文件
            @Override
            public boolean accept(File pathname) {
                if(pathname.isFile())//如果是文件
                    countFiles++;
                else
                    //如果是目录
                    countFolders++;
                // 目录或文件包含关键字
                if(pathname.isDirectory()||(pathname.isFile() && pathname.getName().toLowerCase().contains(keyword.toLowerCase())))
                    return true;
                return false;
            }
        });
        List<File> result=new ArrayList<>();//声明一个集合
        for(int i=0;i<subFolders.length;i++){
            if(subFolders[i].isFile()){//如果是文件则将文件添加到结果列表中
                result.add(subFolders[i]);
            }else{//如果是文件夹，则递归调用本方法，然后把所有的文件加到结果列表中
                File[] foldResult=searchFile(subFolders[i],keyword);
                for(int j=0;j<foldResult.length;j++){// 循环显示文件
                    result.add(foldResult[j]);// 文件保存到集合中
                }
            }
        }
        File[] files=new File[result.size()];// 声明文件数组，长度为集合的长度
        result.toArray(files);//集合数组化
        return files;
    }
}
~~~

