演进架构：单线程实现简单 IO不是主要平静下来

快<=多路复用reactor + 内存

#

# 使用问题

## 缓存穿透
null-key -> redis 查不到->查数据库

 --**穿透--**

解：cache null key

 cache null search condition + expire time

## 缓存击穿
hot-key -> expire -> 查数据库

解：限流 ，cache-warm.

## 缓存雪崩
many key -> expire -> 查数据库

解：限流，random expire time。

## 缓存更新

#### Cache Aside 更新模式
取缓存 ，取不到->db ,存 cache

更新：先存数据库,再存缓存

问题：并发时，数据库更新和缓存更新非原子的，可能出现脏数据

1 先更新数据库再更新缓存：

 A-A'

 B-B'

期望结果B' 但是可能时序： A -> B -> B' -A'

2 删除缓存再更新数据库也有问题：

Delete A -Update A -> Cache A

Read B(old) -> cache B

期望：Cache A 可能错误时序： DeleteA -> Read B-> Cache A -> Cache B

3 先更新数据库，再失效缓存。也会有问题

并发的读操作，读到的脏数据，上一个操作失效之后，将脏数据更新到缓存。

#### Read/Write Through 更新模式
通过代理读写缓存。

read throught 查询是更新缓存

write throught 命中更新缓存，缓存中间件去同步数据库，没命中直接更新数据库

#### Write Behind Caching 更新模式
读写缓存，异步更新到数据库

# 使用场景

## 分布式锁
setnx

限流器

session管理

秒杀系统

uv计数器 ( 直播观看人数）

## 延迟队列（取消订单过期
zset score存时间

#

# 🤔
redis使用其他内存分配器

如果频繁因为内存不足交换内存写入磁盘肯定影响性能，如何解决？控制不写入

# 学习资料ref
[https://redis.io/documentation](https://redis.io/documentation)

[**《redis设计与实现》**](http://redisbook.com/)** 原理 **[**黄健宏**](https://book.douban.com/search/%E9%BB%84%E5%81%A5%E5%AE%8F)

 使用

[阿里云文档](https://help.aliyun.com/document_detail/71881.html) 实践