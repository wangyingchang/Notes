API---java.lang.reflect



##### **1.Class类与Java反射**

所有Java类都是继承了Object类,在Object类中定义了一个getClass()方法，该方法返回一个类型为Class的对象,

~~~java
Class text=textField.getClass();
~~~

~~~java
public class ReflectDemo {
    public static void main(String[] args) throws IllegalAccessException, InvocationTargetException, InstantiationException, NoSuchMethodException {
        Class clazz=com.java.course.day12.Student.class;
        getAllFiled(clazz);
        getAllConstructor(clazz);
        getAllMethod(clazz);
    }
~~~



##### 2.通过反射访问构造方法

~~~java

    public static void getAllConstructor(Class clazz) throws IllegalAccessException, InvocationTargetException, InstantiationException {
        //获得所有构造函数数组对象-包括私有的
        Constructor<Student>[] constructors=clazz.getDeclaredConstructors();
        for(Constructor<Student> c:constructors){
            String constrName=c.getName();//获取构造函数名
            System.out.println("构造函数名："+constrName);

            int modifiers=c.getModifiers();//获得构造函数的修饰符
            System.out.println("构造函数修饰符："+modifiers);

            Class[] typeClass=c.getParameterTypes();//获得构造函数参数列表的类型
            if(typeClass.length==0){//无参构造函数
                Student s=c.newInstance(null);//Student s1=new Student();
            }
            if(typeClass.length==2){
                Student s=c.newInstance("tom",22);//Student s2=new Student("tom",22);
                System.out.println("创建的学生的姓名："+s.getName()+"年龄："+s.getAge());
            }
            for(Class type:typeClass){
                System.out.print("参数列表类型："+type+"  ");
            }
            System.out.println();
            System.out.println("------------------------------------");
        }
    }

~~~



##### 3.通过反射访问成员变量

~~~java

    public static void getAllFiled(Class clazz) throws IllegalAccessException {
        //获取所有成员变量数组对象-包括私有的
        Field[] fields=clazz.getDeclaredFields();
        for(Field field:fields){
            System.out.println("成员变量修饰符："+field.getModifiers());//获取成员变量修饰符--返回int总值
            System.out.println("成员变量类型："+field.getGenericType());//获取成员变量类型--返回type
            System.out.println("成员变量名："+field.getName());//获取成员变量名--返回String
            if(field.getModifiers()==25) {//只有UNIVERSITY_NAME有值
                Object value = field.get(null);
                System.out.println("成员变量的值：" + value);
            }
            System.out.println("---------------------------------");

        }
    }
~~~



##### 4.通过反射访问成员方法

~~~java
    //获取成员方法
    public static void getAllMethod(Class clazz) throws NoSuchMethodException, InvocationTargetException, IllegalAccessException {
        Class[] parameterType={String.class,int.class};//参数列表
        Method method=clazz.getDeclaredMethod("chooseCourse",parameterType);//获取指定方法
        System.out.println("方法返回值类型："+method.getReturnType());//获取指定方法返回值类型

        Student student=new Student();//创建一个学校对象
        Object[] params={"123",123};
        Object result=method.invoke(student,params);
        System.out.println("方法"+method.getName()+"的返回值"+result);
    }
}
~~~

