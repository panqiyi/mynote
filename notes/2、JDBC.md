# JDBC

## 概念

JDBC：java DateBase Connectivity   java数据库连接；即用Java语言操作数据库

![](C:\Users\panqiyi\Desktop\notes\image\2img\11.png)

JDBC本质：

**Java定义的一套操作所有关系型数据库的规则，即接口。**

各个数据库厂商去实现这套接口，提供数据库驱动jar包；

我们可以使用这套接口(JDBC)编程，但真正执行的是驱动jar包的实现类(即多态)。

```java 
Fu接口   Zi实现类        Fu f=new Zi();    f.eat();  //实际调用的是子类重写父接口的方法  即多态
```

## 快速入门

**驱动jar包的下载：**

进入mysql官网

<img src="C:\Users\panqiyi\Desktop\notes\image\2img\12.png" style="zoom:60%;" />

下拉到底部

![](C:\Users\panqiyi\Desktop\notes\image\2img\13.png)

<img src="C:\Users\panqiyi\Desktop\notes\image\2img\14.png" style="zoom:60%;" />

**步骤：**

- **1、导入驱动jar包**

  ​		1、复制mysql-connector-java-8.0.22.jar到项目的libs(自定义)目录下

  ​		<img src="C:\Users\panqiyi\Desktop\notes\image\2img\15.png" style="zoom:60%;" />

  ​		![](C:\Users\panqiyi\Desktop\notes\image\2img\17.png)

  ​		2、选择libs右键---->Add as Library 完成导入

  

- 2、注册驱动

- 3、获取数据库连接对象 Connection

- 4、定义sql

- 5、获取执行sql语句的对象 Statement

- 6、执行sql，接收返回结果

- 7、处理结果

- 8、释放资源

  ```java
  public static void main(String[] args) throws Exception {
          //1、导入对应数据库驱动jar包
  
          //2、注册驱动（mysql5后可以省略）
          Class.forName("com.mysql.jdbc.Driver");
  
          //3、获取数据库连接对象
          Connection conn = DriverManager.getConnection("jdbc:mysql://localhost:3306/db2", "root", "pqy219");
  
          //4、定义sql语句
          String sql="update account set balance=500 where id=3";
  
          //5、获取执行sql的对象  Statement
          Statement stmt = conn.createStatement();
  
          //6、执行sql
          int count = stmt.executeUpdate(sql);
  
          //7、处理结果
          System.out.println(count);
          //释放资源
          stmt.close();
          conn.close();
      }
  ```

  <img src="C:\Users\panqiyi\Desktop\notes\image\2img\22.png" style="zoom: 200%;" />

  sql语句定义在步骤中是随意的！！

  **对象详解：**

  **1、DriverManager：驱动管理对象**

  <img src="C:\Users\panqiyi\Desktop\notes\image\2img\18.png" style="zoom: 80%;" />

  ​                        ![](C:\Users\panqiyi\Desktop\notes\image\2img\19.png)

  **2、Connection：数据库连接对象**

  <img src="C:\Users\panqiyi\Desktop\notes\image\2img\20.png"  />

  **3、Statement：执行sql的对象**

  ![](C:\Users\panqiyi\Desktop\notes\image\2img\21.png)

  **4、ResultSet：结果集对象，封装查询结果**
  
  - boolean next()：游标向下移一行，并判断该行是否有数据，false则没有数据，true则有数据。
  
    游标一开始在属性行，
  
    ![](C:\Users\panqiyi\Desktop\notes\image\2img\23.png)
  
  - getXxx(参数)：获取表中数据
  
    ​		Xxx：代表列(属性)的数据类型   如：int  getInt()
  
    ​		参数：
  
    ​				int类型：代表列的编号 ，从1开始     如：getString(1)
  
    ​				String类型：代表列名称。如：getDouble("balance")
  
    **注意：** 使用步骤：
  
    ​		1、游标向下移动一行
  
    ​		2、判断是否有数据
  
    ​		3、获取数据
  
  **5、PreparedStatement：执行sql的对象**
  
  **解决sql注入问题**，具体详解在下面的‘抽取JDBC工具类’的账户密码登录案例下

**例子1：**

在表中添加一列

```java
public static void main(String[] args) {

    Connection conn =null; //定义在这里是因为让 它的作用范围到finally中
    Statement stmt =null;

    try {
        //1、注册驱动
        Class.forName("com.mysql.jdbc.Driver");
        //定义sql语句
        String sql="insert into account values(null,'王五',3500)";
        //2、获取jdbc连接到数据库对象
        conn = DriverManager.getConnection("jdbc:mysql:///db2", "root", "pqy219");
        //3、获取sql执行对象
        stmt = conn.createStatement();
        //执行sql
        int i = stmt.executeUpdate(sql);
        //处理结果
        System.out.println(i);
        //释放资源不放这里，是因为如果上面步骤出现问题，就不会往下执行，而是直接抛出异常
    } catch (ClassNotFoundException  e) {
        e.printStackTrace();
    } catch (SQLException e) {
        e.printStackTrace();
    }finally {
       // stmt.close();
        //释放资源
        //避免空指针,因为在try中代码如果出现问题可能对象赋值为空，如连接数据库路径出错
        if (stmt!=null){
            try {
                stmt.close();
            } catch (SQLException e) {
                e.printStackTrace();
            }
        }
        if (conn!=null){
            try {
                conn.close();
            } catch (SQLException e) {
                e.printStackTrace();
            }
        }
    }
}
```

**例子2:**

修改表中‘王五’的工资

```Java
public static void main(String[] args) {
    Connection conn =null;
    Statement stmt =null;

    try {
        //注册驱动，告诉程序使用哪一个数据库驱动jar
        Class.forName("com.mysql.jdbc.Driver");
        //定义sql语句
        String sql="update account set balance=1500 where name='王五'";
        //连接数据库，返回连接对象
         conn = DriverManager.getConnection("jdbc:mysql:///db2", "root", "pqy219");
        //使用连接数据库对象调用方法，返回sql执行对象
         stmt = conn.createStatement();
        //执行sql语句
        int i = stmt.executeUpdate(sql);
        //处理数据
        System.out.println(i);
    } catch (ClassNotFoundException  e) {
        e.printStackTrace();
    } catch (SQLException e) {
        e.printStackTrace();
    } finally {
        if (stmt!=null){
            try {
                stmt.close();
            } catch (SQLException e) {
                e.printStackTrace();
            }
        }
        if (conn!=null){
            try {
                conn.close();
            } catch (SQLException e) {
                e.printStackTrace();
            }
        }
    }
}
```

更多操作(DML,DDL)修改定义sql语句即可！！

**案例3：查询操作**

查询表中所有数据！

```Java
public static void main(String[] args) {
    Connection conn =null;
    Statement stmt =null;
    ResultSet re =null;
    try {
        //注册驱动，告诉程序使用哪一个数据库驱动jar
        Class.forName("com.mysql.jdbc.Driver");
        //定义sql语句
        String sql="select * from account";
        //连接数据库，返回连接对象
        conn = DriverManager.getConnection("jdbc:mysql:///db2", "root", "pqy219");
        //使用连接数据库对象调用方法，返回sql执行对象
        stmt = conn.createStatement();
        //执行sql语句
        re = stmt.executeQuery(sql);
        
        while (re.next()){ //循环判断游标所在行是否有数据，有数据则获取数据
            int id = re.getInt(1);
            String name = re.getString("name");
            double balance = re.getDouble(3);
            System.out.println(id+","+name+","+balance);
        }

    } catch (ClassNotFoundException  e) {
        e.printStackTrace();
    } catch (SQLException e) {
        e.printStackTrace();
    } finally {
        if (re!=null){
            try {
                re.close();
            } catch (SQLException e) {
                e.printStackTrace();
            }
        }
        if (stmt!=null){
            try {
                stmt.close();
            } catch (SQLException e) {
                e.printStackTrace();
            }
        }
        if (conn!=null){
            try {
                conn.close();
            } catch (SQLException e) {
                e.printStackTrace();
            }
        }
    }
}
```

**案例：表-->类-->集合**

即：1、将表中的属性(列)作为一个类的成员变量

​		2、连接数据库，查询表获取数据赋值给对应类对象的对应属性

​		3、将每一个对象存储到集合中

​		4、main方法遍历集合

![](C:\Users\panqiyi\Desktop\notes\image\2img\24.png)

```Java
public class Student {
    // 成员变量对应表属性(列)
    private int id;
    private String name;
    private String club;
    private double wage;
    private String love;
    省略了 get/set方法、重写toString
    }
```

```Java
public class StuDemo {
    public static void main(String[] args) {
        List<Student> list = new StuDemo().findAll();
       list.forEach(System.out::println);
      //  System.out.println(list);
    }

    //连接数据库查询获取数据-->数据赋值给Student类对象的对应成员变量-->将Student类对象存储到集合中，返回集合对象
    public List<Student> findAll(){
        Connection conn =null;
        Statement stmt =null;
        ResultSet re = null;

        Student stu;
        ArrayList<Student> list = new ArrayList<>();
        try {
            //注册驱动，告诉程序使用哪一个驱动jar
            Class.forName("com.mysql.jdbc.Driver");
            //定义sql
            String sql="select * from student";
            //连接数据库,返回连接对象
            conn = DriverManager.getConnection("jdbc:mysql:///db2", "root", "pqy219");
            //获取执行sql对象
            stmt = conn.createStatement();
            //执行sql对应的 语句 ，DQL
            re = stmt.executeQuery(sql);

            while (re.next()){//每一次下移一行并判断是否还有数据
                //获取数据
                int id = re.getInt(1);
                String name = re.getString("name");
                String club = re.getString("club");
                double wage = re.getDouble("wage");
                String love = re.getString("love");
                //将数据赋值给Student对象的对应成员变量
                stu = new Student();
                stu.setId(id);
                stu.setName(name);
                stu.setClub(club);
                stu.setWage(wage);
                stu.setLove(love);
                //将对象存储到集合中
                list.add(stu);
            }
        } catch (ClassNotFoundException e) {
            e.printStackTrace();
        } catch (SQLException e) {
            e.printStackTrace();
        }finally {
            //释放资源
            if (re!=null){
                try {
                    re.close();
                } catch (SQLException e) {
                    e.printStackTrace();
                }
            }
            if (stmt!=null){
                try {
                    stmt.close();
                } catch (SQLException e) {
                    e.printStackTrace();
                }
            }
            if (conn!=null){
                try {
                    conn.close();
                } catch (SQLException e) {
                    e.printStackTrace();
                }
            }
        }
        return list; //返回集合
    }
```

![](C:\Users\panqiyi\Desktop\notes\image\2img\25.png)

## 抽取JDBC工具类

JDBCUtils

**目的：**简化书写

**分析：**

​	1、注册驱动也抽取

​	2、抽取一个方法获取连接对象

​				1、需求：不想传递参数(麻烦)，保证工具类的通用性

​				2、解决：配置文件

​	3、抽取一个方法释放资源

**自定义JDBC工具类：**

**将重复代码放入工具类中：1、获取连接对象 2、释放资源 3、注册驱动**

1、配置文件

![](C:\Users\panqiyi\Desktop\notes\image\2img\26.png)

2、定义JDBC工具类（注意：变量、方法都是静态的）

```Java
public class JDBCUtils {
    private static String url;  //静态代码块（方法）只能访问静态变量
    private static String user;
    private static String password;
    private static String driver;
    /**
     * 文件的读取，只需要读取一次即可拿到这些值。使用静态代码块
     */
    static{
        //读取资源文件，获取值。

        try {
            //1. 创建Properties集合类。
            Properties pro = new Properties();

            //获取src路径下的文件的方式--->ClassLoader 类加载器
            ClassLoader classLoader = JDBCUtils.class.getClassLoader();
            URL res  = classLoader.getResource("jdbc.properties");
            String path = res.getPath();

            pro.load(new FileReader(path));

            //3. 获取数据，赋值
            url = pro.getProperty("url");
            user = pro.getProperty("user");
            password = pro.getProperty("password");
            driver = pro.getProperty("driver");
            //4. 注册驱动
            Class.forName(driver);
        } catch (IOException e) {
            e.printStackTrace();
        } catch (ClassNotFoundException e) {
            e.printStackTrace();
        }
    }


    /**
     * 获取连接
     * @return 连接对象
     */
    public static Connection getConnection() throws SQLException {

        return DriverManager.getConnection(url, user, password);
    }

    /**释放资源，执行DML,DLL时需要释放两个
     */
    public static void close(Statement stmt,Connection conn){
        if( stmt != null){
            try {
                stmt.close();
            } catch (SQLException e) {
                e.printStackTrace();
            }
        }

        if( conn != null){
            try {
                conn.close();
            } catch (SQLException e) {
                e.printStackTrace();
            }
        }
    }
    /**
     * 释放资源
    执行DQL查询时需要释放3个，所以重载上面方法即可
     */
    public static void close(ResultSet rs,Statement stmt, Connection conn){
        if( rs != null){
            try {
                rs.close();
            } catch (SQLException e) {
                e.printStackTrace();
            }
        }

        if( stmt != null){
            try {
                stmt.close();
            } catch (SQLException e) {
                e.printStackTrace();
            }
        }
        if( conn != null){
            try {
                conn.close();
            } catch (SQLException e) {
                e.printStackTrace();
            }
        }
    }
}
```

**使用工具类**

```Java
public static void main(String[] args) {
    Connection conn = null;
    Statement stmt = null;
    ResultSet re = null;
    try {

         conn = JDBCUtils.getConnection(); // 返回连接对象
//初始化JDBCUtils工具类时，会最先执行里面的代码块，所以也完成了 注册驱动
        
        //定义sql语句
        String sql = "select * from account";
        //连接数据库对象调用方法，返回sql执行对象
        stmt = conn.createStatement();
        //执行sql语句
        re = stmt.executeQuery(sql);

        while (re.next()) { //循环判断游标所在行是否有数据，有数据则获取数据
            int id = re.getInt(1);
            String name = re.getString("name");
            double balance = re.getDouble(3);
            System.out.println(id + "," + name + "," + balance);
        }

    }catch (SQLException e) {
        e.printStackTrace();
    } finally {
        JDBCUtils.close(re,stmt,conn); //工具类调用释放资源的静态方法
    }
}
```

**案例：账号密码登录**

![](C:\Users\panqiyi\Desktop\notes\image\2img\27.png)

```java
/*登录案例：
* 键盘输入账户和密码,判断与数据库中信息是否一致，一致则登录成功！*/
public class Demo07 {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        System.out.println("请输入用户名：");
        String userName = sc.next();
        System.out.println("请输入密码：");
        String password = sc.next();
        
        boolean flag = new Demo07().login(userName, password);
        if (flag){
            System.out.println("登录成功！");
        }else{
            System.out.println("账户或密码错误！");
        }
    }

    //登录方法
    public boolean login(String userName,String password){
        if (userName==null||password==null){
            return false;
        }
// 连接数据库，判断 查询数据库中是否存在账户信息  有则返回true
        Connection conn =null;
        Statement stmt =null;
        ResultSet re =null;
        try {
            //1、获取连接
            conn = JDBCUtils.getConnection();
            //2、定义sql
            String sql="select * from user where username='"+userName+"'and password='"+password+"'";
            //3、获取sql执行对象
            stmt = conn.createStatement();
            //4、执行sql
            re = stmt.executeQuery(sql); //返回查询的结果集，有(即查到了对应userName与password)数据则true
            //5、判断
            return re.next();

        } catch (SQLException e) {
            e.printStackTrace();
        }finally {
            JDBCUtils.close(re,stmt,conn);
        }
        return false; //上面出现异常则返回false
    }
}
```

![](C:\Users\panqiyi\Desktop\notes\image\2img\28.png)

**上面登录案例存在安全问题：**

1、SQL注入问题：在拼接sql时，有一些sql的特殊关键字参与字符串的拼接，会造成安全性问题

​		1、随便输入账户名 如qwde，输入密码：a'  or  'a' = 'a

​		2、此时sql语句为：

```sql
select * from user where username='qwde' and password='a'  or  'a' = 'a'
// 查询数据库中 用户名没有 false；  密码没有 false ； 'a'='a' true
//false and false ==false
//false or true ==true   所以账户密码都错，但登录成功了！！
```

**解决sql注入问题：使用PreparedStatement对象来解决**

预编译的sql：参数使用 '?' 作为占位符

PreparedStatement是Statement的子类；

它在使用上的区别：

1、sql语句的定义上：注意：sql的参数使用 '?' 作为占位符。如下：

```sql
select * from user where username=? and password=?;
```

2、获取sql执行对象上：方法上的区别,需传入sql语句    conn.prepareStatement(String  sql)

3、获取sql语句执行对象后，需要先给占位符 '?' 赋值：

```
方法: setXxx(参数1,参数2)  
		Xxx: 数据类型
 		参数1: ? 的位置编号  从1开始
 		参数2：? 的值
```

4、执行sql语句上，不需要传递sql语句，在获取sql执行对象时已经传递了

**注意：**后期都会使用PreparedStatement来完成增删改查的所用操作

​			1、可以防止SQL注入

​			2、效率更高

**登录方法改进：使用PreparedStatement 的sql语句执行对象**

```Java
//登录方法  preparedStatement获取执行sql语句对象
public boolean login2(String userName,String password){
    if (userName==null||password==null){
        return false;
    }

    Connection conn =null;
    ResultSet re =null;
    PreparedStatement pstmt =null;
    try {
        //1、获取连接
        conn = JDBCUtils.getConnection();
        //2、定义sql
        String sql="select * from user where username=? and password=?";
        //3、获取sql执行对象
        pstmt = conn.prepareStatement(sql);
        //给占位符？赋值
        pstmt.setString(1,userName);
        pstmt.setString(2,password);
        //4、执行sql
        re = pstmt.executeQuery(); //返回查询的结果集，有(即查到了对应userName与password)数据则true
        //5、判断
        return re.next();

    } catch (SQLException e) {
        e.printStackTrace();
    }finally {
        JDBCUtils.close(re,pstmt,conn);
    }
    return false; //上面出现异常则返回false
}
```

## JDBC管理事务

**使用Connection对象来管理事务**

- 开启事务：setAutocommit(boolean  autoCommit)：调用该方法设置参数为false，即开启事务

-  提交事务：commit()

- 回滚事务：rollback()

  **如下：有如下表，先将张三转账给李四500块**

  ![](C:\Users\panqiyi\Desktop\notes\image\2img\29.png)

  ```java
  public static void main(String[] args) {
  
      Connection conn=null;
      PreparedStatement pstmt1=null;
      PreparedStatement pstmt2=null;
      try {
          //1、获取连接对象
          conn = JDBCUtils.getConnection();
          //定义sql
          String sql1="update account set  balance=balance-? where name=?";
          String sql2="update account set  balance=balance+? where name=?";
          //获取sql执行对象
           pstmt1 = conn.prepareStatement(sql1);
          pstmt2 = conn.prepareStatement(sql2);
          //给占位符？赋值
          int m=500;
          pstmt1.setInt(1,m);
          pstmt1.setString(2,"张三");
          pstmt2.setInt(1,m);
          pstmt2.setString(2,"李四");
  
          //执行sql
          pstmt1.executeUpdate();
          pstmt2.executeUpdate();
      } catch (SQLException e) {
          e.printStackTrace();
      }finally {
          JDBCUtils.close(pstmt1,conn);
          JDBCUtils.close(pstmt2,null);
      }
  }
  ```

**注意：这样写虽然转账成功    ，但是当执行完sql1出现异常时就会有问题！**

```java
//执行sql
        pstmt1.executeUpdate(); //执行sql1
		//手动制造异常
		int i=3/0; // 分子不能为0，会报数学异常，然后抛出给下面的catch捕获处理；所以try里面的sql2就无法执行到
        pstmt2.executeUpdate(); // 未执行
```

**此时就会凭空消失500块钱：**

![](C:\Users\panqiyi\Desktop\notes\image\2img\30.png)

**解决方案：添加事务**

```Java
public static void main(String[] args) {

    Connection conn=null;
    PreparedStatement pstmt1=null;
    PreparedStatement pstmt2=null;
    try {
        //1、获取连接对象
        conn = JDBCUtils.getConnection();
        //开启事务
        conn.setAutoCommit(false);
        //定义sql
        String sql1="update account set  balance=balance-? where name=?";
        String sql2="update account set  balance=balance+? where name=?";
        //获取sql执行对象
         pstmt1 = conn.prepareStatement(sql1);
        pstmt2 = conn.prepareStatement(sql2);
        //给占位符？赋值
        int m=500;
        pstmt1.setInt(1,m);
        pstmt1.setString(2,"张三");
        pstmt2.setInt(1,m);
        pstmt2.setString(2,"李四");

        //执行sql
        pstmt1.executeUpdate();
        int i =3/0;  //异常语句，直接抛出给catch语句中的 事务回滚处理
        pstmt2.executeUpdate();
        //提交事务
        conn.commit();
    } catch (Exception e) {
        //事务回滚
        try {
            if (conn!=null){
                conn.rollback();
            }
        } catch (SQLException ex) {
            ex.printStackTrace();
        }
        e.printStackTrace();
    }finally {
        JDBCUtils.close(pstmt1,conn);
        JDBCUtils.close(pstmt2,null);
    }
}
```

**使用事务管理后 语句出现异常后会回滚到初始状态！所以下面的结果没有出现变化**

![](C:\Users\panqiyi\Desktop\notes\image\2img\31.png)

## 数据库连接池

### 概念

其实就是一个容器(集合)，存放数据库连接对象的容器

- 当系统初始化好后，容器被创建，容器中会申请一些连接对象，当用户访问数据库时，从容器中获取连接对象，用户访问之后，会  将连接对象归还到容器！

![](C:\Users\panqiyi\Desktop\notes\image\2img\32.png)

**好处：**

1、节约资源

2、用户访问效率更高  (之前每用一次都要向底层申请创建一次连接对象(较慢)，用完又释放资源；使用连接池则可以复用，并且更快)

**实现：**

**1、**标准接口：DataSource          javax.sql包下的接口

​		1、方法：

				- 获取连接对象：getConnection()
				- 归还连接对象：Connection.close()     如果连接对象Connection是从连接池中获取的，那么调用Connection.close()方法，则不会再关闭连接，而是归还连接

**2、**一般我们不去实现该接口，由数据库厂商来实现：

​		1、C3P0：数据库连接池技术

​		2、Druid：数据库连接池实现技术，由阿里巴巴提供（速度等方面世界前列，常用）

### C3P0：数据库连接池技术

厂商实现了接口：DataSource  的数据库连接池技术

***

**步骤**

**1、**导入jar包(两个) ：

<img src="C:\Users\panqiyi\Desktop\notes\image\2img\33.png" style="zoom: 80%;" />

**注意：**如果你的模块没有导入数据库驱动jar包，需要导入！！

**2、**定义配置文件：

- 名称：必须是  c3p0.propertier 或者 c3p0-config.xml
- 路径：直接将文件放在src目录下即可

**3、**创建核心对象 :  数据库连接池对象    ComboPooledDataSource

**4、**获取连接：getConnection()

![](C:\Users\panqiyi\Desktop\notes\image\2img\34.png)

![](C:\Users\panqiyi\Desktop\notes\image\2img\35.png)

```java
public static void main(String[] args) throws SQLException {
    //1、创建数据库连接池对象，使用多态；未传参是使用默认配置
   // DataSource ds=new ComboPooledDataSource();
    
    //2、创建数据库连接池对象，使用多态；使用其他指定名称的配置
    //配置在.xml文件中设置，可设置多个指定名称配置
    DataSource ds=new ComboPooledDataSource("otherc3p0");
    
    //3、获取连接对象
    Connection conn = ds.getConnection();
    
    System.out.println(conn);
}
```

### Druid：数据库连接池技术

由阿里巴巴提供的，也实现了接口 DataSource

**步骤：**

1、导入jar包：

![](C:\Users\panqiyi\Desktop\notes\image\2img\36.png)

2、定义配置文件：

- 是properties文件的
- 可以叫任意名称，可以放在任意目录下

3、加载配置文件：

```java
Properties pro = new Properties();
        InputStream is = DruidDemo1.class.getClassLoader().getResourceAsStream("druid.properties"); //返回指定文件流
        pro.load(is);
```

4、获取数据库连接池对象：通过工厂   DruidDataSourceFactory 的createDataSource()方法来获取

5、获取连接：getConnection()

<img src="C:\Users\panqiyi\AppData\Roaming\Typora\typora-user-images\image-20201126220629263.png" alt="image-20201126220629263" style="zoom:80%;" />

```Java
public static void main(String[] args) throws Exception {
    //1、导入jar包
    //2、定义配置文件
    //3、加载配置文件
    Properties pro = new Properties();
    InputStream is = DruidDemo1.class.getClassLoader().getResourceAsStream("druid.properties"); //返回指定文件的流对象
    pro.load(is);
    //4、获取数据库连接池对象
    DataSource ds = DruidDataSourceFactory.createDataSource(pro);
    //5、获取连接对象
    Connection conn = ds.getConnection();

    System.out.println(conn);


}
```

#### 定义工具类

```java
/*Druid连接池工具类  JDBCUtils*/
public class JDBCUtils {
    //定义数据库连接对象变量
    private static DataSource ds;

    static {
        try {
            //加载配置文件
            Properties pro = new Properties();
            pro.load( JDBCUtils.class.getClassLoader().getResourceAsStream("druid.properties"));
            //获取连接池对象
            ds = DruidDataSourceFactory.createDataSource(pro);
        } catch (IOException e) {
            e.printStackTrace();
        } catch (Exception e) {
            e.printStackTrace();
        }
    }

    //返回获取连接对象
    public static Connection getConnection() throws SQLException {
        return ds.getConnection();
    }

    //返回 连接池对象
    public static DataSource getDataSource(){
        return ds;
    }

    //释放资源   //在线程池这里是归还资源到线程池！
    public static void close(Statement stmt,Connection conn){
        /*if (stmt!=null){
            try {
                stmt.close();
            } catch (SQLException e) {
                e.printStackTrace();
            }
        }

        if (conn!=null){
            try {
                conn.close();
            } catch (SQLException e) {
                e.printStackTrace();
            }
        }*/
        close(null,stmt,conn);

    }

    public static void close(ResultSet re,Statement stmt, Connection conn){
        if (re!=null){
            try {
                re.close();
            } catch (SQLException e) {
                e.printStackTrace();
            }
        }

        if (stmt!=null){
            try {
                stmt.close();
            } catch (SQLException e) {
                e.printStackTrace();
            }
        }

        if (conn!=null){
            try {
                conn.close();
            } catch (SQLException e) {
                e.printStackTrace();
            }
        }
    }
}
```



**使用工具类**

```Java
public static void main(String[] args) {
    Connection conn =null;
    PreparedStatement pstmt =null;
    try {
        //获取连接
         conn = JDBCUtils.getConnection();
        //定义sql
        String sql="insert into user values(null,?,?)";
        //获取sql执行对象
         pstmt = conn.prepareStatement(sql);
        //给?赋值
        pstmt.setString(1,"李小龙");
        pstmt.setString(2,"ppp111");
        //执行sql
        pstmt.executeUpdate();
    } catch (SQLException e) {
        e.printStackTrace();
    }finally {
        JDBCUtils.close(pstmt,conn);
    }
}
```



## Spring  JDBC  ：  JdbcTemplate

### 概念：

Spring框架对JDBC的简单封装。提供了一个JdbcTemplate对象简化JDBC的开发

### 步骤：

**1、导入jar包**

![image-20201125225830921](https://gitee.com/panqiyi/pqimg/raw/master/20201125225831.png)

**注意:**JdbcTemplate依赖于连接池， 前提记得导入连接池的jar包！！

**2、创建JdbcTemplate对象。依赖于数据源DataSource**

```java
JdbcTemplate  template = new JdbcTemplate(ds) //需要传入连接池对象ds
```

**3、调用JDBCTemplate的方法来完成CRUD的操作**

```java
update():执行DML语句。增、删、改语句
queryForMap():查询结果将结果集封装为map集合
queryForList:查询结果将结果集封装为list集合
query():查询结果，将结果集封装为JavaBean对象
queryForObject():查询结果，将结果封装为对象
```

**例如：**

```Java
public static void main(String[] args) {
        //1、导入jar包
        //2、创建JDBCTemplate对象
        JdbcTemplate template = new JdbcTemplate(JDBCUtils.getDataSource());
        //3、调用方法
        String sql="update user set username=?,password=? where id=?";
        int l = template.update(sql,  "梨花","666qqq",1); //返回值为改变(影响)行数，可不必返回  ；(sql,后面为对应？的值)
        System.out.println(l);
    }
```

![image-20201125235133956](https://gitee.com/panqiyi/pqimg/raw/master/20201125235134.png)

**案例：**

![image-20201126100305931](https://gitee.com/panqiyi/pqimg/raw/master/20201126100306.png)

```java
public class Student {
    // 成员变量对应表属性(列)
    private int id;
    private String name;
    private String club;
    private double wage;
    private String love;
    //省略get/set方法与重写toSring
    }
```

**一、执行DML语句**

```
DML:
1、修改1号数据 wage为3560
2、添加一条记录
3、删除添加的一条记录
```

```Java
public static void main(String[] args) {
    //获取JdbcTemplate对象
    JdbcTemplate template = new JdbcTemplate(JDBCUtils.getDataSource());
    //定义sql语句
    
   // String sql="update student set wage = ? where id=?";
  //  String sql="insert into student values(null,?,?,?,?)";
    String sql="delete from student where name=?";
    
    //调用方法执行sql
    
    // template.update(sql,3560,1); //sql对象后，根据?顺序，赋予值！
    // template.update(sql,"索隆","海贼团",4444,"打架");
    template.update(sql,"索隆");
    
}
```

1、

![image-20201126100842765](https://gitee.com/panqiyi/pqimg/raw/master/20201126100842.png)

2、

![image-20201126101403737](https://gitee.com/panqiyi/pqimg/raw/master/20201126101403.png)

3、

![image-20201126101616166](https://gitee.com/panqiyi/pqimg/raw/master/20201126101616.png)

**二、执行DQL语句**

```
DQL需求：
1、查询id为1的记录，将其封装为Map集合 ：queryForMap()
2、查询所有记录，将其封装为list集合：queryForList()
3、查询所有记录，将其封装为sudent类对象的list集合 : query(sql, new BeanPropertyRowMapper<类名>(类名.class))
4、查询总记录(行数)数 : queryForObject(sql,Long.class)
```

**实现如下：**

```java
//执行DQL语句
@Test //1、
public void test1(){ //queryForMap()
    String sql="select * from student where id=?";
    Map<String, Object> map = template.queryForMap(sql,6);
    System.out.println(map);
}
@Test  //2、
public void test2(){ //queryForList()
    String sql="Select * from student";
    List<Map<String, Object>> list = template.queryForList(sql);
    list.forEach(System.out::println);
}

@Test  //3、
public void test3(){ //查询所有记录，将其封装为Sudent类对象的list集合
    String sql="select * from student";
    List<Student> list = template.query(sql, new BeanPropertyRowMapper<Student>(Student.class));
    for (Student s : list) {
        System.out.println(s);
    }
}
 
@Test  //4、
public void test4(){ //常用于聚合函数
    String sql="Select count(id) from student";
    Long total = template.queryForObject(sql, Long.class);
    System.out.println(total);
}
```

