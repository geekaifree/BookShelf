# 影视管理

> 本文档整合了以下源文件：sonarr.md, tv.md, indexer.md

---

## 来源：sonarr.md

## 简介

Sonarr 是一款面向 Usenet 和 BitTorrent 用户的 PVR（个人录像机）。它监控多个 RSS 源以获取您喜爱电视剧的新剧集，自动下载它们，并使用正确的命名和元数据将它们组织到媒体库中。

| 特性 | 描述 |
|---------|-------------|
| 剧集监控 | 跟踪电视剧并自动搜索新剧集 |
| 日历视图 | 显示即将播出和已播剧集的可视化日历 |
| 质量配置文件 | 定义首选质量和升级路径 |
| 自动导入 | 重命名文件并移动到有序的文件夹结构 |
| 下载管理 | 与 Torrent 和 Usenet 下载客户端集成 |

## 架构

### 系统组件

| 组件 | 角色 |
|-----------|------|
| Sonarr | 电视剧监控和管理应用 |
| 索引器 | 查找剧集发布的来源 |
| 下载客户端 | 执行实际下载的软件 |
| 媒体服务器 | Plex、Jellyfin 或 Emby 用于播放 |
| Prowlarr | 可选的集中索引管理器 |

### 工作流程

| 步骤 | 描述 |
|------|-------------|
| 1 | 用户向 Sonarr 添加电视剧 |
| 2 | Sonarr 在索引器中监控匹配的剧集发布 |
| 3 | 根据质量配置文件设置评估发布 |
| 4 | 将下载请求发送到已配置的下载客户端 |
| 5 | 下载客户端获取文件 |
| 6 | Sonarr 使用正确命名导入文件 |
| 7 | 媒体服务器检测到新文件并更新库 |

## 安装

### Docker 部署

```bash
docker run -d \
  --name=sonarr \
  -p 8989:8989 \
  -v /path/to/config:/config \
  -v /path/to/tv:/tv \
  -v /path/to/downloads:/downloads \
  -e PUID=1000 \
  -e PGID=1000 \
  -e TZ=UTC \
  --restart unless-stopped \
  lscr.io/linuxserver/sonarr:latest
```

### Docker Compose

```yaml
version: "3.8"
services:
  sonarr:
    image: lscr.io/linuxserver/sonarr:latest
    container_name: sonarr
    environment:
      - PUID=1000
      - PGID=1000
      - TZ=UTC
    volumes:
      - ./config:/config
      - /path/to/tv:/tv
      - /path/to/downloads:/downloads
    ports:
      - "8989:8989"
    restart: unless-stopped
```

## 配置

### 添加剧集

| 方式 | 描述 |
|--------|-------------|
| 搜索 | 在 Sonarr 界面中按剧名搜索 |
| 列表 | 从 Trakt、IMDb 或其他列表来源导入 |
| 手动 | 通过 TVDb ID 或 IMDb ID 添加 |

### 质量配置文件

质量配置文件定义可接受的质量级别和升级路径。

| 配置文件 | 典型用途 |
|---------|-------------|
| SD | 标清，文件体积小 |
| HD-720p | 720p 高清 |
| HD-1080p | 1080p 全高清 |
| Ultra-HD | 4K UHD 内容 |
| Any | 接受任何可用质量 |

### 质量定义

| 质量 | 分辨率 | 每集典型大小 |
|---------|-----------|-------------------------|
| SDTV | 480p | 200-500 MB |
| WEBDL-720p | 720p | 500 MB - 1.5 GB |
| HDTV-720p | 720p | 500 MB - 1.5 GB |
| WEBDL-1080p | 1080p | 1 - 3 GB |
| HDTV-1080p | 1080p | 1 - 3 GB |
| Bluray-1080p | 1080p | 2 - 6 GB |
| WEBDL-2160p | 4K | 3 - 10 GB |
| Bluray-2160p | 4K | 5 - 20 GB |

### 剧集类型

| 类型 | 描述 | 监控方式 |
|------|-------------|------------|
| 标准 | 按季播出的常规剧集 | 默认监控所有剧集 |
| 每日 | 每日播出的节目（脱口秀、新闻） | 仅监控最近剧集 |
| 动漫 | 日本动画系列 | 剧集编号方式不同 |

### 下载客户端

| 客户端 | 协议 | 配置 |
|--------|----------|---------------|
| qBittorrent | Torrent | 主机、端口、用户名、密码 |
| Transmission | Torrent | 主机、端口、用户名、密码 |
| Deluge | Torrent | 主机、端口、密码 |
| SABnzbd | Usenet | 主机、端口、API 密钥 |
| NZBGet | Usenet | 主机、端口、用户名、密码 |

## 剧集管理

### 监控选项

| 选项 | 描述 |
|--------|-------------|
| 所有剧集 | 监控每一季的每一集 |
| 未来剧集 | 仅监控尚未播出的剧集 |
| 最新一季 | 仅监控最近一季 |
| 第一季 | 仅监控第一季 |
| 缺失 | 监控尚未下载的剧集 |
| 无 | 不监控任何剧集 |

### 季管理

| 操作 | 描述 |
|--------|-------------|
| 搜索整季 | 手动搜索一季中的所有剧集 |
| 取消监控某季 | 停止监控特定季 |
| 整季包 | 搜索完整季的下载 |

## 文件管理

### 命名规范

| 标记 | 描述 | 示例 |
|-------|-------------|---------|
| {Series Title} | 剧集名称 | Breaking Bad |
| {Season} | 季号（补零） | 01 |
| {Episode} | 集号（补零） | 05 |
| {Episode Title} | 剧集标题 | Gray Matter |
| {Quality Title} | 发布质量 | Bluray-1080p |
| {MediaInfo VideoCodec} | 视频编解码器 | x264 |
| {MediaInfo AudioCodec} | 音频编解码器 | DTS |

### 推荐命名模式

| 模式 | 示例输出 |
|---------|---------------|
| `{Series Title}/Season {Season}/{Series Title} - S{Season}E{Episode} - {Episode Title}` | Breaking Bad/Season 01/Breaking Bad - S01E05 - Gray Matter.mkv |
| `{Series Title} - {Season}x{Episode} - {Episode Title}` | Breaking Bad - 1x05 - Gray Matter.mkv |

### 文件夹结构

```
/tv/
  Breaking Bad/
    Season 01/
      Breaking Bad - S01E01 - Pilot.mkv
      Breaking Bad - S01E02 - Cat's in the Bag....mkv
      Breaking Bad - S01E03 - ...And the Bag's in the River.mkv
    Season 02/
      Breaking Bad - S02E01 - Seven Thirty-Seven.mkv
  The Office (US)/
    Season 01/
      The Office (US) - S01E01 - Pilot.mkv
```

## 配置文件和偏好

### 发布配置文件

| 设置 | 描述 |
|---------|-------------|
| 首选词 | 提高发布评分的术语 |
| 禁止包含 | 拒绝发布的术语 |
| 首选语言 | 音频语言偏好 |
| 索引器标志 | 额外的索引器特定设置 |

### 语言配置文件

| 配置文件 | 接受的语言 |
|---------|-------------------|
| English | 仅英语音频 |
| Multi | 多语言音轨 |
| Any | 接受任何语言 |

## 日历和调度

### 日历视图

| 功能 | 描述 |
|---------|-------------|
| 月视图 | 查看一个月内播出的所有剧集 |
| 剧集信息 | 悬停查看剧集详情 |
| 颜色编码 | 已下载、已监控、未播出使用不同颜色 |
| 筛选器 | 按剧集、状态或监控筛选 |

### RSS 同步

| 设置 | 描述 |
|---------|-------------|
| 间隔 | 检查索引器的频率（默认：15 分钟） |
| 自动搜索 | 自动搜索缺失剧集 |
| 交互式搜索 | 带用户选择的手动搜索 |

## 通知

### 支持的服务

| 服务 | 配置 |
|---------|--------------|
| Email | SMTP 服务器设置 |
| Discord | Webhook URL |
| Telegram | Bot Token、Chat ID |
| Slack | Webhook URL |
| Pushover | 用户密钥、API Token |
| Webhook | 自定义 HTTP 端点 |

### 通知触发器

| 触发器 | 描述 |
|---------|-------------|
| 下载时 | 剧集成功下载时 |
| 升级时 | 剧集升级到更好质量时 |
| 重命名时 | 剧集文件被重命名时 |
| 添加剧集时 | 添加新剧集时 |
| 健康问题时 | 健康检查失败时 |

## API 访问

### 关键端点

| 端点 | 方法 | 描述 |
|----------|--------|-------------|
| `/api/v3/series` | GET | 列出所有剧集 |
| `/api/v3/series/{id}` | GET | 获取特定剧集 |
| `/api/v3/episode` | GET | 列出剧集 |
| `/api/v3/calendar` | GET | 获取即将播出的剧集 |
| `/api/v3/command` | POST | 触发命令 |
| `/api/v3/history` | GET | 获取下载历史 |

### API 认证

```bash
# 使用 API 密钥
curl -H "X-Api-Key: your_api_key" http://localhost:8989/api/v3/series
```

## 健康监控

### 健康检查

| 检查项 | 描述 |
|-------|-------------|
| 下载客户端 | 验证下载客户端连接性 |
| 索引器 | 检查索引器是否可访问 |
| 磁盘空间 | 监控可用存储空间 |
| 根文件夹 | 验证已配置的电视剧目录 |
| 数据库 | 检查数据库完整性 |

## 故障排除

### 常见问题

| 问题 | 原因 | 解决方案 |
|-------|-------|----------|
| 剧集未下载 | 未配置索引器 | 添加索引器或连接 Prowlarr |
| 导入了错误文件 | 命名模式不匹配 | 检查命名配置 |
| 下载卡住 | 下载客户端问题 | 验证下载客户端设置 |
| 元数据缺失 | TVDb API 问题 | 检查 API 访问和网络 |
| 未找到剧集 | 标题不匹配 | 改用 TVDb ID 搜索 |

## 总结

| 主题 | 核心要点 |
|-------|-------------|
| 用途 | 自动化电视剧收藏管理 |
| 设置 | 带电视剧和下载卷映射的 Docker 部署 |
| 质量 | 配置文件控制可接受和首选质量级别 |
| 监控 | 日历视图查看即将播出剧集和基于 RSS 的监控 |
| 组织 | 使用季/集结构自动重命名 |
| 集成 | 与 Prowlarr、Plex、Jellyfin 和下载客户端配合使用 |


---

## 来源：tv.md

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


---

## 来源：indexer.md

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


---
