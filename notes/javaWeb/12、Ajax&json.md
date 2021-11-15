# Ajax&Json

## Ajax

### 概念

1、概念： ASynchronous JavaScript And XML	异步的JavaScript 和 XML

```
异步和同步：客户端和服务器端相互通信的基础上

* 客户端必须等待服务器端的响应。在等待的期间客户端不能做其他操作。
* 客户端不需要等待服务器端的响应。在服务器处理请求的过程中，客户端可以进行其他的操作。

同步，是所有的操作都做完，才返回给用户结果。即写完数据库之后，再响应用户，用户体验不好。
异步，不用等所有操作都做完，就响应用户请求。即先响应用户请求，然后慢慢去写数据库，用户体验较好。
	如 用户写入数据库的数据很多，同步要一直等，异步就可以关闭浏览器了(用ridis缓存,先响应用户，后台慢慢写入数据库)
```

<font color=red>Ajax 是一种在无需重新加载整个网页的情况下，能够更新部分网页的技术。 </font>
通过在后台与服务器进行少量数据交换，Ajax 可以使网页实现异步更新。这意味着可以在不重新加载整个网页的情况下，对网页的某部分进行更新。
传统的网页（不使用 Ajax）如果需要更新内容，必须重载整个网页页面。提升用户的体验

### 实现方式

#### 1、 原生的JS实现方式（了解）

```javascript
 				//1.创建核心对象
	            var xmlhttp;
	            if (window.XMLHttpRequest)
	            {// code for IE7+, Firefox, Chrome, Opera, Safari
	                xmlhttp=new XMLHttpRequest();
	            }
	            else
	            {// code for IE6, IE5
	                xmlhttp=new ActiveXObject("Microsoft.XMLHTTP");
	            }
	
	            //2. 建立连接
	            /*
	                参数：
	                    1. 请求方式：GET、POST
	                        * get方式，请求参数在URL后边拼接。send方法为空参
	                        * post方式，请求参数在send方法中定义
	                    2. 请求的URL：
	                    3. 同步或异步请求：true（异步）或 false（同步）
	
	             */
	            xmlhttp.open("GET","ajaxServlet?username=tom",true);
	
	            //3.发送请求
	            xmlhttp.send();
	
	            //4.接受并处理来自服务器的响应结果
	            //获取方式 ：xmlhttp.responseText
	            //什么时候获取？当服务器响应成功后再获取
	
	            //当xmlhttp对象的就绪状态改变时，触发事件onreadystatechange。
	            xmlhttp.onreadystatechange=function()
	            {
	                //判断readyState就绪状态是否为4，判断status响应状态码是否为200
	                if (xmlhttp.readyState==4 && xmlhttp.status==200)
	                {
	                   //获取服务器的响应结果
	                    var responseText = xmlhttp.responseText;
	                    alert(responseText);
	                }
	            }
```

#### 2、jQuery实现方式

**1、 $.ajax({键值对})** ：post/get通用方式

```html
<script>
     //使用$.ajax()发送异步请求
    //定义方法
    function fun() {
        $.ajax({
            //键值对的方式 设置值
            url:"ajaxServlet", //请求路径
            type:"post", //请求方式
            //date:"username=jack&age=23",  //请求参数
            data:{"username":"jack","age":23}, //常用
            success:function (data) {
                //响应成功后自动调用
                //在函数内定义一个变量date接收后台响应的数据
            },
            error:function () {
                alert("出错了")
                //表示如果请求响应出现错误了就会执行的回调函数
            },
            dataType:"text" //设置接收到响应数据的格式

            //注意：每一个键值对后都要有逗号，最后一个不用
        })
    }
</script>
```

**2、$.get() ：**发送get请求方式

```
* 语法：$.get(url, [data], [callback], [type])   //[] 中括号为可选内容
		* 参数：
			* url：请求路径
			* data：请求参数
			* callback：回调函数
			* type：响应结果的类型
```

```html
<script>
        //定义方法
        function fun() {
            $.get("ajaxServlet",{"username":"npnp"},function (data) {
                alert(data)
            },"text")
        }
    </script>
</head>
<body>
<input type="submit" name="sub" value="异步提交" onclick="fun()">
<input type="text">
</body>
```

**3、$.post() ：**发送post请求方式

与$.get() 实现方式是一样的，唯一区别就是名称不同

```
* 语法：$.post(url, [data], [callback], [type])  //[] 中括号为可选内容
	* 参数：
		* url：请求路径
		* data：请求参数
		* callback：回调函数
		* type：响应结果的类型
```



## json

### 1.概念：

 JavaScript Object Notation		JavaScript对象表示法

```
	//java
	Person p = new Person();
	p.setName("张三");
	p.setAge(23);
	p.setGender("男");

	var p = {"name":"张三","age":23,"gender":"男"};

	* json现在多用于存储和交换文本信息的语法
	* 进行数据的传输
	* JSON 比 XML 更小、更快，更易解析。
```

### 2.语法：

```
1. 基本规则
		* 数据在名称/值对中：json数据是由键值对构成的
			* 键用引号(单双都行)引起来，也可以不使用引号
			* 值得取值类型：
				1. 数字（整数或浮点数）
				2. 字符串（在双引号中）
				3. 逻辑值（true 或 false）
				4. 数组（在方括号中）	{"persons":[{},{}]}
				5. 对象（在花括号中） {"address":{"province"："陕西"....}}
				6. null
		* 数据由逗号分隔：多个键值对由逗号分隔
		* 花括号保存对象：使用{}定义json 格式
		* 方括号保存数组：[]
```

```html
<script>
    //1、定义基本格式
   var p1={"name":"张三",age:45,'gender':true}; //建议 键统一格式 如： "键名"
    alert(p)
    //2.1、嵌套格式  {} --> []
    var p2={
        "persons":[{"name":"张三","age":34,"gender":true},
                    {"name":"李四","age":14,"gender":true},
                    {"name":"王五","age":24,"gender":false},
                    {"name":"李小龙","age":54,"gender":true}
        ]
    }
    alert(p)
    //2.2、嵌套格式  [] --> {}
    var p3=[{"name":"张三","age":34,"gender":true},
            {"name":"李四","age":14,"gender":true},
            {"name":"李小龙","age":54,"gender":true}]
    alert(p)
</script>
```

### 3.获取数据

```
1. json对象.键名
2. json对象["键名"]
3. 数组对象[索引]
```

```html
<script>
    //1、定义基本格式
   var p1={"name":"张三",age:45,'gender':true}; //建议 键统一格式 如： "键名"

    var name = p1.name;   
    alert(name) //张三
    //2.1、嵌套格式  {} --> []
    var p2={
        "persons":[{"name":"张三","age":34,"gender":true},
                    {"name":"李四","age":14,"gender":true},
                    {"name":"王五","age":24,"gender":false},
                    {"name":"李小龙","age":54,"gender":true}
        ]
    }
    var name1 = p2.persons[2].name;
    alert(name1) //王五
    //2.2、嵌套格式  [] --> {}
    var p3=[{"name":"张三","age":34,"gender":true},
            {"name":"李四","age":14,"gender":true},
            {"name":"李小龙","age":54,"gender":true}]
    var name2 = p3[2].name;
    alert(name2) //李小龙
```

### 4.遍历

```
语法：适用于json对象遍历
for(var key in json对象)  //key 为键变量，String类型 ，所以不能用 json对象.键名 取值  只能 json对象.[key]

对于数组遍历需用普通遍历 for(var i=0; i<arr.lenght; i++)
```

```html
<script>
//1、定义基本格式
var p1={"name":"张三",age:45,'gender':true}; 

 //遍历
 for (var key in p1){  // key 为字符串 如 "name"   p1."name"是无效的
     alert(key+":"+p1[key])
 }
 </script>
```

```html
<script>
//2.1、嵌套格式  {} --> []
        var p2={
            "persons":[{"name":"张三","age":34,"gender":true},
                        {"name":"李四","age":14,"gender":true},
                        {"name":"王五","age":24,"gender":false},
                        {"name":"李小龙","age":54,"gender":true}
            ]
        }
       //遍历
       for (var key in p2){  // 遍历json对象每个键
           for (var i = 0; i < p2[key].length; i++) { //遍历每个键对应的数组
               var p=p2[key][i];  //注意：需定义变量 ； 数组索引对应的json对象
               for (var keys in p){  //遍历json对象
                   alert(keys+":"+p[keys])
               }
           }
       }
 </script>
```

```html
<script>
     //2.2、嵌套格式  [] --> {}
        var p3=[{"name":"张三","age":34,"gender":true},
                {"name":"李四","age":14,"gender":true},
                {"name":"李小龙","age":54,"gender":true}]
        //遍历
       for (var i=0; i<p3.length; i++){
           var p=p3[i]; //注意：需定义变量 ；
           for (var key in p){
               alert(key +":" +p[key])
           }
       }
</script>
```



### 5.JSON数据和Java对象相互转换

Json解析器：

```
常见的解析器：Jsonlib, Gsno, fastjson, jackson   下面用的是jackson解析器(因为后面spring里封装有)
```

**1、Java对象转为JSON** (常用)

使用步骤：

```
1、导入jackson的相关jar包
2、创建Jackson核心对象: ObjectMapper
3、调用ObjectMapper的相关转换方法进行转换
		转换方法：
			* writeValue(参数1，obj):
	               参数1：
	                    File：将obj对象转换为JSON字符串，并保存到指定的文件中
	                    Writer：将obj对象转换为JSON字符串，并将json数据填充到字符输出流中
	                    OutputStream：将obj对象转换为JSON字符串，并将json数据填充到字节输出流中
	         * writeValueAsString(obj):将对象转为json字符串
```

```Java
@Test
public void test1() throws IOException {
    Person person = new Person();
    person.setName("张三");
    person.setAge(23);
    person.setGender("男");

    //创建Jackson的核心对象  ObjectMapper
    ObjectMapper mapper=new ObjectMapper();

    //转换为json 字符串类型
    String json = mapper.writeValueAsString(person);
    System.out.println(json); //{"name":"张三","age":23,"gender":"男"}

    //writeValue ，将数据写到 C:\Users\panqiyi\Desktop\abc\dd\a.txt
    mapper.writeValue(new File("C:\\Users\\panqiyi\\Desktop\\abc\\dd\\a.txt"),person);

    //writeValue  将数据关联到writer中
    mapper.writeValue(new FileWriter("C:\\Users\\panqiyi\\Desktop\\abc\\dd\\b.txt"),person);

    //writeValue  将数据关联到OutputStream中
    mapper.writeValue(new FileOutputStream("C:\\Users\\panqiyi\\Desktop\\abc\\dd\\c.txt"),person);
}
```

<img src="https://gitee.com/panqiyi/pqimg/raw/master/20210515111516.png" alt="image-20210515111516252" style="zoom:67%;" />

**注解：**

​	1、`@JsonIgnore` : 排除属性

```
	使用:在java类属性上添加  @JsonIgnore
```

​	2、`@JsonFormat` : 属性值的格式化

```
	使用:在java类属性上添加  @JsonFormat(pattern = "yyyy-MM-dd") 指定格式
```



例如：有如下java类

```java
public class Person {
    private String name;
    private int age;
    private String gender;

    private Date birthday; //新增日期
    //……get/set和toString()
    }
```

将Java 对象转换为json

```java
@Test
public void test2() throws IOException {
    Person person = new Person();
    person.setName("张三");
    person.setAge(23);
    person.setGender("男");
    person.setBirthday(new Date());

    ObjectMapper mapper = new ObjectMapper();
    String s = mapper.writeValueAsString(person);
    System.out.println(s); //{"name":"张三","age":23,"gender":"男","birthday":1621049467880}
}
```

会发现 "birthday":1621049467880 日期的格式为毫秒值，不好看

1、此时可以使用注解：`@JsonIgnore` : 排除属性  这个会在转换时排除使用该注解的属性

```java
public class Person {
    private String name;
    private int age;
    private String gender;
    @JsonIgnore
    private Date birthday; //}
```

如上面一样 将Java 对象转换为json，打印输出结果为

```
{"name":"张三","age":23,"gender":"男"}
//排除了使用 @JsonIgnore 注解的属性 birthday
```

2、使用  `@JsonFormat` : 属性值的格式化 ；可以设置转换后的日期格式

```Java
public class Person {
    private String name;
    private int age;
    private String gender;

    @JsonFormat(pattern = "yyyy-MM-dd")   //指定格式
    private Date birthday; //}
```

如上面一样 将Java 对象转换为json，打印输出结果为

```
{"name":"张三","age":23,"gender":"男","birthday":"2021-05-15"}
```



**复杂java对象转换**

​	 List对象 ---> json

list存储JavaBean对象

```java
@Test
public void test3() throws JsonProcessingException {
    Person p1 = new Person();
    p1.setName("张三");
    p1.setAge(23);
    p1.setGender("男");
    p1.setBirthday(new Date());

    Person p2 = new Person();
    p2.setName("李四");
    p2.setAge(34);
    p2.setGender("男");
    p2.setBirthday(new Date());

    ArrayList<Person> str = new ArrayList<Person>();
    str.add(p1);
    str.add(p2);


    ObjectMapper mapper = new ObjectMapper();
    String s = mapper.writeValueAsString(str);
    System.out.println(s);

    /*
        [{"name":"张三","age":23,"gender":"男","birthday":"2021-05-15"},
         {"name":"李四","age":34,"gender":"男","birthday":"2021-05-15"}]
    */
}
```

​	 Map ---> json

```java
@Test
public void test4() throws JsonProcessingException {
    HashMap<String, Object> map = new HashMap<>();
    map.put("name","李小龙");
    map.put("age",34);
    map.put("gender","男");

    ObjectMapper mapper = new ObjectMapper();
    String s = mapper.writeValueAsString(map);
    System.out.println(s);
 // {"gender":"男","name":"李小龙","age":34}
}
```



2、JSON转为Java对象

```java
@Test
public void test5() throws IOException {
    //初始化json字符串
    String json="{\"name\":\"张三\",\"age\":23,\"gender\":\"男\"}";

    //创建ObjectMapper对象
    ObjectMapper mapper = new ObjectMapper();

    //转换为java对象  Person对象
    Person person = mapper.readValue(json, Person.class);
    System.out.println(person);  //Person{name='张三', age=23, gender='男', birthday=null}

    //读取文件中的json字符串
    Person person1 = mapper.readValue(new File("C:\\Users\\panqiyi\\Desktop\\abc\\dd\\c.txt"), Person.class);
    System.out.println(person1);

    //InputStream 读取文件中的json字符串
    Person person2 = mapper.readValue(new FileInputStream("C:\\Users\\panqiyi\\Desktop\\abc\\dd\\c.txt"), Person.class);
    System.out.println(person2);

    //Reader 读取文件中的json字符串
    Person person3 = mapper.readValue(new FileReader("C:\\Users\\panqiyi\\Desktop\\abc\\dd\\c.txt"), Person.class);
    System.out.println(person3);
    
   // Person{name='张三', age=23, gender='男', birthday=null}
}
```



## 校验用户名是否存在

![65](https://gitee.com/panqiyi/pqimg/raw/master/20210515182140.gif)

jsp:

```html
<script>
       $(function (){
           //给username绑定失去焦点blur事件
           $("#username").blur(function (){
               //获取username文本输入框的值
               var username = $(this).val();
               //发送ajax请求
               $.get("${pageContext.request.contextPath}/findUserServlet",{username:username},function (data) {
                   //期望服务器响应回的data数据格式：{"userExsit":true} 或 {"userExsit":false}
                   var span=$("#s_username");
                   if (data.userExsit){
                       //用户名存在
                       span.css("color","red")
                       span.html("用户名已存在")
                   }else {
                       //用户名不存在
                       span.css("color","green")
                       span.html("用户名可用")
                   }
               },"json") //指定响应的数据格式为json，不然会默认为服务器指定类型；或者在服务器设置mime类型为json
           })
       })
    </script>
</head>
<body>
<input type="text" name="username" id="username" placeholder="请输入用户名">
<span id="s_username"></span>
<br>
<input type="password" name="password" ><br>
<input type="submit" value="注册">
</body>
```

Servelt:

```Java
@WebServlet("/findUserServlet")
public class FindUserServlet extends HttpServlet {
    protected void doPost(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
        //1.获取用户名
        String username = request.getParameter("username");

        //2.调用service层判断用户名是否存在
        ImgService service=new ImgServiceImpl();
        User user = service.findName(username);
        System.out.println(user);

        //期望服务器响应回的数据格式：{"userExsit":true}
        //                         {"userExsit":false}

        //设置响应的数据格式为json，并指定字符集，防止响应到页面是乱码
        //response.setContentType("application/json;charset=utf-8");

        response.setCharacterEncoding("utf-8"); //设置响应编码；(前提是在ajax中$.get()中设置了json类型)
        Map<String,Object> map = new HashMap<String,Object>();

        if(user!=null){
            //存在
            map.put("userExsit",true);
        }else{
            //不存在
            map.put("userExsit",false);
        }

        // 创建json核心对象
        ObjectMapper mapper = new ObjectMapper();
        //将map转为json，并且传递给客户端
        mapper.writeValue(response.getWriter(),map);


    }

    protected void doGet(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
        this.doPost(request, response);
    }
}
```

**注意：**

```
服务器响应的数据，在客户端使用时，要想当做json数据格式使用。有两种解决方案：
		1. $.get(type):将最后一个参数type指定为"json"
			 设置响应编码： response.setCharacterEncoding("utf-8");
		2. 在服务器端设置MIME类型(并设置了编码)
			response.setContentType("application/json;charset=utf-8");
```

