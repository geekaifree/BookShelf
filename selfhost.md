# 自托管指南

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
