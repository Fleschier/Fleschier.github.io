---
layout:     post
title:      "Scala学习笔记——进阶"
date:       2018-04-6 16:47:00
tags: <Scala>
---

> 不适合人类阅读的学习笔记  

## case class与模式匹配
---
- case class一般被翻译为样例类，它是一种特殊的类，能够被优化以用于模式匹配。

-

## scala性能测试
---
- 测试程序的运行时间的函数：`System.currentTimeMillis()`

- 用法：

```
[...]
  val time = System.currentTimeMillis()
  [要测试运行时间的代码段]
  println(" 耗时: " + (System.currentTimeMillis() - time))  //以时间差来看运行时间
[...]
```

## 函数式循环
---

- 函数式编程的循环都是用迭代来实现的

- 例1：对于一个Int数组a,对里面每个元素执行 +1的操作
```
a.map{x =>
  val y = x + 1  //因为Int是不可变类型，所以必须要新建一个值来存储改变后的值
  y  //返回值是y
}
```

- 例2：对于一个Int数组，每找出一个大于5的数count就加1
```
var count:Int = 0
a.foreach{x =>      //与map遍历方式不同，foreach不会对里面的内容修改，所以匿名函数也不需要返回值
  if(x >  5)
    count += 1
}
```



<br>

>最后更新于2018.4.21
