# Lidarr：自动化音乐收藏管理器

## 简介

Lidarr 是一个面向 Usenet 和 BitTorrent 用户的音乐收藏管理器。它监控多个 RSS 源，获取喜爱艺术家的新音乐，并自动下载、排序和重命名。

| 属性 | 详情 |
|----------|--------|
| 仓库 | Lidarr/Lidarr |
| 许可证 | GPL-3.0 |
| 语言 | C#, .NET |
| 平台 | Windows, macOS, Linux |
| 数据库 | SQLite |

## Lidarr 工作原理

Lidarr 自动化音乐获取工作流程。

| 步骤 | 描述 |
|------|-------------|
| 1 | 将艺术家添加到您的库 |
| 2 | Lidarr 监控新发行 |
| 3 | 在索引器中搜索匹配文件 |
| 4 | 发送到下载客户端 |
| 5 | 导入并重命名下载的文件 |
| 6 | 更新库数据库 |

## 使用 Docker 安装

### Docker Compose 配置

```yaml
version: "3.8"

services:
  lidarr:
    image: lscr.io/linuxserver/lidarr:latest
    ports:
      - "8686:8686"
    environment:
      PUID: 1000
      PGID: 1000
      TZ: America/New_York
    volumes:
      - ./config:/config
      - /path/to/music:/music
      - /path/to/downloads:/downloads
    restart: unless-stopped

  prowlarr:
    image: lscr.io/linuxserver/prowlarr:latest
    ports:
      - "9696:9696"
    environment:
      PUID: 1000
      PGID: 1000
      TZ: America/New_York
    volumes:
      - ./prowlarr_config:/config
    restart: unless-stopped

  transmission:
    image: lscr.io/linuxserver/transmission:latest
    ports:
      - "9091:9091"
      - "51413:51413"
    environment:
      PUID: 1000
      PGID: 1000
      TZ: America/New_York
    volumes:
      - ./transmission_config:/config
      - /path/to/downloads:/downloads
    restart: unless-stopped
```

### 初始设置

1. 访问 `http://localhost:8686`。
2. 添加下载客户端（Transmission, qBittorrent, SABnzbd）。
3. 添加索引器（通过 Prowlarr 或手动）。
4. 设置音乐存储的根文件夹。
5. 将艺术家添加到您的库。

## 添加艺术家

### 搜索和添加

1. 点击 "Add Artist"。
2. 搜索艺术家名称。
3. 从结果中选择正确的艺术家。
4. 选择根文件夹。
5. 设置监控选项。
6. 点击 "Add"。

### 艺术家配置

| 字段 | 描述 |
|-------|-------------|
| Name（名称） | 艺术家名称 |
| MusicBrainz ID | 唯一标识符 |
| Path（路径） | 本地存储路径 |
| Quality Profile（质量配置） | 期望的音频质量 |
| Metadata Profile（元数据配置） | 获取哪些元数据 |
| Monitor（监控） | 跟踪哪些发行 |

## 质量配置

质量配置定义可接受的音频质量和升级偏好。

| 设置 | 描述 |
|---------|-------------|
| Name（名称） | 配置名称 |
| Upgrades Allowed（允许升级） | 是否升级现有文件 |
| Cutoff（截止） | 停止升级的质量级别 |
| Qualities（质量） | 可接受质量的有序列表 |

### 质量定义

| 质量 | 描述 |
|---------|-------------|
| FLAC | 无损音频 |
| ALAC | Apple 无损 |
| MP3 320 | 高质量有损 |
| MP3 V0 | 可变比特率有损 |
| AAC 256 | 高质量 AAC |
| OGG V0 | 可变比特率 OGG |

## 下载客户端

| 客户端 | 协议 |
|--------|----------|
| Transmission | BitTorrent |
| qBittorrent | BitTorrent |
| Deluge | BitTorrent |
| rTorrent | BitTorrent |
| SABnzbd | Usenet |
| NZBGet | Usenet |

### 客户端配置

| 字段 | 描述 |
|-------|-------------|
| Host（主机） | 下载客户端主机名或 IP |
| Port（端口） | 客户端的 API 端口 |
| Username（用户名） | 认证用户名 |
| Password（密码） | 认证密码 |
| Category（类别） | Lidarr 下载的标签 |

## 索引器

索引器是 Lidarr 查询音乐的搜索提供者。

| 索引器类型 | 示例 |
|--------------|----------|
| Usenet | NZBIndex, NZBgeek, Drunkenslug |
| Torrent | 1337x, RARBG, The Pirate Bay |

### 使用 Prowlarr

Prowlarr 是一个伴随应用程序，为所有 *arr 应用管理索引器。

| 步骤 | 描述 |
|------|-------------|
| 1 | 安装 Prowlarr |
| 2 | 在 Prowlarr 中添加索引器 |
| 3 | 将 Lidarr 连接到 Prowlarr |
| 4 | 索引器自动同步 |

## 文件管理

### 命名规范

Lidarr 根据可配置的模式重命名文件。

| 标记 | 描述 |
|-------|-------------|
| {Artist Name} | 艺术家名称 |
| {Album Title} | 专辑标题 |
| {Release Year} | 发行年份 |
| {Track Number} | 曲目编号 |
| {Track Title} | 曲目标题 |
| {Quality} | 音频质量 |

### 示例模式

```
{Artist Name}/{Album Title} ({Release Year})/{track:00} - {Track Title}
```

### 文件夹结构

```
Music/
  Artist Name/
    Album Title (2023)/
      01 - Track One.flac
      02 - Track Two.flac
      cover.jpg
```

## 元数据管理

| 元数据 | 描述 |
|----------|-------------|
| Tags（标签） | 写入文件的 ID3/Vorbis 标签 |
| Album Art（专辑封面） | 嵌入和保存封面图片 |
| Lyrics（歌词） | 获取和嵌入歌词 |
| Release Info（发行信息） | 发行组、国家、厂牌 |

## 监控和通知

| 功能 | 描述 |
|---------|-------------|
| Calendar（日历） | 查看即将发行 |
| Activity（活动） | 监控进行中的下载 |
| History（历史） | 查看过去的下载活动 |
| Wanted（缺失） | 列出缺失的专辑 |
| Queue（队列） | 当前下载队列 |

### 通知服务

| 服务 | 描述 |
|---------|-------------|
| Email（邮件） | 发送邮件通知 |
| Discord | 发布到 Discord webhook |
| Slack | 发布到 Slack 频道 |
| Telegram | 发送 Telegram 消息 |
| Pushover | 推送通知 |
| Webhook | 自定义 HTTP 通知 |

## 健康检查

| 检查 | 描述 |
|-------|-------------|
| Indexer Status（索引器状态） | 验证索引器可访问 |
| Download Client（下载客户端） | 验证下载客户端运行中 |
| Disk Space（磁盘空间） | 监控可用存储 |
| Root Folder（根文件夹） | 验证音乐目录存在 |

## 搜索行为

| 搜索类型 | 描述 |
|-------------|-------------|
| Automatic（自动） | 搜索 RSS 源获取新发行 |
| Manual（手动） | 搜索特定专辑 |
| Missing（缺失） | 搜索所有缺失的专辑 |
| Cutoff Unmet（未达标） | 搜索质量升级 |

## 技巧和最佳实践

| 技巧 | 说明 |
|-----|-------------|
| 使用 Prowlarr | 集中管理索引器 |
| 设置质量截止 | 避免不必要的升级 |
| 使用硬链接 | 做种时节省磁盘空间 |
| 按艺术家组织 | 保持文件夹结构整洁 |
| 监控磁盘空间 | 音乐库增长很快 |
| 使用正确的命名 | 使文件与媒体服务器兼容 |

## 与媒体服务器集成

| 服务器 | 集成 |
|--------|-------------|
| Plex | 自动库扫描 |
| Jellyfin | 自动库扫描 |
| Emby | 自动库扫描 |
| Navidrome | Subsonic 兼容串流 |

## 故障排除

| 问题 | 解决方案 |
|-------|----------|
| 无结果 | 检查索引器配置 |
| 下载失败 | 验证下载客户端设置 |
| 导入失败 | 检查命名和权限 |
| 缺少元数据 | 验证 MusicBrainz 连接 |
| 下载缓慢 | 检查索引器和客户端健康状况 |

## 结论

Lidarr 自动化了音乐收藏的管理，确保喜爱艺术家的唱片目录完整且组织得当。它与下载客户端和媒体服务器集成，提供无缝的音乐库管理体验。
