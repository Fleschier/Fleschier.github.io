---
layout:     post
title:      "Scala方法查询记录"
date:       2018-07-12 16:40:00
tags:   ๑Scala
---

> 仅供查询，禁止转载

#### List的一些方法和用途

|方法|用途|
|---|---|
|List()或者Nil|表示空列表|
|List("Cool","Tools")|创建一个新的List[String],包含两个值:"Cool","Tools"|
|val thrill = "Will"::"Fill"::Nil|创建一个新的List[String]包含两个值："Will"和"Fill"|
|List("a","b"):::List("c","d")|将两个列表拼接起来(返回一个新的列表List("a","b","c","d"))|
|thrill(2)|返回列表thrill下标为2(从0开始计数)|
|thrill.count(s => s.length == 4)|对thrill中长度为4的字符串进行计数|
|thrill.drop(2)|返回去掉了thrill的头两个元素的列表|
|thrill.dropRight(2)|返回去掉了thrill后两个元素的列表|
|thrill.exists(s => s=="until")|判断thrill中是否有字符串元素的值为"until"，返回值为Boolean|
|thrill.filter(s => s.length == 4)|按顺序返回列表thrill中所有长度为4的元素列表|
|thrill.forall(s => s.endsWith("1"))|表示列表中是否所有元素都以字母"1"结尾|
|thrill.foreach(s => println(s)) / thrill.foreach(println)|遍历列表执行打印|
|thrill.head|返回列表的首个元素|
|thrill.init|返回列表thrill除最后一个元素之外其他元素组成的列表|
|thrill.isEmpty|判断列表是否为空|
|thrill.last|返回thrill的最后一个元素|
|thrill.length|返回列表的元素个数|
|thrill.map(s => s + "y")|返回一个对列表thrill所有字符串元素末尾添加"y"的新字符串列表|
|thrill.makeString", "|返回用列表thrill的所有元素组合成的字符串，以", "连接各个元素|
|thrill.filterNot(s => s.length == 4)|按顺序返回列表中所有长度不为4的元素列表|
|thrill.reverse|返回包含列表thrill的逆序列表|
|thrill.sort( (s,t) => s.charAt(0).toLower < t.charAt(0).toLower)|返回包含thrill的所有元素，按照首字母小写顺序排序的列表|
|thrill.tail|返回列表thrill除首个元素之外其他元素组成的列表|


<br>
> 最后更新于2018.7.14
