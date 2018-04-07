---
layout:     post
title:      "Java学习笔记"
subtitle:   "Keep foolish, Keep hungry"
date:       2018-04-6 16:47:00
author:     "Fleschier"
header-img: "img/Java/Java-bg.jpg"

---

>不适合人类阅读的学习笔记

## Java编译环境

---

编译环境首选JetBrian的[Intellij IDEA](https://www.jetbrains.com/idea/)，虽然几乎所有的教材都清一色的使用eclipse，但是jetBrian的社区版Intellij IDEA已经满足了我们的需求，其无与伦比的代码补全功能，清爽的界面会让人眼前一亮。专业版只有公司里才可能会用到其中的一些功能，所以我们也不用担心。

## 基本语法
---

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
#### Java注释

- Java注释与C++一致


## Java的类，继承与接口

---

