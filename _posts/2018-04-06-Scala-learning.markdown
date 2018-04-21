---
layout:     post
title:      "Scala学习笔记"
subtitle:   "Keep foolish, Keep hungry"
date:       2018-04-6 16:47:00
author:     "Fleschier"
header-img: "img/Scala/Scala-bg.jpg"
tags: Scala
---

>不适合人类阅读的学习笔记

## 编译环境
---
- 编译首选jetbrain的intellij IDEA，下载一个Scala plugin，然后选择创建maven工程，模板选择Scala对应的模板即可。main函数应当写在object文件中，object通过创建Scala class文件选项创建。

- 如果要写分布式处理程序的话，需要自己重写配置文件

- Scala注释与C++类似

#### 示例程序
```
object HelloWorld {
   def main(args: Array[String]) {
      println("Hello, world!") // 输出 Hello World
   }
}
```

#### 执行scala程序

- 脚本执行：我们可以将 Scala 表达式写在一个文件里，比如 Hello.scala。在命令行中直接输入 scala Hello.scala

- 作为应用程序执行：作为应用程序执行时，我们需要在一个单例对象中定义入口函数 main，经过编译后就可以执行该应用程序了。

## 基础
---

> scala的语句分号规则与C++相类似(一般都不用加，加了一般也不会错)

> scala中的通配符为'_'，而C++中为'*'

> scala与spark很契合，所以写spark程序推荐使用scala语言

###### 变量

- Scala中变量分为可变变量和不可变变量。可变变量用关键字`var`修饰，不可变变量用`val`修饰。
> 注意scala中变量定义时必须赋初始值

- scala大多数数据结构中的变量默认为val类型

- 特例：若用占位符'_'作为值进行初始化，则String类会被初始化为null,Float,Int,Double等被初始化为0,Char类型会被初始化为"?".

- 如果用lazy关键字修饰变量，则他只有在真正被使用时才会被赋值。
> 注意lazy关键字只能修饰val类型变量，不能修饰var类型

#### 输入输出
###### 输出：`print("...")` 或者 `println("...")`

###### 输入：
> 注意，控制台的输入均为string类型，需要在后面加上.toInt  .toFloat等转换操作

- 控制台输入：
```
 val scan = scala.io.StdIn  //设置scan
 val n = scan.readLine.trim.toInt  //输入一个int
 val arr = scan.readLine.split(" ").map(_.trim.toInt)  //输入一串数字，之间以空格间隔
 // .trim方法是去掉输入字符串两旁的空格
```

- scala还有一系列专门的用来读下**一个**输入并且可以自动转换的方法，例如：
```
val scan = scala.io.StdIn
val myint = scan.readInt()
val myfloat = scan.readFloat()
val myboolean = scan.readBoolean()
...
//这些方法均可以读取下一个输入并且自动转换类型
```

#### 排序
- 例如：
```
val a = new Array[Int](3)
a(0)  =1
a(1) = 2
a(2) = 0
a.foreach(print)  //结果: 120
val sorted_a = a.sortWith((x,y) => x > y)  //从大到小排序（sortWith的参数为一个lambda函数，返回一个布尔值用于比较）
a.foreach(print) //结果： 210
```

#### 一些注意点

- scala中没有 `++` 操作，可以用 `+= 1` 代替 `++`（x += y ，y可以是一个数字，也可以是一个数字变量，但不能是数组或是其他一些类似结构的某个元素）

- Scala所有数据类型首字母都要大写，因为Scala中所有值类型都是对象，**其中布尔类型应写为“Boolean”**

- Scala中有<= 和 >= 以及逻辑与 && 和逻辑或 || 运算符，与C++相同。

- Scala中String类型就是Java中的String.lang.String类型，因此可以调用Java中String的所有方法（例：`str.reverse`表示字符逆序）

- **Scala中有一类特殊的运算符 "::"(list构造)，":::"(list拼接)，他们是右操作。例如：a::b::Nill执行顺序为(a::(b::Nill))**

#### 一些数据类型

###### 整型和浮点型
 - 整型字面量用于 Int 类型，如果表示 Long，可以在数字后面添加 L 或者小写 l 作为后缀。

- 如果浮点数后面有f或者F后缀时，表示这是一个Float类型，否则就是一个Double类型的。

###### 符号字面量

- 也就是符号类型

- 符号字面量被写成： '<标识符> ，这里 <标识符> 可以是任何字母或数字的标识（注意：不能以数字开头）。这种字面量被映射成预定义类scala.Symbol的实例。

###### string类
- 一个Array[String]类型的数据使用 .toString方法后得到的是一个java.lang.string类型的数据，这个数据直接print是这个Array的地址（一堆符号）

- string类的substring方法，有两个参数，第一个参数为起始位置，第二个参数为结束位置，可以不写，默认为末尾

- 通常，toString 方法会返回一个“以文本方式表示”此对象的字符串。结果应是一个简明但易于读懂的信息表达式。建议所有子类都重写此方法。
- Object 类的 toString 方法返回一个字符串，该字符串由类名（对象是该类的一个实例）、at 标记符“@”和此对象哈希码的无符号十六进制表示组成。换句话说，该方法返回一个字符串，它的值等于：
```
getClass().getName() + '@' + Integer.toHexString(hashCode())
```

- 将java.lang.string以可读的形式打印出来的方法：



###### 元组类型（类似于Python中的元组）

- 如果想要访问元组的内容，可以通过 变量名._N的方式进行。其中N表示元组中元素的索引号。 例：tuple._1 表示tuple中的第一个元素。

- **注意：元组的访问元素的索引是从1开始，而且是不可改变的。**

- 元组用 '==' 进行比较时，是进行内容的比较，这与String类型一致。

###### 数组

> 数组的索引是从0开始的

- 声明格式：
```
val a: Array[String] = new Array[String](3)
或者： val a = new Array[String](3)
```
- 赋值： `a(0) = "abc"`  //注意即时是声明为val变量，数组a的元素的值也是可以改变的。 **同时，使用索引时数组名后面跟的是圆括号而不是方括号，这点与C++不同，切记**

- 可以使用foreach()方法实现遍历。
![](/img/Scala/Scala-test.jpg)

## 流程控制结构
---
###### 判断语句

- if语句格式：
```
if(条件判断){
	[...] //条件判断为真时执行
}
else{
	[...] //条件判断为假时执行
}  //也可以写成 if(){...} else if(){...} 同C++
```

- 与Java，C++不同的是，Scala中if语句可以作为表达式使用。例：
```
scala> val x = if("hello" == "hell") 1 else 0
x: Int = 0
```
从这个例子可以看出，if是个表达式，其返回值可以给变量赋值。**Scala会将if语句的最后一条执行语句作为返回值**

###### 循环语句

- while循环,do..while循环同C++

- for循环格式：
```
for(i <- 表达式){
	[...]
}
```

- 示例：
```
for(i <- 1 to 3){
	println("i = " + i);
}
```
- 结果： i = 1  i = 2  **i = 3** **(1 to 3 的集合是包含3的)**

- 其中 '<-'被称为生成器（generator），for循环实际上是通过集合的遍历来达到循环的目的的。

- 如果希望集合是右开的，可以使用`1 until 5`来实现，范围是[1,5)

- 还可以设置for 循环的步长。例：
```
for(i <- 1 until (10，2))
	println("i = " + i);
结果： i =1 i = 3 .... i = 9
```

- **不过，由于Scala是函数式编程，应当尽量使用迭代来代替循环**

- 例如：使用 `标识符.foreach()`方法来实现对元素的遍历

## case class与模式匹配
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

>最后更新于2018.4.18
