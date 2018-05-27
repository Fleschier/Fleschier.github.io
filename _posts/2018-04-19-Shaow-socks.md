---
layout:     post
title:      "Shadowsocks"
date:       2018-04-19 22:04:00
tags:   ๑ScientificSurfing ๑Ubuntu
---
> 科学上网从我做起  

## 安装Shadowsocks-Qt5
---
```
sudo add-apt-repository ppa:hzwhuang/ss-qt5
sudo apt-get update
sudo apt-get install shadowsocks-qt5
```
## 配置 shadowsocks-qt5
---
- 找好代理服务器，下载配置文件，选择从.json文件导入配置


## 使用ssr
---

- 自己租好服务器之后，获得了服务器的相关信息之后，借用别人的一个脚本来简单实现ssr终端使用

- [链接](https://showzeng.itscoder.com/shadowsocksr/2017/12/02/use-ssr-under-linux)

- 这个里面的github网址没法clone，所以我fork了一份备份到我自己的guithub下. `git clone git@github.com:Fleschier/shadowsocksr.git`

- runssr 和 stopssr 两个脚本文件在 /usr/local/bin 目录下

- 目录 shadowsocksr/ 在 /opt/ 目录下

- 启动ssr:终端输入 `runssr`

- 停止ssr：终端输入 `stopssr`


## 图形界面的ssr
---

- [链接](https://github.com/erguotou520/electron-ssr/releases)

- 配置方法与windows几乎一致

> [参考文档](https://www.litcc.com/2016/12/29/Ubuntu16-shadowsocks-pac/)
