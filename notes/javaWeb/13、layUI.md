## layUI

### 下载

网址：https://www.layui.com/      点击下载解压即可

![image-20210517184234411](https://gitee.com/panqiyi/pqimg/raw/master/20210517184234.png)

### 引入

1、将下载的layUI文件复制到项目下

![image-20210517184903935](https://gitee.com/panqiyi/pqimg/raw/master/20210517184903.png)

layUI文件目录：

![image-20210517184445288](https://gitee.com/panqiyi/pqimg/raw/master/20210517184445.png)

2、引入到项目文件中

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
    <!--引用layUI的核心css样式文件-->
    <link rel="stylesheet" href="../layui-v2.6.6/layui/css/layui.css">
    <!--引入layUI的核心js文件,(需要用到组件 或者 基本元素需要依赖模块时再引js)-->
  	<script src="../layui-v2.6.6/layui/layui.js"></script>
    
   
</head>
<body>
    
    <!--你的代码-->
    
    <!--当使用某基本元素或者组件时，官方文档上面指明需要依赖模块则设置依赖模块，否则不需要-->
    <!--导入模块的格式：如下面导入layer和form模块，在<script>标签内设置-->
    <script>
layui.use(['layer', 'form'], function(){
  var layer = layui.layer
  ,form = layui.form;
  
});
</script> 
    </body>
```

```html
<!--当导入一个模块时可用字符串，多个模块用数组-->
    <script>
layui.use('element', function(){
  var element = layui.element
});
</script> 
```

### 布局：栅格系统

跟bootstrap一样：<font color=orange>响应式布局依赖于栅格系统：将一行平均分成12个格子(列)，可以指定元素占几个格子(列)</font>

**1、定义容器**。相当于之前的table

```
容器分类：
1、layui-container  :两边留白
2、layui-fluid : 每一种设备都是100%宽度
```

`<div class="layui-container" style="height: 500px;background-color: orange;">` ：如下

<img src="https://gitee.com/panqiyi/pqimg/raw/master/20210517191156.png" alt="image-20210517191156835" style="zoom: 33%;" />

`<div class="layui-fluid" style="height: 500px;background-color: orange;">` : 如下

<img src="https://gitee.com/panqiyi/pqimg/raw/master/20210517191320.png" alt="image-20210517191320382" style="zoom:33%;" />

**2、定义行，定义列**

```
定义行：.layui-row  (设置div类名为layui-row)
定义列：.layui-col-md*
	md设备代号：
		1、xs: 超小屏幕 手机 (<768px)：col-xs-12
		2、sm: 小屏幕 平板 (>=768px)
		3、md: 中等屏幕 桌面显示器 (>=992px)
		4、lg: 大屏幕 大桌面显示器 (>=1200px)
	* : 代表一列占12个格子中的几个，当一行中定义的列数超过了12，那么会自动换行。
响应式规则：栅格会自动根据屏幕的分辨率选择对应的样式效果
```

```html
<div class="layui-container" style="height: 500px;background-color: orange;">
    <div class="layui-row">
        <div class="layui-col-md3" style="background-color: #00F7DE;">3/12</div>
        <div class="layui-col-md3" style="background-color: #00F7DE;">3/12</div>
        <div class="layui-col-md3" style="background-color: #00F7DE;">3/12</div>
        <div class="layui-col-md3" style="background-color: #00F7DE;">3/12</div>
    </div>
</div>
```

![image-20210517214237171](https://gitee.com/panqiyi/pqimg/raw/master/20210517214237.png)

**3、列边距**

```
.layui-col-space*
	* : 代表的是px值*(1~30)
```

**4、列偏移**

```
将添加该class属性值的列向右移动指定列数
	.layui-col-md-offset*
		* : 代表的是列数
```

**5、列嵌套**

```
列之间可以无限嵌套
```

```html
<div class="layui-container" style="height: 500px;background-color: orange;">
    <div class="layui-row">
        <div class="layui-col-md6" style="background-color: #00F7DE;">
            <div class="layui-row">
            <div class="layui-col-md4" style="background-color: yellowgreen;">内部列4/12</div>
            <div class="layui-col-md4" style="background-color: khaki;">内部列4/12</div>
            <div class="layui-col-md4" style="background-color: skyblue;">内部列4/12</div>
            </div>
        </div>
        <div class="layui-col-md6" style="background-color: green;">6/12</div>
    </div>
</div>
```

![image-20210517221018415](https://gitee.com/panqiyi/pqimg/raw/master/20210517221018.png)

### 使用方法

1、点击官网示例，将中意的样式复制粘贴对应代码下来即可(注意有些依赖js代码，别漏复制了)

​			一些基本元素页可直接看文档，也有例子和代码。但组件只有示例有，文档是一些属性详细

2、关于样式属性的一些详细设置与用法，点击文档页面查看。

### 基本元素

**直接去看官方文档和示例**，将**喜欢的样式的class属性设置到对应的标签上**即可

https://www.layui.com/doc/  ：即layUI官网的文档选项

#### 按钮

```
向任意HTML元素设定*class="layui-btn"*，建立一个基础按钮。通过追加格式为*layui-btn-{type}*的class来定义其它按钮风格。内置的按钮class可以进行任意组合，从而形成更多种按钮风格。    
```

```html
<!--class属性值都是去layUI官方文档查看对应样式，然后复制到标签中-->
<button type="button" class="layui-btn">一个标准的按钮</button>
<a href="http://www.layui.com" class="layui-btn">一个可跳转的按钮</a>
<div class="layui-btn">一个按钮</div>
<hr/>
<button  class="layui-btn layui-btn-normal">百搭按钮</button>
<button class="layui-btn layui-btn-radius layui-btn-warm">暖色按钮</button>
<hr/>
<!--图标按钮-->
<button class="layui-btn layui-btn-radius layui-btn-warm">
    <i class="layui-icon layui-icon-cart"></i>  <!--layui-icon-face-smile:图标 去文档看更多图标-->
    购物车</button>

<button class="layui-btn ">
    <i class="layui-icon layui-icon-login-wechat"></i>  <!--layui-icon-face-smile:图标 去文档看更多图标-->
    微信</button>
<!--图标-->
<i class="layui-icon layui-icon-login-wechat" style="font-size: 35px;color: green"></i>
```

![image-20210517224926274](https://gitee.com/panqiyi/pqimg/raw/master/20210517224926.png)

#### 导航

查看官方文档

<img src="https://gitee.com/panqiyi/pqimg/raw/master/20210517230455.png" alt="image-20210517230455520" style="zoom: 67%;" />

发现需要依赖模块，则需要我们设置依赖模块

​	1、导入需要的核心CSS，JS(依赖文件，需要引入css)

​	2、设置依赖模块

​	3、将文档中对应导航样式的代码复制到自己的项目中即可

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
    <!--导入css-->
    <link rel="stylesheet" href="../layui-v2.6.6/layui/css/layui.css">
    <!--导入js-->
    <script src="../layui-v2.6.6/layui/layui.js"></script>
</head>
<body>

<!--将文档中的导航样式代码复制粘贴到这即可-->

<!--设置依赖模块-->
<script>
    layui.use('element',function () {
        var element=layui.element
    });
</script>
</body>
</html>
```

#### 选项卡

都是一样的步骤：

查看文档是否需要依赖模块，需要则导入js并设置对应的依赖模块

1、导入css，js(需依赖模块导入)

2、看文档是否需要设置依赖模块

3、将样式代码复制粘贴到自己的项目即可

#### 表格

都是一样的步骤：

查看文档是否需要依赖模块(静态表格依赖table模块)，需要则导入js并设置对应的依赖模块

1、导入css，js(需依赖模块导入)

2、看文档是否需要设置依赖模块

3、将样式代码复制粘贴到自己的项目即可

#### 表单

与上面一样步骤；

表单常用属性：

```
required             浏览器固定的必填字段
lay-verify			需要验证的类型(required表示必填项，还要邮箱等)
class="layui-input"  提供通用的样式
class="layui-input-inline"  占据浏览器部分宽度
class="layui-input-block"	占据浏览器部分宽度
文本框：
	placeholder		当文本框为空时，默认显示的文本信息
	autocompleter	表单元素是否自动填充(当浏览器缓存中存在相同name属性值时，会填充如密码)
```

#### 颜色

对于样式框架会有默认颜色

<img src="https://gitee.com/panqiyi/pqimg/raw/master/20210518133404.png" alt="image-20210518133404724" style="zoom:50%;" />

但是自己不喜欢就去掉class属性里的颜色值，自己定义样式设置自定义颜色

如：进度条(其他的元素也可)

```html
<div class="layui-progress layui-progress-big" lay-showPercent="yes">
    <div class="layui-progress-bar layui-bg-orange" lay-percent="50%" ></div>
</div>  <!--layui-bg-orange: 框架的自带背景色-->
```

![image-20210518133759681](https://gitee.com/panqiyi/pqimg/raw/master/20210518133759.png)

去掉class的框架自带背景颜色，自己定义样式

```html
<div class="layui-progress layui-progress-big" lay-showPercent="yes">
    <div class="layui-progress-bar " style="background-color: green;" lay-percent="50%" ></div>
</div>
```

![image-20210518133916549](https://gitee.com/panqiyi/pqimg/raw/master/20210518133916.png)



### 组件

#### 颜色选择器

1、引入layUI的核心css和js

2、点击layui官网的实例，下拉到 颜色选择器

<img src="https://gitee.com/panqiyi/pqimg/raw/master/20210518140405.png" alt="image-20210518140405820" style="zoom:80%;" />

3、使用；点击查看代码，将需要的代码复制粘贴

**注意：颜色选择的核心代码为js代码，一定要带上对应的js代码**

例如：

```html
<!--常规-->
<div style="margin-left: 30px;">
    <div id="test1"></div>
    <div id="test2" style="margin-left: 30px;"></div>
</div>

<!--表单赋值-->
<div style="margin-left: 30px;">
    <form class="layui-form" action="">
        <div class="layui-form-item">
            <div class="layui-input-inline" style="width: 120px;">
                <input type="text" value="" placeholder="请选择颜色" class="layui-input" id="test-form-input">
            </div>
            <div class="layui-inline" style="left: -11px;">
                <div id="test-form"></div>
            </div>
        </div>
    </form>
</div>

<script> /*别忘记了复制需要的js代码*/
    layui.use('colorpicker', function() {
        var $ = layui.$
            , colorpicker = layui.colorpicker;
        //常规使用
        colorpicker.render({
            elem: '#test1' //绑定元素
            , change: function (color) { //颜色改变的回调
                layer.tips('选择了：' + color, this.elem, {
                    tips: 1
                });
            }
        });

        //初始色值
        colorpicker.render({
            elem: '#test2'
            , color: '#2ec770' //设置默认色
            , done: function (color) {
                layer.tips('选择了：' + color, this.elem);
            }
        });

        //表单赋值
        colorpicker.render({
            elem: '#test-form'
            , color: '#1c97f5'
            , done: function (color) {
                $('#test-form-input').val(color);
            }
        });
    })
    </script>
```

![image-20210518141338151](https://gitee.com/panqiyi/pqimg/raw/master/20210518141338.png)

#### 评价

1、导入layUI核心css和js

2、到官网找示例

3、复制示例中需要的样式代码(注意复制对应的js)

![image-20210518143027797](https://gitee.com/panqiyi/pqimg/raw/master/20210518143027.png)

如：

```html
<!--普通显示文字-->
<div id="test2"></div>
<!--半星显示文字-->
<div><div id="test4"></div></div>
<!--数字-->
<div><div id="test6"></div></div>

<!--别忘记复制js-->
<script>
    layui.use(['rate'], function() {
            var rate = layui.rate;

        //显示文字
        rate.render({
            elem: '#test2'
            ,value: 2 //初始值
            ,text: true //开启文本
        });

        rate.render({
            elem: '#test4'
            ,value: 3.5
            ,half: true
            ,text: true
        })

        rate.render({
            elem: '#test6'
            ,value: 1.5
            ,half: true
            ,text: true
            ,setText: function(value){
                this.span.text(value);
            }
        })
        })
</script>
```

![image-20210518142722957](https://gitee.com/panqiyi/pqimg/raw/master/20210518142723.png)

#### 轮播

1、打开官网，进入示例页面，下拉选择轮播示例

2、选择中意样式，点击查看代码

3、复制对应的代码(注意复制js)

如：

<img src="https://gitee.com/panqiyi/pqimg/raw/master/20210518144918.png" alt="image-20210518144917912" style="zoom:50%;" />

看上该图片轮播后，点击查看代码。下拉到对应的轮播代码

<img src="https://gitee.com/panqiyi/pqimg/raw/master/20210518145138.png" alt="image-20210518145138729" style="zoom: 67%;" />

​	1、复制粘贴html骨架代码。2、下拉到js，复制对应的js代码

<img src="https://gitee.com/panqiyi/pqimg/raw/master/20210518145404.png" alt="image-20210518145403971" style="zoom:67%;" />

<img src="https://gitee.com/panqiyi/pqimg/raw/master/20210518145436.png" alt="image-20210518145436146" style="zoom:67%;" />



