## Servlet

server  applet

### 概念

运行在服务器端的小程序

- servlet就是一个接口，定义了Java类被浏览器访问(tomcat识别)的规则。
- 将来我们自定义一个类，实现Servlet接口，复写方法。

### 快速入门

1、创建JavaEE项目

2、定义一个类，实现Servlet接口

```Java
public class Servlet01 implements Servlet 
```

3、实现接口中的抽象方法

4、配置Servlet

​		<font color=red>在web.xml中配置</font>

![image-20210118202325436](https://gitee.com/panqiyi/pqimg/raw/master/20210118202325.png)

```xml
<!--Servlet的配置-->
    <servlet>
        <servlet-name>demo1</servlet-name><!--设置名称-->
        <servlet-class>cn.web.servlet.Servlet01</servlet-class><!--文件路径，全类名-->
    </servlet>

    <servlet-mapping>
        <servlet-name>demo1</servlet-name> <!--对demo1的映射-->
        <url-pattern>/demo1</url-pattern><!--设置资源路径名：/demo1-->
    </servlet-mapping>
```

此时通过如下路径即可访问该类（资源文件路径，不是虚拟目录）

![image-20210118104012528](https://gitee.com/panqiyi/pqimg/raw/master/20210118104012.png)

### 执行原理

1、当服务器接收到客户端浏览器的请求后，会解析请求的URL路径，获取访问的Servlet的资源路径

2、查找web.xml文件，是否有对应的<url-pattern>标签体内容

3、如果有，则在找到对应的<servlet-class>全类名

4、tomcat会将字节码文件加载进内存，并且创建其对象

5、调用方法



### 生命周期（方法）

1、被创建：执行init方法，只执行一次

```
Servlet什么时候被创建？
- 默认情况下，第一次被访问时，Servlet被创建
- 可以配置执行Servlet的创建时机
	- 在web.xml中的<servlet>标签下配置
		1、第一次被访问时创建
			设置<load-on-startup>标签内的值为负数
		2、在服务器启动时创建
			设置<load-on-startup>标签内的值为0或正整数
Servlet的init方法，只执行一次，说明一个Servlet在内存中只存在一个对象，Servlet是单例的
	- 多个用户同时访问时可能存在线程安全问题
	- 解决：尽量不要在Servlet中定义成员变量，即使定义了成员变量，也不要修改值。
```

2、提供服务：执行service方法，执行多次（访问一次servlet就执行一次）

```
每次访问Servlet时,Service方法都会被调用一次
```

3、被销毁：执行destroy方法，执行一次

```
- Servlet被销毁时执行，服务器关闭时，Servlet被销毁
- 只有服务器正常关闭时，才会执行destroy方法
- destroy方法在Servlet被销毁前执行，一般用于释放资源
```

getServletInfo() ：获取Servlet的一些信息，版本，作者等等

getServletConfig() ：获取ServletConfig对象，（ServletConfig：Servlet的配置对象）



### Servlet 3.0：注解配置

好处：支持注解配置，可以不需要web.xml了

**步骤：**

1、创建JavaEE项目，选择Servlet的版本3.0以上，可以不创建web.xml

2、定义一个类，实现Servlet接口

3、重写方法

4、在类上使用@WebServlet注解，进行配置

			- @WebServlet("资源路径")

![image-20210118212015924](https://gitee.com/panqiyi/pqimg/raw/master/20210118212015.png)

![image-20210118212106477](https://gitee.com/panqiyi/pqimg/raw/master/20210118212106.png)

因为设置了虚拟路径为“/” 所以不用写虚拟路径



**工作空间项目  和  tomcat部署的web项目**

- tomcat真正访问的是“tomcat部署的web项目”，“tomcat部署的项目”对应着“工作空间项目” 的web目录下的所有资源

  ​		idea会为每一个部署的项目单独建立一份配置文件，在控制台中有路径：

  Using CATALINA_BASE:   "C:\Users\panqiyi\.IntelliJIdea2019.3\system\tomcat\_ideaJAVA"

- WEB-INF目录下的资源不能被浏览器直接访问



### Servlet体系结构

Servlet (接口) --> GenericServlet (抽象类) --> HttpServlet (抽象类)

- GenericServlet：将Servlet接口中其他的方法做了默认空实现，之将service() 方法作为抽象

  ​		将来定义Servlet类时，可以继承GenericServlet，实现service()方法即可，如需其他方法重写即可。

- HttpServlet：对http协议的一种封装，简化操作 (常用)

  ​		1、定义类继承HttpServlet

  ​		2、重写doGet和doPost方法

### 快速创建servlet

<img src="https://gitee.com/panqiyi/pqimg/raw/master/20210121104444.png" alt="image-20210121104444668" style="zoom: 80%;" />

<img src="https://gitee.com/panqiyi/pqimg/raw/master/20210121111109.png" alt="image-20210121111109111" style="zoom:80%;" />

然后得到一个有注解，继承HttpServlet，重写了doGet和doPost方法的类

我只需要将注解的负值修改即可，生成时的注解如下

![image-20210121111407811](https://gitee.com/panqiyi/pqimg/raw/master/20210121111407.png)

修改为我们自定义的资源路径：如`@WebServlet("/pqy")`



**资源路径定义**

1、一个Servlet可以定义多个访问路径：如   @WebServlet({"/d1","/d2","/d3"})

2、路径定义规则：

​	1. /xxx

 	2. /xxx/xxx：多层路径，目录结构
      	3. *.do  （ * 通配符 写什么都可以）



## HTTP



### 概念

Hyper  Text  Transfer  Protocol  超文本传输协议

- 传输协议：定义了 客户端和服务端通信时，发送数据的格式

- 特点：

  ​	1、基于TCP/IP的高级协议

  ​	2、默认端口号：80

  ​	3、基于请求/响应模型：一次请求对应一次响应

  ​	4、无状态的：每次请求之间相互独立，不能交互数据

- 历史版本：

   	1.0：每一次请求响应都会建立新的连接

  ​	 1.1：建立一次连接复用

### 请求消息数据格式

**1、请求行**

```
请求方式  请求url  请求协议/版本
GET  /login.html  HTTP/1.1

- 请求方式
	- HTTP协议有7中请求方式，常用的有2种
		GET:
			1、请求参数在请求行中，在url后
			2、请求的url长度有限制的
			3、不太安全
		POST:
			1、请求参数在请求体中
			2、请求的url长度没有限制
			3、相对安全
```

2、请求头：客户端浏览器告诉服务器一些信息

格式：请求头名称：请求头值

```
常见的请求头：
	1、User-Agent：浏览器告诉服务器，我访问你使用的浏览器版本信息
		可以在服务器端获取该头的信息，解决浏览器兼容性问题
	2、Referer：http://localhost/login.html
		告诉服务器，我(当前请求)从哪里来
		作用：1、防盗链  2、统计工作
```

3、请求空行

空行

4、请求体（正文）：封装POST请求消息的请求参数

![image-20210120115034276](https://gitee.com/panqiyi/pqimg/raw/master/20210120115034.png)



## Request

#### request对象和response对象的原理

			- request 对象和response 对象是由服务器创建的，我们来使用它
			- request对象是用来获取请求消息，response对象是来设置响应消息

![image-20210120134629181](https://gitee.com/panqiyi/pqimg/raw/master/20210120134629.png)

#### request对象继承体系结构

![image-20210121100851425](https://gitee.com/panqiyi/pqimg/raw/master/20210121100851.png)

#### request 功能

<font color="orange">1、获取请求消息数据</font>

​		**1、获取请求行数据：**

```
GET /day1/demo01?name=lisi HTTP/1.1
方法:
	1、获取请求方式 : GET
		String getMethod()
	2、获取虚拟目录 : /day1  (常用)
		String getContextPath()
	3、获取Servlet路径: /demo01
		String getServletPath()
	4、获取get方式请求参数: name=lisi
		String getQueryString()
	5、获取请求URI : /day1/demo01  (常用)
		String getRequestURI() : /day1/demo01
		StringBuffer getRequestURL() : http://localhost/day1/demo01
		URL：统一资源定位符:  http://localhost/day1/demo01  中华人民共和国
		URI：统一资源标识符:  /day1/demo01  共和国
	6、获取协议及版本 : HTTP/1.1
		String getProtocol()
	7、获取客户机的IP地址
		String getRemoteAddr()
		
 如：String method = request.getMethod();
        System.out.println(method);
```

​		**2、获取请求头数据**

```Java
// 请求头:user-agent 获取浏览器版本，后期用于解决兼容性问题
 String agent = request.getHeader("user-agent"); //getHeader()方法 返回对应请求头的值
        if (agent.contains("Chrome")){  //如果agent包含"Chrome"
            System.out.println("谷歌浏览器……");
        }else if (agent.contains("Firefox")){
            System.out.println("火狐浏览器……");
        }
```

```java
//请求头:referer 获取当前请求源地址, 用于防盗链
 String referer = request.getHeader("referer");
 if (referer!=null){
     if (referer.contains("/day")){ //源地址是否包含/day这个虚拟目录
         System.out.println("播放电影……");
     }else {
         System.out.println("想看电影？来day吧");
     }
 }
```

​	**3、获取请求体数据**

   - 请求体：只有POST请求方式，才有请求体，在请求体中封装了POST请求的请求参数

   - 步骤：

     ​		1、获取流对象 (方法)

     ​				BufferedReader  getReader() : 获取字符输入流，只能操作字符数据

     ​				ServletInputStream  getInputStream() :  获取字符输入流，可以操作所有类型数据

     ​		2、在从流中获取数据

     如下：

![image-20210122182346970](https://gitee.com/panqiyi/pqimg/raw/master/20210122182347.png)

```html
<form action="/day/request04" method="post">  <!--/day/request04：Servlet文件路径-->
    <input type="text" name="user" placeholder="请输入用户名"><br>
    <input type="password" name="password" placeholder="请输入密码"><br>
    <input type="submit" value="注册">
</form> <!--注册页面代码-->
```

```java
//在doPost()中 通过getReader()方法获取流对象，再从流中获取数据
BufferedReader br = request.getReader();
String line;
while ((line=br.readLine())!=null){
    System.out.println(line);
}
```

![image-20210122182906821](https://gitee.com/panqiyi/pqimg/raw/master/20210122182906.png)

<font color="orange">2、其他功能</font>

**1、获取请求参数通用方式 (get/post都可以)**

```
1、String  getParameter(String  name): 根据参数名称获取参数值 (常用)   
2、String[]  getParameterValues(String name): 根据参数名称获取参数值数组(如复选框)   hobby=song&hobby=game 
3、Enumeration<String>  getParameterNames(): 获取所有请求的参数名称
4、Map<String,String[]>  getParameterMap(): 获取所有参数的map集合 (常用)

因为get/post通用，所以doGet/doPost方法内获取参数的代码都一样
所以在其中一个方法内调用其他方法即可，如在doPost()方法中编写代码，doGet方法调用：this.doPost(request,response)
```

中文乱码问题：

- get 方式 : tomcat 8 已经将get方式乱码问题解决
- post  方式：会乱码
  		- 解决：在获取参数时，设置request的编码：request.setCharacterEncoding("utf-8");



**2、请求转发：一种在服务器内部的资源跳转方式**

​	1、步骤：

​			1、通过request对象获取请求转发器对象：RequestDispatcher  getRequestDispatcher(String  path)

​			2、使用RequestDispatcher对象来进行转发：forward(ServletRequest  request,ServletResponse  response)

```java
	request.getRequestDispatcher("/request06").forward(request,response);
//在/request05中跳转到另一个Servlet文件"/request06"
```

2、特点：

​			1、浏览器地址栏路径不发生变化

​			2、只能转发(跳转)到当前服务器内部资源中

​			3、跳转都是用原本的一次请求

**3、共享数据**

即数据通信，A资源跳转到B资源，在A中可以存储数据,B可以获取A存储的数据

- 域对象 :  一个有作用范围的对象，可以在范围内共享数据
- request域：代表一次请求的范围，一般用于请求转发的多个资源中共享数据
- 方法：

```
1、void  setAttribute(String name,boject obj) : 存储数据
2、Object  getAttribute(String name) : 通过键获取值
3、void  removeAttribute(String name) : 通过键移除键值对
```

```Java
 		request.setAttribute("np",686); //在资源路径“/request05”中存储数据
        request.getRequestDispatcher("/request06").forward(request,response); //跳转到"/request06"
        
         Object np = request.getAttribute("np"); //在"request06中获取资源"
        System.out.println(np);
```



**4、获取ServletContext**

- ServletContext  getServletContext()

  

## 登录案例

### 分析与实现



用户登录案例需求：

```
1.编写login.html登录页面
		username & password 两个输入框
2.使用Druid数据库连接池技术,操作mysql，day14数据库中user表
3.使用JdbcTemplate技术封装JDBC
4.登录成功跳转到SuccessServlet展示：登录成功！用户名,欢迎您
5.登录失败跳转到FailServlet展示：登录失败，用户名或密码错误
```

案例分析：

![image-20210124183539596](https://gitee.com/panqiyi/pqimg/raw/master/20210124183539.png)

案例实现：

1、创建一个javaEE项目

2、在web下创建一个 login.html 登录页面

![image-20210124184954308](https://gitee.com/panqiyi/pqimg/raw/master/20210124184954.png)

```html
<form action="/login_test/loginServlet" method="post"> <!--action值：虚拟目录和资源目录-->
        用户名:<input type="text" name="username"> <br>
        密码:<input type="password" name="password"><br>
        <input type="submit" value="登录">
    </form> <!-- 一个简单的登录页面 -->
```

3、将配置文件放到src下

```properties
driverClassName=com.mysql.jdbc.Driver
url=jdbc:mysql:///db4
username=root
password=pqy219
initialSize=5
maxActive=10
maxWait=3000
```

4、将依赖文件导入到web下的WEB-INF文件下的lib目录（没有自己创建）

![image-20210125193059302](https://gitee.com/panqiyi/pqimg/raw/master/20210125193059.png)

5、创建数据库环境

```sql
CREATE DATABASE db4;
CREATE TABLE USER(
	id INT PRIMARY KEY AUTO_INCREMENT, -- id
	username VARCHAR(32) UNIQUE NOT NULL, -- 用户名
	PASSWORD VARCHAR(32) NOT NULL -- 密码
); -- 先里面先添加了 username=笑春风 password=123
```

6、创建数据库表中的实体类  User

```java
package cn.pqy.domain; // 包
/**
 *  用户实体类
 */
public class User {
    private int id;
    private String username;
    private String password;

   // 省略get/set方法和toString()方法
}
```



7、创建Druid工具类

```java 
package cn.pqy.util; //包
public class JdbcUtil {
    private static DataSource ds;

    static {
        try {
            // 加载配置文件
            Properties pro = new Properties();
            InputStream is = JdbcUtil.class.getClassLoader().getResourceAsStream("druid.properties");
            pro.load(is);
            // 初始化连接池对象
            ds=DruidDataSourceFactory.createDataSource(pro);
        } catch (IOException e) {
            e.printStackTrace();
        } catch (Exception e) {
            e.printStackTrace();
        }
    }

    // 获取连接池对象
    public static DataSource getDataSource(){
        return ds;
    }

    // 获取连接对象
    public static Connection getConnection() throws SQLException {
        return ds.getConnection();
    }
}
```



8、创建操作数据库表中User的类  UserDao

```jaVA
package cn.pqy.dao; //包
public class UserDao {
    // 声明一个JdbcTemplate对象共用
    private JdbcTemplate template= new JdbcTemplate(JdbcUtil.getDataSource());

    //登录时只需要用户名和密码loginUser，但返回的是该用户表中的所有信息
    //如果在数据库中没有查询到对应用户与密码，则返回 null
    public User login(User loginUser){
        try {
            // 1、编写sql
            String sql="select * from user where username=? and password=?";
            //调用query方法
            User user = template.queryForObject(sql,
                    new BeanPropertyRowMapper<User>(User.class), //封装为对象
                    loginUser.getUsername(),  //给?赋值
                    loginUser.getPassword());

            return user;
        } catch (DataAccessException e) {
            e.printStackTrace();
            return null;
        }
    }
}
```



9、创建Servlet登录逻辑类 LoginServlet

```java
@WebServlet("/loginServlet")
public class LoginServlet extends HttpServlet {
    protected void doPost(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
        //1、设置编码
        request.setCharacterEncoding("utf-8");
        //2、获取请求参数
        String username = request.getParameter("username");
        String password = request.getParameter("password");
        //3、封装User对象
        User loginUser = new User();
        loginUser.setUsername(username);
        loginUser.setPassword(password);
        //4、调用UserDao类的login方法登录
        UserDao userDao = new UserDao();
        User user = userDao.login(loginUser);
        //5、判断user
        if (user!=null){
            //登陆成功
            //转发到登录成功资源文件
            request.setAttribute("user",user); //存储共享数据
            //转发
            request.getRequestDispatcher("/successServlet").forward(request,response);


        }else {
            //登录失败
            //转发到登录失败资源文件
            request.getRequestDispatcher("/failServlet").forward(request,response);
        }
    }

    protected void doGet(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
        this.doPost(request,response);
    }
}
```



10、创建转发Servelt类  登录成功/登录失败  

```Java
//登录成功页面
@WebServlet("/successServlet")
public class SuccessServlet extends HttpServlet {
    protected void doPost(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
        //设置编码
        response.setContentType("text/html;charset=utf-8");
        //获取request域中的共享对象
        User user = (User) request.getAttribute("user");
        String username = user.getUsername();
       response.getWriter().write("登录成功！"+username+",欢迎您");

    }

    protected void doGet(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
        this.doPost(request,response);
    }
}
```

```Java
//登录失败页面
@WebServlet("/failServlet")
public class failServlet extends HttpServlet {
    protected void doPost(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
        //设置编码
        response.setContentType("text/html;charset=utf-8");
        //在页面输出
       response.getWriter().write("登录失败，用户名或密码错误");
    }

    protected void doGet(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
        this.doPost(request,response);
    }
}
```

运行测试：

![50](https://gitee.com/panqiyi/pqimg/raw/master/20210126134139.gif)

![51](https://gitee.com/panqiyi/pqimg/raw/master/20210126134340.gif)

### BeanUtils 工具类， 简化封装请求参数

```java
		// 原本上面的Servlet登录逻辑类 LoginServlet 中封装请求参数
		//这样做需要一次次获取每一个参数值，再一一给对象赋值。当参数过多时就很麻烦。
		//2、获取请求参数
        String username = request.getParameter("username");
        String password = request.getParameter("password");
        //3、封装User对象
        User loginUser = new User();
        loginUser.setUsername(username);
        loginUser.setPassword(password);
```

使用BeanUtils 步骤：

1、导入jar包到web下的WEB-INF下的lib

![image-20210128121837132](https://gitee.com/panqiyi/pqimg/raw/master/20210128121837.png)

2、将上面的2、3步骤改为如下：

```Java
//2、获取所有请求参数
Map<String, String[]> map = request.getParameterMap();
//3.1、创建User对象
User loginUser = new User();
//3.2 使用BeanUtils封装
try {
    BeanUtils.populate(loginUser,map); //这一句代码有异常
} catch (IllegalAccessException e) {
    e.printStackTrace();
} catch (InvocationTargetException e) {
    e.printStackTrace();
}
```



#### JavaBean：标准的Java类

1、要求：

```
1、类必须被public修饰
2、必须提供空参的构造器
3、成员变量必须使用private修饰
4、提供公共的setter和getter方法

//像上面的User类就是javaBean
```

2、功能：封装数据



成员变量与属性的区别：

属性：setter和getter方法截取后的产物

例如：getUsername() ---> Username ---> username



BeanUtils工具类的方法：

```
1、setProperty()
2、getProperty()
	这两个方法操作的都是属性。一般情况下属性与成员变量名称相同。

3、populate(object  obj,Map  map) :  将map集合的键值对信息，封装到对应的JavaBean对象中
```



## Response

响应消息对象：服务器端发送给客户端的数据

**1、响应行**

```
1、组成格式：协议/版本  响应状态码  状态码描述
2、响应状态码：服务器告诉客户端浏览器本次请求和响应的一个状态
	- 状态码都是3位数字
	- 分类
		1、1xx : 服务器接收客户端消息，但没有接收完成，等待一段时间后，发送"一百多"状态码
		2、2xx : 成功。代表:200
		3、3xx : 重定向。代表: 302：重定向 ，304：访问缓存
		4、4xx : 客户端请求错误。
			代表：404：请求路径没有对应的资源
				 405：请求方式没有对应的doXxx方法
		5、5xx : 服务器错误，代表：500：服务器内部出现异常
```



**2、响应头**

```
1、格式： 头名称:值
2、常见的响应头：
		1、Content-Type : 服务器告诉客户端本次响应体数据格式以及编码格式
		2、Content-disposition : 服务器告诉客户端以什么格式打开响应体数据
			- 值：
				- in-line: 默认值，在当前页面内打开
				- attachment:以附件形式打开响应体。文件下载
```



**3、响应空行**

**4、响应体 ：**传输的数据

字符串格式如下：

![image-20210201174014211](https://gitee.com/panqiyi/pqimg/raw/master/20210201174014.png)

### response对象功能

功能：设置响应消息

**1、设置响应行**

```
格式：HTTP/1.1 200 ok
设置状态码方法：setStatus(int sc)
```

**2、设置响应头**

```
方法：setHeader(String name,String value)
```

**3、设置响应体**

```
步骤：
1、获取输出流方法
	- 字符输出流: PrintWriter  getWriter()
	- 字节输出流: ServletOutputStream  getOutputStream()

2、使用输出流，将数据输出到客户端浏览器
```



### 案例：

#### 1、重定向

<img src="https://gitee.com/panqiyi/pqimg/raw/master/20210205104058.png" alt="image-20210205104058557" style="zoom:80%;" />

```
//1、设置状态码302
resp.setStatus(302);
//2、设置响应头
resp.setHeader("location","/response02");

//简便方法
resp.sendRedirect("/response02");
```

**重定向和转发的区别**（redirect和forward的区别）

重定向的特点：

```
1、地址栏发生变化
2、重定向可以访问其他网址(服务器)资源
3、重定向是两次请求。不能使用request对象来共享数据
```

转发的特点：

```
1、地址栏路径不变
2、只能访问当前服务器下的资源
3、转发是一次请求，可以使用request对象来共享数据
```

###### 路径写法

![image-20210308230224508](https://gitee.com/panqiyi/pqimg/raw/master/20210308230224.png)

#### 2、服务器用字符/字节流输出数据到浏览器

​	1、字符输出流

```java
//1、告诉浏览器，服务器发送信息体数据的编码，让浏览器使用该编码，防止出现中文乱码问题
response.setHeader("content-type","text/html;charset=utf-8");

//简便的
response.setContentType("text/html;charset=utf-8");
//2、获取字符输出流
PrintWriter pw = response.getWriter();
//3、输出数据
pw.write("你好 ，世界");
```

​	2、字节输出流

```java
//设置编码
response.setContentType("text/html;charset=utf-8");
//获取字节流
ServletOutputStream sos = response.getOutputStream();
sos.write("hello".getBytes("utf-8")); //默认gbk
```



#### 3、验证码

如下，但实际开发一般都网上找交好看的验证码代码将其修改

```Java
int width = 100;
int height = 50;

//1.创建一对象，在内存中图片(验证码图片对象)
BufferedImage image = new BufferedImage(width,height,BufferedImage.TYPE_INT_RGB);


//2.美化图片
//2.1 填充背景色
Graphics g = image.getGraphics();//画笔对象
g.setColor(Color.PINK);//设置画笔颜色
g.fillRect(0,0,width,height);

//2.2画边框
g.setColor(Color.BLUE);
g.drawRect(0,0,width - 1,height - 1);

String str = "ABCDEFGHIJKLMNOPQRSTUVWXYZabcdefghigklmnopqrstuvwxyz0123456789";
//生成随机角标
Random ran = new Random();

for (int i = 1; i <= 4; i++) {
    int index = ran.nextInt(str.length());
    //获取字符
    char ch = str.charAt(index);//随机字符
    //2.3写验证码
    g.drawString(ch+"",width/5*i,height/2);
}


//2.4画干扰线
g.setColor(Color.GREEN);

//随机生成坐标点

for (int i = 0; i < 10; i++) {
    int x1 = ran.nextInt(width);
    int x2 = ran.nextInt(width);

    int y1 = ran.nextInt(height);
    int y2 = ran.nextInt(height);
    g.drawLine(x1,y1,x2,y2);
}


//3.将图片输出到页面展示
ImageIO.write(image,"jpg",response.getOutputStream());
```

**切换验证码**：

```Java
<script>
        /*
            分析：
                点击超链接或者图片，需要换一张
                1.给超链接和图片绑定单击事件

                2.重新设置图片的src属性值

         */
    window.onload = function(){ //加载页面
        //1.获取图片对象
        var img = document.getElementById("checkCode");
        //2.绑定单击事件
        img.onclick = function(){
            //加时间戳
            var date = new Date().getTime();

            img.src = "/day15/checkCodeServlet?"+date;
        }

    }

    </script>

</head>
<body>

    <img id="checkCode" src="/day15/checkCodeServlet" />

    <a id="change" href="">看不清换一张？</a>

</body>
```



## ServletContext对象

​	**1、概念：**代表整个web应用，可以和程序的容器(服务器)来通信

​	**2、获取：**

```Java
//1、通过request对象获取
ServletContext context1 = request.getServletContext();
//2、通过HttpServlet获取
ServletContext context2 = this.getServletContext();
```

```java
ServletContext context = this.getServletContext();
// 获取绝对路径目录(D:\PRoject\JavaWeb\out\artifacts……)
String serverPath = context.getRealPath("")
```

**3、功能：**

​			**1、获取MIME类型**

```
MIME类型：在互联网通信过程中定义的一种文件数据类型
	如格式：		大类型/小类型		text/html	image/jpeg
	获取方法: String  getMimeType(String file)
	
```

```java
//1、通过HttpServlet获取
ServletContext context = this.getServletContext();

//2、定义文件名
String filename="a.jpg";

//3、获取MIME类型
String mimeType = context.getMimeType(filename);
System.out.println(mimeType); //image/jpeg
```

​			**2、域对象：共享数据**

```
setAttribute(String name,Object value)    （键，存储的信息）
getAttribute(String name)      据键取值
removeAttribute(String name)   据键删值

```

**ServletContext对象范围：存储的共享数据所有用户都可以访问**

它与request对象共享数据的区别：

![image-20210316000726737](https://gitee.com/panqiyi/pqimg/raw/master/20210316000727.png)

​			**3、获取文件的真实(服务器)路径**

​					方法：String  getReadPath()

![image-20210317111317929](https://gitee.com/panqiyi/pqimg/raw/master/20210317111318.png)

```Java
//获取ServletContext对象
ServletContext context = this.getServletContext();

//访问web下的资源
String realPath = context.getRealPath("/b.txt");
System.out.println(realPath);

//访问WEB-INF下的资源
String realPath1 = context.getRealPath("/WEB-INF/c.txt");
System.out.println(realPath1);

//访问src下的资源；因为src下的文件都会copy一份到 WEB-INF\classes下
String realPath2 = context.getRealPath("/WEB-INF/classes/a.txt");
System.out.println(realPath2);
```



## 案例：文件下载

<img src="https://gitee.com/panqiyi/pqimg/raw/master/20210319164102.png" alt="image-20210319164102685" style="zoom:80%;" />

#### 代码实现：

![image-20210319164242477](https://gitee.com/panqiyi/pqimg/raw/master/20210319164242.png)

```html
<!--download.html-->
<body>
<a href="/day16/downloadServlet?filename=1.png">图片1</a>
<a href="/day16/downloadServlet?filename=adc.mp4">视频1</a>
</body>
```

```java
@WebServlet("/downloadServlet")
public class downloadServlet extends HttpServlet {
    protected void doPost(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {

        //1、获取请求参数，文件名称
        String filename = request.getParameter("filename");
        //2、使用字节输入流加载文件进内存
        //2.1、找到文件服务器路径
        ServletContext servletContext = this.getServletContext();
        String realPath = servletContext.getRealPath("/img/" + filename);
        //2.2、用字节流关联
        FileInputStream fis = new FileInputStream(realPath);

        //3、设置response响应头
        //3.1设置响应头类型：content-type
        String mimeType = servletContext.getMimeType(filename);//获取文件的mime类型
        response.setHeader("content-type",mimeType);
        //3.2设置响应头打开方式：content-disposition
        response.setHeader("content-disposition","attachment;filename="+filename);

        //4、将输入流的数据写出到输出流中
        ServletOutputStream sos = response.getOutputStream();
        byte[] buff = new byte[1024 * 8];
        int len=0;
        while ((len=fis.read(buff))!=-1){
            sos.write(buff,0,len);
        }
        fis.close();
    }

    protected void doGet(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {

        this.doPost(request,response);
    }
}
```

![image-20210319165157275](https://gitee.com/panqiyi/pqimg/raw/master/20210319165157.png)

#### 中文文件名问题

![image-20210319170645225](https://gitee.com/panqiyi/pqimg/raw/master/20210319170645.png)

**中文的文件名会出现无法显示或者乱码的情况：**

<img src="https://gitee.com/panqiyi/pqimg/raw/master/20210319195049.png" alt="image-20210319195049067" style="zoom:80%;" />

**解决方案：**

```
1、获取客户端使用的浏览器信息、
2、根据不同的版本信息，设置filename的编码方式不同
```

对于不同浏览器的编码方式，可用此工具类

链接：https://pan.baidu.com/s/1hKHOTwLdZICZhQmpkPTvMA 
提取码：3q4s 


```Java
//在第三步添加如下

//解决中文文件名问题
//1、获取user-agent请求头
String agent = request.getHeader("user-agent");
//2.使用工具类方法编码文件名即可
String fileName = DownLoadUtils.getFileName(agent, filename);

response.setHeader("content-disposition","attachment;filename="+fileName); //这里传入的是编码好的filename
```



<img src="https://gitee.com/panqiyi/pqimg/raw/master/20210320100327.png" alt="image-20210320100327801" style="zoom:80%;" />