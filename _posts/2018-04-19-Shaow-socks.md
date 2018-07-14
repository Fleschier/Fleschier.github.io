---
layout:     post
title:      "Shadowsocks"
date:       2018-05-28 15:34:00
tags:   ๑ScientificSurfing ๑Ubuntu
---
> 科学上网从我做起  

## 重大更新
---

- 现在大多数的ssr或者ss图形界面的在ubuntu18上已经歇菜了,但是这里分享一个命令行下的ss和一个图形界面的ssr(推荐)。

###### 命令行方式的ss
---

- ```
sudo apt-get install python-pip
sudo pip install shadowsocks
```

- 通过配置文件指定配置信息
```
mkdir ~/.shadowsocks
cd .shadowsocks
touch ss.json
//添加内容如下
{
    "server":"1.1.1.1",
    "server_port":8388,
    "local_address": "127.0.0.1",
    "local_port":1080,
    "password":"your passwd",
    "timeout":300,
    "method":"aes-256-cfb"
}
```
- server填你的服务器ip，sever_port填远程端口号，local_address本地ip，local_part本地端口，password填密码，timeout是延迟时间，method是加密方式，按照实际情况填写并保存

- 终端运行：`sslocal -c ~/.shadowsocks/ss.json`

- 后台运行(不推荐)：`sslocal -c ~/.shadowsocks/ss.json -d start`

- 现在运行的话会有报错，修改方法：
```
vim /usr/local/lib/python2.7/dist-packages/shadowsocks/crypto/openssl.py
//跳转到52行（shadowsocks2.8.2版本，其他版本搜索一下cleanup
//
将第52行libcrypto.EVP_CIPHER_CTX_cleanup.argtypes = (c_void_p,)
改为libcrypto.EVP_CIPHER_CTX_reset.argtypes = (c_void_p,)
//
再次搜索cleanup（全文件共2处，此处位于111行），将libcrypto.EVP_CIPHER_CTX_cleanup(self._ctx)
改为libcrypto.EVP_CIPHER_CTX_reset(self._ctx)
//然后就可以正常运行了
```

- 详细见[博客](https://blog.csdn.net/blackfrog_unique/article/details/60320737)

#### 图形界面的ssr
---

- 首先说一句，图形界面不仅美观好用，而且可以支持在线订阅，及时更新，总之，**我们又可以优雅地翻墙了**，美滋滋～

- 这里我fork了一份相关github的代码，[链接](https://github.com/erguotou520/electron-ssr/releases)

- 配置方法非常简单，可以导入json文件，或者从剪贴板导入等等。

> [参考文档](https://blog.csdn.net/u010658816/article/details/79344970)

## 重点
---

- 上面两种方式而选一即可，但是下面还有最关键的一步，配置浏览器代理。

- 首先，想要实现全局模式请按如下方法设置：
系统设置 >> 网络 >> 网络代理 >> 方法 >> 手动

- 再将Socks主机的ip和端口填好，如图。
![](/images/ssr/systemset.png)

- 然后，需要在google商店下载SwitchyOmega插件，但是需要翻墙～这里可以进入如下[网址](http://googlehelper.net/),先下载一个googlehelper插件(打开chrome所有插件，把下载的插件直接拉进去即可添加完成)，用邮箱注册一个免费的体验账号，先翻了墙再说。

- 然后去chrome网上应用商店下载SwitchyOmega，接下来便可以配置了。

- 在SwitchyOmega的配置页面  
先新建一个情景模式，选择代理服务器，名称为gfwlist(这个随意)  
  配置时,代理服务器和代理端口分别是ssr config中的   
    "local_address":"127.0.0.1"  
    "local_port":1080  
确认后无误后应用选项  
![](/images/ssr/gfwlist.png)

- 接下来点击情景模式中的自动切换，输入参数如下：
```
条件设置：raw.githubusercontent.com  
规则列表网址：https://raw.githubusercontent.com/gfwlist/gfwlist/master/gfwlist.txt  
点击立即更新情景模式  
结束,在SwitchyOmega插件(chorme浏览器右上角处)那换成自动切换,大功告成.
```
![](/images/ssr/auto_switch_01.png)

![](/images/ssr/auto_switch_02.png)

![](/images/ssr/example.png)

- 最后把多余的情景模式删除,看起来清爽一点。

- 这样就相当于在chorme中启用的是pcd模式,在能穿墙的同时,既保证了访问国内网站速度不慢,又节省了ssr的流量。

- 接下来就可以优雅地体验翻墙上网了～

<br>
> 最后更新于2018.5.28
