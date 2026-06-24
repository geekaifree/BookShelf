# Vaultwarden：自托管密码保险库教程

## 简介

Vaultwarden 是一个非官方的、轻量级的 Bitwarden 兼容服务器，使用 Rust 编写。它提供了一个自托管的密码管理解决方案，完全兼容 Bitwarden 客户端。本教程涵盖安装、配置和安全运行。

## Vaultwarden 与 Bitwarden 官方版对比

| 功能 | Vaultwarden | Bitwarden 官方版 |
|------|------------|-----------------|
| 语言 | Rust | C#（.NET） |
| 资源占用 | 非常低 | 较高 |
| 数据库 | SQLite、MySQL、PostgreSQL | SQL Server、MySQL、PostgreSQL |
| 官方支持 | 社区 | Bitwarden 团队 |
| 高级功能 | 全部免费 | 需要订阅 |
| 邮件 | 需要 SMTP | 需要 SMTP |
| 设置 | 单一二进制文件 | 多个容器 |

## 系统要求

| 组件 | 最低要求 | 推荐配置 |
|------|---------|---------|
| CPU | 1 核 | 2 核 |
| 内存 | 64 MB | 256 MB |
| 磁盘 | 100 MB | 1 GB |
| 操作系统 | 任何支持 Docker 的系统 | Linux + Docker |
| 网络 | 生产环境需要 HTTPS | 带 SSL 的反向代理 |

## 安装

### Docker（推荐）

```bash
docker run -d \
  --name vaultwarden \
  --restart=unless-stopped \
  -v /vw-data/:/data/ \
  -p 80:80 \
  vaultwarden/server:latest
```

### Docker Compose

```yaml
version: '3'
services:
  vaultwarden:
    image: vaultwarden/server:latest
    container_name: vaultwarden
    restart: unless-stopped
    environment:
      - DOMAIN=https://vault.example.com
      - SIGNUPS_ALLOWED=false
      - ADMIN_TOKEN=your-secure-token
      - SMTP_HOST=smtp.example.com
      - SMTP_FROM=vault@example.com
      - SMTP_PORT=587
      - SMTP_SECURITY=starttls
      - SMTP_USERNAME=vault@example.com
      - SMTP_PASSWORD=your-smtp-password
    volumes:
      - ./vw-data:/data
    ports:
      - "8080:80"
```

## 配置

### 环境变量

| 变量 | 用途 | 默认值 |
|------|------|--------|
| DOMAIN | 服务器的基础 URL | 必填 |
| SIGNUPS_ALLOWED | 允许新注册 | true |
| INVITATIONS_ALLOWED | 允许管理员邀请 | true |
| ADMIN_TOKEN | 管理面板访问令牌 | 无 |
| DATABASE_URL | 数据库连接字符串 | SQLite（默认） |
| SMTP_HOST | 邮件服务器主机 | 无 |
| SMTP_PORT | 邮件服务器端口 | 587 |
| SMTP_FROM | 发件人邮箱地址 | 无 |
| SMTP_SECURITY | TLS 模式 | starttls |
| LOG_LEVEL | 日志详细程度 | warn |
| WEBSOCKET_ENABLED | 启用 WebSocket 通知 | false |
| DISABLE_ICON_DOWNLOAD | 禁用网站图标获取 | false |
| ICON_CACHE_TTL | 图标缓存时间（秒） | 2592000 |

### 数据库选项

| 数据库 | 连接字符串 |
|--------|-----------|
| SQLite | sqlite:///data/db.sqlite3（默认） |
| MySQL | mysql://user:pass@host/dbname |
| PostgreSQL | postgresql://user:pass@host/dbname |

## 反向代理设置

### Nginx

```nginx
server {
    listen 443 ssl;
    server_name vault.example.com;

    ssl_certificate /etc/ssl/certs/vault.pem;
    ssl_certificate_key /etc/ssl/private/vault.key;

    location / {
        proxy_pass http://localhost:8080;
        proxy_set_header Host $host;
        proxy_set_header X-Real-IP $remote_addr;
        proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
        proxy_set_header X-Forwarded-Proto $scheme;
    }

    location /notifications/hub {
        proxy_pass http://localhost:8080;
        proxy_http_version 1.1;
        proxy_set_header Upgrade $http_upgrade;
        proxy_set_header Connection "upgrade";
    }
}
```

### Caddy

```
vault.example.com {
    reverse_proxy localhost:8080
}
```

## 管理面板

访问管理面板：`https://vault.example.com/admin`。

### 管理功能

| 功能 | 用途 |
|------|------|
| 用户管理 | 查看、删除、禁用用户 |
| 组织管理 | 管理组织 |
| SMTP 设置 | 配置邮件发送 |
| 诊断 | 检查服务器健康状态 |
| 邀请用户 | 发送注册邀请 |
| 移除 2FA | 重置用户双因素认证 |

### 生成管理令牌

```bash
# 生成随机令牌
openssl rand -base64 48
```

## 客户端应用

| 平台 | 应用 | 下载 |
|------|------|------|
| Web | Web Vault | 通过浏览器访问你的域名 |
| 桌面 | Bitwarden Desktop | bitwarden.com/download |
| 移动 | Bitwarden Mobile | App Store / Play Store |
| 浏览器 | Bitwarden Extension | Chrome、Firefox、Safari、Edge |
| CLI | Bitwarden CLI | npm install -g @bitwarden/cli |

### 连接客户端

1. 安装 Bitwarden 客户端。
2. 登录前打开设置。
3. 将服务器 URL 设置为你的 Vaultwarden 域名。
4. 使用凭据登录。

## 安全加固

### 必要的安全步骤

| 步骤 | 操作 |
|------|------|
| 1 | 使用有效的 SSL 证书启用 HTTPS |
| 2 | 初始设置后禁用注册 |
| 3 | 设置强 ADMIN_TOKEN |
| 4 | 启用双因素认证 |
| 5 | 配置 SMTP 用于邮箱验证 |
| 6 | 设置自动备份 |
| 7 | 保持 Vaultwarden 更新 |
| 8 | 使用防火墙限制访问 |

### 双因素认证

| 方式 | 安全级别 |
|------|---------|
| TOTP（认证器应用） | 高 |
| 邮箱 | 中等 |
| FIDO2/WebAuthn | 非常高 |
| Duo Security | 高 |
| YubiKey | 非常高 |

## 备份与恢复

### 备份数据

```bash
# 备份数据库和附件
tar -czf vaultwarden-backup-$(date +%Y%m%d).tar.gz /vw-data/
```

### 自动备份脚本

```bash
#!/bin/bash
BACKUP_DIR="/backups/vaultwarden"
DATE=$(date +%Y%m%d_%H%M%S)
mkdir -p $BACKUP_DIR
docker exec vaultwarden sqlite3 /data/db.sqlite3 ".backup /data/backup.db"
docker cp vaultwarden:/data/backup.db $BACKUP_DIR/db_$DATE.db
tar -czf $BACKUP_DIR/attachments_$DATE.tar.gz /vw-data/attachments/
find $BACKUP_DIR -mtime +30 -delete
```

### 恢复

```bash
# 停止服务器
docker stop vaultwarden
# 恢复数据库
cp backup.db /vw-data/db.sqlite3
# 恢复附件
tar -xzf attachments_backup.tar.gz -C /vw-data/
# 启动服务器
docker start vaultwarden
```

## 性能调优

| 设置 | 影响 | 建议 |
|------|------|------|
| 数据库 | 查询速度 | 大规模部署使用 PostgreSQL |
| 缓存 | 响应时间 | 启用图标缓存 |
| Workers | 并发数 | 根据 CPU 核心数设置 |
| 日志 | 磁盘使用 | 生产环境使用 warn 级别 |
| WebSockets | 实时同步 | 多设备用户启用 |

## 故障排除

| 问题 | 原因 | 解决方案 |
|------|------|---------|
| 无法连接 | 服务器 URL 错误 | 验证 DOMAIN 与实际 URL 匹配 |
| 邮件未发送 | SMTP 配置错误 | 在管理面板测试 SMTP 设置 |
| 性能缓慢 | SQLite 负载过大 | 切换到 PostgreSQL |
| 2FA 不工作 | 时间同步问题 | 使用 NTP 同步服务器时钟 |
| 登录失败 | 数据库损坏 | 从备份恢复 |

## 总结

Vaultwarden 提供了一个轻量级的自托管密码管理解决方案，完全兼容 Bitwarden 客户端。其极低的资源需求、基于 Docker 的部署方式和全面的功能集，使其成为希望掌控密码数据的个人和团队的理想选择。
