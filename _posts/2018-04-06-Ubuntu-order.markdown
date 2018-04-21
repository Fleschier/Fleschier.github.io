---
layout:     post
title:      "Ubuntu终端常用命令"
subtitle:   "点滴成海"
date:       2018-04-6 16:47:00
author:     "Fleschier"
header-img: "img/Ubuntu/Ubuntu-bg.jpg"
tags: Ubuntu
---

>不适合人类阅读的备忘笔记

## 命令
---

###### 常用基本命令

- ls -l 的简略写法就是 ll，但是这个与ls -a又不同，后者用来显示隐藏文件和文件夹。

- ubuntu改文件名用 `mv name1 name2`即可

- `cp filename filepath` //拷贝文件

- `cp -r 源目录  指定目录` //拷贝一个文件夹到另一个目录

- 从hdfs上取文件到本地需要链接集群，然后 `hdfs dfs -get /.../filename  storepath`

- 查看路径：例如用`which python`查看python安装的路径

- `sudo apt-get remove + 软件名` 用于删除apt方式安装的软件

- `chmod [-可选参数][<权限范围>+/-/=<权限设置>] 文件/目录`  //改变文件权限

- `chown [-R] username filename/directoryname`  //更改文件或者文件夹所属用户

- `touch 文件名`命令用来创建一个空的文件

- 查看系统的所有PATH环境变量： `echo $PATH`

- `rm -rf` 强制 递归地删除某个文件或者文件夹的所有文件

- `dpkg -i filename.deb`  //安装 .deb 文件

###### grep语句

- Linux grep命令用于查找文件里符合条件的字符串。

- 简单命令格式： `grep [option] pattern file`
- 完整格式： `grep [-abcEFGhHilLnqrsvVwxy][-A<显示列数>][-B<显示列数>][-C<显示列数>][-d<进行动作>][-e<范本样式>][-f<范本文件>][--help][范本样式][文件或目录...]`

- **例（最常用）**：`cat AR_log | grep "===="
`此句就是打印日志AR_log当中所有包含了"===="的行

- 在当前目录中，查找后缀有 file 字样的文件中包含 test 字符串的文件，并打印出该字符串的行。此时，可以使用如下命令：
```
grep test *file
```

###### apt常用命令

- apt-cache search package 搜索包

- apt-cache show package 获取包的相关信息，如说明、大小、版本等

- sudo apt-get install package 安装包

- sudo apt-get install package - - reinstall 重新安装包

- sudo apt-get -f install 修复安装"-f = ——fix-missing"

- **sudo apt autoremove 卸载某个软件并且删除与之相关的多余依赖**

- sudo apt-get update 更新源

- **sudo apt-get upgrade 更新已安装的包**

- apt-cache depends package 了解使用依赖

- apt-cache rdepends package 是查看该包被哪些包依赖

- sudo apt-get build-dep package 安装相关的编译环境

- sudo apt-get clean && sudo apt-get autoclean 清理无用的包

- sudo apt-get check 检查是否有损坏的依赖

###### scp语句

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
- 参考资料：[linux命令大全-菜鸟教程](http://www.runoob.com/linux/linux-command-manual.html)以及各大博客网站大佬们的博文。


<br>

>最后更新于2018.4.21
