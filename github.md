# GitHub

> 本文档整合了以下源文件：github.md

---

## 来源：github.md

本文档整理了 Git 和 GitHub 的实用功能和技巧，涵盖 GitHub 平台操作和 Git 命令行两大类别。

---

## 一、GitHub 平台技巧

### 1.1 URL 参数技巧

| 技巧 | 操作方式 | 说明 |
|------|----------|------|
| 忽略空白差异 | 在 diff URL 末尾添加 `?w=1` | 只显示实质性代码变更，过滤空白字符差异 |
| 调整 Tab 宽度 | 在 diff 或文件 URL 末尾添加 `?ts=4` | 将 Tab 显示为 4 个空格宽（默认为 8），数字可自定义 |
| 按作者查看提交历史 | 在 commits URL 末尾添加 `?author={user}` | 示例：`https://github.com/rails/rails/commits/master?author=dhh` |
| 行高亮 | 在文件 URL 末尾添加 `#L52` 或 `#L53-L60` | 点击行号也可触发，按住 Shift 可选范围 |
| 代码行永久链接 | 查看文件时按 `y` 键 | URL 变为永久链接，即使代码后续修改仍可查看当时版本 |

### 1.2 分支操作

| 操作 | URL 格式 | 说明 |
|------|----------|------|
| 查看所有分支 | `https://github.com/{user}/{repo}/branches` | 查看未合并到主分支的分支列表 |
| 比较两个分支 | `https://github.com/{user}/{repo}/compare/{range}` | `{range}` 示例：`master...4-1-stable` |
| 按日期比较 | `https://github.com/{user}/{repo}/compare/master@{2014-10-04}...master` | 日期格式为 `YYYY-MM-DD` |
| 获取 diff/patch | 在比较 URL 末尾添加 `.diff` 或 `.patch` | 获取纯文本格式的差异或补丁文件 |
| 跨 Fork 比较 | `https://github.com/{user}/{repo}/compare/{foreign-user}:{branch}...{own-branch}` | 比较不同 Fork 的分支 |

### 1.3 Issue 与 Pull Request

| 功能 | 用法 | 说明 |
|------|------|------|
| 提交关闭 Issue | 在提交信息中使用 `fix/fixes/fixed`、`close/closes/closed` 或 `resolve/resolves/resolved` + Issue 编号 | 合并到默认分支后自动关闭对应 Issue |
| 交叉引用 Issue | 输入 `#` + Issue 编号 | 同仓库内自动链接 |
| 跨仓库引用 | 使用 `{user}/{repo}#ISSUE_NUMBER` | 链接其他仓库的 Issue |
| 锁定对话 | 在 Issue 或 PR 页面锁定 | 仅协作者可继续评论 |
| 过滤 Issue/PR | 使用 `is:issue`、`is:pr`、`is:merged`、`label:xxx`、`-label:xxx`、`status:success` | 支持多种过滤条件组合 |
| 任务列表 | 使用 `- [ ]` 和 `- [x]` 语法 | 在 Issue 和 PR 中创建可交互的复选框 |
| 快速引用 | 选中评论文本后按 `r` 键 | 以引用格式复制到回复框 |
| 粘贴剪贴板图片 | 直接在评论区粘贴截图（仅 Chrome） | 图片自动上传到 GitHub |
| 撤销 PR | 在已合并的 PR 页面点击 **Revert** 按钮 | 自动生成撤销 PR |

### 1.4 文件与内容

| 功能 | 说明 |
|------|------|
| Markdown 语法高亮 | 在代码块标记后指定语言，如 ` ```ruby `。GitHub 使用 Linguist 进行语言检测 |
| Emoji 支持 | 在 PR、Issue、提交信息中使用 `:name_of_emoji:` 格式 |
| 图片嵌入 | 使用 `![Alt](url)` 语法，支持仓库内原始图片和外部链接 |
| Wiki 图片尺寸 | 使用 `[[ url | height = 100px ]]` 语法指定尺寸 |
| 相对链接 | Markdown 文件中使用相对路径，如 `[链接](docs/readme)`，便于项目迁移 |
| 渲染表格数据 | GitHub 支持直接渲染 `.csv` 和 `.tsv` 文件 |
| 渲染 PDF | GitHub 支持直接在浏览器中查看 PDF 文件 |
| YAML 元数据 | Jekyll 页面的 YAML 前置元数据会渲染为表格显示 |

### 1.5 Diff 功能

| 功能 | 说明 |
|------|------|
| 渲染模式差异 | Markdown 等文件支持"源码"和"渲染"两种 diff 视图 |
| 地图可视化 | 包含地理数据的提交会渲染为可视化地图 |
| 展开上下文 | 点击 diff 边栏的展开按钮可显示更多上下文行 |
| 图片差异对比 | 支持 PNG、JPG、GIF、PSD 等格式的可视化差异对比 |

### 1.6 仓库管理

| 功能 | 说明 |
|------|------|
| 克隆仓库 | URL 中可省略 `.git` 后缀 |
| Gist | 代码片段管理工具，支持克隆和推送。添加 `.pibb` 获取嵌入用 HTML 版本 |
| Git.io | GitHub 官方短链接服务，支持 curl 方式创建 |
| 快速添加 License | 创建仓库或文件时，输入文件名 `LICENSE` 或 `.gitignore` 可选择模板 |
| 仓库模板 | 在仓库设置中启用模板功能，其他用户可一键复制仓库结构 |
| 贡献指南 | 在根目录或 `.github` 目录下添加 `CONTRIBUTING`、`ISSUE_TEMPLATE`、`PULL_REQUEST_TEMPLATE` 文件 |

### 1.7 键盘快捷键

在仓库页面按 `?` 查看所有快捷键：

| 按键 | 功能 |
|------|------|
| `t` | 打开文件浏览器 |
| `w` | 打开分支选择器 |
| `s` | 聚焦当前仓库搜索框 |
| `l` | 编辑 Issue 标签 |
| `y` | 生成当前文件的永久链接 |

### 1.8 用户信息获取

| 信息 | URL 格式 |
|------|----------|
| SSH 公钥 | `https://github.com/{user}.keys` |
| 头像图片 | `https://github.com/{user}.png` |

### 1.9 GitHub 资源

| 资源 | 链接 |
|------|------|
| GitHub Explore | https://github.com/explore |
| GitHub Blog | https://github.com/blog |
| GitHub Help | https://help.github.com/ |
| GitHub Training | https://training.github.com/ |
| GitHub Developer | https://developer.github.com/ |
| GitHub Education | https://education.github.com/ |
| Student Developer Pack | https://education.github.com/pack |
| Hub (命令行扩展) | https://github.com/github/hub |
| Octicons (图标库) | https://octicons.github.com |

#### 推荐演讲

| 标题 | 链接 |
|------|------|
| How GitHub Uses GitHub to Build GitHub | https://www.youtube.com/watch?v=qyz3jkOBbQY |
| Introduction to Git with Scott Chacon | https://www.youtube.com/watch?v=ZDR433b0HJY |
| Git and GitHub Secrets | https://www.youtube.com/watch?v=Foz9yvMkvlA |
| More Git and GitHub Secrets | https://www.youtube.com/watch?v=p50xsL-iVgU |

---

## 二、Git 命令行技巧

### 2.1 文件与状态

| 命令 | 说明 |
|------|------|
| `git rm $(git ls-files -d)` | 批量删除已从工作目录中移除的文件 |
| `git status -sb` | 显示简洁的分支状态信息 |
| `git stripspace < README.md` | 清除尾部空白、合并空行、确保文件末尾有换行 |

### 2.2 分支操作

| 命令 | 说明 |
|------|------|
| `git checkout -` | 切换到上一个分支，交替在两个分支间切换 |
| `git branch --merged` | 列出已合并到当前分支的所有分支 |
| `git branch --no-merged` | 列出尚未合并到当前分支的分支 |

### 2.3 提交与查询

| 命令 | 说明 |
|------|------|
| `git commit --allow-empty` | 创建无代码变更的空提交，用于标记里程碑或初始化仓库 |
| `git show :/query` | 搜索提交历史中最近匹配关键词的提交（区分大小写） |
| `git grep <pattern>` | 搜索代码中包含指定模式的行，支持 `-e` 和 `--and`/`--or`/`--not` 组合 |

### 2.4 日志美化

```bash
git log --all --graph --pretty=format:'%Cred%h%Creset -%C(auto)%d%Creset %s %Cgreen(%cr) %C(bold blue)<%an>%Creset' --abbrev-commit --date=relative
```

### 2.5 Pull Request 检出

| 命令 | 说明 |
|------|------|
| `git fetch origin refs/pull/[PR-Number]/head` | 获取指定 PR 到 FETCH_HEAD |
| `git fetch origin '+refs/pull/*/head:refs/remotes/origin/pr/*'` | 获取所有 PR 分支为本地远程分支 |
| `git checkout pr/42` | 从 PR 分支创建本地分支（需先配置 fetch） |

全局配置自动获取 PR：

```bash
git config --global --add remote.origin.fetch "+refs/pull/*/head:refs/remotes/origin/pr/*"
```

### 2.6 Fixup 与 Autosquash

修复之前某次提交（如 `abcde`）的问题：

```bash
git commit --fixup=abcde
git rebase abcde^ --autosquash -i
```

### 2.7 本地 Web 浏览

```bash
git instaweb
```

启动 gitweb 服务，通过浏览器查看本地仓库。

### 2.8 Git 配置

#### 常用别名

| 别名 | 对应命令 | 设置方式 |
|------|----------|----------|
| `git cm` | `git commit` | `git config --global alias.cm commit` |
| `git co` | `git checkout` | `git config --global alias.co checkout` |
| `git st` | `git status -sb` | `git config --global alias.st 'status -sb'` |
| `git ac` | `git add -A && git commit` | `git config --global alias.ac '!git add -A && git commit'` |
| `git lg` | 带颜色和图形的日志 | `git config --global alias.lg "log --color --graph --pretty=format:'%Cred%h%Creset -%C(yellow)%d%Creset %s %Cgreen(%cr) %C(bold blue)<%an>%Creset' --abbrev-commit --"` |
| `git cleanup` | 删除已合并的分支 | `git config --global alias.cleanup "!git branch --merged \| grep -v '*' \| xargs git branch -d"` |
| `git tags` | `git tag -l` | `git config --global alias.tags 'tag -l'` |
| `git branches` | `git branch -a` | `git config --global alias.branches 'branch -a'` |
| `git remotes` | `git remote -v` | `git config --global alias.remotes 'remote -v'` |

#### 自动纠错

启用自动纠错（延迟以十分之一秒为单位，15 表示 1.5 秒）：

```bash
git config --global help.autocorrect 15
```

#### 输出着色

```bash
git config --global color.ui 1
```

### 2.9 Git 学习资源

| 资源 | 链接 |
|------|------|
| Git 官方网站 | http://git-scm.com/ |
| Git 视频教程 | http://git-scm.com/videos |
| Git 官方教程 | http://git-scm.com/docs/gittutorial |
| Git Immersion | http://gitimmersion.com/ |
| Learn Git Branching | http://pcottle.github.io/learnGitBranching/ |
| Git 可视化 | http://onlywei.github.io/explain-git-with-d3/#freeplay |
| .gitignore 模板集 | https://github.com/github/gitignore |

#### 推荐书籍

| 书名 | 链接 |
|------|------|
| Pro Git | http://git-scm.com/book |
| Pragmatic Version Control Using Git | https://pragprog.com/titles/tsgit/pragmatic-version-control-using-git |
| Git Internals (PluralSight) | https://github.com/pluralsight/git-internals-pdf |
| Git in the Trenches | http://cbx33.github.io/gitt/ |

#### 推荐视频

| 标题 | 链接 |
|------|------|
| Linus Torvalds on Git | https://www.youtube.com/watch?v=4XpnKHJAok8 |
| Git From the Bits Up | https://www.youtube.com/watch?v=MYP56QJpDr4 |
| GitHub Training & Guides | https://www.youtube.com/watch?list=PLg7s6cbtAD15G8lNyoaYDuKZSKyJrgwB-&v=FyfwLX4HAxM |

---

## 三、关键要点

1. **善用 URL 参数**：GitHub 的 `?w=1`、`?ts=4`、`?author=`、`#L` 等参数可大幅提升代码审查效率
2. **掌握键盘快捷键**：按 `?` 查看当前页面可用快捷键，减少鼠标操作
3. **利用提交信息自动化**：在提交信息中使用 `fixes #` 语法可自动关联和关闭 Issue
4. **配置 Git 别名**：将常用命令缩短为简写，显著提升日常开发效率
5. **使用相对链接**：Markdown 文档中使用相对路径，提高可移植性
6. **善用模板文件**：`CONTRIBUTING`、`ISSUE_TEMPLATE`、`PULL_REQUEST_TEMPLATE` 规范协作流程
7. **利用 PR 检出**：配置自动获取 PR 分支，方便本地测试和审查


---
