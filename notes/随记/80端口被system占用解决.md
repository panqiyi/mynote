### 80端口被system占用解决

 netstat -ano | findstr 80

发现占用程序的PID为4，打开任务管理器找到对应的PID=4的程序，发现是system,而且无法结束进程。

![image-20211105160914949](https://gitee.com/panqiyi/pqimg/raw/master/20211105160915.png)

解决方法：

#### 1、原因：  

**netsh http show servicestate** 查看一下当前的http服务状态

![image-20211105161455741](https://gitee.com/panqiyi/pqimg/raw/master/20211105161455.png)

80端口被一个DefaultAppPool的东西占用了，如果用过IIS的童鞋，这时候肯定一定想到了原因，这里我们依然要接着往下找原因，图中可以看出控制器进程ID为4640，那么就 就继续查看一下4640进程是什么鬼，进入任务管理器，找到PID4640的进程，右键转到服务，可以看到当前的进程所在的服务，如图所示：

<img src="https://gitee.com/panqiyi/pqimg/raw/master/20211105161646.png" alt="image-20211105161646350" style="zoom:67%;" />

<img src="https://gitee.com/panqiyi/pqimg/raw/master/20211105161710.png" alt="image-20211105161710888" style="zoom:67%;" />

看到图中的服务，这里原因也就找到了，IIS的World Wid Web Publishing Service 万维网服务的问题。

#### 2、解决：

**控制面板**–>**程序**–>**启用或者关闭Windows功能**–>找到**Internet Information Service，将其关闭即可**

<img src="https://gitee.com/panqiyi/pqimg/raw/master/20211105161853.png" alt="image-20211105161853303" style="zoom:67%;" />