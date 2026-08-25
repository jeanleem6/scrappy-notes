# scrappy-notes

Cedric 的 Hexo 博客源码，使用 [hexo-theme-even](https://github.com/ahonn/hexo-theme-even) 主题，部署到 [cedriclee85.github.io](https://cedriclee85.github.io)。

## 环境要求

- Node.js 20.19+（Hexo 8 要求）
- Git
- yarn

## 本地安装

```shell
npm install hexo-cli -g # 可选：全局 CLI（用 npm 装）；不装则用 yarn 脚本或 yarn hexo <命令>
git clone git@github.com:cedriclee85/scrappy-notes.git # clone 本 blog
cd scrappy-notes # 进入 blog 目录
yarn # 安装依赖
```

## 主题 even

主题 [hexo-theme-even](https://github.com/ahonn/hexo-theme-even) 已整体入库在 `themes/even/`（基于上游 `991ce19`，含本站定制：`_config.yml`、`source/favicon.ico`、`layout/_partial/footer.ejs`、`source/css/_partial/_post/_content.scss`），clone 本仓库后无需另行安装。

> 主题所需的渲染器 `hexo-renderer-dartsass`、`hexo-renderer-ejs` 已在 `package.json` 中声明，`yarn` 安装时会一并装好。

## 常用命令

| 操作                                | hexo 命令                   | 缩写     | yarn 脚本     |
| ----------------------------------- | --------------------------- | -------- | ------------- |
| 本地预览（<http://localhost:4000>） | `hexo server`               | `hexo s` | `yarn server` |
| 新建文章                            | `hexo new [layout] <title>` | `hexo n` | —             |
| 生成静态文件（输出到 `public/`）    | `hexo generate`             | `hexo g` | `yarn build`  |
| 部署网站                            | `hexo deploy`               | `hexo d` | `yarn deploy` |
| 清除缓存与已生成文件                | `hexo clean`                | —        | `yarn clean`  |
| 列出网站数据                        | `hexo list <type>`          | `hexo l` | —             |
| 查看/修改配置                       | `hexo config [key] [value]` | —        | —             |

> 未全局安装 hexo-cli 时，上表 `hexo` 命令可写成 `yarn hexo <命令>`（走项目本地依赖），如 `yarn hexo new xxx`。
>
> 完整指令文档：<https://hexo.io/zh-cn/docs/commands>

## 写作

```shell
hexo new <title> # 使用 _config.yml 中 default_layout 指定的布局（post）
hexo new [layout] <title> # layout 对应 scaffolds/ 下的文件名；标题含空格时用引号括起来
```

已开启 `post_asset_folder`，新建文章会自动生成同名文件夹，用于存放该文章的图片等资源。

### 添加图片

```markdown
<!-- alt 和 title 可以不填 -->
![image alt](image-name.png 'image title')

<!-- 带链接的图片：将图片的 Markdown 括在方括号中 -->
[![image alt](image-name.png "image title")](https://markdown.com.cn)
```

> **注意：**
>
> 1. 图片需要存放到以该 markdown 文件名命名的文件夹中
> 2. 图片不需要写路径，`hexo-renderer-marked` 的 `postAsset` 选项会自动为文章资源目录内的图片补全路径

## 部署

`hexo d` 通过 `hexo-deployer-git` 将 `public/` 推送到 `cedriclee85/cedriclee85.github.io` 的 `master` 分支（见 `_config.yml` 的 `deploy` 配置）。

发布前建议完整跑一遍（逐行执行）：

```shell
yarn clean # 清缓存
yarn build # 生成静态文件
yarn deploy # 部署
```
