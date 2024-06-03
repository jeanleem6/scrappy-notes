---
title: epub电子书制作杂录
date: 2018-11-05 17:30:46
description: 简要介绍如何制作 epub 文档
tags: [epub]
---

> 工具准备：[Calibre](https://calibre-ebook.com/)，Calibre 中文轉換插件 [TradSimpChinese](https://github.com/Hopkins1/TradSimpChinese)

## *编辑书籍/Edit Book* 简介

打开 Calibre，软件右上角工具栏中即可找到*编辑书籍/Edit Book*

- 左侧：文件浏览，双击任何一个文件可在中间区域查看文件源码或图片
- 右侧：文件预览区，查看html页面预览效果

## 让 ibooks 支持内置字体

第一步，修改 content.opf 文件，新增一行：`<meta property="ibooks:specified-fonts">true</meta>`

第二步，创建xml文件: `com.apple.ibooks.display-options.xml`，内容如下：

```xml
<display_options>
    <platform name="*"> <!-- allowed values for platform "iphone", "ipad", or "*" for all -->
        <option name="specified-fonts">true</option> <!-- must be set to "true" for embedded fonts -->
    </platform>
</display_options>
```

第三步，点击 calibre 中的 *编辑书籍/Edit Book* 打开 *Edit Book* 工具，点击 *新增文件/New File*：

- 在弹窗中输入 `meta-inf/com.apple.ibooks.display-options.xml`
- 点击 *导入文件(图片/字体等)/Import resource file*，定位到第二步创建的xml文件选择打开，点 *确定* 后xml文件就添加好了。

第四步，点击 *工具栏* 中的 *管理字体(TTF)* > *安装字体*，添加字体后可通过重命名更改字体路径：`Fonts/FontName.ttf`

第五步，在样式表中添加内置字体：

```css
@font-face {
  font-family: "FontName"; /* FontName 可设定为任意名字 */
  src: url(../Path/FontName.ttf); /* 注意将 Path 和 FontName 修改为你创建的路径名和字体名称 */
}
```

## 竖排，从右向左翻页

第一步，修改 content.opf 文件，新增一行：`<meta content="vertical-rl" name="primary-writing-mode"/>`

第二步，修改 content.opf 文件， 给 spine 标签增加一属性：`page-progression-direction="rtl"`

第三步，修改样式表，为 body 增加一属性： `writing-mode: vertical-rl`;

> 有时需要**局部横排**显示，例如图片的说明文字可以横排显示在图片下方，可为说明文字单独设置css：writing-mode: horizontal-tb

## 添加弹注效果

![footnote](flowing_footnote.png)

```html
<html xmlns="http://www.w3.org/1999/xhtml" xmlns:epub="http://www.idpf.org/2007/ops">
...
<p>
    <a href="chapter.xhtml#myNote" epub:type="noteref">1</a>
</p>
<aside id="myNote" epub:type="footnote">Text in popup</aside>
```

> 注意，必须有这几个属性：
>
> - html 标签: `xmlns:epub="http://www.idpf.org/2007/ops"`
> - a (注释序号)：`epub:type="noteref"`
> - aside (注释)：`epub:type="footnote"`
>
> aside 标签会自动隐藏，如果希望注释正常显示出来，可用 `div` / `p` 等标签替代。
> ios 中为整屏弹注，多看等其它阅读器不支持这种方式。

## 繁体标点替换

- `“` 替换成 `「`
- `”` 替换成 `」`
- `‘` 替换成 `『`
- `’` 替换成 `』`

## 修改语言

```xml
<dc:language>zh-Hans</dc:language>
```

- **繁体**：`zh-Hant`
- 大陆繁体：`zh-Hant-CN`
- 香港繁体：`zh-Hant-HK`
- 澳门繁体：`zh-Hant-MO`
- 新加坡繁体：`zh-Hant-SG`
- 台湾繁体：`zh-Hant-TW`
- **简体**：`zh-Hans`
- 大陆简体：`zh-Hans-CN`
- 香港简体：`zh-Hans-HK`
- 澳门简体：`zh-Hans-MO`
- 新加坡简体：`zh-Hans-SG`
- 台湾简体：`zh-Hans-TW`

## body 样式设置参考

```css
body {
    margin: 5%;
    text-align: justify;
    writing-mode: vertical-rl;
    -webkit-writing-mode:vertical-rl;
    -epub-writing-mode: vertical-rl;
    -epub-line-break: auto;
}
```

## epub目录树结构

```text
├── META-INF
│   ├── com.apple.ibooks.display-options.xml
│   └── container.xml
├── OEBPS
│   ├── Fonts
│   │   └── kangxidict.ttf
│   ├── Images
│   │   ├── Image00000.jpg
│   │   ├── Image00001.jpg
│   │   ├── ...
│   │   └── Image00200.jpg
│   ├── OEBPS
│   │   └── cover.jpg
│   ├── Styles
│   │   ├── flow0001.css
│   │   ├── flow0002.css
│   │   ├── ...
│   │   └── flow0005.css
│   ├── Text
│   │   ├── text00000.html
│   │   ├── text00001.html
│   │   ├── ...
│   │   └── text00090.html
│   ├── content.opf
│   └── toc.ncx
└── mimetype
```

---
reference:
[Custom Fonts](http://guidohenkel.com/2015/04/custom-fonts-in-ibooks/)
[Pop-up Footnotes](https://help.apple.com/itc/booksassetguide/en.lproj/static.html)（Section: **Pop-up Footnotes**）
[如何把 Kindle 电子书的横排文字改成竖排](https://bookfere.com/post/204.html)
