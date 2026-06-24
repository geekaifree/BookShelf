# LinkAce：自托管书签管理器

## 简介

LinkAce 是一个自托管的书签管理器，帮助用户组织、归档和检索网页链接。它提供了一个简洁的界面，具有标签、分类和归档功能。

| 属性 | 详情 |
|----------|--------|
| 仓库 | Kovah/linkace |
| 许可证 | GPL-3.0 |
| 语言 | PHP, Laravel |
| 平台 | 基于 Web |
| 数据库 | MySQL, PostgreSQL, SQLite |

## 主要功能

| 功能 | 描述 |
|---------|-------------|
| 书签管理 | 保存、编辑和组织书签 |
| 标签 | 灵活的标签系统 |
| 分类 | 层次化分类 |
| 列表 | 将书签分组到自定义列表 |
| 归档 | 自动页面归档 |
| 全文搜索 | 搜索书签内容 |
| 导入/导出 | 从浏览器和其他工具导入 |
| API | 用于集成的 REST API |
| 分享 | 公开分享书签 |

## 使用 Docker 安装

### Docker Compose 配置

```yaml
version: "3.8"

services:
  app:
    image: linkace/linkace:latest
    ports:
      - "8080:80"
    volumes:
      - linkace_data:/app/storage
    environment:
      APP_KEY: base64:your-app-key
      DB_CONNECTION: mysql
      DB_HOST: db
      DB_DATABASE: linkace
      DB_USERNAME: linkace
      DB_PASSWORD: secret
    depends_on:
      - db

  db:
    image: mariadb:10
    environment:
      MYSQL_ROOT_PASSWORD: rootsecret
      MYSQL_DATABASE: linkace
      MYSQL_USER: linkace
      MYSQL_PASSWORD: secret
    volumes:
      - db_data:/var/lib/mysql

volumes:
  linkace_data:
  db_data:
```

### 初始设置

1. 运行 `docker compose up -d`。
2. 访问 `http://localhost:8080`。
3. 按照设置向导操作。
4. 创建管理员账户。
5. 配置应用程序设置。

## 管理书签

### 添加书签

| 字段 | 描述 |
|-------|-------------|
| URL | 要保存的网址 |
| Title（标题） | 书签的显示名称 |
| Description（描述） | 关于链接的可选说明 |
| Category（类别） | 单一类别分配 |
| Tags（标签） | 多个标签分配 |
| Lists（列表） | 添加到一个或多个列表 |
| Visibility（可见性） | 公开或私有 |

### 书签字段

| 字段 | 类型 | 描述 |
|-------|------|-------------|
| URL | 必填 | 书签 URL |
| Title（标题） | 自动填充 | 页面标题（自动获取） |
| Description（描述） | 可选 | 用户提供的说明 |
| Category（类别） | 可选 | 单一类别 |
| Tags（标签） | 可选 | 多个标签 |
| Is Private（是否私有） | 布尔值 | 可见性设置 |

## 组织

### 分类

分类提供层次结构来组织书签。

| 级别 | 示例 |
|-------|---------|
| 第 1 级 | Technology |
| 第 2 级 | Programming |
| 第 3 级 | Python |

### 标签

标签提供灵活的非层次化组织。

| 用途 | 示例 |
|-------|---------|
| 主题 | python, javascript, devops |
| 状态 | todo, reading, archived |
| 优先级 | important, reference |

### 列表

列表是为特定目的策划的书签集合。

| 列表类型 | 示例 |
|-----------|---------|
| 项目 | "网站重设计资源" |
| 阅读 | "待读文章" |
| 参考 | "常用工具" |

## 导入和导出

### 导入来源

| 来源 | 格式 |
|--------|--------|
| 浏览器书签 | HTML 导出文件 |
| Pocket | CSV 导出 |
| Raindrop | CSV 导出 |
| Wallabag | JSON 导出 |
| Delicious | HTML 导出 |
| CSV | 自定义 CSV 格式 |

### 导出格式

| 格式 | 描述 |
|--------|-------------|
| CSV | 逗号分隔值 |
| JSON | 结构化 JSON 数据 |

## 归档

LinkAce 可以自动归档已添加书签的页面。

| 功能 | 描述 |
|---------|-------------|
| Wayback Machine | 保存到 Internet Archive |
| Local Archive（本地归档） | 存储页面的本地副本 |
| Screenshot（截图） | 捕获页面截图 |
| PDF | 生成页面的 PDF |

### 归档配置

```env
BACKUP_ARCHIVE=enabled
BACKUP_SCREENSHOTS=enabled
BACKUP_PDF=enabled
WAYBACK_MACHINE_ENABLED=true
```

## 搜索

| 功能 | 描述 |
|---------|-------------|
| Full-Text（全文） | 搜索书签内容 |
| By Tag（按标签） | 按特定标签过滤 |
| By Category（按类别） | 按类别过滤 |
| By List（按列表） | 按列表过滤 |
| By Date（按日期） | 按创建日期过滤 |
| Combined（组合） | 同时使用多个过滤器 |

## API

LinkAce 提供 REST API 以进行编程访问。

| 端点 | 方法 | 描述 |
|----------|--------|-------------|
| /api/v1/links | GET | 列出所有书签 |
| /api/v1/links | POST | 创建书签 |
| /api/v1/links/{id} | GET | 获取书签 |
| /api/v1/links/{id} | PUT | 更新书签 |
| /api/v1/links/{id} | DELETE | 删除书签 |
| /api/v1/tags | GET | 列出所有标签 |
| /api/v1/categories | GET | 列出所有类别 |
| /api/v1/lists | GET | 列出所有列表 |

### 认证

API 请求需要 API token。

```bash
curl -H "Authorization: Bearer YOUR_API_TOKEN" \
  https://your-domain.com/api/v1/links
```

## 浏览器扩展

LinkAce 提供浏览器扩展以便快速添加书签。

| 功能 | 描述 |
|---------|-------------|
| One-Click Save（一键保存） | 即时保存当前页面 |
| Quick Add（快速添加） | 添加标签和类别 |
| Search（搜索） | 搜索您的书签 |
| Sync（同步） | 自动同步 |

## 用户管理

| 角色 | 权限 |
|------|-------------|
| Admin（管理员） | 完全系统访问 |
| User（用户） | 管理自己的书签 |
| Guest（访客） | 仅查看公开书签 |

## 配置选项

| 设置 | 描述 |
|---------|-------------|
| Dark Mode（深色模式） | 启用深色主题 |
| Date Format（日期格式） | 自定义日期显示 |
| Bookmark Order（书签排序） | 默认排序方式 |
| Archive Settings（归档设置） | 配置归档行为 |
| Notification（通知） | 链接失效的邮件通知 |

## 技巧和最佳实践

| 技巧 | 说明 |
|-----|-------------|
| 使用一致的标签 | 维护受控的词汇表 |
| 添加描述 | 使书签日后更容易找到 |
| 用列表管理项目 | 按项目分组相关书签 |
| 启用归档 | 保留可能消失的内容 |
| 导入现有书签 | 从当前浏览器书签开始 |
| 使用 API | 与其他工具和工作流程集成 |

## 备份

| 组件 | 方法 |
|-----------|--------|
| 数据库 | 定期 MySQL/PostgreSQL 备份 |
| 文件 | 备份存储卷 |
| 配置 | 备份环境文件 |

```bash
# 数据库备份
docker compose exec db mysqldump -u linkace -psecret linkace > backup.sql
```

## 结论

LinkAce 是一个设计良好的书签管理器，将简洁性与强大的组织功能相结合。其自托管特性确保了隐私，而 API 和浏览器扩展使其易于集成到日常工作流程中。
