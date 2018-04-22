---
layout:     post
title:      "Python学习笔记——基础"
date:       2018-04-6 16:47:00
tags: Python
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

###### dick

> disk（字典）是一种键-值对类型的数据结构，在其他语言中会被称为map。dict的key必须为不可变的量

> 注意，Python中的dick类型是以hash方式存储的，读取速度非常快。

- 将数据添加进dick的方式，除了初始化时设定之外，还可以直接给一个键赋值的方式添加，例如：
```
d = {'A': 95, 'B': 75, 'C': 85} //初始化添加元素
d['E'] = 100   //直接赋值添加元素
```

- 判断一个key是否存在的方法：

1. `"Thomas" in d`		//若不存在会返回false
2. `d.get("Thomas")`  //若不存在返回null
3. `d.get("Thomas",-1)`  //自己指定返回的值

###### set

> set和dict类似，也是一组key的集合，但不存储value。由于key不能重复，所以，在set中，没有重复的key。

- 通过`.add(key)`的方法添加元素。

- 通过`.remove(key)`的方法删除元素。

- 符号 & 和 | 分别表示集合的交和并

- list的简单的去重：
```
>>> a = [1,2,2,3,4,5,5,6,1]
>>> b= set(a)
>>> b
>>>{1,2,3,4,5,6}
>>>a =list(b)
>>>a
>>>[1,2,3,4,5,6]
```

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
//但是如果此处的输入不是一个数值类型，int函数无法强制转化便会报错。
if birth < 2000:
    print('00前')
else:
    print('00后')
```

#### 循环

- 例（求和）：
```
for x in [1,2,3,4,5,6]:
	sum = sum + x
print(sum)
```
- `range()`函数： 生成从0 - **输入数值-1** 的一个迭代器，可用作循环条件。例`list(range(5))`的结果为 `[0,1,2,3,4]`


- 例求 1- 100 的和：
```
sum = 0
for x in range(101):
    sum = sum + x
print(sum)
```

## 函数
---

###### 函数定义的格式
```
def 函数名([参数1,参数2,参数3...]):   //参数没有参数类型，如果要设置参数的默认值则要满足从右向左的原则
	[函数体]
	[return [返回值]] 		//没有写return或者直接写return都是返回None
```

- Python中可以让函数返回一个有多个元素的tuple来实现返回多个值的要求。


<br>

>最后更新于2018.4.10
