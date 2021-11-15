## 8080端口被占用/JMX port被占用 解决

![image-20210422001857650](https://gitee.com/panqiyi/pqimg/raw/master/20210422001858.png)

![image-20210422003427385](https://gitee.com/panqiyi/pqimg/raw/master/20210422003427.png)

**1.cmd窗口查看被占用的端口号：**
 netstat -ano | findstr 8080

![image-20210422002126617](https://gitee.com/panqiyi/pqimg/raw/master/20210422002126.png)

**2.查看PID对应的进程:**
 tasklist | findstr “pid”

```
如这里pid=15828
 tasklist | findstr “15828”
```

![image-20210422002420522](https://gitee.com/panqiyi/pqimg/raw/master/20210422002420.png)

找到了占用8080端口的进程: java.exe

**3、进入到任务管理器结束该进程：**(快捷键：ctrl+shift+exit)

详细信息--->输入占用端口的进程(注意对应pid)--->右键结束任务

<img src="https://gitee.com/panqiyi/pqimg/raw/master/20210422003141.png" alt="image-20210422003141071" style="zoom:80%;" />