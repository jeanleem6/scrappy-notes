---
title: 同一台电脑同时使用 gitHub 和 gitLab
date: 2024-06-03 10:07:19
description: 工作中我们有时可能会在同一台电脑上使用多个 git 账号，例如：公司的 gitLab 账号；个人的 gitHub 账号。<br /><br />怎样才能在使用 gitLab 与 gitHub 时，切换成对应的账号，并且免密？<br /><br />这时我们需要使用 ssh（git可以选择使用 https 方式、ssh 方式两种方式通信，但使用 https 方式时，每次 `fetch` 和 `push` 代码都需要输入账号和密码），本文将以windows为例。
tags: [git]
---

工作中我们有时可能会在同一台电脑上使用多个 git 账号，例如：

- 公司的 **gitLab** 账号
- 个人的 **gitHub** 账号

怎样才能在使用 gitLab 与 gitHub 时，切换成对应的账号，并且免密？

这时我们需要使用 ssh（git可以选择使用 https 方式、ssh 方式两种方式通信，但使用 https 方式时，每次 `fetch` 和 `push` 代码都需要输入账号和密码），下文将以windows为例。

## 一，生成ssh密钥并配置

分别对 gitLab 和 gitHub 生成对应的密钥（默认情况下本地生成的秘钥位于 `C:/Users/用户名/.ssh/`）

### 1，生成 gitLab 密钥并配置

- 电脑开始菜单中找到已安装的 Git Bash 并打开，输入命令：

  ```bash
  ssh-keygen -t rsa -C "公司邮箱地址" -f ~/.ssh/gitlab_rsa
  ```

  按回车，再按3次enter键，生成对应的 gitLab 密钥：`gitlab_rsa`和 `gitlab_rsa.pub`

- 将 gitLab 公钥即 `gitlab_rsa.pub`（Windows下路径为 `C:/Users/用户名/.ssh/`）中的内容配置到公司的gitlab上，点击右上角的用户头像 > `Preferences` > `SSH Keys`

### 2，生成 gitHub 密钥并配置

- 在gitbash中输入命令：

  ```bash
  ssh-keygen -t rsa -C "github邮箱地址" -f ~/.ssh/github_rsa
  ```

- 生成对应的 gitHub 密钥：`github_rsa` 和 `github_rsa.pub`

- 将 gitHub 公钥即 `github_rsa.pub` 中的内容配置到自己的github上，点击右上角的用户头像 > `Settings` > `SSH and GPG Keys` > `New SSH key`

### 3，配置git，访问不同 host 时使用不同的密钥

- 进入密钥生成的位置（`C:/Users/用户名/.ssh/`），手动创建一个 `config` 文件（注意这个 `config` 文件要无后缀）。

- 在新建的 `config` 文件里面配置如下内容：

  ```ini
  # 自己的github账号配置(HostName 需去掉"https://")
  Host github.com
    port 22
      User git
      HostName github.com
      PreferredAuthentications publickey
      IdentityFile C:\Users\用户名\.ssh\github_rsa

  # 公司的gitlab账号配置(HostName为公司的gitlab地址)
  Host gitlab.com
      port 22
      User git
      # HostName 可以配置域名或 IP (需去掉 "https://")
      HostName gitlab.xxx.com / xxx.xxx.xxx.xxx
      User git
      PreferredAuthentications publickey
      IdentityFile C:\Users\用户名\.ssh\gitlab_rsa
  ```

  > 字段配置简单说明：
  >
  > - **Host** - Host 可以看作是一个你要识别的模式，对识别的模式，配置对应的主机名和ssh 文件
  > - **Port** - 自定义的端口。默认为22，可不配置
  > - **User** - 自定义的用户名，默认为 git，可不配置
  > - **HostName** - 真正连接的服务器地址
  > - **PreferredAuthentications** - 指定优先使用哪种方式验证，支持密码和秘钥验证方式
  > - **IdentityFile** - 指定本次连接使用的密钥文件

## 二，验证是否设置成功

在 `C:/Users/用户名/.ssh` 中，右键点击 `Open Git Bash here`，分别输入命令：

```bash
# 测试github
ssh -T git@github.com

# 测试gitlab(ps: xxx的意思是公司用的是Gitlab的私有域名)
ssh -T git@gitlab.xxx.com

# 没有Gitlab的私有域名，则直接使用 git@gitlab.com
ssh -T git@gitlab.com
```

显示如下信息则说明配置成功

```bash
# for GitHub
Hi 用户名! You've successfully authenticated, but GitHub does not provide shell access.

# for GitLab
Welcome to GitLab, @用户名!
```

## 三，git仓库配置

### 1，简介

在git中，我们使用git config 命令用来配置git的配置文件，git配置级别主要有以下3类：

- **仓库级别 local** 【优先级最高】 - 对应的配置文件是当前仓库下的 `.git/config` 【在当前目录下 `.git` 目录默认是隐藏的，所以在文件管理器中我们要打开显示隐藏文件】
- **用户级别 global**【优先级次之】 - 对应的配置文件是用户宿主目录下的 `~/.gitconfig` 【宿主目录：`C:\Users\用户名`】
- **系统级别 system**【优先级最低】 - 对应的配置文件是 git 安装目录下的 `/etc/gitconfig`

简单了解后我们就可以进行配置了

### 2，配置

- 用户级别配置

  用户级别是配置公司 gitLab 账号还是自己的 gitHub 账号，可以自由选择。因为平常使用公司的代码频率较高，所以我选择将 gitLab 账号配置成用户级别。Git Bash下执行如下命令：

  ```bash
  git config --global user.name '用户名' #公司账号名称
  git config --global user.email '邮箱' #公司账号邮箱
  ```

- 仓库级别配置

  local（仓库级别）配置成 gitHub 的账号。选择一个文件夹作为 gitHub 的本地仓库，在该文件夹里鼠标右键 > `Open Git Bash here`，执行命令：**`git init`**

  再执行命令：

  ```bash
  git config --local user.name '用户名' #github账号名称
  git config --local user.email '邮箱' #github账号邮箱
  ```

  之后自己的 gitHub 的代码都应该在这个仓库下进行 `pull`、`push` 操作。

### 3，克隆项目代码

克隆自己 gitHub 的项目代码至本地仓库。在2.2中的本地仓库打开 Git Bash，输入命令：

```bash
git clone git@github.com:jeanleem6/scrappy-notes.git # github项目地址(clone with ssh)
```

这样就可以对克隆的项目进行git其他的操作了。

至此，我们就可以在这台电脑上同时使用 gitHub 与 gitLab 进行代码的设置就完成了。
