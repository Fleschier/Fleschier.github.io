---
layout:     post
title:      "Hadoop单机伪分布式环境搭建"
date:       2018-05-30 09:46:00
tags:   ๑Hadoop ๑BigData
---

## Hadoop 单机伪分布式环境搭建
---

#### 前言

- 这是对之前spark环境搭建的一点补充。

- 首先要了解一下Hadoop的运行模式：

- 单机模式（standalone）:单机模式是Hadoop的默认模式。当首次解压Hadoop的源码包时，Hadoop无法了解硬件安装环境，便保守地选择了最小配置。在这种默认模式下所有3个XML文件均为空。当配置文件为空时，Hadoop会完全运行在本地。因为不需要与其他节点交互，单机模式就不使用HDFS，也不加载任何Hadoop的守护进程。该模式主要用于开发调试MapReduce程序的应用逻辑。

- 伪分布模式（Pseudo-Distributed Mode）: 伪分布模式在“单节点集群”上运行Hadoop，其中所有的守护进程都运行在同一台机器上。该模式在单机模式之上增加了代码调试功能，允许你检查内存使用情况，HDFS输入输出，以及其他的守护进程交互。

- 全分布模式（Fully Distributed Mode）:Hadoop守护进程运行在一个集群上。

#### 新建用户

- 添加一个名为hadoop到系统用户，专门用来做Hadoop测试:
```
sudo addgroup hadoop
sudo adduser --ingroup hadoop hadoop
```

- 再赋予hadoop用户 sudo的权限：`sudo usermod -aG sudo hadoop
`
- 这里`sudo`是我的电脑上有sudo权限的用户组的名称，你可以`cat /etc/group`看看有哪些用户组以及这些用户组下的用户。

- 实在不行就吧你原来用户在的组都加一个hadoop用户

- [创建新用户并增加管理员详解](https://blog.csdn.net/lymemoryzz/article/details/50627767)

#### 安装ssh

- **注意先切换到hadoop用户**

- 命令：`sudo apt-get install openssh-server `

- 启动服务：`sudo /etc/init.d/ssh start `

- 检查服务是否正确启动：`ps -e | grep ssh  `

![](/images/Hadoop/ssh_log.png)

#### 生成公钥和私钥

- 这个也要在hadoop用户下完成(因为这会在你这个用户的文件夹下的.ssh文件夹生成key)

- 我们要设置成免密码登录，生成私钥和公钥：`ssh-keygen -t rsa -P ""`

![](/images/Hadoop/ssh_key.png)

- 第一次操作时会提示输入密码，按Enter直接过，这时会在～/home/{username}/.ssh下生成两个文件：id_rsa和id_rsa.pub，前者为私钥，后者为公钥，现在我们将公钥追加到到authorized_keys中（authorized_keys用于保存所有允许以当前用户身份登录到ssh客户端用户的公钥内容）：
- `cat ~/.ssh/id_rsa.pub >> ~/.ssh/authorized_keys  `

- 现在登录就不需要密码了：`ssh localhost `

- `exit`命令退出登录localhost

- 确保下面的操作在hadoop用户下完成：`sudo chown -R  hadoop:hadoop/usr/local/Apache/hadoop... (自己hadoop的安装路径)`

- 最后输入 `hadoop version` 确认安装

- 至此单机模式配置完成(在hadoop用户下的单机模式)

#### 伪分布式环境搭建

-

<br>
最后更新于2018.5.30
