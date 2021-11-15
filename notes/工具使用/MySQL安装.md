## MySQL

数据库软件

### 安装配置

**1、**百度进入官网

<img src="C:\Users\panqiyi\Desktop\my-note\notes\image\37.png" style="zoom:60%;" />

**2、**进入下载选项卡

<img src="C:\Users\panqiyi\Desktop\my-note\notes\image\38.png" style="zoom:67%;" />

**3、**

<img src="C:\Users\panqiyi\Desktop\my-note\notes\image\39.png" style="zoom:60%;" />

**4、**

<img src="C:\Users\panqiyi\Desktop\my-note\notes\image\40.png" style="zoom:60%;" />

\1. MySQL Community Server 社区版本，开源免费，但不提供官方技术支持。
\2. MySQL Enterprise Edition 企业版本，需付费，可以试用30天。
\3. MySQL Cluster 集群版，开源免费。可将几个MySQL Server封装成一个Server。
\4. MySQL Cluster CGE 高级集群版，需付费。
\5. MySQL Workbench（GUI TOOL）一款专为MySQL设计的ER/数据库建模工具。它是著名的数据库设计工具DBDesigner4的继任者。MySQL Workbench又分为两个版本，分别是社区版（MySQL Workbench OSS）、商用版（MySQL Workbench SE）。

MySQL Community Server 是开源免费的，这也是我们通常用的MySQL的版本。根据不同的操作系统平台细分为多个版本，我下载的是mysql-8.0.21-winx64版本。

**5、**

<img src="C:\Users\panqiyi\Desktop\my-note\notes\image\41.png" style="zoom:60%;" />

**6、**解压，然后在MySQL目录下创建一个my.ini文件，打开方式为记事本

然后输入下面这段配置数据库

```
[mysql]
default-character-set=utf8
[mysqld]
#skip-grant-tables
#设置3306端口
port = 3306
# 设置mysql的安装目录
basedir=D:\XUEXI\MySQL\mysql-8.0.21-winx64
# 设置mysql数据库的数据的存放目录
datadir=D:\XUEXI\MySQL\mysql-8.0.21-winx64\data
# 允许最大连接数
max_connections=200
# 服务端使用的字符集默认为8比特编码的latin1字符集
character-set-server=utf8
# 创建新表时将使用的默认存储引擎
default-storage-engine=INNODB
```

basedir=**D:\XUEXI\MySQL\mysql-8.0.21-winx64**

datadir=**D:\XUEXI\MySQL\mysql-8.0.21-winx64**\data

上面这两处加粗的是自己安装MySQL的路径，需要自己替换

**7、**

**7.1、以管理员身份运行cmd**

在C:\Windows\System32的目录下找到cmd.exe 右键已管理员身份运行

![](C:\Users\panqiyi\Desktop\my-note\notes\image\44.png)

**7.2、**将路径切换至mysql安装目录下的bin目录，输入以下命令安装MySQL:

mysqld install

![](C:\Users\panqiyi\Desktop\my-note\notes\image\42.png)

**如果出现以下问题**

（1）问题1、输入mysqld install回车后出现以下界面

![](C:\Users\panqiyi\Desktop\my-note\notes\image\45.png)

**下载并安装以下运行库得已解决**

![](C:\Users\panqiyi\Desktop\my-note\notes\image\46.png)

https://pan.baidu.com/s/1KYM0h80ICHs4cZVaU72Tkw
提取码:9o56

（2）问题2、输入mysqld install回车后就出现**Install/Remove of the Service Denied!** 的提示错误

原因：普通用户模式权限下的cmd安装mysql会出现这样的报错提示

需要像7.1、**以管理员身份运行cmd**即可解决

**7.3、**输入:

mysqld --initialize-insecure --user=mysql

回车，执行完这条命令，这时mysql就帮你自己创建一个data文件夹，

如果提示**Can’ t create directory.....**什么一大串的问题，可能的导致的原因：你的my.ini里面的basedir与datadir路径有误。 

**7.4、**开启MySQL服务。输入：

net start mysql

![](C:\Users\panqiyi\Desktop\my-note\notes\image\43.png)

****

### 删除已安装版本

输入以下命令安装MySQL:

mysqld install

![](C:\Users\panqiyi\Desktop\my-note\notes\image\47.jpg)

显示安装过MySQL，想重新安装，则**以管理员身份运行cmd**

并输入命令sc query mysql查看安装过的mysql服务

![](C:\Users\panqiyi\Desktop\my-note\notes\image\48.png)

输入命令sc delete mysql，删除老版mysql服务

![](C:\Users\panqiyi\Desktop\my-note\notes\image\49.png)

然后就可以继续7.2步骤的安装新MySQL

**7.2、**将路径切换至mysql安装目录下的bin目录，输入以下命令安装MySQL:

mysqld install

### 修改密码

输入以下指令：

mysql -u root –p

```
mysql -u 用户名 -p 密码 是连接数据库服务器的命令。
考虑密码如果直接明文写在这条命令行上，有些不方便（怕被别人看到），可以像你写的那样，只输入：mysql -u 用户名 -p 然后回车，此时提示你输入密码，这时候输入的密码就不再是明文的了。
```

让你输入密码时直接回车(如果设置过密码则想要输入密码)，然后可以进入到,mysql的管理界面

输入以下代码设置密码：

ALTER USER 'root'@'localhost' IDENTIFIED WITH mysql_native_password BY '你的密码';

![](C:\Users\panqiyi\Desktop\my-note\notes\image\50.png)