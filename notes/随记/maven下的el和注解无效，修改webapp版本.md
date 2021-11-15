### maven下的el和注解无效，修改webapp版本

maven模板构建的web工程，如下图，查看web.xml，看到默认的是web2.3版本；不支持@WebServlet注解配置，甚至不支持El表达式（在web 3.0版本之后才支持）(Servlet3.0： 支持注解配置。)

![image-20210531104424367](https://gitee.com/panqiyi/pqimg/raw/master/20210531104424.png)

解决el表达式无效也可以在jsp的 <%@ page %> 内添加 isELIgnored=”false”。但注解还是得需要web版本升级

**修改web版本：**

**1、删除原先的web.xml (如果有重要内容，可以先备份)**

1、

<img src="https://gitee.com/panqiyi/pqimg/raw/master/20210531105405.png" alt="image-20210531105405449" style="zoom:80%;" />

2、选择web，点击"-" 删除

![image-20210531105955613](https://gitee.com/panqiyi/pqimg/raw/master/20210531105955.png)

3、点击yes

<img src="https://gitee.com/panqiyi/pqimg/raw/master/20210531110100.png" alt="image-20210531110059990" style="zoom:80%;" />

4、**注意：此时还未删除成功，需点击右下角的 "apply" 应用，才删除成功**

![image-20210531110301731](https://gitee.com/panqiyi/pqimg/raw/master/20210531110301.png)

**2、创建新的web.xml**

1、在上面删除的那 点击 "+" 添加 web.xml

![image-20210531110759077](https://gitee.com/panqiyi/pqimg/raw/master/20210531110759.png)2、选择版本

<img src="https://gitee.com/panqiyi/pqimg/raw/master/20210531111000.png" alt="image-20210531111000893" style="zoom: 67%;" />

3、点击 "apply" 应用，然后确认

<img src="https://gitee.com/panqiyi/pqimg/raw/master/20210531111307.png" alt="image-20210531111307404" style="zoom:67%;" />

4、打开web.xml查看，发现版本已经修改成了4.0

![image-20210531111444135](https://gitee.com/panqiyi/pqimg/raw/master/20210531111444.png)