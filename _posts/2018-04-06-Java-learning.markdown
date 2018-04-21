---
layout:     post
title:      "Java学习笔记——基础"
subtitle:   "Keep foolish, Keep hungry"
date:       2018-04-6 16:47:00
author:     "Fleschier"
header-img: "img/Java/Java-bg.jpg"
tags: Java
---

>不适合人类阅读的学习笔记

## Java编译环境

---

编译环境首选JetBrian的[Intellij IDEA](https://www.jetbrains.com/idea/)，虽然几乎所有的教材都清一色的使用eclipse，但是jetBrian的社区版Intellij IDEA已经满足了我们的需求，其无与伦比的代码补全功能，清爽的界面会让人眼前一亮。专业版只有公司里才可能会用到其中的一些功能，所以我们也不用担心。

## 基本语法
---

> java与C++一样，需要用分号来分割句子

#### 第一个JAVA程序：Helloworld

- 示例
```
public class HelloWorld {
    public static void main(String[] args) {
        System.out.println("Hello World"); // 打印 Hello World
    }
}
```

#### 编写Java程序时注意点：

- 大小写敏感：Java是大小写敏感的，这就意味着标识符Hello与hello是不同的。

- 类名：对于所有的类来说，类名的首字母应该大写。如果类名由若干单词组成，那么每个单词的首字母应该大写，例如 MyFirstJavaClass 。

- 方法名：所有的方法名都应该以小写字母开头。如果方法名含有若干单词，则后面的每个单词首字母大写。
源文件名：源文件名必须和类名相同。当保存文件的时候，你应该使用类名作为文件名保存（切记Java是大小写敏感的），文件名的后缀为.java。（如果文件名和类名不相同则会导致编译错误）。

- 主方法入口：所有的Java 程序由public static void main(String[] args)方法开始执行。

- java的通配符与C++一样，都是"*"

- **Java与C++不同的地方是：Java中的整数，浮点数不能与布尔值相互转换，当然也不能用0或非0的的整数代替true或者false。**

#### Java修饰符

- 像其他语言一样，Java可以使用修饰符来修饰类中方法和属性。主要有两类修饰符：

- 访问控制修饰符 : default, public , protected, private

- 非访问控制修饰符 : final, abstract, strictfp

#### Java枚举

- 枚举限制变量只能是预先设定好的值,使用枚举可以减少代码中的bug
```
class ENUM_class{
	enum Test{Small, Medium, Large}
   Test size;
}
public class ENUM_class_Test{
	public static void main(String[] args){
		ENUM_class tst = new ENUM_class();
		tst.size = ENUM_class.Test.Small;
	}
}
```
#### Java的三目运算符

- 格式：逻辑表达式 ? 值1 : 值2

- 执行过程：若逻辑值表达式为true，就取值1，否则取值2

- 例：
```
int x =1,y =2;
x<y ? System.out.println("x<y"):System.out.println("x>y");
```
- 注意，此三目运算符不是一个完整的式子，一般是用作赋值。

#### Java注释

- Java注释与C++一致


## Java的输入
>Java的输入比起C++和Python要麻烦很多

---

#### 方法一：

```
import java.io.*   //引入java.io包的类
...
...
InputStreamReader in = new InputStreamReader(System.in);
BufferedReader br = new BufferedReader(in);
System.out.print("Please enter a num:");
String s = br.readLine(); //从键盘读取一行字符到s中
float num;
num = Float.parseFloat(s); //将字符型转换成float型
System.out.println();
...
```
#### 方法二：
###### 通过Scannner类

```
import java.util.*
...
float score;
Scanner sn = new Scanner(System.in);
System.out.println("Please enter a num:");
score = sn.nextFloat();
System.out.println();
```
- *scan在读取多行数据时会遇到的问题：*
```
Scanner scan = new Scanner(System.in)
int num  = scan.nextInt();  //这句会正确执行
Double d = scan.nextDouble(); //这句也会正确执行，即使输入在不同的行上
String s = scan.nextline();  //这句这样写便会读到一个空串×××××××
```
原因分析：首先，Scanner是一个扫描器，它扫描数据都是去内存中一块缓冲区中进行扫描并读入数据的，而我们在控制台中输入的数据也都是被先存入缓冲区中等待扫描器的扫描读取。这个扫描器在扫描过程中判断停止的依据就是“空白符”，空格啊，回车啊什么的都算做是空白符。
nextInt()方法在扫描到空白符的时候会将前面的数据读取走，但会丢下空白符“\r”在缓冲区中，但是，nextLine()方法在扫描的时候会将扫描到的空白符一同清理掉。
了解了这两个方法特性和区别，就知道了上边的代码究竟是怎么回事，以及知道了解决的方法。像是上边的代码nextInt()方法之后在缓冲区中留下了“\r”，然后nextLine()方法再去缓冲区找数据的时候首先看到了“\r”，然后就把这个“\r”扫描接收进来，并在缓冲区内清除掉。其实，nextLine()方法是执行过的，并没有不执行。

- 解决方案：

1. 在调用nextline()之前先调用一次nextline()将那个换行符读取掉

2. 在读取Int的时候就调用nextline()方法，再用parseInt()转化为Int



#### 图形界面输入方式

```
import javax.swing.* //导入javax,swing包中的类
...
String str;
float score;
str = JOptionPane.showInputDialog("please enter a num:");
score = Float.parseFloat(str);
...
```

## 输出
---
- 标准输出：`System.out.println();`

- 格式化输出：`System.out.printf();` //格式化输出允许对输出进行规改
```
//"%"表示进行格式化输出，"%"之后的内容为格式的定义。
System.out.printf("%f",d);//"f"表示格式化输出浮点数。
System.out.printf("%9.2f",d);//"9.2"中的9表示输出的长度，2表示小数点后的位数。
System.out.printf("%+9.2f",d);//"+"表示输出的数带正负号。
System.out.printf("%-9.4f",d);//"-"表示输出的数左对齐（默认为右对齐）。
System.out.printf("%+-9.3f",d);//"+-"表示输出的数带正负号且左对齐。
System.out.printf("%d",i);//"d"表示输出十进制整数。
System.out.printf("%o",i);//"o"表示输出八进制整数。
System.out.printf("%x",i);//"d"表示输出十六进制整数。
System.out.printf("%#x",i);//"d"表示输出带有十六进制标志的整数。
System.out.printf("%s",s);//"d"表示输出字符串。
System.out.printf("输出一个浮点数：%f，一个整数：%d，一个字符串：%s",d,i,s);
//可以输出多个变量，注意顺序。
System.out.printf("字符串：%2$s，%1$d的十六进制数：%1$#x",i,s);
//"X$"表示第几个变量。
```

###### 图形界面输出

```
JOptionPane.showMessageDialog(....)  //具体参数见类库
```

## 一些注意点
---
#### 数组

- 数组的声明格式： 数据类型[] 数组名 或者 数据类型 数组名[]

- Java的数组声明只是指明了一个对象引用，并没有为数组元素分配内存空间。**因此声明不能指定数组元素个数**。例如：`int a[10];`是错误的。**如果要声明并创建数组应该采用如下格式 ： 数据类型 数组名[] = new 数据类型[数组长度]**。

- 数组的初始化与C++相同。例：`int a[] = {1,6,8};`  这句相当于`int a = new int[3]; a[0]=1,a[1]=6,a[2]=8;`

- 只进行了声明的数组，它的元素是不能被访问的，只有经过初始化后，才能访问数组的元素。

- 数组的长度的获取：`a.length` 就表示数组a的长度（即a的元素个数）**注意这里的.length是数组的属性（相当于类的尘成员变量）而不是方法，所以a.length()的写法是错误的，他把length当做一个类的方法来调用了**

#### 随机数

###### Math.random()
- `int num =(int)(Math.random() * 11);`  生成一个范围在[0,1)的随机数。

###### java.util.Random

- 例：
```
import Java.util.Random;
Random rand = new Random([数值]);
int randomNum = rand.nextInt() //Random支持的随机值类型包括：boolean, byte, int, long, float, double
int randomNUM2 = rand.nextInt(100); //表示获取[0,100)范围的随机数
...
```

#### String类

- String是常量，对一个String的任何修改都会使java创建一个新的String，而原来的会被当做垃圾回收掉
- 例如：
```
String a = "avc";
a = "bfd";    //则会创建一个新的string，然后将a链向这个string，原先的string会被抛弃掉
```


<br>

>最后更新于2018.4.9
