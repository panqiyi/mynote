# Bootstrap

## 概念

一个前端开发的框架，Bootstrap

框架：一个半成品软件，开发人员可以在框架基础上，在进行开发，简化编码

**好处：**

​	**1、定义了很多的css样式和js插件**。我们开发人员直接可以使用这些样式和插件得到丰富的页面效果，简便开发。

​	**2、响应式布局**：同一套页面可以兼容不同分辨率的设备



##  环境配置

**1、下载Bootstrap**

网址：https://www.bootcss.com/

<img src="https://gitee.com/panqiyi/pqimg/raw/master/20201220191600.png" alt="image-20201220191600061" style="zoom: 67%;" />

<img src="C:\Users\panqiyi\AppData\Roaming\Typora\typora-user-images\image-20201220191653830.png" alt="image-20201220191653830" style="zoom:67%;" />

<img src="https://gitee.com/panqiyi/pqimg/raw/master/20201220192955.png" alt="image-20201220192955859" style="zoom:67%;" />

**2、将下载的文件资源复制到项目下**

![image-20201220200536281](https://gitee.com/panqiyi/pqimg/raw/master/20201220200536.png)

![image-20201220200549573](https://gitee.com/panqiyi/pqimg/raw/master/20201220200549.png)

还有jquery框架文件导入到js中(此另下载)

![image-20201220202311029](https://gitee.com/panqiyi/pqimg/raw/master/20201220202311.png)

**3、在html文件中引入必要资源文件**

直接复制如下，修改对应路径

```html
<!DOCTYPE html>
<html lang="zh-CN">
<head>
    <meta charset="utf-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1">
    <!-- 上述3个meta标签*必须*放在最前面，任何其他内容都*必须*跟随其后！ -->
    <title>Bootstrap 101 Template</title>

    <!-- Bootstrap -->
    <link href="css/bootstrap.min.css" rel="stylesheet"> <!--导入css下的bootstrap.min-->

    <!-- 以下两句为了兼容ie浏览器-->
    <script src="//cdn.bootcss.com/html5shiv/3.7.2/html5shiv.min.js"></script>
    <script src="//cdn.bootcss.com/respond.js/1.4.2/respond.min.js"></script>

</head>
<body>
<h1>你好，世界！</h1>


<script src="js/jquery-3.2.1.min.js"></script> <!--导入js下的jq.min-->
<script src="js/bootstrap.min.js"></script> <!--导入js下的bootstrap.min-->
</body>
</html>
```

注意：

带min的是压缩版，体积小，传输速度快，引入html时一般用min版的

![image-20201221084417567](https://gitee.com/panqiyi/pqimg/raw/master/20201221084417.png)

不带min的正常版一般用于阅读。



## 响应式布局

同一套页面可以兼容不同分辨率的设备

### 栅格系统

**实现：**<font color=orange>依赖于栅格系统：将一行平均分成12个格子，可以指定元素占几个格子</font>

**步骤：**

​	**1、定义容器**。相当于之前的table

```
容器分类：
1、container  :两边留白
2、container-fluid : 每一种设备都是100%宽度
```

​	**2、定义行**。相当于之前的 tr 。 样式：row

​	**3、定义元素**。指定该元素在不同的设备上，所占有的格子(列)数目。样式：col-设备代号-格子数目

```
设备代号：
1、xs: 超小屏幕 手机 (<768px)：col-xs-12
2、sm: 小屏幕 平板 (>=768px)
3、md: 中等屏幕 桌面显示器 (>=992px)
4、lg: 大屏幕 大桌面显示器 (>=1200px)
```

如下：记得先引入资源文件，即上面的  “3、在html文件中引入必要资源文件”

```html
<div class="container-fluid"><!--定义容器-->
    <div class="row"><!--定义行-->
        <!--定义元素
        中显示器（笔记本）一行显示12个
        平板一行显示6个 -->
        <div class="col-md-1 col-sm-2 inner">栅格系统</div>
        <div class="col-md-1 col-sm-2 inner">栅格系统</div>
        <div class="col-md-1 col-sm-2 inner">栅格系统</div>
        <div class="col-md-1 col-sm-2 inner">栅格系统</div>
        <div class="col-md-1 col-sm-2 inner">栅格系统</div>
        <div class="col-md-1 col-sm-2 inner">栅格系统</div>
        <div class="col-md-1 col-sm-2 inner">栅格系统</div>
        <div class="col-md-1 col-sm-2 inner">栅格系统</div>
        <div class="col-md-1 col-sm-2 inner">栅格系统</div>
        <div class="col-md-1 col-sm-2 inner">栅格系统</div>
        <div class="col-md-1 col-sm-2 inner">栅格系统</div>
        <div class="col-md-1 col-sm-2 inner">栅格系统</div>
    </div>
</div>
```

效果：使用container-fluid容器时：占满

![41](https://gitee.com/panqiyi/pqimg/raw/master/20201221151024.gif)

使用 container 容器时: 两边留白

![42](https://gitee.com/panqiyi/pqimg/raw/master/20201221151322.gif)

**注意：**

1、一行中如果格子数超过12，则超出部分自动换行

2、栅格类属于向上兼容。栅格类适用于与屏幕宽度大于或等于分界点大小的设备

3、如果使用的设备宽度小于设置的栅格类属性的设备代码最小值，会一个元素占满一行

**列偏移**

现想让第二行红色背景的盒子移动到右边

![image-20201221202429327](https://gitee.com/panqiyi/pqimg/raw/master/20201221202429.png)

```
添加类名：col-md-offset-4   因为红的每个占4个栅格，所以值为 12-2*4=4
```

![image-20201221202751609](https://gitee.com/panqiyi/pqimg/raw/master/20201221202751.png)

**栅格盒子嵌套**

嵌套时，记得写上 row类来包含，此时这个父盒子就有12个栅格给子盒子分

```html
<div class="row"> <!--在上面左红盒子内嵌套-->
    <div class="col-md-6 s">子1</div>
    <div class="col-md-6 s">子2</div>
</div>
```

![image-20201221203553923](https://gitee.com/panqiyi/pqimg/raw/master/20201221203553.png)

**响应式工具**

![image-20201221200854676](https://gitee.com/panqiyi/pqimg/raw/master/20201221200854.png)



## css样式&js插件

### 全局css样式

**1、按钮**

为 `<a>`、`<button>` 或 `<input>` 元素添加按钮类，即可使用 Bootstrap 提供的样式。

```
class="btn btn-default"
```

**2、图片**

```
class="img-responsive" ：添加该类的图片，可以在任意尺寸显示都占100%
```

图片形状

```
class="img-rounded" ：方形
class="img-circle" ：圆形
class="img-thumbnail" ：相框
```



**3、表格**

自定义一个表格

![image-20201221205643792](https://gitee.com/panqiyi/pqimg/raw/master/20201221205643.png)

添加如下类名：

```
table  //基础表格
table-bordered     //有线条的表格
table-hover   //鼠标悬停有效果
```

<img src="https://gitee.com/panqiyi/pqimg/raw/master/20201221210655.png" alt="image-20201221210655879" style="zoom:80%;" />

**4、表单**

进入文档复制使用，再进行结构与样式修改

### 组件

**导航条**

**分页栏**

去文档复制代码，再根据需要修改即可

### 插件

**轮播图**

去文档的js插件下，点击如下，将轮播图代码复制，修改图片路径等

![image-20201221213718332](https://gitee.com/panqiyi/pqimg/raw/master/20201221213718.png)

