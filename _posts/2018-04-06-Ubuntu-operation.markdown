---
layout:     post
title:      "Ubuntu随笔"
subtitle:   "点滴成海"
date:       2018-04-6 16:47:00
author:     "Fleschier"
header-img: "img/Ubuntu/Ubuntu-bg.jpg"

---

>不适合人类阅读的备忘笔记

## 一些推荐的软件
---
>  一旦出现某个软件没有安装，Linux系统大多数情况下都会提示你怎样安装这个软件，最常用的就是 sudo apt-get install XXX 命令

-  fish! fish! fish!： fish大法好啊，功能强大，自动补全，Ubuntu最好用的软件之一。

- vim和gedit：这个不用我多说大家都知道，Linux非常好用的编辑软件

- gnome 桌面： 装了gnome桌面和它的一系列插件之后我才真正感受到了Ubuntu的魅力！（教程以及主题百度很多）

- yakuake : 可以从上方一键滑出和滑入的终端（滑出时强制窗口在最前端）（gnome中也有类似功能的插件，两个选一个即可）

- Moeditor: Ubuntu下界面简洁美观，功能强大的markdown格式文件编辑器，已经在github上开源

- processon： 一个网页上的设计工具，可以很简单地完成诸如流程图的设计和生成图片文件。

## 一些注意点
---

- 触摸板双击之后再移动就相当于长按鼠标左键的效果了

- ls -l 的简略写法就是 ll，但是这个与ls -a又不同，后者用来显示隐藏文件和文件夹。

- 在Ubuntu终端窗口中，复制粘贴的快捷键需要加上 shift，即粘贴是 ctrl+shift+v。

- ssh cyx@192.168.1.201 cyx  高性能服务器  WIFI:sklcc_slave

- 192.168.1.201:18080
- 192.168.1.201:18088 进程
- 192.168.1.201:50070 hdfs

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

###### 关于桌面快捷方式的创建

- 方法一：进入 /usr/share/applications/ 目录，里面会有**绝大多数**你安装的软件的 .desktop文件，只需要把你需要的软件的 .desktop文件复制到home目录下的 桌面文件夹里即可。

- 方法二： 有点蠢但是很简单的一个方法。对于那些没有安装直接可以使用的软件，我们在上个方法中提到的文件夹里是找不到 .desktop文件的。怎么办呢？我们只需要进入我们那个软件的目录，找到启动文件，创建一个它的链接文件（右键还是终端随意），然后将这个链接文件复制到桌面，改下名字即可。虽然和简单，但是缺点是没有图标....身为一个外观党还是有点难以接受的...

- 方法三（未验证）：就是自己写一个.desktop文件，网上有很多教程，虽然我尝试过但是不知道为什么没能成功....所以等什么时候成功了再更吧.....

###### 关于shell脚本的创建

- 首先可以touch一个文件再进行内容的修改。或者直接`vim filename'新建一个文件并进行内容的编辑

- 所有shell脚本本质上都是文本文件，命名格式为`filename.sh`,内容必须以`#!/bin/bash`为第一行，当中没有空格。

- 事实上，这个#!字符序列是一种特殊的结构叫做 shebang。 这个 shebang 被用来告诉操作系统将执行此脚本所用的解释器的名字。每个 shell 脚本都应该把这一文本行作为它的第一行。

- 示例写法：
```
#!/bin/bash
#This is a test script!    #本句是一个注释，'#'号之后的字符都会被忽略
echo 'Hello World!'  #本句会在终端中打印 "Hello World!"
```

- 然后在终端中执行： `chmod +x filename.sh` 为这个脚本文件添加可执行权限

- 或者使用另外一个更改权限的写法：
```
[me@linuxbox ~]$ ll hello_world
-rw-r--r-- 1  me    me      63  2009-03-07 10:10 hello_world
[me@linuxbox ~]$ chmod 755 hello_world
[me@linuxbox ~]$ ll hello_world
-rwxr-xr-x 1  me    me      63  2009-03-07 10:10 hello_world
```
对于脚本文件，有两个常见的权限设置：权限为755的脚本，则每个人都能执行，权限为700的 脚本，只有文件所有者能够执行。注意为了能够执行脚本，脚本必须是可读的。

- 最后是运行脚本，终端进入脚本所在文件夹，输入： `./filename.sh` 

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

###### apt命令详解
- apt-cache search package 搜索包

- apt-cache show package 获取包的相关信息，如说明、大小、版本等

- sudo apt-get install package 安装包

- sudo apt-get install package - - reinstall 重新安装包

- sudo apt-get -f install 修复安装"-f = ——fix-missing"

- **sudo apt autoremove 卸载某个软件并且删除与之相关的多余依赖**

- sudo apt-get update 更新源

- sudo apt-get upgrade 更新已安装的包

- sudo apt-get dist-upgrade 升级系统

- sudo apt-get dselect-upgrade 使用 dselect 升级

- apt-cache depends package 了解使用依赖

- apt-cache rdepends package 是查看该包被哪些包依赖

- sudo apt-get build-dep package 安装相关的编译环境

- apt-get source package 下载该包的源代码

- sudo apt-get clean && sudo apt-get autoclean 清理无用的包

- sudo apt-get check 检查是否有损坏的依赖

#### Linux中添加环境变量的方法

> $PATH：决定了shell将到哪些目录中寻找命令或程序，PATH的值是一系列目录，当您运行一个程序时，Linux在这些目录下进行搜寻编译链接。

- 为什么要添加环境变量呢？如果你在Linux下载了一个免安装的软件，你要启动它的话，要么创建一个桌面快捷方式（方法见上文），要么就是每次进入它的目录点开。这时候如果我们把它添加进了PATH环境变量，那么我们只需要在终端中输入这个软件的名字，回车，就可以启动它了。

- 方法一：修改profile文件（**注意：一定要切换到root用户，一定要切换到root用户，一定要切换到root用户(sudo su)! ! ! !** 否则最后保存文件会一直被拒绝又退不出去只能强退终端...可能还会有其他一些麻烦事...总之有的爽呢...） //对所有用户永久生效

```  
(root模式下执行) vim /etc/profile 
在文档最后加入一行:
export PATH=$PATH: 软件的启动脚本文件所在的**绝对路径**"
(一般都是 /.../bin目录)
退出修改后在root模式下执行： source /etc/profile
或者重启
```

- spark-shell的路径写法例子：
```
export SPARK_HOME=/usr/lib/spark/spark-2.2.0-bin-hadoop2.7
export PATH=${SPARK_HOME}/bin:$PATH
```

> 使用source命令时要关闭fish，否则会报错

- 方法二：修改.bashrc文件（注意点同上）//仅对当前用户永久生效
```
(root模式下执行)vi /root/.bashrc
在文档最后加入一行：
export PATH=$PATH: 软件的启动脚本文件所在的**绝对路径**"
退出修改后在root模式下执行： source /root/.bashrc
```

- 这两种方法最后的source语句就是让系统重新读取文件使之生效，没有写最后一句source的话，会在下次启动系统后生效

#### 分布式文件系统(HDFS)
- **注意，分布式文件系统中没有切换到某个目录下的概念，因为其文件全是分散在各个节点上的**

- 分布式文件系统的文件路径完整格式为 hdfs://namenode|master:编号/root/...
- 例如：`hdfs://master:8020/dataset/evaluation/bots_10m_10.csv`
> 其实很多时候可以省略前面的`hdfs://master:8020:`

- `hdfs dfs -ls  /...`显示分布式文件系统中某个目录（实际并不存在，只是逻辑上的）下的文件

- `hdfs dfs -rm -r file|directory` 删除某个文件

<br>
- 参考资料：[linux命令大全-菜鸟教程](http://www.runoob.com/linux/linux-command-manual.html)以及各大博客网站大佬们的博文。

<br>

>最后更新于2018.4.15