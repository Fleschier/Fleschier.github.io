---
layout:     post
title:      "C++学习笔记（不定期更新）"
subtitle:   "同样的错，不能犯第二次"
date:       2018-04-6 16:47:00
author:     "Fleschier"
header-img: "img/C++/C++-bg.jpg"

---

>不适合人类阅读的学习笔记

## 类
---

#### 模板类

- 示例：
```
template <class T> //声明一个模板，虚拟类型名为T。注意：这里没有分号。  
class T_Class //类模板名为Compare  
{  
public :  
   Compare(T a,T b){  
      x=a;y=b;  
   }  
   T max( ){  
      return (x>y)?x:y;  
   }  
   T min( ){  
      return (x<y)?x:y;  
   }  
private :  
   T x,y;  
};  
```

- 模板类所有的函数，如果在类外面实现的话，需要写成如下形式：
```
template <class T> 
T_Class<T>::max( ){  
     return (x > y)? x : y;  
}  
```

- **模板类不能将类的声明写在头文件而定义写在源文件中**，这样会出现无法辨析的编译错误。