# 使用 Jellyfin 搭建媒体服务器

## 简介

Jellyfin 是一个免费开源的媒体服务器，用于组织、管理和串流您的个人媒体收藏。它提供了类似 Netflix 的界面，用于播放电影、电视节目、音乐和书籍，无追踪和广告。本教程涵盖安装、库设置、客户端应用和优化。

## 架构概览

| 组件 | 描述 | 角色 |
|------|------|------|
| Server | .NET 应用 | 核心媒体管理和串流 |
| Web UI | 浏览器界面 | 管理和播放 |
| Client Apps | 原生应用 | 在各种设备上播放 |
| Plugins | 扩展 | 附加功能 |
| Metadata Providers | 外部服务 | 自动内容信息 |

## 系统要求

| 组件 | 最低配置 | 推荐配置 |
|------|----------|----------|
| CPU | 1 GHz | 2+ GHz（用于转码） |
| RAM | 512 MB | 2 GB+ |
| 磁盘 | 1 GB（服务器） | SSD 用于数据库 |
| 操作系统 | Linux, macOS, Windows | Linux（Docker） |
| 网络 | 100 Mbps | 1 Gbps |

## 安装

### Docker Compose

```yaml
version: "3.8"

services:
  jellyfin:
    image: jellyfin/jellyfin:latest
    container_name: jellyfin
    restart: unless-stopped
    ports:
      - "8096:8096"
    volumes:
      - ./config:/config
      - ./cache:/cache
      - /path/to/media:/media:ro
    environment:
      - JELLYFIN_PublishedServerUrl=http://your-server:8096
    devices:
      - /dev/dri:/dev/dri  # Hardware acceleration
```

### 初始设置

1. 访问 `http://your-server:8096`
2. 完成设置向导
3. 创建管理员账户
4. 添加第一个媒体库
5. 如需配置远程访问

## 媒体组织

### 文件夹结构

```
media/
├── Movies/
│   ├── Movie Name (Year)/
│   │   ├── Movie Name (Year).mkv
│   │   └── Movie Name (Year).srt
│   └── Another Movie (Year)/
│       └── Another Movie (Year).mp4
├── TV Shows/
│   ├── Show Name/
│   │   ├── Season 01/
│   │   │   ├── S01E01.mkv
│   │   │   └── S01E02.mkv
│   │   └── Season 02/
│   │       └── S02E01.mkv
│   └── Another Show/
├── Music/
│   ├── Artist/
│   │   ├── Album/
│   │   │   ├── 01 - Track.flac
│   │   │   └── 02 - Track.flac
│   │   └── Another Album/
│   └── Another Artist/
└── Books/
    └── Book Title.pdf
```

### 命名约定

| 内容 | 约定 | 示例 |
|------|------|------|
| 电影 | `Title (Year).ext` | `Inception (2010).mkv` |
| 电视节目 | `SxxExx.ext` | `S01E01.mkv` |
| 音乐 | `Artist/Album/Track.ext` | `Pink Floyd/Dark Side/01 - Time.flac` |
| 书籍 | `Title.ext` | `Programming Guide.epub` |

### 文件命名提示

| 问题 | 麻烦 | 解决方案 |
|------|------|----------|
| 匹配错误 | 错误识别 | 在文件名中添加年份 |
| 重复 | 多个版本 | 使用版本标签 |
| 字幕 | 未检测到 | 使字幕文件名与视频匹配 |
| 合集 | 未分组 | 使用合集文件夹 |

## 库配置

### 库类型

| 类型 | 内容 | 元数据源 |
|------|------|----------|
| Movies | 电影 | TMDB, OMDB |
| TV Shows | 连续剧、剧集 | TMDB, TVDB |
| Music | 专辑、曲目 | MusicBrainz |
| Books | PDF、EPUB | Google Books |
| Home Videos | 个人录像 | 手动 |
| Photos | 图片集合 | EXIF 数据 |

### 添加库

1. 前往 Dashboard > Libraries
2. 点击 "Add Library"
3. 选择内容类型
4. 命名库
5. 添加文件夹路径
6. 配置元数据提供者
7. 设置显示偏好

### 元数据提供者

| 提供者 | 内容 | 功能 |
|--------|------|------|
| TheMovieDB | 电影、电视 | 主要来源 |
| TheTVDB | 电视节目 | 剧集详情 |
| Open Movie DB | 电影 | 备选来源 |
| MusicBrainz | 音乐 | 专辑和曲目信息 |
| IMDb | 所有 | 评分和详情 |

## 转码

### 转码类型

| 类型 | 描述 | CPU 影响 |
|------|------|----------|
| Direct Play | 原始格式 | 无 |
| Direct Stream | 容器更换 | 最小 |
| Video Transcode | 重新编码视频 | 高 |
| Audio Transcode | 重新编码音频 | 中等 |
| Subtitle Burn | 烧录字幕 | 中等 |

### 硬件加速

| 方法 | GPU 类型 | 性能 |
|------|----------|------|
| VAAPI | Intel, AMD | 良好 |
| NVENC | NVIDIA | 优秀 |
| QSV | Intel | 优秀 |
| VideoToolbox | Apple | 良好 |
| AMF | AMD | 良好 |

### 转码设置

| 设置 | 建议 |
|------|------|
| 硬件加速 | 如可用则启用 |
| 转码线程数 | CPU 核心数的一半 |
| 临时转码路径 | 快速 SSD |
| 最大并发流数 | 基于 CPU/GPU |
| 比特率限制 | 基于网络 |

## 客户端应用

### 官方客户端

| 平台 | 应用 | 功能 |
|------|------|------|
| Web | 浏览器 | 功能齐全 |
| Android | Jellyfin Android | 移动播放 |
| iOS | Jellyfin iOS | 移动播放 |
| Android TV | Jellyfin TV | 电视界面 |
| Apple TV | Swiftfin | 原生 tvOS |
| Roku | Jellyfin Roku | Roku 设备 |
| Fire TV | Jellyfin Fire TV | Amazon 设备 |

### 第三方客户端

| 平台 | 应用 | 功能 |
|------|------|------|
| LG WebOS | Jellyfin WebOS | LG 电视 |
| Samsung Tizen | Jellyfin Tizen | 三星电视 |
| Kodi | Jellyfin Kodi | 媒体中心 |
| mpv | 直接播放 | 高级播放器 |

### 客户端对比

| 功能 | Web | Android | iOS | TV 应用 |
|------|-----|---------|-----|---------|
| Direct Play | 是 | 是 | 是 | 是 |
| Transcoding | 是 | 是 | 是 | 是 |
| Downloads | 是 | 是 | 是 | 否 |
| Live TV | 是 | 是 | 是 | 是 |
| Music | 是 | 是 | 是 | 是 |

## 用户管理

### 用户角色

| 角色 | 权限 | 用途 |
|------|------|------|
| Admin | 完全控制 | 服务器所有者 |
| Regular | 查看内容 | 家庭成员 |
| Guest | 有限访问 | 临时访客 |

### 用户设置

| 设置 | 描述 | 选项 |
|------|------|------|
| Library access | 内容可见性 | 按库 |
| Remote access | 从外部串流 | 启用/禁用 |
| Transcoding | 质量限制 | 比特率上限 |
| Downloads | 离线访问 | 启用/禁用 |
| Parental control | 内容过滤 | 评分限制 |

## 直播电视和 DVR

### 设置要求

| 组件 | 选项 |
|------|------|
| Tuner | HDHomeRun, USB 调谐器 |
| Guide Data | XMLTV, 内置提供者 |
| Storage | 录制目标 |

### DVR 功能

| 功能 | 描述 |
|------|------|
| Scheduled recording | 录制未来节目 |
| Series recording | 录制所有剧集 |
| Conflict management | 处理调度冲突 |
| Commercial skip | 自动跳过广告 |

## 插件

### 基本插件

| 插件 | 用途 | 分类 |
|------|------|------|
| Open Subtitles | 字幕下载 | 字幕 |
| TMDb Box Sets | 电影合集 | 组织 |
| Intro Skipper | 跳过电视片头 | 播放 |
| LDAP | 外部认证 | 安全 |
| Kodi Sync Queue | Kodi 集成 | 同步 |

### 安装插件

1. 前往 Dashboard > Plugins
2. 浏览或搜索仓库
3. 点击 Install
4. 重启服务器
5. 配置插件设置

## 性能优化

### 服务器优化

| 设置 | 建议 | 影响 |
|------|------|------|
| Database location | SSD | 更快查询 |
| Cache location | SSD | 更快元数据 |
| Transcode path | SSD | 更快转码 |
| Parallel tasks | 匹配 CPU 核心数 | 更好吞吐量 |
| Chapter image extraction | 安排在低峰期 | 减少负载 |

### 网络优化

| 设置 | 建议 | 影响 |
|------|------|------|
| Remote bitrate | 基于上传速度 | 更流畅串流 |
| Local bitrate | 无限 | 最佳质量 |
| CDN | 使用反向代理 | 减少服务器负载 |
| IPv6 | 如可用则启用 | 直接连接 |

## 备份与恢复

### 备份策略

| 组件 | 方法 | 频率 |
|------|------|------|
| Configuration | 文件复制 | 每周 |
| Database | 导出 | 每周 |
| Metadata | 自动重建 | 按需 |
| Media | 原始文件 | 持续 |

### 备份脚本

```bash
#!/bin/bash
BACKUP_DIR="/backups/jellyfin/$(date +%Y%m%d)"
mkdir -p "$BACKUP_DIR"

# 停止服务器
docker stop jellyfin

# 备份配置
cp -r /path/to/config "$BACKUP_DIR/"

# 备份数据库
cp /path/to/config/data/jellyfin.db "$BACKUP_DIR/"

# 启动服务器
docker start jellyfin

# 压缩
tar czf "$BACKUP_DIR.tar.gz" "$BACKUP_DIR"
rm -rf "$BACKUP_DIR"
```

## 故障排除

| 问题 | 可能原因 | 解决方案 |
|------|----------|----------|
| 播放卡顿 | 转码瓶颈 | 启用硬件加速 |
| 元数据缺失 | 命名错误 | 遵循命名约定 |
| 无远程访问 | 端口未开放 | 配置防火墙/路由器 |
| 缓冲 | 网络带宽 | 降低串流质量 |
| 库未扫描 | 路径问题 | 验证文件夹权限 |

## 总结

Jellyfin 提供了一个强大的自托管解决方案，用于管理和串流个人媒体收藏。其广泛的客户端支持、硬件转码功能和插件生态系统使其适用于任何规模的家庭媒体服务器。

关键实践：

- 按照推荐的命名约定组织媒体文件
- 启用硬件加速以实现高效转码
- 设置多个用户账户并配置适当权限
- 使用反向代理实现安全远程访问
- 定期备份配置和数据库
