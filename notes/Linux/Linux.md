# Linux

## 本机系统与虚拟机与各系统的关系

<img src="https://gitee.com/panqiyi/pqimg/raw/master/20210605232217.png" alt="image-20210605232217921" style="zoom:80%;" />

## Linux目录



![image-20210606085249764](https://gitee.com/panqiyi/pqimg/raw/master/20210606085249.png)

## 远程操作Linux服务器

### 远程登录和操作

<img src="https://gitee.com/panqiyi/pqimg/raw/master/20210605230955.png" alt="image-20210605230955848" style="zoom:80%;" />

**通过Xshell来远程登录并操作Linux服务器**

1、安装打开Xshell，安装完成后新建会话

​	1.1: 先要知道linux的ip地址(在linux中终端输入指令查看)

![image-20210605225319951](https://gitee.com/panqiyi/pqimg/raw/master/20210605225320.png)

​	1.2：要知道本机与linux服务器网络是否可以连接

​			在本机打开cmd，输入一些指令，如果显示如下则连接成功

<img src="https://gitee.com/panqiyi/pqimg/raw/master/20210605225735.png" alt="image-20210605225735940" style="zoom:80%;" />

2、打开Xshell新建会话，然后确定

<img src="https://gitee.com/panqiyi/pqimg/raw/master/20210605230043.png" alt="image-20210605230043834" style="zoom:80%;" />

<img src="C:\Users\panqiyi\AppData\Roaming\Typora\typora-user-images\image-20210605230356762.png" alt="image-20210605230356762" style="zoom:80%;" />

填写用户和密码然后即可 用命令来操作Linux文件！

![image-20210605224832906](https://gitee.com/panqiyi/pqimg/raw/master/20210605224832.png)

### 远程文件传输

安装Xftp，安装完成后与上面的Xshell一样，新建会话。

此时就可以进行本机与远程Linux的文件传输了(选择文件右键-->传输)

<img src="https://gitee.com/panqiyi/pqimg/raw/master/20210605233631.png" alt="image-20210605233631324" style="zoom: 67%;" />



## vi & vim 编辑器

vi 是Linux系统内置的文本编辑器；

Vim 具有程序编辑能力，可以看作 Vi 的增强版，有代码的字体颜色，方便编程。还有代码补全、编译、错误跳转等等，在程序员中被广泛使用。

**Vi 和 Vim 常用的三种模式**

**正常模式**

1、以 vim 打开一个文档就进入一般模式(默认模式)，可以使光标上下左右移动，可以删除、复制粘贴。但是不能编写内容。

**插入模式**

键盘按 i 、I、o、O、a、A  等任何一个字母之后进入编辑模式，一般按 i 

**命令行模式**

按esc退出键，然后再输入" : "  在这个模式中，可以输入相关指令完成读取、存盘、替换、离开vim、显示行号等。

## 开机/重启，用户登录/注销 指令



## 用户管理



## 实用指令

### 运行级别

```
0 : 关机
1 : 单用户 (重置密码)
2 : 多用户状态没有网络服务
3 : 多用户状态有网络服务
4 : 系统未使用保留给用户
5 : 图形界面
6 : 系统重启
```

常用的运行级别是3和5

级别 3：节省资源，一般工作使用的为级别3

<img src="https://gitee.com/panqiyi/pqimg/raw/master/20210606152235.png" alt="image-20210606152235345" style="zoom:80%;" />

级别 5：在级别3上增加了图形化界面，占用资源

<img src="https://gitee.com/panqiyi/pqimg/raw/master/20210606152533.png" alt="image-20210606152532946" style="zoom: 67%;" />

**切换运行级别**

```
命令：
init [0123456]
如 init 3   就会切换到运行级别3 的状态。
```

**设置默认运行级别**

设置默认的运行级别后，以后打开虚拟机进入Linux系统都会默认进入该运行级别

CentOS 7 以前，在 /etc/inittab文件中修改。

7进行了简化，使用命令行来修改：

```
multi-user.target  运行级别 3
graphical.target   运行级别 5

查看默认运行级别:
systemctl get-default
修改默认运行级别:
systemctl set-default 运行级别
如设置默认运行级别 3 :  systemctl set-default multi-user.target
```



韩顺平笔记 纠错：

![image-20210606171003815](https://gitee.com/panqiyi/pqimg/raw/master/20210606171003.png)

### 指令补充：

文件目录类 ls 指令 

选项: -lh   以方便人观看数据的格式显示

![image-20210607213807966](https://gitee.com/panqiyi/pqimg/raw/master/20210607213808.png)

## 组管理和权限管理

### 补充

chown命令：（英文全拼：**change owner**）



查看所有组：

```
cat  /etc/group
//筛选查看组是否存在
cat /etc/group | grep 组名
```



## 网络配置

### IP地址修改

linux IP地址修改。

1、输入如下命令

```
vim /etc/sysconfig/network-scripts/ifcfg-ens33
```

2、添加修改信息

```
#先将上面对应的原始内容的修改为 BOOTPROTO=static
#IP地址
IPADDR=192.168.200.130
#网关
GATEWAY=192.168.200.2
#域名解析器
DNS1=192.168.200.2

```

3、Linux的网段变成:192.168.200，所以本地对应也要修改对应相同网段才能通讯，编辑 --> 虚拟网络编辑器

![image-20210611002642280](https://gitee.com/panqiyi/pqimg/raw/master/20210611002642.png)

修改子网IP为对应的Linux修改数据

<img src="C:\Users\panqiyi\AppData\Roaming\Typora\typora-user-images\image-20210611003240344.png" alt="image-20210611003240344" style="zoom:67%;" />

修改网关为对应修改的网关

![image-20210611003504659](https://gitee.com/panqiyi/pqimg/raw/master/20210611003504.png)

<img src="C:\Users\panqiyi\AppData\Roaming\Typora\typora-user-images\image-20210611003552198.png" alt="image-20210611003552198" style="zoom: 80%;" />

然后点击应用，然后确定即可。

4、如何生效

```
输入命令，两种方式。
1、service network restart
2、reboot   重启Linux
```

查看Linux的IP地址

<img src="https://gitee.com/panqiyi/pqimg/raw/master/20210611004528.png" alt="image-20210611004527900" style="zoom:80%;" />

查看本机vm8 ip

![image-20210611004650305](https://gitee.com/panqiyi/pqimg/raw/master/20210611004650.png)

查看本机是否能与Linux连接

<img src="https://gitee.com/panqiyi/pqimg/raw/master/20210611005351.png" alt="image-20210611005350980" style="zoom:67%;" />

连接成功。

此时打开Xshell，原来的配置以失效，需要重新配置属性，指定新的Linux的IP地址

进入Xshell远程连接本地，看能否连接

```
ping 192.168.200.1
```

**注意：**如果没有动，可能是因为本机的防火墙打开着不允许连接，关闭防火墙即可连接成功。

### 设置主机名和hosts映射

看韩顺平笔记即可

## JavaEE安装软件

### 安装jdk

<img src="https://gitee.com/panqiyi/pqimg/raw/master/20210612183332.png" alt="image-20210612183332387" style="zoom:80%;" />

### 安装tomcat

```
1、mkdir /opt/tomcat  新建目录
2、用Xftp上传tomcat压缩包 到 /opt/tomcat
3、tar -zxvf apache-tomcat-8.5.59.tar.gz
4、进入解压目录/bin，启动tomcat
	cd /opt/tomcat/apache-tomcat-8.5.59
	./startup.sh
5、开放8080端口
	firewall-cmd --permanent --add-port=8080/tcp  [开放端口]
	firewall-cmd --reload  [重载生效]
	firewall-cmd --query-port=8080/tcp  [查看端口是否开放]
6、本机windows进入浏览器测试：
	http://192.168.200.130:8080/
```

### 安装idea

```
1、mkdir /opt/idea
2、用Xftp上传tomcat压缩包 到 /opt/idea
3、tar -zxvf ideaIU-2020.2.3.tar.gz
//进入运行级别5(图形化界面) 进入终端输入命令进入到idea文件的bin目录下,运行idea: ./idea.sh
```

### 安装mysql

```
1、mkdir /opt/mysql
2、用Xftp上传mysql压缩包 到 /opt/mysql （也可以用命令直接在Linux下载，看韩顺平笔记）
后面看韩顺平笔记
补充:删除冲突文件时：要删除两个
rpm -e --nodeps mariadb-libs
rpm -e --nodeps marisa
```

补充：依次安装的rpm文件如下

![image-20210612201041969](https://gitee.com/panqiyi/pqimg/raw/master/20210612201042.png)

退出数据库: quit

### 安装redis

```
1、mkdir /opt/redis
2、用Xftp上传redis压缩包 到 /opt/redis
也可以用命令直接在Linux下载: wget http://download.redis.io/releases/redis-5.0.0.tar.gz
```

<img src="https://gitee.com/panqiyi/pqimg/raw/master/20210612210619.png" alt="image-20210612210619677" style="zoom:80%;" />

```
3、解压  tar -zxvf redis-5.0.0.tar.gz
```

![image-20210612210729507](https://gitee.com/panqiyi/pqimg/raw/master/20210612210729.png)

```
4、将redis-5.0.0 移动到 /usr/local/redis 下
	mv redis-5.0.0  /usr/local/redis
5、在/opt/redis 安装gcc编译
	yum install gcc-c++
6、进入进入到 /usr/local/redis/src 文件目录下
	cd /usr/local/redis/src 或者 ./src  [进入目录]
	make install  [安装redis]
```

7、 将redis目录下的 redis.conf 移动到 redis目录下的etc文件夹下

      将mkreleasehdr.sh、redis-benchmark、redis-check-aof、redis-cli、redis-server 移动到   /usr/local/redis/bin/ 目录下
```
//将redis-5.0.0目录下的 redis.conf 移动到 redis-5.0.0目录下的src文件夹下
[root@localhost redis]# mv redis.conf ./etc/  
 
[root@localhost redis]# cd ./src/      //进入redis-5.0.0目录下的src文件夹下
 
//将mkreleasehdr.sh、redis-benchmark、redis-check-aof、redis-cli、redis-server 移动到   /usr/local/redis-5.0.0/bin/ 目录下
[root@localhost src]# mv mkreleasehdr.sh redis-benchmark redis-check-aof redis-cli redis-server /usr/local/redis/bin/
```

8、编辑 redis.conf配置文件，设置后台启动redis服务

```
[root@pqyEdu100 etc]# vim redis.conf   //进找到对应位置修改为yes,vim中可以切换到命令模式输入 /关键词  来查找
```

![image-20210612214555907](https://gitee.com/panqiyi/pqimg/raw/master/20210612214556.png)

9、编辑 redis.conf配置文件，开启redis远程访问服务

 （1）把 redis.conf配置文件中的 bind 127.0.0.1 这一行给注释掉，这里的bind指的是只有指定的网段才能远程访问这个redis，注释掉后，就没有这个限制了。

![image-20210612215045979](https://gitee.com/panqiyi/pqimg/raw/master/20210612215046.png)

（2）把 redis.conf配置文件中的 protected-mode 设置成no（默认是设置成yes的， 防止了远程访问，在redis3.2.3版本后）

![image-20210612215229808](https://gitee.com/panqiyi/pqimg/raw/master/20210612215229.png)

10、启动redis

切换到 /usr/local/redis/bin/ 目录下执行 redis-server 命令，使用 /usr/local/redis/etc/redis.conf配置文件来启动redis服务

```
//进入到/usr/local/redis/bin/ 目录下
[root@localhost etc]# cd /usr/local/redis-5.0.0/bin/  
 
[root@localhost bin]# ls        //查看bin目录
mkreleasehdr.sh  redis-benchmark  redis-check-aof  redis-cli  redis-server
 
[root@localhost bin]# ./redis-server /usr/local/redis/etc/redis.conf   //启动Redis服务
```

![image-20210612220648173](https://gitee.com/panqiyi/pqimg/raw/master/20210612220648.png)