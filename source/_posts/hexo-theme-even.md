---
title: Hexo-Theme-Even
date: 2016-08-10 10:45:37
tags: [hexo]
---

A simple theme for Hexo blog framework

![even](hexo-theme-even.png)

<!-- more -->

## Demo
Check out Even theme in live : [demo](http://www.ahonn.me)

## Document
- [中文文档](https://github.com/ahonn/hexo-theme-even/wiki)
- [Document](https://github.com/ahonn/hexo-theme-even/wiki)

## Installation

```shell
$ npm install hexo-renderer-ejs hexo-renderer-dartsass --save
$ git clone https://github.com/ahonn/hexo-theme-even themes/even
$ cp themes/even/_config.yml.example themes/even/_config.yml
```

Then update your blog's **_config.yml**(yourblog/_config.yml) to use the theme.

``` yaml
# Extensions
## Plugins: http://hexo.io/plugins/
## Themes: http://hexo.io/themes/
theme: even
```

For more options, check out the [document](https://github.com/ahonn/hexo-theme-even/wiki)

## Update

You can update to latest master branch by the following command:

```shell
$ cd themes/even
$ git pull
```

## 首页文章展现方式

首页默认会展示文章全文。也可以通过以下两种不同的形式在首页展示文章。

### 文章截断

在文章内容中添加 `<!-- more -->` 即可在首页显示时只显示其之上的内容。

并且会在 `<!-- more -->` 添加一个 Read more 的链接。

### 自定义文章简述

可在文章头信息中添加 **description** 字段，并填写自定义的文章简述。

就可以在首页显示文章简述而不显示文章内容。

## 一处样式问题

Hexo 会将无序列表项 (即：`ul li`) 的内容解析并放置于 `<p>` 标签内，even 主题默认情况对这种结构的处理有一点问题，无序列表的 `::marker` 和 `<p>` 标签会分行显示，解决方法如下：

```css
/* 修改文件：themes/even/source/css/_partial/_post/_content.scss */
ul {
  margin-left: 1em;   /* 增加行 */
  padding-left: 0;
  list-style: inside; /* 删除行 */

  li {
    input[type="checkbox"] {
      margin-right: 5px;
    }
  }
}
```
