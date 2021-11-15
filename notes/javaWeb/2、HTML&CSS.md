# HTML&CSS

`pqy笔记`

## HTML

### 概念

Hyper Text Markup Language  :  超文本标记语言

- 超文本：用超链接的方法，将不同资源组织在一起。

  <img src="https://gitee.com/panqiyi/pqimg/raw/master/20201127101015.png" alt="image-20201127101014900" style="zoom:80%;" />

- 标记语言：

  1、由标签构成的语言，<标签名称>  如  html、xml 语言

  2、标记语言不是编程语言！ 

### 基本语法

html文档后缀名 .html  或者  .htm

1、标签分类：

​		1、围堵标签：有开始和结束的一对标签。 如：<html> </html>

​		2、自闭和标签：开始和结束标签在一起。如：<br/>

2、标签可以嵌套

3、在开始标签中可以定义属性。

4、html不区分大小写，建议小写。

### 标签学习

#### 文件标签

- < !DOCTYPE html>：声明标签，html5中用于声明定义该文档是html文档

- html：html文档的根标签

  ​		其lang属性：lang="en" ：en就是指英文网站，zh-CN 就是中文网站。对于浏览器和搜索引擎有作用(如提示是否翻译)

- head：头标签。用于指定html文档的一些属性，和引入外部资源

- title：网页标题标签

- body：体标签

#### 文本标签

注释：<!-- 注释内容 -->

- < h1> …< h6> : 标题标签

- < p>: 段落标签

- < br> : 换行标签

- < hr> : 水平线

- < b>或者< strong> (表强调): 字体加粗 

- < i>或者< em>: 字体斜体

- < del> ：字体删除线标签

- < ins>：下划线

- < font> : 字体标签

  ```html
  <font color="red" size="6" face="楷体"> 白日依山尽</font>
  ```

  ​	color属性的赋值：

  ​		1、颜色对应的英语单词

  ​		2、rgb(值1，值2，值3)：值得范围 0~255

  ​		3、#值1值2值3：值得范围：00~FF之间。 如：#FF00FF （常用） 

     width：属性得赋值：

  ​		1、数值：width='20' , 单位默认 px (像素)

  ​		2、百分比：width=50% : 占比相对于父元素的比例

**注意：**学到CSS后，样式要全部写在CSS中，不推荐写在标签中！



#### 图片标签

- img：展示图片

  ![image-20201127141517979](https://gitee.com/panqiyi/pqimg/raw/master/20201127141518.png)

  ```html
  <img src="../image/nn.jpg" alt="图片信息">
  <img src="ww.jpg">
  <!-- 相对路径 ：
           以 ./ 代表当前目录 (可省略)
           以../代表上一级目录
           -->
  alt属性：当图片没有显示出来时，会显示内容。
  title属性：鼠标悬浮到图片会显示的内容。
  height：设置高度 单位像素
  width：设置宽度 单位像素
  一般情况值设置高与宽的其中一个属性，另一个会等比缩放
  ```



#### 列表标签

常用来布局。

**1、有序列表**

（了解即可，无序列表使用场景较少）

当需要一些排序时才使用，如排行榜。

```html
<ol>
    <li></li> <!--自动生成有序号的-->
    <li></li>
    ……
</ol>
<!--规范：ol里面只能放li。li里面可以放任何标签-->
```

![image-20201127142343676](https://gitee.com/panqiyi/pqimg/raw/master/20201127142343.png)

![image-20201127142528894](https://gitee.com/panqiyi/pqimg/raw/master/20201127142528.png)

**2、无序列表：**

重点：常用于布局

```html
<ul>
    <li></li>
    <li></li>
    ……
</ul>

<!--规范: ul里面只能放li。li里面随便放任何标签-->
```

![image-20201127142955358](https://gitee.com/panqiyi/pqimg/raw/master/20201127142955.png)
注意：黑点可以使用CSS去掉

```css
li{
list-style:none;
}
```

应用：如下一些的很多布局情况。

<img src="https://gitee.com/panqiyi/pqimg/raw/master/20201130115714.png" alt="image-20201130115714566" style="zoom:80%;" />



**3、自定义列表**

常用于网页下方的进一步了解信息链接栏

![image-20201130114452428](https://gitee.com/panqiyi/pqimg/raw/master/20201130114452.png)

```html
<dl>
	<dt>标题</dt>
	<dd>围绕标题的小标题</dd>
	……
</dl>
<!--规范：dl里面只能包含dt和dd。dt,dd里面可放任意标签-->
```



#### 链接标签

- a : 定义一个超链接

  ![image-20201127144052055](https://gitee.com/panqiyi/pqimg/raw/master/20201127144052.png)

![image-20201127145401769](https://gitee.com/panqiyi/pqimg/raw/master/20201127145401.png)

属性：

​		href ：指定访问资源的URL（网络地址），也可以是本地文件路径

​		target ：指定打开资源方式

​				1、_self：默认值，在当前页面打开

​				2、_blank : 在另一个空白页面打开

**锚点标签**： < a href = #目标id属性值> < /a >   :  快速定位到页面的某个位置。

```html
<body id="top">
<a href=#top>返回顶部</a>
</body>
```



#### div、span标签

没有语义，用来做盒子模型，用于网页布局

span：行内标签，又叫内联标签

div：每一个div**独占一行**，叫块级标签

#### 语义化标签

html5中为了提高程序的可读性，提供了一些标签

1、< header> 网页头部标签 

2、< footer> 网页尾部标签

等等



#### 表格标签

![image-20201127204519092](https://gitee.com/panqiyi/pqimg/raw/master/20201127204519.png)

- table：定义表格

   	width：宽度

  ​	 border：边框

  ​     bgcolor：背景色

  ​	 cellpadding：定义内容和单元格的距离

  ​	 cellspacing：定义单元格之间的距离。值为0，则单元格的线会合并为一条

  ​	align：对齐方式

- tr：定义行

   	  bgcolor：背景色

  ​	   align：对齐方式

- td：定义单元格

  ​		colspan：合并列

  ​		rowspan：合并行

- th：定义 表头单元格

<img src="https://gitee.com/panqiyi/pqimg/raw/master/20201127204932.png" alt="image-20201127204932823" style="zoom:80%;" />

- < caption>：表格标题

  <img src="https://gitee.com/panqiyi/pqimg/raw/master/20201127220623.png" alt="image-20201127220623375" style="zoom:80%;" />

- thead：用于包围住表头部分，方便阅读

- tbody：用于包围住表身部分
- tfooter：用于包围表尾部分

**表格 行或者列 合并：**

![image-20201127222019115](https://gitee.com/panqiyi/pqimg/raw/master/20201127222019.png)

合并成为如下：

<img src="https://gitee.com/panqiyi/pqimg/raw/master/20201127222250.png" alt="image-20201127222250133" style="zoom:80%;" />

合并操作要看 合并的结果图 来操作

如这里合并后：第一行有3单元格，第二行变为两个单元格，第三行变为两个单元格。

所以在定义表格时也需要修改单元格数量。

![image-20201127222824357](https://gitee.com/panqiyi/pqimg/raw/master/20201127222824.png)



#### 表单标签

**表单：**

- 概念：用于采集用户输入的数据。用于和服务器进行交互的

- **表单标签：from**：用于定义表单的。在from标签范围中(开始标签与结束标签之间)才能提交数据

  ​     属性：

  ​		**action：**指定提交数据的URL(网址)

  ​		**method：**指定提交方式

  ​				分类：一共7种，2种比较常用

  ​						get：

  ​								1、请求参数会在地址栏中显示 (即封装到请求行中，HTTP协议再讲解)
  
  ​								2、请求参数的大小没有限制
  
  ​								3、不太安全
  
  <img src="https://gitee.com/panqiyi/pqimg/raw/master/20201127232133.png" alt="image-20201127232133053" style="zoom:50%;" />
  
  ![image-20201127231700688](https://gitee.com/panqiyi/pqimg/raw/master/20201127231700.png)
  
  ​						post：
  
  ​								1、请求参数不会在地址栏中显示，会封装在请求体中(HTTP协议后讲解)
  
  ​								2、请求参数大小没有限制、
  
  ​								3、较为安全
  
  
  
  **注意：表单项中的数据要想被提交；必须指定其name属性。**

- **表单项标签：**

- **一、input**：通过type属性值，改变元素展示的样式

  ​			**type属性的值：**

  ​						**1、text：文本输入框**(不写type属性，默认是这个)

  ​						**2、password：密码输入框**

  <img src="https://gitee.com/panqiyi/pqimg/raw/master/20201127235408.png" alt="image-20201127235408103" style="zoom:80%;" />

  ```css
			css属性样式：outline: 0px;  /*单击文本框/按钮时，外部会出现一个高亮轮廓的效果，对，这个就是outline*/
  		设置 outline:none||0px; 都能取消点击时出现的轮廓线
  ```

未设置前：按钮/文本框 点击后都有一个轮廓线条

<img src="https://gitee.com/panqiyi/pqimg/raw/master/20201223093458.gif" alt="44" style="zoom:80%;" />

<img src="https://gitee.com/panqiyi/pqimg/raw/master/20201223093753.gif" alt="45" style="zoom:80%;" />

设置后：点击不会出现一个高亮的轮廓

  <img src="https://gitee.com/panqiyi/pqimg/raw/master/20201223090745.gif" alt="43" style="zoom:80%;" />

  <img src="https://gitee.com/panqiyi/pqimg/raw/master/20201223093825.gif" alt="46" style="zoom:80%;" />

**表单去除历史记录：**

```
方法一：在form表单中添加：autocomplete="off"

<form method="post" action="" autocomplete="off">

方法二：在input框中添加：autocomplete="off"

<input type="text" name="" autocomplete="off" />
```

  						**3、radio：单选框**

  							多个单选框name属性要一样！！

  ![image-20201128000311386](https://gitee.com/panqiyi/pqimg/raw/master/20201128000311.png)

  						注意：如果name值不一样则不是一组单选框，则不能实现多个选项组单选。如下：

![image-20201128000608771](https://gitee.com/panqiyi/pqimg/raw/master/20201128000608.png)

                       注意：一般会给每一个单选框提供value属性，指定其被选中后提交的值（否则没有提交具体选项的值）

```html
  <form action="#" method="get">
    用户名：<input type="text" name="username"><br>
     密码 ：<input type="password" name="password"><br>
    性别：男 <input type="radio" name="gender" value="男">
         女 <input type="radio" name="gender" value="女"><br>
    <input type="submit" value="登录">
  </form>
```

![image-20201128002539227](https://gitee.com/panqiyi/pqimg/raw/master/20201128002539.png)

​                  **input表单项的  checked属性**，可以指定默认值

![image-20201128004336618](https://gitee.com/panqiyi/pqimg/raw/master/20201128004336.png)

  ​					 

  ​			**4、checkbox：复选框**

  ​					也是需要写上value属性值，这样才有选中后提交的对应value值的数据

  ​						![image-20201128003539073](https://gitee.com/panqiyi/pqimg/raw/master/20201128003539.png)

  ​					  checked属性，可以指定默认值

  ​			**input的属性  value :** 给表单输入框默认值

  ![image-20201128004654264](https://gitee.com/panqiyi/pqimg/raw/master/20201128004654.png)

  ​		   

  ​			**input的属性 placeholder：**给表单输入框设置提示内容，输入后提示内容消失

![image-20201128005228906](https://gitee.com/panqiyi/pqimg/raw/master/20201128005229.png)

![2](https://gitee.com/panqiyi/pqimg/raw/master/20201128093504.gif)

```  
readonly="readonly" 属性：文本框不能修改
```

![51](https://gitee.com/panqiyi/pqimg/raw/master/20210429113810.gif)

**label标签：**

定义 input 元素的标注

label的for属性一般会和input 的 id 属性值 相等(对应)，如果相等，则点击label区域的文字，会让input 输入框获取焦点

```html
<label for="user">用户名：</label> <input type="text" name="username" id="user" placeholder="请输入用户名">
```

![image-20201128010601948](https://gitee.com/panqiyi/pqimg/raw/master/20201128010602.png)

![1](https://gitee.com/panqiyi/pqimg/raw/master/20201128093238.gif)

​			    **5、file:**文件选择框

```html
<label for="img">图片：</label><input type="file" name="file" id="img">
```

<img src="https://gitee.com/panqiyi/pqimg/raw/master/20201128102557.gif" alt="3" style="zoom:80%;" />

​			**6、hidden** : 隐藏域。内容不可见，但是会提交

```html
隐藏域：<input type="hidden" name="hidden" value="6x6x6x">
```

<img src="https://gitee.com/panqiyi/pqimg/raw/master/20201128103625.gif" alt="4" style="zoom:80%;" />

​			**7、type属性值：按钮**

​						1、**submit**：提交按钮，可以提交表单

​						2、**button**：普通按钮 (无作用，将来和 js一起使用)

​						3、**image**：图片提交按钮，与submit一样提交表单

​											不过其 src属性可指定图片路径，样式是图片的。

​	type还有一些格式类属性值：如 date 日期  email 邮箱 等等

```html
生日 ：<input type="date" name="生日">
```

![image-20201128110058143](https://gitee.com/panqiyi/pqimg/raw/master/20201128110058.png)





- **二、select：**下拉列表

```html
地区：<select name="地区"> 
    <option>--请选择--</option>
    <option value="北京">北京</option>
    <option value="上海">上海</option>
    <option value="深圳">深圳</option>
    
    <!-- <option value="南京" selected >南京</option> selected:添加该属性为默认选项 -->
</select>
```

注意： select 表单项记得定义name属性，否则不能提交

![5](https://gitee.com/panqiyi/pqimg/raw/master/20201128111434.gif)



- **三、textarea：**文本域

   属性： 

  ​			cols：指定列数，每一行有多少个字

  ​			rows：默认多少行

  ​			设置样式使其不能伸缩改变大小：resize: none;
  
  ![image-20201128112112613](https://gitee.com/panqiyi/pqimg/raw/master/20201128112112.png)

#### 特殊字符表

<img src="https://gitee.com/panqiyi/pqimg/raw/master/20201130114148.png" alt="image-20201130114148643" style="zoom:80%;" />



## CSS

### 概念

![image-20201130122320609](https://gitee.com/panqiyi/pqimg/raw/master/20201130122320.png)

Cascading Style Sheets  ：**层叠样式表**

**作用：**美化页面的，网页布局。

层叠：多个样式可以作用在同一个html元素上，同时生效

**好处：**

1、功能强大

2、将内容展示和样式控制分离

- 降低耦合度，解耦(即样式写在html标签中耦合度高)
- 让分工协作更容易
- 提高开发效率

### CSS与html的结合

**一、内联样式**

通过 style 属性 在标签中定义样式，**此法不推荐**

```html
<!--内联样式-->
<p style="color: red">hello</p>
```

**二、内部样式**

在head 标签内 使用 style 标签，在style 标签中定义样式。

```html
<head>
    
    <style>
        div{
            color: blue;
        }
    </style>
</head>

<body>
<!-- 内部样式-->
<div>world</div>
</body>
```

**三、外部样式**

1、定义css资源文件

2、在 head 标签内，定义 link 标签，引入外部资源文件

```html
<head>
    
    <link rel="stylesheet" href="../css/c.css">
</head>
```

补充：导入外部资源还可以如下(不常用 了解即可)

```html
<head>
    <style>
        @import "../css/c.css";
    </style>
</head>
```

### 语法格式

```css
选择器{
    属性1:属性值1;
    属性2:属性值2;
    ……
}
```

### 选择器

概念：用来筛选一些相似的元素。

#### 基础选择器

**1、id选择器：**选择对应的id属性值的元素

建议：一个html页面中id属性值定义要不同

```
#id属性值{}
```

**2、标签选择器：**选择对应标签的所有标签 (也叫元素选择器，标签=元素)

```
标签名称{}
```

注意：id选择器优先级高于标签选择器

**3、类选择器：**选择具有相同的class属性值的元素

```
.class属性值{}
```

class 属性值多个标签可相同

**多类名：**

一个标签可以指定多个类名，从而可以有多个选择，多类名选择其中的一个都有效。

```html
<div class="aa bb"></div> <!--多个类名中间用空格分开-->
```

**应用场景：**当多个标签有共同的属性时，可以将他们写成多类名形式，减少代码重复

```css
/*如有多个div,他们的宽高都一样 ，就可以将多个div设置多类名，然后选择其相同的一个类名*/
<div class="aa bb"></div>
<div class="aa cc"></div>/*html*/
.aa{
    height:200px;
    width:250px;
}
公共样式就选择aa  独有样式就选择 bb
```



**4、通配符选择器：**选择页面所有元素（标签）

```css
*{}
```

常用于清除所有标签的内外边距（后面会讲）：

```css
*{
    padding:0;
    margin:0;
}
```



#### 复合选择器：

由一些基础选择器的组合。

复合选择器由两个或者多个基础选择器通过不同方式组合而成
包括：后代选择器  子类选择器  并集选择器   伪类选择器  属性选择器

**1、并集选择器：**同时选中多个 , 习惯竖着写

```css
选择器1,
选择器2{}
```

**2、后代选择器：**筛选 选择器1下的选择器2…的其**后代任意**元素

```css
选择器1 选择器2…{} <!--空格隔开-->
```

**3、子选择器：**筛选 父标签下 的**第一层**对应 子标签

```css
选择器1>选择器2{}
如：div>p{} 就会选中div标签内第一层所有的p标签
```

如下：css中: div>p 然后设置颜色属性为下图橙色。

![image-20201128200019881](https://gitee.com/panqiyi/pqimg/raw/master/20201128200019.png)



**4、属性选择器：**可以根据标签的属性及属性值来选择标签。

属性选择器在为不带有 class 或 id 的**表单**（input）设置样式时特别有用

```css
标签[属性]{} 或者 标签[属性="属性值"]{}
```



**5、伪类选择器：**用于向某些选择器添加特殊的效果

```
格式-用冒号分隔 
 选择器：效果
```

**1、链接伪类选择器：**

```css
a:link{}  /*选中所有未点击访问链接*/
a:visited{} /*选中所有已点击访问链接*/
a:hover{} /*选中鼠标指向悬停的链接*/
a:active{} /*选中活动链接(即点击未松开)*/
```

如下：

![image-20201128221850830](https://gitee.com/panqiyi/pqimg/raw/master/20201128221850.png)

![6](https://gitee.com/panqiyi/pqimg/raw/master/20201128221923.gif)

**注意：**

1、为了确保效果生效，按照<font color=red>LVHA</font>的顺序声明
2、标签有默认样式，需要单独对a指定样式，如对其父标签或者对body指定文本颜色对a无效



**2、:focus伪类选择器：**选中哪一个表单 ， 该表单就获取光标，并使用样式

```css
input:focus{}
```

如：

```css
input:focus{
    background-color: #fa7f1c;
}
```

![6](https://gitee.com/panqiyi/pqimg/raw/master/20201130135743.gif)



### 选择器优先级

!important > 行内样式 > ID选择器 > 类选择器、伪类选择器 > 元素选择器 > 通配符选择器



### 属性

#### 字体

**1、font-family：**设置字体系列

```css
font-family:字体1,字体2,字体3,字体4;/*浏览器依次从字体1开始使用  没有则顺序使用  当字体名字有空格时 该字体用单引号括起来*/
```

**2、font-size：**设置字体大小   浏览器默认值为16px

**3、font-weight：**设置字体粗细

```css
font-weight:normal|bold|bolder|lighter;
			/*正常 粗体  特粗   细体  */
常用数字表示:100|200|300|400|500|600|700|800|900;	/*700=粗体  400=正常  */	
```

**4、font-style：**字体样式，正常与斜体

**font复合写法：**

```css
p{
font: 样式 粗细 大小/行高 字体系列;
}
```



#### 文本

**1、color：**文本颜色

**2、text-align：**文本对齐方式

**3、text-decoration：**装饰文本，即加 上中下线。链接标签用其取值为none时则无下划线。

**4、line-height：**设置行间距(行与行之间的距离)

行间距=文本高度+上下间距

```css
line-height:1.5;/*行高则是当前文字大小的1.5倍*/
line-height:24px;/*像素值*/
```

**5、text-indent：**首行缩进

```css
text-indent:2em;/*即相对当前缩进2个字符*/
```

**注意：** 当如下：文本已居中，想让其到中间 (即垂直居中)？

<img src="https://gitee.com/panqiyi/pqimg/raw/master/20201129001352.png" alt="image-20201129001352353" style="zoom:50%;" />

只需要在css中添加属性：line-height 其属性值与盒子高度相等即可！

<img src="https://gitee.com/panqiyi/pqimg/raw/master/20201129001555.png" alt="image-20201129001555321" style="zoom:50%;" />



#### 尺寸

定义块元素 和 行内块元素 的高度和宽度

高度：必须是像素单位   宽度：百分比或者像素单位

```css
height: 150px; /*像素*/
width: 100%;  /*相对于父标签的百分比*/
```



#### 背景

**1、background-color：**设置背景颜色

```css
 background-color: red|transparent;/*红色|透明*/
```

**设置背景颜色半透明：**

```css
div{
    height: 250px;
    background:rgba(35,67,45,0.5); /*前三个值为三原色的值(红绿蓝)，后面的是透明的的值：0~1（0是全透明，1是不透明，值越低透明的越高）*/
}
```

<img src="https://gitee.com/panqiyi/pqimg/raw/master/20201130205812.png" alt="image-20201130205812046" style="zoom:80%;" />



**2、background-image：**设置背景图片

```css
background-image : url( "图片路径" );
```

**3、background-repeat：**设置图片的平铺方式  默认是平铺的(即图片重复铺放)

```css
background-repeat:repeat|no-repeat|repeat-x|repeat-y
				/*平铺  不平铺     x轴平铺   y轴平铺 */
```

**4、background-position：**调整背景图片的位置

```css
background-position:x y;/*水平方向的  垂直方向的*/
如：
/*1、值为方向名称*/
background-position:left center; /*水平 左中右：left|center|right  垂直 上中下: top|center|bottom*/
注意：当只写一个方位名词时，如果是水平方向的，那垂直方向的就默认是居中，反正亦然。
background-position:top; /*那么水平方向就默认 center*/

/*2、值为精确值*/
background-position:20px 50px;

/*3、值为混合单位*/
background-position:20px center;
```

**5、background-attachment：**背景图像固定   用于做 视差滚动 的效果  如QQ官网

<img src="https://gitee.com/panqiyi/pqimg/raw/master/20201130204707.gif" alt="9" style="zoom:80%;" />

```css
background-attachment:scroll|fixed;/*滚动|固定*/ 取值为fixed就会有如上效果，下拉时背景图片没动
```

**background背景复合写法：**

```css
background:颜色 url("图片地址") 背景平铺 背景固定 背景位置;
```

#### 鼠标

```
cursor: not-allowed;  //鼠标变禁用样式
cursor: pointer; //鼠标变小手样式
```



### Emmet语法

使用缩写来提高html/css的编写速度。

**1、快速生成HTML结构的语法：**

![image-20201130132316611](https://gitee.com/panqiyi/pqimg/raw/master/20201130132316.png)

```html
如6: .name$*5 按tab键 就会生成5个div 类名：name1~name5
如5还可以：input.cc 就会生成类名=cc的表单，其他标签也一样，p.name$*5 +tab 会生成5个p标签 类名：name1~5
```

**2、快速生成CSS样式的语法：**

写样式属性与属性值时，只需要写单词字母开头+tab键即可自动生成属性。

如下等等：

```css
.name1{
    text-align: center; /*ta 然后选择，因为单词开头t和a的属性也多*/
    tab-index: 2em; /*ti +tab*/
    width: 200px; /*w200 +tab*/
    height: 300px; /*h300 +tab*/
    tab-index: 2em; /*ti +tab*/
    line-height: 26px; /*lh +tab*/
    text-decoration: none; /*td +tab*/
    background-color: #fff; /*bgc +tab*/
    background-image: url(); /*bgj +tab*/
}
```



### 显示模式

显示模式：标签(元素)以什么方式显示

元素的显示模式
将标签分为不同的种类，方便布局。
标签分为两大类：块元素，行内元素。

#### 块元素

h1-h6, div, p , ul , ol , dl ,li 等
div是最经典的块元素

**特点：**
1.独占一行

2.高度，宽度，内外边距都可以调

3.如果没有给宽度，宽度默认占父标签100%

4.是一个容器，可以放块元素或者行内元素

**注意：**<font color=red>文本块元素内不能放块级元素，如p，h</font>



#### 行内元素

a , strong, em ,del , ins , b , i , span 等
span标签是最经典的行内元素

**特点：**

1.相邻的行内标签在一行上显示，一行内显示多个标签

2.高，宽直接设置是无效的（行内替换元素除外）

3.默认宽度是它内容的宽度

4.行内元素只能放文本和其他行内元素，不能放块元素

**注意：**

<font color=red>1、a链接标签里面不能放a标签</font>

<font color=red>2、 a链接标签较特殊，可以放块元素，但最好先模式转换为块元素</font>

3、行内块元素设置上下内外边距无效，所以<font color=orange>只设置左右内外边距</font>。(但是转换为 块元素/行内块元素 就可以)



##### 行内块元素

​		**行内替换元素：**是浏览器根据元素的标签和属性，来决定元素的具体显示内容。
如img , input 。img浏览器会根据src路径来显示图片，input浏览器会根据type属性来觉得显示样式。

这几种特殊的元素又叫做行内块元素：< img/>、< input/>

<font color=red>特点：一行内可以有多个、又可以设置高，宽，和内外边距</font>



### 标签显示模式转换

一个模式需要另一个模式的特性时，我们需要去转换

如：想增加< a> 链接的触发范围：本来链接只有在"手机 电话卡"字上的效果，但是模式转换后可以点击整个盒子来触发。

![image-20201130194612408](https://gitee.com/panqiyi/pqimg/raw/master/20201130194612.png)

```css
a{
    display:block; /*转换为块元素 (常用)*/
}
```

```css
div{
	display:inline; /*转换为行内元素*/
}
```

```css
div{
    display:inline-block; /*转换为行内块元素 (常用)*/
}
```



### CSS三大特性

**1、层叠性：**

<font color=red>相同选择器</font>设置相同的样式，此时后面一个样式就会覆盖(层叠)前一个冲突样式(一样的属性)

层叠性原则：

1、样式冲突后用最后一个选择器的样式

2、后面的选择器只会层叠前面相同的属性样式，没有冲突的属性不覆盖(层叠)

![image-20201130211200459](https://gitee.com/panqiyi/pqimg/raw/master/20201130211200.png)

像上面，就覆盖了冲突的属性color，而前面的font-size依然生效



**2、继承性：**

子标签会继承父标签的样式

如：

```css
body{
    color: red;
}
```

此时页面内所有的文字都会变成红色，当标签自己设置了color属性时，就会用自己的(特性1的层叠性)

**可以继承的样式：**关于文本和文字的(text-，font-，line-，color)

**3、优先级：**

!important > 行内样式 > ID选择器 > 类选择器、伪类选择器 > 元素选择器 > 通配符选择器



### 盒子模型

用于布局的

##### 边框

**border：**定义边框

注意：加边框的盒子大小= 边框粗细+盒子大小

border-top 上边框  border-left 左边框  等等

```css
border:1px  solid  red; /*solid实线  dashed虚线 dotted点线*/
	 /*粗细 线条样式  颜色*/  /*|transparent 透明色*/
```

**border-radius：**定义圆角边框

```css
border-radius:30px;/*四个角都一个值*/
border-radius:10px 40px;/*两个对角线关系*/
```

![image-20201129000301964](https://gitee.com/panqiyi/pqimg/raw/master/20201129000302.png)



##### 内、外边距

**1、padding：**内边距，调整 盒子边框与盒子内部的距离

padding-left    top  right  bottom  四个方向

**内边距复合写法：**

<img src="https://gitee.com/panqiyi/pqimg/raw/master/20201129143725.png" alt="image-20201129143725613" style="zoom:80%;" />

**注意：**padding会影响盒子大小(没有设置宽度不影响盒子大小)   加了多少padding值 在盒子原来大小(高宽)减去加的padding值  盒子就大小不变



**2、margin：**外边距，盒子与盒子间的距离

也是margin-left \top\right\bottom。与 padding 写法一致。

```css
margin:0 auto;/*块级元素居中对齐*/
注意：行内元素或者行内块元素水平居中 给其父元素添加 text-align: center; 即可
```

**注意：**行内块元素设置上下内外边距无效，所以只设置左右内外边距。(但是转换为 块元素/行内块元素 就可以)



**嵌套关系的垂直外边距塌陷问题：**

如下 红色父盒子 margin-top: 20px; 

<img src="https://gitee.com/panqiyi/pqimg/raw/master/20201130222455.png" alt="image-20201130222455468" style="zoom:50%;" />

然后现在想让 粉色子盒子 margin-top: 40px; 想让它离父盒子顶部40px

<img src="https://gitee.com/panqiyi/pqimg/raw/master/20201130222911.png" alt="image-20201130222911354" style="zoom:50%;" />

结果却是父盒子的margin-top变成了40px!!

**解决方案：**

1、为父元素定义上边框（定义一个透明色边框）

2、为父元素定义内边距（给父标签添加一个很小的内边距，如1px）

**3、**为父元素添加 overflow : hidden  (常用)

其他方法：如浮动、固定、绝对定位 的盒子不会有塌陷问题，后面再学



##### 盒子&文字阴影

**1、盒子阴影**

如下：将鼠标悬浮后，盒子底下就会出现淡淡的阴影效果

<img src="https://gitee.com/panqiyi/pqimg/raw/master/20201130231339.gif" alt="10" style="zoom: 67%;" />

```css
box-shadow:0 5px 20px 5px black;
/*第一个值1、水平阴影方向 (正值向右，负值向左) 
	     2、垂直阴影方向 (正值向下，负值向上)
	     3、模糊程度 (即颜色的虚实程度，0为纯色，值越大越虚)
		 4、阴影大小 
		 5、阴影颜色(可用rgba())*/ 默认是外阴影，一般也都是用的外阴影，所以不用写

box-shadow: black 0 0 10px; 盒子四周添加阴影
```

![image-20201130231618705](https://gitee.com/panqiyi/pqimg/raw/master/20201130231618.png)

如下，实现鼠标悬浮到盒子上呈现阴影

```css
div:hover{
    box-shadow: 0px 10px 10px 0px rgba(0,0,0,0.3);
} /*这里只写了鼠标悬浮在div盒子时的伪类选择器样式，盒子的样式省略了*/
```

<img src="https://gitee.com/panqiyi/pqimg/raw/master/20201130235103.gif" alt="11"  />

****

**2、文字阴影**

```css
text-shadow:水平方向  垂直方向 模糊程度 阴影颜色; /*设置和效果与盒子阴影一样*/
```



![image-20201201103106212](https://gitee.com/panqiyi/pqimg/raw/master/20201201103106.png)



### 浮动

#### 标准流

就是标签按照默认方式排列

1、块级元素会独占一行，从上向下顺序排序

2、行内元素会按照顺序，从左到右顺序排序，碰到元素边缘则自动换行

之前学习的都是标准流，就是正常的布局。

**为什么要用浮动？**

<img src="https://gitee.com/panqiyi/pqimg/raw/master/20201201105914.png" alt="image-20201201105914390" style="zoom:67%;" />

我们第一时间可能会想到使用 前面标准流的 将块级元素 显示模式转换为 行内块元素 。效果如下图

<img src="https://gitee.com/panqiyi/pqimg/raw/master/20201201110220.png" alt="image-20201201110220662" style="zoom:80%;" />

**注意：**提前已经清除了网页的内外边距，但是盒子之间还是会有默认的距离，这样不方便我们进行开发。



<img src="https://gitee.com/panqiyi/pqimg/raw/master/20201201110456.png" alt="image-20201201110456126" style="zoom:67%;" />

上面的这个效果就很难用标准流去实现。

想上面这些标准流没办法完成的布局就可以用浮动来完成！！

**浮动属性：float**

浮动可以改变标签的默认排列方式

经典应用：**让多个块级元素在一行内排列显示**

**网页布局第一准则：**多个块级标签纵向排列找标准流，多个块级标签横向排列用浮动



#### 浮动特性

**1、浮动的标签会脱离标准流(脱标)**

- 脱离标准流，<font color=red>漂浮</font>移动到指定位置，即脱标

- 浮动的盒子<font color=#F24E3D>不再保留原先的位置</font>，原来位置会被后面的标准流标签占有

- 浮动不会覆盖文字，定位会

  ​       如下：给红色的块元素盒子添加浮动：

  <img src="https://gitee.com/panqiyi/pqimg/raw/master/20201201112806.gif" alt="12" style="zoom:67%;" />

**2、多个块级元素都添加浮动，会按照排序在一行内显示(且上边框对齐)**

​			如下：给四个块级元素的盒子都添加了左浮动

<img src="https://gitee.com/panqiyi/pqimg/raw/master/20201201115406.gif" alt="14" style="zoom:50%;" />

​         	 **注意：**浮动元素是互相贴靠在一起的(无空隙)，如果父级标签装不下这些浮动的盒子，多出的盒子会另起一行对齐显示

**3、任何元素都能添加浮动，浮动后都具有<font color=#F24E3D>行内块元素</font>相似特性**

- 如果标准流块元素没有设置宽度，默认宽度和父级一样宽。但添加浮动后没有设置宽度，宽度根据内容大小决定。
- 行内元素添加浮动就可以设置宽高，具有行内块元素特点。

#### 浮动使用

```css
{
float:left|right;
}
```

<font color=orange>先用标准流的父元素排列上下位置，然后内部子元素采用浮动排列左右位置，符合网页布局的第一准则</font>

<img src="https://gitee.com/panqiyi/pqimg/raw/master/20201201121638.png" alt="image-20201201121638124" style="zoom:67%;" />

**使用浮动布局的注意事项：**

**1、浮动搭配标准流父盒子使用**

​		上面已说了

**2、一个元素浮动，其兄弟元素也要浮动**

​		如一个标准流父盒子里面有多个子盒子，如果其中一个子盒子浮动，其兄弟盒子也应该浮动，避免出现问题

**3、浮动的盒子<font color=red>只会影响后面的标准流盒子</font>，不会影响前面的标准流**

粉盒子浮动，其位置会被后面的标准流占有

<img src="https://gitee.com/panqiyi/pqimg/raw/master/20201201141137.gif" alt="15" style="zoom:67%;" />



#### 清除浮动

浮动子元素的标准流父盒子一定要加高度吗？？ 那当子盒子很多或者子盒子数量不断更新 岂不是很麻烦，那有没有什么方法是让父盒子的高度是随着子盒子数量的变化而变化呢？

1、首先我们可能想到 试一下让标准流父盒子不设置高度的效果 :

​           1.1、 一开始如下：父盒子设置了高度，子盒子浮动

<img src="https://gitee.com/panqiyi/pqimg/raw/master/20201201143703.png" alt="image-20201201143703337" style="zoom:50%;" />

​			1.2、然后去除父盒子的高度，如下：父盒子的位置被下面的盒子占了

​             											 <img src="https://gitee.com/panqiyi/pqimg/raw/master/20201201144018.gif" alt="16" style="zoom: 50%;" />

**因为**很多情况下我们不方便定义父盒子高度，但是不设置父盒子高度时 ，子盒子浮动又不占有位置，所以就会影响下面的标准流。



那么我们怎样做才能不影响下面的盒子呢？？

<font color=orange>为了解决上面的问题，所以我们要使用 </font><font color=orange size=4> 清除浮动</font>



**使用清除浮动：**

<font color=#F24E3D>清除浮动后，父盒子就会根据 浮动的子盒子 自动检测高度。父级有了高度就不会影响到下面的标准流了</font>

清除浮动本质：清除浮动元素脱离标准流造成的影响。

去除浮动的策略：闭合浮动，只让浮动影响父盒子里面，对外面的盒子不产生影响

**清除浮动方法：**

![image-20201201152613554](https://gitee.com/panqiyi/pqimg/raw/master/20201201152613.png)

- **1、额外标签法(隔墙法)：**

     1.1、在子元素最后添加一个空标签，如< br/>，然后添加 clear : both; 样式  如下：

  **注意：**空标签必须是 块级标签 或者< br>

  ```html
  <!--行内样式写法-->
  <br style="clear: both"> 
  
  <!--外部样式写法如下-->
  1、先在最后的子盒子后定义任意空标签，如<br> ,<div> 等等
      如这里用了 空的div标签： <div class="clear"></div>
  2、然后去css中写如下内容：
      .clear{
     			clear:both;
      }
  ```

  ​        缺点：多出无用标签，结构较差

  

- **2、父盒子添加 overflow 属性**

  ```css
  .fu{
      overflow:hidden|auto|scroll; /*常用hidden, 这里后面再讲*/
  }
  ```

  缺点：无法显示溢出部分

  

- **3、父级添加 after 伪元素**

  相当于额外标签法的升级版，额外标签需要在html结构中定义一个空标签，这里是通过css生成

  <img src="https://gitee.com/panqiyi/pqimg/raw/master/20201201185424.png" alt="image-20201201185424226" style="zoom:80%;" />

  1、给父盒子标签添加一个 类名为：clearfix

  2、然后在css给父元素添加如下样式

  ```css
  .clearfix:after{
      content: "";
      display: block;
      height: 0;
      clear: both;
      visibility: hidden;
  }
  .clearfix{ /*IE6、7专有*/
      *zoom: 1;
  }
  /*百度 淘宝 网易等*/
  ```

- **父级添加双伪元素**

  <img src="https://gitee.com/panqiyi/pqimg/raw/master/20201201184940.png" alt="image-20201201184940528" style="zoom:67%;" />
  
  1、给父盒子标签添加一个 类名为：clearfix
  
  2、然后在css给父元素添加如下样式                  
  
  ```css
  .clearfix:before,
   .clearfix:after{
       content: "";
       display: table;
   }
  .clearfix:after{
      clear: both;
  }
  .clearfix{
      zoom: 1;
  }
  /*小米 腾讯等*/
  ```
  
  

### 定位

**为什么需要定位？**

我们怎么实现如下效果？

![image-20201202233309905](https://gitee.com/panqiyi/pqimg/raw/master/20201202233310.png)

<img src="https://gitee.com/panqiyi/pqimg/raw/master/20201202234543.gif" alt="17" style="zoom:50%;" />

以上效果，标准流或者浮动都无法快速实现，此时**需要定位来实现。**

1、浮动可以让多个块级盒子在一行内显示，并且盒子间没有空隙，经常用于横向排列盒子。

2、定位则是可以让盒子在某个父盒子里**任意的移动位置** 或者 **固定位置**，并且可以压住其他盒子。

#### 定位组成

**定位=定位模式+边偏移**

定位模式指盒子的定位方式。边偏移则决定了该元素的最终位置。

**1、定位模式：**

通过position属性来设置，其值可以分为四个：

| 值       | 语义     |
| -------- | -------- |
| static   | 静态定位 |
| relative | 相对定位 |
| absolute | 绝对定位 |
| fixed    | 固定定位 |

**2、边偏移**

有top、bottom、left、right 4个属性

![image-20201203091559232](https://gitee.com/panqiyi/pqimg/raw/master/20201203091559.png)

#### 四种定位方式

**1、静态定位 static（了解）**

静态定位是元素 默认定位方式，就是没有定位的意思。跟标准流摆放位置一样，没有边偏移。

```css
选择器{
    position:static;
}
```



**2、相对定位 relative **

1、相对于盒子**原来的位置**进行移动，就是添加定位前的位置 ，跟父元素没有关系。

2、原来在标准流的位置继续占有，**不脱离标准流，继续保留原来位置**。

如：让第一个橙色盒子添加如下相对定位与偏移量

```css
{
    position: relative;
    top: 100px;
    left: 150px;
}
```

<img src="https://gitee.com/panqiyi/pqimg/raw/master/20201203093618.gif" alt="18" style="zoom:67%;" />

**3、绝对定位 absolute  **

1、如果**没有祖先元素**  或者 **祖先元素没有定位**，则以浏览器为准定位

2、如果祖先元素有定位，则**以最近一级的有定位祖先元素为参考点移动位置。**

3、**绝对定位不占有原来位置 (脱标)**

```css
选择器{
    position:absolute;
}
```

**如下1**：橙色的父盒子没有添加定位，然后给绿色子盒子添加绝对定位与边偏移

```css
选择器{
    position: absolute;
    top: 100px;
    left: 50px;
}
```

<img src="https://gitee.com/panqiyi/pqimg/raw/master/20201203105939.gif" alt="19" style="zoom:50%;" />

**如下2**：绿色的子盒子会以 **最近一个有定位的祖先元素** 为参考点移动，即红色的盒子

<img src="https://gitee.com/panqiyi/pqimg/raw/master/20201203111532.png" alt="image-20201203111532603" style="zoom:50%;" />

**子绝父相：**

**因为父级需要占有位置，因此是相对定位，子盒子不需要占有位置，则是绝对定位。**

如下：

<img src="https://gitee.com/panqiyi/pqimg/raw/master/20201203113754.png" alt="image-20201203113754705" style="zoom: 67%;" />

**4、固定定位：**

**1、以浏览器的可视窗口为参照点移动元素**

如下：浏览器窗口变小了，它依然在最左边，是参照浏览器可视窗口的

<img src="https://gitee.com/panqiyi/pqimg/raw/master/20201203141731.gif" alt="21" style="zoom:67%;" />

- 跟父元素没有任何关系、
- 不随滚动条滚动

**2、固定定位不在占有原先的位置（脱标）**

<img src="https://gitee.com/panqiyi/pqimg/raw/master/20201203142017.gif" alt="22" style="zoom:67%;" />

```css
选择器{
    position:fixed; /*定位模式*/
    top:0;  /*偏移量*/
    left:0;
}
```

**固定定位小技巧：固定在版心右侧位置**

如下：那个 向上箭头的盒子 是一直跟随版心的，缩放也一样。 

<img src="https://gitee.com/panqiyi/pqimg/raw/master/20201203143931.gif" alt="23" style="zoom:67%;" />

**做法：**

1、让固定定位盒子left: 50% 到浏览器可视的一半(也是版心一半)

2、让固定定位的盒子 margin-left：版心宽度的一半距离。



除了上面4种定位还有一种粘性定位 sticky ，这个兼容性差，几乎不用，了解即可。



**定位叠放次序 z-index**

在使用定位布局时，可能会出现盒子重叠的情况。此时使用z-index属性来控制盒子 的前后顺序。

```css
选择器{
    z-index: 1;  /*默认值是auto, 数值：正数，负数，0；数值越大，盒子越靠上*/
}
```

- 如果属性值相同，则按照书写顺序，后来者居上。

- 数字后面不能加单位

- 只有定位的盒子才有z-index属性

  

### 元素显示与隐藏

类似网站上的广告，当我们点击关闭，刷新后又出现广告。

本质：让一个元素在页面中隐藏或者显示出来。

**1、display 属性**

display 属性用于设置一个元素如何显示。

- display: none;  隐藏元素
- display: block;  除了转换为块级元素外，同时还用显示元素的意思。

如下：将上面橙色盒子添加display:none; 隐藏；<font color=red>盒子隐藏，并不占有原来位置</font>

<img src="https://gitee.com/panqiyi/pqimg/raw/master/20201204132523.gif" alt="24" style="zoom:67%;" />



**2、visibility 属性**

- visibility : visible;  元素可视
- visibility : hidden;  元素隐藏

 <font color=red>盒子隐藏，占有原来位置</font>

<img src="https://gitee.com/panqiyi/pqimg/raw/master/20201204133408.gif" alt="25" style="zoom:67%;" />

**overflow 属性**

**对溢出盒子部分进行显示/隐藏设置**

如下的块盒子中，默认情况就是会溢出超出范围文字。

<img src="https://gitee.com/panqiyi/pqimg/raw/master/20201204134106.png" alt="image-20201204134106531" style="zoom:67%;" />

- overflow : visible；默认情况；写不写都是显示溢出内容。

- voerflow : hidden;  将溢出部分隐藏。如下：

  <img src="https://gitee.com/panqiyi/pqimg/raw/master/20201204134602.png" alt="image-20201204134602650" style="zoom: 80%;" />

- overflow : scroll;  直接添加滚动条，不过内容有没有溢出。如下：

<img src="https://gitee.com/panqiyi/pqimg/raw/master/20201204135030.gif" alt="26" style="zoom:67%;" />

- overflow : auto;  当内容溢出时才自动添加滚动条，没有溢出不添加。

```css
.boxfu:hover  .boxzi{  /*鼠标悬浮到父盒子时，显示子盒子*/
    display:block;
}
```



****

### 网页布局

三大核心：盒子模型、浮动、定位

本质：通过css来将盒子放到对应的位置

**1、 清除网页内外边距**(css初始一部分)

如下图

<img src="https://gitee.com/panqiyi/pqimg/raw/master/20201130225723.png" alt="image-20201130225723762" style="zoom: 80%;" />

![image-20201130225826928](https://gitee.com/panqiyi/pqimg/raw/master/20201130225826.png)

网页各种标签都带有默认的内外边距，不同浏览器默认值也不一样，所有在布局前我们首先要清除网页所有元素的内外边距。

```css
*{
  	margin:0;
    padding:0;
}
/*css记得先清除网页元素默认内外边距*/
```



**2、css样式书写顺序**

建议遵循以下顺序：

![image-20201202212926081](https://gitee.com/panqiyi/pqimg/raw/master/20201202212926.png)



**3、页面布局的整体思路：**

<img src="https://gitee.com/panqiyi/pqimg/raw/master/20201202213442.png" alt="image-20201202213442691" style="zoom:50%;" />

<img src="https://gitee.com/panqiyi/pqimg/raw/master/20201202213648.png" alt="image-20201202213648401" style="zoom:50%;" />

**1、**确定版心(页面中很多宽度相同的盒子)，然后将其添加如下样式
.w{
    width: 1260px;
    margin:0 auto;
}

当后面的盒子也是宽度一样且居中时，直接在那些盒子标签添加一个 w 的类名 (当然这个类名是自己定义的)

**2、** 从上至下，1.写结构(html)，2.写对应结构的css。

从上到下一行一行的大盒子用标准流块元素，盒子里面多个小盒子用浮动

**3、**像导航栏这些 ：用ul下的 li 包含 a 

想增加a的选择范围就 显示模式转换 外块元素 再设置宽高



****

### CSS高级技巧

#### 精灵图

精灵图：将多张网页需要的小图片结合到一张图片中。如下：

<img src="https://gitee.com/panqiyi/pqimg/raw/master/20201204154509.png" alt="image-20201204154509144" style="zoom:80%;" />

<font color='red'>精灵图可以有效减少服务器接收和发送次数，提高页面加载速度</font>

即 一次请求服务器一张精灵图，网页多个地方使用使用同一张图的不同位置。

**精灵图的使用**

1、精灵图主要针对背景图片使用，把多个小背景图片整合到一张图中 (该图就叫精灵图)

2、移动背景图片位置，得到自己想要的小图片，用**background-position**

3、移动距离就是这个目标图的x和y坐标，上移和左移都是负值



#### 字体图标

一些结构样式简单的小图标，它其实是文字，兼容性也好。如下：

<img src="https://gitee.com/panqiyi/pqimg/raw/master/20201204160412.png" alt="image-20201204160412514" style="zoom: 50%;" />

**1、阿里矢量图标库**

https://www.iconfont.cn/

**1、**选择一个图标库

<img src="https://gitee.com/panqiyi/pqimg/raw/master/20201204195948.png" alt="image-20201204195948666" style="zoom: 67%;" />

**2、**选择自己需要的图标加入‘购物车’

<img src="https://gitee.com/panqiyi/pqimg/raw/master/20201204200110.png" alt="image-20201204200110454" style="zoom:80%;" />

**3、**点击右上角的 购物车 图标，然后点击下载代码

<img src="https://gitee.com/panqiyi/pqimg/raw/master/20201204200508.png" alt="image-20201204200508122" style="zoom:50%;" />

​					3.1、也可以先添加到项目，然后到项目中下载到本地，这样方便**以后添加新图标**时可以在原有图标添加新图标

​										3.1.1、直接下载该项目<img src="https://gitee.com/panqiyi/pqimg/raw/master/20201204204756.png" alt="image-20201204204756701" style="zoom: 50%;" />

​					                   3.1.2、在该项目的基础上 添加新图标   

<img src="https://gitee.com/panqiyi/pqimg/raw/master/20201205100203.png" alt="image-20201205100203085" style="zoom:67%;" />

​                                选择项目

![image-20201205100245188](https://gitee.com/panqiyi/pqimg/raw/master/20201205100245.png)

​                              此时该项目中在原有图标的基础上增加了新图标，点击下载即可

![image-20201205100502304](https://gitee.com/panqiyi/pqimg/raw/master/20201205100502.png)



**4、**将下载的文件复制粘贴到html文件夹的同级文件夹下，或者放到html文件夹/css文件下 都可以

​					4.1、放到与html,css,等同级文件夹 

![image-20201204203140516](https://gitee.com/panqiyi/pqimg/raw/master/20201204203140.png)

​					4.2、放到css文件夹下

​							                                         	   ![image-20201204203407329](https://gitee.com/panqiyi/pqimg/raw/master/20201204203407.png)

​				   4.3、放到html文件夹下

​																			![image-20201204203538132](https://gitee.com/panqiyi/pqimg/raw/master/20201204203538.png)

​                            这三个都行！！



**5、**打开下载的文件中的 iconfont.css文件，将下面内容复制

![image-20201204201657156](https://gitee.com/panqiyi/pqimg/raw/master/20201204201657.png)

**6、**将复制的代码粘贴到自己的html文件调用的 **对应的css文件中**

**7、**打开该文件夹下的.html文件

![image-20201204201959674](https://gitee.com/panqiyi/pqimg/raw/master/20201204201959.png)

然后选择对应的图标，将其图标下的 字码复制

<img src="https://gitee.com/panqiyi/pqimg/raw/master/20201204202122.png" alt="image-20201204202122145" style="zoom:67%;" />

**8、**将复制的字码粘贴到html中，并将使用字体图标的标签类名改为对应的 css样式中的类名

<img src="https://gitee.com/panqiyi/pqimg/raw/master/20201204202648.png" alt="image-20201204202648594" style="zoom:67%;" />

**9、**此时打开浏览器测试，就可以看到字体图标成功使用

![image-20201204202756864](https://gitee.com/panqiyi/pqimg/raw/master/20201204202756.png)

**2、外国的图标库：**

http://icomoon.io

1、点击右上角

![image-20201204225256858](https://gitee.com/panqiyi/pqimg/raw/master/20201204225256.png)

2、选择自己需要的图标

<img src="https://gitee.com/panqiyi/pqimg/raw/master/20201204225625.png" alt="image-20201204225625467" style="zoom: 50%;" />

3、如觉得此页面样式自己不喜欢，可以下拉点击如下：

<img src="https://gitee.com/panqiyi/pqimg/raw/master/20201204225856.png" alt="image-20201204225856742" style="zoom:67%;" />

4、此时就会有更多的图库提供选择

<img src="https://gitee.com/panqiyi/pqimg/raw/master/20201204230259.png" alt="image-20201204230259483" style="zoom: 50%;" />

5、选择好自己要的图标后，选择右下角获取文字图标

<img src="https://gitee.com/panqiyi/pqimg/raw/master/20201204230928.png" alt="image-20201204230928346" style="zoom:50%;" />

6、点击下载

<img src="https://gitee.com/panqiyi/pqimg/raw/master/20201204231413.png" alt="image-20201204231413474" style="zoom: 50%;" />

7、此时下载好的文件夹内容如下

<img src="https://gitee.com/panqiyi/pqimg/raw/master/20201205001343.png" alt="image-20201205001343518" style="zoom:80%;" />

8、将里面的**fonts**文件夹复制到工程目录下（即与存放html文件夹同级）

![image-20201205001517258](https://gitee.com/panqiyi/pqimg/raw/master/20201205001517.png)

9、用记事本方式打开里面的**style.css**，然后复制下面这一段到要使用的css中

<img src="https://gitee.com/panqiyi/pqimg/raw/master/20201205002619.png" alt="image-20201205002619063" style="zoom:67%;" />

10、**特别注意：**将上面复制的粘贴到css中时，**url 路径需要在前面添加：../**   要不然可能会出现无法显示图标的问题。如下：

![image-20201205003623970](https://gitee.com/panqiyi/pqimg/raw/master/20201205003624.png)

11、打开下载文件中.html后缀的页面，选择自己使用的图标，然后复制该图标右下角的小矩形

![image-20201205004118474](https://gitee.com/panqiyi/pqimg/raw/master/20201205004118.png)

<img src="https://gitee.com/panqiyi/pqimg/raw/master/20201205004213.png" alt="image-20201205004213210" style="zoom:67%;" />

12、粘贴到html标签中，打开浏览器测试即可

![image-20201205004551357](https://gitee.com/panqiyi/pqimg/raw/master/20201205004551.png)

![image-20201205004645010](https://gitee.com/panqiyi/pqimg/raw/master/20201205004645.png)

13、在原有图标追加新图标，

![image-20201205101345971](https://gitee.com/panqiyi/pqimg/raw/master/20201205101346.png)

选择如下

![image-20201205101435571](https://gitee.com/panqiyi/pqimg/raw/master/20201205101435.png)

此时会显示自己原本有的所有图标，下拉在去添加新图标即可

![image-20201205101612134](https://gitee.com/panqiyi/pqimg/raw/master/20201205101612.png)





#### 三角

<img src="https://gitee.com/panqiyi/pqimg/raw/master/20201205102342.png" alt="image-20201205102341998" style="zoom:67%;" />

将盒子宽高设置为0，分别设置四个边框

![image-20201205103153784](https://gitee.com/panqiyi/pqimg/raw/master/20201205103153.png)

![image-20201205103103323](https://gitee.com/panqiyi/pqimg/raw/master/20201205103103.png)

那么我们想要哪一个三角，就把其余的边框设置为透明颜色

```css
.bk1{
    width: 0;
    height: 0;
    border:20px solid transparent;
    border-left-color: red;
}
```

![image-20201205103540028](https://gitee.com/panqiyi/pqimg/raw/master/20201205103540.png)

像上面小米那个，可以先弄个显示二维码的大盒子，然后在大盒子里面设置三角，然后三角盒子添加绝对定位移动到对应位置，父盒子记得添加相对定位，(子绝父相)



#### vertical-align 属性

**图片，表单等行内块元素与文字对齐**

如下：默认情况对齐方式，我们想让图片与文字居中对齐

![image-20201205110431443](https://gitee.com/panqiyi/pqimg/raw/master/20201205110431.png)

![image-20201205105136806](https://gitee.com/panqiyi/pqimg/raw/master/20201205105136.png)

```css
img{ /*在行内块元素设置属性*/
    vertical-align: middle;
}
```

![image-20201205105408477](https://gitee.com/panqiyi/pqimg/raw/master/20201205105408.png)



**解决图片底部默认空白缝隙问题：**

![image-20201205110252230](https://gitee.com/panqiyi/pqimg/raw/master/20201205110252.png)

**原因：**图片默认与字体基线对齐

![image-20201205110517285](https://gitee.com/panqiyi/pqimg/raw/master/20201205110517.png)

**解决方案：**

1、将img图片标签修改  vertical-align 属性的属性值，只要不是基线对齐即可

2、将img图片标签转换为块级元素 display:block;



#### 单行/多行 文字省略

如下，某些情况我们将只显示文字的部分内容，后面的用省略号代替

 如下：单行溢出显示省略号

![image-20201205111117770](https://gitee.com/panqiyi/pqimg/raw/master/20201205111117.png)

如下：多行溢出显示省略号

![image-20201205111302315](https://gitee.com/panqiyi/pqimg/raw/master/20201205111302.png)



**1、单行文本溢出显示省略号--必须满足三个条件**

使用时直接复制到对应元素的样式下即可

```
/*1、先强制文本在一行内显示*/
white-space: nowrap;
/*2、超出部分隐藏*/
overflow: hidden;
/*3、文字用省略号代替超出部分*/
text-overflow: ellipsis;
```

如下：盒子未添加上面三个属性前：

<img src="https://gitee.com/panqiyi/pqimg/raw/master/20201205112424.png" alt="image-20201205112424394" style="zoom:67%;" />

盒子添加三个属性后：

<img src="https://gitee.com/panqiyi/pqimg/raw/master/20201205112456.png" alt="image-20201205112456748" style="zoom:80%;" />

**2、多行文本溢出显示省略号：**

该方法存在兼容性问题，如ie无法显示

使用时直接复制到对应元素的样式下即可

```
overflow:hidden;
text-overflow:ellipsis;
display:-webkit-box;
-webkit-line-clamp:2;/*2为显示省略号行数  如省略号后一行还有文字则调整盒子大小*/
-webkit-box-orient:vertical;
```

![image-20201205113649570](https://gitee.com/panqiyi/pqimg/raw/master/20201205113649.png)

推荐后台做这个效果更简单，兼容性也好



### css初始化

```css
/*把所有标签内外边距清零*/
*{
	margin: 0;
	padding: 0;
}
/*em和i斜体的文字不倾斜*/
em,
i{
	font-style: normal;
}
/*去掉li前面的小圆点*/
li{
	list-style: none;
}

img{
	border: 0;  /*照顾低版本浏览器，如果图片外面包含链接会有边框的问题*/
	vertical-align: middle;  /*取消图片底测有空白缝隙问题*/
}

button{
    cursor: pointer; /*当鼠标经过button按钮时，鼠标样式变成小手*/
}
/*定义链接颜色*/
a{ 
    text-decoration:none;
    color: ;
}
a:hover{  /*定义鼠标悬浮到链接时的颜色*/
    color: ;
}

body{font:12px"宋体","Arial Narrow",HELVETICA;background:#fff;-webkit-text-size-adjust:100%;}

/*清除浮动*/
.clearfix:after{
    content: "";
    display: block;
    height: 0;
    clear: both;
    visibility: hidden;
}
.clearfix{ /*IE6、7专有*/
    *zoom: 1;
}
```

**根据需求对上面初始进行修改与添加**



### 过渡与转换

**1、过渡动画：**从一个状态，渐渐过渡到另一个状态。经常和 :hover 一起搭配使用。

```css
transition: 要过渡的属性  花费时间  运动曲线  何时开始;
/*一般情况下都省略后面两个*/
```

**谁用过渡就给谁加**

如下：给box1盒子添加过渡，让鼠标悬浮时他缓慢变宽高并改变背景颜色

```css
.box1{
    width: 100px;
    height: 200px;
    background-color: #fa7f1c;
    transition:all 1s; /*添加过渡，写all 方便多个属性使用*/
}
.box1:hover{
    width:200px;
    height:300px;
     background-color: skyblue;
}
```

<img src="https://gitee.com/panqiyi/pqimg/raw/master/20201205210137.gif" alt="28" style="zoom:67%;" />

**2D转换 transform：**

**1、移动：translate**

改变元素在页面中的位置

```css
transfrom:translate(x,y); /*x轴，y轴，注意网页坐标，如向上y为负值*/
/*或者x轴与y轴分开写*/
transfrom:translateX(x);
transfrom:translateY(y);
```

**注意：**1、移动位置对其他元素不影响。2、对行内标签没有效果, 像img这样行内块元素可用

如下：让盒子悬浮时缓慢(在上面过渡基础上)上升

```css
.box1{
    width: 100px;
    height: 200px;
    background-color: #fa7f1c;
    margin: 300px auto;
    transition:all .5s; /*缓慢的过渡动画效果*/
}
.box1:hover{
   transform:translateY(-10px); /*鼠标悬浮时上升10px*/
}
```

<img src="https://gitee.com/panqiyi/pqimg/raw/master/20201205212947.gif" alt="29" style="zoom:80%;" />

2D转换还有 旋转、缩放。这个占时不去了解。



### 标题小图片

```html
<link rel="shortcut icon" href="favicon.ico" type="image/x-icon">
```

