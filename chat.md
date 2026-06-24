# Element Web 教程：Matrix 聊天客户端

## 简介

Element Web 是一个功能丰富的 Matrix 客户端，基于 matrix-js-sdk 库构建。Matrix 是一个开放标准，用于去中心化、持久化的通信，支持端到端加密、服务器间联合以及与外部平台的桥接。

## Matrix 协议基础

| 概念 | 说明 |
|------|------|
| Homeserver（主服务器） | 存储账户数据和房间历史 |
| Room（房间） | 用于消息和协作的共享空间 |
| Event（事件） | 房间中的任何操作（消息、反应、状态变更） |
| Federation（联合） | 主服务器之间的通信 |
| E2EE（端到端加密） | 用于私密通信的端到端加密 |
| Bridge（桥接） | 与外部聊天服务的连接 |

## 系统要求

| 组件 | 最低配置 | 推荐配置 |
|------|---------|---------|
| Synapse 内存 | 1 GB | 4 GB |
| PostgreSQL | 10 | 14+ |
| CPU | 2 核 | 4 核 |
| 磁盘 | 20 GB | 100 GB |
| Element Web | 静态托管 | Nginx 或 Apache |

## 主服务器安装（Synapse）

### Docker Compose

```yaml
version: '3.8'
services:
  synapse:
    image: matrixdotorg/synapse:latest
    restart: unless-stopped
    volumes:
      - ./synapse-data:/data
    ports:
      - "8008:8008"
    environment:
      - SYNAPSE_SERVER_NAME=example.com
      - SYNAPSE_REPORT_STATS=no

  db:
    image: postgres:15
    restart: unless-stopped
    volumes:
      - ./pg-data:/var/lib/postgresql/data
    environment:
      - POSTGRES_DB=synapse
      - POSTGRES_USER=synapse
      - POSTGRES_PASSWORD=securepassword
```

### 生成配置

```bash
docker run --rm -v ./synapse-data:/data \
  matrixdotorg/synapse:latest generate
```

## Element Web 部署

```bash
wget https://github.com/element-hq/element-web/releases/download/v1.11.60/element-v1.11.60.tar.gz
tar -xzf element-v1.11.60.tar.gz
cd element-v1.11.60
cp config.sample.json config.json
```

### 配置文件

```json
{
  "default_server_config": {
    "m.homeserver": {
      "base_url": "https://matrix.example.com",
      "server_name": "example.com"
    }
  },
  "default_theme": "dark",
  "show_labs_settings": true,
  "brand": "My Chat"
}
```

## 房间类型和功能

| 房间类型 | 访问方式 | 用途 |
|---------|---------|------|
| 公开房间 | 任何人可加入 | 开放社区讨论 |
| 私有房间 | 仅限邀请 | 团队沟通 |
| Space（空间） | 房间容器 | 组织结构 |
| 私信 | 两人对话 | 私人对话 |

### 房间设置

| 设置 | 选项 | 说明 |
|------|------|------|
| 历史可见性 | world_readable, joined, invited | 谁可以查看历史消息 |
| 加密 | 开/关 | 端到端加密开关 |
| 加入规则 | public, invite, knock | 用户如何加入房间 |
| 访客访问 | 可/不可加入 | 未注册用户访问权限 |
| 权限 | Power levels | 基于角色的控制 |

## Power Levels（权限级别）

| 级别 | 默认角色 | 功能 |
|------|---------|------|
| 0 | 用户 | 发送消息、添加反应 |
| 50 | 版主 | 踢人、封禁、删除消息 |
| 100 | 管理员 | 更改房间设置、管理权限级别 |

### 自定义 Power Level 操作

| 操作 | 默认级别 | 说明 |
|------|---------|------|
| `invite` | 0 | 邀请用户加入房间 |
| `kick` | 50 | 临时移除用户 |
| `ban` | 50 | 永久移除用户 |
| `redact` | 0 | 删除消息 |
| `state_default` | 0 | 更改房间状态事件 |
| `events_default` | 0 | 发送房间事件 |

## 端到端加密

| 功能 | 状态 | 说明 |
|------|------|------|
| 一对一消息 | 默认启用 | 使用 Olm/Megolm |
| 群组消息 | 按房间选择启用 | 需要设备验证 |
| 密钥备份 | 支持 | 将密钥加密存储在服务器 |
| 交叉签名 | 支持 | 验证所有用户设备 |
| 密钥验证 | 交互式 | Emoji 或二维码比对 |

### 设置加密

1. 在房间设置中启用加密
2. 通过 Settings > Security > Sessions 验证会话
3. 设置 Secure Backup 用于密钥恢复
4. 交叉签名其他设备以建立信任

## 桥接（Bridges）

桥接将 Matrix 连接到外部聊天平台，实现跨服务通信。

| 桥接 | 平台 | 方法 |
|------|------|------|
| mautrix-whatsapp | WhatsApp | Puppeting |
| mautrix-telegram | Telegram | Puppeting |
| mautrix-signal | Signal | Puppeting |
| mautrix-slack | Slack | Appservice |
| mx-puppet-discord | Discord | Puppeting |
| matrix-appservice-irc | IRC | Appservice |

### 桥接安装示例

```yaml
# docker-compose.yml
services:
  whatsapp-bridge:
    image: dock.mau.dev/mautrix/whatsapp:latest
    volumes:
      - ./whatsapp-data:/data
    restart: unless-stopped
```

## 通知设置

| 级别 | 说明 | 用途 |
|------|------|------|
| 所有消息 | 每条消息都通知 | 重要频道 |
| 提及和关键词 | 仅在被提及时或关键词匹配时 | 一般房间 |
| 静音 | 无通知 | 低优先级房间 |

## 小部件集成（Widgets）

小部件可将外部应用嵌入房间内进行协作。

| 小部件类型 | 示例 | 集成方式 |
|-----------|------|---------|
| 视频通话 | Jitsi, Element Call | 内置支持 |
| 文档 | Etherpad, Google Docs | URL 小部件 |
| 投票 | Element Polls | 内置功能 |
| 贴纸 | Sticker picker packs | 小部件管理器 |

## Spaces（空间）

空间将房间组织成层级结构，便于结构化导航。

| 空间类型 | 可见性 | 用途 |
|---------|--------|------|
| 公开 | 可在目录中发现 | 开放社区 |
| 私有 | 仅限邀请 | 组织团队 |
| 受限 | 基于角色的访问 | 企业部门 |

## 联合（Federation）

联合允许不同主服务器上的用户无缝通信。

| 组件 | 默认端口 | 用途 |
|------|---------|------|
| Client-Server API | 8448 / 443 | 客户端连接 |
| Server-Server API | 8448 | 联合流量 |
| Well-Known | 443 | 服务器委派 |

### 联合配置

```yaml
# homeserver.yaml
federation_domain_whitelist:
  - example.com
  - partner.org
# 留空以允许所有联合服务器
```

## 管理工具

| 工具 | 操作 | 所需 Power Level |
|------|------|-----------------|
| Kick（踢出） | 临时移除用户 | 50 |
| Ban（封禁） | 永久屏蔽用户 | 50 |
| Redact（撤回） | 删除消息 | 0（与发送者同级） |
| Mute（静音） | 设置用户权限为 -1 | 50 |
| Server ACL | 屏蔽整个服务器 | 100 |

## 性能调优

| 设置 | 位置 | 影响 |
|------|------|------|
| 缓存因子 | `caches.global_factor` | 内存与速度的权衡 |
| 事件缓存 | `caches.event_cache_size` | 查询性能 |
| Workers | 分离 worker 进程 | 水平扩展 |
| 媒体存储 | S3 兼容后端 | 可扩展的文件存储 |

## 备份与恢复

| 组件 | 方法 | 频率 |
|------|------|------|
| 数据库 | pg_dump | 每日 |
| 媒体存储 | rsync / S3 sync | 每日 |
| 签名密钥 | 手动导出 | 创建时 |
| Element 设置 | Secure Backup 功能 | 自动 |

## 总结

Element Web 提供了一个功能丰富的 Matrix 客户端，用于去中心化通信。它对端到端加密的支持、与外部平台的桥接以及服务器间联合功能，使其适合需要掌控通信基础设施的组织。
