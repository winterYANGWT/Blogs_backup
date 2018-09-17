---
title: 2 Database Language
date: 2018-03-14 23:00:31
category: Database
tags: [SQL]
---
<font size=6>数据库语言
<!--more-->

---
<font size=5>数据库语言 (database language) : 
<font size=3>数据库提供了两种数据库语言：
- 数据定义语言 (data-definition language, DDL) : DDL指定了数据库模式。一种特殊的DDL叫做数据存储定义语言 (data storage and definition language), 这种语言定义了数据库模式的细节实现。DDL同时具有一致性限制 : 
    - 完整性限制 (integrity constraints) : 对整个数据库数据进行限制。若一个操作不满足这种限制是不允许发生的。
    - 引用完整性 (referential integrity) : 一个表引用其他表的数据必须是存在的。当一个表A引用了表B的主关键字，当我们删除表B中的一些数据前，必须保证表A中引用了表B中被删除数据的数据被删除。
    - 断言 (assertions) : 前面的两条都是断言的一部分，断言可以更加普遍的限制，比如“一个学院每学期必须提供8门课程”
    - 授权 (authorization) : 限制不同用户的权限，一些用户只有读取的权限，另外一些可以添加的权限，等等。

  DDL的输入为指令，输出为数据字典 (data dictionary), 是一种元数据。

- 数据操作语言 (data-manipulation language, DML) : DML让使用者能够访问和操作数据库。 其类型有 : 
    - 获取数据
    - 插入新数据
    - 删除数据
    - 修改数据

  也可被分为两种类型 : 
    - 过程化 (procedural DMLs) : 要求使用者定义需要怎样的数据和怎样获取数据。
    - 声明化 (declarative DMLs, nonprocedural DMLs) : 要求使用者指定需要什么数据但并不需要该如何获得该数据。

在后面我们将学习SQL语言，一种被广泛用于数据库的语言。