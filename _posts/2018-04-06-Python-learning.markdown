---
layout:     post
title:      "Python学习笔记"
subtitle:   "Keep foolish, Keep hungry"
date:       2018-04-6 16:47:00
author:     "Fleschier"
header-img: "img/Python/Python-bg.jpg"

---

>不适合人类阅读的学习笔记

- **Python语句不需要分号分割，但是Python各语句严格按照缩进对其方式运行**

- 与C++一样，可以将一些非空，非零的值作为bool值的真，其余的为假

## 环境
---

- Python推荐使用jetbrain公司的pycharm

- Python可以直接使用自带的IDE逐句执行，方便测试


## 基础
---

- Python中不需要声明变量类型，编译器会根据赋值自动判别，但是作为程序的编写者，我们需要清楚某个变量究竟是什么类型的

###### 输出

- `print("Hellowrold! \n","This is my first Python program!")`

- 各个输出之间以逗号间隔

###### 输入

```
num = input(“please enter a num: ”)  //Python的输入提示可以直接写在input函数中，非常方便
```

#### 一些数据类型

###### List

> Python中list里的元素允许是不同的数据类型，虽然平常编写程序不推荐这样做。list中也允许某个元素是list或者元组什么的。

- 例： `classmates = ["Mike","Davaid"]`

- `len()`函数可以获得list中的元素个数

- 与其他编程语言不同的是，Python的list下标允许负数的index，例如： `classmates[-1]`就表示这个list的最后一个元素，以此类推。

- 在list末尾末尾添加元素：`classmates.append("Alex")`

- 把元素插入到指定的位置，比如索引号为1的位置：`classmates.insert(1, 'Jack')` 这样Jack的位置索引即为1，原来索引为1的元素及后面的元素依次后移。

- 删除list末尾的元素，使用`.pop()`方法，要删除指定位置的元素，使用`.pop(i)`的方法，i为元素的索引。

###### tuple

- 元组与；list非常类似，但是tuple一经初始化其内容便不允许修改，不允许插入和删除等操作。

- 元组一般用来保存那些不允许修改的数据以保障安全。

- 但是如果tuple中某个元素是list时，这个list中的元素还是可以修改的。

#### 条件判断

- 格式：
```
if <条件判断1>:
    <执行1>
elif <条件判断2>:
    <执行2>
elif <条件判断3>:
    <执行3>
else:
    <执行4>
```
- 例： 
```
age = 20
if age >= 6:
    print('teenager')
elif age >= 18:
    print('adult')
else:
    print('kid')
```

- 与input结合（涉及数据类型转换）：
```
s = input('birth: ')
birth = int(s) 		//如果没有这句转换会报错，因为input进来的是str，不能直接和int比较，因此要先转换为int再比较。
if birth < 2000:
    print('00前')
else:
    print('00后')
```

## 爬虫

<br>

>最后更新于2018.4.10