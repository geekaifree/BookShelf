# 笔记与知识管理

> 本文档整合了以下源文件：notes.md, joplin.md, siyuan.md, logseq.md, knowledge.md, note.md

---

## 来源：notes.md

## 简介

AppFlowy 是 Notion 的开源替代品，提供笔记、项目管理和知识管理功能。以隐私为核心设计，AppFlowy 允许你将数据存储在本地或自己的服务器上，同时提供现代化的块编辑体验。

AppFlowy 结合了文档编辑器的灵活性和数据库的结构化，适用于个人笔记、团队 Wiki 和项目追踪。

## 为什么使用 AppFlowy？

| 特性 | AppFlowy | Notion | Obsidian |
|------|----------|--------|----------|
| 开源 | 是 | 否 | 否 |
| 自托管 | 是 | 否 | 本地文件 |
| 离线模式 | 是 | 有限 | 是 |
| 费用 | 免费 | 免费增值 | 免费增值 |
| 数据所有权 | 完全 | 云端 | 本地 |
| 协作 | 是 | 是 | 有限 |

## 核心功能

| 功能 | 描述 |
|------|------|
| 块编辑器 | 富文本块编辑 |
| 数据库 | 多视图结构化数据 |
| 看板 | 可视化任务管理 |
| 日历 | 日程和事件追踪 |
| 文档 | 长文写作 |
| Wiki | 组织化知识库 |
| 模板 | 预建布局 |
| 协作 | 实时团队编辑 |

## 安装

### 桌面应用

| 平台 | 安装方式 |
|------|---------|
| Windows | 从 appflowy.io 下载 |
| macOS | 从 appflowy.io 下载 |
| Linux | AppImage、Snap 或 Flatpak |
| Docker | 自托管服务器 |

### Docker 部署

```bash
# 创建目录
mkdir -p /opt/appflowy/data

# 使用 Docker 运行
docker run -d \
  --name appflowy \
  -p 8080:8080 \
  -v /opt/appflowy/data:/data \
  appflowy/appflowy_cloud:latest
```

### 移动应用

| 平台 | 可用性 |
|------|-------|
| iOS | App Store |
| Android | Google Play |

## 快速上手

### 首次启动

| 步骤 | 操作 |
|------|------|
| 1 | 打开 AppFlowy |
| 2 | 创建账户或跳过进入本地模式 |
| 3 | 选择工作区名称 |
| 4 | 创建第一个页面 |
| 5 | 开始写作 |

### 界面概述

| 区域 | 用途 |
|------|------|
| 侧边栏 | 页面间导航 |
| 编辑器 | 主内容区 |
| 工具栏 | 格式选项 |
| 属性 | 页面/数据库设置 |

## 文档编辑

### 块类型

| 块类型 | 描述 | 快捷键 |
|-------|------|-------|
| 文本 | 普通段落 | `/text` |
| 标题 1 | 大标题 | `/h1` |
| 标题 2 | 中标题 | `/h2` |
| 标题 3 | 小标题 | `/h3` |
| 无序列表 | 项目符号列表 | `/bullet` |
| 有序列表 | 编号列表 | `/number` |
| 折叠列表 | 可折叠列表 | `/toggle` |
| 引用 | 块引用 | `/quote` |
| 代码 | 代码块 | `/code` |
| 分割线 | 水平线 | `/divider` |
| 高亮框 | 高亮框 | `/callout` |
| 数学公式 | LaTeX 数学 | `/math` |

### 文本格式

| 格式 | 快捷键 | 描述 |
|------|-------|------|
| 粗体 | Ctrl+B | **粗体文本** |
| 斜体 | Ctrl+I | *斜体文本* |
| 下划线 | Ctrl+U | 下划线文本 |
| 删除线 | Ctrl+Shift+S | ~~删除线~~ |
| 代码 | Ctrl+E | `行内代码` |
| 链接 | Ctrl+K | 添加超链接 |

### 媒体

| 媒体类型 | 方式 |
|---------|------|
| 图片 | `/image` 或拖放 |
| 文件 | `/file` 或拖放 |
| 视频 | `/video` 或嵌入 URL |
| 音频 | `/audio` |

## 数据库功能

### 创建数据库

| 步骤 | 操作 |
|------|------|
| 1 | 在侧边栏点击 + |
| 2 | 选择"网格"或"看板" |
| 3 | 定义列 |
| 4 | 添加行 |
| 5 | 选择视图类型 |

### 列类型

| 类型 | 描述 | 示例 |
|------|------|------|
| 文本 | 自由文本 | 备注、描述 |
| 数字 | 数值 | 价格、数量 |
| 选择 | 单选 | 状态、优先级 |
| 多选 | 多选 | 标签、分类 |
| 日期 | 日期选择器 | 截止日期、创建日期 |
| 复选框 | 布尔值 | 完成、已批准 |
| URL | 网页链接 | 网站、文档 |
| 邮箱 | 电子邮件 | 联系信息 |
| 电话 | 电话号码 | 联系信息 |
| 清单 | 任务列表 | 子任务 |

### 数据库视图

| 视图类型 | 描述 | 最适合 |
|---------|------|-------|
| 网格 | 电子表格布局 | 数据管理 |
| 看板 | 带列的看板 | 任务追踪 |
| 日历 | 日历布局 | 日程规划 |
| 画廊 | 卡片网格 | 视觉内容 |

### 过滤和排序

| 功能 | 描述 |
|------|------|
| 过滤 | 仅显示匹配记录 |
| 排序 | 按字段排序记录 |
| 分组 | 按字段值组织 |

## 项目管理

### 看板设置

| 列 | 用途 | 颜色 |
|----|------|------|
| 待办 | 未开始 | 灰色 |
| 进行中 | 进行中 | 蓝色 |
| 审核 | 等待审核 | 黄色 |
| 完成 | 已完成 | 绿色 |

### 任务属性

| 属性 | 类型 | 描述 |
|------|------|------|
| 标题 | 文本 | 任务名称 |
| 状态 | 选择 | 当前状态 |
| 优先级 | 选择 | 紧急程度 |
| 负责人 | 人员 | 负责人 |
| 截止日期 | 日期 | 截止时间 |
| 标签 | 多选 | 分类 |

## 模板

### 内置模板

| 模板 | 使用场景 |
|------|---------|
| 个人笔记 | 日记 |
| 项目追踪 | 任务管理 |
| 会议记录 | 会议文档 |
| 周计划 | 日程管理 |
| 阅读清单 | 书籍追踪 |
| 食谱集 | 烹饪食谱 |

### 创建自定义模板

| 步骤 | 操作 |
|------|------|
| 1 | 设计页面布局 |
| 2 | 添加内容块 |
| 3 | 点击"保存为模板" |
| 4 | 命名和分类 |
| 5 | 分享或保留私有 |

## 协作

### 分享和权限

| 权限级别 | 能力 |
|---------|------|
| 所有者 | 完全控制 |
| 编辑者 | 编辑内容 |
| 评论者 | 添加评论 |
| 查看者 | 只读 |

### 实时协作

| 功能 | 描述 |
|------|------|
| 实时光标 | 看到他人编辑 |
| 评论 | 添加反馈 |
| 提及 | @通知团队成员 |
| 活动日志 | 追踪变更 |

## 数据管理

### 导入

| 来源 | 格式 |
|------|------|
| Notion | Markdown 导出 |
| Markdown | .md 文件 |
| CSV | 电子表格数据 |
| JSON | 结构化数据 |

### 导出

| 格式 | 描述 |
|------|------|
| Markdown | 带格式的纯文本 |
| CSV | 电子表格格式 |
| JSON | 结构化数据 |
| PDF | 文档格式 |

## 键盘快捷键

| 操作 | 快捷键 |
|------|-------|
| 新页面 | Ctrl+N |
| 搜索 | Ctrl+F |
| 命令面板 | Ctrl+P |
| 粗体 | Ctrl+B |
| 斜体 | Ctrl+I |
| 撤销 | Ctrl+Z |
| 重做 | Ctrl+Y |
| 保存 | Ctrl+S |

## 故障排除

| 问题 | 原因 | 解决方案 |
|------|------|---------|
| 应用无法启动 | 数据损坏 | 重新安装应用 |
| 性能缓慢 | 数据库过大 | 归档旧数据 |
| 同步问题 | 网络问题 | 检查连接 |
| 缺少功能 | 版本过旧 | 更新应用 |
| 导入错误 | 格式错误 | 检查导出设置 |

## 更多资源

| 资源 | URL |
|------|-----|
| 官方网站 | appflowy.io |
| GitHub | github.com/AppFlowy-IO/AppFlowy |
| 文档 | docs.appflowy.io |
| 社区 | community.appflowy.io |


---

## 来源：joplin.md

## 简介

Joplin 是一个开源的笔记和待办事项应用，具有同步功能。它支持 Markdown、端到端加密，可在多个平台上使用。本教程涵盖安装、笔记组织、同步和生产力功能。

## 平台可用性

| 平台 | 类型 | 同步支持 | 加密 |
|------|------|----------|------|
| Windows | 桌面 | 完全 | 完全 |
| macOS | 桌面 | 完全 | 完全 |
| Linux | 桌面 | 完全 | 完全 |
| iOS | 移动 | 完全 | 完全 |
| Android | 移动 | 完全 | 完全 |
| Terminal | CLI | 完全 | 完全 |
| Web Clipper | 浏览器扩展 | 通过同步 | 通过同步 |

## 安装

### 桌面

```bash
# macOS (Homebrew)
brew install joplin

# Linux (AppImage)
wget -O - https://raw.githubusercontent.com/laurent22/joplin/dev/Joplin_install_and_update.sh | bash

# Windows
# 从 joplinapp.org 下载安装程序
```

### 终端 (CLI)

```bash
# npm
npm install -g joplin

# 验证
joplin version
```

## 笔记基础

### Markdown 支持

Joplin 使用 GitHub 风格的 Markdown 并有扩展：

| 功能 | 语法 | 预览 |
|------|------|------|
| Headers | `# H1`, `## H2` | 样式化标题 |
| Bold | `**text**` | **text** |
| Italic | `*text*` | *text* |
| Links | `[text](url)` | 可点击链接 |
| Images | `![alt](path)` | 内联图片 |
| Code | `` `code` `` | 内联代码 |
| Code blocks | ` ```language ``` ` | 语法高亮 |
| Tables | `| col | col |` | 格式化表格 |
| Checkboxes | `- [ ] task` | 待办事项 |
| Math | `$E=mc^2$` | LaTeX 渲染 |

### 富文本编辑器

Joplin 还提供所见即所得编辑器：

| 功能 | 描述 |
|------|------|
| Toolbar | 格式按钮 |
| Live preview | 实时渲染 |
| Keyboard shortcuts | 常用格式化 |
| Table editor | 可视化表格创建 |

## 组织

### 笔记本结构

| 层级 | 用途 | 示例 |
|------|------|------|
| Notebook | 顶层类别 | 工作、个人、项目 |
| Sub-notebook | 子类别 | 工作/会议、工作/研究 |
| Note | 单个条目 | 会议笔记、研究文章 |
| Tag | 跨类别标签 | 紧急、参考、草稿 |

### 创建笔记本

1. 在侧边栏点击 "New Notebook"
2. 输入名称
3. 拖动以嵌套在另一个笔记本下（可选）
4. 右键点击以重命名或删除

### 标签系统

| 功能 | 描述 | 用途 |
|------|------|------|
| Multiple tags | 每个笔记 | 交叉引用 |
| Tag search | 按标签筛选 | 快速访问 |
| Tag auto-complete | 建议 | 一致命名 |
| Nested tags | `parent/child` | 分层 |

## 同步

### 同步目标

| 目标 | 设置 | 加密 | 免费层 |
|------|------|------|--------|
| Joplin Cloud | 账户注册 | 可选 | 10 MB 笔记 |
| Dropbox | OAuth | 可选 | 2 GB |
| OneDrive | OAuth | 可选 | 5 GB |
| Nextcloud | 服务器 URL | 可选 | 自托管 |
| WebDAV | 服务器 URL | 可选 | 自托管 |
| S3 | 存储桶配置 | 可选 | 不同 |
| File system | 路径 | 手动 | 无限 |

### 设置同步

1. 前往 Settings > Synchronization
2. 选择同步目标
3. 认证或输入凭据
4. 设置同步间隔
5. 启用加密（可选）
6. 点击 "Synchronize"

### 同步设置

| 设置 | 描述 | 建议 |
|------|------|------|
| Interval | 自动同步频率 | 5 分钟 |
| Conflict resolution | 处理冲突 | 手动审查 |
| Encryption | E2E 加密 | 云同步启用 |
| Resource sync | 同步附件 | 启用 |

## 加密

### 端到端加密

| 步骤 | 操作 | 详情 |
|------|------|------|
| 1 | 启用加密 | Settings > Encryption |
| 2 | 设置主密码 | 强密码短语 |
| 3 | 等待加密 | 处理现有笔记 |
| 4 | 共享密码 | 设备间共享 |

### 加密详情

| 功能 | 实现 |
|------|------|
| Algorithm | AES-256 |
| Key derivation | PBKDF2 |
| Per-note keys | 每个笔记唯一 |
| Password recovery | 不可能 |

## 搜索

### 搜索语法

| 查询 | 描述 | 示例 |
|------|------|------|
| Simple text | 全文搜索 | `meeting notes` |
| Title only | `title:query` | `title:project` |
| Tag filter | `tag:name` | `tag:urgent` |
| Notebook | `notebook:name` | `notebook:work` |
| Created date | `created:date` | `created:20260115` |
| Updated date | `updated:date` | `updated:20260115` |
| Type | `type:todo` | 未完成待办 |
| Regex | `/pattern/` | `/meeting \d+/` |

### 搜索示例

| 目标 | 查询 |
|------|------|
| 最近笔记 | `updated:20260101` |
| 带图片的笔记 | `resource:image/*` |
| 特定笔记本笔记 | `notebook:work tag:project` |
| 未完成任务 | `iscompleted:0 type:todo` |
| 带代码的笔记 | ` ``` ` |

## 待办管理

### 创建待办

```markdown
- [ ] Buy groceries
- [ ] Call dentist
- [x] Send email
```

### 待办功能

| 功能 | 描述 |
|------|------|
| Due dates | 设置截止日期 |
| Reminders | 通知提醒 |
| Completion | 复选框切换 |
| Sorting | 按截止日期、标题、状态 |
| Filtering | 仅显示未完成 |

## Web Clipper

### 浏览器扩展

为 Chrome 或 Firefox 安装 Joplin Web Clipper。

### 剪藏类型

| 类型 | 描述 | 用途 |
|------|------|------|
| Complete page | 完整 HTML | 归档 |
| Simplified page | 纯净内容 | 阅读 |
| Selection | 选定文本 | 特定内容 |
| Screenshot | 页面图片 | 视觉参考 |
| URL | 仅链接 | 书签 |

### Clipper 设置

| 设置 | 描述 |
|------|------|
| Default notebook | 剪藏去向 |
| Tags | 自动应用标签 |
| Source URL | 包含原始 URL |
| Markdown | 转换为 Markdown |

## 插件

### 基本插件

| 插件 | 用途 | 分类 |
|------|------|------|
| Rich Markdown | 增强编辑 | 编辑器 |
| Note Tabs | 标签界面 | 导航 |
| Outline | 目录 | 导航 |
| Templates | 笔记模板 | 生产力 |
| Kanban | 任务看板 | 组织 |
| Markdown Table | 表格编辑器 | 编辑器 |
| Backup | 自动备份 | 维护 |

### 安装插件

1. 前往 Settings > Plugins
2. 浏览可用插件
3. 在所需插件上点击 "Install"
4. 重启 Joplin
5. 配置插件设置

## 模板

### 模板变量

| 变量 | 描述 | 示例 |
|------|------|------|
| `{{date}}` | 当前日期 | 2026-01-15 |
| `{{time}}` | 当前时间 | 14:30 |
| `{{datetime}}` | 日期和时间 | 2026-01-15 14:30 |
| `{{#custom}}` | 自定义字段 | 用户输入 |

### 模板示例

会议笔记：
```markdown
# {{date}} Meeting

## Attendees
- 

## Agenda
1. 

## Notes
- 

## Action Items
- [ ] 
```

每日日记：
```markdown
# {{date}} Journal

## Today's Focus
- 

## Accomplishments
- 

## Tomorrow's Plan
- 

## Reflections

```

## 导入和导出

### 导入来源

| 来源 | 格式 | 备注 |
|------|------|------|
| Evernote | .enex | 完全导入支持 |
| Markdown | .md | 直接导入 |
| Plain text | .txt | 基本导入 |
| HTML | .html | 转换为 Markdown |
| OneNote | 通过转换器 | 第三方工具 |

### 导出格式

| 格式 | 用途 | 质量 |
|------|------|------|
| Markdown | 通用 | 完全保真 |
| HTML | Web 发布 | 渲染 |
| PDF | 分享 | 格式化 |
| JEX | Joplin 备份 | 完整 |
| RAW | 开发 | JSON 格式 |

## 命令行界面

### 基本命令

| 命令 | 描述 |
|------|------|
| `joplin` | 启动交互模式 |
| `joplin ls` | 列出笔记 |
| `joplin mkbook` | 创建笔记本 |
| `joplin mknote` | 创建笔记 |
| `joplin use` | 选择笔记 |
| `joplin cat` | 显示笔记内容 |
| `joplin set` | 设置笔记属性 |
| `joplin sync` | 同步 |

### CLI 工作流

```bash
# 列出笔记本
joplin ls

# 创建笔记
joplin mknote "My Note"

# 在外部编辑器中编辑
joplin use "My Note"
joplin edit

# 同步
joplin sync
```

## 生产力技巧

### 工作流策略

| 策略 | 描述 | 优势 |
|------|------|------|
| PARA method | 项目、领域、资源、归档 | 结构化组织 |
| Zettelkasten | 链接的原子笔记 | 知识构建 |
| Bullet journal | 快速记录 | 每日生产力 |
| Cornell notes | 结构化笔记 | 学习效率 |

### 键盘快捷键

| 操作 | 快捷键 | 分类 |
|------|--------|------|
| 新建笔记 | Ctrl+N | 笔记 |
| 新建待办 | Ctrl+T | 笔记 |
| 新建笔记本 | Ctrl+Shift+N | 组织 |
| 搜索 | Ctrl+G | 导航 |
| 同步 | Ctrl+S | 同步 |
| 切换编辑器 | Ctrl+L | 视图 |
| 粗体 | Ctrl+B | 格式 |
| 斜体 | Ctrl+I | 格式 |
| 链接 | Ctrl+K | 格式 |

## 故障排除

| 问题 | 可能原因 | 解决方案 |
|------|----------|----------|
| 同步冲突 | 并发编辑 | 手动解决 |
| 同步慢 | 大附件 | 减少资源大小 |
| 笔记缺失 | 同步问题 | 检查同步目标 |
| 插件错误 | 版本不匹配 | 更新插件 |
| 搜索不工作 | 索引问题 | 重建搜索索引 |

## 总结

Joplin 提供了一个多功能的、注重隐私的笔记解决方案，具有强大的 Markdown 支持和灵活的同步功能。其跨平台可用性和加密功能使其适合个人和专业使用。

关键实践：

- 使用笔记本和标签组织笔记结构
- 为云同步启用端到端加密
- 安装插件以增强功能
- 创建模板以获得一致的笔记格式
- 使用 web clipper 捕获网页内容
- 利用 CLI 进行自动化和脚本编写


---

## 来源：siyuan.md

## 简介

SiYuan 是一款本地优先的个人知识管理系统，具有块级引用和所见即所得编辑器。它提供强大的链接、大纲和查询功能，用于构建互联笔记。

## 目录

1. [核心概念](#核心概念)
2. [安装](#安装)
3. [界面概览](#界面概览)
4. [块级编辑](#块级编辑)
5. [链接与引用](#链接与引用)
6. [查询与搜索](#查询与搜索)
7. [模板与自动化](#模板与自动化)
8. [同步与备份](#同步与备份)

## 核心概念

### 核心功能

| 功能 | 说明 |
|------|------|
| 基于块 | 一切都是块 |
| 本地优先 | 数据存储在设备上 |
| 双向链接 | 双向连接 |
| 所见即所得 | 所见即所得 |
| 大纲 | 层级结构 |
| 查询语言 | 基于 SQL 的查询 |

### 块类型

| 块类型 | 说明 | 使用场景 |
|--------|------|----------|
| 文档 | 顶层容器 | 笔记页面 |
| 标题 | 章节分隔符 | 文档结构 |
| 段落 | 文本块 | 内容 |
| 列表 | 有序/无序 | 大纲 |
| 代码 | 语法高亮 | 代码片段 |
| 表格 | 表格数据 | 结构化数据 |
| 图片 | 嵌入媒体 | 视觉内容 |
| 嵌入 | 链接块 | 引用 |

## 安装

### 平台支持

| 平台 | 方式 | 大小 |
|------|------|------|
| Windows | 安装程序 | ~150 MB |
| macOS | DMG | ~150 MB |
| Linux | AppImage/DEB | ~150 MB |
| Android | APK | ~100 MB |
| iOS | TestFlight | ~100 MB |
| Docker | 容器 | ~500 MB |

### Docker 安装

```yaml
# docker-compose.yml
services:
  siyuan:
    image: b3log/siyuan:latest
    ports:
      - "6806:6806"
    volumes:
      - ./siyuan:/siyuan/workspace
    command: --workspace=/siyuan/workspace
    restart: unless-stopped
```

### 系统要求

| 组件 | 最低要求 | 推荐配置 |
|------|----------|----------|
| CPU | 2 核 | 4 核 |
| 内存 | 2 GB | 4 GB |
| 存储 | 1 GB | 10 GB+ |
| 操作系统 | 64 位 | 现代 OS |

## 界面概览

### 主要区域

| 区域 | 位置 | 用途 |
|------|------|------|
| 侧边栏 | 左侧 | 文件树、大纲 |
| 编辑器 | 中央 | 笔记编辑 |
| 右面板 | 右侧 | 反向链接、大纲 |
| 标签栏 | 顶部 | 打开的文档 |
| 状态栏 | 底部 | 文档信息 |

### 导航方式

| 方式 | 说明 |
|------|------|
| 文件树 | 层级浏览 |
| 快速搜索 | Ctrl+P 搜索文档 |
| 全局搜索 | Ctrl+Shift+F 搜索内容 |
| 反向链接 | 查看传入引用 |
| 图谱视图 | 可视化连接 |

## 块级编辑

### 创建块

| 操作 | 方法 |
|------|------|
| 新段落 | 回车键 |
| 新标题 | 输入 `#` + 空格 |
| 代码块 | 输入 ` ``` ` |
| 列表项 | 输入 `-` 或 `1.` |
| 表格 | 输入 `\|` |
| 分隔线 | 输入 `---` |

### 块操作

| 操作 | 方法 |
|------|------|
| 移动块 | 拖动手柄 |
| 复制块 | Ctrl+C |
| 剪切块 | Ctrl+X |
| 删除块 | Delete 键 |
| 复制 | Ctrl+D |
| 折叠/展开 | 点击箭头 |

### 块属性

| 属性 | 说明 |
|------|------|
| ID | 唯一块标识符 |
| 类型 | 块种类 |
| 创建时间 | 创建时间戳 |
| 更新时间 | 最后修改 |
| 标签 | 关联标签 |
| 自定义属性 | 用户定义属性 |

## 链接与引用

### 链接类型

| 链接类型 | 语法 | 说明 |
|----------|------|------|
| 块引用 | `((block-id "text"))` | 链接到特定块 |
| 文档链接 | `[[document name]]` | 链接到文档 |
| 锚点链接 | `[[document#heading]]` | 链接到标题 |
| URL 链接 | `[text](url)` | 外部链接 |

### 块引用

```markdown
这引用了另一个块: ((block-id "源文本"))
```

### 双向链接

| 功能 | 说明 |
|------|------|
| 正向链接 | 文档链接到另一个 |
| 反向链接 | 被链接文档显示引用 |
| 未链接提及 | 无链接的文本提及 |
| 链接计数 | 引用数量 |

### 创建链接

| 方式 | 操作 |
|------|------|
| 块引用 | 输入 `((` 并搜索 |
| 文档链接 | 输入 `[[` 并搜索 |
| 拖放 | 将文档拖入编辑器 |
| 复制引用 | 右键 > 复制块引用 |

## 查询与搜索

### 查询语法

| 操作符 | 示例 | 说明 |
|--------|------|------|
| `content:` | `content:keyword` | 搜索内容 |
| `tag:` | `tag:todo` | 按标签过滤 |
| `type:` | `type:document` | 块类型 |
| `path:` | `path:/notes/` | 路径过滤 |
| `created:` | `created:2024-01-15` | 日期过滤 |

### 高级查询

```sql
-- 基于 SQL 的查询
SELECT * FROM blocks WHERE content LIKE '%keyword%'
AND type = 'p'
ORDER BY updated DESC
LIMIT 10
```

### 搜索功能

| 功能 | 说明 |
|------|------|
| 全文 | 搜索所有内容 |
| 正则 | 模式匹配 |
| 过滤器 | 多条件 |
| 排序 | 多种排序 |
| 保存查询 | 可重用搜索 |

### 全局搜索

| 快捷键 | 操作 |
|--------|------|
| Ctrl+Shift+F | 打开全局搜索 |
| Enter | 执行搜索 |
| Esc | 关闭搜索 |
| 上/下 | 导航结果 |

## 模板与自动化

### 模板语法

| 语法 | 说明 | 示例 |
|------|------|------|
| `{{date}}` | 当前日期 | 2024-01-15 |
| `{{time}}` | 当前时间 | 14:30 |
| `{{title}}` | 文档标题 | - |
| `{{tags}}` | 文档标签 | - |
| `{{query}}` | 嵌入查询 | - |

### 模板示例

```markdown
# {{date}} - 每日笔记

## 任务
- [ ] 任务 1
- [ ] 任务 2

## 笔记
{{query: SELECT * FROM blocks WHERE tag='note' AND created > '{{date}}'}}

## 反思
```

### 模板管理

| 操作 | 方法 |
|------|------|
| 创建模板 | Templates 文件夹 |
| 应用模板 | 模板选择器 |
| 全局模板 | 随处可用 |
| 路径模板 | 特定位置 |

### 自动化功能

| 功能 | 说明 |
|------|------|
| 每日笔记 | 自动每日文档 |
| 定时查询 | 自动更新结果 |
| 闪卡 | 间隔重复 |
| 数据库视图 | 结构化数据 |

## 同步与备份

### 同步方式

| 方式 | 说明 | 使用场景 |
|------|------|----------|
| S3 | 云存储同步 | 多设备 |
| WebDAV | 标准协议 | NAS、云 |
| 本地 | 手动文件复制 | 单设备 |
| Git | 版本控制 | 高级用户 |

### S3 配置

| 设置 | 说明 |
|------|------|
| Endpoint | S3 兼容端点 |
| Bucket | 存储桶 |
| Access Key | S3 访问密钥 |
| Secret Key | S3 密钥 |
| Region | 存储区域 |

### 备份选项

| 选项 | 说明 | 频率 |
|------|------|------|
| 完整备份 | 所有数据 | 每周 |
| 增量 | 仅更改 | 每日 |
| 数据快照 | 时间点 | 按需 |

### 导出格式

| 格式 | 说明 | 使用场景 |
|------|------|----------|
| Markdown | .md 文件 | 可移植性 |
| SiYuan | .sy.zip | 完整备份 |
| HTML | 网页 | 分享 |
| PDF | 文档 | 打印 |

## 高级功能

### 闪卡（间隔重复）

| 功能 | 说明 |
|------|------|
| 创建卡片 | 将块标记为闪卡 |
| 复习 | 定时复习会话 |
| 算法 | SuperMemo-2 算法 |
| 统计 | 复习历史 |

### 图谱视图

| 功能 | 说明 |
|------|------|
| 节点可视化 | 文档作为节点 |
| 边可视化 | 链接作为连接 |
| 过滤 | 按标签、类型、路径 |
| 聚类 | 相关文档 |

### 数据库

| 功能 | 说明 |
|------|------|
| 表格视图 | 类似电子表格 |
| 看板视图 | 面板视图 |
| 画廊视图 | 卡片网格 |
| 属性 | 自定义字段 |

### API 访问

| 端点 | 方法 | 用途 |
|------|------|------|
| `/api/block/getBlockByID` | POST | 获取块 |
| `/api/block/insertBlock` | POST | 创建块 |
| `/api/block/updateBlock` | POST | 更新块 |
| `/api/block/deleteBlock` | POST | 删除块 |
| `/api/search/fullTextSearchBlock` | POST | 搜索 |

## 键盘快捷键

### 通用

| 快捷键 | 操作 |
|--------|------|
| Ctrl+N | 新建文档 |
| Ctrl+P | 快速搜索 |
| Ctrl+Shift+F | 全局搜索 |
| Ctrl+E | 编辑模式 |
| Ctrl+L | 聚焦编辑器 |

### 编辑

| 快捷键 | 操作 |
|--------|------|
| Ctrl+B | 粗体 |
| Ctrl+I | 斜体 |
| Ctrl+K | 插入链接 |
| Ctrl+Shift+C | 代码块 |
| Tab | 缩进 |
| Shift+Tab | 取消缩进 |

## 总结

SiYuan 提供了一个强大的本地优先知识管理系统，具有块级引用和双向链接。其结合了所见即所得编辑、SQL 查询和同步功能，使其适合构建具有互联笔记的全面个人知识库。


---

## 来源：logseq.md

## 简介

Logseq 是一个隐私优先的开源知识管理平台。它将笔记、大纲和知识图谱功能结合在一个应用中。

### 什么是 Logseq？

Logseq 是一个本地优先的知识库，使用纯文本文件，提供双向链接、块级引用和强大的图谱视图。

| 特性 | 描述 |
|------|------|
| 大纲 | 层级化项目符号编辑 |
| 双向链接 | 自然地连接笔记 |
| 知识图谱 | 连接的可视化表示 |
| 本地优先 | 文件存储在设备上 |
| Markdown/Org-mode | 纯文本格式 |

### 与其他工具的比较

| 特性 | Logseq | Obsidian | Roam |
|------|--------|----------|------|
| 开源 | 是 | 否 | 否 |
| 本地优先 | 是 | 是 | 否 |
| 大纲 | 是 | 部分 | 是 |
| 图谱视图 | 是 | 是 | 是 |
| 免费 | 是 | 免费增值 | 否 |

## 安装

### 系统要求

| 平台 | 要求 |
|------|------|
| Windows | Windows 10+ |
| macOS | macOS 10.15+ |
| Linux | Ubuntu 18.04+ |
| 移动端 | iOS 14+ / Android 8+ |

### 安装方式

```bash
# macOS (Homebrew)
brew install --cask logseq

# Linux (Flatpak)
flatpak install flathub com.logseq.Logseq

# Windows (Winget)
winget install Logseq.Logseq
```

### 下载

访问 https://logseq.com/downloads 获取官方安装包。

## 核心概念

### 页面和块

| 概念 | 描述 |
|------|------|
| 页面 | 文档或主题 |
| 块 | 项目符号或内容单元 |
| 属性 | 附加到块的元数据 |
| 命名空间 | 层级化页面组织 |

### 块结构

```
- Block 1
  - Child block 1.1
  - Child block 1.2
    - Grandchild block
- Block 2
  - Child block 2.1
```

### 页面链接

```markdown
This is a link to [[Another Page]]
This references [[Another Page]] with more context
```

## 日志和每日笔记

### 日志结构

Logseq 自动创建每日日志页面：

```
Journal
├── 2024-01-15
├── 2024-01-14
├── 2024-01-13
└── ...
```

### 日志模板

```markdown
- ## Morning
  - Today's priorities
- ## Notes
  - Meeting notes
- ## Evening
  - Reflections
```

### 每日笔记配置

| 设置 | 描述 |
|------|------|
| 首选格式 | Markdown 或 Org-mode |
| 日志页面标题格式 | 日期格式 |
| 默认模板 | 自动应用的模板 |

## 双向链接

### 创建链接

| 语法 | 结果 |
|------|------|
| `[[Page Name]]` | 链接到页面 |
| `[[Page Name][Display Text]]` | 自定义显示文本的链接 |
| `#Tag` | 标签链接 |
| `#[[Multi Word Tag]]` | 多词标签 |

### 反向链接

当您链接到某个页面时，被链接的页面会自动显示反向引用。

| 功能 | 描述 |
|------|------|
| 链接引用 | 链接到当前页面的页面 |
| 未链接引用 | 没有显式链接的提及 |
| 过滤引用 | 缩小引用列表 |

## 知识图谱

### 图谱视图

图谱视图可视化页面之间的连接：

| 元素 | 含义 |
|------|------|
| 节点 | 页面 |
| 边 | 页面之间的链接 |
| 大小 | 连接数量 |
| 颜色 | 页面类型或标签 |

### 图谱过滤器

| 过滤器 | 用途 |
|--------|------|
| 页面过滤器 | 显示特定页面 |
| 标签过滤器 | 显示带标签的页面 |
| 属性过滤器 | 按属性过滤 |
| 时间过滤器 | 显示日期范围内的页面 |

## 模板

### 创建模板

```markdown
- template:: Meeting Notes
  - Date: 
  - Attendees: 
  - Agenda: 
  - Notes: 
  - Action Items: 
```

### 使用模板

输入 `/Template` 并从可用模板中选择。

### 模板示例

| 模板 | 用例 |
|------|------|
| Meeting Notes | 记录会议详情 |
| Book Notes | 结构化读书笔记 |
| Project Plan | 项目组织 |
| Daily Review | 每日回顾反思 |

## 属性

### 添加属性

```markdown
- type:: book
  author:: [[Author Name]]
  rating:: 4
  status:: reading
```

### 属性类型

| 类型 | 示例 |
|------|------|
| 文本 | `title:: My Note` |
| 数字 | `rating:: 5` |
| 日期 | `date:: [[2024-01-15]]` |
| 页面 | `author:: [[Author]]` |
| 复选框 | `done:: true` |
| URL | `url:: https://example.com` |

### 查询属性

```markdown
{{query (property type book)}}
{{query (property status reading)}}
```

## 查询

### 基本查询

```markdown
{{query (page [[Tag Name]])}}
{{query (property type book)}}
```

### 高级查询

```clojure
#+BEGIN_QUERY
{:title "Books to read"
 :query [:find (pull ?b [*])
         :in $ ?type
         :where [?b :block/properties ?props]
                [(get ?props :type) ?type]
                [(= ?type "book")]]
 :inputs ["book"]}
#+END_QUERY
```

### 查询示例

| 查询 | 结果 |
|------|------|
| `{{query (page [[TODO]])}}` | 所有待办事项 |
| `{{query (property status done)}}` | 已完成项目 |
| `{{query (between -7d today)}}` | 最近 7 天 |

## 任务管理

### TODO 系统

```markdown
- TODO Buy groceries
  SCHEDULED: <2024-01-15>
- DOING Write report
- DONE Submit assignment
```

### 任务状态

| 状态 | 含义 |
|------|------|
| `TODO` | 未开始 |
| `DOING` | 进行中 |
| `DONE` | 已完成 |
| `LATER` | 以后再做 |
| `NOW` | 当前优先 |

### 调度

```markdown
- TODO Task name
  SCHEDULED: <2024-01-15>
  DEADLINE: <2024-01-20>
```

## 插件

### 热门插件

| 插件 | 功能 |
|------|------|
| TODO Master | 增强任务管理 |
| Agenda | 日历集成 |
| Markdown Table Editor | 表格编辑 |
| Zotero | 参考文献管理 |
| GitHub Sync | 版本控制 |

### 安装插件

1. 打开设置
2. 导航到插件
3. 浏览市场
4. 点击安装

## 导入和导出

### 支持的格式

| 格式 | 导入 | 导出 |
|------|------|------|
| Markdown | 是 | 是 |
| Org-mode | 是 | 是 |
| Roam JSON | 是 | 否 |
| Notion | 是 | 否 |
| HTML | 否 | 是 |

### 从 Roam 导入

```bash
# 从 Roam 导出为 JSON
# 在 Logseq 中使用导入功能
# 选择 Roam JSON 格式
```

## 同步

### Git 同步

```bash
# 在图谱文件夹初始化 git
cd ~/logseq/graphs/my-graph
git init
git add .
git commit -m "Initial commit"
```

### 同步选项

| 方式 | 描述 |
|------|------|
| Git | 版本控制 |
| Syncthing | 点对点同步 |
| iCloud | Apple 设备 |
| Google Drive | 云同步 |
| Logseq Sync | 官方同步服务 |

## 自定义

### 主题

| 主题 | 风格 |
|------|------|
| Light | 默认亮色主题 |
| Dark | 暗色模式 |
| Dracula | 紫色暗色主题 |
| Solarized | 柔和对比 |
| Custom | 用户自定义 CSS |

### 自定义 CSS

```css
/* Custom styling */
.ls-block {
  font-size: 16px;
}

.page-title {
  color: #4a90d9;
}
```

## 键盘快捷键

### 常用快捷键

| 操作 | Windows/Linux | macOS |
|------|--------------|-------|
| 新建页面 | Ctrl+Shift+N | Cmd+Shift+N |
| 搜索 | Ctrl+K | Cmd+K |
| 粗体 | Ctrl+B | Cmd+B |
| 斜体 | Ctrl+I | Cmd+I |
| 链接 | Ctrl+L | Cmd+L |

## 总结

| 概念 | 用途 |
|------|------|
| 页面 | 组织知识主题 |
| 块 | 内容的基本单元 |
| 链接 | 连接相关信息 |
| 图谱 | 可视化知识网络 |
| 查询 | 检索信息 |
| 模板 | 标准化笔记格式 |


---

## 来源：knowledge.md

## 简介

Trilium Notes 是一款层次化笔记应用，专注于构建个人知识库。它支持富文本编辑、代码编辑，并提供强大的信息组织和关联功能。

| 特性 | 描述 |
|---------|-------------|
| 层次化笔记 | 树状结构的笔记组织 |
| 富文本 | 所见即所得编辑器，带格式选项 |
| 代码笔记 | 语法高亮的代码编辑 |
| 关系 | 通过关系将笔记相互链接 |
| 加密 | 端到端笔记加密 |

## 架构

### 核心概念

| 概念 | 描述 |
|---------|-------------|
| Note | 知识库中的单个内容 |
| Branch | 笔记之间的父子关系 |
| Attribute | 附加到笔记的元数据（标签、关系） |
| Relation | 两个笔记之间的有向链接 |
| Label | 笔记上的键值元数据 |

### 笔记类型

| 类型 | 描述 | 使用场景 |
|------|-------------|----------|
| Text | 带格式的富文本 | 通用笔记和文档 |
| Code | 语法高亮的代码 | 代码片段和脚本 |
| Render | 动态渲染内容 | 计算和模板 |
| File | 附加文件 | 文档和图片 |
| Image | 图片笔记 | 截图和图表 |
| Book | 子笔记的容器 | 组织收藏 |
| Search | 保存的搜索查询 | 动态笔记集合 |

## 安装

### Docker 部署

```bash
docker run -d \
  --name=trilium \
  -p 8080:8080 \
  -v ./data:/home/node/trilium-data \
  -e TRILIUM_DATA_DIR=/home/node/trilium-data \
  --restart unless-stopped \
  zadam/trilium:latest
```

### Docker Compose

```yaml
version: "3.8"
services:
  trilium:
    image: zadam/trilium:latest
    container_name: trilium
    ports:
      - "8080:8080"
    volumes:
      - ./data:/home/node/trilium-data
    environment:
      - TRILIUM_DATA_DIR=/home/node/trilium-data
    restart: unless-stopped
```

### 桌面应用

| 平台 | 下载 |
|----------|----------|
| Windows | TriliumNotes-windows-x64.zip |
| macOS | TriliumNotes-macos-x64.dmg |
| Linux | TriliumNotes-linux-x64.tar.xz |

## 笔记组织

### 树状结构

```
Root
├── 每日笔记
│   ├── 2024-01
│   │   ├── 2024-01-15
│   │   └── 2024-01-16
│   └── 2024-02
├── 项目
│   ├── 项目 Alpha
│   └── 项目 Beta
├── 参考资料
│   ├── 编程
│   └── 设计
└── 日志
```

### 移动和克隆

| 操作 | 描述 |
|--------|-------------|
| 移动 | 更改笔记的父级 |
| 克隆 | 在另一个位置创建笔记的引用 |
| 复制 | 创建笔记的独立副本 |
| 删除 | 将笔记移到回收站（可恢复） |

### Book 笔记

Book 笔记用作组织相关笔记的容器。

| 功能 | 描述 |
|---------|-------------|
| 排序子项 | 自动排序子笔记 |
| 默认展开 | 打开笔记时显示子项 |
| 提升显示 | 将视图聚焦于此笔记和子项 |

## 富文本编辑器

### 格式选项

| 格式 | 描述 |
|--------|-------------|
| 加粗 | 使文本加粗 |
| 斜体 | 使文本倾斜 |
| 下划线 | 为文本添加下划线 |
| 删除线 | 为文本添加删除线 |
| 标题 | H1 到 H4 标题 |
| 列表 | 项目符号和编号列表 |
| 链接 | 内部和外部链接 |
| 表格 | 插入和编辑表格 |
| 代码块 | 内联和块级代码 |
| 图片 | 插入图片 |
| 颜色 | 文本和背景颜色 |

### 键盘快捷键

| 快捷键 | 操作 |
|----------|--------|
| Ctrl+B | 加粗 |
| Ctrl+I | 斜体 |
| Ctrl+U | 下划线 |
| Ctrl+K | 插入链接 |
| Ctrl+Shift+C | 代码块 |
| Ctrl+S | 保存笔记 |

## 代码笔记

### 支持的语言

| 语言 | 语法高亮 |
|----------|-------------------|
| JavaScript | 完全支持，可执行 Node.js |
| Python | 语法高亮 |
| SQL | 语法高亮，支持查询执行 |
| HTML | 语法高亮，支持预览 |
| CSS | 语法高亮 |
| JSON | 语法高亮，支持验证 |
| Markdown | 语法高亮，支持预览 |
| TypeScript | 语法高亮 |

### 代码执行

```javascript
// JavaScript 笔记可执行
return "Hello from Trilium!";

// 访问 API
const note = api.origin.getActiveNote();
return note.title;
```

## 属性

### 标签属性

| 标签 | 描述 |
|-------|-------------|
| `#readOnly` | 使笔记只读 |
| `#autoReadOnlyDisabled` | 禁用自动只读 |
| `#sorted` | 按字母顺序排序子项 |
| `#sortDirection` | 排序方向（asc/desc） |
| `#calendarRoot` | 标记为日历根 |
| `#hidePromoted` | 隐藏提升的属性 |
| `#cssClass` | 为笔记添加 CSS 类 |

### 关系属性

| 关系 | 描述 |
|----------|-------------|
| `~` 前缀 | 定义到另一个笔记的关系 |
| `run` | 笔记加载时执行的脚本 |
| `renderNote` | 在当前笔记内渲染的笔记 |
| `template` | 创建新笔记的模板 |

### 属性继承

| 行为 | 描述 |
|----------|-------------|
| 继承 | 子笔记继承父级属性 |
| 覆盖 | 子级可覆盖继承的属性 |
| 提升 | 在 UI 中突出显示的属性 |

## 搜索

### 搜索语法

| 语法 | 描述 | 示例 |
|--------|-------------|---------|
| 简单文本 | 全文搜索 | `machine learning` |
| 精确短语 | 引号搜索 | `"neural network"` |
| 属性搜索 | 按属性搜索 | `#book` |
| 通配符 | 模式匹配 | `prog*` |
| 逻辑运算符 | AND、OR、NOT | `python AND tutorial` |

### 保存的搜索

基于搜索查询创建动态笔记集合。

| 示例 | 描述 |
|---------|-------------|
| `#book` | 所有标记为书籍的笔记 |
| `#dateModified >= NOW-7` | 最近修改的笔记 |
| `note.title LIKE '%project%'` | 标题中包含 "project" 的笔记 |

## 关系和图谱

### 创建关系

| 步骤 | 操作 |
|------|--------|
| 1 | 打开笔记属性面板 |
| 2 | 添加关系属性 |
| 3 | 设置关系名称（如 "related-to"） |
| 4 | 选择目标笔记 |
| 5 | 关系双向创建 |

### 关系图

关系图将笔记之间的连接可视化为图谱。

| 功能 | 描述 |
|---------|-------------|
| 节点 | 笔记显示为圆圈 |
| 边 | 关系显示为线条 |
| 缩放 | 平移和缩放图谱 |
| 布局 | 自动或手动定位 |
| 过滤 | 按关系类型过滤 |

## 加密

### 笔记加密

| 设置 | 描述 |
|---------|-------------|
| 受保护笔记 | 笔记使用密码加密 |
| 密码保护 | 查看需要密码 |
| 本地加密 | 在本地存储上加密 |
| 同步加密 | 同步期间加密 |

### 加密选项

| 选项 | 描述 |
|--------|-------------|
| 单笔记 | 加密单个笔记 |
| 分支 | 加密整个笔记分支 |
| 全局 | 加密整个数据库 |

## 同步

### 同步方式

| 方式 | 描述 |
|--------|-------------|
| 服务器同步 | 通过 Trilium 服务器同步 |
| 文件同步 | 通过共享文件系统同步 |
| 手动导出/导入 | 手动数据传输 |

### 同步配置

| 设置 | 描述 |
|---------|-------------|
| 服务器实例 | 同步服务器的 URL |
| 同步间隔 | 同步更改的频率 |
| 冲突解决 | 如何处理同步冲突 |

## 脚本和自动化

### 脚本能力

| 类型 | 描述 |
|------|-------------|
| 后端脚本 | 在服务器上运行，完全 API 访问 |
| 前端脚本 | 在浏览器中运行，UI 访问 |
| 定时脚本 | 在指定间隔执行 |
| 事件脚本 | 在笔记事件时触发 |

### API 访问

```javascript
// 获取当前笔记
const note = api.origin.getActiveNote();

// 搜索笔记
const results = await api.searchForNotes("my search");

// 创建新笔记
await api.createNote({
  parentNoteId: 'root',
  title: 'New Note',
  content: 'Note content',
  type: 'text'
});
```

## 导入和导出

### 导入格式

| 格式 | 描述 |
|--------|-------------|
| Markdown | 导入 .md 文件 |
| HTML | 导入 HTML 文件 |
| OPML | 导入大纲文件 |
| Text | 导入纯文本文件 |
| Enex | 从 Evernote 导入 |

### 导出格式

| 格式 | 描述 |
|--------|-------------|
| HTML | 导出为 HTML 文件 |
| Markdown | 导出为 Markdown |
| OPML | 导出为大纲 |
| JSON | 导出笔记结构 |

## 总结

| 主题 | 核心要点 |
|-------|-------------|
| 组织 | 层次化树状结构，支持克隆 |
| 笔记 | 富文本、代码和文件笔记类型 |
| 属性 | 标签和关系用于元数据和链接 |
| 搜索 | 强大的全文和基于属性的搜索 |
| 加密 | 单笔记和分支级加密 |
| 自动化 | JavaScript API 用于脚本和自动化 |


---

## 来源：note.md

Trilium（现为 TriliumNext）综合教程，这是一个用于构建个人知识库的分层笔记应用。用强大的功能组织你的想法、研究和知识。

## 目录

- [什么是 Trilium](#什么是-trilium)
- [安装](#安装)
- [笔记类型](#笔记类型)
- [属性](#属性)
- [关系](#关系)
- [脚本](#脚本)
- [同步](#同步)
- [分享](#分享)
- [搜索](#搜索)
- [模板](#模板)
- [API](#api)
- [备份](#备份)
- [移动端访问](#移动端访问)

---

## 什么是 Trilium

### 概述

Trilium 是一个分层笔记应用，专注于构建大型个人知识库。它使用树形结构组织笔记，支持脚本、属性和关系等丰富功能。

### 核心特性

| 特性 | 描述 |
|---------|-------------|
| 分层笔记 | 无限嵌套深度 |
| 富文本编辑器 | 所见即所得编辑 |
| 代码笔记 | 代码语法高亮 |
| 属性 | 笔记的元数据和属性 |
| 关系 | 笔记间的链接 |
| 脚本 | JavaScript 自动化 |
| 全文搜索 | 快速搜索所有笔记 |
| 同步 | 多设备同步 |
| 分享 | 将笔记发布为网页 |
| 版本控制 | 笔记历史和修订 |
| 加密 | 密码保护笔记 |
| API | REST API 集成 |

### 与其他工具对比

| 特性 | Trilium | Obsidian | Notion | Joplin | Logseq |
|---------|---------|----------|--------|--------|--------|
| 自托管 | 是 | 否 | 否 | 是 | 否 |
| 开源 | 是 | 否 | 否 | 是 | 是 |
| 分层 | 是 | 有限 | 是 | 扁平 | 大纲 |
| 脚本 | 是 | 插件 | 有限 | 否 | 否 |
| Web 访问 | 是 | 否 | 是 | 否 | 否 |
| 离线优先 | 是 | 是 | 否 | 是 | 是 |
| 关系 | 是 | 链接 | 链接 | 链接 | 链接 |
| API | 是 | 否 | 是 | 是 | 否 |

---

## 安装

### 安装方式

| 方式 | 最适合 | 难度 |
|--------|----------|------------|
| Docker | 自托管、服务器 | 简单 |
| 桌面应用 | 个人使用 | 简单 |
| Snap | Ubuntu/Linux | 简单 |
| 手动 | 自定义设置 | 中等 |

### Docker 安装

```bash
# 创建数据目录
mkdir -p ~/trilium-data

# 运行 Trilium
docker run -d \
  --name trilium \
  --restart=always \
  -p 8080:8080 \
  -v ~/trilium-data:/home/node/trilium-data \
  triliumnext/notes:latest
```

### Docker Compose

```yaml
version: "3.8"

services:
  trilium:
    image: triliumnext/notes:latest
    container_name: trilium
    ports:
      - "8080:8080"
    volumes:
      - trilium-data:/home/node/trilium-data
    environment:
      - TRILIUM_DATA_DIR=/home/node/trilium-data
    restart: unless-stopped

volumes:
  trilium-data:
```

### 桌面应用

| 平台 | 下载来源 |
|----------|----------------|
| Windows | GitHub releases (.exe) |
| macOS | GitHub releases (.dmg) |
| Linux | GitHub releases (.AppImage) |
| Flatpak | `flatpak install com.github.TriliumNext.Notes` |
| Snap | `sudo snap install trilium` |

### 系统要求

| 要求 | 最低 | 推荐 |
|-------------|---------|-------------|
| RAM | 512 MB | 2 GB |
| 存储 | 100 MB + 数据 | 1 GB + 数据 |
| CPU | 1 核 | 2 核 |
| 浏览器 | 现代浏览器 | Chrome、Firefox、Edge |

---

## 笔记类型

### 可用笔记类型

| 类型 | 描述 | 用例 |
|------|-------------|----------|
| 文本 | 带格式的富文本 | 通用笔记、文档 |
| 代码 | 语法高亮代码 | 编程、脚本 |
| 画布 | 无限绘图画布 | 图表、草图 |
| Mermaid | 文本生成图表 | 流程图、时序图 |
| 关系图 | 可视化关系图 | 知识可视化 |
| 书籍 | 子笔记容器 | 组织章节 |
| 搜索 | 保存的搜索结果 | 动态集合 |
| 渲染笔记 | 渲染的 HTML | 自定义视图 |
| 文件 | 上传的文件附件 | 文档、图片 |
| 图片 | 图片笔记 | 截图、照片 |

### 创建笔记

| 操作 | 方法 |
|--------|--------|
| 创建子笔记 | 右键笔记 > 添加子笔记 |
| 创建同级笔记 | 右键笔记 > 添加同级笔记 |
| 在根目录创建 | 点击笔记树中的"+" |
| 快速创建 | Ctrl+O > 输入新名称 |

### 笔记属性

| 属性 | 描述 |
|----------|-------------|
| 标题 | 笔记名称 |
| 类型 | 笔记内容类型 |
| MIME | 内容 MIME 类型 |
| 创建时间 | 创建日期 |
| 修改时间 | 最后修改日期 |
| 笔记 ID | 唯一标识符 |
| 受保护 | 加密状态 |

### 富文本编辑器功能

| 功能 | 快捷键 | 描述 |
|---------|----------|-------------|
| 粗体 | Ctrl+B | 粗体文本 |
| 斜体 | Ctrl+I | 斜体文本 |
| 下划线 | Ctrl+U | 下划线文本 |
| 删除线 | Ctrl+Shift+S | 删除线 |
| 标题 | Ctrl+1-6 | 标题级别 |
| 无序列表 | Ctrl+Shift+8 | 项目符号 |
| 有序列表 | Ctrl+Shift+9 | 有序列表 |
| 复选框 | Ctrl+Shift+C | 任务复选框 |
| 行内代码 | Ctrl+` | 行内代码 |
| 代码块 | Ctrl+Shift+` | 代码块 |
| 链接 | Ctrl+L | 插入链接 |
| 表格 | - | 插入表格 |
| 图片 | - | 插入图片 |
| 数学公式 | - | LaTeX 数学公式 |

---

## 属性

### 什么是属性

属性是附加到笔记的元数据。它们提供属性、标签和关系，丰富你的笔记并启用高级功能。

### 属性类型

| 类型 | 前缀 | 示例 | 描述 |
|------|--------|---------|-------------|
| 标签 | `#` | `#favorite` | 简单标签或标志 |
| 带值标签 | `#` | `#priority=high` | 键值元数据 |
| 关系 | `~` | `~relatedNote` | 链接到另一笔记 |
| 带值关系 | `~` | `~author=NoteID` | 带值链接 |

### 内置属性

| 属性 | 类型 | 描述 |
|-----------|------|-------------|
| `#readOnly` | 标签 | 设为只读 |
| `#autoReadOnlyDisabled` | 标签 | 禁用自动只读 |
| `#hiddenLinks` | 标签 | 隐藏出站链接 |
| `#hidePromoted` | 标签 | 隐藏提升的属性 |
| `#cssClass` | 标签 | 自定义 CSS 类 |
| `#iconClass` | 标签 | 自定义图标 |
| `#color` | 标签 | 树中的笔记颜色 |
| `#run` | 标签 | 自动运行脚本 |
| `#sorted` | 标签 | 按字母排序子项 |
| `#top` | 标签 | 置顶 |
| `#excludeFromExport` | 标签 | 导出时跳过 |
| `#template` | 标签 | 标记为模板 |
| `#disableVersioning` | 标签 | 禁用笔记历史 |
| `#shareHiddenFromTree` | 标签 | 从共享树中隐藏 |
| `#shareAlias` | 标签 | 自定义分享 URL |

### 提升的属性

提升的属性显示在笔记的属性面板中，方便编辑。

```javascript
// 要提升属性，将其添加到笔记：
#priority(promoted, number)
#status(promoted, label=pending/in-progress/done)
#dueDate(promoted, date)
~assignedTo(promoted, relation)
```

### 属性继承

属性由子笔记继承：

| 行为 | 描述 |
|----------|-------------|
| 向下 | 子项继承父项属性 |
| 覆盖 | 子项可以覆盖继承的值 |
| 累积 | 可以存在多个值 |
| 深度优先 | 更近的父项优先 |

### 使用属性进行组织

| 系统 | 属性 | 描述 |
|--------|-----------|-------------|
| GTD | `#status=next/waiting/someday` | Getting Things Done |
| PARA | `#type=project/area/resource/archive` | PARA 方法 |
| Zettelkasten | `#type=fleeting/literature/permanent` | Zettelkasten 方法 |
| Cornell Notes | `#type=note/cue/summary` | Cornell 方法 |

---

## 关系

### 什么是关系

关系是笔记间的链接。与简单的超链接不同，关系是结构化的，可用于导航、脚本和可视化。

### 关系类型

| 类型 | 语法 | 描述 |
|------|--------|-------------|
| 出站 | `~targetNote` | 从本笔记出发 |
| 入站 | 显示在目标上 | 指向本笔记 |
| 双向 | 双向 | 相互关系 |

### 创建关系

| 方法 | 操作 |
|--------|--------|
| 自动完成 | 输入 `~` 并开始输入笔记名称 |
| 属性面板 | 在属性中添加关系 |
| 拖放 | 将笔记拖到关系图 |
| 脚本 | 使用 API 编程创建 |

### 内置关系

| 关系 | 描述 |
|----------|-------------|
| `~template` | 笔记使用此模板 |
| `~run` | 要运行的脚本 |
| `~iconClass` | 自定义图标类 |

### 关系图

关系图提供笔记关系的可视化图：

| 功能 | 描述 |
|---------|-------------|
| 可视化图 | 一览所有关系 |
| 拖动节点 | 重新排列布局 |
| 添加关系 | 在节点间画线 |
| 缩放和平移 | 导航大型图表 |
| 导出 | 保存为图片 |

---

## 脚本

### 脚本类型

| 类型 | 作用域 | 触发器 |
|------|-------|---------|
| 后端脚本 | 服务器端 | 手动、定时 |
| 前端脚本 | 客户端 | UI 事件 |
| 关系图脚本 | 可视化 | 手动 |
| 小部件 | 自定义 UI | 自动加载 |
| 自定义请求处理 | HTTP 端点 | HTTP 请求 |

### 后端脚本

```javascript
// 示例：列出具有特定标签的所有笔记
const notes = await api.searchForNotes('#status/todo');
for (const note of notes) {
    api.log(`Note: ${note.title}`);
}

// 示例：创建新笔记
const note = await api.createNote({
    parentNoteId: 'root',
    title: 'New Note',
    content: 'Hello, World!',
    type: 'text'
});

// 示例：更新笔记内容
const note = await api.getNote('noteId');
await note.setContent('Updated content');

// 示例：搜索笔记
const results = await api.searchForNotes({
    query: 'search term',
    ancestorNoteId: 'parentNoteId'
});
```

### 前端脚本

```javascript
// 示例：显示通知
api.showMessage('Hello from script!');

// 示例：获取当前笔记
const currentNote = api.getActiveTabNote();

// 示例：在新标签页打开笔记
api.openNoteInNewTab('noteId');

// 示例：监听事件
api.addEventListener('noteSwitched', ({noteId}) => {
    api.log(`Switched to note: ${noteId}`);
});
```

### 定时脚本

```javascript
// 设置定时脚本
// 使用 #run=backend 和 #schedule 属性

// 脚本笔记上的属性：
// #run=backend
// #schedule=daily 09:00

const notes = await api.searchForNotes('#reminder');
for (const note of notes) {
    // 处理提醒
    api.log(`Reminder: ${note.title}`);
}
```

### API 方法

| 方法 | 描述 |
|--------|-------------|
| `api.getNote(noteId)` | 按 ID 获取笔记 |
| `api.createNote(opts)` | 创建新笔记 |
| `api.updateNote(noteId, opts)` | 更新笔记 |
| `api.deleteNote(noteId)` | 删除笔记 |
| `api.searchForNotes(query)` | 搜索笔记 |
| `api.getNotePath(noteId)` | 获取笔记路径 |
| `api.log(message)` | 记录消息 |
| `api.showMessage(message)` | 显示 UI 消息 |
| `api.getActiveTabNote()` | 获取当前笔记 |
| `api.openNoteInNewTab(noteId)` | 打开笔记 |

---

## 同步

### 同步选项

| 方式 | 描述 | 最适合 |
|--------|-------------|----------|
| 内置同步 | Trilium 自己的同步协议 | 多设备 |
| 自托管同步 | 运行同步服务器 | 完全控制 |
| 文件同步 | 使用 Syncthing/rsync | 简单设置 |
| Web 访问 | 通过浏览器访问 | 任何设备 |

### 设置同步

#### 同步服务器设置

```bash
# 运行同步服务器
docker run -d \
  --name trilium-sync \
  --restart=always \
  -p 8081:8080 \
  -v trilium-sync-data:/home/node/trilium-data \
  triliumnext/notes:latest \
  --no-cert-check
```

#### 客户端配置

| 步骤 | 操作 |
|------|--------|
| 1 | 打开 Trilium 桌面应用 |
| 2 | 转到选项 > 同步 |
| 3 | 输入同步服务器 URL |
| 4 | 输入同步密码 |
| 5 | 等待初始同步 |

### 同步冲突解决

| 场景 | 解决方案 |
|----------|------------|
| 同一笔记被编辑 | 最后写入获胜 |
| 一侧删除笔记 | 删除传播 |
| 结构更改 | 结构合并 |
| 附件更改 | 最新版本获胜 |

### 基于文件的同步

```bash
# 使用 Syncthing
# 在所有设备上安装 Syncthing
# 将 Trilium 数据文件夹添加到 Syncthing
# 在所有设备上设为"发送和接收"

# 使用 rsync
rsync -avz ~/trilium-data/ user@remote:~/trilium-data/
```

---

## 分享

### 分享选项

| 类型 | 描述 | 访问 |
|------|-------------|--------|
| 单个笔记 | 分享一个笔记 | 直接 URL |
| 子树 | 分享笔记和子项 | 树视图 |
| 自定义布局 | 自定义 HTML | 嵌入 |

### 发布笔记

| 步骤 | 操作 |
|------|--------|
| 1 | 右键笔记 > 分享 |
| 2 | 选择分享类型 |
| 3 | 配置选项 |
| 4 | 获取分享 URL |

### 分享配置

| 设置 | 描述 |
|---------|-------------|
| 包含子项 | 分享子树 |
| 自定义 CSS | 设置分享页面样式 |
| 自定义头部 | 添加头部内容 |
| 自定义底部 | 添加底部内容 |
| 密码保护 | 需要密码 |
| 过期日期 | 自动过期分享 |

### 自定义分享主题

```css
/* 分享笔记的自定义 CSS */
body {
    font-family: 'Inter', sans-serif;
    max-width: 800px;
    margin: 0 auto;
    padding: 20px;
}

.note-content {
    line-height: 1.6;
}

h1 {
    color: #2563eb;
}
```

---

## 搜索

### 搜索方式

| 方式 | 描述 | 示例 |
|--------|-------------|---------|
| 全文 | 搜索笔记内容 | `search term` |
| 仅标题 | 搜索笔记标题 | `note.title=search` |
| 属性 | 按属性搜索 | `#tag` 或 `#key=value` |
| 关系 | 按关系搜索 | `~relation` |
| 路径 | 按路径搜索 | `path=/root/folder` |
| 正则 | 正则表达式 | `regex=/pattern/` |
| 快速搜索 | 快速查找 | Ctrl+O |

### 搜索语法

| 语法 | 描述 | 示例 |
|--------|-------------|---------|
| `text` | 全文搜索 | `machine learning` |
| `#label` | 有标签 | `#important` |
| `#key=value` | 带值标签 | `#status=active` |
| `~relation` | 有关系 | `~author` |
| `note.title=X` | 标题匹配 | `note.title=API` |
| `note.type=X` | 笔记类型 | `note.type=code` |
| `note.dateCreated>X` | 创建于之后 | `note.dateCreated>2024-01-01` |
| `note.dateModified>X` | 修改于之后 | `note.dateModified>LAST_WEEK` |
| `note.content=X` | 内容匹配 | `note.content=TODO` |
| `AND` | 逻辑与 | `#tag1 AND #tag2` |
| `OR` | 逻辑或 | `#tag1 OR #tag2` |
| `NOT` | 逻辑非 | `#tag NOT #exclude` |
| `*` | 通配符 | `program*` |

### 搜索快捷键

| 快捷键 | 操作 |
|----------|--------|
| Ctrl+O | 快速搜索（笔记切换器） |
| Ctrl+S | 在当前笔记中搜索 |
| Ctrl+Shift+F | 全局搜索 |

### 保存的搜索

```javascript
// 创建保存的搜索笔记
// 类型：search
// 内容：#status/todo AND #priority=high

// 这将创建匹配笔记的动态列表
// 随笔记变化自动更新
```

---

## 模板

### 什么是模板

模板是为新笔记定义默认属性、内容和行为的笔记。

### 创建模板

| 步骤 | 操作 |
|------|--------|
| 1 | 创建具有所需内容的笔记 |
| 2 | 添加 `#template` 标签 |
| 3 | 设置所需属性 |
| 4 | 在目标笔记上使用 `~template` 关系 |

### 模板结构

```markdown
## 模板：每日日志

#template
#iconClass="bx bx-calendar"

---

### 日期：${date}

### 任务
- [ ] 

### 笔记


### 反思


### 链接
- 上一篇：~previousDay
```

### 模板属性

| 属性 | 描述 |
|-----------|-------------|
| `#template` | 标记笔记为模板 |
| `#autoCreate` | 自动创建子笔记 |
| `#inherit` | 继承到子项 |
| `#clone` | 克隆而非引用 |

### 使用模板

| 方式 | 描述 |
|--------|-------------|
| 手动 | 将模板应用到笔记 |
| 自动 | 带 `#autoCreate` 的模板 |
| 继承 | 子项继承模板 |
| 克隆 | 复制模板内容 |

---

## API

### REST API

Trilium 提供 REST API 用于外部集成。

### API 端点

| 方法 | 端点 | 描述 |
|--------|----------|-------------|
| GET | /api/notes/{noteId} | 获取笔记 |
| POST | /api/create-note | 创建笔记 |
| PUT | /api/notes/{noteId} | 更新笔记 |
| DELETE | /api/notes/{noteId} | 删除笔记 |
| GET | /api/search | 搜索笔记 |
| GET | /api/notes/{noteId}/content | 获取笔记内容 |
| PUT | /api/notes/{noteId}/content | 设置笔记内容 |
| GET | /api/notes/{noteId}/attributes | 获取属性 |
| POST | /api/notes/{noteId}/attributes | 创建属性 |
| GET | /api/notes/{noteId}/relations | 获取关系 |
| POST | /api/notes/{noteId}/relations | 创建关系 |

### API 认证

```bash
# 在 Options > API 生成 API token
# 使用 ETAPI token 进行认证

curl -H "Authorization: YOUR_ETAPI_TOKEN" \
  http://localhost:8080/api/notes/root
```

### ETAPI（外部 API）

```python
import requests

BASE_URL = "http://localhost:8080"
TOKEN = "your_etapi_token"

headers = {
    "Authorization": TOKEN
}

# 获取笔记
response = requests.get(
    f"{BASE_URL}/api/notes/noteId",
    headers=headers
)

# 创建笔记
data = {
    "parentNoteId": "root",
    "title": "New Note",
    "type": "text",
    "content": "Hello from API!"
}
response = requests.post(
    f"{BASE_URL}/api/create-note",
    headers=headers,
    json=data
)
```

### WebSocket API

| 事件 | 描述 |
|-------|-------------|
| `noteCreated` | 创建新笔记 |
| `noteUpdated` | 笔记已修改 |
| `noteDeleted` | 笔记已删除 |
| `attributeChanged` | 属性已修改 |
| `syncStarted` | 同步已开始 |
| `syncCompleted` | 同步已完成 |

---

## 备份

### 备份方式

| 方式 | 描述 | 自动化 |
|--------|-------------|------------|
| 内置导出 | 导出为 ZIP | 手动 |
| 数据库复制 | 复制 SQLite 文件 | 脚本化 |
| Docker 卷 | 备份卷 | Docker 工具 |
| rsync | 增量复制 | Cron 任务 |

### 内置导出

| 导出类型 | 描述 | 格式 |
|-------------|-------------|--------|
| HTML | 导出为网页 | .html 文件 |
| Markdown | 导出为 markdown | .md 文件 |
| OPML | 导出大纲 | .opml |
| ZIP | 完整导出 | .zip 归档 |

### 自动备份脚本

```bash
#!/bin/bash
# backup-trilium.sh

BACKUP_DIR="/backups/trilium"
DATE=$(date +%Y%m%d_%H%M%S)
TRILIUM_DATA="/home/node/trilium-data"

# 创建备份目录
mkdir -p $BACKUP_DIR

# 复制数据库
cp $TRILIUM_DATA/document.db $BACKUP_DIR/document_$DATE.db

# 复制日志
cp $TRILIUM_DATA/log.db $BACKUP_DIR/log_$DATE.db

# 仅保留最近 30 个备份
ls -t $BACKUP_DIR/document_*.db | tail -n +31 | xargs -r rm

echo "备份完成：$DATE"
```

### 备份频率

| 频率 | 保留 | 存储 |
|-----------|-----------|---------|
| 每天 | 7 天 | 本地 |
| 每周 | 4 周 | 本地 + 远程 |
| 每月 | 12 个月 | 远程 |
| 重大更改前 | - | 本地 |

---

## 移动端访问

### 移动端访问选项

| 方式 | 描述 | 最适合 |
|--------|-------------|----------|
| Web 浏览器 | 通过浏览器访问 | 任何移动设备 |
| TriliumNext Mobile | 原生应用 | Android |
| PWA | 渐进式 Web 应用 | iOS、Android |

### Web 访问设置

| 步骤 | 操作 |
|------|--------|
| 1 | 在服务器上安装 Trilium |
| 2 | 配置反向代理（Nginx/Caddy） |
| 3 | 设置 SSL 证书 |
| 4 | 通过移动浏览器访问 |
| 5 | 添加到主屏幕 |

### Nginx 反向代理

```nginx
server {
    listen 443 ssl;
    server_name notes.example.com;

    ssl_certificate /etc/letsencrypt/live/notes.example.com/fullchain.pem;
    ssl_certificate_key /etc/letsencrypt/live/notes.example.com/privkey.pem;

    location / {
        proxy_pass http://localhost:8080;
        proxy_set_header Host $host;
        proxy_set_header X-Real-IP $remote_addr;
        proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
        proxy_set_header X-Forwarded-Proto $scheme;
        
        # WebSocket 支持
        proxy_http_version 1.1;
        proxy_set_header Upgrade $http_upgrade;
        proxy_set_header Connection "upgrade";
    }
}
```

### 移动端友好技巧

| 技巧 | 描述 |
|-----|-------------|
| 使用 PWA | 添加到主屏幕获得应用体验 |
| 启用离线 | 配置离线访问 |
| 使用书签 | 收藏常用笔记 |
| 简化 UI | 使用移动端优化主题 |
| 快速捕获 | 设置快速笔记创建 |

---

## 最佳实践

### 组织结构

| 结构 | 描述 | 最适合 |
|-----------|-------------|----------|
| 按主题 | 主题作为分支 | 研究 |
| 按项目 | 每个项目一个分支 | 工作 |
| 按时间 | 每日/每周/每月笔记 | 日记 |
| 按类型 | 笔记、任务等分开 | 混合使用 |

### 命名约定

| 约定 | 示例 | 用例 |
|-----------|---------|----------|
| 日期前缀 | 2024-01-15 会议笔记 | 按时间排序 |
| 类型前缀 | [PROJECT] 网站改版 | 分类 |
| 使用一致格式 | API - 认证指南 | 参考 |
| CamelCase | myNoteTitle | 通用 |

### 属性系统

| 用途 | 属性 | 描述 |
|---------|-----------|-------------|
| 状态 | `#status=todo/doing/done` | 任务跟踪 |
| 优先级 | `#priority=low/medium/high` | 优先级排序 |
| 类型 | `#type=note/reference/task` | 分类 |
| 日期 | `#dueDate=2024-01-15` | 截止日期 |
| 人员 | `~author`、`~assignedTo` | 人员 |

---

## 总结

Trilium 是构建个人知识库的强大工具。其分层结构结合属性和关系，提供了灵活的系统来组织任何类型的信息。

关键要点：
- 使用 Docker 或桌面应用轻松安装
- 使用笔记类型处理不同内容
- 利用属性进行元数据和组织
- 在笔记间创建关系形成知识图谱
- 使用脚本实现自动化
- 设置同步实现多设备访问
- 定期备份

从简单开始，随着知识库的增长逐步采用更高级的功能。


---
