# Outline 文档平台

全面的 Outline 设置和使用指南，这是一个开源团队知识库和文档平台。

## 目录

- [安装](#installation)
- [配置](#configuration)
- [工作区](#workspaces)
- [文档](#documents)
- [集合](#collections)
- [搜索](#search)
- [分享](#sharing)
- [API](#api)
- [集成](#integrations)
- [权限](#permissions)
- [模板](#templates)
- [Markdown 支持](#markdown-support)

---

## 安装

### 前置要求

| 要求 | 最低版本 | 用途 |
|------|----------|------|
| Node.js | 18+ | 应用运行时 |
| PostgreSQL | 12+ | 主数据库 |
| Redis | 6+ | 缓存和实时事件 |
| Yarn | 1.22+ | 包管理器 |

### Docker 安装（推荐）

```bash
git clone https://github.com/outline/outline.git
cd outline
cp .env.sample .env
```

编辑 `.env` 文件配置，然后：

```bash
docker compose up -d
```

这将启动 Outline、PostgreSQL、Redis 和存储容器。

### 手动安装

```bash
git clone https://github.com/outline/outline.git
cd outline
yarn install --frozen-lockfile
yarn build
yarn start
```

### 环境变量

| 变量 | 必需 | 描述 |
|------|------|------|
| `SECRET_KEY` | 是 | 会话加密的随机字符串 |
| `UTILS_SECRET` | 是 | 工具加密的随机字符串 |
| `DATABASE_URL` | 是 | PostgreSQL 连接字符串 |
| `REDIS_URL` | 是 | Redis 连接字符串 |
| `URL` | 是 | 实例的公开 URL |
| `PORT` | 否 | 服务器端口（默认: 3000） |
| `FILE_STORAGE` | 否 | `local` 或 `s3` |
| `AWS_ACCESS_KEY_ID` | S3 | AWS S3 存储访问密钥 |
| `AWS_SECRET_ACCESS_KEY` | S3 | AWS S3 存储密钥 |
| `AWS_S3_UPLOAD_BUCKET_NAME` | S3 | S3 桶名称 |

### 认证提供商

Outline 支持多种认证方式：

| 提供商 | 环境变量 | 描述 |
|--------|----------|------|
| Slack | `SLACK_CLIENT_ID` | 通过 Slack 工作区 OAuth |
| Google | `GOOGLE_CLIENT_ID` | 通过 Google 账号 OAuth |
| Microsoft | `MICROSOFT_CLIENT_ID` | 通过 Azure AD OAuth |
| OIDC | `OIDC_CLIENT_ID` | 通用 OpenID Connect |
| SAML | `SAML_*` | 企业 SSO |

---

## 配置

### 常规设置

通过侧边栏访问管理设置：`Settings > Administration`。

| 设置 | 描述 |
|------|------|
| 团队名称 | 工作区的显示名称 |
| 团队图标 | 工作区的 logo/头像 |
| 默认语言 | 所有用户的界面语言 |
| 默认访问 | 新成员的默认文档可见性 |
| 公开分享 | 允许文档公开分享 |
| 访客分享 | 允许与外部访客分享 |

### 文件存储配置

| 存储类型 | 配置 |
|----------|------|
| 本地 | 文件存储在 `./data` 目录 |
| Amazon S3 | 在环境变量中配置桶、区域、凭据 |
| Google Cloud Storage | 使用 S3 兼容 API 连接 GCS |
| MinIO | 自托管 S3 兼容存储 |

### 邮件配置

| 变量 | 描述 |
|------|------|
| `SMTP_HOST` | SMTP 服务器主机名 |
| `SMTP_PORT` | SMTP 服务器端口 |
| `SMTP_USERNAME` | 认证用户名 |
| `SMTP_PASSWORD` | 认证密码 |
| `SMTP_FROM_EMAIL` | 发件人邮箱 |
| `SMTP_REPLY_EMAIL` | 回复邮箱 |

### 速率限制

| 设置 | 默认值 | 描述 |
|------|--------|------|
| `RATE_LIMITER_ENABLED` | false | 启用速率限制 |
| `RATE_LIMITER_REQUESTS` | 1000 | 每窗口最大请求数 |
| `RATE_LIMITER_DURATION_WINDOW` | 60 | 窗口持续时间（秒） |

---

## 工作区

工作区是团队知识库的顶级容器。

### 工作区设置

| 设置 | 描述 |
|------|------|
| 名称 | 团队或组织名称 |
| 图标 | 工作区 logo |
| 子域名 | 自定义子域名（如 team.getoutline.com） |
| 允许域名 | 允许加入的邮箱域名 |
| 邀请分享 | 允许成员邀请他人 |
| 成员默认角色 | 分配给新成员的角色 |

### 管理成员

| 操作 | 方法 |
|------|------|
| 通过邮箱邀请 | Settings > Members > Invite |
| 通过链接邀请 | Settings > Members > Invite Link |
| 更改角色 | 点击成员 > 选择新角色 |
| 移除成员 | 点击成员 > Remove |
| 停用 | 点击成员 > Deactivate |

### 成员角色

| 角色 | 权限 |
|------|------|
| Viewer | 只读访问共享文档 |
| Member | 在共享集合中创建和编辑文档 |
| Admin | 完整工作区管理、成员邀请 |
| Owner | 所有管理员权限加计费和删除 |

---

## 文档

文档是 Outline 的核心内容单元。

### 创建文档

| 方式 | 方法 |
|------|------|
| 新建文档按钮 | 点击侧边栏 `+` |
| 快捷键 | 按 `Ctrl + N` |
| 从模板 | 创建时选择模板 |
| 导入 | 拖放 `.md`、`.docx` 或 `.txt` 文件 |

### 文档编辑器

编辑器是支持 Markdown 快捷键的块级富文本编辑器。

| 功能 | 方法 |
|------|------|
| 标题 | 输入 `#`、`##`、`###` 后加空格 |
| 粗体 | 选中文本按 `Ctrl + B` |
| 斜体 | 选中文本按 `Ctrl + I` |
| 行内代码 | 用反引号包裹文本 |
| 链接 | 选中文本按 `Ctrl + K` |
| 图片 | 从剪贴板粘贴或拖放 |
| 清单 | 输入 `[]` 后加空格 |
| 表格 | 输入 `/table` 或使用斜杠命令 |
| 分隔线 | 输入 `---` |
| 代码块 | 输入三个反引号或 `/code` |
| 嵌入 | 粘贴 URL 或使用 `/embed` |

### 文档操作

| 操作 | 方法 |
|------|------|
| 归档 | 移至归档（可恢复） |
| 删除 | 移至回收站（30 天内可恢复） |
| 移动 | 拖到其他集合或使用移动选项 |
| 复制 | 创建文档副本 |
| 置顶 | 置顶到集合顶部 |
| 收藏 | 添加到个人收藏列表 |
| 打印 | File > Print |
| 导出 | 下载为 Markdown、PDF 或 HTML |

### 文档属性

| 属性 | 描述 |
|------|------|
| 创建者 | 文档作者 |
| 创建时间 | 创建时间戳 |
| 最后编辑者 | 最近编辑者 |
| 最后编辑时间 | 最后编辑时间戳 |
| 字数 | 大约字数 |
| 协作者 | 编辑过文档的用户 |

### 版本历史

Outline 追踪所有文档变更：

1. 打开文档。
2. 点击顶部栏的时钟图标。
3. 按日期浏览历史版本。
4. 点击版本预览。
5. 如需要可恢复版本。

---

## 集合

集合是层级组织文档的文件夹。

### 创建集合

1. 点击侧边栏 Collections 旁的 `+`。
2. 输入集合名称。
3. 选择图标和颜色。
4. 设置权限（私有或工作区范围）。
5. 点击 `Create`。

### 集合类型

| 类型 | 可见性 | 用途 |
|------|--------|------|
| Private | 仅受邀成员 | 敏感文档 |
| Workspace | 所有工作区成员 | 共享团队知识 |
| Public | 有链接的任何人 | 外部文档 |

### 集合结构

集合支持嵌套文档（子文档）：

```
Engineering (Collection)
  Getting Started
  Architecture Overview
    Frontend
    Backend
    Database
  Deployment Guide
  API Documentation
```

### 集合设置

| 设置 | 描述 |
|------|------|
| 排序 | 字母、手动或最近更新 |
| 分享 | 控制谁可以访问 |
| 索引 | 手动排序文档 |
| 删除 | 删除集合及所有文档 |

---

## 搜索

Outline 提供跨所有可访问文档的全文搜索。

### 搜索功能

| 功能 | 描述 |
|------|------|
| 全文搜索 | 搜索文档标题和内容 |
| 即时结果 | 输入时显示结果 |
| 筛选 | 按集合、作者、日期筛选 |
| 最近搜索 | 快速重复之前的搜索 |
| 快捷键 | `Ctrl + K` 或 `/` 聚焦搜索 |

### 搜索运算符

| 运算符 | 示例 | 描述 |
|--------|------|------|
| `collection:` | `collection:Engineering` | 在集合中搜索 |
| `author:` | `author:John` | 按文档作者搜索 |
| `created:` | `created:2024-01-01` | 按创建日期筛选 |
| `updated:` | `updated:>2024-06-01` | 按更新日期筛选 |

### 搜索技巧

- 使用具体词语而非常见词。
- 组合运算符获得精确结果。
- 结果按相关性和时间排序。
- 你有权访问的文档会包含在结果中。

---

## 分享

### 内部分享

| 方式 | 方法 |
|------|------|
| 分享链接 | 点击 Share 按钮，复制链接 |
| 提及 | 在文档中输入 `@username` |
| 集合访问 | 将用户添加到集合权限 |

### 公开分享

1. 打开文档。
2. 点击 `Share`。
3. 切换 `Share publicly`。
4. 复制公开链接。

公开文档为只读，无需认证即可访问。

| 设置 | 描述 |
|------|------|
| 公开链接 | 任何人都可访问的 URL |
| 包含嵌套文档 | 公开分享子文档 |
| 撤销 | 禁用公开访问 |

### 访客访问

邀请外部协作者而不给予完整工作区访问权限：

1. 前往 `Settings > Members`。
2. 点击 `Invite` 并输入访客邮箱。
3. 选择 `Guest` 角色。
4. 选择要分享的特定集合。

### 分享链接设置

| 设置 | 描述 |
|------|------|
| 链接过期 | 设置过期日期 |
| 密码保护 | 需要密码查看 |
| 允许下载 | 允许 PDF/Markdown 下载 |

---

## API

Outline 提供 RESTful API 用于程序化访问。

### 认证

所有 API 请求需要个人 API token：

1. 前往 `Settings > API`。
2. 点击 `Create Token`。
3. 复制 token。

在请求中包含 token：

```
Authorization: Bearer YOUR_API_TOKEN
```

### API 端点

| 端点 | 方法 | 描述 |
|------|------|------|
| `/api/documents.list` | POST | 列出所有文档 |
| `/api/documents.info` | POST | 获取文档详情 |
| `/api/documents.create` | POST | 创建文档 |
| `/api/documents.update` | POST | 更新文档 |
| `/api/documents.delete` | POST | 删除文档 |
| `/api/documents.search` | POST | 搜索文档 |
| `/api/collections.list` | POST | 列出集合 |
| `/api/collections.create` | POST | 创建集合 |
| `/api/collections.info` | POST | 获取集合详情 |
| `/api/users.list` | POST | 列出工作区用户 |

### 示例：创建文档

```bash
curl -X POST https://your-outline.com/api/documents.create \
  -H "Authorization: Bearer YOUR_TOKEN" \
  -H "Content-Type: application/json" \
  -d '{
    "title": "API Created Document",
    "text": "# Hello\nThis document was created via API.",
    "collectionId": "COLLECTION_ID",
    "publish": true
  }'
```

### 速率限制

| 限制 | 值 |
|------|-----|
| 每分钟请求数 | 100/token |
| 负载大小 | 10 MB |

---

## 集成

### 内置集成

| 集成 | 描述 | 配置 |
|------|------|------|
| Slack | 搜索、分享和接收通知 | 在设置中添加 Slack 应用 |
| Google Drive | 嵌入 Google Docs、Sheets | 粘贴 Google URL |
| Figma | 嵌入 Figma 设计 | 粘贴 Figma URL |
| Loom | 嵌入 Loom 视频 | 粘贴 Loom URL |
| Lucidchart | 嵌入图表 | 粘贴 Lucidchart URL |

### Slack 集成

| 功能 | 描述 |
|------|------|
| `/outline search` | 从 Slack 搜索文档 |
| 链接预览 | 在 Slack 中预览 Outline 链接 |
| 通知 | 在频道接收文档更新 |
| 自动发布 | 将新文档发布到频道 |

### Webhook 集成

配置 webhook 接收事件：

1. 前往 `Settings > Webhooks`。
2. 点击 `Add Webhook`。
3. 输入目标 URL。
4. 选择要订阅的事件。

| 事件 | 触发 |
|------|------|
| `documents.create` | 新文档创建 |
| `documents.update` | 文档编辑 |
| `documents.delete` | 文档删除 |
| `collections.create` | 新集合创建 |
| `users.create` | 新用户加入 |

### Zapier 集成

通过 Zapier 将 Outline 连接到 5000+ 应用：

| 触发 | 动作 |
|------|------|
| 新文档 | 创建 Trello 卡片 |
| 文档更新 | 发送 Slack 消息 |
| 新集合 | 创建 Notion 页面 |

---

## 权限

### 权限级别

| 级别 | 描述 |
|------|------|
| 读取 | 查看文档内容 |
| 读写 | 查看和编辑文档 |
| Admin | 管理集合设置和成员 |

### 集合权限

| 设置 | 选项 |
|------|------|
| 谁可以查看 | 所有人、特定组、受邀用户 |
| 谁可以编辑 | 所有人、特定组、受邀用户 |
| 谁可以管理 | 仅管理员 |
| 嵌套文档继承 | 子文档继承父文档权限 |

### 文档级权限

文档可以拥有独立于集合的权限：

| 设置 | 描述 |
|------|------|
| Public | 有链接的任何人都可查看 |
| Invite-only | 仅明确受邀用户 |
| Collection default | 从父集合继承 |

### 权限继承

```
Collection (Edit: Team A)
  Document A (inherits Collection)
  Document B (Custom: Team B only)
  Document C (Public)
```

### 组

创建组以高效管理权限：

1. 前往 `Settings > Groups`。
2. 创建组（如 "Engineering"、"Marketing"）。
3. 添加成员到组。
4. 将组分配到集合权限。

---

## 模板

模板提供可复用的文档结构。

### 创建模板

1. 创建具有所需结构的文档。
2. 点击 `...` 菜单。
3. 选择 `Save as template`。
4. 命名模板。

### 模板功能

| 功能 | 描述 |
|------|------|
| 占位文本 | 用示例文本引导内容 |
| 结构化标题 | 预定义的章节标题 |
| 清单 | 可复用的任务列表 |
| 表格 | 预格式化的数据表 |
| 变量 | 使用 `{{variable}}` 实现动态内容 |

### 使用模板

| 方式 | 方法 |
|------|------|
| 新文档 | 从下拉菜单选择模板 |
| 现有文档 | 插入模板内容 |
| 斜杠命令 | 在编辑器中输入 `/template` |

### 模板管理

| 操作 | 方法 |
|------|------|
| 查看所有模板 | Settings > Templates |
| 编辑模板 | 打开模板，进行修改 |
| 删除模板 | 模板列表 > Delete |
| 复制模板 | 模板列表 > Duplicate |

### 默认模板

为集合设置默认模板：

1. 打开集合设置。
2. 选择 `Default template`。
3. 选择模板。

此集合中的新文档将从模板内容开始。

---

## Markdown 支持

Outline 的编辑器支持 Markdown 语法，便于快速创建内容。

### 支持的语法

| 元素 | 语法 | 结果 |
|------|------|------|
| 标题 1 | `# H1` | 大标题 |
| 标题 2 | `## H2` | 中标题 |
| 标题 3 | `### H3` | 小标题 |
| 粗体 | `**text**` | **粗体文本** |
| 斜体 | `*text*` | *斜体文本* |
| 删除线 | `~~text~~` | ~~删除线~~ |
| 行内代码 | `` `code` `` | `code` |
| 代码块 | ``` ``` | 代码块 |
| 链接 | `[text](url)` | 超链接 |
| 图片 | `![alt](url)` | 内联图片 |
| 引用 | `> text` | 引用文本 |
| 有序列表 | `1. item` | 编号列表 |
| 无序列表 | `- item` | 项目列表 |
| 清单 | `[] item` | 复选框 |
| 水平线 | `---` | 分隔线 |
| 表格 | 见下文 | 数据表 |

### 表格语法

```markdown
| Header 1 | Header 2 | Header 3 |
|---|---|---|
| Cell 1 | Cell 2 | Cell 3 |
| Cell 4 | Cell 5 | Cell 6 |
```

### 斜杠命令

在编辑器中输入 `/` 访问块命令：

| 命令 | 描述 |
|------|------|
| `/heading1` | 插入 H1 标题 |
| `/heading2` | 插入 H2 标题 |
| `/bullet-list` | 插入项目列表 |
| `/ordered-list` | 插入编号列表 |
| `/checklist` | 插入清单 |
| `/code` | 插入代码块 |
| `/table` | 插入表格 |
| `/blockquote` | 插入引用 |
| `/hr` | 插入水平线 |
| `/image` | 插入图片 |
| `/embed` | 嵌入外部内容 |
| `/template` | 插入模板 |

### Markdown 快捷键

| 快捷键 | 操作 |
|--------|------|
| `Ctrl + B` | 粗体 |
| `Ctrl + I` | 斜体 |
| `Ctrl + K` | 插入链接 |
| `Ctrl + Shift + C` | 行内代码 |
| `Ctrl + Shift + H` | 循环标题级别 |
| `Ctrl + Shift + 7` | 有序列表 |
| `Ctrl + Shift + 8` | 无序列表 |
| `Ctrl + Shift + 9` | 清单 |
| `Ctrl + ]` | 缩进 |
| `Ctrl + [` | 减少缩进 |

### 导入 Markdown

直接导入 `.md` 文件：

1. 将 `.md` 文件拖放到 Outline 中。
2. 或使用 `File > Import > Markdown`。
3. 文档保留标题、列表、表格和链接。
