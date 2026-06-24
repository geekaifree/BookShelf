# BookStack：构建文档和 Wiki 平台

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
