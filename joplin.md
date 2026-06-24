# 使用 Joplin 进行笔记管理

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
