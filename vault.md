# Vaultwarden：自托管密码保险库

## 简介

Vaultwarden（前身为 Bitwarden_RS）是 Bitwarden 服务器 API 的轻量级自托管实现。它与官方 Bitwarden 客户端完全兼容，同时更易于部署且更节省资源。本教程涵盖设置、配置和管理。

## 与官方 Bitwarden 的对比

| 功能 | Vaultwarden | 官方 Bitwarden |
|------|-------------|----------------|
| 语言 | Rust | C#/.NET |
| 数据库 | SQLite/MySQL/PostgreSQL | SQL Server/MSSQL |
| 内存使用 | 约 50 MB | 约 1+ GB |
| 设置复杂度 | 简单 Docker | 复杂多容器 |
| 客户端兼容性 | 完全 | 完全 |
| 许可证 | AGPL-3.0 | AGPL-3.0（服务器） |
| 免费功能 | 所有功能 | 部分需要付费 |

## 安装

### Docker Compose

```yaml
version: "3"
services:
  vaultwarden:
    image: vaultwarden/server:latest
    ports:
      - "80:80"
      - "3012:3012"
    volumes:
      - vw-data:/data
    environment:
      DOMAIN: "https://vault.example.com"
      SIGNUPS_ALLOWED: "false"
      INVITATIONS_ALLOWED: "true"
      ADMIN_TOKEN: "your-secure-admin-token"
      WEBSOCKET_ENABLED: "true"
      SMTP_HOST: "smtp.example.com"
      SMTP_FROM: "vault@example.com"
      SMTP_PORT: 587
      SMTP_SECURITY: "starttls"
      SMTP_USERNAME: "vault@example.com"
      SMTP_PASSWORD: "smtp-password"
    restart: unless-stopped
volumes:
  vw-data:
```

### Docker Run

```bash
docker run -d \
  --name vaultwarden \
  -v /vw-data/:/data/ \
  -p 80:80 \
  -e DOMAIN="https://vault.example.com" \
  -e SIGNUPS_ALLOWED="false" \
  -e ADMIN_TOKEN="your-secure-token" \
  vaultwarden/server:latest
```

## 配置

### 环境变量

| 变量 | 描述 | 默认值 |
|------|------|--------|
| `DOMAIN` | 服务器完整 URL | 必填 |
| `SIGNUPS_ALLOWED` | 允许新注册 | `true` |
| `INVITATIONS_ALLOWED` | 允许管理员邀请 | `true` |
| `ADMIN_TOKEN` | 管理面板访问令牌 | 无 |
| `WEBSOCKET_ENABLED` | 启用 WebSocket 通知 | `true` |
| `DISABLE_ADMIN_TOKEN` | 禁用管理员令牌要求 | `false` |
| `LOG_LEVEL` | 日志详细程度 | `info` |
| `EXTENDED_LOGGING` | 启用详细日志 | `false` |
| `ICON_SERVICE` | Favicon 服务 | `internal` |
| `ICON_BLACKLIST_NON_GLOBAL_IPS` | 阻止私有 IP 图标 | `true` |
| `ROCKET_PORT` | HTTP 端口 | `80` |
| `ROCKET_WORKERS` | Worker 数量 | `10` |

### 数据库配置

| 变量 | 描述 | 示例 |
|------|------|------|
| `DATABASE_URL` | 数据库连接字符串 | `sqlite:///data/db.sqlite3` |
| `DB_CONNECTION_TIMEOUT` | 连接超时（秒） | `10` |
| `DB_CONNECTION_RETRIES` | 最大重试次数 | `15` |

### SQLite（默认）

```env
DATABASE_URL=sqlite:///data/db.sqlite3
```

### MySQL

```env
DATABASE_URL=mysql://user:password@localhost:3306/vaultwarden
```

### PostgreSQL

```env
DATABASE_URL=postgresql://user:password@localhost:5432/vaultwarden
```

## SMTP 配置

邮箱是邀请、2FA 和密码重置所必需的。

| 变量 | 描述 | 示例 |
|------|------|------|
| `SMTP_HOST` | SMTP 服务器主机名 | `smtp.gmail.com` |
| `SMTP_FROM` | 发件人邮箱地址 | `vault@example.com` |
| `SMTP_PORT` | SMTP 端口 | `587` |
| `SMTP_SECURITY` | 加密方式 | `starttls` |
| `SMTP_USERNAME` | SMTP 用户名 | `vault@example.com` |
| `SMTP_PASSWORD` | SMTP 密码 | `password` |
| `SMTP_AUTH_MECHANISM` | 认证方式 | `Plain` |

### SMTP 提供商

| 提供商 | 主机 | 端口 | 安全 |
|--------|------|------|------|
| Gmail | smtp.gmail.com | 587 | starttls |
| Outlook | smtp.office365.com | 587 | starttls |
| SendGrid | smtp.sendgrid.net | 587 | starttls |
| Mailgun | smtp.mailgun.org | 587 | starttls |
| Amazon SES | email-smtp.region.amazonaws.com | 587 | starttls |

## 管理面板

### 访问管理面板

1. 导航到 `https://vault.example.com/admin`。
2. 输入管理员令牌。
3. 访问管理功能。

### 管理功能

| 部分 | 描述 |
|------|------|
| Dashboard | 服务器统计和健康状况 |
| Users | 管理用户账户 |
| Organizations | 管理组织 |
| Settings | 服务器配置 |
| Diagnostics | 系统健康检查 |

### 用户管理

| 操作 | 描述 |
|------|------|
| 查看用户 | 列出所有注册用户 |
| 编辑用户 | 更改用户设置 |
| 删除用户 | 删除用户和数据 |
| 禁用用户 | 暂时停用 |
| 邀请用户 | 发送邮箱邀请 |
| 确认用户 | 手动确认邮箱 |

### 邀请

```bash
# 通过管理面板发送邀请
# 或配置自动邀请：
INVITATIONS_ALLOWED=true
```

## 客户端设置

### 支持的客户端

| 客户端 | 设置 |
|--------|------|
| Web 保险库 | 导航到你的域名 |
| 浏览器扩展 | Settings > Self-hosted > Server URL |
| 桌面应用 | Settings > Self-hosted > Server URL |
| 移动应用 | Settings > Self-hosted > Server URL |
| CLI | `bw config server https://vault.example.com` |

### 浏览器扩展配置

1. 安装 Bitwarden 浏览器扩展。
2. 点击扩展图标。
3. 点击齿轮图标（设置）。
4. 选择"Self-hosted"。
5. 输入服务器 URL：`https://vault.example.com`
6. 保存并登录。

### 移动应用配置

1. 打开 Bitwarden 移动应用。
2. 点击设置图标。
3. 点击"Self-hosted"。
4. 输入服务器 URL：`https://vault.example.com`
5. 保存并登录。

## 组织

### 组织类型

| 类型 | 描述 | 用户数 |
|------|------|--------|
| Free | 基本共享 | 最多 2 用户 |
| Families | 家庭共享 | 最多 6 用户 |
| Teams | 团队协作 | 无限 |
| Enterprise | 高级管理 | 无限 |

### 创建组织

1. 登录 Web 保险库。
2. 点击"New Organization"。
3. 输入组织名称和账单邮箱。
4. 配置设置。
5. 邀请成员。

### 集合

集合在组织内组织共享项目。

| 集合 | 项目 | 访问权限 |
|------|------|----------|
| Engineering | 开发凭证 | 开发团队 |
| Marketing | 社交账户 | 市场团队 |
| Finance | 支付信息 | 财务团队 |
| Shared | 通用密码 | 所有成员 |

## 安全

### 双因素认证

| 方式 | 安全性 | 设置 |
|------|--------|------|
| TOTP 应用 | 高 | 用认证器扫描二维码 |
| 邮箱 | 中 | 通过邮箱发送验证码 |
| YubiKey | 非常高 | 注册硬件密钥 |
| Duo | 高 | Duo 集成 |
| FIDO2 | 非常高 | WebAuthn 生物识别/密钥 |

### 安全头

```nginx
# Nginx 安全头
add_header X-Frame-Options "SAMEORIGIN" always;
add_header X-Content-Type-Options "nosniff" always;
add_header X-XSS-Protection "1; mode=block" always;
add_header Referrer-Policy "no-referrer" always;
add_header Content-Security-Policy "default-src 'self'; script-src 'self'; style-src 'self' 'unsafe-inline'; img-src 'self' data: https:; font-src 'self';" always;
```

## 反向代理

### Nginx 配置

```nginx
server {
    listen 443 ssl http2;
    server_name vault.example.com;

    ssl_certificate /etc/letsencrypt/live/vault.example.com/fullchain.pem;
    ssl_certificate_key /etc/letsencrypt/live/vault.example.com/privkey.pem;

    # 允许大附件
    client_max_body_size 100M;

    location / {
        proxy_pass http://localhost:80;
        proxy_set_header Host $host;
        proxy_set_header X-Real-IP $remote_addr;
        proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
        proxy_set_header X-Forwarded-Proto $scheme;
    }

    # WebSocket 支持通知
    location /notifications/hub {
        proxy_pass http://localhost:3012;
        proxy_set_header Upgrade $http_upgrade;
        proxy_set_header Connection "upgrade";
    }
}
```

## 备份

### 备份组件

| 组件 | 位置 | 方法 |
|------|------|------|
| 数据库 | `/data/db.sqlite3` | 文件复制 |
| 附件 | `/data/attachments/` | 文件复制 |
| 配置 | `/data/config.json` | 文件复制 |
| Sends | `/data/sends/` | 文件复制 |

### 备份脚本

```bash
#!/bin/bash
BACKUP_DIR="/backups/vaultwarden/$(date +%Y%m%d)"
mkdir -p "$BACKUP_DIR"

# 停止容器以获得一致备份
docker stop vaultwarden

# 复制数据
docker cp vaultwarden:/data/ "$BACKUP_DIR/"

# 重启容器
docker start vaultwarden

# 清理旧备份（保留 30 天）
find /backups/vaultwarden -maxdepth 1 -mtime +30 -exec rm -rf {} \;
```

### 备份到 S3

```bash
#!/bin/bash
# 本地备份后，同步到 S3
aws s3 sync /backups/vaultwarden/ s3://my-backups/vaultwarden/ \
  --storage-class STANDARD_IA
```

## 迁移

### 从官方 Bitwarden 迁移

```bash
# 从官方 Bitwarden 导出
# （Settings > Export > CSV）

# 导入到 Vaultwarden
# （Settings > Import Data > Bitwarden CSV）
```

### Vaultwarden 实例间迁移

```bash
# 从旧实例导出（Web 保险库 > Settings > Export）
# 导入到新实例（Web 保险库 > Settings > Import）
```

## 性能调优

| 设置 | 描述 | 建议 |
|------|------|------|
| `ROCKET_WORKERS` | HTTP worker 数量 | 匹配 CPU 核数 |
| 数据库 | SQLite vs MySQL/PostgreSQL | 超过 50 用户用 PostgreSQL |
| `ICON_SERVICE` | Favicon 提供商 | `internal` 保护隐私 |
| 缓存 | 启用 gzip | 是 |

## 故障排除

| 问题 | 解决方案 |
|------|----------|
| 无法连接 | 检查 DOMAIN 设置和 DNS |
| 邮件不发送 | 验证 SMTP 配置 |
| 性能缓慢 | 检查数据库，增加 worker |
| 2FA 不工作 | 同步设备时间（NTP） |
| WebSocket 错误 | 确保端口 3012 被代理 |
| 管理面板被阻止 | 检查 ADMIN_TOKEN 设置 |

## 更新

```bash
# 拉取最新镜像
docker pull vaultwarden/server:latest

# 重建容器
docker-compose down
docker-compose up -d
```

## 总结

Vaultwarden 提供了与所有官方 Bitwarden 客户端兼容的轻量级自托管密码管理服务器。它使用的资源远少于官方服务器，同时支持所有核心功能，包括组织、2FA 和邮箱通知。使用 Docker 部署，配置 SMTP 和反向代理，将任何 Bitwarden 客户端连接到你的自托管保险库。
