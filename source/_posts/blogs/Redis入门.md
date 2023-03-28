---
title: Redis入门
tags:
  - redis
categories:
  - Redis
abbrlink: 6a343b7f
date: 2023-03-21 16:00:32
updated: 2023-03-23 22:31:01
keywords:
description:
---

# 入门

---

> redis 官网 [https://redis.io/download](https://redis.io/download)
>
> 中文网站 [redis.cn](http://www.redis.cn)  [www.redis.com.cn](https://www.redis.com.cn)
>
> Redis 命令文档 [http://doc.redisfans.com/](http://doc.redisfans.com/)
>
> github [https://github.com/redis/redis](https://github.com/redis/redis)
>
> 在线测试 [https://try.redis.io](https://try.redis.io)

‍

Redis（Remote Dictionary Server）：基于内存的 KV 键值对数据库

![](https://cdn.jsdelivr.net/gh/kcyln/ImageHosting@latest/2023/03/28/8a2a9dbc87cc0349e4d0c161b8d2627b.png)

**优势、注意事项、应用**

* 性能极高，读写速度可达 110000 次/秒，81000 次/秒
* 数据类型丰富，支持 list，set，zset，hash 等数据结构的存储
* 内存存储和持久化（RDB 和 AOF），可将内存中的数据异步写到硬盘，同时不影响继续服务；支持主从模式的数据备份。
* 分布式缓存，为 MySQL 数据库缓解压力
* 高可用架构搭配：单机、主从、哨兵、集群
* 缓存穿透、击穿、雪崩
* 分布式锁
* 队列
* 排行榜 + 点赞

# 数据类型

* string
* list
* hash
* set
* zset

‍

* bitmap
* bitfield
* geospatial
* HyperLogLog
* stream

bitfield 位域  位域修改，溢出控制； 了解即可

stream 流  类似于消息队列，似乎使用不多，还是用 kafka 这类吧

‍

> **相关命令**

## 字符串（String）

1. 既可以保存普通文字，也可以保存序列化的二进制数据
2. 最大可以存储 512M 数据
3. 字符串指令

   * SET key value
   * GET key
   * DEL key
   * GETRANGE key 起始位置 结束位置 获得截取字符串内容（结束位置写-1 表示最后一位）
   * STRLEN key 获取字符串长度
   * SETEX key seconds value 设置带有过期时间（秒）的 key-value
   * PSETEX key milliseconds value 设置带有过期时间（毫秒）的 key-value
   * MSET key1 value1 key2 value2 设置多个 key-value
   * MGET key1 key2 获得多个 value
   * APPEND key value 用于在字符串结尾追加内容
   * INCR key 数字自增加 1
   * INCRBY key int 数字加上指定的整数值
   * INCRBYFLOAT key float 数字加上指定的浮点数（没有减去指定浮点数的命令，可以用此命令加负数实现）
   * DECR key 数字自增减 1
   * DECRBY key int 数字减去指定的整数值

## 哈希（Hash）

1. 格式类似于 Python 的字典
2. 哈希指令

   * HSET key key1 value1 设置哈希表字段
   * HMSET key key1 value1 key2 value2 设置哈希表多个字段
   * HGET key key1 获取哈希表字段值
   * HMGET key key1 key2 获取哈希表多个字段值
   * HGETALL key 获取哈希表所有字段值（key value 都会获取到）
   * HKEYS key 获得哈希表所有字段名
   * HLEN key 获得哈希表中的字段数量
   * HEXISTS key key1 判断哈希表是否存在某个字段，存在返回 1，不存在返回 0
   * HVALS key 获得哈希表所有字段值（只获取 value）
   * HDEL key key1 key2 删除哈希表的字段
   * HINCRBY key key1 int 让哈希表某个字段值加上指定的整数值（哈希表没有减法指令）
   * HINCRBYFLOAT key key1 float 让哈希表某个字段值加上指定的浮点数

## 列表（List）

1. 格式类似于 Python 的列表
2. 列表指令

   * RPUSH key value1 value2 创建列表，向列表右侧插入内容
   * LPUSH key value1 value2 向列表左侧插入内容
   * LSET key index value 修改列表中的第几个值（index 索引，从 0 开始）
   * LRANGE key 起始位置 结束位置 获取列表起始位置与结束位置之间的内容（包含起始位置与结束位置）
   * LLEN key 获得列表长度
   * LINDEX key index 获得列表某个元素
   * LINSERT key [BEFORE|AFTER] value value1 在某个元素前面或后面插入新的元素
   * LPOP key 删除列表最左边的元素
   * RPOP key 删除列表最右边的元素
   * LREM key count value 删除列表某个元素，列表中可能有重复元素，count 表示删除几个，从左往右删除

## 集合（Set）

1. 集合中的元素不能重复，Redis 通过比较两个元素的哈希值来判断是否重复，为了加快比较速度，还会对哈希值进行排序，这样新插入的元素在判断哈希值时只要比较某个区间内的哈希值即可，也因此集合是无序的（或者说集合的顺序其实是按照哈希值排序的）
2. 集合指令

   * SADD key value1 value2 向集合中插入元素
   * SMEMBERS key 获得所有元素
   * SCARD key 获得集合长度
   * SISMEMBER key value 判断是否含有某个元素
   * SREM key value1 value2 删除元素
   * SPOP key 随机删除某个元素并返回删除的这个元素
   * SRANDMEMBER key count 随机返回集合中的元素 count 表示返回的元素的数量

## 有序集合（Zset）

1. 有序集合是带有排序功能的集合，Redis 会按照元素分数值排序（分数值相同的情况下，会根据元素值计算出来的哈希值进行排序）

   * 有序集合是按照大小对元素进行排序的一种数据结构，Redis 要求列表中每个元素除了元素值以外，还需要有一个分数值，有序列表就是对分数值排序实现的元素的排序
   * 关于有序集合为什么叫 Zset，而不是 Sorted Set

     ​![img](https://cdn.jsdelivr.net/gh/kcyln/ImageHosting@latest/2022/04/22/ea13766dc5d6b3682c085b61f0b84691.jpg)​
2. 有序集合指令

   * ZADD key score value [score] [value] 创建一个有序集合，添加数据（value 需要用双引号括起来）
   * ZINCRBY key increment value 对元素的分数值进行加法运算 increment 是数字
   * ZREVRANGE key 起始位置 结束位置 获得有序集合的内容，降序
   * ZRANGE key 起始位置 结束位置 获得有序集合的内容，升序
   * ZCARD key 获得有序集合长度
   * ZCOUNT key score1 score2 查询某个分数值区间内的元素数量
   * ZSCORE key value 返回元素的分数值
   * ZRANGEBYSCORE key score1 score2 获得分数值区间内的集合内容，升序（小括号表示不包括 10， +inf 是正无穷，-inf 是负无穷）

     ```bash
     ZRANGEBYSCORE keyword 5 10
     ZRANGEBYSCORE keyword 5 (10
     ZRANGEBYSCORE keyword 5 +inf
     ```
   * ZREVRANGEBYSCORE key score1 score2 获得分数值区间内的集合内容，降序（分数值要反着写）

     ```bash
     ZREVRANGEBYSCORE keyword 10 5
     ```
   * ZRANK key value 获得元素的升序排名（从 0 开始）
   * ZREVRANK key value 获得元素的降序排名（从 0 开始）
   * ZREM key value1 value2 删除有序集合中的元素
   * ZREMRANGEBYRANK key start stop 删除排名区间内的元素
   * ZREMRANGEBYSCORE key score1 score2 删除分数值区间内的元素

# Key命令

* DEL key 删除记录
* EXISTS key 判断是否存在某个key，存在返回1，否则返回0
* EXPIRE key seconds 设置过期时间（秒） PEXPIRE 是毫秒
* EXPIREAT key timestamp 设置记录的过期时间（UNIX时间戳）
* MOVE key 1 把记录迁移到其他逻辑库
* RENAME key key1 修改key名称
* PERSIST key 移除过期时间
* TYPE key 判断value的数据类型

# 其他指令

* FLUSHDB 清空当前数据库
* FLUSHALL 清理所有数据库中的数据
