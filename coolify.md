# Coolify：自托管 PaaS 指南

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
