## python基础语法

### 注释

```python
单行注释：
# 注释内容 
快捷键 ctrl+/

多行注释：
""" 注释内容 """ 
或 
''' 注释内容 '''
```



### 变量

变量标识符：

1、由数字、字母、下划线组成

2、不能数字开头

3、不能使用关键字/保留字

4、严格区分大小写

定义格式：

```
变量名 = 值
```

```python
name = '中国红旗！！'
print(name)

num1 = 34 
num2 = 78
num3=num1+num2
print(num3)
```

### 数据类型

<img src="https://gitee.com/panqiyi/pqimg/raw/master/20210313142445.png" alt="image-20210313142445786" style="zoom:67%;" />

检测某数据的数据类型

```python
# type(数据) 返回该数据的数据类型
num1 = 34
print(type(num1))   # int 
b = True
print(type(b))  # bool
```

### 格式化输出

%s：字符串     %d：有符号十进制数      %f：浮点数

```python
name = "步惊云"
age = 23
weight = 59.5
s_id = 1

print("他叫%s"%name)   # 他叫步惊云
print("体重%.3f"%weight)  # 体重59.500; %.3f 保留3位小数（默认保留6位）
print("学号为%03d"%s_id)  # 学号为001；%03d：以三位数格式输出，不够在前面补零，超过就原样输出

print("我的名字是%s,今年%d岁了，体重%.2f,学号为%03d"%(name,age,weight,s_id))
# 我的名字是步惊云,今年23岁了，体重59.50,学号为001

print("我的名字是%s,今年%s岁了，体重%s,学号为%s"%(name,age+5,weight,s_id)) 
# 我的名字是步惊云,今年28岁了，体重59.5,学号为1
# 都能转化为字符串%s输出
```

**f 格式化：python3.6后可用**

```python
print(f'我叫{name},今年{age}岁')  # 我叫步惊云,今年23岁
```

#### 转义字符

\ : 反斜杠    / ：斜杠

\n ：换行     \t ：制表符

#### 结束符

python默认结束符号为：\n

```python
print("你好",end="\n")   # 默认结束符为换行

# 可以根据需要自行修改
print("你好",end=" ")
```

### input输入

1、input ('提示信息') 

2、特点

- 遇到input，等待用户输入
- 接收输入数据，存到变量中
- input接收到的数据类型都是字符串

```python
password = input("请输入密码：")
print(f'你输入的密码是：{password}')

'''
请输入密码：12345
你输入的密码是：12345
'''
```

### 数据类型转换

```
int(x) : 将x转换为一个整数
float(x) : 将x转换为一个浮点数
str(x) : 将对象x转换为字符串
eval(str) : 用来计算在字符串中的有效python表达式，并返回一个对象
tuple(s) : 将序列S转换为一个元组
list(s) : 将序列S转换为一个列表
```

```python
# eval(str) 其实就是将字符串数据类型的式子，变回原来的类型

str1="23"
str2="12.3"
str3="123,456,789"

print(type(eval(str1)))  # int
print(type(eval(str2)))  # float
print(type(eval(str3)))  # tuple
```

```python
# int(x)  float(x)  x可以是字符型str
str1="23"
str2="12.3"

print(type(int(str1)))   # int
print(type(float(str2)))   # float
```



### 运算符

#### 算术运算符

<img src="https://gitee.com/panqiyi/pqimg/raw/master/20210318150759.png" alt="image-20210318150759554" style="zoom:67%;" />

```
优先级：() 大于 ** 大于 *、/、//、% 大于 +、-
```



#### 赋值运算符

<img src="https://gitee.com/panqiyi/pqimg/raw/master/20210318151413.png" alt="image-20210318151413202" style="zoom:80%;" />

1、单个变量赋值

```python
num=44
print(num) # 44
```

2、多个变量赋值

```python
num1,num2,str3 = 1,12.3,"你好"
print(num2) # 12.3
print(str3)  # 你好
```

3、多个变量赋相同值

```python
a=b=c=45
print(f"{a},{b},{c}")  # 45,45,45
```



#### 复合赋值运算符

<img src="https://gitee.com/panqiyi/pqimg/raw/master/20210318153939.png" alt="image-20210318153939746" style="zoom:80%;" />

**注意：**先算复合赋值运算右边，再算复合运算

```python
# 如：
a=3
a+=10+2
a*=8+2
# 先算复合赋值运算右边，再算复合运算
# 10+2=12 --> a=a+12=15
# 8+2=10 --> a=a*10=30
```



#### 比较运算符

<img src="https://gitee.com/panqiyi/pqimg/raw/master/20210318155730.png" alt="image-20210318155730674" style="zoom:80%;" />

#### 逻辑运算符

<img src="https://gitee.com/panqiyi/pqimg/raw/master/20210318155923.png" alt="image-20210318155923137" style="zoom:80%;" />

数字之间的逻辑运算：

```python
# and运算符，只要有一个值为0，则结果为0，否则结果为最后一个非0数字
a=0
b=1
c=2
print(a and b)  # 0
print(a and c)  # 0
print(b and c)  # 2
print(c and b)  # 1

# or运算符，只有所有值为0结果才为0，否则结果为第一个非0数字
a=0
b=1
c=2
d=0
print(a or d)  # 0
print(a or c)  # 2
print(b or c)  # 1
print(c or b)  # 2
```

### if语句

```python
if False:
    print("执行语句1？")
    print("执行语句2？")

# 下方代码没有缩进到if语句块，所以和if语句无关
print("执行语句3？")
```

```python
num=23
if num>25:
    print(f"{num}大于20执行了？")
elif num==23:
    print("相等")
else:
    print("hello")
```

#### 随机数

```python
# 1、导包
import random 
# 调用randint(x,y)方法，生成包含[x,y]的随机整数
num = random.randint(0,2) # 随机生成0，1，2
print(num)
```

#### 三目运算符

```python
'''
三目运算符：
格式： 条件成立执行表达式 if 条件 else 条件不成立执行的表达式
从if开始读
'''
num1=1
num2=2
c=num2 if num2>num1 else num1
print(c) # 2
```



### while循环

```python
while 条件:
	条件成立执行代码（注意是while下回车的语句）
```

如：1-100的和

```python
i=1
sum=0
while i <= 100:
    sum+=i
    i+=1
print(sum)
```

```
break:终止当前整个循环
continue:退出当前的一次循环，继续执行后面的循环
```

while-else

```python
当while 循环正常结束时会执行else后的语句，如break就不不是正常结束
```



### for循环

```python
for 临时变量 in 序列:
	重复执行的代码
```



### 字符串

**1、下标**

```python
# 从0开始，左往右
str1="hello"
print(str1[0])
```

**2、切片**

切片是指对操作对象截取其中一部分的操作。

```python
格式：
序列[开始位置下标:结束位置下标:步长]

"""
注意：
1、不包含结束位置对应下标,相当于 [开始,结束)
2、步长是选取间隔，默认步长为1
"""
```

<img src="https://gitee.com/panqiyi/pqimg/raw/master/20210323101627.png" alt="image-20210323101627576" style="zoom:67%;" />

如下：

```python
str1="abcdefg"
print(str1[2:5:1]) # cde
print(str1[2:5:2]) # ce
print(str1[2:5]) # cde
print(str1[:4]) # abcd  -->不写开始，默认从0开始
print(str1[3:]) # defg  -->不写结束，表示选取到最后
print(str1[:]) # abcdefg  -->不写开始和结束，表示选取所有

# 测试负数
print(str1[::-1]) # gfedcba  -->如果步长为负数，表示倒序选取
print(str1[-4:-1]) # def -->下标-1为最后一个数

print(str1[-4:-1:1]) # def
print(str1[-4:-1:-1]) #   --->不能读取数据
# -4：-1，选取方向左到右；但步长为-1：方向从右到左
# 如果选取方向(下标开始到结束方向)和 步长方向冲突，则无法选取数据
```

**一些操作字符串的方法：**

**1、查找**

```
1、字符串序列.find('子串',开始位置,结束位置) : 左到右查找，有则返回下标，无则返回-1
2、字符串序列.index('子串',开始位置,结束位置) : 左到右查找，有则返回下标，无则报错

3、字符串序列.count('子串',开始位置,结束位置) : 统计'子串'出现次数
```

```python
str="hello and world and like and book"
print(str.find('and')) # 6 不写开始结束位置，即从整个序列左到右查
print(str.find('and',10,20)) # 16 从开始10到结束20查找
print(str.find('ads')) # -1 没有，返回-1

# index()与find()一样，区别是没有查找到会报错

print(str.count('and')) # 3
```





### range()

python range()函数可以创建一个整数列表，一般用在for循环中。
 函数语法

```
range(start, stop[,step])
1
```

参数说明：
 start:计数从start开始，默认是从0开始
 stop:计数到stop结束，但是不包括stop。
 step:步长，默认为1.
 实例：

```python
range(10)
[0,1,2,3,4,5,6,7,8,9]
range(1,11)
[1,2,3,4,5,6,7,8,9,10]
range(0,30,5)
[0,5,10,15,20,25]
range(0,-10,-1)
[0,-1,-2,-3,-4,-5,-6,-7,-8,-9]
```