# Coolify：自托管 PaaS 平台

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
