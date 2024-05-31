---
title: vim 使用
date: 2016-11-23 15:12:10
tags: [vim]
---

## 进入vim编辑器

``` bash
    vim [File PATH]

    #例如：
    vim ～/.zshrc
```

## 进入、退出编辑模式

``` bash
    A  #按 🅰️ 键进入编辑模式
```

<!-- more -->

``` bash
    esc  #按 esc 键退出编辑模式
```

> 下面几个操作需要先退出`编辑模式`

## 保存并退出

``` vim
    #以下两个命令均为保存并退出
    :wq
    shift ZZ  #按住shift键，同时按2次 z 键
```

## 不保存退出

``` vim
    :quit  #未做任何修改适用
    :quit!  #有无修改均适用
```
