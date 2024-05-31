---
title: Boost Baidu-Cloud
date: 2016-09-01 08:39:01
tags: [tools, Mac, aria2]
---

Mac 用户肯定都受够了百度网盘在自己电脑上的糟糕体验，至少我是如此：安装官方的 App，经常下载时中断，有时甚至 Bug 般连续中断，无奈使用浏览器下载，速度却是令人挠头。花点时间来配置 aria2，结合 Chrome，一定让你舒心。

## aria2 是什么？

aria2 是一款支持多种协议的轻量级命令行下载工具。有以下特性：

- 多线程连线：aria2 会自动从多个线程下载文件，并充分利用你的带宽；
- 轻量：运行时不会占用过多资源，根据官方介绍，内存占用通常在 4MB~9MB，使用 BitTorrent 协议，下行速度 2.8MB/s 时 CPU 占用率约 6%；
- 全功能 BitTorrent 客户端；
- 支持 RPC 界面远程控制（下文重点介绍）。

## 下载方式介绍

- 一种为**command-line download mode(命令行下载模式)**；
- 另一种为**RPC server mode(RPC服务器模式)**

第一种模式推荐技术人员使用；第二种模式推荐普通人使用。

<!-- more -->

## 1、命令行下载模式

命令行下载可以直接使用，例如：

Download from WEB:

``` bash
aria2c http://example.org/mylinux.iso
```

Download from 2 sources:

``` bash
aria2c http://a/f.iso ftp://b/f.iso
```

Download using 2 connections per host:

``` bash
aria2c -x2 http://a/f.iso
```

BitTorrent:

``` bash
aria2c http://abc.org/123.torrent
```

BitTorrent Magnet URI:

``` bash
aria2c 'magnet:?xt=urn:btih:248D0A1CD08284299DE78D5C1ED359BB46717D8C'
```

Metalink:

``` bash
aria2c http://example.org/mylinux.metalink
```

Download URIs found in text file:

``` bash
aria2c -i uris.txt
```

## 2、RPC服务器模式

### 下载 aria2

你可以在[aria2][link-01] 的 Download 下载对应的安装程序。下载之后直接双击打开安装即可。喜欢用 homebrew 的同学也可以使用命令`brew install aria2`来安装，已经安装好 aria2 的同学直接看第五步。

[link-01]: http://aria2.sourceforge.net/

### 安装 Homebrew

``` bash
    ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
```

### 安装 aria2

``` bash
    brew install aria2
```

### 设置配置文件
aria2 提供两种方式使用，一种是直接命令行模式下载，不推荐使用这种方法，推荐使用另外一种 RPC 模式，这种方式 aria 启动之后只会安静的等待下载请求，下载完成后也只会安静的驻留后台不会自动退出。而使用RPC模式推荐做一个配置文件方便使用。我们把配置文件放在 `~/.aria2` 下，依次输入命令：

``` bash
    cd ~
    mkdir .aria2
    cd .aria2
    touch aria2.conf
```

接着打开 Finder，利用 Shift+Cmd+G 进入路径：`~/.aria2/aria2.conf`，用文本编辑器打开 aria2.conf，将[雪月秋水君][link-02]提供的以下配置直接拷贝进去：

``` bash
    #用户名
    #rpc-user=user
    #密码
    #rpc-passwd=passwd
    #上面的认证方式不建议使用,建议使用下面的token方式
    #设置加密的密钥
    #rpc-secret=token
    #允许rpc
    enable-rpc=true
    #允许所有来源, web界面跨域权限需要
    rpc-allow-origin-all=true
    #允许外部访问，false的话只监听本地端口
    rpc-listen-all=true
    #RPC端口, 仅当默认端口被占用时修改
    #rpc-listen-port=6800
    #最大同时下载数(任务数), 路由建议值: 3
    max-concurrent-downloads=5
    #断点续传
    continue=true
    #同服务器连接数
    max-connection-per-server=5
    #最小文件分片大小, 下载线程数上限取决于能分出多少片, 对于小文件重要
    min-split-size=10M
    #单文件最大线程数, 路由建议值: 5
    split=10
    #下载速度限制
    max-overall-download-limit=0
    #单文件速度限制
    max-download-limit=0
    #上传速度限制
    max-overall-upload-limit=0
    #单文件速度限制
    max-upload-limit=0
    #断开速度过慢的连接
    #lowest-speed-limit=0
    #验证用，需要1.16.1之后的release版本
    #referer=*
    #文件保存路径, 默认为当前启动位置
    dir=/Users/xxx/Downloads
    #文件缓存, 使用内置的文件缓存, 如果你不相信Linux内核文件缓存和磁盘内置缓存时使用, 需要1.16及以上版本
    #disk-cache=0
    #另一种Linux文件缓存方式, 使用前确保您使用的内核支持此选项, 需要1.15及以上版本(?)
    #enable-mmap=true
    #文件预分配, 能有效降低文件碎片, 提高磁盘性能. 缺点是预分配时间较长
    #所需时间 none < falloc ? trunc « prealloc, falloc和trunc需要文件系统和内核支持
    file-allocation=prealloc
```

默认下载路径的「/Users/xxx/Downloads」可以改为任何你想要的绝对路径。此处写为 Downloads 目录，xxx 请自行替换成你的 Mac 用户名，然后保存，退出编辑器。

[link-02]: https://blog.icehoney.me/about

### 启动 RPC 模式

``` bash
    aria2c --conf-path="/Users/xxxxxx/.aria2/aria2.conf" -D
```

但是如何搞定百度网盘？还需要在 [这里] [link-03] 下载 Chrome 插件。

[link-03]: https://chrome.google.com/webstore/detail/baiduexporter/mjaenbjdjmgolhoafkohbhhbaiedbkno

### 如何下载

随便打开一个百度网盘的链接，会发现网页上多出一个「导出下载」按钮，点击它弹出的「ARIA2 RPC」就自动添加到你的下载队列里了，然后利用 [管理界面][link-04] 或 [管理界面一][link-05] 提供的网页界面管理你的下载任务。

**管理界面**

点右上角的扳手按钮，修改`JSON-RPC Path`内容：

``` bash
    http://binux.github.io:6800/jsonrpc
    # 改为
    http://127.0.0.1:6800/jsonrpc
```

**管理界面一**

依次点击 **设置** > **连接设置**，将**主机：**的值修改为localhost

如果你想关掉后台的 aria2，可以到活动监视器中找到 aria2c 杀掉，也可以在终端输入`kill aria2`之后按 Tab 键，aria2 会自动变成进程号，回车即可杀掉它。

[link-04]: http://binux.github.io/yaaw/demo/
[link-05]: http://ziahamza.github.io/webui-aria2/

---

reference:
<http://sspai.com/32167>
<https://aria2.github.io>
