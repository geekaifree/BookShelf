# 密码管理

> 本文档整合了以下源文件：password.md, vault.md, vault2.md

---

## 来源：password.md

## 简介

Bitwarden 是一个开源密码管理平台。它将凭证安全地存储在加密保险库中，跨设备同步，并提供生成和共享密码的工具。客户端仓库包括浏览器扩展、桌面应用、移动应用和 Web 保险库。本教程涵盖用法、设置和最佳实践。

## 为什么使用密码管理器

| 问题 | 解决方案 |
|------|----------|
| 重复使用密码 | 为每个网站生成唯一密码 |
| 弱密码 | 使用内置密码生成器 |
| 忘记凭证 | 集中化、可搜索的保险库 |
| 共享账户 | 通过组织安全共享 |
| 钓鱼 | 仅在匹配域名上自动填充 |

## 平台支持

| 平台 | 应用 | 状态 |
|------|------|------|
| Web | Web 保险库 | 生产环境 |
| Chrome | 浏览器扩展 | 生产环境 |
| Firefox | 浏览器扩展 | 生产环境 |
| Safari | 浏览器扩展 | 生产环境 |
| Edge | 浏览器扩展 | 生产环境 |
| Windows | 桌面应用 | 生产环境 |
| macOS | 桌面应用 | 生产环境 |
| Linux | 桌面应用 | 生产环境 |
| iOS | 移动应用 | 生产环境 |
| Android | 移动应用 | 生产环境 |

## 安装

### 自托管（Docker）

```yaml
version: "3"
services:
  bitwarden:
    image: vaultwarden/server:latest
    ports:
      - "80:80"
      - "3012:3012"
    volumes:
      - ./vw-data:/data
    environment:
      DOMAIN: "https://bitwarden.example.com"
      SIGNUPS_ALLOWED: "false"
      ADMIN_TOKEN: "your-admin-token"
    restart: unless-stopped
```

### 云托管

| 服务 | URL | 免费套餐 |
|------|-----|----------|
| Bitwarden Cloud | bitwarden.com | 是 |
| Vaultwarden 自托管 | 自定义域名 | 免费（开源） |

## 保险库项目

### 项目类型

| 类型 | 描述 | 字段 |
|------|------|------|
| Login | 网站凭证 | 用户名、密码、URL |
| Secure Note | 加密文本 | 自由格式内容 |
| Credit Card | 支付信息 | 卡号、有效期、CVV |
| Identity | 个人信息 | 姓名、地址、电话、邮箱 |

### 创建登录项目

| 字段 | 描述 | 示例 |
|------|------|------|
| Name | 显示名称 | "GitHub Account" |
| Username | 登录用户名 | "user@example.com" |
| Password | 登录密码 | "s3cur3P@ssw0rd!" |
| URL | 网站地址 | "https://github.com" |
| Notes | 附加信息 | "已启用 2FA，恢复码在安全笔记中" |
| Folder | 组织文件夹 | "Development" |

### 自定义字段

添加额外字段用于安全问题、API 密钥或其他数据。

| 字段类型 | 使用场景 |
|----------|----------|
| Text | 安全问题、API 密钥 |
| Hidden | PIN 码、二级密码 |
| Boolean | 账户偏好 |

## 密码生成器

### 生成器设置

| 设置 | 描述 | 推荐 |
|------|------|------|
| 类型 | 密码或密码短语 | Password |
| 长度 | 字符数 | 20+ 个字符 |
| 大写字母 | 包含 A-Z | 是 |
| 小写字母 | 包含 a-z | 是 |
| 数字 | 包含 0-9 | 是 |
| 特殊字符 | 包含符号 | 是 |
| 最少数字 | 最少数字数 | 2 |
| 最少特殊字符 | 最少符号数 | 2 |

### 密码短语生成

| 设置 | 描述 | 示例 |
|------|------|------|
| 单词分隔符 | 单词间的字符 | `-` 或 `.` |
| 单词数量 | 单词数 | 4-6 个单词 |
| 首字母大写 | 每个单词首字母大写 | 是 |

密码短语示例：`correct-horse-battery-staple`

## 自动填充

### 浏览器扩展

| 操作 | 方法 |
|------|------|
| 自动填充 | 点击扩展图标，选择项目 |
| 键盘快捷键 | `Ctrl+Shift+L`（默认） |
| 自动提交 | 在设置中启用填充后提交 |
| 上下文菜单 | 右键 > Bitwarden > Autofill |

### 自动填充设置

| 设置 | 描述 |
|------|------|
| 页面加载时自动填充 | 自动填充凭证 |
| 默认 URI 匹配检测 | URL 匹配方式 |
| 清除剪贴板 | 超时后清除复制的密码 |
| 禁用时关闭自动填充 | 遵循站点级设置 |

## 组织和文件夹

### 文件夹结构

```
Personal/
  Banking
  Email
  Social Media
  Shopping
Work/
  Development
  Infrastructure
  SaaS Services
Shared/
  Team Credentials
  Client Access
```

### 组织

组织允许安全共享保险库项目。

| 角色 | 权限 |
|------|------|
| Owner | 完全控制、账单、删除组织 |
| Admin | 管理用户、集合、项目 |
| User | 访问分配的集合 |
| Custom | 细粒度权限分配 |

### 集合

集合在组织内对项目进行分组。

| 集合 | 项目 | 访问权限 |
|------|------|----------|
| Engineering | 开发工具、API | 开发团队 |
| Marketing | 社交账户 | 市场团队 |
| Finance | 银行、支付 | 财务团队 |
| Shared | 通用密码 | 所有成员 |

## 双因素认证

### 支持的方式

| 方式 | 安全级别 | 设置 |
|------|----------|------|
| 认证器应用 | 高 | 使用任何认证器的 TOTP |
| 邮箱 | 中 | 通过邮箱发送验证码 |
| YubiKey | 非常高 | 硬件安全密钥 |
| Duo | 高 | Duo Security 集成 |
| FIDO2 WebAuthn | 非常高 | 生物识别或硬件密钥 |

### 启用 2FA

1. 前往 Settings > Security > Two-step login。
2. 选择你偏好的方式。
3. 按照设置向导操作。
4. 将恢复码保存在安全位置。

## 紧急访问

### 受信任联系人

| 功能 | 描述 |
|------|------|
| 指定联系人 | 添加受信任的人 |
| 等待期 | 授予访问权限前的天数 |
| 拒绝期 | 拒绝请求的时间 |
| 查看或接管 | 授予的访问级别 |

## 导入和导出

### 从其他管理器导入

| 来源 | 格式 |
|------|------|
| LastPass | CSV 导出 |
| 1Password | 1PUX 格式 |
| Chrome | CSV 导出 |
| Firefox | CSV 导出 |
| KeePass | XML 导出 |
| Dashlane | CSV 导出 |

### 导出

| 格式 | 安全性 |
|------|--------|
| JSON | 加密或未加密 |
| CSV | 未加密（明文） |

**警告**：导出文件包含所有可读格式的凭证。使用后请立即删除。

## 安全架构

### 加密

| 层级 | 算法 | 用途 |
|------|------|------|
| 主密码 | PBKDF2/Argon2 | 派生加密密钥 |
| 保险库数据 | AES-256-CBC | 加密存储的项目 |
| 传输 | TLS 1.2+ | 保护传输中的数据 |
| 密钥 | RSA-2048/OAEP | 组织密钥共享 |

### 零知识架构

| 原则 | 描述 |
|------|------|
| 客户端加密 | 数据在离开设备前加密 |
| 无明文存储 | 服务器永远看不到未加密数据 |
| 主密码哈希 | 仅发送哈希用于认证 |
| 密钥派生 | 主密钥在本地派生 |

## 共享

### 个人共享

与另一个 Bitwarden 用户共享单个项目。

1. 打开项目。
2. 点击"Share"。
3. 输入接收者的邮箱地址。
4. 设置权限（只读或读写）。

### 组织共享

通过组织集合共享项目。

1. 将项目添加到组织集合。
2. 将用户或组分配到集合。
3. 用户自动看到共享项目。

## 紧急程序

### 丢失主密码

| 步骤 | 操作 |
|------|------|
| 1 | 检查是否在任何设备上已登录 |
| 2 | 重置前导出保险库 |
| 3 | 重置主密码（会删除保险库） |
| 4 | 从备份重新导入 |

### 账户恢复

| 方法 | 描述 |
|------|------|
| 恢复码 | 在 2FA 设置时保存 |
| 紧急联系人 | 有访问权限的受信任人 |
| 管理员重置 | 组织管理员可以重置（仅限云端） |

## 命令行界面

```bash
# 安装 CLI
npm install -g @bitwarden/cli

# 登录
bw login user@example.com

# 解锁保险库
bw unlock

# 列出项目
bw list items

# 获取特定项目
bw get item "GitHub Account"

# 创建新项目
bw create item '{"type":1,"name":"New Login","login":{"username":"user","password":"pass"}}'
```

## 总结

Bitwarden 提供了完整的密码管理解决方案，支持跨平台、强加密和安全共享功能。使用它生成唯一密码、安全存储凭证，并通过组织与团队共享访问。使用 Vaultwarden 自托管以获得完全控制，或使用云服务以获得便利。


---

## 来源：vault.md

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


---

## 来源：vault2.md

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


---
