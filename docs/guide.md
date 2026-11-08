# 使用指南

本页说明怎样把一次文档修改发布到网站。以下命令默认在仓库根目录执行，本地推荐使用 Python 3.12。

## 1. 准备环境

```bash
git clone https://github.com/seteor-re/my-docs.git
cd my-docs
python3.12 -m venv .venv
source .venv/bin/activate
python -m pip install -r requirements.txt
```

上面的激活命令适用于 macOS / Linux。Windows Git Bash 使用 `source .venv/Scripts/activate`，PowerShell 使用 `.\.venv\Scripts\Activate.ps1`。

## 2. 修改与本地检查

在 `docs/` 中修改 Markdown，然后执行：

```bash
python -m mkdocs build --strict
python -m mkdocs serve
```

打开终端给出的本地地址，通常是 `http://127.0.0.1:8000/`。依次检查首页、关于、使用指南和 API 参考，确认中文标题、导航、表格、代码块以及页面链接。按 `Ctrl+C` 停止预览。

`--strict` 会将警告视为构建失败，避免明显的配置或文档链接问题被直接发布。它不能代替浏览器检查，也不能保证外部网站始终可访问。

## 3. 提交与自动发布

```bash
git status
git add docs mkdocs.yml
git diff --staged
git commit -m "更新技术文档"
git push origin main
```

推送后，打开[Actions 运行列表](https://github.com/seteor-re/my-docs/actions)，查看 `Deploy MkDocs to GitHub Pages` 的运行。`build` 与 `deploy` 都成功后，再访问[公开网站](https://seteor-re.github.io/my-docs/)。

首次发布前，需要在仓库 `Settings → Pages → Source` 选择 **GitHub Actions**。修改文档后由 `push` 自动触发；`workflow_dispatch` 仅用于需要时手动重试。

## 4. 哪些修改会触发部署

| 修改内容 | 推送到 main 后是否自动部署 |
| --- | --- |
| `docs/**` | 是 |
| `mkdocs.yml` | 是 |
| `requirements.txt` | 是 |
| `.github/workflows/deploy.yml` | 是 |
| 仅 `README.md` 或 `report/**` | 否 |

分支条件与文件条件要同时满足。报告和截图不参与网站构建，因此只修改报告不会产生一次新的网站部署。

## 5. 按失败步骤排查

| 现象 | 优先检查 |
| --- | --- |
| `Install dependencies` 失败 | 依赖名称、版本范围、下载日志 |
| `Build documentation` 失败 | YAML 缩进、`nav` 路径、Markdown 链接 |
| `Configure Pages` 失败 | 仓库是否公开、Pages 来源是否已启用 |
| `deploy` 失败 | 部署权限、构建产物、环境规则 |
| 网站没有显示新内容 | 本次运行是否对应最新提交、是否成功、浏览器缓存 |

排错时应记录日志中的具体错误及解决操作，修改后再次检查。自动更新的验证方式是：首次成功发布后，再修改首页的一句话，推送后确认新的运行事件是 `push`，最后检查线上新增文字。

相关内容：[项目组成](about.md) · [API 文档示例](api.md) · [返回首页](index.md)
