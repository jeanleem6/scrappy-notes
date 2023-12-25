---
title: Git 使用入门 02-基础（Mac）
date: 2016-11-16 09:17:20
tags: [git]
---

> 将你的 `code` 托管到 `git`，从此不用再担心：**代码丢失、误删、误改**
> `git` *鼓励*你多提交代码，这样你的备份愈多，可回溯的点也愈多

## clone 项目

clone项目时自定义本地仓库的名字**mydemo**；如果不自定义，可去掉

``` bash
    git clone https://github.com/jeanleem6/demo mydemo  # mydemo为可选项
```

## 初始化仓库

如果你打算使用 Git 来对现有的项目进行管理，你只需要进入该项目目录并输入：

``` bash
    git init
```

<!-- more -->

## 跟踪新文件

``` bash
    git add [file]  # file为要跟踪的文件，如readme.md，注意：实际操作中去掉[]，下同
```

## 提交更新

``` bash
    git commit -m 'commit'
```
## 跳过使用暂存区域

尽管使用暂存区域的方式可以精心准备要提交的细节，但有时候这么做略显繁琐。 Git 提供了一个跳过使用暂存区域的方式， 只要在提交的时候，给 `git commit` 加上 `-a` 选项，Git 就会自动把所有已经跟踪过的文件暂存起来一并提交，从而跳过 `git add` 步骤：

``` bash
    git commit -a -m 'commit'
```

## 重新提交

``` bash
    git commit -m 'initial commit'
    git add forgotten_file
    git commit --amend  # 最终你只会有一个提交 - 第二次提交将代替第一次提交的结果
```

## 取消暂存的文件

例如你通过 `add *` 添加了 `readme.md、CONTRIBUTING.md` 两个文件到暂存区，但是现在想把 `CONTRIBUTING.md` 从暂存区移除，那么可以通过如下命令实现：

``` bash
    add *
    git reset HEAD CONTRIBUTING.md  # 取消暂存CONTRIBUTING.md文件
```

## 撤消对文件的修改

``` bash
    git checkout -- [file]
```

## 移除文件

1. 移除暂存区文件

    ``` bash
        git rm --cached [file]  # 本地文件不会移除
    ```

2. 同时移除本地和暂存区文件

    ``` bash
        rm [file]  # 移除本地文件
        git rm [file]  # 记录此次移除文件的操作
    ```

    或者

    ``` bash
        git rm -f [file]  # -f为强制删除
    ```

## 移动文件

``` bash
    git mv [file] [file1]  # 将file改为file1，本地和暂存区文件都会被改动
```

## 检查当前文件状态

``` bash
    git status
```

## 状态简览

``` bash
    git status -s
```

## 查看提交历史

``` bash
    git log
```

## 忽略文件

``` bash
    cat .gitignore
```

---

reference:
<https://git-scm.com/book/zh/v2>
