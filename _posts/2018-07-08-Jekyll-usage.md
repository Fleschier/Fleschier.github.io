---
layout:     post
title:      "Ubuntu下使用jekyll预览博客"
date:       2018-07-08 22:40:00
tags:   ๑Blog
---


## 环境安装
---

确保下面环境的齐全：
```
brew install ruby
//
gem install jekyll
//
gem install bundler
//
gem install jekyll-paginate
//
gem install jekyll-gist
```

- 如果执行命令的过程中有提示什么什么未安装，按照提示的命令来安装即可。

- 然后将终端切换到你博客所在的根目录，执行：`jekyll serve`即可

- 终端中会告诉你博客使用了本地4000端口，在网页中输入：`http://127.0.0.1:4000/
`即可预览博客的效果
