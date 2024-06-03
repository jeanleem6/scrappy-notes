---
title: brew_cask_install_software
date: 2018-01-14 09:56:44
description: 用 brew 安装和管理 Mac 的软件✨
tags: [Mac,tools]
---

首先你需要改装下Mac的Terminal，在终端里安装homebrew

``` bash
/usr/bin/ruby -e "$(curl -fsSL <a href="https://raw.githubusercontent.com/Homebrew/install/master/install"
```

你可以方便快捷的通过类似于`brew install python3`的命令安装诸如MySQL、R亦或是一些你需要的包，其他的命令参见homebrew官网，你可以方便的升级或卸载各种各样的包

另外在这里推荐你 `brew install cask`

比如说我们想安装纯洁的chrome浏览器 `brew cask install google-chrome`就好啦，而且下载速度很快，当然哪天用的不舒服了，uninstall就好

附上安装和卸载Yandex的图

![Terminal-Install yandex](165839nk1c2bqgw4qqbcab.png)

安装完后 应用程序栏就会出现

然后卸载`brew cask uninstall yandex`，毕竟我的主力浏览器是Safari和Chrome，当然安卓端大力推荐Yandex
![Terminal-Uninstall yandex](170054cxxdqoz7ozo5xzc7.png)

非常的方便快捷有没有
对了，记得 `brew cask cleanup`清理缓存及软链

另外`brew cask` 和 `brew`的区别在于 brew主要用来下载一些不带界面的命令行下的工具
brew cask主要用来下载一些图形化界面的应用软件，下载好后会自动安装，并能在mac中直接运行使用

- - -

再安利一个小东西 **you-get**
一个基于 Python 3 的下载工具。使用 You-Get 可以很轻松的下载到网络上的视频、图片及音乐，油管的也可以哦
![Tool you-get](171135m4zaax6ardkp4aka.png)

详情请参见[you-get 主页](https://you-get.org/)

这里是一个youtube视频下载的实例
![you-get-download video](246E39B3-6EF5-4066-AB16-ACDC94FC4948.png)

你可以通过Mac的terminal学习Linux的command line ，如果出现了command not found，这个时候你可以通过homebrew来安装那些缺失的包附上一个链接：[Linux 命令行学习网站](https://billie66.github.io/TLCL/book/)

值得一提的一些命令行

显示/不显示 隐藏文件 `defaults write com.apple.finder AppleShowAllFiles TRUE/FAUSE`

还有如果你把Mac玩坏了，可以参考一下这篇文章：制作正式版 [macOS 10.12 Sierra 安装 U盘](http://www.jianshu.com/p/a1851d7deee8)，亲测有效

哦对了，Mac的终端需要美化，具体步骤可以参考：[让Mac OS X的终端多姿多彩](http://linfan.info/blog/2012/02/27/colorful-terminal-in-mac/)
