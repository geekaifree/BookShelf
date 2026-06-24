# DokuWiki 教程：搭建自托管 Wiki

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
