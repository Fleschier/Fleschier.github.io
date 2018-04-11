---
layout:     post
title:      "Ubuntu常用操作命令及注意点"
subtitle:   "点滴成海"
date:       2018-04-6 16:47:00
author:     "Fleschier"
header-img: "img/Ubuntu/Ubuntu-bg.jpg"

---

>不适合人类阅读的备忘笔记

## 一些注意点
---

- 在Ubuntu终端窗口中，复制粘贴的快捷键需要加上 shift，即粘贴是 ctrl+shift+v。

- ssh cyx@192.168.1.201 cyx  高性能服务器  WIFI:sklcc_slave

- 192.168.1.201:18080
- 192.168.1.201:18088 进程
- 192.168.1.201:50070 hdfs

- ubuntu改文件名用 `mv name1 name2`即可

- `cp filename filepath` //拷贝文件

- 从hdfs上取文件到本地需要链接集群，然后 `hdfs dfs -get /.../filename  storepath`

- 查看路径：例如用`which python`查看python安装的路径

- `sudo apt-get remove + 软件名` 用于删除apt方式安装的软件

- `chmod [-可选参数][<权限范围>+/-/=<权限设置>] 文件/目录`  //改变文件权限

- `chown [-R] username filename/directoryname`  //更改文件或者文件夹所属用户

<br>

>最后更新于2018.4.11