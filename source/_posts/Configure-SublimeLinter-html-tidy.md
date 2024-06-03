---
title: Configure SublimeLinter-html-tidy
date: 2019-08-11 16:47:19
description: 为 sublime 配置 html 格式检查工具：tidy
tags: [sublime]
---

### Ready Works

1. Install [Sublime Text 3](https://www.sublimetext.com/3)
2. Install *SublimeLinter*
3. [Download tidy.zip](https://tidybatchfiles.info/tidy.zip) from [HTML Tidy for Windows](https://tidybatchfiles.info/)
4. Install *SublimeLinter HTML Tidy*

Step 2 and 4 install from `Package Control: Install Package`. Not introduce here.

### Configure

- 解压第3步下载的文件得到 `tidy.exe`，拷贝到目录`C:/Users/Username/tidy`，其它目录也可以。
- 依次打开：`Preferences > Package Settings > SublimeLinter > Settings`
- 下滑找到 `paths` 节点，如下：

  ```json
  {
      "paths": {
          "linux": [],
          "osx": [],
          "windows": []
      }
  }
  ```

- 拷贝 `tidy.exe` 所在的目录到 `windows` 项：

  ```json
    {
      "paths": {
          "linux": [],
          "osx": [],
          "windows": ["~/tidy"]
      },
    }
    ```

    > 注意：路径 `"~/tidy"` 是相对用户目录的路径，即 `C:/Users/Username`，路径不包含 `tidy.exe` 程序本身。当然，用**绝对路径**或**其它目录**也是可以的（如：`d:/tidy`）。

- Done!!

---

[阅读原文](https://jecosolutions.com/linting-html-with-sublime-text-3-sublimelinter-html-tidy-for-windows-and-sublimelinter-html-tidy-on-windows/)
