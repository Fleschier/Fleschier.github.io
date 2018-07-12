---
layout:     post
title:      "前端学习——JavaScript"
date:       2018-07-07 11:26:00
tags:   ๑FrontEnd ๑JavaScrpt
---

> 不适合人类阅读的学习笔记


## 基础
---

>建议把javascript脚本放在 `<body> `部分的底部。
>这会提高网页加载速度，因为 HTML 加载不受制于脚本加载。

- [Js是放在head还是body解析](https://blog.csdn.net/w405722907/article/details/78517757)

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

- 例子：
```
<script type="text/javascript">
  var mystr="hello";
  document.write(mystr+"I love JavaScript"); //多项内容之间用+号连接
</script>
```

###### javascript警告(消息对话框)

- 语法：`alert(字符串或变量)`

> 注意：alert弹出一个消息对话框，只有一个确定按钮，多个对话框之间按顺序弹出。

###### 确认(confirm对话框)

- 语法：`confirm(str);`

- 参数说明：
1. str：在消息对话框中要显示的文本
2. 返回值: Boolean值

- 返回值：
当用户点击"确定"按钮时，返回true ；当用户点击"取消"按钮时，返回false

###### 打开新窗口(window.open)

- 语法：`window.open([URL], [窗口名称], [参数字符串])`

- 参数说明：
```
URL：可选参数，在窗口中要显示网页的网址或路径。如果省略这个参数，或者它的值是空字符串，那么窗口就不显示任何文档。
窗口名称：可选参数，被打开窗口的名称。
    1.该名称由字母、数字和下划线字符组成。
    2."_top"、"_blank"、"_self"具有特殊意义的名称。
       _blank：在新窗口显示目标网页
       _self：在当前窗口显示目标网页
       _top：框架网页中在上部窗口中显示目标网页
    3.相同 name 的窗口只能创建一个，要想创建多个窗口则 name 不能相同。
   4.name 不能包含有空格。
参数字符串：可选参数，设置窗口参数，各参数用逗号隔开。
```
![](/images/JavaScript/003.png)

> 注意：所有的参数都要写在一个参数字符串中，中间以逗号间隔，例如 'height=100.width=100' 这样。

- 可以将窗口对象存储在变量test中：`var test = window.open(...);`

- 关闭窗口：

1. `window.close();`:关闭本窗口

2. `<窗口对象>.close();`:关闭指定窗口

## 控制权(DOM操作)
---

- 文档对象模型DOM（Document Object Model）定义访问和处理HTML文档的标准方法。DOM 将HTML文档呈现为带有元素、属性和文本的树结构（节点树）。

- 将HTML代码分解为DOM节点层次图:
![](/images/JavaScript/004.png)

###### HTML文档可以说由节点构成的集合，三种常见的DOM节点:

- 元素节点：上图中`<html>`、`<body>`、`<p>`等都是元素节点，即标签。

- 文本节点:向用户展示的内容，如`<li>...</li>`中的JavaScript、DOM、CSS等文本。

- 属性节点:元素属性，如`<a>`标签的链接属性`href="http://www.imooc.com"`。

- 例子：`<a href="http://www.imooc.com">JavaScript DOM</a>`
![](/images/JavaScript/005.png)

#### 通过ID获取元素

- 网页由标签将信息组织起来，而标签的id属性值是唯一的，就像是每人有一个身份证号一样，只要通过身份证号就可以找到相对应的人。那么在网页中，我们通过id先找到标签，然后进行操作。

- 语法：`document.getElementById(“id”) `

- 例子：
```
<!DOCTYPE HTML>
<html>
<head>
<meta http-wquiv="Content-Type" content="text/html; charest=gb2312" />
<title>获取元素</title>
  <script type="text/javascript">
    var mye = document.getElementById("con");    //获取元素变量存储在变量mye中
    document.write(mye);                    //输出变量
  </script>
</head>
<body>
    <h3>Hello</h3>
    <p id="con">I love JavaScript</p>
</body>
</html>
```
#### innerHTML属性

- innerHTML 属性用于获取或替换 HTML 元素的内容。

- 语法：`Object.innerHTML`

- 例子：
```
<!DOCTYPE HTML>
<html>
<head>
<title>innerHTML</title>
</head>
<body>
  <p id="con">Hello World!</p>
  <script>
    var mycon = document.getElementById("con");
    document.write("P标签原始内容：" + mycon.innerHTML + “<br>”);
    //输入想要修改的元素内容
    mycon.innerHTML = "New test!";          //修改P元素内容
    document.write("P标签修改后的内容：" + mycon.innerHTML);
  </script>
</body>
</html>
```

#### 改变HTML样式

- HTML DOM 允许 JavaScript 改变 HTML 元素的样式。

- 语法：`Object.style.property=new style;`

- 注意:Object是获取的元素对象，如通过`document.getElementById("id")`获取的元素。

- 基本属性表：

| 属性 | 描述 |
|---|---|
|backgroundColor|设置元素背景颜色 |
|height|设置元素高度|
|width|设置元素宽度|
|color|设置文本颜色|
|font|在一行设置所有的字体属性|
|fontFamily|设置元素的字体系列|
|fontSize|设置元素的字体大小|
|...|...|

- CSS的其他的一些样式也可以通过该方法修改

- 例子：改变`<p>`元素的样式，将颜色改为红色，字号改为20,背景颜色改为蓝：
```
<p id="pcon">Hello World!</p>
<script>
   var mychar = document.getElementById("pcon");
   mychar.style.color="red";
   mychar.style.fontSize="20";
   mychar.style.backgroundColor ="blue";
</script>
```

#### 显示和隐藏

- 网页中经常会看到显示和隐藏的效果，可通过display属性来设置。

- 语法：`Object.style.display = value`

> 注意这里的Object也是元素对象，可通过document.getElementById("id")来获取

- value取值：

1. none：此元素讲不会被显示(即隐藏)
2. block：此元素将显示为块级元素

例子：
![](/images/JavaScript/006.png)

#### 控制类名

- className 属性设置或返回元素的class 属性。

- 语法：`object.className = classname`

- 作用：
1. 获取元素的class属性
2. 为网页内某个元素指定一个CSS样式来更改该元素的外观

- 例子：
```
<!DOCTYPE HTML>
<html>
<head>
<meta http-equiv="Content-Type" content="text/html;charset=gb2312">
<title>className属性</title>
<style type="text/css">
  input{
    font-size:10px;
  }
  .one{
    width:200px;
    background-color:#CCC; //灰色
  }
  .two{
    font-size:18px;
    color:#F00
  }
</style>
</head>
<body>
  <p id="con" class="one">JavaScript</p>
  <form>
    <input type="button" value="点击更改" onclick="modifyclass()"/>
  </form>
  <script type="text/javascript">
    var mychar=document.getElementById("con");
    document.write("p元素的Class值为：" + mychar.className + "<br>"); //输出P元素的class属性
    function modifyclass(){
      mychar.className="two"; //改变className,即更换用来修饰的class
    }
    </script>
</body>
</html>
```
- 结果：

![](/images/JavaScript/007.png)

## 进阶
---

- 循环、分支、判断等语法与C++一致

#### 事件响应

- JavaScript 创建动态页面。事件是可以被 JavaScript 侦测到的行为。 网页中的每个元素都可以产生某些可以触发 JavaScript 函数或程序的事件。

|事件|说明|
|---|---|
|onclick|鼠标单击事件|
|onmouseover|鼠标经过事件|
|onmouseout|鼠标移开事件|
|onchange|文本框内容改变事件|
|onselect|文本框内容被选中事件|
|onfocus|光标聚集|
|onblur|光标移开|
|onload|网页导入|
|onunload|关闭网页|

###### 鼠标单击事件

- onclick是鼠标单击事件，当在网页上单击鼠标时，就会发生该事件。同时onclick事件调用的程序块就会被执行，通常与按钮一起使用。

- 例如：单击按钮时出发onclick事件，调用add2()函数
```
<form>
     <input name="button" type="button" value="点击提交" onclick="add2()" />  //注意最后的斜杠
  </form>
```

###### 鼠标经过事件

- 与鼠标单击事件调用方法一致

###### 其他的事件

- 除了onload与onunload的使用有一点区别，别的都一致。

#### 对象

- JavaScript 中的所有事物都是对象，如:字符串、数值、数组、函数等，每个对象带有属性和方法。

- 创建对象使用`new`关键字

###### 日期对象

- 日期对象可以储存任意一个日期，并且可以精确到毫秒数（1/1000 秒）

- 定义一个时间对象：`var Udate = new Date();`
> 这是默认定义，初始值为当前电脑时间

- 如果要自定义值，使用以下方法：`var DATE = new Date(2018,10,4); //2018年10月4日`

#### 浏览器对象

###### window对象

- window对象是BOM的核心，window对象指当前的浏览器窗口。

- window对象方法：

|方法|描述|
|---|---|
|alert()|显示带有一段消息和一个确认按钮的警告框|
|prompt()|显示可提示用户输入的对话框|
|confirm()|显示带有一段消息以及确认按钮和取消按钮的对话框|
|open()|打开一个新的浏览器窗口或者查找一个已经命名的窗口|
|close()|关闭浏览器窗口|
|print()|打印当前窗口的内容|
|focus()|把键盘焦点给予一个窗口|
|blur()|把键盘焦点从顶层窗口移开|
|moveBy()|可相对窗口的当前坐标把它移动指定的像素|
|moveTo()|把窗口的左上角移动到一个指定的坐标|
|resizeBy()|按照|
|resizeTo()|把窗口的大小调整到指定的宽度和高度|
|scrollBy()|按照指定的像素值来滚动内容|
|scrollTo()|把内容滚动到指定的坐标|
|setInterval()|每隔指定的时间执行代码|
|setTimeout()|在指定的延迟时间后来执行代码|
|clearInterval()|取消setInterval()的设置|
|clearTimeout()|取消setTimeout()的设置|

- 调用这些方法格式：`window.方法名(参数名);`

例子：
```
function myFunction()
{
    alert("欢迎")
    window.open('http://www.imooc.com','_blank','width=600 height=400')
    //第一个参数表示要打开的网页，'_blank'参数表示打开一个新网页，后面的参数设置新窗口的初始大小
}
```

###### JavaScript计时器

- 在JavaScript中，我们可以在设定的时间间隔之后来执行代码，而不是在函数被调用后立即执行。

- 计时器类型：

  1. 一次性计时器：仅在指定的延迟时间之后触发一次。(setTimeout())

  2. 间隔性触发计时器：每隔一定的时间间隔就触发一次。(setInterval())

- setInterval()方法格式：`setInterval(代码，交互时间)`
>参数中，代码就是要执行的函数挥着代码串，交互时间就是执行的时间间隔，以毫秒为单位

- setInterval的返回值可以传递给clearInterval从而取消对代码的周期性执行。

- 假设有一个clock()函数，则调用格式为：
```
setInterval("clock()",1000)
或者
setInterval(clock,1000)
```

## DOM对象
---

#### getElementsByName方法

- 返回带有指定名称的节点对象的集合

- 语法：`document.getElementsByName(name)`
>其中name参数是标签上设置的name属性，和设置id属性格式一样，但是不同的标签可以设置同一个name属性，而id属性必须唯一

- 与getElementById()不同的是，通过元素的name属性查询元素而不是通过id属性

- 注意：因为文档中的name属性可能不唯一，所有的getElementByName()方法的返回值是元素的数组，而不是一个元素

- 和数组类似的也有length属性，可以和访问数组一样的方法来访问，从0开始








<br>
> 最后更新于2018.7.8
