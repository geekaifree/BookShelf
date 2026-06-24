# 自托管

> 本文档整合了以下源文件：selfHost.md, selfhost.md, selfhosted.md, hosting.md

---

## 来源：selfHost.md

## 简介

自托管是在您自己控制的硬件上运行服务的实践。本指南涵盖了设置和维护自托管应用的基础知识。

### 什么是自托管？

自托管意味着在自己的服务器上运行应用，而不是使用第三方云服务。

| 方面 | 云 | 自托管 |
|------|------|--------|
| 控制 | 有限 | 完全 |
| 隐私 | 第三方 | 您的数据 |
| 费用 | 持续 | 前期 |
| 维护 | 提供商 | 您自己 |
| 定制 | 有限 | 无限 |

### 自托管的好处

| 好处 | 描述 |
|------|------|
| 隐私 | 控制您的数据 |
| 独立 | 无供应商锁定 |
| 学习 | 技术技能 |
| 定制 | 根据需求定制 |
| 费用 | 长期节省 |

## 硬件要求

### 服务器选项

| 选项 | 费用 | 功率 | 噪音 |
|------|------|------|------|
| Raspberry Pi | 低 | 低 | 无声 |
| Mini PC | 中 | 中 | 安静 |
| 旧电脑 | 免费 | 不定 | 不定 |
| 专用服务器 | 高 | 高 | 响 |
| VPS | 月付 | 不定 | 无声 |

### 最低规格

| 服务类型 | CPU | 内存 | 存储 |
|----------|-----|------|------|
| 基本 Web | 1 核 | 1 GB | 20 GB |
| 媒体服务器 | 2 核 | 4 GB | 1 TB |
| 数据库 | 2 核 | 4 GB | 100 GB |
| 全能 | 4 核 | 8 GB | 2 TB |

### 推荐硬件

| 组件 | 推荐 |
|------|------|
| CPU | Intel i5 或 AMD Ryzen 5 |
| 内存 | 16-32 GB |
| 存储 | SSD 用于系统，HDD 用于数据 |
| 网络 | 千兆以太网 |
| UPS | 电池备份 |

## 操作系统

### Linux 发行版

| 发行版 | 最佳用途 | 支持 |
|--------|----------|------|
| Ubuntu Server | 初学者 | 5 年 |
| Debian | 稳定性 | 3 年 |
| CentOS Stream | 企业 | 5 年 |
| Arch Linux | 高级用户 | 滚动更新 |
| Proxmox VE | 虚拟化 | 3 年 |

### 安装步骤

```bash
# 下载 ISO
# 创建可启动 USB
# 安装操作系统
# 配置网络
# 更新系统
sudo apt update && sudo apt upgrade -y
```

## Docker

### 为什么选择 Docker？

| 好处 | 描述 |
|------|------|
| 隔离 | 独立环境 |
| 可移植 | 任何地方运行 |
| 可重现 | 一致的设置 |
| 效率 | 共享资源 |
| 版本控制 | 轻松更新 |

### Docker 安装

```bash
# 安装 Docker
curl -fsSL https://get.docker.com -o get-docker.sh
sudo sh get-docker.sh

# 将用户添加到 docker 组
sudo usermod -aG docker $USER

# 安装 Docker Compose
sudo apt install docker-compose
```

### Docker Compose 示例

```yaml
version: '3'
services:
  web:
    image: nginx:alpine
    ports:
      - "80:80"
    volumes:
      - ./html:/usr/share/nginx/html

  database:
    image: postgres:13
    environment:
      - POSTGRES_PASSWORD=secret
    volumes:
      - postgres_data:/var/lib/postgresql/data

volumes:
  postgres_data:
```

## 网络

### 域名配置

| 步骤 | 描述 |
|------|------|
| 1. 注册域名 | 选择注册商 |
| 2. DNS 设置 | 指向服务器 |
| 3. SSL 证书 | 启用 HTTPS |
| 4. 反向代理 | 路由流量 |

### DNS 记录

| 类型 | 用途 | 示例 |
|------|------|------|
| A | IPv4 地址 | server.example.com → 1.2.3.4 |
| AAAA | IPv6 地址 | server.example.com → ::1 |
| CNAME | 别名 | www → server.example.com |
| MX | 邮件 | mail.example.com |

### 反向代理

#### Nginx 配置

```nginx
server {
    listen 80;
    server_name app.example.com;
    return 301 https://$server_name$request_uri;
}

server {
    listen 443 ssl;
    server_name app.example.com;

    ssl_certificate /etc/letsencrypt/live/app.example.com/fullchain.pem;
    ssl_certificate_key /etc/letsencrypt/live/app.example.com/privkey.pem;

    location / {
        proxy_pass http://localhost:8080;
        proxy_set_header Host $host;
        proxy_set_header X-Real-IP $remote_addr;
    }
}
```

### 使用 Let's Encrypt 配置 SSL

```bash
# 安装 Certbot
sudo apt install certbot python3-certbot-nginx

# 获取证书
sudo certbot --nginx -d app.example.com

# 自动续期
sudo certbot renew --dry-run
```

## 必备服务

### Web 服务器

| 服务器 | 用例 |
|--------|------|
| Nginx | 反向代理、静态文件 |
| Apache | 传统 Web 服务器 |
| Caddy | 自动 HTTPS |

### 数据库

| 数据库 | 类型 | 用例 |
|--------|------|------|
| PostgreSQL | 关系型 | 通用 |
| MySQL | 关系型 | Web 应用 |
| MongoDB | 文档型 | 灵活 Schema |
| Redis | 键值型 | 缓存 |

### 监控

| 工具 | 用途 |
|------|------|
| Uptime Kuma | 服务监控 |
| Grafana | 指标可视化 |
| Prometheus | 指标收集 |
| Netdata | 实时监控 |

## 常见自托管应用

### 媒体和娱乐

| 应用 | 用途 |
|------|------|
| Jellyfin | 媒体服务器 |
| Navidrome | 音乐服务器 |
| Immich | 照片管理 |
| Calibre-web | 电子书管理 |

### 生产力

| 应用 | 用途 |
|------|------|
| Nextcloud | 文件同步、日历 |
| Bitwarden | 密码管理器 |
| Joplin | 笔记 |
| Vikunja | 任务管理 |

### 通讯

| 应用 | 用途 |
|------|------|
| Matrix/Element | 聊天 |
| Mattermost | 团队消息 |
| Mailcow | 邮件服务器 |
| Discourse | 论坛 |

### 开发

| 应用 | 用途 |
|------|------|
| Gitea | Git 托管 |
| Drone CI | 持续集成 |
| Harbor | 容器镜像仓库 |
| Portainer | Docker 管理 |

### 家庭自动化

| 应用 | 用途 |
|------|------|
| Home Assistant | 智能家居 |
| Node-RED | 自动化 |
| ESPHome | IoT 设备 |
| Zigbee2MQTT | Zigbee 网关 |

## 安全

### 安全清单

| 实践 | 描述 |
|------|------|
| 强密码 | 使用密码管理器 |
| 2FA | 启用双因素认证 |
| 防火墙 | 配置 UFW/iptables |
| 更新 | 定期系统更新 |
| 备份 | 定期备份 |

### 防火墙配置

```bash
# 启用防火墙
sudo ufw enable

# 允许 SSH
sudo ufw allow 22/tcp

# 允许 HTTP/HTTPS
sudo ufw allow 80/tcp
sudo ufw allow 443/tcp

# 检查状态
sudo ufw status
```

### SSH 安全

```bash
# 禁用 root 登录
sudo sed -i 's/PermitRootLogin yes/PermitRootLogin no/' /etc/ssh/sshd_config

# 禁用密码认证
sudo sed -i 's/PasswordAuthentication yes/PasswordAuthentication no/' /etc/ssh/sshd_config

# 重启 SSH
sudo systemctl restart sshd
```

## 备份策略

### 备份方式

| 方式 | 描述 |
|------|------|
| rsync | 文件同步 |
| Borgbackup | 去重备份 |
| Restic | 加密备份 |
| Duplicati | 云备份 |

### 3-2-1 备份规则

| 规则 | 描述 |
|------|------|
| 3 份 | 备份总数 |
| 2 种介质 | 不同存储类型 |
| 1 份异地 | 远程备份位置 |

### 备份脚本

```bash
#!/bin/bash
# 数据库备份
pg_dump -U postgres dbname > /backup/db_$(date +%Y%m%d).sql

# 文件备份
rsync -av --delete /data/ /backup/data/

# 清理旧备份
find /backup -mtime +30 -delete
```

## 性能优化

### 系统调优

| 设置 | 描述 |
|------|------|
| Swap | 配置交换空间 |
| Limits | 设置文件描述符限制 |
| Kernel | 调优内核参数 |
| Scheduler | 优化 I/O 调度器 |

### Docker 优化

| 技巧 | 描述 |
|------|------|
| 资源限制 | 设置 CPU/内存限制 |
| 健康检查 | 监控容器健康 |
| 重启策略 | 失败时自动重启 |
| 日志轮转 | 限制日志大小 |

## 监控和维护

### 监控栈

| 组件 | 用途 |
|------|------|
| Prometheus | 指标收集 |
| Grafana | 可视化 |
| Alertmanager | 告警 |
| Node Exporter | 系统指标 |

### 定期维护

| 任务 | 频率 |
|------|------|
| 系统更新 | 每周 |
| 安全补丁 | 可用时 |
| 备份验证 | 每月 |
| 日志审查 | 每周 |
| 性能审查 | 每月 |

## 故障排除

### 常见问题

| 问题 | 可能原因 | 解决方案 |
|------|----------|----------|
| 服务无法启动 | 配置错误 | 检查日志 |
| CPU 使用率高 | 进程循环 | 识别进程 |
| 磁盘满 | 日志文件 | 清理日志 |
| 网络问题 | DNS/防火墙 | 检查配置 |

### 日志位置

| 服务 | 日志位置 |
|------|----------|
| 系统 | /var/log/syslog |
| Nginx | /var/log/nginx/ |
| Docker | docker logs container |
| 应用 | 应用特定 |

## 费用估算

### 每月费用

| 项目 | 费用范围 |
|------|----------|
| 电费 | $5-20 |
| 网络 | $50-100 |
| 域名 | $1-2 |
| VPS（可选） | $5-50 |
| **合计** | **$60-170** |

### 一次性费用

| 项目 | 费用范围 |
|------|----------|
| 服务器硬件 | $100-500 |
| UPS | $50-150 |
| 网络设备 | $50-200 |
| **合计** | **$200-850** |

## 入门指南

### 分步指南

| 步骤 | 操作 |
|------|------|
| 1 | 选择硬件 |
| 2 | 安装操作系统 |
| 3 | 配置网络 |
| 4 | 安装 Docker |
| 5 | 部署服务 |
| 6 | 设置备份 |
| 7 | 配置监控 |

### 首先部署的服务

| 优先级 | 服务 | 原因 |
|--------|------|------|
| 1 | 反向代理 | 所有服务都需要 |
| 2 | 监控 | 了解何时出问题 |
| 3 | 备份 | 保护数据 |
| 4 | 密码管理器 | 安全 |
| 5 | 文件同步 | 生产力 |

## 总结

| 组件 | 用途 |
|------|------|
| 硬件 | 物理服务器 |
| 操作系统 | 运行系统 |
| Docker | 容器运行时 |
| 网络 | 域名、SSL、代理 |
| 服务 | 应用 |
| 安全 | 保护 |
| 备份 | 数据安全 |
| 监控 | 可见性 |


---

## 来源：selfhost.md

## 简介

自托管是在您自己控制的硬件上运行服务的实践。本指南涵盖了设置和维护自托管应用的基础知识。

### 什么是自托管？

自托管意味着在自己的服务器上运行应用，而不是使用第三方云服务。

| 方面 | 云 | 自托管 |
|------|------|--------|
| 控制 | 有限 | 完全 |
| 隐私 | 第三方 | 您的数据 |
| 费用 | 持续 | 前期 |
| 维护 | 提供商 | 您自己 |
| 定制 | 有限 | 无限 |

### 自托管的好处

| 好处 | 描述 |
|------|------|
| 隐私 | 控制您的数据 |
| 独立 | 无供应商锁定 |
| 学习 | 技术技能 |
| 定制 | 根据需求定制 |
| 费用 | 长期节省 |

## 硬件要求

### 服务器选项

| 选项 | 费用 | 功率 | 噪音 |
|------|------|------|------|
| Raspberry Pi | 低 | 低 | 无声 |
| Mini PC | 中 | 中 | 安静 |
| 旧电脑 | 免费 | 不定 | 不定 |
| 专用服务器 | 高 | 高 | 响 |
| VPS | 月付 | 不定 | 无声 |

### 最低规格

| 服务类型 | CPU | 内存 | 存储 |
|----------|-----|------|------|
| 基本 Web | 1 核 | 1 GB | 20 GB |
| 媒体服务器 | 2 核 | 4 GB | 1 TB |
| 数据库 | 2 核 | 4 GB | 100 GB |
| 全能 | 4 核 | 8 GB | 2 TB |

### 推荐硬件

| 组件 | 推荐 |
|------|------|
| CPU | Intel i5 或 AMD Ryzen 5 |
| 内存 | 16-32 GB |
| 存储 | SSD 用于系统，HDD 用于数据 |
| 网络 | 千兆以太网 |
| UPS | 电池备份 |

## 操作系统

### Linux 发行版

| 发行版 | 最佳用途 | 支持 |
|--------|----------|------|
| Ubuntu Server | 初学者 | 5 年 |
| Debian | 稳定性 | 3 年 |
| CentOS Stream | 企业 | 5 年 |
| Arch Linux | 高级用户 | 滚动更新 |
| Proxmox VE | 虚拟化 | 3 年 |

### 安装步骤

```bash
# 下载 ISO
# 创建可启动 USB
# 安装操作系统
# 配置网络
# 更新系统
sudo apt update && sudo apt upgrade -y
```

## Docker

### 为什么选择 Docker？

| 好处 | 描述 |
|------|------|
| 隔离 | 独立环境 |
| 可移植 | 任何地方运行 |
| 可重现 | 一致的设置 |
| 效率 | 共享资源 |
| 版本控制 | 轻松更新 |

### Docker 安装

```bash
# 安装 Docker
curl -fsSL https://get.docker.com -o get-docker.sh
sudo sh get-docker.sh

# 将用户添加到 docker 组
sudo usermod -aG docker $USER

# 安装 Docker Compose
sudo apt install docker-compose
```

### Docker Compose 示例

```yaml
version: '3'
services:
  web:
    image: nginx:alpine
    ports:
      - "80:80"
    volumes:
      - ./html:/usr/share/nginx/html

  database:
    image: postgres:13
    environment:
      - POSTGRES_PASSWORD=secret
    volumes:
      - postgres_data:/var/lib/postgresql/data

volumes:
  postgres_data:
```

## 网络

### 域名配置

| 步骤 | 描述 |
|------|------|
| 1. 注册域名 | 选择注册商 |
| 2. DNS 设置 | 指向服务器 |
| 3. SSL 证书 | 启用 HTTPS |
| 4. 反向代理 | 路由流量 |

### DNS 记录

| 类型 | 用途 | 示例 |
|------|------|------|
| A | IPv4 地址 | server.example.com → 1.2.3.4 |
| AAAA | IPv6 地址 | server.example.com → ::1 |
| CNAME | 别名 | www → server.example.com |
| MX | 邮件 | mail.example.com |

### 反向代理

#### Nginx 配置

```nginx
server {
    listen 80;
    server_name app.example.com;
    return 301 https://$server_name$request_uri;
}

server {
    listen 443 ssl;
    server_name app.example.com;

    ssl_certificate /etc/letsencrypt/live/app.example.com/fullchain.pem;
    ssl_certificate_key /etc/letsencrypt/live/app.example.com/privkey.pem;

    location / {
        proxy_pass http://localhost:8080;
        proxy_set_header Host $host;
        proxy_set_header X-Real-IP $remote_addr;
    }
}
```

### 使用 Let's Encrypt 配置 SSL

```bash
# 安装 Certbot
sudo apt install certbot python3-certbot-nginx

# 获取证书
sudo certbot --nginx -d app.example.com

# 自动续期
sudo certbot renew --dry-run
```

## 必备服务

### Web 服务器

| 服务器 | 用例 |
|--------|------|
| Nginx | 反向代理、静态文件 |
| Apache | 传统 Web 服务器 |
| Caddy | 自动 HTTPS |

### 数据库

| 数据库 | 类型 | 用例 |
|--------|------|------|
| PostgreSQL | 关系型 | 通用 |
| MySQL | 关系型 | Web 应用 |
| MongoDB | 文档型 | 灵活 Schema |
| Redis | 键值型 | 缓存 |

### 监控

| 工具 | 用途 |
|------|------|
| Uptime Kuma | 服务监控 |
| Grafana | 指标可视化 |
| Prometheus | 指标收集 |
| Netdata | 实时监控 |

## 常见自托管应用

### 媒体和娱乐

| 应用 | 用途 |
|------|------|
| Jellyfin | 媒体服务器 |
| Navidrome | 音乐服务器 |
| Immich | 照片管理 |
| Calibre-web | 电子书管理 |

### 生产力

| 应用 | 用途 |
|------|------|
| Nextcloud | 文件同步、日历 |
| Bitwarden | 密码管理器 |
| Joplin | 笔记 |
| Vikunja | 任务管理 |

### 通讯

| 应用 | 用途 |
|------|------|
| Matrix/Element | 聊天 |
| Mattermost | 团队消息 |
| Mailcow | 邮件服务器 |
| Discourse | 论坛 |

### 开发

| 应用 | 用途 |
|------|------|
| Gitea | Git 托管 |
| Drone CI | 持续集成 |
| Harbor | 容器镜像仓库 |
| Portainer | Docker 管理 |

### 家庭自动化

| 应用 | 用途 |
|------|------|
| Home Assistant | 智能家居 |
| Node-RED | 自动化 |
| ESPHome | IoT 设备 |
| Zigbee2MQTT | Zigbee 网关 |

## 安全

### 安全清单

| 实践 | 描述 |
|------|------|
| 强密码 | 使用密码管理器 |
| 2FA | 启用双因素认证 |
| 防火墙 | 配置 UFW/iptables |
| 更新 | 定期系统更新 |
| 备份 | 定期备份 |

### 防火墙配置

```bash
# 启用防火墙
sudo ufw enable

# 允许 SSH
sudo ufw allow 22/tcp

# 允许 HTTP/HTTPS
sudo ufw allow 80/tcp
sudo ufw allow 443/tcp

# 检查状态
sudo ufw status
```

### SSH 安全

```bash
# 禁用 root 登录
sudo sed -i 's/PermitRootLogin yes/PermitRootLogin no/' /etc/ssh/sshd_config

# 禁用密码认证
sudo sed -i 's/PasswordAuthentication yes/PasswordAuthentication no/' /etc/ssh/sshd_config

# 重启 SSH
sudo systemctl restart sshd
```

## 备份策略

### 备份方式

| 方式 | 描述 |
|------|------|
| rsync | 文件同步 |
| Borgbackup | 去重备份 |
| Restic | 加密备份 |
| Duplicati | 云备份 |

### 3-2-1 备份规则

| 规则 | 描述 |
|------|------|
| 3 份 | 备份总数 |
| 2 种介质 | 不同存储类型 |
| 1 份异地 | 远程备份位置 |

### 备份脚本

```bash
#!/bin/bash
# 数据库备份
pg_dump -U postgres dbname > /backup/db_$(date +%Y%m%d).sql

# 文件备份
rsync -av --delete /data/ /backup/data/

# 清理旧备份
find /backup -mtime +30 -delete
```

## 性能优化

### 系统调优

| 设置 | 描述 |
|------|------|
| Swap | 配置交换空间 |
| Limits | 设置文件描述符限制 |
| Kernel | 调优内核参数 |
| Scheduler | 优化 I/O 调度器 |

### Docker 优化

| 技巧 | 描述 |
|------|------|
| 资源限制 | 设置 CPU/内存限制 |
| 健康检查 | 监控容器健康 |
| 重启策略 | 失败时自动重启 |
| 日志轮转 | 限制日志大小 |

## 监控和维护

### 监控栈

| 组件 | 用途 |
|------|------|
| Prometheus | 指标收集 |
| Grafana | 可视化 |
| Alertmanager | 告警 |
| Node Exporter | 系统指标 |

### 定期维护

| 任务 | 频率 |
|------|------|
| 系统更新 | 每周 |
| 安全补丁 | 可用时 |
| 备份验证 | 每月 |
| 日志审查 | 每周 |
| 性能审查 | 每月 |

## 故障排除

### 常见问题

| 问题 | 可能原因 | 解决方案 |
|------|----------|----------|
| 服务无法启动 | 配置错误 | 检查日志 |
| CPU 使用率高 | 进程循环 | 识别进程 |
| 磁盘满 | 日志文件 | 清理日志 |
| 网络问题 | DNS/防火墙 | 检查配置 |

### 日志位置

| 服务 | 日志位置 |
|------|----------|
| 系统 | /var/log/syslog |
| Nginx | /var/log/nginx/ |
| Docker | docker logs container |
| 应用 | 应用特定 |

## 费用估算

### 每月费用

| 项目 | 费用范围 |
|------|----------|
| 电费 | $5-20 |
| 网络 | $50-100 |
| 域名 | $1-2 |
| VPS（可选） | $5-50 |
| **合计** | **$60-170** |

### 一次性费用

| 项目 | 费用范围 |
|------|----------|
| 服务器硬件 | $100-500 |
| UPS | $50-150 |
| 网络设备 | $50-200 |
| **合计** | **$200-850** |

## 入门指南

### 分步指南

| 步骤 | 操作 |
|------|------|
| 1 | 选择硬件 |
| 2 | 安装操作系统 |
| 3 | 配置网络 |
| 4 | 安装 Docker |
| 5 | 部署服务 |
| 6 | 设置备份 |
| 7 | 配置监控 |

### 首先部署的服务

| 优先级 | 服务 | 原因 |
|--------|------|------|
| 1 | 反向代理 | 所有服务都需要 |
| 2 | 监控 | 了解何时出问题 |
| 3 | 备份 | 保护数据 |
| 4 | 密码管理器 | 安全 |
| 5 | 文件同步 | 生产力 |

## 总结

| 组件 | 用途 |
|------|------|
| 硬件 | 物理服务器 |
| 操作系统 | 运行系统 |
| Docker | 容器运行时 |
| 网络 | 域名、SSL、代理 |
| 服务 | 应用 |
| 安全 | 保护 |
| 备份 | 数据安全 |
| 监控 | 可见性 |


---

## 来源：selfhosted.md

## 概述

自托管（Self-hosting）是指在自己的服务器上托管和管理应用程序，而非依赖第三方云服务提供商。本指南整理了数百款可自托管的免费开源软件，涵盖数据分析、通讯协作、内容管理、文件同步、媒体流、开发工具等众多领域。

**核心价值：**
- 数据主权：完全掌控自己的数据
- 隐私保护：避免第三方数据收集
- 成本可控：无订阅费用，按需部署
- 可定制性：根据需求自由修改和扩展

---

## 目录

1. [数据分析与可视化](#1-数据分析与可视化)
2. [数字归档与保存](#2-数字归档与保存)
3. [自动化工具](#3-自动化工具)
4. [博客平台](#4-博客平台)
5. [预约与排程](#5-预约与排程)
6. [书签与链接管理](#6-书签与链接管理)
7. [日历与联系人](#7-日历与联系人)
8. [通讯系统](#8-通讯系统)
9. [电子邮件](#9-电子邮件)
10. [内容管理系统（CMS）](#10-内容管理系统cms)
11. [客户关系管理（CRM）](#11-客户关系管理crm)
12. [数据库管理](#12-数据库管理)
13. [DNS 服务](#13-dns-服务)
14. [文档管理](#14-文档管理)
15. [电子商务](#15-电子商务)
16. [订阅阅读器](#16-订阅阅读器)
17. [文件传输与同步](#17-文件传输与同步)
18. [文件上传与分享](#18-文件上传与分享)
19. [游戏服务器](#19-游戏服务器)
20. [生成式人工智能](#20-生成式人工智能)
21. [群件协作](#21-群件协作)
22. [物联网（IoT）](#22-物联网iot)
23. [知识管理](#23-知识管理)
24. [学习与课程](#24-学习与课程)
25. [媒体管理](#25-媒体管理)
26. [媒体流](#26-媒体流)
27. [财务与预算](#27-财务与预算)
28. [笔记与编辑器](#28-笔记与编辑器)
29. [办公套件](#29-办公套件)
30. [密码管理](#30-密码管理)
31. [粘贴板服务](#31-粘贴板服务)
32. [个人仪表盘](#32-个人仪表盘)
33. [照片管理](#33-照片管理)
34. [投票与活动](#34-投票与活动)
35. [代理服务器](#35-代理服务器)
36. [食谱管理](#36-食谱管理)
37. [远程访问](#37-远程访问)
38. [企业资源规划（ERP）](#38-企业资源规划erp)
39. [搜索引擎](#39-搜索引擎)
40. [自托管解决方案](#40-自托管解决方案)
41. [软件开发工具](#41-软件开发工具)
42. [任务管理](#42-任务管理)
43. [工单系统](#43-工单系统)
44. [时间追踪](#44-时间追踪)
45. [URL 缩短器](#45-url-缩短器)
46. [视频监控](#46-视频监控)
47. [Web 服务器](#47-web-服务器)
48. [Wiki 系统](#48-wiki-系统)
49. [地图与 GPS](#49-地图与-gps)
50. [库存管理](#50-库存管理)
51. [人力资源管理](#51-人力资源管理)
52. [健康与健身](#52-健康与健身)
53. [家谱管理](#53-家谱管理)
54. [制造业工具](#54-制造业工具)
55. [社区农业协作](#55-社区农业协作)
56. [会议管理](#56-会议管理)

---

## 1. 数据分析与可视化

数据的计算分析，用于发现、解释和传达数据中的有意义模式。

| 项目名称 | 简介 | 许可证 | 技术栈 |
|---------|------|--------|--------|
| [Matomo](https://matomo.org/) | 保护用户隐私的网站分析（Google Analytics 替代品） | GPL-3.0 | PHP |
| [Plausible Analytics](https://plausible.io/) | 简洁轻量（<1KB）、隐私友好的网站分析 | AGPL-3.0 | Elixir |
| [Umami](https://umami.is/) | 简单、快速、注重隐私的 Google Analytics 替代品 | MIT | Nodejs/Docker |
| [PostHog](https://posthog.com) | 产品分析、会话录制、功能标记和 A/B 测试 | MIT | Python |
| [Metabase](https://metabase.com/) | 让公司每个人都能提问并从数据中学习 | AGPL-3.0 | Java/Docker |
| [Superset](http://superset.apache.org/) | 现代数据探索和可视化平台 | Apache-2.0 | Python |
| [GoAccess](http://goaccess.io/) | 实时 Web 日志分析器和交互式终端查看器 | GPL-2.0 | C |
| [GoatCounter](https://www.goatcounter.com) | 简单的网站统计，不追踪个人数据 | EUPL-1.2 | Go |
| [Redash](http://redash.io) | 连接查询数据源，构建仪表盘并分享 | BSD-2-Clause | Docker |
| [Swetrix](https://swetrix.com/) | 开源网站分析，满足所有需求 | AGPL-3.0 | Docker |
| [Offen](https://www.offen.dev/) | 公平、轻量的开源网站分析工具 | Apache-2.0 | Go/Docker |

---

## 2. 数字归档与保存

用于数字归档和长期保存的软件。

| 项目名称 | 简介 | 许可证 | 技术栈 |
|---------|------|--------|--------|
| [ArchiveBox](https://archivebox.io/) | 从书签、浏览历史、RSS 等创建 HTML 和截图归档 | MIT | Python/Docker |
| [Wallabag](https://www.wallabag.org) | 保存文章以便稍后阅读，提升可读性 | MIT | PHP |
| [CKAN](https://ckan.org) | 创建开放数据网站 | AGPL-3.0 | Python |
| [Wayback](https://github.com/wabarc/wayback) | 自托管网页归档工具包，支持多种存储后端 | GPL-3.0 | Go |
| [Piler](https://www.mailpiler.org/) | 功能丰富的电子邮件归档解决方案 | GPL-3.0 | C/Docker |

---

## 3. 自动化工具

减少人工干预的流程自动化软件。

| 项目名称 | 简介 | 许可证 | 技术栈 |
|---------|------|--------|--------|
| [Activepieces](https://www.activepieces.com) | 无代码业务自动化工具（Zapier 替代品） | MIT | Docker |
| [Apache Airflow](https://airflow.apache.org/) | 以编程方式编排、调度和监控工作流 | Apache-2.0 | Python/Docker |
| [Huginn](https://github.com/huginn/huginn) | 构建代表您监控和操作的代理 | MIT | Ruby |
| [changedetection.io](https://changedetection.io/) | 监控网站内容变化 | Apache-2.0 | Python/Docker |
| [Healthchecks](https://healthchecks.io/) | 监听 ping 并在延迟时发送警报 | BSD-3-Clause | Python/Docker |
| [Kestra](https://kestra.io) | 事件驱动、语言无关的工作流编排平台 | Apache-2.0 | Docker |

---

## 4. 博客平台

用于创建和管理博客的软件。

| 项目名称 | 简介 | 许可证 | 技术栈 |
|---------|------|--------|--------|
| [Ghost](https://ghost.org/) | 专注于内容发布的博客平台 | MIT | Nodejs |
| [WordPress](https://wordpress.org/) | 全球使用最广泛的博客和 CMS 引擎 | GPL-2.0 | PHP |
| [WriteFreely](https://writefreely.org) | 极简风格的联邦博客写作软件 | AGPL-3.0 | Go |
| [Castopod](https://castopod.org) | 播客管理托管平台，支持 Podcast 2.0 标准 | AGPL-3.0 | PHP/Docker |
| [HTMLy](https://www.htmly.com/) | 无数据库的 PHP 博客平台（扁平文件 CMS） | GPL-2.0 | PHP |

---

## 5. 预约与排程

活动排程、预约和预约管理软件。

| 项目名称 | 简介 | 许可证 | 技术栈 |
|---------|------|--------|--------|
| [Cal.diy](https://cal.diy/) | 在线预约排程系统 | MIT | Nodejs |
| [Easy!Appointments](https://easyappointments.org/) | 允许客户通过 Web 预约 | GPL-3.0 | PHP |
| [Rallly](https://rallly.co) | 创建投票来决定日期和时间（Doodle 替代品） | AGPL-3.0 | Nodejs/Docker |
| [Hi.Events](https://hi.events) | 活动管理和票务平台 | AGPL-3.0 | Docker |
| [Seatsurfing](https://seatsurfing.app/) | 办公室座位、桌面和房间预订 | GPL-3.0 | Docker |

---

## 6. 书签与链接管理

用于添加、标注、编辑和分享网页书签的软件。

| 项目名称 | 简介 | 许可证 | 技术栈 |
|---------|------|--------|--------|
| [linkding](https://linkding.link/) | 极简书签管理，快速干净的 UI | MIT | Docker |
| [LinkAce](https://www.linkace.org/) | 书签归档，支持自动备份到 Internet Archive | GPL-3.0 | Docker/PHP |
| [LinkWarden](https://linkwarden.app/) | 书签和归档管理器 | MIT | Docker/Nodejs |
| [Karakeep](https://karakeep.app/) | 带 AI 功能的全能书签应用 | AGPL-3.0 | Docker |
| [Shiori](https://github.com/go-shiori/shiori) | 用 Go 构建的简单书签管理器 | MIT | Go/Docker |
| [Shaarli](https://github.com/shaarli/Shaarli) | 个人极简、超快速、无数据库的书签和链接分享 | Zlib | PHP |
| [Readeck](https://readeck.org/en/) | 保存网页的可读内容，兼具书签管理和稍后阅读 | AGPL-3.0 | Go/Docker |

---

## 7. 日历与联系人

CalDAV 和 CardDAV 协议服务器及 Web 客户端。

| 项目名称 | 简介 | 许可证 | 技术栈 |
|---------|------|--------|--------|
| [Radicale](https://radicale.org/) | 简单的日历和联系人服务器，管理开销极低 | GPL-3.0 | Python |
| [Baikal](https://sabre.io/baikal/) | 基于 sabre/dav 的轻量级 CalDAV 和 CardDAV 服务器 | GPL-3.0 | PHP |
| [DAViCal](https://www.davical.org/) | 使用 PostgreSQL 的日历共享服务器 | GPL-2.0 | PHP |
| [SabreDAV](https://sabre.io/) | 开源 CardDAV、CalDAV 和 WebDAV 框架和服务器 | MIT | PHP |

---

## 8. 通讯系统

### 8.1 自定义通讯系统

| 项目名称 | 简介 | 许可证 | 技术栈 |
|---------|------|--------|--------|
| [Rocket.Chat](https://rocket.chat/) | 以数据保护为先的通讯平台（Slack 替代品） | MIT | Nodejs/Docker |
| [Zulip](https://zulip.org) | 强大的开源群聊应用 | Apache-2.0 | Python |
| [Element](https://element.io) | 功能完整的 Matrix 客户端（Web/iOS/Android） | Apache-2.0 | Nodejs |
| [Synapse](https://element-hq.github.io/synapse/latest/index.html) | Matrix 去中心化通讯协议的服务器 | Apache-2.0 | Python |
| [Mumble](https://wiki.mumble.info/wiki/Main_Page) | 低延迟、高质量的语音/文字聊天软件 | BSD-3-Clause | C++ |
| [ntfy](https://ntfy.sh/) | 使用 HTTP PUT/POST 推送通知到手机或桌面 | Apache-2.0 | Go/Docker |
| [Gotify](https://gotify.net/) | 带 Android 和 CLI 客户端的通知服务器 | MIT | Go/Docker |
| [Novu](https://novu.co/) | 面向开发者的通知基础设施 | MIT | Docker/Nodejs |
| [Apprise](https://github.com/caronc/apprise) | 向几乎所有主流通知服务发送通知 | MIT | Python/Docker |

### 8.2 社交网络与论坛

| 项目名称 | 简介 | 许可证 | 技术栈 |
|---------|------|--------|--------|
| [Mastodon](https://joinmastodon.org/) | 联邦制微博服务器 | AGPL-3.0 | Ruby |
| [Discourse](https://www.discourse.org/) | 基于 Ruby 和 JS 的高级论坛/社区解决方案 | GPL-2.0 | Docker |
| [Lemmy](https://join-lemmy.org/) | 联邦宇宙的链接聚合器（Reddit 替代品） | AGPL-3.0 | Docker/Rust |
| [Flarum](https://flarum.org) | 简洁优雅的论坛软件 | MIT | PHP |
| [NodeBB](https://nodebb.org/) | 为现代 Web 构建的论坛软件 | GPL-3.0 | Nodejs/Docker |
| [PixelFed](https://pixelfed.social) | 合乎道德的照片分享平台（Instagram 替代品） | AGPL-3.0 | PHP |
| [Misskey](https://misskey.io/) | 去中心化的微博服务器/SNS | AGPL-3.0 | Nodejs/Docker |
| [Isso](https://isso-comments.de/) | 轻量级评论服务器（Disqus 替代品） | MIT | Python/Docker |

### 8.3 视频会议

| 项目名称 | 简介 | 许可证 | 技术栈 |
|---------|------|--------|--------|
| [Jitsi Meet](https://jitsi.org/Projects/JitsiMeet) | 高质量、可扩展的视频会议 | Apache-2.0 | Nodejs/Docker |
| [BigBlueButton](https://bigbluebutton.org/) | 支持实时音视频、幻灯片、聊天和屏幕共享 | LGPL-3.0 | Java |
| [Galene](https://galene.org/) | 易于部署、资源需求适中的视频会议服务器 | MIT | Go |

---

## 9. 电子邮件

### 9.1 完整邮件解决方案

| 项目名称 | 简介 | 许可证 | 技术栈 |
|---------|------|--------|--------|
| [Mail-in-a-Box](https://mailinabox.email/) | 一条命令将 Ubuntu 服务器变成完整邮件服务器 | CC0-1.0 | Shell |
| [Mailcow](https://mailcow.email/) | 基于 Dovecot、Postfix 的邮件服务器套件，提供现代 Web UI | GPL-3.0 | Docker/PHP |
| [Mailu](https://mailu.io/) | 简单而功能完整的 Docker 邮件服务器 | MIT | Docker/Python |
| [docker-mailserver](https://docker-mailserver.github.io/docker-mailserver/edge/) | 生产就绪的全栈邮件服务器容器 | MIT | Docker |
| [Stalwart Mail Server](https://stalw.art) | 支持 JMAP、IMAP4 和 SMTP 的全功能邮件服务器 | AGPL-3.0 | Rust/Docker |
| [Maddy Mail Server](https://maddy.email/) | 一体化邮件服务器，单一守护进程替代多个组件 | GPL-3.0 | Go |
| [iRedMail](https://www.iredmail.org/) | 基于 Postfix 和 Dovecot 的完整邮件服务器方案 | GPL-3.0 | Shell |

### 9.2 邮件列表与新闻通讯

| 项目名称 | 简介 | 许可证 | 技术栈 |
|---------|------|--------|--------|
| [Listmonk](https://listmonk.app/) | 高性能自托管新闻通讯和邮件列表管理器 | AGPL-3.0 | Go/Docker |
| [Mailman](https://www.list.org/) | 管理电子邮件讨论和电子新闻通讯列表 | GPL-3.0 | Python |
| [Mautic](https://www.mautic.org/) | 营销自动化软件（邮件、社交媒体等） | GPL-3.0 | PHP |
| [Keila](https://www.keila.io) | 可靠易用的新闻通讯工具（Mailchimp 替代品） | AGPL-3.0 | Docker |

### 9.3 Webmail 客户端

| 项目名称 | 简介 | 许可证 | 技术栈 |
|---------|------|--------|--------|
| [Roundcube](https://roundcube.net) | 基于浏览器的 IMAP 客户端 | GPL-3.0 | PHP |
| [SnappyMail](https://snappymail.eu/) | 简单、现代、轻量快速的 Web 邮件客户端 | AGPL-3.0 | PHP |

---

## 10. 内容管理系统（CMS）

使用第三方插件、主题和功能来构建网站的实用方式。

| 项目名称 | 简介 | 许可证 | 技术栈 |
|---------|------|--------|--------|
| [WordPress](https://wordpress.org/) | 全球使用最广泛的博客和 CMS 引擎 | GPL-2.0 | PHP |
| [Drupal](https://www.drupal.org/) | 高级开源内容管理平台 | GPL-2.0 | PHP |
| [Strapi](https://strapi.io/) | 最先进的开源内容管理框架（Headless CMS） | MIT | Nodejs |
| [Payload CMS](https://payloadcms.com/) | 开发者优先的 Headless CMS 和应用框架 | MIT | Nodejs |
| [Joomla!](https://www.joomla.org/) | 高级内容管理系统 | GPL-2.0 | PHP |
| [Backdrop CMS](https://backdropcms.org/) | 面向中小型企业和非营利组织的综合 CMS | GPL-2.0 | PHP |
| [Cockpit](https://getcockpit.com) | 简单的内容平台，管理任何结构化内容 | MIT | PHP |
| [Squidex](https://squidex.io) | 基于 MongoDB 的 Headless CMS | MIT | .NET |
| [Wagtail](https://wagtail.io/) | 专注于灵活性和用户体验的 Django CMS | BSD-3-Clause | Python |
| [Plone](https://plone.org/) | 强大的开源 CMS 系统 | ZPL-2.0 | Python/Docker |

---

## 11. 客户关系管理（CRM）

管理、分析和改进客户互动的战略流程。

| 项目名称 | 简介 | 许可证 | 技术栈 |
|---------|------|--------|--------|
| [Twenty](https://twenty.com) | 现代 CRM，提供开源灵活性和高级功能 | AGPL-3.0 | Docker |
| [SuiteCRM](https://suitecrm.com) | 获奖的企业级开源 CRM | AGPL-3.0 | PHP |
| [EspoCRM](https://www.espocrm.com/) | 前端为单页应用的 CRM，带 REST API | AGPL-3.0 | PHP |
| [Monica](https://monicahq.com/) | 个人关系管理器，一种新型 CRM | AGPL-3.0 | PHP/Docker |
| [Corteza](https://docs.cortezaproject.org) | 包含统一工作区、企业消息和低代码环境的 CRM | Apache-2.0 | Go |

---

## 12. 数据库管理

数据库管理的 Web 界面，包括分析和可视化工具。

| 项目名称 | 简介 | 许可证 | 技术栈 |
|---------|------|--------|--------|
| [Adminer](https://www.adminer.org/) | 单个 PHP 文件中的数据库管理 | Apache-2.0 | PHP |
| [Baserow](https://baserow.io/) | 无需技术经验即可创建数据库（Airtable 替代品） | MIT | Docker |
| [Metabase](https://metabase.com/) | 让公司每个人都能从数据中学习 | AGPL-3.0 | Java/Docker |
| [Datasette](https://datasette.io/) | 探索和发布数据，支持导入导出和数据库管理 | Apache-2.0 | Python/Docker |
| [Bytebase](https://www.bytebase.com/) | 安全的数据库架构变更和版本控制 | MIT | Docker/Go |
| [CloudBeaver](https://dbeaver.com/) | 管理数据库，支持 PostgreSQL、MySQL、SQLite 等 | Apache-2.0 | Docker |
| [Mathesar](https://mathesar.org/) | 直观的 UI 协作管理数据，基于 Postgres | GPL-3.0 | Docker/Python |

---

## 13. DNS 服务

DNS 服务器和管理工具，主要面向家庭或小型网络。

| 项目名称 | 简介 | 许可证 | 技术栈 |
|---------|------|--------|--------|
| [Pi-hole](https://pi-hole.net/) | 网络广告黑洞，带 GUI 管理和监控 | EUPL-1.2 | Shell/PHP/Docker |
| [AdGuard Home](https://adguard.com/en/adguard-home/overview.html) | 用户友好的广告和追踪器阻止 DNS 服务器 | GPL-3.0 | Docker |
| [blocky](https://0xerr0r.github.io/blocky/latest/) | 快速轻量的 DNS 代理广告拦截器（Pi-hole 替代品） | Apache-2.0 | Go/Docker |
| [Technitium DNS Server](https://technitium.com/dns/) | 带广告拦截功能的权威/递归 DNS 服务器 | GPL-3.0 | Docker/C# |

---

## 14. 文档管理

用于接收、跟踪、管理和存储文档的系统。

| 项目名称 | 简介 | 许可证 | 技术栈 |
|---------|------|--------|--------|
| [Paperless-ngx](https://docs.paperless-ngx.com/) | 扫描、索引和归档纸质文档 | GPL-3.0 | Python/Docker |
| [Stirling-PDF](https://github.com/Stirling-Tools/Stirling-PDF) | 本地托管的 PDF 操作工具（合并、拆分、转换、OCR） | Apache-2.0 | Docker/Java |
| [Documenso](https://documenso.com) | 数字文档签名平台（DocuSign 替代品） | AGPL-3.0 | Nodejs/Docker |
| [Mayan EDMS](https://www.mayan-edms.com) | 电子文档管理系统，支持预览、OCR 和自动分类 | GPL-2.0 | Docker |
| [Gotenberg](https://gotenberg.dev) | 开发者友好的文档转换 API | MIT | Docker |
| [Docspell](https://docspell.org) | 自动标签的文档组织器和归档 | GPL-3.0 | Scala/Java/Docker |

### 电子书管理

| 项目名称 | 简介 | 许可证 | 技术栈 |
|---------|------|--------|--------|
| [Calibre Web](https://github.com/janeczku/calibre-web) | 使用现有 Calibre 数据库浏览、阅读和下载电子书 | GPL-3.0 | Python |
| [Kavita](https://www.kavitareader.com/) | 跨平台电子书/漫画/PDF 服务器和 Web 阅读器 | GPL-3.0 | .NET/Docker |
| [Komga](https://komga.org) | 漫画/图书媒体服务器，支持 API 和 OPDS | MIT | Java/Docker |
| [Audiobookshelf](https://www.audiobookshelf.org/) | 有声书和播客服务器，支持跨设备同步进度 | GPL-3.0 | Docker/Nodejs |

---

## 15. 电子商务

在线商店和电商平台软件。

| 项目名称 | 简介 | 许可证 | 技术栈 |
|---------|------|--------|--------|
| [WooCommerce](https://woocommerce.com/) | 基于 WordPress 的电商解决方案 | GPL-3.0 | PHP |
| [Saleor](https://saleor.io) | 基于 Django 的开源电商店面 | BSD-3-Clause | Docker/Python |
| [MedusaJs](https://medusajs.com/) | 无头电商引擎 | MIT | Nodejs |
| [PrestaShop](https://www.prestashop.com/) | 完全可扩展的电商解决方案 | OSL-3.0 | PHP |
| [Magento Open Source](https://business.adobe.com/products/magento/magento-commerce.html) | 领先的全渠道创新开源方案 | OSL-3.0 | PHP |
| [OpenCart](https://www.opencart.com) | 购物车解决方案 | GPL-3.0 | PHP |
| [Sylius](https://sylius.com) | 基于 Symfony 的开源全栈电商平台 | MIT | PHP |
| [Vendure](https://www.vendure.io) | 无头电商框架 | MIT | Nodejs |

---

## 16. 订阅阅读器

聚合网页内容（报纸、博客、播客等）的应用程序。

| 项目名称 | 简介 | 许可证 | 技术栈 |
|---------|------|--------|--------|
| [FreshRSS](https://freshrss.org/) | 自托管的 RSS 聚合器 | AGPL-3.0 | PHP/Docker |
| [Miniflux](https://miniflux.app/) | 极简新闻阅读器 | Apache-2.0 | Go/Docker |
| [Tiny Tiny RSS](https://tt-rss.org) | 基于 Web 的新闻阅读器和聚合器 | GPL-3.0 | Docker/PHP |
| [RSSHub](https://docs.rsshub.app) | 万物皆可 RSS，从社交媒体到大学部门 | MIT | Nodejs/Docker |
| [NewsBlur](https://www.newsblur.com/) | 个人新闻阅读器 | MIT | Python |
| [RSS-Bridge](https://github.com/RSS-Bridge/rss-bridge) | 为没有 RSS 的网站生成 RSS/ATOM 订阅源 | Unlicense | PHP/Docker |
| [CommaFeed](https://www.commafeed.com/) | Google Reader 风格的自托管 RSS 阅读器 | Apache-2.0 | Java/Docker |

---

## 17. 文件传输与同步

文件传输、共享和同步软件。

| 项目名称 | 简介 | 许可证 | 技术栈 |
|---------|------|--------|--------|
| [Nextcloud](https://nextcloud.com/) | 从任何设备访问和共享文件、日历、联系人、邮件等 | AGPL-3.0 | PHP |
| [Syncthing](https://syncthing.net/) | 开源点对点文件同步工具 | MPL-2.0 | Go/Docker |
| [Seafile](https://www.seafile.com/en/home/) | 面向团队和组织的文件托管和共享方案 | GPL-2.0 | C |
| [ownCloud](https://owncloud.org/) | 文件保存、同步、查看、编辑和共享的一体化方案 | AGPL-3.0 | PHP/Docker |
| [Samba](https://www.samba.org/) | Linux 和 Unix 的标准 Windows 互操作套件 | GPL-3.0 | C |
| [Cloudreve](https://cloudreve.org/) | 文件管理和共享系统，支持多种存储提供者 | GPL-3.0 | Docker/Go |

---

## 18. 文件上传与分享

简化文件服务器，提供单击或拖放上传功能。

| 项目名称 | 简介 | 许可证 | 技术栈 |
|---------|------|--------|--------|
| [Send](https://gitlab.com/timvisee/send) | 简单、私密、端到端加密的临时文件共享 | MPL-2.0 | Nodejs/Docker |
| [Sharry](https://github.com/eikek/sharry) | 通过互联网在认证和匿名用户之间轻松共享文件 | GPL-3.0 | Scala/Java/Docker |
| [Plik](https://github.com/root-gg/plik) | 可扩展友好的临时文件上传系统 | MIT | Go/Docker |
| [transfer.sh](https://github.com/dutchcoders/transfer.sh) | 从命令行轻松共享文件 | MIT | Go |
| [Filebrowser](https://filebrowser.org/) | 带 Material Design 的 Web 文件浏览器 | Apache-2.0 | Go |
| [Chibisafe](https://chibisafe.app) | 易于使用的文件上传器服务 | MIT | Docker/Nodejs |

---

## 19. 游戏服务器

多人游戏服务器和浏览器游戏。

| 项目名称 | 简介 | 许可证 | 技术栈 |
|---------|------|--------|--------|
| [Lila](https://lichess.org/) | 无广告的国际象棋服务器（lichess.org） | AGPL-3.0 | Scala |
| [OpenTTD](https://www.openttd.org/) | 运输大亨模拟游戏 | GPL-2.0 | C++/Docker |
| [Mindustry](https://mindustrygame.github.io/) | 类似 Factorio 的塔防游戏 | GPL-3.0 | Java |
| [Pterodactyl](https://pterodactyl.io/) | 游戏服务器管理面板 | MIT | PHP |
| [Pelican Panel](https://pelican.dev/) | 游戏服务器管理 Web 应用（Pterodactyl 分支） | AGPL-3.0 | PHP/Docker |

---

## 20. 生成式人工智能

用于生成文本、图像、视频或其他数据的 AI 工具。

| 项目名称 | 简介 | 许可证 | 技术栈 |
|---------|------|--------|--------|
| [Ollama](https://ollama.com/) | 运行 Llama、DeepSeek、Phi、Gemma 等大语言模型 | MIT | Docker/Python |
| [Open-WebUI](https://openwebui.com) | 用户友好的 AI 界面，支持 Ollama 和 OpenAI API | BSD-3-Clause | Docker/Python |
| [LocalAI](https://localai.io/) | 本地运行 AI 模型，生成图像和音频（OpenAI 替代品） | MIT | Docker/K8S |
| [LibreChat](https://www.librechat.ai) | 增强的 ChatGPT 兼容 AI 聊天界面 | MIT | Nodejs/Docker |
| [Khoj](https://khoj.dev/) | AI 第二大脑，从 Web 或文档获取答案 | AGPL-3.0 | Python/Docker |
| [AnythingLLM](https://anythingllm.com/) | 一体化桌面和 Docker AI 应用 | MIT | Nodejs/Docker |

---

## 21. 群件协作

帮助团队协作完成共同任务的软件。

| 项目名称 | 简介 | 许可证 | 技术栈 |
|---------|------|--------|--------|
| [Nextcloud](https://nextcloud.com/) | 访问和共享文件、日历、联系人等 | AGPL-3.0 | PHP |
| [Zimbra Collaboration](https://www.zimbra.com/) | 邮件、日历、协作服务器 | GPL-2.0 | Java |
| [SOGo](https://www.sogo.nu/) | 提供多种方式访问日历和消息数据 | LGPL-2.1 | Objective-C |
| [egroupware](https://www.egroupware.org/) | 包含日历、地址簿、项目管理、CRM 等的软件套件 | GPL-2.0 | PHP |
| [Cozy Cloud](https://cozy.io/) | 管理和同步文件、笔记、联系人、密码和个人文档的个人云 | GPL-3.0 | Nodejs |

---

## 22. 物联网（IoT）

连接和交换数据的物理对象和设备管理。

| 项目名称 | 简介 | 许可证 | 技术栈 |
|---------|------|--------|--------|
| [Home Assistant](https://home-assistant.io/) | 家庭自动化平台 | Apache-2.0 | Python/Docker |
| [openHAB](https://www.openhab.org) | 厂商和技术无关的开源家庭自动化软件 | EPL-2.0 | Java |
| [Node-RED](https://nodered.org/) | 基于浏览器的流程编辑器，连接硬件设备、API 和在线服务 | Apache-2.0 | Nodejs/Docker |
| [Domoticz](https://www.domoticz.com/) | 家庭自动化系统 | GPL-3.0 | C/C++/Docker |
| [Gladys](https://gladysassistant.com/) | 隐私优先的家庭助手 | Apache-2.0 | Nodejs/Docker |
| [Thingsboard](https://thingsboard.io/) | 开源 IoT 平台：设备管理、数据收集、处理和可视化 | Apache-2.0 | Java/Docker |

---

## 23. 知识管理

创建、共享、使用和管理知识与信息的方法集合。

| 项目名称 | 简介 | 许可证 | 技术栈 |
|---------|------|--------|--------|
| [AFFiNE](https://affine.pro/) | 下一代知识库，集规划、排序和创建于一体（Notion 替代品） | MIT/AGPL-3.0 | Docker |
| [SiYuan](https://b3log.org/siyuan/) | 隐私优先的个人知识管理软件 | AGPL-3.0 | Docker/Go |
| [BookStack](https://www.bookstackapp.com/) | 以书籍方式组织和存储文档 | MIT | PHP/Docker |
| [Wiki.js](https://js.wiki/) | 现代轻量强大的 Wiki 应用 | AGPL-3.0 | Nodejs/Docker |

---

## 24. 学习与课程

教育和学习工具及软件。

| 项目名称 | 简介 | 许可证 | 技术栈 |
|---------|------|--------|--------|
| [Moodle](https://moodle.org/) | 全球最大开源社区之一的学习和课程平台 | GPL-3.0 | PHP |
| [Canvas LMS](https://www.instructure.com/canvas/) | 革新教育方式的学习管理系统 | AGPL-3.0 | Ruby |
| [edX](https://www.edx.org/) | 驱动 edX.org 的开源平台 | AGPL-3.0 | Python |
| [Chamilo LMS](https://chamilo.org/) | 创建虚拟校园，提供在线或半在线培训 | GPL-3.0 | PHP |

---

## 25. 媒体管理

数字媒体管理工具和软件。

| 项目名称 | 简介 | 许可证 | 技术栈 |
|---------|------|--------|--------|
| [Sonarr](https://sonarr.tv/) | Usenet 和 BitTorrent 的自动电视剧下载管理器 | GPL-3.0 | C#/Docker |
| [Radarr](https://radarr.video/) | Usenet 和 BitTorrent 的自动电影下载（Sonarr 分支） | GPL-3.0 | C#/Docker |
| [Lidarr](https://lidarr.audio/) | Usenet 和 BitTorrent 用户的音乐收藏管理器 | GPL-3.0 | C#/Docker |
| [MeTube](https://github.com/alexta69/metube) | youtube-dl 的 Web GUI，支持播放列表 | AGPL-3.0 | Python/Docker |
| [Ombi](https://ombi.io/) | Plex/Emby 的内容请求系统 | GPL-2.0 | C# |

---

## 26. 媒体流

### 26.1 音频流

| 项目名称 | 简介 | 许可证 | 技术栈 |
|---------|------|--------|--------|
| [Navidrome](https://www.navidrome.org) | 现代音乐服务器和流媒体，兼容 Subsonic/Airsonic | GPL-3.0 | Docker/Go |
| [Jellyfin](https://jellyfin.org) | 音频、视频、书籍、漫画和照片的媒体服务器 | GPL-2.0 | C#/Docker |
| [Funkwhale](https://dev.funkwhale.audio/funkwhale) | 现代、基于 Web 的多用户音乐服务器 | BSD-3-Clause | Python |
| [koel](https://koel.dev/) | 个人音乐流媒体服务器 | MIT | PHP |
| [Ampache](https://ampache.org/) | 基于 Web 的音频/视频流应用 | AGPL-3.0 | PHP |
| [AzuraCast](https://www.azuracast.com/) | 现代易用的网络电台管理套件 | Apache-2.0 | Docker |

### 26.2 视频流

| 项目名称 | 简介 | 许可证 | 技术栈 |
|---------|------|--------|--------|
| [Jellyfin](https://jellyfin.org) | 免费的媒体服务器（Plex 替代品） | GPL-2.0 | C#/Docker |
| [PeerTube](https://joinpeertube.org/en/) | 去中心化视频流平台，使用 P2P 技术 | AGPL-3.0 | Nodejs |
| [Owncast](https://owncast.online/) | 去中心化单用户直播视频流和聊天服务器 | MIT | Go |
| [OvenMediaEngine](https://github.com/OvenMediaLabs/OvenMediaEngine) | 亚秒级延迟的流媒体服务器 | AGPL-3.0 | C++/Docker |
| [Invidious](https://github.com/iv-org/invidious) | 替代性 YouTube 前端 | AGPL-3.0 | Docker/Crystal |

---

## 27. 财务与预算

个人和企业财务管理软件。

| 项目名称 | 简介 | 许可证 | 技术栈 |
|---------|------|--------|--------|
| [Firefly III](https://firefly-iii.org/) | 现代财务管理器，支持信用卡、高级规则引擎 | AGPL-3.0 | PHP/Docker |
| [Actual](https://actualbudget.org) | 本地优先的个人财务工具，基于零基预算 | MIT | Nodejs/Docker |
| [Ghostfolio](https://ghostfol.io/) | 财富管理软件，跟踪股票、ETF 和加密货币 | AGPL-3.0 | Docker/Nodejs |
| [IHateMoney](https://ihatemoney.org/) | 轻松管理共享开支 | BSD-3-Clause | Docker/Python |
| [InvoicePlane](https://www.invoiceplane.com/) | 管理报价、发票、付款和客户 | MIT | PHP |
| [BTCPay Server](https://btcpayserver.org/) | 比特币和其他加密货币支付处理器 | MIT | C# |
| [FOSSBilling](https://fossbilling.org/) | 托管和计费自动化 | Apache-2.0 | PHP/Docker |

---

## 28. 笔记与编辑器

笔记记录和编辑器软件。

| 项目名称 | 简介 | 许可证 | 技术栈 |
|---------|------|--------|--------|
| [Joplin](https://joplinapp.org/) | 带 Markdown 编辑器和加密支持的笔记应用（Evernote 替代品） | MIT | Nodejs |
| [Standard Notes](https://docs.standardnotes.com/self-hosting/getting-started) | 简单私密的笔记应用 | GPL-3.0 | Ruby |
| [HedgeDoc](https://hedgedoc.org/) | 全平台实时协作 Markdown 笔记 | AGPL-3.0 | Docker/Nodejs |
| [TriliumNext Notes](https://github.com/TriliumNext/Trilium) | 跨平台分层笔记应用，专注于构建大型个人知识库 | AGPL-3.0 | Nodejs/Docker |
| [SilverBullet](https://silverbullet.md/) | 为黑客思维优化的笔记应用 | MIT | Docker/Deno |
| [Memos](https://usememos.com/) | 使用 SQLite 数据库的知识库 | MIT | Docker/Go |
| [Overleaf](https://www.overleaf.com/) | 基于 Web 的协作 LaTeX 编辑器 | AGPL-3.0 | Ruby |
| [AppFlowy](https://appflowy.io/) | 开源 Notion 替代品 | AGPL-3.0 | Rust/Docker |

---

## 29. 办公套件

包含文字处理、电子表格和演示文稿程序的生产力软件集合。

| 项目名称 | 简介 | 许可证 | 技术栈 |
|---------|------|--------|--------|
| [ONLYOFFICE](https://helpcenter.onlyoffice.com/faq/server-opensource.aspx) | 在一个地方管理文档、项目、团队和客户关系 | AGPL-3.0 | Nodejs/Docker |
| [Collabora Online](https://www.collaboraoffice.com/code) | 基于 LibreOffice 的强大在线办公套件 | MPL-2.0 | C++ |
| [CryptPad](https://cryptpad.org) | 为协作而构建的加密协作套件 | AGPL-3.0 | Nodejs/Docker |
| [Etherpad](https://etherpad.org/) | 高度可定制的实时协作在线编辑器 | Apache-2.0 | Nodejs/Docker |
| [Grist](https://getgrist.com/) | 具有关系结构的下一代电子表格（Airtable 替代品） | Apache-2.0 | Nodejs/Python/Docker |

---

## 30. 密码管理

用于存储、生成和管理密码的工具。

| 项目名称 | 简介 | 许可证 | 技术栈 |
|---------|------|--------|--------|
| [Vaultwarden](https://github.com/dani-garcia/vaultwarden) | 轻量级 Bitwarden 服务器 API 实现 | GPL-3.0 | Rust/Docker |
| [Bitwarden](https://bitwarden.com/) | 带 Web 应用、浏览器扩展和移动应用的密码管理器 | AGPL-3.0 | Docker/C# |
| [Passbolt](https://www.passbolt.com/) | 协作密码管理器 | AGPL-3.0 | PHP/Docker |

---

## 31. 粘贴板服务

用于共享和存储代码及文本的在线内容托管服务。

| 项目名称 | 简介 | 许可证 | 技术栈 |
|---------|------|--------|--------|
| [PrivateBin](https://privatebin.info/) | 极简粘贴板/讨论板，服务器对托管数据零知识 | Zlib | PHP |
| [Hemmelig](https://hemmelig.app) | 跨组织共享加密密钥 | MIT | Docker/Nodejs |
| [Opengist](https://opengist.io) | 由 Git 驱动的粘贴板 | AGPL-3.0 | Docker/Go |
| [Yopass](https://github.com/jhaals/yopass) | 密码、密钥和文件的安全共享 | Apache-2.0 | Go/Docker |

---

## 32. 个人仪表盘

用于访问信息和应用程序的仪表盘。

| 项目名称 | 简介 | 许可证 | 技术栈 |
|---------|------|--------|--------|
| [Homer](https://github.com/bastienwirtz/homer) | 极简静态主页，展示服务器服务 | Apache-2.0 | Docker/Nodejs |
| [Dashy](https://dashy.to/) | 功能丰富的家庭实验室主页 | MIT | Nodejs/Docker |
| [Homarr](https://homarr.dev) | 时尚现代的仪表盘，众多集成 | MIT | Docker/Nodejs |
| [Heimdall](https://heimdall.site/) | 组织所有 Web 应用的优雅方案 | MIT | PHP |
| [Glance](https://github.com/glanceapp/glance) | 高度可定制的仪表盘，将所有订阅源集中一处 | AGPL-3.0 | Docker/Go |
| [Homepage](https://github.com/gethomepage/homepage) | 高度可定制的主页，支持 Docker 和服务 API 集成 | GPL-3.0 | Docker/Nodejs |

---

## 33. 照片管理

用于发布或分享照片、图片、视频或其他数字媒体的软件。

| 项目名称 | 简介 | 许可证 | 技术栈 |
|---------|------|--------|--------|
| [Immich](https://immich.app/) | 直接从手机备份照片和视频（Google Photos 替代品） | AGPL-3.0 | Docker |
| [PhotoPrism](https://photoprism.org) | 由 Go 和 TensorFlow 驱动的个人照片管理 | AGPL-3.0 | Go/Docker |
| [Ente](https://ente.io/) | 端到端加密的照片分享平台 | AGPL-3.0 | Docker/Nodejs/Go |
| [LibrePhotos](https://github.com/LibrePhotos/librephotos) | 照片管理服务（Google Photos 替代品） | MIT | Python/Docker |
| [Piwigo](https://piwigo.org/) | 由活跃社区构建的照片库软件 | GPL-2.0 | PHP |
| [Lychee](https://lycheeorg.github.io/) | 基于网格和相册的照片管理系统 | MIT | PHP/Docker |
| [Photoview](https://photoview.github.io/) | 面向摄影师的简单用户友好照片库 | GPL-3.0 | Go/Docker |

---

## 34. 投票与活动

组织投票和活动的软件。

| 项目名称 | 简介 | 许可证 | 技术栈 |
|---------|------|--------|--------|
| [Mobilizon](https://mobilizon.org) | 帮助发现、创建和组织活动与团体的联邦工具 | AGPL-3.0 | Elixir/Docker |
| [LimeSurvey](https://www.limesurvey.org) | 功能丰富的基于 Web 的投票软件 | GPL-2.0 | PHP |
| [Formbricks](https://formbricks.com) | 基于全球最大开源调查堆栈的体验管理套件 | AGPL-3.0 | Nodejs/Docker |
| [Fider](https://fider.io) | 收集和优先排序反馈的开放平台 | MIT | Docker |
| [Gancio](https://gancio.org/) | 本地社区活动和日程分享 | AGPL-3.0 | Nodejs |

---

## 35. 代理服务器

在客户端和服务器之间充当中介的服务器应用。

| 项目名称 | 简介 | 许可证 | 技术栈 |
|---------|------|--------|--------|
| [Squid](http://www.squid-cache.org/) | 支持 HTTP、HTTPS、FTP 等的 Web 缓存代理 | GPL-2.0 | C |
| [Privoxy](https://www.privoxy.org) | 非缓存 Web 代理，具有高级过滤功能 | GPL-2.0 | C |
| [imgproxy](https://imgproxy.net/) | 快速安全的远程图像调整和转换服务器 | MIT | Go/Docker |
| [Outline Server](https://getoutline.org/) | 运行 Shadowsocks 实例的代理服务器 | Apache-2.0 | Docker/Nodejs |

---

## 36. 食谱管理

管理食谱的软件和工具。

| 项目名称 | 简介 | 许可证 | 技术栈 |
|---------|------|--------|--------|
| [Mealie](https://nightly.mealie.io/) | Material Design 风格的食谱管理器 | MIT | Python |
| [Bar Assistant](https://barassistant.app/) | 管理家庭酒吧，添加原料、搜索鸡尾酒 | MIT | PHP/Docker |
| [RecipeSage](https://github.com/julianpoy/recipesage) | 食谱保存器、膳食计划组织器和购物清单管理器 | AGPL-3.0 | Nodejs |

---

## 37. 远程访问

远程桌面和 SSH 服务器及 Web 界面。

| 项目名称 | 简介 | 许可证 | 技术栈 |
|---------|------|--------|--------|
| [Guacamole](https://guacamole.apache.org) | 无客户端远程桌面网关，支持 VNC 和 RDP | Apache-2.0 | Java/C |
| [MeshCentral](https://meshcentral.com/) | 运行 Web 服务器以远程管理和控制计算机 | Apache-2.0 | Nodejs |
| [Firezone](https://www.firezone.dev/) | 支持 WireGuard 协议的安全远程访问网关 | Apache-2.0 | Elixir/Docker |
| [ShellHub](https://www.shellhub.io) | 现代 SSH 服务器，通过命令行或 Web UI 远程访问 Linux 设备 | Apache-2.0 | Docker |

---

## 38. 企业资源规划（ERP）

资源和供应链规划软件。

| 项目名称 | 简介 | 许可证 | 技术栈 |
|---------|------|--------|--------|
| [ERPNext](https://frappe.io/erpnext) | 帮助运营业务的 ERP 系统 | GPL-3.0 | Python/Docker |
| [Odoo](https://www.odoo.com) | 免费开源 ERP 系统 | LGPL-3.0 | Python/Docker |
| [Dolibarr](https://www.dolibarr.org/) | 现代 CRM 软件包，管理公司活动 | GPL-3.0 | PHP |
| [grocy](https://grocy.info/) | 冰箱之外的 ERP，杂货和家务管理方案 | MIT | PHP/Docker |
| [LedgerSMB](https://ledgersmb.org/) | 集成会计和 ERP 系统 | GPL-2.0 | Docker/Perl |

---

## 39. 搜索引擎

帮助查找存储在计算机系统中的信息的信息检索系统。

| 项目名称 | 简介 | 许可证 | 技术栈 |
|---------|------|--------|--------|
| [SearXNG](https://docs.searxng.org/) | 互联网元搜索引擎，聚合各种搜索服务的结果 | AGPL-3.0 | Python/Docker |
| [MeiliSearch](https://www.meilisearch.com) | 超相关、即时且容错的全文搜索 API | MIT | Rust/Docker |
| [Typesense](https://typesense.org) | 极速容错的开源搜索引擎 | GPL-3.0 | C++/Docker |
| [Apache Solr](https://lucene.apache.org/solr/) | 企业搜索平台 | Apache-2.0 | Java/Docker |
| [OpenSearch](https://opensearch.org) | 分布式 RESTful 搜索引擎 | Apache-2.0 | Java/Docker |
| [Yacy](https://yacy.net/en/index.html) | 基于 P2P 的去中心化搜索引擎服务器 | GPL-2.0 | Java/Docker |

---

## 40. 自托管解决方案

用于轻松安装、管理和配置自托管服务的软件。

| 项目名称 | 简介 | 许可证 | 技术栈 |
|---------|------|--------|--------|
| [YunoHost](https://yunohost.org/) | 旨在让自托管人人可及的服务器操作系统 | AGPL-3.0 | Python/Shell |
| [CasaOS](https://casaos.zimaspace.com/) | 简单易用优雅的家庭云系统 | Apache-2.0 | Go/Docker |
| [Tipi](https://runtipi.io/) | 家庭服务器管理器，一键安装自托管应用 | GPL-3.0 | Shell |
| [FreedomBox](https://freedombox.org/) | 为私人通讯运行自由软件的个人服务器 | AGPL-3.0 | Python |
| [Sandstorm](https://sandstorm.io/) | 轻松安全运行自托管应用的个人服务器 | Apache-2.0 | C++/Shell |
| [OpenMediaVault](https://www.openmediavault.org/) | 基于 Debian Linux 的 NAS 解决方案 | GPL-3.0 | PHP |
| [DietPi](https://dietpi.com/) | 针对单板计算机优化的极简 Debian 系统 | GPL-2.0 | Shell |

---

## 41. 软件开发工具

### 41.1 项目管理与代码托管

| 项目名称 | 简介 | 许可证 | 技术栈 |
|---------|------|--------|--------|
| [GitLab](https://about.gitlab.com) | 自托管 Git 仓库管理、代码审查、问题跟踪 | MIT | Ruby/Docker |
| [Gitea](https://gitea.com) | 轻松自托管的一体化软件开发服务 | MIT | Go/Docker |
| [Forgejo](https://forgejo.org) | 专注于扩展、联邦和隐私的轻量级软件锻造 | MIT | Docker/Go |
| [Gogs](https://gogs.io/) | 无痛自托管 Git 服务 | MIT | Go |
| [Redmine](https://www.redmine.org/) | 灵活的项目管理 Web 应用 | GPL-2.0 | Ruby |
| [Plane](https://plane.so) | 以最简单的方式跟踪问题、史诗和产品路线图 | AGPL-3.0 | Docker |
| [Taiga](https://www.taiga.io/) | 基于看板和 Scrum 方法的敏捷项目管理工具 | MPL-2.0 | Docker/Python |
| [OpenProject](https://www.openproject.org) | 管理项目、任务和目标 | GPL-3.0 | Ruby/Docker |

### 41.2 API 管理

| 项目名称 | 简介 | 许可证 | 技术栈 |
|---------|------|--------|--------|
| [Kong](https://konghq.com/kong/) | 微服务 API 网关和平台 | Apache-2.0 | Lua/Docker |
| [Tyk](https://tyk.io) | 快速可扩展的开源 API 网关 | MPL-2.0 | Go/Docker |
| [Hasura](https://hasura.io) | 在 Postgres 上快速即时的实时 GraphQL API | Apache-2.0 | Haskell/Docker |
| [Hoppscotch](https://hoppscotch.io) | 快速美观的 API 请求构建器 | MIT | Nodejs/Docker |

### 41.3 低代码平台

| 项目名称 | 简介 | 许可证 | 技术栈 |
|---------|------|--------|--------|
| [Appsmith](https://www.appsmith.com/) | 构建管理面板、CRUD 应用和工作流 | Apache-2.0 | Java/Docker |
| [ToolJet](https://tooljet.io/) | 低代码框架，以最少的工程工作量构建和部署内部工具 | GPL-3.0 | Nodejs/Docker |
| [PocketBase](https://pocketbase.io/) | 一个文件中的后端服务 | MIT | Go/Docker |
| [Saltcorn](https://saltcorn.com/) | 无代码数据库应用构建器 | MIT | Docker/Nodejs |
| [Appwrite](https://appwrite.io) | 面向 Web、原生和移动开发者的端到端后端服务器 | BSD-3-Clause | Docker |

### 41.4 IDE 与开发工具

| 项目名称 | 简介 | 许可证 | 技术栈 |
|---------|------|--------|--------|
| [code-server](https://github.com/coder/code-server) | 浏览器中的 VS Code | MIT | Nodejs/Docker |
| [JupyterLab](https://jupyterlab.readthedocs.io/en/stable/) | 交互式和可复现计算的 Web 环境 | BSD-3-Clause | Python/Docker |
| [Langfuse](https://langfuse.com) | LLM 工程平台，用于模型追踪、提示管理和应用评估 | MIT | Docker |

### 41.5 本地化

| 项目名称 | 简介 | 许可证 | 技术栈 |
|---------|------|--------|--------|
| [Weblate](https://weblate.org) | 基于 Web 的翻译工具，与版本控制紧密集成 | GPL-3.0 | Python/Docker |
| [Tolgee](https://tolgee.io) | 面向开发者和翻译者的 Web 本地化平台 | Apache-2.0 | Docker/Java |

---

## 42. 任务管理

任务管理软件。

| 项目名称 | 简介 | 许可证 | 技术栈 |
|---------|------|--------|--------|
| [Vikunja](https://vikunja.io/) | 组织生活的待办应用 | AGPL-3.0 | Go |
| [Kanboard](https://kanboard.org/) | 简单的可视化任务看板 | MIT | PHP |
| [Wekan](https://wekan.github.io/) | 开源 Trello 风格看板 | MIT | Nodejs |
| [Super Productivity](https://super-productivity.com) | 高级待办列表应用，集成时间箱和时间追踪 | MIT | Docker |
| [AppFlowy](https://appflowy.io/) | 开源 Notion 替代品 | AGPL-3.0 | Rust/Docker |

---

## 43. 工单系统

帮助跟踪用户请求、错误和功能缺失的帮助台软件。

| 项目名称 | 简介 | 许可证 | 技术栈 |
|---------|------|--------|--------|
| [Zammad](https://zammad.org/) | 易用但强大的开源支持和工单系统 | AGPL-3.0 | Ruby |
| [FreeScout](https://freescout.net/) | 基于邮件的客户支持应用（Zendesk 替代品） | AGPL-3.0 | PHP/Docker |
| [MantisBT](https://www.mantisbt.org/) | 适合软件开发的错误跟踪器 | GPL-2.0 | PHP |
| [Bugzilla](https://www.bugzilla.org/) | 通用错误跟踪和测试工具 | MPL-2.0 | Perl |

---

## 44. 时间追踪

允许用户记录在任务或项目上花费时间的软件。

| 项目名称 | 简介 | 许可证 | 技术栈 |
|---------|------|--------|--------|
| [ActivityWatch](https://activitywatch.net) | 自动追踪在设备上的时间花费 | MPL-2.0 | Python |
| [Kimai](https://www.kimai.org/) | 跟踪工作时间并按需打印活动摘要 | AGPL-3.0 | PHP |
| [solidtime](https://www.solidtime.io) | 面向自由职业者和机构的现代时间追踪应用 | AGPL-3.0 | Docker |
| [Wakapi](https://wakapi.dev/) | 编码统计追踪工具，兼容 WakaTime | GPL-3.0 | Go/Docker |

---

## 45. URL 缩短器

缩短 URL 以使其更短同时仍指向所需页面的操作。

| 项目名称 | 简介 | 许可证 | 技术栈 |
|---------|------|--------|--------|
| [Shlink](https://shlink.io) | 带 REST API 和命令行界面的 URL 缩短器 | MIT | PHP/Docker |
| [Kutt](https://kutt.to) | 支持自定义域名和自定义 URL 的现代 URL 缩短器 | MIT | Nodejs/Docker |
| [YOURLS](https://yourls.org/) | 运行自己的 URL 缩短器的 PHP 脚本集 | MIT | PHP |

---

## 46. 视频监控

使用视频摄像机进行安全区域或持续监控。

| 项目名称 | 简介 | 许可证 | 技术栈 |
|---------|------|--------|--------|
| [Frigate](https://frigate.video/) | 使用本地处理的 AI 监控安全摄像头 | MIT | Docker/Python |
| [Zoneminder](https://www.zoneminder.com/) | 支持 IP、USB 和模拟摄像头的 CCTV 软件 | GPL-2.0 | PHP |
| [motionEye](https://github.com/motioneye-project/motioneye) | Motion 视频监控程序的在线界面 | GPL-3.0 | Python/Docker |

---

## 47. Web 服务器

Web 服务器和反向代理。

| 项目名称 | 简介 | 许可证 | 技术栈 |
|---------|------|--------|--------|
| [Nginx](https://nginx.org/en/) | HTTP 和反向代理服务器 | BSD-2-Clause | C/Docker |
| [Apache HTTP Server](https://httpd.apache.org/) | 安全高效可扩展的 HTTP 服务 | Apache-2.0 | C/Docker |
| [Caddy](https://caddyserver.com/) | 自动 HTTPS 的强大开源 Web 服务器 | Apache-2.0 | Go/Docker |
| [Traefik](https://traefik.io/) | HTTP 反向代理和负载均衡器 | MIT | Go/Docker |
| [HAProxy](https://www.haproxy.org/) | 非常快速可靠的反向代理 | GPL-2.0 | C/Docker |
| [Nginx Proxy Manager](https://nginxproxymanager.com/) | 管理 Nginx 代理主机的 Docker 容器 | MIT | Docker |
| [BunkerWeb](https://www.bunkerweb.io) | 下一代 Web 应用防火墙（WAF） | AGPL-3.0 | Docker/Python |
| [SafeLine](https://waf.chaitin.com/) | Web 应用防火墙/反向代理 | GPL-3.0 | Docker |

---

## 48. Wiki 系统

由其读者直接使用 Web 浏览器协作编辑和管理的出版物。

| 项目名称 | 简介 | 许可证 | 技术栈 |
|---------|------|--------|--------|
| [Wiki.js](https://js.wiki/) | 现代轻量强大的 Wiki 应用 | AGPL-3.0 | Nodejs/Docker |
| [BookStack](https://www.bookstackapp.com/) | 以书籍方式组织和存储信息 | MIT | PHP/Docker |
| [DokuWiki](https://www.dokuwiki.org/DokuWiki) | 易用轻量的 Wiki 引擎，无需数据库 | GPL-2.0 | PHP |
| [XWiki](https://www.xwiki.org) | 第二代 Wiki，支持强大的扩展架构 | LGPL-2.1 | Java/Docker |
| [TiddlyWiki](https://tiddlywiki.com/) | 可复用的非线性个人 Web 笔记本 | BSD-3-Clause | Nodejs |
| [Gollum](https://github.com/gollum/gollum) | 简单的 Git 驱动 Wiki | MIT | Ruby |
| [docmost](https://docmost.com/) | 协作 Wiki 和文档软件（Confluence、Notion 替代品） | AGPL-3.0 | Docker/Nodejs |

---

## 49. 地图与 GPS

地图、制图、GIS 和 GPS 软件。

| 项目名称 | 简介 | 许可证 | 技术栈 |
|---------|------|--------|--------|
| [OpenStreetMap](https://www.openstreetmap.org/) | 创建自由可编辑世界地图的协作项目 | GPL-2.0 | Ruby |
| [Traccar](https://www.traccar.org/) | 追踪 GPS 位置的 Java 应用 | Apache-2.0 | Java |
| [GraphHopper](https://graphhopper.com/) | 使用 OpenStreetMap 的快速路由库和服务器 | Apache-2.0 | Java |
| [Nominatim](https://nominatim.org/) | OpenStreetMap 数据的地理编码和反向地理编码 | GPL-2.0 | C |

---

## 50. 库存管理

库存管理软件。

| 项目名称 | 简介 | 许可证 | 技术栈 |
|---------|------|--------|--------|
| [InvenTree](https://docs.inventree.org/en/latest/) | 提供直观零件管理和库存控制的库存管理系统 | MIT | Python |
| [HomeBox](https://homebox.software/) | 为家庭用户构建的库存和组织系统 | AGPL-3.0 | Docker/Go |
| [Part-DB](https://docs.part-db.de/) | 电子元件库存管理系统 | AGPL-3.0 | Docker/PHP |

---

## 51. 人力资源管理

人力资源管理系统。

| 项目名称 | 简介 | 许可证 | 技术栈 |
|---------|------|--------|--------|
| [Frappe HR](https://frappe.io/hr) | 完整的 HRMS 方案，包含 13+ 模块 | GPL-3.0 | Docker/Python |

---

## 52. 健康与健身

医疗、健康和健身软件。

| 项目名称 | 简介 | 许可证 | 技术栈 |
|---------|------|--------|--------|
| [OpenEMR](https://www.open-emr.org/) | 电子健康记录和医疗实践管理方案 | GPL-3.0 | PHP/Docker |
| [wger](https://wger.de/) | 基于 Web 的个人健身和体重追踪器 | AGPL-3.0 | Python/Docker |
| [FitTrackee](https://docs.fittrackee.org/) | 简单的锻炼/活动追踪器 | AGPL-3.0 | Python/Docker |

---

## 53. 家谱管理

用于记录、组织和发布家谱数据的软件。

| 项目名称 | 简介 | 许可证 | 技术栈 |
|---------|------|--------|--------|
| [webtrees](https://www.webtrees.net) | Web 上领先的在线协作家谱应用 | GPL-3.0 | PHP |
| [Gramps Web](https://www.grampsweb.org/) | 基于 Gramps 的协作家谱 Web 应用 | AGPL-3.0 | Docker |
| [GeneWeb](https://geneweb.tuxfamily.org/wiki/GeneWeb) | 可离线使用或作为 Web 服务的家谱软件 | GPL-2.0 | OCaml |

---

## 54. 制造业工具

管理 3D 打印机、CNC 机器和其他物理制造工具的软件。

| 项目名称 | 简介 | 许可证 | 技术栈 |
|---------|------|--------|--------|
| [OctoPrint](https://octoprint.org/) | 控制消费级 3D 打印机的 Web 界面 | AGPL-3.0 | Docker/Python |
| [Mainsail](https://docs.mainsail.xyz/) | Klipper 3D 打印机固件的现代响应式 UI | GPL-3.0 | Docker/Python |
| [CNCjs](https://cnc.js.org/) | CNC 铣削控制器的 Web 界面 | MIT | Nodejs |

---

## 55. 社区农业协作

社区支持农业和食品合作社的管理工具。

| 项目名称 | 简介 | 许可证 | 技术栈 |
|---------|------|--------|--------|
| [Foodsoft](https://foodcoops.net/) | 管理非营利食品合作社 | AGPL-3.0 | Docker/Ruby |
| [Open Food Network](https://www.openfoodnetwork.org/) | 本地食品在线市场 | AGPL-3.0 | Ruby |

---

## 56. 会议管理

学术会议的摘要提交和管理软件。

| 项目名称 | 简介 | 许可证 | 技术栈 |
|---------|------|--------|--------|
| [pretalx](https://pretalx.org) | 基于 Web 的活动管理，包括征稿、审稿和排程 | Apache-2.0 | Python |
| [indico](https://getindico.io/) | CERN 开发的功能丰富的活动管理系统 | MIT | Python |

---

## 关键要点

### 选型建议

1. **个人用户优先考虑：** 部署简单、资源占用低、社区活跃的项目
2. **企业用户优先考虑：** 安全性、可扩展性、技术支持和合规性
3. **Docker 部署：** 大多数现代自托管项目都支持 Docker，推荐作为首选部署方式
4. **数据备份：** 无论选择哪个方案，定期备份都是必须的

### 部署前检查清单

- 确认服务器硬件配置满足最低要求
- 检查项目是否仍在活跃维护（最近提交时间）
- 阅读官方文档的安装指南
- 配置 HTTPS 和防火墙
- 设置自动化备份策略
- 考虑使用反向代理（如 Nginx、Caddy）统一管理多个服务

### 常见部署架构

```
互联网 → 反向代理（Caddy/Nginx）→ 各自托管应用
                                    ├── Nextcloud（文件）
                                    ├── Gitea（代码）
                                    ├── Jellyfin（媒体）
                                    ├── Vaultwarden（密码）
                                    └── 其他服务...
```

### 许可证说明

| 许可证 | 类型 | 要点 |
|--------|------|------|
| MIT | 宽松 | 几乎无限制，可商用 |
| Apache-2.0 | 宽松 | 允许商用，需保留版权声明 |
| GPL-2.0/3.0 | Copyleft | 修改后代码必须以相同许可证发布 |
| AGPL-3.0 | 强 Copyleft | 网络使用也需开源 |
| BSD-2/3-Clause | 宽松 | 类似 MIT，限制极少 |
| MPL-2.0 | 弱 Copyleft | 文件级 Copyleft |

---

## 外部资源

- [Awesome Sysadmin](https://github.com/awesome-foss/awesome-sysadmin) - 系统管理员开源资源精选列表
- [PRISM Break](https://prism-break.org/en/) - 隐私和去中心化软件推荐
- [awesome-web-archiving](https://github.com/iipc/awesome-web-archiving) - Web 归档资源
- [awesome-openstreetmap](https://github.com/osmlab/awesome-openstreetmap) - OpenStreetMap 资源


---

## 来源：hosting.md

## 简介

自托管意味着在自己的基础设施上运行软件，而不是依赖第三方 SaaS 提供商。这种方式让你完全控制数据、隐私和自定义。本教程涵盖自托管软件的主要类别和部署实践指导。

## 为什么要自托管

| 优势 | 描述 |
|------|------|
| 数据所有权 | 所有数据保存在你的服务器上 |
| 隐私 | 没有第三方访问你的信息 |
| 自定义 | 修改和扩展以满足需求 |
| 成本控制 | 避免按用户计费的 SaaS 订阅费 |
| 独立性 | 没有供应商锁定或服务关停 |
| 合规性 | 满足数据驻留要求 |

## 基础设施要求

| 组件 | 最低配置 | 推荐配置 |
|------|----------|----------|
| CPU | 2 核 | 4+ 核 |
| 内存 | 2 GB | 8+ GB |
| 存储 | 20 GB SSD | 100+ GB SSD |
| 网络 | 10 Mbps | 100+ Mbps |
| 操作系统 | Ubuntu 22.04 LTS | Ubuntu 22.04/Debian 12 |

## 部署方式

### Docker Compose

大多数自托管应用提供 Docker 镜像。

```yaml
version: "3"
services:
  app:
    image: application:latest
    ports:
      - "8080:8080"
    volumes:
      - ./data:/app/data
    restart: unless-stopped
```

### Proxmox

用于运行多个服务的虚拟化平台。

| 功能 | 描述 |
|------|------|
| LXC 容器 | 轻量级 Linux 容器 |
| 虚拟机 | 完整虚拟机 |
| 集群 | 多节点管理 |
| 备份 | 内置备份和恢复 |

### Kubernetes

用于高可用的生产级部署。

| 工具 | 用途 |
|------|------|
| k3s | 轻量级 Kubernetes |
| Helm | Kubernetes 包管理器 |
| Traefik | 入口控制器 |
| Cert-Manager | 自动化 TLS 证书 |

## 类别：文件存储和同步

| 软件 | 描述 | 核心功能 |
|------|------|----------|
| Nextcloud | 文件同步和共享平台 | 办公套件集成 |
| Seafile | 高性能文件同步 | 块级同步 |
| Syncthing | 点对点文件同步 | 无需中央服务器 |
| MinIO | S3 兼容对象存储 | 与 AWS S3 API 兼容 |
| FileBrowser | 基于 Web 的文件管理器 | 简单轻量 |

## 类别：通信

| 软件 | 描述 | 协议 |
|------|------|------|
| Matrix (Synapse) | 去中心化聊天 | Matrix 协议 |
| Rocket.Chat | 团队通信 | Web、移动、桌面 |
| Mattermost | Slack 替代品 | 频道、线程 |
| Jitsi Meet | 视频会议 | WebRTC |
| Mumble | 语音聊天（游戏） | 低延迟音频 |
| Mailcow | 邮件服务器 | SMTP/IMAP |

## 类别：媒体和娱乐

| 软件 | 描述 | 媒体类型 |
|------|------|----------|
| Jellyfin | 媒体流服务器 | 电影、电视、音乐 |
| Navidrome | 音乐流媒体 | 音频文件 |
| Immich | 照片和视频备份 | 照片、视频 |
| Kavita | 电子书阅读器 | 漫画、小说、书籍 |
| Audiobookshelf | 有声书和播客服务器 | 音频 |
| TubeArchivist | YouTube 存档器 | YouTube 视频 |

## 类别：生产力

| 软件 | 描述 | 替代 |
|------|------|------|
| BookStack | Wiki 和文档 | Confluence |
| Vikunja | 任务和项目管理 | Todoist、Asana |
| Outline | 团队知识库 | Notion |
| Cal.com | 日程安排和预约 | Calendly |
| Penpot | 设计和原型 | Figma |
| CryptPad | 协作文档 | Google Docs |

## 类别：监控和分析

| 软件 | 描述 | 重点 |
|------|------|------|
| Grafana | 仪表板和可视化 | 指标 |
| Prometheus | 指标收集和告警 | 基础设施 |
| Umami | 网站分析 | 注重隐私 |
| Plausible | 网站分析 | 符合 GDPR |
| Uptime Kuma | 正常运行时间监控 | 服务健康 |
| Netdata | 实时性能监控 | 系统指标 |

## 类别：DevOps 和开发

| 软件 | 描述 | 用途 |
|------|------|------|
| Gitea | Git 托管 | 源代码管理 |
| Drone | 持续集成 | 构建自动化 |
| Harbor | 容器注册表 | Docker 镜像存储 |
| Portainer | Docker 管理 UI | 容器管理 |
| Nginx Proxy Manager | 反向代理 | HTTPS 路由 |

## 类别：安全和身份

| 软件 | 描述 | 使用场景 |
|------|------|----------|
| Vaultwarden | 密码管理器 | 凭证存储 |
| Authentik | 身份提供者 | SSO、LDAP |
| Authelia | 认证门户 | 2FA、SSO |
| WireGuard | VPN 服务器 | 安全隧道 |
| CrowdSec | 协作安全 | 威胁检测 |

## 反向代理设置

反向代理对于将流量路由到多个服务至关重要。

### Nginx Proxy Manager 配置

```nginx
server {
    listen 80;
    server_name app.example.com;
    return 301 https://$host$request_uri;
}

server {
    listen 443 ssl;
    server_name app.example.com;

    ssl_certificate /etc/letsencrypt/live/app.example.com/fullchain.pem;
    ssl_certificate_key /etc/letsencrypt/live/app.example.com/privkey.pem;

    location / {
        proxy_pass http://localhost:8080;
        proxy_set_header Host $host;
        proxy_set_header X-Real-IP $remote_addr;
        proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
        proxy_set_header X-Forwarded-Proto $scheme;
    }
}
```

## 备份策略

| 方法 | 工具 | 频率 |
|------|------|------|
| 文件备份 | rsync、borgbackup | 每日 |
| 数据库导出 | pg_dump、mysqldump | 每日 |
| Docker 卷 | tar、restic | 每周 |
| 异地同步 | rclone、rsync.net | 持续 |

### 备份脚本示例

```bash
#!/bin/bash
BACKUP_DIR="/backups/$(date +%Y%m%d)"
mkdir -p "$BACKUP_DIR"

# 备份 Docker 卷
docker run --rm \
  -v app_data:/data:ro \
  -v "$BACKUP_DIR":/backup \
  alpine tar czf /backup/app_data.tar.gz -C /data .

# 备份数据库
docker exec db_container pg_dump -U postgres mydb > "$BACKUP_DIR/db.sql"

# 保留最近 7 天
find /backups -maxdepth 1 -mtime +7 -exec rm -rf {} \;
```

## 安全最佳实践

| 实践 | 描述 |
|------|------|
| 全面使用 HTTPS | 使用 Let's Encrypt 并自动续期 |
| 防火墙 | 仅允许端口 80、443 和 SSH |
| 定期更新 | 保持操作系统和应用补丁更新 |
| 非 root 容器 | 以非特权用户运行服务 |
| 网络隔离 | 使用 Docker 网络隔离服务 |
| 强密码 | 使用密码管理器管理凭证 |
| 2FA | 启用双因素认证 |

## 资源规划

| 服务类型 | 内存估算 | CPU 估算 | 存储估算 |
|----------|----------|----------|----------|
| 轻量级（静态站点） | 128 MB | 0.1 核 | 1 GB |
| 中等（Nextcloud、Gitea） | 1 GB | 1 核 | 50 GB |
| 重型（Jellyfin、Matrix） | 4 GB | 2 核 | 500 GB |
| 数据库 | 2 GB | 1 核 | 100 GB |

## 总结

自托管相比 SaaS 替代方案提供了控制权、隐私和成本节省。从小型 VPS 或家庭服务器开始，使用 Docker Compose 部署服务，设置带 TLS 的反向代理，并实施可靠的备份策略。awesome-selfhosted 列表包含数百个各类别选项，使得几乎可以用自托管替代方案替换每个云服务。


---
