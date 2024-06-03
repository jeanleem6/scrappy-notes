---
title: Mac中安装配置Python2、Python3及自由切换
date: 2019-03-03 10:47:49
description: Mac系统已经默认带有Python2.7了，所以无需安装它。用 brew 安装 python3
tags: [python]
---

## 安装Python2

Mac系统已经默认带有Python2.7了，所以无需安装它。

``` bash
which python
# 输出如下：
# /usr/bin/python
```

## 安装Python3

``` bash
# 安装 python3
brew install python3

which python3
# 输出如下：
# /usr/local/bin/python3
```

## 不同版本Python路径

``` bash
/System/Library/Frameworks/Python.framework/Versions/2.7  # 系统默认
/usr/local/Cellar/python  # brew安装
```

## 配置Python2 和Python3

1. 指定对应路径，控制台输入：`vi ~/.zshrc`

   按一下键盘 `I` 键，变成可编辑状态后，在末尾加上如下内容：

   ``` bash
   # Setting PATH for Python 2.7
   PATH="/System/Library/Frameworks/Python.framework/Versions/2.7/bin:${PATH}"
   export PATH
   # Setting PATH for Python 3.7.2_2(修改为实际安装的版本号，下同)
   PATH="/usr/local/Cellar/python/3.7.2_2/bin:${PATH}"
   ```

   编辑完后，按 `esc` 退出编辑状态，然后输入 `:wq` 并回车，这样就保存了所修改的 `~/.zshrc` 文件

2. 添加alias（zsh 环境可以省略这一步），控制台输入：`vi ~/.zshrc`

   ``` bash
   alias python2='/System/Library/Frameworks/Python.framework/Versions/2.7/bin/python2.7'
   alias python3='/usr/local/Cellar/python/3.7.2_2/bin/python3.7'
   # alias python=python3
   ```

3. 上述步骤的修改，虽然保存了，但是系统还没让其生效，所以我们需要source一下。控制台输入：`source ~/.zshrc`  然后按回车键。最后关闭终端，重新打开，即生效。
4. 输入对应的命令，即可自由选择使用对应的Python版本。

   ``` bash
   $ python # (或者 python2)，进入python2 环境
   Python 2.7.10 (default, Oct  6 2017, 22:29:07)
   [GCC 4.2.1 Compatible Apple LLVM 9.0.0 (clang-900.0.31)] on darwin
   Type "help", "copyright", "credits" or "license" for more information.
   >>>
   ```

   ``` bash
   $ python3 # 进入python3 环境
   Python 3.7.2 (default, Feb 12 2019, 08:16:38)
   [Clang 10.0.0 (clang-1000.11.45.5)] on darwin
   Type "help", "copyright", "credits" or "license" for more information.
   >>>
   ```

5. 退出Python控制台

   ``` python
   # 方法 1：
   quit()

   # 方法 2：
   exit()

   # 方法 3：
   ctrl + D
   ```
