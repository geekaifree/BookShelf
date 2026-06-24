# 使用 SFTPGo 搭建 SFTP 服务器

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
