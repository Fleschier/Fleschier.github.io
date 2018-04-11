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

###### grep语句
- 语法： `scp [可选参数] file_source file_target `

- 例：`scp /home/fleshier/My_Programes/Programes/AssociationRuleDiscovery/target/AR.jar   root@192.168.1.201:/root`
此句就是吧一个本地的文件拷贝到远端的服务器上，用户是root，服务器地址是192.168.1.201，存放目录是 /root

- 如果指定了用户名（如上例），则需要输入密码，如果没有指定用户名，则回车后需要输入用户名和密码。

- 额外说明：如果远程服务器防火墙有为scp命令设置了指定的端口，我们需要使用 -P 参数来设置命令的端口号，命令格式如下：
```
#scp 命令使用端口号 4588
scp -P 4588 remote@www.runoob.com:/usr/local/sin.sh /home/administrator
```

<br>
- 参考资料：[linux命令大全-菜鸟教程](http://www.runoob.com/linux/linux-command-manual.html)

<br>

>最后更新于2018.4.11