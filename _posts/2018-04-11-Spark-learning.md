---
layout:     post
title:      "Spark学习笔记——基础"
date:       2018-04-11 16:47:00
tags: Spark
---
> 不适合人类阅读的学习笔记  

> 有问题经常去**[stackoverflow.com](https://stackoverflow.com/)**上找找

## 环境搭建
---
- 首先确保电脑安装了JAVA Development Kit JDK(使用java -version查看版本)

- 安装hadoop（比如我在安装了hadoop-2.7.5），后面下载spark的版本时也要选择与hadoop版本一致的spark版本。然后添加hadoop路径到PATH（修改/etc/profile文件）

- 下载spark，解压，设置路径。 ———[详细设置](https://www.cnblogs.com/earendil/p/5564492.html)

- 调整日志级别控制输出的信息量：在spark了文件目录的conf目录下将log4j.properties.template 复制为  log4j.properties, 然后找到 log4j.rootCategory = INFO, console。将其中的INFO改为WARN即可。

- [sbt安装网址](https://www.scala-sbt.org/download.html)

## 编程环境
---
- spark支持多种语言的编写，包括Python，Java，scala以及R语言，**本篇中均采用scala作为编程语言**。
- 使用的编译器为intellij IDEA，工程为maven项目

###### 编译器的一些使用技巧

- ctrl + Q 在intellij中可以快速地查看变量的类型

- Maven 项目使用maven自带的打jar包的即可，不推荐在build当中打jar包

- 新建的Maven项目很可能缺失很多spark的库，需要修改pom文件来使得编译器引入这些库

## spark下的 wordcount
---
> 摘自官方文档

```
text_file = sc.textFile("hdfs://...") //文件需要放在hdfs上
counts = text_file.flatMap(lambda line: line.split(" ")) \
             .map(lambda word: (word, 1)) \
             .reduceByKey(lambda a, b: a + b)
counts.saveAsTextFile("hdfs://...")
```
- 精简版：  (足见scala的优美与强大)
```
val counts = sc.textFile(“hdfs://...”)
counts.flatMap(_.split(" ")).map(x => (x,1)).reduceByKey(_ + _).collect().foreach(println) //打印结果
```
- 注意：上面的.collect()不能少，因为这是一个action操作，一个语句如果没有action操作则spark什么也不会做。同时，**读取文件的路径一定要用引号括起来！**


## 关于jar包以及提交集群运行
---
#### `spark-submit`命令
- spark-submit脚本用于在集群上启动应用程序,它位于Spark的bin目录中。

###### 命令行提交

- 命令行下切换到spark的安装目录，执行

```
./bin/spark-submit \  
 --class <main-class> \
 --master <master-url> \
 --deploy-mode <deploy-mode> \
 --conf <key>=<value> \  
     ... # other options  
 <application-jar> \  
 [application-arguments]
```

###### 脚本方式：(创建并编辑.sh脚本文件，赋予执行权限即可)

```
input=/data/
output=/AR_res/
    hdfs dfs -rm -r $output
    hdfs dfs -rm -r /user_res
    spark-submit \
        -v \
        --name "ARsMiner" \
        --class "com.hazzacheng.AR.Main" \
        --executor-cores 4 \
        --executor-memory 10G \
        --driver-memory 20G \
        AR.jar \
        $input \
        $output \
        2>&1 | tee log/AR_log
    rm -rf AR_res/
    hdfs dfs -get $output
    cat /root$output/part* > /root/res
    #sort /root$output/part* > /root/res
```

###### 常用的参数讲解

- --class：应用程序的入口点,main函数所在的类（例如org.apache.spark.examples.SparkPi）

- --master：群集的主网址（例如spark：//23.195.26.187：7077）

- --deploy-mode：是否将驱动程序部署在工作节点（cluster）上，或作为外部客户机（client）本地部署（默认值：client）

- --conf：Key = value格式的任意Spark配置属性。对于包含空格的值，用引号括起“key = value”（参见示例）。

- application-jar：包含应用程序和所有依赖关系的捆绑jar的路径。该URL必须在集群内全局可见，例如hdfs：//路径或所有节点上存在的file：//路径。

- application-arguments：参数传递给主类的main方法（如果有的话）

- 常见的部署策略是从与您的工作机器物理上位于的网关机器提交应用程序（例如，独立的EC2集群中的主节点）。在此设置中，client模式是适当的。在client模式下，驱动程序直接在spark-submit过程中启动，该过程充当集群的客户端。应用程序的输入和输出连接到控制台。因此，该模式特别适用于涉及REPL（例如Spark shell）的应用。

- 或者，如果您的应用程序从远离工作机器（例如本地在笔记本电脑上）的机器提交，通常使用cluster模式来最大限度地减少驱动程序和执行程序之间的网络延迟。

###### 其他的一些示例
```
# Run application locally on 8 cores
./bin/spark-submit \
  --class org.apache.spark.examples.SparkPi \
  --master local[8] \
  /path/to/examples.jar \
  100
```
```
# Run on a Spark standalone cluster in client deploy mode
./bin/spark-submit \
  --class org.apache.spark.examples.SparkPi \
  --master spark://207.184.161.138:7077 \
  --executor-memory 20G \
  --total-executor-cores 100 \
  /path/to/examples.jar \
  1000
```
```
# Run on a Spark standalone cluster in cluster deploy mode with supervise
./bin/spark-submit \
  --class org.apache.spark.examples.SparkPi \
  --master spark://207.184.161.138:7077 \
  --deploy-mode cluster \
  --supervise \
  --executor-memory 20G \
  --total-executor-cores 100 \
  /path/to/examples.jar \
  1000
```
```
# Run on a YARN cluster
export HADOOP_CONF_DIR=XXX
./bin/spark-submit \
  --class org.apache.spark.examples.SparkPi \
  --master yarn \
  --deploy-mode cluster \  # can be client for client mode
  --executor-memory 20G \
  --num-executors 50 \
  /path/to/examples.jar \
  1000
```
```
# Run a Python application on a Spark standalone cluster
./bin/spark-submit \
  --master spark://207.184.161.138:7077 \
  examples/src/main/python/pi.py \
  1000
```
```
# Run on a Mesos cluster in cluster deploy mode with supervise
./bin/spark-submit \
  --class org.apache.spark.examples.SparkPi \
  --master mesos://207.184.161.138:7077 \
  --deploy-mode cluster \
  --supervise \
  --executor-memory 20G \
  --total-executor-cores 100 \
  http://path/to/examples.jar \
  1000
```

## spark程序入口

- Spark SQL中所有功能的入口点是 SparkSession 类. 要创建一个 SparkSession, 仅使用 SparkSession.builder()就可以了：
```
import org.apache.spark.sql.SparkSession
val sparkses = SparkSession
  .builder()	//必须有
  [.appName("Spark SQL basic example") ]
  [.config("spark.some.config.option", "some-value")]
  [.master("local")]
  .getOrCreate() //必须有
// For implicit conversions like converting RDDs to DataFrames    //即需要用到类型转换时，要引入这个以你的变量名字开头的隐式转换包
import sparkses.implicits._
```

> 未来Dataset可能会取代RDD作为主要使用的API，而RDD会成为最底层的供用户使用的API

- spark一般的入口是 sparkcontext类：
```
import org.apache.spark.{SparkConf, SparkContext}
...
 val conf = new SparkConf()[.set(...)...]
 val sc = new SparkContext(conf)
```



## 一些注意点
---
> 如要学习spark请看官方文档以及源码

- **这里推荐一个[官方文档的中文版](http://spark.apachecn.org/)供英语薄弱的朋友阅读。**

- 今天试验了FP-Growth算法，打包到集群运行时报错:
```
Items in a transaction must be unique but got WrappedArrayMaven
```
出现此问题的主要原因是fpg算法要求输入的数据是`RDD(Array[String])`类型，但是Array类型中是不允许出现重复的内容的，所以才会出现这个错误，只需要对输入的数据做个distinct即可

- spark中出现一长细条的信息才是报错

- List 的 `distinct` 方法会对列表去重

- item::list 将新生成一个列表，item会成为新列表的有元素

- Array 不能被`flatMap`,必须为`list.(?)`

- scala中的`.sortBy()`方法如果在括号里最前面加上一个减号表示按逆序排序。



<br>
> 最后更新于2018.4.15
