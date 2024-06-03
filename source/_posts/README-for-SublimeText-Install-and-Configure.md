---
title: 安装、配置 SublimeText 及其插件
date: 2024-06-03 10:19:14
description: Sublime Text 的安装、配置及插件安装说明文档。重点讲述 SublimeLinter 的安装及配置；如何在不同计算机之间正确同步配置信息及已安装的插件。
tags: [sublime]
---

Sublime Text 的安装、配置及插件安装说明文档。

## Download

**[下载地址](https://appnee.com/sublime-text-portable-full-versions/)**

## 禁用软件更新

1. 设置中添加以下配置：

   ```json
    "update_check": false,
   ```

2. `hosts` 文件(路径见下面表格)中添加以下内容

   ```cmd
   # Disable Sublime Text’s update check
   127.0.0.1    www.sublimetext.com
   127.0.0.1    license.sublimehq.com
   127.0.0.1    45.55.255.55
   127.0.0.1    45.55.41.223
   ```

   | OS      | $PATH                                   |
   | ------- | --------------------------------------- |
   | Windows | `C:\Windows\System32\drivers\etc\hosts` |
   | Mac     | `/Private/etc/hosts`                    |
   | Linux   | `/etc/hosts`                            |

## Color Scheme

```text
Mariana
```

## Theme

```text
Default Dark
```

## Sidebar / TabLabel 设置

假设您正在使用默认主题之一，您可以尝试在用户包中创建包含以下内容的 `Default.sublime-theme` 和/或 `Adaptive.sublime-theme` 文档

```json
[
    {
        "class": "sidebar_container",
        "layer0.tint": [20, 30, 40],
        "layer0.opacity": 1.0,
        "layer0.draw_center": false,
        "layer0.inner_margin": [0, 0, 1, 0],
        "content_margin": [0, 0, 1, 0]
    },
    {
        "class": "sidebar_tree",
        "row_padding": [8, 3],
        "indent": 12,
        "indent_offset": 17,
        "indent_top_level": false,
        "layer0.tint": [27, 43, 52],
        "layer0.opacity": 1.0,
        "dark_content": false
    },
    {
        "class": "sidebar_heading",
        "font.face": "Microsoft YaHei UI",
        "font.size": 13,
        "color": [178, 204, 214],
        "font.bold": true,
        "shadow_color": [35, 35, 35],
        "shadow_offset": [0, 1]
    },
    {
        "class": "sidebar_heading",
        "parents":
        [
            { "class": "tree_row", "attributes": ["selected"] }
        ],
        "shadow_color": [160, 174, 192]
    },
    {
        "class": "sidebar_label",
        "font.face": "Microsoft YaHei UI",
        "font.size": 12,
        "color": [108, 134, 146],
        "font.bold": false,
        "font.italic": false
    },
    {
        "class": "sidebar_label",
        "parents": [{"class": "tree_row", "attributes": ["selected"]}],
        "color": [0, 188, 212],
    },

    {
        "class": "sidebar_label",
        "parents": [{"class": "tree_row", "attributes": ["expandable"]}],
        "settings": ["bold_folder_labels"],
        "font.bold": true
    },

    {
        "class": "sidebar_label",
        "attributes": ["transient"],
        "font.italic": true
    },

    {
        "class": "tab_label",
        "font.face": "Microsoft YaHei UI",
        "font.size": 12,
    },
    {
        "class": "quick_panel_label",
        "font.face": "Microsoft YaHei UI",
    },
    {
        "class": "label_control",
        "font.face": "Microsoft YaHei UI",
    },
    {
        "class": "tool_tip_label_control",
        "font.face": "Microsoft YaHei UI",
    }
]
```

1. 主菜单依次点击: `Preferences` > `Browse Packages`
2. 打开 `/User` 文件夹
3. 新建 txt 文档并命名为： `Default.sublime-theme`；

   如果 Theme 选择的是默认的 `Adaptive`，txt 文档命名为：`Adaptive.sublime-theme`
4. 将上面的代码粘贴到文档中
5. 将 `font.face` 的值改为一个你系统中有的字体名称
6. 以 UTF-8 编码格式保存这个文档
7. 一切正常的话, ST 的 **Sidebar** / **TabLabel** 样式应该会立即更新

## Install Package Control

安装包管理器。

1. `Ctrl+Shift+P` 调出 `Command Palette`
2. 输入 `ipc` (Install Package Control 的首字母)
3. 选择 `Install Package Control` 开始安装
4. 完成

## 安装 `SublimeLinter` 代码检查工具

### 一、安装 `SublimeLinter`

1. `Ctrl+Shift+P` 调出 `Command Palette`
2. 输入 `install` 进入 `Package Control: Install Package`
3. 输入 `SublimeLinter`，选择 `SublimeLinter` 进行安装

### 二、安装 `SublimeLinter-contrib-htmlhint`

可以把 `sublimeLinter-contrib-htmlhint` 看成是 `SublimeLinter` 的一个插件，`sublimeLinter-contrib-htmlhint` 调用 `htmlhint` 来进行语法检查。

1. 打开 CMD 命令窗口输入命令 `npm install -g htmlhint@latest` 安装 **htmlhint**；
2. 在 Sublime 中按下 `Ctrl+Shift+P` > 输入 `pci` 安装插件 > 搜索 `SublimeLinter-contrib-htmlhint` 回车安装

### 三、安装 `jshint` 和 `csslint`

1. 打开 CMD 命令窗口安装 `jshint`、`csslint`，输入命令安装 `npm install -g jshint csslint`；
2. 在 Sublime 中按下 `Ctrl+Shift+P` 使用 `Package Control` 安装 `SublimeLinter-csslint` 和 `SublimeLinter-jshint`

### 四、安装 `SublimeLinter-contrib-markdownlint`

1. 打开 CMD 命令窗口安装 `markdownlint`，输入命令安装 `npm install -g markdownlint-cli`；
2. 在 Sublime 中按下 `Ctrl+Shift+P` 使用 `Package Control` 安装 `SublimeLinter-contrib-markdownlint`

> 其它代码检查工具请查看：[Package Control-SublimeLinter](https://packagecontrol.io/search/SublimeLinter)

### 五、配置文件

#### 配置文件名

为插件编写配置文件，四种类型的配置文件名依次为：

- `.htmlhintrc`
- `.jshintrc`
- `.csslintrc`
- `.markdownlintrc`

#### 自定义配置文件

也可以提供一个自定义的配置文件在args参数中设置，例如：

```ini
"args": ["--config", "C:\\Users\\Username\\htmlhint.conf"]
```

文件的名字可以随意定，只要内容配置 `htmlhint` 规则就可以。

#### 配置文件内容

具体的配置参数可参见github上对应项目，下面配置仅供参考：

1. **`.htmlhintrc`**

   ```json
   {
       "tagname-lowercase":true,
       "attr-lowercase":true,
       "attr-value-double-quotes":true,
       "attr-value-not-empty":true,
       "attr-no-duplication":true,
       "doctype-first":false,
       "tag-pair":true,
       "tag-self-close":true,
       "spec-char-escape":true,
       "id-unique":true,
       "src-not-empty":true,
       "title-require":false,
       /*规范类*/
       "doctype-html5":false,
       "id-class-value":false,
       "style-disabled":false,
       "inline-style-disabled":false,
       "inline-script-disabled":false,
       "space-tab-mixed-disabled":false,
       "id-class-ad-disabled":false,
       "href-abs-or-rel":false,
       "attr-unsafe-chars":false
   }
   ```

2. **`.jshintrc`**

   ```json
   {
       "curly": true,
       "eqeqeq": true,
       "forin": true,
       "freeze": true,
       // 全局变量需要手动加到配置文件的globals属性里
       "globals": {

       },
       "latedef": true,
       "maxerr": 200,
       "nonew": true,
       "shadow": "inner",
       "singleGroups": true,
       "undef": true,
       "unused": true,

       "evil": true,
       "expr": true,
       "proto": true,
       "scripturl": true,
       "sub": true,

       "browser": true,
       "devel": true,
       "jquery": true,
       "nonstandard": true,
       "typed": true,
       "worker": true
   }
   ```

3. **`.csslintrc`**

   ```json
   {
       "box-model": false,
       "adjoining-classes": false,
       "box-sizing": false,
       "compatible-vendor-prefixes": false,
       "gradients": false,
       "text-indent": false,
       "fallback-colors": false,
       "star-property-hack": false,
       "underscore-property-hack": false,
       "bulletproof-font-face": false,
       "font-faces": false,
       "import": false,
       "regex-selectors": false,
       "universal-selector": false,
       "unqualified-attributes": false,
       "overqualified-elements": false,
       "duplicate-background-images": false,
       "floats": false,
       "font-sizes": false,
       "ids": false,
       "important": false,
       "outline-none": false,
       "qualified-headings": false,
       "unique-headings": false
   }
   ```

4. **`.markdownlintrc`**

   ```json
   {
     "default": true,
     "headings": { "style": "atx" },
     "first-heading-h1": false,
     "line_length": { "line_length": 120, "tables": false },
     "whitespace": { "br_spaces": 2 },
     "ul": { "indent": 4 },
     "ol": { "style": "ordered" },
     "fenced-code-language": false,
     "blanks-around-fences": false,
     "html": {
       "allowed_elements": [
         "a",
         "details",
         "kbd",
         "p",
         "strong",
         "summary"
       ]
     }
   }
   ```

#### 1. 用户级配置

也可理解为全局配置，对所有项目有效。

1. 将四种类型的配置文件存放到目录 `D:\sublimelinter` 中，内容见[配置文件内容](#配置文件内容)
2. 依次选择 Sublime Text 的菜单：`Preferences` > `Package Settings` > `SublimeLinter` > `Settings` 打开 `SublimeLinter.sublime-settings`
3. 将以下配置拷贝到右侧用户配置文档中：

   ```json
   // SublimeLinter Settings - User
   {
      // "debug": true,
      "lint_mode": "load_save",
      "linters": {
         "csslint": {
             "disable": false,
             "args": ["--config", "D:\\sublimelinter\\.csslintrc"],
             "errors": "ids,display-property-grouping,duplicate-properties,empty-rules,errors,known-properties,vendor-prefix",
             "excludes": [],
             "ignore": "",
             "warnings": "adjoining-classes,box-model,box-sizing,compatible-vendor,duplicate-background,fallback-colors,floats,font-faces,font-sizes,gradients,import,important,outline-none,overqualified-elements,qualified-headings,regex-selectors,rules-count,shorthand,star-property,text-indent,underscore-property,unique-headings,universal-selector,zero-units"
         },
         "htmlhint": {
               "@disable": false,
               "args": ["--config", "D:\\sublimelinter\\.htmlhintrc"],
               "excludes": []
           },
           "jshint": {
               "@disable": false,
               "args": ["--config", "D:\\sublimelinter\\.jshintrc"],
               "excludes": []
           },
           "markdownlint": {
               "@disable": false,
               "args": ["--config", "D:\\sublimelinter\\.markdownlintrc"],
               "excludes": []
           }
      },
      "paths": {
           "linux": [],
           "osx": [],
           // user relative directory
           // (～ == C:/Users/Username)
           "windows": []
       },
       "show_marks_in_minimap": true,
       "styles": [
           {
               "mark_style": "squiggly_underline"
           }
       ],
   }
   ```

#### 2. 项目级配置

三个配置文件(项目级一般不需要配置 `.markdownlintrc`)需要放在工程目录的最顶层（至少应包含所有需要检测的代码文件），sublime 会自动找到这些配置文件并使其生效。

## Syncing

要在不同计算机之间正确同步已安装的插件，你不应该同步整个 `Packages/` 和 `Installed Packages/` 文件夹。

原因是某些插件针对不同的操作系统有不同的版本。通过跨操作系统同步插件的实际内容，您可能会发现这些插件已经损坏。

**正确的解决方案**是：

1. 在所有计算机上安装 **`Package Control`**

2. 然后仅同步 **`Packages/User/`** 文件夹

   此文件夹包含 `Package Control.sublime-settings` 文件(包含已安装的插件列表)，如果将此文件复制到另一台计算机，则下次启动 Sublime Text 时，`Package Control` 将安装任何缺失插件的正确版本。

> 也可以通过 Git、Dropbox 来同步，具体方法请查看[这里](https://packagecontrol.io/docs/syncing)。

## 其它插件列表

- Emmet

   ```cmd
   ul#nav>li.item$*4>a{Item $}
   ```

   输出：

   ```html
   <ul id="nav">
      <li class="item1"><a href="">Item 1</a></li>
      <li class="item2"><a href="">Item 2</a></li>
      <li class="item3"><a href="">Item 3</a></li>
      <li class="item4"><a href="">Item 4</a></li>
   </ul>
   ```

- Terminus
- MarkdownPreview
- MarkdownEditing
- JavaScript Completions
- JsFormat
- JsPrettier
- CSS3
- CSScomb
- CSS Format
- Alignment
- ConvertToUTF8

  转UTF-8快捷键设置:
  进入目录 `/Packages/ConvertToUTF8/` 下找到对应操作系统的 `Default.sublime-keymap` 文件，设置快捷键

  ```json
  // Windows
  [
      { "keys": ["ctrl+shift+c"], "command": "convert_to_utf8", "args": {"encoding": "GBK", "stamp": "0" } },
      { "keys": ["ctrl+shift+g"], "command": "convert_to_utf8", "args": {"encoding": "UTF-8", "stamp": "0" } }
  ]

  // Mac
  [
      { "keys": ["super+shift+c"], "command": "convert_to_utf8", "args": {"encoding": "GBK", "stamp": "0" } },
      { "keys": ["super+shift+g"], "command": "convert_to_utf8", "args": {"encoding": "UTF-8", "stamp": "0" } }
  ]
  ```

- HTML-CSS-JS Prettify

  配置node.js路径:

  1. 依次点击菜单：`Preferences` > `Package Settings` > `HTML-CSS-JS Prettify` > `Plugin Options - Default`
  2. 修改 Windows 的 `node.exe` 路径

   ```json
   {
      "node_path":
       {
           "windows": "C:/nvm/nodejs/node.exe" // 设置为 node.exe的实际路径
       },

   }
   ```

- A File Icon
- AutoFileName
- ColorHelper
- Vue Syntax Highlight
- LSP-vue
