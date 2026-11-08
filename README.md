# seteor 的技术笔记

开源软件课程实践项目 02：使用 MkDocs Material 编写四页中文文档，通过 GitHub Actions 构建并部署到 GitHub Pages。

- [网站地址](https://seteor-re.github.io/my-docs/)
- [个人实验报告](report/README.md)
- [Actions 运行记录](https://github.com/seteor-re/my-docs/actions)
- [课程要求](https://github.com/hunnuOpenSourceSoftware2026/assignments/blob/main/02-github-pages.md)

已完成两次由 `push` 触发的成功部署：[首次发布](https://github.com/seteor-re/my-docs/actions/runs/42460574000) · [自动更新验证](https://github.com/seteor-re/my-docs/actions/runs/42460790215)。首页绿色提示框与第二次提交对应，完整过程和截图见实验报告。

## 本地预览

```bash
python3.12 -m venv .venv
source .venv/bin/activate
python -m pip install -r requirements.txt
python -m mkdocs build --strict
python -m mkdocs serve
```

Windows Git Bash 激活命令为 `source .venv/Scripts/activate`。打开终端显示的本地地址，检查四页导航、表格、代码和链接。

## 文件说明

| 路径 | 用途 |
| --- | --- |
| `docs/` | 首页、关于、使用指南、API 参考 |
| `mkdocs.yml` | 站点、主题、导航与 Markdown 配置 |
| `.github/workflows/deploy.yml` | 官方 Pages artifact 部署工作流 |
| `report/` | 实验报告与实际截图 |
| `site/` | 自动生成的构建产物，由 Git 忽略 |

## 自动部署

将仓库 Pages 的 Source 设为 **GitHub Actions**。推送 `docs/**`、`mkdocs.yml`、`requirements.txt` 或工作流文件到 `main` 后，工作流执行严格构建，上传 `site/`，再由 `deploy` 发布。仅修改报告或 README 不会触发部署。
