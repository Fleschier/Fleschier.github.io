---
layout:     post
title:      "一些关于git 和 github 的随笔"
subtitle:   "点滴成海"
date:       2018-04-11 22:04:00
author:     "Fleschier"
header-img: "img/Git/Git-bg.jpg"

---
> 不适合人类阅读的随笔~

## 关于windows和Ubuntu下的可视化git管理工具
---

#### windows
- windows下有一个非常好用的git管理工具，与github有很好的连接——[github desktop](https://desktop.github.com/)。界面美观，方便好用。

- 同时要搭配Windows下的[git](https://git-scm.com/download/win)来使用。

- 登录你的github账号之后，便可以非常轻松地clone，add，commit，push等操作。

- 左上角点开选择clone到本地的repo，右键选择open in explorer 即可进入存放本地文件的位置。对文件进行过修改之后，按照下面的同步步骤即可。

- 推荐使用命令行来实现同步。左上角点开后选择要修改的repo，右键选择 open in command 即可进入命令行。

- 一些简单的命令操作：
```
git add .  //把本地的所有修改add
git commit -m "..."  //commit本地的修改，“...”中写本次修改的备注（这个备注必须有）
git push   //将本地的修改同步到github上
```
这样修改同步就完成了，一共只需要三步即可。

#### Ubuntu

- Ubuntu下找到一个甚至比Windows下的 github desktop更加好用的软件——[GitKraken](https://www.gitkraken.com/)

- 在上面不仅可以进行查看同步等操作，甚至可以看到之前在这个repo当中所有的人做出的任何修改，并且可以查看修改了哪些内容！*但是唯一美中不足的是有些更加NB的功能要开vip...*

- 比Windows更加便捷的是，这里想要进入对一个repo进行同步的命令行（终端）时，只需要在界面按下`Alt+T`的组合键就可以打开相应的终端了。

- 有个一直没能解决的问题：在添加完我的github账号之后，add和commmit操作在终端中都可以顺利的完成，但是在push的时候始终是访问被dennied掉，也不知道是什么原因。虽然在终端中没办法push，**但是直接点击界面上的push按钮却可以成功push...**。具体的原因等我找到了再更吧...