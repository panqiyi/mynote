## PicGo+gitee+Typora自键图床

这玩意之前弄过几次都出现了错误，本打算放弃了，就用别人的线上图床算了。但是发现使用其他的图床也很麻烦，就像我那篇文章用的图床：

博客导入本地markdown文件连图片一起导入？

用这种现成的在线图床，比较麻烦，1、先有图片(或者先截图)保存在本地，2、然后再去那个图床网站上面导入本地图片，3、然后再复制生成的图片链接 4、大部分情况还得删除本地的图片；

<font color='red' size=5>是不是挺麻烦的！</font>

那有没有什么办法是一劳永逸的呢？截图直接复制图片粘贴到Typora中，然后图片地址**自动**从本地地址变成网上的地址，或者说图床的地址。

**这样就会很方便！**

那我们先来康康<font color='orange'>**屏幕截图的软件** </font> ：**Snipaste**

![image-20201124113433581](https://gitee.com/panqiyi/pqimg/raw/master/20201124113433.png)

这个截图软件挺好用的，截图可直接编辑与复制

![image-20201124113132601](https://gitee.com/panqiyi/pqimg/raw/master/20201124113132.png)

然后到 Typora中ctrl+v 即可粘贴图片；

这里给个我用的这个截图软件的百度云盘链接：Snipaste

**下面我们就来实现 粘贴图片到Typora中后：** <font color='orange'>**图片地址自动变为网上的**</font>

就像下面

![image-20201124114353087](https://gitee.com/panqiyi/pqimg/raw/master/20201124114353.png)

复制粘贴的图片原本地址是C盘下某个文件的，这里粘贴后会**自动**变成了网上路径 。       

**实现步骤：**

**1、下载安装node.js    **（防止PicGo安装插件失败！）

链接：https://pan.baidu.com/s/1VCbVzq27jTbQ-jKPKC36sA 
提取码：3enb 

**2、下载安装PicGO**

链接：https://pan.baidu.com/s/1mB6gBoGIF8CCaXHadkcQ1w 
提取码：6aq9 

**3、**如果没有**Typora**（0.9.86版本以上）这里也可下载：

链接：https://pan.baidu.com/s/1BVf-rpJSe7lKlBcvgaAjJA 
提取码：v0aq 

**配置步骤：**

**步骤1、**去gitee（码云）上**注册一个账户**

- 创建一个仓库用于存储上传的图片

![image-20201124115355358](https://gitee.com/panqiyi/pqimg/raw/master/20201124115355.png)

<img src="https://gitee.com/panqiyi/pqimg/raw/master/20201124115700.png" alt="image-20201124115700467" style="zoom:80%;" />

<img src="https://gitee.com/panqiyi/pqimg/raw/master/20201124115801.png" alt="image-20201124115801842" style="zoom:80%;" />

**步骤2、 PicGo的配置**

1、点击**插件配置**，搜索gitee,  安装gitee-uploader 

<img src="https://gitee.com/panqiyi/pqimg/raw/master/20201124120127.png" alt="image-20201124120127802" style="zoom:80%;" />

2、打开 **图床设置** ---> 找到gitee 点击 

<img src="https://gitee.com/panqiyi/pqimg/raw/master/20201124120553.png" alt="image-20201124120553600" style="zoom:80%;" />

**repo:** 1、打开码云 ----> 2、点击存储上传图片的仓库

<img src="https://gitee.com/panqiyi/pqimg/raw/master/20201124120842.png" alt="image-20201124120841973" style="zoom:80%;" />

<img src="https://gitee.com/panqiyi/pqimg/raw/master/20201124121004.png" alt="image-20201124121004777" style="zoom:67%;" />

repo这行就是填这个你自己复制下来的内容，这里我的是上图的：panqiyi / pqimg

**branch :** 就填 master

**token :** 填私人令牌，令牌获取步骤如下：

1、打开设置

<img src="https://gitee.com/panqiyi/pqimg/raw/master/20201124121444.png" alt="image-20201124121444287" style="zoom: 80%;" />

2、下拉 点击私人令牌

![image-20201124121601400](https://gitee.com/panqiyi/pqimg/raw/master/20201124121601.png)

3、点击生成令牌

![image-20201124121651841](https://gitee.com/panqiyi/pqimg/raw/master/20201124121651.png)

4、选择 projects, 然后提交

<img src="https://gitee.com/panqiyi/pqimg/raw/master/20201124121744.png" alt="image-20201124121743982" style="zoom:80%;" />

5、输入密码 

<img src="https://gitee.com/panqiyi/pqimg/raw/master/20201124121937.png" alt="image-20201124121937686" style="zoom:80%;" />

6、复制

<img src="https://gitee.com/panqiyi/pqimg/raw/master/20201124122052.png" alt="image-20201124122052069" style="zoom:67%;" />

**然后到PicGo选项 token中粘贴即可！**



**打开PicGo设置 选项：**

1、 设置如下图

<img src="https://gitee.com/panqiyi/pqimg/raw/master/20201124122643.png" alt="image-20201124122643476" style="zoom:67%;" />

2、点击 设置 Server 选项

<img src="https://gitee.com/panqiyi/pqimg/raw/master/20201124122844.png" alt="image-20201124122844453" style="zoom:67%;" />

3、配置同如下图

<img src="https://gitee.com/panqiyi/pqimg/raw/master/20201124123021.png" alt="image-20201124123021791" style="zoom:80%;" />



**步骤3：Typora的配置：**

1、打开Typora  点击文件、选择偏好设置

<img src="https://gitee.com/panqiyi/pqimg/raw/master/20201124123223.png" alt="image-20201124123223499" style="zoom:67%;" />

2、配置如下图

<img src="https://gitee.com/panqiyi/pqimg/raw/master/20201124123543.png" alt="image-20201124123543049" style="zoom:67%;" />

3、验证成功：

<img src="https://gitee.com/panqiyi/pqimg/raw/master/20201124123650.png" alt="image-20201124123650923" style="zoom:80%;" />

<font color='red' size=6>到这里配置就大功告成了！</font>



使用时，写笔记或者文章中，将图片放到Typora中后，图片路径地址就会自动变换成 自己建立的图床 地址！

这样图片就是存储再gitee码云上面了，图片地址在其他网站也有效果，

<font color='orange'>所以文章发布到其他平台也不会出现图片导不出来的问题！！</font>



<img src="https://gitee.com/panqiyi/pqimg/raw/master/20201124124553.png" alt="image-20201124124553667" style="zoom:80%;" />