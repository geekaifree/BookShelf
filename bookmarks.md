# 链接与书签管理

> 本文档整合了以下源文件：link.md, bookmark.md, read.md

---

## 来源：link.md

## 简介

Shaarli 是一款极简的自托管书签应用，使用 PHP 编写。它提供了一种快速简单的方式来保存、组织和分享网页链接，支持标签和多种查看模式。

## 目录

1. [功能概览](#功能概览)
2. [安装](#安装)
3. [配置](#配置)
4. [添加书签](#添加书签)
5. [组织与标签](#组织与标签)
6. [搜索与浏览](#搜索与浏览)
7. [订阅与导出](#订阅与导出)
8. [插件系统](#插件系统)

## 功能概览

| 功能 | 说明 |
|------|------|
| 书签 | 保存 URL 并附带笔记 |
| 标签 | 多标签组织 |
| 搜索 | 全文搜索 |
| 订阅 | RSS/Atom 输出 |
| 导出 | 多格式支持 |
| 插件 | 可扩展功能 |
| API | 基于 REST 的接口 |
| 主题 | 可定制外观 |

## 安装

### 系统要求

| 组件 | 最低要求 | 推荐配置 |
|------|----------|----------|
| PHP | 7.4+ | 8.1+ |
| Web 服务器 | Apache, Nginx | Nginx |
| 存储 | 10 MB | 100 MB+ |
| 扩展 | mbstring, curl, gd | 建议全部 |
| 数据库 | 无 (SQLite) | SQLite |

### Docker 安装

```yaml
# docker-compose.yml
services:
  shaarli:
    image: shaarli/shaarli:latest
    ports:
      - "8080:80"
    volumes:
      - ./data:/var/www/shaarli/data
    restart: unless-stopped
```

### 手动安装

| 步骤 | 操作 |
|------|------|
| 1 | 从 GitHub 下载发布版 |
| 2 | 解压到 Web 目录 |
| 3 | 设置 data 目录权限 |
| 4 | 通过浏览器访问 |
| 5 | 完成安装向导 |

### Web 服务器配置

#### Nginx

```nginx
server {
    listen 80;
    server_name shaarli.example.com;
    root /var/www/shaarli;
    index index.php;

    location / {
        try_files $uri $uri/ /index.php?$args;
    }

    location ~ \.php$ {
        fastcgi_pass unix:/var/run/php/php-fpm.sock;
        fastcgi_index index.php;
        include fastcgi_params;
    }
}
```

#### Apache

```apache
<VirtualHost *:80>
    ServerName shaarli.example.com
    DocumentRoot /var/www/shaarli
    
    <Directory /var/www/shaarli>
        AllowOverride All
        Require all granted
    </Directory>
</VirtualHost>
```

## 配置

### 配置文件

主配置存储在 `data/config.php` 中：

| 设置 | 说明 | 默认值 |
|------|------|--------|
| `title` | 站点标题 | Shaarli |
| `header_link` | 标题 URL | / |
| `language` | 界面语言 | English |
| `timezone` | 服务器时区 | UTC |
| `enabled_plugins` | 活跃插件 | [] |

### 安全设置

| 设置 | 说明 |
|------|------|
| `username` | 管理员用户名 |
| `password` | 管理员密码（哈希） |
| `login_protection` | 暴力破解防护 |
| `ban_after` | 封禁前失败次数 |
| `ban_duration` | 封禁时间（分钟） |

### 隐私设置

| 设置 | 说明 | 选项 |
|------|------|------|
| `private_links_by_default` | 新链接默认私有 | true/false |
| `hide_timestamps` | 隐藏日期 | true/false |
| `show_atom` | 启用 Atom 订阅 | true/false |
| `feed_need_login` | 订阅需要认证 | true/false |

## 添加书签

### Web 界面

| 步骤 | 操作 |
|------|------|
| 1 | 点击"添加链接"按钮 |
| 2 | 输入 URL |
| 3 | 添加标题（自动获取） |
| 4 | 添加描述 |
| 5 | 添加标签（空格分隔） |
| 6 | 设置公开/私有 |
| 7 | 点击"保存" |

### 书签字段

| 字段 | 说明 | 必需 |
|------|------|------|
| URL | 网址 | 是 |
| 标题 | 链接标题 | 是 |
| 描述 | 笔记 | 否 |
| 标签 | 空格分隔的标签 | 否 |
| 私有 | 可见性设置 | 否 |
| 日期 | 自定义日期 | 否 |

### 浏览器书签小工具

| 功能 | 说明 |
|------|------|
| 一键保存 | 在任何页面点击书签小工具 |
| 自动填充 | URL 和标题预填 |
| 弹出窗口 | 添加标签和笔记 |
| 安装 | 拖到书签栏 |

### 批量导入

| 来源 | 格式 | 方式 |
|------|------|------|
| 浏览器导出 | HTML/JSON | 导入工具 |
| Delicious | JSON | 导入工具 |
| Pinboard | JSON | 导入工具 |
| Wallabag | JSON | 导入工具 |
| Pocket | CSV | 导入工具 |

## 组织与标签

### 标签系统

| 功能 | 说明 |
|------|------|
| 多标签 | 添加时空格分隔 |
| 标签层级 | 使用下划线嵌套 |
| 标签同义词 | 映射相似标签 |
| 标签计数 | 每个标签的链接数 |

### 标签最佳实践

| 实践 | 示例 |
|------|------|
| 一致命名 | `javascript` 而非 `js` 或 `JavaScript` |
| 层级化 | `programming_python`, `programming_rust` |
| 描述性 | `tutorial` 而非 `tut` |
| 数量有限 | 每个链接 3-5 个标签 |

### 标签管理

| 操作 | 方法 |
|------|------|
| 查看所有标签 | 标签页面 |
| 按标签过滤 | 点击标签 |
| 多标签过滤 | 选择多个标签 |
| 编辑标签 | 编辑链接 > 修改标签 |
| 批量重命名 | 标签管理工具 |

### 链接状态

| 状态 | 说明 | 可见性 |
|------|------|--------|
| 公开 | 所有人可见 | 任何人 |
| 私有 | 仅管理员可见 | 已认证 |

## 搜索与浏览

### 搜索方式

| 方式 | 说明 | 示例 |
|------|------|------|
| 全文 | 搜索标题 + 描述 | `python tutorial` |
| 标签过滤 | 按标签过滤 | `#python` |
| URL 搜索 | 搜索 URL | `github.com` |
| 日期过滤 | 按日期过滤 | `2024-01-15` |

### 搜索操作符

| 操作符 | 说明 | 示例 |
|--------|------|------|
| `#tag` | 按标签过滤 | `#javascript` |
| `!tag` | 排除标签 | `!deprecated` |
| `date:YYYY-MM-DD` | 特定日期 | `date:2024-01-15` |
| `url:domain` | 按域名过滤 | `url:github.com` |

### 浏览模式

| 模式 | 说明 |
|------|------|
| 时间顺序 | 最新优先 |
| 标签云 | 可视化标签大小 |
| 每日 | 逐日视图 |
| 图片墙 | 缩略图网格 |
| 搜索结果 | 过滤视图 |

## 订阅与导出

### 订阅类型

| 订阅 | URL | 格式 |
|------|-----|------|
| Atom | `/feed.atom` | Atom 1.0 |
| RSS | `/feed.rss` | RSS 2.0 |
| 每日 | `/feed/daily` | Atom |
| 标签 | `/feed/tag/python` | Atom |

### 订阅配置

| 设置 | 说明 |
|------|------|
| 订阅页面大小 | 每页条目数 |
| 订阅需要认证 | 需要认证 |
| 订阅密码 | 自定义订阅密码 |
| 显示 Atom | 启用/禁用订阅 |

### 导出格式

| 格式 | 命令/方式 | 使用场景 |
|------|-----------|----------|
| HTML | Web 界面 | 浏览器导入 |
| JSON | API | 备份、迁移 |
| CSV | API | 电子表格 |
| Netscape | 文件 | 浏览器导入 |

### API 访问

```bash
# 获取所有链接
curl -H "Authorization: Bearer YOUR_API_TOKEN" \
  http://localhost:8080/api/v1/links

# 创建链接
curl -X POST \
  -H "Authorization: Bearer YOUR_API_TOKEN" \
  -H "Content-Type: application/json" \
  -d '{"url":"https://example.com","title":"Example","tags":["test"]}' \
  http://localhost:8080/api/v1/links
```

## 插件系统

### 可用插件

| 插件 | 说明 |
|------|------|
| Wallabagger | 从 Wallabag 导入 |
| FeedInject | 从 RSS 添加链接 |
| QRCode | 生成二维码 |
| Share2Clipboard | 复制分享 URL |
| MarkdownExport | 导出为 Markdown |
| Readability | 提取文章内容 |

### 插件配置

| 步骤 | 操作 |
|------|------|
| 1 | 导航到插件管理 |
| 2 | 启用所需插件 |
| 3 | 配置插件设置 |
| 4 | 保存配置 |

### 插件开发

| 组件 | 说明 |
|------|------|
| 插件目录 | `plugins/` 文件夹 |
| 注册 | 插件元数据文件 |
| 钩子 | 基于事件的系统 |
| 模板 | 自定义 UI 元素 |

## 自定义

### 主题系统

| 主题 | 说明 |
|------|------|
| 默认 | 简洁、极简 |
| Material | Material Design |
| 自定义 | 用户创建的主题 |

### 自定义 CSS

| 位置 | 方式 |
|------|------|
| 自定义 CSS 文件 | `data/user.css` |
| 主题覆盖 | 修改模板 |
| 插件 CSS | 通过插件系统 |

### 链接模板

| 模板 | 使用场景 |
|------|----------|
| 默认 | 标准链接显示 |
| 紧凑 | 最小视图 |
| 详细 | 扩展信息 |

## 备份与恢复

| 组件 | 位置 | 方法 |
|------|------|------|
| 数据库 | `data/shaarli.db` | 文件复制 |
| 配置 | `data/config.php` | 文件复制 |
| 插件 | `plugins/` | 文件同步 |
| 主题 | `tpl/` | 文件同步 |

## 总结

Shaarli 提供了一个轻量级的自托管书签解决方案，具有强大的标签和搜索功能。其最低的资源需求、插件系统和多种订阅格式使其成为个人链接管理和分享的理想选择。


---

## 来源：bookmark.md

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


---

## 来源：read.md

## 简介

Wallabag 是一个自托管的稍后阅读应用。它保存网页文章供离线阅读，去除广告和干扰。本教程涵盖安装、配置、浏览器集成和高级功能。

## Wallabag 与 Pocket、Instapaper 对比

| 功能 | Wallabag | Pocket | Instapaper |
|------|----------|--------|------------|
| 自托管 | 是 | 否 | 否 |
| 开源 | 是 | 否 | 否 |
| 导出格式 | EPUB、PDF、MOBI、CSV、JSON、XML | EPUB、PDF | EPUB、PDF |
| API | 是 | 是 | 是 |
| 标签 | 是 | 是 | 是 |
| 标注 | 是 | 是（高级版） | 是 |
| 全文搜索 | 是 | 是 | 是 |
| 价格 | 免费 | 免费增值 | 免费增值 |

## 安装

### Docker Compose

```yaml
version: '3'
services:
  wallabag:
    image: wallabag/wallabag:latest
    container_name: wallabag
    restart: unless-stopped
    environment:
      - SYMFONY__ENV__DOMAIN_NAME=https://read.example.com
      - SYMFONY__ENV__SERVER_NAME=Wallabag
      - SYMFONY__ENV__DATABASE_DRIVER=pdo_sqlite
      - SYMFONY__ENV__FOSUSER_REGISTRATION=false
    volumes:
      - ./wallabag-images:/var/www/wallabag/web/assets/images
      - ./wallabag-data:/var/www/wallabag/data
    ports:
      - "8080:80"
```

### 手动安装

```bash
git clone https://github.com/wallabag/wallabag.git
cd wallabag
composer install --no-dev -o --prefer-dist
php bin/console wallabag:install
```

## 核心功能

### 保存文章

| 方式 | 方法 |
|------|------|
| 浏览器扩展 | 点击 Wallabag 图标 |
| 书签工具 | JavaScript 书签 |
| URL 提交 | 在 Web 界面粘贴 URL |
| API | POST 到 /api/entries |
| RSS 导入 | 从 feed 导入 |
| Pocket 导入 | 从 Pocket 导入 |
| Instapaper 导入 | 从 Instapaper 导入 |
| Pinboard 导入 | 从 Pinboard 导入 |

### 文章属性

| 属性 | 描述 |
|------|------|
| Title | 文章标题 |
| URL | 原始链接 |
| Content | 清理后的文章文本 |
| Preview picture | 主图 |
| Reading time | 预计阅读分钟数 |
| Tags | 用户分配的标签 |
| Starred | 收藏状态 |
| Archived | 已读状态 |
| Annotations | 用户高亮和笔记 |

## Web 界面

### 导航

| 部分 | 用途 |
|------|------|
| Unread | 待读的新文章 |
| Starred | 收藏文章 |
| Archive | 已读文章 |
| Tags | 按标签浏览 |
| Search | 全文搜索 |
| Config | 账户设置 |

### 文章操作

| 操作 | 方法 |
|------|------|
| 收藏 | 点击星标图标 |
| 归档 | 点击归档图标 |
| 添加标签 | 给文章添加标签 |
| 删除 | 点击删除图标 |
| 分享 | 生成公开链接 |
| 打开原文 | 访问源 URL |
| 编辑 | 修改标题或内容 |

## 浏览器扩展

| 浏览器 | 安装 |
|--------|------|
| Chrome | Chrome Web Store |
| Firefox | Firefox Add-ons |
| Safari | Mac App Store |
| Opera | Opera Add-ons |

### 扩展功能

| 功能 | 描述 |
|------|------|
| 一键保存 | 保存当前页面 |
| 保存选区 | 保存选中的文本 |
| 带标签保存 | 保存时添加标签 |
| 自动归档 | 保存后归档 |
| 徽章计数 | 显示未读数量 |

## 移动应用

| 平台 | 应用名称 |
|------|---------|
| Android | Wallabag（F-Droid、Play Store） |
| iOS | Wallabag（App Store） |

### 应用配置

| 设置 | 值 |
|------|-----|
| Server URL | https://your-wallabag-instance.com |
| Username | 你的 Wallabag 用户名 |
| Password | 你的 Wallabag 密码 |
| Client ID | 来自 API 客户端管理 |
| Client Secret | 来自 API 客户端管理 |

## 标签

### 标签管理

| 操作 | 方法 |
|------|------|
| 添加标签 | 在文章的标签字段中输入 |
| 移除标签 | 点击标签上的 X |
| 重命名标签 | 标签管理页面 |
| 删除标签 | 标签管理页面 |
| 合并标签 | 标签管理页面 |

### 标签策略

| 策略 | 示例 |
|------|------|
| 按主题 | programming、design、science |
| 按优先级 | read-later、urgent、reference |
| 按来源 | newsletter、twitter、reddit |
| 按状态 | to-review、archived-reference |

## 标注

### 创建标注

1. 打开一篇文章。
2. 选择文本。
3. 点击"Annotate"。
4. 添加你的笔记。
5. 保存标注。

### 标注类型

| 类型 | 用途 |
|------|------|
| Highlight（高亮） | 标记重要文本 |
| Note（笔记） | 添加评论 |

## API 参考

### 认证

```bash
# 获取 OAuth2 令牌
curl -X POST https://read.example.com/oauth/v2/token \
  -d "grant_type=password" \
  -d "client_id=YOUR_CLIENT_ID" \
  -d "client_secret=YOUR_CLIENT_SECRET" \
  -d "username=YOUR_USERNAME" \
  -d "password=YOUR_PASSWORD"
```

### API 端点

| 方法 | 端点 | 描述 |
|------|------|------|
| GET | /api/entries | 列出所有条目 |
| POST | /api/entries | 创建条目 |
| GET | /api/entries/{id} | 获取条目 |
| PUT | /api/entries/{id} | 更新条目 |
| DELETE | /api/entries/{id} | 删除条目 |
| GET | /api/tags | 列出所有标签 |
| POST | /api/entries/{id}/tags | 给条目添加标签 |
| GET | /api/entries/{id}/export | 导出条目 |

### 导出格式

| 格式 | 扩展名 | 用例 |
|------|--------|------|
| EPUB | .epub | 电子阅读器 |
| PDF | .pdf | 打印 |
| MOBI | .mobi | Kindle |
| CSV | .csv | 数据分析 |
| JSON | .json | API 集成 |
| XML | .xml | 数据交换 |

## 导入和导出

### 导入来源

| 来源 | 方法 |
|------|------|
| Pocket | CSV 文件 |
| Instapaper | CSV 文件 |
| Pinboard | JSON/CSV 文件 |
| Readability | JSON 文件 |
| Firefox | JSON 书签 |
| Chrome | HTML 书签 |
| Wallabag | JSON 导出 |

### 导出

| 格式 | 命令 |
|------|------|
| 所有条目 | Settings > Export > 选择格式 |
| 按标签 | 按标签过滤，然后导出 |
| 按状态 | 过滤未读/收藏/归档，然后导出 |

## 配置

### 环境变量

| 变量 | 用途 | 默认值 |
|------|------|--------|
| SYMFONY__ENV__DOMAIN_NAME | 公开 URL | 必填 |
| SYMFONY__ENV__DATABASE_DRIVER | 数据库类型 | pdo_sqlite |
| SYMFONY__ENV__DATABASE_HOST | 数据库主机 | localhost |
| SYMFONY__ENV__DATABASE_NAME | 数据库名称 | wallabag |
| SYMFONY__ENV__DATABASE_USER | 数据库用户 | wallabag |
| SYMFONY__ENV__DATABASE_PASSWORD | 数据库密码 | wallabag |
| SYMFONY__ENV__FOSUSER_REGISTRATION | 允许注册 | false |

### 数据库选项

| 数据库 | 驱动 | 用例 |
|--------|------|------|
| SQLite | pdo_sqlite | 单用户，简单设置 |
| MySQL/MariaDB | pdo_mysql | 多用户，生产环境 |
| PostgreSQL | pdo_pgsql | 多用户，生产环境 |

## 自定义

### 自定义 CSS

在 Configuration > Settings > Custom CSS 中添加自定义样式。

### 阅读设置

| 设置 | 选项 |
|------|------|
| 字体 | Serif、Sans-serif |
| 字体大小 | Small、Medium、Large |
| 行高 | Compact、Normal、Relaxed |
| 暗色模式 | 开、关、自动 |

## 故障排除

| 问题 | 原因 | 解决方案 |
|------|------|---------|
| 无法保存文章 | JavaScript 密集型网站 | 尝试阅读模式 |
| 图片缺失 | 热链保护 | 检查代理设置 |
| 导入缓慢 | 文件过大 | 分批导入 |
| 登录失败 | 凭据错误 | 通过 CLI 重置密码 |
| API 401 | 令牌无效 | 重新生成 OAuth 凭据 |

## 总结

Wallabag 提供了一个自托管的、尊重隐私的稍后阅读解决方案。其浏览器扩展、移动应用和 API 让你在任何设备上轻松保存和阅读文章。导出选项、标签系统和标注功能使其成为研究和知识管理的强大工具。


---
