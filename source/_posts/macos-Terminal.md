---
title: MAC 终端(Terminal)命令入门
date: 2016-08-05 10:41:36
tags: [Mac,server]
---

> Mac常用*终端*(Terminal)命令，帮助我们更好地使用Mac(Let's Rock.&.&.)

## 访问目录

``` bash
    pwd　　　　　　#显示当前工作目录路径
    cd         　　#进root
    ~         　 　#进root
    cd ~　　　　　　#返回root
    cd FolderName　　#进入文件夹
    cd ..　　　　　　#上级目录
    cd -　　　　　　#返回上一个访问的目录
```

<!-- more -->

## 设置权限

``` bash
    chmod -R 0777 /usr/local/mysql/var/dedeadmin/  #设置目录权限为0777
```

## 查看文件

``` bash
    cat FileName　　#在终端里面直接显示文件内容
    cat FileName|less　　#用less编辑器显示文件内容，输入:q退出编辑器
    ls　　#列出目录下所有文件
```

## 拷贝文件

``` bash
    cp 文件名 目标目录　　#将文件拷贝到目标目录下
```

## 合并多个文件夹

``` bash
    mv ../*/* ./ #将多个文件夹下的文档合并到一个文件夹下
```

> **解释：**文件夹A下有a1/a2/a3子文件夹，每个子文件夹下有若干文件，则在A下面建文件夹b，进入b，调出terminal，执行 `mv ../*/* ./`（注意最后的 `./`） ，就会把所有a1-3的子文件移动到b里面。
> **需要注意的是，如果文档太多会合并失败并报错：`argument list too long: mv`，可以分多次合并（文档数量6000左右没有问题）**

## 合并多个文件内容

``` bash
    cat *.html > new.txt #将指定目录下所有html文件的内容合并到文本文档new.txt中
```

## 切割文件

`split [-a] [-b] [-C] [-l] [要分割的文件名] [分割后的文件名前缀]`

- `–version` 显示版本信息
- `-l` 指定每多少行切割一次，用于文本文件分割
- `-b` 指定切割文件大小,单位 m 或 k
- `-C` 与-b类似，但尽量维持每行完整性
- `-d` 使用数字而不是字母作为后缀名
- `-a` 指定后缀名的长度，默认为2位

``` bash
    split -l line_count file newFiles_prefix #指定每多少行切割一次
    split -b byte_count file newFiles_prefix #指定切割文件大小,单位 m 或 k

    #eg:
    split -a 4 -l 100000 dict.txt dict_ #每十万行切割一次，后缀为4位数的字母
    split -a 4 -b 100m dict.txt dict_ #每 100MB 切割一次，后缀为4位数的字母
```

**为分割后的文件批量添加后缀**

``` bash
#以添加 html 后缀为例
for i in *; do mv "$i" "$i.html"; done

#修改后缀名(以修改.html 为 .json 为例)
for i in *.html; do mv "$i" "${i%.html}.json"; done
```

> ### Attention: For OS X
> OS X 的 `split` 不支持 `-d` 参数。可以安装 **GNU core utilities** (including split)，不过`split` 命令需要加一个前缀即：`gsplit`。
>**安装：**
> ``` bash
 brew install coreutils
 ```
> **使用：**
> ```
gsplit -a 4 -d -l 100000 dict.txt dict_ #每十万行切割一次，后缀为4位数的数字
gsplit -a 4 -d -b 100m dict.txt dict_ #每 100MB 切割一次，后缀为4位数的数字
```

## sort 排序

**sort命令**是在Linux里非常有用，它将文件进行排序，并将排序结果标准输出。sort命令既可以从特定的文件，也可以从stdin中获取输入。

- 语法：
``` bash
sort(选项)(参数)
```

- 选项：
``` bash
-b：忽略每行前面开始出的空格字符；
-c：检查文件是否已经按照顺序排序；
-d：排序时，处理英文字母、数字及空格字符外，忽略其他的字符；
-f：排序时，将小写字母视为大写字母；
-i：排序时，除了040至176之间的ASCII字符外，忽略其他的字符；
-m：将几个排序号的文件进行合并；
-M：将前面3个字母依照月份的缩写进行排序；
-n：依照数值的大小排序；
-o<输出文件>：将排序后的结果存入制定的文件；
-r：以相反的顺序来排序；
-t<分隔字符>：指定排序时所用的栏位分隔字符；
+<起始栏位>-<结束栏位>：以指定的栏位来排序，范围由起始栏位到结束栏位的前一栏位。
```

- 参数：
文件：指定待排序的文件列表。

- 实例：
sort将文件/文本的每一行作为一个单位，相互比较，比较原则是从首字符向后，依次按[ASCII码值](http://zh.wikipedia.org/zh/ASCII)进行比较，最后将他们按升序输出。[【更多实例】](http://man.linuxde.net/sort)
``` bash
sort -o sort.txt unsort.txt  #对【unsort.txt】中的内容进行排序并输出到【sort.txt】文档
```

## 新建文件（夹）

``` bash
    mkdiv 文件夹名　　　　　#新建文件夹
    touch 文件名　　　　　　#新建文件
```

## 删除文件（夹）

``` bash
    rm FileName  #删除文件
```

<!--  -->

``` bash
    rm -Rf FolderName  #循环删除文件夹及文件夹下的所有文件
```

> `-R`: recursive<循环的>
> `f`: force<强制>，避免可能引起的程序或系统错误，可以去掉该参数

## 进程操作

``` bash
    ps -ax　　　　　　#查看所有进程
    ps -ax | grep <application name>　　#带正则查询进程
    kill PID　　　　　#通过进程ID关闭进程
    killall <application name>　　#通过进程名关闭进程
```

## 向文件写入内容

``` bash
    echo "text sth." >> filename　　#如果文件不存在新建文件写入双引号中的内容（>>表示在现有内容下一行写入）
    echo "text sth." > filename　　#写入双引号中的内容（>表示抹掉原来的内容写入新的内容）

    echo -e "\ntext sth." >> filename　　#写入双引号中的内容（双引号中的\n表示换行）

    echo "" >> filename
    echo "text sth." >> filename　　#与上面代码的功能相同

    echo ""; echo "text sth." >> filename　　#与上面代码的功能相同
```

> Mac OS中以`.`开头的文件会被系统自动隐藏，如：`.zshrc`、`.aliase` 这类文件默认是隐藏的。

## 显示隐藏文件

``` bash
    defaults write com.apple.finder AppleShowAllFiles -boolean true ; killall Finder
```

## 恢复隐藏

``` bash
    defaults write com.apple.finder AppleShowAllFiles -boolean false ; killall Finder
```

## 查看文件大小分布

``` bash
du -sh *   # 查看根目录下，所有文件的大小分布

#### 查看Library目录下，所有文件的大小分布
cd ~/Library
ls
du -d 1 -h
#### 其它文件夹知道怎么操作了吧……^o^
```

## 安装任何来源的软件

`Terminal` 中输入如下代码：

``` shell
sudo spctl --master-disable
```
