---
layout:     post
title:      "Intellij IDEA Ultimate版本使用"
date:       2018-05-25 09:46:00
tags:   ๑JetBrains ๑JS
---

## JetBrains Toolbox
---

- 如果你决定使用jetbrains的开发环境的话，那么去官网上获取一个jetbrains toolbox会是个不错的主意～

- 这个工具可以很方便地管理你的所有jetbrains的产品，避免了太多快捷方式的麻烦。

## 免费获取Ultimate版本
---

- jetbrains给学生的优惠还是非常大的，我们可以用我们学校的邮箱免费获取JetBrains全家桶

- 这个在我上一篇文章里也提到了，这里再作一次系统的记录。

- [Jetbrains学生免费账号申请](https://sales.jetbrains.com/hc/zh-cn/articles/207154369-%E5%AD%A6%E7%94%9F%E6%8E%88%E6%9D%83%E7%94%B3%E8%AF%B7%E6%96%B9%E5%BC%8F)

- 申请流程其实很简单，你需要一个你们学校的邮箱即可。然后验证通过之后会发送验证邮件，依次填写并且最终注册完账号即可激活。注册的时候一定要确定邮箱的地址填写正确，不出于意外一分钟之内就能收到确认邮件。

- 如果填错了也没关系，你可以一遍一遍地写邮箱然后申请，jetbrains好像对此没有什么限制。

- 成功激活：

![](/images/node.js/info.png)

## 初始配置
---

- 装好Ultimate版本之后我们就可以开始配置一些东西了。

- 首先打开intellij IDEA，不用进入某个项目，在初始界面设置(这样这些设置便是对全局生效)

- 在plugins里面添加一些我们需要的插件。比如 scala , nodejs, junitGenerator2.0等，这些插件比community版本要丰富很多。

- 在 system settings 里面把 reopen previous project勾掉，这样每次打开我们就可以手动选择要打开的项目了。

- 然后在global lib里面点击绿色的加号，添加我们用到的编成语言的lib，在弹出的选择框里找到我们安装的目录。比如添加scala的lib，要找到scala sdk的安装目录即可，intellij 会自己扫描目录然后添加lib，最后保存确定即可。

## 添加已有工程时遇到的坑
---

- 最近老师布置了个jdbc的作业，是个eclipse的工程。但是在intellij打开的话，test部分始终有问题，不能访问到src里的代码。。

- 然后换了一种导入工程的方式，但是无论是eclipse方式导入还是maven方式导入，都会出现没有工程可以导入的错误???(No projects are found to import 这个问题在用eclipse来导入工程的时候也可能遇到) 上网查阅之后发现，可能是缺少`.classpath`文件和`.project`文件(或者有可能是这两个文件有问题)。

- 解决方法就是，用eclipse重新建立一个同名的工程，然后把这个工程里面的这两个文件复制到要导入的工程里再试着导入。

- 或者如果代码不太多的话，直接新建一个工程，把代码复制进去就好了。
















<br>
> 最后更新于2018.6.4
