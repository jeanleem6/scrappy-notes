---
title: Mac下安装Homebrew/ZSH/Node/NPM
date: 2016-11-20 11:14:07
tags: [server, Mac]
---

## 安装 [Homebrew][link-01]

``` bash
    /usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
```

[link-01]:http://brew.sh/

**自检Brew**

``` bash
    brew doctor
```

## 安装 [oh-my-zsh][link-02]

``` bash
    sh -c "$(curl -fsSL https://raw.githubusercontent.com/robbyrussell/oh-my-zsh/master/tools/install.sh)"
```

[link-02]:http://ohmyz.sh

<!-- more  -->

## 安装Node

安装Node之前先确认以下两件事：

1. 安装 **XCode**
    XCode是免费的，可在[Apple App Store][links-01]上找到。

2. 安装好了 **Homebrew**
    > **为什么使用Homebrew**
    >
    > 1. 通过安装包安装Node，必须通过`sudo`来取得administrators的权限以正确安装；而通过Homebrew来安装Node（或其它package）有一个好处就是不需要取得administrators权限，这确保了电脑的安全。
    > 2. 通过安装包安装Node，需要添加node的路径到你的`system $PATH`，这会让新手心生畏惧；虽然Homebrew这种方法需要安装几种不同的软件，但是只需简单的点击和等待，这是一种稍微耗时一点的方法，但是更安全。
    > 3. Homebrew对程序员来说是一个非常棒的工具。首先，它让移除Node变得非常简单（一条简单的命令搞定）；第二，让你安装其它有用的packages（如git、Ruby、wget等）变得非常非常简单。

[links-01]: https://itunes.apple.com/us/app/xcode/id497799835?mt=12



### 安装

``` bash
    brew install node
```

<!--  -->

``` bash
    node -v  #检查node版本
    npm -v  #检查npm版本
```

### 更新

``` bash
    brew update  # 更新Homebrew
    brew upgrade node  # 更新Node和NPM
```

### 卸载

``` bash
    brew uninstall node  # 卸载Node和NPM
```
