#### 1.什么是XML?

- XML是Extensible Markup Language的简写，一种扩展性标识语言。 XML里允许你自己创建这样的标签，所以叫做可扩展性。


#### 2.XML的用途?

- 把数据从 HTML 分离：数据能够存储在独立的 XML 文件中；
- 简化数据共享：不兼容的系统之间轻松地交换数据；如中英文切换
- 简化数据传输：XML 数据以文本格式存储。


#### 3.XML使用场合

- 数据交换 
- Web服务 
- 内容管理 
- Web集成 
- 配置 



#### 4.XML文件组成

(1).前导区：规定XML的页面属性
~~~
version:表示使用的XML版本
encoding:页面文字编码
standalone表示文档是否附带DTD文件（用来定义XML文档中元素，属性以及元素之间关系的），如果有，参数为no；
~~~

(2).数据区：所有数据区必须有一个跟根元素

~~~xml
<!--前导区-->
<?xml version="1.0" encoding="UTF-8"?> 
<!--数据区-->
<root>
    <author name="汪应昌" location="China">Jam</author>
    <author name="bo" location="US">Bo</author>
</root>
~~~



#### 5.XML的严格格式

 XML标记必须遵循下面的命名规则:
 - 名字中可以包含字母、数字以及其它字母；
 - 名字不能以数字或"_" (下划线) 开头；
 - 名字不能以字母xml (或XML 或Xml ..) 开头；
 - 名字中不能包含空格。
 - 在XML文档 中任何的差错，都会得到同一个结果：网页不能被显示。

 注意:

 - 注意大小写，例如：\<P>和\<p>是不同的标识
 - 给属性值加引号
 - 所有的标识必须有相应的结束标识
 - 所有的空标识也必须被关闭
   注释：<!--注释的内容-->



#### 6.XML解析(重要)

(1).什么是解析?

在得到一个XML文件之后，应该利用程序按照里面元素的定义名称取出相应的内容，这就是XML解析;

XML解析的四种方式: DOM解析、SAX解析、JDOM解析、DOM4J解析方式;

(2).各种解析方式的优缺点:

DOM 可逆的过程:

~~~
a.将整个XML文件装入，组装成一颗DOM树，然后通过节点以及节点之间的关系来解析xml文件，适合对对XML的随机访问。
b.不过当XML过大时，其性能会严重下降；这个问题是DOM树形结构造成的，这种结构内存占用较大。
c.适用范围：小型 XML 文件解析、需要全解析或者大部分解析 XML、需要修改 XML 树内容以生成自己的对象模型.
~~~

SAX是基于事件流的解析:

~~~
a.它是顺序的读取XML文件，不需要一次把整个文件都读入内存。当遇到文件开头、文档结束、或者开始标签和结束标签时，
它会触发一个事件，用户通过在其回调事件中写入处理代码来处理XML文件，适用与XML的顺序访问。
b.顺序的过程，解析速度快，由于其不需要将整个 XML 文档读入内存当中，它对系统资源的节省是十分显而易见的.

c.适用范围：大型 XML 文件解析、只需要部分解析或者只想取得部分 XML 树内容、
有 XPath 查询需求、有自己生成特定 XML 树对象模型的需求
~~~

DOM4J解析(重要)

~~~
DOM4J有更复杂的api,所以dom4j比jdom有更大的灵活性.DOM4J性能最好，连Sun的JAXM也在用DOM4J.目前许多开源项目中大量采用DOM4J，例如大名鼎鼎的Hibernate也用DOM4J来读取XML配置文件。如果不考虑可移植性，那就采用DOM4J.

优点：1、灵活性最高	
	 2、易用性和功能强大、性能优异

缺点：1、复杂的api	
	 2、移植性差

适用：自行选择
~~~

#### 7.DTD:文件类型定义

~~~
　DTD是用来定义XML文档中元素，属性以及元素之间关系的。
　　通过DTD文件可以检测XML文档的结构是否正确。但建立XML文档并不一定需要DTD文件。 

如果文档是一个"有效的XML文档"，那么文档一定要有相应DTD文件，并且严格遵守DTD文件制定的规范。DTD文件的声明语句紧跟在XML声明语句后面，格式如下：
　　<!DOCTYPE type-of-doc SYSTEM/PUBLIC "dtd-name"> 
　　其中：
　　"!DOCTYPE"是指你要定义一个DOCTYPE;
　　"type-of-doc"是文档类型的名称，由你自己定义，通常于DTD文件名相同；
　　"SYSTEM/PUBLIC"这两个参数只用其一。SYSTEM是指文档使用的私有DTD文件的网址，而PUBLIC则指文档调用一个公用的DTD文件的网址。
　　"dtd-name" 就是DTD文件的网址和名称。所有DTD文件的后缀名为".dtd"。
~~~

#### 8.XML解析实例

解析students.xml文件
~~~xml
<?xml version="1.0" encoding="utf-8"?>
<students>
	<student no="001">
		<name>张三丰</name>
		<sex>男</sex>
		<major>挖掘机专业</major>	
	</student>
	<student no="002">
		<name>李逍遥</name>
		<sex>女</sex>
		<major>撩妹专业</major>	
	</student>
	<student no="003">
		<name>碧瑶</name>
		<sex>男</sex>
		<major>撩汉专业</major>	
	</student>
</students>
~~~

**8.1 DOM解析**
-- ParseByDom.java
~~~java
package com.xml.parse;
 
import java.io.File;
import java.io.IOException;
import java.util.ArrayList;
import java.util.List;
 
import javax.xml.parsers.DocumentBuilder;
import javax.xml.parsers.DocumentBuilderFactory;
import javax.xml.parsers.ParserConfigurationException;
 
import org.w3c.dom.Document;
import org.w3c.dom.Element;
import org.w3c.dom.NodeList;
import org.xml.sax.SAXException;
 
import com.xml.model.Student;
 
public class ParseByDom {
 
	public static void main(String[] args) throws ParserConfigurationException, SAXException, IOException {		
		
		//声明一个集合用于存储解析文件之后获取的数据
		List<Student> students=new ArrayList<Student>();
		
		//获取需要被解析的文件对象
		File f=new File("src/student.xml");	
		
		//获取解析工厂
		DocumentBuilderFactory factory=DocumentBuilderFactory.newInstance();
		//获取解析器对象
		DocumentBuilder builder=factory.newDocumentBuilder();
		//解析文件获取一个document对象
		Document document=builder.parse(f);	
		
		//builder.parse(is);
		
		//获取指定标签的所有元素对象(student元素)
		NodeList list=document.getElementsByTagName("student");
		
		for(int i=0;i<list.getLength();i++){			
			//获取每一个遍历的元素
			Element element=(Element)list.item(i);
			//获取当前元素的指定属性值
			String no=element.getAttribute("no");
			//获取子元素
			Element ename=(Element)element.getElementsByTagName("name").item(0);
			Element esex=(Element)element.getElementsByTagName("sex").item(0);
			Element emajor=(Element)element.getElementsByTagName("major").item(0);
			String name=ename.getTextContent();
			String sex=ename.getTextContent();
			String major=emajor.getTextContent();
			
			Student s=new Student(no,name,sex,major);
			students.add(s);
		
		}		
		for(Student student:students){
			System.out.println(student);
		}		
	}
}
~~~


**8.2 SAX 解析**
-- ParseBySax.java
~~~java
package com.xml.parse;
 
import java.io.File;
import java.io.IOException;
import java.util.List;
 
import javax.xml.parsers.ParserConfigurationException;
import javax.xml.parsers.SAXParser;
import javax.xml.parsers.SAXParserFactory;
 
import org.xml.sax.SAXException;
import org.xml.sax.helpers.DefaultHandler;
 
import com.xml.model.Student;
 
public class ParseBySax {
	public static void main(String[] args) throws ParserConfigurationException, SAXException, IOException {
				
		File file=new File("src/student.xml");		
		//获取sax解析工厂
		SAXParserFactory factory=SAXParserFactory.newInstance();		
		//创建解析器对象
		SAXParser parser=factory.newSAXParser();
		
		MyHandler handler=new MyHandler();
		
		//开始解析
		parser.parse(file,handler);
		
		List<Student> students=handler.getStudents();
		
		for (Student student : students) {
			System.out.println(student);
		}		
	}
}
~~~
MyHandler.java
~~~java
package com.xml.parse;
 
import java.util.ArrayList;
import java.util.List;
 
import org.xml.sax.Attributes;
import org.xml.sax.SAXException;
import org.xml.sax.helpers.DefaultHandler;
 
import com.xml.model.Student;
 
 
/**
 * 事件处理器
 * @author Administrator
 *
 */
 
public class MyHandler extends DefaultHandler{
	
	private List<Student> students;
	private Student tempStu;//声明当前读取到的学生对象
	private String tag;//声名变量记录当前的标记	
	
	//对外暴露一个方法，返回一个集合对象	
	public List<Student> getStudents() {
		return students;
	}
 
	@Override
	public void startDocument() throws SAXException {
		System.out.println("开始解析");		
		students=new ArrayList<Student>();
	}
 
	@Override
	public void startElement(String uri, String localName, String qName,
			Attributes attributes) throws SAXException {
		tag=qName;
		//如果读取到的元素开始标记为student则创建学生对象，并获取no属性值
		if("student".equals(qName)){
			tempStu=new Student();
			String no=attributes.getValue("no");
			tempStu.setNo(no);
			students.add(tempStu);
		}	
	}
		
	@Override
	public void characters(char[] ch, int start, int length)
			throws SAXException {
		String s=new String(ch,start,length);
		if("name".equals(tag)){
			tempStu.setName(s);
		}else if("sex".equals(tag)){
			tempStu.setSex(s);
		}else if("major".equals(tag)){
			tempStu.setMajor(s);
		}	
			
	}
	
	@Override
	public void endElement(String uri, String localName, String qName)
			throws SAXException {
		//将标记置空
		tag=null;	
	}
	
	@Override
	public void endDocument() throws SAXException {
		System.out.println("解析完成");		
	}
	
}
~~~
**8.3 JDOM解析**
~~~java
package com.xml.parse;
 
import java.io.File;
import java.io.IOException;
import java.util.ArrayList;
import java.util.List;
 
import org.jdom.Document;
import org.jdom.Element;
import org.jdom.JDOMException;
import org.jdom.input.SAXBuilder;
 
import com.xml.model.Student;
 
public class ParseByJDOM {
	
	public List<Student> parse() throws JDOMException, IOException{
		List<Student> students=new ArrayList<Student>();
		
		File file=new File("src/student.xml");
		
		//创建jdom
		SAXBuilder builder=new SAXBuilder();
		
		//解析指定文件获取文档对象
		Document document=builder.build(file);
		
		//获取文档根节点
		Element root=document.getRootElement();
		
		//获取当前根节点下所有的student子节点
		List<Element> list=root.getChildren("student");		
		
		for(Element e:list){
			Student s=new Student();
			String no=e.getAttributeValue("no");
			String name=e.getChild("name").getText();
			String sex=e.getChild("sex").getText();
			String major=e.getChild("major").getText();
			
			s.setNo(no);
			s.setName(name);
			s.setSex(sex);
			s.setMajor(major);
			
			students.add(s);			
		}
		
		for (Student s : students) {
			System.out.println(s);
		}	
		
		return students;	
	}	
	
	public static void main(String[] args) throws JDOMException, IOException {
		List<Student> list=new ParseByJDOM().parse();
	}
}
~~~

**8.4 DOM4J解析**
~~~java
package com.xml.parse;
 
import java.io.File;
import java.util.ArrayList;
import java.util.List;
 
import org.dom4j.Document;
import org.dom4j.DocumentException;
import org.dom4j.Element;
import org.dom4j.Node;
import org.dom4j.io.SAXReader;
 
import com.xml.model.Student;
 
public class ParseByDom4j {
 
	public List<Student> parse() throws DocumentException{
		List<Student> students=new ArrayList<Student>();
		
		File file=new File("src/student.xml");
		//创建解析器对象
		SAXReader reader=new SAXReader();
		//解析指定的文件获取文档对象
		Document document=reader.read(file);
		
		Element root=document.getRootElement();
		
		//获取根节点下所有的student节点
		List<Element> list=root.elements("student");
		
		for (Element e : list) {		
			
			String no=e.attributeValue("no");
			String name=e.element("name").getTextTrim();
			String sex=e.element("sex").getTextTrim();
			String major=e.element("major").getTextTrim();
			
			Student s=new Student(no, name, major, sex);
			
			students.add(s);			
		}	
		return students;	
	}
	
	
	public List<Student> parse2() throws DocumentException{
		List<Student> students=new ArrayList<Student>();
		
		File file=new File("src/student.xml");
		//创建解析器对象
		SAXReader reader=new SAXReader();
		//解析指定的文件获取文档对象
		Document document=reader.read(file);
		
		List<Node> nodes=document.selectNodes("students/student");
		
		for (Node node : nodes) {
			String no=node.valueOf("@no");
			String name=node.selectSingleNode("name").getText().trim();
			String sex=node.selectSingleNode("sex").getText().trim();
			String major=node.selectSingleNode("major").getText().trim();
			Student s=new Student(no, name, major, sex);
			students.add(s);		
		}		
		return students;	
	}	
	public static void main(String[] args) throws DocumentException {
		
		List<Student> list=new ParseByDom4j().parse2();
		for (Student student : list) {
			System.out.println(student);
		}		
	}
	
}
~~~

**8.5 DOM4j_xpath解析**
~~~

package com.xml.parse;
 
import java.io.File;
import java.util.List;
 
import org.dom4j.Document;
import org.dom4j.DocumentException;
import org.dom4j.Node;
import org.dom4j.io.SAXReader;
 
public class ParseByDom4j_xpath {	
	public static void main(String[] args) throws DocumentException {
		
		File file=new File("src/student.xml");		
		
		SAXReader reader=new SAXReader();
		
		Document document=reader.read(file);
		
		//搜索节点
		List<Node> nodes=document.selectNodes("students/student/name");
		
		for (Node node : nodes) {
			String name=node.getText();
			System.out.println(name);
		}		
		
		List<Node> list=document.selectNodes("students/student");
		for (Node node : list) {
			//查询属性值
			String no=node.valueOf("@no");
			System.out.println(no);
			
			String name=node.selectSingleNode("name").getText();
			System.out.println(name);
			
		}		
	}	
}
~~~
