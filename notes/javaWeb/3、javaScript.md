# JavaScript

## 概念：

一门客户端脚本语言

- 运行在客户端浏览器中的，每一个浏览器都有JavaScript 的解析引擎
- 脚本语言：不需要编译，直接就可以被浏览器解释执行

**功能：**

- 可以来增强用户和html页面的交互过程，可以来控制html元素，让页面有一些动态的效果，增强用户的体验。

**ECMA(欧洲计算机制造商协会)制定了所有客户端脚本语言的标准：ECMAScript**

**JavaScript = ECMAScript + javaScript自己特有的东西 (BOM+DOM)**



## ECMAScript

客户端脚本语言的标准。

### 基本语法

**1、与html结合方式**

**一般推荐写在< body/>结束标签上面**

**内部样式：**在HTML页面内的**< script>标签内写js的代码**。< script>标签可以在html的**任意位置**，但有从**上到下的执行顺序**(写在html代码上面就先执行js才会显示html，写在html代码下面就先执行html再执行js，内部外部样式都这样)。

<img src="https://gitee.com/panqiyi/pqimg/raw/master/20201207153719.png" alt="image-20201207153719488" style="zoom:67%;" />

<img src="https://gitee.com/panqiyi/pqimg/raw/master/20201207153648.png" alt="image-20201207153648549" style="zoom:80%;" />

**外部样式**

**在< script> 标签中，使用src属性引入外部javaScript文件。**

![image-20201207154650993](https://gitee.com/panqiyi/pqimg/raw/master/20201207154651.png)

**注意：script标签可以定义多个**



**2、注释**

跟Java注释一样

单行注释：//注释内容

多行注释：/* 注释内容 */

**3、数据类型**

- **原始数据类型(基本数据类型):**

  1、number：数字。整数/小数/NaN ( not a number  一个不是数字的数字类型 )

  2、String：字符串

  3、boolean：true和false

  4、null：一个对象为空的占位符

  5、undefined：未定义。如果一个变量没有给初始化值，则会默认赋值为undefined

- **引用数据类型：**对象

**4、变量**

- 变量：一小块储存数据的内存空间
- Java语言是强类型语言，而JavaScript是弱类型语言，
- 强类型：开辟变量存储空间时，定义了空间将来存储的数据只能是对应的数据类型
- 弱语言：开辟变量存储空间时，没有定义空间将来的存储数据类型，可以存储任意类型的数据。

```js
语法：
var 变量名=初始化值;
```

**typeof(变量)**   返回该变量的数据类型字符串

但是null会返回object类型

![image-20201207192400453](https://gitee.com/panqiyi/pqimg/raw/master/20201207192400.png)



**5、运算符**

**1、一元运算符：**只有一个运算数的运算符  如：	++、--、+(正号)  -(负号)

​		++、--、在数前：如++1  ，先自增，在运算。反之在数后，如 i++，则先运算，再自增

​		+(-)正负号

​		**注意：**在js中，如果**运算数不是运算符所要求的类型**，那么js会自动将运算数进行类型转换，

​                     其他类型转number:

​							String转number: 按照字面值转换。如果不是数字，则转换为NaN（不是数字的数字）

​										如下面：+（正号要求的是number数据类型）

![image-20201207200826699](https://gitee.com/panqiyi/pqimg/raw/master/20201207200826.png)

​							boolean转number：true转1，false转0

​		

2、算数运算符：

​		+   -   *   /   %…

3、赋值运算符：

​		=   +=   -=   …

4、比较运算符：

​		>   <    >=    <=   ==    ===(全等于)

​		比较方式：

​				1、类型相同：直接比较

​							字符串：按照字典顺序比较，按左到右一位一位的比较，直到得出比较大小为止(如 adb 与 adc 左到右比，发现c比b大 所以 adb>adc)

​				2、类型不同：先进行类型转换，再比较。

​							=== ：全等于。在比较前，先判断类型，如果类型不同，直接返回false

![image-20201207204821440](https://gitee.com/panqiyi/pqimg/raw/master/20201207204821.png)

5、逻辑运算符：&&   ||   ！

! ：非  （会出现与+(正号）那样的问题：当运算数与运算符要求的数据类型不符时，js会自动进行类型转换）

​		     其他类型转换为 boolean

​					1、number：0或NaN为假，其他为真。

​					2、string：除了空字符串("")，其他都为true

​					3、null & undefined：都是false

​					4、对象：所有对象都是true

<img src="https://gitee.com/panqiyi/pqimg/raw/master/20201207221801.png" alt="image-20201207221801844" style="zoom:80%;" />

6、三元运算符：? :

```js
var a=3; var =4;
var c=a>b?1:0; //a>b如为真 c=1  如为假c=0 这里=0
```



**6、流程控制语句**

**1、js特殊语法**

- 如果一行只有一条语句则可以省略 “;” （不建议）

- 变量的定义使用var关键字，也可以不使用

  ​		用：定义的变量是局部变量

  ​		不用：定义的变量是全局变量 (不建议)

**2、流程控制语句**

- if…else

- switch

  **注意：**java中switch表达式的值只能是：byte，short，char，int，枚举(1.5)，String(1.7)。而js中可以是任意类型

- while

- do…while

- for

  注意：for(var i; i<100 ; i++){}  i 的数据类型不能声明数据类型，必须是var



### 基本对象

#### **Function：函数对象(方法)对象**

**1、创建：**

​		 1.1	function  方法名(形式参数列表){ 方法体}

​		 1.2	var  方法名=function(形式参数列表){ 方法体}

​		**注意：**参数列表不写数据类型

**2、属性**

​		length：返回方法形参列表的参数个数

**3、特点**

​			1、方法定义时，形参的类型不用写，返回值类型也不写

​			2、方法是一个对象，如果定义名称相同的方法时，会覆盖

![image-20201209093608701](https://gitee.com/panqiyi/pqimg/raw/master/20201209093608.png)

​			3、在js中，方法的调用只与方法的名称有关，和参数列表无关。

```javaScript
function name1(a,b) {
    alert(a);
    alert(b);
}
name1(4,3); //第一个:4，第二个:3
name1(4); //第一个值:4，第二个赋值:undefined
name1(); // 两个参数都是赋值:undefined
name1(4,3,5); //只弹出4和3，因为形参只有a,b。

//但是传入的所有参数都被内置arguments数组对象接收封装
```

​			4、方法在声明中有一个隐藏的内置数组对象，arguments，封装所有的实际参数。

```js
function fun01() {
    var sum=0;
    for (var i=0;i<arguments.length;i++){
        sum+=arguments[i];
    }
    alert(sum)
}
fun01(4,5,6,7); // 弹出结果 22
```

**4、调用**

​		方法名称(实际参数列表);



#### **Array：数组对象**

**1、创建：**

```js
var arr1=new Array(5); //初始化默认长度为5
var arr2=new Array("ni","号","java!"); //初始直接赋值
var arr3=[1,2,3,4]; // 初始直接赋值
var arr4=new Array(); //初始化空数组
```

**2、方法**

```js
var arr=[1,"ab",2,3];
1、join：把数组所有元素放入一个字符串，通过指定分隔符分隔，默认是逗号","
		document.write(arr.join("--")+"<br>"); // 1--ab--2--3
2、push：向数组末尾添加一个或多个元素，并返回新长度的数组
		arr.push(99,"java"); // 此时打印： 1--ab--2--3--99--java
```

**3、属性**

​		1、length：数组长度

**4、特点**

​		1、js中数组元素类型是可变的。

```js
var arr=[12,"java",true];
```

​		2、js中数组的长度是变化的。



#### Date：日期对象

**1、创建**

```js
var date = new Date();
```

**2、方法**

```js
1、toLocaleString(); //返回当前date对象对应的本地字符串格式时间
2、getTime(); //返回当前日期对象时间到1970年1月1日零点的毫秒值差
```



#### Math：数学对象

**1、创建**

​    **注意：**Math对象不用创建，直接使用。Math.方法名();

**2、方法**

```js
1、random();  //返回[0,1)之间的随机数
2、ceil(x);  //对数进行向上取整
3、floor(x);  //对数进行向下取值
4、round(x);  //把数四舍五入

如：取0~10的随机数
document.write(Math.floor((Math.random()*10))+1+"<br>") 
// Math.random()*10生成0到9的小数，然后向下取整，再+1
```

**3、属性**

​     PI ：圆周率

#### RegExp：正则表达式对象

**正则表达式：定义字符串的组成规则。**

​		**1、单个字符：**[ ]

```js
如：
[a];  [ab]:a或者b ;   [a-zA-Z0-9_]：a~z或者A~Z或者0~9和下划线  
//特殊符号代表含义的单个字符
\d:单个数字字符 [0-9]
\w：表示单词字符：[a-zA-Z_0-9]
中文：[\u4e00-\u9fa5]
```

​		**2、量词符号：**

```js
?:表示出现0或者1次
*:表示出现0次或者多出
+:表示出现1次或者多出
{m,n}:表示  m<=数量<=n
		m如果缺少：{,n}:最多n次
         n如果缺少: {m,}:最少m次
         {x}：长度为x
开始结束符号：分别给正则表达式的两头加
^ ：开始
$ ：结束                 
```

**正则对象**

​	**1、创建**

```js
var reg = new RegExp("正则表达式");
var reg = /正则表达式/;
```

​     **2、方法**

```js
test(参数); //验证指定字符串是否符合正则表达式的规则
```

```js
var reg=/^\w{6,12}$/;
var name="zhangsan";
var flag = reg.test(name); //满足则true，反之false
document.write(flag);
```



#### Global

**全局对象，这个Global中封装的方法不需要对象来调用，可直接调用：方法名();**

**方法：**

**一、编解码**

URL编码：将输入的网址或字符串进行编码

![image-20201210221508313](https://gitee.com/panqiyi/pqimg/raw/master/20201210221508.png)

```js
1、
encodeURI():url编码
decodeURI():url解码
2、
encodeURIComponent():url编码，编码的字符更多。
decodeURIComponent():url解码
```

**如1、**

```js
var word1="上善若水";
//编码
var s1 = encodeURI(word1);
document.write(s1+"<br>"); //%E4%B8%8A%E5%96%84%E8%8B%A5%E6%B0%B4 ; 有12个%。说明12个字节，12/4(4个字符)=3字节，说明是utf-8编码
//解码
var s2 = decodeURI(s1);
document.write(s2); //上善若水
```

**如2、**

```js
var word2="https://www.baidu.com/s?wd=百度一下";
var s2 = encodeURI(word2); //1
document.write(s2+"<br>");
var s3 = encodeURIComponent(word2); //2
document.write(s3);
```

打印如下，encodeURIComponent()方法能编码的字符更多。

![image-20201210225558524](https://gitee.com/panqiyi/pqimg/raw/master/20201210225558.png)



**二、parseInt():将字符串转换为数字**

注意：左到右逐一判断每一个字符是否是数字，直到不是数字为止，将数字部分转为number。

```js
var a1="123ab";
var a2="a123ab";
var num1 = parseInt(a1);
var num2 = parseInt(a2);
document.write(num1); //123
document.write(num2); //NaN
```

**三、isNaN：判断某个参数是否是NaN**

因为NaN与任何类型参与比较结果都是false,包括NaN==NaN

```js
var a=NaN;
document.write((a==NaN)+"<br>"); //false
document.write(isNaN(a)); //true
```



**四、eval()：将JavaScript中字符串作为代码执行**

```js
var a="java";
var s="document.write(a)"; 
var s1="alert(123)"; 
eval(s); // 网页显示：java
eval(s1); //弹出 123
```



**DOM简单学习：**为了先完成开关灯案例

- 功能：控制html文档内容
- 代码：获取页面标签(元素)对象  Element

```js
documetn.getElementById("id值"); //通过元素id获取元素对象
```

- 操作Element对象：

  1、修改属性值：找到对应标签属性然后在js中操作

  2、修改标签内容: innerHTML

```js
<img src="../image/off.gif" id="light">
<h1 id="name">刘德华</h1>

<script>
    //修改属性
    var light = document.getElementById("light");
    alert("我要换图片了")
    light.src="../image/on.gif";
	//修改标签内容
	var name = document.getElementById("name");
	alert("换人");
	name.innerHTML="张国荣";
</script>
```

**事件的简单学习：**

- **功能：**某组件被执行了某先操作后，触发某些代码的执行。

  ​	如：图片被点击，更换另一张图片

- **如何绑定事件：**

  ​	1、在标签中绑定（不推荐）

  ```js
  <img src="../image/off.gif" id="light" onclick="alert('我被点了')">
  ```

  ​    2、在js中绑定

```js
//获取元素对象，指定事件属性，设置一个函数
<script>
    var light = document.getElementById("light");
    light.onclick=function () {
        alert("我被点了")
    }
</script>
```

**开关灯案例：**

如果是关灯图片，点击切换开灯图片。如果是开灯图片，点击切换关灯图片。

![image-20201212084058619](https://gitee.com/panqiyi/pqimg/raw/master/20201212084058.png)

```js
<script>
    var light = document.getElementById("light");
    var flag=false;//定义一开始关灯为false
    light.onclick=function () {
        if (flag){ //true开灯进去
            //切换关灯图片
            light.src="../image/off.gif";
            flag=false;
        }else {
            light.src="../image/on.gif";
            flag=true;
        }
    }
</script>
```

![30](https://gitee.com/panqiyi/pqimg/raw/master/20201212084006.gif)



## BOM

### 概念

Browser Object Model ：**浏览器对象模型**

<font color='orange'>将浏览器的各个组成部分封装成对象</font>

<img src="https://gitee.com/panqiyi/pqimg/raw/master/20201212093517.png" alt="image-20201212093517761" style="zoom:80%;" />

### 组成

<font color='orange'>Window：窗口对象</font>
<font color='orange'>History：历史记录对象</font>
<font color='orange'>Location：地址栏对象</font>
Navigator：浏览器对象  (了解)
Screen：显示器屏幕对象 （了解）

### Window 窗口对象

**1、创建**

​	1、Window对象不需要创建可以直接使用：window.方法名();

​	2、window引用可以省略：方法名();



**2、方法**

​			**1、与弹出框有关的方法：**

​				**alert()**：显示带有一段消息和一个**确认按钮**的警告框

```js
window.alert('你好！');
```

<img src="https://gitee.com/panqiyi/pqimg/raw/master/20201212101913.png" alt="image-20201212101913652" style="zoom: 67%;" />

​				**confirm()**：显示带有一段消息以及**确认按钮**和**取消按钮**的对话框（常用）

```js
window.confirm("你确定要退出吗？"); //返回值为true/false
```

<img src="https://gitee.com/panqiyi/pqimg/raw/master/20201212102101.png" alt="image-20201212102101692" style="zoom:67%;" />

​												                      点击确定：返回true    点击取消：返回false

​				**prompt()**：显示可提示用户输入的对话框 （了解）

```js
window.prompt('请输入信息'); //返回值为输入的内容
```

<img src="https://gitee.com/panqiyi/pqimg/raw/master/20201212102346.png" alt="image-20201212102346931" style="zoom: 67%;" />

**2、打开&关闭页面方法：**

​		1、**open()**：打开新页面，返回值为新窗口对象

```js
<input type="button" value="打开窗口" id="butt">
<script>
    var butt = document.getElementById("butt"); //获取元素对象
    butt.onclick=function () { //指定事件属性，赋予操作方法
        open("https://www.baidu.com/"); //打开的页面地址，返回值为新窗口对象
    }
</script>
```

<img src="https://gitee.com/panqiyi/pqimg/raw/master/20201212214233.gif" alt="31" style="zoom: 67%;" />

​		2、**close()**：**谁调用就关谁**

```js
<input type="button" value="关闭窗口" id="butt">
<script>
    var butt = document.getElementById("butt"); //获取元素对象
    butt.onclick=function () { //指定事件属性，赋予操作方法
        close(); //window.close() 当前页面，就关闭当前窗口
    }
</script>
```

<img src="https://gitee.com/panqiyi/pqimg/raw/master/20201212220312.gif" alt="32" style="zoom:67%;" />

​		**关闭调用close的窗口：**

```js
<input type="button" value="打开窗口" id="openBt">
<input type="button" value="关闭窗口" id="closeBt">
<script>
    var openBt = document.getElementById("openBt");
    var baidu;
    openBt.onclick=function () {
        baidu = open("https://www.baidu.com"); //指定打开新窗口地址，并返回新窗口对象
    }

    var closeBt = document.getElementById("closeBt"); //获取元素对象
    closeBt.onclick=function () { //指定事件属性，赋予操作方法
        baidu.close(); //新窗口调用close,则就关闭的是baidu窗口对象的这个窗口
    }
</script>
```

<img src="https://gitee.com/panqiyi/pqimg/raw/master/20201212222501.gif" alt="33" style="zoom:67%;" />

**3、定时器的方法**

```js
1、setTimeout()   在指定的毫秒数后调用函数或者计算表达式
		参数：(js代码或者方法对象,毫秒值)
		返回值：唯一标识，用于取消定时器
   clearTimeout()  取消由 setTimeout() 方法设置的单次定时器
   		参数：
2、setInterval()  按照指定周期来调用函数或计算表达式
   clearInterval()  取消由 setInterval() 设置的循环定时器，括号里面为 setInterval()的返回值
```

```js
<script>
    //setTimeout(fun,2000) //单次定时器 
    setInterval(fun,3000) //循环定时器
    function fun() {
        alert('hello!')
    }
</script>
```

#### 案例：轮播图：

​			按照一定时间循环展示以下三张图片。

![image-20201213102319620](https://gitee.com/panqiyi/pqimg/raw/master/20201213102319.png)

```js
<img src="../image/banner_1.jpg" width=100% id="img"> //展示图片
<script>
var bann = document.getElementById("img"); //获取图片元素对象
var number=1;
function fun() { //设置换图片路径方法
    number++;
    if (number>3){
        number=1;
    }
    bann.src="../image/banner_"+number+".jpg";
}
setInterval(fun,3000); //循环定时器，调用换图片方法，设置时间
</script>
```

**3、属性**

​		1、获取其他BOM对象

```js
history  //如：window.history返回History对象（window可省略）
location
Navigator
screen
```

​		2、获取DOM对象

```js
document
```



**4、特点**

​			1、Window对象不需要创建可以直接使用：window.方法名();

​			2、window引用可以省略：方法名();



### Location地址栏对象

**1、创建**

通过window属性获取location对象

**2、方法**

```js
1、reload()  //刷新页面
```

```js
<input type="button" id="but" value="刷新">
<script>
    var but = document.getElementById("but"); //获取按钮对象
    but.onclick=function () {//绑定单击事件
        location.reload();//刷新页面
    }
</script>
```

<img src="https://gitee.com/panqiyi/pqimg/raw/master/20201213105603.gif" alt="34" style="zoom:80%;" />

```js
2、href //获取设置的地址
```

```js
<input type="button" id="but" value="百度">
<script>
    var but = document.getElementById("but"); //获取按钮对象
    but.onclick=function () {//绑定单击事件
        location.href="https://www.baidu.com"; //获取设置的访问网址
    }
</script>
```

<img src="https://gitee.com/panqiyi/pqimg/raw/master/20201213110443.gif" alt="35" style="zoom:80%;" />

#### 案例：倒计时自动跳转

```js
<p>
    <span id="time">5</span>秒后，自动跳转到...
</p>
<script>
    var second=5; //设置初始时间
    var time = document.getElementById("time");
    //定义方法，获取span标签，修改标签内 时间--
    function showTime() {
        second--;
        if (second<=0){ //时间<=0跳转页面
            location.href="https://www.baidu.com";
        }
        time.innerHTML=second+""; //将标签中每一秒的时间展示
    }
    //设置定时器，1秒执行一次该方法
    setInterval(showTime,1000);
</script>
```

<img src="https://gitee.com/panqiyi/pqimg/raw/master/20201213112724.gif" alt="36" style="zoom:67%;" />



### History历史记录对象

**1、创建**

通过window对象的属性返回

window.history或者history

**2、方法**

```js
bank()：加载history列表中的上一个URL（加载当前页面的上一个页面）
forward：加载history列表中的下一个URL（加载当前页面的下一个页面）
go(参数)：加载列表中具体的某个页面
	参数：
    	正数：前进几个历史记录
        负数：后退几个历史记录
```

**3、属性**

```js
length ：返回当前窗口历史列表中的URL数量
```

**如：**就是当前页面根据浏览历史记录进行前进后退

```js
<input type="button" value="--->" id="s">
<script>
    var back = document.getElementById("s");//获取元素对象
    back.onclick=function () { //指定事件属性，赋值一个内部方法
        history.forward(); //在当前页面的访问记录中，进入下一个页面记录
    }
</script>
```

<img src="https://gitee.com/panqiyi/pqimg/raw/master/20201213170607.gif" alt="37" style="zoom:80%;" />



## DOM

### 概念

Document Object Model：文档对象模型

将标记语言文档的各个组成部分 封装为对象，可以使用这些对象 对标记语言文档进行CRUD的动态操作

<img src="https://gitee.com/panqiyi/pqimg/raw/master/20201213171831.png" alt="image-20201213171830732" style="zoom:80%;" />

**W3C    DOM 标准被分为3个不同的部分：**

- 核心 DOM -- 针对任何结构化文档的标准模型
  - <font color='orange'>Document：文档对象</font>
  - <font color='orange'>Element：元素对象</font>
  - Attribute：属性对象
  - Text：文本对象
  - Comment：注释对象
  - <font color='orange'>Node：节点对象，其他5个的父对象</font>

- XML  DOM --  针对XML文档的标准模型
- HTML DOM -- 针对HTML文档的标准模型



### 核心DOM模型

**1、Document：文档对象**

​			**1、创建(获取)**：在html dom 模型中可以使用window对象来获取

​				1、window.document

​				2、document

​			**2、方法**：

​				2.1、获取Element对象：

​						1、getElementById() ：根据**id属性值**获取元素对象。id属性值一般唯一

​						2、getElementsByTagName() ：根据**元素名称**获取元素对象们。返回值是一个数组

​						3、getElementsByClassName() ：根据**class属性值**获取元素对象们。返回值是一个数组

​						4、getElementsByName() ：根据**name属性值**获取元素对象们。返回值是一个数组（常用在表单input）

​				2.2、创建其他DOM对象 (了解即可)

```js
createAttribute(name)
createComment()
createElement()  //新建一个标签
createTextNode() //新建一个文本节点
```

​			**3、属性**

​						

**2、Element：元素对象**

​		**1、创建**：通过document来获取和创建

​		**2、方法：**

​				1、setAttribute()：设置属性

​				2、removeAttribute()：删除属性

**3、Node：节点对象，其他对象的父对象**

所有的dom对象都可以被认为是一个节点

​		**2、方法：**删除/添加子节点。

```js
1、appendChild()：向节点的子结点列表的结尾添加新的子结点。
2、removeChiled()：删除（并返回）当前节点的指定子节点
3、replaceChiled()：用新的节点替换一个子结点
parentNode //获取父元素对象
```

```html
<div id="div1">
    父
    <div id="div2">子</div>
</div>
<a href="javascript:void(0);" id="del">删除子结点</a>
<a href="javascript:void(0);" id="add">添加子结点</a>
<!--
    注意：超链接功能：
            1、可以被点击：样式
            2、点击后跳转到href指定的url
    需求，保留1功能，去掉2功能。---将href="javascript:void(0);"
    -->
<script>
    var element_del = document.getElementById("del");
    element_del.onclick = function () {
        var element_div1 = document.getElementById("div1");
        var element_div2 = document.getElementById("div2");
        element_div1.removeChild(element_div2);
    }

    var element_add = document.getElementById("add");
    element_add.onclick=function () {
        var element_div1 = document.getElementById("div1");
        var div2 = document.createElement("div"); //创建一个div
        div2.setAttribute("id","div2"); //设置属性与属性值
        element_div1.appendChild(div2); //给div1添加子元素div2
    }
</script>
```

<img src="https://gitee.com/panqiyi/pqimg/raw/master/20201214124812.gif" alt="38" style="zoom:67%;" />



### HTML DOM

#### innerHTML

标签体的**设置**和**获取**：获取标签中的所有内容，包括标签和文本

如下获取：得到的是div1中的所有内容-->div2和文本

```html
<div id="div1">
    <div class="div2">你好</div>
</div>
<script>
    var div1 = document.getElementById("div1");
    var innerHTML = div1.innerHTML;
    document.write(innerHTML); //div1标签体中所有内容: <div class="div2">你好</div>
</script>
```

设置：此时div1中的div2被替换为了< input type='text'>

```html
<div id="div1">
    <div class="div2">你好</div>  <!--被替换为 <input type='text'>  -->
</div>
<script>
    var div1 = document.getElementById("div1");
     div1.innerHTML= "<input type='text'>"
</script>
```

##### 案例：动态表格

<img src="https://gitee.com/panqiyi/pqimg/raw/master/20201216094022.gif" alt="39" style="zoom:67%;" />



```html
//省略html部分
<script>
    document.getElementById("btn_add").onclick=function () { //获取‘添加’按钮，指定事件书属性，赋予方法
        //获取文本框的值
        var id = document.getElementById("id").value;
        var name = document.getElementById("name").value;
        var gender = document.getElementById("gender").value;
        var table=document.getElementsByTagName("table")[0]; //获取表格对象
        table.innerHTML +="<tr>\n" +
            "            <td>"+id+"</td>\n" +
            "            <td>"+name+"</td>\n" +
            "            <td>"+gender+"</td>\n" +
            "            <td><a href=\"javascript:void(0);\" onclick=\"delTr(this);\">删除</a></td>\n" + //this为当前对象，即当前a标签‘删除’
            "        </tr>";
    }
    function delTr(obj) { //删除的方法
        var table = obj.parentNode.parentNode.parentNode; //获取父标签对象：a-->td-->tr-->table
        var tr = obj.parentNode.parentNode; //a-->td-->tr
        table.removeChild(tr);
    }
</script>
```



#### 样式控制

```html
<script>
    //方式1： 获取元素对象，调用style-->调用样式属性并赋值
    var div1 = document.getElementById("div1");
    div1.onclick=function () {
        div1.style.border="1px solid red";
    }
    //方式2：先在css中创建一个 类选择器并设置样式，然后在js中给指定元素设置类名为对应的类选择器
    var div2 = document.getElementById("div2");
    div2.onclick=function () {
        div2.className="d2";
    }
</script>
```



### 事件

事件监听机制

概念：某些组件被执行了某些操作后，触发某些代码的执行

- 事件：某些操作。如：单击，双击，键盘按下，鼠标移动……
- 事件源：组件。如：按钮、文本输入框等标签……
- 监听器：将要执行的代码。
- 注册监听：将事件、事件源、监听器结合在一起。当事件源上发生了某个事件，则触发执行某个监听器代码

#### 常见的事件

**1、点击事件**

		- onclick：单机事件
		- ondblclick：双击事件

**2、焦点事件**

	- onblur：失去焦点
	- onfocus：元素获得焦点

**3、加载事件**

	- onload：一张页面或一幅图像完成加载

**4、鼠标事件**

	- onmousedown：鼠标按钮被按下。
		* 定义方法时，定义一个形参，接收event(事件)对象
		* event对象的button属性可以获取鼠标被点击的按钮键（鼠标左到右:0,1,2）
	- onmouseup：鼠标按键被松开
	- onmousemove：鼠标被移开
	- onmouseover：鼠标移到某元素之上
	- onmouseout：鼠标从某元素移开
**5、键盘事件**

```
- onkeydown：某个键盘按键被按下
- onkeyup：某个键盘按键被松开
- onkeypress：某个键盘按键被按下并松开
```

**6、选择和改变事件**

```
- onchange：域的内容被改变
- onselect：文本被选中
```

**7、表单事件**

```
- onsubmit：确认按钮被点击
	* 可以阻止表单的提交
		* 方法返回false则表单被阻止。
- onreset：重置按钮被点击
```

#### 案例：表单全选

```html
<th><label for="all">全选</label><input type="checkbox" id="all"></th>

<script>
    document.getElementById("all").onclick=function () { //获取 ‘全选’复选框对象 ，并给予单击事件
        var cbs = document.getElementsByName("cb"); //获取所有复选框数组
        for (var i=0;i<cbs.length;i++){  //遍历
            cbs[i].checked = this.checked;  //this即‘all’这个对象，使每一个复选框与‘全选’的复选框状态一致；
        }
    }
</script>  <!--复选框对象checked属性=true时为选中状态 -->
```



#### 案例：表单验证

**常用正则表达式：**

```js
用户名： /^[\S\w_\u4e00-\u9fa5]{2,7}$/   非空符号\字母 数字 下划线\中文\2~7个 （S为大写）
密码：/^：[a-zA-Z0-9]{6,12}$/  数字或者字母6~12个
号码：/^[1][3578]\d{9}$/
邮箱：/^\w{3,12}@\w{1,5}\.[a-z]{2,3}$/
年龄：/^(?:[1-9][0-9]?|1[01][0-9]|120)$/   1-120岁
价格：/(^[1-9]\d*(\.\d{1,2})?$)|(^0(\.\d{1,2})?$)/
    ^[1-9]\d*(.\d{1,2})?$ ： 1-9开头，后跟是0-9，可以跟小数点，但小数点后要带上1-2位小数，类似2,2.0,2.1,2.22等
    ^0(.\d{1,2})?$ ： 0开头，后可以跟小数点，小数点后要待上1-2位小数，类似0,0.22,0.1等
```

**案例：**

如下两个表单项

![image-20201220134211694](https://gitee.com/panqiyi/pqimg/raw/master/20201220134211.png)

实现如下效果：

用户名为长度2~7位

密码6-12位

并设置输入正确与错误的反馈信息

```html
<script>

        window.onload=function () { //先加载网页（这里script标签放在了头标签内）

            /* 1、给表单绑定onsubmit事件，监听器中判断每个方法校验结果
                          都是true,则监听器方法返回true,否则返回false
                     2、定义一些方法分别校验各个表单项
                     3、给各个表单项绑定onblur事件
                  * */
            document.getElementById("form").onsubmit=function () {
                return checkUsername() && checkPassword();
            }

            document.getElementById("username").onblur=checkUsername; //方法对象，没有()
            document.getElementById("password").onblur=checkPassword;

            //校验用户名
            function checkUsername() {
                //1、获取表单项中的值
                var username = document.getElementById("username").value;
                //2、定义正则表达式
                var reg_username=/^[\S\w_\u4e00-\u9fa5]{2,7}$/;
                //3、判断值是否符合正则的规则
                var flag = reg_username.test(username);
                //4、提示信息的标签对象，并设置提示内容
                var s_username = document.getElementById("s_username");

                if (flag){ //符合正则
                    s_username.innerHTML="<img width='30' height='20' src='../image/gou.png'>";
                }else {
                    s_username.innerHTML="用户名格式有误";
                }
                return flag;

            }

            //校验密码
            function checkPassword() {
                //1、获取表单项中的值
                var password = document.getElementById("password").value;
                //2、定义正则表达式
                var reg_password = /^[a-zA-Z0-9]{6,12}$/;
                //3、判断值是否符合正则的规则
                var flag = reg_password.test(password);
                //4、提示信息的标签对象，并设置提示内容
                var s_password = document.getElementById("s_password");

                if (flag) { //符合正则
                   s_password.innerHTML = "<img width='30' height='20' src='../image/gou.png'>";
                } else {
                    s_password.innerHTML = "密码格式有误";
                }
                return flag;
            }
        }

    </script>

```



![40](https://gitee.com/panqiyi/pqimg/raw/master/20201220145926.gif)

