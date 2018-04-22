---
layout:     post
title:      "Java学习笔记——类与继承"
subtitle:   "Keep foolish, Keep hungry"
date:       2018-04-18 16:47:00
author:     "Fleschier"
header-img: "img/Java/Java-bg.jpg"
tags: Java
---

>不适合人类阅读的学习笔记

## Java的类，继承与接口
---

#### 类的定义

- 类的修饰符有两种：public 和 缺省。public表示共有的访问级别，即任何类都可以访问它。缺省只允许同一个包中的类来访问它。

- 类的类型修饰符：缺省、abstract及final三种。abstract表示这是一个抽象类，**有些方法**还没有实现。final表示这是一个最终类，不能被其他的类继承。

- *类是对象的模板，对象是类的实例化*

###### 一个类可以包含以下类型变量：

- 局部变量：在方法、构造方法或者语句块中定义的变量被称为局部变量。变量声明和初始化都是在方法中，方法结束后，变量就会自动销毁。

- 成员变量：成员变量是定义在类中，方法体之外的变量。这种变量在创建对象的时候实例化。成员变量可以被类中方法、构造方法和特定类的语句块访问。

- **类变量**：类变量也声明在类中，方法体之外，但必须声明为static类型。（**同C++中的静态变量**）

- 最终变量：即**常量**，用final关键字修饰。一般与static关键字连用，例如定义PI、E等。

###### 源文件声明规则

- 一个源文件中只能有一个public类

- 一个源文件可以有多个非public类

- 源文件的名称应该和public类的类名保持一致。例如：源文件中public类的类名是Employee，那么源文件应该命名为Employee.java。

- 如果一个类定义在某个包中，那么package语句应该在源文件的首行。

- 如果源文件包含import语句，那么应该放在package语句和类定义之间。如果没有package语句，那么import语句应该在源文件中最前面。
import语句和package语句对源文件中定义的所有类都有效。在同一源文件中，不能给不同的类不同的包声明。

- 类有若干种访问级别，并且类也分不同的类型：抽象类和final类等。这些将在访问控制章节介绍。

- 除了上面提到的几种类型，Java还有一些特殊的类，如：内部类、匿名类。

#### 对象

###### 对象的引用
- 创建对象后，可以将对象的引用赋值给其他对象变量。

- 例如下面的程序
```
public class test{
	public static void main(String[] args){
		StringBuffer s;
		s= new StringBuffer("AAAAA");
		StringBuffer s1 = s; //此句会使得s1和s指向同一个对象
		s1.append("BBBB");
		Syetem.out.println("s = " + s.toString());
		Syetem.out.println("s1 = " + s1.toString());
	}
}
```
- 输出结果为：
```
s = AAAAABBBB
s1 = AAAAABBBB
```

#### 方法参数传递

###### 按值传递(一般的函数参数)

- 传入方法中的参数是一份拷贝，对其的修改不会影响其本身

```
class Printer{
	public void printinfo(String name, int age){
		age ++;
		System.out.println("Hello! My name is" + name + "and I'm " + age);
	}
	public static void main(String args[]){
		Printer p = new Printer();
		int age = 20;
		p.printinfo("Mike",age);
		System.out.println("Now the initial age = " + age);
	}
}
```

###### 按引用传递

- 调用方法时，**如果传递的是一个对象、接口或数组时**，实际上传递的是对象的、接口或者数组的引用。因此如果方法中对参数进行了修改，那么原来的数据也会受到影响。

#### 继承

- 类的继承格式：
```
class 父类{
	...
}
class 子类 extends 父类{
	...
}
```

###### 继承的特性：

- 子类拥有父类非private的属性，方法。

- 子类可以拥有自己的属性和方法，即子类可以对父类进行扩展。

- 子类可以用自己的方式实现父类的方法。

- Java的继承是单继承，但是可以多重继承，java的多继承通过接口来实现。

- **关键字super和this在java的类中分别可以指代父类和类本身。**



## 多继承的实现
---

#### 抽象类

- 抽象类的定义：
```
[访问修饰符] <abstract> class <类名>{
	[成员变量声明]
	[方法定义]
}
```
- 抽象方法的定义：抽象方法是指只有声明而没有实现方法，用abstract修饰，一般格式如下：
```
[访问修饰符] <abstract> 返回类型 方法名(参数列表);
```
>注意抽象类不能定义为final类，因为抽象类不能实例化。抽象方法也不能声明为final方法，因为要在子类中实现该抽象方法。

- **抽象类不能被实例化，实例化的工作应该交由它的子类来完成**，它只需要有一个引用即可。

- 抽象方法必须由子类来进行重写。

- **只要包含了抽象方法的类，该类必须要定义成抽象类，不管是否还包含有其他已经实现了的方法**。

- 抽象类中可以包含具体的方法，**当然也可以不包含抽象方法**。

- 子类中的抽象方法不能与父类的抽象方法同名。

- abstract 不能与private、static、final或native并列修饰同一个方法。

#### 接口
- 接口用interface来定义

- **抽象类是对类抽象，而接口是对行为的抽象**。

- 接口中可以定义“成员变量”，或者说是不可变的常量，因为接口中的“成员变量”会自动变为为public static final。可以通过类命名直接访问：ImplementClass.name

- 接口实质也是一个抽象类，但与抽象类不同的是**接口中只能包含常量的定义和方法的声明**。接口只关心功能，而不关心功能的具体实现。

- **接口中的常量在声明时必须对它赋初始值**。

- 一般的继承使用extends作为关键字，只能单继承。接口使用implements作为关键字。可以接受多继承。

- 接口是抽象类的延伸，java了保证数据安全是不能多重继承的，也就是说继承只能存在一个父类，但是接口不同，一个类可以同时实现多个接口，不管这些接口之间有没有关系，所以接口弥补了抽象类不能多重继承的缺陷。

- 接口是用来建立类与类之间的协议，它所提供的只是一种形式，而没有具体的实现。同时实现该接口的实现类必须要实现该接口的所有方法，通过使用implements关键字，他表示该类在遵循某个或某组特定的接口。

- 接口的使用格式：
 `[访问修饰符][类型修饰符] class 类名 implements 接口名1,接口名2,......`

- 一个类如果继承了某个接口，那么它就要实现这个接口的所有方法，否则这个类要定义为抽象类。
>需要注意的是，接口中的方法默认是public，所以在类中实现接口时，必须使用public来修饰方法。如果接口中某个方法返回为void，则在类中实现该方法时，方法体可以为空，即只有两个大括号。

- 接口使用示例：
```
interface Computable{
	final int x = 10;
	int add();
	void point();
}
class TESt implements Computable{
	private int y;
	public TEST(int y){
		this.y = y;
	}
	public int add(){ //实现抽象方法时添加public 和 return 语句
		return x + y;
	}
	public void print(){} //返回类型为void方法体可以留空
}
```

- 接口之间也可以继承，用关键字extends，但是一个接口可以同时extends多个接口，之间以逗号间隔。
>如果一个接口继承了别的几个接口，那么实现这个接口的类同时也要实现被这个接口继承的几个接口的所有方法。

## Java API 实用类
---

#### String类

#### StringBuffer类 和 StringBuilder类

#### Math类

<br>
> 最后更新于2018.4.21
