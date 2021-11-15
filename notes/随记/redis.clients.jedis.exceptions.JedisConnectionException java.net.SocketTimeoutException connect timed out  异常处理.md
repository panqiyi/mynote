### redis.clients.jedis.exceptions.JedisConnectionException: java.net.SocketTimeoutException: connect timed out  异常处理

问题原因：`防火墙(本机或远程linux) 未关闭，导致IDE无法连接到Linux。`

问题解决：

1、确定本机系统已关闭防火墙（控制面板-->搜索防火墙）

2、关闭Linux的防火墙

```java
//查看防火状态
systemctl status firewalld
```

如图：为开启防火墙状态

![image-20210816160436930](https://gitee.com/panqiyi/pqimg/raw/master/20210816160437.png)

```java
//暂时关闭防火墙(立即生效，重启Linux会自动开启)
systemctl stop firewalld
//打开防火墙
systemctl start firewalld
```

如图：为关闭防火墙状态

![image-20210816160635306](https://gitee.com/panqiyi/pqimg/raw/master/20210816160635.png)

`指令补充：`

```java
//永久关闭防火墙(重启Linux后生效)
systemctl disable firewalld
//重启防火墙(重启Linux后生效)
systemctl enable firewalld
```

