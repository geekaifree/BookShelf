# Awesome Self-Hosted：自托管软件指南

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
