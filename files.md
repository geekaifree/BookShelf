# FileBrowser 教程：基于 Web 的文件管理器

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
