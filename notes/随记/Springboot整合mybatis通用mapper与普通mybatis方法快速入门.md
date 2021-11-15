### Springboot整合mybatis通用mapper与普通mybatis方法快速入门

> 通用mapper，它就是个辅助mybatis极简单表开发的组件。让mybatis的开发更方便。可以按照自己的需要选择通用方法，当通用mapper提供的方法不能满足你时，还能很方便的开发自己的通用方法。

1、pom配置依赖

可以使用如下快速构建springboot项目

![image-20211018091128398](https://gitee.com/panqiyi/pqimg/raw/master/20211018091128.png)

```xml
        <!--jdbc-->
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-jdbc</artifactId>
        </dependency>
        <!--web (集成了springMvc)-->
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-web</artifactId>
        </dependency>
        <!--mybatis-->
        <dependency>
            <groupId>org.mybatis.spring.boot</groupId>
            <artifactId>mybatis-spring-boot-starter</artifactId>
            <version>2.2.0</version>
        </dependency>
        <!--mysql驱动-->
        <dependency>
            <groupId>mysql</groupId>
            <artifactId>mysql-connector-java</artifactId>
            <scope>runtime</scope>
        </dependency>
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-test</artifactId>
            <scope>test</scope>
        </dependency>

        <!--通用mapper启动器依赖-->
        <dependency>
            <groupId>tk.mybatis</groupId>
            <artifactId>mapper-spring-boot-starter</artifactId>
            <version>2.1.5</version>
        </dependency>
        <!--druid启动器依赖-->
        <dependency>
            <groupId>com.alibaba</groupId>
            <artifactId>druid-spring-boot-starter</artifactId>
            <version>1.1.10</version>
        </dependency>
```

2、实体类与数据库表编写

> 可以通过mybatis的MBG逆向工程写数据库表，然后生成对应的实体类。而spring date jpa 则是正向工程，写实体类然后自动生成数据库表。

mysql:

```sql
CREATE TABLE `tb_user` (
  `id` INT(11) NOT NULL AUTO_INCREMENT,
  `name` VARCHAR(20) NOT NULL,
  `gender` VARCHAR(5) DEFAULT NULL,
  `age` INT(11) DEFAULT NULL,
  `address` VARCHAR(32) DEFAULT NULL,
  `qq` VARCHAR(20) DEFAULT NULL,
  `email` VARCHAR(50) DEFAULT NULL,
  `username` VARCHAR(20) NOT NULL,
  `phone` VARCHAR(11) DEFAULT NULL,
  PRIMARY KEY (`id`),
  UNIQUE KEY `user_username_uindex` (`username`)
) ENGINE=INNODB AUTO_INCREMENT=8 DEFAULT CHARSET=utf8;
```

pojo:

```java
/**
 * @author panqiyi
 * @date 2021/10/17 - 10:00
 */
@Entity // 表示该类为一个实体类
@Table(name = "tb_user") // 对应数据库中的tb_user表
public class User implements Serializable {
    @Id
    @GeneratedValue(strategy = GenerationType.IDENTITY) // 自增
    private Integer id;
    private String name;
    private String gender;
    private Integer age;
    private String address;
    private String qq;
    private String email;
    private String username;
    private String phone;
 //get/set……   
}
```

3、配置文件 application.yml

```yml
server:
  port: 10001
spring:
  datasource:
    driver-class-name: com.mysql.jdbc.Driver
    url: jdbc:mysql://192.168.200.130:3306/springboot
    username: root
    password: pqy
    type: com.alibaba.druid.pool.DruidDataSource
mybatis:
  type-aliases-package: com.pqy.springboot_case01.pojo # 别名包
  config-location: classpath:mybatis/mybatis-Config.xml # mybatis核心配置文件
  mapper-locations: classpath:mybatis/mapper/*.xml  # mapper映射（sql语句）
```

4、dao层接口

继承Mapper接口，可以直接使用父接口Mapper中提供的很多方法，不满足自己可以自定义方法（与普通使用mybatis时一样）

```java
public interface UserMapper extends Mapper<User> {
    public List<User> findalls(); // 自定义的方法，通过mybatis的xml映射配置实现
}
```

满足自定义方法的配置：

​     mybatis核心配置文件

```xml
<?xml version="1.0" encoding="UTF-8" ?>
<!DOCTYPE configuration PUBLIC "-//mybatis.org//DTD Config 3.0//EN"
        "http://mybatis.org/dtd/mybatis-3-config.dtd">
<configuration>

</configuration>
```

​     sql映射文件

```xml
<?xml version="1.0" encoding="UTF-8" ?>
<!DOCTYPE mapper PUBLIC "-//mybatis.org//DTD Mapper 3.0//EN" "http://mybatis.org/dtd/mybatis-3-mapper.dtd">
<mapper namespace="com.pqy.springboot_case01.dao.UserMapper">
    <select id="findalls" resultType="user">
        select * from tb_user
    </select>
</mapper>
```

配置SpringBoot启动器

```java
@SpringBootApplication
@EnableTransactionManagement // 开启声明式事务
@MapperScan("com.pqy.springboot_case01.dao")  // 批量扫描mapper,即dao包下的所有子包，如UserMapper(否则需要在每一个上面使用@Mapper注解)
public class SpringbootCase01Application {
    public static void main(String[] args) {
        SpringApplication.run(SpringbootCase01Application.class, args);
    }

}
```

 其实到这里已经完成了。你只要在service层调用UserMapper中的方法操作数据库即可。

文件目录：

<img src="https://gitee.com/panqiyi/pqimg/raw/master/20211018095711.png" alt="image-20211018095711469" style="zoom:80%;" />