# Prowlarr 索引管理器教程

## 简介

Prowlarr 是一款索引管理器和代理，可与各种 PVR（个人录像机）应用集成。它管理 Torrent 和 Usenet 索引器，为跨多个应用配置搜索源提供集中化界面。

| 特性 | 描述 |
|---------|-------------|
| 索引器管理 | 所有索引器的集中配置 |
| 应用同步 | 自动将索引器同步到已连接的应用 |
| Torrent 支持 | 管理公开和私有 Torrent 追踪器 |
| Usenet 支持 | 配置 Usenet 索引器和新闻组 |
| 代理模式 | 充当应用和索引器之间的代理 |

## 架构

### Prowlarr 的定位

| 组件 | 角色 |
|-----------|------|
| Prowlarr | 中央索引管理和代理 |
| Radarr | 电影收藏管理器，从 Prowlarr 接收索引器 |
| Sonarr | 剧集管理器，从 Prowlarr 接收索引器 |
| Lidarr | 音乐收藏管理器，从 Prowlarr 接收索引器 |
| Readarr | 书籍收藏管理器，从 Prowlarr 接收索引器 |
| 下载客户端 | 实际的下载软件（qBittorrent、SABnzbd 等） |

### 数据流

| 步骤 | 描述 |
|------|-------------|
| 1 | 用户在 Prowlarr 中配置索引器 |
| 2 | Prowlarr 将索引器配置同步到已连接的应用 |
| 3 | 应用使用同步的索引器搜索内容 |
| 4 | Prowlarr 将搜索请求代理到索引器 |
| 5 | 结果返回给请求的应用 |
| 6 | 应用将下载请求发送给下载客户端 |

## 安装

### Docker 部署

```bash
docker run -d \
  --name=prowlarr \
  -p 9696:9696 \
  -v /path/to/config:/config \
  -e PUID=1000 \
  -e PGID=1000 \
  -e TZ=UTC \
  --restart unless-stopped \
  lscr.io/linuxserver/prowlarr:latest
```

### Docker Compose

```yaml
version: "3.8"
services:
  prowlarr:
    image: lscr.io/linuxserver/prowlarr:latest
    container_name: prowlarr
    environment:
      - PUID=1000
      - PGID=1000
      - TZ=UTC
    volumes:
      - ./config:/config
    ports:
      - "9696:9696"
    restart: unless-stopped

  radarr:
    image: lscr.io/linuxserver/radarr:latest
    container_name: radarr
    environment:
      - PUID=1000
      - PGID=1000
      - TZ=UTC
    volumes:
      - ./radarr-config:/config
      - /path/to/movies:/movies
      - /path/to/downloads:/downloads
    ports:
      - "7878:7878"
    restart: unless-stopped

  sonarr:
    image: lscr.io/linuxserver/sonarr:latest
    container_name: sonarr
    environment:
      - PUID=1000
      - PGID=1000
      - TZ=UTC
    volumes:
      - ./sonarr-config:/config
      - /path/to/tv:/tv
      - /path/to/downloads:/downloads
    ports:
      - "8989:8989"
    restart: unless-stopped

  qbittorrent:
    image: lscr.io/linuxserver/qbittorrent:latest
    container_name: qbittorrent
    environment:
      - PUID=1000
      - PGID=1000
      - TZ=UTC
      - WEBUI_PORT=8080
    volumes:
      - ./qbittorrent-config:/config
      - /path/to/downloads:/downloads
    ports:
      - "8080:8080"
      - "6881:6881"
      - "6881:6881/udp"
    restart: unless-stopped
```

## 配置

### 添加索引器

| 索引器类型 | 配置字段 |
|-------------|---------------------|
| 公开 Torrent | 名称、URL、分类 |
| 私有 Torrent | 名称、URL、API 密钥、用户名/密码、分类 |
| Usenet | 名称、URL、API 密钥、分类 |

### 索引器分类

| 分类 ID | 描述 |
|------------|-------------|
| 2000 | 电影 |
| 3000 | 电视剧 |
| 4000 | PC/游戏 |
| 5000 | 音乐 |
| 6000 | 书籍 |
| 7000 | 其他 |

### 热门索引器

| 名称 | 类型 | 备注 |
|------|------|-------|
| 1337x | 公开 Torrent | 综合内容 |
| RARBG mirror | 公开 Torrent | 电影和电视剧 |
| Nyaa | 公开 Torrent | 动漫内容 |
| IPTorrents | 私有 Torrent | 需要邀请 |
| TorrentLeech | 私有 Torrent | 高质量发布 |
| NZBgeek | Usenet | NZB 索引器 |

## 应用同步

### 连接应用

| 应用 | API 密钥位置 | 同步方式 |
|------------|-----------------|-------------|
| Radarr | 设置 > 常规 | 通过 Prowlarr 自动同步 |
| Sonarr | 设置 > 常规 | 通过 Prowlarr 自动同步 |
| Lidarr | 设置 > 常规 | 通过 Prowlarr 自动同步 |
| Readarr | 设置 > 常规 | 通过 Prowlarr 自动同步 |

### 同步配置

| 设置 | 描述 |
|---------|-------------|
| 同步级别 | 完全同步、仅添加或禁用 |
| 同步分类 | 共享哪些索引器分类 |
| 应用 URL | 已连接应用的地址 |
| API 密钥 | 已连接应用的认证密钥 |

## 高级功能

### 索引器代理

| 代理类型 | 使用场景 |
|-----------|----------|
| HTTP 代理 | 通过 HTTP 代理路由索引器请求 |
| SOCKS 代理 | 通过 SOCKS5 代理路由以保护隐私 |
| FlareSolverr | 自动解决 Cloudflare 验证 |

### 通知

| 通知类型 | 描述 |
|------------------|-------------|
| Email | 通过 SMTP 发送告警 |
| Discord | 通过 Webhook 发送通知到 Discord 频道 |
| Telegram | 通过 Bot 发送通知到 Telegram |
| Slack | 通过 Webhook 发送通知到 Slack |
| Webhook | 自定义 HTTP POST 通知 |

### 健康检查

| 检查项 | 描述 |
|-------|-------------|
| 索引器可用性 | 测试索引器是否响应 |
| API 功能 | 验证搜索 API 是否正常工作 |
| SSL 证书 | 检查索引器的有效 SSL |
| DNS 解析 | 确认索引器主机名可解析 |

## 故障排除

### 常见问题

| 问题 | 原因 | 解决方案 |
|-------|-------|----------|
| 索引器未同步 | 应用 URL 不正确 | 验证应用可从 Prowlarr 访问 |
| 搜索无结果 | 分类不匹配 | 检查索引器和应用之间的分类映射 |
| 认证失败 | API 密钥或凭证错误 | 重新验证索引器登录详情 |
| 速率限制 | 向索引器发送过多请求 | 在索引器设置中增加查询延迟 |

### 日志

| 日志级别 | 信息 |
|-----------|-------------|
| Info | 正常运行消息 |
| Debug | 详细诊断信息 |
| Trace | 用于故障排除的非常详细的输出 |
| Warn | 可能需要关注的潜在问题 |
| Error | 需要立即处理的故障 |

## 索引器设置

### 全局设置

| 设置 | 默认值 | 描述 |
|---------|---------|-------------|
| 查询延迟 | 0 秒 | 向索引器发送请求之间的延迟 |
| 最大重试次数 | 3 | 失败时的重试次数 |
| User Agent | 默认 | 请求的 HTTP User Agent 字符串 |
| 代理 | 无 | 全局代理配置 |

### 单个索引器设置

| 设置 | 描述 |
|---------|-------------|
| 优先级 | 优先级较高的索引器先被搜索 |
| 做种比率 | Torrent 结果的最低做种比率 |
| 做种时间 | 最低做种时间（分钟） |
| 整季包 | 包含整季包搜索 |

## 总结

| 主题 | 核心要点 |
|-------|-------------|
| 用途 | PVR 应用的集中索引管理 |
| 设置 | 基于 Docker 的部署，与媒体管理应用并行 |
| 索引器 | 支持公开/私有 Torrent 和 Usenet 索引器 |
| 同步 | 与 Radarr、Sonarr 等自动共享索引器 |
| 代理 | 支持 FlareSolverr 处理 Cloudflare 保护的索引器 |
| 监控 | 健康检查和日志用于故障排除 |
