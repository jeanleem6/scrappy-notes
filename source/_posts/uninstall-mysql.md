---
title: Uninstall Mysql
date: 2016-11-17 13:47:19
tags: [mysql, server]
---

## dmg 安装包

如果通过 dmg安装包 方式安装的Mysql，需要手动删除部分Mysql运行和配置文件，如下为删除相关文件的shell，可能不存在，但尽量查找并删除，避免出现一些莫名问题。

``` bash
    sudo rm /usr/local/mysql
    sudo rm -rf /usr/local/mysql*
    sudo rm -rf /Library/StartupItems/MySQLCOM
    sudo rm -rf /Library/PreferencePanes/My*
    vim /etc/hostconfig  (and removed the line MYSQLCOM=-YES-)
    rm -rf ~/Library/PreferencePanes/My*
    sudo rm -rf /Library/Receipts/mysql*
    sudo rm -rf /Library/Receipts/MySQL*
    sudo rm -rf /var/db/receipts/com.mysql.*
```

<!-- more -->

## brew install

通过 `brew install mysql` 命令行方式安装的Mysql，可以运行如下命令删除Mysql:

``` bash
    brew uninstall mysql
    brew cleanup
    launchctl unload -w ~/Library/LaunchAgents/homebrew.mxcl.mysql.plist
    rm -Rf ~/Library/LaunchAgents/homebrew.mxcl.mysql.plist
```

---

reference:

[How do you uninstall MySQL from Mac OS X?][ref-01]

[ref-01]: http://stackoverflow.com/questions/1436425/how-do-you-uninstall-mysql-from-mac-os-x
