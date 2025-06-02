# 源码阅读指南
Redis源码的顶级目录结构如下：

## deps：这个目录包含了Redis依赖的第三方库。Redis为了保持轻量，只包含了一些必要的依赖。常见的包括：

- hiredis：一个C语言的Redis客户端库，Redis服务器本身也使用它来作为客户端库（例如在Redis模块中）。
- jemalloc：一个内存分配器，Redis默认使用它来分配内存，因为它在高并发场景下性能较好。
- lua：Lua脚本引擎，Redis使用Lua来执行脚本。
- linenoise：一个简单的命令行编辑库，用于redis-cli。
- hdr_histogram：用于延迟跟踪的直方图库。
- 其他如crc32、xxHash等。

## src：这是Redis核心源码所在的目录，包含了Redis服务器的所有实现代码。下面详细介绍src目录中的主要文件和子目录：

- server.c：Redis服务器的入口点，包含main函数。负责初始化服务器、事件循环等。
- networking.c：处理网络相关操作，如连接、读写客户端数据等。
- ae.c：Redis的事件循环实现（A simple event-driven programming library），支持epoll、kqueue、select等。
- adlist.c：一个简单的双向链表实现。
- dict.c：Redis的字典（哈希表）实现，用于存储键值对。
- sds.c：简单动态字符串（Simple Dynamic Strings）的实现，Redis中字符串的基本数据结构。
- zmalloc.c：内存分配封装，用于跟踪内存使用情况，支持使用jemalloc或libc。
- object.c：Redis对象的实现，Redis中所有数据都被封装为对象（robj）。
- db.c：数据库相关的操作，如键的增删改查。
- t_string.c、t_list.c、t_hash.c、t_set.c、t_zset.c：分别实现了字符串、列表、哈希、集合、有序集合等数据类型的操作。
- redis.h：主要的头文件，包含了许多结构定义和函数声明。
- util：一些实用工具函数，如字符串处理、随机数生成等。
- modules：与Redis模块系统相关的代码。
- aof.c：AOF（Append Only File）持久化相关实现。
- rdb.c：RDB持久化相关实现。
- replication.c：主从复制功能的实现。
- sentinel.c：Redis Sentinel（哨兵）的实现。
- cluster.c：Redis集群的实现。
- scripting.c：Lua脚本功能的实现。
- slowlog.c：慢查询日志的实现。
- bio.c：后台I/O操作（Background I/O）的实现，用于在后台执行一些耗时的操作（如AOF写入、关闭文件等）。
- pubsub.c：发布/订阅功能的实现。
- multi.c：事务（multi/exec）功能的实现。
- debug.c：调试相关的命令实现，如DEBUG命令。
- crc64.c、crc16.c：CRC校验码的实现。
- endianconv.c：字节序转换相关函数。
- ziplist.c、intset.c、quicklist.c等：Redis中特殊的数据结构实现，用于优化内存使用。
- evict.c：内存淘汰策略的实现。
- expire.c：键的过期处理。
- geohash.c、geo.c：地理位置相关功能的实现。
- hyperloglog.c：HyperLogLog数据结构的实现。
- latency.c：延迟监控的实现。
- lazyfree.c：惰性删除的实现。
- localtime.c：时间处理函数。
- lzf_c.c、lzf_d.c：LZF压缩算法的实现（用于RDB压缩）。
- memtest.c：内存测试。
- notify.c：键空间通知的实现。
- rax.c：基数树（Radix Tree）的实现，用于Streams等。
- stream.c：Redis Stream数据结构的实现。
- tls.c：TLS/SSL支持。
- tracking.c：客户端缓存跟踪（Redis 6中的特性）。
- defrag.c：内存碎片整理。
- acl.c：访问控制列表（ACL）的实现（Redis 6新增）。
- connhelpers.h、connection.c：Redis 6中重构的连接抽象层。
- blocked.c：处理阻塞命令（如BLPOP、BRPOP等）。
- loadlib.c：用于加载动态库（模块）的函数。
- tests：包含Redis的测试代码，主要是Tcl测试脚本（位于tests目录下）和单元测试（在src目录下的tests子目录中）。Redis有非常完善的测试套件。

## utils：包含一些实用工具脚本，如：

- redis_init_script：Redis的初始化脚本（用于启动、停止等）。
- redis-sha1.rb：用于生成Lua脚本的SHA1校验和。
- create-cluster：用于创建Redis集群的脚本。
- hiredis、lru等子目录下的工具。
- redis.conf：Redis的默认配置文件。

## sentinel.conf：Redis Sentinel的默认配置文件。

## COPYING：版权信息（BSD许可证）。

## Makefile、Makefile.dep：构建文件。

## CONTRIBUTING.md：贡献指南。

## README.md：项目概述和基本使用说明。

## man：Redis命令的手册页。

## modules：Redis模块的示例代码。

以上是Redis 8源码的主要目录结构。通过阅读源码，可以深入理解Redis的内部机制。建议从server.c的main函数开始，逐步了解服务器的启动过程，然后深入到事件循环、网络处理、命令执行等关键部分。
