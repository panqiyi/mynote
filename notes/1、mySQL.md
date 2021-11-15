## my SQL

**DB**

数据库(database)：储存一系列有组织的数据 "仓库" ；

**DBMS**

数据库管理系统(Database Management System)，DB是通过DBMS创建和操作容器；

**SQL**

用来与数据库通信的语言；

### 通用语法

1、SQL语句可以单行或多行书写，以分号结尾；

2、可以使用空格和缩进来增强语句的可读性；

3、MySQL数据库的SQL语句不区分大小写，关键字建议大写；

**注释**

单行注释：-- 注释内容(注意空格)   或  #注释内容(MySQL特有)

多行注释：/* 注释 */

### SQL的分类

1、**DDL**: 数据定义语言；用来定义数据库、表、列等。

2、**DML**：数据操作语言；用来对数据库表中的数据进行增删改。

3、**DQL**：数据查询语言；用来查询数据库表中数据。

4、**DCL**：数据控制语言；用来定义数据库的访问权限和安全级别，级创建用户。

![](C:\Users\panqiyi\Desktop\notes\image\51.png)

### DDL:操作数据库、表

#### 操作数据库：CRUD

**1、C(Create)：创建**

* 创建一个数据库：

  ```
  create database 数据库名称; 
  ```

* 创建数据库，并判断是否存在；

 ```
 create database if not exists 数据库名称;    (这样先判断有无重名数据库，不存在重命则会创建，避免报错)
 ```

* 创建名为db4数据库，判断是否存在，并指定字符集为gbk;

  ```
  create database if not exists db4 character set gbk;
  ```

**2、R(Retrieve)：查询**

* 查询数据库所有名称：

  ```
  show databases;
  ```

* 查询某个数据库的字符集  或 某个数据库的创建语句：

  ```
  show create database 数据库名称;
  ```

**3、U(Update)：修改**

* 修改数据库字符集：

  ```
  alter database 数据库名称 character set 字符集名称;
  ```

**4、D(Delete)：删除**

* 删除数据库

  ```
  drop database 数据库名称;
  ```

* 判断数据库存在 再删除

  ```
  drop database if exists 数据库名称;
  ```

**5、使用数据库**

* 查询当前正在使用的数据名称

  ```
  select database();
  ```

* 使用数据库

  ```
  use 数据库名称;-- 进入了这个数据库
  ```

#### 操作表：CRUD 

**1、C(Create)：创建**

* 语法

  ```sql
  create table 表名(
  	列名1 数据类型,
  	列名2 数据类型,
  	……
  	列名n 数据类型  #最后一列不需加逗号
  );
  常用数据类型：
  	1、int:整数类型
  	    age int
  	2、double：小数类型
  	   score double(5,2)  共五位，小数为有2位 
  	3、date：日期，只包含年月日，yyyy-MM-dd
  	4、datetime: 日期，包含年月日时分秒，yyyy-MM-dd HH:mm:ss
  	5、timestamp:时间戳类型：包含年月日时分秒，yyyy-MM-dd HH:mm:ss
  	不赋值或者赋值null，则默认使用当前的系统时间来自动赋值；
  	6、varchar：字符串
  		name varchar(20)：设置姓名最大20个字符
  		zhangsan 8个字符   张三 2个字符
  
  ```

  * 创建表

    ```sql
    create table student(
    	id int,
        name varchar(32),
        age int,
        score double(4,1),
        birthday date,
        insert_time timestamp
    );
    ```

    ![](C:\Users\panqiyi\Desktop\notes\image\52.png)

补充: 复制表

```
create table 新表名 like 老表名;
复制一份跟老表一样的新表;
```

**2、R(Retrieve)：查询**

* 查询某个数据库中所有表的名称

  ```
  show tables;
  ```

* 查询表结构

  ```
  desc 表名;
  ```

**3、U(Update)：修改**

* 修改表名

  ```
  alter table 表名 rename to 新表名;
  ```

* 修改表的字符集

  ```
  alter table 表名 character set 字符集名称;
  ```

* 添加一列

  ```
  alter table 表名 add 列名 数据类型;
  ```

* 修改列名称，类型

  ```
  alter table 表名 change 列名 新列名 数据类型; -- 即改列名又改数据类型
  alter table 表名 modify 列名 新数据类型; -- 只改数据类型;
  ```

* 删除列

  ```
  alter table 表名 drop 列名;
  ```

**4、D(Delete)：删除**

* 删除表

  ```
  drop table 表名;
  drop table if exists 表名;
  ```

### DML：增删改 表中的数据

**1、添加数据**

语法：

```
insert into 表名 (列名1,列名2,……,列名n) values(值1,值2,……值n);
```

注意：

1、列名与值要一 一对应

2、如果不写列名，则默认给全部列名添加值；

```
insert into 表名 values(值1,值2,……值n);
```

3、除了数字类型，其他类型需要使用引号(单双都可以)引起来；

```
INSERT INTO stu1 VALUES(345,"李连杰",56,94.6,"1893-8-23",NULL);
```

例：

```
INSERT INTO stu1(id,NAME,age) VALUES(33,'李小龙',19);
```

```
SELECT * FROM stu1;  -- DQL查询表中记录
```

![](C:\Users\panqiyi\Desktop\notes\image\56.png)

**2、删除数据**

语法：

```
delete  from  表名 where 条件;
```

例：

```
DELETE FROM stu1 WHERE id=33;
```

注意：如果没有写“where 条件” 则会全部删除表中的记录

```
DELETE FROM stu1; -- (不推荐)有多少条记录就执行多少次，效率低；
```

如果要删除表中全部数据建议使用：

```
truncate from 表名; -- (推荐) 删除表，再创建一个一样的空表
```

**3、修改数据**

语法：

```
update 表名  set  列名1=值,列名2=值2 where 条件;
```

```
UPDATE stu1 SET id=888,NAME="吕布" WHERE id=777; -- 找id为777的修改
```

注意：

1、如果不加任何条件，则会将对应列的值都要修改；

### DQL查询表中的记录

```
select * from  stu;-- 查询全部表内数据
```

语法：

```
select
	字符列表
from
	表名列表
where
	条件列表
group by
	分组字段
having
	分组之后的条件
order by
	排序
limit
	分页限定
```

#### 基础查询

1、多个属性查询

2、去除重复

3、计算列

4、起别名

创建一个表

```
CREATE TABLE student(id INT, -- 学号
			NAME VARCHAR(20), -- 名字
			address VARCHAR(20), -- 地址
			sex VARCHAR(5), -- 性别
			math INT, -- 数学
			yuwen DOUBLE(3,1) -- 语文
			);
INSERT INTO student VALUES(111,"李易峰","香港","男",78,88),(222,"杨洋","北京","男",68,98),
			(333,"吴亦凡","香港","男",78,68),(444,"张艺兴","浙江","男",78,77),
			(555,"李易峰","北京","男",98,88),(666,"李易峰","深圳","男",758,99);
			-- 一个表内可以直接添加

UPDATE student SET math=NULL WHERE id=333; -- 替换id为333的行替换其math成绩为null
```

```
-- 查询全部属性
SELECT * FROM student;
```

![](C:\Users\panqiyi\Desktop\notes\image\57.png)

```
-- 查询部分：姓名和数学成绩
SELECT NAME,math FROM student; 
```

![](C:\Users\panqiyi\Desktop\notes\image\58.png)

```
-- 查询部分：地址属性
SELECT address FROM student;
```

![](C:\Users\panqiyi\Desktop\notes\image\59.png)

```
-- 去除重复结果集
SELECT DISTINCT address FROM student; -- 在属性前加distinct	
```

![](C:\Users\panqiyi\Desktop\notes\image\60.png)

```
-- 计算math和yuwen的成绩和
SELECT  NAME,math,yuwen,math+yuwen FROM student;
-- 如果有null参与的运算，计算结果都为null
```

![](C:\Users\panqiyi\Desktop\notes\image\61.png)

```
SELECT math,yuwen,IFNULL(math,0)+yuwen FROM student;-- 如果math为null，则让它为0
```

![](C:\Users\panqiyi\Desktop\notes\image\62.png)

```
-- 起别名
SELECT NAME AS 姓名,math 数学,yuwen 语文,IFNULL(math,0)+yuwen AS 总分 FROM student; -- 也可以不用as，空格即可
```

![](C:\Users\panqiyi\Desktop\notes\image\63.png)

#### 条件查询

1、where子句后面加条件；

2、运算符：>  、<  、<=  、>=  、  =   、<>

```
between...and 、   and 、    or  、   not  、  in(集合)
```

例：

```
CREATE TABLE student(id INT, -- 学号
			NAME VARCHAR(20), -- 名字
			address VARCHAR(20), -- 地址
			sex VARCHAR(5), -- 性别
			math INT, -- 数学
			yuwen DOUBLE(3,1) -- 语文
			);
INSERT INTO student VALUES(111,"李易峰","香港","男",78,88),(222,"杨洋","北京","男",68,98),
			(333,"吴亦凡","香港","男",78,68),(444,"张艺兴","浙江","男",78,NULL),
			(555,"步惊云","北京","男",98,88),(666,"聂风","深圳","男",75,99);
			-- 一个表内可以直接添加

SELECT * FROM student;

-- 查询语文成绩大于80的
SELECT * FROM student WHERE yuwen>80;
-- 查询语文成绩大于等于80的
SELECT * FROM student WHERE yuwen >= 80;
-- 查询语文成绩为88的
SELECT * FROM student WHERE yuwen = 88;

-- 查询数学成绩不为78的 
SELECT * FROM student WHERE math !=78;
SELECT * FROM student WHERE math <> 78;-- 两个都行

-- 查询数学成绩在70到80之间
SELECT * FROM student WHERE math >=70 AND math<=80;
SELECT * FROM student WHERE math BETWEEN 70 AND 80;-- 一样

-- 查询数学成绩68和75的
SELECT * FROM student WHERE math =68 OR math=75;
SELECT * FROM student WHERE math IN(68,75);-- 一样

-- 查询语文值为null的
SELECT * FROM student WHERE yuwen IS NULL;-- null值不能用 =(!=) 来判断
-- 查询语文值不为null的
SELECT * FROM student WHERE yuwen IS NOT NULL;
```

##### 模糊查询

select  * from  表名 where  属性 like  '条件' ;

```
-- 查询学号开头是4的学生
SELECT * FROM student WHERE id LIKE "4%"; -- % 表示不管有几位字符；  _ 下划线表示一位字符
-- 查询id尾号是39的学生
SELECT * FROM student WHERE id LIKE '%39';-- 单双引号都可以

-- 查询名字中间为：艺 的学生
SELECT * FROM student WHERE NAME LIKE "_艺%";
-- 查询名字带有：峰 的学生
SELECT * FROM student WHERE NAME LIKE '%峰%';
```

#### 排序查询

语法：

```
select * from student order by 属性 排序方式, 属性 排序方式...;
```

```
-- 查询让数学成绩升序
SELECT * FROM student ORDER BY math ASC;-- asc:升序  desc:降序

-- 查询让数学成绩降序
SELECT * FROM student ORDER BY math DESC;

-- 查询让数学成绩升序条件下，当数学成绩相同时，语文成绩才按照升序
SELECT * FROM student ORDER BY math ASC,yuwen ASC;

注意：
select * from student order by math;-- 不写则默认升序
```



#### 聚合函数

1、count()：统计行(信息条)数

```
语法：
select count(属性) from 表名;
如：
SELECT COUNT(NAME) FROM student;-- 结果7 条信息

SELECT COUNT(yuwen) FROM student;-- 结果6 ;因为null没有算
-- 解决方法1：尽量使用主码(主键)来计数（推荐）
	-- 2: 使用ifnull
       SELECT COUNT(IFNULL(yuwen,0)) FROM student;-- 结果7

-- count(*) ：只要有一个一个属性不为null就会计数 (不推荐)
```

2、max()：某属性的最大值;   

   min()：某属性的最小值

```
语法：
select max(属性)/min(属性) from 表名;
-- 求数学成绩最大值
SELECT MAX(math) FROM student;-- 98
-- 求数学成绩最小值
SELECT MIN(math) FROM student;-- 68
```

3、sum()：某属性的和

```
-- 计算数学成绩的总和
SELECT SUM(math) FROM student;-- 564
```

4、avg()：某属性的平均分

```
-- 计算数学成绩的平均分
SELECT AVG(math) FROM student;-- 80.5714
```



#### 分组查询

语法：

```
group by 分组的列;
注意：
分组之后查询的字段：分组的列，聚合函数
```

例：

1、

```
-- 按照性别分组，分别查询男、女同学语文的平均分
SELECT sex,AVG(yuwen) FROM student GROUP BY sex;
```

![](C:\Users\panqiyi\Desktop\notes\image\64.png)

2、

```
-- 按照性别分组，分别查询男，女生的平均分和人数
SELECT  sex,AVG(math),COUNT(id) 人数  FROM student GROUP BY sex;
```

![](C:\Users\panqiyi\Desktop\notes\image\65.png)

3、

```
-- 按照性别分组，分别查询男女生数学大于70的平均分
SELECT sex,AVG(math),COUNT(id) FROM student WHERE math>70 GROUP BY sex;-- 分组前：where条件限制大于70才参与分组
```

![](C:\Users\panqiyi\Desktop\notes\image\67.png)

4、

```
-- 在第三步的基础上，限制条件 分组后：分组的人数大于1才能被查询出来
SELECT sex,AVG(math),COUNT(id) FROM student WHERE math>70 GROUP BY sex HAVING COUNT(id)>1;

简洁优化：起别名
SELECT sex,AVG(math),COUNT(id) as num FROM student WHERE math>70 GROUP BY sex HAVING num>1;
```

![](C:\Users\panqiyi\Desktop\notes\image\66.png)

**where和having的区别？**

1、where是在分组前进行限定，满足条件才能分组；having是分组后进行限定，满足条件才能被查询；

2、where后不能使用 聚合函数；而having可以使用 聚合函数；

#### 分页查询

将数据分一定条数为一页来查询

语法：

mySQL语句是这样，但其他数据库有不一样；

```
limit 开始索引,每页的查询的条数;
公式： 开始索引=(当前页码-1)*每一页的条数;

```

select * from student;

![](C:\Users\panqiyi\Desktop\notes\image\69.png)

将数据按3条数分为一页查询

```
SELECT * FROM student LIMIT 0,3;  -- 第一页   【LIMIT 开始索引,每一页条数】
```

![](C:\Users\panqiyi\Desktop\notes\image\68.png)

```
SELECT * FROM student LIMIT 3,3; -- 第二页    索引=(当前页数-1)*每一页条数   (2-1)*3=3

SELECT * FROM student LIMIT 6,3;  -- 第三页     (3-1)*3=6
```



### 约束

概念：对表中数据的限定，保证数据的准确性，有效性，和完整性；

分类：

**1、**主键约束：primary  key

某一列为主键，不能为空，不能重复

**2、**非空约束：not null  

某一列的值不能为null

**3、**唯一约束：unique

某一列的值不能重复

**4、**外键约束：foreign key

#### 非空约束：not null

约束前：可以添加name值为空的数据

```
CREATE TABLE stu(
	id INT,
	NAME VARCHAR(20)
	);

INSERT INTO stu VALUES(111,"黄飞鸿"),(222,NULL);
```

![](C:\Users\panqiyi\Desktop\notes\image\70.png)

**1、创建表时添加非空约束**

约束后：不能添加name值为空的数据

```
CREATE TABLE stu(
	id INT,
	NAME VARCHAR(20) NOT NULL -- 非空约束，name不能为空
	);

INSERT INTO stu VALUES(111,"黄飞鸿"),(222,NULL);
```

![](C:\Users\panqiyi\Desktop\notes\image\71.png)

**2、创建表完后添加非空约束**

```
CREATE TABLE stu(
	id INT,
	NAME VARCHAR(20)
	);

INSERT INTO stu VALUES(111,"黄飞鸿");

ALTER TABLE stu MODIFY NAME VARCHAR(20) NOT NULL;-- 通过修改列来添加非空约束

INSERT INTO stu VALUES(22,NULL);-- 执行添加非空约束后就不能添加name值为空的数据了
```

**也可以通过此法删除非空约束；**

```
-- 通过修改name列 来达到删除非空约束; 
ALTER TABLE stu MODIFY NAME VARCHAR(20);
```

#### 唯一约束：unique

可以储存null，但是只能一次，也不能重复

约束前：

```
CREATE TABLE stu(
		id INT,-- 学号
		number VARCHAR(20) -- 号码
		);

INSERT INTO stu VALUES(111,1111);

INSERT INTO stu VALUES(22,1111);-- 在添加号码一样的
```

![](C:\Users\panqiyi\Desktop\notes\image\72.png)

**1、创建表时添加 唯一约束**

```
CREATE TABLE stu(
		id INT,
		number VARCHAR(20) UNIQUE -- 使号码不能重复
		);

INSERT INTO stu VALUES(111,1111);

INSERT INTO stu VALUES(22,1111);-- 报错，不能添加重复号码
```

**2、删除 唯一约束语句**

注意：与创建表后删除非空唯一约束语句不同；

```
alter table 表名 drop index 唯一约束的列;

ALTER TABLE stu DROP INDEX number;
```

**3、创建表后添加 唯一约束**

```
CREATE TABLE stu(
		id INT,
		number VARCHAR(20)
		);

INSERT INTO stu VALUES(111,1111);-- 添加number为1111的信息；


ALTER TABLE stu MODIFY number VARCHAR(20) UNIQUE;-- 通过修改表信息来添加唯一约束
```

**注意：**

**当创建表后**，如果表中a列已经添加有null值，则不能为a列添加非空约束not null ；     如果该表a列已经添加有重复的值，则不能为a列添加唯一约束 unique



#### 主键约束：primary key

1、含义：非空且唯一

2、一张表只能有一个列(属性)为主键

3、主键就是表中信息的唯一标识

**1、创建表时添加主键约束**

```
CREATE TABLE stu(
		id INT PRIMARY KEY, -- 添加主键约束,将id设置为主键
		number VARCHAR(20)
		);
INSERT INTO stu VALUES(111,2323);
INSERT INTO stu VALUES(111,3434); -- 无法添加，主键不能重复
INSERT INTO stu VALUES(NULL,3434); -- 无法添加，主键不能为空
```

**2、删除  主键约束**

```
alter table stu drop primary key;
```

**3、创建表后添加 主键**

```
alter table stu modify id int primary key;
```

##### 自动增长

一般与主键一起使用；

概念：如果某列使数值类型，使用auto_increment 可以完成值的自动增长；

**1、创建表时添加主键约束，并且完成主键自动增长**

没有给主键添加值即为null，如int类会自动从1开始1、2、3……自动增长赋值

```
CREATE TABLE stu(
		id INT PRIMARY KEY AUTO_INCREMENT, 
		number VARCHAR(20)
		);
INSERT INTO stu VALUES(1,2323);
INSERT INTO stu VALUES(NULL,3434); -- 设主键为null，主键id则会自动+1
```

![](C:\Users\panqiyi\Desktop\notes\image\73.png)

**删除自动增长**

```
alter table stu modify id int;
```

**添加自动增长**

```
alter table stu modify id int auto_increment;
```



#### 外键约束：foreign key

如果一个表(关系)中的一个属性是另外一个关系中的主码(主键)则这个属性为外码

**外键约束前：**

```
CREATE TABLE emp( -- 创建emp表
	id INT PRIMARY KEY AUTO_INCREMENT,
	NAME VARCHAR(20),
	age INT,
	dep_name VARCHAR(30), -- 部门名称
	dep_location VARCHAR(30) -- 部门地址
	);


-- 添加数据
INSERT INTO emp (NAME,age,dep_name,dep_location) VALUES('张三',20,'研发部','广州');
INSERT INTO emp (NAME,age,dep_name,dep_location) VALUES('李四',22,'研发部','广州');
INSERT INTO emp (NAME,age,dep_name,dep_location) VALUES('王五',24,'研发部','广州');

INSERT INTO emp (NAME,age,dep_name,dep_location) VALUES('老大',18,'研发部','上海');
INSERT INTO emp (NAME,age,dep_name,dep_location) VALUES('老二',20,'研发部','上海');
INSERT INTO emp (NAME,age,dep_name,dep_location) VALUES('老三',26,'研发部','上海');

SELECT * FROM emp; -- 发现数据有冗余  地址与部门过于重复
```

(id为主键并且自动增长，这里没有给id赋值，id列为null，则会自动增长)

![](C:\Users\panqiyi\Desktop\notes\image\74.png)

**1、在创建表时添加外键约束**

foreign key , 让表与表之间产生关系，保证数据的完整性正确性

语法：

```
create table 表名(
		……
		外键列,
		constraint 外键名称 foreign key （外键列名称）references 主表名字(主表列名) -- 通过外键列与另一个表(主表)的主键关联(一般为主键，也可以不是)
		);
```

例：

```
-- 创建部门表(id,dep_name,dep_location)
--
CREATE TABLE department(
		id INT PRIMARY KEY AUTO_INCREMENT,
		dep_name VARCHAR(30),
		dep_location VARCHAR(20)
		);

INSERT INTO department VALUES(NULL,'研发部','广州'),(NULL,'销售部','上海');

-- 创建员工表(id,name,age,dep_id)
CREATE TABLE employee(
		id INT PRIMARY KEY AUTO_INCREMENT,
		NAME VARCHAR(20),
		age INT,
		dep_id INT, -- 外键对应部门表的主键
		CONSTRAINT emp_dept_fk FOREIGN KEY (dep_id) REFERENCES department(id) -- 添加外键
		);

-- 添加员工  dep_id表示员工所在部门
INSERT INTO employee (NAME,age,dep_id) VALUES('张三',20,1);
INSERT INTO employee (NAME,age,dep_id) VALUES('李四',22,1);
INSERT INTO employee (NAME,age,dep_id) VALUES('王五',24,1);

INSERT INTO employee (NAME,age,dep_id) VALUES('老大',18,2);
INSERT INTO employee (NAME,age,dep_id) VALUES('老二',20,2);
INSERT INTO employee (NAME,age,dep_id) VALUES('老三',26,2);
```

![](C:\Users\panqiyi\Desktop\notes\image\75.png)

![](C:\Users\panqiyi\Desktop\notes\image\76.png)

通过为员工表添加主键与部门表关联，如果删除研发部则不行，因为员工表有信息关联研发部(张三李四王五都在研发部)；如果添加员工的外键dep_id为3，而关联的部门表没有id为3的部门，则此员工信息不能添加；

**2、删除外键**

```
alter table 表名 drop foreign key 外键名称;

ALTER TABLE employee DROP FOREIGN KEY emp_dept_fk;
```

**3、创建表后添加 外键约束**

```
alter table 表名 add constraint 外键名称 foreign key （外键列名称）references 主表名字(主表列名);


ALTER TABLE employee ADD CONSTRAINT emp_dept_fk FOREIGN KEY (dep_id) REFERENCES department(id); -- 添加外键
```

##### 联级操作

![](C:\Users\panqiyi\Desktop\notes\image\75.png)

![](C:\Users\panqiyi\Desktop\notes\image\76.png)

通过联级操作 **级联更新：**如修改部门表的研发部id为6，则与之关联的员工表的dep_id外键也会变为6；**级联删除：** 如删除部门表的研发部，与之相关的员工表的信息也会删除；

**1、添加联级操作**

语法：

在添加外键键后添加 

```
ALTER TABLE employee ADD CONSTRAINT emp_dept_fk FOREIGN KEY (dep_id) REFERENCES department(id) ON UPDATE CASCADE ON DELETE CASCADE;-- 这里两个级联操作都添加了

-- 级联更新
on update cascade
-- 级联删除
on delete cascade
```

删除级联即删除外键即可

****

### 数据库的设计

#### 多表关系

 **1、一对一(了解)**

如：人和身份证

**2、一对多(多对一)**

如：一个部门与员工

**3、多对多**

如：学生与老师

**实现关系**

**一对多**

![](C:\Users\panqiyi\Desktop\notes\image\77.png)

在"多"的添加外键，指向“一”的一方的主键；

**多对多**

借助第三张表建立外键指向两张表的主键

![](C:\Users\panqiyi\Desktop\notes\image\78.png)

**一对一**

随便其中一张表添加外键并让外键唯一，指向另一张表的主键

![](C:\Users\panqiyi\Desktop\notes\image\79.png)

一般 一对一会合成一张表

**多表关系案例**

![](C:\Users\panqiyi\Desktop\notes\image\80.png)

````
-- 创建旅游路线分类表 tab_categor
-- cid 旅游线路分类主键，自动增长
-- cname 旅游路线分类名称非空，唯一，
CREATE TABLE tab_categor(
		cid INT PRIMARY KEY AUTO_INCREMENT,
		cname VARCHAR(100) NOT NULL UNIQUE
		);

-- 添加添加旅游路线分类数据
INSERT INTO tab_categor (cname) VALUES('周边游'),('国内游'),('港澳游');


-- 创建旅游路线表 tab_route
-- rid 旅游路线主键，自动增长
-- rname 旅游路线名称非空，唯一
-- price 价格
-- rdate 上架时间
-- cid 外键
CREATE TABLE tab_route(
		rid INT PRIMARY KEY AUTO_INCREMENT,
		rname VARCHAR(100) NOT NULL UNIQUE,
		price DOUBLE,
		rdate DATE,
		cid INT,
		FOREIGN KEY (cid) REFERENCES tab_categor(cid) -- 省略了外键名，系统会自动生成
		);

-- 用户表
CREATE TABLE tab_user(
		uid INT PRIMARY KEY AUTO_INCREMENT,-- 用户主键，自动增长
		username VARCHAR(100)NOT NULL UNIQUE,-- 用户名
		PASSWORD VARCHAR(30) NOT NULL,-- 密码
		birthday DATE,
		sex CHAR(1) DEFAULT '男',
		telephone VARCHAR(11),
		email VARCHAR(100)
		);
		
-- 建立中间表
CREATE TABLE tab_favorite(
		rid INT, -- 用户主键
		DATE DATETIME,
		uid INT, -- 路线主键
		-- 创建复合主键
		PRIMARY KEY(rid,uid),-- 联合主键，两个主键联合为中间表的主键
		-- 然后为这两个主键添加外键关联对应表
		FOREIGN KEY (rid) REFERENCES tab_route(rid),
		FOREIGN KEY (uid) REFERENCES tab_user(uid)
		);
````

![](C:\Users\panqiyi\Desktop\notes\image\1img\6.png)

### 范式

概念：设计数据库时，需要遵循的一些规范，要遵循后面的范式要求，必须先遵循前面所有的范式要求

目前关系数据库有六种范式：第一范式（1NF）、第二范式（2NF）、第三范式（3NF）、巴斯-科德范式（BCNF）、第四范式(4NF）和 第五范式（5NF，又称完美范式）

目前学前三种范式

分类：

**1、第一范式：**每一列都是不可分割的原子数据项

**2、第二范式：**在1NF的基础上，非码属性必须完全依赖于候选码(在1NF基础上消除非主码对主码的部分函数依赖)

**3、第三范式：**在2NF的基础上，任何非主码不依赖于其他非主码（在2NF基础上消除传递依赖）

#### 第一范式

![](C:\Users\panqiyi\Desktop\notes\image\82.png)

每一列都是不可分割的原子数据项

![](C:\Users\panqiyi\Desktop\notes\image\81.png)

#### 第二范式

了解几个概念：

**1、函数依赖：**A - ->B，如果通过A属性(属性组)值，可以确定唯一B属性的值；则称B依赖于A。

​	例如：学号  - -> 姓名；    (学号,课程名称) - -> 分数；

**2、完全函数依赖：**A - ->B，如果通过A属性组的所有属性的值，可以确定唯一B属性的值；则称B完全依赖于A。       

​	 例如：（学号，课程名称）-- > 成绩

**3、部分函数依赖：**A - ->B，如果通过A属性组的部分属性的值，可以确定唯一B属性的值；则称B部分依赖于A。

​		例如：     （学号，课程名称）--> 姓名

**4、传递函数依赖：**A -- >B , B -- > C；如果通过A属性(属性组)的C值，可以确定唯一B属性的值，再通过B属性(属性组)的值，可以确定唯一C属性的值，则称C传递函数依赖于A。

​	例如：学号 -- > 系名 ， 系名 -- > 系主任

**5、主码(主键)：**在一个表中，如果一个属性或者属性主，被其他所有属性完全依赖

![](C:\Users\panqiyi\Desktop\notes\image\81.png)

此表主码为 学号与课程，分数完全依赖于主码；而姓名，系名，系主任部分依赖主码(其中的学号)

将部分依赖的属性与他们依赖的属性(学号)分为另一个表

![](C:\Users\panqiyi\Desktop\notes\image\83.png)

#### 第三范式

消除传递依赖

![](C:\Users\panqiyi\Desktop\notes\image\84.png)



### 数据库的备份与还原

#### 命令行操作

语法

**备份：**

```
mysqldump -u用户名 -p密码  数据库名称 > 保存的路径
```

![](C:\Users\panqiyi\Desktop\notes\image\85.png)

不直接输入密码的方式：

![](C:\Users\panqiyi\Desktop\notes\image\90.png)

**还原：**

```
1、登录数据库
2、创建数据库
3、使用数据库
4、执行文件：source 文件路径
```

![](C:\Users\panqiyi\Desktop\notes\image\88.png)

![](C:\Users\panqiyi\Desktop\notes\image\86.png)

![](C:\Users\panqiyi\Desktop\notes\image\87.png)

![](C:\Users\panqiyi\Desktop\notes\image\89.png)

#### 可视化工具SQLyog操作

**备份**

![](C:\Users\panqiyi\Desktop\notes\image\91.png)

![](C:\Users\panqiyi\Desktop\notes\image\92.png)

**还原**

![](C:\Users\panqiyi\Desktop\notes\image\93.png)

![](C:\Users\panqiyi\Desktop\notes\image\94.png)

###  多表查询

**笛卡尔积**

* 有两个集合A，B 取这两个集合的所有组成情况

* 要完成多表查询需要消除无用的数据

  员工表：

  ![](C:\Users\panqiyi\Desktop\notes\image\96.png)

​      部门表：

​                                   ![](C:\Users\panqiyi\Desktop\notes\image\97.png)

```
SELECT * FROM emp,dept; -- 未加限制，两个表 笛卡尔积把所用组合情况计算出来
```

![](C:\Users\panqiyi\Desktop\notes\image\95.png)

#### 内连接查询

**1、隐式内连接：**使用where条件消除无用的数据

例：

员工表（emp）的外键为: dept_id  它关联部门表（dept）的主键：id

```
-- 查询所有员工信息和对应的部门名称
select * from  emp,dept where emp.'dept_id'=dept.'id';-- 让外键等于关联的主键就可以消除无用的数据	
```

![](C:\Users\panqiyi\Desktop\notes\image\98.png)

```
-- 标准写法
select
 	列名(属性)
from
	表名
where 
	条件;
	
-- 查询两张表的部分属性
SELECT 
	t1.`id`,t1.`name`,t1.`sex`,t2.`name` -- t1.员工表的属性  t2.部门表属性  

FROM 
	emp t1,dept t2  为两张表起别名，方便使用
WHERE 
	t1.`dept_id`=t2.`id`;
```

![](C:\Users\panqiyi\Desktop\notes\image\99.png)

**2、显式内连接**

``` 
select 列名(属性) from 表名1 inner join 表名2 on 条件;
-- inner 可以省略
SELECT * FROM emp INNER JOIN dept ON emp.`dept_id`=dept.`id`;

SELECT * FROM emp JOIN dept ON emp.`dept_id`=dept.`id`;
```

效果更隐式内连接一样；

#### 外连接查询

**左外连接**

语法

```
select 列表(属性) from 表1 left [outer] join 表2 on 条件;
-- []里面的outr可以省略，一般不用写
```

**查询的是左表的所有数据以及其交集部分。**

例如：为员工表添加了数据，内连接查询不到

```
SELECT * FROM emp INNER JOIN dept ON emp.`dept_id`=dept.`id`;-- 内连接查询
```

![](C:\Users\panqiyi\Desktop\notes\image\98.png)

使用外连接的左连接

```\
SELECT * FROM emp LEFT JOIN dept ON emp.`dept_id`=dept.`id`;
-- emp表相对于dept表在左边
```

![](C:\Users\panqiyi\Desktop\notes\image\100.png)

**右外连接**

**查询的是右表的所有数据以及其交集部分。**


```
select 列表(属性) from 表1 right [outer] join 表2 on 条件;
```

```
SELECT * FROM dept RIGHT JOIN emp ON emp.`dept_id`=dept.`id`;
-- 注意：此时将添加数据的emp表放在了右边
```

![](C:\Users\panqiyi\Desktop\notes\image\101.png)

**注意：**左连接与右连接是相对的，两个作用其实一样，只是查询的表是相对于语法的左边还是右边 还有与主表交集的部分，一般使用左连接即可；

#### 子查询

概念：查询中嵌套查询，称嵌套查询为子查询

例：有如下表，即上面的员工部门表，只是多了工资

![](C:\Users\panqiyi\Desktop\notes\image\103.png)

```
-- 查看最高的工资
SELECT MAX(emp.`salary`) FROM emp ; -- 结果9800
-- 在根据最高工资来查看该员工的信息
SELECT * FROM emp WHERE emp.`salary`=9800;
```

![](C:\Users\panqiyi\Desktop\notes\image\102.png)

嵌套查询后：

```
SELECT * FROM emp WHERE emp.`salary`=(SELECT MAX(emp.`salary`) FROM emp);-- 结果一样
```

又如：

**最高工资员工信息：**

```
SELECT 
	t1.`id`,t1.`name`,t1.`salary`,t2.`name` -- 两个表部分属性
FROM 
	emp t1,dept t2  -- 两个表起别名
WHERE 
	t1.`salary`=(SELECT MAX(emp.`salary`) FROM emp) AND t1.`dept_id`=t2.`id`;-- 条件1 工资最高； 条件2 emp表外码与dept表主码相等，去除笛卡尔积中的无用数据
```

![](C:\Users\panqiyi\Desktop\notes\image\104.png)



**大于平均工资员工信息：**

![](C:\Users\panqiyi\Desktop\notes\image\105.png)

```
SELECT 
	t1.`id`,t1.`name`,t1.`salary`,t2.`name` -- 两个表部分属性
FROM 
	emp t1,dept t2  -- 两个表起别名
WHERE 
	t1.`salary`>(SELECT AVG(emp.`salary`) FROM emp) AND t1.`dept_id`=t2.`id`;-- 与上面的最高工资一样，只是条件不同
```

![](C:\Users\panqiyi\Desktop\notes\image\106.png)

**求开发部与财务部的员工信息：**

![](C:\Users\panqiyi\Desktop\notes\image\107.png)

```
SELECT 
	t1.`id`,t1.`name`,t1.`sex`,t1.`salary`,t2.`NAME`
FROM 
	emp t1,dept t2

WHERE
	t1.`dept_id` IN(SELECT id FROM dept WHERE NAME IN('开发部','财务部')) AND t1.`dept_id`=t2.`id`;
	-- where 条件：当员工表的外码dept_id等于开发部或财务部的id时，查询出所要的信息；
```

![](C:\Users\panqiyi\Desktop\notes\image\108.png)



**求入职日期大于‘2015-11-11’的员工：**

![](C:\Users\panqiyi\Desktop\notes\image\109.png)

```
-- 内连接查询
SELECT	t1.`id`,t1.`name`,t1.`sex`,t1.`salary`,t1.`joins`,t2.`NAME`
FROM 
	emp t1,dept t2
WHERE 
	t1.`joins`>'2015-11-11' AND t1.`dept_id`=t2.`id`;

```

![](C:\Users\panqiyi\Desktop\notes\image\110.png)

#### 练习

**例：**

![](C:\Users\panqiyi\Desktop\notes\image\1img\5.png)

```
SELECT 
	t1.`name` 姓名,
	t1.`sex` 性别,
	t1.`salary` 工资,
	t1.`joins` 入职日期,
	t3.`NAME` 部门,
	t2.`name` 地区,
	t4.`id` 工资等级
FROM
	emp t1,diq t2,dept t3,salarys t4
WHERE 
	t1.`dept_id`=t3.`id` AND t2.`dept_id`=t3.`id`
	 AND t1.`salary` BETWEEN t4.`mina` AND t4.`maxb`;
```

![](C:\Users\panqiyi\Desktop\notes\image\1img\7.png)



**例：**

```
-- 查询部门，部门地区，部门人数

-- 先部门人数，通过emp员工表外键dept_id分组查询人数，外键又对应部门表的主键
SELECT 
	dept_id,COUNT(id)
FROM
	emp 
GROUP BY 
	dept_id;
```

![](C:\Users\panqiyi\Desktop\notes\image\1img\8.png)

```
-- 将上面分组查询部门人数作为一个虚拟表 t3
SELECT
	t1.`NAME`,t2.`name`,t3.num
FROM
	dept t1,diq t2,
	(SELECT 
	dept_id,COUNT(id) num
	FROM
	emp
	GROUP BY 
	dept_id) t3
WHERE
	t1.`id`=t2.`dept_id` AND t1.`id`=t3.dept_id;
	//t1.`id`=t3.dept_id 当表3(emp员工表分组查询得到)的外键与部门表主键相等时
```

![](C:\Users\panqiyi\Desktop\notes\image\1img\9.png)

**例：**

![](C:\Users\panqiyi\Desktop\notes\image\1img\10.png)

```sql
-- 查询员工姓名及 与其对应管理者，无管理者的员工也要查询
-- 管理者就是同一表对应id的其他人
SELECT 
	t1.`name`,-- 员工
	t1.`mgr`,-- 管理者id
	t2.`id`,-- 管理者对应id
	t2.`name`-- 管理者name
FROM 		
	emp t1 -- 相对于t2 在左边
LEFT JOIN
	emp t2
ON
	t1.`mgr`=t2.`id`;
	
-- emp表的id与mgr是自关联，将emp用起别名可分为内容相同的两个表进行操作
-- 无管理者的员工也要查询：询左表的所有数据和 两表的交集数据  使用左连接	
```

![](C:\Users\panqiyi\Desktop\notes\image\1img\11.png)



### 视图

含义： 虚拟表，

MySQL5.1版本新特性，是通过表动态生成的数据
从数据库表中提取需要的数据 形成一个虚拟表展现出来，并没有保存在库中；

**使用场景**

- 多个地方用到同样的查询结果

- 该查询结果使用的SQL语句较复杂

```sql
-- 查询  student表中学生姓名，与SC表中的系名  约束条件为姓张的学生
SELECT  s.`Sname`,c.`Sno`
FROM
	student s
INNER JOIN SC c ON s.`Sno`=c.`Cno`
WHERE 
	s.`Sname` LIKE '张%';
	
-- 创建一个视图  从student表中提取 名字列，从SC表中提取 系名列   构成一个虚拟表
-- 查询  student表中学生姓名，与SC表中的系名
CREATE VIEW v1
AS
SELECT  s.`Sname`,c.`Sno`
FROM
	student s
INNER JOIN SC c ON s.`Sno`=c.`Cno`
-- 此时视图中就有学生姓名与系名两列，需要查询视图中的数据只需添加条件即可
-- 如查询姓张的学生姓名与系名
WHERE 
	s.`Sname` LIKE '张%'; 
```



### 事务

#### 基本介绍

**概念：**

* 如果一个包含多个步骤的业务操作，被事务管理，那么这些操作要么同时成功，要么同时失败；

**操作：**

**1、开启事务：start transaction;** 

将多个步骤当成整体管理

**2、回滚：rollback;**

出现异常则返回原来未操作的状态，即对数据操作无效

**3、提交：commint;**

结果正常，则提交事务，结果改变



**基本演示：**

现有如下表：

![](C:\Users\panqiyi\Desktop\notes\image\2img\1.png)

张三转钱500给李四：则张三-500，李四+500

```sql
-- 张三账户 -500
UPDATE account SET balance=balance-500 WHERE NAME='张三';
-- 2、李四账户 +500
UPDATE account SET balance=balance+500 WHERE NAME='李四'; 
```

当张三执行转账完后，后面语句出现异常，导致李四收钱语句无法执行，就会丢失500块  如：

```sql
UPDATE account SET balance=balance-500 WHERE NAME='张三';
出错了 这里有异常 这里未注释
-- 2、李四账户 +500
UPDATE account SET balance=balance+500 WHERE NAME='李四'; -- 上面出现异常则不会执行下面代码，就会凭空消失500块
```

![](C:\Users\panqiyi\Desktop\notes\image\2img\2.png)

**为了避免 数据丢失与安全，所以使用事务来管理：**

```sql
-- 开启事务
START TRANSACTION;
-- 张三给李四转账500
-- 1、张三账户 -500
UPDATE account SET balance=balance-500 WHERE NAME='张三';
出错了 这里有异常
-- 2、李四账户 +500
UPDATE account SET balance=balance+500 WHERE NAME='李四'; -- 上面出现异常则不会执行下面代码，就会凭空消失500块

-- 发现没有问题，提交事务
COMMIT;
-- 发现结果异常，回滚事务
ROLLBACK;
```

![](C:\Users\panqiyi\Desktop\notes\image\2img\3.png)

 **提交事务：**

提交事务即永久更新sql语句的作用

永久更新：关闭软件后，再打开，其语句执行的变化是永久的，是存储在硬盘了的；

**自动提交：**

mysql就是自动提交   (Oracle 数据库是手动提交事务)

一条DML(增删改)语句会自动提交一次事务。

**手动提交：**

需要先开启事务，再提交事务 commit，语句才会生效

**修改事务的默认提交方式：**

1、查看事务的默认提交方式：`select @@autopcommit; --1代表自动提交，0代表手动提交 `

2、修改默认提交方式：`set @@autocommit=0;`



#### 四大特征

##### 原子性

是不可分割的最小操作单位，要么同时成功，要么同时失败。

##### 持久性

当事务提交或回滚后，数据库会持久化的保存数据。

##### 隔离性

多个事务之间，相互独立。

##### 一致性

事务操作前后，数据总量不变



#### 隔离级别

概念：多个事务之间，是相互独立的。但是如果多个事务操作同一批数据，则会引发一些问题，设置不同的隔离级别就会解决这些问题。 

- **存在的问题：**

  1、脏读：一个事务，读取到另一个事务中没有提交的数据

  2、不可重复读(虚读)：在同一个事务中，两次读取到的数据不一样

  3、幻读：一个事务操作(DML)数据表中所有记录，另一个事务添加了一条数据，则第一个事务查询不到自己的修改

  

**隔离级别：**

**1、read uncommitted：读未提交**

- 产生问题：脏读、不可重复读、幻读

**2、read committed：读已提交 （Oracle默认）**

- 产生问题：不可重复读、幻读

**3、repeatable  read：可重复读 (mySQL默认)**

- 产生问题：幻读

**4、serializable：串行化**

- 可以解决所有问题

**注意：**隔离级别从小到大安全性 越来越高，但是效率越来越低

**数据库查询隔离级别：**

`select  @@tx_isolation;`  

**数据库设置隔离级别：**

`set  global  transaction  isolation  level  级别字符串`



**事务隔离级别演示：**

**1----读未提交**

1、将事务隔离级别修改为 **read uncommitted**：读未提交

```sql
set  global  transaction  isolation  level  read uncommitted;
```

2、开启事务1  `satrt transaction`

3、张三转账500给李四，张三账户-500，李四账户+500；**未提交事务**。

4、另开启一个事务2，查询表中两者账户情况。

(另开启一个事务2：这里是重新另打开cmd来查询，重新打开即可看出事务1的操作有没有永久存储在硬盘）

![](C:\Users\panqiyi\Desktop\notes\image\2img\5.png)

事务1未提交事务，所以结果未永久保存；但是事务2直接读取到了事务1未提交的数据，就出现了 脏读问题；还有 不可重复读、幻读的问题

![](C:\Users\panqiyi\Desktop\notes\image\2img\9.png)



**2-----读已提交**

1、将事务隔离级别修改为 **read read committed**：读已提交

2、开启事务1  `satrt transaction`

3、张三转账500给李四，张三账户-500，李四账户+500；**未提交事务**。

4、另开启一个事务2，查询表中两者账户情况。

![](C:\Users\panqiyi\Desktop\notes\image\2img\4.png)

修改隔离级别后，**脏读问题得到解决！**！

5、事务1**提交事务**，然后事务2在查询：

![](C:\Users\panqiyi\Desktop\notes\image\2img\6.png)

脏读问题解决，上面就是不可重复读问题，事务2对同一数据读到两次结果不一样！

读已提交：解决了脏读，但还有不可重复读，幻读这两个问题

![](C:\Users\panqiyi\Desktop\notes\image\2img\8.png)



**3----可重复读**

![](C:\Users\panqiyi\Desktop\notes\image\2img\7.png)

**事务1提交前 后，事务2查询读到的结果没有变化，只有事务2提交后，事务2才读到数据的更新！！**

**4----串行化：**

![](C:\Users\panqiyi\Desktop\notes\image\2img\10.png)

隔离级别为串行化时，相对于把事务1给锁住，其他事务无法访问事务1操作的数据，直到事务1提交事务时方可出查询结果。



### DCL

#### 账户管理

**1、查询用户：**

```sql
-- 1、切换到mysql数据库
-- 2、查询user表
SELECT * FROM USER;
```



**2、添加用户：**

```sql
-- 创建用户
create user '用户名'@'主机名' identified by '密码'; -- 注意'用户名'@'主机名' 三者之间没有空格！
```

```sql

CREATE USER 'zhangsan'@'localhost' IDENTIFIED BY '123'; -- localhost 当前主机访问

CREATE USER 'lisi'@'%' IDENTIFIED BY '123'; -- % 在任意主机访问
```



**3、删除用户：**

```sql
-- 删除用户
drop user '用户名'@'主机名';

DROP USER 'zhangsan'@'localhost';
```



**4、修改用户密码：**

```sql
set password for '用户名'@'主机名' = password('新密码');

SET PASSWORD FOR 'lisi'@'%' = PASSWORD('abc');
```



**当忘记root账户密码时怎么办？？**

```
1、以管理员身份运行cmd，输入以下指令停止mysql服务
net stop mysql
2、使用无验证方式启动mysql服务：
mysqld --skip-grant-tables
3、打开新的cmd窗口，直接输入: mysql 敲回车,就可以登陆成功。
4、use mysql 
5、set password for 'root'@'localhost' = password('新密码');
6、关闭两个cmd窗口
7、打开任务管理器，手动结束mysqld.exe的进程
8、启动mysql服务:net start mysql
9、使用新密码登录即可:mysql -uroot -p
```



#### 权限管理

**1、查询权限：**

```sql
-- 查询权限
show grants for '用户名'@'主机名';
```

**2、授予权限：**

```sql
-- 授予权限
GRANT 权限列表 ON 数据库.表名 TO '用户名'@'主机名';

GRANT SELECT,UPDATE ON db2.account TO 'lisi'@'%';
```

```sql
-- 授权给lisi用户：对所有数据库的任意表有所有权限
GRANT ALL ON *.* TO 'lisi'@'%';
```

**3、撤销权限：**

```sql
-- 撤销权限
revoke 权限列表 on 数据库名.表名 from '用户名'@'主机名';

-- 撤销zhangsan在db2数据库下的account表的查询权限
REVOKE SELECT ON db2.`account` FROM 'zhangsan'@'localhost';
```

撤销权限后，张三就无法进行其相应的操作；

