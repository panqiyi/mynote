# JQuery

## 概念

一个JavaScript框架。简化js开发；

JavaScript框架：本质上就是一些js文件，封装了js原生代码而已。

## 快速入门

1、下载jQuery：

```
目前jQuery有三个大版本：
	1.x：兼容ie678,使用最为广泛的，官方只做BUG维护，
		 功能不再新增。因此一般项目来说，使用1.x版本就可以了，
		 最终版本：1.12.4 (2016年5月20日)
	2.x：不兼容ie678，很少有人使用，官方只做BUG维护，
		 功能不再新增。如果不考虑兼容低版本的浏览器可以使用2.x，
		 最终版本：2.2.4 (2016年5月20日)
	3.x：不兼容ie678，只支持最新的浏览器。除非特殊要求，
		 一般不会使用3.x版本的，很多老的jQuery插件不支持这个版本。
		 目前该版本是官方主要更新维护的版本。
		
- jquery-xxx.js 与 jquery-xxx.min.js的区别：
	1、jquery-xxx.js: 开发版本。给程序员看的，有良好的缩进和注释。体积大一些（查看）
	2、jquery-xxx.min.js: 生产版本。程序中使用，没有缩进。体积小一些。程序加载更快（导入）
```

2、导入jQuery的js文件 ：导入min.js文件

![image-20210506124741719](https://gitee.com/panqiyi/pqimg/raw/master/20210506124741.png)

3、使用

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
    <script src="js/jquery-3.3.1.min.js"></script> <!--引入jquery文件-->
</head>
<body>
<div id="div1">你好</div>

<script >
    var div1 = $("#div1");
    alert(div1.html());  //弹窗 ： 你好
</script>
</body>
</html>
```



## jquery对象与js对象区别于转换

1、jQuery对象在操作时，更加方便

2、jQuery对象和JS对象方法不通用

3、两对象相互转换即可用对方方法

 			jq ---> js :  `jq对象[索引]`  或者 `jq对象.get(索引)`

​			 js ---> jq :   `$(js对象)`

```html
<div id="div1">你好</div>

<script>
    //js
    var div1s = document.getElementById("div1");
    //div1s.innerHTML = "ccc";
    //js转jq : $(js对象)
    $(div1s).html("gggg");

    //jq
    var $div1 = $("#div1");
    // $div1.html("ddd");
    //jq转js : jq对象[索引] 或 jq对象.get(索引)
    $div1[0].innerHTML="nnnn";
</script>
```



## 函数入口&事件&样式控制 基础

```html
<script>
    //函数入口（先加载完html文档再进入js）
    $(function () {
        //为按钮添加事件
        $("#b1").click(function () {
            alert("牛皮牛皮")
        })
    })

    $(function () {
        //样式控制
        //方式1
        $("#div1").css("background-color","red");
        //方式2
        $("#div1").css("backgroundColor","red");
    })
</script>
        
<!--
	window.onload  和  $(function) 区别 :
		- window.onload 只能定义一次，如果定义多次，后边的会将前边的覆盖掉。
		- $(function) 可以定义多次的。
-->
```



## 选择器

### 1.基本选择器

1、标签选择器（元素选择器）

```
语法：$("html标签名")   获取所有匹配标签名称的元素
```

2、id选择器

```
语法：$("#id的属性值")   获得于指定id属性值匹配的元素
```

3、类选择器

```
语法：$(".class的属性值")   获得与指定的class属性值匹配的元素
```

4、并集选择器

```
语法：$("选择器1,选择器2……")  获取多个选择器选中的所有元素
```

### 2. 层级选择器

1. 后代选择器

```
语法： $("A B") 选择A元素内部的所有B元素		
```

2. 子选择器

```
语法： $("A > B") 选择A元素内部的所有B子元素
```

### 3. 属性选择器

1.属性名称选择器 

    语法： $("A[属性名]") 包含指定属性的选择器(A:标签名)

2.属性选择器

 ```
语法： $("A[属性名='值']") 包含指定属性等于指定值的选择器

	 - $("A[属性名^="值"]")  选出指定属性名以指定值 开头 的选择器
	 - $("A[属性名$="值"]")  选出指定属性名以指定值 结尾 的选择器
	 - $("A[属性名*="值"]")  选出指定属性名 包含 了指定值的选择器
 ```

3.复合属性选择器

    语法： $("A[属性名='值'][]...") 包含多个属性条件的选择器
### 4.过滤选择器

1.首元素选择器 

```
语法： :first 获得选择的元素中的第一个元素
	div:first  选取所有div元素的第一个
```

2.尾元素选择器

```
语法： :last 获得选择的元素中的最后一个元素
	div:last  选取所有div元素的最后一个
```

3.非元素选择器

```
语法： :not(selector) 不包括指定内容的元素
	div:not(.one) 选中所有div中class属性不为one的
```

4.偶数选择器

```
语法： :even 偶数，从 0 开始计数
	div:even 选中第1，3，5…个div元素
```

5.奇数选择器

```
语法： :odd 奇数，从 0 开始计数
	div:odd 选中第2，4，6…个div元素
```

6.等于索引选择器

```
语法： :eq(index) 指定索引元素(0开始)
```

7.大于索引选择器 

```
语法： :gt(index) 大于指定索引元素(0开始)
	$("div:gt(3)") 选中所有div中索引>3的
```

8.小于索引选择器 

```
语法： :lt(index) 小于指定索引元素(0开始)
```

9.标题选择器

```
语法： :header 获得标题（h1~h6）元素，固定写法
```

### 5.表单过滤选择器

1.可用元素选择器 (能够点击输入的)

![57](https://gitee.com/panqiyi/pqimg/raw/master/20210509145232.gif)

```
语法： :enabled 获得可用元素
	$("input[type='text']:enabled").val("aa")
	选中可用的表单，将value内容替换为aa
```

2.不可用元素选择器 (设置属性disabled="disabled的表单)

![56](https://gitee.com/panqiyi/pqimg/raw/master/20210509145220.gif)

```
语法： :disabled 获得不可用元素
	$("input[type='text']:disabled").val("aa")
	选中不可用的表单，将value内容替换为aa
```

3.选中选择器 

```
语法： :checked 获得单选/复选框选中的元素
	alert($("input[type='checkbox']:checked").length);
	弹出复选框选中个数。
```

4.选中选择器 

（设置multiple="multiple"属性的下拉框可多选）

```
语法： :selected 获得下拉框选中的元素
	alert($("#se>option:selected").length);
	弹出id为se的下拉列表多选框选中的个数。
```



## DOM操作

### 1.内容操作

```
	1. html(): 获取/设置元素的标签体内容   <a><font>内容</font></a>  --> <font>内容</font>
	2. text(): 获取/设置元素的标签体纯文本内容   <a><font>内容</font></a> --> 内容
	3. val()： 获取/设置元素的value属性值
```

```html
<script>
      $(function () {
         // 获取/设置myinput 的value值
         alert($("#myinput").val());
         $("#myinput").val("java");
         
         // 获取/设置mydiv的标签体内容
         alert($("#mydiv").html());
         $("#mydiv").html("<p>还行吧</p>"); //设置标签有效
         
         // 获取/设置mydiv文本内容
         alert($("#mydiv").text())
         $("#mydiv").text("hello world") //将<div id="mydiv">中的所有内容(包括标签)替换为hello world
      })
   </script>
   
</head>
<body>
   <input id="myinput" type="text" name="username" value="张三" /><br />
   <div id="mydiv"><p><a href="#">标题标签</a></p></div>
</body>
```

### 2.属性操作

1.通用属性操作

```
1. attr(): 获取/设置元素的属性
2. removeAttr():删除属性
3. prop():获取/设置元素的属性
4. removeProp():删除属性

* attr和prop区别？
		1. 如果操作的是元素的固有属性，则建议使用prop
		2. 如果操作的是元素自定义的属性，则建议使用attr
```

```html
<script type="text/javascript">

   $(function () {
      //获取北京节点的name属性值
      var name = $("#bj").attr("name");
      //alert(name)
      //设置北京节点的name属性的值为dabeijing
      $("#bj").attr("name","dabeijing");
      //新增北京节点的discription属性 属性值是didu
      $("#bj").attr("discription","didu");
      //删除北京节点的name属性并检验name属性是否存在
      $("#bj").removeAttribute("name");
      //获得hobby的的选中状态
      var prop = $("#hobby").prop("checked"); //选中true,没选false
      alert(prop)

   })
   
</script>
</head>
<body>
    <ul>
       <li id="bj" name="beijing" xxx="yyy">北京</li> <!--li中没有name这个默认属性-->
       <li id="tj" name="tianjin">天津</li>
    </ul>
    <input type="checkbox" id="hobby" />
</body>
```

2.对class属性操作

```
1. addClass():添加class属性值
2. removeClass():删除class属性值
3. toggleClass():切换class属性
   * toggleClass("one"): 
     * 判断如果元素对象上存在class="one"，则将属性值one删除掉。  如果元素对象上不存在class="one"，则添加
```



### 3.CRUD操作

```
1. append():父元素将子元素追加到末尾
		* 对象1.append(对象2): 将对象2添加到对象1元素内部，并且在末尾
2. prepend():父元素将子元素追加到开头
		* 对象1.prepend(对象2):将对象2添加到对象1元素内部，并且在开头
3. appendTo():
		* 对象1.appendTo(对象2):将对象1添加到对象2内部，并且在末尾
4. prependTo()：
		* 对象1.prependTo(对象2):将对象1添加到对象2内部，并且在开头
```

```
5. after():添加元素到元素后边
		* 对象1.after(对象2)： 将对象2添加到对象1后边。对象1和对象2是兄弟关系
6. before():添加元素到元素前边
		* 对象1.before(对象2)： 将对象2添加到对象1前边。对象1和对象2是兄弟关系
7. insertAfter()
		* 对象1.insertAfter(对象2)：将对象2添加到对象1后边。对象1和对象2是兄弟关系
8. insertBefore()
		* 对象1.insertBefore(对象2)： 将对象2添加到对象1前边。对象1和对象2是兄弟关系
```

```
9. remove():移除元素
		* 对象.remove():将对象删除掉
10. empty():清空元素的所有后代元素。
		* 对象.empty():将对象的后代元素全部清空，但是保留当前对象以及其属性节点
```



## 案例

### 1、隔行换色

```html
<script>
      //需求：将数据行的奇数行背景色设置为 pink，偶数行背景色设置为 yellow
      $(function () {
         $("tr:gt(1):odd").css("backgroundColor","pink")
         //tr:gt(1):odd : 所有tr标签选中大于1(0开始)的索引，odd 选中奇数
         //大于1是为了不选中前两行（不是数据行）
         $("tr:gt(1):even").css("backgroundColor","yellow")
      })
   </script>
</head>
<body>
   <table id="tab1" border="1" width="800" align="center" >
      <tr>
         <td colspan="5"><input type="button" value="删除"></td>
      </tr>
      <tr style="background-color: #999999;">
         <th><input type="checkbox"></th>
         <th>分类ID</th>
         <th>分类名称</th>
         <th>分类描述</th>
         <th>操作</th>
      </tr>
      …… 
   </table>
</body>
```

### 2、表单全选

```html
<script>
      function selectAll(obj) {
         //使下边(class="itemSelect")所有复选框选中状态和第一个复选框状态一致
         $(".itemSelect").prop("checked",obj.checked);
      }
   </script>
   
</head>
<body>
   <table id="tab1" border="1" width="800" align="center" >
      <tr>
         <td colspan="5"><input type="button" value="删除"></td>
      </tr>
      <tr>
         <th><input type="checkbox" onclick="selectAll(this)" ></th>
         <th>分类ID</th>
         <th>分类名称</th>
         <th>分类描述</th>
         <th>操作</th>
      </tr>
      <tr>
         <td><input type="checkbox" class="itemSelect"></td>
         <td>1</td>
         <td>手机数码</td>
         <td>手机数码类商品</td>
         <td><a href="">修改</a>|<a href="">删除</a></td>
      </tr>
      ……
      </table>
```

### 3、qq表情选择

```html
<script>
        //需求：点击qq表情，将其追加到发言框中
        $(function () {
            //1、给所有img图片添加onclick事件
            $("ul img").click(function () {
                //点到谁，谁就是this对象(js对象)
                //2、追加到p标签中
                //$(this).clone() : 将this对象克隆(防止点击图片后就将图片移动添加到p中，而在原地的就会消失)
                $(".word").append($(this).clone())
            })
        })
    </script>
   
</head>
<body>
    <div class="emoji">
        <ul>
            <li><img src="img/01.gif" height="22" width="22" alt="" /></li>
            <li><img src="img/02.gif" height="22" width="22" alt="" /></li>
            <li><img src="img/03.gif" height="22" width="22" alt="" /></li>
            <li><img src="img/04.gif" height="22" width="22" alt="" /></li>
            <li><img src="img/05.gif" height="22" width="22" alt="" /></li>
            <li><img src="img/06.gif" height="22" width="22" alt="" /></li>
            <li><img src="img/07.gif" height="22" width="22" alt="" /></li>
            <li><img src="img/08.gif" height="22" width="22" alt="" /></li>
            <li><img src="img/09.gif" height="22" width="22" alt="" /></li>
            <li><img src="img/10.gif" height="22" width="22" alt="" /></li>
            <li><img src="img/11.gif" height="22" width="22" alt="" /></li>
            <li><img src="img/12.gif" height="22" width="22" alt="" /></li>
        </ul>
        <p class="word">
            <strong>请发言：</strong>
            <img src="img/12.gif" height="22" width="22" alt="" />
        </p>
    </div>
</body>
```

![58](https://gitee.com/panqiyi/pqimg/raw/master/20210511160447.gif)

### 4、下拉列表选择条目左右移动

```html
<script>

      //需求：实现下拉列表选择条目左右选择功能
      $(function () {
         $("#toRight").click(function () {
            $("#rightName").append($("#leftName option:selected"))
         })
      })

      $(function () {
         $("#toLeft").click(function () {
            $("#leftName").append($("#rightName option:selected"))
         })
      })
   </script>
   
</head>
<body>
   <div class="border">
      <select id="leftName" multiple="multiple">
         <option>张三</option>
         <option>李四</option>
         <option>王五</option>
         <option>赵六</option>
      </select>
      <div id="btn">
         <input type="button" id="toRight" value="-->"><br>
         <input type="button" id="toLeft" value="<--">

      </div>
      <select id="rightName" multiple="multiple">
         <option>钱七</option>
      </select>
   </div>
</body>
```



## 动画

1. 三种方式显示和隐藏元素

```
		1. 默认显示和隐藏方式
			1. show([speed,[easing],[fn]]) : 显示
				参数(下面的滑动与淡入淡出参数一样)：
					1. speed：动画的速度。三个预定义的值("slow","normal", "fast")或表示动画时长的毫秒数值(如：1000)
					2. easing：用来指定切换效果，默认是"swing"，可用参数"linear"
						* swing：动画执行时效果是 先慢，中间快，最后又慢
						* linear：动画执行时速度是匀速的
					3. fn：在动画完成时执行的函数，每个元素执行一次。

			2. hide([speed,[easing],[fn]]) : 隐藏
			3. toggle([speed],[easing],[fn]) : 显示隐藏切换
		
		2. 滑动显示和隐藏方式
			1. slideDown([speed],[easing],[fn]) : 下滑显示
			2. slideUp([speed,[easing],[fn]]) : 上滑隐藏
			3. slideToggle([speed],[easing],[fn]) : 显示隐藏切换

		3. 淡入淡出显示和隐藏方式
			1. fadeIn([speed],[easing],[fn]) : 淡入显示
			2. fadeOut([speed],[easing],[fn]) : 淡出隐藏
			3. fadeToggle([speed,[easing],[fn]]) : 显示隐藏切换
```

​	1、默认显示和隐藏方式示例：

```html
 <script>
        function showFn() { //显示
            $("#showDiv").show("slow");
            // 速度，效果，方法；效果不写默认swing
        }
        function hideFn() { //隐藏
            $("#showDiv").hide("slow","swing")
        }
        function toggleFn() { //显示隐藏切换
            $("#showDiv").toggle("slow")
        }
    </script>
</head>
<body>
<input type="button" value="点击按钮隐藏div" onclick="hideFn()">
<input type="button" value="点击按钮显示div" onclick="showFn()">
<input type="button" value="点击按钮切换div显示和隐藏" onclick="toggleFn()">

<div id="showDiv" style="width:300px;height:300px;background:pink">
    div显示和隐藏
</div>
</body>
```

<img src="https://gitee.com/panqiyi/pqimg/raw/master/20210511180441.gif" alt="59" style="zoom: 67%;" />

​	2、滑动显示和隐藏方式示例：

```html
<script>
function showFn() {
        $("#showDiv").slideDown("fast");
        // 速度，效果，方法；效果不写默认swing
    }
    function hideFn() {
        $("#showDiv").slideUp("fast","swing")
    }
    function toggleFn() {
        $("#showDiv").slideToggle("fast")
    }
</script>
```

<img src="https://gitee.com/panqiyi/pqimg/raw/master/20210511215112.gif" alt="60" style="zoom:67%;" />

3、淡入淡出显示和隐藏方式

```html
<script>
    function showFn() {
        $("#showDiv").fadeIn("fast");
        // 速度，效果，方法；效果不写默认swing
    }
    function hideFn() {
        $("#showDiv").fadeOut("fast","swing")
    }
    function toggleFn() {
        $("#showDiv").fadeToggle("fast")
    }
</script>
```

<img src="https://gitee.com/panqiyi/pqimg/raw/master/20210511215609.gif" alt="61" style="zoom:67%;" />

## 遍历

```
1. js的遍历方式
		* for(初始化值;循环结束条件;步长)
2. jq的遍历方式
		1. jq对象.each(callback)
			1. 语法：
				jquery对象.each(function(index,element){});
					* index:就是元素在集合中的索引
					* element：就是集合中的每一个元素对象

					* this：集合中的每一个元素对象
			2. 回调函数返回值：
				* true:如果当前function返回为false，则结束循环(break)。
				* false:如果当前function返回为true，则结束本次循环，继续下次循环(continue)
		2. $.each(object, [callback])
		3. for..of: jquery 3.0 版本之后提供的方式
			for(元素对象 of 容器对象)
```

1、js的遍历：

```html
 <script type="text/javascript">
        $(function () {
            var $city = $("#city li");
            //1、js获取ul下所有li对象
            for (var i = 0; i < $city.length; i++) {
                if ("上海" == $city[i].innerHTML){
                    break; //js用break结束循环 (继续下次用continue)
                }
                //获取内容
                alert(i+":"+$city[i].innerHTML);
            }

            //2、jq对象.each(callback)
                //2.1 获取li对象 第一种方式
            $city.each(function () {
                //获取内容
                alert(this.innerHTML)
            })
                //2.2  获取li对象 第二种方式 在回调函数中定义参数  index(索引) element(元素对象)
            $city.each(function (index,element) {

                //判断如果是上海，则退出循环
                if ("上海" == $(element).html()){
                    return false; //结束循环 ； （结束本次循环，下次继续循环用true）
                }
                //获取索引和内容
                alert(index+":"+element.innerHTML)
                alert(index+":"+$(element).html()) //jq对象调用jq的html()方法
            })

            //3、$.each(jq对象,callback)
            $.each($city,function () {
                alert($(this).html())
                //其他的跟第2种方法一致
            })

            //4、for ... of   jquery 3.0 版本之后提供的方式
            for (li of $city){
                alert($(li).html())
            }

        })
    </script>
</head>
<body>
<ul id="city">
    <li>北京</li>
    <li>上海</li>
    <li>天津</li>
    <li>重庆</li>
</ul>
</body>
```

## 事件绑定

```
1. jquery标准的绑定方式
		* jq对象.事件方法(回调函数)；
		* 注：如果调用事件方法，不传递回调函数，则会触发浏览器默认行为。
			* 文本框对象.focus(); //让文本输入框获得焦点
			* 表单对象.submit();//让表单提交
2. on绑定事件/off解除绑定
		* jq对象.on("事件名称",回调函数)
		* jq对象.off("事件名称")
			* 如果off方法不传递任何参数，则将组件上的所有事件全部解绑
3. 事件切换：toggle
		* jq对象.toggle(fn1,fn2...)
			* 当单击jq对象对应的组件后，会执行fn1.第二次点击会执行fn2.....
			
		* 注意：1.9版本 .toggle() 方法删除,jQuery Migrate（迁移）插件可以恢复此功能。
			 <script src="../js/jquery-migrate-1.0.0.js" type="text/javascript" charset="utf-8"></script>
```

1、jq标准绑定方式示例：

```html
<script type="text/javascript">
        $(function () {
            //给id=name绑定单击事件
            $("#name").click(function () {
                alert("点击弹出了")
            })

            //给name绑定鼠标移动到元素之上事件。绑定鼠标移出事件
            $("#name").mouseover(function () {
                alert("鼠标来了")
            })
            $("#name").mouseout(function () {
                alert("鼠标走了")
            })
            //简化操作，链式编程
            $("#name").mouseover(function () {
                alert("鼠标来了……")
            }).mouseout(function () {
                alert("鼠标走了……")
            })
            
            $("#name").focus() //获取焦点
            $("#name").submit(function () {  //提交表单
                //传入回调函数可设置表单校验
            })
        })
    </script>
</head>
<body>
<input id="name" type="text" value="绑定点击事件">
```

2、on绑定事件/off解除绑定

```html
<script type="text/javascript">
        $(function () {
            //1、使用on给按钮添加单击绑定事件 click
            $("#btn").on("click",function () {
                alert("单击事件")
            })
            //2、使用off解除btn2按钮的单击事件
            $("#btn2").click(function () {
                $("#btn").off("click") //解除单击事件
                $("#btn").off() //q对象组件上的事件全部解绑
            })
        })

    </script>
</head>
<body>
<input id="btn" type="button" value="使用on绑定点击事件">
<input id="btn2" type="button" value="使用off解绑点击事件">
```

3、事件切换：toggle

```html
<script type="text/javascript">
        $(function () {
            //传入两个方法，一个变green，一个变pink ; 当有多个方法时会依次执行，到头后又从头开始执行
          $("#btn").toggle(function () {
              $("#myDiv").css("backgroundColor","green")
          },function () {
              $("#myDiv").css("backgroundColor","pink")
          })
        })
    </script>
</head>
<body>

    <input id="btn" type="button" value="事件切换">
    <div id="myDiv" style="width:300px;height:300px;background:pink">
        点击按钮变成绿色，再次点击红色
    </div>
</body>
```

## 案例

### 1、广告的定时显示与隐藏

```html
<!--引入jquery-->
    <script type="text/javascript" src="../../js/jquery-3.3.1.min.js"></script>
    <script>
        /*
        * 分析：
        * 1、使用定时器  setTimeout  (执行一次定时器)
        * 2、jq显示和隐藏动画效果其实就是控制display属性
        * 3、使用显示隐藏动画来完成广告的显示*/
        
        $(function () {
            setTimeout(adShow,3000)
            setTimeout(adHide,8000)
        })

        function adShow() {
            //获取广告div，调用显示方法
            $("#ad").fadeIn("fast")
        }
        function adHide() {
            //获取广告div，调用隐藏方法
            $("#ad").fadeOut("fast")
        }
    </script>
</head>
<body>
<!-- 整体的DIV -->
<div>
    <!-- 广告DIV -->
    <div id="ad" style="display: none;">
        <img style="width:100%" src="../img/adv.jpg" />
    </div>

    <!-- 下方正文部分 -->
    <div id="content">
        正文部分
    </div>
</div>
</body>
```

### 2、抽奖

![64](https://gitee.com/panqiyi/pqimg/raw/master/20210512124412.gif)

```html
<script>
        $(function () {
            disable(true) //调用按钮禁用方法，结束按钮禁用
            //定义存储图片路径的数组
            var srcArr=["../img/man00.png",
                        "../img/man01.png",
                        "../img/man02.png",
                        "../img/man03.png",
                        "../img/man04.png",
                        "../img/man05.png",
                        "../img/man06.png",]
            var interval;//循环定时全局变量
            var index; //随机路径全局变量
            //1、定义开始按钮单击事件
            $("#startID").click(function () {
                //调用按钮禁用方法，开始按钮禁用
                disable(false)
                //定义循环定时,30毫秒切换一次
                interval = setInterval(function () {
                     //生成 0-(数组长度-1) 的随机数用于做数组的索引
                    index = Math.floor(Math.random()*(srcArr.length));
                    //设置小图片的路径
                    $("#img1ID").prop("src",srcArr[index])
                },30);
            })

            //2、定义结束按钮单击事件
            $("#stopID").click(function () {
                //调用按钮禁用方法，结束按钮禁用
                disable(true)
                //使设置的循环定时结束
                clearInterval(interval)
                //设置随机图片路径到大图片中
                    //先隐藏，在动画显示,看起来效果更好
                $("#img2ID").prop("src",srcArr[index]).hide()
                $("#img2ID").show("slow")

            })

            //定义一个按钮禁用方法（点击开始/结束按钮后禁用该按钮）
            function disable(bool) {
                if (bool){
                    $("#startID").prop("disabled",false)
                    $("#stopID").prop("disabled",true)
                }else {
                    $("#startID").prop("disabled",true)
                    $("#stopID").prop("disabled",false)
                }
            }
        })
    </script>
</head>
<body>

<!-- 小像框 -->
<div style="border-style:dotted;width:160px;height:100px">
    <img id="img1ID" src="../img/man00.png" style="width:160px;height:100px"/>
</div>

<!-- 大像框 -->
<div
        style="border-style:double;width:800px;height:500px;position:absolute;left:500px;top:10px">
    <img id="img2ID" src="../img/man00.png" width="800px" height="500px"/>
</div>

<!-- 开始按钮 -->
<input
        id="startID"
        type="button"
        value="点击开始"
        style="width:150px;height:150px;font-size:22px"
        onclick="imgStart()">

<!-- 停止按钮 -->
<input
        id="stopID"
        type="button"
        value="点击停止"
        style="width:150px;height:150px;font-size:22px"
        onclick="imgStop()">
</body>
```

## 插件

作用：增强JQuery的功能

```
- 实现方式：
	1. $.fn.extend(object) 
			* 增强通过Jquery获取的对象的功能  $("#id")
	2. $.extend(object)
			* 增强JQeury对象自身的功能  $/jQuery
```

```html
//jq获取的元素对象
<script>
//1、定义jq获取的对象插件(所有jq对象都可以调用的方法,方法扩展)
    $.fn.extend({
        check:function () {
            alert("12345！")
        }
    })
    $(function () {
        //获取按钮
        $("#btn-check").click()
    })
</script>
```

```html
//jq自身对象  $或jQuery
<script type="text/javascript">
    //对全局方法扩展2个方法，扩展min方法：求2个值的最小值；扩展max方法：求2个值最大值
    $.extend({
        max:function (a,b) {
            return a>=b?a:b;
        },
        min:function (a,b) {
            return a<=b?a:b;
        }
    })
    $(function () {
        var max = $.max(5,7);
        alert(max)

        var min = $.min(3,5);
        alert(min)
    })
</script>
```

