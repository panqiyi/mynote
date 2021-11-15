## Jsp

### JSP入门

### 概念

Java Servler Pages :  Java服务器端页面

	- 可以理解为一个特殊的页面，其中即可以指定html标签，又可以定义Java代码

### 原理

**jsp本质上就是一个Servlet**

运行tomcat，打开浏览器访问一个jsp文件，看控制台日志信息上面有如下一段

![image-20210330220437083](https://gitee.com/panqiyi/pqimg/raw/master/20210330220437.png)

复制该路径，文件打开

![image-20210330221004918](https://gitee.com/panqiyi/pqimg/raw/master/20210330221004.png)

即运行的jsp文件产生的资源

![image-20210330221127457](https://gitee.com/panqiyi/pqimg/raw/master/20210330221127.png)

由此可以看出：.jsp --> .java --> .class

打开.java文件查看代码：发现index_jsp类继承 HttpJspBase类

![image-20210330221503212](https://gitee.com/panqiyi/pqimg/raw/master/20210330221503.png)

而HttpJspBase类是由apache提供的，即tomcat提供的。

下面再看tomcat中HttpJspBase类，

![image-20210330221751916](https://gitee.com/panqiyi/pqimg/raw/master/20210330221751.png)

发现他继承自 HttpServlet, 所以说jsp本质上是一个Servlet

### 脚本

1、代码脚本

```
格式：<% Java语句 %>
作用：在JSP页面中可以编写需要的Java代码
```

2、表达式脚本

```
格式：<%=表达式 %>
作用：在浏览器的JSP页面上输出数据
```

3、声明脚本

```
格式：<%! 声明Java代码 %>
作用：可以给JSP翻译出来的Java类定义属性、方法、静态代码块、内部类等
```

### 指令

作用：用于配置jsp页面，导入资源文件

```
格式：
	<%@ 指令名称 属性名1=属性值1 属性2=属性值2……%>
```

分类：

**1、page     ：配置jsp页面**

- contenType：等同于response.setContentType()

  ​	1、设置响应体的mime类型以及字符集

  ​	2、设置当前jsp页面的编码(只能是高级的ide才能生效，低级工具则需要设置pageEncoding属性设置当前页面字符集)

- import：导包，如使用Java 的list集合就要导包

- errorPage：当前页面发生异常后，会自动跳转到指定的错误页面

- isErrorPage：标识当前页面是否是错误页面

  ​		true：是，可以使用内置对象exception(异常信息对象)

  ​		false：否，默认值。不可以使用内置对象exception

**2、include  ：页面包含的。引入页面的资源文件**

```
如很多页面都包含有某个特点，将该特点写到一个页面a，其他页面引入该页面a
<%@ include file="a.jsp" %>
```

**3、taglib    ：导入资源**

```
多用于导入标签库
<%@ taglib prefix="c" url="http://java.sun.com/jsp/jstl/core"%>
	- prefix ：前缀，自定义的
```

### 注释

```
html注释：
	<!-- 注释内容--> 只能注释html代码片段

jsp注释：推荐使用

	<%注释内容%> 可注释所有
```



### 内置对象

在jsp页面中不需要获取和创建，可以直接使用的对象、

jsp一共有9个内置对象。

- request

- response

- out : 字符串输出流对象。可以将数据输出到页面上。和response.getWriter()类似

  - response. getWriter() 和 out. writer() 的区别

    ​	在tomcat服务器真正给客户端做出响应之前，会先找response 缓冲区数据，再找out缓冲区数据。

    ​	所以response. getWriter() 会比 out. writer() 先输出，为了不影响布局，jsp会都选择用out. writer() 

![image-20210419233144801](https://gitee.com/panqiyi/pqimg/raw/master/20210419233145.png)

（exception对象只有在 page指令下的isErrorPage属性的属性值为true才有）



### MVC：开发模式

1、jsp演变历史

​		1、早期只有servlet，只能使用response输出标签数据，非常麻烦

​		2、后来有jsp，简化了servlet的开发，如果过度使用jsp，在jsp中写入大量的Java代码和html结构，造成难于维护，难于分工协作。

​		3、再后来，Java的web开发，借鉴mvc开发模式，使得程序得设计更加合理

**2、MVC：**

M：Model，模型。JavaBean

​		- 完成具体得业务操作，如：查询数据库，封装对象

V：View，视图。jsp

​		- 展示数据

C：Controller，控制器。Servlet

​		- 获取用户输入

​		- 调用模型

​		- 将模型返回数据给视图进行展示

![image-20210420093707052](https://gitee.com/panqiyi/pqimg/raw/master/20210420093707.png)

### EL表达式

1、概念：Expression Language 表达式语言

2、作用：替换和简化jsp页面中的Java代码编写

3、语法：${表达式}

4、注意：

  - jsp默认支持EL表达式，如果要忽略EL表达式

    ​			1、设置jsp中page指令中：isELIgnored="true" 忽略当前页面中所有EL表达式

    ​			2、\ ${表达式} ：忽略当前这个EL 表达式

5、使用：

​		常用于：1、运算；2、获取值

```
${5+7}
${pageContext.request.contextPath} 获取虚拟目录
action="${pageContext.request.contextPath}/loginServlet"
```

​	**1、运算符**

```
1、算数运算符：+ - * /(也可div) %(mod)
2、比较运算符：> < >= <= == !=
3、逻辑运算符：&&(and) ||(or) !(not)
4、空运算符：empty
		- 功能：用于判断字符串、集合、数组对象是否为null并且长度是否为0
		- 长度为0或者对象为null则返回true
			- ${empty lists}
			
```

```
empty举例:
<%
    String str="";
    ArrayList ali=new ArrayList<>();
    ali.add(str);
%>

${empty ali} <%--长度为0或者 为空，返回true--%>
${not empty ali} <%--不为空   相当于 if(ali != null && ali.lenght !=0)--%>
```

​	**2、获取值**

1、el表达式只能从域对象中获取值

2、语法：

​		**1、${域名称 . 键名} ： 从指定域中获取指定键的值**

   - 域名称：

     ```
     	域名称
     1、pageScope         --->pageContext
     2、requstScope       --->requst
     3、sessionScope      --->session
     4、applicationScope  --->application
     
     - 举例：在request域中存储了name=张三
     - 获取：${requstScope.name}
     ```
```
     
     **2、${键名} ： 表示依次从最小的域中查找是否有该键对应的值，直到找到为止(即上面的1~4从小到大)**

​```jsp
<%request.getSession().setAttribute("name","李四");%>
${pageContext.request.setAttribute("name","张三")}


${name} <%--张三--%>
${sessionScope.name} <%--李四--%>
```

​		**3、获取对象、list集合、Map集合的值**

​				**1、对象：${域名称.键名.属性名}**

​						- 本质上会去调用对象的getter方法

例如：现在有User类，要在jsp中获取其对象内容

```java
public class User {
    private String name;
    private int age;
    private Date birthday;
    //省略get/set方法
    }
```

```jsp
jsp:
<%@ page import="maindao.User" %> <%--导入java类--%>

<%--获取对象，设置值. 并将对象存储到request域中--%>
<%
    User user = new User();
    user.setName("张三");
    user.setAge(18);
    user.setBirthday(new Date());

    request.setAttribute("u",user);
%>

<%--
    通过的是对象的属性来获取
        - setter或getter方法，去掉set或get，在将剩余部分，首字母变小写。
        - setName --> Name --> name
        实际上是调用成员方法。
--%>

${requestScope.u.name}<br>
${u.name}<br>
${u.age}<br>
${u.birthday}
```

![image-20210424123643939](https://gitee.com/panqiyi/pqimg/raw/master/20210424123644.png)

将时间格式化输出：在Bean类中添加一个方法

```java
public class User {
    private String name;
    private int age;
    private Date birthday;
    
    //逻辑视图
   public String getBirStr(){
        if (birthday != null){
            SimpleDateFormat sdf=new SimpleDateFormat("yyyy-MM-dd HH:mm:ss");
            return sdf.format(birthday);
        }else {
            return "";
        }
    }
    
    //省略get/set方法
    }

jsp:
${requestScope.u.name}<br>
${u.name}<br>
${u.age}<br>
${u.birthday}<br>

${u.birStr} //调用了getBirStr()方法

```

![image-20210424125910714](https://gitee.com/panqiyi/pqimg/raw/master/20210424125910.png)

​		**2、List集合：**`${域名称.键名[索引]}`

```jsp
<%--LIst--%>
<% ArrayList list = new ArrayList<>();
    list.add("张三");
    list.add(23);

    request.setAttribute("list",list);
%>

${requestScope.list[0]}
${list[1]}
```

​		**3、Map集合：**`${域名称.键名.key名称}`  或  `${域名称.键名["key名称"]}`

```jsp
<%--Map--%>
<%
    HashMap hash=new HashMap<>();
    hash.put("name","李小龙");
    hash.put("gender","男");
    hash.put("user",user);

    request.setAttribute("map",hash);
%>

${requestScope.map.name}
${map.gender}<br>
${map.user.birStr}
```



**3、隐式对象：**

- el表达式中有11个隐式对象

- pageContext：

    - 获取jsp其他八个内置对象

      ​		-  ${pageContext. request. contextPath }  : 动态获取虚拟目录



### JSTL

1、概念：JavaServer  Page  Tag   Library      Jsp标准标签库	

			- 是由Apache组织提供的开源的免费的jsp标签

2、作用：用于简化和替换jsp页面上的Java代码

3、使用步骤：

​		1、导入jstl相关jar包

![image-20210424201347060](https://gitee.com/panqiyi/pqimg/raw/master/20210424201347.png)

​		2、引入标签库：taglib指令：<%@  taglib %>

```
jsp中：<%@taglib prefix="c" uri="http://java.sun.com/jsp/jstl/core" %>
 prefix="c" ：前缀
```

​		3、使用标签

4、常用标签：

​		**1、if             ： 相当于Java中的if语句**

```jsp
<c:if test="true">
    你好啊,真的才能进哦
</c:if>

c:if标签：
	属性：test 必须写的属性，接收Boolean表达式
		- 如果表达式为true，则显示if标签体内容，如果为false，则不显示标签体内容
		- 一般情况下，test属性值会结合el表达式一起使用
	注意：c:if标签没有else情况，想要else情况，则可以再定义一个c:if标签
```

​		**2、choose   ：相当于Java中的switch语句**

```jsp
<%
    request.setAttribute("number",7);
%>

<c:choose>
    <c:when test="${number==1}">星期1</c:when>
    <c:when test="${number==2}">星期2</c:when>
    <c:when test="${number==3}">星期3</c:when>
    <c:when test="${number==4}">星期4</c:when>
    <c:when test="${number==5}">星期5</c:when>
    <c:when test="${number==6}">星期6</c:when>
    <c:when test="${number==7}">星期天</c:when>
    <c:otherwise>数字输入有误</c:otherwise>
</c:choose>
```

​		**3、foreach   ：相当于Java 中的for语句**

```jsp
<%--
1、完成重复的操作
    - 属性：
        begin：开始值
        end：结束值
        var:临时变量
        step：步长
        varStatus:循环状态对象
            index:容器中元素的索引，从0开始(非容器会显示值)
            count：循环次数，从1开始
--%>

<c:forEach begin="1" end="10" var="i" step="2" varStatus="s">
    ${i} ，${s.index} ，${s.count} <br>
</c:forEach>
```

![image-20210425194209779](https://gitee.com/panqiyi/pqimg/raw/master/20210425194209.png)

```jsp
<%--
  2、遍历容器
        - 属性
           items:容器对象
           var:容器中元素的临时状态对象
           varStatus:循环状态对象
                index:容器中元素的索引，从0开始
                count：循环次数，从1开始
--%>
    

<%
    ArrayList list = new ArrayList();
    list.add("aa");
    list.add("bb");
    list.add("cc");

    request.setAttribute("list",list);
%>

<c:forEach items="${list}" var="str" varStatus="s">
    ${s.index} ${s.count} ${str}<br>
</c:forEach>
```

![image-20210425194802719](https://gitee.com/panqiyi/pqimg/raw/master/20210425194802.png)

**4、< c : set>**

存储数据

```html
    <c:set var="salary" scope="session" value="${100*3}" />
	<c:set>这里面也是存储的值</c:set>
    薪水值：
    <c:out value="${salary}" />
    结果：薪水值:300

     var：变量     scope：作用域范围(page、request、session、application)  value:存储的值
     <c:out value="${变量名}" />: 获取存储的值
```



**案例：**

需求：在request域中有一个存有User对象的List集合。需要使用jstl+el将list集合展示到jsp页面的表格中

```jsp
<%--该User类为上面el表达式哪里的User类--%>
<%
    List list = new ArrayList();
    list.add(new User("张三",23,new Date()));
    list.add(new User("李四",15,new Date()));
    list.add(new User("聂风",26,new Date()));
    list.add(new User("步惊云",20,new Date()));

    request.setAttribute("list",list);
%>

<table width="400" border="1">
    <tr>
        <th>编号</th>
        <th>姓名</th>
        <th>年龄</th>
        <th>生日</th>
    </tr>
    <c:forEach items="${list}" var="s" varStatus="st">
        <tr>
            <td>${st.count}</td>
            <td>${s.name}</td>
            <td>${s.age}</td>
            <td>${s.birStr}</td>
        </tr>
    </c:forEach>
</table>
```



### 三层架构

1、界面层(表示层) ：用户看的界面。用户可以通过界面上的组件和服务器进行交互

2、业务逻辑层 ：处理业务逻辑的。

3、数据访问层 ：操作数据存储文件。

![image-20210426110655211](https://gitee.com/panqiyi/pqimg/raw/master/20210426110655.png)



### 案例：用户信息列表展示

1、需求：用户信息的增删改查操作

2、设计：

​			1、技术选型：Servlet+JSP+MySQL+JdbcTempleat + Duird + BeanUtils + tomcat

​			2、数据库设计：

```
create database  day1;  -- 创建数据库
use day1;  -- 使用数据库
create table user(  -- 创建表
	id int primary key auto_increment,
	name varchar(20) not null,
	gender varchar(5),
	age int,
	address varchar(32),
	qq varchar(20),
	email varchar(50)
);
```

3、开发：

​		1、环境搭建

​				1、创建数据库环境

​				2、创建项目，导入需要的jar包

![image-20210426165422952](https://gitee.com/panqiyi/pqimg/raw/master/20210426165423.png)

​		2、编码

![image-20210426172235952](https://gitee.com/panqiyi/pqimg/raw/master/20210426172236.png)

首先创建一些必要的包：

<img src="https://gitee.com/panqiyi/pqimg/raw/master/20210428093909.png" alt="image-20210428093909351" style="zoom:80%;" />

```
dao包：
UserDao接口：定义一些操作数据库的抽象方法
impl包：定义UserDao接口的实现类，在该类中通过JDBC访问数据库
service包：
UserService接口：定义了一些业务操作(操作数据库)方法
impl包：定义UserService接口的实现类，该类通过调用UserDao接口的实现类完成业务，返回操作后的对象
```

接口：定义业务方法

```java
//UserService接口，暂时定义了两个业务操作
public interface UserService {
    /**
     *查询
     * @return
     */
    public List<User> findAll();

    /**
     * 登录
     * @param user
     * @return
     */
    public User login(User user);
}
```

```java
//UserDao接口，为完成service对应的业务操作，同时定义了满足业务操作的访问数据库的方法
public interface UserDao {
    /**
     * 查找全部属性
     * @return
     */
    public List<User> findAll();

    /**
     * (登录查找)查找用户名和密码
     * @param user
     * @return
     */
    public User findByUsernameAndPassword(User user);
}
```

实现类：实现接口方法，并编写对应功能

```Java
//UserDaoImpl实现类
public class UserDaoImpl implements UserDao {
    JdbcTemplate template=new JdbcTemplate(JDBCUtils.getDataSource());
    @Override
    public List<User> findAll() { //实现UserDao接口的查询全部信息方法
        //jdbc操作数据库
        //定义sql
        try {
            String sql="select * from user";
            List<User> users = template.query(sql, new BeanPropertyRowMapper<User>(User.class));
            return users;
        } catch (DataAccessException e) {
            e.printStackTrace();
            return null;
        }
    }}
```

```Java
//UserServiceImpl实现类
public class UserServiceImpl implements UserService {  //实现UserService接口方法
   private UserDao dao=new UserDaoImpl(); //创建UserDaoImpl实现类对象

    @Override
    public List<User> findAll() {
        //调用UserDaoImpl实现类对象的对应方法完成查询
        return dao.findAll();
    }}
```

#### **1、简单功能：**

##### 		1、列表查询

```java
@WebServlet("/userLiseServlet")  //Servlet控制
public class UserListServlet extends HttpServlet {
    protected void doPost(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
        //使用UserService完成查询
        UserService service=new UserServiceImpl();
        List<User> users = service.findAll();

        //将list存入request域中
        request.setAttribute("users",users);
        //转发到list.jsp
        request.getRequestDispatcher("/list.jsp").forward(request,response);
    }
    protected void doGet(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
        this.doPost(request, response);
    }
}
```

```java
public interface UserService { //service接口
    /**
     *查询
     * @return
     */
    public List<User> findAll();
    }

public class UserServiceImpl implements UserService { //service接口实现类
   private UserDao dao=new UserDaoImpl();

    @Override
    public List<User> findAll() {
        //调用Dao完成查询
        return dao.findAll();
    }}
```

```java
public interface UserDao { //dao访问数据库接口
    /**
     * 查找全部属性
     * @return
     */
    public List<User> findAll();
    }
    
  public class UserDaoImpl implements UserDao { //dao访问数据库接口实现类
    JdbcTemplate template=new JdbcTemplate(JDBCUtils.getDataSource());
    @Override
    public List<User> findAll() { //实现UserDao接口的查询全部信息方法
        //jdbc操作数据库
        //定义sql
        try {
            String sql="select * from user";
            List<User> users = template.query(sql, new BeanPropertyRowMapper<User>(User.class));
            return users;
        } catch (DataAccessException e) {
            e.printStackTrace();
            return null;
        }
    }}
```

```jsp
list.jsp页面的部分代码，信息展示，遍历由servlet存储的list集合展示
<c:forEach items="${requestScope.users}" varStatus="s" var="user">
            <tr>
                <td><input type="checkbox"></td>
                <td>${s.count}</td>
                <td>${user.name}</td>
                <td>${user.gender}</td>
                <td>${user.age}</td>
                <td>${user.address}</td>
                <td>${user.qq}</td>
                <td>${user.email}</td>
                <td><a class="btn btn-default btn-sm" href="${pageContext.request.contextPath}/findUserServlet?id=${user.id}">修改</a>&nbsp;
 <%--                    点击删除按钮，进入删除的Servlet,并传入主键--%>
                    <a class="btn btn-default btn-sm" id="del_btn" href="javascript:deleteUser(${user.id});">删除</a></td>
            </tr>
        </c:forEach>
```

##### 		2、登录

```java
//Servlet
@WebServlet("/loginServlet")
public class LoginServlet extends HttpServlet {
    protected void doPost(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
        //1、设置编码
        request.setCharacterEncoding("utf-8");

        //2 验证验证码
         //2.1获取用户输入验证码
        String verifycode = request.getParameter("verifycode");
         //2.1 获取生成的随机验证码
        HttpSession session = request.getSession();
        String checkcode_server = (String) session.getAttribute("CHECKCODE_SERVER");
        session.removeAttribute("CHECKCODE_SERVER"); //确保验证码一次性
        if (!checkcode_server.equalsIgnoreCase(verifycode)){
            //验证码不正确，提示信息
            //跳转到登陆页面
            request.setAttribute("login_msg","验证码有误");
            request.getRequestDispatcher("login.jsp").forward(request,response);

            return; //验证码不正确，结束程序，不用执行下面的代码节省资源
        }


        //3、获取所以请求头和创建User对象
        Map<String, String[]> map = request.getParameterMap();
        User user = new User();
        //4、封装User对象
        try {
            BeanUtils.populate(user,map);
        } catch (IllegalAccessException e) {
            e.printStackTrace();
        } catch (InvocationTargetException e) {
            e.printStackTrace();
        }
        //5、调用Service完成查询
        UserService service = new UserServiceImpl();
        User loginUser=service.login(user);
        if (loginUser!=null){
            //登陆成功
            session.setAttribute("user",loginUser);
            response.sendRedirect(request.getContextPath()+"/index.jsp");
        }else {
            //登陆失败
            //跳转到登陆页面
            request.setAttribute("login_msg","用户名或密码有误");
            request.getRequestDispatcher("login.jsp").forward(request,response);
        }
    }

    protected void doGet(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
        this.doPost(request, response);
    }
}
```

​	Service接口中增加了登录方法

```java
 //UserService接口增加登录抽象方法
/**
 * 登录
 * @param user
 * @return
 */
public User login(User user);
//////////////////////////////////////////
@Override
    public User login(User user) { //接口的实现类 UserServiceImpl也自然重写接口方法
        return dao.findByUsernameAndPassword(user);
    }
```

dao包访问数据库接口也对应增加登录抽象方法

```java
//UserDao接口增加登录抽象方法
/** 
 * (登录查找)查找用户名和密码
 * @param user
 * @return
 */
public User findByUsernameAndPassword(User user);
///////////////////////////////////////////////////////
//实现类UserDaoImpl自然重写接口所有抽象方法
 @Override
    public User findByUsernameAndPassword(User user) { //登录

        try {
            String sql="select * from user where username=? and password=?";
            User loginUser = template.queryForObject(sql, new BeanPropertyRowMapper<User>(User.class),
                    user.getUsername(),
                    user.getPassword());
            return loginUser;
        } catch (DataAccessException e) {
            e.printStackTrace();
            return null;
        }
    }
```

##### 		3、添加

```java
@WebServlet("/addServelt")
public class AddServelt extends HttpServlet {
    protected void doPost(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {

        //设置编码
        request.setCharacterEncoding("utf-8");
        //获取页面表单输入信息
        Map<String, String[]> map = request.getParameterMap();
        //获取User对象
        User user = new User();
        //使用BeanUtils封装对象
        try {
            BeanUtils.populate(user,map);
        } catch (IllegalAccessException e) {
            e.printStackTrace();
        } catch (InvocationTargetException e) {
            e.printStackTrace();
        }

        //调用service提交存储联系人信息
        UserService service=new UserServiceImpl();
        service.addUser(user);

        //添加后访问查询
        //request.getRequestDispatcher("/userLiseServlet").forward(request,response);
        response.sendRedirect(request.getContextPath()+"/userLiseServlet");
    }

    protected void doGet(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
        this.doPost(request, response);
    }
}
```

​		直接写访问数据库的实现类，因为UserService和其实现类欢迎UserDao与上面大同小异

```Java
@Override
public void addUser(User user) { //添加
    String sql="insert into user values(null ,?,?,?,?,?,?,null ,null )";


    int update = template.update(sql,
            user.getUsername(),
            user.getGender(),
            user.getAge(),
            user.getAddress(),
            user.getQq(),
            user.getEmail());
}
```

##### 4、删除

```jsp
<%--                    点击删除按钮，进入删除的Servlet,并传入主键--%>
                    <a class="btn btn-default btn-sm" id="del_btn" href="javascript:deleteUser(${user.id});">删除</a></td>
 
<%-- 为了避免误触删除，增加安全提示--%>
<script>
        function deleteUser(id){
            //安全提示
            if (confirm("你确定要删除吗？")){
                //访问地址
                location.href="${pageContext.request.contextPath}/deleteServlet?id="+id;
            }
        }
    </script>
```

```Java
@WebServlet("/deleteServlet")
public class DeleteServlet extends HttpServlet {
    protected void doPost(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {

        //设置编码（id为数字，也可无需设置）
        request.setCharacterEncoding("utf-8");
        //获取主键
        String id = request.getParameter("id");
        //调用service执行删除业务
        UserService service=new UserServiceImpl();
        service.deleteUser(id);

        //重定向到查询servlet
        response.sendRedirect(request.getContextPath()+"/userLiseServlet");

    }

    protected void doGet(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
        this.doPost(request, response);
    }
}
```

```java
@Override  //
public void delect(int id) {  //删除
    String sql="delete from user where id=?";
    template.update(sql, id);
}
```

##### 5、修改

![image-20210429103149571](https://gitee.com/panqiyi/pqimg/raw/master/20210429103149.png)

```jsp
在list.jsp中传入id给findUserServlet
<td><a class="btn btn-default btn-sm" href="${pageContext.request.contextPath}/findUserServlet?id=${user.id}">修改</a>&nbsp;
```

```java
@WebServlet("/findUserServlet")
public class findUserServlet extends HttpServlet {
    protected void doPost(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
        //获取id
        String id = request.getParameter("id");
        //调用service查询并返回User对象
        UserService service=new UserServiceImpl();
        User user = service.findId(id);

        //存储对象到request，然后转发到添加联系人jsp页面 回显
        request.setAttribute("user",user);
        request.getRequestDispatcher("/update.jsp").forward(request,response);


    }

    protected void doGet(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
        this.doPost(request, response);
    }
}
```

```java
@Override 
public User findId(int id) { //根据id查询信息
    String sql="select * from user where id=?";
    User user = template.queryForObject(sql, new BeanPropertyRowMapper<User>(User.class),id);
    return user;

}
```

```java
//在update.jsp使用数据库返回user对象完成回显，就是value的值和性别、籍贯的默认值与user对象的值相等时
//注意性别与籍贯回显是的比较判断写法
<div class="container" style="width: 400px;">
<h3 style="text-align: center;">修改联系人</h3>
<form action="${pageContext.request.contextPath}/updateServlet" method="post">
    <%--隐藏域提交id,因为修改时查询需要id--%>
    <input type="hidden" name="id" value="${user.id}">

  <div class="form-group">
    <label for="name">姓名：</label>
    <input type="text" class="form-control" id="name" name="name" value="${user.name}"  readonly="readonly" placeholder="请输入姓名" />
  </div>

  <div class="form-group">
    <label>性别：</label>
      //判断 <c:if test="${user.gender == '男'}"> checked </c:if> jstl语句，如gender == '男'则默认为男
          <input type="radio" name="gender" value="男" <c:if test="${user.gender == '男'}"> checked </c:if>/>男
          <input type="radio" name="gender" value="女" <c:if test="${user.gender == '女'}"> checked </c:if> />女

  </div>

  <div class="form-group">
    <label for="age">年龄：</label>
    <input type="text" class="form-control" id="age" value="${user.age}"  name="age" placeholder="请输入年龄" />
  </div>

  <div class="form-group">
    <label for="address">籍贯：</label>
     <select name="address" class="form-control"  >
        <option value="广东" <c:if test="${user.address == '广东'}">selected</c:if> >广东</option>
        <option value="广西" <c:if test="${user.address == '广西'}">selected</c:if> >广西</option>
        <option value="湖南" <c:if test="${user.address == '湖南'}">selected</c:if> >湖南</option>
        <option value="南京" <c:if test="${user.address == '南京'}">selected</c:if> >南京</option>
    </select>
  </div>

  <div class="form-group">
    <label for="qq">QQ：</label>
    <input type="text" class="form-control" name="qq" value="${user.qq}" placeholder="请输入QQ号码"/>
  </div>

  <div class="form-group">
    <label for="email">Email：</label>
    <input type="text" class="form-control" name="email" value="${user.email}" placeholder="请输入邮箱地址"/>
  </div>

     <div class="form-group" style="text-align: center">
        <input class="btn btn-primary" type="submit" value="提交" />
        <input class="btn btn-default" type="reset" value="重置" />
        <input class="btn btn-default" type="button" value="返回"/>
     </div>
</form>
</div>
```

#### **2、复杂功能：**

##### 		**1、删除选中**

![image-20210429150754715](https://gitee.com/panqiyi/pqimg/raw/master/20210429150754.png)

​		获取选中条目id:

在表格外添加一个< form>表单，提交数据时只会提交< form>内的表单项，而里面刚好只有复选框这个表单项。

并设置name和value（设置为选中条目的数据的id），设置value提交到DelSelectedServlet中

```jsp
<%--给信息展示列表外面添加一个表单，用来提交被选中的多选表单项--%>
    <form  action="${pageContext.request.contextPath}/delSelectedServlet" method="post" id="formSelected">
    <table border="1" class="table table-bordered table-hover">

        <tr class="success">
            <th><input type="checkbox" id="firstCb"></th>
            <th>编号</th>
            <th>姓名</th>
            <th>性别</th>
            <th>年龄</th>
            <th>籍贯</th>
            <th>QQ</th>
            <th>邮箱</th>
            <th>操作</th>
        </tr>
        <c:forEach items="${requestScope.users}" varStatus="s" var="user">
            <tr>
                <td><input type="checkbox" name="uid" value="${user.id}"></td> <!--每条数据的复选框-->
                <td>${s.count}</td>
                <td>${user.name}</td>
                <td>${user.gender}</td>
                <td>${user.age}</td>
                <td>${user.address}</td>
                <td>${user.qq}</td>
                <td>${user.email}</td>
                <td><a class="btn btn-default btn-sm" href="${pageContext.request.contextPath}/findUserServlet?id=${user.id}">修改</a>&nbsp;
<%--                    点击删除按钮，进入删除的Servlet,并传入主键--%>
                    <a class="btn btn-default btn-sm" id="del_btn" href="javascript:deleteUser(${user.id});">删除</a></td>
            </tr>
        </c:forEach>


    </table>
    </form>

<script>
 window.onload=function () {
                //给删除选中按钮添加单击事件
                document.getElementById("delSelected").onclick = function () {
                    if (confirm("你确定要删除吗？")) {
                    //表单提交
                    document.getElementById("formSelected").submit();
                }}}
    
  window.onload=function () { /*全选*/
            //获取第一个复选框
            document.getElementById("firstCb").onclick=function () {
                //获取下边列表所有复选框
                 var cbs = document.getElementsByName("uid");
                 //遍历
                for (var i = 0; i < cbs.length; i++) {
                    //设置这些cbs[i]的checked状态 = firstCb.checked
                    cbs[i].checked=this.checked;
                }} }
</script>

```

```JAVA
@WebServlet("/delSelectedServlet")
public class DelSelectedServlet extends HttpServlet {
    protected void doPost(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {

        //获取被选中的复选框数据id
        String[] uids = request.getParameterValues("uid");
        //调用service删除
        UserService service=new UserServiceImpl();
        service.delSelected(uids);

        //跳转到查询所以的Servlet
        response.sendRedirect(request.getContextPath()+"/userLiseServlet");

    }

    protected void doGet(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
        this.doPost(request, response);
    }
}
```

```Java
//UserServiceImpl实现类重写service接口新增方法，然后遍历id数组，调用UserDaoImpl内的删除对应id的方法(就是前面单击删除的操作)
@Override
public void delSelected(String[] uid) {
   if (uid !=null && uid.length!=0 ) {
            //遍历复选框id数组
            for (String id : uid) {
                dao.delectId(Integer.parseInt(id));
            }
        }
}
```

#### 		**2、分页查询**

![image-20210430130521261](https://gitee.com/panqiyi/pqimg/raw/master/20210430130521.png)

![image-20210430131538889](https://gitee.com/panqiyi/pqimg/raw/master/20210430131539.png)

//javaBean

```java
/*分页对象*/
public class PageBean<T> { //泛型方便复用，如商品列表等等
    private int totalCount;  //总记录数
    private int totalPage;  //总页码
    private List<T> list;  //每页的数据
    private int currentPage;  //当前页码
    private int rows;  //每页显示的记录数
    //省略get/set和toString()
    }
```

```java
//Servlet
@WebServlet("/findUserByPageServlet")
public class FindUserByPageServlet extends HttpServlet {
    protected void doPost(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {

        //获取当前页码
        String currentPage = request.getParameter("currentPage");
        //获取每页显示的记录数
        String rows = request.getParameter("rows");

        //优化前端页码刚跳转到 list.jsp页时 currentPage与rows 为""或空的空指针异常
        if (currentPage==null || "".equals(currentPage)){
            currentPage="1";
        }
        if (rows==null || "".equals(rows)){
            rows="6";
        }

        //调用 service 查询
        UserService service=new UserServiceImpl();
        PageBean<User> pb=service.findUserByPage(currentPage,rows);


        //将PageBean存入request
        request.setAttribute("pb",pb);
        //转发到list.jsp
        request.getRequestDispatcher("/list.jsp").forward(request,response);
    }

    protected void doGet(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
        this.doPost(request, response);
    }
}
```

```Java
//Service实现类添加的方法
@Override
public PageBean<User> findUserByPage(String _currentPage, String _rows) {
    int currentPage=Integer.parseInt(_currentPage);
    int rows=Integer.parseInt(_rows);

    // 1、创建空的PageBean对象
    PageBean<User> pb = new PageBean<>();
    // 2、设置参数
    pb.setCurrentPage(currentPage); //当前页数
    pb.setRows(rows);  //每页数据条数

    //3、调用dao查询总记录数
    int totalCount=dao.findTotalCount();
    pb.setTotalCount(totalCount);
    //4、调用dao查询List集合
        //计算开始的记录索引 =（当前页码-1）*每页显示条数
    int start = (currentPage-1)*rows;
    List<User> list=dao.findByPage(start,rows);
    pb.setList(list);

    //5、计算总页码
    int totalPage=(totalCount%rows) == 0 ? totalCount/rows : (totalCount/rows)+1;
    pb.setTotalPage(totalPage);

    return pb;
}
```

```Java
//Dao实现类
@Override
public int findTotalCount() {  //查询总记录数
    String sql="select count(*) from user";
    return template.queryForObject(sql,Integer.class);
}

@Override
public List<User> findByPage(int start, int rows) { //分页查询每页数据
    String sql="select * from user limit ? , ?";
    return template.query(sql,new BeanPropertyRowMapper<User>(User.class),start,rows);
}
```

前端：

将index.jsp的链接到分页的Servlet中（注意，跳转时未传送currentPage和rows，所以Servlet里面解决了这个问题）

```jsp
<a
        href="${pageContext.request.contextPath}/findUserByPageServlet" style="text-decoration:none;font-size:33px">查询所有用户信息
</a>
```

分页展示页面：

```jsp
<script>
        
            function disabled() { //在第一页点上一页无效，在最后一页点下一页无效
                if (${pb.currentPage==1}){
                    document.getElementById("a_begin").href="javascript:void(1)"
                }
                if (${pb.currentPage==pb.totalPage}){
                    document.getElementById("a_end").href="javascript:void(${pb.totalPage})"
                }
            }

    </script>
</head>
<body>
<div class="container">
    <%--省略了信息展示（遍历的是分页的List），这里只说分页--%>
    <%--分页--%>
    <!--该分页样式为bootstrap的分页组件-->
    <div>
        <nav aria-label="Page navigation">
            <ul class="pagination">
                <!--上一页字符-->
                <!--如果当前页面=1 ，则设置class="disabled" 即bootstrap中的禁止鼠标样式-->
                <li <c:if test="${pb.currentPage==1}">class="disabled"</c:if>>
                    <a id="a_begin" onclick="disabled();" href="${pageContext.request.contextPath}/findUserByPageServlet?currentPage=${pb.currentPage-1}&rows=6" aria-label="Previous">
                        <span aria-hidden="true">&laquo;</span>
                    </a>
                </li>

			<!--   1、显示全部页数-->
                <%--<c:forEach begin="1" end="${pb.totalPage}" var="i">
                    <li <c:if test="${pb.currentPage==i}"> class="active"</c:if>><a href="${pageContext.request.contextPath}/findUserByPageServlet?currentPage=${i}&rows=6">${i}</a></li>
                </c:forEach>--%>

			<!--2、显示一个页数--%>
                    <%--<li <c:if test="${pb.currentPage==pb.currentPage}"> class="active"</c:if>><a href="${pageContext.request.contextPath}/findUserByPageServlet?currentPage=${pb.currentPage}&rows=6">${pb.currentPage}</a></li>--%>

                <1--显示3个页数-->
        		<!--如果当前页>=2， 则显示前一页-->
                <c:if test="${pb.currentPage>=2}">
                <li ><a href="${pageContext.request.contextPath}/findUserByPageServlet?currentPage=${pb.currentPage-1}&rows=6">${pb.currentPage-1}</a></li>
                </c:if>
				<!--当前页-->
        		<!--如果点击的当前页=数据库返回的当前叶，当前页面其样式不同于其他页面选项-->
                <li <c:if test="${pb.currentPage==pb.currentPage}"> class="active"</c:if>><a href="${pageContext.request.contextPath}/findUserByPageServlet?currentPage=${pb.currentPage}&rows=6">${pb.currentPage}</a></li>
				<!--当前页<=最后一页时，显示最后一页-->
                <c:if test="${pb.currentPage<=pb.totalPage-1}">
                <li ><a href="${pageContext.request.contextPath}/findUserByPageServlet?currentPage=${pb.currentPage+1}&rows=6">${pb.currentPage+1}</a></li>
                </c:if>

<!-------------  - -  - -  -------->
    			<!--下一页字符-->
                <li <c:if test="${pb.currentPage==pb.totalPage}">class="disabled"</c:if>>
                    <a id="a_end" onclick="disabled();" href="${pageContext.request.contextPath}/findUserByPageServlet?currentPage=${pb.currentPage+1}&rows=6" aria-label="Next">
                        <span aria-hidden="true">&raquo;</span>
                    </a>
                </li>

                <span style="margin-left: 5px;font-size: 25px">
                    共${pb.totalCount}条记录，共${pb.totalPage}页
                </span>
            </ul>
        </nav>
    </div>
```

1、显示全部页数选项

<img src="https://gitee.com/panqiyi/pqimg/raw/master/20210430223935.png" alt="image-20210430223935258" style="zoom:80%;" />

2、显示一个页数

<img src="https://gitee.com/panqiyi/pqimg/raw/master/20210430224150.gif" alt="53" style="zoom:80%;" />

3、显示三个页数

<img src="https://gitee.com/panqiyi/pqimg/raw/master/20210430224443.gif" alt="54" style="zoom:80%;" />

**3、复杂条件查询**

![image-20210501212607619](https://gitee.com/panqiyi/pqimg/raw/master/20210501212607.png)

将分页的Servlet添加由条件查询传来的参数map集合对象，将对象传入service和dao进一步操作

```java
@WebServlet("/findUserByPageServlet")
public class FindUserByPageServlet extends HttpServlet {
    protected void doPost(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {

        //设置编码
        request.setCharacterEncoding("utf-8");
        //获取当前页码
        String currentPage = request.getParameter("currentPage");
        //获取每页显示的记录数
        String rows = request.getParameter("rows");

        //优化前端页码刚跳转到 list.jsp页时 currentPage与rows 为""或空的空指针异常
        if (currentPage==null || "".equals(currentPage)){
            currentPage="1";
        }
        if (rows==null || "".equals(rows)){
            rows="6";
        }

        //获取复杂条件查询表单数据参数的map集合----request获取搜索表单参数
        Map<String, String[]> condition = request.getParameterMap();

        //调用 service 查询
        UserService service=new UserServiceImpl();
        PageBean<User> pb=service.findUserByPage(currentPage,rows,condition);//----添加传入map参数对象（alt+enter修改方法参数）

        //将PageBean存入request
        request.setAttribute("pb",pb);
        //将map集合存储到request中用于搜索表单回显-----
        request.setAttribute("condition",condition);
        //转发到list.jsp
        request.getRequestDispatcher("/list.jsp").forward(request,response);
    }
    protected void doGet(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
        this.doPost(request, response);
    }
}
```

```Java
//service实现类的对应分页查找方法，在调用dao实现类操作数据库时都传入map参数对象
@Override
public PageBean<User> findUserByPage(String _currentPage, String _rows, Map<String, String[]> condition) {
    int currentPage=Integer.parseInt(_currentPage);
    int rows=Integer.parseInt(_rows);


    // 1、创建空的PageBean对象
    PageBean<User> pb = new PageBean<>();
    // 2、设置参数
    pb.setCurrentPage(currentPage); //当前页数
    pb.setRows(rows);  //每页数据条数

    //3、调用dao查询总记录数
    int totalCount=dao.findTotalCount(condition); //----传map参数对象
    pb.setTotalCount(totalCount);
    //4、调用dao查询List集合
        //计算开始的记录索引 =（当前页码-1）*每页显示条数
    int start = (currentPage-1)*rows;
    List<User> list=dao.findByPage(start,rows,condition); //----传map参数对象
    pb.setList(list);

    //5、计算总页码
    int totalPage=(totalCount%rows) == 0 ? totalCount/rows : (totalCount/rows)+1;
    pb.setTotalPage(totalPage);

    return pb;
}
```

dao实现类对应被调用访问数据库的方法

```Java
@Override
public int findTotalCount(Map<String, String[]> condition) {  //查询记录数

    //定义模板初始化sql
    String sql="select count(*) from user where 1=1 "; //1=1为恒等式，方便sql代码拼接
    StringBuilder sb = new StringBuilder(sql);
    //遍历map,拿出查询条件的参数。
    Set<String> keySet = condition.keySet();
    //存储参数的值value集合List
    List<Object> params=new ArrayList<>();
    for (String key : keySet) {
        //先排除 当前页数(currentPage)和 每页展示数据条数(rows) 参数
        if ("currentPage".equals(key) || "rows".equals(key)){
            continue;
        }
        String value = condition.get(key)[0]; //为什么是：get(key)[0]，因为request.getParameterMap()返回的值为String[]

        //判断value是否有值，有值则添加sql
        if (value!=null && !"".equals(value)) {
            sb.append(" and " + key + " like ? ");
            params.add( "%" + value + "%");
        }
    }

    //System.out.println(sb.toString());

    return template.queryForObject(sb.toString(),Integer.class,params.toArray());
    //Integer.class ： 返回Integer包装类，自动自动拆箱
    //params.toArray() : list集合转换为数组，将自动将数据内值赋值给?
}

@Override
public List<User> findByPage(int start, int rows, Map<String, String[]> condition) { //分页查询每页数据

    //定义模板初始化sql
    String sql="select * from user where 1=1 "; //1=1为恒等式，方便sql代码拼接
    StringBuilder sb = new StringBuilder(sql);
    //遍历map,拿出查询条件的参数。
    Set<String> keySet = condition.keySet();
    //存储参数的值value集合List
    List<Object> params=new ArrayList<>();
    for (String key : keySet) {
        //先排除 当前页数(currentPage)和 每页展示数据条数(rows) 参数
        if ("currentPage".equals(key) || "rows".equals(key)){
            continue;
        }
        String value = condition.get(key)[0]; //为什么是：get(key)[0]，因为request.getParameterMap()返回的值为String[]

        //判断value是否有值，有值则添加sql
        if (value!=null && !"".equals(value)) {
            sb.append(" and " + key + " like ? ");
            params.add("%"+value+"%");
        }
    }

    //添加分页查询
    sb.append("limit ? , ?");
    //添加分页查询参数值
    params.add(start);
    params.add(rows);
    //System.out.println(sb.toString());

    return template.query(sb.toString(),new BeanPropertyRowMapper<User>(User.class),params.toArray());
}
```

前端jsp的list.jsp页面：

<img src="https://gitee.com/panqiyi/pqimg/raw/master/20210502095904.png" alt="image-20210502095904535" style="zoom:80%;" />

```jsp
<div style="float: left">
    <%--多条件复杂查询表单--%>
    <!--设置表单提交数据的地址-->
    <form class="form-inline" action="${pageContext.request.contextPath}/findUserByPageServlet" method="post">
        <div class="form-group">
            <!--注意表单必要的设置name属性，否则无法提交数据，value用于回显servlet存储来的参数，condition.name[0]是因为request.getParameterMap()返回的value为数组-->
            <label for="exampleInputName2">姓名</label>
            <input type="text" class="form-control" value="${condition.name[0]}" name="name" id="exampleInputName2" >
        </div>
        <div class="form-group">
            <label for="exampleInputEmail2">籍贯</label>
            <input type="text" class="form-control" value="${condition.address[0]}"name="address" id="exampleInputEmail2">
        </div>
        <div class="form-group">
            <label for="exampleInputEmail3">邮箱</label>
            <input type="text" class="form-control" value="${condition.email[0]}" name="email" id="exampleInputEmail3">
        </div>
        <button type="submit" class="btn btn-default">查询</button>
    </form>
</div>


<!--分页的样式要传条件查询表单的参数去servlet，否则点击分页条就会跳到普通的分页而取消了条件查询-->
<div>
        <nav aria-label="Page navigation">
            <ul class="pagination">
                <!--上一页-->
                <li <c:if test="${pb.currentPage==1}">class="disabled"</c:if>>
                    <a id="a_begin" onclick="disabled();" href="${pageContext.request.contextPath}/findUserByPageServlet?currentPage=${pb.currentPage-1}&rows=6&name=${condition.name[0]}&address=${condition.address[0]}&email=${condition.email[0]}" aria-label="Previous">
         <!--就是传入 &name=${condition.name[0]}&address=${condition.address[0]}&email=${condition.email[0]} -->
                        <span aria-hidden="true">&laquo;</span>
                    </a>
                </li>

<%--                1、显示全部页数--%>
                <%--<c:forEach begin="1" end="${pb.totalPage}" var="i">
                    <li <c:if test="${pb.currentPage==i}"> class="active"</c:if>><a href="${pageContext.request.contextPath}/findUserByPageServlet?currentPage=${i}&rows=6">${i}</a></li>
                </c:forEach>--%>

<%--                2、显示一个页数--%>
                    <li <c:if test="${pb.currentPage==pb.currentPage}"> class="active"</c:if>><a href="${pageContext.request.contextPath}/findUserByPageServlet?currentPage=${pb.currentPage}&rows=6&name=${condition.name[0]}&address=${condition.address[0]}&email=${condition.email[0]}">${pb.currentPage}</a></li>

                
<%--         - -  - -  - ------%>
			<!--下一页-->
                <li <c:if test="${pb.currentPage==pb.totalPage}">class="disabled"</c:if>>
                    <a id="a_end" onclick="disabled();" href="${pageContext.request.contextPath}/findUserByPageServlet?currentPage=${pb.currentPage+1}&rows=6&name=${condition.name[0]}&address=${condition.address[0]}&email=${condition.email[0]}" aria-label="Next">
                        <span aria-hidden="true">&raquo;</span>
                    </a>
                </li>

                <span style="margin-left: 5px;font-size: 25px">
                    共${pb.totalCount}条记录，共${pb.totalPage}页
                </span>
            </ul>
        </nav>
    </div>
```



4、测试

5、部署运维

