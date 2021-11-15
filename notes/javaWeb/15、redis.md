# redis

后期学完ssm在去看b站狂神的redis

## 概念

**首先redis是一款Nosql非关系型数据库**

<font color='orange'>NoSQL仅仅是一个概念，泛指非关系型的数据库，区别于关系数据库</font>

redis是一个开源的、使用C语言编写的、支持网络交互的、**高性能的、**

**可基于内存（存储在内存中）也可持久化（存储到硬盘中）的Key-Value（键值对）数据库。**

<img src="https://gitee.com/panqiyi/pqimg/raw/master/20210530151046.png" alt="image-20210530151046089" style="zoom:80%;" />

目前Redis键的值支持的数据类型如下：

```
1、字符串类型  String
2、哈希类型   hash
3、列表类型  list
4、集合类型  set
5、有序集合类型  sorted set
```

redis的应用场景：

```
- 缓存(数据查询、短连接、新闻内容、商品内容等)
- 聊天室的在线好友列表
- 任务队列 (秒杀、抢购等)
- 应用排行帮
- 网站访问统计
- 数据过期处理 (可以精确到毫秒)
- 分布式集群架构中的session分离
```



## 下载安装

官网：https://redis.io/

中文网：https://www.redis.net.cn/

解压可直接使用，如下主要的目录：

```
redis.windows.conf    配置文件
redis-cli.exe		 redis的客户端
redis-server.exe	 redis服务器端
```

双击服务器端即可启动redis，然后点击客户端即可使用

## 命令操作

### redis的数据结构

redis存储的是键值对：key,value格式的数据，其中key都是字符串，value目前有5种不同的数据结构

```
value的数据结构：
	1、字符串类型  String  
	2、哈希类型   hash  ：map格式
	3、列表类型  list  ：linkedlist格式（允许重复）
	4、集合类型  set ：hashset（不允许重复,无序）
	5、有序集合类型  sorted Set （不允许重复且自动排序）
	
```

### 命令操作数据

看尚硅谷的ppt比较好

1、字符串类型  String

```
常用命令：
1、存储：set key value
2、获取：get key
3、删除：del key
```

2、哈希类型  hash

<img src="https://gitee.com/panqiyi/pqimg/raw/master/20210530164803.png" alt="image-20210530164803406" style="zoom:80%;" />

```
1、存储：hset key field value
2、获取
	1、hget key field : 获取指定的field对应的值
	2、hget key : 获取所有的field和value
3、删除 : hdel key field  : 删除对应的field和value
```

3、列表类型 list ：可以添加一个元素到列表的头部 (左边)  或者  尾部 （右边）

<img src="https://gitee.com/panqiyi/pqimg/raw/master/20210530165633.png" alt="image-20210530165633546" style="zoom:67%;" />

```
1、添加：
	1.lpush key value : 将元素加入列表(头)左边
	2.rpush key value : 将元素添加到列表(尾)右边
2、获取：
	lrange key start end : 范围获取(start:开始索引 end:结束索引; 获取所有：0 -1)
3、删除：
	1.lpop key : 删除列表最左边的元素，并将元素返回
	2.rpop key : 删除列表最右边的元素，并将元素返回
```

5、集合类型 set ：不允许重复元素

```
1、存储 : sadd key value
2、获取 : smembers key : 获取set集合中所有元素
3、删除 : srem key value : 删除set集合中的某个元素
```

6、有序集合类型 sortedset : 不允许重复元素，且元素有顺序，(自动排序)

```
1、存储 : zadd key score value  (score:value 对应的评分数值，用于排名的 大到小)
2、获取 : 
		zrange key start end   (start:开始索引 end:结束索引; 获取所有：0 -1)
		zrange key start end withscores  (获取value并获取对应的数值)
3、删除 : zrem key value  (删除对应value 的数据)
```



**通用命令**

```
1、keys *  : 查询所有的键
2、type key  : 获取键对应的 value 的类型
3、del key  : 删除对应key的数据
```



### 持久化

redis是存储数据在内存的数据库，当redis服务器 或者 电脑重启后，数据就会丢失，我们可以将redis内存中的数据持久化保存到硬盘中。

**redis持久化机制：**

​	**1、RDB：默认方式，不需要进行配置，默认就使用这种机制**

​				在一定的间隔时间中，检测key的变化情况，然后持久化数据

​				打开redis.windwos.conf文件

<img src="https://gitee.com/panqiyi/pqimg/raw/master/20210602225941.png" alt="image-20210602225941803" style="zoom: 80%;" />

```
save 900 1   (900秒(15分钟)后，至少有1个key变化就会持久化一次)
save 300 10	 (300秒(5分钟)后，至少有10个key变化就会持久化一次)
save 60  10000	(60秒后，至少有一个10000变化就会持久化一次)

一般情况下不修改，看你项目需求去和服务器性能修改
```

使用：

为了效果明显，将配置改为 10秒后至少有5个key改变就持久化

<img src="https://gitee.com/panqiyi/pqimg/raw/master/20210602231619.png" alt="image-20210602231619187" style="zoom:80%;" />

1、先用命令行进入到redis服务器(并指定配置)

<img src="https://gitee.com/panqiyi/pqimg/raw/master/20210602224632.png" alt="image-20210602224631945" style="zoom:80%;" />

2、打开redis文件下的客户端：redis-cli.exe ，存储5个键值对

<img src="https://gitee.com/panqiyi/pqimg/raw/master/20210602231905.png" alt="image-20210602231905569" style="zoom: 80%;" />

存储5个键值对后，就会在redis文件夹内出现dump.rdb文件，这个就是内存数据持久化到本地硬盘文件

下一次我们直接进入redis启动服务器，然后启动客户端，此时就自动将持久化的数据读取到内存中，我们就能直接获取数据。

**2、AOF ：日志记录的方式，可以记录每一条命令的操作。可以每一次命令操作后，持久化数据。**

​		1、编辑 redis.windwos.conf 文件

<img src="https://gitee.com/panqiyi/pqimg/raw/master/20210602233929.png" alt="image-20210602233929458" style="zoom:67%;" />

```
appendonly no (关闭aof)  -->  appendonly yes  (开启aof)

# appendfsync always  : 每一次操作都进行持久化
appendfsync everysec  : 每个一秒进行一次持久化
# appendfsync no      : 不进行持久化
```

使用：与上面的RDB一样，先用命令行进入到redis服务器(并指定配置)



## Jedis : java客户端

jedis : 一款Java操作redis数据库的工具。

使用：

1、先下载引入jedis的jar包

2、使用java来操作redis （前提是启动redis服务器）

```java
//1、获取连接
        Jedis jedis = new Jedis("localhost",6379);
        //2、操作
        jedis.set("username","ttt");
        //关闭连接
        jedis.close();
```

**java操作redis的方法名与命令操作数据的一样。**

### jedis操作String

```java
//1、获取连接对象
        Jedis jedis = new Jedis(); //如果使用空参构造，默认值 "localhost",6379端口
        //2、操作
        //存储
        jedis.set("username","zhangsan");
        //3、获取
        String username = jedis.get("username");
        System.out.println(username);

        //可以使用setex()方法存储可以指定过期时间的 key value
        jedis.setex("activecode", 20, "java redis");  //将activecode: java redis 键值对存入redis，并且20秒后删除改键值对
        String activecode = jedis.get("activecode");
        System.out.println(activecode);

		//关闭连接
        jedis.close();
```

### jedis操作hash

```java
//1、获取连接对象
Jedis jedis = new Jedis();
//2、操作
//存储
jedis.hset("user","username","lisi");
jedis.hset("user","age","24");

//获取
String username = jedis.hget("user", "username");
System.out.println(username); //lisi

//获取全部
Map<String, String> user = jedis.hgetAll("user");

Set<String> keySet = user.keySet();
for (String key : keySet) {
    String value = user.get(key);
    System.out.println(key+":"+value);
}

/*Set<Map.Entry<String, String>> entrySet = user.entrySet();
for (Map.Entry<String, String> entry : entrySet) {
    String key = entry.getKey();
    String value = entry.getValue();
    System.out.println(key+":"+value);
}*/

/*
age:24
username:lisi
*/

//关闭连接
jedis.close();
```

### jedis操作list

```java
//1、获取连接
Jedis jedis = new Jedis();
//2、操作
//存储
jedis.lpush("mylist","a","b","c"); // 从左边存 ,可以存多个值
jedis.rpush("mylist","a","b","c"); // 从右边存

//获取
List<String> mylist = jedis.lrange("mylist", 0, -1);
System.out.println(mylist); // [c, b, a, a, b, c]

//弹出(删除)
String lpop = jedis.lpop("mylist");
String rpop = jedis.rpop("mylist");
System.out.println(lpop+" & "+rpop); // c & c

List<String> mylist1 = jedis.lrange("mylist", 0, -1);
System.out.println(mylist1); // [b, a, a, b]

//关闭连接
 jedis.close();
```



### jedis操作set和zset

```java
//1、获取连接
Jedis jedis = new Jedis();
//2、操作
//存储
jedis.sadd("mySet","java","c","php");
//获取
Set<String> mySet = jedis.smembers("mySet");
System.out.println(mySet); //[php, java, c]

//zset的
//存储
jedis.zadd("mySortedset",99,"李白");
jedis.zadd("mySortedset",55,"露娜");
jedis.zadd("mySortedset",78,"孙悟空");
//获取
Set<String> mySortedset = jedis.zrange("mySortedset", 0, -1);
System.out.println(mySortedset); // [露娜, 孙悟空, 李白]
//关闭连接
jedis.close();
```



## 连接池

Jedis自带连接池

```java
 //1、创建连接池配置对象 (也可以省略)
        JedisPoolConfig config = new JedisPoolConfig();
        config.setMaxTotal(50); //各种配置

        //2、创建Jedis连接池对象
        JedisPool jedisPool = new JedisPool(config,"localhost",6379);
        //3、获取连接
        Jedis jedis = jedisPool.getResource();
        //4、使用
        jedis.set("username","lihua");
        String s = jedis.get("username");
        System.out.println(s); // lihua
```

jedis连接池详情配置：

```
#最大活动对象数     
redis.pool.maxTotal=1000    
#最大能够保持idel状态的对象数      
redis.pool.maxIdle=100  
#最小能够保持idel状态的对象数   
redis.pool.minIdle=50    
#当池内没有返回对象时，最大等待时间    
redis.pool.maxWaitMillis=10000    
#当调用borrow Object方法时，是否进行有效性检查    
redis.pool.testOnBorrow=true    
#当调用return Object方法时，是否进行有效性检查    
redis.pool.testOnReturn=true  
#“空闲链接”检测线程，检测的周期，毫秒数。如果为负值，表示不运行“检测线程”。默认为-1.  
redis.pool.timeBetweenEvictionRunsMillis=30000  
#向调用者输出“链接”对象时，是否检测它的空闲超时；  
redis.pool.testWhileIdle=true  
# 对于“空闲链接”检测线程而言，每次检测的链接资源的个数。默认为3.  
redis.pool.numTestsPerEvictionRun=50  
#redis服务器的IP    
redis.ip=xxxxxx  
#redis服务器的Port    
redis1.port=6379   
```



## 连接池工具类

```java
public class JedisPoolUtil {
    //连接池对象
    private static JedisPool jedisPool;

    static {
        //读取配置文件
        InputStream is = JedisPoolUtil.class.getClassLoader().getResourceAsStream("jedis.properties");
        //创建Properties对象
        Properties pro = new Properties();
        //从流中获取键值列表
        try {
            pro.load(is);
        } catch (IOException e) {
            e.printStackTrace();
        }
        //获取数据，设置到 JedisPoolConfig 中
        JedisPoolConfig config = new JedisPoolConfig();
        config.setMaxTotal(Integer.parseInt(pro.getProperty("maxTotal")));
        config.setMaxTotal(Integer.parseInt(pro.getProperty("maxIdle")));
        //初始化 连接池对象
         jedisPool = new JedisPool(config, pro.getProperty("host"), Integer.parseInt(pro.getProperty("port")));
    }

    //获取连接方法
    public static Jedis getJedis(){
        return jedisPool.getResource();
    }
}
```

jedis.properties

```properties
host=127.0.0.1
port=6379
maxTotal=50
maxIdle=10
```

使用：

```Java
//获取连接对象
Jedis jedis = JedisPoolUtil.getJedis();
//存储
jedis.set("java","java np");
//获取
String java = jedis.get("java");
System.out.println(java);
```



## 案例

案例需求：

```
1、提供index.html页面，页面中有一个省份下拉列表
2、当 页面加载完成后 发送一个ajax请求，加载所有省份
```

核心代码：

1、servlet

```java
@WebServlet("/provinceServlet")
public class ProvinceServlet extends HttpServlet {
    protected void doPost(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
       /* //1.调用service查询 （未使用redis缓存时）
        ProvinceService service = new ProvinceServiceImpl();
        List<Province> list = service.findAll();
        //2.序列化list为json
        ObjectMapper mapper = new ObjectMapper();
        String json = mapper.writeValueAsString(list);*/

        //1.调用service查询
        ProvinceService service = new ProvinceServiceImpl();
        String json = service.findAllJson();
        
        System.out.println(json);
        //3.响应结果
        response.setContentType("application/json;charset=utf-8");
        response.getWriter().write(json);
    }
    protected void doGet(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
        this.doPost(request, response);
    }
}
```

2、service

```java
//接口
public interface ProvinceService {
    //查询数据(未使用redis缓存)
    public List<Province> findAll();
    //使用缓存
    public String findAllJson();
}
```

```java
//实现类 （使用redis）
public class ProvinceServiceImpl implements ProvinceService {
    //声明dao
    private ProvinceDao dao = new ProvinceDaoImpl();
    @Override
    public List<Province> findAll() {
        return dao.findAll();
    }
    /**
        使用redis缓存
     */
    @Override
    public String findAllJson() {
        //1.先从redis中查询数据
        //1.1获取redis客户端连接
        Jedis jedis = JedisPoolUtil.getJedis();
        String province_json = jedis.get("province");

        //2判断 province_json 数据是否为null
        if(province_json == null || province_json.length() == 0){
            //redis中没有数据
            System.out.println("redis中没数据，查询数据库...");
            //2.1从数据中查询
            List<Province> ps = dao.findAll();
            //2.2将list序列化为json
            ObjectMapper mapper = new ObjectMapper();
            try {
                province_json = mapper.writeValueAsString(ps);
            } catch (JsonProcessingException e) {
                e.printStackTrace();
            }
            //2.3 将json数据存入redis
            jedis.set("province",province_json);
            //归还连接
            jedis.close();

        }else{
            System.out.println("redis中有数据，查询缓存...");
        }
        return province_json;
    }}
```

3、dao

```java
//接口
public interface ProvinceDao {
    public List<Province> findAll();
}
```

```java
//实现类
public class ProvinceDaoImpl implements ProvinceDao {
    //1.声明成员变量 jdbctemplement
    private JdbcTemplate template = new JdbcTemplate(JDBCUtils.getDataSource());
    @Override
    public List<Province> findAll() {
        //1.定义sql
        String sql = "select * from province ";
        //2.执行sql
        List<Province> list = template.query(sql, new BeanPropertyRowMapper<Province>(Province.class));
        return list;
    }}
```

前端:

```java
<script>
        $(function () {
            //发送ajax请求，加载所有省份数据
            $.get("provinceServlet",{},function (data) {
                //[{"id":1,"name":"北京"},{"id":2,"name":"上海"},{"id":3,"name":"广州"},{"id":4,"name":"陕西"}]

                //1.获取select
                var province = $("#province");
                //2.遍历json数组
                $(data).each(function () {
                    //3.创建<option>
                    var option = "<option name='"+this.id+"'>"+this.name+"</option>";

                    //4.调用select的append追加option
                    province.append(option);
                });
            });
        });        
    </script>    
</head>
<body>
        <select id="province">
            <option>--请选择省份--</option>
        </select>
</body>
```

**注意：使用redis缓存一些不经常发送改变的数据。**

```
- 数据库的数据一旦发生改变，则需要更新缓存。
	- 数据库的表执行增删改操作 ，需要将redis缓存数据情况，再次存入
	- 在service对应的增删改方法中，将redis数据删除。(删除reids，然后更新mysql后再次添加更新的数据到redis中)
```

