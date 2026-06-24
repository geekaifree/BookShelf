# 使用 Mattermost 进行团队消息

## 简介

Mattermost 是一个开源、自托管的团队消息平台。它为组织提供安全通信，功能类似于 Slack 和 Microsoft Teams。

### 什么是 Mattermost？

Mattermost 是一个工作场所消息解决方案，提供频道、私信、文件共享和集成功能，同时将数据控制权掌握在自己手中。

| 特性 | 描述 |
|------|------|
| 频道 | 有组织的团队对话 |
| 私信 | 私人对话 |
| 文件共享 | 分享文档和图片 |
| 集成 | 与其他工具连接 |
| 搜索 | 全文消息搜索 |

### 与其他方案的比较

| 特性 | Mattermost | Slack | Teams |
|------|-----------|-------|-------|
| 自托管 | 是 | 否 | 否 |
| 开源 | 是 | 否 | 否 |
| 免费层级 | 是 | 有限 | 有限 |
| 数据控制 | 完全 | 有限 | 有限 |
| 合规 | HIPAA、SOC2 | SOC2 | SOC2 |

## 安装

### 系统要求

| 组件 | 最低 | 推荐 |
|------|------|------|
| CPU | 1 核 | 2+ 核 |
| 内存 | 2 GB | 4+ GB |
| 存储 | 10 GB | 50+ GB |
| 数据库 | PostgreSQL 11+ | PostgreSQL 13+ |

### Docker 安装

```yaml
version: '3'
services:
  mattermost:
    image: mattermost/mattermost-team-edition
    ports:
      - "8065:8065"
    volumes:
      - ./mattermost/config:/mattermost/config
      - ./mattermost/data:/mattermost/data
      - ./mattermost/logs:/mattermost/logs
    environment:
      - MM_SQLSETTINGS_DRIVERNAME=postgres
      - MM_SQLSETTINGS_DATASOURCE=mmuser:password@db:5432/mattermost?sslmode=disable&connect_timeout=10
    depends_on:
      - db

  db:
    image: postgres:13
    environment:
      - POSTGRES_USER=mmuser
      - POSTGRES_PASSWORD=password
      - POSTGRES_DB=mattermost
    volumes:
      - postgres_data:/var/lib/postgresql/data

volumes:
  postgres_data:
```

### 手动安装

```bash
# 下载 Mattermost
wget https://releases.mattermost.com/9.0.0/mattermost-9.0.0-linux-amd64.tar.gz
tar -xzf mattermost-9.0.0-linux-amd64.tar.gz

# 创建用户和目录
sudo useradd -r -U mattermost
sudo mv mattermost /opt/
sudo chown -R mattermost:mattermost /opt/mattermost

# 配置数据库
sudo -u postgres createuser -P mmuser
sudo -u postgres createdb -O mmuser mattermost
```

## 配置

### 基本配置

```json
{
  "ServiceSettings": {
    "SiteURL": "https://mattermost.example.com",
    "ListenAddress": ":8065",
    "EnableSecurityFixAlert": true
  },
  "SqlSettings": {
    "DriverName": "postgres",
    "DataSource": "mmuser:password@localhost:5432/mattermost?sslmode=disable"
  },
  "FileSettings": {
    "Directory": "/opt/mattermost/data/",
    "MaxFileSize": 104857600
  }
}
```

### 环境变量

```env
MM_SQLSETTINGS_DRIVERNAME=postgres
MM_SQLSETTINGS_DATASOURCE=mmuser:password@localhost:5432/mattermost
MM_SERVICESETTINGS_SITEURL=https://mattermost.example.com
```

### 系统控制台设置

| 类别 | 设置 |
|------|------|
| 常规 | 站点名称、描述 |
| 认证 | 登录方式、安全 |
| 通知 | 邮件、推送通知 |
| 集成 | Webhook、Bot |
| 合规 | 数据保留、导出 |

## 频道

### 频道类型

| 类型 | 描述 | 可见性 |
|------|------|--------|
| Public | 对所有团队成员开放 | 所有人可见 |
| Private | 仅邀请频道 | 非成员不可见 |
| Direct | 一对一对话 | 私密 |
| Group | 小组对话 | 私密 |

### 频道管理

| 操作 | 描述 |
|------|------|
| 创建 | 创建新频道 |
| 归档 | 停用频道 |
| 静音 | 停止通知 |
| 收藏 | 固定到侧边栏 |
| 标记已读 | 清除未读状态 |

### 频道设置

| 设置 | 描述 |
|------|------|
| 头部 | 频道主题/描述 |
| 用途 | 频道用途 |
| 权限 | 谁可以发帖、管理 |
| 通知 | 通知偏好 |

## 消息

### 消息格式

| 语法 | 结果 |
|------|------|
| `**bold**` | **bold** |
| `*italic*` | *italic* |
| `~~strike~~` | ~~strike~~ |
| `` `code` `` | `code` |
| ```code block``` | 代码块 |

### 消息功能

| 功能 | 描述 |
|------|------|
| @mentions | 通知特定用户 |
| @channel | 通知所有频道成员 |
| @here | 通知在线成员 |
| Emoji | 反应表情 |
| 线程 | 线程回复 |
| 置顶 | 置顶重要消息 |

### 命令

| 命令 | 描述 |
|------|------|
| `/away` | 设置状态为离开 |
| `/online` | 设置状态为在线 |
| `/dnd` | 请勿打扰 |
| `/code` | 格式化为代码 |
| `/help` | 显示帮助 |

## 用户管理

### 用户角色

| 角色 | 权限 |
|------|------|
| System Admin | 完全系统访问 |
| Team Admin | 管理团队设置 |
| Channel Admin | 管理频道设置 |
| Member | 基本消息 |
| Guest | 有限访问 |

### 团队管理

| 操作 | 描述 |
|------|------|
| 创建团队 | 新团队工作区 |
| 邀请用户 | 发送邀请 |
| 管理成员 | 添加/移除用户 |
| 团队设置 | 配置团队 |

### 用户设置

| 设置 | 描述 |
|------|------|
| 个人资料 | 姓名、头像、状态 |
| 通知 | 邮件、推送、桌面 |
| 显示 | 主题、语言 |
| 安全 | 密码、2FA |
| 高级 | 性能设置 |

## 集成

### Webhook

#### 传入 Webhook

```json
POST /hooks/webhook-id
{
  "text": "Build completed successfully",
  "username": "CI/CD",
  "icon_emoji": ":rocket:"
}
```

#### 传出 Webhook

```json
{
  "trigger_words": ["build", "deploy"],
  "url": "https://ci.example.com/webhook",
  "channel": "dev-ops"
}
```

### Bot 账户

| 功能 | 描述 |
|------|------|
| API 令牌 | 编程访问 |
| 自定义帖子 | 富消息格式 |
| 集成 | 连接外部服务 |

### 斜杠命令

```json
{
  "trigger": "/deploy",
  "url": "https://deploy.example.com/command",
  "method": "POST"
}
```

### 热门集成

| 集成 | 用途 |
|------|------|
| GitHub | 代码通知 |
| Jira | 问题跟踪 |
| Jenkins | CI/CD 通知 |
| GitLab | 代码管理 |
| Zapier | 工作流自动化 |

## API 访问

### REST API

| 端点 | 方法 | 描述 |
|------|------|------|
| `/api/v4/users` | GET | 列出用户 |
| `/api/v4/channels` | GET | 列出频道 |
| `/api/v4/posts` | GET | 列出帖子 |
| `/api/v4/posts` | POST | 创建帖子 |

### 身份验证

```bash
# 登录并获取令牌
curl -X POST https://mattermost.example.com/api/v4/users/login \
  -d '{"login_id":"user","password":"pass"}' \
  -H "Content-Type: application/json"
```

### WebSocket API

```javascript
const ws = new WebSocket('wss://mattermost.example.com/api/v4/websocket');
ws.onmessage = function(event) {
  const data = JSON.parse(event.data);
  console.log(data);
};
```

## 安全

### 认证方式

| 方式 | 描述 |
|------|------|
| 邮箱/密码 | 基本认证 |
| LDAP/AD | 目录集成 |
| SAML | 单点登录 |
| OAuth 2.0 | 外部提供者 |
| MFA | 双因素认证 |

### 安全设置

| 设置 | 描述 |
|------|------|
| 密码策略 | 最低要求 |
| 会话管理 | 超时、限制 |
| IP 过滤 | 允许/拒绝 IP |
| 加密 | TLS、静态加密 |

### 合规

| 功能 | 描述 |
|------|------|
| 数据保留 | 自动删除消息 |
| 合规导出 | 用于审计的导出 |
| 审计日志 | 跟踪用户操作 |
| eDiscovery | 搜索和导出 |

## 高可用性

### 集群配置

```json
{
  "ClusterSettings": {
    "Enable": true,
    "ClusterName": "production",
    "InterNodeListenAddress": ":8075",
    "InterNodeUrls": ["http://node1:8075", "http://node2:8075"]
  }
}
```

### 负载均衡

| 组件 | 策略 |
|------|------|
| 应用 | 轮询 |
| 数据库 | 主从 |
| 文件存储 | 共享存储 |
| 会话 | 会话粘性 |

## 备份和恢复

### 备份方式

| 方式 | 描述 |
|------|------|
| 数据库导出 | PostgreSQL 备份 |
| 文件备份 | 数据目录备份 |
| 配置备份 | 配置文件 |

### 备份脚本

```bash
#!/bin/bash
# 数据库备份
pg_dump -U mmuser mattermost > backup_$(date +%Y%m%d).sql

# 文件备份
tar -czf mattermost_files_$(date +%Y%m%d).tar.gz /opt/mattermost/data/
```

## 监控

### 指标

| 指标 | 描述 |
|------|------|
| 活跃用户 | 当前连接数 |
| 每日帖子 | 消息量 |
| 频道数量 | 频道数 |
| 文件存储 | 存储使用 |

### 健康检查

```bash
curl https://mattermost.example.com/api/v4/system/ping
```

## 总结

| 功能 | 用途 |
|------|------|
| 频道 | 有组织的对话 |
| 集成 | 连接外部工具 |
| API | 编程访问 |
| 安全 | 企业级安全 |
| 自托管 | 完全数据控制 |
