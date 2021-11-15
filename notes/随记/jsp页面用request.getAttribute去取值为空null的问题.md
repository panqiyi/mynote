## jsp页面用request.getAttribute去取值为空的问题



Servlet后台

```

@WebServlet("/servlet")
public class Servlet extends HttpServlet {
    protected void doPost(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {

        request.setCharacterEncoding("utf-8");
        request.setAttribute("user","霓虹身体");
        request.getRequestDispatcher("list.jsp").forward(request,response);
    }

    protected void doGet(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
        this.doPost(request, response);
    }
}
```

jsp：

```

<%@ page contentType="text/html;charset=UTF-8" language="java" %>
<html>
<head>
    <title>Title</title>
</head>
<body>
<%=request.getAttribute("user")%>
</body>
</html>
```



启动服务器，访问资源

![image-20210427154436133](https://gitee.com/panqiyi/pqimg/raw/master/20210427154436.png)

出现问题：页面值为null

<font color=red>问题原因：直接访问了jsp页面，未访问后台的Servlet文件，就不会执行servlet中的request 数据共享，所以jsp中的request自然为空。</font>

![image-20210427155938037](https://gitee.com/panqiyi/pqimg/raw/master/20210427155938.png)



**问题解决：**

先访问后台Servlet文件，servlet会自动跳转到指定的jsp页面。

![image-20210427160119955](https://gitee.com/panqiyi/pqimg/raw/master/20210427160120.png)