# Alist：通用文件列表与分享

## 简介

Alist 是一个开源的文件列表和分享程序，支持多种存储提供商。它提供了一个统一的 Web 界面，可从单个仪表板访问存储在各种云服务、本地存储和网络驱动器上的文件。

Alist 通过一个一致的界面简化了跨不同存储平台的文件管理，可在任何 Web 浏览器中访问。

## 为什么使用 Alist？

| 特性 | Alist | 独立应用 |
|---------|-------|----------------|
| 统一界面 | 单一仪表板 | 多个应用 |
| 多提供商 | 30+ 种存储类型 | 每个服务一个 |
| 文件分享 | 直接链接 | 服务特定 |
| API 访问 | RESTful API | 各不相同 |
| 自托管 | 完全控制 | 取决于服务 |
| 费用 | 免费 | 各不相同 |

## 支持的存储提供商

| 提供商 | 类型 | 协议 | 功能 |
|----------|------|----------|----------|
| 本地磁盘 | 文件系统 | 直接 | 完全访问 |
| OneDrive | 云 | API | 读/写 |
| Google Drive | 云 | API | 读/写 |
| Dropbox | 云 | API | 读/写 |
| S3 | 对象存储 | API | 读/写 |
| WebDAV | 网络 | 协议 | 读/写 |
| FTP/SFTP | 网络 | 协议 | 读/写 |
| SMB | 网络 | 协议 | 读/写 |
| 阿里云盘 | 云 | API | 读/写 |
| Mega | 云 | API | 读/写 |
| 百度网盘 | 云 | API | 读/写 |
| 123盘 | 云 | API | 读/写 |
| GitHub | Git | API | 只读 |
| GitLab | Git | API | 只读 |

## 安装

### Docker 部署

```bash
# 创建数据目录
mkdir -p /opt/alist/data

# 运行 Alist
docker run -d \
  --name alist \
  --restart unless-stopped \
  -p 5244:5244 \
  -v /opt/alist/data:/opt/alist/data \
  xhofe/alist:latest
```

### Docker Compose

```yaml
version: '3'
services:
  alist:
    image: xhofe/alist:latest
    container_name: alist
    restart: unless-stopped
    ports:
      - "5244:5244"
    volumes:
      - ./data:/opt/alist/data
```

### 直接安装

```bash
# Linux
curl -fsSL "https://alist.nn.ci/install.sh" | bash

# 或从 GitHub releases 下载
# https://github.com/alist-org/alist/releases
```

### 系统要求

| 要求 | 最低配置 | 推荐配置 |
|------------|---------|-------------|
| 内存 | 64MB | 256MB |
| 存储 | 50MB | 500MB |
| CPU | 1 核 | 2 核 |
| 网络 | 端口 5244 | 带 SSL 的反向代理 |

## 初始设置

### 获取管理员密码

首次运行后，从日志中获取管理员密码：

```bash
# Docker 日志
docker logs alist

# 直接安装
cat /opt/alist/data/log/log.log | grep password
```

### Web 界面

访问 `http://your-server-ip:5244` 上的仪表板。

| 步骤 | 操作 |
|------|--------|
| 1 | 打开浏览器访问端口 5244 |
| 2 | 使用管理员凭据登录 |
| 3 | 添加存储提供商 |
| 4 | 配置设置 |
| 5 | 创建分享链接 |

## 添加存储提供商

### 本地存储

| 设置 | 值 | 描述 |
|---------|-------|-------------|
| 存储类型 | Local | 本地磁盘 |
| 根文件夹 | /path/to/files | 要服务的目录 |
| 只读 | false | 允许文件操作 |

### OneDrive 配置

| 设置 | 值 | 描述 |
|---------|-------|-------------|
| Client ID | Azure 应用 ID | 来自 Azure 门户 |
| Client Secret | Azure 应用密钥 | 来自 Azure 门户 |
| Refresh Token | OAuth 令牌 | 授权令牌 |
| 根文件夹 | / | OneDrive 根路径 |

### S3 兼容存储

| 设置 | 值 | 描述 |
|---------|-------|-------------|
| 桶名称 | my-bucket | S3 存储桶 |
| 区域 | us-east-1 | AWS 区域 |
| 端点 | s3.amazonaws.com | S3 端点 |
| Access Key | AKIA... | AWS 访问密钥 |
| Secret Key | ... | AWS 秘密密钥 |

### Google Drive

| 设置 | 值 | 描述 |
|---------|-------|-------------|
| Client ID | Google 应用 ID | 来自 Google Cloud |
| Client Secret | Google 应用密钥 | 来自 Google Cloud |
| Refresh Token | OAuth 令牌 | 授权令牌 |
| 根文件夹 | / | Drive 根路径 |

## 文件管理

### 上传文件

| 方法 | 描述 | 大小限制 |
|--------|-------------|-----------|
| Web 上传 | 浏览器上传 | 取决于提供商 |
| API 上传 | RESTful API | 提供商限制 |
| WebDAV | 挂载为驱动器 | 提供商限制 |
| Rclone | CLI 同步 | 无限制 |

### 下载文件

| 方法 | 描述 | 速度 |
|--------|-------------|-------|
| 直接下载 | 浏览器下载 | 良好 |
| 分享链接 | 公开 URL | 良好 |
| API 下载 | RESTful API | 良好 |
| WebDAV | 挂载为驱动器 | 良好 |

### 文件操作

| 操作 | 描述 | 支持 |
|-----------|-------------|---------|
| 创建文件夹 | 新目录 | 是 |
| 重命名 | 更改文件名 | 是 |
| 移动 | 重新定位文件 | 是 |
| 复制 | 复制文件 | 是 |
| 删除 | 移除文件 | 是 |
| 预览 | 查看文件内容 | 是（图片、视频、文本） |

## 分享功能

### 创建分享链接

| 链接类型 | 描述 | 过期时间 |
|-----------|-------------|-----------|
| 公开链接 | 任何有链接的人 | 永不过期 |
| 密码保护 | 需要密码 | 永不过期 |
| 临时链接 | 限时访问 | 自定义时长 |
| 目录链接 | 分享整个文件夹 | 永不过期 |

### 分享链接设置

| 设置 | 描述 | 选项 |
|---------|-------------|---------|
| 密码 | 访问密码 | 自定义字符串 |
| 过期时间 | 链接有效期 | 小时/天/永不过期 |
| 下载限制 | 最大下载次数 | 无限制或指定次数 |
| 永久 | 重启后保留 | 是/否 |

## API 访问

### RESTful API 端点

| 端点 | 方法 | 描述 |
|----------|--------|-------------|
| `/api/fs/list` | GET | 列出目录内容 |
| `/api/fs/get` | GET | 获取文件信息 |
| `/api/fs/dirs` | GET | 仅列出目录 |
| `/api/fs/search` | GET | 搜索文件 |
| `/api/fs/put` | PUT | 上传文件 |
| `/api/fs/remove` | POST | 删除文件 |
| `/api/fs/move` | POST | 移动文件 |
| `/api/fs/copy` | POST | 复制文件 |
| `/api/fs/mkdir` | POST | 创建目录 |
| `/api/fs/rename` | POST | 重命名文件 |

### API 认证

```bash
# 获取认证令牌
curl -X POST http://localhost:5244/api/auth/login \
  -H "Content-Type: application/json" \
  -d '{"username":"admin","password":"your_password"}'

# 在请求中使用令牌
curl -H "Authorization: your_token" \
  http://localhost:5244/api/fs/list?path=/
```

## WebDAV 访问

Alist 提供 WebDAV 接口用于挂载为网络驱动器。

| 设置 | 值 |
|---------|-------|
| URL | `http://your-server:5244/dav` |
| 用户名 | admin |
| 密码 | your_password |
| 协议 | WebDAV |

### 不同操作系统挂载方式

| 操作系统 | 方法 |
|----|--------|
| Windows | 映射网络驱动器 |
| macOS | Finder > 连接服务器 |
| Linux | `mount -t davfs` |

## Rclone 集成

Alist 可与 Rclone 配合使用，进行高级文件操作。

```bash
# 配置 Rclone 远程
rclone config create alist webdav url http://localhost:5244/dav user admin pass your_password

# 列出文件
rclone ls alist:/

# 复制文件
rclone copy /local/path alist:/remote/path

# 同步目录
rclone sync /local/path alist:/remote/path
```

## 高级功能

### 搜索

| 搜索类型 | 描述 | 性能 |
|-------------|-------------|-------------|
| 名称搜索 | 文件名匹配 | 快速 |
| 全文搜索 | 内容搜索 | 慢 |
| 正则表达式 | 模式匹配 | 中等 |

### 离线下载

| 方法 | 描述 | 支持 |
|--------|-------------|---------|
| URL 下载 | 从 URL 下载 | 是 |
| Torrent | 磁力链接 | 是 |
| Aria2 | 外部下载器 | 是 |

### 缩略图

| 功能 | 描述 | 配置 |
|---------|-------------|---------------|
| 图片缩略图 | 预览图片 | 在设置中启用 |
| 视频缩略图 | 视频预览帧 | 需要 ffmpeg |
| Office 预览 | 文档预览 | 需要 LibreOffice |

## 反向代理设置

### Nginx 配置

```nginx
server {
    listen 443 ssl;
    server_name files.yourdomain.com;

    ssl_certificate /etc/letsencrypt/live/files.yourdomain.com/fullchain.pem;
    ssl_certificate_key /etc/letsencrypt/live/files.yourdomain.com/privkey.pem;

    client_max_body_size 0;

    location / {
        proxy_pass http://localhost:5244;
        proxy_set_header Host $host;
        proxy_set_header X-Real-IP $remote_addr;
        proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
        proxy_set_header X-Forwarded-Proto $scheme;
    }
}
```

## 故障排除

| 问题 | 原因 | 解决方案 |
|-------|-------|----------|
| 无法登录 | 密码错误 | 检查日志获取初始密码 |
| 上传慢 | 提供商限速 | 检查提供商限制 |
| 文件不显示 | 缓存问题 | 清除浏览器缓存 |
| 分享链接失效 | 服务器重启 | 重新创建链接 |
| WebDAV 错误 | 认证问题 | 检查凭据 |

## 更多资源

| 资源 | URL |
|----------|-----|
| 官方网站 | alist.nn.ci |
| GitHub | github.com/alist-org/alist |
| 文档 | alist.nn.ci/guide |
| API 参考 | alist.nn.ci/guide/api |
