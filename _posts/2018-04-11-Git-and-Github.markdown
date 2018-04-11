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
- windows下有一个非常好用的git管理工具，与github有很好的连接——[github destop](https://desktop.github.com/)。界面美观，方便好用。

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