## java.sql.SQLException: Access denied for user 'root'@'localhost' (using password: YES)异常解决

在网上找了很久，都没有合适我的问题的解决方法，如修改权限，密码 等等。

**1、配置文件有误**

```
一、配置文件存在空格
```

![image-20210804084731490](https://gitee.com/panqiyi/pqimg/raw/master/20210804084731.png)

```
二、配置文件"键名"有误
```

对应异常：`java.sql.SQLException: Access denied for user 'panqiyi'@'localhost' (using password: YES)`

我的问题就出现在这里，像下面这样取键名是不可取的

```properties
driver=com.mysql.jdbc.Driver
url=jdbc:mysql://localhost:3306/test
username=root
password=66666
```

原因：

<font color=  violet  >在系统中也有个username属性，这时系统变量覆盖了Properties中的值，这时取得username的值为系统的用户名panqiyi，密码为properties中的password去查询数据库，此时用户名名和密码并不匹配就会报错。</font>

![image-20210804085920075](https://gitee.com/panqiyi/pqimg/raw/master/20210804085920.png)

解决方法：可以在键名加前缀，反正不要和username一样。如下：

```properties
jdbc.driver=com.mysql.jdbc.Driver
jdbc.url=jdbc:mysql://localhost:3306/test
jdbc.username=root
jdbc.password=66666
```

