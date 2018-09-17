---
title: 1 Introduction of Database Systems
date: 2018-03-11 19:43:02
category: Database
tags: [Data Model, Schema]
---
<font size=6>数据库基本概念介绍
<!--more-->

---
<font size=5>数据库系统 (database system, DBS) : 
<font size=3>DBS是一个互相有关的数据的集合和一系列程序来访问数据库。

<font size=5>使用DBS的目的 : 
<font size=3>使用DBS的目的能够解决以下几点问题 : 
- 数据冗余 (data redundancy) 和矛盾 (data inconsistency) : 我们可能会把同样的数据存入不同的文件中，这样就会造成数据冗余。当改动数据时，可能会忘记将全部文件的同一数据同时改变，这样就会造成数据的矛盾。且在添加对数据的限制时，可能无法对所有需要限制的数据项进行限制。
- 访问数据的难度 : 当我需要访问特定需求的数据时需要写一个程序进行获取，但是，当我们需要获得其他数据时就需要编写新程序。这样做就会增加难度。
- 数据隔离 (data isolation) ： 数据被分离在多个文件中，这些文件可能有不同的格式，所以编写程序来处理数据会比较困难。
- 原子性问题 (atomicity problem) : 在DBS中一些行为需要同时发生或者都不发生，比如将银行A中钱转到银行B，钱从A的账户中减少与B的账户增加就需要同时发生或者都不发生。
- 同时访问异常 (concurrent-access anomalies) ： 当许多人同时访问同一数据可能会造成异常，DBS需要能够同时正确地处理数据。
- 安全问题（security problems) : 不是所有用户都能看见同一数据。每个用户都有访问数据的限制，只能看见能够看见的数据。
<br/>

<font size=5>数据抽象 (data abstraction) : 
<font size=3>为了使DBS能够使用，我们需要将数据进行抽象，抽象后的数据有三层 : 分别是物理层，逻辑层，视图层。
- 物理层 (physical level) : 物理层描述了数据是如何被存储的。也就是复杂数据结构的细节实现。
- 逻辑层 (logical level) : 逻辑层描述了那些数据被存储和这些数据的关系。将数据描述为一些具有相关性的结构。在逻辑层中就算是简单的结构，其背后的物理层都有着复杂的结构，但是数据库管理员却并不需要了解这个复杂性，这就是物理数据独立 (physical data independece)。
- 视图层 (view level) : 虽然逻辑层我们可以使用简单的结构，但是在面对大量的数据时，就产生了复杂性，许多用户可能并不需要了解所有的信息，他们只需知道他们想知道的，所以视图层就是为了简化用户与数据库之间的交互。
<br/>

<font size=5>实例 (instance) 与模式 (schema) : 
<font size=3>储存在DBS中的数据集合就是实例，而数据库的所有设计就是模式，或可以这样理解，模式就是程序里的变量声明，实例就是所有变量的值。模式与数据抽象有着密切关系，同样也分为三层 : 
- 物理模式 (physical schema) : 物理模式描述物理层的数据库设计。
- 逻辑模式 (logical schema) ： 逻辑模式描述逻辑层的数据库设计。
- 视图模式 (view schema, subschema) : 视图模式可以有许多个，描述了许多不同的数据库视图。
<br/>

<font size=5>数据模型 (data model) : 
<font size=3>数据模型是一个概念性工具用来描述数据，数据之间的关系，数据语义 (data semantics)，一致性限制 (consistency constraints)。

一个数据模型提供了物理，逻辑，视图三层的设计。

有许多的数据模型，主要分为四种：关系模型 (relational model)， 实体关系模型(entity-relationship model)，基于对象数据模型 (object-based data model),，半结构化数据模型 (semistructured data model)。不用担心，我将在以后娓娓道来。