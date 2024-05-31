---
title: MAC下终端走代理的几种方法
date: 2018-07-02 09:23:33
tags: [Mac, agent]
---

### 方法1:
在终端中直接运行命令

``` bash
export http_proxy=http://proxyAddress:port
```

这个办法的好处是简单直接，并且影响面很小（只对当前终端有效）。

### 方法2:
把代理服务器地址写入shell配置文件.bashrc或者.zshrc
直接在.bashrc或者.zshrc添加下面内容

``` bash
export http_proxy="http://localhost:port"
export https_proxy="http://localhost:port"
```

以使用shadowsocks代理为例，ss的代理端口为1080,那么应该设置为

``` bash
export http_proxy="http://127.0.0.1:1080"
export https_proxy="http://127.0.0.1:1080"
```

localhost就是一个域名，域名默认指向 127.0.0.1，两者是一样的。
然后 `ESC` 后 `:wq` 保存文件，接着在终端中执行 `source ~/.bashrc`
或者退出当前终端再起一个终端。 这个办法的好处是把代理服务器永久保存了，下次就可以直接用了。

### 方法3:
改相应工具的配置，比如apt的配置

``` bash
sudo vim /etc/apt/apt.conf
```

在文件末尾加入下面这行

``` bash
Acquire::http::Proxy "http://proxyAddress:port"
```

保存apt.conf文件即可。关于apt的代理设置可以参考[这里](http://askubuntu.com/questions/349702/apt-conf-acquirehttpproxy-proxyserverport-seems-not-to-be-used-ubuntu-13)
关于git的代理设置看这里:[用shadowsocks加速git clone](http://blog.fazero.cc/2015/07/11/%E7%94%A8shadowsocks%E5%8A%A0%E9%80%9Fgit-clone/)

### 方法4:
[利用proxychains在终端使用socks5代理](http://blog.fazero.cc/2015/08/31/%E5%88%A9%E7%94%A8proxychains%E5%9C%A8%E7%BB%88%E7%AB%AF%E4%BD%BF%E7%94%A8socks5%E4%BB%A3%E7%90%86/)

### 补充：
如果代理服务器需要登陆，这时可以直接把用户名和密码写进去

``` bash
http_proxy=http://userName:password@proxyAddress:port
```
