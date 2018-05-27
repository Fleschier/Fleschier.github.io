---
layout:     post
title:      "Spark学习笔记——进阶"
date:       2018-04-11 16:47:00
tags: ◢Spark
---
> 不适合人类阅读的学习笔记

> **有问题经常去[stackoverflow.com](https://stackoverflow.com/)上找找**
> 或者直接去看官方的API原版或者翻译版:[官方文档的中文版](http://spark.apachecn.org/)


## DataSet 与 DataFrame
---

- Dataset是特定域对象中的强类型集合，它可以使用函数或者相关操作并行地进行转换等操作。每个Dataset都有一个称为DataFrame的非类型化的视图，这个视图是行的数据集。

- DataSet和RDD主要的区别是：DataSet是特定域的对象集合；然而RDD是任何对象的集合。DataSet的API总是强类型的；而且可以利用这些模式进行优化，然而RDD却不行。

- Dataset的定义中还提到了DataFrame，DataFrame是特殊的Dataset，它在编译时不会对模式进行检测。在未来版本的Spark，Dataset将会替代RDD成为我们开发编程使用的API。

###### 创建DataFrame
```
import org.apache.spark.sql.SparkSession
...
val sparkses = SparkSession
				.builder()
                .getOrCreate() //这两个为必须有的
val df = sparkses.read.csv("...filename.csv")
//这里read后面的方法名称与具体要读的文件类型有关
df.show()  //打印内容
```

###### 创建DataSet

-  方法一：创建case class （对于复杂的数据没有成功）
- 例如
```
val sparkses = SparkSession
				.builder()
                .getOrCreate()
case class KeyValue(key: Int, value: String)
import sparkses.implicit._   //引入隐式转换库
val df = Seq((1,"asdf"),(2,"34234")).toDF("key", "value")
val ds = df.as[KeyValue]
// org.apache.spark.sql.Dataset[KeyValue] = [key: int, value: string]
```

- case class的参数上限为22

- 方法二：以元组隐式转化
- 例：
```
val tupDs = df.as[(Int,String)]
// org.apache.spark.sql.Dataset[(Int, String)] = [_1: int, _2: string]
```




<br>
> 最后更新于2018.4.21
