# 使用 MediaWiki 搭建 Wiki 平台

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
