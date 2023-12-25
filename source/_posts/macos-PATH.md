---
title: Mac 配置环境变量
date: 2016-11-02 17:25:32
tags: [server, Mac]
---

## 系统级全局变量

系统级全局变量针对系统所有用户，仅root用户可修改它们；
一般用户想修改它们，可以在命令前加`sudo`，即以root身份执行。

``` bash
    sudo vi /etc/profile
    sudo vi /etc/bashrc
```


## 用户级全局变量

对于一般用户而言，通常我们建议去修改~/.bash_profile或~/.zshrc来设置环境变量，它们是用户级的设置，只对当前用户有效。

<!-- more -->

``` bash
    #shell为bash或zsh
    vi ~/.bash_profile

    #shell为zsh
    vi ~/.zshrc
```

> 命令中的 `vi` 可改为 `vim`，效果一样
> 也可以使用 **nano**，一个更现代、方便的文本编辑器，底部有快捷键列表。
> 使用方式与 **vim** 类似： `nano ~/.zshrc`

## 全局变量立即生效

``` bash
    source [File PATH]

    #例如：
    source ~/.bash_profile
    source ~/.zshrc
```

## 查看环境变量的值

``` bash
    echo $PATH

    #输出：
    /usr/local/bin /usr/local/sbib /usr/local/opt/php56/sbin /usr/local/opt/php56/bin /usr/local/bin /usr/bin /bin /usr/sbin /sbin
```

## 实例

以下命令是为php56添加环境变量，以替代系统自带的PHP版本，直接写入~/.zshrc，不用进vim编辑器

``` bash
    echo 'export PATH="$(brew --prefix php56)/bin:$PATH"' >> ~/.zshrc  #for php
    echo 'export PATH="$(brew --prefix php56)/sbin:$PATH"' >> ~/.zshrc  #for php-fpm
    echo 'export PATH="/usr/local/bin:/usr/local/sbib:$PATH"' >> ~/.zshrc #for other brew install soft
    source ~/.zshrc  #立即生效
```

> 注意：
> 1、`~/.bash_profile`中有个点
> 2、如果是新增环境变量或者是修改环境变量的值，都需要`source`一下才能立即生效。如果是删除一个环境变量，必须输入`exit`以`logout`当前**shell**，然后再重新打开一个新的**shell**并`login`才能生效。
