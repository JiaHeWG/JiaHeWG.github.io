# BillZH的小站

个人博客，记录一些技术笔记和折腾记录。

## 技术栈

- [Hugo](https://gohugo.io/)（extended 版）
- [Hugo Theme Stack](https://github.com/CaiJimmy/hugo-theme-stack) v4，使用[hugo-theme-stack-starter](https://github.com/CaiJimmy/hugo-theme-stack-starter)快速构建

## 本地开发

需要先安装 Git、Go 和 Hugo extended，并通过git clone拉取项目，具体内容参见[Stack官方文档](https://stack.cai.im/zh/guide/getting-started).

```bash
# 拉取依赖
hugo mod tidy

# 启动本地服务
hugo server
```

访问 http://localhost:1313 预览（端口号请根据hugo配置定义实际改动）。

## 构建

```bash
hugo --minify
```
## 更新主题

```bash
hugo mod get -u github.com/CaiJimmy/hugo-theme-stack/v4
hugo mod tidy
```

## 部署

推送到 `main` 分支后，GitHub Actions 自动构建并部署到 GitHub Pages。

## 目录结构

```text
.
├── config/_default/     # 站点配置
├── content/             # 文章与页面
│   ├── post/            # 博客文章
│   ├── links/           # 友链
│   └── ...
├── layouts/             # 覆盖主题的模板
├── static/              # 静态资源（favicon 等）
└── assets/              # 需要处理的资源（SCSS、图片等）
```

## 许可

文章内容采用 [CC BY-NC-SA 4.0](https://creativecommons.org/licenses/by-nc-sa/4.0/) 许可。
代码部分采用 MIT 许可。