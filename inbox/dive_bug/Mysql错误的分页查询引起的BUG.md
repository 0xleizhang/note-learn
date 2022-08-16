demo table

create demo_data (

 `id` bigint(20) NOT NULL AUTO_INCREMENT,

 `name` varchar(255) DEFAULT NULL,

 `age` tinyint(4) DEFAULT NULL,

 `create_time` datetime DEFAULT NULL,

 `update_time` datetime DEFAULT NULL,

 PRIMARY KEY (`id`)

 ) ENGINE=InnoDB DEFAULT CHARSET=utf8;

​

​

# 错误描述
​

​

# 两个错误
select id,name

from demo_data offset 0,100 order by datetime

select id,name

from demo_data offset 10000,100 order by datetime

​

1 使用重复值字段作为排序结果可能会重复

1.1 使用非索引字段排序 性能堪忧

2 offset 还是会读取全部数据，性能不高，多次查询总性能反而下降

​

​

# 正确方式

SELECT id,name

 FROM demo_data

 WHERE

 AND id < ?last_seen_id

 ORDER BY id DESC

 limit 100

​

​

​

ref:

​

[https://use-the-index-luke.com/no-offset](https://use-the-index-luke.com/no-offset)

[https://bugs.mysql.com/bug.php?id=69732](https://bugs.mysql.com/bug.php?id=69732)

[https://dba.stackexchange.com/questions/123737/same-record-shows-up-multiple-times-in-ordered-paginated-query](https://dba.stackexchange.com/questions/123737/same-record-shows-up-multiple-times-in-ordered-paginated-query)