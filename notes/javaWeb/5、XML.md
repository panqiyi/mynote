## XML

### 概念

1、Extensible Markup Language：可扩展标记语言

早期用于像html一样展示页面，现几乎用于配置文件

2、功能：存储数据

  		  1、配置文件

​			2、在网络中传输

3、xml与html的区别

​			1、xml标签都是自定义的，html标签是预定义的。

​			2、xml语法严格，html语法松散

​			3、xml是存储数据的，html是展示数据

### 语法

#### 基础语法

```
1、xml文档的后缀名 .xml
2、xml第一行必须定义为文档声明
3、xml文档中有且仅有一个根标签
4、属性值必须使用引号(单双都可)引起来
5、标签必须正确关闭
6、xml标签名称区分大小写
```

如：

```xml
<?xml version="1.0" encoding="utf-8" ?>
<users><!--根标签-->
    <user id="1">
        <name>zhangsan</name>
        <age>23</age>
        <gender>male</gender>
    </user>
    <br/>
    <user id="2">
        <name>lisi</name>
        <age>22</age>
        <gender>famale</gender>
    </user>
</users>
```



#### 组成部分

**1、文档声明**

​		1、格式：<?xml 属性列表 ?>

```
<?xml 属性列表 ?>
属性列表:
- version:版本号（必须的属性）
- encoding:编码方式。告知解析引擎当前文档使用的字符集，默认值：ISO-8859-1
- standalone:是否独立
	取值：yes：不依赖其他文件。no:依赖其他文件
```

**2、指令(了解)：结合css样式**

因为xml早期用于做页面，所以这个是用于引入css样式的，但现在已经几乎不会用到，了解即可

```xml
<?xml-stylesheet type="text/css" href="a.css" ?>
```

**3、标签**:标签自己定义 

```
规则：
- 名称可以包含字母，数字以及其他的字符
- 名称不能以数字开头或者标点符号开头
- 名称不能以字母xml开始
- 名称不能包含空格
```

**4、属性**

id属性值唯一

**5、文本**

CDATA区：在该区域的数据会被原样展示

```
格式: <![CDATA[文本]]>
```

### 约束

规定xml文档的书写规则

1、在xml中引入约束文档

2、简单的读懂约束规则

#### 分类

**1、DTD **:一种简单的约束

- 引入dtd文档到xml文档中

   - 内部dtd：将约束规则定义在xml文档中（了解）

     ​	<!DOCTYPE 根标签名 [约束内容]>

   - 外部dtd：将约束规则定义在外部的dtd文件中（常用）

     		- 本地：<!DOCTYPE 根标签名 SYSTEM "dtd文件的位置">
       		- 网络：<!DOCTYPE 根标签名 PUBLIC "dtd文件名字" "dtd文件位置URL">

如：

dtd文件约束如下：

```dtd
<!--xml文件引入该约束规则，就会遵守该套规则-->
<!ELEMENT students (student*) > <!--student根标签  (student*)：子标签，*为可出现0~n次-->
<!ELEMENT student (name,age,sex)> <!--子标签内包含的标签-->
<!ELEMENT name (#PCDATA)> <!--name (#PCDATA)>:name标签内为字符串-->
<!ELEMENT age (#PCDATA)>
<!ELEMENT sex (#PCDATA)>
<!ATTLIST student number ID #REQUIRED> <!--定义属性，ID表示值唯一，#REQUIRED表示值必须写-->
```

在xml文件中引入约束dtd文件，该xml就只能按照该约束编写

```xml
<?xml version="1.0" encoding="utf-8" ?>
<!DOCTYPE students SYSTEM "dtd/student.dtd"><!--引入约束的dtd文件-->
<students>
    <student number="x01"> <!--number赋值不能纯数字-->
        <name>zs</name>
        <age>13</age>
        <sex>male</sex>
    </student>
    <student number="s02">
        <name>lisi</name>
        <age>17</age>
        <sex>male</sex>
    </student>
</students>
```



**2、Schema**：一种复杂的约束

scheme约束的文件后缀名为xsd。

如下有一个xsd文件约束

```xml
<?xml version="1.0"?>
<xsd:schema xmlns="http://www.itcast.cn/xml"
        xmlns:xsd="http://www.w3.org/2001/XMLSchema"
        targetNamespace="http://www.itcast.cn/xml" elementFormDefault="qualified">
    <xsd:element name="students" type="studentsType"/>   <!--根标签名：students 类型为：studentsType(自定义类型)-->
    <xsd:complexType name="studentsType"><!--复杂类型：complexType，看类型名即用来规定根标签students内-->
        <xsd:sequence><!--顺序-->
            <xsd:element name="student" type="studentType" minOccurs="0" maxOccurs="unbounded"/>
            <!--子标签：student 类型：studentType(自定义) 个数：0~n个-->
        </xsd:sequence>
    </xsd:complexType>
    <xsd:complexType name="studentType"> <!--看类型名即规定student标签中-->
        <xsd:sequence>
            <!--里面有如下标签，并且每个标签有对应的类型-->
            <xsd:element name="name" type="xsd:string"/><!--字符串类型-->
            <xsd:element name="age" type="ageType" /><!--自定义类型-->
            <xsd:element name="sex" type="sexType" /><!--自定义类型-->
        </xsd:sequence>
        <xsd:attribute name="number" type="numberType" use="required"/> <!--属性：number 类型：自定义  use="required"：需要写-->
    </xsd:complexType>
    <xsd:simpleType name="sexType"><!--simpleType：简单类型  对上面对应自定义类型进行编写-->
        <xsd:restriction base="xsd:string"><!--restriction：限制-->
            <!--enumeration：枚举  值只能为male或female-->
            <xsd:enumeration value="male"/>
            <xsd:enumeration value="female"/>
        </xsd:restriction>
    </xsd:simpleType>
    <xsd:simpleType name="ageType">
        <xsd:restriction base="xsd:integer">
            <!--限制年龄：0~256-->
            <xsd:minInclusive value="0"/>
            <xsd:maxInclusive value="256"/>
        </xsd:restriction>
    </xsd:simpleType>
    <xsd:simpleType name="numberType">
        <xsd:restriction base="xsd:string">
            <!--限制number属性值格式：P_1234 -->
            <xsd:pattern value="P_\d{4}"/>
        </xsd:restriction>
    </xsd:simpleType>
</xsd:schema> 
```

**使用**

```xml
<students   xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"  <!--引入xsi前缀，固定（有多种版本，工具会提示）-->
         xsi:schemaLocation="http://www.qiyi.cn/xml  student.xsd"
       xmlns="http://www.itcast.cn/xml">

   <student number="heima_0001">
      <name>tom</name>
      <age>18</age>
      <sex>male</sex>
   </student>
    
</students>
```

```xml
<!-- 
   1.填写xml文档的根元素 :students
   2.引入xsi前缀.  xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
   3.引入xsd文件命名空间.  xsi:schemaLocation="http://www.qiyi.cn/xml  student.xsd"
			http://www.qiyi.cn/xml:文件路径的名字(代号)    student.xsd:文件位置
   4.为每一个xsd约束声明一个前缀,作为标识  xmlns="http://www.qiyi.cn/xml" （这样声明为默认，方便使用）
   			xmlns:a="http://www.qiyi.cn/xml" (此时为a),这样就需要在每一个标签前添加“a:”
   			 <a:sex>male<a:/sex>
  			 <a:/student>
 -->
```



### 解析

操作xml文档，将文档中的数据读取到内存中

**解析xml的方式：**

**1、DOM**：将标记语言文档一次性加载进内存，在内存中形成dom树

		- 优点：操作方便，可以对文档进行CRUD的所有操作
		- 缺点：占较大内存 (用于服务器端)

**2、SAX**：逐行读取，基于事件驱动

		- 优点：几乎不占内存  （用于移动端）
		- 缺点：只能读取，不能增删改



### xml常见解析器

**1、JAXP：**sun公司提供的解析器java，支持dom和sax两种思想

**2、DOM4J：**一款非常优秀的解析器

**3、JSOUP：**jsoup是一款java的html解析器，也可用于xml

**4、PULL：**android操作系统内置的解析器，sax方式



### jsoup解析器

#### 快速入门

**1、导入jar包**

与jdbc导入jar方式一样，记得

<img src="https://gitee.com/panqiyi/pqimg/raw/master/20201227153252.png" alt="image-20201227153252073" style="zoom:80%;" />

**然后 ：**

```java
public static void main(String[] args) throws IOException {
    //2、获取Document对象，根据xml文档获取
        //2.1 获取xml文件的path
    String path = Jsoup01.class.getClassLoader().getResource("students.xml").getPath();
        //2.2 解析xml文档，加载文档进内存，获取dom树-->Document
    Document document = Jsoup.parse(new File(path), "utf-8");
    //3、获取元素对象 Element
    Elements elements = document.getElementsByTag("name"); //传入标签，返回标签对象集合
        //3.1 获取第一个name的Element对象
    Element element = elements.get(0);
        //3.2 获取标签内容数据
    String name = element.text();
    System.out.println(name);
}
```



#### 对象的使用

**1、Jsoup**：工具类，可以解析html或xml文档，返回Document

```java
parse: 解析html文档或xml文档，返回Document
	parse(File in,String charsetName): 解析xml或html文件的
	parse(String html): 解析xml或html字符串的
	parse(URL url,int timeoutMillis): 通过网络路径获取指定html或xml的文档对象
	如：
	URL url = new URL("https://www.baidu.com/");
        Document document = Jsoup.parse(url, 5000); //网络地址,超时时间
        System.out.println(document);
```

**2、Document**：文档对象。代表内存中的dom树

- 获取Element对象

```java
getElementsByTag(String tagName): 根据标签名称获取元素对象集合
getElementById(String id): 根据id 属性值获取元素对象
getElementsByAttribute(String key): 根据属性名获取元素集合对象
getElementsByAttributeValue(String key,String value): 根据属性名，属性值获取元素对象集合
```

**3、Elements**：元素对象集合，可以当作ArrayList<Element>来使用

**4、Element**：元素对象

- 获取子标签内容

```java
getElementsByTag(String tagName): 根据标签名称获取元素对象集合
getElementById(String id): 根据id 属性值获取元素对象
getElementsByAttribute(String key): 根据属性名获取元素集合对象
getElementsByAttributeValue(String key,String value): 根据属性名，属性值获取元素对象集合
```

- 获取属性值

```java
String attr(String key): 根据属性值名获取属性值
```

- 获取文本内容

```java
String text(): 获取文本内容
String html(): 获取标签体的全部内容(包括子标签)
```

**5、Node**：节点对象

是Document和Element的父类

#### 快捷查询

##### 选择器查询

selector:选择器

 - 使用方法：Elements	select(String  cssQuery)
   	- 语法：参考Selector类中定义的语法

如：

```Java
String path = Jsoup03.class.getClassLoader().getResource("students.xml").getPath();
Document document = Jsoup.parse(new File(path), "utf-8");
Elements student = document.select("student"); //根据标签名获取dom对象
Elements element1 = document.select("#001"); //根据id属性值获取dom对象
Elements element2 = document.select("student[number='a2']>age"); 
//获取标签名为student 属性number='a2'的标签内的age标签对象

 Elements element3 = document.select("student[number='a1'] name b");
//获取标签名为student 属性number='a1'的标签内 name标签内的b标签dom对象，后代选择器
```



##### XPath

XPath即为xml路径语言，它是用来确定xml文档中某部分位置的语言

- 使用Jsoup的Xpath需要额外导入jar包。
- 查询w3cshool参考手册，使用xpath的语法完成查询

如：

```java
String path = Jsoup04.class.getClassLoader().getResource("students.xml").getPath();
Document document = Jsoup.parse(new File(path), "utf-8");
//创建JXdocument对象,传入document对象
JXDocument jxDocument = new JXDocument(document);
List<JXNode> jxNodes = jxDocument.selN("//student"); 
for (JXNode jxNode : jxNodes) {
    System.out.println(jxNode);
}
```