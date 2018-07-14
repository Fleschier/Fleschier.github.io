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

###### 配置ssh无密码登录

- 这个也要在hadoop用户下完成(因为这会在你这个用户的文件夹下的.ssh文件夹生成key)

- 我们要设置成免密码登录，生成私钥和公钥：`ssh-keygen -t rsa -P ""`

![](/images/Hadoop/ssh_key.png)

- 第一次操作时会提示输入密码，按Enter直接过，这时会在～/home/{username}/.ssh下生成两个文件：id_rsa和id_rsa.pub，前者为私钥，后者为公钥，现在我们将公钥追加到到authorized_keys中（authorized_keys用于保存所有允许以当前用户身份登录到ssh客户端用户的公钥内容）：
- `cat ~/.ssh/id_rsa.pub >> ~/.ssh/authorized_keys  `

- 多台实体机进行通信（发送或者读取数据，namenode和datanode之间）就是借助ssh，在通信过程中如果需要操作人员频繁输入密码是不切实际的，所以需要ssh的无密码登录。

- 现在登录就不需要密码了：`ssh localhost `

- `exit`命令退出登录localhost

###### 安装hadoop

- 我下载的是hadoop-2.7.6版本

- 存放的路径是`/uer/local/Apache/hadoop-2.7.6`

- 然后修改path环境变量，路径对应自己的实际存放路径：
![](/images/Hadoop/path.png)

- 修改hadoop-env.sh: **(这个不能用默认的，否则会报错)**
```
export JAVA_HOME=${JAVA_HOME} #将这个改成JDK路径，如下  
export JAVA_HOME=/opt/jdk1.8.0_172
```

- 确保下面的操作在hadoop用户下完成：`sudo chown -R  hadoop:hadoop /usr/local/Apache/hadoop-2.7.6 (自己hadoop的安装路径)`

- 最后输入 `hadoop version` 确认安装

- 至此单机模式配置完成(在hadoop用户下的单机模式)

#### 伪分布式环境搭建

-设定*-site.xml:这里需要设定三个文件。我的三个文件的路径是`/usr/local/Apache/hadoop-2.7.6/etc/hadoop/`

- core-site.xml:  Hadoop Core的配置项，例如HDFS和MapReduce常用的I/O设置等。
- hdfs-site.xml:  Hadoop 守护进程的配置项，包括namenode，辅助namenode和datanode等。
- mapred-site.xml： MapReduce 守护进程的配置项，包括jobtracker和tasktracker。

###### 首先在hadoop根目录下新建几个文件夹：
```
mkdir hdfs
mkdir hdfs/name
mkdir hdfs/data
mkdir tmp
```

- 接下来编辑这三个文件：

core-site.xml:
```
<configuration>  
    <property>  
        <name>fs.default.name</name>  
        <value>hdfs://localhost:9000</value>  
    </property>  
    <property>  
        <name>hadoop.tmp.dir</name>  
        <value>/usr/local/Apache/hadoop-2.7.1/tmp</value>  
    </property>  
</configuration>  
```

hdfs-site.xml:
```
<configuration>  
    <property>  <!--设置副本数1，不写默认是3份-->
        <name>dfs.replication</name>  
        <value>1</value>  
    </property>  
    <property>  
        <name>dfs.name.dir</name>  
        <value>/usr/local/Apache/hadoop-2.7.1/hdfs/name</value>  
    </property>  
    <property>  
        <name>dfs.data.dir</name>  
        <value>/usr/local/Apache/hadoop-2.7.1/hdfs/data</value>  
    </property>  
</configuration>  
```

mapred-site.xml:
```
<configuration>  
    <property>  
        <name>mapred.job.tracker</name>  
        <value>localhost:9001</value>  
    </property>  
</configuration>  
```
###### 格式化hdfs

- 启动Hadoop到相关服务，格式化namenode,secondarynamenode,tasktracker的文件系统目录:
```
source /usr/local/Apache/hadoop-2.7.1/etc/hadoop/hadoop-env.sh
hadoop namenode -format
```

###### 启动hadoop

- **首先要先连接到localhost!!**(否则无法在网页上查看节点)。
`ssh localhost`

- 我的`start-all.sh`脚本在sbin目录下，各个版本可能不太一样，如果这个文件夹没有就去别的文件夹找找。

- 执行start-all.sh来启动所有服务:
```
cd sbin
./start-all.sh
```

- 使用命令`jps`查看是否启动成功：
![](/images/Hadoop/launch_info.png)
如果出现NodeManager DataNode Jps SecondaryNameNode ResourceManager NameNode则表示启动成功(缺一不可)

- 检查运行状态:
所有的设置已完成，Hadoop也启动了，现在可以通过下面的操作来查看服务是否正常，在Hadoop中用于监控集群健康状态的Web界面：

`http://localhost:50030/     - Hadoop 管理介面`

`http://localhost:50060/     - Hadoop Task Tracker 状态`

`http://localhost:50070/     - Hadoop DFS 状态`

- 目前我只有50070是正常访问的，其余的还不能访问，原因有待进一步探究
![](/images/Hadoop/datanode_info.png)


- 停止服务：
`./stop-all.sh`

 ![](/images/Hadoop/stop_all.png)

- 由于之前已经将hadoop的`bin`和`sbin`两个目录添加到系统环境路径里去了，这样下次启动直接就可以是
```
ssh localhost
start-all.sh
...
stop-all.sh
```
这样就方便很多了。

- 参考博客——[hadoop伪分布式搭建](https://blog.csdn.net/hitwengqi/article/details/8008203)，[很详细的搭建步骤(Hadoop-2.7.2版本)](https://blog.csdn.net/Dr_Guo/article/details/50886667)

<br>
> 最后更新于2018.5.31
