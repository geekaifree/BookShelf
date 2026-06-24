# 自托管指南

## 目录

- [入门](#入门)
- [服务器设置](#服务器设置)
- [操作系统选择](#操作系统选择)
- [Docker 基础](#docker-基础)
- [反向代理](#反向代理)
- [SSL 证书](#ssl-证书)
- [DNS 设置](#dns-设置)
- [备份策略](#备份策略)
- [监控](#监控)
- [安全加固](#安全加固)
- [性能调优](#性能调优)

---

## 入门

### 为什么要自托管？

| 优势 | 说明 |
|---------|-------------|
| 隐私 | 数据保留在自己的硬件上 |
| 控制 | 完全掌控软件和配置 |
| 定制 | 按需修改任何内容 |
| 学习 | 深入了解服务运行原理 |
| 成本 | 长期来看可能比云服务更便宜 |
| 独立 | 无供应商锁定 |

### 需要什么

| 要求 | 说明 |
|-------------|-------------|
| 硬件 | 服务器、旧电脑或 VPS |
| 网络 | 稳定的连接和良好的上传速度 |
| 域名 | 方便访问和获取 SSL 证书 |
| 时间 | 用于设置和持续维护 |
| 基本 Linux 知识 | 命令行基础 |

### 硬件选项

| 选项 | 优点 | 缺点 |
|--------|------|------|
| 旧电脑 | 免费、性能强 | 噪音大、耗电 |
| Raspberry Pi | 低功耗、静音 | 资源有限 |
| 迷你主机 | 小巧、高效 | 有成本 |
| VPS | 无需维护硬件 | 月费、存储有限 |
| 独立服务器 | 性能强、可靠 | 贵 |

---

## 服务器设置

### 初始服务器配置

**第 1 步：更新系统**

    # Debian/Ubuntu
    sudo apt update && sudo apt upgrade -y

    # CentOS/RHEL
    sudo yum update -y

    # Fedora
    sudo dnf upgrade -y

**第 2 步：创建非 Root 用户**

    # 创建用户
    sudo adduser username

    # 添加到 sudo 组
    sudo usermod -aG sudo username

    # 切换到新用户
    su - username

**第 3 步：设置主机名**

    sudo hostnamectl set-hostname your-hostname

**第 4 步：配置时区**

    sudo timedatectl set-timezone UTC

### 网络配置

| 设置 | 说明 |
|---------|-------------|
| 静态 IP | 分配固定 IP 地址 |
| 防火墙 | 配置 UFW 或 iptables |
| SSH | 安全远程访问 |
| DNS | 将域名指向服务器 |

**基本防火墙设置（UFW）：**

    # 启用防火墙
    sudo ufw enable

    # 允许 SSH
    sudo ufw allow 22/tcp

    # 允许 HTTP/HTTPS
    sudo ufw allow 80/tcp
    sudo ufw allow 443/tcp

    # 检查状态
    sudo ufw status verbose

---

## 操作系统选择

### Linux 发行版

| 发行版 | 最佳用途 | 包管理器 |
|--------------|----------|-----------------|
| Ubuntu LTS | 初学者、通用 | apt |
| Debian | 稳定性、服务器 | apt |
| Fedora | 最新特性 | dnf |
| CentOS Stream | 类企业级 | dnf |
| Alpine | 容器、极简 | apk |
| Arch Linux | 高级用户 | pacman |

### 对比

| 特性 | Ubuntu LTS | Debian | Fedora |
|---------|------------|--------|--------|
| 发布周期 | 2 年 | 2-3 年 | 6 个月 |
| 支持时长 | 5 年 | 3 年（稳定版） | 13 个月 |
| 软件新旧 | 适中 | 稳定 | 最新 |
| 社区 | 非常大 | 大 | 大 |
| 文档 | 优秀 | 优秀 | 良好 |
| 容器支持 | 优秀 | 优秀 | 优秀 |

### 推荐配置

| 使用场景 | 推荐系统 |
|----------|----------------|
| 首次自托管 | Ubuntu LTS |
| 最大稳定性 | Debian |
| 最新软件 | Fedora |
| 仅容器 | Alpine |
| Raspberry Pi | Raspberry Pi OS |

---

## Docker 基础

### 为什么用 Docker？

| 优势 | 说明 |
|---------|-------------|
| 隔离 | 每个服务在独立容器中运行 |
| 一致性 | 各处环境相同 |
| 易更新 | 拉取新镜像、重启即可 |
| 资源高效 | 比虚拟机开销更小 |
| 可移植 | 在服务器间迁移容器 |

### 安装 Docker

    # 安装 Docker
    curl -fsSL https://get.docker.com -o get-docker.sh
    sudo sh get-docker.sh

    # 将用户添加到 docker 组
    sudo usermod -aG docker $USER

    # 安装 Docker Compose
    sudo apt install docker-compose-plugin

    # 验证安装
    docker --version
    docker compose version

### Docker 概念

| 概念 | 说明 |
|---------|-------------|
| 镜像 | 容器的只读模板 |
| 容器 | 镜像的运行实例 |
| 卷 | 持久数据存储 |
| 网络 | 容器间通信 |
| Dockerfile | 构建镜像的指令 |
| Compose | 多容器应用定义 |

### Docker Compose 示例

    version: '3'

    services:
      webapp:
        image: nginx:alpine
        ports:
          - "8080:80"
        volumes:
          - ./html:/usr/share/nginx/html
        restart: unless-stopped

      database:
        image: postgres:15
        environment:
          POSTGRES_PASSWORD: securepassword
          POSTGRES_DB: myapp
        volumes:
          - db-data:/var/lib/postgresql/data
        restart: unless-stopped

    volumes:
      db-data:

### 常用 Docker 命令

| 命令 | 用途 |
|---------|---------|
| `docker ps` | 列出运行中的容器 |
| `docker ps -a` | 列出所有容器 |
| `docker images` | 列出镜像 |
| `docker pull image` | 下载镜像 |
| `docker start container` | 启动容器 |
| `docker stop container` | 停止容器 |
| `docker rm container` | 删除容器 |
| `docker logs container` | 查看容器日志 |
| `docker exec -it container bash` | 进入容器 shell |

### Docker Compose 命令

| 命令 | 用途 |
|---------|---------|
| `docker compose up -d` | 后台启动服务 |
| `docker compose down` | 停止并删除服务 |
| `docker compose ps` | 列出运行中的服务 |
| `docker compose logs` | 查看服务日志 |
| `docker compose pull` | 更新服务镜像 |
| `docker compose restart` | 重启服务 |

### 数据管理

**命名卷：**

    volumes:
      db-data:
        driver: local

**绑定挂载：**

    volumes:
      - ./config:/app/config
      - /data:/app/data

**备份卷：**

    # 备份卷
    docker run --rm -v myvolume:/source -v $(pwd):/backup alpine tar czf /backup/myvolume.tar.gz -C /source .

    # 恢复卷
    docker run --rm -v myvolume:/target -v $(pwd):/backup alpine tar xzf /backup/myvolume.tar.gz -C /target

---

## 反向代理

### 什么是反向代理？

反向代理位于客户端和你的服务之间，处理：

| 功能 | 说明 |
|----------|-------------|
| SSL 终止 | 处理 HTTPS 加密 |
| 路由 | 将请求定向到正确的服务 |
| 负载均衡 | 在服务间分配流量 |
| 缓存 | 存储频繁请求的内容 |
| 安全 | 隐藏后端服务器、限速 |

### 热门选项

| 软件 | 说明 |
|----------|-------------|
| Nginx | 高性能 Web 服务器和反向代理 |
| Caddy | 自动 HTTPS、配置简单 |
| Traefik | Docker 感知的反向代理 |
| HAProxy | 高性能负载均衡器 |
| SWAG | 安全 Web 应用网关（基于 Nginx） |

### Nginx 配置

    server {
        listen 80;
        server_name example.com;
        return 301 https://$server_name$request_uri;
    }

    server {
        listen 443 ssl http2;
        server_name example.com;

        ssl_certificate /etc/letsencrypt/live/example.com/fullchain.pem;
        ssl_certificate_key /etc/letsencrypt/live/example.com/privkey.pem;

        location / {
            proxy_pass http://localhost:8080;
            proxy_set_header Host $host;
            proxy_set_header X-Real-IP $remote_addr;
            proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
            proxy_set_header X-Forwarded-Proto $scheme;
        }
    }

### Caddy 配置

    example.com {
        reverse_proxy localhost:8080
    }

Caddy 自动获取和续期 SSL 证书。

### Traefik 配置（Docker）

    version: '3'

    services:
      traefik:
        image: traefik:v2.10
        command:
          - "--providers.docker=true"
          - "--entrypoints.web.address=:80"
          - "--entrypoints.websecure.address=:443"
          - "--certificatesresolvers.letsencrypt.acme.email=you@example.com"
          - "--certificatesresolvers.letsencrypt.acme.storage=/letsencrypt/acme.json"
          - "--certificatesresolvers.letsencrypt.acme.httpchallenge.entrypoint=web"
        ports:
          - "80:80"
          - "443:443"
        volumes:
          - /var/run/docker.sock:/var/run/docker.sock:ro
          - traefik-certs:/letsencrypt

      webapp:
        image: nginx:alpine
        labels:
          - "traefik.enable=true"
          - "traefik.http.routers.webapp.rule=Host(\`example.com\`)"
          - "traefik.http.routers.webapp.entrypoints=websecure"
          - "traefik.http.routers.webapp.tls.certresolver=letsencrypt"

    volumes:
      traefik-certs:

---

## SSL 证书

### 为什么需要 SSL？

| 优势 | 说明 |
|---------|-------------|
| 加密 | 保护传输中的数据 |
| 身份验证 | 验证服务器身份 |
| 信任 | 浏览器显示锁图标 |
| SEO | Google 偏好 HTTPS 站点 |

### Let's Encrypt

免费、自动化的 SSL 证书。

**安装 Certbot：**

    # Debian/Ubuntu
    sudo apt install certbot

    # 带 Nginx 插件
    sudo apt install python3-certbot-nginx

**获取证书：**

    # 独立模式
    sudo certbot certonly --standalone -d example.com

    # Nginx 模式
    sudo certbot --nginx -d example.com

**自动续期：**

    # 测试续期
    sudo certbot renew --dry-run

    # 检查定时器
    sudo systemctl status certbot.timer

### 证书位置

| 文件 | 用途 |
|------|---------|
| `/etc/letsencrypt/live/domain.com/fullchain.pem` | 证书 + 链 |
| `/etc/letsencrypt/live/domain.com/privkey.pem` | 私钥 |
| `/etc/letsencrypt/live/domain.com/cert.pem` | 仅证书 |
| `/etc/letsencrypt/live/domain.com/chain.pem` | 仅链 |

### SSL 最佳实践

| 实践 | 说明 |
|----------|-------------|
| 使用 TLS 1.2+ | 禁用旧协议 |
| 强加密套件 | 使用现代加密套件 |
| HSTS | 强制浏览器使用 HTTPS |
| OCSP Stapling | 提升 SSL 性能 |
| 证书监控 | 跟踪过期日期 |

---

## DNS 设置

### DNS 记录

| 记录 | 用途 | 示例 |
|--------|---------|---------|
| A | 将域名指向 IPv4 | `example.com -> 192.168.1.1` |
| AAAA | 将域名指向 IPv6 | `example.com -> 2001:db8::1` |
| CNAME | 别名 | `www -> example.com` |
| MX | 邮件服务器 | `example.com -> mail.example.com` |
| TXT | 文本信息 | SPF、DKIM 记录 |
| NS | 名称服务器 | `example.com -> ns1.dns.com` |

### 动态 DNS

适用于 IP 地址会变化的家庭服务器。

**服务：**

| 服务 | 说明 |
|---------|-------------|
| DuckDNS | 免费动态 DNS |
| No-IP | 带免费层级的动态 DNS |
| Cloudflare | 带 API 的 DNS 更新 |
| ddclient | 动态 DNS 客户端 |

**ddclient 配置：**

    # /etc/ddclient.conf
    protocol=dyndns2
    use=web
    server=domains.google.com
    login=username
    password='password'
    example.com

---

## 备份策略

### 备份类型

| 类型 | 说明 | 速度 | 存储 |
|------|-------------|-------|---------|
| 全量 | 所有数据的完整副本 | 慢 | 高 |
| 增量 | 上次备份后的变更 | 快 | 低 |
| 差异 | 上次全量后的变更 | 中等 | 中等 |

### 3-2-1 备份法则

| 法则 | 说明 |
|------|-------------|
| 3 份副本 | 至少保留 3 份数据副本 |
| 2 种介质 | 存储在 2 种不同类型的介质上 |
| 1 份异地 | 保留 1 份异地副本 |

### 备份工具

| 工具 | 说明 |
|------|-------------|
| Restic | 快速、加密、去重 |
| BorgBackup | 去重、压缩 |
| Duplicati | 图形界面、云存储支持 |
| rsync | 文件同步 |
| rsnapshot | 基于 rsync 的增量备份 |

### 备份脚本示例

    #!/bin/bash

    # 变量
    BACKUP_DIR="/backups"
    DATE=$(date +%Y-%m-%d)
    RETENTION_DAYS=30

    # 备份 Docker 卷
    for volume in $(docker volume ls -q); do
        docker run --rm \
            -v $volume:/source:ro \
            -v $BACKUP_DIR:/backup \
            alpine tar czf /backup/$volume-$DATE.tar.gz -C /source .
    done

    # 备份数据库
    docker exec postgres pg_dump -U postgres mydb > $BACKUP_DIR/mydb-$DATE.sql

    # 删除旧备份
    find $BACKUP_DIR -name "*.tar.gz" -mtime +$RETENTION_DAYS -delete
    find $BACKUP_DIR -name "*.sql" -mtime +$RETENTION_DAYS -delete

### 使用 Cron 自动备份

    # 编辑 crontab
    crontab -e

    # 每天凌晨 2 点备份
    0 2 * * * /path/to/backup.sh

    # 每周日凌晨 3 点全量备份
    0 3 * * 0 /path/to/full-backup.sh

---

## 监控

### 监控什么

| 类别 | 指标 |
|----------|---------|
| 系统 | CPU、内存、磁盘、网络 |
| 服务 | 可用性、响应时间 |
| 应用 | 错误、性能 |
| 安全 | 登录失败、可疑活动 |

### 监控工具

| 工具 | 说明 |
|------|-------------|
| Uptime Kuma | 简单的可用性监控 |
| Netdata | 实时系统监控 |
| Prometheus + Grafana | 指标收集和可视化 |
| Zabbix | 企业级监控 |
| LibreNMS | 网络监控 |

### Uptime Kuma 设置

    version: '3'

    services:
      uptime-kuma:
        image: louislam/uptime-kuma
        ports:
          - "3001:3001"
        volumes:
          - uptime-kuma:/app/data
        restart: unless-stopped

    volumes:
      uptime-kuma:

### 告警

| 方式 | 说明 |
|--------|-------------|
| 邮件 | 传统告警 |
| Telegram | 即时通知 |
| Discord | 团队通知 |
| Slack | 团队通知 |

---

## 安全加固

### SSH 安全

| 设置 | 说明 |
|---------|-------------|
| 禁用 root 登录 | 防止直接 root 访问 |
| 使用密钥认证 | 比密码更安全 |
| 更改默认端口 | 减少自动化攻击 |
| 限制用户 | 仅允许特定用户 |

**SSH 加固（/etc/ssh/sshd_config）：**

    PermitRootLogin no
    PasswordAuthentication no
    PubkeyAuthentication yes
    Port 2222
    AllowUsers username
    MaxAuthTries 3

### 防火墙配置

| 规则 | 用途 |
|------|---------|
| 允许 SSH | 远程访问 |
| 允许 HTTP/HTTPS | Web 服务 |
| 阻止其他一切 | 默认拒绝 |

**UFW 命令：**

    sudo ufw default deny incoming
    sudo ufw default allow outgoing
    sudo ufw allow 2222/tcp  # SSH
    sudo ufw allow 80/tcp    # HTTP
    sudo ufw allow 443/tcp   # HTTPS
    sudo ufw enable

### Fail2Ban

在多次登录失败后封禁 IP 地址。

    # 安装
    sudo apt install fail2ban

    # 配置 /etc/fail2ban/jail.local
    [sshd]
    enabled = true
    port = 2222
    maxretry = 3
    bantime = 3600

### 自动更新

    # 安装 unattended-upgrades
    sudo apt install unattended-upgrades

    # 配置 /etc/apt/apt.conf.d/50unattended-upgrades
    Unattended-Upgrade::Allowed-Origins {
        "${distro_id}:${distro_codename}";
        "${distro_id}:${distro_codename}-security";
    };

### 安全清单

| 任务 | 说明 |
|------|-------------|
| 定期更新 | 保持系统和软件更新 |
| 使用强密码 | 长随机密码 |
| 启用 2FA | 尽可能启用双因素认证 |
| 限制访问 | 仅开放必要端口和用户 |
| 监控日志 | 检查可疑活动 |
| 定期备份 | 测试恢复流程 |
| 加密数据 | 静态和传输中 |
| 使用 VPN | 用于远程访问 |

---

## 性能调优

### 系统优化

| 领域 | 优化 |
|------|--------------|
| Swap | 配置适当的 swap 大小 |
| 文件系统 | 使用合适的文件系统（ext4、xfs） |
| 内核 | 调优内核参数 |
| 服务 | 禁用不必要的服务 |

### Docker 优化

| 实践 | 说明 |
|----------|-------------|
| 使用 Alpine 镜像 | 更小的镜像体积 |
| 多阶段构建 | 减小最终镜像体积 |
| 资源限制 | 设置 CPU 和内存限制 |
| 健康检查 | 监控容器健康 |
| 日志 | 限制日志大小 |

**资源限制示例：**

    services:
      webapp:
        image: nginx:alpine
        deploy:
          resources:
            limits:
              cpus: '0.50'
              memory: 512M
            reservations:
              cpus: '0.25'
              memory: 256M

### 数据库优化

| 设置 | 说明 |
|---------|-------------|
| 连接池 | 复用数据库连接 |
| 查询优化 | 添加索引、优化查询 |
| 缓存 | 缓存频繁查询 |
| 维护 | 定期 VACUUM、ANALYZE |

### Web 服务器优化

| 设置 | 说明 |
|---------|-------------|
| Gzip 压缩 | 减小传输体积 |
| 缓存 | 缓存静态资源 |
| Keep-alive | 复用连接 |
| Worker 进程 | 匹配 CPU 核心数 |

**Nginx 优化：**

    worker_processes auto;
    worker_connections 1024;

    gzip on;
    gzip_types text/plain text/css application/json application/javascript;

    keepalive_timeout 65;

    location ~* \.(jpg|jpeg|png|gif|ico|css|js)$ {
        expires 1y;
        add_header Cache-Control "public, immutable";
    }

---

## 常见问题

### 排障指南

| 问题 | 可能原因 | 解决方案 |
|---------|-----------------|-----------|
| 无法连接 | 防火墙、端口错误 | 检查 UFW、验证端口 |
| SSL 错误 | 证书问题 | 续期证书、检查路径 |
| 性能慢 | 资源限制、无缓存 | 监控资源、添加缓存 |
| 磁盘满 | 日志、旧备份 | 清理、扩展存储 |
| 服务无法启动 | 配置错误、端口冲突 | 检查日志、验证配置 |
| DNS 不工作 | 记录错误、传播中 | 验证 DNS、等待传播 |

### 常用命令

| 命令 | 用途 |
|---------|---------|
| `docker stats` | 容器资源使用 |
| `df -h` | 磁盘空间 |
| `free -h` | 内存使用 |
| `top` | 进程监控 |
| `journalctl -u service` | 服务日志 |
| `netstat -tlnp` | 开放端口 |
| `ss -tlnp` | 开放端口（现代） |

---

## 新自托管者清单

| 步骤 | 任务 | 状态 |
|------|------|--------|
| 1 | 选择硬件/VPS | |
| 2 | 安装操作系统 | |
| 3 | 初始服务器设置 | |
| 4 | 安装 Docker | |
| 5 | 设置反向代理 | |
| 6 | 配置 SSL | |
| 7 | 设置 DNS | |
| 8 | 部署第一个服务 | |
| 9 | 配置备份 | |
| 10 | 设置监控 | |
| 11 | 安全加固 | |
| 12 | 记录一切 | |
