# 使用 Uptime Kuma 进行运行监控

## 简介

Uptime Kuma 是一个自托管监控工具，用于跟踪网站、API 和服务的可用性和性能。它提供实时状态页面和通知告警。

### 什么是 Uptime Kuma？

Uptime Kuma 监控您的服务，并在服务宕机时通知您。它提供了一个简洁的仪表盘和公开状态页面。

| 特性 | 描述 |
|------|------|
| 监控 | HTTP、TCP、DNS、Docker 检查 |
| 通知 | 邮件、Slack、Discord、Telegram |
| 状态页面 | 公开或私有状态展示 |
| 多语言 | 支持多种语言 |
| 2FA | 双因素认证 |

### 与其他方案的比较

| 特性 | Uptime Kuma | UptimeRobot | Pingdom |
|------|------------|-------------|---------|
| 自托管 | 是 | 否 | 否 |
| 免费 | 是 | 免费增值 | 否 |
| 状态页面 | 是 | 是 | 是 |
| 通知 | 80+ 服务 | 邮件、短信 | 邮件、短信 |
| Docker 支持 | 是 | N/A | N/A |

## 安装

### Docker 安装

```bash
docker run -d \
  --restart=always \
  -p 3001:3001 \
  -v uptime-kuma:/app/data \
  --name uptime-kuma \
  louislam/uptime-kuma
```

### Docker Compose

```yaml
version: '3'
services:
  uptime-kuma:
    image: louislam/uptime-kuma
    container_name: uptime-kuma
    ports:
      - "3001:3001"
    volumes:
      - uptime-kuma:/app/data
    restart: unless-stopped

volumes:
  uptime-kuma:
```

### 手动安装

```bash
git clone https://github.com/louislam/uptime-kuma.git
cd uptime-kuma
npm install
npm run build
node server/server.js
```

### 系统要求

| 要求 | 最低 | 推荐 |
|------|------|------|
| CPU | 1 核 | 2 核 |
| 内存 | 256 MB | 512 MB |
| 存储 | 1 GB | 5 GB |
| Node.js | 18+ | 20+ |

## 初始设置

### 首次登录

1. 访问 http://localhost:3001
2. 创建管理员账户
3. 添加第一个监控

### 配置文件

```env
# .env
UPTIME_KUMA_PORT=3001
UPTIME_KUMA_HOST=0.0.0.0
NODE_ENV=production
```

## 监控类型

### HTTP 监控

| 设置 | 描述 |
|------|------|
| URL | 要检查的端点 |
| 方法 | GET、POST、HEAD |
| 间隔 | 检查频率 |
| 超时 | 响应超时时间 |
| 状态码 | 期望的 HTTP 码 |

### HTTP 监控配置

```yaml
Name: Website
URL: https://example.com
Method: GET
Interval: 60 seconds
Timeout: 10 seconds
Retry: 3
Accepted Status Codes: 200-299
```

### TCP 监控

| 设置 | 描述 |
|------|------|
| 主机名 | 服务器地址 |
| 端口 | 端口号 |
| 间隔 | 检查频率 |

### DNS 监控

| 设置 | 描述 |
|------|------|
| 域名 | 要解析的域名 |
| 解析器 | DNS 服务器 |
| 记录类型 | A、AAAA、CNAME、MX |

### Docker 监控

| 设置 | 描述 |
|------|------|
| Docker 主机 | Docker daemon URL |
| 容器 | 容器名称或 ID |
| 检查类型 | 运行状态 |

### 监控类型汇总

| 类型 | 用例 |
|------|------|
| HTTP | 网站、API |
| TCP | 数据库、SSH、自定义端口 |
| DNS | 域名解析 |
| Docker | 容器状态 |
| Ping | 服务器可达性 |
| Steam | 游戏服务器 |
| Push | 心跳监控 |

## 通知渠道

### 支持的服务

| 服务 | 类别 |
|------|------|
| Email (SMTP) | 邮件 |
| Slack | 团队聊天 |
| Discord | 社区 |
| Telegram | 消息 |
| Webhook | 自定义 |
| PagerDuty | 事件管理 |
| Gotify | 自托管推送 |
| Matrix | 去中心化聊天 |

### 邮件配置

```yaml
Type: SMTP
Hostname: smtp.gmail.com
Port: 465
Username: your-email@gmail.com
Password: app-password
From: your-email@gmail.com
To: recipient@example.com
Secure: SSL/TLS
```

### Slack 配置

```yaml
Type: Slack
Webhook URL: https://hooks.slack.com/services/xxx/yyy/zzz
Channel: #alerts
Username: Uptime Kuma
Icon Emoji: :warning:
```

### Discord 配置

```yaml
Type: Discord
Webhook URL: https://discord.com/api/webhooks/xxx/yyy
```

### 通知触发器

| 触发器 | 描述 |
|--------|------|
| Up | 服务恢复 |
| Down | 服务宕机 |
| Testing | 测试通知 |

## 状态页面

### 创建状态页面

1. 导航到 Status Pages
2. 点击 "Add New Status Page"
3. 配置标题和 URL
4. 添加要展示的监控

### 状态页面设置

| 设置 | 描述 |
|------|------|
| 标题 | 页面标题 |
| URL slug | 公开 URL 路径 |
| 描述 | 页面描述 |
| 主题 | 亮色或暗色 |
| 自定义 CSS | 自定义样式 |

### 公开与私有

| 类型 | 访问 |
|------|------|
| 公开 | 任何有链接的人 |
| 私有 | 需要登录 |

### 自定义域名

```nginx
server {
    listen 80;
    server_name status.example.com;

    location / {
        proxy_pass http://localhost:3001/status/mypage;
        proxy_set_header Host $host;
    }
}
```

## 事件管理

### 创建事件

1. 进入状态页面
2. 点击 "Add Incident"
3. 输入标题和内容
4. 选择受影响的监控

### 事件状态

| 状态 | 含义 |
|------|------|
| Investigating | 正在调查问题 |
| Identified | 已找到根本原因 |
| Monitoring | 已修复，观察中 |
| Resolved | 问题已解决 |

## 分组和标签

### 监控分组

将监控组织为逻辑分组：

```
Websites
├── Main Website
├── Blog
└── API

Infrastructure
├── Database Server
├── Cache Server
└── Load Balancer
```

### 标签

| 标签 | 颜色 | 用途 |
|------|------|------|
| Production | 红色 | 关键服务 |
| Staging | 黄色 | 测试环境 |
| Internal | 蓝色 | 内部工具 |
| External | 绿色 | 公开服务 |

## 数据保留和备份

### 数据保留

```env
# 保留数据 365 天
KEEP_DATA_PERIOD=365
```

### 备份方式

| 方式 | 描述 |
|------|------|
| 导出 | 从 UI 导出 JSON |
| Docker volume | 备份 Docker volume |
| 文件系统 | 复制数据目录 |

### 备份脚本

```bash
#!/bin/bash
docker exec uptime-kuma \
  node -e "const {exportData} = require('./server/export'); \
  exportData().then(data => console.log(JSON.stringify(data)))" \
  > backup.json
```

## API 访问

### API 端点

| 端点 | 方法 | 描述 |
|------|------|------|
| `/api/status/page/{slug}` | GET | 状态页面数据 |
| `/api/monitors` | GET | 列出监控 |
| `/api/monitor/{id}` | GET | 监控详情 |

### 身份验证

```bash
# 从 Settings > API 获取 API 令牌
curl -H "Authorization: Bearer YOUR_TOKEN" \
  https://status.example.com/api/monitors
```

## 反向代理设置

### Nginx 配置

```nginx
server {
    listen 80;
    server_name status.example.com;

    location / {
        proxy_pass http://localhost:3001;
        proxy_http_version 1.1;
        proxy_set_header Upgrade $http_upgrade;
        proxy_set_header Connection "upgrade";
        proxy_set_header Host $host;
        proxy_set_header X-Real-IP $remote_addr;
    }
}
```

### SSL 配置

```bash
# 安装 Certbot
sudo apt install certbot python3-certbot-nginx

# 获取 SSL 证书
sudo certbot --nginx -d status.example.com
```

## 性能调优

### 数据库优化

| 设置 | 建议 |
|------|------|
| 数据库 | SQLite（默认）或 MariaDB |
| 索引 | 监控自动索引 |
| 清理 | 定期数据修剪 |

### 资源限制

```yaml
# docker-compose.yml
services:
  uptime-kuma:
    deploy:
      resources:
        limits:
          cpus: '1.0'
          memory: 512M
```

## 故障排除

### 常见问题

| 问题 | 原因 | 解决方案 |
|------|------|----------|
| 通知未发送 | 配置错误 | 测试通知设置 |
| CPU 使用率高 | 监控过多 | 增加检查间隔 |
| WebSocket 错误 | 代理配置错误 | 配置 WebSocket 支持 |
| 数据库锁定 | 并发写入 | 生产环境使用 MariaDB |

### 日志

```bash
# 查看日志
docker logs uptime-kuma

# 跟踪日志
docker logs -f uptime-kuma
```

## 总结

| 功能 | 用途 |
|------|------|
| 监控 | 跟踪服务可用性 |
| 通知 | 宕机告警 |
| 状态页面 | 展示服务状态 |
| 分组 | 组织监控 |
| API | 编程访问 |
