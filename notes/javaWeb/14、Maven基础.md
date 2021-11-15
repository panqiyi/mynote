## Maven

### 概念

Maven 是一个项目管理工具，可以对项目进行构建、依赖管理等。

#### 依赖管理概念

依赖管理：maven工程对jar包的管理过程

<img src="https://gitee.com/panqiyi/pqimg/raw/master/20210528235541.png" alt="image-20210528235541141" style="zoom: 50%;" />

#### 一键构建

构建：指项目从编译、测试、运行、打包、安装、部署整个过程都交给maven进行管理

一键构建：指整个构建过程，使用maven一个命令可以轻松完成整个工作。

### 下载安装配置

**1、下载安装**

网址：https://maven.apache.org/download.cgi

<img src="https://gitee.com/panqiyi/pqimg/raw/master/20210529001708.png" alt="image-20210529001707981" style="zoom:67%;" />

下载后，解压即可。

**2、配置**

与Java的配置一样(java是jdk路径)

**1、复制解压的maven路径**

**2、到我的电脑环境变量中配置**

​	1、新建环境变量

![image-20210529002722227](https://gitee.com/panqiyi/pqimg/raw/master/20210529002722.png)

​	2、到Path新建

![image-20210529002959430](https://gitee.com/panqiyi/pqimg/raw/master/20210529002959.png)

注意：maven的运行依赖于JAVA_HOME；即Java的jdk配置

**3、验证配置是否成功**

​	cmd输入：mvn -v   出现以下内容即成功。

![image-20210529003431929](https://gitee.com/panqiyi/pqimg/raw/master/20210529003432.png)

### 仓库种类与关系

仓库就是一个存放所有依赖文件(jar包等)的目录。创建maven项目时，项目所有的依赖jar包都会放在本地仓库，供所有maven项目使用。

![image-20210530014212700](https://gitee.com/panqiyi/pqimg/raw/master/20210530014212.png)

**配置本地仓库路径**

maven文件下的 conf-->settings.xml

将本地仓库目录复制到如下红线即可

<img src="https://gitee.com/panqiyi/pqimg/raw/master/20210529103124.png" alt="image-20210529103124450" style="zoom:80%;" />

**配置阿里私服仓库**

在mirrors镜像标签下配置（所以私服又称镜像），默认被注释掉：

<img src="https://gitee.com/panqiyi/pqimg/raw/master/20210529104539.png" alt="image-20210529104539952" style="zoom:67%;" />

添加阿里私服镜像：

```
<mirror>
		<id>nexus-aliyun</id>
		<mirrorOf>central</mirrorOf>
		<name>Nexus aliyun</name>
		<url>http://maven.aliyun.com/nexus/content/groups/public</url>
	</mirror>
```

### maven项目目录结构

maven项目标准目录结构

```
src/main/java目录   核心代码部分
src/main/resources  配置文件部分
src/test/java目录   测试代码部分
src/test/resources  测试配置文件
src/main/webapp   页面资源，js.css,图片等
```



### maven常用命令

我们可以在 cmd 中通过一系列的 maven 命令来对我们的 如：maven-helloworld 工程进行编译、测试、运行、打包、安装、部署。

想要执行mvn命令，需要进入工程所在目录 （即进入到pom.xml 所在目录）

<img src="https://gitee.com/panqiyi/pqimg/raw/master/20210529112422.png" alt="image-20210529112422880" style="zoom:80%;" />

常用的Maven命令行指令：

| **命令作用** | **命令格式** |
| ------------ | ------------ |
| **清理**     | mvn clean    |
| **编译**     | mvn compile  |
| **测试**     | mvn test     |
| **打包**     | mvn package  |
| **安装**     | mvn install  |
| **发布**     | mvn deploy   |

**1、进入cmd，进入到项目目录，输入mvn compile  命令编译。**

![image-20210529112844144](https://gitee.com/panqiyi/pqimg/raw/master/20210529112844.png)

​	作用：在工程目录生成target目录，将源码（\src\main）编译为class文件，存放在**target/classes**目录。

![image-20210529114938168](https://gitee.com/panqiyi/pqimg/raw/master/20210529114938.png)

**2、** **输入清除命令 mvn clean**

作用：清除编译后的结果，会**删除target目录**及相关文件。

**3、** **输入 mvn test**  

作用：运行测试，会先对**核心代码(main下)和测试代码自动编译**，生成target目录和测试报告。

将源码（\src\main）编译为class文件，存放在**target/classes**目录

测试代码编译结果：**target/test-classes** 生成class文件

**4、输入打包命令 mvn package**

作用：Java项目自动打成 jar包；Web项目自动打成war包，在target目录下。

<img src="https://gitee.com/panqiyi/pqimg/raw/master/20210529120107.png" alt="image-20210529120107473" style="zoom:80%;" />

提示：该文件名的名字为：工程名字-版本-版本性质.jar，SNAPSHOT表示开发版本。

**5、安装命令 mvn install** 

作用：将项目打包后，安装（存储）到本地仓库中

### 生命周期

![image-20210529153505370](https://gitee.com/panqiyi/pqimg/raw/master/20210529153505.png)

### 概念模型图

![image-20210529154711615](https://gitee.com/panqiyi/pqimg/raw/master/20210529154711.png)

### pom.xml

pom:项目对象模型，是一个pom.xml文件

**坐标**：唯一值，在互联网中唯一标识一个项目

```xml
 <groupId>公司域名的倒写，如:com.jd</groupId>
  <artifactId>自定义项目名称</artifactId>
  <version>自定义版本号</version>

	开发中，不稳定版本通常在版本号后带-SNAPSHOT
	通常使用三位数标识 ，如: 1.1.0
	<groupId>：域名倒写 或者 域名倒写.项目名
```

##### 中央仓库导jar包

中央仓库：https://mvnrepository.com    搜索使用中央仓库，使用groupId 或 artifactId 作为搜索条件

1、搜索关键字

<img src="https://gitee.com/panqiyi/pqimg/raw/master/20210530102935.png" alt="image-20210530102935475" style="zoom:67%;" />

2、选择版本

<img src="https://gitee.com/panqiyi/pqimg/raw/master/20210530103038.png" alt="image-20210530103038189" style="zoom:50%;" />

3、**复制坐标到项目的pom.xml中，会自动下载（本地仓库有就会自动用本地的）**

<img src="https://gitee.com/panqiyi/pqimg/raw/master/20210530103155.png" alt="image-20210530103154949" style="zoom:67%;" />

```xml
<packaging>war</packaging>  <!--项目打包后扩展名类型：默认是jar(不写也是jar)；web项目是war-->
```

**依赖：**本地导入jar包 （**进入中央仓库复制坐标到pom.xml，本地仓库有就会自动导入，否则自动下载**）

![image-20210530001815955](https://gitee.com/panqiyi/pqimg/raw/master/20210530001816.png)

当如下时：

![image-20210530010718729](https://gitee.com/panqiyi/pqimg/raw/master/20210530010718.png)

```xml
<dependencies>
  <!--依赖，导入本地仓库的jar包到项目中使用-->
  <!--导入jar包1-->
  <dependency>
    <groupId>c3p0</groupId>
    <artifactId>c3p0</artifactId>
    <version>0.9.1.1</version>
  </dependency>

  <!--导入jar包2-->
  <dependency>
    <groupId>javax.servlet</groupId>
    <artifactId>javax.servlet-api</artifactId>
    <version>3.1.0</version>
    <scope>provided</scope>  <!--依赖范围-->
  </dependency>

</dependencies>
```

**注意：当对应坐标的jar包本地仓库没有时，会自动下载。并保存到仓库**



### idea集成maven插件

在idea中内置了maven，一般不使用内置的，因为内置修改maven的设置不方便。

使用自己安装的maven，需要覆盖内置的默认设置。

1、File ---> Settings

2、File --> Other Settings （别忘记设置这个）

两个设置都是一样的，下面先设置settings的

![image-20210529221048895](https://gitee.com/panqiyi/pqimg/raw/master/20210529221048.png)

![image-20210529222218594](https://gitee.com/panqiyi/pqimg/raw/master/20210529222218.png)

2、搜索maven

<img src="https://gitee.com/panqiyi/pqimg/raw/master/20210529160045.png" alt="image-20210529160045511" style="zoom:67%;" />

3、点击maven选项进行配置

![image-20210529160643366](https://gitee.com/panqiyi/pqimg/raw/master/20210529160643.png)

![image-20210529222943340](https://gitee.com/panqiyi/pqimg/raw/master/20210529222943.png)

```java
-DarchetypeCatalog=internal   //使用maven提供的骨架(模板)创建工程，一般默认需要联网下载模板文件。当设置这个属性，只要曾经用maven的骨架创建过项目，就会在不联网的情况下自动从本地找到对应插件创建maven项目
```



### 创建maven工程

#### 使用骨架搭建maven的Java工程

选择maven，然后选择idea为maven提供的创建Java项目的骨架（确保联网）

1、

![image-20210529200431168](https://gitee.com/panqiyi/pqimg/raw/master/20210529200431.png)

2、

![image-20210529234003420](https://gitee.com/panqiyi/pqimg/raw/master/20210529234003.png)

3、

![image-20210529201724325](https://gitee.com/panqiyi/pqimg/raw/master/20210529201724.png)

4、项目创建完成

<img src="https://gitee.com/panqiyi/pqimg/raw/master/20210529203012.png" alt="image-20210529203011863" style="zoom:80%;" />

右下角弹出，选择允许自动导入

![image-20210529210119301](https://gitee.com/panqiyi/pqimg/raw/master/20210529210119.png)

但是发现他的**项目目录是不完整**的；缺少了配置文件目录：resources  这个需要我们自己手动创建

​	1、在main和test中分别创建一个名称为 resources 的文件夹 ----> 然后将文件夹设置为资源文件。

​			选择文件右键（新版idea会在main新键文件时提示生成resources资源文件，点击即可生成）

<img src="https://gitee.com/panqiyi/pqimg/raw/master/20210529203726.png" alt="image-20210529203726623" style="zoom:80%;" />

​			完成：

<img src="https://gitee.com/panqiyi/pqimg/raw/master/20210529203813.png" alt="image-20210529203813461" style="zoom:80%;" />



#### 不使用骨架创建maven的java工程

1、

<img src="https://gitee.com/panqiyi/pqimg/raw/master/20210529204616.png" alt="image-20210529204616854" style="zoom:80%;" />

2、与上面用骨架类似，步骤会更加简洁。完成如下

![image-20210529205139569](https://gitee.com/panqiyi/pqimg/raw/master/20210529205139.png)

选择允许自动导入

![](https://gitee.com/panqiyi/pqimg/raw/master/20210529210119.png)

就只有test下的resources配置文件没有创建，需要手动创建。

**普通的Java工程不使用骨架的方式更加方便。推荐**



#### 使用骨架创建web工程

1、

<img src="https://gitee.com/panqiyi/pqimg/raw/master/20210529211644.png" alt="image-20210529211644619" style="zoom:80%;" />

2、

<img src="https://gitee.com/panqiyi/pqimg/raw/master/20210529231850.png" alt="image-20210529231849982" style="zoom:80%;" />

3、

![image-20210529212119060](https://gitee.com/panqiyi/pqimg/raw/master/20210529212119.png)

4、

![image-20210529232014226](https://gitee.com/panqiyi/pqimg/raw/master/20210529232014.png)

缺少的目录需要自己补。如：src/main中的java目录

1、在main下自己创建一个名称为java的文件夹；然后右键改变文件属性

<img src="https://gitee.com/panqiyi/pqimg/raw/master/20210529213706.png" alt="image-20210529213706592" style="zoom:80%;" />

2、在main下新建文件时提示如下，也可以直接点击即可

![image-20210529213601752](https://gitee.com/panqiyi/pqimg/raw/master/20210529213601.png)

其他的缺少目录也是一样的添加方法。最后如下：

![image-20210529232120199](https://gitee.com/panqiyi/pqimg/raw/master/20210529232120.png)

### maven工具窗口

<img src="https://gitee.com/panqiyi/pqimg/raw/master/20210530005050.png" alt="image-20210530005050129" style="zoom:80%;" />

生命周期：点击对应的 命令 ，即可执行对应的 命令指令

### 依赖范围

```xml
<!--依赖-->
<dependencies>
  <!--单元测试-->
  <dependency>
    <groupId>junit</groupId>
    <artifactId>junit</artifactId>
    <version>4.11</version>
    <scope>test</scope> <!--scope标签-->
  </dependency>
```

如用maven开发时的 servlet继承HttpServlet是maven仓库中的。将写好的程序打包部署到tomcat服务器时，程序不需要servlet的jar包(maven本地仓库)，因为tomcat提供了servlet的jar。所有导入servlet的jar时依赖范围是provided; jsp也是一样

![image-20210530003900598](https://gitee.com/panqiyi/pqimg/raw/master/20210530003900.png)

<img src="https://gitee.com/panqiyi/pqimg/raw/master/20210530100805.png" alt="image-20210530100805354" style="zoom: 80%;" />

```
如Junit单元测试：
当<scope>complie</scope>时就能在main下用单元测试。
当<scope>test<scope>时就不能在main下用单元测试，只能在test下用
```



### maven属性设置和全局变量

1、属性设置

在< properties> 设置 maven常用属性

2、maven全局变量

​		1、在< properties> 中通过自定义标签声明变量，标签名就是变量名

​		2、在pom.xml文件其他位置使用：${标签名} 使用变量值

​		3、自定义全局变量一般定义   依赖的版本号，当项目中使用多个jar包是相同版本号时可使用全局变量定义版本号。

```xml
<properties>
  <!--maven构建项目使用的时utf-8，避免中文乱码-->
  <project.build.sourceEncoding>UTF-8</project.build.sourceEncoding>
  <!--编译代码使用的jdk版本-->
  <maven.compiler.source>1.8</maven.compiler.source>
  <!--当前java项目运行的jdk版本-->
  <maven.compiler.target>1.8</maven.compiler.target>
  <!--自定义变量，表示版本号-->
  <c3p0.version>0.9.1.1</c3p0.version>  <!--自定义的标签名c3p0.version 就是变量名；使用：${c3p0.version} -->
</properties>

 <!--依赖-->
  <dependencies>
    <dependency>
      <groupId>c3p0</groupId>
      <artifactId>c3p0</artifactId>
      <version>${c3p0.version}</version> <!--自定义版本号变量的使用-->
    </dependency>

  </dependencies>
```



### 资源插件

```
src/main/java 和 src/test/java 这两个目录中所有的*.java文件会分别在comile和test-comiple阶段被编译，编译分别放到 target/classes 和 target/test-class 目录中。
这两个目录除了.java文件的其他文件都会被忽略，如果需要把src目录下的其他文件包放到 target/classes目录，作为输出jar的一部分。需要指定资源文件。配置放到<build>标签中

作用：mybatis会用到
```

```xml
<build>
    <resources>
      <resource>
        <directory>src/main/java</directory>  <!--所在的目录-->
        <!--包括目录下的.properties, .xml文件都会被扫描-->
        <includes>
          <include>**/*.properties</include>
          <include>**/*.xml</include>
        </includes>
        <!-- filtering选项 false 不启用过滤器， *.property已经起到过滤作用-->
        <filtering>false</filtering>
      </resource>
    </resources>
  </build>
```

