---
title: Git 使用入门 05-Git 分支的应用
date: 2016-11-16 14:10:07
tags: [git]
---

**创建分支**( modify-README 为分支名)：

``` bash
    git checkout -b modify-README
```

注：创建完之后默认切换到这个分区。

**列出所有的分支：**

``` bash
    git branch
```

**合并到主分支：**

``` bash
    git checkout master
    git merge modify-README
```

注：先切换到主分支，再合并。

<!-- more -->

**修改分支名**

``` bash
    git branch -m oldname newname
```

**删除分支：**

``` bash
    # 本地
    git branch -d modify-README
    # 远程
    git push origin --delete modify-README
```



---

reference:
<https://git-scm.com/book/zh/v2>
