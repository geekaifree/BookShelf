# Wiki 平台

> 本文档整合了以下源文件：wiki.md, wiki4.md, mediawiki.md, xwiki.md, tiddly.md, doku.md

---

## 来源：wiki.md

## 简介

BookStack 是一个开源的、自托管的文档和知识组织存储平台。它使用简单的书架、书籍、章节和页面层次结构来组织内容。本教程涵盖设置、内容组织、权限和自定义。

## 架构

| 组件 | 技术 | 用途 |
|------|------|------|
| 后端 | Laravel (PHP) | 应用框架 |
| 数据库 | MySQL/MariaDB | 内容和用户存储 |
| 搜索 | 内置 / Meilisearch | 全文搜索 |
| 前端 | Blade 模板 | Web 界面 |
| API | REST 端点 | 编程访问 |

## 安装

### Docker Compose

```yaml
version: "3"
services:
  bookstack:
    image: lscr.io/linuxserver/bookstack:latest
    ports:
      - "80:80"
    environment:
      - APP_URL=https://docs.example.com
      - DB_HOST=mariadb
      - DB_DATABASE=bookstack
      - DB_USERNAME=bookstack
      - DB_PASSWORD=secure_password
    volumes:
      - bookstack_data:/config
    depends_on:
      - mariadb
  mariadb:
    image: lscr.io/linuxserver/mariadb:latest
    environment:
      - MYSQL_ROOT_PASSWORD=root_password
      - MYSQL_DATABASE=bookstack
      - MYSQL_USER=bookstack
      - MYSQL_PASSWORD=secure_password
    volumes:
      - mariadb_data:/config
volumes:
  bookstack_data:
  mariadb_data:
```

### 手动安装

```bash
git clone https://github.com/BookStackApp/BookStack.git --branch release --single-branch
cd BookStack
composer install --no-dev
cp .env.example .env
php artisan key:generate
php artisan migrate
```

## 内容层次

### 结构层级

| 层级 | 描述 | 示例 |
|------|------|------|
| Shelf（书架） | 顶级分组 | "工程文档" |
| Book（书籍） | 主要主题领域 | "后端服务" |
| Chapter（章节） | 子主题分组 | "API 文档" |
| Page（页面） | 单独文档 | "认证指南" |

### 层次图

```
Shelf: Engineering
  Book: Backend Services
    Chapter: API Documentation
      Page: Authentication Guide
      Page: Rate Limiting
      Page: Error Codes
    Chapter: Database
      Page: Schema Design
      Page: Migrations
  Book: Frontend
    Chapter: Components
      Page: Button Component
      Page: Modal Component
```

## 创建内容

### 创建书架

1. 点击侧边栏中的"Shelves"。
2. 点击"Create New Shelf"。
3. 输入名称和描述。
4. 选择要包含的书籍。
5. 保存书架。

### 创建书籍

1. 点击侧边栏中的"Books"。
2. 点击"Create New Book"。
3. 输入名称和描述。
4. 可选择分配到书架。
5. 保存书籍。

### 创建页面

| 步骤 | 操作 |
|------|------|
| 1 | 导航到书籍或章节 |
| 2 | 点击"Create New Page" |
| 3 | 输入页面标题 |
| 4 | 使用编辑器编写内容 |
| 5 | 设置页面模板（可选） |
| 6 | 保存为草稿或发布 |

## 编辑器

### 所见即所得编辑器

默认的可视化编辑器提供富文本编辑。

| 功能 | 描述 |
|------|------|
| 标题 | H1 到 H6 |
| 文本格式 | 粗体、斜体、下划线、删除线 |
| 列表 | 有序、无有序、复选框 |
| 链接 | 内部和外部链接 |
| 图片 | 上传和嵌入图片 |
| 代码块 | 语法高亮的代码 |
| 表格 | 创建和编辑表格 |
| 提示框 | 信息、警告、成功、危险框 |

### Markdown 编辑器

适合喜欢用 Markdown 写作的用户。

```markdown
# 标题 1
## 标题 2

**粗体文本**和*斜体文本*

- 无序列表
- 另一项

1. 有序列表
2. 另一项

[链接文本](https://example.com)

![替代文本](图片URL)

> 这是引用块

```javascript
const code = "带语法高亮";
```
```

### 编辑器对比

| 功能 | 所见即所得 | Markdown |
|------|-----------|----------|
| 易用性 | 高 | 中 |
| 格式化 | 可视化工具栏 | 基于语法 |
| 代码块 | 点击插入 | 三个反引号 |
| 图片 | 拖拽 | 粘贴或输入 URL |
| 表格 | 可视化编辑器 | 管道语法 |

## 模板

### 页面模板

创建可复用的模板以保持页面结构一致。

```html
<h2>概述</h2>
<p>此服务的简要描述。</p>

<h2>前提条件</h2>
<ul>
  <li>要求 1</li>
  <li>要求 2</li>
</ul>

<h2>设置说明</h2>
<ol>
  <li>步骤 1</li>
  <li>步骤 2</li>
</ol>

<h2>配置</h2>
<table>
  <tr><th>选项</th><th>描述</th><th>默认值</th></tr>
  <tr><td>option1</td><td>描述</td><td>value</td></tr>
</table>

<h2>故障排除</h2>
<p>常见问题和解决方案。</p>
```

### 模板管理

| 操作 | 步骤 |
|------|------|
| 创建模板 | Settings > Templates > Create Template |
| 分配到书籍 | 书籍设置 > Default Template |
| 在页面中使用 | 页面编辑器 > 选择模板 |

## 权限

### 权限层级

| 层级 | 范围 | 控制 |
|------|------|------|
| System | 全局 | 管理员访问、系统设置 |
| Shelf | 每个书架 | 查看、编辑、创建书籍 |
| Book | 每本书 | 查看、编辑、创建页面 |
| Chapter | 每个章节 | 查看、编辑页面 |
| Page | 每个页面 | 查看、编辑特定页面 |

### 角色权限

| 权限 | 描述 |
|------|------|
| View | 对内容的读取访问 |
| Create | 添加新内容 |
| Edit | 修改现有内容 |
| Delete | 删除内容 |
| Manage | 更改设置和权限 |

### 默认角色

| 角色 | 描述 |
|------|------|
| Admin | 完全系统访问 |
| Editor | 创建和编辑所有内容 |
| Viewer | 只读访问 |
| Public | 未认证访问（如启用） |

## 搜索

### 内置搜索

从搜索栏搜索所有内容。

| 搜索功能 | 语法 | 示例 |
|----------|------|------|
| 全文 | 简单词语 | `authentication setup` |
| 精确短语 | 引号 | `"API key rotation"` |
| 页面名称 | `name:` | `name:deployment` |
| 内容类型 | `type:` | `type:page` |

### Meilisearch 集成

用于在大型实例上提升搜索性能。

```yaml
# .env
SCOUT_DRIVER=meilisearch
MEILISEARCH_HOST=http://meilisearch:7700
MEILISEARCH_KEY=your-master-key
```

## API 访问

### 认证

```bash
# 在用户设置中创建 API token
curl -H "Authorization: Token YOUR_API_TOKEN" \
  https://docs.example.com/api/pages
```

### API 端点

| 端点 | 方法 | 描述 |
|------|------|------|
| `/api/books` | GET | 列出所有书籍 |
| `/api/books/{id}` | GET | 获取书籍 |
| `/api/pages` | GET | 列出所有页面 |
| `/api/pages/{id}` | GET | 获取页面 |
| `/api/pages` | POST | 创建页面 |
| `/api/pages/{id}` | PUT | 更新页面 |
| `/api/chapters` | GET | 列出所有章节 |
| `/api/shelves` | GET | 列出所有书架 |
| `/api/search` | GET | 搜索内容 |

### 通过 API 创建页面

```bash
curl -X POST https://docs.example.com/api/pages \
  -H "Authorization: Token YOUR_API_TOKEN" \
  -H "Content-Type: application/json" \
  -d '{
    "book_id": 1,
    "chapter_id": 5,
    "name": "New API Page",
    "html": "<p>Content created via API</p>",
    "tags": [
      {"name": "api", "value": "generated"}
    ]
  }'
```

## 附件和图片

### 图片上传

| 方法 | 描述 |
|------|------|
| 编辑器上传 | 点击图片图标，选择文件 |
| 拖拽 | 将图片拖入编辑器 |
| URL 嵌入 | 粘贴图片 URL |
| 图库 | 复用已上传的图片 |

### 文件附件

| 功能 | 描述 |
|------|------|
| 上传文件 | 将文档附加到页面 |
| 内联链接 | 在内容中链接到附件 |
| 外部链接 | 链接到外部文件 |
| 版本跟踪 | 保留附件历史 |

## 自定义

### 主题

```
themes/
  mytheme/
    info.json
    views/
    translations/
    assets/
```

### 自定义 CSS

在 Settings > Customization > Custom HTML Head 中添加自定义样式。

```css
/* 自定义样式 */
.markdown-section h2 {
    border-bottom: 2px solid #0073aa;
    padding-bottom: 8px;
}

.page-content table {
    border-collapse: collapse;
    width: 100%;
}
```

## 回收站

删除的内容会进入回收站。

| 操作 | 描述 |
|------|------|
| 软删除 | 移动到回收站 |
| 恢复 | 恢复已删除内容 |
| 永久删除 | 从回收站移除 |
| 自动清理 | 配置自动清理 |

## 备份

### 备份组件

| 组件 | 方法 |
|------|------|
| 数据库 | mysqldump 或 pg_dump |
| 上传文件 | 复制 uploads/ 目录 |
| .env | 备份配置文件 |

### 自动备份脚本

```bash
#!/bin/bash
BACKUP_DIR="/backups/bookstack/$(date +%Y%m%d)"
mkdir -p "$BACKUP_DIR"

# 数据库备份
docker exec mariadb mysqldump -u root -p$ROOT_PASSWORD bookstack > "$BACKUP_DIR/database.sql"

# 文件备份
tar czf "$BACKUP_DIR/uploads.tar.gz" /path/to/bookstack/uploads/

# 清理旧备份
find /backups/bookstack -maxdepth 1 -mtime +30 -exec rm -rf {} \;
```

## 总结

BookStack 提供了一个结构化的文档平台，具有清晰的书架、书籍、章节和页面层次结构。它支持丰富的内容编辑、细粒度的权限控制、API 访问和自定义。使用它构建知识库、团队 Wiki 或产品文档站点，拥有整洁有序的界面。


---

## 来源：wiki4.md

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


---

## 来源：mediawiki.md

## 简介

MediaWiki 是驱动 Wikipedia 的开源 Wiki 软件。它提供了一个用于协作内容创建和知识管理的平台。

### 什么是 MediaWiki？

MediaWiki 是一个强大的 Wiki 引擎，专为处理大量内容和多个贡献者而设计。它支持 Wiki 标记、模板和广泛的自定义。

| 特性 | 描述 |
|------|------|
| Wiki 标记 | 简单的内容格式化 |
| 版本历史 | 跟踪所有更改 |
| 用户管理 | 多用户协作 |
| 模板 | 可重用内容块 |
| 扩展 | 可扩展功能 |

### 与其他 Wiki 的比较

| 特性 | MediaWiki | Wiki.js | BookStack |
|------|-----------|---------|----------|
| 规模 | 非常大 | 中等 | 中等 |
| 标记 | Wikitext | Markdown | WYSIWYG |
| 扩展 | 2000+ | 有限 | 有限 |
| 复杂度 | 高 | 低 | 低 |
| Wikipedia 兼容 | 是 | 否 | 否 |

## 安装

### 系统要求

| 要求 | 最低 | 推荐 |
|------|------|------|
| PHP | 7.4+ | 8.1+ |
| 数据库 | MySQL 5.7+ | MySQL 8.0+ |
| Web 服务器 | Apache/Nginx | Apache 2.4+ |
| 内存 | 256 MB | 512 MB+ |

### Docker 安装

```yaml
version: '3'
services:
  mediawiki:
    image: mediawiki:latest
    ports:
      - "8080:80"
    volumes:
      - mediawiki_images:/var/www/html/images
      - ./LocalSettings.php:/var/www/html/LocalSettings.php
    environment:
      - MEDIAWIKI_DB_HOST=db
      - MEDIAWIKI_DB_NAME=wikidb
      - MEDIAWIKI_DB_USER=wikiuser
      - MEDIAWIKI_DB_PASSWORD=password

  db:
    image: mysql:8.0
    environment:
      - MYSQL_DATABASE=wikidb
      - MYSQL_USER=wikiuser
      - MYSQL_PASSWORD=password
      - MYSQL_ROOT_PASSWORD=rootpassword
    volumes:
      - mysql_data:/var/lib/mysql

volumes:
  mediawiki_images:
  mysql_data:
```

### 手动安装

```bash
# 下载 MediaWiki
wget https://releases.wikimedia.org/mediawiki/1.40/mediawiki-1.40.0.tar.gz
tar -xzf mediawiki-1.40.0.tar.gz
mv mediawiki-1.40.0 /var/www/html/wiki

# 设置权限
chown -R www-data:www-data /var/www/html/wiki
```

### 数据库设置

```sql
CREATE DATABASE wikidb;
CREATE USER 'wikiuser'@'localhost' IDENTIFIED BY 'password';
GRANT ALL PRIVILEGES ON wikidb.* TO 'wikiuser'@'localhost';
FLUSH PRIVILEGES;
```

## 配置

### LocalSettings.php

```php
<?php
$wgSitename = "My Wiki";
$wgScriptPath = "/wiki";
$wgServer = "https://wiki.example.com";

$wgDBtype = "mysql";
$wgDBserver = "localhost";
$wgDBname = "wikidb";
$wgDBuser = "wikiuser";
$wgDBpassword = "password";

$wgLanguageCode = "en";
$wgDefaultSkin = "vector";
```

### 基本设置

| 设置 | 描述 |
|------|------|
| `$wgSitename` | Wiki 名称 |
| `$wgScriptPath` | URL 路径 |
| `$wgServer` | 服务器 URL |
| `$wgLanguageCode` | 默认语言 |
| `$wgDefaultSkin` | 默认皮肤 |

## 内容创建

### Wiki 标记

| 语法 | 结果 |
|------|------|
| `== Heading ==` | 标题 |
| `'''bold'''` | **bold** |
| `''italic''` | *italic* |
| `[[Link]]` | 内部链接 |
| `[https://example.com Link]` | 外部链接 |
| `[[File:Image.png]]` | 图片 |

### 创建页面

1. 导航到目标 URL
2. 点击 "Create" 或 "Edit"
3. 使用 Wiki 标记添加内容
4. 保存页面

### 页面结构

```wiki
{{Infobox
|title = Page Title
|image = Example.png
|description = Brief description
}}

== Introduction ==
Main content here...

== Section 1 ==
Details...

== See Also ==
* [[Related Page]]
* [[Another Page]]

== References ==
<references />
```

## 模板

### 模板语法

```wiki
<!-- Template:Infobox -->
{| class="wikitable"
|-
! Title
| {{{title}}}
|-
! Image
| [[File:{{{image}}}]]
|}
```

### 使用模板

```wiki
{{Infobox
|title = Example
|image = Example.png
}}
```

### 常用模板

| 模板 | 用途 |
|------|------|
| Infobox | 结构化信息 |
| Citation | 引用格式 |
| Notice | 警告通知 |
| Navigation | 导航框 |

## 分类

### 分类结构

```
Main Category
├── Subcategory 1
│   ├── Article A
│   └── Article B
├── Subcategory 2
│   └── Article C
└── Article D
```

### 添加分类

```wiki
[[Category:Main Category]]
[[Category:Subcategory 1]]
```

### 分类管理

| 操作 | 描述 |
|------|------|
| 创建 | 添加分类页面 |
| 分类 | 将页面添加到分类 |
| 排序 | 控制排序顺序 |
| 层级 | 组织子分类 |

## 用户管理

### 用户权限

| 群组 | 权限 |
|------|------|
| Anonymous | 阅读、部分编辑 |
| User | 编辑、创建页面 |
| Autoconfirmed | 移动页面、上传 |
| Admin | 删除、保护、封禁 |
| Bureaucrat | 管理用户 |

### 用户设置

| 设置 | 描述 |
|------|------|
| 偏好 | 个人设置 |
| 监视列表 | 跟踪的页面 |
| 贡献 | 编辑历史 |
| 通知 | 告警偏好 |

### 用户管理

```php
// 将用户添加到群组
$wgGroupPermissions['groupname']['right'] = true;

// 限制匿名编辑
$wgGroupPermissions['*']['edit'] = false;
```

## 扩展

### 必备扩展

| 扩展 | 用途 |
|------|------|
| VisualEditor | WYSIWYG 编辑 |
| ParserFunctions | 模板逻辑 |
| Scribunto | Lua 脚本 |
| Semantic MediaWiki | 结构化数据 |
| ConfirmEdit | 垃圾防护 |

### 安装扩展

```bash
# 下载扩展
cd /var/www/html/wiki/extensions
git clone https://gerrit.wikimedia.org/r/mediawiki/extensions/ExtensionName

# 在 LocalSettings.php 中启用
wfLoadExtension('ExtensionName');
```

### 扩展配置

```php
// 启用 VisualEditor
wfLoadExtension('VisualEditor');
$wgDefaultUserOptions['visualeditor-enable'] = 1;

// 启用 ParserFunctions
wfLoadExtension('ParserFunctions');
```

## 皮肤

### 可用皮肤

| 皮肤 | 描述 |
|------|------|
| Vector | 默认、现代 |
| Timeless | 简洁、响应式 |
| Monobook | 经典 Wikipedia |
| Minerva | 移动优化 |

### 更换皮肤

```php
$wgDefaultSkin = "vector";

// 启用皮肤
wfLoadSkin('Timeless');
```

## 搜索

### 搜索配置

```php
$wgEnableMWSuggest = true;
$wgSearchType = 'CirrusSearch';
```

### 搜索功能

| 功能 | 描述 |
|------|------|
| 全文 | 搜索页面内容 |
| 建议 | 自动补全 |
| 前缀 | 按前缀搜索 |
| 命名空间 | 限定命名空间 |

## 备份和恢复

### 数据库备份

```bash
# 备份数据库
mysqldump -u wikiuser -p wikidb > wiki_backup.sql

# 恢复数据库
mysql -u wikiuser -p wikidb < wiki_backup.sql
```

### 文件备份

```bash
# 备份 Wiki 文件
tar -czf wiki_files_backup.tar.gz /var/www/html/wiki/

# 备份图片
tar -czf wiki_images_backup.tar.gz /var/www/html/wiki/images/
```

### 维护脚本

```bash
# 运行维护脚本
php maintenance/update.php
php maintenance/runJobs.php
php maintenance/rebuildrecentchanges.php
```

## 安全

### 安全设置

```php
$wgGroupPermissions['*']['edit'] = false;
$wgGroupPermissions['*']['createaccount'] = false;
$wgPasswordPolicy['default']['MinimalPasswordLength'] = 10;
$wgEnableAPI = true;
$wgEnableWriteAPI = true;
```

### 反垃圾

| 措施 | 描述 |
|------|------|
| CAPTCHA | ConfirmEdit 扩展 |
| 频率限制 | 限制编辑频率 |
| 黑名单 | 拦截垃圾内容 |
| 滥用过滤器 | 自动规则 |

## API 访问

### REST API

| 端点 | 方法 | 描述 |
|------|------|------|
| `/api.php?action=query` | GET | 查询页面 |
| `/api.php?action=parse` | GET | 解析 wikitext |
| `/api.php?action=edit` | POST | 编辑页面 |

### API 示例

```bash
# 获取页面内容
curl "https://wiki.example.com/api.php?action=parse&page=Main_Page&format=json"
```

## 性能

### 缓存

```php
$wgMainCacheType = CACHE_ACCEL;
$wgCacheDirectory = '/tmp/mw-cache';
$wgUseFileCache = true;
$wgFileCacheDirectory = '/tmp/mw-file-cache';
```

### 优化

| 设置 | 描述 |
|------|------|
| 对象缓存 | Redis、Memcached |
| 页面缓存 | 静态页面缓存 |
| CDN | 内容分发网络 |
| 压缩 | Gzip 压缩 |

## Web 服务器配置

### Nginx 配置

```nginx
server {
    listen 80;
    server_name wiki.example.com;
    root /var/www/html/wiki;
    index index.php;

    location / {
        try_files $uri $uri/ @rewrite;
    }

    location @rewrite {
        rewrite ^/(.*)$ /index.php?title=$1&$args;
    }

    location ~ \.php$ {
        fastcgi_pass unix:/var/run/php/php8.1-fpm.sock;
        fastcgi_param SCRIPT_FILENAME $document_root$fastcgi_script_name;
        include fastcgi_params;
    }
}
```

## 维护

### 定期任务

| 任务 | 频率 | 命令 |
|------|------|------|
| 更新数据库 | 更新后 | `php maintenance/update.php` |
| 运行作业 | 定期 | `php maintenance/runJobs.php` |
| 重建搜索 | 每周 | `php maintenance/rebuildfulltextsearch.php` |
| 清理缓存 | 按需 | `php maintenance/purgeList.php` |

## 总结

| 组件 | 用途 |
|------|------|
| Wiki 标记 | 内容格式化 |
| 模板 | 可重用内容 |
| 分类 | 内容组织 |
| 扩展 | 附加功能 |
| API | 编程访问 |
| 用户 | 协作编辑 |


---

## 来源：xwiki.md

## 简介

XWiki 是一个用 Java 编写的开源企业 Wiki 平台。它支持结构化内容、脚本编写、应用开发和广泛的自定义。本教程涵盖安装、内容管理、脚本编写和管理。

## XWiki 与其他企业 Wiki 对比

| 功能 | XWiki | Confluence | SharePoint | Notion |
|------|-------|------------|------------|--------|
| 开源 | 是 | 否 | 否 | 否 |
| 自托管 | 是 | Server 版 | 是 | 否 |
| 脚本 | Groovy、Velocity、JavaScript | 有限 | Power Automate | 否 |
| 应用构建器 | 是 | 市场 | Power Apps | 有限 |
| 数据库 | MySQL、PostgreSQL、Oracle、HQL | PostgreSQL | SQL Server | 专有 |
| REST API | 是 | 是 | 是 | 是 |
| 扩展 | 900+ | 3000+ | SPFx | 有限 |
| 价格 | 免费 | 免费增值 | 许可证 | 免费增值 |

## 系统要求

| 组件 | 最低要求 | 推荐配置 |
|------|---------|---------|
| Java | JDK 11 | JDK 17 |
| 内存 | 2 GB | 4 GB+ |
| 数据库 | MySQL 8、PostgreSQL 12 | PostgreSQL 15 |
| Servlet | Tomcat 9+ | Tomcat 10 |
| 磁盘 | 2 GB | 20 GB |
| CPU | 2 核 | 4+ 核 |

## 安装

### 独立版（XAR）

```bash
# 下载 WAR 和 Jetty JAR
wget https://nexus.xwiki.org/.../xwiki-platform-distribution-war-*.war

# 使用 Jetty 启动
java -jar xwiki-jetty-runner.jar --port 8080 xwiki.war
```

### Docker

```bash
docker run -d \
  --name xwiki \
  -p 8080:8080 \
  -e DB_DATABASE=xwiki \
  -e DB_USER=xwiki \
  -e DB_PASSWORD=xwiki \
  -e DB_HOST=xwiki-db \
  xwiki:lts-mysql-tomcat
```

### Docker Compose

```yaml
version: '3'
services:
  xwiki-db:
    image: mysql:8.0
    container_name: xwiki-db
    restart: unless-stopped
    environment:
      - MYSQL_ROOT_PASSWORD=root
      - MYSQL_DATABASE=xwiki
      - MYSQL_USER=xwiki
      - MYSQL_PASSWORD=xwiki
    volumes:
      - xwiki-db:/var/lib/mysql

  xwiki:
    image: xwiki:lts-mysql-tomcat
    container_name: xwiki
    restart: unless-stopped
    depends_on:
      - xwiki-db
    environment:
      - DB_DATABASE=xwiki
      - DB_USER=xwiki
      - DB_PASSWORD=xwiki
      - DB_HOST=xwiki-db
    ports:
      - "8080:8080"
    volumes:
      - xwiki-data:/usr/local/xwiki

volumes:
  xwiki-db:
  xwiki-data:
```

## 核心概念

### 内容层级

| 级别 | 描述 | 示例 |
|------|------|------|
| Wiki | 顶层容器 | 公司 Wiki |
| Space | 逻辑分组 | 工程、市场 |
| Page | 单个内容页 | API 文档 |
| Child Page | 嵌套页面 | REST API 参考 |

### 页面属性

| 属性 | 描述 |
|------|------|
| Title | 显示名称 |
| Content | Wiki 标记或渲染后的 HTML |
| Syntax | 渲染语法（XWiki、Markdown） |
| Parent | 父页面引用 |
| Tags | 分类标签 |
| Author | 创建者和最后编辑者 |
| Created | 创建时间戳 |
| Modified | 最后修改时间戳 |

## 内容编辑

### 语法选项

| 语法 | 描述 | 最佳用途 |
|------|------|---------|
| XWiki 2.1 | 原生 Wiki 语法 | XWiki 特有功能 |
| Markdown | 标准 Markdown | 技术内容 |
| HTML | 原始 HTML | 自定义布局 |
| Creole | Creole Wiki 语法 | 跨平台兼容 |

### XWiki 语法

| 元素 | 语法 |
|------|------|
| 标题 1 | = Heading 1 = |
| 标题 2 | == Heading 2 == |
| 粗体 | **bold** |
| 斜体 | //italic// |
| 下划线 | __underline__ |
| 删除线 | ~~strike~~ |
| 链接 | [[label>>URL]] |
| 图片 | image:url |
| 表格 | \|cell1\|cell2\| |
| 列表 | * item |
| 代码 | {{code}}...{{/code}} |
| 宏 | {{macro parameter="value"}}...{{/macro}} |

### 所见即所得编辑器

| 功能 | 描述 |
|------|------|
| 富文本 | 类似 Word 的编辑 |
| 工具栏 | 格式按钮 |
| 表格 | 可视化表格编辑 |
| 图片 | 拖放上传 |
| 宏 | 通过对话框插入 |
| 源码 | 切换到 Wiki 语法 |

## 宏

宏扩展页面功能。

### 内置宏

| 宏 | 用途 |
|----|------|
| {{toc}} | 目录 |
| {{children}} | 列出子页面 |
| {{include}} | 嵌入另一个页面 |
| {{velocity}} | Velocity 脚本块 |
| {{groovy}} | Groovy 脚本块 |
| {{html}} | 原始 HTML 块 |
| {{code}} | 语法高亮代码 |
| {{table}} | 动态表格 |
| {{gallery}} | 图片库 |
| {{box}} | 样式化内容框 |

### 宏参数

| 参数 | 常用选项 |
|------|---------|
| id | 唯一标识符 |
| output | rendered、wiki |
| scope | current、all |
| sort | name、date |
| limit | 结果数量 |

## 脚本编写

### Velocity 脚本

```velocity
{{velocity}}
#set($docs = $xwiki.searchDocuments("space = 'Main'"))
#foreach($doc in $docs)
  * [[$doc]]
#end
{{/velocity}}
```

### Groovy 脚本

```groovy
{{groovy}}
def docs = xwiki.searchDocuments("space = 'Main'")
docs.each { doc ->
  println("* [[" + doc + "]]")
}
{{/groovy}}
```

### JavaScript

```javascript
{{javascript}}
require(['jquery'], function($) {
  $('.xwikidocumentcontainer').addClass('custom-style');
});
{{/javascript}}
```

## App Within Minutes

无需编码即可创建数据库驱动的应用。

### 应用结构

| 组件 | 用途 |
|------|------|
| Class | 数据结构定义 |
| Properties | 字段（文本、数字、日期等） |
| Sheets | 显示模板 |
| Templates | 新条目表单 |
| Livetables | 带过滤器的数据列表 |

### 属性类型

| 类型 | 用例 |
|------|------|
| String | 文本字段 |
| Number | 整数、浮点数 |
| Date | 日期和时间 |
| Boolean | 真/假 |
| Static List | 下拉选项 |
| Database List | 外键引用 |
| TextArea | 长文本、富文本 |
| File | 文件上传 |
| Email | 邮箱地址 |
| URL | 网址 |

## 访问控制

### 权限模型

| 级别 | 范围 |
|------|------|
| Wiki | 全局 Wiki 权限 |
| Space | 空间级权限 |
| Page | 单个页面权限 |

### 权限类型

| 权限 | 描述 |
|------|------|
| View | 查看页面 |
| Edit | 修改页面 |
| Delete | 删除页面 |
| Admin | 管理设置 |
| Comment | 添加评论 |
| Script | 运行脚本 |

### 用户组

| 组 | 默认角色 |
|----|---------|
| XWikiAdminGroup | 完全管理 |
| XWikiAllGroup | 所有注册用户 |
| 自定义组 | 自行定义 |

## 扩展

### 扩展管理器

| 操作 | 方法 |
|------|------|
| 浏览 | 搜索扩展仓库 |
| 安装 | 点击安装按钮 |
| 更新 | 检查更新 |
| 卸载 | 移除扩展 |
| 配置 | 扩展设置 |

### 热门扩展

| 扩展 | 用途 |
|------|------|
| Flamingo Theme | 现代 UI 主题 |
| Markdown Support | Markdown 语法 |
| Diagram Application | Draw.io 集成 |
| File Manager | 文件管理 |
| Calendar | 活动安排 |
| Meeting Notes | 会议模板 |
| Idea Management | 想法跟踪 |

## 主题

### Flamingo 主题

| 自定义 | 选项 |
|--------|------|
| 颜色 | 主色、辅色、强调色 |
| Logo | 上传自定义 Logo |
| Favicon | 自定义网站图标 |
| Footer | 自定义页脚内容 |
| CSS | 额外样式表 |

## 搜索

### 搜索方式

| 方式 | 语法 |
|------|------|
| 全文搜索 | 头部搜索框 |
| HQL | 高级 HQL 查询 |
| SOLR | 基于 SOLR 的搜索 |
| Livetable | 带过滤器的表格 |

### HQL 查询示例

| 查询 | 用途 |
|------|------|
| space = 'Main' | Main 空间中的页面 |
| doc.author = 'Admin' | 按作者筛选页面 |
| doc.creationDate > '2024-01-01' | 最近的页面 |
| doc.tags = 'important' | 带标签的页面 |

## 导入/导出

| 格式 | 方向 | 内容 |
|------|------|------|
| XAR | 导出/导入 | 完整 Wiki 或空间 |
| HTML | 导出 | 页面为 HTML |
| PDF | 导出 | 页面为 PDF |
| ODT | 导出 | OpenDocument |
| RTF | 导出 | 富文本格式 |

## 备份

### 备份策略

| 组件 | 方法 | 频率 |
|------|------|------|
| 数据库 | pg_dump/mysqldump | 每天 |
| 附件 | 文件系统备份 | 每天 |
| 配置 | Git 仓库 | 变更时 |
| 扩展 | 扩展列表导出 | 每周 |

## REST API

### 端点

| 方法 | 端点 | 描述 |
|------|------|------|
| GET | /rest/wikis | 列出 Wiki |
| GET | /rest/wikis/{wiki}/spaces | 列出空间 |
| GET | /rest/wikis/{wiki}/spaces/{space}/pages | 列出页面 |
| GET | /rest/wikis/{wiki}/pages/{space}/{page} | 获取页面 |
| PUT | /rest/wikis/{wiki}/pages/{space}/{page} | 更新页面 |
| POST | /rest/wikis/{wiki}/spaces/{space}/pages | 创建页面 |
| DELETE | /rest/wikis/{wiki}/pages/{space}/{page} | 删除页面 |

## 性能调优

| 设置 | 建议 |
|------|------|
| JVM Heap | 生产环境 2-4 GB |
| 数据库 | 连接池 |
| 缓存 | 启用页面缓存 |
| SOLR | 索引以加速搜索 |
| GZIP | 启用响应压缩 |
| CDN | 提供静态资源 |

## 总结

XWiki 提供了一个强大的企业 Wiki 平台，通过脚本编写、应用构建和丰富的扩展生态系统实现广泛自定义。其结构化内容模型、细粒度访问控制和 REST API 使其适合需要灵活知识管理和协作平台的大型组织。


---

## 来源：tiddly.md

## 简介

TiddlyWiki 是一个自包含的单文件个人 Wiki。它完全在网页浏览器中运行，无需服务器。本教程涵盖在 TiddlyWiki 中创建、组织和管理知识。

## TiddlyWiki 的独特之处

| 功能 | 描述 |
|------|------|
| 单 HTML 文件 | 整个 Wiki 在一个便携文件中 |
| 无需服务器 | 在任何现代浏览器中运行 |
| 离线优先 | 无需互联网即可工作 |
| 高度可定制 | 内置 JavaScript 和 CSS |
| 非线性 | 以相互关联的 tiddler 组织思路 |
| 开源 | MIT 许可证 |

## 快速开始

### 下载选项

| 选项 | URL | 描述 |
|------|-----|------|
| 空白 Wiki | tiddlywiki.com | 从头开始的空白 Wiki |
| TiddlyWiki on Node.js | npm | 基于服务器的多用户 Wiki |
| TiddlyDesktop | GitHub | 桌面应用封装 |
| Timimi Extension | 浏览器商店 | 从浏览器保存单文件 Wiki |

### Node.js 安装

```bash
npm install -g tiddlywiki
tiddlywiki mywiki --init server
tiddlywiki mywiki --listen
```

| 命令 | 用途 |
|------|------|
| --init server | 创建服务器版 Wiki |
| --init empty | 创建空白 Wiki |
| --listen | 在 8080 端口启动 HTTP 服务器 |
| --build | 构建静态 HTML 输出 |

## 核心概念

### Tiddler

Tiddler 是内容的基本单元。

| 字段 | 类型 | 描述 |
|------|------|------|
| title | String | 唯一标识符（必填） |
| text | String | 主要内容体 |
| tags | List | 分类标签 |
| created | Date | 创建时间戳 |
| modified | Date | 最后修改时间戳 |
| fields | Custom | 任何额外的元数据 |

### 标签

标签创建集合和导航结构。

| 标签 | 用途 |
|------|------|
| GettingStarted | 入门内容 |
| $:/tags/Stylesheet | CSS 自定义 |
| $:/tags/JavaScript | 自定义脚本 |
| $:/tags/Macro | 可复用宏 |
| 自定义标签 | 你的组织系统 |

### 链接和嵌入

| 语法 | 效果 |
|------|------|
| [[Tiddler Title]] | 创建链接 |
| [[Display Text\|Tiddler Title]] | 带自定义文本的链接 |
| {{Tiddler Title}} | 嵌入内容 |
| {{Tiddler Title\|field}} | 嵌入特定字段 |

## 编辑 Tiddler

### 创建 Tiddler

1. 点击侧边栏中的"+"按钮。
2. 输入唯一标题。
3. 使用 wikitext 语法编写内容。
4. 添加标签以便组织。
5. 点击"Done"保存。

### Wikitext 格式

| 语法 | 结果 |
|------|------|
| ''bold'' | 粗体文本 |
| //italic// | 斜体文本 |
| __underline__ | 下划线 |
| ~~strikethrough~~ | 删除线 |
| ^^superscript^^ | 上标 |
| ,,subscript,, | 下标 |
| !Heading 1 | 标题 1 |
| !!Heading 2 | 标题 2 |
| !!!Heading 3 | 标题 3 |
| --- | 水平线 |
| <!-- comment --> | 隐藏注释 |

### 列表

| 语法 | 类型 |
|------|------|
| * Item | 无序列表 |
| # Item | 有序列表 |
| ;Term | 定义术语 |
| :Definition | 定义内容 |

### 代码块

| 语法 | 用途 |
|------|------|
| {{{code}}} | 行内代码 |
| \`\`\` code \`\`\` | 代码块 |
| <pre>code</pre> | 预格式化文本 |

## 宏

宏是可复用的内容模板。

### 内置宏

| 宏 | 用途 | 示例 |
|----|------|------|
| <<now>> | 当前日期/时间 | <<now YYYY-MM-DD>> |
| <<toc>> | 目录 | <<toc "TableOfContents">> |
| <<list-tagged>> | 按标签列出 tiddler | <<list-tagged "Projects">> |
| <<search>> | 搜索框 | <<search>> |
| <<slider>> | 可展开内容 | <<slider "Info">> |

### 自定义宏

```
\rules only filteredtranscludeinline transcludeinline
\define hello(name)
Hello, $name$!
\end

<<hello("World")>>
```

## 插件

### 必备插件

| 插件 | 用途 |
|------|------|
| TiddlyMap | 可视化思维导图和图表 |
| Stroll | 叙事风格布局 |
| TW5-CodeMirror | 更好的代码编辑器 |
| Relink | 自动链接更新 |
| DPL | 动态页面列表 |
| Mermaid | 图表和流程图 |

### 安装插件

1. 打开插件库：$:/core/ui/ControlPanel/Plugins。
2. 浏览或搜索插件。
3. 点击"Install"并重新加载。

## 组织策略

### 基于标签的结构

| 标签 | 内容类型 |
|------|---------|
| Project | 项目描述 |
| Note | 会议记录、想法 |
| Reference | 外部资源 |
| Task | 待办事项 |
| Journal | 每日条目 |
| Template | 可复用模板 |

### 文件夹结构（Node.js 版）

| 文件夹 | 用途 |
|--------|------|
| tiddlers/ | 所有 tiddler 文件 |
| plugins/ | 自定义插件 |
| themes/ | 视觉主题 |
| languages/ | 翻译 |
| output/ | 构建的静态 HTML |

## 过滤器

过滤器用于选择和操作 tiddler。

| 过滤器 | 用途 | 示例 |
|--------|------|------|
| [tag[Project]] | 按标签 | 所有项目 |
| [search[text]] | 全文搜索 | 包含"text" |
| [sort[title]] | 按字母排序 | A-Z 按标题 |
| [limit[10]] | 限制结果 | 前 10 个 |
| [days[-7]] | 最近项目 | 最近 7 天 |
| [is[tiddler]] | 所有 tiddler | 排除系统 |
| [fields:title[My Title]] | 按字段值 | 精确匹配 |
| [!tag[draft]] | 否定 | 排除草稿 |

### 组合过滤器

```
[tag[Project]] +[sort[modified]] +[limit[5]]
// 获取最近修改的 5 个项目
```

## 自定义

### 主题

| 主题 | 风格 |
|------|------|
| Vanilla | 简洁、极简 |
| Snowwhite | 明亮、现代 |
| Plain | 超极简 |
| Custom | 用 CSS 覆盖 |

### 自定义 CSS

创建标记为 $:/tags/Stylesheet 的 tiddler：

```css
.tc-tiddler-title {
  color: #2c3e50;
  font-size: 1.5em;
}
.tc-sidebar {
  background-color: #f8f9fa;
}
```

## 保存和备份

### 单文件 Wiki

| 浏览器 | 保存方法 |
|--------|---------|
| Chrome | Timimi 扩展（推荐） |
| Firefox | Timimi 扩展（推荐） |
| 任意 | 下载按钮，重新上传 |

### Node.js 版

| 方法 | 命令 |
|------|------|
| 自动保存 | 内置，编辑时保存 |
| Git 备份 | git add tiddlers/ && git commit -m "backup" |
| 导出 | tiddlywiki mywiki --build |

## 快捷键

| 快捷键 | 操作 |
|--------|------|
| Ctrl+Enter | 关闭当前 tiddler |
| Ctrl+Shift+E | 编辑当前 tiddler |
| Ctrl+G | 打开搜索 |
| Ctrl+N | 新建 tiddler |
| Ctrl+S | 保存（配合 Timimi） |

## 用例

| 用例 | 组织方式 |
|------|---------|
| 个人知识库 | 按主题标签，日志条目 |
| 项目管理 | 项目标签，任务子标签 |
| 研究笔记 | 来源标签，引用字段 |
| 写作 | 章节标签，草稿/已发布状态 |
| 学习 | 主题标签，间隔重复 |

## 总结

TiddlyWiki 提供了一个独特灵活的个人 Wiki 系统。其单文件便携性、丰富的 wikitext 语法、过滤系统和插件生态系统，使其适用于任何知识管理需求。无论是用作笔记本、项目跟踪器还是研究数据库，TiddlyWiki 都能适应你的工作流程。


---

## 来源：doku.md

## 简介

DokuWiki 是一个简单的、基于文件的 Wiki 引擎，它将数据存储在纯文本文件中，而不是数据库中。它需要最少的服务器资源，并支持丰富的插件功能，适用于知识管理和文档编写。

## 系统要求

| 组件 | 最低配置 | 推荐配置 |
|------|---------|---------|
| PHP 版本 | 7.4 | 8.1+ |
| Web 服务器 | Apache 2.4 | Nginx 1.20+ |
| 内存 | 64 MB | 256 MB |
| 磁盘空间 | 50 MB | 500 MB |
| 扩展 | mbstring, xml | +intl, +json |

## 安装方式

| 方式 | 平台 | 难度 |
|------|------|------|
| 手动安装 | 任意 Linux | 中等 |
| Docker | 任意操作系统 | 简单 |
| Snap 包 | Ubuntu | 简单 |
| 共享主机 | cPanel/Plesk | 简单 |

### 手动安装

下载最新的稳定版本并解压到 Web 根目录：

```bash
cd /var/www/html
wget https://download.dokuwiki.org/src/dokuwiki/dokuwiki-stable.tgz
tar -xzf dokuwiki-stable.tgz
mv dokuwiki-*/ dokuwiki
chown -R www-data:www-data /var/www/html/dokuwiki
```

### Docker 安装

```bash
docker run -d \
  --name dokuwiki \
  -p 8080:80 \
  -v /path/to/data:/dokuwiki/data \
  dokuwiki/dokuwiki:latest
```

## 目录结构

| 目录 | 用途 |
|------|------|
| `conf/` | 配置文件 |
| `data/` | 所有用户内容和页面 |
| `data/pages/` | Wiki 页面内容（文本文件） |
| `data/meta/` | 元数据和修订信息 |
| `data/media/` | 上传的媒体文件 |
| `data/attic/` | 页面的旧版本 |
| `lib/` | 核心库和插件 |
| `lib/plugins/` | 已安装的插件 |

## 配置基础

主配置文件为 `conf/local.php`。主要设置包括：

| 设置项 | 说明 | 示例 |
|--------|------|------|
| `title` | Wiki 站点标题 | `"Team Knowledge Base"` |
| `lang` | 默认语言 | `"zh"` |
| `license` | 内容许可证 | `"cc-by-sa"` |
| `useacl` | 启用 ACL | `true` |
| `superuser` | 管理员账户 | `"@admin"` |
| `authtype` | 认证后端 | `"authplain"` |

### 配置示例

```php
<?php
$conf['title'] = 'Company Wiki';
$conf['lang'] = 'en';
$conf['useacl'] = 1;
$conf['superuser'] = 'admin';
$conf['authtype'] = 'authplain';
$conf['allowregister'] = 0;
$conf['usewordblock'] = 1;
```

## 命名空间管理

命名空间作为文件夹使用，用于将 Wiki 页面组织成层级结构。

| 功能 | 语法 | 结果 |
|------|------|------|
| 创建链接 | `[[namespace:page]]` | 链接到命名空间中的页面 |
| 起始页 | `namespace:start` | 命名空间的默认页面 |
| 面包屑导航 | 自动生成 | 显示导航路径 |
| 媒体路径 | `:namespace:image.png` | 特定命名空间中的媒体 |

## 语法参考

### 基本格式

| 元素 | 语法 | 输出 |
|------|------|------|
| 粗体 | `**text**` | **text** |
| 斜体 | `//text//` | *text* |
| 下划线 | `__text__` | 下划线文字 |
| 删除线 | `<del>text</del>` | ~~text~~ |
| 行内代码 | `''code''` | `code` |

### 标题

```
====== 一级标题 ======
===== 二级标题 =====
==== 三级标题 ====
=== 四级标题 ===
== 五级标题 ==
```

### 列表和表格

| 类型 | 语法 |
|------|------|
| 无序列表 | `  * Item` |
| 有序列表 | `  - Item` |
| 嵌套列表 | `    * Sub-item` |
| 表头 | `^ Header ^` |
| 表格单元格 | `| Cell |` |

### 代码块

````
<code python>
def hello():
    print("Hello World")
</code>
````

## 访问控制列表（ACL）

ACL 规则控制谁可以在特定命名空间中读取、编辑和创建页面。

| 权限级别 | 值 | 功能 |
|---------|-----|------|
| 无 | 0 | 无访问权限 |
| 读取 | 1 | 查看页面 |
| 编辑 | 2 | 编辑现有页面 |
| 创建 | 4 | 创建新页面 |
| 上传 | 8 | 上传文件 |
| 删除 | 16 | 删除页面 |
| 管理 | 255 | 完全控制 |

### ACL 规则示例

| 规则 | 用户/组 | 命名空间 | 权限 |
|------|---------|---------|------|
| 1 | @user | * | 8 |
| 2 | @admin | * | 255 |
| 3 | @public | public | 1 |
| 4 | @staff | internal | 12 |

## 插件安装

DokuWiki 拥有丰富的插件生态系统，可通过扩展管理器获取。

| 插件 | 用途 | 分类 |
|------|------|------|
| Struct | 结构化数据 | 内容 |
| Bureaucracy | 表单处理 | 工作流 |
| AuthPDO | 数据库认证 | 认证 |
| Move | 页面移动 | 管理 |
| Tag | 页面标签 | 组织 |
| Include | 页面嵌入 | 内容 |

通过管理面板安装：

1. 导航到 **Admin > Extension Manager**
2. 搜索插件名称
3. 点击 **Install**
4. 通过插件设置进行配置

## 备份与恢复

| 组件 | 位置 | 频率 |
|------|------|------|
| 页面 | `data/pages/` | 每日 |
| 媒体 | `data/media/` | 每日 |
| 配置 | `conf/` | 每周 |
| 插件 | `lib/plugins/` | 每周 |
| ACL | `conf/acl.auth.php` | 每周 |

### 自动备份脚本

```bash
#!/bin/bash
BACKUP_DIR="/var/backups/dokuwiki"
DATE=$(date +%Y%m%d)
mkdir -p "$BACKUP_DIR"
tar -czf "$BACKUP_DIR/dokuwiki-$DATE.tar.gz" \
  /var/www/html/dokuwiki/data \
  /var/www/html/dokuwiki/conf
find "$BACKUP_DIR" -mtime +30 -delete
```

## 升级 DokuWiki

| 步骤 | 操作 | 说明 |
|------|------|------|
| 1 | 备份数据 | 复制 `data/` 和 `conf/` |
| 2 | 下载更新 | 获取最新稳定版本 |
| 3 | 解压文件 | 覆盖现有文件（`data/` 和 `conf/` 除外） |
| 4 | 修复权限 | 设置正确的所有权 |
| 5 | 运行更新程序 | 如有提示访问 `install.php` |

## 性能调优

| 设置 | 位置 | 影响 |
|------|------|------|
| 缓存 | `conf/local.php` | 减少页面解析时间 |
| Gzip | Web 服务器配置 | 减少传输大小 |
| OPcache | `php.ini` | 加速 PHP 执行 |
| 索引 | `data/index/` | 加快搜索结果 |

## 安全加固

| 措施 | 配置 |
|------|------|
| 禁用注册 | `$conf['allowregister'] = 0` |
| CAPTCHA | 安装 captcha 插件 |
| 垃圾信息拦截 | `$conf['usewordblock'] = 1` |
| 文件上传限制 | `$conf['upload_maxfilesize'] = 2` |
| 禁用 XML 导出 | `$conf['xml'] = 0` |
| 安全 Cookie | 在 Web 服务器中设置 `secure` 标志 |

## 总结

DokuWiki 提供了一个轻量但强大的 Wiki 解决方案，无需数据库后端。其纯文本存储模型简化了备份和版本控制，而丰富的插件生态系统允许针对几乎任何文档和知识管理用例进行自定义。


---
