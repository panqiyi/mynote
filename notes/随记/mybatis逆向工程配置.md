### mybatis逆向工程配置

  MyBatis Generator: 简称MBG，是一个专门为MyBatis框架使用者定制的代码生成器，可以快速的根据表生成对应的映射文件，接口，以及bean类。支持基本的增删改查，以及QBC风格的条件查询。但是表连接、存储过程等这些复杂sql的定义需要我们手工编写

1、 导入逆向工程的jar包

```xml
<!--mybatis逆向工程-->
<dependency>
  <groupId>org.mybatis.generator</groupId>
  <artifactId>mybatis-generator-core</artifactId>
  <version>1.3.7</version>
</dependency>
```

2、编写MBG的配置文件generatorConfig.xml

```xml
<!DOCTYPE generatorConfiguration PUBLIC
        "-//mybatis.org//DTD MyBatis Generator Configuration 1.0//EN"
        "http://mybatis.org/dtd/mybatis-generator-config_1_0.dtd">
<generatorConfiguration>
    <!-- 引入jdbc.properties配置文件 -->
    <properties resource="dbconfig.properties"/>
    <!--
       id属性：设置一个唯一标识
       targetRuntime属性值说明：
         MyBatis3Simple：基本的增删改查
         MyBatis3：带条件查询的增删改查
    -->
    <context id="simple" targetRuntime="MyBatis3Simple">

        <!--去除自动生成的注释-->
        <commentGenerator>
            <property name="suppressAllComments" value="true"/>  <!--阻止生成注释，默认为false-->
            <property name="suppressDate" value="true"/>  <!--阻止生成的注释包含时间戳，默认为false-->
        </commentGenerator>

        <!-- 数据库连接信息：驱动类，驱动地址，用户名，密码 -->
        <jdbcConnection driverClass="${jdbc.driver}" connectionURL="${jdbc.url}"
                        userId="${jdbc.username}" password="${jdbc.password}">
        </jdbcConnection>

        <!--设置JavaBean的生产位置-->
        <javaModelGenerator targetPackage="com.pqy.ssm.pojo" targetProject="maven_ssm/src/main/java"/>

        <!--设置SQL映射文件的生产位置-->
        <sqlMapGenerator targetPackage="com.pqy.ssm.mapper" targetProject="maven_ssm/src/main/resources"/>

        <!--设置Mapper接口的生产位置-->
        <javaClientGenerator type="XMLMAPPER" targetPackage="com.pqy.ssm.mapper" targetProject="maven_ssm/src/main/java"/>
    	<!--
        ANNOTATEDMAPPER:基于注解的Mapper接口，不会有对应的XML映射文件
        XMLMAPPER:所有的方法都在XML中，接口调用依赖XML文件。
		-->

        <!--逆向分析的表-->
        <!--
        tableName="item" : 表名
        domainObjectName="Item" ： 实体类名
        -->
        <table tableName="item" domainObjectName="Item"/>

    </context>
</generatorConfiguration>
```

3、测试

```Java
public static void main(String[] args) throws Exception  {
    
    List<String> warnings = new ArrayList<String>();
    boolean overwrite = true;
    File configFile = new File("maven_ssm/src/main/resources/generatorConfig.xml");
    ConfigurationParser cp = new ConfigurationParser(warnings);
    Configuration config = cp.parseConfiguration(configFile);
    DefaultShellCallback callback = new DefaultShellCallback(overwrite);
    MyBatisGenerator myBatisGenerator = new MyBatisGenerator(config, callback, warnings);
    myBatisGenerator.generate(null);
    System.out.println("生成成功！");
    
}
```