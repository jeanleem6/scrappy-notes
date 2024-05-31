---
title: 全新安装 Mac OS Sierra (10.12)
date: 2016-11-08 14:58:25
tags: [Mac]
---

在App Store上下载系统后，做成U盘启动盘，然后把电脑格盘重新安装Sierra。
制作U盘启动盘很简单，首先要使用Mac`磁盘工具`把你的U盘或者移动硬盘进行格式化，最好用移动硬盘，速度会快点：

![磁盘工具](disk_tool.jpg)

<!-- more -->

然后打开终端，执行下面的命令就可以了:

``` bash
    sudo /Applications/Install\ macOS\ High\ Sierra.app/Contents/Resources/createinstallmedia --volume /Volumes/Sierra --applicationpath /Applications/Install\ macOS\ High\ Sierra.app
```

> 上面这个代码应该是能看懂它的意思的，如果看不懂的话，那也没有关系，你在格式化U盘的时候，一定要注意取名叫`Sierra`，然后拷贝上面的代码到终端执行就可以了。就是那么的简单，你的U盘启动盘就做好了。然后备份你电脑的资料，重启电脑，按住`option`选择U盘的盘符安装就行了。

另见[全新安装 Mac OS Capitan (10.11)](/2016/11/08/mac-os-x-capitan/)

