## linux中MySQL打开远程访问

1、启动MySQL服务并访问

![image-20210826164448154](https://gitee.com/panqiyi/pqimg/raw/master/20210826164455.png)

2、查看用户

![image-20210826164735910](https://gitee.com/panqiyi/pqimg/raw/master/20210826164735.png)

![image-20210826164823934](https://gitee.com/panqiyi/pqimg/raw/master/20210826164823.png)

3、修改root为远程访问（host为%）

![image-20210826170457135](https://gitee.com/panqiyi/pqimg/raw/master/20210826170457.png)

记得flush，否则不生效，还是无法远程连接

