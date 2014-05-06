# 全栈系列之 MongoDB 初级篇

## 简介

本文介绍一些基本概念，涉及到文档、集合和数据库，以及一些基本的操作。

那MongoDB是干嘛的呢？

其实关键词还是NoSQL

### 基础的概念

#### 文档

先看一个我们熟悉的js里面的对象：

```shell
{"name" : "yaochun" , "company" : "wandoujia" , "group" : "w3cplus" , "job" : "fe"}
```

其实这也是MongoDB里面的核心概念：**文档**

就是键值对，但是有一些特有的特性：

1. 这个键值对是有序的：

```shell
{"name" : "yaochun" , "company" : "wandoujia"}

{"company" : "wandoujia" , "name" : "yaochun"}

```

所以以上两个文档是不一样的。

2. 键是字符串，不能还有\0，**.** 和 **$** 有特别的意义，**_**开头的是保留的

3. 值可以是双引号的字符串，也可以是其他几种数据类型。

4. 区分类型和大小写：

```shell
{"name" : "yaochun" , "company" : "wandoujia" , "age" : 50}

{"company" : "wandoujia" , "name" : "yaochun" , "age" : "50"}

```

所以以上两个文档也是不一样的。


5. 文档里面的键不能重复，否则视为非法。

#### 集合

集合其实就是**一组**文档。

集合的命名也有规则：

1. 不能是空字符串
2. 也不能还有**\0**字符
3. 不能以一些系统集合的保留的前缀，比如**system.**这样开头
4. 也不能包含$

集合里面有没有数学里面的子集合呢？

可以用*.*来划分子集合。

#### 数据库

数据库其实是由多个集合组成。数据库之间是相对独立的，存储在不同的文件中。

数据库的命名同样也有规则：

1. 不能是空字符串
2. 也不能还有**\0** 、 $ 类似这些字符
3. 小写
4. 最多64字节

因为数据库名其实最终都会变成文件系统的文件，所以命名有一定的约束。

保留的数据库名词：

1. admin
2. local
3. config


### 数据类型介绍

其实大家发现没有，文档的结构类似我们常用的**JSON**。那在MongoDB里面的有哪些数据类型呢？

> null

```shell
{ "freetime" : null }

```


> 日期

```shell
{ "date" : new Date() }

```

> 数组

实例：

```shell
{ "keywords" : [ "yaochun" , "wandoujia" , "w3cplus" ] }

```

> 内嵌文档

实例：

```shell
{ "info" : {"yaochun" , "company" : "wandoujia" , "group" : "w3cplus" } }

```

其实就是文档包含某个文档


> 正则

实例：

```shell
{ "name" :  /yaochun/i }

```

> 代码

实例：

```shell
{ "code" :  function() {/*..*/} }

```


其他的比较基础的比如：布尔、字符串等就不在这里介绍了。




### 基础的操作

一般包含：插入、更新、删除和查询

#### 插入

实例：

```shell
//welcome to join us: http://www.wandoujia.com/join
db.wandoujia.fe.insert({ "name" : "yourname" })

```

其实插入从上面的实例直观的看到：

1. 也是用*insert*
2. insert方法里面传入的其实就是一个文档


那没有什么主键吗？

MongoDB的插入操作默认会给文档加一个 *_id* 。





#### 更新






#### 删除


实例1：

```shell
db.book.mongodb.remove()

```

这个代表我把book这个集合的子集合mongodb的所有文档都删除掉，但是子集合mongodb本身还在，索引也会保留。



实例2：

```shell
db.book.mongodb.remove({ "part" : "primary" })

```

这里给remove这个操作传递了一个文档，做查询和筛选用的。符合条件的文档才会被删除。

这个代表我把book这个集合的子集合mongodb中所有part为primary的删除掉。

#### 查询

初级教程里面我们只是简单地看看基本的查询方式，在中级里面会全面地去学习一下。


实例1：

```shell

//welcome to join us: http://www.wandoujia.com/join
db.wandoujia.jobs.find()

```

实例2：

```shell

//welcome to join us: http://www.wandoujia.com/join
db.wandoujia.jobs.find({ "category", "fe" , "level" : 2 })

```

从上面的实例中，我们看出，最基本的查询可以用**find**

而且find里面可以传递参数，比如某个或者某几个文档来指定查询的条件。
