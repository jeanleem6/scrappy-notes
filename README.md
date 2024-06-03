# scrappy-notes

Scrappy notes

## 安装 Hexo

```shell
npm install hexo-cli -g
```

> 官网： https://hexo.io/zh-cn/

## 安装 scrappy-notes

```shell
cd E:/gitRepo # 进入 Blog 存放目录
git clone git@github.com:jeanleem6/scrappy-notes.git # clone 本 blog
cd scrappy-notes # 进入 blog 目录
yarn # 安装 packages
```

## 安装 hexo-theme-even

```shell
# 检查 package.json 中是否有 hexo-renderer-ejs，如果没有在这里一并安装
yarn add hexo-renderer-dartsass hexo-renderer-ejs
git clone https://github.com/ahonn/hexo-theme-even themes/even
cp themes/even/_config.yml.example themes/even/_config.yml
```

将 `themes/_bak_for_theme_even` 文件夹下的文件拷贝到 `themes/even/` 目录中**替换**

> hexo-theme-even Git Repository：https://github.com/ahonn/hexo-theme-even

## 运行 Hexo - server

```shell
hexo s
# or
hexo server
```

## 新建文章 - new

新建一篇文章。如果没有设置 layout 的话，默认使用 `_config.yml` 中的 `default_layout` 参数代替。如果标题包含空格的话，请使用引号括起来。

```shell
hexo n <title>
# or
hexo new <title>
#or
hexo n [layout] <title> # [layout] 调用的是 scaffolds/ 中的文件，写文件名即可
#or
hexo new [layout] <title>
```

## 生成静态文件 - generate

静态文件默认保存位置为 `public` 文件夹

```shell
hexo g
# or
hexo generate
```

## 部署网站 - deploy

```shell
hexo d
# or
hexo deploy
```

以这种命令行方式创建 `markdown` 文件，会自动生成一个文件夹(*文件夹名称为该文件名*)，用于存放其图片等资源文件。

## 添加图片

```markdown
<!-- alt 和 title 可以不填 -->
![image alt](image-name.png 'image title')

<!-- 添加链接的图片，将图像的Markdown 括在方括号中 -->
[![image alt](image-name.png "image title")](https://markdown.com.cn)
```

> **注意：**
>
> 1. 图片需要存放到以该 markdown 文件名命名的文件夹中
> 2. 这里的图片不需要添加路径，插件 `hexo-asset-image` 会自动为所有图片添加路径

## 清除缓存文件 - clean

```shell
hexo c
# or
hexo clean
```

## 列出网站数据 - list

```shell
hexo l <type> # Available types: page, post, route, tag, category
# or
hexo list <type>
```

## 显示 Hexo 版本 - version

```shell
hexo v
# or
hexo version
```

## 列出网站的配置 - config

列出网站的配置（`_config.yml`）。

如果指定了 `key`，则只展示配置中对应 `key` 的值；

如果同时指定了 `key` 和 `value`，则将配置中对应的 `key` 的值修改为 `value`。

```shell
hexo c [key] [value]
# or
hexo config [key] [value]
```

---

## Hexo 指令

https://hexo.io/zh-cn/docs/commands
