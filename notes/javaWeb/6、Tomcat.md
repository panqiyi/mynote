# Tomcat

## web服务器软件

- 服务器：安装了服务器软件的计算机
- 服务器软件：接收用户请求，处理请求，做出响应
- web服务器软件：
  		- 接收用户请求，处理请求，做出响应
    		- 在web服务器软件中，可以部署web项目，让用户通过浏览器来访问这些项目。
        		- web容器

**常见的Java相关的web服务器软件：**

- webLogic：oracle公司，大型的JavaEE服务器，支持所有的JavaEE规范，收费的。
- webSphere：IBM公司，大型的JavaEE服务器，支持所有的JavaEE规范，收费的。
- JBOSS：JBOSS公司的，大型的JavaEE服务器，支持所有的JavaEE规范，收费的。
- Tomct：Apache基金组织，中小型的JavaEE服务器，仅仅支持少量的JavaEE规范，如servlet/jsp，开源的，免费的。

**Java EE**：Java语言在企业级开发中使用的技术规范的总和，一共规定了13项大的规范。

## Tomcat

**1、下载：**https://tomcat.apache.org/

**2、安装：**解压压缩包即可

**3、卸载：**删除目录即可

目录结构：

![image-20210113140943587](https://gitee.com/panqiyi/pqimg/raw/master/20210113140943.png)

**4、启动**

- bin/startup.bat，双击运行该文件即可

- **访问**：浏览器输入：http://localhost:8080 访问本机

  ​								http://别人的ip地址:8080 访问别人

**可能遇到的问题：**

**1、黑窗口一闪而过**

	 - 原因：没有正确配置JAVA_HOME环境变量
	 - 解决方案：正确配置JAVA_HOME环境变量

**2、启动报错：**

 - 1、暴力：找到占用的端口号，并且找到对应的进程，杀死该进程

   ​		在cmd输入指令：netstat -ano  找到占用8080的端口进程的PID，然后在任务管理器中找到对应pid的进程将其结束

- 2、温柔：修改自身端口号

  ​	1、打开conf下的server.xml

  ​	2、找到如下位置修改端口号（默认为8080）

  ![image-20210113182314495](https://gitee.com/panqiyi/pqimg/raw/master/20210113182314.png)		

**注意：**一般会将tomcat的默认端口号修改为80。80端口号是http协议的默认端口号。

​		好处：在访问时，就不用输入端口号

**5、关闭**

​	**1、正常关闭：**

		- 1、点击 bin/shutdown.bat
		- 2、ctrl+c

​    **2、强制关闭：**

	- 点击启动窗口右上角的x

**6、配置**

**部署项目的方式：**

​	**1、直接将项目放到webapps目录下即可**

<img src="https://gitee.com/panqiyi/pqimg/raw/master/20210116113413.png" alt="image-20210116113413772" style="zoom: 80%;" />

![image-20210116113500318](https://gitee.com/panqiyi/pqimg/raw/master/20210116113500.png)

**/hello  项目路径--->虚拟路径**

**简化部署：**

将项目文件打包压缩为一个war包，再将war包放到webapps目录下，这样war会自动解压缩，删除war包后对应的文件也会删除。

<img src="https://gitee.com/panqiyi/pqimg/raw/master/20210116114255.png" alt="image-20210116114255101" style="zoom:80%;" />

缺点：必须要弄到webapps目录下，麻烦

**2、配置conf/server.xml文件**

​	再< Host>标签体中配置

```
< Context docBase="D:\PRoject\hello"  path="/aaa" />
docBase:项目存放的路径
path:虚拟路径
```

缺点：要关闭再开启tomcat才生效，且易使配置文件出错。

**3、在conf\ catalina\ localhost创建任意名称的xml文件。在文件中编写如下：**

```
< Context docBase="D:\PRoject\hello"  />
虚拟目录：xml文件名称
```

<img src="https://gitee.com/panqiyi/pqimg/raw/master/20210116121112.png" alt="image-20210116121112661" style="zoom:80%;" />

![image-20210116120936776](https://gitee.com/panqiyi/pqimg/raw/master/20210116120936.png)



**静态项目和动态项目**

目录结构

 - java动态项目的目录结构‘
      - 项目的根目录
           - WEB-INF目录
             		- web.xml：web项目的核心配置文件
               		- classes目录：放置字节码文件的目录
                   		- lib目录：放置依赖的jar包

**将Tomcat集成到IDEA中，并且创建javaEE的项目，部署项目**

**1、集成到idea**

![image-20210116134707262](https://gitee.com/panqiyi/pqimg/raw/master/20210116134707.png)

<img src="C:\Users\panqiyi\AppData\Roaming\Typora\typora-user-images\image-20210116134744586.png" alt="image-20210116134744586" style="zoom:80%;" />

![image-20210116134848537](https://gitee.com/panqiyi/pqimg/raw/master/20210116134848.png)

![image-20210116134924239](https://gitee.com/panqiyi/pqimg/raw/master/20210116134924.png)

![image-20210116135132430](https://gitee.com/panqiyi/pqimg/raw/master/20210116135132.png)

<img src="https://gitee.com/panqiyi/pqimg/raw/master/20210116135355.png" alt="image-20210116135355666" style="zoom:80%;" />

<img src="https://gitee.com/panqiyi/pqimg/raw/master/20210116135518.png" alt="image-20210116135518460" style="zoom:80%;" />

**2、创建web项目**

创建一个模块

![image-20210116141232979](https://gitee.com/panqiyi/pqimg/raw/master/20210116141233.png)

**查看/设置 虚拟目录**

![image-20210116142057564](https://gitee.com/panqiyi/pqimg/raw/master/20210116142057.png)

![image-20210116142158666](https://gitee.com/panqiyi/pqimg/raw/master/20210116142158.png)

只写 “/” ，访问时就不用写虚拟目录



**3、热部署**

设置热部署后，访问其他文件不需要重启tomcat

![image-20210116143606885](https://gitee.com/panqiyi/pqimg/raw/master/20210116143606.png)

