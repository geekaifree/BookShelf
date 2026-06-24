# Cloudreve：构建自托管云存储平台

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
