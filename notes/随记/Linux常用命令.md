## Linux常用命令

### vim 编辑三种模式切换

```
vim /home/hello.txt  vim方式进入文件
```

<img src="https://gitee.com/panqiyi/pqimg/raw/master/20210913100735.png" alt="image-20210913100735763" style="zoom:80%;" />

```
命令行模式下:
1、显示行号
:set nu
2、单词查找
/单词  按n下一个
```

### 关机、重启

```
shutdown -h now  立即关机
reboot  重启
```

### 用户管理

#### 用户登录注销

```
su - 用户名   切换用户
logout  注销登录
```

#### 添加、删除用户、密码

```
useradd 用户名   添加用户
password 用户名  指定/修改密码
userdel 用户名   删除用户
```

#### 用户组

```
groupadd 组名  新增组
groupdel 组名  删除组

增加用户时直接指定组：
useradd -g 组名 用户名

修改用户所在组：
usermod -g 组名 用户名

```

### 运行级别

运行级别说明：

```
0:关机
1:单用户（用于找回用户密码）
2:多用户状态没用网络服务
3:多用户状态有网络服务 (常用)
4:系统未使用保留给用户
5:图形界面（常用）
6:系统重启
```

`常用的未运行级别3和运行级别5`

运行级别切换：

```
init 3  切换到运行级别3，可取值0-6
```

如运行级别3，即没用用户界面，体积小。

<img src="https://gitee.com/panqiyi/pqimg/raw/master/20210913104659.png" alt="image-20210913104658939" style="zoom:67%;" />

### 文件目录

**pwd**

```
pwd  显示当前工作目录的绝对路径
```

**ls**

```
ls [选项]
ls -a 显示当前目录所有文件和目录，包括隐藏文件
ls -l 以列表方式显示（ll等于ls -l）
ls -al (组合)
```

**cd**

```
cd ..  返回上一级目录
cd ~   到家目录（如/root）
cd /home  去到指定目录
```

**mkdir**

```
mkdir /home/cat          创建一个目录
mkdir -p /home/cat/foot  创建多级目录
```

**rmdir**

```
rmdir /home/cat  删除一个空目录
如果目录不为空，则用：
rm -rf /home/cat
```

**touch**

```
touch  /home  npnp.txt  在/home目录下创建一个npnp.txt的文件
```

**cp**

```
cp /home/npnp.txt  /home/bbb  将home目录下的npnp.txt复制到bbb目录下
cp -r /home/bbb  /opt         遍历bbb整个目录复制到/opt目录下
```

**rm**

```
rm /home/hello.txt     删除hello.txt文件
rm -f /home/hello.txt  删除hello.txt文件，并且不提示
rm -r /home/bbb        遍历删除整个目录
rm -rf                 删除（包括目录）文件且不提示
```

**mv**

```
mv hello.txt  npnp.txrt            将hello.txt重命名为npnp.txt
mv /home/npnp.txt /opt             将npnp.txt移动到/opt目录下
mv /home/npnp.txt  /opt/good.txt   将npnp.txt移动到/opt目录下,并重命名为good.txt
```

**cat**

```
cat /home/hello.txt           显示文件所有内容（只能浏览，不能修改）
cat -n  /home/hello.txt       显示文件所有内容,并显示行号
cat -n  /home/hello.txt|more  显示一页内容，按空格到下一页，方便查看
```

**echo**

```
echo "怎么样"  输出内容到控制台
echo $PATH    输出指定环境变量
```

**\>  和  >>**

```
ll /home > hello.txt   将home目录信息内容写入到hello.txt文件中（全部覆盖文件内容）
ll /home >> hello.txt  将home目录信息内容追加写入到hello.txt文件中（追加，不覆盖）
cat np.txt >> npnp.txt
```

**tree**

```
tree /home    以树状显示目录结构（没有tree,用 yum install tree 安装）
```

<img src="https://gitee.com/panqiyi/pqimg/raw/master/20210918174010.png" alt="image-20210918174010314" style="zoom:67%;" />

### 时间日期

**date**

```
date		（打印时间到控制台）
date +%Y	（按照格式要求打印时间）
date +%m
date +%d
date +"%Y-%m-%d %H:%M:%S"
date +"%Y-%m-%d"
(注意：date后面有个空格，然后才 +%Y等等)
```

![image-20210914231158901](https://gitee.com/panqiyi/pqimg/raw/master/20210914231158.png)

date设置系统日期时间

```
date -s "2023-09-23 20:09:10"
```

**cal**

```
cal        显示当前时间日历
cal 2020   显示2020年日历
```



### 搜索查找

**find**

```
find /opt -name hello.txt  在opt目录下，按文件名查找
find /home -user tom   在home目录下，按属于tom用户的文件
find /opt -size +100M  在opt目录下找到大于100M的文件（+n：大于 -n：小于 n：等于 单位：k\M\G）
```

**locate**

```
locate  文件名称

1、locate利用事先建立的locate（系统所有文件名称及路径）数据库实现快速定位，无需遍历，查询速度很快。
2、为保证查询精确，可定期更新locate数据库。一般可在查询前更新（命令：updatedb）
```

**grep**

```
cat np.txt | grep "np" 在np.txt中查找yes
写法2：
grep -n "yes" np.txt   (-n:显示行号，-i:忽略大小写)
```

### 压缩和解压

**tar**

`压缩后后缀是 .tar.gz 的文件`

```
压缩：
tar -zcvf myhome.tar.gz /home/                  将home目录压缩为 myhome.tar.gz
tar -zcvf mm.tar.gz /home/ss.txt /home/cc.txt   将ss.txt和cc.txt 压缩为mm.tar.gz
解压：
tar -zxvf redis.tar.gz                解压redis.tar.gz到当前目录
tar -zxvf redis.tar.gz  /opt/redis    解压redis.tar.gz 到 /opt/redis 目录
```

**zip和unzip**

`压缩后后缀是 .zip的文件`

```
压缩：
zip -r myhome.zip /home/           将home目录压缩为myhome.zip(-r压缩整个目录)
解压:
unzip -d /opt/tmp  /home/np.zip    将np.zip解压到 /opt/tmp目录
```

**gzip和gunzip**

`压缩后后缀为 .gz`

``` 
gzip /home/np.txt    将np.txt压缩
gunzip  /home/np.txt.gz  将np.txt.gz解压
```

### 组管理和权限管理

#### 组管理

**查看文件所有者**

```
ll 或 ls -la
```

![image-20210913210219465](https://gitee.com/panqiyi/pqimg/raw/master/20210913210219.png)

**修改文件所有者**

```
chown tom np.txt   将np.txt所有者改为tom
```

**组的创建**

```
groupadd  omg     创建一个组为omg
```

```
useradd -g omg  tom   创建tom用户时添加到omg组
```

**查看用户所在组**

```
ll 或 ls -la
```

![image-20210913211344042](https://gitee.com/panqiyi/pqimg/raw/master/20210913211344.png)

**改变目录/文件所在组**

```
chgrp  omg  np.txt
```

**改变用户所在组**

```
usermod  -g omg  jack  将用户jack修改到omg组
```



#### 权限管理

**权限介绍：**对文件的操作权限

![image-20210913212916083](https://gitee.com/panqiyi/pqimg/raw/master/20210913212916.png)

一共0-9共10位

**第0位确定文件类型：**取值（ -  d  c   d  b ）

```
l是链接,相当于windows的快捷方式
d是目录，相当于windows的文件夹
c是字符设备文件，鼠标，键盘
b是块设备，比如硬盘
-是普通文件
```

**第1-3位确定所有者（该文件的所有者）用户权限**

**第4-6位确定所在组（同用户组）用户权限**

**第7-9位确定其他用户权限**



**rwx权限作用**：

1、作用在文件

```
r:可读。可以读取，查看
w:可写。可以修改，但不一定能删除（删除一个文件，需要对该文件所在的目录有写的权力）
x:可执行，可以被执行的文件
```

2、作用在目录

```
r:可读。ls查看目录
w:可写。可以修改，对目录内创建、删除、重命名
X:可执行，可进入该目录
```

**修改权限**

**chmod** : 通过chmod指令修改文件/目录的权限。

`u:所有者  g:所在组  o:其他人   a:所有人(u、g、o的总和)`

方式一：

```
chmod  u=rwx,g=rw,o=x  hello.txt   修改hello.txt的权限为 所有者：可读可写可执行 所在组：可读可写 其他组：可执行
chmod  u-r,o+w  hello.txt          修改hello.txt的 所有者权限减去可读，其他组加上可写权限
cgmod  a-x  np                     修改np目录的 所有者、所在组、其他组权限都减去 可执行
```

方式二：

通过数字来修改权限

r=4, w=2 , x=1

```
3个一组，如：-rwx-wx-r--  就是 734
```

则上面方式一可修改为：

```
chmod  u=rwx,g=rw,o=x  hello.txt   修改hello.txt的权限为 所有者：可读可写可执行 所在组：可读可写 其他组：可执行
chmod  761  hello.txt
```



### 定时任务调度

在指定的时间执行特定的命令或程序

#### crond 任务调度

通过 crontab进行 定时任务设置

```
1.  cd /etc
2.  执行命令
	crontab -e  进入vim编写定时任务
	crontab -l  列出crontab定时任务
	crontab -r  删除当前用户下所有的定时任务
```

**编写定时任务：**

如：`*/1 * * * * date >> /home/npnp.txt`   即 每分钟将当前日期追加到npnp.txt文件中

- 5个占位符说明

<img src="https://gitee.com/panqiyi/pqimg/raw/master/20210914121448.png" alt="image-20210914121448301" style="zoom:80%;" />

- 特殊符号说明

![image-20210914121610410](https://gitee.com/panqiyi/pqimg/raw/master/20210914121610.png)

- 特殊时间执行案例

![image-20210914121713148](https://gitee.com/panqiyi/pqimg/raw/master/20210914121713.png)

如：每天凌晨两点半 将 mysql 数据库 mydb 备份到文件中

```
30 2 * * * myslqdump -u root -p密码 mydb > /home/db.bak
```



#### at 定时任务

1、`at`命令是一次性执行定时任务

2、`at`的守护进程`atd`默认在后台运行，每60秒检查任务队列。如果当前时间与任务时间匹配，则执行该任务，并将该任务从队列中删除。

3、在使用`at`命令前要保证`atd`进程启动，可用` ps -ef | grep atd` 查看该进程是否在运行。

**命令格式：**

```
1、at [选项] [时间]
2、输入执行脚本
3、两次结束输入 Ctrl+D 结束输入
```

选项：

![image-20210914213141489](https://gitee.com/panqiyi/pqimg/raw/master/20210914213141.png)

```
atq：查看任务队列
atrm: 删除指定序号的任务
```

![image-20210914225706764](https://gitee.com/panqiyi/pqimg/raw/master/20210914225706.png)

时间：

```
HH:MM    03:12   
在今日的 HH:MM 时刻进行，若该时刻已超过，则明天的 HH:MM 进行此任务。
```

```
HH:MM YYYY-MM-DD   22:15 2021-9-14
规定在某年某月的某一天的特殊时刻进行该项任务
```

```
am(上午) pm(下午)   4pm
12小时制，am:00:00-12:00 ; pm:12:00-24:00;  如 3am(凌晨3点)，11pm(晚上11点)
```

```
now + 数量 时间单位   now + 3 minutes
相对计时法，now ：当前时间；时间单位: hours(时)、minutes(分)、days(天)、weeks(星期)
```

```
today(今天)、tomorrow(明天)
```

```
midnight(深夜)、noon(中午)、teatime(饮茶时间，一般下午4点)
```



例子：

```
at now + 3 minutes  （当前时间过两分钟后，执行任务）
at> date >> npnp.txt （输入要执行的任务）
ctrl+d两次结束输入
```

```
at 22:40  （今天22:40执行，超过时间则明天）
at> date >> npnp.txt （输入要执行的任务）
ctrl+d两次结束输入
```

```
at 22:40 2021-10-01  （指定日期时间执行任务）
at> date >> npnp.txt （输入要执行的任务）
ctrl+d两次结束输入
```



### 磁盘分区、挂载

磁盘分区：

```
计算机中存放信息的主要的存储设备就是硬盘，但是硬盘不能直接使用，必须对硬盘进行分割，分割成的一块一块的硬盘区域就是磁盘分区。
```

如配置Linux系统时，我给20G硬盘存储空间给Linux，然后将20G分为3个区

```
/  17G,  /boot  1G  , /swap  2G
```

挂载：

将硬盘分区的存储空间 与 Linux目录 联系起来，然后通过访问这个目录来访问存储设备（硬盘分区的存储空间）。

![image-20210915123537386](https://gitee.com/panqiyi/pqimg/raw/master/20210915123537.png)

```
lsblk  或  lsblk -f   查看系统挂载情况
df -h       查看硬盘使用信息，包括挂载点
```

![image-20210916111639957](https://gitee.com/panqiyi/pqimg/raw/master/20210916111640.png)

```
Linux硬盘分IDE硬盘和SCSI硬盘；
SCSI:驱动器标识符为'sd',如‘sda1’,a为盘号(a:基本盘,b:基本从属盘,c:辅助主盘,d:辅助从属盘);1为分区编号(前面1-4个分区为主分区或扩展分区，5开始后面为逻辑分区)
IDE:驱动器标识符为'hd',如‘hda1’,其余与上面SCSI一致
```



#### 新增硬盘

```
虚拟机添加硬盘 --> 分区 --> 格式化 --> 挂载 --> 设置可以自动挂载
```

1、虚拟机添加硬盘

```
一、选择需要添加硬盘虚拟机，右键选择设置
二、点击添加，选择硬盘
三、一路下一步（就中间硬盘容量需要选择）
```

2、分区

```
一：fdisk /dev/sdb
二：n  新增分区  p  显示磁盘分区  w  写入并退出
```

![image-20210916123411604](https://gitee.com/panqiyi/pqimg/raw/master/20210916123411.png)

<img src="C:\Users\panqiyi\AppData\Roaming\Typora\typora-user-images\image-20210916123539690.png" alt="image-20210916123539690" style="zoom:80%;" />

3、格式化磁盘

```
mkfs -t ext4 /dev/sdb1    (ext4为分区类型)
```

4、挂载（将一个分区与目录联系起来）

挂载后，重启系统会失效

```
mount /dev/sdb1 /newdisk
mount  设备名称  挂载点（挂载目录）
```

```
卸载：
# umount  /dev/sda1     通过设备名卸载  
# umount  /newdisk      通过挂载点卸载  
```

5、设置自动挂载（永久挂载）

```
一：vim /etc/fstab
二：修改文件，添加自动挂载设备
三：保存后，mount -a 立即生效
```

![image-20210918172622338](https://gitee.com/panqiyi/pqimg/raw/master/20210918172622.png)



