## web项目路径问题

### 1、servlet转发到jsp路径问题:

```java
 //跳转到seach.jsp
request.getRequestDispatcher("/seach.jsp").forward(request,response);
```

当jsp页面在web下是子文件时是正确的：web > seach.jsp

![image-20210531225246261](https://gitee.com/panqiyi/pqimg/raw/master/20210531225246.png)

但是当jsp页面是在web下的文件夹里面是就会报错，启动服务器浏览器会显示404  :web > jsp > seach.jsp

![image-20210531225501446](https://gitee.com/panqiyi/pqimg/raw/master/20210531225501.png)

**解决：**将servlet的跳转路径添加文件夹目录

```java
 //跳转到seach.jsp
request.getRequestDispatcher("jsp/seach.jsp").forward(request,response);
```



### **2、jsp使用相对路径出现问题**

使用当前文件的相对路径容易出现问题，很多情况都不知道为什么，就比如我下面这个

<img src="https://gitee.com/panqiyi/pqimg/raw/master/20210531231853.png" alt="image-20210531231853330" style="zoom:67%;" />

```html
在jsp中用相对路径引入css资源
<link rel="stylesheet" href="../css/seach.css">
```

这个相对路径写的没问题吧！！ 不知道什么原因，后台跳转到这个jsp就会加载不到css，直接只运行这个jsp时css就是有用。下面是css没有用的网页效果

<img src="https://gitee.com/panqiyi/pqimg/raw/master/20210531232332.png" alt="image-20210531232332478" style="zoom:80%;" />

### 3、避免路径问题，使用绝对路径

先看看我设置项目的虚拟路径 ：/erhshou

![image-20210531233343896](https://gitee.com/panqiyi/pqimg/raw/master/20210531233344.png)

再看看浏览器是通过什么路径访问资源的

先看项目目录：

<img src="https://gitee.com/panqiyi/pqimg/raw/master/20210531234917.png" alt="image-20210531234917030" style="zoom: 80%;" />

访问login.jsp

![image-20210531234800974](https://gitee.com/panqiyi/pqimg/raw/master/20210531234801.png)

点击login.jsp访问后台servlet

![image-20210531235841821](https://gitee.com/panqiyi/pqimg/raw/master/20210531235841.png)

```java
@WebServlet("/myServlet") //servlet文件名（目录）
public class MyServlet extends HttpServlet {
    protected void doPost(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
        response.setContentType("text/html;charset=utf-8");
        response.getWriter().write("执行了！！");
    }

    protected void doGet(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
        this.doPost(request, response);
    }
}
```

**总结：**

```
访问web下的页面资源时：
本机ip地址:端口号/项目虚拟目录/web下文件目录
如：
	访问 web>login.jsp  (web下的jsp文件)
http://localhost:8080/erhshou/login.jsp
	访问 web/jsp/login.jsp  (web下的jsp文件夹下的jsp文件)
http://localhost:8080/erhshou/jsp/login.jsp

访问servlet资源时：
本机ip地址:端口号/项目虚拟目录/servlet名称
http://localhost:8080/erhshou/myServlet
```



那么我们绝对路径访问就是用  <font color='red'>本机ip地址:端口号/项目虚拟目录</font> 

如上面引入 css文件

```html
<!--相对路径-->
<link rel="stylesheet" href="../css/seach.css">
<!--绝对路径，这里就是寻找web/css/seach.css ;根据上面总结得-->
<link rel="stylesheet" href="http://localhost:8080/erhshou/css/seach.css">
```

上面那个绝对路径是不是有点复杂了

正是开始：



#### **1、EL表达式**

```
//这个获取项目的虚拟目录，因为运行http://localhost:8080浏览器自动添加
${pageContext.request.contextPath} 
```

login.jsp（上面有项目目录）

```html
<body>
<a href="${pageContext.request.contextPath}/myServlet">点击访问后台</a><br>

    绝对路径的虚拟目录：${pageContext.request.contextPath}
</body>
```

![image-20210601002550776](C:\Users\panqiyi\AppData\Roaming\Typora\typora-user-images\image-20210601002550776.png)



#### **2、使用basePath**

**配置：**在jsp头部添加绝对路径的变量

```jsp
<%@ page contentType="text/html;charset=UTF-8" language="java" isELIgnored="false" %>
<%@taglib prefix="c" uri="http://java.sun.com/jsp/jstl/core" %>

<%
    String path=request.getContextPath(); //项目虚拟路径 /erhshou
    // 获得项目完全路径（假设你的项目(虚拟路径)叫erhshouq，那么获得到的地址就是 http://localhost:8080/erhshou/）:    
    String basePath = request.getScheme()+"://"+request.getServerName()+":"+request.getServerPort()+path+"/";
%>    

<html>
```

**使用方式一：**每在跳转或者导入资源时，在前面调用 basePath 这个变量

```html
<link rel="stylesheet" href="<%basePath%>css/seach.css">
<a href="<%basePath%>myServlet">点击访问后台</a>
```

缺点：每一次跳转或导入都需要在前面添加 <%basePath%>

**使用方式二：**(头部添加配置一样的) 在 < head> 标签内添加 <base href="<%=basePath%>">  

```jsp
<head>
    <title>Title</title>
    
     <base href="<%=basePath%>">   basePath：对应jsp头部定义的绝对路径变量
</head>
```

在<head>中添加这个 `<base>` 标签后，每一次跳转或导入都不用在前面添加 <%basePath%>

意思是 所有路径都相对于 basePath (即 http://localhost:8080/erhshou/) 来访问

```html
<link rel="stylesheet" href="css/seach.css">
<a href="myServlet">点击访问后台</a>
```

缺点：需要在每个页面配置路径变量 和定义< base>标签；(可以去idea设置jsp生成模板，添加到模板中即可，这样新建的jsp都定义好了路径变量和<base>标签了)



#### **3、引入一个提供绝对路径的jsp资源文件**

![image-20210601141437136](https://gitee.com/panqiyi/pqimg/raw/master/20210601141437.png)

```jsp
<!--common.jsp-->
<%@ page contentType="text/html;charset=UTF-8" language="java" %>
<%@ taglib prefix="c" uri="http://java.sun.com/jsp/jstl/core" %>
<c:set var="path" scope="request">${pageContext.request.contextPath}</c:set>
```

后面的jsp页面都引用这个配置路径的jsp，然后就可以使用el表达式使用绝对路径

jsp引入

```jsp
<%@ include file="/WEB-INF/jsp/basePath/common.jsp" %>
```

使用：

```jsp
<link rel="stylesheet" href="${path}/css/login.css">
<a href="${path}/myServlet">点击访问后台</a><br>
```

