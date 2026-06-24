# Radarr 电影收藏管理教程

## 简介

Radarr 是一款面向 Usenet 和 BitTorrent 用户的电影收藏管理器。它监控多个 RSS 源以获取新电影，并自动下载、排序和重命名。它与下载客户端和媒体服务器集成，实现完整的自动化流程。

| 特性 | 描述 |
|---------|-------------|
| 电影监控 | 跟踪想要的电影并自动搜索 |
| 质量配置文件 | 定义首选质量和升级路径 |
| 下载管理 | 与 Torrent 和 Usenet 下载客户端集成 |
| 库管理 | 使用一致的命名规范组织文件 |
| 通知 | 通过 Email、Discord、Telegram 等发送告警 |

## 架构

### 系统组件

| 组件 | 角色 |
|-----------|------|
| Radarr | 电影监控和管理应用 |
| 索引器 | 查找电影发布的来源（Torrent 站点、Usenet） |
| 下载客户端 | 执行实际下载的软件 |
| 媒体服务器 | Plex、Jellyfin 或 Emby 用于播放 |
| Prowlarr | 可选的集中索引管理器 |

### 工作流程

| 步骤 | 描述 |
|------|-------------|
| 1 | 用户将电影添加到 Radarr 的待下载列表 |
| 2 | Radarr 在已配置的索引器中搜索可用发布 |
| 3 | 根据质量配置文件设置评估发布 |
| 4 | 将下载请求发送到已配置的下载客户端 |
| 5 | 下载客户端获取文件 |
| 6 | Radarr 使用正确命名导入文件 |
| 7 | 媒体服务器检测到新文件并更新库 |

## 安装

### Docker 部署

```bash
docker run -d \
  --name=radarr \
  -p 7878:7878 \
  -v /path/to/config:/config \
  -v /path/to/movies:/movies \
  -v /path/to/downloads:/downloads \
  -e PUID=1000 \
  -e PGID=1000 \
  -e TZ=UTC \
  --restart unless-stopped \
  lscr.io/linuxserver/radarr:latest
```

### Docker Compose

```yaml
version: "3.8"
services:
  radarr:
    image: lscr.io/linuxserver/radarr:latest
    container_name: radarr
    environment:
      - PUID=1000
      - PGID=1000
      - TZ=UTC
    volumes:
      - ./config:/config
      - /path/to/movies:/movies
      - /path/to/downloads:/downloads
    ports:
      - "7878:7878"
    restart: unless-stopped
```

## 配置

### 添加电影

| 方式 | 描述 |
|--------|-------------|
| 搜索 | 在 Radarr 界面中按标题搜索 |
| 列表 | 从 IMDb、TMDb、Trakt 或 Letterboxd 导入 |
| 手动 | 通过 TMDb ID 或 IMDb ID 添加电影 |

### 质量配置文件

质量配置文件定义可接受的质量级别和升级时机。

| 配置文件 | 典型用途 |
|---------|-------------|
| SD | 标清，文件体积小 |
| HD-720p | 720p 高清 |
| HD-1020p | 1080p 全高清 |
| Ultra-HD | 4K UHD 内容 |
| Any | 接受任何可用质量 |

### 质量定义

| 质量 | 分辨率 | 典型大小 |
|---------|-----------|--------------|
| SDTV | 480p | 700 MB - 1.5 GB |
| WEBDL-720p | 720p | 1 - 3 GB |
| Bluray-720p | 720p | 2 - 6 GB |
| WEBDL-1080p | 1080p | 2 - 6 GB |
| Bluray-1080p | 1080p | 4 - 12 GB |
| WEBDL-2160p | 4K | 6 - 20 GB |
| Bluray-2160p | 4K | 10 - 40 GB |

### 下载客户端

| 客户端 | 协议 | 配置 |
|--------|----------|---------------|
| qBittorrent | Torrent | 主机、端口、用户名、密码 |
| Transmission | Torrent | 主机、端口、用户名、密码 |
| Deluge | Torrent | 主机、端口、密码 |
| SABnzbd | Usenet | 主机、端口、API 密钥 |
| NZBGet | Usenet | 主机、端口、用户名、密码 |

## 索引器配置

### 支持的索引器类型

| 类型 | 描述 | 要求 |
|------|-------------|-------------|
| 公开 Torrent | 免费 Torrent 追踪器 | 仅需 URL |
| 私有 Torrent | 仅限邀请的追踪器 | URL、凭证或 API 密钥 |
| Usenet | 新闻组索引器 | URL、API 密钥 |

### 索引器设置

| 设置 | 描述 |
|---------|-------------|
| RSS 同步间隔 | 检查新发布的频率 |
| 优先级 | 索引器的搜索顺序 |
| 整季搜索 | 启用搜索完整电影包 |
| 最低做种人数 | 过滤掉做种人数太少的发布 |

## 文件管理

### 命名规范

Radarr 根据可配置的模式重命名文件。

| 标记 | 描述 | 示例 |
|-------|-------------|---------|
| {Movie Title} | 原始电影标题 | The Matrix |
| {Release Year} | 发行年份 | 1999 |
| {Quality Title} | 发布质量 | Bluray-1080p |
| {Edition} | 特别版信息 | Extended |
| {MediaInfo VideoCodec} | 视频编解码器 | x264 |
| {MediaInfo AudioCodec} | 音频编解码器 | DTS |

### 推荐命名模式

| 模式 | 示例输出 |
|---------|---------------|
| `{Movie Title} ({Release Year})` | The Matrix (1999).mkv |
| `{Movie Title} ({Release Year}) {Quality Title}` | The Matrix (1999) Bluray-1080p.mkv |
| `{Movie Title} ({Release Year}) {Edition} {Quality Title}` | The Matrix (1999) Extended Bluray-1080p.mkv |

### 文件夹结构

```
/movies/
  The Matrix (1999)/
    The Matrix (1999) Bluray-1080p.mkv
    The Matrix (1999) Bluray-1080p.srt
  Inception (2010)/
    Inception (2010) WEBDL-2160p.mkv
```

## 列表集成

### 支持的列表

| 列表来源 | 描述 |
|------------|-------------|
| IMDb 列表 | 从 IMDb 观看列表或自定义列表导入 |
| TMDb 合集 | 从 The Movie Database 导入合集 |
| Trakt 列表 | 从 Trakt 观看列表或自定义列表导入 |
| Letterboxd | 从 Letterboxd 观看列表导入 |
| StevenLu | 用于发现的热门电影列表 |
| 自定义 | 从 RSS 源或 JSON 端点导入 |

### 列表设置

| 设置 | 描述 |
|---------|-------------|
| 自动添加 | 自动将列表电影添加到收藏 |
| 监控 | 是否监控已添加电影的下载 |
| 添加时搜索 | 添加电影时立即搜索 |
| 质量配置文件 | 分配给列表电影的配置文件 |
| 根文件夹 | 存储下载电影的位置 |

## 通知

### 支持的通知服务

| 服务 | 配置 |
|---------|--------------|
| Email | SMTP 服务器、端口、凭证 |
| Discord | Webhook URL |
| Telegram | Bot Token、Chat ID |
| Slack | Webhook URL |
| Pushover | 用户密钥、API Token |
| Webhook | 带 POST 数据的自定义 URL |

### 通知触发器

| 触发器 | 描述 |
|---------|-------------|
| 下载时 | 电影成功下载时 |
| 升级时 | 电影升级到更好质量时 |
| 重命名时 | 电影文件被重命名时 |
| 导入时 | 电影导入到库中时 |
| 健康问题时 | 健康检查失败时 |

## API 访问

### API 端点

| 端点 | 方法 | 描述 |
|----------|--------|-------------|
| `/api/v3/movie` | GET | 列出所有电影 |
| `/api/v3/movie/{id}` | GET | 获取特定电影 |
| `/api/v3/movie` | POST | 添加新电影 |
| `/api/v3/command` | POST | 触发命令 |
| `/api/v3/calendar` | GET | 获取即将发布的电影 |

### API 认证

```
# 在请求头中使用 API 密钥
curl -H "X-Api-Key: your_api_key" http://localhost:7878/api/v3/movie

# 使用 API 密钥作为查询参数
curl "http://localhost:7878/api/v3/movie?apikey=your_api_key"
```

## 健康监控

### 健康检查

| 检查项 | 描述 |
|-------|-------------|
| 下载客户端 | 验证下载客户端连接性 |
| 索引器 | 检查索引器是否可访问 |
| 磁盘空间 | 监控可用存储空间 |
| 根文件夹 | 验证已配置的电影目录 |
| 数据库 | 检查数据库完整性 |

## 故障排除

### 常见问题

| 问题 | 原因 | 解决方案 |
|-------|-------|----------|
| 电影未下载 | 未配置索引器 | 添加索引器或连接 Prowlarr |
| 导入了错误文件 | 命名模式不匹配 | 检查命名配置 |
| 下载卡住 | 下载客户端问题 | 验证下载客户端设置 |
| 海报缺失 | TMDb API 问题 | 检查 API 密钥和网络连接 |

## 总结

| 主题 | 核心要点 |
|-------|-------------|
| 用途 | 自动化电影收藏管理 |
| 设置 | 带卷映射的 Docker 部署 |
| 质量 | 配置文件控制可接受和首选质量 |
| 下载 | 与 Torrent 和 Usenet 客户端集成 |
| 组织 | 自动重命名和文件夹结构化 |
| 集成 | 与 Prowlarr、Plex、Jellyfin 等配合使用 |
