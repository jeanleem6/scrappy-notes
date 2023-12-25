---
title: Git 使用入门 03-远程仓库的使用（Mac）
date: 2016-11-16 09:18:32
tags: [git]
---

## 查看远程仓库

``` bash
    git remote  # 至少应该能看到 origin - 这是 Git 给你克隆的仓库服务器的默认名字
    git remote -v  # 显示需要读写远程仓库使用的 Git 保存的简写与其对应的 URL
```

## 添加远程仓库

``` bash
    git remote add <shortname> <url>  # 添加一个新的远程 Git 仓库

    # 例如：
    git remote add pb https://github.com/paulboone/ticgit
```

<!-- more -->

## 从远程仓库中抓取与拉取

``` bash
    git fetch [remote-name]

    # 例如：
    git fetch origin
```

这个命令会访问远程仓库，从中拉取所有你还没有的数据。执行完成后，你将会拥有那个远程仓库中所有分支的引用，可以随时合并或查看。

``` bash
    # 拉取远程代码并合并
    git pull [remote] [branch]

    # 例如:
    # 拉取master分支的远程代码库upstream并合并到local
    git pull upstream master
    # 等于下面两条命令
    git fetch
    git merge
```


## 推送到远程仓库

``` bash
    git push [remote-name] [branch-name]

    # 例如：
    git push origin master  # 将 master 分支推送到 origin 服务器
```

只有当你有所克隆服务器的写入权限，并且之前没有人推送过时，这条命令才能生效。当你和其他人在同一时间克隆，他们先推送到上游然后你再推送到上游，你的推送就会毫无疑问地被拒绝。你必须先将他们的工作拉取下来并将其合并进你的工作后才能推送。

## 查看远程仓库

``` bash
    git remote show [remote-name]

    # 例如：
    git remote show [remote-name]
    git remote show  # 可以看到更多的信息
```

## 远程仓库的移除与重命名

``` bash
    git remote rename oldname newname  #重命名

    # 例如：
    git remote rename pb paul  # 将 pb 重命名为 paul，这同样也会修改你的远程分支名字，那些过去引用 pb/master 的现在会引用 paul/master。

    git remote rm  #移除

    # 例如：
    git remote rm paul
```

## git 标签

``` bash
    git tag -a v1.4 -m 'my version 1.4'  # 设置标签，-m后为给标签指定的信息
    git tag  # 列出标签
    git tag -l 'v1.4'  # 使用特定模式查找标签
```

---

reference:
<https://git-scm.com/book/zh/v2>

