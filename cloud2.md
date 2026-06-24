# Nextcloud：自托管云平台指南

## 目录

1. [Nextcloud 简介](#introduction)
2. [安装方式](#installation)
3. [初始配置](#configuration)
4. [文件管理](#file-management)
5. [应用与扩展](#apps)
6. [协作功能](#collaboration)
7. [安全加固](#security)
8. [管理](#administration)

---

## 简介

Nextcloud 是一个自托管的生产力平台，让你完全掌控自己的数据。它提供与商业云服务相当的文件同步、分享和协作工具。

### Nextcloud 核心功能

| 功能 | 描述 | 好处 |
|------|------|------|
| 文件同步 | 跨设备同步 | 随处访问 |
| 分享 | 内部和外部 | 便捷协作 |
| 日历 | CalDAV 日历 | 日程管理 |
| 联系人 | CardDAV 联系人 | 联系人管理 |
| Talk | 视频会议 | 团队沟通 |

### Nextcloud vs 商业服务

| 功能 | Nextcloud | Google Drive | Dropbox |
|------|-----------|--------------|---------|
| 自托管 | 是 | 否 | 否 |
| 数据控制 | 完全 | 有限 | 有限 |
| 成本 | 免费 (OSS) | 订阅 | 订阅 |
| 隐私 | 符合 GDPR | 数据挖掘 | 数据挖掘 |
| 可扩展 | 300+ 应用 | 有限 | 有限 |

### 系统要求

| 组件 | 最低 | 推荐 |
|------|------|------|
| CPU | 1 核 | 2+ 核 |
| 内存 | 512MB | 2GB+ |
| 存储 | 10GB | 100GB+ |
| PHP | 8.0 | 8.2 |
| 数据库 | SQLite | MySQL/PostgreSQL |

---

## 安装方式

Nextcloud 可以通过多种方式安装，取决于你的环境。

### Docker 安装

```yaml
# docker-compose.yml
version: '3'
services:
  nextcloud:
    image: nextcloud:latest
    ports:
      - 8080:80
    volumes:
      - nextcloud:/var/www/html
      - ./data:/var/www/html/data
    environment:
      - MYSQL_HOST=db
      - MYSQL_DATABASE=nextcloud
      - MYSQL_USER=nextcloud
      - MYSQL_PASSWORD=secret
      - NEXTCLOUD_ADMIN_USER=admin
      - NEXTCLOUD_ADMIN_PASSWORD=admin_password
    depends_on:
      - db
  
  db:
    image: mysql:8
    volumes:
      - db:/var/lib/mysql
    environment:
      - MYSQL_ROOT_PASSWORD=root_password
      - MYSQL_DATABASE=nextcloud
      - MYSQL_USER=nextcloud
      - MYSQL_PASSWORD=secret

volumes:
  nextcloud:
  db:
```

### Web 安装器

| 步骤 | 操作 | 备注 |
|------|------|------|
| 1 | 下载 | nextcloud.com/install |
| 2 | 解压 | 到 Web 根目录 |
| 3 | 设置权限 | www-data 所有权 |
| 4 | 运行向导 | 浏览器设置 |

### Snap 安装

```bash
# Ubuntu/Debian
sudo snap install nextcloud
```

### 手动安装步骤

| 步骤 | 操作 | 命令/配置 |
|------|------|-----------|
| 1 | 安装 PHP | apt install php8.2 |
| 2 | 安装扩展 | ctype, curl, dom... |
| 3 | 安装数据库 | MySQL 或 PostgreSQL |
| 4 | 下载 Nextcloud | 解压到 Web 根目录 |
| 5 | 配置 Web 服务器 | Apache 或 Nginx |
| 6 | 运行安装器 | 浏览器向导 |

---

## 初始配置

配置 Nextcloud 以获得最佳性能和安全性。

### 基本设置

| 设置 | 位置 | 推荐值 |
|------|------|--------|
| 域名 | config.php | 你的域名 |
| 可信域名 | config.php | 添加所有域名 |
| 默认语言 | 管理设置 | 用户偏好 |
| 时区 | 管理设置 | 服务器时区 |

### config.php 关键设置

```php
<?php
$CONFIG = array (
  'trusted_domains' => array (
    0 => 'localhost',
    1 => 'cloud.example.com',
  ),
  'datadirectory' => '/var/www/nextcloud/data',
  'dbtype' => 'mysql',
  'version' => '28.0.0',
  'overwrite.cli.url' => 'https://cloud.example.com',
  'htaccess.RewriteBase' => '/',
);
```

### 数据库配置

| 数据库 | 优点 | 缺点 |
|--------|------|------|
| SQLite | 简单设置 | 不适合生产 |
| MySQL | 广泛使用 | 资源消耗 |
| PostgreSQL | 高级功能 | 略复杂 |
| MariaDB | MySQL 兼容 | 推荐 |

### PHP 配置

| 设置 | 推荐值 | 位置 |
|------|--------|------|
| memory_limit | 512M | php.ini |
| upload_max_filesize | 16G | php.ini |
| post_max_size | 16G | php.ini |
| max_execution_time | 3600 | php.ini |

---

## 文件管理

Nextcloud 提供全面的文件管理功能。

### 上传方式

| 方式 | 描述 | 限制 |
|------|------|------|
| Web UI | 浏览器上传 | 文件大小限制 |
| 桌面客户端 | 自动同步 | 存储空间 |
| 移动应用 | 手动/自动上传 | 网络速度 |
| WebDAV | 直接协议 | 客户端支持 |
| CLI | OCC 命令 | 服务器访问 |

### 文件操作

| 操作 | Web UI | 桌面 | 移动 |
|------|--------|------|------|
| 上传 | 是 | 自动 | 是 |
| 下载 | 是 | 自动 | 是 |
| 分享 | 是 | 是 | 是 |
| 删除 | 是 | 是 | 是 |
| 移动 | 是 | 是 | 否 |
| 版本历史 | 是 | 是 | 否 |

### 存储配置

| 后端 | 描述 | 用途 |
|------|------|------|
| 本地 | 服务器磁盘 | 主存储 |
| S3 | 对象存储 | 可扩展存储 |
| SMB/CIFS | 网络共享 | 企业 |
| External | FTP, SFTP | 旧系统 |

### 配额管理

| 设置 | 范围 | 配置 |
|------|------|------|
| 默认配额 | 所有用户 | 管理设置 |
| 用户配额 | 个人 | 用户设置 |
| 群组配额 | 群组 | 群组设置 |

---

## 应用与扩展

Nextcloud 拥有丰富的应用生态系统来扩展功能。

### 必备应用

| 应用 | 类别 | 描述 |
|------|------|------|
| Calendar | 生产力 | CalDAV 日历 |
| Contacts | 生产力 | CardDAV 联系人 |
| Talk | 通信 | 视频通话、聊天 |
| Mail | 通信 | 邮件客户端 |
| Deck | 项目管理 | 看板 |

### 办公与文档

| 应用 | 描述 | 格式 |
|------|------|------|
| Collabora Online | 办公套件 | DOC, XLS, PPT |
| OnlyOffice | 办公套件 | DOC, XLS, PPT |
| Text | Markdown 编辑器 | MD, TXT |
| Markdown Editor | MD 编辑 | MD 文件 |

### 媒体与文件

| 应用 | 描述 | 功能 |
|------|------|------|
| Photos | 照片库 | 相册、分享 |
| Music | 音频播放器 | 串流 |
| Preview Generator | 缩略图 | 图片预览 |
| Files PDF viewer | PDF 查看 | 浏览器内 |

### 安装应用

| 步骤 | 操作 | 位置 |
|------|------|------|
| 1 | 打开应用 | 管理菜单 |
| 2 | 浏览分类 | 已启用/已禁用 |
| 3 | 搜索 | 搜索栏 |
| 4 | 安装 | 点击安装 |
| 5 | 启用 | 开关打开 |

### 应用管理

| 操作 | 命令 | 效果 |
|------|------|------|
| 列出应用 | `occ app:list` | 显示已安装 |
| 启用 | `occ app:enable <app>` | 激活 |
| 禁用 | `occ app:disable <app>` | 停用 |
| 更新 | `occ app:update <app>` | 获取最新 |

---

## 协作功能

Nextcloud 在团队协作和沟通方面表现出色。

### 文件分享

| 分享类型 | 描述 | 权限 |
|----------|------|------|
| 内部 | 用户或群组 | 读、写、分享 |
| 链接 | 公开 URL | 读、写、密码 |
| 联邦 | 其他 Nextcloud | 读、写 |
| 邮件 | 发送链接 | 读、写 |

### Talk（视频会议）

| 功能 | 描述 | 容量 |
|------|------|------|
| 视频通话 | 一对一和群组 | 最多 100 用户 |
| 屏幕分享 | 分享桌面 | 全屏或应用 |
| 聊天 | 文字消息 | 持久化 |
| 文件分享 | 通话中分享 | 直接集成 |

### 日历功能

| 功能 | 描述 | 协议 |
|------|------|------|
| 事件 | 创建、编辑、删除 | CalDAV |
| 重复 | 重复事件 | RRULE |
| 提醒 | 通知 | VALARM |
| 分享 | 分享日历 | 内部/外部 |
| 导入/导出 | ICS 文件 | iCalendar |

### 协作编辑

| 工具 | 实时 | 格式 | 集成 |
|------|------|------|------|
| Collabora | 是 | Office 文档 | 内置 |
| OnlyOffice | 是 | Office 文档 | 插件 |
| Text | 是 | Markdown | 内置 |
| Cryptpad | 是 | 多种 | 插件 |

---

## 安全加固

保护 Nextcloud 安装对数据安全至关重要。

### 安全清单

| 项目 | 优先级 | 实施方式 |
|------|--------|----------|
| HTTPS | 关键 | SSL 证书 |
| 强密码 | 关键 | 密码策略 |
| 2FA | 高 | TOTP 或 U2F |
| 暴力破解防护 | 高 | 内置 |
| 安全头 | 中等 | Web 服务器配置 |

### SSL/TLS 配置

```nginx
# Nginx SSL configuration
server {
    listen 443 ssl http2;
    server_name cloud.example.com;
    
    ssl_certificate /etc/letsencrypt/live/cloud.example.com/fullchain.pem;
    ssl_certificate_key /etc/letsencrypt/live/cloud.example.com/privkey.pem;
    
    ssl_protocols TLSv1.2 TLSv1.3;
    ssl_ciphers ECDHE-ECDSA-AES128-GCM-SHA256:ECDHE-RSA-AES128-GCM-SHA256;
}
```

### 双因素认证

| 方式 | 安全性 | 用户体验 |
|------|--------|----------|
| TOTP | 高 | 需要应用 |
| U2F/WebAuthn | 最高 | 硬件密钥 |
| SMS | 中等 | 需要手机 |
| Email | 中等 | 需要邮箱 |

### 安全扫描器

| 分数 | 含义 | 操作 |
|------|------|------|
| A+ | 优秀 | 保持 |
| A | 良好 | 小改进 |
| B | 一般 | 需要安全加固 |
| C 或以下 | 差 | 需要立即行动 |

### 暴力破解防护

| 设置 | 默认值 | 推荐 |
|------|--------|------|
| 最大尝试次数 | 10 | 5 |
| 超时 | 30s | 300s |
| 白名单 | 无 | 你的 IP |

---

## 管理

Nextcloud 的日常管理任务。

### 用户管理

| 任务 | 管理 UI | OCC 命令 |
|------|---------|----------|
| 创建用户 | 用户页面 | `occ user:add` |
| 删除用户 | 用户页面 | `occ user:delete` |
| 设置配额 | 用户页面 | `occ user:setting` |
| 禁用用户 | 用户页面 | `occ user:disable` |

### 群组管理

| 任务 | 命令 | 示例 |
|------|------|------|
| 创建群组 | `occ group:add` | `occ group:add developers` |
| 添加用户 | `occ group:adduser` | `occ group:adduser john developers` |
| 移除用户 | `occ group:removeuser` | `occ group:removeuser john developers` |
| 列出群组 | `occ group:list` | 显示所有群组 |

### 备份策略

| 组件 | 方法 | 频率 |
|------|------|------|
| 数据库 | mysqldump | 每天 |
| 数据目录 | rsync | 每天 |
| 配置 | 文件复制 | 每周 |
| 应用 | OCC 导出 | 每周 |

### 维护命令

| 命令 | 用途 | 何时使用 |
|------|------|----------|
| `occ maintenance:mode --on` | 启用维护模式 | 更新时 |
| `occ maintenance:mode --off` | 禁用维护模式 | 更新后 |
| `occ files:scan --all` | 重新扫描文件 | 文件丢失时 |
| `occ db:add-missing-indices` | 修复数据库 | 性能问题 |

### 监控

| 指标 | 工具 | 阈值 |
|------|------|------|
| 磁盘使用 | 系统工具 | < 80% |
| 数据库大小 | OCC 命令 | 监控增长 |
| 用户活动 | 管理审计 | 异常模式 |
| 性能 | 服务器日志 | 响应时间 |

---

## 总结

| 主题 | 核心要点 |
|------|----------|
| 安装 | 推荐 Docker 简化部署 |
| 配置 | PHP 调优对大文件很重要 |
| 应用 | 丰富的生产力生态系统 |
| 协作 | 内置分享、Talk、日历 |
| 安全 | HTTPS、2FA 和定期更新 |
| 管理 | OCC 命令用于维护 |
