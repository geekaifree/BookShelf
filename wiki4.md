# Wiki.js：现代 Wiki 平台教程

## 简介

Wiki.js 是一个基于 Node.js 构建的现代开源 Wiki 引擎。它具有简洁的界面、多种存储后端和强大的搜索功能。本教程涵盖安装、内容创建、访问控制和管理。

## Wiki.js 与其他 Wiki 对比

| 功能 | Wiki.js | MediaWiki | DokuWiki | Confluence |
|------|---------|-----------|----------|------------|
| 语言 | Node.js | PHP | PHP | Java |
| 数据库 | PostgreSQL、MySQL、SQLite、MSSQL | MySQL/PostgreSQL | 扁平文件 | PostgreSQL |
| Markdown | 是 | Wikitext | 是 | 是 |
| 所见即所得 | 是 | 有限 | 有限 | 是 |
| Git 同步 | 是 | 扩展 | 扩展 | 否 |
| LDAP/SAML | 是 | 扩展 | 扩展 | 是 |
| 搜索 | 内置、Algolia、Elasticsearch | 扩展 | 扩展 | 内置 |
| 开源 | 是 | 是 | 是 | 否 |

## 系统要求

| 组件 | 最低要求 | 推荐配置 |
|------|---------|---------|
| Node.js | 18.x | 20.x LTS |
| 数据库 | SQLite | PostgreSQL 14+ |
| 内存 | 512 MB | 2 GB |
| 磁盘 | 1 GB | 10 GB |
| 操作系统 | Linux、Windows、macOS | Linux |

## 安装

### Docker

```bash
docker run -d \
  --name wiki \
  -p 3000:3000 \
  -e DB_TYPE=sqlite \
  -e DB_FILEPATH=/data/wiki.sqlite \
  -v wiki-data:/data \
  ghcr.io/requarks/wiki:2
```

### Docker Compose

```yaml
version: '3'
services:
  wiki:
    image: ghcr.io/requarks/wiki:2
    container_name: wikijs
    restart: unless-stopped
    depends_on:
      - db
    environment:
      - DB_TYPE=postgres
      - DB_HOST=db
      - DB_PORT=5432
      - DB_USER=wikijs
      - DB_PASS=secret
      - DB_NAME=wikijs
    ports:
      - "3000:3000"
    volumes:
      - wiki-data:/data

  db:
    image: postgres:15-alpine
    container_name: wikijs-db
    restart: unless-stopped
    environment:
      - POSTGRES_DB=wikijs
      - POSTGRES_USER=wikijs
      - POSTGRES_PASSWORD=secret
    volumes:
      - db-data:/var/lib/postgresql/data

volumes:
  wiki-data:
  db-data:
```

## 内容管理

### 页面结构

| 组件 | 描述 |
|------|------|
| Title | 页面显示名称 |
| Path | URL 路径（如 /guides/getting-started） |
| Content | Markdown 或 HTML 内容 |
| Tags | 分类标签 |
| Editor | Markdown、所见即所得或原始 HTML |
| Locale | 页面语言 |

### 创建页面

1. 在侧边栏点击"New Page"。
2. 选择编辑器模式。
3. 设置页面路径。
4. 编写内容。
5. 添加标签。
6. 点击"Create"。

### 编辑器选项

| 编辑器 | 最佳用途 |
|--------|---------|
| Markdown | 技术内容、开发者 |
| WYSIWYG | 通用用户、富文本格式 |
| Raw HTML | 自定义布局、嵌入内容 |

### 页面操作

| 操作 | 方法 |
|------|------|
| 创建 | 侧边栏 > New Page |
| 编辑 | 点击页面上的编辑图标 |
| 移动 | 页面设置 > 更改路径 |
| 删除 | 页面设置 > Delete |
| 复制 | 页面设置 > Duplicate |
| 历史 | 页面菜单 > Page History |
| 导出 | 页面菜单 > Export |

## 侧边栏导航

### 导航结构

| 级别 | 类型 | 示例 |
|------|------|------|
| 根级 | 文件夹 | Documentation |
| 1 级 | 文件夹 | Guides |
| 2 级 | 页面 | Getting Started |
| 2 级 | 页面 | Installation |

### 导航类型

| 类型 | 用途 |
|------|------|
| Page | 直接页面链接 |
| Folder | 页面组 |
| Divider | 可视分隔线 |
| Header | 区域标签 |
| External Link | 外部网站 URL |

## 访问控制

### 权限模型

| 级别 | 范围 |
|------|------|
| Global | 系统级设置 |
| Group | 团队级权限 |
| Page | 单个页面访问 |
| Path | 文件夹级权限 |

### 角色

| 角色 | 默认权限 |
|------|---------|
| Admin | 完全系统访问 |
| Editor | 创建和编辑所有页面 |
| Viewer | 只读访问 |
| Guest | 有限读取访问 |

### 页面权限

| 权限 | 描述 |
|------|------|
| Read | 查看页面内容 |
| Write | 编辑页面内容 |
| Create | 添加子页面 |
| Delete | 删除页面 |
| Manage | 更改页面设置 |

## 存储后端

| 后端 | 用例 |
|------|------|
| Local Filesystem | 简单单服务器设置 |
| Git | 版本控制、协作 |
| S3 | 云存储、可扩展性 |
| Azure Blob | Microsoft 云存储 |
| DigitalOcean Spaces | 对象存储 |

### Git 同步

| 方向 | 行为 |
|------|------|
| Push | 本地更改推送到远程仓库 |
| Pull | 远程更改拉取到本地 |
| Bidirectional | 双向同步 |

## 搜索

### 内置搜索

| 功能 | 描述 |
|------|------|
| Full-text | 搜索页面内容 |
| Tags | 按标签过滤 |
| Paths | 按 URL 路径搜索 |
| Locale | 特定语言结果 |

### 外部搜索引擎

| 引擎 | 设置 |
|------|------|
| Algolia | API key 配置 |
| Elasticsearch | 连接 URL |
| MeiliSearch | API key 和 URL |
| MS SQL Fulltext | SQL Server 集成 |

## 主题

### 内置主题

| 主题 | 风格 |
|------|------|
| Default | 简洁、现代 |
| Docs | 文档导向 |
| Hero | 着陆页风格 |

### 自定义 CSS

在 Administration > Theme > Custom CSS 中覆盖样式。

## 模块

### 可用模块

| 模块 | 用途 |
|------|------|
| Authentication | LDAP、SAML、OAuth、Local |
| Storage | Git、S3、Azure、Local |
| Editor | Markdown、WYSIWYG、Raw HTML |
| Search | 内置、Algolia、Elasticsearch |
| Rendering | Markdown、AsciiDoc、LaTeX |
| Analytics | Google Analytics、Matomo |
| Notification | Email、Slack、webhooks |
| Commenting | 内置、Disqus、Giscus |

## Markdown 扩展

### 标准 Markdown

| 语法 | 结果 |
|------|------|
| # Heading | H1 标题 |
| **bold** | 粗体文本 |
| *italic* | 斜体文本 |
| [link](url) | 超链接 |
| ![alt](url) | 图片 |
| \`code\` | 行内代码 |
| > blockquote | 引用块 |

### Wiki.js 扩展

| 扩展 | 语法 | 用途 |
|------|------|------|
| Alerts | > [!NOTE] | 提示框 |
| Tabs | \`\`\`tabs | 标签页内容 |
| Math | $$LaTeX$$ | 数学公式 |
| Mermaid | \`\`\`mermaid | 图表 |
| Embeds | {{embed}} | 嵌入外部内容 |

## 备份与恢复

### 备份方法

| 方法 | 命令 |
|------|------|
| 数据库导出 | pg_dump、mysqldump |
| Git 同步 | 使用 Git 存储时自动 |
| 文件备份 | 复制数据卷 |
| 导出 | 内置页面导出 |

### 恢复

| 步骤 | 操作 |
|------|------|
| 1 | 停止 Wiki.js 服务 |
| 2 | 从导出恢复数据库 |
| 3 | 恢复文件存储 |
| 4 | 启动服务 |
| 5 | 验证内容完整性 |

## API

### GraphQL API

Wiki.js 使用 GraphQL 作为其 API。

```graphql
query {
  pages {
    list(limit: 10, orderBy: CREATED) {
      id
      title
      path
      createdAt
    }
  }
}
```

### 认证

```bash
# API key 认证
curl -H "Authorization: Bearer YOUR_API_KEY" \
  -X POST https://wiki.example.com/graphql \
  -d '{"query": "{ pages { list { id title } } }"}'
```

## 快捷键

| 快捷键 | 操作 |
|--------|------|
| Ctrl+S | 保存页面 |
| Ctrl+E | 编辑页面 |
| Ctrl+Shift+E | 切换编辑器模式 |
| / | 聚焦搜索 |
| Ctrl+K | 插入链接 |
| Ctrl+Shift+M | 插入公式 |

## 总结

Wiki.js 提供了一个现代化的功能丰富的 Wiki 平台，具有灵活的存储后端、多种编辑器选项和全面的访问控制。其 Node.js 架构、GraphQL API 和 Git 同步使其适合技术文档、知识库和团队协作。
