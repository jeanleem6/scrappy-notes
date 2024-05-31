---
title: 全新安装 Mac OS Capitan (10.11)
date: 2016-11-08 14:07:19
tags: [Mac]
---

## 一、准备工作：

1. 准备一个8GB或以上容量的U盘

2. 打开App store下载OS X El Capitan系统

3. 下载完成后, 打开 Launchpad

4. 找到刚才下载的OS X El Capitan

    ![udisk-00](udisk_img_00.png)

<!-- more -->

> 如果是从其它途径下载的安装包，需要先双击安装并拖到Applications中
> 然后再到 Launchpad 中找到OS X El Capitan


## 二、格式化优盘

1. 插入 U 盘，然后在「应用程序」->「实用工具」里面找到并打开「磁盘工具」

2. 在左侧列表中找到 `外置` -> U盘的名称 并点击

3. 右边顶部选择 `抹掉` 并且在 `名称` 输入 `Capitan`，开始格式化 (抹掉U盘)
    由于后面的命令中会用到此名称，如果你要修改为其它名称(英文)，请务必对应修改后面的命令, (如果不清楚、请按照我的步骤来，包你不会碰壁！）

    ![udisk-02](udisk_img_02.jpg)

## 三、输入终端命令开始制作启动盘

1. 请再次确保名为 “安装 OS X El Capitan” 的文件是保存在 `应用程序` 的目录中

2. 在`应用程序`->`实用工具`里面找到`终端`并打开, 也可以直接通过 Spotlight 搜索`终端`打开

3. 复制下面的命令，并粘贴到`终端`里，按回车运行! (指令有点长！请复制完全哦~)

	``` bash
	    sudo /Applications/Install\ OS\ X\ El\ Capitan.app/Contents/Resources/createinstallmedia --volume /Volumes/Capitan --applicationpath /Applications/Install\ OS\ X\ El\ Capitan.app --nointeraction
	```
    > 命令说明：
    > `Install\ OS\ X\ El\ Capitan.app` 这个是正式版的“安装 `OS X El Capitan`
    > `Capitan` 这个是`U盘`的名字 `终端`上的如果有空格需要加上` \(空格)`

4. 回车之后，系统会提示你输入电脑的管理员密码 (如果没有设置密码直接再按一次回车)

    > 终端显示是这样的: password (后面输入的密码是不显示的哦~输入完成后直接回车)

5. 接下来就是等待系统开始制作启动盘了。
    这时，命令执行中你会陆续`陆续`陆续看到类似以下的信息：

	``` bash
        Erasing Disk: 0%... 10%... 20%... 30%...100%...
        Copying installer files to disk...
        Copy complete.
        Making disk bootable...
        Copying boot files...
        Copy complete.
        Done.
	```
    当你看到最后有 Copy complete 和Done 字样出现就是表示启动盘已经制作完成了!!!

6. 当你制作完成的 `OS X El Capitan` 启动盘之后,
    桌面出现 `Install OS X El Capitan` 的盘符那么就表示启动盘是正常的了。

## U 盘启动安装 OS X El Capitan 的方法

1. 那么怎样通过 `USB` 启动进行全新的系统安装呢？
    其实很简单，先在目标电脑上插上 `U盘`，然后重启你的 `Mac`
    然后一直按住键盘`option 或者是 (alt)` 按键不放，直到屏幕显示多出一个 `USB` 启动盘的选项，如下图所示

    ![udisk-05](udisk_img_05.jpg)

2. 这时，你可以直接覆盖安装系统(升级)，也可以在磁盘工具里面格式化抹掉整个硬盘，
    或者重新分区等实现全新的干净的安装。

3. 选择磁盘工具.....

4. 选择电脑`内置`磁盘，右侧选择`抹掉`，磁盘名称 `Macintosh HD`，格式 `OS X 扩展 （日志式）`

5. 选择安装 OS X

6. 继续 > 同意 > 同意

7. 选择电脑内置磁盘进行安装.....

    开始安装了....来杯茶🍵等待....
    最后一分钟的时候....超级慢的.... 请耐心等待!!!

另见[全新安装 Mac OS Sierra (10.12)](/2016/11/08/mac-os-x-sierra/)
