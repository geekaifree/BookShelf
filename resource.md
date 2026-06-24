# 资源合集 - 媒体和软件资源指南

## 目录

- [流媒体网站](#流媒体网站)
- [下载工具](#下载工具)
- [Torrent 客户端](#torrent-客户端)
- [Usenet](#usenet)
- [Debrid 服务](#debrid-服务)
- [媒体服务器](#媒体服务器)
- [字幕工具](#字幕工具)
- [漫画](#漫画)
- [动漫](#动漫)
- [有声书和播客](#有声书和播客)
- [游戏](#游戏)
- [软件](#软件)

---

## 流媒体网站

### 电影和电视剧

| 网站 | 类型 | 画质 | 备注 |
|------|------|---------|-------|
| Fmovies | 电影/电视剧 | HD | 资源丰富 |
| 123movies | 电影/电视剧 | HD | 多个镜像 |
| Putlocker | 电影/电视剧 | HD | 经典网站 |
| SolarMovie | 电影/电视剧 | HD | 界面简洁 |
| YesMovies | 电影/电视剧 | HD | 分类清晰 |
| LookMovie | 电影/电视剧 | HD | 广告少 |
| CouchTuner | 电视剧 | HD | 专注电视剧 |

### 动漫

| 网站 | 类型 | 画质 | 备注 |
|------|------|---------|-------|
| 9anime | 动漫 | HD | 资源丰富 |
| Gogoanime | 动漫 | HD | 更新快 |
| AnimePahe | 动漫 | HD | 文件小 |
| Zoro.to | 动漫 | HD | 界面简洁 |
| KickAssAnime | 动漫 | HD | 选择多 |

### 体育直播

| 网站 | 类型 | 备注 |
|------|------|-------|
| Sportsurge | 综合体育 | 聚合器 |
| Buffstreams | 综合体育 | 赛事直播 |
| Stream2Watch | 综合体育 | 多源 |
| VIPBox | 综合体育 | 覆盖广 |

### 电视直播

| 网站 | 类型 | 备注 |
|------|------|-------|
| USTVGO | 美国电视 | 免费美国频道 |
| TV247 | 国际 | 全球频道 |
| OKLiveTV | 国际 | 各类频道 |

---

## 下载工具

### 视频下载器

| 工具 | 平台 | 支持网站 |
|------|----------|-----------------|
| yt-dlp | 全平台 | YouTube、1000+ 网站 |
| youtube-dl | 全平台 | YouTube、众多网站 |
| gallery-dl | 全平台 | 图库 |
| JDownloader | 全平台 | 多网盘 |
| Internet Download Manager | Windows | 浏览器集成 |
| Motrix | 全平台 | 多协议 |

### yt-dlp 用法

    # 下载视频
    yt-dlp https://www.youtube.com/watch?v=VIDEO_ID

    # 最佳画质下载
    yt-dlp -f best https://www.youtube.com/watch?v=VIDEO_ID

    # 下载播放列表
    yt-dlp https://www.youtube.com/playlist?list=PLAYLIST_ID

    # 仅下载音频
    yt-dlp -x --audio-format mp3 https://www.youtube.com/watch?v=VIDEO_ID

    # 下载带字幕
    yt-dlp --write-subs --sub-lang en https://www.youtube.com/watch?v=VIDEO_ID

### gallery-dl 用法

    # 从图库下载
    gallery-dl https://www.instagram.com/username/

    # 使用配置下载
    gallery-dl -c config.json https://imgur.com/a/ALBUM_ID

---

## Torrent 客户端

### 桌面客户端

| 客户端 | 平台 | 开源 | 功能 |
|--------|----------|-------------|----------|
| qBittorrent | 全平台 | 是 | 功能丰富、无广告 |
| Transmission | 全平台 | 是 | 轻量、简洁 |
| Deluge | 全平台 | 是 | 插件系统 |
| rTorrent | Linux | 是 | 终端版 |
| Tixati | Windows/Linux | 否 | 详细统计 |
| BiglyBT | 全平台 | 是 | 功能丰富 |

### 对比

| 功能 | qBittorrent | Transmission | Deluge |
|---------|-------------|--------------|--------|
| Web UI | 是 | 是 | 是 |
| RSS | 是 | 否 | 插件 |
| 计划任务 | 是 | 否 | 插件 |
| 加密 | 是 | 是 | 是 |
| DHT | 是 | 是 | 是 |
| 磁力链接 | 是 | 是 | 是 |
| 顺序下载 | 是 | 否 | 否 |

### Web 客户端

| 客户端 | 说明 |
|--------|-------------|
| Flood | rTorrent 的现代 Web UI |
| ruTorrent | rTorrent 的 Web UI |
| Sonarr | 电视剧自动化 |
| Radarr | 电影自动化 |
| Lidarr | 音乐自动化 |

### Seedbox 提供商

| 提供商 | 价格 | 功能 |
|----------|-------|----------|
| Seedbox.io | /月 | 共享、简单 |
| Ultra.cc | /月 | 共享、支持好 |
| Whatbox | /月 | 有独立选项 |
| Feral Hosting | /月 | 共享、不限流量 |
| Bytesized | /月 | Appbox |

---

## Usenet

### 什么是 Usenet？

Usenet 是一个分布式讨论系统，也支持二进制文件共享。需要订阅 Usenet 提供商和索引器。

### Usenet 提供商

| 提供商 | 保留天数 | 价格 | 备注 |
|----------|-----------|-------|-------|
| Newshosting | 5000+ 天 | /月 | 不限流量 |
| Eweka | 5000+ 天 | /月 | 欧洲骨干 |
| UsenetServer | 5000+ 天 | /月 | 不限流量 |
| Newsgroup.ninja | 4000+ 天 | /月 | 经济选择 |
| Frugal Usenet | 3000+ 天 | /月 | 保留天数有限 |

### Usenet 索引器

| 索引器 | 类型 | 价格 | 备注 |
|---------|------|-------|-------|
| NZBgeek | VIP | /年 | 流行 |
| NZBFinder | VIP | /年 | 适合荷兰用户 |
| DrunkenSlug | 免费/VIP | 免费//年 | 免费有限 |
| NZBPlanet | VIP | /年 | 数据库大 |
| NinjaCentral | 免费/VIP | 免费//年 | 较新 |

### Usenet 客户端

| 客户端 | 平台 | 功能 |
|--------|----------|----------|
| SABnzbd | 全平台 | 基于 Web、自动化 |
| NZBGet | 全平台 | 轻量、快速 |
| Newsbin | Windows | 功能丰富 |

### Usenet 自动化

| 工具 | 用途 |
|------|---------|
| Sonarr | 电视剧管理 |
| Radarr | 电影管理 |
| Lidarr | 音乐管理 |
| Readarr | 书籍管理 |
| Prowlarr | 索引器管理 |
| Bazarr | 字幕管理 |

---

## Debrid 服务

### 什么是 Debrid 服务？

Debrid 服务以单一订阅提供多个文件托管服务的高级访问。它们也可以将 Torrent 转换为直接下载。

### Debrid 服务

| 服务 | 价格 | 功能 |
|---------|-------|----------|
| Real-Debrid | 5 EUR/月 | 多网盘、Torrent 转换 |
| AllDebrid | 5 EUR/月 | 类似 Real-Debrid |
| Premiumize | 10 EUR/月 | 云存储、VPN |
| LinkSnappy | 10 EUR/月 | 多网盘 |
| Offcloud | /月 | 云下载 |

### 对比

| 功能 | Real-Debrid | AllDebrid | Premiumize |
|---------|-------------|-----------|------------|
| 文件托管 | 50+ | 50+ | 30+ |
| Torrent 支持 | 是 | 是 | 是 |
| 云存储 | 否 | 否 | 是 |
| VPN | 否 | 否 | 是 |
| Kodi 支持 | 是 | 是 | 是 |
| API 访问 | 是 | 是 | 是 |

---

## 媒体服务器

### 自托管媒体服务器

| 服务器 | 开源 | 功能 |
|--------|-------------|----------|
| Jellyfin | 是 | 免费、无付费功能 |
| Emby | 否 | 免费 + 高级 |
| Plex | 否 | 免费 + Plex Pass |
| Stremio | 是 | 基于插件 |
| Kodi | 是 | 本地媒体播放器 |

### 对比

| 功能 | Jellyfin | Emby | Plex |
|---------|----------|------|------|
| 价格 | 免费 | 免费/付费 | 免费/付费 |
| 直播电视 | 是 | 是 | 是 |
| 硬件转码 | 是 | 是 | 付费 |
| 移动应用 | 是 | 是 | 是 |
| DLNA | 是 | 是 | 是 |
| 插件 | 是 | 是 | 是 |
| 离线同步 | 是 | 是 | 付费 |

### 媒体自动化

| 工具 | 用途 |
|------|---------|
| Sonarr | 电视剧下载 |
| Radarr | 电影下载 |
| Lidarr | 音乐下载 |
| Readarr | 书籍下载 |
| Prowlarr | 索引器管理 |
| Overseerr | 媒体请求 |
| Jellyseerr | Jellyfin/Emby 请求 |
| Tdarr | 媒体转码 |

### 媒体服务器设置（Docker Compose）

    version: "3"

    services:
      jellyfin:
        image: jellyfin/jellyfin
        ports:
          - "8096:8096"
        volumes:
          - ./config:/config
          - ./cache:/cache
          - /media:/media
        restart: unless-stopped

      sonarr:
        image: lscr.io/linuxserver/sonarr
        ports:
          - "8989:8989"
        volumes:
          - ./sonarr:/config
          - /media/tv:/tv
          - /downloads:/downloads
        restart: unless-stopped

      radarr:
        image: lscr.io/linuxserver/radarr
        ports:
          - "7878:7878"
        volumes:
          - ./radarr:/config
          - /media/movies:/movies
          - /downloads:/downloads
        restart: unless-stopped

---

## 字幕工具

### 字幕下载器

| 工具 | 平台 | 功能 |
|------|----------|----------|
| Bazarr | 全平台 | 自动、集成 Sonarr/Radarr |
| Subliminal | 全平台 | 基于 Python、多源 |
| Filebot | 全平台 | 重命名 + 字幕下载 |
| Subscene | Web | 手动下载 |
| OpenSubtitles | Web | 大型数据库 |
| Addic7ed | Web | 专注电视剧 |

### 字幕搜索和下载

    # Subliminal
    subliminal download -l en /path/to/video.mkv

    # Filebot
    filebot -script fn:suball /path/to/media

### 字幕提供商

| 提供商 | 免费 | API | 备注 |
|----------|------|-----|-------|
| OpenSubtitles | 是 | 是 | 最大数据库 |
| Subscene | 是 | 否 | 仅手动 |
| Addic7ed | 是 | 否 | 专注电视剧 |
| Podnapisi | 是 | 是 | 多语言 |
| Gestdown | 是 | 是 | 专注电视剧 |

---

## 漫画

### 漫画阅读器

| 应用 | 平台 | 功能 |
|-----|----------|----------|
| Tachiyomi | Android | 扩展、追踪 |
| Mihon | Android | Tachiyomi 分支 |
| Komga | 自托管 | 服务器 + Web 阅读器 |
| Kavita | 自托管 | 服务器 + Web 阅读器 |
| LANraragi | 自托管 | 服务器 + Web 阅读器 |

### 漫画阅读器（桌面）

| 应用 | 平台 | 功能 |
|-----|----------|----------|
| YACReader | 桌面 | CBR/CBZ 阅读器 |
| ComicRack | Windows | 功能丰富 |
| Perfect Viewer | Android | CBR/CBZ/PDF |
| Panels | iOS | CBR/CBZ 阅读器 |

### 漫画来源

| 来源 | 类型 | 备注 |
|--------|------|-------|
| MangaDex | 翻译 | 社区翻译 |
| MangaSee | 聚合 | 资源丰富 |
| MangaKakalot | 聚合 | 更新快 |
| Manganato | 聚合 | 界面简洁 |

---

## 动漫

### 动漫下载

| 工具 | 功能 |
|------|----------|
| yt-dlp | 从流媒体网站下载 |
| anime-dl | 专用动漫下载器 |
| gallery-dl | 图库 |

### 动漫 Tracker

| 网站 | 类型 | 备注 |
|------|------|-------|
| Nyaa | 公开 | 动漫 Torrent |
| AniDex | 公开 | 动漫 Torrent |
| AnimeBytes | 私密 | 高质量 |
| BakaBT | 私密 | 精选 |
| ABtorrents | 私密 | 专注动漫 |

### 动漫流媒体应用

| 应用 | 平台 | 功能 |
|-----|----------|----------|
| Aniyomi | Android | 流媒体 + 漫画 |
| CloudStream | Android | 流媒体 |
| Stremio | 全平台 | 基于插件 |
| Kodi + 插件 | 全平台 | 可定制 |

### 动漫管理

| 工具 | 用途 |
|------|---------|
| MyAnimeList | 追踪 |
| AniList | 追踪 |
| Kitsu | 追踪 |
| Shoko | 服务器管理 |

---

## 有声书和播客

### 有声书来源

| 来源 | 类型 | 备注 |
|--------|------|-------|
| Librivox | 公共领域 | 免费、志愿者朗读 |
| Open Culture | 公共领域 | 免费有声书 |
| MAM (MyAnonaMouse) | 私密 | 有声书 Tracker |
| Audible | 付费 | 最大选择 |

### 有声书服务器

| 服务器 | 开源 | 功能 |
|--------|-------------|----------|
| Audiobookshelf | 是 | 功能齐全 |
| Booksonic | 是 | Subsonic 兼容 |
| Plex + 插件 | 否 | 通过插件 |

### 播客工具

| 工具 | 平台 | 功能 |
|------|----------|----------|
| AntennaPod | Android | 开源 |
| Podcast Addict | Android | 功能丰富 |
| Overcast | iOS | 智能加速 |
| gpodder | 桌面 | 开源 |

---

## 游戏

### 游戏资源

| 网站 | 类型 | 备注 |
|------|------|-------|
| FitGirl Repacks | 压缩版 | 压缩、可信 |
| DODI Repacks | 压缩版 | 安装快 |
| KaOS Krew | 压缩版 | Scene 压缩版 |
| ElAmigos | 压缩版 | 干净安装 |

### 游戏启动器

| 启动器 | 功能 |
|----------|----------|
| Steam | 最大商店 |
| GOG | 无 DRM 游戏 |
| Epic Games | 每周免费游戏 |
| Heroic | 开源 Epic/GOG 启动器 |
| Lutris | Linux 游戏 |

### ROM 网站

| 网站 | 类型 | 备注 |
|------|------|-------|
| Vimm's Lair | 复古 | 精选、安全 |
| ROMsmania | 复古 | 大量收藏 |
| CDRomance | 复古 | 翻译版游戏 |
| Myrient | 复古 | 存档 |

### 模拟器

| 模拟器 | 平台 | 系统 |
|----------|----------|---------|
| RetroArch | 全平台 | 多系统 |
| Dolphin | 全平台 | GameCube/Wii |
| PCSX2 | 全平台 | PS2 |
| RPCS3 | 桌面 | PS3 |
| Yuzu/Ryujinx | 桌面 | Switch |
| Cemu | 桌面 | Wii U |

---

## 软件

### 软件破解

| 网站 | 类型 | 备注 |
|------|------|-------|
| CS.RIN.RU | 论坛 | 专注游戏 |
| nsaneforums | 论坛 | 通用软件 |
| r/Piracy | Reddit | 精华帖 |

### 软件工具

| 工具 | 用途 |
|------|---------|
| MAS | Microsoft 激活 |
| KMS_VL_ALL | KMS 激活 |
| Adobe GenP | Adobe 激活 |
| Lulu | macOS 防火墙 |

### Linux 软件

| 工具 | 用途 |
|------|---------|
| Flatpak | 包管理 |
| Snap | 包管理 |
| AppImage | 便携应用 |
| Wine | Windows 兼容 |
| Bottles | Wine 管理 |
| Proton | Steam Windows 游戏 |

---

## 安全和隐私

### 必备工具

| 工具 | 用途 |
|------|---------|
| VPN | 隐藏 IP |
| uBlock Origin | 拦截广告和恶意软件 |
| Firefox | 隐私浏览器 |
| Malwarebytes | 反恶意软件 |
| VirusTotal | 文件扫描 |

### 最佳实践

| 实践 | 说明 |
|----------|-------------|
| 使用 VPN | 隐藏你的 IP 地址 |
| 拦截广告 | 使用 uBlock Origin |
| 查看评论 | 阅读用户反馈 |
| 验证来源 | 使用可信网站 |
| 扫描文件 | 检查恶意软件 |
| 使用沙盒 | 在隔离环境测试 |
| 保持更新 | 更新所有软件 |

### 推荐 VPN

| 提供商 | 日志 | 速度 | 价格 |
|----------|---------|-------|-------|
| Mullvad | 无日志 | 快 | 5 EUR/月 |
| ProtonVPN | 无日志 | 好 | 免费/付费 |
| IVPN | 无日志 | 好 | 付费 |
| AirVPN | 无日志 | 好 | 付费 |

---

## 快速参考

### 推荐软件栈

| 类别 | 推荐 |
|----------|-------------|
| 浏览器 | Firefox + uBlock Origin |
| VPN | Mullvad 或 ProtonVPN |
| Torrent 客户端 | qBittorrent |
| 媒体服务器 | Jellyfin |
| 媒体自动化 | Sonarr + Radarr + Prowlarr |
| 字幕 | Bazarr |
| 下载 | yt-dlp |
| Usenet | SABnzbd + NZBgeek |

### 入门清单

| 步骤 | 任务 |
|------|------|
| 1 | 设置 VPN |
| 2 | 安装 qBittorrent |
| 3 | 安装 Jellyfin |
| 4 | 设置 Sonarr/Radarr |
| 5 | 配置 Prowlarr |
| 6 | 设置 Bazarr |
| 7 | 安装 uBlock Origin |
| 8 | 加入私密 Tracker |
