---
layout:     post
title:      "Ubuntu随笔"
date:       2018-04-6 16:47:00
tags: ๑Ubuntu
---

> 不适合人类阅读的备忘笔记

## Ubuntu目录结构

- `/`:这就是根目录，一台电脑有且只有一个根目录，所有的文件都是从这里开始的。举个例子：当你在终端里输入“/home”，你其实是在告诉电脑，先从/（根目录）开始，再进入到home目录。

- `/root`:系统管理员（root user）的目录。至于系统管理员的权限有多大我这里就不在废话了。因此，请小心使用root帐号。

- `/boot`: 系统启动文件，所有与系统启动有关的文件都保存在这里 。

- `/bin`: 这里是存放系统的程序。

- `/etc`:主要存放了系统配置方面的文件。

- `/dev`:这里主要存放与设备（包括外设）有关的文件（unix和linux系统均把设备当成文件）。想连线打印机吗？系统就是从这个目录开始工作的。另外还有一些包括磁盘驱动、USB驱动等都放在这个目录。

- `/home`:这里主要存放你的个人数据。具体每个用户的设置文件，用户的桌面文件夹，还有用户的数据都放在这里。每个用户都有自己的用户目录，位置为：/home/用户名。当然，root用户除外。

- `/tmp`:这是临时目录。对于某些程序来说，有些文件被用了一次两次之后，就不会再被用到，像这样的文件就放在这里。因此，千万不要把重要的数据放在这里哦。

- `/usr`:在这个目录下，你可以找到那些不适合放在/bin或/etc目录下的额外的工具。比如像游戏阿，一些打印工具等等。/usr目录包含了许多子目录： /usr/bin目录用于存放程序；/usr/share用于存放一些共享的数据，比如音乐文件或者图标等等；/usr/lib目录用于存放那些不能直接 运行的，但却是许多程序运行所必需的一些函数库文件。你的软件包管理器会自动帮你管理好/usr目录的。

- `/opt`:这里主要存放一些可选的程序。如你想尝试最新的firefox测试版吗？那就装到/opt目录下吧，这样，当你尝试完，想删掉firefox的时候，你就 可以直接删除它，而不影响系统其他任何设置。安装到/opt目录下的程序，它所有的数据、库文件等等都是放在同个目录下面。

- `usr/local`:这里主要存放那些手动安装的软件，即不是通过“新立得”或apt-get安装的软件。它和/usr目录具有相类似的目录结构。让软件包管理器来管理/usr目录，而把自定义的脚本（scripts）放到/usr/local目录下面。

- `/media`:这个目录是用来挂载那些usb接口的移动硬盘（包括U盘）、CD/DVD驱动器等等。

## 一些推荐的软件
---
>  一旦出现某个软件没有安装，Linux系统大多数情况下都会提示你怎样安装这个软件，最常用的就是 sudo apt-get install XXX 命令

-  fish! fish! fish!： fish大法好啊，功能强大，自动补全，Ubuntu最好用的软件之一。

- vim和gedit：这个不用我多说大家都知道，Linux非常好用的编辑软件

- [atom](https://atom.io/)  //集成许多功能于一体的编辑器

- [SpaceVim](https://zhuanlan.zhihu.com/p/24802058)模块化Vim-IDE。[使用手册](https://spacevim.org/cn/documentation/)

- gnome 桌面： 装了gnome桌面和它的一系列插件之后我才真正感受到了Ubuntu的魅力！（教程以及主题百度很多）

- docky: 一款mac风格的dock,删除图标直接拉出去(sudo apt-get install docky)

- tweak-tool: 与gnome桌面对应的是tweak-tool(sudo apt install unity-tweak-tool)

- yakuake : 可以从上方一键滑出和滑入的终端（滑出时强制窗口在最前端）（gnome中也有类似功能的插件，两个选一个即可）

- Moeditor: Ubuntu下界面简洁美观，功能强大的markdown格式文件编辑器，已经在github上开源

- processon： 一个网页上的设计工具，可以很简单地完成诸如流程图的设计和生成图片文件。

## 一些注意点
---

- **F11键可以进入全屏模式**

- 触摸板双击之后再移动就相当于长按鼠标左键的效果了

- 在Ubuntu终端窗口中，复制粘贴的快捷键需要加上 shift，即粘贴是 ctrl+shift+v。

- ssh cyx@192.168.1.201 cyx  高性能服务器  WIFI:sklcc_slave

- 192.168.1.201:18080
- 192.168.1.201:18088 进程
- 192.168.1.201:50070 hdfs


###### 关于添加Ubuntu的本地ssh-key与github相关联

- 首先检测本地有没有安装ssh  `终端输入ssh`

- 然后终端执行`ssh-kengen -t rsa`，连续三次默认回车就行。接着 ~/.ssh目录下就会多出来两个文件：`id_rsa`和`id_rsa.pub`

- 接着只要在github上添加`id_rsa.pub`这个key就行了。在github的setting中，找到sshkey一栏，选择new key，将`id_rsa.pub`的文件内容复制到里面，随便起个title即可。


###### 关于挂载本地的卷到Ubuntu

- 使用`mount /dev/卷名  /挂载点`   //将某个卷挂载到某个文件目录下，该卷就可以在这个文件目录下访问了。

- Ubuntu中，所有的硬件设备都是作为文件存储的，这一点与Windows不同。

###### 关于桌面快捷方式的创建

- 方法一：进入 /usr/share/applications/ 目录，里面会有**绝大多数**你安装的软件的 .desktop文件，只需要把你需要的软件的 .desktop文件复制到home目录下的 桌面文件夹里即可。

- 方法二： 有点蠢但是很简单的一个方法。对于那些没有安装直接可以使用的软件，我们在上个方法中提到的文件夹里是找不到 .desktop文件的。怎么办呢？我们只需要进入我们那个软件的目录，找到启动文件，创建一个它的链接文件（右键还是终端随意），然后将这个链接文件复制到桌面，改下名字即可。虽然和简单，但是缺点是没有图标....身为一个外观党还是有点难以接受的...

- 方法三：就是自己写一个.desktop文件，这里举例我写的Moeditor的桌面文件：
```
//首先终端切到桌面
vim Moeditor.desktop
//然后输入如下内容
[Desktop Entry]
Version=1.0
Type=Application
Name=Moeditor
GenericName=Moeditor
Comment=editor for markdown
Exec=/home/fleshier/Programe\ Files/Moeditor-linux-x64/Moeditor %F  //文件启动器的路径
Terminal=false
Icon=/home/fleshier/Programe\ Files/Images/icons/g10.png  //图标的路径
StartupNotify=true
Actions=Window;
//空行
[Desktop Action Window]
Name=New Window
Exec=/home/fleshier/Programe\ Files/Moeditor-linux-x64/Moeditor -n
OnlyShowIn=Unity;
```
- 保存之后执行 `chmod a+x filename` 改变执行权限即可运行

- 实际写的时候要把注释删除掉，不然会出错。

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

- 分布式文件系统的文件路径完整格式为 `hdfs://namenode|master:编号/root/...`
- 例如：`hdfs://master:8020/dataset/evaluation/bots_10m_10.csv`

- `hdfs dfs -ls  /...`显示分布式文件系统中某个目录（实际并不存在，只是逻辑上的）下的文件

- `hdfs dfs -rm -r file|directory` 删除某个文件

- 附[vim教程](https://github.com/wsdjeg/vim-galore-zh_cn)

<br>

>最后更新于2018.4.19
