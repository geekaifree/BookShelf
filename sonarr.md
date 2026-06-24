# Sonarr 剧集管理教程

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
