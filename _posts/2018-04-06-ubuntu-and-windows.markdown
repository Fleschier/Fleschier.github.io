---
layout:     post
title:      "双系统的那些坑"
subtitle:   "踩得坑多了，就更加会走路了..."
date:       2018-04-06
author:     "Fleschier"
header-img: "img/post-2018-04-06.jpg"

---
> 不适合人类阅读的学习笔记

##关于ubuntu 和 windows 双系统

---

- 在长时间使用Windows时候，难免会想要尝试新系统，而专业又是如此，于是我选择了linux中图形界面最为友好的ubuntu系统作为自己双系统的入门系统。

- 虽然网上的双系统教程多说的很是简单，但是大多数已经是几年前的文章了，其中所讲的一些计算机的硬件系统已经落伍了，就比如说，网上绝大多数的双系统引导模式是建立在bios支持legacy（传统模式）模式下的，然而我自己的bios只能在UEFI模式下引导系统启动.....作为一名计算机系的学生当然不服气啊，当然各种百度什么的，期间踩过的坑实在难为外人道也。

- 如果你的电脑支持legacy模式的话，自行百度一些教程就行了。装好ubuntu系统之后，进入bios将启动顺序整下，将Ubuntu启动器放在Windows boot manager前面就可以了。因为Ubuntu启动器可以调用Windows boot manager 而Windows不能启动Ubuntu。

- 如果你也像我一样，电脑不支持legacy启动，那么下面将要介绍一个非常好用的第三方启动引导程序。

##第三方启动引导程序——refind

- refind是一款功能非常强大的开机启动引导程序，它能够自定义开机界面。你可以吧系统图标，背景什么的换成你自己喜欢的风格。这里附上一张我自己的开机界面![](/img/linux-and-windows/opening-bg.jpg)

- 