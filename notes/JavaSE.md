# JavaSE

<img src="https://gitee.com/panqiyi/pqimg/raw/master/20210628190020.jpg" alt="qq_pic_merged_1624877976883" style="zoom: 33%;" />

**Java的运行：**
1、编译Java代码生成字节码(.class)文件；不同平台编译的字节码文件是一样的；

2、字节码不能直接运行，必须通过对应的jvm翻译为机器码才能运行

我们编写的Java代码，编译后会生成 **.class** 文件（字节码文件），(某系统)Java虚拟机负责将字节码文件翻译（转译）成对应系统下的**机器码**然后运行。也就是说，**只要在不同平台上安装对应的JVM**，就可以运行字节码文件，运行Java程序。

（**注意：**这里的jvm翻译为解释与编译，jvm再去了解）

在这个过程中，Java程序没有任何改变，仅仅是通过JVM，就能在不同平台上运行，真正实现了“一次编译，到处运行”。

JVM是实现Java程序跨平台的关键。

注意：跨平台的是Java程序，而不是jvm,不同系统需要安装对应版本的JVM;

![](C:\Users\panqiyi\Desktop\notes\image\55.png)

### jvm/jre/jdk区别

1、JVM 

Java虚拟机  不同jvm与不同系统接触  这就是Java跨平台的关键

2、JRE

java运行环境  包含了jvm  库函数  运行java的文件

3、JDK

包含jre  增加编译器和调试器等开发文件

### 环境变量配置

1、在系统变量中新建：JAVA_HOML    其内容为jdk路径

2、在Path中新加一行内容为：%JAVA_HOME%\bin;

### 注释

单行注释 ：//         多行注释：/**/         文档注释：/ * * 内容 */

### 标识符

由字母  数字  _   $  构成   开头不能是数字   不能用关键字和保留字

1.包名  小写 当多个单词组合 都是小写  如xxxyyyzzz

2.类，接口名  每一个单词首字母都要大写 如XxxYyyZzz

3.变量名，方法名  只有只有开头第一个单词首字母小写   如xxxYyyZzz(驼峰写法)

4.常量名  全大写 每个单词间以下划线连接 如XXX_YYY_ZZZ

### 变量的类型

1、局部变量

方法或语块内部        从属于方法或语句块

2、成员变量(实例变量)

类内部，方法外部      从属于对象  

3、静态变量(类变量)

类内部 ，static修饰     从属于类  	 

### 变量与final 

```java
String name="pan";//"pan"是常量  name是变量
final String name="pan";//此时name为常量 
```



### 数据类型

基本数据类型：整型： byte(1字节)--short(2字节)--int(4字节)--long(8字节)

​						 浮点型：float(4字节)   double(8字节)

​						 字符型：char(2字节)

​						 布尔型：boolean(1bit)

引用数据类型(4字节)：类(class)     接口(interface)   数组    字符串



十进制：123，-234；

八进制：以0开头，如012；

十六进制：以0x开头，0xac;

二进制：0b开头，0b1011



float(单精度  精确小数点后7位)  型定义数据时 数据后面必须加f或者F

否则默认为double(双精度   精确15位 );

同样 定义long型数据时 数据后面加 l或者L

否则默认 int 型

：浮点数存在误差，数字计算不能精确表示，如排除需要用BigDecimal类

### char与转义字符

char a='A';     char字符型   ' '  单引号里面只能是一个字符

char a=65;   输出a=A    A=65  a=65+32=97

转义字符   \n:换行     \t :制表符   \ \ : 一个\       \ ' :一个 '

### 运算

整数：

如果运算中有long型   那结果为 long 型

如果无long型   结果默认为 int 型

浮点：

如果有double  运算结果为double

只有两个 float 时运算结果才为float

取模：java  %两边可以是浮点数  一般两边都为整数   c两边只能是整数

自增自减:

i++  i--  :先赋值，后自增

++i  --i  :先自增，后赋值

### 逻辑运算符

逻辑与   &      两个操作数为true  结果才为true

逻辑或    |	   一个为true   结果也为true

逻辑非    ！     取反  !false  为true

逻辑异或   ^    相同为false   不同为true

短路与    &&    只要一个为false  直接false

短路或     ||      只要一个为true   直接true      

### 位运算

&  |   ^   ~  <<    >>

<img src="C:\Users\panqiyi\Desktop\notes\image\Snipaste_2020-03-06_13-04-34.png" style="zoom:60%;" />

### 字符串连接符

+

```java
public static void main(String[] args){
    int a=3;
    String b="6";
    char c='a';
    System.out.println(a+b);//36 与字符型连接
    System.out.println(b+c);//6a
    System.out.println(a+c);//100
}
```

### 条件运算符(三元)

表达式1？表达式2 : 表达式3;

如果表达式1为真  则执行表达式2  否则执行表达式3

### 优先级

不要刻意的使用运算符的优先级别，

对于不清楚优先级的地方使用小括号去进行替代

注意：非>与>或        

```java
a||b&&c /*其实是*/  a||(b&&c)
```

### 自动类型转换

<img src="C:\Users\panqiyi\Desktop\notes\image\Snipaste_2020-03-06_19-59-34.png" style="zoom:60%;" />

```java
double a=12.0;
        long b;
        b=a;// 这样是不对的  因为double不能自动转换为long
```

### 强制类型转换

```java
double a=3.95;
int b=(int)a;//a强制转换为int  值为3  
```



### 选择结构

1、if    if-else if

```java
if(){//1

}else{

}

if(){//2

}else if(){//在前一个判断基础上判断

}else if(){

}else{}

```

2、switch

多值选择一般用switch

```java
switch(表达式){
	case 值1:
	表达式1;break;
	case 值2:
	表达式2;break;
	……
	default://其他值
	System.out.pritln("其他");
	break;
}//值可以是：byte,short,char,int,1.5增加枚举与前面4个的包装类，1.7增加String
```

### 循环结构

while 循环

```java
while(条件){  //条件成立继续循环  否则跳出循环
	
}
```

do while 循环(不常用)

```java
do{

}while(条件)   //先执行 后判断
```

for循环

无限循环:    for(;;){ }

### break与continue

break;   跳出整个循环  执行下一个语句    

continue;   跳出循环剩余部分  开始下一个循环

continue还有跳转功能：

```java
标记name:for(){
	……
	continue 标记name;//跳转到标记的语句执行
}
```

```Java
//for each循环
int[] array={1,2,3,4,5,6};
for(int n:array){
	System.out.print(n);
}
//for each循环可以直接遍历数组的每个元素
//二维数组的遍历
int[][] arr={{12,34,45,5},{1,2,3,4},{55,77,88}};
        for (int[] d:arr) {//二维数组中是int[] 类型
            for (int n:d) {//一维数组中是int 类型
                System.out.print(n+",");
            }
            System.out.println();
        }
```



### 方法

方法就是 用来完成特定功能的代码段  类似c的函数

参数：进入方法的数据(当对象与数组作为参数时，传入的是地址)

返回值：方法执行后最终产生的结果(当对象与数组作为返回值时，返回的是地址)

修饰符：现阶段固定写法 public static

返回值类型：也就是方法产生的最后结果是什么类型；无返回值  则类型为void

return：1、停止当前方法，2、将后面的结果数据(返回值)还给调用处

注意：return 后的返回值 要与 方法名前的 “返回值类型” 保持对应

```java
修饰符  返回值类型  方法名(参数类型 参数名称,……){
    方法体;
    return 返回值; 
}
```

#### 方法的调用

```java
public static void main(String[] args) {
        sum(10,15);//单独调用
        System.out.println(sum(15,20));//打印调用
        int num=sum(5,15);//赋值调用
    }
    public static int sum(int a,int b){
        int c=a+b;
        return c;
    }
```

**对于无返回值(void)的方法只能 单独调用；**

### 方法的重载

完全不同的方法  只是方法名相同

构成重载的条件：(方法名相同，参数列表不同；）

​				详情：1、方法名相同，参数个数不同

​							 2、方法名相同，参数类型不同

​							 3、方法名相同，多类型参数顺序不同

注意：与参数名无关，与返回值类型无关；

```java
 public static boolean isSame(int a,int b) {
        boolean same=a==b?true:false;
        return same;
    }
    public static long isSame(long a,long b) {//参数类型不同构成重载
        long sum=a+b;
        return sum;

    }
```



```java
public class Test{
public static void main(String[] args){
	System.out.println(add(1,3,2));//自动调用方法1
    System.out.println(add(1,3));//自动调用方法2
    System.out.println(add(1.0,3));//自动调用方法3
    System.out.println(add(1,3.0));//自动调用方法4
}
public static int add(int a,int b,int c){//1
	int sum=a+b+c;
    return sum;
}
public static int add(int a,int b){//2 与1相比 参数个数不同
	int sum=a+b;
    return sum;
}
public static double add(double a,int b){ //3 与2相比参数类型不同
	double sum=a+b;
    return sum;
}
public static double add(int a,double b){ //4 与3相比参数顺序不同
	double sum=a+b;
    return sum;
}
}
```

static 修饰方法可以直接调用  不用创建对象

### 数组

一种容器，可以存放多个数值

1、引用数据类型

2、储存多个数据类型统一

3、数组长度在 程序运行期间不可改变

数组的初始默认值：

byte: 0 short: 0 int: 0 long: 0 float: 0.0 double: 0.0 boolean: false  String: null

#### 初始化

**注意二维数组的长度为 行数(一维数组的个数)**

数组索引从0开始   如arr[0]  为第一个数

<img src="C:\Users\panqiyi\Desktop\notes\image\Snipaste_2020-03-14_10-53-55.png" style="zoom:60%;" />

动态初始化：指定数组长度

````java
//数据类型[] 名称 = new 数据类型[长度];
int[] arrayA=new int[10];

//二维数组
//数据类型[][] 名称 = new 数据类型[二维数组长度][一维数组长度];
int[][] arr= new int[n][y];
//n代表二维数组长度，y代表每一个一维数组长度

//定义二维数组长度 然后再给每一个长度(一维数组)赋值
double[][] arr= new double[5][];
    arr[0]=new double[]{2.3,4.0,5.1};
	arr[1]=new double[]{1.0,3.0};
````

静态初始化：指定内容

```java
int[] arrayB={12,34,6,23};//常用
//也可以
int[] arryaB= new int[12,34,6,23];
//二维
 int[][] arr={{1,2,3,4},{12,34,6},{5,6,7}};
```

获取数组长度    数组名.length

当数组储存对象是  类名[]  数组名=new  类名[]          储存的是它的地址

### 递归

优点：递归把问题简单化

缺点：内存调用多，速度比循环(迭代)慢

 基本思想是“自己调自己”

递归结构包括两部分：递归头：停止调用自身方法，避免陷入死循环

​									递归体：需要调用自身方法

```Java
static long factorial(int n){//n的阶乘
	if(n==1){//递归头
	return 1;
	}else{//递归体
	return n*factoral(n-1);
	}
}
```

### 类的定义

类中有  属性与行为

属性：成员变量    行为：成员方法

成员方法没有static     

```java
public void array(){
}
```

### 对象的创建及使用

1、导包(不在同一个包下时  只有lang包不用导)    2、创建对象  

3、用谁就拿     对象名 . 变量(或者方法) 

```
/*对象引用与对象实例
* 对象引用是一个储存对象地址的  指向堆中对象的地址
* 对象就是new储存在堆当中的*/
new 类名()  匿名对象(只能调用一次)
```

### 成员变量与局部变量

1、定义位置不同

成员变量定义在类中 方法外         局部变量定义在方法内

2、作用范围不一样

成员变量作用于整个类          局部变量作用于该方法

3、默认值不同

成员变量默认值与数组相同          局部变量无默认值，使用需赋值；

4、内存位置不一样

成员变量位于堆内存             局部变量位于栈内存

(引用类型局部变量声明在栈,即在栈存储的是指向堆中对象实例的地址；)

5、生命周期不一样

成员变量随着对象创建诞生 ，随着对象被垃圾回收消失

局部变量随着方法进栈诞生，随着方法出栈消失

### 栈 堆  方法区

栈：1、表示方法执行的内存模型

​			 (主要用来存储局部变量)

​		2、栈属于线程私有，不能线程间共享

​		3、特点”先进后出 后进先出“； 像弹夹

​		4、由系统自动分配，速度比堆快(仅次与寄存器)，是连续的内存空间

堆：1、用来存放new的对象和数组(String字符型，数组也是对象)

​		2、jvm只有一个堆，被所有的线程共享

​		3、堆是一个不连续的内存空间，分配灵活，速度慢

方法区(又称永久代    常称PermGen)：

​		1、jvm只有一个方法区，被所有线程共享

​		 2、(static)静态变量 + (class)类信息(构造方法/接口定义) +常量+ 运行时常量池 在方法区中

​		3、JDK 1.8 的HotSpot中方法区已经被彻底移出了，取而代之使用的是元		空间（Metaspace），元空间使用的是本地内存（Native Mem ory） 

​		【在jdk1.8之前，方法区实际上属于堆的一个区域，只是逻辑上独立，称为		非堆区（Non-Heap），是为了把方法区和Java堆区分开来】

![](C:\Users\panqiyi\Desktop\notes\image\Snipaste_2020-03-15_09-15-36.png)

### 传参

1、基本类型传参：在方法内无法修改方法外的基本类型参数，"值传递"

值传递是指在调用方法时将实际参数复制一份传递到方法中，这样在方法中如果对参数进行修改，将不会影响到实际参数。

类类型传参：

```java
public class exercise1 {
    String name;
    float hp;
    public exercise1(String name,float hp){//te new赋值
        this.name=name;
        this.hp=hp;//*
    }
    public void attkck(exercise1 p,int dam){//引用p取*处值
        p.hp-=dam;
    }
    public static void main(String[] args) {
        exercise1 te=new exercise1("pqy",500);
        exercise1 gl=new exercise1("gl",300);
        gl.attkck(te,100);//
        System.out.println(te.hp);
/*最终值为400.0而不是500.0;*/
    }
}
//如下值就为500   因为方法内的运算不影响方法外的值  "值传递"
public class exercise1 {
    String name;
    float hp;
    public exercise1(String name,float hp){
        this.name=name;
        this.hp=hp;
    }
    public void attkck(int dam){
        hp-=dam;
    }
    public static void main(String[] args) {
        exercise1 te=new exercise1("pqy",500);
        exercise1 gl=new exercise1("gl",300);
        gl.attkck(100);
        System.out.println(te.hp);

    }
```

```Java
public static void main(String[] args) {
    int num=36;
    for (int i = 0; i < 3; i++) {
        add(num);
    }
    System.out.println(num);//还是36
}
public static int add(int num){
    num=num++;
    return num;
}
```

### 封装

1、方法就是一种封装

2、关键字private也是一种封装

封装就是将一些细节信息隐藏起来，对于外界不可见

用private进行修饰，那么本类可以随便访问。但是超出了本类范围就不能直接访问

间接访问private成员变量，就定义一对set/get方法

set方法无返回值 有参数          get方法有返回值，无参数（即set设值    get拿值）

注意：布尔类型的get方法为isXxx   而set方法不变

```java
public class exercise1 {
    private int age;
    String name;
    public void setAge(int age){//设置age值方法
       if(age>0&&<100) {
        this.age=age;
       }else{
           System.out.println("输入有问题");
       }
    }
    public int getAge(){//返回age值方法
        return age;
    }
    }
    class test{
        public static void main(String[] args) {
            exercise1 p=new exercise1();
            p.name="pqy";
            p.setAge(23);//调用set方法输入值
            System.out.println(p.getAge());//调用get方法返回值到此
        }
    }
```



### 构造器(构造方法)

1、通过new关键字调用 ！！！！

2、不要写返回值类型，void也不能 

不能在构造器使用return返回某个值

3、没有定义构造器则编译器会自动添加一个无参方法，有则不会。

4、构造器的方法名必须与类名一致

构造方法的重载与方法的重载相同

### 定义一个标准类

1、所有成员变量使用private修饰

2、为每一个成员变量编写一对set/get方法

3、编写一个无参和全参的构造方法

### 垃圾回收机制

1、当一个对象没有被任何引用的时候，java的垃圾回收机制就会自动回收这些对象。即释放该垃圾对象的内存。

可以调用System.gc(),来通知GC（垃圾回收器运行），但是并不会立马运行，相当于只是给jvm一个建议



### Scanner键盘输入

```java
import java.util.Scanner;//先导包
……
Scanner sc=new Scanner(System.in);//引用
……
String name=sc.nextLine();//字符型  nextLine()
int age=sc.nextInt();//数字型   nextInt()
```

### Math.random()

1、无导包

.如果生成11~99的随机数：

直接 int x=（int）(Math.random()* 89 +11);

//首先Math.random() 类会随机生成<b>[0.0,1.0)</b>的<b>double</b>型；而自定义区域要与给定的[0.0,1.0)区域进行运算；

此处为 ：0.0 * 89+11=11.0    1.0*89+11=100.0； 即[11,100)区域 正是 11~99 的取值范围；但还要强制转化为int型；

2、导包

```java
import java.util.ArrayList;
import java.util.Random;

public class ArrayListMe {
    public static void main(String[] args) {
        Random ranNUm=new Random();//创建Random对象
        ArrayList<Integer> ad=new ArrayList<>();
        for (int i = 0; i < 6; i++) {
            int num=ranNUm.nextInt(5)+1;//生成1~5的一个随机数（包含1、5）
            //int num=ranNUm.nextInt(5) //0 ~ 5
            ad.add(num);
        }
        for (int i = 0; i < ad.size(); i++) {
            System.out.println(ad.get(i));
        }
    }
    }
```



### ArrayList集合

数组长度不可以发生改变

但是ArrayList集合的长度是可以随意变化的

```Java
//ArrayList<E>   <E>内代表泛型，就是装在集合中所有的元素统一是什么类的
//注意：泛型只能是引用类型，不是基本数据类型；
//创建
ArrayList<String> p=new ArrayList<>();
//如果直接打印p 得到的是[]  而不是地址
//添加数据
p.add("李小龙");
p.add("功夫");
p.add("李连杰");//此时p为  [李小龙,功夫,李连杰]
//删除数据
String san=p.remove(2);//索引从0开始  此删除第三个  打印p为[李小龙,功夫]
//提取数据
String look=p.get(1);//索引1  打印为  look为: 功夫 
//遍历ArrayList集合
for (int i = 0; i < p.size(); i++) {//p.size()长度
            System.out.println(p.get(i));//注意：p.get(i)
        }
```

#### 储存基本数据

基本数据类型的包装类为他们的开头字母变成大写   除了int  与  char

如：byte-->Byte     short-->Short  ……    而int-->Integer    char-->Character

```java
ArrayList<Integer>  p=new ArrayList<>();
p.add(23);//此时就可以添加int类型数据
int num=p.get(0);//num=23
int numB=remove(0);//删除23  打印: []
```

### String类

三种构造方法：

```java
//1、无参构造
String str1=new String();//无内容
System.out.println("结果："+str1);//结果：
//2、字符数组创建字符串
char[] array={'A','B','C'};
String str2=new String(array);//打印结果：ABC
//3、字节数组创建字符串
byte[] array1={97,98,99};
String str3=new String(array1);//打印结果：abc

//直接创建
String str="Hello";//此也为String对象
```

#### 字符串常量池

jdk1.7后 在堆中，直接写上双引号的字符串，就在字符串常量词中，而new得是在堆中

#### 字符串常用方法

**比较字符串内容**

数组与对象用''==''比较时是比较地址

1、str1.equals(str2)    equals成员方法用来比较字符串内容是否相等  区分大小写

"hello".equals(str2)     //有常量是推荐这样，防止前面=null时报错  注意：null不能调用方法

2、"hello".equalsIgnoreCase(str2)       与equals一样用于比较，但是这个不区分大小写

```java
String str1 = "hello";
String str2="Hello";
System.out.println("hello".equalsIgnoreCase(str2));
System.out.println(str1.equals(str2));
```

**长度、拼接、截取、索引与字符相互提取**

字符串索引也是从0开始

```java
/*1、字符串长度  .length()
* 2、拼接字符串  .concat()
* 3、用索引提取字符串   .charAt()
* 4、用字符串提取索引   .indexOf()
* 5、截取字符串    .substring()和.substring(,)*/
public class StringBj {
    public static void main(String[] args) {
        String str="qqrmcevnwjwk";
        String str1="李小龙";
        System.out.println(str.length());//1长度
        String str2=str.concat(str1);//2拼接
        System.out.println(str2);
        System.out.println(str.charAt(3));//3索引提取字符串
        System.out.println(str.indexOf("cev"));//4字符串提取索引(首个字符)
        System.out.println(str.substring(5));//5  从索引5开始截取至最右边
        System.out.println(str.substring(5,9));// [5,9) 从5开始截取至第8个字符
    }
}
```

**转换、替换**

```java
byte[] bytes = "abc".getBytes();//转换为字节数组
System.out.println(bytes[1]);//98
char[] chars = "ABC".toCharArray();//转换为字符数组
String s="qwe";
char[] S=s.toCharArray();//字符串转化为字符数组
System.out.println(chars[2]);
String nm="王者荣耀，你大爷的";
String rep = nm.replace("你大爷的", "****");//将后面内容替换前面内容
System.out.println(rep);
```

**分割**

根据字符串中某字符  分割为字符串数组

```java
String fg="aaa,bb,cc,ee";
    String[] array=fg.split(",");//选择分割的字符
    for (int i = 0; i < array.length; i++) {
        System.out.print(array[i]+"\t");
    }
}//特例：当符号是'.'(英文句号)时  分割split里面应该写'\\.' 否则分割失败
```

其他方法：

| `boolean` | `startsWith(String prefix)`               | 测试此字符串是否以指定的前缀开头。                           |
| --------- | ----------------------------------------- | ------------------------------------------------------------ |
| `boolean` | `startsWith(String prefix,  int toffset)` | 测试在指定索引处开始的此字符串的子字符串是否以指定的前缀开头。 |

 | `String`     |      `toUpperCase()` |     将此 `String`所有字符转换为大写，使用默认语言环境的规则。 

boolean   contains("")   判断包含有该字符串返回true ,否则返回false


### static

```
1、修饰成员变量
2、修饰成员方法
3、静态代码块
4、修饰类【只能修饰内部类也就是静态内部类】
5、静态导包
```

1、成员变量使用static关键字，那么此变量不在属于对象自己，而是属于所在的类，多个对象共享一份数据

2、使用static修饰成员方法，叫静态方法，静态方法属于类，不属于对象，如果没有static修饰的方法需要创建对象才可以使用

3、静态方法不能调用非静态成员

4、在本类中的静态方法调用时可以直接   静态方法名(); 调用；也可以  类名.静态方法名；

但是在另一个类时调用静态方法    类名.静态方法名();   

static修饰的静态变量调用也是   类名.变量名

静态方法中不能使用this关键字

5、根据类名称访问静态成员变量时，与对象没有关系，只和类有关（类信息存储于方法区）

**静态代码块**

```java
public class Exer{
	static{
	   //静态代码块内容
	}
}
```

静态代码块只在用到本类时执行唯一 一次；

静态内容优先于非静态，所以静态代码块优先执行于构造方法

### Arrays数组工具类

1、Arrays.tostring();  将数组按照默认格式变成字符串输出；

补充：数组变为字符串：String.valueof(数组);

二维数组用deeptostring();

2、Arrays.sort();  将数组按照从小到大升序排列；

```java
int[] array={1,34,23,546,37,4};
String[] arrays={"aa","dd","cc"};
Arrays.sort(array);
Arrays.sort(arrays);
System.out.println(Arrays.toString(array));
System.out.println(Arrays.toString(arrays));
/*注意：1、Arrays.sort();对于字符串数组，sort按照字母升序
2、如果是自定义类型，那么需要Comparable或者Comparator接口支持*/
```

### 数学工具类

```java
/*1、Math.abs()  绝对值
* 2、Math.ceil()   小数向上取整(数轴正方向)
* 3、Math.floor()  小数向下取整(数轴负方向)
* 4、Math.round()  四舍五入*/
System.out.println(Math.abs(-45.5));//45.5
System.out.println(Math.ceil(43));//43.0
System.out.println(Math.ceil(3.6));//4.0
System.out.println(Math.ceil(-3.6));//3.0
System.out.println(Math.floor(39));//39.0
System.out.println(Math.floor(3.5));//3.0
System.out.println(Math.floor(-3.5));//4.0
System.out.println(Math.round(3.4));//3
System.out.println(Math.round(3.5));//4
```

```java
//取大小值
Math.max(100, 99); // 100
Math.min(1.2, 2.3); // 1.2
```

**计算x的y次方：**

```java
Math.pow(2, 10); // 2的10次方=1024
```

**计算√x：**

```java
Math.sqrt(2); // 1.414...
```

计算e的x次方：j

```Java
Math.exp(2); // 7.389...
```

计算以e为底的对数：

```Java
Math.log(4); // 1.386...
```

计算以10为底的对数：

```Java
Math.log10(100); // 2
```

三角函数：

```Java
Math.sin(3.14); // 0.00159...
Math.cos(3.14); // -0.9999...
Math.tan(3.14); // -0.0015...
Math.asin(1.0); // 1.57079...
Math.acos(1.0); // 0.0
```

Math还提供了几个数学常量：

```Java
double pi = Math.PI; // 3.14159...
double e = Math.E; // 2.7182818...
```

### 继承

extends关键词     共性抽取

```java
public class exercise1 {
    int id;
    String name;
    public static void main(String[] args) {
        study p=new study();
        p.id=666;
        p.name="潘啟毅";
        System.out.println(p.id+p.name);
    }
}
class study extends exercise1{//study类继承父类exercise1类的属性

}
```

1、java中子类只有一个直接父类，单继承 ;    一个父类可以有多个子类  ; 可以多级继承

2、子类继承父类，可以得到父类的全部属性和方法，但可能不能直接访问(比如父类私有的属性和方法)

3、子类对象访问成员变量时子类没有就往父类找  方法一样  ；

对象(对象引用)是哪个类就优先哪个类，没有就往上找，不会往下找

4、**重名变量访问**

​	访问局部变量     直接写名

​	访问成员变量       this.成员变量名

​	访问父类成员变量      super.成员变量名

```java
public class Extends1 extends Extends {
    int id=456;
    public static void main(String[] args) {
        new Extends1().method();
    }
    public void method(){
        int id=789;
        System.out.println(id);
        System.out.println(this.id);
        System.out.println(super.id);//父类成员变量id=123
    }
}
```

**继承中的构造方法**

只有子类构造方法才能调用父类构造方法；

1、子类构造方法中有一个默认的隐含"super()"调用，必须是先调用父类构造

2、子类可以通过super();关键字调用父类重载构造方法

3、super()必须放在子类构造方法的第一个语句，一个子类构造方法只能有一个super。

注意：子类构造方法必须调用父类构造方法，不写默认赠送super();写了则用指定的super调用；

```Java
public class Fu {
    public Fu() {
        System.out.println("父类无参构造方法");
    }
  //  public Fu(int num){//有参构造
  //  }
}
///////////////////
public class Zi extends Fu {
    public Zi() {
       // super(20);//
        System.out.println("子类无参构造方法");
    }
}
/////////////////
public class Main1 {
    public static void main(String[] args) {
        Zi zi=new Zi();
    }
}
//结果1：父类无参构造方法
//      子类无参构造方法

//结果2： 子类无参构造方法   此时子类构造通过super(20);调用父类有参构造
```

#### 方法重写(覆盖)

 重写发生在继承中，子类对父类方法的重新编辑；

1、子类与父类方法名称相同，参数列表相同

2、子类返回值必须<=父类方法返回值

3、子类方法权限必须>=父类方法权限

备注：权限大小  public>protected>(default)(等于不写)>private

```java
@Override
public void num() {
    super.num();//访问父类方法,在某些功能重复时使用可以避免重新写相同功能;
    System.out.println("2");
}//如这里父类num方法只有打印1，重写父类增加打印1和2，就访问父类方法即可，无需重新写相同代码;
```

#### super

1、在子类成员中方法中，访问父类的成员变量(如上重名时)

2、子类成员方法中访问父类成员方法(如上重写时避免重新写相同功能代码)

3、子类构造方法中，访问父类的构造方法

### this

表当前对象

1、在本类的成员方法中，访问本类成员变量

```Java
public class exercise1 {
    int a,b;//成员
    public exercise1(int a,int b){//局部
        this.a=a;
        this.b=b;
        }
        }
```

2、本类构造方法调用本类另一个构造方法 

```Java
public class exercise1 {
    int a,b;//成员
    public exercise1(int a,int b){//局部
        this.a=a;
        this.b=b;
        }
    public exercise1(int a,int b,int c){
    	this(a,b);//调用上面那个构造方法   且只能放于第一句
    }
        }
```

3、本类成员方法调用本类另一个成员方法

```java
public void method(){
    this.num();//调用本类而不是父类
    int id=789;
}
@Override
public void num() {//父类方法的重写
    super.num();
    System.out.println("2");
}
```

4、static里不可用this        this与super不能同时用

this与super内存分析

![](C:\Users\panqiyi\Desktop\notes\image\Snipaste_2020-03-19_10-04-54.png)

### 抽象

抽象方法:父类方法功能不确定，多个子类可以有不同的功能实现

![](C:\Users\panqiyi\Desktop\notes\image\Snipaste_2020-03-19_13-45-07.png)

格式：

抽象方法：就是加上abstract关键字，去掉大括号直接分号结束；

抽象类：抽象方法必须在抽象类（还有接口）中，在class前面写上abstract

即有抽象方法的类肯定是抽象类；

**注意：**抽象类不一定有抽象方法

```java
public abstract class Abstract {//抽象类
    public abstract void eat();//抽象方法
}
```

**如何使用抽象类和抽象方法**

1、不能直接创建new抽象类对象      (所有其父类构造方法只能被子类构造方法super();)

2、必须用一个子类继承抽象父类

3、子类必须覆盖重写抽象父类当中的所有抽象方法(子类重写父类抽象方法去掉abstract,补加大括号)     然后创建子类对象进行使用

```java
//抽象父类
public abstract class Abstract {
    public abstract void eat();
}
//------------------
//子类继承抽象父类
public class Abstracttwo extends Abstract {
    public static void main(String[] args) {
        Abstracttwo p=new Abstracttwo();
        p.eat();
    }
    @Override
    public void eat() {
        System.out.println("猫吃鱼");
    }
}
```

### 接口

接口就是多个类的公共规范

接口是一种引用数据类型，最重要的内容是其中的：抽象方法

```java
//定义接口;
public interface 接口名称{
}//编译生成的字节码文件后缀依然是.class
```

如果是java7:  接口包含  1、常量  2、抽象方法

Java8：增加 3、默认方法、4、静态方法

Java9：增加 5、私有方法

**接口中抽象方法定义**

```Java
public interface MyInterfaceAbstract {
    /*1、接口当中抽象方法修饰符必须是固定的两个关键字：public abstract
    * 2、这两个关键字可以选择性省略*/
    public abstract void methodAbs1();
    
    public  void methodAbs2();
    
     abstract void methodAbs3();
     
     void methodAbs4();
}//这4个都是抽象方法
```

**接口抽象方法的使用**

1、不能直接使用，必须有一个实现类来实现该接口

```java
public 实现类名称 implements 接口名称{
}
```

2、实现类必须对接口所有抽象方法的重写(即去abstract关键字等)

3、创建实现类对象进行使用

```java
//定义一个接口
public interface MyInterfaceAbstract {
    public abstract void methodAbs1();
    public  void methodAbs2();
}
//一个接口实现类
public class MyInterfaceAbsImpl implements MyInterfaceAbstract{
    @Override
    public void methodAbs1() {
        System.out.println("第一个");
    }
    @Override
    public void methodAbs2() {
        System.out.println("第二个");
    }
    public static void main(String[] args) {
        MyInterfaceAbsImpl impl=new MyInterfaceAbsImpl();
        impl.methodAbs1();
        impl.methodAbs2();
    }
}
```

**接口默认方法**

解决接口升级的问题

```java
public default 返回值类型 方法名称(参数列表){ //public可以省略
	方法体
}
```

2、在接口中添加的默认方法其实现类会继承默认方法，实现类可以对默认方法进行重写

**接口静态方法**

使用：在实现类直接   接口名.静态方法名

```Java
public static 返回值类型 名称(参数列表){  //public可以省略
	方法体
}
//接口的一个静态方法
public interface MyInterfaceAbstract {
    public static void methodStatic(){
        System.out.println("接口的静态方法");
    }
}
//实现类的使用
public class MyInterfaceAbsImpl implements MyInterfaceAbstract{
    public static void main(String[] args) {
        MyInterfaceAbsImpl impl=new MyInterfaceAbsImpl();
        MyInterfaceAbstract.methodStatic();
    }
}
```

**接口私有方法**

解决接口 多个默认方法 或者多个静态方法 之间代码重复问题

只有接口自己可以调用，不能被实现类或别人使用

```Java
//默认方法代码重复
public default void methodDefault1(){
    Pri();
}
public default void methodDefault2(){
    Pri();
}
private  void Pri(){
    System.out.println("你好");
    System.out.println("hello");
}
//静态方法代码重复
 public static void methodDefault1(){
        Pri();
    }
    public static void methodDefault2(){
        Pri();
    }
    private static void Pri(){
        System.out.println("你好");
        System.out.println("hello");
    }
```

**接口常量**

```java
//定义常量----"所谓变量"
public static final int NUM-Of=10; int //前面可以省略
int NUM=10;//这个也是和第一个一样的  
注意：名称要大写 多个单词下划线连接   调用是  接口名.常量名
```

**使用 接口注意**

1、接口无构造方法和静态代码块

2、一个类直接父类是唯一的，但是一个类可以实现多个接口

```Java
public class 类名 implements 接口1,接口2{
	覆盖重写的抽象方法
}
```

3、如果实现类没有全部重写接口的抽象方法，那么这个实现类就必须是抽象类

4、接口有重复的抽象方法，实现类只需要重写一次

5、接口有重复的默认方法，实现类需要对默认方法重写

6、如果直接父类的方法与接口方法重复，则默认优先使用父类方法（即继承与接口实现可以一起）

```Java
public class InterfaceMain extends Fu implements InterfaceOne//继承父类并实现接口
```

**接口的继承**

1、接口是多继承的

```Java
public interface 接口名 extends 接口1,接口2……{
}
```

2、如果多个父接口默认方法有重复，则子接口要对默认方法进行重写

**接口与抽象类的区别**

1.抽象类可以有构造方法，接口中不能有构造方法。

2.抽象类中可以有任何类型成员变量，接口中只能有`public static final`变量

3.抽象类中可以包含非抽象的其他成员方法，接口中1.8在前只有抽象方法，1.8 增加了默认方法与静态方法，1.9增加了静态方法。

4.类可以实现多个接口，但只能继承一个抽象类。

5、抽象类的抽象方法修饰符不能省略，而接口的抽象方法修饰符可以省略

**相同点：**

1、都不能直接实例化，可以使用多态。

2、如果一个类实现了接口或者抽象类，但是没有全部重写接口或者抽象类的抽象方法，那么这个实现类一定是抽象类。



### 多态

同一个对象，在不同时刻表现出来的不同形态。

**多态的前提**

1、有继承/实现关系

2、方法重写

3、子类对象 赋值 给父类引用

代码中：父类引用指向子类对象；

```
/*父类名称 对象名=new 子类名称
或者
接口名称 对象名=new 实现类名称*/
```

**2、多态中访问成员变量**

1、通过对象名访问成员变量：看等号左边是谁，优先用谁，没有向上找

```Java
Fu p=new Zi();
System.out.print(p.num);//此时num为父类成员变量
```

2、通过成员方法访问成员变量：方法是哪个类优先用谁，没有向上找；

总结：编译看左，运行也看左：编译运行都是左边父类的成员变量；

3、**多态访问成员方法**

只能调用父类成员方法和子类重写父类的方法，

如果重写了父类方法，则运行的是重写的方法

**注意：** 多态的成员变量、方法访问规则与继承一样

(总结：编译看左，运行看右)：编译 (即输入在编辑区中是否出现错误) 看父类中有没有 被调用的那个方法，如果父类中没有，则会报错；如果被调用的方法父类中有，且被子类重写，则运行的就是子类重写的父类方法；没有被子类重写则运行父类成员方法；

**多态的好处与弊端**

**好处：** 提高程序的扩展性

​		体现：定义方法时，使用父类型作为参数，使用时传入 子类型进行操作；(即 多个子类 重写父类的同一个方法 进行不同功能时)；

```java
//动物父类
public class Animals {
    public void eat(){//动物吃东西方法
        System.out.println("动物吃不同东西");
    }}
//////////////猫，动物子类
public class Cat extends Animals{
    @Override
    public void eat() {//重写动物吃东西方法
        System.out.println("猫吃鱼！");
    }}
/////////////狗，动物子类
public class Dog extends Animals {
    @Override
    public void eat() {//重写动物吃东西方法
        System.out.println("够吃骨！");
    }}
///////////////////

//不同动物吃东西的类
public class AnimalsDemo {
    /*public void CatEat(Cat cat){     //传入猫类对象
        cat.eat();    //调用猫类吃东西方法
    }
    public void DogEat(Dog dog){
        dog.eat();
    }*/

    //上面方法每增加一个动物吃的功能
    // 就需每一次都要创建对应新的方法

    //而下面多态方法，
    // 只要需在main方法 创建新添加动物对象，然后传入下面方法即可；

    public void eat(Animals ans){//多态
        // Animals ans = new  Cat();
        // Animals ans = new  Cat();
        ans.eat();
    }}
///////////////////
//main方法
public class AnimalsMain {
    public static void main(String[] args) {
        AnimalsDemo an = new AnimalsDemo();

        an.eat(new Cat());  // 传入猫类对象
        an.eat(new Dog());
        
        //如果新增某动物，直接传入其对象即可

        //结果：   猫吃鱼！
        //        够吃骨！
    }
}
```

**坏处**：多态不能调用子类特有的方法与成员变量；



**对象的向上转型**

![](C:\Users\panqiyi\Desktop\notes\image\Snipaste_2020-03-21_16-08-05.png)

弊：一旦向上转型为父类，那么就无法调用子类原本特有的方法和属性；

```Java
////////父类
public class Review01 {
    int num=100;
    int aer=66;
    public void method01(){
        System.out.println("父类方法1");
    }
    public void sss(){
        System.out.println("父类方法2");
    }
}
///////////子类
public class Review02 extends Review01{
    int num=99;
    int ber=88;
    public static void method02(){
        System.out.println("02子类方法");
    }
    @Override
    public void method01() {//重写父类方法
        System.out.println(new Review02().num);//99 02类对象调用即02类实例
        System.out.println("子类重写父类01");
    }
}
/////主方法
public class Main01 {
    public static void main(String[] args) {

        Review01 r= new Review02();//子类对象 赋值给 父类引用

        r.method01();//子类的  子类重写父类方法，优先使用子类重写父类的方法
        //r.sss
        //不能调用子类特有方法  method02()

        System.out.println(r.num);// 100  父类num
        //只能调用右边父类的成员变量，没有继续往上找，不能调用子类的成员变量   这里就不能调用子类成员变量  ber=88;
        //可以调用父类的 aer=66;
    }
}
```

**对象的向下转型**

![](C:\Users\panqiyi\Desktop\notes\image\Snipaste_2020-03-21_16-22-04.png)

解决向上转型时就要用到 向下转型    

**instanceof判断父类引用对象本来是哪个子类**

```java
Animal aim=new Dog();

public static void giveAnimal(){
if(aim instanceof Dog){
Dog dog=new Dog();
dog.watchHouse();
}
if(aim instanceof Cat){
Cat cat=new Cat();
cat.eat();
}
```

### final

常见的四类用法：

用来修饰一个类；修饰一个方法；修饰一个局部变量；修饰一个成员变量

1、final关键字修饰类

```Java
public final class 类名{}
```

final修饰的类不能有子类

2、final修饰的方法不能被重写

3、final修饰变量时变量的值不可改变，修饰引用变量时(如对象引用)是地址值不可以改变

4、注意：成员方法有初始值(与数组给的初始值一致)；而局部变量没有初始值；所以成员变量在使用final时必须手动赋值；

### 权限修饰符

![](C:\Users\panqiyi\Desktop\my-note\notes\image\Snipaste_2020-03-23_11-50-18.png)

### 内部类

分类：

1、成员内部类      2、局部内部类(包含匿名内部类)

**成员内部类**

```
修饰符 class 外部类名称{
	修饰符 class 内部类名称{
	}
}
```

注意：内用外，随便用；外用内，需要内部类对象

外部类使用成员内部类：

1、间接使用：先在外部类方法内创建内部类对象，外部类再调用自己的那个方法从而使用了内部类

2、直接使用：在外部类的main方法中直接创建内部类对象

```java
外部类.内部类 对象=new 外部类().new 内部类();
```

3、使用重名的外部类成员变量

```java
public class Ppdp {
    int num=20;//外部类成员变量；
    public class Nei{
        int num=10;//内部类成员变量；
        public void print(){
            int num=30;//内部类成员方法局部变量
            System.out.println(num);//30
            System.out.println(this.num);//10
            System.out.println(Ppdp.this.num);//20
        }// 重名 内用外成员变量   外类名.this.变量
    }
    public static void main(String[] args) {
        Ppdp.Nei p=new Ppdp().new Nei();
        p.print();
    }
}
```

**局部内部类**

1、定义在方法内部；只有当前方法才能使用它，方法外不能使用

```Java
修饰符 class 外部类名称{
	修饰符 返回值类型 方法名(参数列表){
		class 局部内部类{
		//……
		}
	}
}
```

注意：定义类时修饰符规则：

1、外部类：public  //  (default)

2、成员内部类：public  //  protected  //  (default)  //  private

3、局部内部类：什么都不写

4、局部内部类访问所在方法的局部变量：此变量得是不可变的

![](C:\Users\panqiyi\Desktop\my-note\notes\image\1.png)

**匿名内部类**

当接口的实现类(或者父类的子类)只需要使用一次；那么可以使用匿名内部类，可以减少定义一个正常类；直接在main方法使用匿名内部类，然后直接调用

```Java
//格式
接口(或父类)名  对象名=new 接口(或父类名)() {
	重写接口(或父类)所有方法
};//注意这里的分号

public static void main(String[] args) {
    InterfaceNi obj=new InterfaceNi() {
        @Override
        public void method() {
            System.out.println("匿名实现类");
        }
    };
    obj.method();
    //或者
     new InterfaceNi() {
            @Override
            public void method() {
                System.out.println("匿名实现类");
            }
        }.method();
}
```

### 类作为成员变量类型

切记：是引用变量，传来的是地址

```Java
public class InterNi  {//类1
    private String jian;
    //省略了两个构造与set
    public String getJian() {
        return jian;
    }
}
public  class InterfaceNi {//类2
    private InterNi interNi;// 类1类型的成员变量
    //省略了两个构造与get
    public void print(){
        System.out.println(interNi.getJian());//此时interNi是类1的对象
    }
    public void setInterNi(InterNi interNi) {
        this.interNi = interNi;
    }
}//main方法类
public class MainNi {
    public static void main(String[] args) {
        InterfaceNi interfaceNi=new InterfaceNi();//类2对象
        InterNi interNi=new InterNi("长剑");//类1赋值 此对象携带了值地址
        interfaceNi.setInterNi(interNi);//将值地址赋值给类2中的引用变量
    }
}

```

### 接口作为成员变量类型

```Java
只写了main方法类    因为其他跟类成为成员变量是一样的  传递的是地址 
public static void main(String[] args) {
    //匿名内部类实现
    InterLol lol=new InterLol() {
        @Override
        public void use() {
            System.out.println("biu~bia~~~~");
        }
    };
    LolClass1 lu=new LolClass1();
    lu.setName("艾希");
    lu.setInterLol(lol);
    lu.print();

    //匿名内部类加匿名对象
    LolClass1 lu=new LolClass1();
    lu.setName("艾希");
    lu.setInterLol(new InterLol() {//相当于上面lu.setInterLol(lol);
        @Override
        public void use() {
            System.out.println("biu~bia~~~~");
        }
    });
```

### 重写Object类的equals方法

因为equals方法比较对象时是比较地址值

重写实现比较内容；

快捷键：Alt+ins  然后选择对应项

### Objects类的equals方法

jdk7后增加了Objects工具类，由一些静态方法构成，这些方法是空指针安全的；使用Objects类的equals可以避免空指针异常

```java
public static void main(String[] args) {
        String str1=null;
        String str2="aBc";
//        boolean b1=str1.equals(str2); 异常,null不能调用方法
        boolean b2= Objects.equals(str1,str2);//
        System.out.println(b2);
    }
//也可以用数组，集合等Object的子类调用
```

### Date日期类的方法

![](C:\Users\panqiyi\Desktop\my-note\notes\image\2.png)

**两个构造方法**

1、获取系统时间  空参构造方法

```java
Date date=new  Date();
System.out.println(date);
```

2、传递毫秒值转换为Date日期   有参构造方法

```Java
Date p1=new Date(532827825236L);
System.out.println(p1);
```

**一个成员方法**

返回1970年1月1日00：00：00  gmt  到 当前系统日期的毫秒值

```Java
Date p2=new Date();
long time = p2.getTime();
System.out.println(time);
```

### DateFormat类

位于java.text包下 是日期/时间格式化的抽象类

1、格式化(将日期-->文本)       2、解析  (文本-->日期)  

抽象类不能new   而SimpleDateFormat  extends  DateFormat

y   年     M    月    d    日      H    时     m   分    s   秒    S   毫秒

1、通过SimpleDateFormat的构造方法传递指定模式

2、调用SimpleDateFormal对象的方法format，按照构造方法中指定模式，把Date日期格式化为符合模式的字符串

```Java
private static void date3() {
    SimpleDateFormat spd=new SimpleDateFormat("yyyy年MM月dd日 HH时mm分ss秒");//设置要转化的指定模式
    Date date3=new Date();//创造Date类的对象 空参即系统时间
    String format = spd.format(date3);//按照构造方法中的模式格式化
    System.out.println(format);
}
```

3、调用SimpleDateFormal对象的方法parse，按照构造方法中指定模式，将传入parse方法的日期/时间也写成对应格式    此方法将还原为原始Date格式

```Java
private static void date4() throws ParseException {
    SimpleDateFormat apd1=new SimpleDateFormat("yyyy-MM-dd HH:mm:ss");//格式
    Date parse = apd1.parse("2088-12-23 23:23:12");//按照格式输入
    System.out.println(parse);
}
```

此parse方法会有异常 （alt+enter修复异常）

### Calendar日历类

在java.util包下   Calendar是一个抽象类   不能new对象

1、Calendar 类里面有一静态方法getInstance() (子类重写) 该方法返回了Calendar类的子类对象

```Java
Calendar instance = Calendar.getInstance();//多态 
System.out.println(instance);//输出很多日历信息
```

**Calendar常用方法**
西方的月份0~11东方1~12所以输出的月份要比当时月份少1
Calendar类中有很多静态成员变量(就是上面getlnstance()方法返回日历信息的内容赋值给相对应的静态变量)
：静态变量所以用类名直接调用

![](C:\Users\panqiyi\Desktop\notes\image\3.png)

1、get()成员方法：获取指定成员静态变量的值

```java
public static void main(String[] args) {   
    Calendar cd=Calendar.getInstance();
    System.out.println(cd);
    int year = cd.get(Calendar.YEAR);    
    int month = cd.get(Calendar.MONTH);    
    int date = cd.get(Calendar.DATE);
    System.out.println(year+"年"+month+"月"+date+"日");
}//西方月份比东方少1

```

2、set()成员方法：设置指定成员变量的值

```java
public static void main(String[] args) {    
   Calendar cd=Calendar.getInstance();
   System.out.println(cd);
   cd.set(Calendar.YEAR,9899);//给年设值
   cd.set(Calendar.MONTH,10);    
   cd.set(Calendar.DATE,1);    
   int year = cd.get(Calendar.YEAR);    
   int month = cd.get(Calendar.MONTH);    
   int date = cd.get(Calendar.DATE);
   System.out.println(year+"年"+month+"月"+date+"日"); 
}//输出9899年10月1日

```

set()方法一次设置年月日：

```java
public static void main(String[] args) {    
    Calendar cd=Calendar.getInstance();    
    cd.set(9999,10,1);    
    int year = cd.get(Calendar.YEAR);    
    int month = cd.get(Calendar.MONTH);    
    int date = cd.get(Calendar.DATE);
    System.out.println(year+"年"+month+"月"+date+"日");
}

```

3、add()成员方法：增加/减少指定静态成员值

```java
public static void main(String[] args) {    
     Calendar cd=Calendar.getInstance();
     cd.set(9999,10,1);//9999年10月1日
     cd.add(Calendar.YEAR,-5);//年减5
     cd.add(Calendar.MONTH,-5);//月减5
     cd.add(Calendar.DATE,5);//日加5
     int year = cd.get(Calendar.YEAR);
     int month = cd.get(Calendar.MONTH);
     int date = cd.get(Calendar.DATE);  
     System.out.println(year+"年"+month+"月"+date+"日");
}//输出9994年5月6日
```

4、getTime()成员方法：把日历对象转化为日期对象

```java
public static void main(String[] args) {
	Calendar cd=Calendar.getInstance();
	Date time = cd.getTime();
	System.out.println(time);
}//输出内容即Date无参时输出内容  即当前系统时间
```

### System类

常用静态方法：

1、currentTimeMillis方法：获取当前时间的毫秒值

常用于计算程序效率，与计算机性能有一定关系

```Java
long time1 = System.currentTimeMillis();
System.out.println("for循环前时间"+time1);
for (int i = 0; i < 9999; i++) {
    System.out.print(i);
}
System.out.println();
long time2 = System.currentTimeMillis();
System.out.println("for循环后时间"+time2);
long time = time2-time1;
System.out.println("程序用时："+time);
```

2、System.exit()

终止当前运行的Java虚拟机。

```java
public static void main(String[] args) {
    System.out.println("开始");

    System.exit(0);
java
    System.out.println("结束");
}//结果：开始
```

3、数组的复制

```Java
int[] array1={1,2,3,4};
int[] array2={5,6,7,8};
System.arraycopy(array1,0,array2,1,3);
//剪切数组，剪切位置，复制到的数组，复制起始位置，剪切元素个数
System.out.println(Arrays.toString(array2));
//输出 [5, 1, 2, 3]
```

### StringBuilder类

String类与StringBuilder类的区别：

![](C:\Users\panqiyi\Desktop\notes\image\4k.png)

![](C:\Users\panqiyi\Desktop\notes\image\5.png)

1、构造方法

空参构造方法：

构造一个不带如何字符的字符串生成器，其初始容量为16个字符

有参构造方法：

构造一个字符串生成器，初始化内容为指定的字符串内容

```java
//无参
StringBuilder strb=new StringBuilder();
System.out.println("输出内容:"+strb);//输出内容:
//有参
StringBuilder strb1=new StringBuilder("abc");
System.out.println("输出内容:"+strb1);//输出内容:abc
```

**常用方法**

1、append()成员方法：添加任意类型数据的字符串，并返回对象自身

```Java
StringBuilder bu=new StringBuilder();
//bu.append() 返回bu对象自身
StringBuilder bu2 = bu.append("abc");//bu对象地址赋值给bu2
System.out.println(bu);
System.out.println(bu2);
System.out.println(bu==bu2);//true  地址相等
```

使用append方法无需接收返回值；直接对象.append 添加字符串内容

```java
bu.append(123);
bu.append(3.14);
bu.append("abc");
bu.append('中');
System.out.println(bu);//1233.14abc中
```

更为简便的方法：链式编程  (因为bu.append返回的是对象自身  所以添加时可以调用append()再次添加)

```Java
bu.append(123).append(3.14).append("abc").append('中');
System.out.println(bu);//1233.14abc中
```

2、StringBuilder的tostring方法：转化为String类

```Java
String str="Hello";
//String-->StringBuilder
StringBuilder bu=new StringBuilder(str);
bu.append("World");
System.out.println(bu);
//StringBuilder-->String
String s = bu.toString();
System.out.println(s);
```

3、reverse()  字符串反转

### 包装类

把基本数据类型变为为引用数据类型

八大基本数据类型对应的包装类:除了int与char特殊  其他的包装类都是将首字母改为大写

| 基本数据类型 | byte | short | int     | long | float | double | boolean | char      |
| ------------ | ---- | ----- | ------- | ---- | ----- | ------ | ------- | --------- |
| 包装类       | Byte | Short | Integer | Long | Float | Double | Boolean | Character |

  **装箱与拆箱**

基本数据类型与对应的包装类对象之间，来回转换的过程称为"装箱"与”拆箱“；

装箱：基本数据类型转换为对应的包装类对象

拆箱：包装类对象转换为对应的基本数据类型

```Java
        //装箱：
        //静态方法
        Integer in1 = Integer.valueOf(3);
        Integer in2 = Integer.valueOf("3");
        //Integer in2 = Integer.valueOf("a");错误 只能是基本数据类型字符
        System.out.println(in1);
        System.out.println(in2);
        //拆箱：
        int i = in1.intValue();//in1对象拆箱
        System.out.println(i);
```

**自动装箱与自动拆箱**

基本数据类型与对应的包装类之间的自动相互转换

```Java
Integer in=3;//相当于Integer in = Integer.valueOf(3);
int in1=in;//相当于int in1=in.intValue()
System.out.println(in1);
ArrayList<Integer> list=new ArrayList<>();
list.add(4);//自动装箱
```

**基本数据类型与字符串的转换** 

```Java
//基本数据类型-->字符串(String)
        //方法1
        int i=100;
        String str1=i+"";//常用  基本数据直接+""
        System.out.println(str1);

        //方法2
        String str2=Integer.toString(99);
        System.out.println(str2);
 
        //方法3
        String str3=String.valueOf(999);
        System.out.println(str3);

        //字符串-->基本数据类型
        int i1 = Integer.parseInt(str1);
        double i2 = Double.parseDouble(str2);
        System.out.println(i1);
        System.out.println(i2);
```

### 集合

**集合框架**

<img src="C:\Users\panqiyi\Desktop\notes\image\7.png" style="zoom:150%;" />

#### Collection常用功能

Collection是所有单列集合的最顶层接口，里面定义了所有单列集合共性的方法，任意的单列集合都可以使用Collection接口中的方法

7个共性方法：

```Java
public boolean add();//把给定的元素添加到当前集合中

public void clear();//清空集合中所有元素

public boolean remove();///把给定的元素在当前集合中删除

public boolean contains();//判断当前集合中是否有给定的元素

public boolean isEmpty();//判断当前集合是否为空

public int size();//返回集合中的个数

public Object[] toArray();//把集合中的元素储存到数组中
```

7种方法的使用：

```Java
public static void main(String[] args) {
    Collection<String> coll=new ArrayList<>();//多态
    coll.add("张三");
    coll.add("李四");
    coll.add("王五");
    System.out.println(coll);//[张三, 李四, 王五]

    boolean i1 = coll.remove("李四");
    System.out.println(i1);//集合中有该元素就删除并返回true
    System.out.println(coll);//[张三, 王五]
    //如果没有  则返回false  集合不变

    boolean i2 = coll.contains("王五");
    System.out.println(i2);//true
    // 集合有该元素则返回true   没有返回false

    boolean empty = coll.isEmpty();
    System.out.println(empty);//false
    //集合为空则返回true  不为空则返回false

    int size = coll.size();
    System.out.println(size);//2  (前面删除了一个)
    //返回集合元素个数

    Object[] array = coll.toArray();
    for (Object n:array) {
        System.out.print(n+"\t");
    }//张三  王五

    coll.clear();
    System.out.println(coll);//[]
    //清空集合中的所有元素   但是集合还存在

}
```

### Iterator迭代器

**迭代:** 对集合的遍历

#### Iterator接口

Iterator接口无法直接使用；需要使用接口的实现类对象，他获取实现类的方式比较特殊；Collection接口中有 iterator()方法  该方法返回的就是迭代器的实现类对象

**迭代器使用步骤**

1、使用集合中的方法iterator()获取迭代器的实现类对象，使用Iterator接口接收(多态写法)

2、使用Iterator接口中的方法hasNext判断还有没有下一个元素

3、使用Iterator接口中的方法next取出集合中的下一个元素

```Java
//创建一个集合对象
Collection<String> coll=new ArrayList<>();
//往集合中添加元素
coll.add("科比");
coll.add("乔丹");
coll.add("詹姆斯");
coll.add("艾弗森");

//注意：Iterator接口也是有泛型的，迭代器泛型与集合相同
//接口对象来接收实现类对象  多态
Iterator<String> it = coll.iterator();

while (it.hasNext()){//判断  有元素true则继续循环
    String e = it.next();//获取元素
    System.out.println(e);
}
```

**Iterator迭代原理**

![](C:\Users\panqiyi\Desktop\notes\image\8.png)

### 增强for循环

foreach: 底层使用的也是迭代器，使用了for循环格式，简化了迭代器  (没有索引)

```Java
for(集合/数组类型 变量名 : 集合/数组名){
    System.out.println(变量名);
}
```

```java
//for each循环
int[] array={1,2,3,4,5,6};
for(int n:array){
	System.out.print(n);
}
//for each循环可以直接遍历数组的每个元素
//二维数组的遍历
int[][] arr={{12,34,45,5},{1,2,3,4},{55,77,88}};
        for (int[] d:arr) {//二维数组中是int[] 类型
            for (int n:d) {//一维数组中是int 类型
                System.out.print(n+",");
            }
            System.out.println();
        }
//集合的遍历
 //创建一个集合对象
        Collection<String> coll=new ArrayList<>();
        //往集合中添加元素
        coll.add("科比");
        coll.add("乔丹");
        coll.add("詹姆斯");
        coll.add("艾弗森");
        for (String n:coll) {
            System.out.println(n);
        }
```

### 泛型

是一种未知的数据类型，当我们不确定用什么数据类型时可以用泛型；  泛型也可以看作一个变量  用来接收数据类型

E  e:Element  元素

T  t:Type   类型

![](C:\Users\panqiyi\Desktop\notes\image\10.png)

**为什么要使用泛型**

创建集合对象，**不使用泛型**

好处：

​	集合不使用泛型，默认的类型就是Object类型，可以储存任意数据类型

弊端：

不安全，会引发异常

创建集合对象，**使用泛型**

好处：

1、避免了类型转换的麻烦，储存的是什么类型，取出的就是什么类型

2、把运行异常(代码运行后抛出的异常)，提升到编译(写代码的时候会报错)

弊端：

泛型是什么类型，就只能储存什么类型的数据

#### 含泛型的类

注意：泛型<E>中的E可以是任意字母

```Java
public class GenericClass<E> {//定义泛型类(即数据类型未定义)
    private E name;
    public E getName() {
        return name;
    }
    public void setName(E name) {
        this.name = name;
    }
}
```

使用：在创建对象的时候确定数据类型；建立不同对象时可以定义不同的数据类型

```Java
public static void main(String[] args) {
    GenericClass<String> gc=new GenericClass<>();
    gc.setName("asdf");
    System.out.println(gc.getName());
    GenericClass<Integer> gc2=new GenericClass<>();
    gc2.setName(123);
    System.out.println(gc2.getName());
}
```

#### 含泛型的方法

定义含泛型的方法：泛型定义在修饰符与返回值之间

```Java
public class GenericMethod {
    //定义一个含有泛型的成员方法
    public <E> void method(E e){
        System.out.println(e);
    }
    //定义一个含有泛型的静态方法
    public static <E> void method1(E e){
        System.out.println(e);
    }
}
```

使用：

```Java
public static void main(String[] args) {
    GenericMethod gm=new GenericMethod();
    //调用方法时传递什么类型数据  泛型就是什么数据
    gm.method("你好");
    gm.method(666);

    GenericMethod.method1(3.14);//静态方法调用
    GenericMethod.method1("hello");
}
```

#### 含泛型接口

**方式一：**

定义一个含泛型的接口：

```Java
public interface GenericInterface<I> {
    public abstract void method(I i);
}
```

创建一个接口实现类：创建实现类时指定数据类型

```Java
public class GenInterfaceImp implements GenericInterface<String> {//在实现类中指定接口数据类型
    @Override
    public void method(String s) {
        System.out.println(s);
    }
}
```

使用：

```Java
public static void main(String[] args) {
    GenInterfaceImp in=new GenInterfaceImp();
    in.method("字符串");
    //实现类指定什么数据类型  调用时就只能为什么类型的数据
}
```

**方式2：**

与方式一一样定义一个含泛型的接口：

```Java
public interface GenericInterface<I> {
    public abstract void method(I i);
}
```

创建一个实现类：创建实现类时不指定数据类型

```Java
public class GenInterfaceImp<I> implements GenericInterface<I> {
    @Override
    public void method(I i) {
        System.out.println(i);
    }
}
```

使用：创建对象是指定泛型的数据类型 (与含泛型类的使用一样)

```Java
public class InterfaceMain {
    public static void main(String[] args) {
        GenInterfaceImp<String> gf=new GenInterfaceImp<>();
        gf.method("nihao");
    }
}
```

#### 泛型通配符

<?>  :代表任意数据类型

使用方式：

不能创建对象使用；      只能作为方法的参数使用

```Java
public static void main(String[] args) {
    ArrayList<String>  st=new ArrayList<>();
    st.add("a");
    st.add("b");
    st.add("c");

    ArrayList<Integer> list=new ArrayList<>();
    list.add(1);
    list.add(2);
    list.add(3);

    printArray(st);//同一个方法但是传入的对象数据类型不同
    printArray(list);
}
public static void printArray(ArrayList<?> list){
    for (int i = 0; i < list.size(); i++) {
        System.out.println(list.get(i));
    }
}
```

**通配符的高级用法(了解即可)**

泛型的上线限定：<？extends E>    代表使用的泛型只能是E类型的子类或本身

泛型的下限限定：<？ super  E>    代表使用的泛型只能是E的父类或本身

### 集合案例

斗地主：

使用集合工具类Collections中的方法
static void shuffle(List<?> list);//使集合内元素随机存放

```Java
public static void main(String[] args) {
    //1、准备牌
    //定义一个集合储存54张牌
    ArrayList<String> poker=new ArrayList<>();
    //定义两个数组  储存花色和序号
    String[] colcrs={"♠","♥","♣","♦"};
    String[] num={"2","A","K","Q","J","10","9","8","7","6","5","4","3"};
    //添加大王/小王到集合中
    poker.add("大王");
    poker.add("小王");

    for (String nu:num) {
        for (String col:colcrs) {
           //把组装好的牌储存到poker集合中
            poker.add(col+nu);
        }
    }
    System.out.println(poker);

    //洗牌
    //使用集合工具类Collections中的方法
    //static void shuffle(List<?> list);//使集合内元素随机存放

    Collections.shuffle(poker);
    System.out.println(poker);

    //发牌
    //遍历poker集合 (不用foreach因为它没有索引)
    //创建四个集合储存  3人+1底牌
    ArrayList<String> play1=new ArrayList<>();
    ArrayList<String> play2=new ArrayList<>();
    ArrayList<String> play3=new ArrayList<>();
    ArrayList<String> dipai=new ArrayList<>();
    for (int i = 0; i < poker.size(); i++) {
        String p = poker.get(i);
        if(i>=51){
            dipai.add(p);
        }else if (i%3==0){//0%3==0 1%3==1 2%3==2
            play1.add(p);
        }else if (i%3==1){
            play2.add(p);
        }else if (i%3==2){
            play3.add(p);
        }
    }
    System.out.println("玩家1"+play1);
    System.out.println("玩家2"+play2);
    System.out.println("玩家3"+play3);
    System.out.println("底牌"+dipai);

}
```

### 数据结构

#### 栈

特点：进栈也称压栈     出栈也称弹栈

入口与出口同一侧  ：“先进后出”  如弹夹一样

![](C:\Users\panqiyi\Desktop\notes\image\11.png)

#### 队列

特点：入口与出口在集合的两侧

特点：先进先出  

![](C:\Users\panqiyi\Desktop\notes\image\12.png)

#### 数组

查询快：地址连续；通过数组首地址找到数组；通过索引快速查询

增删慢：数组长度固定不变想要增加或删除需要创建另一个数组把原数组复制过来

![](C:\Users\panqiyi\Desktop\notes\image\13.png)

#### 链表

查询慢：地址不连续；每一次查询元素，都必须从头开始查询

增删快：链表增加/删除一个元素对链表结构无影响，所以增删快

![](C:\Users\panqiyi\Desktop\notes\image\14.png)

#### 树

![](C:\Users\panqiyi\Desktop\notes\image\17.png)

**二叉树**

每一个节点的子节点为2

![](C:\Users\panqiyi\Desktop\notes\image\16.png)

##### 二叉搜索树

1、若它左子树结点不空，左子树上所有结点都比根小

2、若右边子树结点不空，右子树上所有结点都比根大

它的左右子树也分别为二叉排序树

![](C:\Users\panqiyi\Desktop\notes\image\18.png)

查找结点：从根开始查找，查找比当前结点大的，则搜索右子树，查找比根小的，则搜索左子树；查找值等于当前结点值停止搜索（终止条件）

插入结点：从根开始比较，小往左，大往右，直到空的位置插入

遍历结点：最常用中序遍历：左子树-->根结点-->右结点（优点：从小到大的顺序）

查找最大值与最小值：最小值在树的最左边  最大值在最右边

删除结点：

1、删除叶结点：将父结点指向该结点的地址改为null;

2、删除有一个结点的结点：将其父结点指向它的地址改为它的子结点

3、删除有两个结点的结点：将其父结点指向它的地址改为它的右子结点中的最小结点 

**平衡树：**左右高度差不超过1

##### 红黑树

1、根结点是黑色

2、每个空结点是黑色

3、每个红结点的两个子节点一定是黑色，不能有两个红色结点相连

4、任意结点到叶子节点的路径包含相等的黑结点

**变色：**结点颜色由黑变红

**左旋：**以某个结点作为旋转结点，其右子结点变为旋转结点的父结点，右子结点的左子结点(右子结点不变)变为旋转结点的右子结点

**右旋：**以某个结点为旋转结点，其左子结点变为旋转结点的父结点，左子结点的右子结点(左子结点不变)变为旋转结点的左结点

**查找：**与二叉搜索树一样

**插入结点**

注意：插入的结点是红色

### List< E>接口

1、有序的集合，储存元素与取出元素顺序一样

2、有索引，包含了一些带索引的方法

3、允许储存重复的元素

**List接口特有带索引的方法**

```java
public void add(int index,E element);//将指定元素添加到集合指定位置
public E get(int index);//返回集合指定位置的元素
public E remove(int index);//删除集合指定位置元素并返回
public E set(int index,E element);//用指定元素替换集合中指定位置元素，返回原来那个元素
```

#### Arraylist集合

底层为数组结构，增删慢，查找快；多线程

#### LinkedList集合

底层为链表结构，增删快，查询慢；多线程

特有的方法(成员方法）：

多态不能使实现类(或者子类)成员方法

```Java
addFirst(E e);//将指定元素添加到列表开头
addLast(E e);//将指定元素添加到列表的结尾
//addLast()作用与add()一样
push();//与addFirst一样

removeFirst();//删除第一个并返回
removeList();//删除最后一个并返回
pop();//作用与removeFirst()一样
```

#### Vector集合(了解)

底层为数组结构，单线程

### Set< E>接口

### HashSet<>集合

1、不允许储存重复的元素，

2、没有索引，没有带索引的方法，也不能用普通for循环遍历

3、是无序集合，储存元素与取出元素的顺序可能不一致

4、底层是一个哈希表(查询速度非常快)

#### 哈希值

系统随机给出的十进制逻辑地址值，并非数据实际物理储存地址

在Object类中有  hashCode()方法 返回对象哈希值

```Java
public class HashMain {
     @Override
    public int hashCode() {
        return super.hashCode();
    }
    public static void main(String[] args) {
        HashMain hash=new HashMain();
        int i = hash.hashCode();
        System.out.println(i);//764977973
        String name="abc";
        System.out.println(name.hashCode());//96354
    }
}
```

重写hashCode

```java 
public class HashMain {
    @Override
    public int hashCode() {
        return 666;
    }
    public static void main(String[] args) {
        HashMain hash=new HashMain();
        int i = hash.hashCode();
        System.out.println(i);//666
    }
}
```

#### 哈希表

jdk1.8之前：哈希表=数组+链表

jdk1.8之后：哈希表=数组+链表  或者  哈希表=数组+红黑树(提高查询速度)

数组结构：将元素按哈希值进行分组

链表/红黑树：将相同的哈希值的元素连接在一起

<img src="https://gitee.com/panqiyi/pqimg/raw/master/20201125084156.png" alt="image-20201125084156360" style="zoom:80%;" />

**set集合中元素不重复原理**

![](C:\Users\panqiyi\Desktop\notes\image\21.png)

**自定义类型元素要重写hashCode和equals方法**

如类  ；重写这两个方法才能使储存数据到set集合时不重复

重写toString()方法 打印的才是属性内容，否则是地址值

注意：这三个方法的重写都可以由Alt+ins生成

```Java
public class Students {
    private String name;
    private int age;

    @Override
    public String toString() {//重写toString方法
        return "Students{" +
                "name='" + name + '\'' +
                ", age=" + age +
                '}';
    }
    @Override
    public boolean equals(Object o) {//重写equals方法
        if (this == o) return true;
        if (o == null || getClass() != o.getClass()) return false;
        Students students = (Students) o;
        return age == students.age &&
                Objects.equals(name, students.name);
    }
    @Override
    public int hashCode() {//重写hashCode方法
        return Objects.hash(name, age);
    }
    public Students() {
    }
    public Students(String name, int age) {
        this.name = name;
        this.age = age;
    }
    public String getName() {
        return name;
    }
    public void setName(String name) {
        this.name = name;
    }
    public int getAge() {
        return age;
    }
    public void setAge(int age) {
        this.age = age;
    }
}
```

```Java
public class HashMain {
    public static void main(String[] args) {
        HashSet<Students> p=new HashSet<>();
        Students stu=new Students("你好",18);
        Students stu2=new Students("你好",18);
        Students stu3=new Students("bu好",18);
        p.add(stu);
        p.add(stu2);
        p.add(stu3);
        System.out.println(p);
    }
    //[Students{name='bu好', age=18}, Students{name='你好', age=18}]  这样就不会储存重复
}
```

#### LinkedHashSet集合

1、底层是哈希表+链表(保证迭代顺序)

2、有序集合，储存元素与取出元素顺序一致

```java
public static void main(String[] args) {
    HashSet<String> st=new HashSet<>();
    st.add("www");
    st.add("abc");
    st.add("it");//abc,www,it
    System.out.println(st);//无序，储存与打印顺序不一致
    LinkedHashSet<String> st1=new LinkedHashSet<>();
    st1.add("www");
    st1.add("abc");
    st1.add("it");//www,abc,it
    System.out.println(st1);//有序，储存与打印顺序一致
}
```

#### TreeSet集合

不同步，多线程，线程不安全

1、默认是自然顺序排序(如 Integer升序)

2、元素不能重复(通过compareTo()方法比较没有返回0,则两个对象不相等.(如果返回0,两个元素相等,则集合不添加相等元素).这个TreeSet确保无重复元素的依据.)   

 前面的HashSet与LinkedHashSet 是通过hashCode()方法equals比较，使元素不能重复    (HashSet与LinkedHashSet使用比较器都无效)

### Comparable<>比较器

```Java
public class ZiDingYi implements Comparable<ZiDingYi>{
    private String name;
    private int age;

    public ZiDingYi() {
    }
    public ZiDingYi(String name, int age) {
        this.name = name;
        this.age = age;
    }
    public String getName() {
        return name;
    }
    public void setName(String name) {
        this.name = name;
    }
    public int getAge() {
        return age;
    }
    public void setAge(int age) {
        this.age = age;
    }

    @Override
    public String toString() {
        return "ZiDingYi{" +
                "name='" + name + '\'' +
                ", age=" + age +
                '}';
    }
    @Override
    public int compareTo(ZiDingYi ziDingYi) {
        int i = this.name.compareTo(ziDingYi.name);//String类实现了comparable接口,调用compareTo按照字母升序排序，整体前加负号则降序
        int i1 = this.getAge() - ziDingYi.getAge();//按找年龄升序排序
        int num=(i==0?i1:i);//当i=0即name相等时，按照年龄升序排序，(当年龄与姓名都一样，则重复，不储存)
        return num;
    }
    //return 0;比较者等于被比较者，则表示两个元素重复，不储存；
    //return 正数;比较者大于被比较者
    //return 负数;比较者小于被比较者
    //return this. -参数.  升序  反正降序  
}
//////////////////////////////////////////////////////////
public static void main(String[] args) {
        TreeSet<ZiDingYi> set=new TreeSet<>();
        set.add(new ZiDingYi("nas",12));
        set.add(new ZiDingYi("yas",12));
        set.add(new ZiDingYi("as",12));
        set.add(new ZiDingYi("jas",12));
        set.add(new ZiDingYi("jas",18));
        set.add(new ZiDingYi("jas",8));
        for (ZiDingYi ziDingYi : set) {
            System.out.println(ziDingYi);
        }
    /*ZiDingYi{name='as', age=12}
	ZiDingYi{name='jas', age=8}
	ZiDingYi{name='jas', age=12}
	ZiDingYi{name='jas', age=18}
	ZiDingYi{name='nas', age=12}
	ZiDingYi{name='yas', age=12}*/
    }
```

自定义类的字符串的比较器用法

```Java
public static void main(String[] args) {
    ArrayList<String> list = new ArrayList<>();

    list.add("ddd");
    list.add("aa");
    list.add("ee");
    list.add("ccc");

    System.out.println(list);

    //Collections下的sort方法自然排序(升序)
    Collections.sort(list);
    System.out.println(list);

    //Collections下的sort方法,使用Comparator比较器比较大小
    Collections.sort(list, new Comparator<String>() {
        @Override
        public int compare(String s1, String s2) {
            int i=-s1.compareTo(s2); //升序
           // int i=s2.compareTo(s1); //降序
           // int i=-s1.compareTo(s2); //降序
            return i;
        }
    });
    System.out.println(list);
}
```

### 可变参数

底层是数组结构；一个数据类型，传入多个数据；

```Java
public static void main(String[] args) {
    int add = add(10, 20, 40, 9);
    System.out.println(add);
}
public static int add(int...arr){
    int sum=0;
    for (int n:arr) {
        sum+=n;
    }
    return sum;
}
```

**注意：**

1、一个方法的参数列表只能有一个可变参数

2、当一个方法的参数列表有多个数据类型和一个可变参数时，可变参数一定放在最右边；

```Java
public static void main(String[] args) {
   print("nihao",true,12,13,14);
}

private static void print(String name,boolean num,int...arr) {
    System.out.println(name);
    for (int n:arr) {
        System.out.println(n);
    }
    System.out.println(num);
}
//特殊写法  (Object...obj){}  此时可以传递任意类型数据
```

### Collections集合工具类

用于对集合进行操作，下面是部分**静态**方法：

```Java
ArrayList<String> st=new ArrayList<>();
        Collections.addAll(st,"a","d","c","b");//往集合中一次添加多个元素
        System.out.println(st);
        Collections.shuffle(st);//打乱集合中元素的顺序
        System.out.println(st);
		Collections.sort(st);//排序，默认升序
        System.out.println(st);//a,b,c,d
//特别注意：Collections.sort()排序只能是List接口下的集合
```

**当泛型是自定义类时的排序：**该自定义类需要实现Comparable接口，重写接口中的CompareTo定义排序规则；

```Java
public class ZiDingYi implements Comparable<ZiDingYi> {//注意泛型
    private String name;
    private int age;
    public ZiDingYi() {
    }
    public ZiDingYi(String name, int age) {
        this.name = name;
        this.age = age;
    }
    public String getName() {
        return name;
    }
    public void setName(String name) {
        this.name = name;
    }
    public int getAge() {
        return age;
    }
    public void setAge(int age) {
        this.age = age;
    }
    @Override
    public String toString() {//重写toString方法
        return "ZiDingYi{" +
                "name='" + name + '\'' +
                ", age=" + age +
                '}';
    }
    @Override
    public int compareTo(ZiDingYi ziDingYi) {
        int i= this.getAge()-ziDingYi.getAge();
        int i1=this.name.compareTo(ziDingYi.name);
        int num=(i==0?i1:i);
        return num;
    }//重写compareTo方法
}
///////////////////////////////////////////////
public class ZiDiYiMain {
    public static void main(String[] args) {
        ArrayList<ZiDingYi> zdy=new ArrayList<>();
        zdy.add(new ZiDingYi("小米",12));
        zdy.add(new ZiDingYi("小红",20));
        zdy.add(new ZiDingYi("小名",17));
        Collections.sort(zdy);
        System.out.println(zdy);
    }
}
```

**排序规则** 

return this.get-参数.get：升序 ；反正降序 (this.age也可以)

**Comparator接口匿名内部类排序**(比较器)

```Java
public class ZiDingYi{
    private String name;
    private int age;

    public ZiDingYi() {
    }

    public ZiDingYi(String name, int age) {
        this.name = name;
        this.age = age;
    }

    public String getName() {
        return name;
    }

    public void setName(String name) {
        this.name = name;
    }

    public int getAge() {
        return age;
    }

    public void setAge(int age) {
        this.age = age;
    }

    @Override
    public String toString() {
        return "ZiDingYi{" +
                "name='" + name + '\'' +
                ", age=" + age +
                '}';
    }
}
//////////////////////////////////////////
public class ZiDiYiMain {
    public static void main(String[] args) {
        ArrayList<ZiDingYi> zdy=new ArrayList<>();
        zdy.add(new ZiDingYi("小米",12));
        zdy.add(new ZiDingYi("小红",20));
        zdy.add(new ZiDingYi("小名",17));
        Collections.sort(zdy, new Comparator<ZiDingYi>() {//注意格式
            @Override
            public int compare(ZiDingYi t1, ZiDingYi t2) {
                return t1.getAge()-t2.getAge();
            }
        });
        System.out.println(zdy);
    }
}
```

**注意：** return  t1.get-t2.get：升序  反之降序(自定义类private修饰，所以get)

```java 
public class ZiDiYiMain {
    public static void main(String[] args) {
        ArrayList<Integer> list=new ArrayList<>();
        Collections.addAll(list,34,12,77,3,9,88);
        System.out.println(list);
        Collections.sort(list, new Comparator<Integer>() {
            @Override
            public int compare(Integer integer, Integer t1) {
                return t1-integer;//非自定义所有类,直接-
            }
        });
        System.out.println(list);//[88, 77, 34, 12, 9, 3]
    }
}
```

### Map<k,v>接口

Map集合的特点：

1、Map集合是一个双列集合，一个元素包含两个值（一个key,一个value；(键和值)）

2、Map集合中的元素，key和value的值可以相同，可以不同

3、Map集合中的元素，key不允许重复，value可以重复

4、Map集合中的元素，key和value一一对应

#### HashMap集合

java.util.HashMap<k,v> 集合 implements  Map<k,v> 接口

HashMap集合特点：

1、底层为哈希表，查询速度特别快

2、无序集合，储存元素顺序与取出顺序可能不一致

#### Map接口常用方法

```java 
//1、put(k,v);方法  添加指定键与指定值添加到Map集合中
HashMap<String,Integer> map=new HashMap<>();
map.put("西安",1234);
map.put("西安",666);
map.put("荔波",666);
map.put("南京",12384);
System.out.println(map);
//{西安=666, 荔波=666, 南京=12384}
//键值重复则取后一个键对应的value值

//2、remove(k);方法 把指定键对应的键值对在Map集合中删除，返回被删除元素的值；返回值：value
//key存在，v返回被删除的值，key不存在返回null
        Integer n = map.remove("南京");
        System.out.println(n);//12384
        System.out.println(map);//{西安=666, 荔波=666}

//3、get(k)方法  通过指定键值，在Map集合中获取对应值
		Integer li = map.get("荔波");
        System.out.println("li:"+li);//li:666

//4、containsKey(k);方法  判断集合是否包含指定键
//有返回true,无则返回false
```

**遍历Map集合**

1、通过keySet()方法将key键转换到Set集合中储存；再通过foreach循环或者iterator迭代器遍历键，在遍历中Map集合调用get()方法取值

（map.values()   返回一个Collection<> 集合  里面存值 ）

```Java
public static void main(String[] args) {
    HashMap<String,Integer> map=new HashMap<>();
    map.put("西安",1234);
    map.put("西安",666);
    map.put("荔波",666);
    map.put("南京",12384);
    map.put("上海",777);
    map.put("广东",999);
    Set<String> set = map.keySet();
    for (String s:set) {
        Integer num = map.get(s);
        System.out.println(num);
    }
    /*Iterator<String> it = str.iterator();
    while (it.hasNext()){
        String s = it.next();
        Integer num = map.get(s);
        System.out.println(num);
    }*/
}
```

**Entry键值对象**

![](C:\Users\panqiyi\Desktop\notes\image\22.png)

2、使用Entry键值对象遍历

​		1、使用Map集合中的方法entrySet()，把Map集合中多个Entry对象取出来，储存到一个Set集合中

​		2、遍历Set集合，获取每一个Entry对象

​		3、使用Entry对象中的方法getkey()和getvalue()获取键与值

```Java
public static void main(String[] args) {
    Map<String,Integer> map=new HashMap<>();
    map.put("迪丽热巴",168);
    map.put("林允儿",166);
    map.put("周杰伦",172);
    Set<Map.Entry<String, Integer>> set = map.entrySet();
    for (Map.Entry<String,Integer> entry:set) {
        String key = entry.getKey();
        Integer value = entry.getValue();
        System.out.println(key+"="+value);
    }
    /*Iterator<Map.Entry<String, Integer>> iterator = set.iterator();
    while (iterator.hasNext()){
        Map.Entry<String, Integer> next = iterator.next();
        String key = next.getKey();
        Integer value = next.getValue();
        System.out.println(key+"="+value);
    }*/  //迭代器遍历
```

**Map储存自定义类**

1、自定义类作为key时，保证key是唯一则 自定义类需要重写hashCode()和equals方法

2、自定义类作为value时不用重写(重写也没用)，value元素可以重复

```Java
public class Person {
    private String name;
    private int age;
    ……构造/get/set/重写toString
        //没有重写hashCode()和equals
///////////////////////////////////////////////////////
public static void main(String[] args) {
    Map<Person,String> map=new HashMap<>();
    map.put(new Person("特朗普",45),"美国");
    map.put(new Person("普京",60),"俄罗斯");
    map.put(new Person("特朗普",45),"香蕉");
    Set<Map.Entry<Person, String>> set = map.entrySet();
    for (Map.Entry<Person,String> entry:set ) {
        Person key = entry.getKey();
        String value = entry.getValue();
        System.out.println(key+"="+value);
    }
}
Person{name='特朗普', age=45}=香蕉
Person{name='普京', age=60}=俄罗斯
Person{name='特朗普', age=45}=美国
    ////////////////////////////////////////////////
    //Person类重写hashCode()和equals后
    Person{name='普京', age=60}=俄罗斯
    Person{name='特朗普', age=45}=香蕉
```

#### LinkedHashMap

java.util.LinkedHashMap<k,v>集合  extends   HashMap<k,v>

1、底层是哈希表+链表(保证迭代顺序)

2、有序集合，储存元素与取出元素顺序一致

#### Hashtable

单线程，线程安全，速度慢，被HashMap取代

HashMap等之前的所有集合都能储存null值 或者null键和null值

而Hashtable不能储存null键，null值

Hashtable的子类properties集合是唯一和IO流相结合的集合

**计算字符串每个字母个数**

```Java
public static void main(String[] args) {
    Scanner sc=new Scanner(System.in);
    System.out.println("请输入一个字符串：");
    String str = sc.next();
    Map<Character,Integer> map=new HashMap<>();
    for (char n:str.toCharArray()) {//字符数组
        if (map.containsKey(n)){
            Integer value = map.get(n);
            value++;
            map.put(n,value);
        }else {
            map.put(n,1);
        }
    }
    System.out.println(map);
    for (Character key:map.keySet()) {//Set集合，所以是包装类
        Integer value = map.get(key);
        System.out.println(key+"="+value);
    }//遍历
}
```

#### jdk9新特性

List,Set,Map接口里面增加了一个静态方法of，可以给集合一次性添加多个元素，

使用前提：

1、储存元素后，集合不能改变，使用of后不能再使用add或者put

2、of方法只能适用于LIst,Set,Map接口，不适用于他们的实现类，如ArrayLIst、HashMap、

3、Set 接口和Map接口在调用of静态方法时，不能有重复元素

### Debug调试

![](C:\Users\panqiyi\Desktop\notes\image\23.png)

### 斗地主增强版

```java
public class DdzMap {
    /*
    * 斗地主综合案例
    * 1、准备牌
    * 2、洗牌
    * 3、发牌
    * 4、排序
    * 5、看牌*/
    public static void main(String[] args) {
        //1、准备牌
        //创建Map集合，储存索引和组装好的牌
        HashMap<Integer,String> poker=new HashMap<>();
        //创建List集合储存索引
        ArrayList<Integer> pokerIndex=new ArrayList<>();
        //创建两个集合，储存花色和牌的序号
        List<String> colors = List.of("♠", "♥", "♠", "♦");
        List<String> numbers = List.of("2", "A", "K", "Q", "J", "10", "9", "8", "7", "6", "5", "4", "3");
        //储存大王小王到集合
        //定义一个牌索引
        int index=0;
        poker.put(index,"大王");
        pokerIndex.add(index);
        index++;
        poker.put(index,"小王");
        pokerIndex.add(index);
        index++;
        //循环嵌套组装52张牌
        for (String number:numbers) {
            for (String color : colors) {
                poker.put(index,color+number);
                pokerIndex.add(index);
                index++;
            }
        }
        System.out.println(pokerIndex);
        System.out.println(poker);
        //洗牌
        Collections.shuffle(pokerIndex);
        //发牌  定义4个集合 储存玩家牌索引 3玩家1底牌
        ArrayList<Integer> play1=new ArrayList<>();
        ArrayList<Integer> play2=new ArrayList<>();
        ArrayList<Integer> play3=new ArrayList<>();
        ArrayList<Integer> dipai=new ArrayList<>();
        //遍历储存牌索引List集合  获取每一个牌的索引
        for (int i = 0; i < pokerIndex.size(); i++) {
            Integer in = pokerIndex.get(i);
            if (i>=51){//底牌
                dipai.add(in);
            }else if (i%3==0){
                play1.add(in);
            }else if (i%3==1){
                play2.add(in);
            }else if (i%3==2){
                play3.add(in);
            }
        }
        //排序
        Collections.sort(play1);
        Collections.sort(play2);
        Collections.sort(play3);
        Collections.sort(dipai);
        //看牌
        lookpoker("刘德华",poker,play1);
        lookpoker("周润发",poker,play2);
        lookpoker("周星驰",poker,play3);
        lookpoker("底牌",poker,dipai);
    }
    public static void lookpoker(String name,HashMap<Integer,String> poker,ArrayList<Integer> list){
        System.out.print(name+":");
        for (Integer key:list) {
            String value = poker.get(key);
            System.out.print(value+" ");
        }
        System.out.println();
    }
}
```

### 异常

异常的根类是java.lang.Throwable；它有两个子类：

java.lang.Error(错误) 和java.lang.Exception(即异常)

Error：严重错误，无法处理，只能避免

Exception：异常；可以通过代码纠正，使程序正常运行，是必须要处理的

![](C:\Users\panqiyi\Desktop\notes\image\24.png)

**异常分类**

Exception：编译期异常，编译(写代码时)程序出现异常

RuntimeException：运行期异常，程序运行过程中出现异常

**异常产生原理**

![](C:\Users\panqiyi\Desktop\notes\image\25.png)

#### 处理异常

##### throw抛出

使用throw关键字在指定方法中抛出指定的异常

```java 
//使用格式：throw new xxxException("异常产生的原因");
//注意：
/*1、throw关键字必须写在方法内部
2、throw关键字后边new的对象必须是Exception或者是Exception的子类
3、throw关键字抛出指定异常对象，我们需处理该异常：
	3.1：throw关键字后创建的是RuntimeException或者是其子类，我们可以不用处理，默认交给JVM处理(打印异常对象,中断程序)
	3.2：throw关键字后创建的是编译异常，我们就必须要处理：throws或者try...catch
*/
运行期异常：不用处理
    public static void main(String[] args) {
        int[] arr=new int[3];
        int moth = moth(arr, 3);
    }
    public static int moth(int[] arr,int index){
        if (index<0||index>arr.length-1) {//合法判断
            throw new ArrayIndexOutOfBoundsException("输入索引不在数组索引范围");
        }
        int i = arr[index];
        return i;
    }
```

判断对象是否为空：

Objects类型有静态方法requireNonNull() 可判断对象是否为空；如果为空则抛出空指针异常

```java 
public class ThrowNull {
    public static void main(String[] args) {
        method(12);
    }
    public static void method(Object obj){
        /*if (obj==null){
            throw new NullPointerException("对象为空");
        }*/
//        Objects.requireNonNull(obj);//无字符串提示
        Objects.requireNonNull(obj,"对象为空");//有字符串提示
    }
}
```

##### throws声明处理

1、throws关键字必须写在方法声明处；

2、throws关键字后声明的异常必须是Exception或者是其子类

3、方法内部如果抛出多个异常对象，那么throws后也声明多个异常，如果多个异常间有子父类关系，那就只需声明父类异常

4、调用一个throws声明异常的方法，调用者也需声明异常，最终交给jvm

```java
public class ThrowsMain {
    public static void main(String[] args) throws FileAlreadyExistsException{
        file("c:\\f.txt");
    }
    private static void file(String file) throws FileAlreadyExistsException{
        if (!file.equals("c:\\d.txt")){
            throw new FileAlreadyExistsException("文件路径不对");//编译异常，声明处理
            System.out.println("路径正确，正在读取");
        }
    }
}
```

处理缺陷：最终交给虚拟机，中断处理，无法再执行后续代码

##### try...catch 捕获异常

自己处理异常；可执行异常后续代码

```java 
//格式:
try{
    //可能产生异常的代码
}catch(定义一个异常变量，接收try中抛出的异常对象){
    异常处理逻辑，如何处理异常，工作一般把异常消息记录到日志中
}
...catch 可以有多个
    catch(异常类名 变量名){}
//注意：
1、当try抛出多个异常时，那么就使用多个catch来处理
2、try出现异常则执行catch异常处理逻辑，再执行后续代码
    try没有出现异常则直接执行后续代码，不会执行catch
    //////////////////////////////////////////
    public static void main(String[] args){
        try {
            file("c:\\f.txt");//异常代码
        }catch (FileAlreadyExistsException e){//传入异常对象，类名即出现异常类
            System.out.println("传递文件路径不正确");
        }
        System.out.println("后续代码");
    }
    private static void file(String file) throws FileAlreadyExistsException{
        if (!file.equals("c:\\d.txt")){
            throw new FileAlreadyExistsException("文件路径不对");
        }
    }
/*传递文件路径不正确
  后续代码*/
```

**Throwable3种异常处理**

```java
/*
1、getMessage();返回此throwable的简短描述
2、toString();返回throwable详细信息字符串
3、printStackTrace(); jvm打印异常对象，打印信息最全面*/
////////////////////////////////////////////
public static void main(String[] args){
        try {
            file("c:\\f.txt");//异常代码
        }catch (FileAlreadyExistsException e){//传入异常对象，类名即出现异常类
            System.out.println(e.getMessage());
            // 文件路径不对
            System.out.println(e.toString());//与直接打印e一样
            // java.nio.file.FileAlreadyExistsException: 文件路径不对
            e.printStackTrace();//注意格式
            //java.nio.file.FileAlreadyExistsException: 文件路径不对
            //	at exception.ThrowsMain.file(ThrowsMain.java:19)
            //	at exception.ThrowsMain.main(ThrowsMain.java:8)
        }
        System.out.println("后续代码");
    }

    private static void file(String file) throws FileAlreadyExistsException{
        if (!file.equals("c:\\d.txt")){
            throw new FileAlreadyExistsException("文件路径不对");
        }
    }
```

##### finally代码块

```
//格式：
try(){
	异常代码
}catch(异常类 变量){
	异常处理逻辑
}finally{
	无论出现异常与否都会执行
}
//1、finally不能单独使用，必须和try一起使用
//2、finally一般用于资源释放(资源回收)，无论出现是否出现异常最后都要释放(IO流会讲)
```

**注意：**

如果finally有return 语句，则永远返回finally 中的语句，避免该情况

```Java
public static void main(String[] args) {
    int a = getA();
    System.out.println(a);//100
}
public static int getA(){
    int a=10;
    try {
        return a;
    }catch (Exception e){
        System.out.println(e);
    }finally {
         a=100;
        return a;
    }
}
```

##### 多异常捕获

```Java
//1、多个异常分别捕获分别处理
try{
	异常代码1
}catch(异常类1 变量1){
	处理逻辑1
}
try{
	异常代码2
}catch(异常类2 变量2){
	处理逻辑2
}

//2、一次捕获多次处理
//注意：当多个异常类之间有子父类关系，catch应该从上到下先写子类，否则报错
try{
	异常代码1
	异常代码2
}catch(异常类1 变量1){
	逻辑处理1
}catch(异常类2 变量2){
	逻辑处理2
}

//3、一次捕获,一次处理
//多个异常类存在子类继承关系时，catch可以只用写父类
try{
	异常代码1
	异常代码2
}catch(异常父类 变量){
	逻辑处理
}
```

**注意：**

子类重写父类方法；子类抛出与父类相同异常(或者父类异常的子类)或者不抛出异常；

父类方法无异常时，子类重写不可抛出异常，子类产生异常，只能捕获处理，不能声明抛出；

##### 自定义异常类

```Java
格式：
public class xxxException extends Exception/RuntimeException{
	添加一个无参构造方法
	添加一个带异常信息的构造方法
}
/*自定义类继承Exception(编译异常)时抛出异常需要处理，要么throws声明，要么try..catch()捕获*/
///自定义一个异常类
public class RegisterException extends Exception {
    public RegisterException(){//定义一个空参构造
        super();
    }
    public RegisterException(String message){//定义一个带异常信息的构造方法
        super(message);
    }
}
////////////////使用该异常类
public static void main(String[] args) /*throws RegisterException*/ {                    
    ArrayList<String> list=new ArrayList<>();                                            
    Collections.addAll(list,"张三","李四","王五");                                             
    Scanner sc=new Scanner(System.in);                                                   
    System.out.println("请输入姓名：");                                                        
    String name = sc.next();                                                             
    checkName(name,list);                                                                
}                                                                                        
public static void checkName(String name,ArrayList list) /*throws RegisterException*/ {  
    for (Object o : list) {                                                              
        if (o.equals(name)){                                                             
            try {                                                                        
                throw new RegisterException("该用户名已被注册！");                                
            } catch (RegisterException e) {                                              
                System.out.println(e.getMessage());                                      
                return; //结束程序                                                                 
            }                                               
        }                                                                                
    }                                                                                    
    System.out.println("注册成功");                                                          
}                                                                                        
```

### 多线程

#### 并发与并行

并发：指两个或多个事件在**同一时间段**发生; **交替执行**

并行：指两个或多个事件在**同一时刻**发生；**同时执行**

#### 进程与线程

进程：在内存中运行的应用程序

线程：线程是进程的一个执行单元，负责进程中程序的执行

![](C:\Users\panqiyi\Desktop\notes\image\26.png)

**线程调度**

分时调度：所有线程轮流使用cpu，平均分配每个线程占用cpu的时间

抢占式调度：优先让优先级高的线程使用cpu，优先级相同则随机选择一个，Java 使用的是抢占式调度

**主线程**

执行main方法的线程；单线程Java程序，从上到下依次执行

(jvm执行main()方法,main()方法进入内存，jvm从操作系统开辟一条main()方法通向cpu的执行路径，cpu通过此路径执行main方法；此路径即为主(main)线程)

#### 多线程创建

方式一：

```Java
/*1、创建一个继承Thread类的子类
2、子类重写Thread父类的run方法，设置线程任务
3、main中创建子类对象
4、调用Thread类的start方法，开启新线程，执行run方法
	start()使该线程执行，jvm调用该线程run方法
	结果(main)线程与新线程(执行run方法)并发运行
	多次启动一个线程是非法的，线程结束不能重新启动
	Java程序属于抢占式调度，线程优先级高的先执行；同一优先级随机选择一个执行；这里main与run方法就是同级别*/
///////////////////////////////////////////////////
//创建一个线程
public class ThreadMain extends Thread {
    @Override
    public void run() {
        for (int i = 0; i < 20; i++) {
            System.out.println("run"+i);
        }
    }
}
//启动该线程
public static void main(String[] args) {
        ThreadMain thread=new ThreadMain();
        thread.start();//启动
        for (int i = 0; i < 20; i++) {//main线程
            System.out.println("num"+i);
        }
    }
	
```

**多线程内存图解**

![](C:\Users\panqiyi\Desktop\notes\image\27.png)

每调用一次start()方法会开辟新的栈空间，cpu会随机执行每个栈的方法

#### 获取/设置线程名称

1、使用Thread类中getName()方法返回该线程名称

2、Thread类静态方法currentThread()获取当前执行线程，返回对象引用

再使用getName()方法获取线程名称

```Java
public class ThreadMe extends Thread{
    @Override
    public void run() {

//        String name = getName();//1
//        System.out.println(name);
        
//        Thread t = Thread.currentThread();//2
//        System.out.println(t);
//        String name = t.getName();
//        System.out.println(name);
        
        System.out.println(Thread.currentThread().getName());//3
        //3为链式编程
    }
}
///////////////////
public class ThreadMain {
    public static void main(String[] args) {
        ThreadMe th=new ThreadMe();
        th.start();
        System.out.println("主线程");
        new ThreadMe().start();
        new ThreadMe().start();
    }
}
```

**设置线程名称**

```java
1、Thread直接在new构造方法时传入线程名(在Thread子类创建构造方法)
 public ThreadMe(String name) {//带参构造方法
        super(name);//调用父类带参构造方法
    } 
    ThreadMe tm=new ThreadMe("线程名");
    // 也可以使用setName()设置
2、Runnable时使用setName()设置线程名：
	JslTest03 js = new JslTest03(); //共享资源,实现Runnable
        Thread t1 = new Thread(js);//创建线程
        Thread t2 = new Thread(js);
   
        t1.setName("电影院"); //设置线程名
        t1.start();
```

1、使用Thread类中setName(名称)方法

2、在Thread子类中创建一个带参的构造方法，传递线程名称，调用父类带参构造方法，传递线程名称给父类

```Java
public class ThreadMe extends Thread{
    public ThreadMe() {}
    public ThreadMe(String name) {//带参构造方法
        super(name);//调用父类带参构造方法
    }
    @Override
    public void run() {
        System.out.println(Thread.currentThread().getName());
    }
}
//////////////////////
public class ThreadMain {
    public static void main(String[] args) {
        ThreadMe th=new ThreadMe();
        th.setName("多线程名称1");//线程名称设置1
        th.start();
        System.out.println("主线程");
        new ThreadMe("二号").start();//设置2
    }
}
```

#### 静态方法sleep()

使当前执行线程以指定的毫秒数暂停，毫秒数结束后线程继续执行

```java
public static void main(String[] args) {
    for (int i = 0; i <=60; i++) {
        System.out.println(i);
        try {
            Thread.sleep(1000);//暂停一秒
        } catch (InterruptedException e) {
            e.printStackTrace();
        }
    }//出现异常  alt+回车 选择try/catch
}
```

#### 实现Runnable接口创建多线程

1、创建Runnable接口实现类

2、在实现类重写Runnable接口run方法，设置线程任务

3、在main方法中创建Runnable接口实现类对象

4、创建Thread类对象，构造方法中传递Runnable接口实现类对象

5、Thread类对象调用start方法，开启多线程执行run方法

```Java
public class MyThread2 implements Runnable {
    @Override
    public void run() {
        for (int i = 0; i < 30; i++) {         System.out.println(Thread.currentThread().getName()+i);
            try {
                Thread.sleep(500);
            } catch (InterruptedException e) {
                e.printStackTrace();
            }
        }
    }
}
////////////////////
public class ThreadMain2 {
    public static void main(String[] args) {
        MyThread2 tm=new MyThread2();
        Thread td=new Thread(tm);
        td.start();
    }
}

```

**使用Runnable接口创建多线程的好处**

1、避免了单继承的局限性

一个类只能继承一个类，类继承了Thread类就不能继承其他的类

实现Runnable接口，还可以继承其他的类，实现其他接口

2、增强程序扩展性，降低程序耦合性

实现Runnable接口，把设置线程任务和开启新线程分离

创建Thread对象时，传入其构造方法的Runnable实现类对象不同，调用start()方法启动的新线程就不同；

**匿名内部类实现线程的创建**

```Java
public static void main(String[] args) {
    new Thread(){
        @Override
        public void run() {
            for (int i = 0; i < 6; i++) {
                System.out.println("内部类"+i);
            }
        }
    }.start();
    Runnable r=new Runnable(){
        @Override
        public void run() {
            for (int i = 0; i < 6; i++) {
                System.out.println("内部接口"+i);
            }
        }
    };
    // Thread(r).start();  可以简化为下面直接一步
    new Thread(new Runnable(){
        @Override
        public void run() {
            for (int i = 0; i < 6; i++) {
                System.out.println("内部接口"+i);
            }
        }
    }).start();
}
```

#### 线程安全问题

多个线程访问了共享的数据会产生线程安全问题

![](C:\Users\panqiyi\Desktop\notes\image\29.png)

**线程安全问题代码**

```Java
public class Thread3 implements Runnable{
    private int num=100;

    @Override
    public void run() {
        for (;;){
        if (num>0){
            System.out.println(Thread.currentThread().getName()+"-->"+num);
            num--;
        }
        }
    }
}
///////////////////////
public static void main(String[] args) {
        Thread3 thread3=new Thread3();//创建Runnable实现类对象
        Thread thread=new Thread(thread3);//两个线程共享一份任务，传入相同对象
        Thread p=new Thread(thread3);
        thread.start();//启动线程1
        p.start();//启动线程2
    }
}
//打印结果有出现重复或者超范围数据，出现线程安全问题
```

#### 解决线程安全

**方法一：同步代码块**

```Java
/*
* 线程安全解决方案一：使用同步代码块
* synchronized(锁对象){
*     可能会出现线程安全问题的代码（多个线程共享同一任务的代码）
* }
* 注意：
* 1、锁对象可以是任何对象
* 2、保证多个线程使用的锁对象是同一个
* 3、锁对象的作用：把同步代码块锁住，只允许一个线程在同步代码块中执行*/
public class Thread3 implements Runnable{
    private int num=100;
    Object obj=new Object();

    @Override
    public void run() {
            for (; ; ) {
                synchronized (obj) {//同步代码块
                    if (num > 0) {                       System.out.println(Thread.currentThread().getName() + "-->" + num);
                        num--;
                    }}}}}
/////////////////////////
public static void main(String[] args) {
        Thread3 thread3=new Thread3();//创建Runnable实现类对象
        Thread t1=new Thread(thread3);//两个线程共享一份任务，传入相同对象
        Thread t2=new Thread(thread3);
        Thread t3=new Thread(thread3);
        t1.start();//启动线程1
        t2.start();//启动线程2
        t3.start();//启动线程3
    }
```

 <img src="C:\Users\panqiyi\Desktop\notes\image\30.png"  />

同步保证了只能有一个线程在同步中执行共享数据，保证了安全；

程序会频繁的判断锁，获取锁，释放锁，程序的效率会降低

**方法二：同步方法**

```Java
/*
* 1、把访问了共享数据的代码抽取出来，放到一个方法中
* 2、在方法上添加synchronized修饰符
* 同步方法也将方法内部代码锁住，只让一个线程执行
* 同步方法的锁对象是  new  Thread5();  也就是this
* */
public class Thread5 implements Runnable {
    private int num=100;
    public synchronized void syn(){//同步方法
            if (num > 0) {
                try {//提高程序安全问题出现的概率，让程序睡眠
                    Thread.sleep(100);
                } catch (InterruptedException e) {
                    e.printStackTrace();
                }
                System.out.println(Thread.currentThread().getName() + "-->" + num);
                num--;
            }
    }
    @Override
    public void run() {
        for (;;) {
            syn();
        }}}
        ////////////////////////////
 public static void main(String[] args) {
        Thread5 thread5=new Thread5();
        Thread t1=new Thread(thread5);
        Thread t2=new Thread(thread5);
        Thread t3=new Thread(thread5);
        Thread t4=new Thread(thread5);
        t1.start();
        t2.start();
        t3.start();
        t4.start();
    }//结果未出现线程安全问题
```

静态同步方法的锁对象是    本实现类.class

本类的class属性 -->class文件对象(反射会讲)

**方法三：使用Lock锁**

```Java
/*
* Lock比synchronized代码块和方法有更广泛的锁定操作
* Lock接口的方法： void lock() 获取锁   void unlock() 释放锁
* 1、创建ReentrantLock对象
* 2、在可能出现安全问题代码前调用lock方法获取锁
* 3、在可能出现安全问题代码后调用unlock方法释放锁
注意：只能用ReentrantLock对象调用
* 一般使用 try/finally语句块
*     try{
*          l.lock();
*          共享代码块
*        }finally{
*         l.unlock()   //保证都会释放锁
* }*/
public class Thread6 implements Runnable{
    private int num=100;
    Lock l=new ReentrantLock(); //Lock为接口，不能直接创建对象
    @Override
    public void run() {
        for (;;){
            try {//
                l.lock();//获取锁
                if (num>0){
                    try {
                        Thread.sleep(50);
                    } catch (InterruptedException e) {
                        e.printStackTrace();
                    }                  System.out.println(Thread.currentThread().getName()+"-->"+num);
                    num--;
                }
            }finally {//
                l.unlock();//释放锁
            }
}}}
////////////////////////////////
 public static void main(String[] args) {
        Thread6 thread6=new Thread6();
        Thread t0=new Thread(thread6);
        Thread t1=new Thread(thread6);
        Thread t2=new Thread(thread6);
        t0.start();
        t1.start();
        t2.start();
    }//未出现线程安全问题
```

#### 线程状态

![](C:\Users\panqiyi\Desktop\notes\image\31.png)

![](C:\Users\panqiyi\Desktop\notes\image\32.png)

![](C:\Users\panqiyi\Desktop\notes\image\33.png)

#### 等待唤醒(线程通信)

也叫**生产者消费者模式**

![](C:\Users\panqiyi\Desktop\notes\image\34.png)

**wait和notify**

```Java
/*创建一个消费者线程：调用wait方法，放弃cpu的执行，进入到 WAITING(无限等待); 【wait()方法内未传值则无限等待】
创建一个生产者线程：设置休眠时间，任务完成后，调用notify方法，唤醒生产者单个线程
注意：
 消费者生产者线程都必须使用同步代码块包裹起来，保证等待和唤醒只能有一个在执行
  同步使用锁对象必须唯一，只有锁对象才能调用wait和notify方法
  唤醒后继续执行wait()之后的代码
* */
public class Thread7Main {
    public static void main(String[] args) {
        //创建锁对象，保证唯一
        Object obj=new Object();
        //创建一个消费者线程
        new Thread(){
            @Override
            public void run() {
                synchronized (obj) {//同步代码块
                    System.out.println("我要吃包子！");
                    try {
                        obj.wait();//使当前线程等待
                    } catch (InterruptedException e) {
                        e.printStackTrace();
                    }
                }
                //唤醒后执行后面代码
                System.out.println("唤醒后代码");
            }
        }.start();
        //创建一个生产者线程
        new Thread(){
            @Override
            public void run() {
                    try {
                        Thread.sleep(5000);//花五秒做包子(睡眠5s)
                    } catch (InterruptedException e) {
                        e.printStackTrace();
                    }
                    synchronized (obj){
                        System.out.println("5秒后包子做好了，请你享用！");
                        obj.notify();//唤醒生产者单个线程
                    }
            }
        }.start();
    }
}
```

**进入到TimeWaiting(计时等待)有两种方式与唤醒方法**

```Java
/*计时等待：
* 1、使用sleep(long m)方法，在毫秒值结束后，线程睡醒后进入运行或阻塞状态
* 2、使用wait(long m)方法，如果毫秒值结束后还没有被notify唤醒则自动唤醒
*唤醒方法：
* void notify()  唤醒在此对象监视器上等待的单个线程(唤醒等待时间最长的线程)
* void notifyAll()  唤醒在此对象监视器上等待的所有线程
* */
public class Thread8 {
    public static void main(String[] args) {
        //创建锁对象，保证唯一
        Object obj=new Object();
        //创建一个消费者线程
        new Thread(){
            @Override
            public void run() {
                synchronized (obj) {//同步代码块
                    System.out.println("顾客1要吃包子！");
                    try {
                        obj.wait();//使当前线程等待
                    } catch (InterruptedException e) {
                        e.printStackTrace();
                    }
                }
                //唤醒后执行后面代码
                System.out.println("顾客1开吃");
            }
        }.start();
        //创建第二个消费者线程
        new Thread(){
            @Override
            public void run() {
                synchronized (obj) {//同步代码块
                    System.out.println("顾客2要吃包子！");
                    try {
                        obj.wait();//使当前线程等待
                    } catch (InterruptedException e) {
                        e.printStackTrace();
                    }
                }
                //唤醒后执行后面代码
                System.out.println("顾客2开吃");
            }
        }.start();
        //创建一个生产者线程
        new Thread(){
            @Override
            public void run() {
                try {
                    Thread.sleep(5000);//花五秒做包子(睡眠5s)
                } catch (InterruptedException e) {
                    e.printStackTrace();
                }
                synchronized (obj){
                    System.out.println("5秒后包子做好了，请你享用！");
                    obj.notifyAll();//唤醒所有等待线程
                }
            }
        }.start();
    }
}
```

#### 线程通信

多个线程在处理同一个资源，但处理的动作(线程任务)不同

如：线程A生产包子，线程B吃包子，包子可以理解为同一资源

**为什么要处理线程间的通信**

多个线程并发的执行时，默认情况cpu会随机选择线程，当我们希望多个线程有规律的执行时，那多个线程间就需要协调通信；

即等待唤醒机制；

#### 等待唤醒机制

wait(): 让线程进入等待

notify(): 唤醒在此对象监视器上等待的单个线程

notifyAll(): 唤醒在此对象监视器上等待的所有线程

等待与唤醒方法都是用同一个对象调用，因为唤醒是唤醒同一个对象监视器上等待的线程。对象可以是任何对象，而任何对象都是继承了Object类；

wait()与notify()方法都是必须要放在同步代码块、或同步函数中使用；因为要通过获得锁对象来调用；

**案例**

![](C:\Users\panqiyi\Desktop\notes\image\35.png)

**1、创建包子类**

```Java
/*
* 设置包子类*/
public class Thread9bz {
    String pi;//皮
    String xian;//陷
    boolean bz=false;//设置初始值为false没有包子
 }
```

**2、创建店铺线程**

```Java
public class Thread9dp extends Thread {
    private Thread9bz baozi;//创建包子类变量

    public Thread9dp(Thread9bz baozi) {//带参构造给变量赋值
        this.baozi = baozi;
    }
    @Override
    public void run() {
        int i=0;
        while (true){
            //使用同步技术保证只有一个线程执行
            synchronized (baozi){
                //对包子状态判断
                if (baozi.bz==true){//有包子则不需要做，进入等待
                    try {
                        baozi.wait();
                    } catch (InterruptedException e) {
                        e.printStackTrace();
                    }
                }
                //被唤醒后继续执行wait后代码，包子铺生产包子
                if (i%2==0){
                    //生产白皮，肉馅包子
                    baozi.pi="白皮";
                    baozi.xian="肉馅";
                }else {
                    //生产黄皮，菜馅
                    baozi.pi="黄皮";
                    baozi.xian="菜馅";
                }
                i++;
                System.out.println("包子铺真正生产"+baozi.pi+baozi.xian+"包子");
                //包子生产需要时间，设置睡眠
                try {
                    Thread.sleep(3000);
                } catch (InterruptedException e) {
                    e.printStackTrace();
                }
                //包子生产好了，该包子状态为true
                baozi.bz=true;
                //唤醒吃货线程，让吃货吃包子
                baozi.notify();
                System.out.println("包子做好了,是"+baozi.pi+baozi.xian+"可以开吃！");
            }
        }}}
```

**3、创建吃货线程**

```Java
public class Thread9ch extends Thread {
    private Thread9bz baozi;

    public Thread9ch(Thread9bz baozi) {
        this.baozi = baozi;
    }

    @Override
    public void run() {
        while (true){//一直吃包子
            synchronized (baozi){
                //判断包子状态
                if (baozi.bz==false){
                    //false无包子
                    try {
                        baozi.wait();
                    } catch (InterruptedException e) {
                        e.printStackTrace();
                    }
                }
                //唤醒后吃货吃包子
                System.out.println("吃货在吃"+baozi.pi+baozi.xian+"包子");
                //吃完包子修改包子状态false
                baozi.bz=false;
                //唤醒包子铺线程，生产包子
                baozi.notify();
                System.out.println("吃货吃完"+baozi.pi+baozi.xian+"包子,开始生产包子");
                System.out.println("---------------------------------");
            }
        }}}
```

**测试类main方法**

```Java
/*
* 1、创建包子对象
* 2、创建包子铺和吃货线程传入包子对象*/
public class Thread9Main {
    public static void main(String[] args) {
        Thread9bz b=new Thread9bz();
        new Thread9dp(b).start();//传入包子对象并开启线程；
        new Thread9ch(b).start();
    }
}
```

#### 线程池

jdk1.5后提供；

就是一个容纳多个线程的容器，其中的线程可以反复使用，省去了频繁创建线程对象的操作，无需反复创建线程而消耗过多的资源。

![](C:\Users\panqiyi\Desktop\notes\image\36.png)

合理利用线程池的好处：

1、降低资源消耗，减少创建和销毁线程，每个工作线程可以被重复利用，可执行多个任务。

2、提高响应速度，当任务达到时，任务无需等到线程创建就能立即执行。

3、提高线程的可管理性，根据系统承受能力，调整线程池中线程数目（每个线程大约1MB内存）；

```Java
/*
* java.util.concurrent.Executors
* Executors类中的静态方法：
* static ExecutorService newFixedThreadPool(int nThreads) 创建一个可重用固定线程数的线程池
* 参数：int nThreads   创建线程池中包含的数量
* 返回值：
* ExecutorService接口实现类对象，可以用ExecutorService接口接受(面向接口编程)
*ExecutorService线程池接口，用来从线程池中获取线程，调用start方法，执行线程任务；
* submit(Runnable task)  提交一个Runnable任务用于执行
*shutdown()  关闭/销毁线程池
* 线程池的使用步骤：
* 1、使用线程池工厂类Executors里边提供的静态方法newFixedThreadPool()生产一个指定数量的线程池
* 2、创建一个实现Runnable接口的类，重写run方法，设置线程任务
* 3、调用ExecutorService接口中的submit()方法，传递线程任务，开启线程，执行run方法
* 4、调用ExecutorService接口中的shutdown()销毁线程池(不建议执行)
 */
public class Thread10 {
    public static void main(String[] args) {
        Thread10Run th=new Thread10Run();
        ExecutorService e = Executors.newFixedThreadPool(2);
        //线程池会一直开启，使用完了的线程，会自动归还线程池，可以继续使用
        e.submit(th);//th线程任务对象
        e.submit(th);
        e.submit(th);
        /*pool-1-thread-1 在线程池pool-1中，先执行线程thread1,然后thread1会自动归还
          pool-1-thread-2 thread1未归还到则先用thread2,然后thread2归还
          pool-1-thread-1  thread1已归还*/
        //以上结果不唯一，是多变的
    }
}
```

**结论**

之前启动多个线程时，每启动一个都要创建一次新的对象；

而线程池就相当于一个池子里面放着自定义个线程数，用了里边的线程，线程会自动归还线程池，可继续使用；

调用ExecutorService接口中的submit()方法，传递线程任务，开启线程，执行run方法

```Java
 ExecutorService e = Executors.newFixedThreadPool(2);
        e.submit(th);//开启第一个线程
        e.submit(th);//开启第二个线程 //th为Runnable实现类对象，即线程对象
```

**线程池未完待续……**

### Lambda表达式

Java8（jdk1.8）中的重量级新特性；

```Java
public class Lambda1 {
    public static void main(String[] args) {
        //匿名内部类实现多线程
        new Thread(new Runnable() {
            @Override
            public void run() {
                System.out.println(Thread.currentThread().getName());
            }
        }).start();
        //使用Lambdd表达式实现多线程
        new Thread(()-> {
            System.out.println(Thread.currentThread().getName());
        }).start();
        /* ()-> { //这里‘(参数)’表示run()方法，由于run无参；‘->’:表示将参数传给后面的语句；
            System.out.println(Thread.currentThread().getName());
        }*/
    }
}
```

**匿名内部类的好处与弊端**

好处：匿名内部类可以省去实现类的定义

弊端：匿名内部类语法太复杂；

**Lambda表达式的标准格式**

```Java
/*
* 有三部分组成：
    a:一些参数；
    b:一个箭头；
    c:一段代码；
 格式：
  (参数列表)->{一些重写的代码}

 解释格式说明：
  ():接口中抽象方法的参数列表，没有参数就空着；有参数就写出参数，多个用逗号隔开
  ->:传递的意思，把参数传递给方法体{}；
  {}:重写接口的抽象方法体；

* */
```

**无参无返回值**

```Java
//自定义一个Cook接口，定义一个无参无返回值抽象方法；
public interface Cook {
    void makefood();
}
///////////////////////////////////////////////
public class CookMain {
    public static void main(String[] args) {
      invokeCook(new Cook() {
          @Override
          public void makefood() {
              System.out.println("你好啊");
          }
      });
      //使用Lambda表达式简化匿名内部类；
        invokeCook(()->{
            System.out.println("nihaoya!");
        });
    }
    public static void invokeCook(Cook cook){
        cook.makefood();
    }
}
```

**有参有返回值**

```Java

public class Person {
    private String name;
    private int age;
}
//此类后面还有alt+ins添加  无、全参构造方法，get、set方法，toString方法；
//////////////////////////////////////////////
 public class PersonMain {
    public static void main(String[] args) {
        Person[] arr={//使用数组存储多个Person对象
                new Person("迪丽热巴",19),
                new Person("张靓颖",29),
                new Person("唐山",23),
                new Person("虎口",17)
        };
        //对数组的Person对象使用Arrays的sort()方法通过年龄进行升序(前-后)排序
        Arrays.sort(arr, new Comparator<Person>() {
            @Override
            public int compare(Person t1, Person t2) {
                return t1.getAge()-t2.getAge();
            }
        });
        //使用Lambda表达式简化匿名内部类；
        Arrays.sort(arr, (Person t1, Person t2)->  {
                return t1.getAge()-t2.getAge();
        });
        for (Person person : arr) {
            System.out.println(person);
        }}}  
```
**例2**

```Java
public interface Calculator {
    int calc(int a,int b);
}
```

```Java
public class CalcMain {
    public static void main(String[] args) {
        invokeCalc(new Calculator() {
            @Override
            public int calc(int a, int b) {
                return a+b;
            }
        },45,78);
        //使用Lambda表达式；
        invokeCalc((int a,int b)->{
            return a+b;
        },99,100);
    }
    public static void invokeCalc(Calculator calculator,int a,int b){
        int i = calculator.calc(a, b);
        System.out.println("相加结果："+i);
    }
}
```

**Lambda优化省略**

```Java
/*
* Lambda表达式：是可推导，可省略的
* 凡是根据上下文推导出来的内容都可以省略书写
* 可省略内容：
*   1、(参数列表)：括号中参数列表的数据类型，可以省略不写；
*   2、(参数列表)：括号中参数如果只有一个，那么类型和括号都可以省略；
*   3、{一些代码}：如果{}中代码只有一行，无论是否有返回值，都可以省略（{},return,分号）
*       注意：要省略{}，return,分号 必须要一起省略*/

public static void main(String[] args) {
        invoke(new Calculator() {
            @Override
            public int calc(int a) {
                return a;
            }
        },999);
        //////////////Lambda表达式   2、
        invoke(a-> { return a; },999);}
    public static void invoke(Calculator calculator,int a){
        calculator.calc(a);
        System.out.println(a);
    }

/////////////////////////////   3、

invokeCook(()->{
            System.out.println("nihaoya!");
        });

invokeCook(()->System.out.println("nihaoya!"));

///////////////////////
public static void main(String[] args) {
        invokeCalc(new Calculator() {
            @Override
            public int calc(int a, int b) {
                return a+b;
            }
        },45,78);
        //使用Lambda表达式；
        invokeCalc(( a, b)->{//   1、
            return a+b;
        },99,100);
    }
    public static void invokeCalc(Calculator calculator,int a,int b){
        int i = calculator.calc(a, b);
        System.out.println("相加结果："+i);
    }
```

**Lambda的使用前提**

1、必须具有接口，且接口中有且仅有一个抽象方法；

注意：必须是函数式接口，抽象类是不行的

2、方法的参数或局部变量类型必须为Lambda对应接口类型，才能使用Lambda作为该接口的实例；

若接口中只有一个抽象方法的接口称为函数式接口l

 ### File类

```Java
/*
* java.io.File类
* 文件和目录路径名的抽象形式。
* Java把电脑中的文件和文件夹（目录）封装为一个File类，
* 我们可以使用File类对文件和文件夹进行操作
* 我们可以用File类中的方法:
*   创建文件/文件夹；
*   删除文件/文件夹；
*   判断文件/文件夹是否存在；
*   对文件夹进行遍历；
*   获取文件的大小；
*  File类是一个与系统无关的类，任何操作系统都可以使用这个类中的方法；
*
*   重点：记住三个单词：
*   file: 文件；
*   directory：文件夹/目录；
*   path：路径；*/
```



#### 两个静态成员变量

pathSeparator   路径分隔符  ；

separator     文件名称分隔符  \  

```Java
/*
* File类两个静态成员变量：
*   static String pathSeparator 与系统有关的路径分隔符，为了方便表示为一个字符串；
*   static char pathSeparatorChar  与系统有关的路径分隔符
*
*   static String separator 与系统有关的默认分割符，为了方便表示为一个字符串；
*   static char separatorCahr 与系统有关的默认名称分割符*/
操作路径：不能死写
	如：D:\XUEXI\JAVA
    应该为  "D:"+"File.separator"+"XUEXI"+"File.separator"+"JAVA"
public class File1 {
    public static void main(String[] args) {
        String p = File.pathSeparator;
        System.out.println(p);// ;  路径分隔符（如配置jdk环境变量时，每个变量用‘;’分隔）
        // 系统的路径分隔符不太一样   windows分号 ;  Linux冒号

        String s = File.separator;
        System.out.println(s);//  \  文件名称分隔符  windows反斜杠 \;  Linux正斜杠 /
    }
}
```

**绝对/相对路径**

绝对路径：完整的路径

​	如：D:\XUEXI\JAVA\IDEA\123.txt

相对路径：简化的路径（相当于此文件）

​	如：123.txt (省略项目根目录D:\XUEXI\JAVA\IDEA)

注意：

windows使用反斜杠，即转义字符，两个\\代表一个\

#### 构造方法 

```Java
/*【1】、通过给定的路径字符串名称转换为File类对象
* File(String pathname)
* 路径可以是 相对路径/绝对路径；
* 可以是存在的/不存在的路径；

【2】、File(String parent, String child) 从父路径名字符串和子路径名字符串创建新的 File实例。 
String parent：父路径；   String child：子路径 
好处： 父子路径可以单独书写，使用起来非常灵活，父子路径可以分别变化；

【3】、File(File parent, String child) 从父抽象路径名和子路径名字符串创建新的 File实例。 
File parent：File对象；   String child：子路径 
好处： 父子路径可以单独书写，使用起来非常灵活，父子路径可以分别变化；
       父路径是File类型，可以使用File方法对路径一些操作，再使用路径来创建对象；*/


public class File2 {
    public static void main(String[] args) {
        File f1 = new File("D:\\XUEXI\\JAVA\\jdk8\\123.txt");
        System.out.println(f1);//重写toString方法 没有输出对象地址  D:\XUEXI\JAVA\jdk8\123.txt
System.out.println(new File("s.txt"));//s.txt

        show02("C:\\","XUEXI\\JAVA");
        show02("D:\\","XUEXI\\JAVA");
        //父子可以分别改变路径，灵活修改

        show03();
    }
    public static void show02(String parent,String child){
        File f2 = new File(parent, child);
        System.out.println(f2);
    }
    public static void show03(){
        File parent= new File("E:\\");
        File f3 = new File(parent, "java\\idea");//parent对象可调用File类方法
        System.out.println(f3);//E:\java\idea
    }
}

```

#### 获取功能方法

```Java
/*
* [1]、getAbsolutePath()  返回File 绝对路径
* [2]、getPath()   将路径名转为字符串 是什么就是什么不变
* [3]、getName()   返回此File路径末尾文件/文件夹名称
* [4]、length()   返回此File路径表示文件大小 字节为单位(文件不能是文件夹)*/
public class File3 {
    public static void main(String[] args) {
        show01();
        show02();
        show03();
        show04();
    }

    private static void show04() {
        File f7 = new File("C:\\Users\\panqiyi\\Desktop\\notes\\image\\1.png");
        File f8 = new File("C:\\Users\\panqiyi\\Desktop\\notes\\image");
        long length1 = f8.length();
        System.out.println(length1);
        long length = f7.length();
        System.out.println(length);//138103
    }

    private static void show03() {
        File f5 = new File("D:\\PRoject\\ideaJAVA\\untitled");
        String n1 = f5.getName();
        System.out.println(n1);//untitled
    }

    private static void show02() {
        File f3 = new File("D:\\PRoject\\ideaJAVA\\untitled");
        String p1 = f3.getPath();
        System.out.println(p1);//D:\PRoject\ideaJAVA\untitled
        File f4 = new File("untitled");
        System.out.println(f4);//untitled
    }

    private static void show01() {
        File f1=new File("D:\\PRoject\\ideaJAVA\\untitled");
        String l1 = f1.getAbsolutePath();
        System.out.println(l1);//D:\PRoject\ideaJAVA\untitled
        File f2=new File("untitled");//D:\PRoject\ideaJAVA\untitled
        String l2 = f2.getAbsolutePath();
        System.out.println(l2);
    }
}
```

#### 判断功能方法

```Java
/*
* 【1】、boolean exists()  判断File表示的路径是否存在
*
* 【2】、boolean isDirectory()  判断File路径末尾是文件夹则true；文件则false；
* 【3】、boolean isFile()  判断File路径末尾是文件则true；文件夹则false；
* 路径存在才能判断路径是文件还是文件夹 ；如果路径不存在则都是false；
* 所以使用前先判断是否存在*/
public class File4 {
    public static void main(String[] args) {
        show01();
        show02();
    }

    private static void show02() {
        File f3 = new File("C:\\Users\\panqiyi\\Desktop\\notes");
        if (f3.exists()){
            System.out.println(f3.isDirectory());//true
            System.out.println(f3.isFile());//false
        }
    }

    private static void show01() {
        File f1 = new File("C:\\Users\\panqiyi\\Desktop\\notes");
        boolean e1 = f1.exists();
        System.out.println(e1);//true

        File f2 = new File("C:\\Users\\panqiyi\\Desktop\\no");
        boolean e2 = f2.exists();
        System.out.println(e2);//false
    }
}
```

#### 创建删除功能方法

```Java
/*
public boolean createNewFile()  当文件名称不存在时，创建一个新的空文件
public boolean delete()  删除由此File表示的文件或文件夹
public boolean mkdir()  创建由此File表示单级的文件夹
public boolean mkdirs()  创建由此File表示的多级文件夹
* */
public class File5 {
    public static void main(String[] args) throws IOException {
        show01();
        show02();
        show03();
    }

    private static void show03() {
        /*删除的文件/文件夹 的路径在File构造方法给出；
        返回值: 布尔值
        true ： 删除成功，返回true
        false ：当文件夹有内容，或路径不存在，返回false
        注意： 1、此法直接从硬盘上删除，不走回收站*/
        File f4 = new File("C:\\Users\\panqiyi\\Desktop\\notes\\111");
        boolean d1 = f4.delete();
        System.out.println(d1);
    }

    private static void show02() {
        /*创建文件夹的路径在File构造方法给出；
        返回值: 布尔值
        true ： 当文件夹不存在，创建文件夹，返回true
        false ：当文件夹存在，不创建文件夹，返回false
        注意： 1、此法只能创建文件夹，不能创建文件*/
        File f2 = new File("C:\\Users\\panqiyi\\Desktop\\notes\\ccc");
        boolean m2 = f2.mkdir();//mkdir()只能创建单级文件夹 ccc
        System.out.println(m2);

        File f3 = new File("C:\\Users\\panqiyi\\Desktop\\notes\\111\\222\\333");
        boolean m3 = f3.mkdirs();//mkdirs() 可创建多级文件夹，111\222\333
        System.out.println(m3);
    }

    private static void show01() throws IOException {
        /*创建文件的路径在File构造方法给出；
        返回值: 布尔值
        true ： 当文件不存在，创建文件，返回true
        false ：当文件存在，不创建文件，返回false
        注意： 1、此法只能创建文件，不能创建文件夹
              2、创建文件的路径必须存在，否则抛出异常

              此方法 public boolean createNewFile() throws IOException
              声明抛出异常；所以我们要处理：throws,try/catch
        * */
        File f1 = new File("C:\\Users\\panqiyi\\Desktop\\notes\\1.txt");
        boolean n1 = f1.createNewFile();
        System.out.println(n1);
    }
}
```

#### 遍历文件夹功能

```Java
/*
* 遍历目录的两个方法：
*  public String[] list()   返回一个String[]数组，表示File路径文件夹下的所有文件/文件夹
*  public File[] listFiles()   返回一个File[]数组，表示File路径文件夹下的所有文件/文件夹
*
*     注意：
*         File路径末尾是文件，
*         File路径不存在，
*         都会运行抛出空指针异常*/
public class File6 {
    public static void main(String[] args) {
        show01();
        show02();
    }

    private static void show02() {
        /*listFiles()方法遍历构造方法中的路径，把文件/文件夹封装为File对象，
        * 多个File对象存储到File数组中*/
        File f1 = new File("C:\\Users\\panqiyi\\Desktop\\notes");
        File[] f2 = f1.listFiles();
        for (File file : f2) {
            System.out.println(file);
        }
        //C:\Users\panqiyi\Desktop\notes\MySQL用法.md
        //C:\Users\panqiyi\Desktop\notes\SQL.md
    }

    private static void show01() {
        File f1 = new File("C:\\Users\\panqiyi\\Desktop\\notes");
        String[] l1 = f1.list();
        for (String s : l1) {
            System.out.println(s);
        }
        //MySQL用法.md
        //SQL.md
    }
}
```

#### 递归

```Java
/*
* 递归：方法自己调用自己
* 递归的分类：
*   递归分为两种，直接递归和间接递归。
*   直接递归：方法自身调用自己。
*       a(){
*            a();
*           }
*   间接递归：a方法调用b,b方法调用a
*   a(){
*       b();
*     }
*   b(){
*       a();
*     }
* 注意事项：
*   递归一定要有条件限定，保证递归能够停止下来，否则会发生占内存溢出；
*   递归次数不能太多，否则也会发生栈内存溢出；
*   构造方法，禁止递归；
*   */
public class digui1 {
    public static void main(String[] args) {
        //a();//1
        b(1);
    }

    private static void b(int i) {
        System.out.println(i);
        if(i==20000){// 递归次数太多，内存溢出异常；
            return;
        }
        b(++i);
    }

    private static void a() {
        System.out.println("a方法");
        a();
        //无结束条件，内存溢出 StackOverflowError异常
    }

}
```

**递归计算1-n之间的和**

```java
public static void main(String[] args) {
   int s= num(3);
    System.out.println(s);
}

private static int  num(int n) {
    if (n==1){
        return 1;
    }
    return n+num(n-1);
}
```

**递归计算阶乘**

```java 
public static void main(String[] args) {
    int jc = jc(5);
    System.out.println(jc);
}
public static int jc(int n){
    if (n==1){
        return 1;
    }
    return n*jc(n-1);
}
```

![](C:\Users\panqiyi\Desktop\notes\image\53.png)

#### 递归多级打印文件夹

```Java
public static void main(String[] args) {
    File f1 = new File("C:\\Users\\panqiyi\\Desktop\\abc");
    getAll(f1);
}
public static void getAll(File f){
    File[] files = f.listFiles();
    for (File file : files) {
        if (file.isDirectory()){//判断如果是文件夹
            getAll(file); //递归 继续打印文件夹内的文件
        }else {
            System.out.println(file);
        }}}
//直接打印会打印abc中的aa文件夹
//递归打印还会打印aa文件夹中的文件
```

#### 文件搜索

需求：遍历abc文件夹的子文件夹，只要.java结尾文件

```Java
public static void main(String[] args) {
    File f1 = new File("C:\\Users\\panqiyi\\Desktop\\abc");
    getAll(f1);
}
public static void getAll(File f){
    File[] files = f.listFiles();
    for (File file : files) {
        if (file.isDirectory()){//判断如果是文件夹
            getAll(file); //递归 继续打印文件夹内的文件
        }else {
            /*要求只打印.java结尾的文件
            * 1、把file类转换成字符串对象*//*
            String name = file.getName();
            //调用String类中的toLowerCase()方法把字符串转化成小写  避免.JAVA结尾不打印
            String s = name.toLowerCase();
            //2、调用String类中的endswith方法判断字符串是否已.java结尾
            boolean b = s.endsWith(".java");
            //3、如果以.java结尾的文件，则输出*/

            //链式编程
            if (file.getName().toLowerCase().endsWith(".java")){
                System.out.println(file);
            }}}}
```

#### 过滤器

**1、FileFilter  过滤器接口**

```Java
/*该过滤器接口需实现类实现接口并重写accept方法*/
public class FileFilterImpl implements FileFilter {
    @Override
    public boolean accept(File file) {
        /*自定义过滤规则： 判断File对象是否.java结尾
        * 是就返回true  不是返回false*/
        if (file.isDirectory()){//文件夹也放到File数组中
            return true;
        }
        return file.getName().toLowerCase().endsWith(".java");
        //return file.isDirectory()||file.getName().toLowerCase().endsWith(".java");
    }
}
//////////////////////////////////////
public class DiGui4 {
    public static void main(String[] args) {
        File f1 = new File("C:\\Users\\panqiyi\\Desktop\\abc");
        getAll(f1);
    }
    public static void getAll(File f){
        /*这里listFiles方法：
        * 1、遍历File构造方法目录中的文件/文件夹--->封装为File对象
        * 2、调用过滤器中的accept方法
        * 3、会把遍历得到的每一个File对象，传递给accept方法的参数
        *
        * accept方法返回值是一个布尔值：
        * true：会把传递过去的Fil对象保存到File数组中
        * false：不会把传递过去的Fil对象保存到File数组中*/
        File[] files = f.listFiles(new FileFilterImpl());
        for (File file : files) {
            if (file.isDirectory()){//判断如果是文件夹
                getAll(file); //递归 继续打印文件夹内的文件
            }else {
                    System.out.println(file);
            }}}}
```

**优化：匿名内部类**

```Java
public class DiGui4 {
    public static void main(String[] args) {
        File f1 = new File("C:\\Users\\panqiyi\\Desktop\\abc");
        getAll(f1);
    }
    public static void getAll(File f){
        File[] files = f.listFiles(new FileFilter() {
            @Override
            public boolean accept(File file) {//可用Lambda表达式进一步优化间接
                return file.isDirectory()||file.getName().toLowerCase().endsWith(".java");
            }
        });
        for (File file : files) {
            if (file.isDirectory()){//判断如果是文件夹
                getAll(file); //递归 继续打印文件夹内的文件
            }else {
                    System.out.println(file);
            }}}}
```

**2、FilenameFilter  过滤器接口**

```java 
 public static void main(String[] args) {
        File f1 = new File("C:\\Users\\panqiyi\\Desktop\\abc");
        getAll(f1);
    }
    public static void getAll(File f){
       /* File[] files = f.listFiles(new FilenameFilter() {
            @Override
            public boolean accept(File file, String s) {//前面是文件目录(路径)，后面是文件名
                //自定义过滤规则
                return new File(file,s).isDirectory()||s.toLowerCase().endsWith(".java");
                //注意：是 String 类型的s文件名来调用
            }
        });*/
        //使用Lambda表达式
        File[] files = f.listFiles(( file, s)-> new File(file,s).isDirectory()||s.toLowerCase().endsWith(".java"));
        for (File file : files) {
            if (file.isDirectory()){//判断如果是文件夹
                getAll(file); //递归 继续打印文件夹内的文件
            }else {
                    System.out.println(file);
            }}}
```

**FileFilter接口与FilenameFilter接口都只有一个accept抽象方法；所以可以用Lambda表达式来优化匿名内部类**

### IO流

io：输入/输出(input/output)

流：数据传输

io流是用来处理设备间数据传输问题的：

常见应用：文件复制，文件上传，文件下载

![](C:\Users\panqiyi\Desktop\notes\image\54.png)

**一切文件在计算机中都是以字节方式存储，**

如果文件以记事本方式打开内容读懂没有乱码，则可以用字符流；否则使用字节流；不知时直接用万能的字节流；

#### 字节流

**字节流可以复制(读写)任何文件**

##### OutputStream写入(输出流)

所有的字节输出流类的**抽象**父类

其子类都以父类名后缀；

###### FileOutputStream

 FileOutputStream是其子类   : 文件输出流用于将数据写入File

**1、FileOutputStream(String  name)构造方法创建文件输出流与对象**

**2、write方法写入**

**close方法释放资源**

```Java
/*
*  FileOutputStream  文件输出流用于将数据写入File
*   FileOutputStream(String name)  创建文件输出流以指定的名称文件写入*/
public class FileOutputStream01 {
    public static void main(String[] args) throws IOException {
        FileOutputStream f1 = new FileOutputStream("C:\\Users\\panqiyi\\Desktop\\abc\\123.txt");
        /* 这里的构造方法做了三件事：
        *           1、调用系统功能创建了文件
        *           2、创建了字节输出流对象
        *           3、让字节输出流对象指向创建好的文件*/

        //void write(int b)  将指定字节写入此文件输出流
        f1.write(97); //123.txt写入了 a

        //最后要释放资源
        //void  close()   关闭此文件输出流并释放与此流相关的系统资源
        f1.close();
    }
}
```

###### 字节流写入三种方式

write(int b)  将指定字节写入此文件输出流

write(byte[] b)  将指定的字节数组写入文件输出流   

```Java
public static void main(String[] args) throws IOException {
    FileOutputStream f1 = new FileOutputStream("C:\\Users\\panqiyi\\Desktop\\abc\\123.txt");
    f1.write(98);//写入该字节  b

    byte[] by = "qwert".getBytes();//返回对应字符串的字节数组
    f1.write(by);//写入该字节数组  qwert

    f1.write(by,1,3);//(字节数组对象，开始写入索引，写入长度)   wer

    f1.close();//释放资源
}
```

**字节流写入数据的两个问题**

1、换行

windows: \r\n          linux:  \n                 mac: \r

2、字节流写入数据如何实现**追加写入**

```Java
public static void main(String[] args) throws IOException {
//        FileOutputStream f1 = new FileOutputStream("C:\\Users\\panqiyi\\Desktop\\abc\\123.txt");
        FileOutputStream f1 = new FileOutputStream("C:\\Users\\panqiyi\\Desktop\\abc\\123.txt", true);//true 可继续在结尾追加
        for (int i = 0; i < 10; i++) {
            f1.write("hello".getBytes());
            f1.write("\r\n".getBytes());
        }
        f1.close();
    }
```

**写入数据的异常处理**

try/catch处理异常（要了解）  写入异常常用还是throws抛出

```Java
FileOutputStream f1=null;//对象初始化
try {
    f1 = new FileOutputStream("C:\\Users\\panqiyi\\Desktop\\abc\\123.txt", true);
    f1.write("hello".getBytes());
}catch (IOException e){
    e.printStackTrace();
}finally {//释放资源语句放在这，避免没有执行
    try {
        f1.close();//null调用方法空指针异常  所以要处理
    } catch (IOException e) {
        e.printStackTrace();
    }
}
```

##### InputStream读取(输入流)

所有字节输入流的**抽象**父类；

其子类都以父类名后缀；

###### FileInputStream

InputStream的一个子类；从文件系统中的文件获取输入字节

**字节输入流读数据使用步骤**

1、创建字节输入流对象

2、调用字节输入流对象的读取方法

3、释放资源

```Java
public static void main(String[] args) throws IOException {
    //创建输出流对象，并在构造方法中创建文件添加数据
    FileOutputStream f1 = new FileOutputStream("C:\\Users\\panqiyi\\Desktop\\abc\\12.txt");
    f1.write("qwewrtyyu".getBytes());
   //创建输入流对象，并在构造方法中指向要读取的文件路径
    FileInputStream f2 = new FileInputStream("C:\\Users\\panqiyi\\Desktop\\abc\\12.txt");
    int by;
    //while不断读取直到没有数据
    //f2.read() 读数据   然后赋值给by
    while ((by=f2.read())!=-1){//读取文件的字节，如果返回-1则表示没有内容了
        System.out.print((char) by);//转换为字符 输出qwewrtyyu  否则输出 113 119……
    }
    //释放资源
    f2.close();
}
```

**文件复制**

将源文件一个一个读取，然后就一个一个写入到目标文件；

```java
public static void main(String[] args) throws IOException {
        FileInputStream f1 = new FileInputStream("C:\\Users\\panqiyi\\Desktop\\abc\\12.txt");
        FileOutputStream f2 = new FileOutputStream("C:\\Users\\panqiyi\\Desktop\\abc\\34.txt");
        int by;
        while((by=f1.read())!=-1){
            f2.write(by);//读一个写入一个
        }
        //释放资源
        f1.close();
        f2.close();
    }
```

![](C:\Users\panqiyi\Desktop\notes\image\111.png)

**字节输入流读取数据(按字节数组)**

一次读取一个字节数组

```java
public static void main(String[] args) throws IOException {
    //创建输出流对象
    FileInputStream f1 = new FileInputStream("C:\\Users\\panqiyi\\Desktop\\abc\\12.txt");
    //创建字节数组
    byte[] by = new byte[5];
    int r1 = f1.read(by);
    System.out.println(r1);//返回实际读取到字符个数(不是数组长度)：5
    //将字节数组转换为字符串
    //System.out.print(new String(by));
    System.out.println(new String(by,0,r1));

    //第二次
     r1 = f1.read(by);
    //将字节数组转换为字符串
    //new String(字符数组对象) 返回一个字符串
    //System.out.println(new String(by));
    System.out.println(new String(by,0,r1));

    //第三次
    r1 = f1.read(by);
    System.out.println(r1);//返回4，因为第三次读到的只有4个字符
    //将字节数组转换为字符串
    /*System.out.println(new String(by)); 这里把整个字符数组都转成了字符串，
    但是我们只需要实际读到的元素转成字符串，否则可能会打印上一次读到剩余元素，如下面第三次读取*/
    System.out.println(new String(by,0,r1));

 /*
    hello\r\n
    javac\r\n
因为windows对字节流识别换行符为\r\n
第一次：hello     字符数组中有：hello 5个字符
第二次：\r\njav   --> 第二次数据将第一次在数组中的元素替换
第三次：ac\r\nc   -->第三次数据将第二次在数组中的元素替换，
                    因为第三次只有4个，所以还剩一个c在第三次中

*/
    //释放资源
    f1.close();
}
```

**优化**

```java
public static void main(String[] args) throws IOException {
    FileInputStream f1 = new FileInputStream("C:\\Users\\panqiyi\\Desktop\\abc\\12.txt");

    byte[] bys = new byte[1024];//一般情况长度定义为1024或 其倍数
    int len;
    //循环不断读取，直到文件无数据
    while((len=f1.read(bys))!=-1){//当无数据是返回-1
        System.out.println(new String(bys,0,len));
    }
    /*  hello
        javac
     */
}
```

**复制图片**

```Java
public static void main(String[] args) throws IOException {
    FileInputStream f1 = new FileInputStream("C:\\Users\\panqiyi\\Desktop\\abc\\aa\\222.jpg");
    FileOutputStream f2=new FileOutputStream("C:\\Users\\panqiyi\\Desktop\\abc\\444.jpg");
    byte[] bys = new byte[1024];
    int len;
    while((len=f1.read(bys))!=-1){
        f2.write(bys,0,len);//注意 (bys,0,len) 写入读取到的实际内容
    }
    f1.close();
    f2.close();
}
```

##### 字节缓冲流

不必为写入的每个字节导致底层系统的调用。增加效率与速度

BufferedOutputStream类：

BufferedInputStream类：

**原理**

![](C:\Users\panqiyi\Desktop\notes\image\1img\12.png)

**构造方法**

* 字节缓冲输出流：BufferedOutputStream(OutputStram  out)
* 字节缓冲输入流：BufferedInputStream(InputStream  in)

```java
public static void main(String[] args) throws IOException {
    //分别创建字节输出、输入缓冲流对象
    BufferedOutputStream bis = new BufferedOutputStream(new FileOutputStream("C:\\Users\\panqiyi\\Desktop\\abc\\33.txt"));
    BufferedInputStream  bos=new BufferedInputStream(new FileInputStream("C:\\Users\\panqiyi\\Desktop\\abc\\12.txt"));
    //缓冲流构造方法中传入的是 字节输入或输出流对象
    bis.write("暗杀部队".getBytes());//写入

    byte[] bys = new byte[1024];//字节数组读取
    int len;
    while ((len=bos.read(bys))!=-1){
        System.out.println(new String(bys,0,len));
    }
    //释放资源
    bis.close();
    bos.close();
}
```

##### 不同方式读写文件效率

```java
public static void main(String[] args) throws IOException{
    /*
      读写.mp4视频文件
      
    1、字节流每次读写   一个字节      --> 时间：5558 ms
    2、字节流每次读写   一个字节数组   --> 时间：10 ms
    3、字节缓冲流每次读写  一个字节     --> 时间：43 ms
    4、字节缓冲流每次读写  一个字节数组    --> 时间：4 ms 
    */
    long l1 = System.currentTimeMillis();
   // methed01(); //1
   // methed02(); //2
   // methed03(); //3
      methed04();
    long l2 = System.currentTimeMillis();
    System.out.println("时间："+(l2-l1));
}

public static void methed01() throws IOException {//1
    //字节流每次读写一个字节
    FileInputStream fis = new FileInputStream("C:\\Users\\panqiyi\\Desktop\\abc\\aa\\adc.mp4");
    FileOutputStream fos = new FileOutputStream("C:\\Users\\panqiyi\\Desktop\\abc\\dvd.mp4");
    int len;
    while ((len=fis.read())!=-1){
        fos.write(len);
    }
    fis.close();
    fos.close();
}
public static void methed02() throws IOException{//2
    //字节流每次读写一个字节数组
    FileInputStream fis = new FileInputStream("C:\\Users\\panqiyi\\Desktop\\abc\\aa\\adc.mp4");
    FileOutputStream fos = new FileOutputStream("C:\\Users\\panqiyi\\Desktop\\abc\\acc.mp4");

    byte[] bys = new byte[1024];
    int len;
    while ((len=fis.read(bys))!=-1){
        fos.write(bys,0,len);
    }
    fis.close();
    fos.close();
}
public static void methed03() throws IOException{//3
    //字节缓冲流每次读写一个字节
    BufferedInputStream bis = new BufferedInputStream(new FileInputStream("C:\\Users\\panqiyi\\Desktop\\abc\\aa\\adc.mp4"));
    BufferedOutputStream bos = new BufferedOutputStream(new FileOutputStream("C:\\Users\\panqiyi\\Desktop\\abc\\aac.mp4"));

    int len;
    while((len=bis.read())!=-1){
        bos.write(len);
    }
    bis.close();
    bos.close();
}
public static void methed04() throws IOException{
    //字节缓冲流读写 每次一个字节数组
    BufferedInputStream bis = new BufferedInputStream(new FileInputStream("C:\\Users\\panqiyi\\Desktop\\abc\\aa\\adc.mp4"));
    BufferedOutputStream bos = new BufferedOutputStream(new FileOutputStream("C:\\Users\\panqiyi\\Desktop\\abc\\acc.mp4"));

    byte[] bys=new byte[1024];
    int len;
    while ((len=bis.read(bys))!=-1){
        bos.write(bys,0,len);
    }
    bis.close();
    bos.close();
}
```

#### 字符流

也叫转换流，构造方法传入字节流对象 

**字符流只能复制(读写)文本文件**

Reader（抽象类）--->  InputStreamReader (子类) ---- > FileReader（子类）

Writer  (抽象类) ---->  OutputStreamWriter (子类) -----> FileWriter（子类）

##### 汉字储存

```Java
/*
*    一个汉字储存：
*       如果是GBK编码，占用两个字节
*       如果是UTF-8 编码，占用3个字节  */
public class BufferedOutStream01 {
    public static void main(String[] args) throws IOException {
        //分别创建字节输出、输入缓冲流对象
        BufferedOutputStream bis = new BufferedOutputStream(new FileOutputStream("C:\\Users\\panqiyi\\Desktop\\abc\\33.txt"));
        BufferedInputStream  bos=new BufferedInputStream(new FileInputStream("C:\\Users\\panqiyi\\Desktop\\abc\\12.txt"));

        String s="中国";
       byte[] bys = s.getBytes(); // 使用默认字符集，这里是utf-8 [-28, -72, -83, -27, -101, -67]
        //可以指定编码
        byte[] bys = s.getBytes("UTF-8");  //[-28, -72, -83, -27, -101, -67]
        byte[] bys = s.getBytes("GBK");// [-42, -48, -71, -6]
        System.out.println(Arrays.toString(bys));
        //  所以GBK编码一个中文 2个字节 ，UTF-8一个中文 3个字节

        
         // 用字节输入流每次读取一个字节
        int len;
        while ((len=bos.read())!=-1){
            System.out.print((char) len);  //结果：ä¸­å½ 输出的不是中文，因为是每次读取一个字符然后直接打印出来了
        }
      
        
        //用字节输入流每次读取一个字节数组
        byte[] bytes = new byte[1024];
        int len;
        while ((len=bos.read(bytes))!=-1){
            System.out.println(new String(bytes,0,len)); //结果：中国
   // 因为无论哪种编码中文每一个字的 所有字节都是负数，底层会根据此进行字节的拼接，从而看到中文；
        }
        
        
        //用字节输入流每次读取一个字节，然后直接储存去文件中
        int len;
        while ((len=bos.read())!=-1) {
            bis.write(len); //每一个字节的读取然后储存，在储存到文件时字节会拼接，从而从储存在文件中看到中文；
        }

        bis.close();
        bos.close();
    }
}
//上面代码变量重复，因为原本就是一个一个的试，其他的就注释，为了好看就把注释删了
```

**总结：**读取中文要用字节数组，储存(写入)中文无所谓；

**由于字节流操作中文不是很方便，所以Java提供了字符流**

字符流：字节流 + 编码

##### 编码表(字符集)

1、储存在计算机中的信息都是用二进制数表示，我们在屏幕上看到的文字等都是经过转换后的结果；

2、按照某种规则，将字符储存到计算机中  -------  编码；反之，将储存在计算机中的二进制数按照某种规则解析出来 ------- 解码；

注意：按照A编码储存吗，就必须按照A编码解析，否则会乱码；

字符编码：一套自然语言字符与二进制数的对应规则(A--->65)

```java
public static void main(String[] args) throws UnsupportedEncodingException {
    String s="中国";
    byte[] bys = s.getBytes();// 默认字符集utf-8编码
    //指定GBK字符集解码
    String gBk = new String(bys, "GBk");
    System.out.println(gBk);// 结果乱码
}
```

##### 字符流的编解码

```Java
public static void main(String[] args) throws IOException {
        /*OutputStreamWriter osw = new OutputStreamWriter(new FileOutputStream("C:\\Users\\panqiyi\\Desktop\\abc\\33.txt")); //默认utf-8写入
        osw.write("中国人");
*/

       /* OutputStreamWriter osw2 = new OutputStreamWriter(new FileOutputStream("C:\\Users\\panqiyi\\Desktop\\abc\\33.txt"),"GBK"); //自定义GBK字符集
        osw2.write("中国人民！");*/


        /*//字符流读取文件
        InputStreamReader isr = new InputStreamReader(new FileInputStream("C:\\Users\\panqiyi\\Desktop\\abc\\33.txt"));
        //默认utf-8读取，因为此文件是以GBK编码保存的，所以用utf-8解码会乱码！！
        int len;
        while ((len=isr.read())!=-1){
            System.out.print((char) len);
        }*/

        InputStreamReader isr = new InputStreamReader(new FileInputStream("C:\\Users\\panqiyi\\Desktop\\abc\\33.txt"),"GBK");
        int len;
        while ((len=isr.read())!=-1){
            System.out.print((char) len); // 中国人民！
            //字符流读取中文可以一个一个字符直接输出！
        }
        isr.close();
    }
```

**注意：**OutputStreamWrite() 方法写入数据时，是先储存在缓冲区，必须刷新流才会储存在文件中；

1、刷新流方法：字符输出流对象调用 flush() 方法可以刷新流，可以继续使用流添加字符；     

2、 close() 方法： 释放资源前刷新流，此方法关闭流，再无法使用此流

##### 字符流写入方法

```Java
public static void main(String[] args) throws IOException {
    /*OutputStreamWriter osw = new OutputStreamWriter(new FileOutputStream("C:\\Users\\panqiyi\\Desktop\\abc\\777.txt"));
    osw.write("高山流水");  //未刷新流，数据还在缓冲区，未写入文件*/

    OutputStreamWriter osw = new OutputStreamWriter(new FileOutputStream("C:\\Users\\panqiyi\\Desktop\\abc\\777.txt"));
    //直接写入字符串
    osw.write("高山流水");
    osw.write("武功盖世");
    osw.write("天下第一");

    osw.write("一二三四",1,2); //二三   写入字符部分
    osw.flush();//刷新流，即从缓冲区储存到文件

    //写入字符数组
    osw.write("你好啊世界！".toCharArray()); //注意：是字符数组
    osw.flush();

    osw.write("天南地北".toCharArray(),1,2); //南地  ：取字符数组的一部分储存
    osw.flush();

    osw.close(); //释放资源、刷新流、关闭流
    // 只要此语句在末尾且无需使用流，可以不需要使用flush()方法刷新流！
}
```

##### 字符流的读取

```Java
public static void main(String[] args) throws IOException {
    InputStreamReader isr = new InputStreamReader(new FileInputStream("C:\\Users\\panqiyi\\Desktop\\abc\\777.txt"));
    //一次读取一个字符
    /*int len;
    while ((len=isr.read())!=-1){
        System.out.print((char)len);
    }*/

    //一次读取一个字符数组
    char[] ch = new char[1024];
    int len;
    while ((len=isr.read(ch))!=-1){
        System.out.print(new String(ch,0,len));
        
       isr.close(); 
    }
}
```

**读写案例：**

```Java
public static void main(String[] args) throws IOException {
    OutputStreamWriter osw = new OutputStreamWriter(new FileOutputStream("C:\\Users\\panqiyi\\Desktop\\abc\\666.txt"));
    InputStreamReader isr = new InputStreamReader(new FileInputStream("C:\\Users\\panqiyi\\Desktop\\abc\\777.txt"));
    //一次读写一个字符数据
   /* int len;
    while ((len=isr.read())!=-1){
        osw.write(len);
    }*/

   //一次读写一个字符数组
    char[] ch = new char[1024];
    int len;
    while ((len=isr.read(ch))!=-1){
        osw.write(ch,0,len); //注意这里 与字节流写入字节数组一样
    }
    osw.close();
    isr.close();
}
```

##### 便捷子类

由于字符输入输出流名称较长，所以使用二者的子类更加便捷，但是不能指定编码解码方式，只能按照本地默认编码；

**FileReader**  用于读取字符文件的便捷类

构造方法：FileReader (String fileName)    // 直接写文件路径

**FileWriter** 用于写入字符文件的便捷类；

构造方法：FileWriter (String fileName)

**读写案例**

```Java
public static void main(String[] args) throws IOException {
    FileReader fr = new FileReader("C:\\Users\\panqiyi\\Desktop\\abc\\777.txt");
    FileWriter fw = new FileWriter("C:\\Users\\panqiyi\\Desktop\\abc\\666.txt");
    //一次读写一个字符数据
   /* int len;
    while ((len=isr.read())!=-1){
        osw.write(len);
    }*/

   //一次读写一个字符数组
    char[] ch = new char[1024];
    int len;
    while ((len=fr.read(ch))!=-1){
        fw.write(ch,0,len); //注意这里 与字节流写入字节数组一样
    }
    fw.close();
    fr.close();

```

##### 字符缓冲流

BufferedReader: 从字符输入流读取文本，缓冲字符，提高读取效率，

BufferedWriter:  将文本写入字符输出流，缓冲字符，提高写入效率，

注意：(缓冲区大小可以自定义，但默认值已经足够大，一般无需自定义);

**读取写入案例：**

```Java
public static void main(String[] args) throws IOException {
    BufferedReader br= new BufferedReader(new FileReader("C:\\Users\\panqiyi\\Desktop\\abc\\777.txt"));
    BufferedWriter bw = new BufferedWriter(new FileWriter("C:\\Users\\panqiyi\\Desktop\\abc\\666.txt"));//构造方法中传入 字符输入或输出流对象

    //字符缓冲流每次读取一个字符
    /*int len;
    while ((len=br.read())!=-1){
        bw.write(len);
    }*/


    //字符缓冲流每次读写一个字符数组
    char[] ch = new char[1024];
    int len;
    while ((len=br.read(ch))!=-1){
        bw.write(ch,0,len);
    }
    br.close();
    bw.close();
    
    //字符缓冲流每次读取一个字符数组，并打印
        char[] chs = new char[1024];
        int len;
        while ((len=br.read(chs))!=-1){
            System.out.println(new String(chs,0,len));
        }

}
```

##### 字符缓冲流特有方法

flush()  ： 换行符，其他系统都可以识别  （输出流）

readLine()   ：一次读取一行内容输出，但不包括换行符   （输入流）

```Java
public static void main(String[] args) throws IOException {
    BufferedReader br = new BufferedReader(new FileReader("C:\\Users\\panqiyi\\Desktop\\abc\\666.txt"));
    BufferedWriter bw = new BufferedWriter(new FileWriter("C:\\Users\\panqiyi\\Desktop\\abc\\666.txt"));

    for (int i = 0; i < 5; i++) {
        bw.write("中国！世界！");
        bw.newLine();// 换行符，其他系统都可以识别
        bw.flush();  
    }

    String line;
    while ((line=br.readLine())!=null){
        System.out.println(line); // 一次读取 一行全部内容，但不包括换行符 (所以是println 读完每一行就换行)
        
        br.close();
        bw.close();
    }
}
```

**readline复制(读写)文件**

```java
public static void main(String[] args) throws IOException {
    BufferedReader br = new BufferedReader(new FileReader("C:\\Users\\panqiyi\\Desktop\\abc\\777.txt"));
    BufferedWriter bw = new BufferedWriter(new FileWriter("C:\\Users\\panqiyi\\Desktop\\abc\\666.txt"));

    String line;
    while ((line=br.readLine())!=null){
        bw.write(line); // 每次读一行全部内容，但是不包括换行符
        bw.newLine(); // 换行符
        bw.flush(); //刷新流
        // 三个步骤都要有！
    }

}
```

##### 总结

字节流：可以读写任何文件；一般使用字节缓冲流 ---> 每次读写一个字节数组；

字符流：只能读写文本文件；一般使用字符缓冲流 ---> 特有方法readLine() 每次读取一行字符

**案例：集合写入文件**

```Java
public static void main(String[] args) throws IOException {
    ArrayList<String> list=new ArrayList<>();
    list.add("中国");
    list.add("世界");
    list.add("和平");
    //创建字符缓冲输出流
    BufferedWriter fw = new BufferedWriter(new FileWriter("C:\\Users\\panqiyi\\Desktop\\abc\\666.txt"));
    for (String s : list) {//遍历集合
        System.out.println(s);
        fw.write(s);//将集合内元素写入文件
        fw.newLine();//字符缓冲流特有方法  newLine()
        fw.flush();
    }

    fw.close();
}
```

**案例：文件到集合**

```Java
public static void main(String[] args) throws IOException {
    ArrayList<String> list=new ArrayList<>(); //创建ArrayList对象
    //创建字符缓冲输入流对象
    BufferedReader br=new BufferedReader(new FileReader("C:\\Users\\panqiyi\\Desktop\\abc\\666.txt"));

    String line;
    while ((line=br.readLine())!=null){ //调用字符缓冲输入流对象方法读取数据
        list.add(line); //将字符串添加到集合中
    }
    br.close();
    
    //遍历集合
    for (String s : list) {
        System.out.println(s);
    }
    
}
```

**点名器**

就是在上面 “文件到集合” 案例 加上随机数索引

```Java
public static void main(String[] args) throws IOException {
    ArrayList<String> list=new ArrayList<>(); //创建ArrayList对象
    //创建字符缓冲输入流对象
    BufferedReader br=new BufferedReader(new FileReader("C:\\Users\\panqiyi\\Desktop\\abc\\666.txt"));

    String line;
    while ((line=br.readLine())!=null){ //调用字符缓冲输入流对象方法读取数据
        list.add(line); //将字符串添加到集合中
    }
    br.close();

    //遍历集合
    for (String s : list) {
        System.out.println(s);
    }

    Random random = new Random();
    int i = random.nextInt(list.size());

    System.out.println("幸运者是："+list.get(i));
}
```

**将集合中类储存到文件**

```Java
public static void main(String[] args) throws IOException {
    ArrayList<Student> list=new ArrayList<>();
    list.add(new Student(1001,"林青霞",23,"香港"));
    list.add(new Student(1002,"关羽",43,"蜀国"));
    list.add(new Student(1003,"张飞",42,"蜀国"));
    list.add(new Student(1004,"毛泽东",33,"中国"));
    list.add(new Student(1005,"特朗普",26,"美国"));

    BufferedWriter bw = new BufferedWriter(new FileWriter("C:\\Users\\panqiyi\\Desktop\\abc\\666.txt"));

    for (Student s : list) {
        StringBuilder sb = new StringBuilder(); //创建StringBuilder类对像
        
        // 把学生对象的数据拼接成指定的格式的字符串
  sb.append(s.getId()).append(",").append(s.getName()).append(",").append(s.getAge()).append(",").append(s.getHome());  ///注意这里的拼接
        
        bw.write(sb.toString()); //sb 是对象，使其变为字符串
        bw.newLine();
        bw.flush();
    }
    bw.close();
}
```

思考：反之，将文件储存到集合中的类呢？----> 将文件每行按某符号分割为字符数组，在将数组中对应的值赋值给类的属性；

![](C:\Users\panqiyi\Desktop\notes\image\1img\51.png)

```Java
//设置学生类
public class Student {
    private String name;
    private int age;
    private int Grade;
    省略了 有无参构造方法/get/set/重写toString()
    }
```

```Java
public static void main(String[] args) throws IOException {
    BufferedReader br = new BufferedReader(new FileReader("C:\\Users\\panqiyi\\Desktop\\abc\\student.txt"));
    String line;
    ArrayList<Student> stulist = new ArrayList<>();
    while ((line=br.readLine())!=null){
        System.out.println(line); //李小龙,28,89

        //将字符串按 "," 分割，返回一个字符串数组
        String[] strArray = line.split(",");


        //将字符串放入对应类属性，然后将类存储到集合中
        stulist.add(new Student(strArray[0],Integer.parseInt(strArray[1]),Integer.parseInt(strArray[2])));

    }
    //遍历集合输出
    stulist.forEach(System.out::println);

    br.close();

}
```

**案例：集合中 类的数据排序 存储到文件**

```Java
public static void main(String[] args) throws IOException {
    Scanner ns=new Scanner(System.in);

    System.out.println("请输入学生个数：");
    int n = ns.nextInt();

    //创建集合对象 并 匿名内部类创建比较器
    TreeSet<Student> s = new TreeSet<>(new Comparator<Student>() {
        @Override
        public int compare(Student s1, Student s2) {
            int num=s2.sum()-s1.sum(); // 总成绩按高到低排
            int num2=num==0?s2.getWen()-s1.getWen():num; //如果总成绩一样，按语文成绩高到低排
            int num3=num2==0?s2.getMath()-s1.getMath():num2;//如果语文成绩一样，按数学成绩高到低排
            return num3;
        }
    });

    for (int i = 1; i <= n; i++) { //循环输入学生信息
        System.out.println("请输入第"+i+"学生信息！");
        System.out.println("学号：");
        int id = ns.nextInt();
        System.out.println("姓名：");
        String name=ns.next();
        System.out.println("语文成绩：");
        int wen = ns.nextInt();
        System.out.println("数学成绩：");
        int math = ns.nextInt();

        Student st = new Student();//创建学生类对象 注意：要放在for中，因为每一次都要存储一次对象去集合中！！所以每循环一次就要创建一次对象

        //将输入的数据传递给学生类属性
        st.setId(id);
        st.setName(name);
        st.setWen(wen);
        st.setMath(math);

        s.add(st); //将学生类对象添加到集合中
    }

    BufferedWriter bw = new BufferedWriter(new FileWriter("C:\\Users\\panqiyi\\Desktop\\abc\\666.txt"));

    // 遍历集合中学生类对象
    for (Student su : s) {
        //将属性值拼接
        StringBuilder sb = new StringBuilder();
        sb.append(su.getId()).append(",").append(su.getName()).append(",").append(su.getWen()).append(",").append(su.getMath());

        //将拼接后的字符串写入文件中
        bw.write(sb.toString());
        bw.newLine();
        bw.flush();
    }

    bw.close();
}
```

**案例：复制单级文件夹**

```Java
需求：
        把D:\\AAA这个文件夹复制到D:\\CCC目录下

    思路：
        1:创建数据源目录File对象，路径是D:\\AAA
        2:获取数据源目录File对象的名称(AAA)
        3:创建目的地目录File对象，路径名是D:\\CCC+AAA组成(D:\\CCC\\AAA)
        4:判断目的地目录对应的File是否存在，如果不存在，就创建
        5:获取数据源目录下所有文件的File数组
        6:遍历File数组，得到每一个File对象，该File对象，其实就是数据源文件
            数据源文件：D:\AAA\\acc.mp4
        7:获取数据源文件File对象的名称(acc.mp4)
        8:创建目的地文件File对象，路径名是目的地目录+mn.jpg组成(D:\\CCC\\AAA\\acc.mp4)
        9:复制文件
            由于文件不仅仅是文本文件，还有图片，视频等文件，所以采用字节流复制文件
 */
public class CopyFolderDemo {
    public static void main(String[] args) throws IOException {
        //创建数据源目录File对象，路径是 D:\AAA
        File srcFolder = new File("D:\\AAA");

        //获取数据源目录File对象的名称 (AAA)
        String srcFolderName = srcFolder.getName();

        //创建目的地目录File对象，路径名是 目的地+AAA组成 (D:\CCC\\AAA)
        File destFolder = new File("D:\\CCC",srcFolderName);

        //判断目的地目录对应的File是否存在，如果不存在，就创建
        if(!destFolder.exists()) {
            destFolder.mkdir();
        }

        //获取数据源目录下所有子文件的File数组
        File[] listFiles = srcFolder.listFiles();

        //遍历File数组，得到每一个File对象，该File对象，其实就是数据源文件
        for(File srcFile : listFiles) {
            //如其中一个数据源文件：D:\AAA\\acc.mp4
            //获取数据源文件File对象的名称(acc.mp4)
            String srcFileName = srcFile.getName();
            //创建目的地文件File对象，路径名是目的地目录+acc.mp4组成(D:\\CCC\\AAA\\acc.mp4)
            File destFile = new File(destFolder,srcFileName);
            //复制文件
            copyFile(srcFile,destFile);
        }
    }

    private static void copyFile(File srcFile, File destFile) throws IOException {
        BufferedInputStream bis = new BufferedInputStream(new FileInputStream(srcFile));
        BufferedOutputStream bos = new BufferedOutputStream(new FileOutputStream(destFile));

        byte[] bys = new byte[1024];
        int len;
        while ((len=bis.read(bys))!=-1) {
            bos.write(bys,0,len);
        }

        bos.close();
        bis.close();
    }
}
```

<img src="C:\Users\panqiyi\Desktop\notes\image\1img\15.png" style="zoom:80%;" />

**案例：复制多级文件夹**

```Java
需求：
        把“E:\\itcast”复制到 F盘目录下

    思路：
        1:创建数据源File对象，路径是E:\\itcast
        2:创建目的地File对象，路径是F:\\
        3:写方法实现文件夹的复制，参数为数据源File对象和目的地File对象
        4:判断数据源File是否是目录
            是：
                A:在目的地下创建和数据源File名称一样的目录
                B:获取数据源File下所有文件或者目录的File数组
                C:遍历该File数组，得到每一个File对象
                D:把该File作为数据源File对象，递归调用复制文件夹的方法
            不是：说明是文件，直接复制，用字节流
 */
public class CopyFoldersDemo {
    public static void main(String[] args) throws IOException {
        //创建数据源File对象，路径是E:\\itcast
        File srcFile = new File("E:\\itcast");
        //创建目的地File对象，路径是F:\\
        File destFile = new File("F:\\");

        //写方法实现文件夹的复制，参数为数据源File对象和目的地File对象
        copyFolder(srcFile,destFile);
    }

    //复制文件夹
    private static void copyFolder(File srcFile, File destFile) throws IOException {
        //判断数据源File是否是目录
        if(srcFile.isDirectory()) {
            //在目的地下创建和数据源File名称一样的目录
            String srcFileName = srcFile.getName();
            File newFolder = new File(destFile,srcFileName); //F:\\itcast
            if(!newFolder.exists()) {
                newFolder.mkdir();
            }

            //获取数据源File下所有文件或者目录的File数组
            File[] fileArray = srcFile.listFiles();

            //遍历该File数组，得到每一个File对象
            for(File file : fileArray) {
                //把该File作为数据源File对象，递归调用复制文件夹的方法
                copyFolder(file,newFolder);
            }
        } else {
            //说明是文件，直接复制，用字节流
            File newFile = new File(destFile,srcFile.getName());
            copyFile(srcFile,newFile);
        }
    }

    //字节缓冲流复制文件
    private static void copyFile(File srcFile, File destFile) throws IOException {
        BufferedInputStream bis = new BufferedInputStream(new FileInputStream(srcFile));
        BufferedOutputStream bos = new BufferedOutputStream(new FileOutputStream(destFile));

        byte[] bys = new byte[1024];
        int len;
        while ((len = bis.read(bys)) != -1) {
            bos.write(bys, 0, len);
        }

        bos.close();
        bis.close();
    }

}
```

#### 异常处理

![](C:\Users\panqiyi\Desktop\notes\image\1img\16.png)

```java
public static void main(String[] args) throws IOException{//这里抛出的是jdk9 方案的
    method01();//标准，无需抛出异常，但是复杂
    method02();//jdk7 优化简介，无需抛出异常 ---> 比较好用
    method03();//jdk9 优化简介，但是需要抛出
}

private static void method03() throws IOException{//jdk9 优化
    BufferedReader br = new BufferedReader(new FileReader("D:\\AAA"));
    BufferedWriter bw= new BufferedWriter(new FileWriter("D:\\CCC"));
    try(br;bw){
        String line;
        while((line=br.readLine())!=null){
            bw.write(line);
            bw.newLine();
            bw.flush();
        }
    }catch (IOException e){
        e.printStackTrace();
    }
}

private static void method02() {// jdk1.7 优化处理异常
    try(FileInputStream fi = new FileInputStream("D:\\AAA");
        FileOutputStream fo = new FileOutputStream("D:\\CCC");){
        byte[] bys = new byte[1024];
        int len;
        while ((len=fi.read(bys))!=-1){
            fo.write(bys,0,len);
        }
    }catch (IOException e){
        e.printStackTrace();
    }
    //自动释放资源
}

private static void method01() { // try{}catch(){}finally{}  处理异常，比较复杂
    FileReader fr =null;
    FileWriter fw =null;
    try {
        fr=new FileReader("C:\\Users\\panqiyi\\Desktop\\abc\\777.txt");
        fw=new FileWriter("C:\\Users\\panqiyi\\Desktop\\abc\\666.txt");

        char[] chs = new char[1024];
        int len;
        while ((len = fr.read(chs)) != -1) {
            fw.write(chs, 0, len);
            fw.flush();
        }

    }catch (IOException e){
        e.printStackTrace();
    }finally {
        if (fr!=null){
            try {
                fr.close();
            } catch (IOException e) {
                e.printStackTrace();
            }
        }
        if (fw!=null){
            try {
                fw.close();
            } catch (IOException e) {
                e.printStackTrace();
            }
        }}}
```

#### 标准流

**System 类中有两个静态成员变量**

 ```
    1、  public static final InputStream in
 ```

标准输入流，通常该流对应于键盘输入 或由主机环境或用户指定的另一个输入源

 ```
    2、  public static final PrintStream out
 ```

标准输出流，通常该流对应于显示输出 或由主机环境 或用户指定的另一个输出目标

**1、System.in**

键盘输入

```java 
public static void main(String[] args) throws IOException {
//in是System类的静态成员变量，数据类型是InputStream类，所以能使用InputStream类的所有方法
    InputStream in1 = System.in; // 创建标准输入流对象，从键盘输入字符串

   1、 // 按原本的字节流 读键盘输入的值
    byte[] bys = new byte[1024];
    int by;
    while ((by=in1.read(bys))!=-1){
        System.out.println(new String(bys,0,by));
    }

    2、//将字节流转换为字符流？ 用转换流
    InputStreamReader in2 = new InputStreamReader(in1);
    //字符流实现一次读取一行数据
    BufferedReader in3 = new BufferedReader(in2);
    String line;
    while((line=in3.readLine())!=null){
        System.out.println(line);
    }

    
   3、 //优化  一步解决 读键盘输入的字符串
    BufferedReader in4 = new BufferedReader(new InputStreamReader(System.in));
    String line;
    //输入一个字符串
    System.out.println(line=in4.readLine());

    //输入一个数字 并返回为int类型
    int i = Integer.parseInt(in4.readLine());
    System.out.println(i+5);

    //自己实现 键盘输入数据太麻烦了
    //Java提供了Scanner类
    Scanner sc=new Scanner(System.in); //底层包装的也是标准输入流

}
```

**2、System.out**

打印输出

```Java
public static void main(String[] args) {
    PrintStream ps = System.out; //out是System类的成员变量，数据类型是PrintStream类

    //System.out本质是字节输出流
    ps.println("中国");  //打印结果： 中国  然后换行
    ps.println(123);  //  123   然后换行
    ps.print(66);  //66  不换行
    
    System.out.println(); //输出语句本质是一个标准输出流
}
```

#### 打印流

**字节打印流: PrintStream**

- java.io.OutputStream
  - java.io.FilterOutputStream
    - java.io.PrintStream 

只负责输出数据，**不负责读取数据**

有自己的特有方法

构造方法：PrintStreram(String fileName) //创建打印流写入指定文件路径

使用父类写入方法时查看会转码，使用特有方法时原封不动；

```Java
public static void main(String[] args) throws IOException {

    PrintStream ps = new PrintStream("C:\\Users\\panqiyi\\Desktop\\abc\\55.txt");
    
    //使用父类字节输出流写入方法
    ps.write(97);  // 55.txt中写入   a

    //特有方法
    ps.print("97");  //97  写入什么就是什么
    ps.println("中国和");//  中国和    并换行
}
```

**字符打印流**

- java.io.Writer
  - java.io.PrintWriter 

构造方法：PrintWriter(String fileName)  

PrintWriter(Writer out,  boolean autoFlush)

```java
public static void main(String[] args) throws IOException {
        /*//创建字符打印流
        PrintWriter pw = new PrintWriter("C:\\Users\\panqiyi\\Desktop\\abc\\55.txt");

        //字符流写入都需要刷新才能成功
        pw.write("hello");
        pw.flush();
        pw.write("\r\n");
        pw.write("world");
        pw.flush();
        pw.write("\r\n");

        //使用字符打印流特有方法
        pw.println("中国");
//        pw.write("中国");
//        pw.write("\r\n");
       pw.flush();  //注意刷新  */

       //创建字符打印流并 不用刷新直接写入
        PrintWriter pw = new PrintWriter(new FileWriter("C:\\Users\\panqiyi\\Desktop\\abc\\55.txt"),true);
        pw.println("高山流水");  //true即无需刷新，直接写入;false就需刷新
    
    pw.close();
    }
```

**案例：使用字符打印流写入**

```Java
 public static void main(String[] args) throws IOException {
//创建字符缓冲流
        BufferedReader br=new BufferedReader(new FileReader("C:\\Users\\panqiyi\\Desktop\\abc\\777.txt"));

        //字符缓冲流写入
        BufferedWriter bw = new BufferedWriter(new FileWriter("C:\\Users\\panqiyi\\Desktop\\abc\\666.txt"));
        String line1;
        while ((line1=br.readLine())!=null){
            bw.write(line1); //写入一行数据但不包括换行符
            bw.newLine(); //换行符
            bw.flush(); //刷新
        }
        
        //打印流只能写入，不能读取； 使用打印流写入
        PrintWriter ps = new PrintWriter(new FileWriter("C:\\Users\\panqiyi\\Desktop\\abc\\666.txt"), true);
        String line;
        while ((line=br.readLine())!=null){
            ps.println(line); //写入一行 并换行
            ps.flush();
        }
     br.close();
     bw.close();
     ps.close();
    }
```

#### 序列化流

**对象序列化：**就是将对象保存到磁盘中，或者在网络中传输对象

使用一个字节序列表示一个对象，该字节序列包含：对象的类型，对象的数据，对象的属性等信息；

字节序列写到文件中，相当于文件中保存了一个对象信息；

反之：从文件中读取回来，重构对象，对它进行反序列化；

对象序列化流：ObjectOutputStream  （写入对象）

对象反序列化流：ObjectInputStream   (读取对象)

**对象序列化流：**

- java.io.OutputStream
  - java.io.ObjectOutputStream 

构造方法：ObjectOuputStream(OutputStream  out)   创建 从指定路径写入对象 的序列化流；

对象序列化的方法：即写入对象信息的方法

void writeObject(Object  obj)

```java 
public class Studen implements Serializable {
    private String name;
    private int age;
    ……省略了构造方法、get/set
}
///////////////////////

public static void main(String[] args) throws IOException {
    ObjectOutputStream oos = new ObjectOutputStream(new FileOutputStream("C:\\Users\\panqiyi\\Desktop\\abc\\55.txt"));
    Studen st = new Studen("令狐冲", 23);  //Studen类需要实现Serializable接口
    
    oos.writeObject(st);  //对象序列化的类必须实现Serializable接口(否则运行异常)，即这里Studen类需要实现
}
```

**注意：**

- 类的序列化由实现java.io.Serializable接口的类启用。  不实现此接口的类将不会使任何状态序列化或反序列化。

Serializable是一个**标记接口**，实现该接口不需要重写任何方法；

**对象反序列化流**

- java.io.InputStream
  - java.io.ObjectInputStream 

构造方法：ObjectInputStream(InputStream in) : 创建 从指定的文件读出对象 的反序列化流

对象反序列化的方法：

readObject() : 从ObjectInputStream读取一个对象；

```Java
public static void main(String[] args) throws IOException, ClassNotFoundException {
    ObjectOutputStream oos = new ObjectOutputStream(new FileOutputStream("C:\\Users\\panqiyi\\Desktop\\abc\\55.txt"));
    Studen studen = new Studen("林超贤",18);
    oos.writeObject(studen);
    ObjectInputStream ois = new ObjectInputStream(new FileInputStream("C:\\Users\\panqiyi\\Desktop\\abc\\55.txt"));

    Object o = ois.readObject();

    Studen s=(Studen)o; //对象向下转型

    System.out.println(s.getName()); //林超贤
}
```

**serialVersionUID**

serialVersionUID：（serial  这里 l 是小写L）

序列化运行时与每个可序列化的类关联一个版本号，称为serialVersionUID，它在反序列化过程中使用，以验证序列化对象的发送者和接收者是否加载了与序列化兼容的对象的类。

1、当序列化一个对象后，我们修改了该对象所属的类，读取时会抛出异常：InvalidClassException  （修改类即版本号serialVersionUID会改变，版本号不对应所以抛出异常）

2、解决：给对象所属类加一个 serialVersionUID 

- *强烈建议*所有可序列化的类显式声明serialVersionUID值

```
private static final long serialVersionUID = 42L; //值可以改变，但是必须是长整型；
```



3、如果一个对象中某个成员变量的值不想被序列化？

给该成员变量添加 `transient` 关键字修饰，该关键字标记的成员变量不参与序列化过程；



```java
public class Studen implements Serializable {
    private static final long serialVersionUID=42L;
    private String name;
    private transient int age;
		……
}
```



#### Properties类

- java.util.Hashtable<Object,Object>
  - java.util.Properties 

Hashtable<k,v>实现Map<k,v> 接口，**所以Properties也是个Map体系集合**  （注意：Properties集合是没有泛型的）

**Properties可以保存到流中或从流中加载**

**1、Properties作为Map集合使用**

```java
public static void main(String[] args) {
    //虽然是Map<k,v>集合体系，但是不同的是它没有泛型
    Properties ppt = new Properties();
    ppt.put(001,"林青霞");
    ppt.put(002,"令狐冲");
    ppt.put(003,"武当");

    //使用KeySet()遍历
    Set<Object> obj = ppt.keySet();
    for (Object o : obj) {
        Object value = ppt.get(o);//据键取值
        System.out.println(o+"\t"+value);
    }
    // 使用键值对遍历
    Set<Map.Entry<Object, Object>> ens = ppt.entrySet();
    for (Map.Entry<Object, Object> en : ens) {
        Object key = en.getKey();
        Object value = en.getValue();
        System.out.println(key+"\t"+value);
    }
}
```

**Properties集合的特有方法**

Object    setProperty(String  key,String  value)       设置集合的键和值，都是String类型，底层调用Hashtable<k,v>集合的put方法

String   getProperty(String  key)      使用此属性列表的键搜索值

Set< String>   stringPropertyName()     返回集合中所有的键组成集合，键对应的值是字符串

```Java
public static void main(String[] args) {
    Properties ppt = new Properties();

    ppt.setProperty("001","林超贤");   //向集合中添加元素
    ppt.setProperty("002","林青霞");
    ppt.setProperty("003","法海");

    String py = ppt.getProperty("001"); //据键取值
    System.out.println(py);

    Set<String> st = ppt.stringPropertyNames(); //返回集合所有键值存储在Set集合中
    for (String key : st) {
        Object value = ppt.get(key);
        System.out.println(key+"\t"+value);
    }
}
```

**Properties与IO流的结合**

![](C:\Users\panqiyi\Desktop\notes\image\1img\20.png)

```java 
public static void main(String[] args) throws IOException{
    //创建Properties集合
    Properties ppt = new Properties();
    ppt.setProperty("001","林青霞");
    ppt.setProperty("002","林允儿");
    ppt.setProperty("003","张曼玉");

    write(ppt);
    read(ppt);
}

private static void read(Properties ppt) throws IOException{// 将集合从文件读取出来  load()
    FileReader fr = new FileReader("C:\\Users\\panqiyi\\Desktop\\abc\\33.txt");
    ppt.load(fr);
    System.out.println(ppt);
}

private static void write(Properties ppt) throws IOException {// 将集合存储到文件  store()
    FileWriter fw = new FileWriter("C:\\Users\\panqiyi\\Desktop\\abc\\33.txt");
    ppt.store(fw,null);
    fw.close();
}
```

**注意：**这里使用的是字符流，所以用的是setProperty() 来设值，否则运行会出现类型转换异常：ClassCastException

**案例：游戏次数**

在文件中初始化：count=0    即键=值

读取文件，据键取值来计数游戏次数，每玩一次就+1并写入文件

```Java
public static void main(String[] args) throws IOException {
    Properties ppt = new Properties();
    //从文件中读取Properties的键，然后据键取值
    FileReader fr = new FileReader("C:\\Users\\panqiyi\\Desktop\\abc\\666.txt");
    ppt.load(fr);
    fr.close();

    String count = ppt.getProperty("count"); //count此时为0，但是是字符串类型
    //将字符串类型数字变为int类型
    int num = Integer.parseInt(count);

    //判断游戏次数是否到3
    if (num>=3){
        System.out.println("游戏结束！想玩请充值");
    }else {
        // 否则调用游戏类的玩游戏方法
        GameNumber.start(); // 如猜数字小游戏

        //次数+1，然后添加到集合中，再重新写入文件
        num++;
        ppt.setProperty("count",String.valueOf(num)); //将num转换为字符串类型才能添加

        //写入文件
        FileWriter fw = new FileWriter("C:\\Users\\panqiyi\\Desktop\\abc\\666.txt");
        ppt.store(fw,null);
        fw.close();
    }
}
```

### 网络编程

**计算机网络：**

![](C:\Users\panqiyi\Desktop\notes\image\1img\21.png)

**网络编程：**

在网络通信协议下，实现网络互连的不同计算机上运行的程序可以进行数据交换

**网络编程三要素：**

**IP地址：**

每台计算机的标识号；通过IP地址来识别计算机；即设备的标识

**端口：**

网络通信本质上是应用程序的通信 (如QQ要对应另一台设备的QQ)，但每台计算机都有很多应用程序，如何区分？

IP地址可以唯一确定网络中的设备；那端口号就是唯一标识设备中的应用程序；即程序的标识

**协议：**

位于同一个网络中的计算机间的连接和通信需要遵守一定的规则 ------->  网络通信协议；

它对数据的传输格式、传输速度、传输步骤等做了统一规定，通信双方必须同时遵守才能完成数据交换。常见协议有：UDP协议和TCP协议

**IP地址的分类:**

IPv4 与 IPv6  两大类；

**IPv4：**32位的地址，也就是4个字节，将每个字节用十进制表示，并用 “.” 分隔开，这就是"点分十进制表示法"表示IP地址；(IPv4仅能提供约42.9亿个IP位置)

**IPv6：**IP地址分配不够用，为了增加ip地址，IPv6二进位制下为128位长度，以16位为一组，每组以冒号“:”隔开，可以分为8组，每组以4位十六进制方式表示

![](C:\Users\panqiyi\Desktop\notes\image\1img\23.png)

常用命令：

ipconfig：查看本机IP地址

ping IP地址：检查网络是否连通

特殊地址：127.0.0.1

是回送地址，可代表本机地址，一般用来测试

**InetAddress类**

无构造方法！！

掌握以下三个方法

<img src="C:\Users\panqiyi\Desktop\notes\image\1img\24.png" style="zoom:80%;" />

```Java
public static void main(String[] args) throws UnknownHostException {
        // 确定主机
        InetAddress byName = InetAddress.getByName("10.15.73.175"); // ip地址或者计算机名
//        InetAddress byName2 = InetAddress.getByName("LAPTOP-LC8VDRK6");

        String hostName = byName.getHostName(); // 获取计算机名
        String hostAddress = byName.getHostAddress();//获取ip地址

        System.out.println(hostName+"\t"+hostAddress);
    }
```

**端口：**

![](C:\Users\panqiyi\Desktop\notes\image\1img\25.png)

**协议：**

**UDP协议**

![](C:\Users\panqiyi\Desktop\notes\image\1img\26.png)

**TCP协议**

![](C:\Users\panqiyi\Desktop\notes\image\1img\29.png)

![](C:\Users\panqiyi\Desktop\notes\image\1img\28.png)

![](C:\Users\panqiyi\Desktop\notes\image\1img\30.png)

**客户端**是主动打开方，**服务器**是被动打开方;

**1过程**和**2过程**叫 **半打开状态**  -----> 1过程发送连接请求但未收到服务器响应；2过程发送响应，但未收到客户端确认信息

**3**时进入**established**状态：建立连接   ----> 收到服务器响应后，客户端即可单方面向服务端建立连接

**4**时进入**established**状态：建立连接   ------>  收到客户端确认连接信息后，服务器也对应建立连接

#### UDP协议

**UDP通信原理**

![](C:\Users\panqiyi\Desktop\notes\image\1img\31.png)

##### UDP发送数据

![](C:\Users\panqiyi\Desktop\notes\image\1img\32.png)

```java
public static void main(String[] args) throws IOException {
    //创建发送端的Socket对象(DatagramSocket)
    //DatagramSocket() 构造数据报套接字并将其绑定到本地主机上的任何可用端口。
    DatagramSocket ds = new DatagramSocket();

    //创建数据，并把数据打包
    //DatagramPacket(byte[] buf, int length, InetAddress address, int port)
    // 构造一个数据包，发送长度为 length的数据包到指定主机上的指定端口号。
    byte[] bys = "hello!我来了".getBytes(); //字节数组
    int length = bys.length; //字节数组长度
    InetAddress address = InetAddress.getByName("10.15.73.175"); //目的地主机的ip地址
    int port=10086; //端口号
    DatagramPacket dp = new DatagramPacket(bys,length,address,port);
    // 也可以一步到位
    // DatagramPacket dp = new DatagramPacket(bys,bys.length,InetAddress.getByName("10.15.73.175"),10086);

    //调用DatagramSocket对象sent()方法发送数据
    ds.send(dp);

    //关闭发送端
    //void close() 关闭此数据报套接字。
    ds.close();
}
```

##### UDP接受数据

![](C:\Users\panqiyi\Desktop\notes\image\1img\33.png)

```java
public static void main(String[] args) throws IOException {
    // DatagramSocket(int port) 构造数据报套接字并将其绑定到本地主机上的指定端口。
    DatagramSocket ds = new DatagramSocket(10086); //传入 发送端对应端口

    //创建一个数据包，用于接收数据
    //DatagramPacket(byte[] buf, int length)
    // 构造一个 DatagramPacket用于接收长度为 length数据包。
    byte[] bys = new byte[1024];
    DatagramPacket dp = new DatagramPacket(bys, bys.length);

    //调用DatagramSocket对象receive()方法接收数据
    ds.receive(dp);

    //解析数据包，并把数据再控制台显示
    //byte[] getData() 返回数据缓冲区。
    //将dp数据包中的数据用一个字节数组接收出来
    byte[] data = dp.getData();

    //int getLength() 返回要发送的数据的长度或接收到的数据的长度。
    int len = dp.getLength();
    System.out.println("传来的数据是："+new String(data,0,len));
    //System.out.println("传来的数据是："+new String(dp.getData(),0,dp.getLength()));
    
    //关闭接收端
    ds.close();
}
//控制台输出：
传来的数据是：hello!我来了
```

**案例：**

1、UDP发送端，键盘输入发送数据，输入"886"结束

2、UDP接受端，不知发送端何时停止，死循环不断接收数据

```Java
//发送端
public static void main(String[] args) throws IOException {
    //创建Socket对象（DatagramSocket）
    DatagramSocket ds = new DatagramSocket();

    //自己封装一个键盘录入
    BufferedReader br=new BufferedReader(new InputStreamReader(System.in));

    String line;
    while ((line=br.readLine())!=null){
        if ("886".equals(line)){  //结束条件  不用"==" 因为String类的对象 "886"等都是对象
            break;
        }
        //未结束输入，则进行传输
        //创建数据，然后将数据打包
        byte[] bys = line.getBytes();
        DatagramPacket dp = new DatagramPacket(bys, bys.length, InetAddress.getByName("10.15.73.175"),10086);
        //调用DatagramSocket对象发送
        ds.send(dp);
    }
    //释放资源
    br.close();
    //关闭发送端
    ds.close();
}
```

```Java
//接收端
public static void main(String[] args) throws IOException {
    //创建Socket对象(DatagramSocket)
    DatagramSocket ds = new DatagramSocket(10086);

    while (true) { //不知发送端何时停止，死循环不断接收数据

        //创建字节数组接收到数据包(相当于缓冲区)
        byte[] bys = new byte[1024];
        DatagramPacket dp = new DatagramPacket(bys, bys.length);

        //调用DatagramSocket对象的方法接收 数据包
        ds.receive(dp);

        //解析数据包 用字节数组接收并把数据再控制台显示
        byte[] data = dp.getData();
        int len = dp.getLength();
        System.out.println(new String(data, 0, len));
    }
}
```

**当运行多个发送端时就有聊天室的效果！！**

#### TCP协议

![](C:\Users\panqiyi\Desktop\notes\image\1img\34.png)

##### TCP发送

客户端发送时以IO流方式进行发送；

![](C:\Users\panqiyi\Desktop\notes\image\1img\35.png)

```Java
/*1、创建Socket对象
* 2、调用方法获取字节输出流，然后写入数据
* 3、释放资源*/
public static void main(String[] args) throws IOException {
    //1、创建Socket对象，并指定目的地主机与端口
    //Socket sk = new Socket(InetAddress.getByName(" 10.24.130.60"), 10000);
    //可以直接传入目的地主机字符串ip地址，底层与上面一样
    Socket sk = new Socket(" 10.24.130.60", 10000);

    //获取字节输出流,并写入数据
    OutputStream os = sk.getOutputStream();
    os.write("你好啊！！".getBytes());

    //释放资源
    os.close();
}
```

##### TCP接收

服务端以IO流方式接收

![](C:\Users\panqiyi\Desktop\notes\image\1img\36.png)

```Java
public static void main(String[] args) throws IOException {
    //创建服务端ServerSocket对象，并传入对应客户端的端口
    ServerSocket ssk = new ServerSocket(16000);

    //Socket accept() 侦听要连接到此套接字并接受它。
    //这个就是在握手时监听到客户端的操作并给予回应

    Socket at = ssk.accept();   //返回Socket类型

    //调用Socket对象方法获取字节输入流，并读取数据
    InputStream is = at.getInputStream();

    byte[] bys = new byte[1024];
    int len = is.read(bys);

    System.out.println(new String(bys, 0, len));
    //释放资源
    ssk.close();
}
```

##### TCP通信练习

**案例1：**

![](C:\Users\panqiyi\Desktop\notes\image\1img\37.png)

客户端：写入数据--->读取服务器反馈

服务器：读取数据---->写入反馈信息

```java
//客户端
public static void main(String[] args) throws IOException {
    //创建Socket对象,并确认主机：传入目的主机ip与端口
    Socket sk = new Socket("10.24.130.60", 18800);

    //获取字节输出流，写入数据
    OutputStream os = sk.getOutputStream();
    os.write("hello!!你好啊".getBytes());

    //创建字节输入流，读取服务器端传来的反馈
    InputStream data = sk.getInputStream();
    byte[] bys = new byte[1024];
    int len = data.read(bys);
    System.out.println("服务器传来："+new String(bys,0,len));

   // os.close();
    //data.close();
    sk.close();   //只需要释放这个即可，其他的也是有Socket对象产生 的
}
```

```Java
//服务器端
public static void main(String[] args) throws IOException {
    //创建服务器端ServerSocket对象。并传入对应客户端的端口
    ServerSocket ssk = new ServerSocket(18800);

    //调用方法监听客户端连接
    Socket s = ssk.accept();

    //获取字节输入流，读取数据
    InputStream is = s.getInputStream();
    byte[] bys = new byte[1024];
    int len = is.read(bys);
    System.out.println(new String(bys,0,len));

    //获取字字节输出流，写入数据给客户端发送反馈
    OutputStream os = s.getOutputStream();
    os.write("数据已经收到了！".getBytes());

    //关闭接收，释放资源
    ssk.close();
}
```

**案例2：**

1、客户端自己封装一个键盘输入，封装一个字符缓冲输出流向服务端写入字符；

2、自己封装一个字符缓冲输入流读取客户端传来的字符。

注意：字符缓冲流只能局限于字符的传输；如图片、视频等都需字节流；

```Java
//客户端
public static void main(String[] args) throws IOException {
    // 创建客户端Socket对象，并确定目的地主机：ip与端口
    Socket sk = new Socket("10.15.73.175", 16999);

    //获取字节输出流，写入数据
    OutputStream os = sk.getOutputStream();
    //自己封装一个键盘输入类    ;  字符缓冲流---> 字符流 --> 字节流  ；System.in返回值为InputStream
    BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
    // 封装一个字符缓冲输出流，
    BufferedWriter bw = new BufferedWriter(new OutputStreamWriter(sk.getOutputStream()));

    String line;
    while ((line=br.readLine())!=null){
        if ("886".equals(line)){
            break;
        }
        // os.write(line.getBytes());  //方式1、按字节输出流写入
        bw.write(line);   //方式2、按字符缓冲输出流写入，这个只能对于字符类型，如图片，视频等等用字节流
        bw.newLine();
        bw.flush();
    }
    sk.close();
}
```

```Java
//服务端
public static void main(String[] args) throws IOException {
    //创建服务端Socket(ServerSocket)对象，并传入对应端口号
    ServerSocket ssk = new ServerSocket(16999);

    Socket s = ssk.accept();

    // 对应方式1、字节输入流接收客户端数据
    /*InputStream is = s.getInputStream();
    byte[] bys = new byte[1024];
    int len;
    while ((len=is.read(bys))!=-1){
        System.out.println(new String(bys,0,len));
    }*/

    //对应方式2、封装一个字符缓冲输入流，读取传来的数据
    BufferedReader br = new BufferedReader(new InputStreamReader(s.getInputStream()));

    String line;
    while ((line=br.readLine())!=null){
        System.out.println(line);
    }

    //关闭接收，释放资源
    ssk.close();
}
```

**案例3:**

1、客户端自己封装一个键盘输入，使用字节缓冲流写入

2、服务端使用字节缓冲流读取，并使用字节缓冲流将读取的数据写入文件；

```java
//客户端
public static void main(String[] args) throws IOException {
    //创建客户端Socket对象，并指定目标服务器的IP与端口
    Socket sk = new Socket("10.24.128.92", 16666);

    //Socket对象获取输出流，并写入数据给服务端
    OutputStream os = sk.getOutputStream();
    BufferedOutputStream bos=new BufferedOutputStream(os);//字节缓冲流
    //封装一个键盘输入
    BufferedReader br=new BufferedReader(new InputStreamReader(System.in));

    String len;
    while ((len=br.readLine())!=null){
        if ("886".equals(len)){
            break;
        }
        os.write(len.getBytes());
    }
    sk.close();
}
```

```Java
//服务端
public static void main(String[] args) throws IOException {
    //创建服务器端Socket对象（ServerSocket）,并指定对应端口
    ServerSocket ssk = new ServerSocket(16666);

    //调用accept()方法监控客户端连接,并返回Socket对象
    Socket s = ssk.accept();
    //Socket对象调用字节输入流读取客户端发来的数据
    InputStream is = s.getInputStream();
    BufferedInputStream bs = new BufferedInputStream(is);
    //创建字节输出流将数据写入文件
    FileOutputStream fos = new FileOutputStream("C:\\Users\\panqiyi\\Desktop\\abc\\888.txt");
    BufferedOutputStream bos=new BufferedOutputStream(fos);

    byte[] bys = new byte[1024];
    int len;
    while ((len=bs.read(bys))!=-1){
        System.out.println(new String(bys,0,len));
        bos.write(bys,0,len);
    }
    bos.close();
    ssk.close();
}
```

**案例4：**

1、客户端数据来自文件

2、服务端将接收的数据写入文件

```Java
//客户端
public static void main(String[] args) throws IOException {
    Socket sk = new Socket("10.15.73.175", 45342);

    //创建字符缓冲流，读取指定文件
    BufferedReader br = new BufferedReader(new FileReader("C:\\Users\\panqiyi\\Desktop\\abc\\soc.txt"));

    //获取字节输出流，并封装为字符缓冲流
    BufferedWriter bw = new BufferedWriter(new OutputStreamWriter(sk.getOutputStream()));

    //读指定要发送的文件，写入给服务器
    String line;
    while ((line=br.readLine())!=null){
        bw.write(line);
        bw.newLine();
        bw.flush();
    }
    br.close();
    sk.close();
}
```

```Java
//服务器
public static void main(String[] args) throws IOException {
    ServerSocket ssk = new ServerSocket(45342);

    //监听客户端连接，并返回Socket对象
    Socket s = ssk.accept();

    //获取字节输入流，并封装为字符缓冲流
    BufferedReader br = new BufferedReader(new InputStreamReader(s.getInputStream()));
    //创建字符缓冲输出流，将从客户端读取的数据写入指定文件
    BufferedWriter bw = new BufferedWriter(new FileWriter("C:\\Users\\panqiyi\\Desktop\\abc\\ssk.txt"));

    //读客户端传来数据，写入指定文件
    String line;
    while ((line=br.readLine())!=null){
        bw.write(line);
        bw.newLine();
        bw.flush();
    }
    bw.close();
    ssk.close();
}
```

**案例5：**

(在案例4的基础增加了反馈)

1、客户端数据来自文件，接收反馈！

2、服务端将接收的数据写入文件，发送反馈！

注意：使用Socket对象的shutdownOutput()可以告知写入结束；

```Java
//客户端
public static void main(String[] args) throws IOException {
    Socket sk = new Socket("10.15.73.175", 45342);

    //创建字符缓冲流，读取指定文件
    BufferedReader br = new BufferedReader(new FileReader("C:\\Users\\panqiyi\\Desktop\\abc\\oo.txt"));

    //获取字节输出流，并封装为字符缓冲流
    BufferedWriter bw = new BufferedWriter(new OutputStreamWriter(sk.getOutputStream()));

    //读指定要发送的文件，写入给服务器
    String line;
    while ((line=br.readLine())!=null){
        bw.write(line);
        bw.newLine();
        bw.flush();
    }

    //写入数据结束标记；这样服务器就不会一直等待，
    // 也避免先执行了下面的接收语句而为执行服务器的反馈导致异常
    sk.shutdownOutput();

    //接收服务器反馈
    BufferedReader brf = new BufferedReader(new InputStreamReader(sk.getInputStream()));
    System.out.println(brf.readLine());

    br.close();
    sk.close();
}
```

```Java
//服务端
public static void main(String[] args) throws IOException {
    ServerSocket ssk = new ServerSocket(45342);

    //监听客户端连接，并返回Socket对象
    Socket s = ssk.accept();

    //获取字节输入流，并封装为字符缓冲流
    BufferedReader br = new BufferedReader(new InputStreamReader(s.getInputStream()));
    //创建字符缓冲输出流，将从客户端读取的数据写入指定文件
    BufferedWriter bw = new BufferedWriter(new FileWriter("C:\\Users\\panqiyi\\Desktop\\abc\\ss.txt"));

    //读客户端传来数据，写入指定文件
    String line;
    while ((line=br.readLine())!=null){
        bw.write(line);
        bw.newLine();
        bw.flush();
    }

    //给客户端反馈
    BufferedWriter bwk = new BufferedWriter(new OutputStreamWriter(s.getOutputStream()));
    bwk.write("服务器：数据已经收到！");
    bwk.newLine();
    bwk.flush();

    bw.close();
    ssk.close();
}
```

**案例6：**

1、客户端：数据来自文件，接收反馈！

2、服务器：接收到的数据写入文件，给出反馈，代码用线程进行封装，为每一个客户端开启一个线程。

```Java
//客户端
public static void main(String[] args) throws IOException {
    Socket sk = new Socket("10.15.73.175", 45342);

    //创建字符缓冲流，读取指定文件
    BufferedReader br = new BufferedReader(new FileReader("C:\\Users\\panqiyi\\Desktop\\abc\\oso.txt"));

    //获取字节输出流，并封装为字符缓冲流
    BufferedWriter bw = new BufferedWriter(new OutputStreamWriter(sk.getOutputStream()));

    //读指定要发送的文件，写入给服务器
    String line;
    while ((line=br.readLine())!=null){
        bw.write(line);
        bw.newLine();
        bw.flush();
    }

    //写入数据结束标记；这样服务器就不会一直等待，
    // 也避免先执行了下面的接收语句而为执行服务器的反馈导致异常
    sk.shutdownOutput();

    //接收服务器反馈
    BufferedReader brf = new BufferedReader(new InputStreamReader(sk.getInputStream()));
    System.out.println(brf.readLine());

    br.close();
    sk.close();
}
```

```Java
//服务器
public static void main(String[] args) throws IOException {
    ServerSocket ssk = new ServerSocket(45342);

    while (true) {
        //监听客户端连接，并返回Socket对象
        Socket s = ssk.accept();
        //使用线程线程封装，每一个客户端上传文件，就会调用一个客户端线程
        new Thread(new ServerTreads(s)).start();
    }
}
```

```Java
//ServerTreads线程类
public class ServerTreads implements Runnable {
    private Socket s;  //成员变量作用整个类
    public ServerTreads(Socket s) {//传入Socket对象
        this.s=s;   //将传入Socket对象赋值给成员变量
    }

    @Override
    public void run() {
        try {//处理异常
            //接收客户端传来数据
            BufferedReader br = new BufferedReader(new InputStreamReader(s.getInputStream()));

            //写入文件,避免每个线程文件名重复
            int count=0;
            File file = new File("C:\\Users\\panqiyi\\Desktop\\abc\\oso[" + count + "].txt");
            while (file.exists()){
                count++;
                file=new File("C:\\Users\\panqiyi\\Desktop\\abc\\oso[" + count + "].txt");
            }
            BufferedWriter bw = new BufferedWriter(new FileWriter(file));
            String line;
            while ((line=br.readLine())!=null){
                bw.write(line);
                bw.newLine();
                bw.flush();
            }

            //给出反馈
            BufferedWriter bwk = new BufferedWriter(new OutputStreamWriter(s.getOutputStream()));
            bwk.write("服务器：文件上传成功！");
            bwk.newLine();
            bwk.flush();

            //释放资源
            s.close();

        }catch(IOException e){
            e.printStackTrace();
        }
    }
}
```

### JDK新特性

#### Lambda表达式

1.8新特性；具体前面Lambda专题已经写过。

#### 接口新特性

java7:  接口包含  1、常量  2、抽象方法

Java8：增加 3、默认方法、4、静态方法

Java9：增加 5、私有方法

具体前面接口专题写过。

#### 方法引用

简化Lambda表达式

方法引用符

::      

该符号为引用运算符，它所在的表达式称为方法引用；

```Java
public interface Printable { //接口
    void printString(String s);
}

//测试类
public static void main(String[] args) {
    //调用方法
    usePrintable(new Printable() {
        @Override
        public void printString(String s) {
            System.out.println(s);
        }
    });
    //Lambda表达式调用
    usePrintable( s-> System.out.println(s));

    //方法引用调用
    usePrintable(System.out::println);
}
private static void usePrintable(Printable s){
    s.printString("你好 世界！");
}
```

```Java
//Lambda表达式调用
    usePrintable( s-> System.out.println(s));
//将参数s 传给(->) 后面的方法体

    //方法引用调用
    usePrintable(System.out::println);
//直接使用了System.out的println方法；省略了 参数传递给方法体的过程，但作用是一样的
```
方法引用与Lambda类似，只是实现方式不同，代码更加简洁；

**1、引用类方法**

即引用类的静态方法；

格式：类名::静态方法

```Java
//接口
public interface Printable {
    String printString(int s);
}
```

```Java
//测试类
public static void main(String[] args) {
    //普通调用
    usePrint(new Printable() {
        @Override
        public String printString(int s) { //重写接口的抽象方法
            return Integer.toString(s);
            //Integer类中静态方法toSring()将字符型数字转化为int型
            //Integer类中静态方法parseInt()将int数字转化为字符型
        }
    });
    //Lambda表达式调用
    usePrint(s -> Integer.toString(s));

    //引用类方法
    usePrint(Integer::toString);
    //形参(如这里的s)全部都会传到静态方法作为参数
}
private static void usePrint(Printable p){
    String s = p.printString(666);  //int 666
    //内部类重写抽象方法返回需求
    System.out.println(s+"hello");  // 666hello
}
```

**2、引用对象的实例方法**

即引用类中的成员方法

格式：对象::成员方法

```Java
public interface Printer {
    void printUpperCase(String s);
}
```

```Java
public class PrinterDemo {
    public static void main(String[] args) {
        //Lambda
        usePrinter((String s)-> {
            String s1 = s.toUpperCase();
            System.out.println(s1);
        }
        );
        //Lambda简写
        usePrinter(s-> System.out.println(s.toUpperCase()));

        //引用对象的实例方法
        PrintString ps = new PrintString();
        usePrinter(ps::printUpper);

        //Lambda表达式被对象的实例方法替代时，它的形参全部传递给该方法作为参数
    }
    private static void usePrinter(Printer p){
        p.printUpperCase("qwert");
    }
}
```

```Java
public class PrintString {
    //定义这个类的printUpper()方法用于将字符串转化为大写
    public void printUpper(String s){
        String s1 = s.toUpperCase();
        System.out.println(s1);
    }
}
```

**3、引用类的实例方法**

即引用类的成员方法

格式：类名::成员方法

```Java
public interface MyString {
    String mySubString(String s,int x,int y);
}
```

```Java
public class MyStringDemo {
    public static void main(String[] args) {
        //Lambda表达式
        useMyString((s, x, y) -> s.substring(x,y) );

        //引用类实例方法
        useMyString(String::substring);

        //第一个参数是调用者，后面两个是传递给方法作为参数
    }
    public static void useMyString(MyString m){
        String h = m.mySubString("helloworld", 2, 6);//内部类重写抽象方法返回需求
        System.out.println(h); // llow
    }
}
```

**4、引用构造器方法**

即引用构造方法

格式：类名::new

```Java
//标准Student类
public class Student {
    private String name;
    private int age;
    ……
    }
```

```Java
//接口
public interface StudentBuilder {
    Student build(String name,int age);
}
```

```Java
//测试类
public class StudentDemo {
    public static void main(String[] args) {
        //简化Lambda表达式
        useStudentBuilder(( name, age)-> new Student(name,age));

        //引用构造方法
        useStudentBuilder(Student::new);

    }
    private static void useStudentBuilder(StudentBuilder sb){
        Student b = sb.build("令狐冲", 35);  //内部类重写返回Student类对象
        System.out.println(b.getName()+","+b.getAge());
    }
    }
```

#### 函数式接口

函数式接口：有且仅有一个抽象方法的接口

java的函数式编程体现 就是Lambda表达式，所以函数式接口就是适用于Lamada使用的接口，只有确保接口中有且仅有一个抽象方法，Java中的Lambda表达式才能顺利的进行推导。

```Java
@FunctionalInterface
//添加函数式接口注解，保证此接口是函数式接口，只能允许一个抽象方法，否则编译失败。
public interface MyInterface { 
    void show();
}
```

```Java
public class MyInterfaceDome {
    public static void main(String[] args) {
        //重写接口抽象方法，赋值给局部变量
        MyInterface m=()-> System.out.println("重写接口抽象方法！");
        //通过接口类型m调用重写后的抽象方法
        m.show();
    }
}
```

**函数式接口作为方法的参数**

```Java
public static void main(String[] args) {
    startTread(new Runnable() {
        @Override
        public void run() {
            System.out.println(Thread.currentThread().getName()+"线程启动！");
        }
    });
    
    //Lambda表达式
    startTread(()-> System.out.println(Thread.currentThread().getName()+"线程启动！！"));

}
public static void startTread(Runnable r){
    new Thread(r).start();
}
```

**函数式接口作为方法返回值**

Comparator比较器是一个函数式接口

```Java
public static void main(String[] args) {
    ArrayList<Integer> list = new ArrayList<>();
    list.add(22);
    list.add(11);
    list.add(66);
    list.add(44);

    System.out.println(list);
    
    //Collections下的sort方法自然排序(升序)
    Collections.sort(list);
    System.out.println(list);
    
    //Collections下的sort方法,使用Comparator比较器比较大小
    Collections.sort(list,getComparator());
    System.out.println(list);
}
public static Comparator<Integer> getComparator(){ //返回接口对象
    return new Comparator<Integer>() {
        @Override
        public int compare(Integer t1, Integer t2) {
            return t2-t1; //降序
        }
    };
    //这里可以用Lambda表达式更加简洁；
    return (t1,t2)-> t2-t1;
}
```

##### Supplier

生产接口：

![](C:\Users\panqiyi\Desktop\notes\image\1img\39.png)

```java 
public static void main(String[] args) {
    //返回字符串
    String s= getSupplier(new Supplier<String>() {
        @Override
        public String get() {
            return "你好";
        }
    });
    //Lambda表达式
    //String s=getSupplier(()->"你好啊！");
    System.out.println(s);
    
    //重写匿名内部类，返回指定数据
    //返回类对象
    Student st=getStudent(()->new Student("李小龙",29));
    System.out.println(st);
}
public static String getSupplier(Supplier<String> s){
    return s.get();
}

public static Student getStudent(Supplier<Student> s){
    return s.get();
}
```

**案例：**

```Java
public static void main(String[] args) {
    int[] arr={12,66,34,56,26};

    int m = getMax(()->{
        int max=arr[0];
        for (int i = 1; i < arr.length; i++) {
            if (arr[i]>max){
                max=arr[i];
            }
        }
        return max;
    });
    System.out.println(m);

}
//返回一个数组中的最大值
public static int getMax(Supplier<Integer> sp){
    return sp.get();
}
```

##### Consumer

消费接口

accept(T t)   在此方法里面对传入的参数进行一系列操作

![](C:\Users\panqiyi\Desktop\notes\image\1img\40.png)

```Java
public static void main(String[] args) {
    // 调用方法，并匿名内部类重写接口的accept方法
    operatorString("林青霞",s -> System.out.println(s));

    System.out.println("-----------------");

    operatorString("张国荣",s -> System.out.println(s),s -> System.out.println(new StringBuilder(s).reverse().toString()));
}
//reverse() StringBuilder的字符串反转
private static void operatorString(String name, Consumer<String> con){
    con.accept(name);  // 传入字符串name, accept将其视为参数 如这里为 accept(String s)
}

//一个字符串做两次操作
private static void operatorString(String name, Consumer<String> con1,Consumer<String> con2){
    // con1.accept(name);
   //  con2.accept(name);
    //等同于下面的方法，依次进行两个操作
    con1.andThen(con2).accept(name);
}
```

**案例：**

String[ ]    atrArray={"林青霞 , 25", "张曼玉 , 27 ","王祖贤 , 28"}

字符串数组中有多条信息，请按照格式：姓名：xx   年龄：xx   打印出来

1、把打印姓名作为第一个Consumer接口的Lambda实例

2、把打印年龄作为第二个Consumer接口的Lambda实例

3、将两个Consumer接口按照顺序组合一起使用

```Java
public static void main(String[] args) {
    String[] strArray={"林青霞,25","张曼玉,27","王祖贤,28"};

   printInfo(strArray,s -> {
      String name= s.split(",")[0];  //s.split(",") 分割为字符串数组
       System.out.print("姓名："+name+"\t");
   },s -> {
       int age=Integer.parseInt(s.split(",")[1]);
       System.out.println("年龄："+age);
   });

   // 可简化
    printInfo(strArray,s -> System.out.print("姓名："+ s.split(",")[0]+"\t")
    ,s -> System.out.println("年龄："+Integer.parseInt(s.split(",")[1])));
}

private static void printInfo(String[] strArray, Consumer<String> con1,Consumer<String> con2){
    //遍历字符串数组，得出每一个字符串 如 "林青霞,25"
    for (String s : strArray) {
        con1.andThen(con2).accept(s);   //两个操作依次对同一个字符串进行
    }
}
```

##### Predicate

判断接口

![](C:\Users\panqiyi\Desktop\notes\image\1img\41.png)

```java 
public static void main(String[] args) {
    boolean b= checkString("hello", s -> s.length() > 8);
    System.out.println(b); //正常为 true  

    boolean b2 = checkString("helloworld", s -> s.length() > 8);
    System.out.println(b2);
}
private static boolean checkString(String s, Predicate<String> p){
  // return p.test(s);   // 正常判断
   return p.negate().test(s);   // 逻辑否定，对应 逻辑非 ！
}
```

```Java
public static void main(String[] args) {
        boolean b = checkString("helloworld", s -> s.length() < 8, s -> s.length() < 15);
        System.out.println(b);
    }

    // 对同一个字符串给出不同的判断条件，最后把这两个判断条件的结果做逻辑运算的结果作为最后结果返回
    private static boolean checkString(String s, Predicate<String> p1,Predicate<String> p2){
//        boolean b1=p1.test(s);
//        boolean b2=p2.test(s);
//        boolean b3=b1 && b2;
//        return b3;
        // 效果与下面相同
       // return p1.and(p2).test(s);  // 短路与  &&
        return p1.or(p2).test(s);   //  对应短路或  ||
    }
```

**案例：**

![](C:\Users\panqiyi\Desktop\notes\image\1img\42.png)

```java
public static void main(String[] args) {
    String[] strArray={"林青霞,30","刘岩,34","张曼玉,35","貂蝉,31","王祖贤,33"};

    ArrayList<String> array = myFilter(strArray,
            s -> s.split(",")[0].length()>2,
            s -> Integer.parseInt(s.split(",")[1])>33);

    for (String s : array) { //遍历满足两个条件存储在集合中的元素
        System.out.println(s);
    }

}

private static ArrayList<String> myFilter(String[] strArray, Predicate<String> p1,Predicate<String> p2){
    //创建一个集合，用来存储判断后的数据
    ArrayList<String> array = new ArrayList<>();
    for (String s : strArray) {
        if (p1.and(p2).test(s)){ //满足这两个条件的存储到集合中
            array.add(s);
        }
    }
    return array;
}
```

##### Function<T,R>

处理，转换参数接口

T：输入类型  R：输出类型

![](C:\Users\panqiyi\Desktop\notes\image\1img\43.png)

```Java
public static void main(String[] args) {

        conversion("100", s -> Integer.parseInt(s));   //String->int

        convertion(100, i -> String.valueOf(i+456));  // int->String

        convertion("111",s -> Integer.parseInt(s),integer -> Integer.toString(integer+555));

    }

    //定义一个方法，把字符串转换为int类型，并在 控制台输出 ： String-->int
    public static void conversion(String s, Function<String, Integer> f) {
        Integer i = f.apply(s);   //apply  Lambda重写该方法对参数进行操作
        System.out.println(i);
    }

    //定义一个方法，把一个int类型数据加上一个整数后，转换为字符串输出： int -->String
    public static void convertion(int i, Function<Integer, String> f) {
        String s = f.apply(i);
        System.out.println(s);
    }

    //定义一个方法，把一个字符串转换为int类型, 然后在加上一个整数后转化为字符串输出 ：String->int  int->String
    public static void convertion(String s,Function<String,Integer> f1,Function<Integer,String> f2){
//        Integer i = f1.apply(s);  //返回Integer i
//        String ss = f2.apply(i);  // 传入i  返回String  ss
//        System.out.println(ss);

        String ss = f1.andThen(f2).apply(s); //作用与上一样
        System.out.println(ss);
    }
```

#### Stream流

**体验：**

集合1  有一系列姓名 --> 集合2 储存从集合1中过滤的性张的姓名 ----> 集合3 储存性张且字符串长度为3的姓名

```Java
public static void main(String[] args) {
    ArrayList<String> list1=new ArrayList<>();
    list1.add("张曼玉");
    list1.add("林青霞");
    list1.add("陈真");
    list1.add("张国荣");
    list1.add("张三");

    ArrayList<String> list2=new ArrayList<>();

    //遍历集合1，姓张的储存到集合2
    for (String s : list1) {
        if (s.startsWith("张")){
            list2.add(s);
        }
    }
    System.out.println(list2);

    //遍历集合2，名字长度为3则储存到集合3

    ArrayList<String> list3=new ArrayList<>();

    for (String s : list2) {
        if (s.length()==3){
            list3.add(s);
        }
    }

     //遍历集合3
        for (String s : list3) {
            System.out.println(s);
        }
       // list3.forEach(s -> System.out.println(s));

        //使用Stream流改进
        list1.stream().filter(s -> s.startsWith("张")).filter(s -> s.length()==3).forEach(s -> System.out.println(s));
 
}
```

![](C:\Users\panqiyi\Desktop\notes\image\1img\44.png)

**Stream流的使用：**

1、生成流 -----> 2、中间操作 -----> 3、终结操作

![](C:\Users\panqiyi\Desktop\notes\image\1img\45.png)

**生成Stream流的几种常见方式**

![](C:\Users\panqiyi\Desktop\notes\image\1img\46.png)

```Java
public static void main(String[] args) {
    // Collection体系的集合可以使用默认方法stream()  生成流
    List<String> list=new ArrayList<>(); //多态
    Stream<String> listStream = list.stream();

    Set<String> set=new HashSet<>();
    Stream<String> setStream = set.stream();

    
    //Map体系的集合间接的生成流
    Map<String,Integer> map=new HashMap<>();
    Stream<String> keyStream = map.keySet().stream();   //map.keySet() 返回储存在Set集合中的键集

    Stream<Integer> valueStream = map.values().stream();  // map.values 返回储存在Collection下的集合的（多态） 值集

    Stream<Map.Entry<String, Integer>> entryStream = map.entrySet().stream();  // map.entrySet() 返回键值对集合储存在Set集合

    
    // 数组可以通过Stream接口的静态方法of(T……values) 生成流
    String[] atrArray = {"hello","world","java"};
    Stream<String> strArrayStream = Stream.of(atrArray);
    // 可以直接传入数组的数据
    Stream<String> arrayStream = Stream.of("hello", "world", "java");
}
```

**Stream流的中间操作**

**1、filter判断过滤**

![](C:\Users\panqiyi\Desktop\notes\image\1img\47.png)

```java 
public static void main(String[] args) {
    ArrayList<String> list=new ArrayList<>();
    list.add("张曼玉");
    list.add("林青霞");
    list.add("陈真");
    list.add("张国荣");
    list.add("张三");

    //1、把list集合中张开头的元素在控制台输出
    list.stream().filter(s -> s.startsWith("张")).forEach(System.out::println);
    System.out.println("-----------------------------");

    //2、把list集合中长度为3的元素在控制台输出
    list.stream().filter(s -> s.length()==3).forEach(System.out::println);
    System.out.println("-----------------------------");

    //3、把集合中以张开头，长度为3 的元素在控制台输出
    list.stream().filter(s -> s.startsWith("张")).filter(s -> s.length()==3).forEach(System.out::println);

}
```

**2、limit()截取 skip()跳过**

```Java
public static void main(String[] args) {
        ArrayList<String> list=new ArrayList<>();
        list.add("张曼玉");
        list.add("林青霞");
        list.add("陈真");
        list.add("张国荣");
        list.add("张三");
        list.add("周杰伦");

        //1、截取前3个数据在控制台输出
        list.stream().limit(3).forEach(System.out::println);
        System.out.println("-------------");

        //2、跳过3个元素，把后面的在控制台输出
        list.stream().skip(3).forEach(System.out::println);
        System.out.println("-------------");

        //3、跳过2个元素，把剩下的前2个在控制台输出
        list.stream().skip(2).limit(2).forEach(System.out::println);
    }
```

**3、concat()合并流  distinct()去重**

接口下的静态方法concat()  ： 需接口调用

默认方法distinct()；

![](C:\Users\panqiyi\Desktop\notes\image\1img\48.png)

```Java
public static void main(String[] args) {
    ArrayList<String> list=new ArrayList<>();
    list.add("张曼玉");
    list.add("林青霞");
    list.add("陈真");
    list.add("张国荣");
    list.add("张三");
    list.add("周杰伦");

    //1、取前4个元素组成一个流
    Stream<String> s1 = list.stream().limit(4);
    //1、跳过2个数据组成一个流
    Stream<String> s2 = list.stream().skip(2);

    //3、合并1、2两个流得到流, 并把结果在控制台上输出
    Stream.concat(s1,s2).forEach(System.out::println);

    //4、合并1、2两个流得到流, 并把结果在控制台上输出，要求字符串不能重复
    Stream.concat(s1,s2).distinct().forEach(System.out::println);
}
```

**sorted() 排序**

![](C:\Users\panqiyi\Desktop\notes\image\1img\49.png)

```java 
public static void main(String[] args) {
    ArrayList<String> list = new ArrayList<>();
    list.add("f张曼玉");
    list.add("s林青霞");
    list.add("s陈真");
    list.add("a张国荣");
    list.add("w张三");
    list.add("z周杰伦");

    //1、按照字母顺序把数据在控制台输出
    list.stream().sorted().forEach(System.out::println);

    System.out.println("-----------------------");

    //2、按照字符串长度把数据在控制台输出
    list.stream().sorted((s1, s2) -> {
        int num1 = s1.length() - s2.length();
        int num = num1 == 0 ? s1.compareTo(s2) : num1;  //字符串长度相等时按照首字母升序
        return num;
    }).forEach(System.out::println);
}
```

**map()  与 mapToInt()**

![](C:\Users\panqiyi\Desktop\notes\image\1img\50.png)

map()  对每个输入元素，都按照规则转换成为另外一个元素

mapToInt()  返回IntStream流，有上面的转换效果，还有IntStream接口自己的一写方法；

```java 
//通过在map() 方法中 写入方法将每个元素转换为大写
//1：1的映射，a->A s->S d->D ……
public static void main(String[] args) {
    ArrayList<String> list = new ArrayList<>();

    list.add("asdfghhjk");

    list.stream().map(String::toUpperCase).forEach(System.out::println);
}
```



```Java
public static void main(String[] args) {
    ArrayList<String> list = new ArrayList<>();
    list.add("10");
    list.add("20");
    list.add("30");
    list.add("40");
    list.add("50");

    //1、将集合中字符串数据转换为整数后在控制台输出
   // list.stream().map(s -> Integer.parseInt(s)).forEach(System.out::println);
    list.stream().map(Integer::parseInt).forEach(System.out::println);

    //2、返回此流中元素的总和   int  sum()
    int result = list.stream().mapToInt(Integer::parseInt).sum();
    System.out.println(result);
}
```



**终结操作**

**forEach与count**

count() 统计元素个数

```java 
public static void main(String[] args) {
    ArrayList<String> list=new ArrayList<>();
    list.add("张曼玉");
    list.add("林青霞");
    list.add("陈真");
    list.add("张国荣");
    list.add("张三");
    list.add("周杰伦");
    
    //直接输出集合
    list.stream().forEach(System.out::println);
    //输出姓张的有多少人
    long z = list.stream().filter(s -> s.startsWith("张")).count();
    System.out.println(z);
}
```

**练习**

```Java
public class Star {
    private String name;
    省略 有无参构造方法/get/set/toString重写
    }
```

```Java
public static void main(String[] args) {
    ArrayList<String> list=new ArrayList<>();
    list.add("张曼玉");
    list.add("林青霞");
    list.add("陈真");
    list.add("张国荣");
    list.add("张三");
    list.add("周杰伦");

    //将集合元素作为参数传入类的构造方法，返回该类的对象
    list.stream().map(Star::new).forEach(star -> System.out.println(star.getName()));

}
```



```Java
public class Star {
    private String name;
    private int age;
    省略 有无参构造方法/get/set/toString重写
    }
```

```Java
public static void main(String[] args) {
    ArrayList<String> list=new ArrayList<>();
    list.add("张曼玉,34");
    list.add("林青霞,23");
    list.add("陈真,45");
    list.add("张国荣,27");
    list.add("张三,35");
    list.add("周杰伦,36");

    //将集合元素作为参数传入类的构造方法，返回该类的对象
    list.stream().map(s -> new Star(s.split(",")[0],Integer.parseInt(s.split(",")[1]))).forEach(star -> System.out.println(star.getName()+","+star.getAge()));

}
```



**Stream收集操作**

将流收集到集合中

![](C:\Users\panqiyi\Desktop\notes\image\1img\52.png)

```java 
public static void main(String[] args) {
    //List
    ArrayList<String> list = new ArrayList<>();
   list.add("张曼玉");
   list.add("林青霞");
   list.add("王祖贤");
   list.add("李白");
   //1、得到名字长度为3的流
    Stream<String> listStream = list.stream().filter(s -> s.length() == 3);
    //2、把使用Stream流对数据操作完毕后；将流收集到list集合中并遍历
    List<String> names = listStream.collect(Collectors.toList());
    for (String name : names) {
        System.out.println(name);
    }


    //1、创建Set集合对象
    HashSet<Integer> set = new HashSet<>();
    set.add(10);
    set.add(15);
    set.add(25);
    set.add(30);
    //2、得到元素大于12的流
    Stream<Integer> setStream= set.stream().filter(s -> s > 12);
    //3、把使用Stream流对数据操作完毕后；将流收集到Set集合中并遍历
    Set<Integer> ages = setStream.collect(Collectors.toSet());
    ages.forEach(System.out::println);


    //1、定义一个字符串数组
    String[] strArray={"林超贤,45","林青霞,25","张曼玉,26","李白,66"};
    //2、得到字符串中年龄大于28的流
    Stream<String> arrStream = Stream.of(strArray).filter(s -> Integer.parseInt(s.split(",")[1]) > 28);
    //3、把使用Stream流对数据操作完毕后；将流收集到 Map集合中并遍历，姓名做键，年龄为值
    Map<String, String> map = arrStream.collect(Collectors.toMap(s -> s.split(",")[0], s -> s.split(",")[1]));
    Set<Map.Entry<String, String>> ent = map.entrySet();
    for (Map.Entry<String, String> se : ent) {
        System.out.println(se.getKey()+","+se.getValue());
    }
}
```



### 反射

#### 类加载器

**1、类加载**

当程序要使用某个类时，如果该类还未被加载到内存中，则系统会通过 ： **类的加载 --> 类的连接 --> 类的初始化**  三个步骤来对类进行初始化。如果不出意外，JVM会连续完成了三个步骤；有时也将这三个步骤称为类加载或类初始化

<img src="C:\Users\panqiyi\Desktop\notes\image\1img\53.png" style="zoom:80%;" />

![](C:\Users\panqiyi\Desktop\notes\image\1img\54.png)

![](C:\Users\panqiyi\Desktop\notes\image\1img\55.png)

#### 反射概述

![](C:\Users\panqiyi\Desktop\notes\image\1img\56.png)

再看看类

![](C:\Users\panqiyi\Desktop\notes\image\1img\57.png)

**Java反射机制：**是指在运行时去获取一个类的变量和方法信息；然后通过获取到的信息(Class类)来创建对象，调用方法的一种机制。

由于这种动态性，可以极大增强程序的灵活性，程序不用在编译期就完成确定，在运行期仍然可以扩展。

##### 获取Class类对象

想要通过反射去使用某个类，首先要获取到该类的字节码文件对象 ------> 即Class类对象

1、通过类名访问class属性来获取该类的对应对象。

如：Student.class 返回Student类对应的Class对象；

2、调用对象的getClass()方法，返回**该对象**所属类对应的Class对象。

该方法是Object类中的方法，所有的Java对象都可以调用该方法；

3、使用Class类中的静态方法forName(String className) , 该方法需要传入某个类的全路径字符串参数，即包含完整包名的路径

```Java
public static void main(String[] args) throws ClassNotFoundException {
    //1、使用类的class属性来获取类对应的class对象
    Class<Student> c1 = Student.class;
    Class<Student> c2 = Student.class;
    System.out.println(c1 == c2); //true   一个类只有一个对应的Class对象

    System.out.println("--------------------");

    //2、调用对象的getClass()方法，返回该对象所属类对应的Class对象。
    Student s = new Student();
    Class<? extends Student> c3 = s.getClass();
    System.out.println(c1 == c3); //true

    System.out.println("--------------------");

    //3、使用Class类中的静态方法forName(String className)
    Class<?> c4 = Class.forName("classfs.Student");
    System.out.println(c1 == c4); //true
}
```

**注意：**通常使用1和3方法来获取Class对象，1简便，3灵活(如：可以将字符串路径配置到文件，方便更换)；(一般不使用2因为还要创建对象)

##### 获取构造方法并使用

![](C:\Users\panqiyi\Desktop\notes\image\1img\58.png)

```java
public static void main(String[] args) throws ClassNotFoundException, NoSuchMethodException, IllegalAccessException, InvocationTargetException, InstantiationException {
    //获取Class对象
    Class<?> c = Class.forName("classfs.Student");

    //返回一个 Constructor对象，该对象反映由该 Class对象表示的类的指定公共构造函数。
    Constructor<?> con = c.getConstructor();

    //Constructor提供了一个类的单个构造函数的信息和访问权限。
    //T newInstance(Object... initargs) 使用由此 Constructor对象表示的构造函数，
    // 使用指定的初始化参数来创建和初始化构造函数的声明类的新实例。
    Object obj = con.newInstance();
    System.out.println(obj);
    
}
```

**练习1、**

![](C:\Users\panqiyi\Desktop\notes\image\1img\59.png)

```java
public static void main(String[] args) throws ClassNotFoundException, IllegalAccessException, InvocationTargetException, InstantiationException, NoSuchMethodException {
    //获取Class类对象
    Class<?> c = Class.forName("classfs.Student");

    //通过Class对象获取构造方法
    Constructor<?> con = c.getConstructor(String.class, int.class, String.class);

    //通过构造方法创建对象实例
    Object o = con.newInstance("林青霞", 19, "西湖");
    System.out.println(o);
}
```

**练习2、**

![](C:\Users\panqiyi\Desktop\notes\image\1img\60.png)

```java 
public static void main(String[] args) throws ClassNotFoundException, IllegalAccessException, InvocationTargetException, InstantiationException, NoSuchMethodException {
    //获取Class类对象
    Class<?> c = Class.forName("classfs.Student");

    //通过Class对象获取构造方法
    Constructor<?> dcon = c.getDeclaredConstructor(String.class);

    //正常情况下私有的构造方法是无法创建对象的，但是在反射中是可以的
    //暴力反射
    //void setAccessible(boolean flag) ：值为true,取消访问检查
    dcon.setAccessible(true);

    //通过构造方法创建对象实例
    Object obj = dcon.newInstance("林青霞");
    System.out.println(obj);
}
```

##### 反射获取成员变量并使用

![](C:\Users\panqiyi\Desktop\notes\image\1img\61.png)

```java
public static void main(String[] args) throws ClassNotFoundException, NoSuchMethodException, NoSuchFieldException, IllegalAccessException, InvocationTargetException, InstantiationException {
    Class<?> c = Class.forName("classfs.Student");
    //获取构造方法
    Constructor<?> con = c.getConstructor();
    //创建对象
    Object o = con.newInstance();
    //获取成员变量
    Field a = c.getDeclaredField("age"); //getDeclaredField可以获取所有成员变量

    //将19赋值给对象o中的a --->即age
    a.set(o,19);

    System.out.println(o);

}
```

**练习：**

![](C:\Users\panqiyi\Desktop\notes\image\1img\62.png)



```java
public static void main(String[] args) throws ClassNotFoundException, NoSuchMethodException, IllegalAccessException, InvocationTargetException, InstantiationException, NoSuchFieldException {
    Class<?> c = Class.forName("classfs.Student");

    Constructor<?> con = c.getConstructor();
    Object o = con.newInstance();

    Field ageField = c.getDeclaredField("age");
    ageField.setAccessible(true); // 因为有些成员变量不是公共的，所以统一都取消访问权限；否则有些不是公共修饰的成员变量无法访问
    Field nameField = c.getDeclaredField("name");
    nameField.setAccessible(true);
    Field addressField = c.getDeclaredField("address");
    addressField.setAccessible(true);

    ageField.set(o,30);
    nameField.set(o,"林青霞");
    addressField.set(o,"西湖");

    System.out.println(o);

}
```



##### 反射获取成员方法并使用

![](C:\Users\panqiyi\Desktop\notes\image\1img\63.png)

```java
public static void main(String[] args) throws ClassNotFoundException, NoSuchMethodException, IllegalAccessException, InvocationTargetException, InstantiationException {
    Class<?> c = Class.forName("classfs.Student");

    Method[] methods = c.getMethods();  //获取所有公共成员方法，包括继承自父类或接口的公共方法
    for (Method method : methods) {
        System.out.println(method);
    }
    System.out.println("-------------------");
    Method[] declaredMethods = c.getDeclaredMethods(); //获取该类所有成员方法
    for (Method m : declaredMethods) {
        System.out.println(m);
    }

    System.out.println("-------------------");

    Method method1 = c.getMethod("method1", String.class);

    //获取无参构造方法创建对象
    Constructor<?> con = c.getConstructor();
    Object obj = con.newInstance();

    //Object invoke(Object obj, Object... args)  在具有指定参数的指定对象上调用此 方法对象表示的基础方法。
    //Object: 返回值类型
    //obj: 调用方法的对象
    //args: 方法需要的参数

     method1.invoke(obj,"hello world！"); //调用obj对象中的mwthod1方法，并传参数为"hello world！"
 
}
```



**练习**

```java
public static void main(String[] args) throws ClassNotFoundException, NoSuchMethodException, IllegalAccessException, InvocationTargetException, InstantiationException {
    //获取Class对象
    Class<?> c = Class.forName("classfs.Student");

    //获取构造方法创建对象   Student s = new Student();
    Constructor<?> con = c.getConstructor();
    Object o = con.newInstance();

    //获取一个成员方法（公共的）
    Method m1 = c.getMethod("method1", String.class);
    m1.invoke(o,"王祖贤");

    Method m2 = c.getMethod("method2", String.class, int.class);
    Object ob = m2.invoke(o, "林青霞", 24);  //method2有返回值的
    System.out.println(ob);


    //获取一个成员方法（所有修饰类型的，不止公共）
    Method f = c.getDeclaredMethod("function");
    f.setAccessible(true);  //私有方法无法访问，所以取消访问权限
    f.invoke(o);
}
```

**练习：越过泛型检查**

在ArrayList< Integer> 集合中  添加字符串类型元素

```java
public static void main(String[] args) throws NoSuchMethodException, InvocationTargetException, IllegalAccessException {
    //创建集合
    ArrayList<Integer> arr = new ArrayList<>();//正常情况只能允许int类型存储

    //获取集合的Class对象
    Class<? extends ArrayList> arrClass = arr.getClass();

    //获取add方法
    Method add = arrClass.getMethod("add", Object.class);

    //往集合对象添加字符串元素
    add.invoke(arr, "哈喽！");
    add.invoke(arr, "Java");

    //打印集合
    System.out.println(arr);
}
```



**练习：运行配置文件指定内容**

```java
public class Students {
    public void sout(){
        System.out.println("我是学生！！！");
    }
}
```

```java 
public class Teacher {
    public void sout(){
        System.out.println("我是老师！！");
    }
}
```

上面有两个类，一个老师类一个学生类；当我们要使用其中一个类的一个方法时，我们需要创建对象然后调用

```Java
public static void main(String[] args) {
   /* Teacher t = new Teacher();
    t.sout();*/
    Students s = new Students();
    s.sout();
}
// 这样不方便切换，想只用其中一个时还需要将另一个注释
```

**所以：**

将其配置到文件中，形成键值对

![](C:\Users\panqiyi\Desktop\notes\image\1img\64.png)

```java
public static void main(String[] args) throws IOException, ClassNotFoundException, NoSuchMethodException, IllegalAccessException, InvocationTargetException, InstantiationException {
    //创建Properties集合
    Properties prop = new Properties();
   //创建字符输入流
    FileReader f = new FileReader("C:\\Users\\panqiyi\\Desktop\\abc\\config.txt");
    prop.load(f); //读取流
    f.close();

    //据键取值
    String className = prop.getProperty("className");
    String methodName = prop.getProperty("methodName");

    //获取class对象
    Class<?> c = Class.forName(className);

    //获取构造方法，创建对象
    Constructor<?> con = c.getConstructor();
    Object obj = con.newInstance();

    //获取方法并调用
    Method m = c.getMethod(methjavaodName);
    m.invoke(obj);
}
```

**如此一来，想调用哪个类的哪一个方法，只需要去配置文件中修改即可**



### 模块化

Java9的

![](C:\Users\panqiyi\Desktop\notes\image\1img\66.png)

**1、一个模块访问另一个模块的内容**

1、创建两个模块：myOne和myTwo

![](C:\Users\panqiyi\Desktop\notes\image\1img\65.png)

```java
//myTwo模块中cn.text包下的text01类要使用myOne类com.print01包下的Student类
//模块与模块之间没有访问权限，所以是不行的
public class text01 {
    public static void main(String[] args) {
        Student s = new Student();
        s.study();
    }
}
```

**问题解决：** 

module-info.java 描述性文件：定义模块名，访问权限，模块依赖等

1、在myOne模块的src新建一个module-info.java （选择src右键即见）；

然后在module-info.java 中配置模块导出  格式：exports  包名;

```Java
module myOne {
     exports com.print01;
    //模块中所有 未导出 的包都是私有的，它们不能在模块外被访问
}
```

2、在myTwo模块的src新建一个module-info.java （选择src右键即见）；

然后在module-info.java 中配置模块依赖  格式：requires 模块名;

```Java
module myTwo {
     requires myOne;
    //模块1要访问模块2，模块1必须指定依赖模块2；未指定依赖的模块不能访问
}
//注意：写模块名报错，需要Alt+Enter提示，然后选择模块依赖
```

这样就访问成功了



**2、模块服务的使用**



### Junit单元测试

测试的分类：

1、黑盒测试：不用写代码，给输入值，看程序能否输出期望值

1、白盒测试：要写代码，关注程序的具体执行流程

**Junit使用**

Junit 属于白盒测试

步骤：

**1、定义一个测试类** 

**建议：**测试类包名xxx.xxx.test    如：com.jd.test

​          测试类名：被测试类名Test     如：StudentTest

**2、定义一个测试方法**

**建议：**方法名：test测试的方法名     如：testAdd()

​           返回值：void          

​		   参数列表：空参

​		权限修饰都是公共的。

**3、给方法加 @Test**

报错  Alt+Enter 导入Junit依赖环境

![image-20201126105711742](https://gitee.com/panqiyi/pqimg/raw/master/20201126105711.png)

判断结果：

红色：失败    绿色：成功

一般我们会使用**断言操作来处理结果**

`Assert.assertEquals(期望结果,程序运行结果);` 二者进行比较，运行结果与期望的相同则成功

**例：**

```Java
//计算器类
public class Calculator {

    public int add(int a,int b){
        return a+b;
    }

    public int Sub(int a,int b){
        return a-b;
    }
}
```

```java
//测试类
public class Demo01test {

    @Test  //添加注解报错 Alt+Enter
    public void testAdd(){
        //创建计算器对象
        Calculator c = new Calculator();
        int sum = c.add(2, 3);
        //System.out.println(sum);
        //断言  我断言结果为5
        Assert.assertEquals(5,sum);  // 断言结果与真实运行结果比较
    }
    @Test
    public void testSub(){
        Calculator c = new Calculator();
        int num = c.Sub(3, 1);
        Assert.assertEquals(2,num);
    }java
}
```

**补充：**两个注解

@Before: 修饰的方法会在测试方法之前被自动执行

@After：修饰的方法会在测试方法执行后自动被执行



### 注解

概念：

1、jdk1.5之后的新特性

2、说明程序的，给计算机看的，可以理解为标签一样；

3、使用注解格式：@注解名称

作用分类：

1、编写文档：通过代码中注解生成doc文档，如使用的java的api文档

2、代码分析：通过注解对代码进行分析

3、编译检查：通过注解让编译器实现基本编译检查，如继承中子类重写父类方法

#### jdk内置注解

```java
/*
* 1、 @Override ：检测被该注解标注的方法是否继承自父类(接口)
* 2、@Deprecated：该注解标注的内容，表示已过时
* 3、@SuppressWarnings：压制警告 ，需传参，一般 "all"*/
@SuppressWarnings("all")
public class AnnoDemo01 {
    @Override
    public String toString() {
        return super.toString();
    }

    @Deprecated
    public void show01(){
        //有缺陷，添加注解表示过时，但还可使用
    }

    public void show02(){java
        //更新，替换show01
    }
}
```

#### 自定义注解

格式：

```Java
public @interface 注解名称{
	
}
// 反编译查看上面代码（步骤：cmd进入该类文件夹，javac 类.java编译->.class文件，javap 类.class反编译）
//使用idea反编译插件ideaJad更为好
public interface com.annotation.MyAnno extends java.lang.annotation.Annotation{}
```

通过反编译可以看出：**注解本质上是一个接口，该接口默认继承Annotation接口**

**属性：**接口中的抽象方法 

在注解中为什么叫属性？接着往下看

1、属性的返回值类型有以下取值 （其他是不行的）

- 基本数据类型
- String
- 枚举
- 注解
- 以上类型的数组

2、定义了属性，在使用注解是需要给对应属性赋值

​	  	1、如果定义属性时，使用default关键字给属性默认初始化，则使用注解时不用赋值

​			2、如果只有一个属性，且属性名称是value，则使用注解时赋值可以省略名称

​			3、数组赋值时，值使用{}包裹。如果数组中只有一个值，则{}可以省略

```Java
//自定义一个注解
public @interface MyAnno {
    int age();
    String name();
    EnumMj person(); //枚举类（EnmuMj中定义了两个变量e1,e2）
    String[] arr();
}
```

```java
@MyAnno(age = 18,name = "牛皮",person = EnumMj.e1,arr = {"all","hello"})
//使用注解时根据注解属性赋值；
public class Test01 {java
}
```

因为注解的使用时赋值方法与变量赋值方式相同，所以称为属性！！

```java
//特殊情况1
public @interface MyAnno {
    String name() default "李";
}

@MyAnno()
public class Test01 {java
}
```

```java
//特殊情况1
public @interface MyAnno {
    int value();
}

@MyAnno(18) 
public class Test01 {
}
```

```Java
//特殊情况3
public @interface MyAnno {
    String[] name();  
}

@MyAnno(name = "all") //当name为value时可以省略
public class Test01 {
}
```

#### 元注解

概念：用于描述注解的注解

就是自定义一个注解时还可以在该自定义注解上添加**注解** 

- @Target：描述注解被作用的位置

- @Retention：描述注解被保留的阶段

- @Documented：描述注解是否被抽取到api文档中

- @Inheriter：描述注解是否被子类继承

  1、@Target

```Java
//  public @interface Target {
//     ElementType[] value();
//  }
// 类型ElementType为枚举类
//  TYPE   被描述的注解只能用来描述类
//  FIELD  被描述的注解只能用来描述成员变量
//  METHOD  被描述的注解只能用来描述方法
@Target({ElementType.TYPE,ElementType.FIELD,ElementType.METHOD}) 
public @interface MyAnno { //自定义注解
    String[] value();
}
```

```Java
@MyAnno("all")
public class Test01 {
    @MyAnno("a")
    public String name;
    @MyAnno("s")
    public static void method(){ }
}
```

2、@Retention

```Java
//类型RetentionPolicy为枚举类 有3个：源码期、字节码文件、运行时期
//一般我们自定义的注解都是用运行期（如用SOURCE源码期，则对应后面的读不到，CLASS也一样）
@Retention(RetentionPolicy.RUNTIME) //当前被描述的注解，会保留到Class文件中，并被jvm读到
public @interface MyAnno {
    String[] value();
}
```

3、@Documented

```java
@Documented  //被该注解描述的注解，生成api文档时会被提取到API中
public @interface MyAnno01 {

}
```

```java
public class Test01 {
    @MyAnno01
    String name;
    @MyAnno01
    public static void method(){ }

    public static void method1(){ }
}
```

1、将两个文件都另存为--->然后改编码为本地----->打开文件去掉导入包名

![](C:\Users\panqiyi\Desktop\notes\image\1img\67.png)

2、打开com，进入到对应路径,然后输入指令

![](C:\Users\panqiyi\Desktop\notes\image\1img\69.png)

生成API

![](C:\Users\panqiyi\Desktop\notes\image\1img\68.png)

<img src="C:\Users\panqiyi\Desktop\notes\image\1img\70.png" style="zoom:67%;" />

**注意：**

Test01类的成员变量name与成员方法method加了自定义注解@MyAnno01, 自定义注解上又加了@Documented元注解 ，所以会这两个上面会提取该注解到API

<img src="C:\Users\panqiyi\Desktop\notes\image\1img\71.png" style="zoom: 80%;" />

如果自定义注解@MyAnno01没有加元注解@Documented, 那么API上也不会出现自定义注解

4、@Inherited

```Java
@Inherited  //用元注解@Inherite去描述注解A,当我们使用注解A去描述一个类时，该类的子类也会继承注解A的描述
public @interface MyAnno01 {
}
```

```java
public class Test01 {
    @MyAnno01
    public String name;
    @MyAnno01
    public static void method(){ }
    public static void method1(){ }
}
```

```java
public class Test02 extends Test01 {
}   //因为父类Test01加了 @MyAnno01注解，又因为 @MyAnno01加了元注解@Inherited描述，所以Test02也继承了@MyAnno01
```

#### 解析注解

之前我们在使用注解时给它赋值了，那么这些值有什么用呢？？？下面我们就去使用他的值！

**解析注解可以理解为：使注解有功能作用，有意义**

1、用于做反射的配置

现有一个类Demo01:

```Java
public class Demo01 {
    public void show01(){
        System.out.println("show01方法执行！！");
    }
}
```

我们想通过反射调用Demo01下的show01()方法？？

1.1 自定义一个注解

```Java
@Target(ElementType.TYPE) //这个
@Retention(RetentionPolicy.RUNTIME) //与这个，这两个元注解得有
public @interface Pro {
    String className(); 
    String methedName();
}
```

1.2 创建一个测试类，使用自定义的注解

```Java
@Pro(className = "com.annotation.Demo01",methedName = "show01")
//com.annotation.Demo01 类全路径 类中的方法
public class UseAnnoTest {
    public static void main(String[] args) throws ClassNotFoundException, NoSuchMethodException, IllegalAccessException, InvocationTargetException, InstantiationException {
        
        //创建该测试类字节码文件对象
        Class<?> c = Class.forName("com.annotation.UseAnnoTest");
        //通过字节码文件对象获取加在该类注解对象（其实是它的实现类对象）
        Pro an = c.getAnnotation(Pro.class);
        //其实就是返回 内存中生成的一个该注解接口的一个实现类的对象 像如下：
        /*  public class ProImpl implements Pro{
                public String className(){
                    return "com.annotation.Demo01";
                    }
                public String methodName(){
                    return "show01";
                   }
                   //实现类重写注解接口抽象方法，返回值为注解的赋值
             }
        */
        //调用注解对象中的抽象方法，获取返回值
        String cn = an.className();
        String mn = an.methedName();
        System.out.println(cn);  //返回注解赋值的对应字符串（这里是类的完整路径）
        System.out.println(mn);  //返回注解赋值的对应字符串（这里是类中的方法）

        //以上其实就是用注解来做反射的配置（使注解有了功能，有了意义，所以上面就叫解析注解），
        // 我们只需要修改注解赋的值，就可以调用不同类或不同方法等等

        
        //获取目标类字节码文件对象
        Class<?> cs = Class.forName(cn);
        //获取构造方法并创建对象
        Constructor<?> con = cs.getConstructor();
        Object o = con.newInstance();
        //获取成员方法
        Method method = cs.getMethod(mn);
        method.invoke(o);
    }
}
```

**案例：**

现有一个计算器类，我们要使用注解来标记 要判断的方法的异常情况，并将异常详情记录到文件中

```Java
//自定义一个注解
@Target({ElementType.TYPE,ElementType.METHOD})
@Retention(RetentionPolicy.RUNTIME)
public @interface Check {
}
```

```Java
//计算器类，在需要判断的方法上加上注解
public class Calculator {

    @Check
    public void add(){//加
        String str=null;
        str.toString(); //null不能调用方法
        System.out.println("1+0="+(1+0));
    }
    @Check
    public void sup(){//减
        System.out.println("1-0="+(1-0));
    }
    @Check
    public void mul(){//乘
        System.out.println("1*0="+(1*0));
    }
    @Check
    public void div(){//除
        System.out.println("1/0="+(1/0));
    }

    public void show(){
        System.out.println("没有加上注解");
    }
}
```

```Java
//解析注解
public class CheckTest {
    public static void main(String[] args) throws IOException {
        Calculator c = new Calculator();
        //获取字节码文件对象
        Class<? extends Calculator> cls = c.getClass();
        //3、获取所有成员方法对象
        Method[] methods = cls.getMethods();

        int number=0; //记录出现异常次数
        BufferedWriter bw = new BufferedWriter(new FileWriter("bug.txt"));

        for (Method method : methods) { //遍历所有方法对象
            //判断方法上是否有Check注解
            if (method.isAnnotationPresent(Check.class)){
                //有，就执行
                try {
                    method.invoke(c);
                } catch (Exception e) {
                    //捕获异常

                    //记录到文件中
                    number++; //出现异常就+1
                    bw.write(method.getName() +"方法出现异常！");
                    //方法对象.getName 获取方法名  类对象.getName 获取全路径类名称
                    bw.newLine();
                    bw.write("异常的名称："+e.getCause().getClass().getSimpleName());//获取简短名称（不包括包名）
                    bw.newLine();
                    bw.write("异常的原因："+e.getCause().getMessage()); //异常原因
                    bw.newLine();
                    System.out.println("------------------------");
                    bw.newLine();

                }
            }
        }
        bw.write("本次出现"+number+"次异常！");
        bw.newLine();
        bw.flush();
        bw.close();

    }
}
```



**总结：**

1、以后大多数情况，我们会使用注解，而不是自定义注解

2、注解给谁用？

​			1、编译器（编译器识别注解功能，检测编译有没有问题）

​			2、解析注解（通过代码编写 使注解有功能有意义）

3、注解不是程序的一部分，但是程序要遵守注解的约束；可以理解注解为标签；

如 ：当一张标签上写着你是某人的儿子时，你却不是，那么就会出错！

