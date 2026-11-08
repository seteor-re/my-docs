# 关于本项目

## 项目目标

本项目对应开源软件课程的 GitHub Pages 实践。目标是搭建四页中文文档，并让文档的发布过程可以复现、可以检查：从修改 Markdown 到浏览器显示新内容，中间的安装、构建和部署都交给工作流执行。

网站内容分为项目介绍、操作指南和接口示例。接口页只是静态文档练习；网站本身没有后端服务。

## 技术组成

| 工具或服务 | 负责什么 | 在本项目中的位置 |
| --- | --- | --- |
| Markdown | 用纯文本编写标题、表格、链接和代码块 | `docs/` |
| MkDocs | 读取配置，将文档转换为静态 HTML | `mkdocs.yml` |
| Material | 提供导航、中文界面、搜索与代码复制 | MkDocs 主题 |
| Git | 保存可追踪的修改历史 | `main` 分支 |
| GitHub Actions | 在固定环境安装依赖、构建和部署 | `.github/workflows/deploy.yml` |
| GitHub Pages | 托管构建完成的网站 | 公开站点地址 |

## 文件之间的关系

```text
my-docs/
├── docs/                     # 手工维护的四页 Markdown
├── mkdocs.yml                # 站点信息、主题、导航
├── requirements.txt          # Python 依赖范围
├── .github/workflows/deploy.yml
├── report/                   # 实验说明与实际截图
└── site/                     # 自动生成，不提交到 main
```

`nav` 的路径相对于 `docs/`，所以首页写成 `index.md`。`site/` 是构建产物，手工修改它会在下一次构建时被覆盖；需要改变网页时应修改 Markdown 或站点配置。

## 发布流程中的两个任务

`build` 负责读取源码，准备 Python 3.12，安装依赖，执行严格构建，上传 `site/`。`deploy` 通过 `needs: build` 等待构建成功，再使用官方 Pages Action 发布产物。

构建只需要读取仓库。部署任务单独声明 `pages: write` 和 `id-token: write`，并使用 `github-pages` 环境记录部署。这样不需要把整个仓库的默认权限设成读写，也不需要创建 `gh-pages` 分支。

## 对文档自动化的理解

一次本地预览成功，只能说明当前电脑能构建。把相同过程写进工作流后，远程环境会重新安装依赖并构建，从而暴露路径大小写、遗漏文件或依赖配置等问题。将构建日志和提交记录一起保留，比只展示最终截图更容易复现问题。

下一步可阅读[使用指南](guide.md)，或者返回[首页](index.md)。
