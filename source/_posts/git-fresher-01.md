---
title: Git 使用入门 01-准备（Mac）
date: 2016-11-14 10:49:00
tags: [git]
---

> 将你的 `code` 托管到 `git`，从此不用再担心：**代码丢失、误删、误改**
> `git` *鼓励*你多提交代码，这样你的备份愈多，可回溯的点也愈多

> 下面就来get这项技能

## 一 安装 git

打开terminal，执行如下命令

- 如果你没有安装过git，这个命令将为你**自动安装**

    ``` bash
        git
    ```

- **查看版本**

    ``` bash
        git --version
    ```
<!-- more -->

## 二 配置 git

- 首先，配置你的**用户名**和**email**，这一步非常重要，因为以后每一次的git commit，这两条信息都会被永久性地嵌入

    ``` bash
        git config --global user.name "John Doe"
        git config --global user.email johndoe@example.com
    ```

- **检查配置**

    ``` bash
        git config --list  # 查看所有配置，包括下面的git别名
        git config user.name  # 查看用户名
        git config user.email  # 查看email
    ```

- git别名（提高效率）

    ``` bash
        $ git config --global alias.co checkout
        $ git config --global alias.br branch
        $ git config --global alias.ci commit
        $ git config --global alias.st status
        $ git config --global alias.unstage 'reset HEAD --'  # 取消暂存文件
        $ git config --global alias.last 'log -1 HEAD'  # 显示最后一条 commit
    ```

## 三 git帮助

可以通过4种方式查看git的帮助

``` bash
    git help
    git help <verb>
    git <verb> --help
    man git-<verb>
```

`<verb>`为git的命令，如：config、add、clone等，如：

``` bash
    git help config
```

## 四 建立 SSH key

SSH key 可以让你在你的电脑和 Git 之间建立安全的加密连接

- 创建 SSH key

    ``` bash
        ssh-keygen -t rsa -C "example@gmail.com"
    ```
- 查看你的 public key

    ``` bash
        cat ~/.ssh/id_rsa.pub
    ```

- 添加到 SSH keys 中 <https://github.com/settings/ssh>

> 如果不能建立连接，[检查SSH是否开启][links-1]

[links-1]: /2016/11/14/ssh-on-and-off-in-Terminal/


到此，准备工作完成。

[下一篇][links-2]介绍[git基础][links-2]

[links-2]: /2016/11/16/git-fresher-02/

---

reference:
<https://git-scm.com/book/zh/v2>


