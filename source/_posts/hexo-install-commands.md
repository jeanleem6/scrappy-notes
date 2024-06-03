---
title: Hexo 安装及常用命令
date: 2016-08-09 16:01:37
tags: [hexo]
---

## Hexo Installation

安装前提，先检查是否安装下列应用程序：

- Xcode
- Node.js
- Git

### 安装 Xcode

请先到 App Store 安装 Xcode，Xcode 完成后，可通过两种方式安装 **Xcode中Command Line Tools**：

- 启动 Xcode 并进入 **Preferences -> Download -> Command Line Tools -> Install** 安装命令行工具。
- 命令行安装

```
xcode-select --install
```

<!-- more -->

### 安装 Node.js

安装 Node.js 的最佳方式是使用 nvm。

cURL:

``` bash
$ curl https://raw.githubusercontent.com/creationix/nvm/master/install.sh | sh
# nvm 安装好之后，重启 Terminal，输入如下命令安装 Node.js
$ nvm install stable
```

### 安装 Git

``` bash
brew install git
```

### 安装 Hexo
``` bash
$ sudo npm install -g hexo-cli
$ hexo init blog
$ cd blog
$ npm install
```

### 安装插件

- `hexo-browsersync` - 浏览器实时、快速响应文件更改

  ``` bash
    yarn add hexo-browsersync hexo-asset-image --save
  ```

- `hexo-asset-image` - 图片资源插件，可以这样添加图片 `![](image.jpg)`，图像将自动解析为其相应帖子的路径

  ```bash
  yarn add https://github.com/xcodebuild/hexo-asset-image.git
  ```

  安装之后，配置根目录下的 `_config.yml` 文档以启用该功能：

  ```yaml
  post_asset_folder: true
  ```

  > **注意：**不建议用以下命令安装该插件，用这个 NPM 包图片路径会有问题
  >
  > ```bash
  > yarn add hexo-asset-image
  >```
  >
  > 如果确实要这样安装，修改文件 `node_modules/hexo-asset-image/index.js` 的第 24 行：
  >
  > ```javascript
  > var endPos = link.lastIndexOf('.');
  > // 改为：
  > var endPos = link.length-1;
  > ```

---

## 建立 SSH key

SSH key 可以让你在你的电脑和 Git 之间建立安全的加密连接

- 创建 SSH key

    ``` bash
        ssh-keygen -t rsa -C "example@gmail.com"
    ```
- 查看你的 public key

    ``` bash
        cat ~/.ssh/id_rsa.pub
    ```

- 添加到 SSH keys 中 <https://github.com/settings/ssh>

> 如果不能建立连接，[检查SSH是否开启][links-1]

[links-1]: /2016/11/14/ssh-on-and-off-in-Terminal/

---

## Hexo Commands

Hexo 约有二十个命令，但普通用户经常使用的大概只有下列几个:

### hexo s

``` bash
    hexo s
```

启动本地服务器，用于预览主题。默认地址： http://localhost:4000/
`hexo s` 是 `hexo server` 的缩写，命令效果一致；
预览的同时可以修改文章内容或主题代码，保存后刷新页面即可；
对 Hexo 根目录 **_config.yml** 的修改，需要重启本地服务器后才能预览效果。


### hexo n

``` bash
    hexo n "学习笔记  六"
```

新建一篇标题为 学习笔记 六 的文章，因为标题里有空格，所以加上了引号。
文章标题可以在对应 md 文件里改，新建时标题可以写的简单些；
`hexo n` 是 `hexo new` 的缩写，命令效果一致。

### hexo d

``` bash
    hexo d
```

自动生成网站静态文件，并部署到设定的仓库。
`hexo d` 是 `hexo deploy` 的缩写，命令效果一致。

该命令需安装插件： **hexo-deployer-git**

``` bash
    npm install hexo-deployer-git --save
```

### hexo clean

``` bash
    hexo clean
```

清除缓存文件 `db.json` 和已生成的静态文件 `public。`
网站显示异常时可以执行这条命令试试。

### hexo g

``` bash
    hexo g
```

生成网站静态文件到默认设置的 `public` 文件夹。
便于查看网站生成的静态文件或者手动部署网站；
如果使用自动部署，不需要先执行该命令；
`hexo g` 是 `hexo generate` 的缩写，命令效果一致。

### hexo n page

``` bash
    hexo n page aboutme
```

新建一个标题为 `aboutme` 的页面，默认链接地址为 `主页地址/aboutme/`
标题可以为中文，但一般习惯用英文；
页面标题和文章一样可以随意修改；
页面不会出现在首页文章列表和归档中，也不支持设置分类和标签。

### 常用组合

``` bash
    # hexo 新版本没有组合用法
    hexo clean && hexo s
    hexo clean && hexo d
    hexo d -g  // 部署并发布
```

可以用输入法等软件为这些命令设置快捷键，方便调用。

### 相关说明

以上命令使用基于 Hexo 3.1.1 版本；
需要删掉用命令新建的文章或页面时，只需要进入 Hexo 根目录下的 `source` 文件夹，删除对应文件或文件夹即可；
更多命令用法请查询 [官方文档](https://hexo.io/zh-cn/docs/commands.html)。

## 文档备份

只需要备份如下文件夹及文件即可：

```ini
#有[]表示文件夹，其它为文件

---- [source] #所有的 markdown 原始文件和目录「重要」
---- [themes] #hexo 的主题，(仅需备份其配置文件 _config.yml)
---- package.json #搭建hexo，安装依赖包时需要「重要」
---- _config.yml #配置文件「重要」
---- readme.md
```

## ~~even 主题一处样式问题~~

> `(even 新版本已无此问题)`

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
