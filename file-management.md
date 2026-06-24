# 文件管理与存储

> 本文档整合了以下源文件：files.md, fileshare.md, alist.md, ftp.md, storage.md, scan.md

---

## 来源：files.md

## 简介

FileBrowser 在指定目录内提供基于 Web 的文件管理界面。它通过简洁的 Web 界面支持文件上传、下载、编辑和分享，并具有全面的用户管理功能。

## 系统要求

| 组件 | 最低配置 | 推荐配置 |
|------|---------|---------|
| CPU | 1 核 | 2 核 |
| 内存 | 128 MB | 512 MB |
| 磁盘 | 10 MB（二进制文件） | 取决于管理的文件 |
| 操作系统 | Linux, macOS, Windows | Linux |
| 网络 | HTTP | 通过反向代理使用 HTTPS |

## 安装

### 二进制安装

```bash
curl -fsSL https://raw.githubusercontent.com/filebrowser/get/master/get.sh | bash
filebrowser config init
filebrowser config set --address 0.0.0.0 --port 8080
filebrowser users add admin admin123 --perm.admin
filebrowser -r /path/to/files
```

### Docker 安装

```bash
docker run -d \
  --name filebrowser \
  -p 8080:80 \
  -v /path/to/srv:/srv \
  -v /path/to/database:/database \
  -v /path/to/config:/config \
  filebrowser/filebrowser:latest
```

### Docker Compose

```yaml
version: '3.8'
services:
  filebrowser:
    image: filebrowser/filebrowser:latest
    ports:
      - "8080:80"
    volumes:
      - ./srv:/srv
      - ./database:/database
      - ./filebrowser.json:/config/filebrowser.json
    restart: unless-stopped
```

## 配置

### filebrowser.json

```json
{
  "port": 8080,
  "baseURL": "",
  "address": "0.0.0.0",
  "log": "stdout",
  "database": "/database/filebrowser.db",
  "root": "/srv",
  "noauth": false,
  "username": "admin",
  "password": "admin123"
}
```

### 命令行配置

| 命令 | 用途 |
|------|------|
| `filebrowser config init` | 创建默认配置 |
| `filebrowser config set` | 修改配置设置 |
| `filebrowser config export` | 将配置导出为 JSON |
| `filebrowser users add` | 创建新用户 |
| `filebrowser users update` | 修改现有用户 |
| `filebrowser users ls` | 列出所有用户 |

## 用户管理

### 权限标志

| 权限 | 标志 | 说明 |
|------|------|------|
| 管理员 | `--perm.admin` | 完全系统访问 |
| 创建 | `--perm.create` | 上传和创建文件 |
| 删除 | `--perm.delete` | 删除文件和文件夹 |
| 修改 | `--perm.modify` | 编辑现有文件 |
| 分享 | `--perm.share` | 创建分享链接 |
| 执行 | `--perm.execute` | 对文件执行命令 |
| 下载 | `--perm.download` | 下载文件 |

### 用户角色

| 角色 | 典型权限 | 用途 |
|------|---------|------|
| 管理员 | 所有权限 | 系统管理 |
| 编辑者 | 创建、修改、删除 | 内容管理 |
| 查看者 | 仅下载 | 只读访问 |
| 上传者 | 仅创建 | 文件上传投放 |

### 创建用户

```bash
# 完全访问的管理员用户
filebrowser users add admin admin123 --perm.admin

# 拥有内容管理权限的编辑者
filebrowser users add editor edit123 --perm.create --perm.modify --perm.delete

# 仅有下载权限的查看者
filebrowser users add viewer view123 --perm.download

# 限定特定目录的用户
filebrowser users add user pass --scope /srv/user-files
```

## Web 界面功能

### 文件操作

| 操作 | 方法 | 快捷键 |
|------|------|--------|
| 上传 | 拖放或按钮 | - |
| 下载 | 点击文件名 | - |
| 删除 | 选择后删除 | Del 键 |
| 重命名 | 右键选择重命名 | F2 |
| 复制 | 右键选择复制 | Ctrl+C |
| 剪切 | 右键选择剪切 | Ctrl+X |
| 粘贴 | 右键选择粘贴 | Ctrl+V |
| 新建文件夹 | 工具栏按钮 | - |
| 新建文件 | 工具栏按钮 | - |

### 内置文件查看器和编辑器

| 功能 | 支持格式 |
|------|---------|
| 文本编辑器 | .txt, .md, .json, .xml, .csv |
| 代码编辑器 | .py, .js, .html, .css, .go, .rs |
| 图片查看器 | .jpg, .png, .gif, .svg, .webp |
| 视频播放器 | .mp4, .webm |
| 音频播放器 | .mp3, .wav, .ogg |
| PDF 查看器 | .pdf |
| Office 查看器 | .docx, .xlsx, .pptx |

### 媒体预览支持

| 类别 | 格式 | 功能 |
|------|------|------|
| 图片 | JPG, PNG, GIF, SVG, WebP | 缩放和幻灯片 |
| 视频 | MP4, WebM, OGG | 播放控制 |
| 音频 | MP3, WAV, OGG, FLAC | 播放控制 |
| 文本 | TXT, MD, JSON, XML, CSV | 语法高亮 |
| PDF | PDF | 页面导航 |
| 代码 | 大多数编程语言 | 语法高亮 |

## 文件分享

### 分享链接选项

| 选项 | 说明 | 默认值 |
|------|------|--------|
| 过期时间 | 超时后自动过期 | 永不 |
| 密码 | 密码保护链接 | 无 |
| 允许编辑 | 接收者可修改文件 | 否 |
| 最大下载次数 | 下载次数限制 | 无限 |

### 创建分享

1. 右键点击文件或文件夹
2. 从上下文菜单中选择 **Share**
3. 设置可选密码和过期日期
4. 复制生成的分享链接

### 分享 URL 格式

```
http://localhost:8080/share/SHARE_ID
```

## 访问规则

### 规则类型

| 规则类型 | 语法 | 示例 |
|---------|------|------|
| 允许 | `+` 前缀 | `+*.jpg` |
| 拒绝 | `-` 前缀 | `-*.exe` |
| 正则表达式 | 正则表达式 | `-\.(exe\|bat\|cmd)$` |

### 路径限定

将用户限定在特定目录：

```bash
filebrowser users add user pass --scope /srv/user-files
```

## 命令行界面

### 常用命令

| 命令 | 用途 |
|------|------|
| `filebrowser` | 启动服务器 |
| `filebrowser version` | 显示版本信息 |
| `filebrowser config init` | 初始化配置文件 |
| `filebrowser users ls` | 列出所有已配置用户 |
| `filebrowser users add` | 添加新用户账户 |
| `filebrowser users update` | 更新用户设置 |
| `filebrowser users rm` | 删除用户账户 |
| `filebrowser hash password` | 生成密码哈希 |

### 环境变量

| 变量 | 配置键 | 示例值 |
|------|--------|--------|
| `FB_ADDRESS` | address | `0.0.0.0` |
| `FB_PORT` | port | `8080` |
| `FB_DATABASE` | database | `/database.db` |
| `FB_ROOT` | root | `/srv` |
| `FB_LOG` | log | `stdout` |
| `FB_NOAUTH` | noauth | `false` |

## 品牌定制

### 自定义外观设置

| 设置 | 位置 | 说明 |
|------|------|------|
| 名称 | `branding.name` | 自定义站点标题 |
| 文件 | `branding.files` | 自定义 CSS 和 JS 目录 |
| 禁用外部 | `branding.disableExternal` | 隐藏外部链接 |
| 禁用使用率 | `branding.disableUsedPercentage` | 隐藏磁盘使用率条 |

### 自定义 CSS 示例

```css
/* custom.css */
#listing .item {
  font-size: 14px;
}
header {
  background: #2c3e50;
}
```

## 反向代理设置

### Nginx 配置

```nginx
server {
    listen 80;
    server_name files.example.com;

    client_max_body_size 100G;

    location / {
        proxy_pass http://localhost:8080;
        proxy_set_header Host $host;
        proxy_set_header X-Real-IP $remote_addr;
        proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
        proxy_set_header X-Forwarded-Proto $scheme;
    }
}
```

### Caddy 配置

```
files.example.com {
    reverse_proxy localhost:8080
}
```

## 数据库选项

| 类型 | 生产使用 | 备份方法 |
|------|---------|---------|
| SQLite（默认） | 小型部署 | 复制 .db 文件 |
| MySQL | 较大部署 | mysqldump |
| PostgreSQL | 企业级 | pg_dump |

## 安全

| 措施 | 实现方式 |
|------|---------|
| HTTPS | 使用 SSL 证书的反向代理 |
| 认证 | 要求强密码 |
| 速率限制 | Fail2ban 或基于代理的限制 |
| 文件规则 | 阻止危险文件类型 |
| 两步验证 | 设置中支持 TOTP |
| CORS | 限制允许的来源 |

## 性能

| 设置 | 影响 | 建议 |
|------|------|------|
| Recaptcha | 拖慢认证 | 内部使用时禁用 |
| 最大上传大小 | 内存使用 | 设置合理限制 |
| 缩略图 | 磁盘和 CPU 使用 | 图片密集目录启用 |

## 监控

```bash
# 检查服务器是否运行
curl http://localhost:8080/health

# 查看容器日志
docker logs filebrowser -f

# 检查数据库大小
ls -lh /database/filebrowser.db
```

## 故障排除

| 问题 | 原因 | 解决方案 |
|------|------|---------|
| 无法上传 | 权限被拒绝 | 检查用户创建权限 |
| 403 Forbidden | 路径范围问题 | 验证用户范围路径存在 |
| 加载缓慢 | 大目录列表 | 在设置中启用分页 |
| 无预览 | 不支持的格式 | 检查支持格式列表 |
| 上传大小限制 | 服务器配置 | 增加 `client_max_body_size` |

## 总结

FileBrowser 提供了一个轻量但功能丰富的基于 Web 的文件管理器。其用户管理、分享链接和内置编辑器使其适合个人使用、团队协作和文件服务器管理。


---

## 来源：fileshare.md

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


---

## 来源：alist.md

## 简介

Alist 是一款开源文件列表和分享程序，支持多种存储提供商。它提供统一的 Web 界面，从单一仪表板访问存储在各种云服务、本地存储和网络驱动器上的文件。

Alist 通过一个一致的界面简化了跨不同存储平台的文件管理，可通过任何 Web 浏览器访问。

## 为什么使用 Alist？

| 特性 | Alist | 独立应用 |
|------|------|---------|
| 统一界面 | 单一仪表板 | 多个应用 |
| 多提供商 | 30+ 存储类型 | 每服务一个 |
| 文件分享 | 直接链接 | 服务特定 |
| API 访问 | RESTful API | 各不相同 |
| 自托管 | 完全控制 | 取决于服务 |
| 费用 | 免费 | 各不相同 |

## 支持的存储提供商

| 提供商 | 类型 | 协议 | 功能 |
|-------|------|------|------|
| 本地磁盘 | 文件系统 | 直接 | 完全访问 |
| OneDrive | 云 | API | 读写 |
| Google Drive | 云 | API | 读写 |
| Dropbox | 云 | API | 读写 |
| S3 | 对象存储 | API | 读写 |
| WebDAV | 网络 | 协议 | 读写 |
| FTP/SFTP | 网络 | 协议 | 读写 |
| SMB | 网络 | 协议 | 读写 |
| 阿里云盘 | 云 | API | 读写 |
| Mega | 云 | API | 读写 |
| 百度网盘 | 云 | API | 读写 |
| 123 盘 | 云 | API | 读写 |
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

| 要求 | 最低 | 推荐 |
|------|------|------|
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

通过 `http://your-server-ip:5244` 访问仪表板。

| 步骤 | 操作 |
|------|------|
| 1 | 打开浏览器访问端口 5244 |
| 2 | 使用管理员凭据登录 |
| 3 | 添加存储提供商 |
| 4 | 配置设置 |
| 5 | 创建分享链接 |

## 添加存储提供商

### 本地存储

| 设置 | 值 | 描述 |
|------|---|------|
| 存储类型 | Local | 本地磁盘 |
| 根文件夹 | /path/to/files | 要服务的目录 |
| 只读 | false | 允许文件操作 |

### OneDrive 配置

| 设置 | 值 | 描述 |
|------|---|------|
| Client ID | Azure 应用 ID | 来自 Azure 门户 |
| Client Secret | Azure 应用密钥 | 来自 Azure 门户 |
| Refresh Token | OAuth 令牌 | 授权令牌 |
| 根文件夹 | / | OneDrive 根路径 |

### S3 兼容存储

| 设置 | 值 | 描述 |
|------|---|------|
| 存储桶名称 | my-bucket | S3 存储桶 |
| 区域 | us-east-1 | AWS 区域 |
| 端点 | s3.amazonaws.com | S3 端点 |
| Access Key | AKIA... | AWS 访问密钥 |
| Secret Key | ... | AWS 密钥 |

### Google Drive

| 设置 | 值 | 描述 |
|------|---|------|
| Client ID | Google 应用 ID | 来自 Google Cloud |
| Client Secret | Google 应用密钥 | 来自 Google Cloud |
| Refresh Token | OAuth 令牌 | 授权令牌 |
| 根文件夹 | / | Drive 根路径 |

## 文件管理

### 上传文件

| 方式 | 描述 | 大小限制 |
|------|------|---------|
| Web 上传 | 浏览器上传 | 取决于提供商 |
| API 上传 | RESTful API | 提供商限制 |
| WebDAV | 挂载为驱动器 | 提供商限制 |
| Rclone | CLI 同步 | 无限制 |

### 下载文件

| 方式 | 描述 | 速度 |
|------|------|------|
| 直接下载 | 浏览器下载 | 良好 |
| 分享链接 | 公开 URL | 良好 |
| API 下载 | RESTful API | 良好 |
| WebDAV | 挂载为驱动器 | 良好 |

### 文件操作

| 操作 | 描述 | 支持 |
|------|------|------|
| 创建文件夹 | 新目录 | 是 |
| 重命名 | 更改文件名 | 是 |
| 移动 | 重新定位文件 | 是 |
| 复制 | 复制文件 | 是 |
| 删除 | 移除文件 | 是 |
| 预览 | 查看文件内容 | 是（图像、视频、文本） |

## 分享功能

### 创建分享链接

| 链接类型 | 描述 | 过期 |
|---------|------|------|
| 公开链接 | 有链接即可访问 | 永不 |
| 密码保护 | 需要密码 | 永不 |
| 临时链接 | 限时访问 | 自定义时长 |
| 目录链接 | 分享整个文件夹 | 永不 |

### 分享链接设置

| 设置 | 描述 | 选项 |
|------|------|------|
| 密码 | 访问密码 | 自定义字符串 |
| 过期 | 链接有效期 | 小时/天/永不 |
| 下载限制 | 最大下载次数 | 无限或指定次数 |
| 永久 | 重启后保留 | 是/否 |

## API 访问

### RESTful API 端点

| 端点 | 方法 | 描述 |
|------|------|------|
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
|------|---|
| URL | `http://your-server:5244/dav` |
| 用户名 | admin |
| 密码 | your_password |
| 协议 | WebDAV |

### 不同操作系统挂载

| 操作系统 | 方式 |
|---------|------|
| Windows | 映射网络驱动器 |
| macOS | Finder > 连接服务器 |
| Linux | `mount -t davfs` |

## Rclone 集成

Alist 可与 Rclone 配合进行高级文件操作。

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
|---------|------|------|
| 名称搜索 | 文件名匹配 | 快 |
| 全文搜索 | 内容搜索 | 慢 |
| 正则表达式 | 模式匹配 | 中等 |

### 离线下载

| 方式 | 描述 | 支持 |
|------|------|------|
| URL 下载 | 从 URL 下载 | 是 |
| Torrent | 磁力链接 | 是 |
| Aria2 | 外部下载器 | 是 |

### 缩略图

| 功能 | 描述 | 配置 |
|------|------|------|
| 图像缩略图 | 预览图像 | 在设置中启用 |
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
|------|------|---------|
| 无法登录 | 密码错误 | 检查日志获取初始密码 |
| 上传缓慢 | 提供商限速 | 检查提供商限制 |
| 文件不显示 | 缓存问题 | 清除浏览器缓存 |
| 分享链接失效 | 服务器重启 | 重新创建链接 |
| WebDAV 错误 | 认证问题 | 检查凭据 |

## 更多资源

| 资源 | URL |
|------|-----|
| 官方网站 | alist.nn.ci |
| GitHub | github.com/alist-org/alist |
| 文档 | alist.nn.ci/guide |
| API 参考 | alist.nn.ci/guide/api |


---

## 来源：ftp.md

## 简介

SFTPGo 是一个用 Go 编写的全功能、高度可配置的 SFTP 服务器。它支持多种存储后端、认证方法，并提供基于 Web 的管理界面。

## 目录

1. [功能概览](#功能概览)
2. [安装](#安装)
3. [初始配置](#初始配置)
4. [用户管理](#用户管理)
5. [存储后端](#存储后端)
6. [协议支持](#协议支持)
7. [Web 管理界面](#web-管理界面)
8. [安全配置](#安全配置)

## 功能概览

| 功能 | 说明 |
|------|------|
| SFTP/SCP | 安全文件传输 |
| FTP/FTPS | 旧协议支持 |
| WebDAV | 基于 Web 的文件访问 |
| HTTP/REST | API 访问 |
| 多存储 | 本地、S3、Azure、GCS |
| 虚拟文件夹 | 挂载多个后端 |
| 带宽限制 | 每用户限速 |
| 事件钩子 | Webhook 和脚本 |

## 安装

### Docker Compose

```yaml
# docker-compose.yml
services:
  sftpgo:
    image: ghcr.io/drakkan/sftpgo:latest
    ports:
      - "8080:8080"
      - "2022:2022"
      - "2121:2121"
    volumes:
      - ./data:/srv/sftpgo
      - ./config:/var/lib/sftpgo
    environment:
      - SFTPGO_DEFAULT_ADMIN_USERNAME=admin
      - SFTPGO_DEFAULT_ADMIN_PASSWORD=admin
    restart: unless-stopped
```

### 二进制安装

| 平台 | 方式 |
|------|------|
| Linux | 从 GitHub releases 下载 |
| macOS | `brew install sftpgo` |
| Windows | 从 GitHub releases 下载 |
| Docker | `docker pull ghcr.io/drakkan/sftpgo` |

### 系统要求

| 组件 | 最低要求 | 推荐配置 |
|------|----------|----------|
| CPU | 1 核 | 2 核 |
| 内存 | 128 MB | 256 MB |
| 存储 | 100 MB | 1 GB+ |
| 操作系统 | Linux, macOS, Windows | Linux |

## 初始配置

### 配置文件

```json
{
  "sftpd": {
    "bindings": [
      {
        "port": 2022,
        "address": "0.0.0.0"
      }
    ]
  },
  "httpd": {
    "bindings": [
      {
        "port": 8080,
        "address": "0.0.0.0"
      }
    ]
  }
}
```

### 环境变量

| 变量 | 说明 | 默认值 |
|------|------|--------|
| `SFTPGO_CONFIG_DIR` | 配置目录 | . |
| `SFTPGO_DATA_PROVIDER__DRIVER` | 数据库驱动 | sqlite |
| `SFTPGO_DEFAULT_ADMIN_USERNAME` | 管理员用户名 | admin |
| `SFTPGO_DEFAULT_ADMIN_PASSWORD` | 管理员密码 | admin |

### 数据库选项

| 驱动 | 说明 | 使用场景 |
|------|------|----------|
| SQLite | 嵌入式数据库 | 单实例 |
| MySQL | MySQL/MariaDB | 多实例 |
| PostgreSQL | PostgreSQL | 多实例 |
| BoltDB | 嵌入式 KV | 简单设置 |
| CockroachDB | 分布式 SQL | 高可用 |

## 用户管理

### 用户属性

| 属性 | 说明 | 必需 |
|------|------|------|
| 用户名 | 登录名 | 是 |
| 密码 | 认证 | 是 |
| 主目录 | 起始路径 | 是 |
| 权限 | 文件操作 | 是 |
| 状态 | 活跃/停用 | 是 |
| 过期 | 账户过期 | 否 |

### 权限模型

| 权限 | 说明 | 默认 |
|------|------|------|
| `*` | 所有权限 | 否 |
| `list` | 列出目录 | 是 |
| `download` | 下载文件 | 是 |
| `upload` | 上传文件 | 是 |
| `delete` | 删除文件 | 是 |
| `rename` | 重命名文件 | 是 |
| `create_dirs` | 创建文件夹 | 是 |
| `overwrite` | 覆盖文件 | 是 |
| `rename_dirs` | 重命名文件夹 | 否 |
| `delete_dirs` | 删除文件夹 | 否 |

### 创建用户

```bash
# 通过 API
curl -X POST http://localhost:8080/api/v2/users \
  -H "Authorization: Basic $(echo -n admin:admin | base64)" \
  -H "Content-Type: application/json" \
  -d '{
    "username": "testuser",
    "password": "testpass",
    "home_dir": "/srv/sftpgo/testuser",
    "permissions": {
      "/": ["*"]
    }
  }'
```

### 虚拟文件夹

| 设置 | 说明 |
|------|------|
| 名称 | 虚拟路径名 |
| 映射路径 | 物理路径 |
| 文件系统 | 存储后端 |
| 配额 | 大小/文件限制 |

## 存储后端

### 支持的后端

| 后端 | 协议 | 使用场景 |
|------|------|----------|
| 本地文件系统 | 直接 | 单服务器 |
| AWS S3 | S3 API | 云存储 |
| Azure Blob | Azure API | Azure 用户 |
| Google Cloud Storage | GCS API | GCP 用户 |
| S3 兼容 | S3 API | MinIO 等 |
| Dropbox | Dropbox API | Dropbox 用户 |
| SFTP | SFTP 协议 | 远程服务器 |

### S3 配置

```json
{
  "filesystem": {
    "provider": 1,
    "s3config": {
      "bucket": "my-bucket",
      "region": "us-east-1",
      "access_key": "YOUR_ACCESS_KEY",
      "access_secret": "YOUR_SECRET_KEY",
      "endpoint": "https://s3.amazonaws.com"
    }
  }
}
```

### 存储对比

| 后端 | 性能 | 成本 | 可扩展性 |
|------|------|------|----------|
| 本地 | 最快 | 低 | 有限 |
| S3 | 良好 | 按使用付费 | 无限制 |
| Azure | 良好 | 按使用付费 | 无限制 |
| GCS | 良好 | 按使用付费 | 无限制 |

## 协议支持

### 支持的协议

| 协议 | 端口 | 加密 | 状态 |
|------|------|------|------|
| SFTP | 2022 | SSH | 活跃 |
| SCP | 2022 | SSH | 活跃 |
| FTP | 2121 | 无 | 可选 |
| FTPS | 2121 | TLS | 可选 |
| WebDAV | 10080 | HTTPS | 可选 |
| HTTP | 8080 | HTTPS | 可选 |

### 协议配置

```json
{
  "sftpd": {
    "bindings": [{"port": 2022}],
    "host_keys": ["/etc/ssh/ssh_host_rsa_key"]
  },
  "ftpd": {
    "bindings": [{"port": 2121}],
    "certificate_file": "/path/to/cert.pem",
    "certificate_key_file": "/path/to/key.pem"
  },
  "webdavd": {
    "bindings": [{"port": 10080}]
  }
}
```

### 客户端兼容性

| 客户端 | 协议 | 状态 |
|--------|------|------|
| FileZilla | SFTP, FTP | 完全支持 |
| WinSCP | SFTP, FTP | 完全支持 |
| Cyberduck | SFTP, WebDAV | 完全支持 |
| OpenSSH | SFTP, SCP | 完全支持 |
| rclone | SFTP | 完全支持 |

## Web 管理界面

### 管理功能

| 功能 | 说明 |
|------|------|
| 用户管理 | 创建、编辑、删除用户 |
| 文件夹管理 | 管理虚拟文件夹 |
| 连接监控 | 活跃连接 |
| 事件日志 | 活动历史 |
| 服务器状态 | 系统健康 |
| 配置 | 服务器设置 |

### 管理 URL

| URL | 用途 |
|-----|------|
| `/web/admin` | 管理仪表盘 |
| `/web/client` | 用户文件浏览器 |
| `/api/v2` | REST API |

### REST API 端点

| 端点 | 方法 | 用途 |
|------|------|------|
| `/api/v2/users` | GET | 列出用户 |
| `/api/v2/users` | POST | 创建用户 |
| `/api/v2/users/:id` | GET | 获取用户 |
| `/api/v2/users/:id` | PUT | 更新用户 |
| `/api/v2/users/:id` | DELETE | 删除用户 |
| `/api/v2/folders` | GET | 列出文件夹 |
| `/api/v2/folders` | POST | 创建文件夹 |
| `/api/v2/status` | GET | 服务器状态 |

### 连接监控

| 指标 | 说明 |
|------|------|
| 活跃连接 | 当前会话 |
| 连接历史 | 过去会话 |
| 传输统计 | 上传/下载字节数 |
| 客户端信息 | IP、协议、用户 |

## 安全配置

### 认证方式

| 方式 | 说明 | 安全级别 |
|------|------|----------|
| 密码 | 用户名/密码 | 基础 |
| 公钥 | SSH 密钥 | 高 |
| 键盘交互 | 质询-响应 | 中等 |
| 多因素 | 组合方式 | 最高 |

### TLS 配置

| 设置 | 说明 |
|------|------|
| 证书文件 | TLS 证书 |
| 密钥文件 | 私钥 |
| 最低 TLS 版本 | 最低 TLS 版本 |
| 密码套件 | 允许的密码 |

### 访问控制

| 控制 | 说明 |
|------|------|
| IP 白名单 | 允许的 IP 地址 |
| IP 黑名单 | 阻止的 IP 地址 |
| 速率限制 | 连接限速 |
| 最大连接数 | 每用户限制 |
| 空闲超时 | 会话超时 |

### 配额管理

| 设置 | 说明 |
|------|------|
| 上传带宽 | 最大上传速度 |
| 下载带宽 | 最大下载速度 |
| 文件大小限制 | 最大单文件大小 |
| 总配额 | 每用户最大存储 |
| 文件配额 | 最大文件数 |

### 事件钩子

| 事件 | 触发条件 |
|------|----------|
| `upload` | 文件已上传 |
| `download` | 文件已下载 |
| `delete` | 文件已删除 |
| `rename` | 文件已重命名 |
| `mkdir` | 目录已创建 |
| `rmdir` | 目录已删除 |

### Webhook 配置

```json
{
  "actions": {
    "execute_on": ["upload", "download"],
    "execute_command": "/path/to/script",
    "hook": "https://example.com/webhook"
  }
}
```

## 备份与恢复

| 组件 | 位置 | 方法 |
|------|------|------|
| 数据库 | SQLite 文件或 DB 服务器 | 转储/备份 |
| 用户文件 | 存储后端 | 文件同步 |
| 配置 | 配置文件 | 文件复制 |
| TLS 证书 | 证书文件 | 文件复制 |

## 总结

SFTPGo 提供了一个全面的文件传输解决方案，支持多种协议和存储后端。其基于 Web 的管理、灵活的用户管理和广泛的安全功能使其适合个人和企业文件传输需求。


---

## 来源：storage.md

## 简介

MinIO 是一款高性能、兼容 S3 的对象存储系统，专为大规模数据基础设施设计。它为云原生工作负载而构建，支持从单节点部署到多 PB 级分布式集群的多种部署方式。

| 特性 | 描述 |
|---------|-------------|
| S3 兼容性 | 完全兼容 Amazon S3 API |
| 性能 | 专为高吞吐量工作负载设计 |
| 可扩展性 | 支持分布式多节点集群 |
| 部署方式 | 可在裸机、虚拟机、Kubernetes 或容器上运行 |
| 许可证 | GNU AGPL v3 |

## 架构概述

MinIO 使用与传统文件系统和块存储不同的独特架构。

| 组件 | 角色 |
|-----------|------|
| MinIO Server | 处理读写操作的核心存储引擎 |
| MinIO Client (mc) | 管理对象和存储桶的命令行工具 |
| Console | 基于 Web 的管理界面 |
| Erasure Coding | 通过奇偶校验实现数据冗余保护 |
| Bitrot Protection | 自动检测和修复静默数据损坏 |

### 存储模型

MinIO 使用扁平命名空间模型组织数据：

| 层级 | 描述 |
|-------|-------------|
| Bucket | 对象的顶层容器，类似于文件夹 |
| Object | 带元数据存储的单个文件 |
| Prefix | 使用对象名称中的正斜杠实现虚拟层级结构 |
| Version | 可选的版本控制，用于跟踪对象随时间的变化 |

## 安装

### 独立部署

```bash
# 下载 MinIO 二进制文件
wget https://dl.min.io/server/minio/release/linux-amd64/minio
chmod +x minio

# 启动 MinIO 服务器
./minio server /data --console-address ":9001"
```

### Docker 部署

```bash
# 在容器中运行 MinIO
docker run -p 9000:9000 -p 9001:9001 \
  -e MINIO_ROOT_USER=admin \
  -e MINIO_ROOT_PASSWORD=strongpassword \
  minio/minio server /data --console-address ":9001"
```

### 分布式部署

```bash
# 启动 4 节点分布式集群
minio server http://node{1...4}/data{1...4}
```

| 部署模式 | 节点数 | 磁盘数 | 使用场景 |
|----------------|-------|--------|----------|
| 独立模式 | 1 | 1 | 开发和测试 |
| 单节点多磁盘 | 1 | 多个 | 小型生产工作负载 |
| 分布式多节点 | 4+ | 每节点多个 | 生产环境 |
| Kubernetes Operator | 可变 | 基于 PVC | 云原生部署 |

## MinIO Client (mc)

MinIO Client 提供了全面的命令行管理接口。

### 安装和配置

```bash
# 安装 mc
wget https://dl.min.io/client/mc/release/linux-amd64/mc
chmod +x mc

# 配置别名
mc alias set myminio http://localhost:9000 admin strongpassword
```

### 常用操作

| 操作 | 命令 | 描述 |
|-----------|---------|-------------|
| 创建存储桶 | `mc mb myminio/mybucket` | 创建新存储桶 |
| 列出存储桶 | `mc ls myminio` | 列出所有存储桶 |
| 上传文件 | `mc put file.txt myminio/mybucket` | 上传单个文件 |
| 下载文件 | `mc get myminio/mybucket/file.txt` | 下载文件 |
| 复制目录 | `mc cp --recursive ./dir myminio/mybucket/` | 上传目录内容 |
| 删除对象 | `mc rm myminio/mybucket/file.txt` | 删除对象 |
| 镜像存储桶 | `mc mirror ./local myminio/mybucket` | 将本地同步到存储桶 |
| 删除存储桶 | `mc rb myminio/mybucket` | 删除空存储桶 |

## 存储桶配置

### 版本控制

版本控制可在同一存储桶中保留对象的多个版本。

```bash
# 启用版本控制
mc version enable myminio/mybucket

# 检查版本控制状态
mc version info myminio/mybucket
```

### 生命周期策略

生命周期规则可自动执行对象的转换和过期操作。

| 策略类型 | 描述 | 示例用例 |
|-------------|-------------|------------------|
| 过期 | 在一段时间后删除对象 | 30 天后删除临时文件 |
| 转换 | 将对象移动到不同的存储层 | 90 天后归档日志 |
| 非当前版本过期 | 移除旧版本 | 仅保留最近 5 个版本 |
| 基于前缀 | 对特定前缀应用规则 | 不同文件夹使用不同规则 |

```bash
# 设置过期策略
cat > lifecycle.json <<EOF
{
  "Rules": [
    {
      "ID": "expire-temp",
      "Status": "Enabled",
      "Expiration": {
        "Days": 30
      },
      "Filter": {
        "Prefix": "temp/"
      }
    }
  ]
}
EOF

mc ilm import myminio/mybucket < lifecycle.json
```

### 存储桶通知

MinIO 支持对象操作的事件通知。

| 目标 | 协议 | 使用场景 |
|--------|----------|----------|
| AMQP | AMQP 0-9-1 | 消息队列集成 |
| NATS | NATS | 实时事件流 |
| Kafka | Kafka | 大规模事件处理 |
| Redis | Redis | 缓存失效和队列 |
| Webhook | HTTP POST | 自定义集成 |
| Elasticsearch | HTTP | 搜索索引 |

## 安全

### 身份和访问管理

| 概念 | 描述 |
|---------|-------------|
| Root 凭证 | 通过环境变量设置的初始管理员用户 |
| IAM 用户 | 具有特定访问密钥的独立用户 |
| 用户组 | 共享通用策略的用户集合 |
| 策略 | 定义允许/拒绝操作的 JSON 文档 |
| 服务账户 | 应用程序的限定范围凭证 |

### 策略示例

```json
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Effect": "Allow",
      "Action": [
        "s3:GetObject",
        "s3:PutObject"
      ],
      "Resource": "arn:aws:s3:::mybucket/*"
    },
    {
      "Effect": "Allow",
      "Action": [
        "s3:ListBucket"
      ],
      "Resource": "arn:aws:s3:::mybucket"
    }
  ]
}
```

### 加密

| 类型 | 描述 |
|------|-------------|
| 服务端加密 (SSE-S3) | MinIO 自动管理加密密钥 |
| SSE-KMS | 与外部密钥管理系统集成 |
| SSE-C | 客户端提供的加密密钥 |
| 客户端加密 | 上传前的应用层加密 |

## 性能调优

### 硬件建议

| 组件 | 建议 |
|-----------|----------------|
| CPU | 多核，生产环境至少 4 核 |
| 内存 | 生产工作负载至少 32 GB |
| 网络 | 分布式部署建议 10 GbE 或更高 |
| 存储 | 热数据使用 NVMe SSD，冷存储使用 HDD |
| 文件系统 | 推荐使用 XFS 格式化磁盘 |

### 磁盘配置

```bash
# 使用 XFS 格式化磁盘
mkfs.xfs /dev/sdb
mkfs.xfs /dev/sdc

# 使用适当的选项挂载
mount /dev/sdb /data/disk1
mount /dev/sdc /data/disk2
```

## 监控

### Prometheus 指标

MinIO 暴露与 Prometheus 兼容的指标。

```yaml
# prometheus.yml
scrape_configs:
  - job_name: 'minio'
    metrics_path: /minio/v2/metrics/cluster
    scheme: https
    static_configs:
      - targets: ['minio-server:9000']
```

| 指标类别 | 示例 |
|----------------|---------|
| 存储桶指标 | 对象数量、存储桶大小、请求速率 |
| 集群指标 | 节点健康状态、磁盘状态、网络吞吐量 |
| 系统指标 | CPU 使用率、内存、goroutines |
| API 指标 | 请求延迟、每个端点的错误率 |

## S3 API 兼容性

MinIO 可与任何兼容 S3 的 SDK 配合使用。

```python
from minio import Minio

client = Minio(
    "localhost:9000",
    access_key="admin",
    secret_key="strongpassword",
    secure=False
)

# 创建存储桶
if not client.bucket_exists("mybucket"):
    client.make_bucket("mybucket")

# 上传文件
client.fput_object("mybucket", "report.pdf", "./report.pdf")

# 列出对象
objects = client.list_objects("mybucket", prefix="reports/")
for obj in objects:
    print(obj.object_name, obj.size)
```

## 总结

| 主题 | 核心要点 |
|-------|-------------|
| 架构 | 扁平命名空间，使用纠删码保证持久性 |
| 部署 | 从单节点到分布式集群的灵活部署 |
| 管理 | mc CLI 和 Web 控制台进行管理 |
| 安全 | 细粒度 IAM 配合多种加密选项 |
| 兼容性 | 完全兼容 S3 API 和标准 SDK |
| 性能 | 针对高吞吐量、大规模工作负载优化 |


---

## 来源：scan.md

## 简介

Paperless-ngx 是一款开源文档管理系统，用于索引和归档纸质文档。它使用 OCR 技术使扫描文档可搜索，并通过标签、通信方和文档类型进行组织管理。

## 目录

1. [系统要求](#系统要求)
2. [安装方式](#安装方式)
3. [初始配置](#初始配置)
4. [文档导入](#文档导入)
5. [标签与组织](#标签与组织)
6. [搜索与检索](#搜索与检索)
7. [自动化规则](#自动化规则)
8. [用户管理](#用户管理)

## 系统要求

| 组件 | 最低要求 | 推荐配置 |
|------|----------|----------|
| CPU | 2 核 | 4 核 |
| 内存 | 2 GB | 4 GB |
| 存储 | 10 GB | 50 GB+ |
| 操作系统 | Linux, macOS, Windows | Ubuntu 22.04+ |
| Docker | 20.10+ | 最新稳定版 |
| Python | 3.9+ (裸机安装) | 3.11+ |

## 安装方式

### Docker Compose

推荐使用 Docker Compose，包含以下服务：

| 服务 | 用途 | 端口 |
|------|------|------|
| webserver | Paperless-ngx 应用 | 8000 |
| broker | Redis 任务队列 | 6379 |
| db | PostgreSQL 数据库 | 5432 |
| gotenberg | 文档转换 | 3000 |
| tika | 内容提取 | 9998 |

```yaml
# docker-compose.yml
services:
  broker:
    image: redis:7
    volumes:
      - redisdata:/data

  db:
    image: postgres:15
    volumes:
      - pgdata:/var/lib/postgresql/data
    environment:
      POSTGRES_DB: paperless
      POSTGRES_USER: paperless
      POSTGRES_PASSWORD: paperless

  webserver:
    image: ghcr.io/paperless-ngx/paperless-ngx:latest
    volumes:
      - data:/usr/src/paperless/data
      - media:/usr/src/paperless/media
      - ./export:/usr/src/paperless/export
      - ./consume:/usr/src/paperless/consume
    environment:
      PAPERLESS_REDIS: redis://broker:6379
      PAPERLESS_DBHOST: db
      PAPERLESS_TIME_ZONE: America/New_York
    ports:
      - "8000:8000"
    depends_on:
      - db
      - broker

volumes:
  data:
  media:
  pgdata:
  redisdata:
```

### 裸机安装

| 步骤 | 命令 | 用途 |
|------|------|------|
| 1 | `git clone https://github.com/paperless-ngx/paperless-ngx` | 获取源码 |
| 2 | `cd paperless-ngx && pip install -r requirements.txt` | 安装依赖 |
| 3 | `cp paperless.conf.example paperless.conf` | 配置模板 |
| 4 | `python manage.py migrate` | 数据库设置 |
| 5 | `python manage.py createsuperuser` | 创建管理员账户 |
| 6 | `python manage.py runserver` | 启动服务器 |

## 初始配置

### 环境变量

| 变量 | 说明 | 默认值 |
|------|------|--------|
| `PAPERLESS_TIME_ZONE` | 服务器时区 | UTC |
| `PAPERLESS_OCR_LANGUAGE` | OCR 语言 | eng |
| `PAPERLESS_CONSUMPTION_DIR` | 监视文件夹 | ../consume |
| `PAPERLESS_MEDIA_ROOT` | 存储位置 | ../media |
| `PAPERLESS_SECRET_KEY` | Django 密钥 | 自动生成 |
| `PAPERLESS_URL` | 公共 URL | http://localhost:8000 |

### OCR 配置

| 设置 | 说明 | 可选值 |
|------|------|--------|
| `PAPERLESS_OCR_MODE` | OCR 执行时机 | force, skip, redo |
| `PAPERLESS_OCR_LANGUAGE` | Tesseract 语言 | eng, deu, fra 等 |
| `PAPERLESS_OCR_DESKEW` | 纠正扫描倾斜 | true, false |
| `PAPERLESS_OCR_ROTATE_PAGES` | 自动旋转 | true, false |
| `PAPERLESS_OCR_CLEAN` | 清理图像 | true, false |

## 文档导入

### 支持的文件格式

| 格式 | 类型 | 说明 |
|------|------|------|
| PDF | 文档 | 主要格式，应用 OCR |
| JPEG | 图像 | 转换为 PDF |
| PNG | 图像 | 转换为 PDF |
| TIFF | 图像 | 支持多页 |
| Office | 文档 | 通过 Gotenberg/Tika |
| 纯文本 | 文本 | 直接索引 |
| HTML | 网页 | 通过 Tika 提取 |

### 导入方式

| 方式 | 说明 | 使用场景 |
|------|------|----------|
| Web UI | 通过浏览器上传 | 手动上传 |
| 监视文件夹 | 将文件放入 consume 目录 | 扫描仪集成 |
| 邮件 | IMAP 轮询 | 邮件附件 |
| API | REST 端点 | 自动化脚本 |
| 移动端 | 响应式 Web UI | 手机扫描 |

### 使用 API

```bash
# 上传文档
curl -X POST http://localhost:8000/api/documents/post_document/ \
  -H "Authorization: Token YOUR_API_TOKEN" \
  -F "document=@/path/to/invoice.pdf" \
  -F "title=Electric Bill June 2024"

# 列出文档
curl http://localhost:8000/api/documents/ \
  -H "Authorization: Token YOUR_API_TOKEN"
```

## 标签与组织

### 核心实体

| 实体 | 用途 | 示例 |
|------|------|------|
| 标签 | 灵活的标签 | 重要、税务、医疗 |
| 通信方 | 文档来源 | 电力公司、银行 |
| 文档类型 | 分类 | 发票、信函、收据 |
| 存储路径 | 文件位置 | Finance/, Medical/ |

### 自动分类

Paperless-ngx 从您的标签模式中学习：

| 设置 | 说明 |
|------|------|
| 匹配算法 | 机器学习分类器 |
| 训练数据 | 您手动标记的文档 |
| 最少样本 | 每个类别需要 1+ 个示例 |
| 自动应用 | 导入时自动分配标签 |

### 批量操作

| 操作 | 说明 | 步骤 |
|------|------|------|
| 批量编辑 | 更改标签/类型 | 选择文档，编辑 |
| 批量删除 | 删除文档 | 选择，删除 |
| 合并 | 合并 PDF | 选择，合并 |
| 批量下载 | 导出为 ZIP | 选择，下载 |

## 搜索与检索

### 搜索语法

| 操作符 | 示例 | 结果 |
|--------|------|------|
| 纯文本 | `invoice electric` | 全文搜索 |
| 精确短语 | `"annual report"` | 短语匹配 |
| 字段搜索 | `tag:important` | 按标签过滤 |
| 日期范围 | `created:[2024-01-01 TO 2024-06-30]` | 日期过滤 |
| 包含标签 | `has:tag` | 已标记文档 |
| 仅标题 | `title:contract` | 标题搜索 |

### 保存的视图

| 组件 | 说明 |
|------|------|
| 名称 | 描述性视图名称 |
| 过滤器 | 条件组合 |
| 排序方式 | 日期、标题、相关性 |
| 显示模式 | 列表、网格或卡片 |
| 共享 | 私有或与组共享 |

## 自动化规则

### 规则组件

| 组件 | 说明 | 示例 |
|------|------|------|
| 触发器 | 规则何时触发 | 文档上传时 |
| 条件 | 匹配条件 | 标题包含 "invoice" |
| 动作 | 执行操作 | 设置标签 "Finances" |

### 规则示例

| 规则名称 | 条件 | 动作 |
|----------|------|------|
| 自动标记发票 | 标题包含 "invoice" | 添加标签: Invoice |
| 银行对账单 | 发件人为 "Bank of America" | 设置类型: Statement |
| 归档旧文档 | 创建时间超过 365 天 | 添加标签: Archive |

## 用户管理

### 权限模型

| 级别 | 访问权限 | 说明 |
|------|----------|------|
| 管理员 | 完全访问 | 系统配置 |
| 用户 | 标准访问 | 查看和编辑自己的文档 |
| 组 | 共享访问 | 共享权限 |

### 组权限

| 权限 | 说明 |
|------|------|
| 查看文档 | 只读访问 |
| 编辑文档 | 修改元数据 |
| 创建文档 | 上传新文件 |
| 删除文档 | 删除文件 |
| 管理标签 | 创建/编辑标签 |
| 管理通信方 | 创建/编辑来源 |

## 备份与恢复

| 组件 | 位置 | 方法 |
|------|------|------|
| 数据库 | PostgreSQL 卷 | pg_dump |
| 媒体文件 | Media 卷 | 文件复制 |
| 配置 | 环境变量文件 | 文件复制 |
| 完整备份 | 所有卷 | Docker 卷导出 |

```bash
# 创建备份
docker compose exec webserver document_exporter ../export

# 从备份恢复
docker compose exec webserver document_importer ../export
```

## 总结

Paperless-ngx 将纸质文档管理转变为可搜索的数字档案。其 OCR 功能、自动分类和灵活的标签系统使其适用于个人和小型企业的文档工作流。


---
