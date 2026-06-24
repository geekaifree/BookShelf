# 云平台与部署

> 本文档整合了以下源文件：cloud.md, cloud2.md, paas.md, coolify.md, aws.md

---

## 来源：cloud.md

## 简介

Cloudreve 是一个开源的自托管云存储平台，支持多种存储提供商。它提供 Web 界面用于文件管理、共享和协作。本教程涵盖设置、存储配置、用户管理和高级功能。

## 架构

| 组件 | 技术 | 用途 |
|------|------|------|
| 后端 | Go | API 服务器和业务逻辑 |
| 前端 | React | Web 界面 |
| 数据库 | SQLite/MySQL/PostgreSQL | 用户和文件元数据 |
| 存储 | 本地/S3/OSS/OneDrive | 文件存储后端 |
| 队列 | 内置 | 后台任务 |

## 安装

### Docker Compose

```yaml
version: "3"
services:
  cloudreve:
    image: cloudreve/cloudreve:latest
    ports:
      - "5212:5212"
    volumes:
      - cloudreve_data:/cloudreve/data
      - cloudreve_uploads:/cloudreve/uploads
    environment:
      - CR_CONF_DB_TYPE=sqlite
    restart: unless-stopped
volumes:
  cloudreve_data:
  cloudreve_uploads:
```

### 二进制安装

```bash
# 下载最新版本
wget https://github.com/cloudreve/Cloudreve/releases/latest/download/cloudreve_linux_amd64.tar.gz
tar -xzf cloudreve_linux_amd64.tar.gz
chmod +x cloudreve

# 运行
./cloudreve
```

### Systemd 服务

```ini
[Unit]
Description=Cloudreve
After=network.target

[Service]
Type=simple
ExecStart=/opt/cloudreve/cloudreve
WorkingDirectory=/opt/cloudreve
Restart=always
RestartSec=5

[Install]
WantedBy=multi-user.target
```

## 存储策略

### 支持的后端

| 后端 | 协议 | 使用场景 |
|------|------|----------|
| 本地 | 文件系统 | 小型部署 |
| Amazon S3 | S3 API | 可扩展存储 |
| 阿里云 OSS | S3 兼容 | 中国云 |
| 腾讯 COS | S3 兼容 | 中国云 |
| 七牛 | S3 兼容 | 中国云 |
| OneDrive | Microsoft Graph | 个人/团队存储 |
| 远程 | 自定义 API | 自定义后端 |

### 配置本地存储

1. 导航到 Dashboard > Storage Policies。
2. 点击"Create New Policy"。
3. 选择"Local"作为后端。
4. 设置存储路径（例如 `/data/uploads`）。
5. 设置上传大小限制和允许的扩展名。
6. 保存策略。

### 配置 S3 存储

| 设置 | 描述 | 示例 |
|------|------|------|
| Bucket Name | S3 存储桶 | `cloudreve-storage` |
| Region | AWS 区域 | `us-east-1` |
| Endpoint | S3 端点 | `https://s3.amazonaws.com` |
| Access Key | IAM 访问密钥 | `AKIAIOSFODNN7EXAMPLE` |
| Secret Key | IAM 密钥 | `wJalrXUtnFEMI/K7MDENG` |
| Base URL | 公共 URL | `https://cdn.example.com` |

### S3 策略 JSON

```json
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Effect": "Allow",
      "Action": [
        "s3:PutObject",
        "s3:GetObject",
        "s3:DeleteObject"
      ],
      "Resource": "arn:aws:s3:::cloudreve-storage/*"
    },
    {
      "Effect": "Allow",
      "Action": "s3:ListBucket",
      "Resource": "arn:aws:s3:::cloudreve-storage"
    }
  ]
}
```

## 用户管理

### 用户组

| 组 | 权限 | 使用场景 |
|----|------|----------|
| Admin | 完全系统控制 | 管理员 |
| Default | 标准文件操作 | 普通用户 |
| VIP | 扩展存储和功能 | 高级用户 |
| 匿名 | 有限的公共访问 | 访客下载 |

### 组设置

| 设置 | 描述 |
|------|------|
| 存储配额 | 每用户最大存储 |
| 最大文件大小 | 单文件上传限制 |
| 速度限制 | 上传/下载速度上限 |
| 允许的扩展名 | 允许的文件类型 |
| 共享设置 | 公共链接选项 |

### 创建用户

| 方法 | 步骤 |
|------|------|
| 手动 | Dashboard > Users > Create User |
| 注册 | 在设置中启用自注册 |
| 导入 | 通过 CSV 批量导入 |

## 文件管理

### Web 界面功能

| 功能 | 描述 |
|------|------|
| 上传 | 拖拽或点击上传 |
| 下载 | 单文件或批量下载 |
| 预览 | 图片、视频、音频、文档预览 |
| 重命名 | 重命名文件和文件夹 |
| 移动 | 在文件夹间移动 |
| 复制 | 复制文件 |
| 删除 | 移至回收站或永久删除 |
| 搜索 | 全文文件名搜索 |

### WebDAV 访问

Cloudreve 支持 WebDAV 用于挂载为网络驱动器。

```
URL: https://cloudreve.example.com/dav/
Username: your-email@example.com
Password: your-password
```

#### macOS 挂载

```bash
mount_webdav -s -v CloudDrive https://cloudreve.example.com/dav/ /Volumes/CloudDrive
```

#### Linux 挂载

```bash
# 安装 davfs2
sudo apt install davfs2

# 挂载
sudo mount -t davfs https://cloudreve.example.com/dav/ /mnt/cloudreve
```

## 共享

### 共享类型

| 类型 | 描述 | 安全性 |
|------|------|--------|
| 公共链接 | 任何有链接的人都能访问 | 可选密码 |
| 过期链接 | 超时后自动过期 | 限时 |
| 用户共享 | 与特定用户共享 | 用户认证 |
| 文件夹共享 | 共享整个文件夹 | 文件夹级访问 |

### 共享设置

| 设置 | 描述 |
|------|------|
| 密码 | 用密码保护 |
| 过期 | 设置链接过期日期 |
| 下载限制 | 最大下载次数 |
| 仅预览 | 允许预览但不允许下载 |

### 创建共享

1. 选择文件或文件夹。
2. 点击工具栏中的"Share"。
3. 配置设置（密码、过期）。
4. 复制共享链接。

## 相册和图库

### 图片图库功能

| 功能 | 描述 |
|------|------|
| 创建相册 | 将图片分组到相册 |
| 缩略图生成 | 自动生成预览图 |
| EXIF 提取 | 显示照片元数据 |
| 幻灯片 | 按顺序查看图片 |
| 公共图库 | 公开分享相册 |

## 通知

### 通知类型

| 类型 | 触发 | 渠道 |
|------|------|------|
| 上传完成 | 文件上传成功 | 应用内 |
| 共享创建 | 生成新共享链接 | 邮箱 |
| 存储警告 | 配额即将满 | 邮箱 |
| 系统更新 | 新版本可用 | 应用内 |

## 任务队列

### 后台任务

| 任务 | 描述 | 状态 |
|------|------|------|
| 缩略图生成 | 创建图片预览 | 异步 |
| 文件解压 | 解压归档 | 异步 |
| 远程下载 | 从 URL 下载 | 异步 |
| 存储迁移 | 在后端间移动文件 | 异步 |

## API 访问

### REST API

| 端点 | 方法 | 描述 |
|------|------|------|
| `/api/v3/user/login` | POST | 用户认证 |
| `/api/v3/file/upload` | POST | 上传文件 |
| `/api/v3/file/list` | GET | 列出目录内容 |
| `/api/v3/file/download/{id}` | GET | 下载文件 |
| `/api/v3/share/create` | POST | 创建共享链接 |
| `/api/v3/directory/create` | POST | 创建文件夹 |

### 认证

```bash
# 登录并获取会话 cookie
curl -X POST https://cloudreve.example.com/api/v3/user/login \
  -H "Content-Type: application/json" \
  -d '{"username": "user@example.com", "password": "password"}'
```

## 自定义

### 站点设置

| 设置 | 描述 |
|------|------|
| 站点名称 | 显示名称 |
| 站点描述 | SEO 描述 |
| Logo | 自定义 logo 图片 |
| Favicon | 浏览器标签图标 |
| 注册 | 启用/禁用自注册 |
| 默认语言 | 界面语言 |

### 自定义主题

通过 CSS 覆盖修改前端外观。

## 反向代理

### Nginx 配置

```nginx
server {
    listen 443 ssl;
    server_name cloud.example.com;

    ssl_certificate /etc/letsencrypt/live/cloud.example.com/fullchain.pem;
    ssl_certificate_key /etc/letsencrypt/live/cloud.example.com/privkey.pem;

    client_max_body_size 1000M;

    location / {
        proxy_pass http://localhost:5212;
        proxy_set_header Host $host;
        proxy_set_header X-Real-IP $remote_addr;
        proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
        proxy_set_header X-Forwarded-Proto $scheme;
    }
}
```

## 备份

### 备份策略

| 组件 | 方法 | 频率 |
|------|------|------|
| 数据库 | mysqldump/pg_dump/sqlite 复制 | 每日 |
| 上传文件 | rsync 或 rclone | 每日 |
| 配置 | 文件复制 | 每周 |
| 存储策略文件 | 存储原生复制 | 持续 |

## 故障排除

| 问题 | 解决方案 |
|------|----------|
| 上传失败 | 检查文件大小限制和存储配额 |
| 上传缓慢 | 验证网络和反向代理限制 |
| 预览不工作 | 安装 LibreOffice 用于文档预览 |
| WebDAV 错误 | 检查认证和代理配置 |
| 存储后端错误 | 验证凭证和权限 |

## 总结

Cloudreve 提供了完整的自托管云存储解决方案，支持多种后端、WebDAV 访问、文件共享和简洁的 Web 界面。使用 Docker 部署，配置本地或 S3 兼容后端的存储策略，通过管理仪表板管理用户。它是商业云存储服务的实用替代方案。


---

## 来源：cloud2.md

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


---

## 来源：paas.md

## 简介

Coolify 是一个开源的、自托管的平台即服务（PaaS），简化了在自己的服务器上部署和管理应用程序、数据库和服务的过程。它提供了类似 Heroku 的体验，没有供应商锁定。本教程涵盖设置、部署工作流程和管理功能。

## 架构

| 组件 | 技术 | 用途 |
|------|------|------|
| UI | SvelteKit | Web 仪表板 |
| Agent | Go | 服务器管理 |
| Proxy | Traefik | 反向代理和 TLS |
| 数据库 | SQLite/PostgreSQL | 配置存储 |
| 容器 | Docker | 应用运行时 |

## 安装

### 一键安装

```bash
curl -fsSL https://cdn.coollabs.io/coolify/install.sh | bash
```

### Docker Compose

```yaml
version: "3.7"
services:
  coolify:
    image: coollabs/coolify:latest
    ports:
      - "8000:8000"
    volumes:
      - coolify_data:/app/data
    environment:
      - APP_ID=coolify
      - DB_URL=postgresql://coolify:password@database:5432/coolify
    depends_on:
      - database
  database:
    image: postgres:15-alpine
    environment:
      POSTGRES_DB: coolify
      POSTGRES_USER: coolify
      POSTGRES_PASSWORD: password
    volumes:
      - db_data:/var/lib/postgresql/data
volumes:
  coolify_data:
  db_data:
```

## 服务器管理

### 添加服务器

| 类型 | 描述 | 设置 |
|------|------|------|
| 本地 | 与 Coolify 同一台机器 | 自动检测 |
| 远程 SSH | 通过 SSH 连接另一台服务器 | 添加 SSH 密钥 |
| VPS | 云提供商服务器 | 配置并连接 |

### 服务器要求

| 资源 | 最低配置 | 推荐配置 |
|------|----------|----------|
| CPU | 1 核 | 2+ 核 |
| 内存 | 1 GB | 4+ GB |
| 存储 | 20 GB | 50+ GB |
| 操作系统 | Ubuntu 22.04 | Ubuntu 22.04/Debian 12 |

### SSH 密钥设置

```bash
# 生成 SSH 密钥
ssh-keygen -t ed25519 -C "coolify@server"

# 复制到远程服务器
ssh-copy-id -i ~/.ssh/id_ed25519.pub user@remote-server
```

## 应用部署

### 部署来源

| 来源 | 描述 | 配置 |
|------|------|------|
| Git 仓库 | 从 GitHub/GitLab 部署 | 连接仓库，设置分支 |
| Docker 镜像 | 从注册表部署 | 指定镜像标签 |
| Docker Compose | 多容器应用 | 上传或粘贴 compose 文件 |
| 静态站点 | HTML/CSS/JS 文件 | 上传或 Git 来源 |
| Nixpacks | 自动检测构建 | 自动配置 |

### 从 Git 部署

| 步骤 | 操作 |
|------|------|
| 1 | 点击"New Resource" |
| 2 | 选择"Application" |
| 3 | 选择"Git Repository" |
| 4 | 连接 GitHub/GitLab 账户 |
| 5 | 选择仓库和分支 |
| 6 | 配置构建设置 |
| 7 | 部署 |

### 构建配置

| 设置 | 描述 | 示例 |
|------|------|------|
| Build Pack | 构建方式 | Nixpacks、Dockerfile、Static |
| Base Directory | 源代码子目录 | `/app` |
| Port | 应用端口 | `3000` |
| Install Command | 依赖安装 | `npm install` |
| Build Command | 构建步骤 | `npm run build` |
| Start Command | 运行时命令 | `npm start` |

### Dockerfile 部署

```dockerfile
FROM node:18-alpine
WORKDIR /app
COPY package*.json ./
RUN npm ci --only=production
COPY . .
EXPOSE 3000
CMD ["node", "server.js"]
```

### Docker Compose 部署

```yaml
version: "3"
services:
  web:
    build: .
    ports:
      - "3000:3000"
    environment:
      - DATABASE_URL=postgresql://user:pass@db:5432/app
    depends_on:
      - db
  db:
    image: postgres:15
    environment:
      POSTGRES_DB: app
      POSTGRES_USER: user
      POSTGRES_PASSWORD: pass
    volumes:
      - pg_data:/var/lib/postgresql/data
volumes:
  pg_data:
```

## 数据库

### 支持的数据库

| 数据库 | 版本 | 使用场景 |
|--------|------|----------|
| PostgreSQL | 14、15、16 | 通用 |
| MySQL | 5.7、8.0 | Web 应用 |
| MariaDB | 10.x | MySQL 兼容 |
| MongoDB | 5、6、7 | 文档存储 |
| Redis | 6、7 | 缓存、会话 |
| CouchDB | 3.x | 文档同步 |
| Dragonfly | 最新 | Redis 替代 |

### 创建数据库

1. 点击"New Resource"。
2. 选择"Database"。
3. 选择数据库类型。
4. 配置设置（名称、用户、密码）。
5. 部署。

### 数据库配置

| 设置 | 描述 |
|------|------|
| Name | 数据库名称 |
| User | 数据库用户名 |
| Password | 数据库密码 |
| Port | 外部端口映射 |
| Volume | 持久数据存储 |
| Extensions | 附加模块 |

## 域名和 SSL

### 自定义域名设置

1. 导航到应用设置。
2. 点击"Domains"。
3. 添加你的域名（例如 `app.example.com`）。
4. 配置 DNS A 记录指向服务器 IP。
5. Coolify 通过 Let's Encrypt 自动配置 SSL。

### 域名配置

| 设置 | 描述 | 示例 |
|------|------|------|
| Domain | 主域名 | `app.example.com` |
| www redirect | 将 www 重定向到非 www | `www.app.example.com` |
| Force HTTPS | 将 HTTP 重定向到 HTTPS | 已启用 |
| Custom SSL | 上传证书 | 手动配置 |

### 通配符域名

用于多租户应用：

```
*.app.example.com -> application
```

## 环境变量

### 管理环境变量

| 功能 | 描述 |
|------|------|
| 键值对 | 为容器设置变量 |
| 构建时 | 构建期间可用 |
| 运行时 | 执行期间可用 |
| 共享 | 跨服务共享 |
| Secrets | 加密存储 |

### 示例变量

| 键 | 值 | 范围 |
|----|----|----|
| `NODE_ENV` | `production` | 运行时 |
| `DATABASE_URL` | `postgresql://...` | 运行时 |
| `API_KEY` | `sk-xxx` | 构建 + 运行时 |
| `PORT` | `3000` | 运行时 |

## 扩展和资源

### 资源限制

| 设置 | 描述 | 示例 |
|------|------|------|
| CPU Limit | 最大 CPU 核数 | `2.0` |
| Memory Limit | 最大内存 | `512MB` |
| CPU Reservation | 保证 CPU | `0.5` |
| Memory Reservation | 保证内存 | `256MB` |

### 水平扩展

```yaml
# 当你增加实例数时，Coolify 自动配置负载均衡
services:
  web:
    instances: 3  # 运行 3 个副本
```

## 监控

### 内置监控

| 指标 | 描述 | 访问 |
|------|------|------|
| CPU 使用率 | 每容器 CPU | 仪表板 |
| 内存使用率 | 每容器内存 | 仪表板 |
| 磁盘使用率 | 存储消耗 | 仪表板 |
| 网络 | 流入/流出流量 | 仪表板 |
| 日志 | 应用输出 | 仪表板 |

### 查看日志

1. 导航到应用。
2. 点击"Logs"标签。
3. 查看实时容器日志。
4. 按时间范围或搜索筛选。

## 备份

### 备份配置

| 组件 | 方法 | 频率 |
|------|------|------|
| 数据库 | 内置备份 | 每日 |
| 卷 | 快照 | 可配置 |
| 配置 | 导出 | 手动 |

### 数据库备份

```bash
# 自动备份到 S3 兼容存储
# 在 Coolify 设置中配置：
# - S3 Endpoint
# - Bucket name
# - Access key
# - Secret key
# - Schedule（cron 表达式）
```

## Webhooks 和 CI/CD

### 自动部署

| 触发器 | 描述 | 配置 |
|--------|------|------|
| Git push | 推送到分支时部署 | 在设置中启用 |
| Pull request | 部署 PR 预览 | 启用 PR 部署 |
| Webhook | 手动触发 | POST 到 webhook URL |
| 定时 | 基于 cron 的重新部署 | 设置计划 |

### GitHub Webhook

```json
{
  "url": "https://coolify.example.com/api/webhooks/deploy/xxx",
  "events": ["push"],
  "active": true
}
```

## 服务

### 一键服务

Coolify 提供预配置的服务。

| 类别 | 服务 |
|------|------|
| 分析 | Plausible、Umami、Matomo |
| CMS | WordPress、Ghost、Strapi |
| 通信 | Rocket.Chat、Mattermost |
| 开发工具 | Gitea、Drone、Portainer |
| 监控 | Uptime Kuma、Grafana |
| 存储 | MinIO、Nextcloud |

### 安装服务

1. 点击"New Resource"。
2. 选择"Service"。
3. 从服务目录中选择。
4. 配置设置。
5. 部署。

## 团队和权限

| 角色 | 权限 |
|------|------|
| Owner | 完全控制 |
| Admin | 管理服务器和应用 |
| Member | 查看和部署分配的应用 |

## API 访问

### REST API

```bash
# 列出应用
curl -H "Authorization: Bearer TOKEN" \
  https://coolify.example.com/api/v1/applications

# 部署应用
curl -X POST -H "Authorization: Bearer TOKEN" \
  https://coolify.example.com/api/v1/applications/{id}/deploy
```

## 故障排除

| 问题 | 解决方案 |
|------|----------|
| 构建失败 | 检查构建日志，验证 Dockerfile |
| SSL 不工作 | 验证 DNS 记录，检查端口 80 访问 |
| 数据库连接被拒绝 | 检查网络设置，验证凭证 |
| 高资源使用 | 审查资源限制，检查内存泄漏 |
| 部署卡住 | 重启 Coolify agent |

## 总结

Coolify 提供了自托管的 PaaS 体验，支持多种部署来源、数据库和服务。它通过简洁的 Web 界面处理 SSL、监控和扩展。从 Git 仓库、Docker 镜像或 Docker Compose 文件部署，从单一仪表板管理一切。


---

## 来源：coolify.md

Coolify 综合教程，这是一个开源的自托管平台即服务（PaaS）。在你自己的服务器上部署应用、数据库和服务，获得类似 Heroku 的体验。

## 目录

- [什么是 Coolify](#什么是-coolify)
- [安装](#安装)
- [部署应用](#部署应用)
- [服务](#服务)
- [数据库](#数据库)
- [SSL 和域名](#ssl-和域名)
- [监控](#监控)
- [备份](#备份)
- [团队管理](#团队管理)
- [API](#api)
- [Git 集成](#git-集成)
- [环境变量](#environment-variables)

---

## 什么是 Coolify

### 概述

Coolify 是 Heroku、Netlify 和 Vercel 的开源自托管替代方案。它运行在你自己的服务器上，提供 Web 界面来部署应用、数据库和服务。

### 核心特性

| 特性 | 描述 |
|---------|-------------|
| 推送部署 | 从 Git 自动部署 |
| 多服务器 | 从一个仪表板管理多个服务器 |
| 基于 Docker | 所有部署运行在 Docker 容器中 |
| SSL 自动化 | 自动 Let's Encrypt 证书 |
| 数据库管理 | PostgreSQL、MySQL、MongoDB、Redis |
| 服务模板 | 一键部署流行应用 |
| 团队协作 | 多用户角色访问 |
| API | REST API 用于自动化 |
| Webhooks | 与外部工具集成 |
| 监控 | 内置资源监控 |
| 备份 | 自动备份到 S3 等 |

### 与替代方案对比

| 特性 | Coolify | Heroku | Vercel | Railway |
|---------|---------|--------|--------|---------|
| 自托管 | 是 | 否 | 否 | 否 |
| 开源 | 是 | 否 | 否 | 否 |
| 免费层 | 自托管（免费） | 已停止 | 是 | 有限 |
| 数据库 | 是 | 是 | 否 | 是 |
| 自定义域名 | 是 | 是 | 是 | 是 |
| Docker 支持 | 是 | 是 | 有限 | 是 |
| 多服务器 | 是 | 否 | 否 | 否 |
| 无供应商锁定 | 是 | 否 | 否 | 否 |

---

## 安装

### 系统要求

| 要求 | 最低 | 推荐 |
|-------------|---------|-------------|
| CPU | 1 核 | 2+ 核 |
| RAM | 2 GB | 4+ GB |
| 存储 | 20 GB | 50+ GB |
| 系统 | Ubuntu 22.04、Debian 12、CentOS 9 | Ubuntu 22.04 LTS |
| 端口 | 80、443、8000 | 80、443、8000 |

### 快速安装

```bash
# 一键安装命令
curl -fsSL https://cdn.coollabs.io/coolify/install.sh | bash
```

### 手动安装

```bash
# 安装 Docker
curl -fsSL https://get.docker.com | bash

# 创建目录
mkdir -p /data/coolify

# 运行 Coolify
docker run -d \
  --name coolify \
  --restart=always \
  -p 8000:8000 \
  -v /data/coolify:/data/coolify \
  -v /var/run/docker.sock:/var/run/docker.sock \
  coollabsio/coolify:latest
```

### 安装后步骤

| 步骤 | 操作 | 详情 |
|------|--------|---------|
| 1 | 访问 UI | 打开 http://your-server-ip:8000 |
| 2 | 创建账户 | 设置管理员用户 |
| 3 | 配置服务器 | 添加第一台服务器 |
| 4 | 设置 DNS | 将域名指向服务器 |
| 5 | 添加 SSH 密钥 | 用于 Git 仓库访问 |

### 支持的提供商

| 提供商 | 类型 | 用例 |
|----------|------|----------|
| 自托管 | VPS/独立服务器 | 完全控制 |
| Hetzner | 云 VPS | 经济实惠的欧洲服务器 |
| DigitalOcean | 云 VPS | 易于使用 |
| AWS EC2 | 云 | 企业功能 |
| Linode | 云 VPS | 对开发者友好 |
| Vultr | 云 VPS | 全球位置 |
| 任意 SSH 服务器 | 远程 | 现有基础设施 |

---

## 部署应用

### 部署方式

| 方式 | 描述 | 最适合 |
|--------|-------------|----------|
| Git 仓库 | 从 GitHub/GitLab 部署 | CI/CD 工作流 |
| Docker 镜像 | 拉取并运行现有镜像 | 预构建应用 |
| Docker Compose | 多容器应用 | 复杂方案 |
| 静态站点 | 部署 HTML/CSS/JS | 网站 |
| 一键服务 | 预配置模板 | 常见应用 |

### Git 仓库部署

| 步骤 | 操作 |
|------|--------|
| 1 | 点击仪表板中的"New Resource" |
| 2 | 选择"Application" |
| 3 | 选择"Public Repository"或连接 Git 提供商 |
| 4 | 输入仓库 URL 和分支 |
| 5 | 配置构建设置 |
| 6 | 设置环境变量 |
| 7 | 部署 |

### 构建包检测

Coolify 自动检测你的应用类型：

| 语言 | 检测方式 | 构建包 |
|----------|-----------------|------------|
| Node.js | package.json | NPM/Yarn |
| Python | requirements.txt、Pipfile | Python |
| PHP | composer.json | PHP |
| Ruby | Gemfile | Ruby |
| Go | go.mod | Go |
| Rust | Cargo.toml | Rust |
| Docker | Dockerfile | Docker |
| 静态 | index.html | Static |

### 构建配置

| 设置 | 描述 | 默认值 |
|---------|-------------|---------|
| 构建包 | 应用类型 | 自动检测 |
| 基础目录 | 构建的子目录 | /（根目录） |
| 构建命令 | 自定义构建命令 | 语言默认 |
| 启动命令 | 自定义启动命令 | 语言默认 |
| 端口 | 应用端口 | 3000 |
| 安装命令 | 依赖安装 | 语言默认 |

### 部署策略

| 策略 | 描述 | 停机时间 |
|----------|-------------|----------|
| 滚动 | 逐个替换容器 | 零 |
| 重建 | 停止所有，启动新的 | 短暂 |
| 蓝绿 | 切换流量到新版本 | 零 |

---

## 服务

Coolify 包含许多流行服务的一键部署。

### Web 服务器和代理

| 服务 | 描述 | 用例 |
|---------|-------------|----------|
| Nginx | Web 服务器和反向代理 | 静态站点、负载均衡 |
| Caddy | 自动 HTTPS Web 服务器 | 简单 Web 托管 |
| Traefik | 动态反向代理 | 微服务 |
| HAProxy | 负载均衡 | 高可用性 |

### 内容管理

| 服务 | 描述 | 用例 |
|---------|-------------|----------|
| WordPress | 博客和 CMS | 网站、博客 |
| Ghost | 发布平台 | 博客、通讯 |
| Strapi | 无头 CMS | API 优先内容 |
| Directus | 无头 CMS | 数据驱动内容 |
| Plausible | Web 分析 | 隐私优先分析 |
| Matomo | Web 分析 | 全功能分析 |

### 通信

| 服务 | 描述 | 用例 |
|---------|-------------|----------|
| Rocket.Chat | 团队聊天 | 团队通信 |
| Mattermost | 团队聊天 | Slack 替代 |
| Matrix/Element | 联邦聊天 | 去中心化消息 |
| n8n | 工作流自动化 | 集成平台 |
| Chatwoot | 客户支持 | 帮助台 |

### 开发工具

| 服务 | 描述 | 用例 |
|---------|-------------|----------|
| Gitea | Git 托管 | 自托管 GitHub |
| GitLab | DevOps 平台 | 完整 DevOps |
| Drone | CI/CD | 持续集成 |
| Woodpecker CI | CI/CD | 轻量 CI |
| Uptime Kuma | 可用性监控 | 服务监控 |
| Stirling PDF | PDF 工具 | 文档处理 |

### 媒体和存储

| 服务 | 描述 | 用例 |
|---------|-------------|----------|
| Nextcloud | 云存储 | 文件共享 |
| MinIO | 对象存储 | S3 兼容存储 |
| Immich | 照片管理 | Google Photos 替代 |
| Navidrome | 音乐服务器 | 音乐流媒体 |
| Jellyfin | 媒体服务器 | 视频流媒体 |

### 数据库和缓存

| 服务 | 描述 | 用例 |
|---------|-------------|----------|
| Redis | 内存缓存 | 缓存、会话 |
| Memcached | 内存缓存 | 简单缓存 |
| KeyDB | Redis 替代 | 高性能 |
| Dragonfly | Redis 替代 | 现代缓存 |

---

## 数据库

### 支持的数据库

| 数据库 | 类型 | 版本 | 用例 |
|----------|------|----------|----------|
| PostgreSQL | 关系型 | 14、15、16 | 通用、JSON |
| MySQL | 关系型 | 5.7、8.0 | Web 应用 |
| MariaDB | 关系型 | 10.x | MySQL 兼容 |
| MongoDB | 文档型 | 5、6、7 | 灵活模式 |
| Redis | 键值 | 6、7 | 缓存、队列 |
| Dragonfly | 键值 | 最新 | 高性能 |

### 数据库配置

| 设置 | 描述 | 默认值 |
|---------|-------------|---------|
| 名称 | 数据库名称 | 必填 |
| 用户 | 数据库用户 | admin |
| 密码 | 数据库密码 | 自动生成 |
| 端口 | 外部端口 | 自动分配 |
| 卷 | 数据持久化 | Docker 卷 |
| 最大连接数 | 连接限制 | 数据库默认 |

### 连接字符串

| 数据库 | 连接字符串格式 |
|----------|------------------------|
| PostgreSQL | `postgres://user:pass@host:5432/dbname` |
| MySQL | `mysql://user:pass@host:3306/dbname` |
| MongoDB | `mongodb://user:pass@host:27017/dbname` |
| Redis | `redis://:pass@host:6379` |

### 数据库管理

| 功能 | 描述 |
|---------|-------------|
| 创建 | 一键创建数据库 |
| 备份 | 自动和手动备份 |
| 恢复 | 从备份恢复 |
| 监控 | 连接数、内存使用 |
| 日志 | UI 中的数据库日志 |
| 终端 | 直接数据库控制台 |

---

## SSL 和域名

### 自动 SSL

Coolify 自动为你的域名配置 Let's Encrypt 证书。

| 功能 | 描述 |
|---------|-------------|
| 自动配置 | 证书自动创建 |
| 自动续期 | 到期前续期 |
| 通配符 | 支持 DNS 挑战 |
| 自定义证书 | 上传你自己的证书 |

### 域名配置

| 步骤 | 操作 | 详情 |
|------|--------|---------|
| 1 | 为应用添加域名 | 在应用设置中 |
| 2 | 配置 DNS | 将 A/CNAME 记录指向服务器 |
| 3 | 等待传播 | 通常 5-60 分钟 |
| 4 | SSL 已配置 | 自动 Let's Encrypt |

### DNS 记录类型

| 类型 | 记录 | 值 | 用例 |
|------|--------|-------|----------|
| A | app.example.com | 服务器 IP | 直接域名 |
| CNAME | app.example.com | other.domain.com | 别名 |
| 通配符 | *.example.com | 服务器 IP | 所有子域名 |

### SSL 证书选项

| 提供商 | 方式 | 费用 |
|----------|--------|------|
| Let's Encrypt | HTTP-01 挑战 | 免费 |
| Let's Encrypt | DNS-01 挑战 | 免费 |
| 自定义 | 上传证书 | 不定 |
| Cloudflare | 代理 | 免费/付费 |

---

## 监控

### 内置监控

| 指标 | 描述 |
|--------|-------------|
| CPU 使用率 | 服务器和容器 CPU |
| 内存使用率 | RAM 利用率 |
| 磁盘使用率 | 存储消耗 |
| 网络 I/O | 传入和传出流量 |
| 容器状态 | 运行、停止、错误 |
| 正常运行时间 | 服务可用性 |

### 资源监控

| 资源 | 仪表板视图 | 告警阈值 |
|----------|---------------|-----------------|
| CPU | 实时图表 | 持续 80% |
| 内存 | 实时图表 | 持续 85% |
| 磁盘 | 使用百分比 | 90% 满 |
| 网络 | 带宽图表 | 异常检测 |

### 日志管理

| 日志类型 | 访问方式 | 保留时间 |
|----------|--------------|-----------|
| 应用日志 | UI / CLI | 默认 7 天 |
| 构建日志 | UI | 每次部署 |
| 系统日志 | SSH | 系统默认 |
| 容器日志 | `docker logs` | 可配置 |

### 与外部工具集成

| 工具 | 集成 | 用途 |
|------|-------------|---------|
| Grafana | API | 高级仪表板 |
| Prometheus | 指标端点 | 指标收集 |
| Uptime Kuma | 服务模板 | 可用性监控 |
| n8n | Webhooks | 告警自动化 |

---

## 备份

### 备份类型

| 类型 | 备份内容 | 存储 |
|------|-----------------|---------|
| 数据库备份 | 完整数据库转储 | S3、FTP、本地 |
| 配置 | 应用设置 | 包含在 Coolify 数据中 |
| 卷 | 持久数据 | 手动或 S3 |

### S3 兼容备份存储

| 提供商 | 端点示例 |
|----------|-----------------|
| AWS S3 | s3.amazonaws.com |
| DigitalOcean Spaces | nyc3.digitaloceanspaces.com |
| MinIO | minio.example.com |
| Backblaze B2 | s3.us-west-000.backblazeb2.com |
| Cloudflare R2 | r2.cloudflarestorage.com |
| Hetzner Storage | fsn1.your-objectstorage.com |

### 备份配置

```yaml
# 备份设置
S3_BUCKET: coolify-backups
S3_ENDPOINT: s3.amazonaws.com
S3_ACCESS_KEY: your-access-key
S3_SECRET_KEY: your-secret-key
S3_REGION: us-east-1
BACKUP_FREQUENCY: daily  # daily, weekly, monthly
BACKUP_RETENTION: 7      # 保留备份数量
```

### 备份计划选项

| 频率 | 描述 | 保留 |
|-----------|-------------|-----------|
| 每小时 | 每小时 | 24 个备份 |
| 每天 | 每天一次 | 7-30 个备份 |
| 每周 | 每周一次 | 4-12 个备份 |
| 每月 | 每月一次 | 12 个备份 |
| 自定义 | Cron 表达式 | 自定义 |

### 恢复流程

| 步骤 | 操作 |
|------|--------|
| 1 | 导航到备份部分 |
| 2 | 选择要恢复的备份 |
| 3 | 选择目标数据库 |
| 4 | 确认恢复 |
| 5 | 验证数据完整性 |

---

## 团队管理

### 用户角色

| 角色 | 权限 |
|------|-------------|
| 所有者 | 完全访问、计费、团队管理 |
| 管理员 | 除计费外完全访问 |
| 成员 | 部署和管理分配的资源 |
| 查看者 | 只读访问 |

### 团队功能

| 功能 | 描述 |
|---------|-------------|
| 多团队 | 创建独立团队 |
| 资源共享 | 团队间共享资源 |
| 活动日志 | 跟踪谁做了什么 |
| API 密钥 | 每用户 API 访问 |
| SSO | 单点登录（企业版） |

### 访问控制

| 级别 | 描述 |
|-------|-------------|
| 服务器 | 用户可访问哪些服务器 |
| 应用 | 用户可管理哪些应用 |
| 数据库 | 用户可访问哪些数据库 |
| 设置 | 谁可以更改团队设置 |

---

## API

### API 概述

Coolify 提供 REST API 用于自动化和集成。

| 功能 | 描述 |
|---------|-------------|
| 认证 | Bearer token |
| 基础 URL | http://your-server:8000/api/v1 |
| 格式 | JSON |
| 文档 | OpenAPI/Swagger |

### 常用 API 操作

| 操作 | 方法 | 端点 |
|-----------|--------|----------|
| 列出应用 | GET | /api/v1/applications |
| 获取应用 | GET | /api/v1/applications/{id} |
| 部署应用 | POST | /api/v1/applications/{id}/deploy |
| 列出数据库 | GET | /api/v1/databases |
| 列出服务器 | GET | /api/v1/servers |
| 获取部署 | GET | /api/v1/deployments |

### API 认证

```bash
# 在 Settings > API 生成 API 密钥
# 在请求中使用：
curl -H "Authorization: Bearer YOUR_API_KEY" \
  http://your-server:8000/api/v1/applications
```

### Webhook 集成

| 触发器 | URL | 负载 |
|---------|-----|---------|
| GitHub Push | Coolify webhook URL | GitHub 负载 |
| GitLab Push | Coolify webhook URL | GitLab 负载 |
| 手动部署 | API 端点 | 自定义负载 |

---

## Git 集成

### 支持的提供商

| 提供商 | 功能 | 设置 |
|----------|----------|-------|
| GitHub | 仓库、PR、webhooks | OAuth 应用 |
| GitLab | 仓库、MR、webhooks | OAuth 应用 |
| Gitea | 仓库、PR、webhooks | OAuth 应用 |
| Bitbucket | 仓库、PR、webhooks | OAuth 应用 |
| 公共仓库 | 任何公共 URL | 无需设置 |

### GitHub 集成

| 步骤 | 操作 |
|------|--------|
| 1 | 创建 GitHub OAuth 应用 |
| 2 | 设置回调 URL 到 Coolify |
| 3 | 在 Coolify 中输入 Client ID 和 Secret |
| 4 | 在 GitHub 中授权 Coolify |
| 5 | 选择要部署的仓库 |

### 自动部署

| 触发器 | 描述 |
|---------|-------------|
| 推送到分支 | 每次推送部署 |
| 创建标签 | 版本标签时部署 |
| Pull request | 预览部署 |
| 手动 | 点击部署按钮 |

### 预览部署

| 功能 | 描述 |
|---------|-------------|
| PR 预览 | 每个 PR 有自己的 URL |
| 自动清理 | PR 关闭时删除 |
| 环境变量 | 与生产环境分离 |
| 自定义域名 | 可选的每预览域名 |

---

## 环境变量

### 变量管理

| 功能 | 描述 |
|---------|-------------|
| UI 编辑 | 在 Web 界面设置变量 |
| 构建时 | 构建期间可用 |
| 运行时 | 执行期间可用 |
| 共享 | 多应用间共享 |
| 多行 | 支持证书、密钥 |

### 变量作用域

| 作用域 | 描述 | 构建时 | 运行时 |
|-------|-------------|------------|---------|
| 构建 | 仅构建期间 | 是 | 否 |
| 运行时 | 仅运行时 | 否 | 是 |
| 两者 | 构建和运行时 | 是 | 是 |

### 密钥管理

| 方式 | 描述 | 安全级别 |
|--------|-------------|----------------|
| 环境变量 | 键值对 | 基础 |
| Docker secrets | 静态加密 | 高 |
| 外部保险库 | HashiCorp Vault 等 | 最高 |
| .env 文件 | 基于文件的密钥 | 基础 |

### 变量示例

```bash
# 数据库连接
DATABASE_URL=postgres://user:pass@db:5432/myapp

# 应用设置
NODE_ENV=production
APP_PORT=3000
APP_SECRET=your-secret-key

# 第三方 API 密钥
STRIPE_SECRET_KEY=sk_live_...
SMTP_HOST=smtp.example.com
SMTP_PORT=587
SMTP_USER=user@example.com
SMTP_PASS=password
```

### 最佳实践

| 实践 | 描述 |
|----------|-------------|
| 敏感数据使用密钥 | 永远不要提交 API 密钥 |
| 分组相关变量 | 使用命名约定 |
| 记录变量 | 包含 .env.example |
| 定期轮换密钥 | 定期更改密码 |
| 每环境使用不同值 | 开发 vs 生产 |

---

## 高级配置

### 自定义 Docker Compose

```yaml
# 复杂应用的 docker-compose.yml
version: "3.8"

services:
  web:
    build: .
    ports:
      - "3000:3000"
    environment:
      - DATABASE_URL=${DATABASE_URL}
    depends_on:
      - db
      - redis

  worker:
    build: .
    command: celery worker
    environment:
      - REDIS_URL=${REDIS_URL}

  db:
    image: postgres:16
    volumes:
      - pgdata:/var/lib/postgresql/data

  redis:
    image: redis:7-alpine

volumes:
  pgdata:
```

### 资源限制

| 设置 | 描述 | 示例 |
|---------|-------------|---------|
| 内存限制 | 最大 RAM | 512M、1G |
| CPU 限制 | 最大 CPU 核心 | 0.5、1、2 |
| 内存预留 | 保证 RAM | 256M |
| CPU 预留 | 保证 CPU | 0.25 |

### 自定义 Nginx 配置

```nginx
# 自定义代理配置
location /api {
    proxy_pass http://app:3000;
    proxy_set_header Host $host;
    proxy_set_header X-Real-IP $remote_addr;
    proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
    proxy_set_header X-Forwarded-Proto $scheme;
}
```

---

## 故障排除

### 常见问题

| 问题 | 原因 | 解决方案 |
|---------|-------|----------|
| 部署失败 | 构建错误 | 检查构建日志 |
| SSL 不工作 | DNS 未配置 | 验证 DNS 记录 |
| 无法连接数据库 | 凭据错误 | 检查环境变量 |
| 内存不足 | 资源限制 | 增加内存限制 |
| 端口冲突 | 另一服务占用端口 | 更改端口映射 |
| 构建缓慢 | 大仓库 | 使用 .dockerignore |

### 常用命令

```bash
# 检查 Coolify 状态
docker ps | grep coolify

# 查看 Coolify 日志
docker logs coolify

# 重启 Coolify
docker restart coolify

# 检查磁盘空间
df -h

# 检查 Docker 磁盘使用
docker system df

# 清理 Docker
docker system prune -a
```

### 健康检查

| 检查 | 命令 | 预期结果 |
|-------|---------|-----------------|
| Coolify 运行 | `docker ps` | coolify 容器运行中 |
| 端口可访问 | `curl localhost:8000` | HTML 响应 |
| DNS 解析 | `dig your-domain.com` | 服务器 IP |
| SSL 有效 | `curl https://your-domain.com` | 有效证书 |

---

## 总结

Coolify 让自托管对每个人都触手可及。通过其直观的 Web 界面，你无需深入的 DevOps 知识即可部署应用、数据库和服务。

关键要点：
- 在任何 Linux 服务器上一键安装
- 从 Git 仓库自动部署
- 管理数据库并备份
- 自动 Let's Encrypt SSL
- 基于角色的团队协作
- API 用于高级自动化

从单台服务器开始，按需扩展。Coolify 会随你的项目一起成长。


---

## 来源：aws.md

## 目录

1. [AWS 简介](#introduction)
2. [账号设置与安全](#account)
3. [计算服务](#compute)
4. [存储服务](#storage)
5. [数据库服务](#database)
6. [网络](#networking)
7. [安全服务](#security)
8. [成本管理](#cost)

---

## 简介

Amazon Web Services (AWS) 是一个综合云平台，提供 200 多种服务。本指南涵盖构建和部署应用最关键的服务。

### AWS 全球基础设施

| 组件 | 描述 | 数量 |
|------|------|------|
| 区域 | 地理区域 | 33 |
| 可用区 | 数据中心 | 105+ |
| 边缘节点 | CDN 端点 | 600+ |

### AWS 服务类别

| 类别 | 服务 | 用途 |
|------|------|------|
| 计算 | EC2, Lambda, ECS | 运行应用 |
| 存储 | S3, EBS, EFS | 存储数据 |
| 数据库 | RDS, DynamoDB, Aurora | 数据管理 |
| 网络 | VPC, Route 53, CloudFront | 网络基础设施 |
| 安全 | IAM, KMS, WAF | 保护资源 |

### AWS vs 其他提供商

| 功能 | AWS | Azure | GCP |
|------|-----|-------|-----|
| 市场份额 | 32% | 23% | 10% |
| 服务数 | 200+ | 200+ | 100+ |
| 区域 | 33 | 60+ | 40+ |
| 免费层 | 12 个月 | 12 个月 | 永久免费 |

---

## 账号设置与安全

从一开始就安全地设置你的 AWS 账号。

### 账号创建

| 步骤 | 操作 | 备注 |
|------|------|------|
| 1 | 访问 aws.amazon.com | 开始注册 |
| 2 | 创建账号 | 邮箱、密码 |
| 3 | 支付方式 | 需要信用卡 |
| 4 | 验证身份 | 电话验证 |
| 5 | 选择支持计划 | 基础（免费） |

### 根账号安全

| 操作 | 优先级 | 实施方式 |
|------|--------|----------|
| 强密码 | 关键 | 20+ 字符 |
| MFA | 关键 | 虚拟或硬件 |
| 不日常使用 | 关键 | 使用 IAM 用户 |
| 安全凭据 | 关键 | 密码管理器 |

### IAM 最佳实践

| 实践 | 描述 | 实施方式 |
|------|------|----------|
| 最小权限 | 最低权限 | IAM 策略 |
| 根账号不日常使用 | 使用 IAM 用户 | 创建用户 |
| 全面 MFA | 多因素认证 | 全部启用 |
| 轮换凭据 | 定期更换 | 90 天轮换 |
| 使用角色 | 用于服务 | EC2 实例角色 |

### IAM 用户和组

| 实体 | 用途 | 最佳实践 |
|------|------|----------|
| User | 个人访问 | 每人一个 |
| Group | 权限集 | 按角色分组 |
| Role | 服务访问 | 用于应用 |
| Policy | 权限规则 | JSON 文档 |

---

## 计算服务

AWS 计算服务用于运行应用。

### EC2 (Elastic Compute Cloud)

| 实例类型 | 用途 | 示例 |
|----------|------|------|
| t3.micro | 小型工作负载 | 开发 |
| m5.large | 通用 | Web 服务器 |
| c5.xlarge | 计算密集 | 批处理 |
| r5.2xlarge | 内存密集 | 数据库 |
| p3.2xlarge | GPU 工作负载 | 机器学习 |

### EC2 定价模型

| 模型 | 描述 | 节省 |
|------|------|------|
| On-Demand | 按小时付费 | 无 |
| Reserved | 1-3 年承诺 | 最高 75% |
| Spot | 竞价 | 最高 90% |
| Savings Plans | 灵活承诺 | 最高 72% |

### Lambda (Serverless)

| 功能 | 描述 | 好处 |
|------|------|------|
| 无服务器 | 托管基础设施 | 无运维 |
| 按使用付费 | 按请求+持续时间 | 成本效益 |
| 自动扩展 | 自动缩放 | 处理任何负载 |
| 事件驱动 | 由事件触发 | 反应式 |

### Lambda 限制

| 限制 | 值 | 可调整 |
|------|-----|--------|
| 内存 | 128MB - 10GB | 是 |
| 超时 | 15 分钟 | 是 |
| 包大小 | 250MB | 是 |
| 并发执行 | 1000 | 是 |

### ECS (Elastic Container Service)

| 启动类型 | 描述 | 用途 |
|----------|------|------|
| Fargate | 无服务器容器 | 无基础设施管理 |
| EC2 | 托管实例 | 更多控制 |

### 容器服务对比

| 服务 | 描述 | 复杂度 |
|------|------|--------|
| ECS | 容器编排 | 中等 |
| EKS | Kubernetes | 高 |
| Fargate | 无服务器容器 | 低 |
| App Runner | 简单部署 | 极低 |

---

## 存储服务

AWS 存储方案满足不同需求。

### S3 (Simple Storage Service)

| 存储类别 | 用途 | 成本 | 检索 |
|----------|------|------|------|
| Standard | 频繁访问 | 较高 | 即时 |
| Intelligent-Tiering | 未知模式 | 不定 | 即时 |
| Standard-IA | 不频繁访问 | 较低 | 即时 |
| One Zone-IA | 可重建数据 | 最低 | 即时 |
| Glacier | 归档 | 极低 | 分钟-小时 |
| Glacier Deep Archive | 长期归档 | 最低 | 12 小时 |

### S3 桶操作

| 操作 | 描述 | API |
|------|------|-----|
| 创建桶 | 创建存储容器 | PUT |
| 上传对象 | 存储文件 | PUT |
| 下载对象 | 获取文件 | GET |
| 删除对象 | 移除文件 | DELETE |
| 列出对象 | 浏览内容 | GET |

### EBS (Elastic Block Store)

| 卷类型 | 用途 | IOPS | 吞吐量 |
|--------|------|------|--------|
| gp3 | 通用 | 3000-16000 | 125-1000 MB/s |
| io2 | 高性能 | 64000 | 1000 MB/s |
| st1 | 吞吐优化 | 500 | 500 MB/s |
| sc1 | 冷存储 | 250 | 250 MB/s |

### EFS (Elastic File System)

| 功能 | 描述 | 用途 |
|------|------|------|
| 共享访问 | 多实例 | 内容管理 |
| 弹性 | 自动增长 | 可变工作负载 |
| NFS 协议 | 标准文件系统 | 旧应用 |

### 存储服务对比

| 服务 | 类型 | 访问 | 用途 |
|------|------|------|------|
| S3 | 对象 | HTTP/HTTPS | 静态文件、备份 |
| EBS | 块 | 挂载到 EC2 | 数据库、文件系统 |
| EFS | 文件 | NFS 挂载 | 共享存储 |
| FSx | 托管 | Windows/NFS | 企业应用 |

---

## 数据库服务

针对不同工作负载的托管数据库服务。

### RDS (Relational Database Service)

| 引擎 | 用途 | 功能 |
|------|------|------|
| MySQL | Web 应用 | 流行、开源 |
| PostgreSQL | 复杂查询 | 高级功能 |
| MariaDB | MySQL 兼容 | 开源 |
| Oracle | 企业 | 商业许可 |
| SQL Server | Windows 工作负载 | Microsoft 生态 |

### RDS 功能

| 功能 | 描述 | 好处 |
|------|------|------|
| Multi-AZ | 高可用 | 自动故障转移 |
| Read Replicas | 扩展读取 | 性能 |
| 自动备份 | 时间点恢复 | 数据保护 |
| 加密 | 静态和传输中 | 安全 |

### DynamoDB

| 功能 | 描述 | 用途 |
|------|------|------|
| NoSQL | 键值和文档 | 灵活模式 |
| 个位数 ms | 低延迟 | 高性能 |
| 自动扩展 | 容量调整 | 可变工作负载 |
| Global Tables | 多区域 | 全球应用 |

### DynamoDB vs RDS

| 功能 | DynamoDB | RDS |
|------|----------|-----|
| 类型 | NoSQL | 关系型 |
| 模式 | 灵活 | 固定 |
| 扩展 | 自动 | 手动 |
| 延迟 | 个位数 ms | 毫秒 |
| 成本 | 按请求 | 按小时 |

### Aurora

| 功能 | 描述 | 好处 |
|------|------|------|
| MySQL 兼容 | 直接替换 | 轻松迁移 |
| PostgreSQL 兼容 | 直接替换 | 轻松迁移 |
| 5x 更快 | 比标准 MySQL | 性能 |
| 自动扩展 | 存储自动缩放 | 无需容量规划 |

### ElastiCache

| 引擎 | 用途 | 功能 |
|------|------|------|
| Redis | 缓存、会话 | 丰富数据结构 |
| Memcached | 简单缓存 | 多线程 |

---

## 网络

AWS 网络服务用于连接和分发。

### VPC (Virtual Private Cloud)

| 组件 | 描述 | 必需 |
|------|------|------|
| VPC | 虚拟网络 | 是 |
| Subnet | 网络段 | 是 |
| Internet Gateway | 公网访问 | 公共子网 |
| Route Table | 流量路由 | 是 |
| Security Group | 实例防火墙 | 是 |
| Network ACL | 子网防火墙 | 可选 |

### 子网类型

| 类型 | 描述 | 路由 |
|------|------|------|
| Public | 可访问互联网 | 通过 Internet Gateway |
| Private | 无直接互联网 | 通过 NAT Gateway |
| Isolated | 完全无互联网 | 无路由 |

### Security Groups vs NACLs

| 功能 | Security Groups | NACLs |
|------|-----------------|-------|
| 级别 | 实例 | 子网 |
| 状态 | 有状态 | 无状态 |
| 规则 | 仅允许 | 允许和拒绝 |
| 默认 | 拒绝所有 | 允许所有 |

### Route 53 (DNS)

| 记录类型 | 用途 | 示例 |
|----------|------|------|
| A | IPv4 地址 | 192.0.2.1 |
| AAAA | IPv6 地址 | 2001:db8::1 |
| CNAME | 域名别名 | www.example.com |
| MX | 邮件服务器 | mail.example.com |

### CloudFront (CDN)

| 功能 | 描述 | 好处 |
|------|------|------|
| 全球边缘 | 600+ 位置 | 低延迟 |
| 缓存 | 静态内容 | 更快分发 |
| SSL/TLS | 加密 | 安全 |
| Lambda@Edge | 边缘无服务器 | 自定义逻辑 |

### 负载均衡器

| 类型 | 层级 | 用途 |
|------|------|------|
| Application (ALB) | HTTP/HTTPS | Web 应用 |
| Network (NLB) | TCP/UDP | 高性能 |
| Gateway (GWLB) | Layer 3 | 安全设备 |

---

## 安全服务

AWS 安全服务保护你的基础设施。

### IAM (Identity and Access Management)

| 资源 | 用途 | 最佳实践 |
|------|------|----------|
| Users | 个人访问 | 最小权限 |
| Groups | 权限集 | 按角色分组 |
| Roles | 服务访问 | 用于应用 |
| Policies | 权限规则 | JSON 文档 |

### KMS (Key Management Service)

| 功能 | 描述 | 用途 |
|------|------|------|
| 密钥创建 | 生成密钥 | 加密 |
| 密钥轮换 | 自动轮换 | 合规 |
| 集成 | AWS 服务 | S3, EBS, RDS |

### WAF (Web Application Firewall)

| 防护 | 描述 | 规则 |
|------|------|------|
| SQL 注入 | 阻止恶意查询 | 托管规则 |
| XSS | 阻止跨站脚本 | 托管规则 |
| 速率限制 | 限制请求 | 基于 IP |
| 地理封锁 | 按国家阻止 | 地理 |

### Shield

| 级别 | 防护 | 成本 |
|------|------|------|
| Standard | 基础 DDoS | 免费 |
| Advanced | 增强 DDoS | $3000/月 |

### GuardDuty

| 功能 | 描述 | 好处 |
|------|------|------|
| 威胁检测 | 持续监控 | 识别威胁 |
| 机器学习 | 异常检测 | 减少误报 |
| 集成 | CloudTrail, VPC | 全面 |

---

## 成本管理

管理和优化 AWS 成本。

### Cost Explorer

| 功能 | 描述 | 用途 |
|------|------|------|
| 成本分析 | 查看支出 | 预算追踪 |
| 预测 | 预测未来成本 | 预算规划 |
| 建议 | 节省建议 | 优化 |

### AWS Budgets

| 预算类型 | 描述 | 告警 |
|----------|------|------|
| 成本 | 支出限额 | Email, SNS |
| 使用量 | 服务使用 | Email, SNS |
| 预留 | RI 利用率 | Email, SNS |

### 成本优化策略

| 策略 | 描述 | 节省 |
|------|------|------|
| 右 sizing | 匹配实例到工作负载 | 30-50% |
| Reserved Instances | 长期承诺 | 30-75% |
| Spot Instances | 竞价 | 50-90% |
| Savings Plans | 灵活承诺 | 20-72% |

### 免费层

| 服务 | 免费限额 | 时长 |
|------|----------|------|
| EC2 | 750 小时 t2.micro | 12 个月 |
| S3 | 5GB 存储 | 12 个月 |
| RDS | 750 小时 t2.micro | 12 个月 |
| Lambda | 1M 请求/月 | 永久 |

### 成本分配标签

| 标签 | 用途 | 示例 |
|------|------|------|
| Environment | 追踪环境成本 | Production, Staging |
| Team | 团队计费 | Engineering, Marketing |
| Project | 项目成本 | ProjectA, ProjectB |
| Owner | 责任人 | john.doe |

---

## 总结

| 主题 | 核心要点 |
|------|----------|
| 账号 | 保护根账号，使用 IAM |
| 计算 | EC2 用于 VM，Lambda 用于无服务器 |
| 存储 | S3 用于对象，EBS 用于块 |
| 数据库 | RDS 用于关系型，DynamoDB 用于 NoSQL |
| 网络 | VPC 用于隔离，CloudFront 用于 CDN |
| 安全 | IAM、KMS、WAF 保护 |
| 成本 | 监控、优化、使用免费层 |


---
