---
title: Transaction学习笔记
date: 2017-12-22 14:02:40
tags:
---

#### 0.事务的特性
    1. 原子性(Atomicity)
    2. 一致性(Consistency)
    3. 隔离性(Isolation)
    4. 持久性(Durability)
	
<!--more-->
    
#### 1.事务隔离级别(Transaction Isolation Level)
    1. READ_UNCOMMITTED
    2. READ_COMMITTED
    3. REPEATABLE_READ
    4. SERIALIZABLE
    
#### 2.数据在高并发下产生的问题
    1. Dirty Read(脏读)
    2. Unrepeatable Read(不可重复读)
    3. Phantom Read(幻读)
    

|事务隔离级别|脏读|不可重复读|幻读
|-|-|-|-
|READ_UNCOMMITTED|<font color=green>允许</font>|<font color=green>允许</font>|<font color=green>允许</font>
|READ_COMMITTED|<font color=red>禁止</font>|<font color=green>允许</font>|<font color=green>允许</font>
|REPEATABLE_READ|<font color=red>禁止</font>|<font color=red>禁止</font>|<font color=green>允许</font>
|SERIALIZABLE|<font color=red>禁止</font>|<font color=red>禁止</font>|<font color=red>禁止</font>

#### 3.Spring事务

##### 事务传播行为(Transaction Propagation Behavior)
    1. PROPAGATION_REQUIRED
    2. PROPAGATION_REQUIRES_NEW
    3. PROPAGATION_NESTED
    4. PROPAGATION_SUPPORTS
    5. PROPAGATION_NOT_SUPPORTED
    6. PROPAGATION_NEVER
    7. PROPAGATION_MANDATORY





#### 4.参考资料
[Transaction那点事儿](https://my.oschina.net/huangyong/blog/160012)

