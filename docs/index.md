# 我的技术文档

**用文档整理知识，用自动化保持更新。**

欢迎来到 seteor 的技术笔记。这个网站把 Markdown 源文件、Git 版本记录和自动部署连接起来：每次把文档修改推送到 `main`，GitHub Actions 就会构建网站，再交给 GitHub Pages 发布。

- 作者：[seteor-re](https://github.com/seteor-re)
- 实践主题：通过 GitHub Actions 自动部署静态文档
- 技术栈：Python 3.12、MkDocs、Material、GitHub Pages

## 从这里开始

| 页面 | 可以了解的内容 |
| --- | --- |
| [关于本项目](about.md) | 项目目标、文件分工与发布流程 |
| [使用指南](guide.md) | 本地预览、严格构建、推送与排错 |
| [API 参考](api.md) | 请求参数、JSON 响应与错误示例 |

## 为什么把笔记做成网站

分散的笔记容易遗漏上下文。这里把操作步骤、命令和原理放在一起，读者可以沿着导航复现过程，也可以通过搜索找到需要的内容。代码块用于保留准确命令，表格用于说明工具分工，页面之间的链接用于连接相关知识。

这个项目还强调一个可检查的发布过程：源码说明改了什么，Actions 日志说明构建是否成功，公开网页说明读者最终看到了什么。三者对应起来，才算完成一次更新。

## 一次更新如何到达读者

```text
docs/*.md → git push main → build → site/ artifact → deploy → GitHub Pages
```

想亲自修改并发布一页文档，可以从[使用指南](guide.md)开始；想了解各个环节为什么存在，可以阅读[关于本项目](about.md)。
