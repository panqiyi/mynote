## Filter&Listener 过滤器&监听器

## Filter ：过滤器

### 概念

web中的过滤器：当访问服务器的资源时，过滤器可以将请求拦截下来，完成一些特殊的功能。

过滤器的作用：

​		一般用于完成通用的操作。如：登录验证(登录了才能访问资源)，统一编码处理，敏感字符过滤…

### 快速入门

​	1、步骤：

​			1、定义一个类，实现接口Filter

![image-20210502110801353](https://gitee.com/panqiyi/pqimg/raw/master/20210502110801.png)

​			2、复写方法

​			3、配置拦截路径

​					1、web.xml

​					2、注解

```java
@WebFilter("/*") //访问所有资源前都会先访问过滤器
public class FilterDemo1 implements Filter {
    @Override
    public void init(FilterConfig filterConfig) throws ServletException {

    }

    @Override
    public void doFilter(ServletRequest servletRequest, ServletResponse servletResponse, FilterChain filterChain) throws IOException, ServletException {

        System.out.println("Filter成功被调用……");

        //放行
        filterChain.doFilter(servletRequest, servletResponse);
    }

    @Override
    public void destroy() {

    }
}
```



### 过滤器的细节

​	**1、web.xml配置**

![image-20210502211241522](https://gitee.com/panqiyi/pqimg/raw/master/20210502211241.png)

```xml
<filter>
    <filter-name>demo1</filter-name>
    <filter-class>cn.pay.filter.FilterDemo1</filter-class>
</filter>
<filter-mapping>
    <filter-name>demo1</filter-name>
    <!--拦截路径-->
    <url-pattern>/*</url-pattern>
</filter-mapping>
```

​	**2、过滤器执行流程**

​			1、执行过滤器 ----> 2、执行放行后的资源 ----> 3、回来执行过滤器放行代码下边的代码

​	**3、过滤器生命周期方法**

​			1、init : 在服务器启动后，会创建Filter对象，然后调用init方法。只执行一次。用于加载资源

​			2、doFilter ：每一次请求被拦截资源时，会执行。执行多次

​			3、deStroy ：在服务器关闭后，Filter对象被销毁。如果服务器正常关闭，则会执行deStroy方法。只执行一次。用于释放资源

​	**4、过滤器配置详解**

   - 拦截路径配置 ：

     ​		1、具体资源路径 ： `/index.jsp`	只访问index.jsp资源时。过滤器才会被执行。

     ​		2、拦截目录：` /user/*  `		访问 /user 下的所有资源时，过滤器都会被执行。

     ![image-20210502225241278](https://gitee.com/panqiyi/pqimg/raw/master/20210502225241.png)

     ```Java
     //使两个servlet都带一个父目录user,那么访问这两个资源都会执行过滤器
     @WebServlet("/user/servlet02")
     ```

     ​		3、后缀名拦截：`*.jsp`		访问所有后缀名为jsp资源时，过滤器都会被执行

     ​		4、拦截所有资源 ：`/*`

   - 拦截方式配置：拦截资源被访问的方式

     ​	1、设置dispatcherTypes属性

     ```
     1、REQUEST : 默认值。浏览器直接访问资源
     2、FORWARD : 转发访问资源
     3、INCLUDE : 包含访问资源
     4、ERROR : 错误跳转资源
     4、ASYNC : 异步访问资源
     ```

```java
//@WebFilter("/*") == @WebFilter(value="/*")
    //浏览器直接请求index,jsp资源时，该过滤器会被执行
//@WebFilter(value = "index.jsp",dispatcherTypes = DispatcherType.REQUEST)
    //只有转发访问index.jsp资源时，该过滤器才会被执行
//@WebFilter(value = "index.jsp",dispatcherTypes = DispatcherType.FORWARD)
    //浏览器直接请求index.jsp或者转发访问index.jsp。该过滤器才会被执行
@WebFilter(value = "index.jsp",dispatcherTypes = {DispatcherType.REQUEST,DispatcherType.FORWARD})   
```

- web.xml配置

  ```xml
  <filter>
      <filter-name>demo1</filter-name>
      <!--过滤器位置-->
      <filter-class>cn.pay.filter.FilterDemo1</filter-class>
  </filter>
  <filter-mapping>
      <filter-name>demo1</filter-name>
      <!--拦截路径-->
      <url-pattern>/*</url-pattern>
      <!--拦截的访问方式-->
      <dispatcher>FORWARD</dispatcher>
      <dispatcher> REQUEST</dispatcher>
  </filter-mapping>
  ```

**5、过滤器链（配置多个过滤器）**

		- 执行顺序：如果有两个过滤器，过滤器1和过滤器2

```
 过滤器1 --> 过滤器2 --> 资源执行 --> 过滤器2 --> 过滤器1
```

- 多个过滤器执行先后顺序问题：

  ​	1、注解配置：按照类名的字符串比较规则比较，值小的先执行

```
过滤器类名左到右比较，小的先执行。如下：
	FilterDemo3 和 FilterDemo5 ，FilterDemo3会先执行
	FilterDemo4 和 FilterDemo14, FilterDemo14会先执行(左到右4和1先比较，1小所有先执行14)
	AFilter BFilter , AFilter会先执行
```

​			2、web.xml 配置：<filter-mapping>谁定义在上边，谁先执行

### 案例：登录验证

要求：

在前面jsp最后一个案例的基础上，添加过滤器，在访问其他资源页面时会先判断登录没有，没有登录的话会跳转到登录页面。

（先判断是否是登录页面的相关资源，如果是登陆页面就直接放行而无需再次跳转到登录页面）

![image-20210503204854767](https://gitee.com/panqiyi/pqimg/raw/master/20210503204854.png)

![image-20210503205129165](https://gitee.com/panqiyi/pqimg/raw/master/20210503205129.png)

```java
@WebFilter("/*")
public class LoginFilter implements Filter {
    public void destroy() {
    }

    public void doFilter(ServletRequest req, ServletResponse resp, FilterChain chain) throws ServletException, IOException {
        //1、强制转换 （因为很多方法是在其子接口HttpServletRequest）
        HttpServletRequest request= (HttpServletRequest) req;
        //2、获取请求资源的路径(URI)
        String uri = request.getRequestURI();
        //3、判断请求路径是否包含登录相关资源路径，注意还要排除 css/js/图片、验证码等资源
        //因为登录页面样式包含了这些css/js/验证码资源
        //如做网站首页可以先浏览，也可添加首页路径
        if (uri.contains("/login.jsp") || uri.contains("/loginServlet") || uri.contains("/css") || uri.contains("/js") || uri.contains("/checkCodeServlet")){
            //包含，则该请求路径为登录页面及其相关资源。放行
            chain.doFilter(req,resp);
        }else {
            //不包含，需要验证用户是否登录
            //4、从获取session中获取user (user为登录成功时servlet存储user对象在session中)
            Object user = request.getSession().getAttribute("user");
            if (user!=null){
                //登录了。放行
                chain.doFilter(req,resp);
            }else {
                //没登录，跳转到登录页面
                request.setAttribute("login_msg","您尚未登录，请登录");
                request.getRequestDispatcher("/login.jsp").forward(req,resp);
            }
        }

        //chain.doFilter(req, resp);
    }

    public void init(FilterConfig config) throws ServletException {

    }

}
```



### 案例：过滤敏感词

需求：

​	1、对jsp最后的案例录入的数据进行敏感词过滤

​	2、敏感词汇参考 《敏感词汇.txt》

​	3、如果是敏感词汇，替换为 ***

分析：对request对象进行增强（因为request对象没有修改参数值的功能）

![image-20210503210359053](https://gitee.com/panqiyi/pqimg/raw/master/20210503210359.png)

- 增强对象功能：

    - 设计模式：一些通用的解决固定问题的方式

    - 增强对象功能：装饰模式；代理模式；

    - **代理模式：**

      概念：

      ​	1、真实对象：被代理的对象

      ​	2、代理对象：代理真实对象，增强功能

      ​	3、代理模式：代理对象代理真实对象，达到增强真实对象功能的目的

      实现方式：

      ​	1、静态代理：有一个类文件描述代理模式

      ​	2、动态代理：在内存中形成代理类

      ​			实现步骤：

      ​				1、代理对象和真实对象实现相同接口

      ​				2、代理对象 = Proxy.newProxyInstance();

      ​				3、使用代理对象调用方法。

      ​				4、增强方法

      **动态代理：代理对象实现方式例子：**

      ![image-20210504204421531](https://gitee.com/panqiyi/pqimg/raw/master/20210504204421.png)

      ![image-20210504195006362](https://gitee.com/panqiyi/pqimg/raw/master/20210504195006.png)

```java
/*买电脑的接口*/
public interface SaleComputer {
    public String sale(double money);
    public void show();
}
```

```java
/*真实类*/
public class Lenovo implements SaleComputer {
    @Override
    public String sale(double money) {

        System.out.println("花了"+money+"元买了一台联想电脑...");
        return "联想电脑";
    }

    @Override
    public void show() {
        System.out.println("展示电脑....");
    }
}
```

```java
public class ProxyTest {

    public static void main(String[] args) {
        //1.创建真实对象
        Lenovo lenovo = new Lenovo();
        
        //2.动态代理增强lenovo对象
        /*
            三个参数：
                1. 类加载器：真实对象.getClass().getClassLoader()
                2. 接口数组：真实对象.getClass().getInterfaces() 保证了代理对象与lenovo真实对象实现自同一个接口
                3. 处理器：new InvocationHandler()

                固定格式：
         */
        SaleComputer proxy_lenovo = (SaleComputer) Proxy.newProxyInstance(lenovo.getClass().getClassLoader(), lenovo.getClass().getInterfaces(), new InvocationHandler() {

            /*
                代理逻辑编写的方法：代理对象调用的所有方法都会触发该方法执行
                    参数：
                        1. proxy:代理对象
                        2. method：代理对象调用的方法，被封装为的对象
                        3. args:代理对象调用的方法时，传递的实际参数
             */
            @Override
            public Object invoke(Object proxy, Method method, Object[] args) throws Throwable {
                System.out.println("该方法执行了....");
                /*System.out.println(method.getName()); //代理对象调用了哪个方法就打印哪个方法，如下面调用show就是show
                System.out.println(args[0]);*/

                //判断是否是sale方法
                if(method.getName().equals("sale")){
                    //是，就对该方法增强，然后返回
                    //1.增强参数
                    double money = (double) args[0];
                    money = money * 0.85;
                    System.out.println("专车接你....");
                    //使用真实对象调用该方法(否则代理对象无法调用的真实对象的方法)
                    String obj = (String) method.invoke(lenovo, money);
                    System.out.println("免费送货...");
                    //2.增强返回值
                    return obj+"_鼠标垫";
                }else{
                    //不是，则使动态代理对象能调用到新增方法
                    // ：invoke(真实对象obj, args) ：简单的说就是调用谁的方法用谁的对象,args为参数数组
                    //method.invoke(Object obj, args); 就是代理对象调用了真实对象的方法 
                    //其他方法就正常调用req的方法，method:代理对象调用的方法
                    Object obj = method.invoke(lenovo, args);
                    return obj;
                }
            }
        });

        //3.调用方法

       /* String computer = proxy_lenovo.sale(8000);
        System.out.println(computer);*/

       //动态代理对象会先这些增强的方法，然后执行原来真实对象方法的代码
        proxy_lenovo.show();
    }
}
```

**<继续过滤敏感词案例：增强request的getParameter系列方法>**

![image-20210504213353217](https://gitee.com/panqiyi/pqimg/raw/master/20210504213353.png)

```java
/*敏感词过滤*/
@WebFilter("/*")
public class SensitiveWordsFilter implements Filter {

    private List<String> list=new ArrayList<String>();
    public void init(FilterConfig config) throws ServletException { //启动服务器时加载一次，用于加载资源，不浪费内存

        //获取文件真实路径
        try {
            ServletContext servletContext = config.getServletContext();
            String realPath = servletContext.getRealPath("/WEB-INF/classes/敏感词汇.txt"); //src下文件
            //读取文件
            BufferedReader br = new BufferedReader(new FileReader(realPath));
            //将文件的每一行数据添加到list集合中
            String line = null;
            while ((line=br.readLine())!=null){
                list.add(line);
            }
            br.close();
        } catch (IOException e) {
            e.printStackTrace();
        }

    }

    public void doFilter(ServletRequest req, ServletResponse resp, FilterChain chain) throws ServletException, IOException {
        //1、创建代理对象，增强getParameter方法（返回value为String字符，getParameterValues为数组，getParameterMap为map集合）
        ServletRequest proxy_req = (ServletRequest) Proxy.newProxyInstance(req.getClass().getClassLoader(), req.getClass().getInterfaces(), new InvocationHandler() {
            @Override
            public Object invoke(Object proxy, Method method, Object[] args) throws Throwable {
                //增强getParameter方法
                //判断是否是getParameter方法
                if (method.getName().equals("getParameter")){  //method.getName()：//代理对象调用了哪个方法就是哪个方法名
                    //增强返回值
                    //1、获取getParameter方法返回值
                   String value = (String) method.invoke(req, args);
                   if (value!=null){
                       for (String str : list) {
                           //包含敏感词，则替换
                           if (value.contains(str)){
                               value=value.replaceAll(str,"***");
                           }
                       }
                   }
                   return value;
                }
                return method.invoke(req,args);  //其他方法就正常调用req的方法，method:代理对象调用的方法
            }
        });
        //放行，传入增强后的request对象
        chain.doFilter(proxy_req, resp);
    }

    public void destroy() {
    }

}
```



## Listener : 监听器

- 概念：web的三大组件之一。

  ​	事件	：一件事情

  ​	事件源	：事件发生的地方

  ​	监听器	：一个对象

  ​	注册监听	：将事件、事件源、监听器绑定在一起。当事件源上发生某个事件后，执行监听器代码

```
ServletContextListener : 监听ServletContext对象的创建和销毁
	- void contextDestroyed(ServletContextEvent sce) : ServletContext对象被销毁之前会调用该方法
	- void ContextInitialized(ServletContextEvent sce) : ServletContext对象创建后会调用该方法
```

- 步骤

  ​	1、定义一个类，实现ServletContextListener

  ​	2、复写方法

  ​	3、配置

  ​			1、web.xml

  ```xml
  <!--配置监听器--> <!--xml配置监听器-->
  <listener>
      <listener-class>cn.pay.listener.ContextLoaderListener</listener-class>
  </listener>
  ```

  ​			2、注解：@WebListener 

  

**例如：**

```java
// @WebListener  //注解配置监听器
public class ContextLoaderListener implements ServletContextListener {
    @Override
    public void contextInitialized(ServletContextEvent servletContextEvent) {
        System.out.println("listener……");
        //加载资源文件
        //1、获取ServletContext对象
        ServletContext servletContext = servletContextEvent.getServletContext();
        //2、加载资源文件
            //"conListener"对应web.xml中的键名
        String conListener = servletContext.getInitParameter("conListener");
        //3、获取真实路径
        String realPath = servletContext.getRealPath(conListener);
        //4、加载到流中
        try {
            FileInputStream fileInputStream = new FileInputStream(realPath);
            System.out.println(fileInputStream); //打印出了流对象地址，说明读取成功
        } catch (FileNotFoundException e) {
            e.printStackTrace();
        }
    }

    @Override
    public void contextDestroyed(ServletContextEvent servletContextEvent) {

    }
}
```

```xml
<!--配置监听器--> <!--xml配置监听器-->
<listener>
    <listener-class>cn.pay.listener.ContextLoaderListener</listener-class>
</listener>

<!--指定初始化参数-->
<context-param>
    <param-name>conListener</param-name> <!--加载资源文件的键名-->
    <param-value>/WEB-INF/classes/listener.txt</param-value> <!--对应路径（src下的txt文件）-->
</context-param>
```

