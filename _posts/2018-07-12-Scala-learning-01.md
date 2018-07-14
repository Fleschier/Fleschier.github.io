---
layout:     post
title:      "《Scala编程》阅读记录——入门部分"
date:       2018-07-12 21:40:00
tags:   ๑Scala
---

> 不适合人类阅读的学习笔记

## 入门
---

- scala是一门函数式编程语言,同时也是面向对象的

- 函数值就是对象

- scala对面向对象的实现是纯的：每个值都是对象，每个操作都是方法调用

- 例如，两个Int类型的相加（注意scala里所有的数据类型首字母都是大写，这说明了他们都是类），+实际上是调用了一个名为+的方法

###### 函数式编程以两大核心概念为指导：

- 1.函数是一等的值：函数值可以作为参数传递给其他函数，可以作为返回值，可以保存在一个变量里。还可以在一个函数里定义另一个函数，就像在函数里定义一个整数一样。也可以在定义函数时不指定名字。

- 2.程序中的操作应该将输入值映射成输出值，而不是当场修改数据。例如Java对String的修改就是生成了一个新的String对象而原先的String不变。这个理念的另一种表述就是函数不应该有副作用(sideeffect)。方法只能通过接受入参数和返回结果这两种方式与外部通信，即参数本身不会被修改，这样的方法被称为是“指称透明的”。
函数式编程鼓励不可变的数据结构和指称透明的方法。

- Scala可以选择使用指令式编程的方法，即使用可变数据和副作用编程。但是推荐使用函数式编程。

- scala定义类的简便的写法： `class MyClass(index: Int, name:String)`这样scala编译器就会产生带有两个 **私有** 实例变量和一个接受这两个变量初始值的参数的构造方法类

- 假设name是一个String 类型的变量
`val IfHasUpperCase = name.exists(_.isUpper)`

- 这段代码实现了判断name中是否存在大写字母，并赋值给IfHasUpperCase这个Boolean类型的变量(scala赋值时如果不明确写出变量类型，则编译器会自动判断)

- scala代码将字符串当做更高级的字符序列(sequence) 来处理，用 前提(predicate) 来处理

- 这里的 前提 `_.isUpper` 是scala的函数字面量(当函数字面量的结果类型是Boolean时，可以被称作前提)。它描述了一个接受 **字符** 作为 **入参(以下划线表示)**，判断该字符是否为大写字母的函数。

- 布尔值不能和整数相加

- scala几乎所有语法结构都支持嵌套

- scala输出： `println("....")`

- 注意编译器不会推断函数参数的类型，因此函数中参数的数据类型要显式地写出

- scala函数形式：
```
def FuncName(x:Int, y:Int): Int = {
	if(...){..}
	else{..}
	x
}
```
- 注意函数结果类型前面的冒号不能省（这里函数的格式实际山是与变量保持一致的，即类型跟在冒号后面）

- scala的函数会将函数体里的最后一条语句的值作为函数的返回值（例子里的函数将x的值返回）

- 大多数时候函数的结果类型不需要显式地给出。但是递归函数必须显式地给出结果类型


- scala表达式`if(x>y) x else y`的行为，与Java里的`(x>y)? x:y`的含义一致

- 编译scala脚本：`scala hello.scala`

- 命令行参数可以通过名为args的scala数组来获取：`println("Hello " + args(0) + "!")`

- 然后执行： `$ scala hello.scala planet  //其中planet被当做参数传入`

- 结果： `Hello planet!`

- 尽量少用for 和 while 循环

###### foreach遍历

- 打印每一个命令行参数的方式：args.foreach(arg => println(arg))
这段代码中，对args执行foreach方法，传入一个函数。本例中传入的是一个函数字面量(function literal)

- 这个(匿名)函数接受一个名为arg的参数(arg仅仅是参数名没有别的特殊含义)
上面也可以指明类型名(这样需要将参数的部分包在圆括号里，这是函数字面量的常规语法)：`args.foreach((arg:String) => println(arg))`

- scala函数字面量语法： `(x:Int, y: Int) => x + y`
其中从左到右，括号中的是参数部分，然后是右箭头，最右边是函数体

- scala对函数字面量还有一个特殊的简写规则：如果函数字面量只是一个接收单个参数的语句，可以不必给出参数名和参数本身。
因此上例可以写为：`args.foreach(println)`


- scala只支持指令式的for语句的函数式亲戚。*for表达式*
- for表达式一个简单的例子：
```
	for(arg <- args)
	    println(arg)
```

- 其中，位于 `<-` 符号右边的，是args数组，在 `<-` 左边的是一个 val变量的名字，为arg。
注意左边的这个变量一定是 val类型 的(即它不能在for表达式循环体里被重新赋值)，并且只能写为 `arg` 而不能写成 `val arg`

###### 用类型参数化数组

- 在scala中，可以用new来实例化对象或类的实例，当实例化对象时，可以用值和类型来对其进行参数化(parameterize)

- 参数化的意思是：在创建实例的时候对实例做"配置"，可以用值来参数化一个实例，做法是在构造方法的括号中传入对象参数。

- 参数化创建数组：
```
	val myArr = new Array[String](3)
	myArr(0) = ...
	myArr(1) = ...
	myArr(2) = ...
```

- 另一种创建方法： `val numArr = Array("zero","one","two")`

- 这实际上是调用了一个名为apply的工厂方法，这个方法创建并返回了新的数组。这个apply方法接受一个变长的参数列表。


- scala数组使用 **圆括号** 来访问元素而不是方括号，原因(原文)：
	>数组不过是类的实例，这一点跟其他scala的实例没有本质区别。当你用一组圆括号讲一个或多个值包起来，并将其应用(apply)到某个对象时，scala会将这段代码转换成对这个对象的一个名为apply的方法调用。因此myArray(i)实际上就是myArray.apply(i)。因此，在scala中访问一个数组的元素就是一个简单的方法调用。

- scala将从数组到表达式的一切都当做带有方法的对象来处理，由此来实现概念是的简单化。不需要记住各种特例。同时，这种统一并不会带来显著的性能开销。因为scala在编译代码时，会尽可能使用Java数组、基本类型和原生的算术指令。

###### 使用列表
- scala的列表(list)是不可变的(数组虽然不能更改长度，但是元素是可以改变的，因此是可变的)
因此list的修改有点像Java的字符串，每次对其中元素的修改都会返回一个新的list对象。

- 不需要写 `new List`，因为scala.List的伴生对象上定义了一个工厂方法`List.apply()`

- 列表上用的最多的操作是 `::`，读作"cons"。它是在一个已有的列表最前面添加一个新元素，并返回这个新的列表。
例：
```
	val twoThree = List(2,3)
	val oneTwoThree = 1 :: twoThree
	println(onTwoThree)
```
结果： `List(1,2,3)`

- 注意：在表达式`1::twoThree`中，`::`是它右操作元的方法。（一般用在操作符表示法的方法都是左结合的，例如 `a * b`相当于 `a.*(b)` ) 除非方法名是以 `:` 结尾的，那么这个方法的调用就会发生在他的右操作元上。 因此上例相当于： `twoThree.::(1)`，1是作为参数传入的。

- 表示空列表的快捷方式是`Nil`，初始化一个新的列表的另一种方式是用`::`将元素串接起来，并将Nil作为最后一个元素。例如：
```
val oneTwoThree = 1 :: 2 :: 3 :: Nil
println(oneTwoThree)
```

- `:::`连接两个List：
```
val a = List(1)
val b = List(2,3)
val c = a ::: b   //c: List(1,2,3)
```

- 列表也有从末尾增加元素的方法，但是应当尽力避免这种写法，因为末尾追加元素的操作所需时间随列表的大小线性增加，而使用`::`只需要常量级的时间。

- 可以通过在头部添加元素的方法，最后调用reverse方法来实现末尾添加的效果

- 也可以使用ListBuffer，这是个可变列表，支持追加操作，最后使用toList方法即可转换为List

###### 使用元祖

- 元祖也是不可变的，但是元祖可以容纳不同类型的元素。

- 当需要从方法返回多个对象时，元祖就非常有用

- 实例化一个元祖非常简单，只要将对象放在圆括号当中，用逗号隔开即可

- 一旦实例化好一个元祖，就可以用英文句点、下划线和 **从1开始** 的序号来访问每一个元素。

- 例如：
```
val pair = (99,"test")
pritln(pair._1)		//访问第一个元素
println(pair._2)	//访问第二个元素
```

- 元祖的实际类型取决于它的元素。例如：`(99,"test")`的类型为`Tuple2[Int,String]`,而元祖`('u','r',"the",1,4,"me")`的类型是`Tuple6[Char,Char,String,Int,Int,String]`

- 元祖为什么不能像数组一样用圆括号来访问元素(原文)：
> 你也许正好奇问什么不能像访问列表元素，也就是“pair(0)”那样访问元祖元素。背后的原因是列表的apply方法永远**只返回同一种类型**，但元祖里的元素可以是不同类型的：`_1`可能是一种类型，`_2`可能是另一种

###### 使用集和映射

- scala的API包含了一个基础的特质(trait)来表示集，这里的特质跟Java的接口定义类似

- scala提供了两个子特质：一个表示可变集，一个表示不可变集。(可变集与不可变集位于不同的包)

- 创建一个集合的例子：
```
var jetSet = Set("Boeing","Airbus")
jetSet += "Lear"
println(jetSet.contains("Cessna"))
```
- 第一行代码表示，可以像创建列表和数组那样创建集：通过调用Set伴生对象的apply工厂方法。

- 在这个例子中，实际上调用了scala.collection.immutable.Set的伴生对象的apply方法，返回一个默认的、**不可变** 的Set对象，类型为`Set[String]`

- 向集添加元素需要调用`+`方法。无论是可变集还是不可变集，`+`方法都会创建并返回一个新的集

- 而本例中的`+=`方法，实际上不可变集并不提供这个方法，其本质上是`jetSet = jetSet + ”Lear"`的简写。因此，**其本质上是将jetSet这个var重新赋值成了一个包含三个元素的新的集**

- 最后一行是打印集中是否包含"Cessna"这个元素，结果应当是`false`

###### 可变集

- 使用可变集需要一次引入，例：
```
import scala.collection.mutable
val movieSet = mutable.Set("Hitch","Peter")
movieSet += "Shrek"
println(movieSet)
```
- 通过import语句，可以使用简短的`mutable.Set()`而不是`scala.colection.mutable.Set()`这样完整的句子

- 这里的`+=`方法在可变集里是有定义的，因此这个可变集声明时用的是 `val`而不是 `var`(上面也提到了不可变集实际上是被重新赋值了，如果使用`val`会编译报错)

- `HashSet`的用法与`Set`一致，只是`HashSet`的存储方式不同，因此一般在需要考虑性能的地方会用到`HashSet`

###### 映射(Map)

- 与Set类似，Map也有可变与不可变的版本。

- 例子：
```
import scala.collection.mutable
val treasureMap = mutable.Map[Int,String]()
treasureMap += (1 -> "Go to island")
treasureMap += (2 -> "Find big X on ground")
treasureMap += (3 -> "Dig")
println(treasureMap(2))
```


<br>
> 最后更新于2018.7.12
