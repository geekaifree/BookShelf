# 使用 Shaarli 进行链接分享

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
