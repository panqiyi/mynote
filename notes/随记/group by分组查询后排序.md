### group by分组查询后排序

如：分组查询

```mysql
SELECT s.name name,COUNT(s.id) value FROM t_setmeal s,t_order o WHERE s.id=o.setmeal_id GROUP BY  s.name 
```

<img src="https://gitee.com/panqiyi/pqimg/raw/master/20211115164539.png" alt="image-20211115164539545" style="zoom:80%;" />

现在想实现 分组查询后，按照value值由高到低排序。

实现：通过子查询分组查询出一个派生表，再对该表排序查询

1、上面查询出来的就是一个新的表，一个属性为 name, value 的表。`（注意：每个派生表都必须有自己的别名 ）`

2、以上面的表为基础 排序查询

```mysql
select b.name,b.value 
from 
(SELECT s.name name,COUNT(s.id) value FROM t_setmeal s,t_order o WHERE s.id=o.setmeal_id GROUP BY  s.name) 
as b 
order by b.value desc
```

<img src="https://gitee.com/panqiyi/pqimg/raw/master/20211115165605.png" alt="image-20211115165605640" style="zoom:80%;" />

更简单的：

```mysql
SELECT s.name name,COUNT(s.id) value 
FROM t_setmeal s,t_order o 
WHERE s.id=o.setmeal_id 
GROUP BY  s.name
ORDER BY value DESC
```

