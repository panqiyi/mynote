## 重启tomcat后，上传图片到webapps被自动删除

### 原因：

webapps中的资源是编译本地的项目得来的，比如你运行存储图片在webapps下的image文件夹下，而且你还判断image不存在就创建。但是这也是存储在tomcat的webapps中，你启动服务器的时段他的确生成了image文件夹并存储了图片，但是你从新启动项目后，他就会消失，因为并没有存储到你的本地项目中。

本地项目文件 ---> 运行部署 --->  产生target文件夹 ---> tomcat的webapps就存储target文件夹下对应项目名的文件夹

再次运行部署后webapps会删除对应文件，生成新的(存储target文件夹下对应项目名) 的文件夹。所有，如果本地项目内容发送改变，那么运行部署后在webapps产生的文件也会随着改变。

详细如下：项目是基于maven 构建项目

1、当你一开始创建项目时没有运行(部署)时

![image-20210601224524557](https://gitee.com/panqiyi/pqimg/raw/master/20210601224524.png)

webapps下

![image-20210601225330145](https://gitee.com/panqiyi/pqimg/raw/master/20210601225330.png)

2、运行部署后产生target文件夹 

<img src="https://gitee.com/panqiyi/pqimg/raw/master/20210601225638.png" alt="image-20210601225638628" style="zoom:80%;" />

我们打开tomcat的webapps查看，发现已经出现了对应上面target下绿框的内容。

<img src="https://gitee.com/panqiyi/pqimg/raw/master/20210601225506.png" alt="image-20210601225505984" style="zoom:67%;" />

所谓本地项目即下图，它存储在本地自定义的工程路径

<img src="https://gitee.com/panqiyi/pqimg/raw/master/20210601230459.png" alt="image-20210601230459685" style="zoom:67%;" />

如我的这个项目就存储在 D:\PRoject\maven_web 

<img src="https://gitee.com/panqiyi/pqimg/raw/master/20210601230625.png" alt="image-20210601230625734" style="zoom:80%;" />

### 解决：

所有说真正存储的路径应该放在 项目本地工程路径中，如这里 图片应该存储在 D:\PRoject\maven_web\src\main\webapp\imag

所以说使用servlet存储从页面上传的图片要存储一份到本地项目工程中，这样你下一次启动项目时先编译本地的项目然后就会传到tomcat中的webapps，这样就会更新了webapps中的数据。而不会出现启动一次项目就会自动删除webapps下的图片(文件) 的问题。

当然存储一份到本地也要同时存储一份到tomcat的，因为存储到本地项目时通过当前项目(虚拟路径：http://localhost:8080/maven_web_war/)的绝对路径是访问不到的，必须存储到服务器的webapps下才能访问到。

当然关闭了webapps内的文件会自动删除，但是在次启动项目时就会读取到本地项目中的图片，他们会编译然后部署到tomcat的webapps中。

**存储图片到tomcat的webapps后，使用字节流读取webapps的图片写入本地项目中(webapp中)，**如我这里的

```java
//将上传到服务器的图片写入本地项目中
String localFile = "D:\\PRoject\\maven_web\\src\\main\\webapp\\image\\" + newFileName; //newFileName 图片文件名
BufferedOutputStream bos = new BufferedOutputStream(new FileOutputStream(localFile)); //localFile：本地存储图片路径
BufferedInputStream bis = new BufferedInputStream(new FileInputStream(image)); //image：存储在tomcat的webapps下的图片路径
byte[] bys = new byte[1024*4];
int len;
while ((len = bis.read(bys))!=-1) {
    bos.write(bys, 0, len);
}
bos.close();
bis.close();
```



**注意：没有使用maven构建的web项目**默认部署时存储的位置不是tomcat的webapps下，而是就存储在**本地项目**的运行产生数据文件out目录下。

普通web项目：

<img src="https://gitee.com/panqiyi/pqimg/raw/master/20210602073450.png" alt="image-20210602073450488" style="zoom:67%;" />

maven构建的web项目上面已经说过了，临时存储在tomcat的webapps下

因为没有使用maven构建的web项目他编译后产生的文件就产生在本地项目中了，所以他不论重新启动部署项目多少次，存储的图片文件都有效。