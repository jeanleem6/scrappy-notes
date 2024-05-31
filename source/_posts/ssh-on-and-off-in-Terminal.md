---
title: 如何通过终端开启/关闭SSH
date: 2016-11-14 10:27:09
tags: [ssh, server]
---

## Mac OS

SSH（Secure Shell）是一种通用的、功能强大的、基于软件的网络安全解决方案。计算机每次向网络发送数据时，SSH都会自动对其进行加密。运行 OS X 又或者是 macOS 的较新 Mac 设备都会默认预装 SSH，不过 SSH 守护进程是默认禁用的。今天我们就来一起学习如何通过终端指令来开启和关闭 SSH。

**通过终端查看 SSH 远程登录是否已经开启**

想要查看 Mac 上 SSH 的当前状态？使用简单的终端就可以检查 SSH 和远程登录目前是否已经开启：

``` bash
    sudo systemsetup -getremotelogin
```

如果已经开启的话，指令会显示 “Remote Login: On” ，反之就会显示“Remote Login: Off”。

**通过终端指令开启Mac的SSH**

要快速开启 SSH 服务器并允许 SSH 连接进入当前 Mac，使用下列指令：

``` bash
    sudo systemsetup -setremotelogin on
```

输入指令后并没有任何确认信息表明远程登录和 SSH 已经开启，但你可以使用上文提到的方法来检查是否开启成功。

**通过终端指令关闭Mac的SSH**

如果你想通过终端指令禁用 SSH 服务器并阻止远程连接，输入下列指令：

``` bash
    sudo systemsetup -setremotelogin off
```

---

## Windows

Testing your SSH connection:

After you've set up your SSH key and added it to your GitHub account, you can test your connection.

1. Open Git Bash.
2. Enter the following:
	```bash
	$ ssh -T git@github.com
	# Attempts to ssh to GitHub
	```
	You may see a warning like this:
	```bash
	> The authenticity of host 'github.com (IP ADDRESS)' can't be established.
	> RSA key fingerprint is 16:27:ac:a5:76:28:2d:36:63:1b:56:4d:eb:df:a6:48.
	> Are you sure you want to continue connecting (yes/no)?
	```
	or like this:
	```bash
	> The authenticity of host 'github.com (IP ADDRESS)' can't be established.
	> RSA key fingerprint is SHA256:nThbg6kXUpJWGl7E1IGOCspRomTxdCARLviKw6E5SY8.
	> Are you sure you want to continue connecting (yes/no)?
	```
3. Verify that the fingerprint in the message you see matches one of the messages in step 2, then type `yes`:
	```bash
	> Hi username! You've successfully authenticated, but GitHub does not
	> provide shell access.
	```
4. Verify that the resulting message contains your username. If you receive a "permission denied" message, see "[Error: Permission denied (publickey)](https://help.github.com/en/articles/error-permission-denied-publickey)".

---
[reference](https://help.github.com/en/github/authenticating-to-github/testing-your-ssh-connection)

<!-- more -->
