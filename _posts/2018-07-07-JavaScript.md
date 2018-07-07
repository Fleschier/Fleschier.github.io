---
layout:     post
title:      "前端学习——JavaScript"
date:       2018-07-07 11:26:00
tags:   ๑FrontEnd ๑JavaScrpt
---

> 不适合人类阅读的学习笔记


## 基础
---

###### 嵌入html的javascript写法

- JavaScript代码写在`<script>`和`</script>`标签之前。
![](/images/JavaScript/001.png)
- 其中`<script type ="text/javascript">`表示在`<script></script>`之间的是文本类型`(text)`,javascript是为了告诉浏览器里面的文本是属于JavaScript语言。

###### 单独写成文件

- JavaScript代码只能写在HTML文件中吗?当然不是，我们可以把HTML文件和JS代码分开,并单独创建一个JavaScript文件(简称JS文件),其文件后缀通常为.js，然后将JS代码直接写在JS文件中。

- **注意:在JS文件中，不需要`<script>`标签,直接编写JavaScript代码就可以了。**

- 单独写成文件的javascript文件不能单独运行，比如一个叫“script.js”的文件，我们需在HTML中添加如下代码，就可将JS文件嵌入HTML文件中：`<script src="script.js"></script>`

#### 位置

- 我们可以将JavaScript代码放在html文件中任何位置，但是我们一般放在网页的head或者body部分。

###### 放在`<head>`部分

- 最常用的方式是在页面中head部分放置`<script>`元素，浏览器解析head部分就会执行这个代码，然后才解析页面的其余部分。

###### 放在`<body>`部分

- JavaScript代码在网页读取到该语句的时候就会执行。

- **注意: javascript作为一种脚本语言可以放在html页面中任何位置，但是浏览器解释html时是按先后顺序的，所以前面的script就先被执行。比如进行页面显示初始化的js必须放在head里面，因为初始化都要求提前进行（如给页面body设置css等）；而如果是通过事件调用执行的function那么对位置没什么要求的。**

## 语法
---

- 一个JavaScript语句以`;`结尾（虽然也可以不写）

- 注释：单行注释：`//`，多行注释`/*...*/`

###### 变量

- 定义变量使用关键字`var 变量名`

- 注意JS中变量无需声明类型

###### 判断语句

- 语法：

```
if(条件)
{ 条件成立时执行的代码 }
else
{ 条件不成立时执行的代码 }
```

- 例子：

```
<script type="text/javascript">
   var myage = 18;
   if(myage>=18)  //myage>=18是判断条件
   { document.write("你是成年人。");}
   else  //否则年龄小于18
   { document.write("未满18岁，你不是成年人。");}
</script>
```

###### 判断函数

- 语法：

```
function 函数名()
{
     函数代码;
}
```

- 例子：
![](/images/JavaScript/002.png)

#### 输出内容(document.write)

- 输出内容可以是双引号括起来的，也可以是变量，多个输出项之间以`+`连接

- 


<br>
> 最后更新于2018.7.7
