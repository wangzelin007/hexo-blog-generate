---
title: mysql
tags: []
toc: true
mathjax: true
date: 2019-06-27 10:49:32
categories:
---
innodb 支持行锁、事务，并发性能高。
局部性原理 多取相邻的数据放到内存
按页(16384 16kb)取
页结构
File Header 文件头部 38字节 页的通用信息
Page Header 页面头部 56字节 数据页专有信息
Infimun + Supremum Records 最小记录和最大记录 26字节 两个虚拟的行记录
User Records 用户记录 实际存储的行记录
Free Space 空闲空间 页中空闲空间
Page Directory 页面目录 页中某些记录的相对位置
File Trailer 文件尾部 8kb 校验页是否完整

行格式 一列最多65535 所以有可能行溢出
Compact Redundant Dynamic Compressed
Compact结构：变长字段长度列表 null标志位 记录头信息 列1数据 列2数据 ......
Compact Redundant 对于占用存储空间非常大的列，记录真实数据处只会存储该列一部分数据，剩余数据分散存储在其他页中，记录真实数据处用20个字节指向这些页的地址。
Dynamic Compressed不会在记录真实数据处存储数据，他们把所有数据都存储在其他页，只在真实数据处存储其他页面的地址，Compressed会采用压缩算法对页面进行压缩。

真实数据隐藏列包含row id, transaction id 事务id, roll_pointer
![真实数据版本链](http://ww3.sinaimg.cn/large/006tNc79ly1g4mqqua0poj30nu0icta8.jpg)

innodb 聚集 
主键索引 非叶子结点存储主键，叶子节点存储完整数据
辅助索引 非叶子结点存储辅助键，叶子节点存储主键值，需要回表查询数据。

innodb 高度和数据量换算 
假设每一行数据1kb
根节点存储：16k->16384/(8主键+6指针) ~= 1170
第二层树存储数据量为：1170*(16/1)~=2w
第三层树存储数据量为：1170*1170*(16/1)~=2000w

myisam 堆表
mysql 索引

utf8 0-3字节
使用 utf8mb4 0-4字节 可以存表情等特殊字符

最左前缀原则 
对于网址可以逆序存储使用索引：WHERE url LIKE 'moc%';

mysql 锁

mysql 事务 ACID
场景：小明向小强转账10元
原子性 atomicity
转账操作是一个不可分割的操作，要么失败，要么成功，不存在中间状态。把这种规则称为原子性。
一致性 consistency
数据一致。
隔离性 isolation
两个操作不能互相影响。
持久性 durability
记录永久保存。

隔离性详解
修改隔离性
set session transaction isolation level read uncommitted;
查看隔离性
select @@tx_isolation;

## 读未提交 READ UNCOMMITTED
  一个事务可以读到其他事物还没有提交的数据，会出现脏读、幻读、不可重复读。

>一个事务读到了另一个未提交事务修改过的数据，即脏读

## 读已提交 READ COMMITED
一个事务只能读到另一个已提交事务修改过的数据，并且其他事务每次对该数据修改并提交，该事务都能查询到最新值，会出现不可重复读、幻读

>不可重复读与幻读的区别是前者是update和delete造成，后者是insert造成。前者是一条数据，后者是多条数据。
>如果事务A查询出一些记录，事务B又插入了符合的记录，那么事务A再次查询时，会读到最新的记录，即幻读。

## 可重复读 REPEATABLE READ 默认
事务A第一次读过某条记录后，即时事物B修改了该记录并提交，事务A再次读取还是第一次读到的值，即可重复读，但是还是会出现幻读问题。(但是mysql不会出现，和标准不同)

## 串行化 SERIALIZABLE
不允许出现读-写、写-读的并发操作。不会出现脏读、幻读、不可重复读等现象。

Readview
对于READ UNCOMMITTED 事务，直接读取最新版本记录；对于SERIALIZABLE 事务，使用加锁方式来访问记录；对于READ COMMITTED 和 REPEATABLE READ 隔离级别的事务，需要使用版本链。

m_ids：当前活跃的读写事务id列表。(即没有提交的)
min_trx_id: 当前系统活跃的读写事务中最小的id。
max_trx_id: 系统应该分配给下一个事务的id值。
creator_trx_id: 当前事务的id。

READ COMMITTED 每次读取数据都会生成ReadView
REPEATABLE READ 只在第一次读取数据时生成ReadView

MVCC Multi-Version Concurrency Control 多版本并发控制，指的就是使用READ COMMITTED、REPEATALBE READ这两种隔离级别的事务执行SELECT操作时访问版本链的过程。高并发的读。

事务的自动提交
SHOW VARIABLES LIKE 'autocommit';
如果不使用 START TRANSCATION 或者 BEGIN 语句开启一个事务，那么每一条语句都算一个独立的事务。

隐式提交
输入某些语句后会隐式的提交之前的语句，比如DDL

保存点 savepoint
SAVEPOINT 保存点名称
ROLLBACK TO 保存点名称

锁
读锁与写锁
+ 读锁：共享锁、Shared Locks、S锁
+ 写锁： 排它锁、Exclusive Locks、X锁
+ select： 不加锁，也不会被阻塞。

select ... lock in share mode
select ... for update
DELETE 删除数据，先加X锁，再删除
INSERT 插入数据，先加隐式锁确保提交前不被别的事务访问到。
UPDATE 
+ 如果更新没有导致存储空间变化，会先加X锁，再对记录进行修改。
+ 如果更新导致存储空间变化，会先加X锁，然后删除记录，再insert新纪录。

行锁
+ LOCK_REC_NOT_GAP: 单个行记录上的锁。
+ LOCK_GAP: 间隙锁，锁定一个范围，但不包括记录本身。GAP锁的目的，是为了防止同一事物的两次当前读，出现幻读的情况。
+ LOCK_ORDINARY: 锁定一个范围，并且锁定记录本身。对于行的查询，都是采用该方法，主要目的是解决幻读的问题。

READ COMMITTED 只对查出来的数据加锁。







mysql 调试死锁