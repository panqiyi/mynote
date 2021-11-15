### springBoot配置热部署

修改代码立即生效，无需重启服务器

先添加pom依赖

```
<!--热部署 -->
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-devtools</artifactId>
    <scope>runtime</scope>
    <optional>true</optional>
</dependency>
```

1、打开settings

<img src="https://gitee.com/panqiyi/pqimg/raw/master/20211021090939.png" alt="image-20211021090939408" style="zoom: 67%;" />

2、在编辑页面  Ctrl+alt+shift+/

<img src="https://gitee.com/panqiyi/pqimg/raw/master/20211021091149.png" alt="image-20211021091149247" style="zoom:80%;" />

3、

![image-20211021091856766](https://gitee.com/panqiyi/pqimg/raw/master/20211021091856.png)

4、

![image-20211021091820697](https://gitee.com/panqiyi/pqimg/raw/master/20211021091820.png)

<img src="https://gitee.com/panqiyi/pqimg/raw/master/20211021091930.png" alt="image-20211021091930733" style="zoom:80%;" />