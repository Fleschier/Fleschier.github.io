---
layout:     post
title:      "Spark学习笔记"
subtitle:   "Keep foolish  Keep hungry"
date:       2018-04-11 16:47:00
author:     "Fleschier"
header-img: "img/Spark/Spark-bg.jpg"

---
> 不适合人类阅读的学习笔记

## 环境
---
- spark支持多种语言的编写，包括Python，Java，scala以及R语言，本篇中均采用scala作为编程语言。
- 使用的编译器为intellij IDEA，工程为maven项目

###### 编译器的一些使用技巧

- ctrl + Q 在intellij中可以快速地查看变量的类型

- Maven 项目使用maven自带的打jar包的即可，不推荐在build当中打jar包

## 一些注意点
---

- 今天试验了FP-Growth算法，打包到集群运行时报错:
```
Items in a transaction must be unique but got WrappedArrayMaven 项目使用maven自带的打jar包的即可，不推荐在build当中打jar包
```
出现此问题的主要原因是fpg算法要求输入的数据是RDD(Array[String])类型，但是Array类型中是不允许出现重复的内容的，所以才会出现这个错误，只需要对输入的数据做个distinct即可

- spark中出现一长细条的信息才是报错

- List 的distinct 方法会对列表去重

- item::list 将新生成一个列表，item会成为新列表的有元素

- Array 不能被flatMap.必须为list.(?)

- scala中的`.sortBy()`方法如果在括号里最前面加上一个减号表示按逆序排序。

<br>
> 最后更新于2018.4.11