---
title: Git 使用入门 04-上传本地项目到 GitHub？
date: 2016-11-16 11:36:03
tags: [git]
---

先进入项目根文件夹

``` bash
    cd demo
    git init
    git add .
    git commit -m "新建项目"
```

到这一步时，你要去你的 GitHub 上新建一个项目，命名为 demo （注意不要选择第三个 - 使用README 文件初始化仓库）

``` bash
    git remote add origin git@github.com:你GitHub的用户名/demo.git
    git push -u origin master
```

<!-- more -->


---

reference:
<https://git-scm.com/book/zh/v2>
