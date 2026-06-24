# 音乐串流

> 本文档整合了以下源文件：player.md, navidrome.md, media.md, media2.md, stream.md

---

## 来源：player.md

## 简介

Koel 是一个开源音乐流媒体服务器，允许您从任何地方托管和播放个人音乐收藏。它提供了一个现代化的 Web 界面，并支持多种音频格式。

### 什么是 Koel？

Koel 是一个自托管音乐流媒体平台，可以索引您的音乐库并提供基于 Web 的播放器界面。

| 特性 | 描述 |
|------|------|
| Web 播放器 | 现代化的音乐播放 UI |
| 音乐串流 | 通过任何有浏览器的设备播放 |
| 播放列表管理 | 创建和管理播放列表 |
| 用户管理 | 多用户独立音乐库 |
| 专辑封面 | 自动获取专辑封面 |

### 与其他方案的比较

| 特性 | Koel | Plex | Jellyfin |
|------|------|------|----------|
| 专注 | 仅音乐 | 多媒体 | 多媒体 |
| Web 界面 | 是 | 是 | 是 |
| 移动应用 | 第三方 | 官方 | 官方 |
| 转码 | 是 | 是 | 是 |
| 自托管 | 是 | 是 | 是 |

## 安装

### 前置要求

| 要求 | 最低版本 |
|------|----------|
| PHP | 8.1 或更高 |
| Composer | 2.0 或更高 |
| Node.js | 16.0 或更高 |
| 数据库 | MySQL 或 MariaDB |
| Web 服务器 | Nginx 或 Apache |

### 安装步骤

```bash
git clone https://github.com/koel/koel.git
cd koel
composer install
npm install
npm run build
php artisan koel:init
```

### 环境配置

```env
APP_NAME=Koel
APP_URL=https://music.example.com
DB_CONNECTION=mysql
DB_HOST=127.0.0.1
DB_PORT=3306
DB_DATABASE=koel
DB_USERNAME=root
DB_PASSWORD=secret
MEDIA_PATH=/path/to/music
```

### 数据库设置

```bash
php artisan migrate
php artisan db:seed
```

## Web 服务器配置

### Nginx 配置

```nginx
server {
    listen 80;
    server_name music.example.com;
    root /var/www/koel/public;
    index index.php;

    location / {
        try_files $uri $uri/ /index.php?$query_string;
    }

    location ~ \.php$ {
        fastcgi_pass unix:/var/run/php/php8.1-fpm.sock;
        fastcgi_param SCRIPT_FILENAME $realpath_root$fastcgi_script_name;
        include fastcgi_params;
    }
}
```

### Apache 配置

```apache
<VirtualHost *:80>
    ServerName music.example.com
    DocumentRoot /var/www/koel/public
    <Directory /var/www/koel/public>
        AllowOverride All
        Require all granted
    </Directory>
</VirtualHost>
```

## 音乐库管理

### 支持的格式

| 格式 | 扩展名 | 质量 |
|------|--------|------|
| MP3 | .mp3 | 良好 |
| FLAC | .flac | 无损 |
| OGG | .ogg | 良好 |
| AAC | .m4a | 良好 |
| WAV | .wav | 无损 |

### 扫描音乐

将音乐文件添加到媒体路径后，扫描音乐库：

```bash
php artisan koel:sync
```

### 音乐库结构

```
/path/to/music/
├── Artist Name/
│   ├── Album Name/
│   │   ├── 01 - Track Name.mp3
│   │   ├── 02 - Track Name.mp3
│   │   └── cover.jpg
│   └── Another Album/
│       └── 01 - Track Name.flac
└── Various Artists/
    └── Compilation/
        └── 01 - Track Name.mp3
```

## 用户管理

### 创建用户

```bash
php artisan koel:user:create
```

### 用户角色

| 角色 | 权限 |
|------|------|
| Admin | 完全访问权限，管理用户 |
| User | 播放音乐，管理自己的播放列表 |

### 用户配置

```bash
# 更改用户密码
php artisan koel:user:change-password

# 删除用户
php artisan koel:user:delete
```

## 播放功能

### 音频串流

Koel 支持多种串流方式：

| 方式 | 描述 | 用例 |
|------|------|------|
| 直接 | 直接串流文件 | 局域网 |
| 转码 | 实时转换 | 远程串流 |
| 渐进式 | 下载后播放 | 低带宽 |

### 转码设置

```env
TRANSCODE_FLAC=true
TRANSCODE_MP3_320=true
TRANSCODE_CACHE_PATH=/tmp/koel-transcode
```

### 播放列表管理

| 功能 | 描述 |
|------|------|
| 创建播放列表 | 将歌曲分组为收藏 |
| 智能播放列表 | 基于规则自动生成 |
| 分享播放列表 | 与其他用户分享 |
| 导出播放列表 | 下载播放列表数据 |

## API 访问

### REST API 端点

| 端点 | 方法 | 描述 |
|------|------|------|
| `/api/songs` | GET | 列出所有歌曲 |
| `/api/albums` | GET | 列出所有专辑 |
| `/api/artists` | GET | 列出所有艺术家 |
| `/api/playlists` | GET | 列出播放列表 |
| `/api/search` | GET | 搜索音乐库 |

### 身份验证

```bash
# 获取 API 令牌
curl -X POST https://music.example.com/api/me \
  -d "email=user@example.com" \
  -d "password=password"
```

### API 使用示例

```bash
# 列出歌曲
curl -H "Authorization: Bearer TOKEN" \
  https://music.example.com/api/songs

# 创建播放列表
curl -X POST https://music.example.com/api/playlists \
  -H "Authorization: Bearer TOKEN" \
  -d "name=My Playlist"
```

## Docker 部署

### Docker Compose

```yaml
version: '3'
services:
  koel:
    image: koel/koel
    ports:
      - "8080:80"
    environment:
      - DB_CONNECTION=mysql
      - DB_HOST=db
      - DB_DATABASE=koel
      - DB_USERNAME=koel
      - DB_PASSWORD=secret
      - MEDIA_PATH=/music
    volumes:
      - /path/to/music:/music

  db:
    image: mysql:8.0
    environment:
      - MYSQL_ROOT_PASSWORD=secret
      - MYSQL_DATABASE=koel
      - MYSQL_USER=koel
      - MYSQL_PASSWORD=secret
    volumes:
      - mysql_data:/var/lib/mysql

volumes:
  mysql_data:
```

### 使用 Docker 运行

```bash
docker-compose up -d
```

## 移动端访问

### 移动应用

| 应用 | 平台 | 状态 |
|------|------|------|
| Amperfy | iOS | 第三方 |
| Ultrasonic | Android | 第三方 |
| Web 浏览器 | 任意 | 原生 |

### Subsonic API

Koel 实现了 Subsonic API，兼容许多第三方客户端。

## 性能优化

### 缓存配置

```env
CACHE_DRIVER=redis
SESSION_DRIVER=redis
QUEUE_CONNECTION=redis
```

### PHP 优化

```ini
memory_limit = 256M
max_execution_time = 60
upload_max_filesize = 50M
```

## 安全

### HTTPS 配置

```nginx
server {
    listen 443 ssl;
    ssl_certificate /path/to/cert.pem;
    ssl_certificate_key /path/to/key.pem;
}
```

### 安全最佳实践

| 实践 | 描述 |
|------|------|
| 使用 HTTPS | 加密所有连接 |
| 强密码 | 强制密码要求 |
| 定期更新 | 保持 Koel 更新 |
| 防火墙 | 限制访问必要端口 |
| 备份 | 定期备份数据库和文件 |

## 总结

| 组件 | 用途 |
|------|------|
| Web UI | 音乐浏览和播放 |
| REST API | 编程访问 |
| Subsonic API | 移动应用兼容性 |
| 转码 | 格式转换用于串流 |
| 用户系统 | 多用户支持 |


---

## 来源：navidrome.md

## 目录

1. [Navidrome 简介](#introduction)
2. [安装方式](#installation)
3. [配置](#configuration)
4. [音乐库管理](#library)
5. [客户端应用](#clients)
6. [用户管理](#users)
7. [高级功能](#advanced)
8. [维护与备份](#maintenance)

---

## 简介

Navidrome 是一款轻量级的自托管音乐服务器，可将你的个人音乐收藏串流到任何设备。它支持 Subsonic API，兼容众多客户端应用。

### Navidrome 功能

| 功能 | 描述 | 好处 |
|------|------|------|
| 多格式支持 | MP3、FLAC、OGG 等 | 播放任何格式 |
| Web UI | 基于浏览器的播放器 | 无需安装应用 |
| Subsonic API | 标准协议 | 广泛的客户端支持 |
| 多用户 | 多个账号 | 家庭共享 |
| 转码 | 实时转换 | 带宽优化 |

### 系统要求

| 组件 | 最低 | 推荐 |
|------|------|------|
| CPU | 1 核 | 2+ 核 |
| 内存 | 512MB | 2GB+ |
| 存储 | 存放音乐文件 | SSD 存放数据库 |
| 网络 | 1 Mbps 上行 | 10+ Mbps |

### 支持的音频格式

| 格式 | 播放 | 转码 | 备注 |
|------|------|------|------|
| MP3 | 原生 | 不需要 | 通用 |
| FLAC | 原生 | 可选 | 无损 |
| OGG | 原生 | 可选 | 开放格式 |
| AAC | 原生 | 可选 | Apple 设备 |
| WMA | 需转码 | 必需 | 旧格式 |

---

## 安装方式

Navidrome 为不同环境提供多种安装选项。

### Docker 安装（推荐）

```bash
# Docker run command
docker run -d \
  --name navidrome \
  --restart=unless-stopped \
  -p 4533:4533 \
  -v /path/to/music:/music:ro \
  -v /path/to/data:/data \
  deluan/navidrome:latest
```

### Docker Compose

```yaml
version: "3"
services:
  navidrome:
    image: deluan/navidrome:latest
    container_name: navidrome
    restart: unless-stopped
    ports:
      - "4533:4533"
    volumes:
      - ./data:/data
      - /path/to/music:/music:ro
    environment:
      ND_SCANSCHEDULE: "1h"
      ND_LOGLEVEL: "info"
      ND_BASEURL: ""
```

### 二进制安装

| 步骤 | 命令 | 备注 |
|------|------|------|
| 1 | 下载二进制文件 | 从 GitHub releases |
| 2 | 解压文件 | 到安装目录 |
| 3 | 创建配置 | navidrome.toml |
| 4 | 运行 | ./navidrome |

### 各平台系统要求

| 平台 | 架构 | 二进制 | Docker |
|------|------|--------|--------|
| Linux | amd64 | 可用 | 支持 |
| Linux | arm64 | 可用 | 支持 |
| Linux | armv7 | 可用 | 支持 |
| macOS | amd64 | 可用 | 支持 |
| Windows | amd64 | 可用 | 支持 |

---

## 配置

Navidrome 通过环境变量或配置文件进行配置。

### 配置选项

| 变量 | 默认值 | 描述 |
|------|--------|------|
| ND_MUSICFOLDER | /music | 音乐库路径 |
| ND_DATAFOLDER | /data | 数据库和缓存 |
| ND_PORT | 4533 | 服务器端口 |
| ND_BASEURL | "" | URL 路径前缀 |
| ND_LOGLEVEL | info | 日志详细程度 |

### 转码设置

| 设置 | 描述 | 选项 |
|------|------|------|
| 默认比特率 | 目标质量 | 128、192、320 kbps |
| 编码 | 输出格式 | mp3、opus、aac |
| 命令 | FFmpeg 命令 | 可自定义 |

### 扫描配置

| 设置 | 描述 | 默认值 |
|------|------|--------|
| ND_SCANSCHEDULE | 自动扫描间隔 | 1m（初始），1h |
| ND_IGNOREARTOVERAGES | 跳过封面 | true |
| ND_ARTISTARTPRIORITY | 艺术家图片来源 | folder.* |

### 完整配置示例

```toml
# navidrome.toml
MusicFolder = "/music"
DataFolder = "/data"
Port = 4533
LogLevel = "info"
BaseURL = ""
ScanSchedule = "1h"
TranscodingCacheSize = "10GB"
ImageCacheSize = "100MB"
```

### 环境变量 vs 配置文件

| 方式 | 优先级 | 用途 |
|------|--------|------|
| 环境变量 | 较高 | Docker 部署 |
| 配置文件 | 较低 | 二进制安装 |
| CLI 参数 | 最高 | 测试 |

---

## 音乐库管理

为 Navidrome 中的最佳体验组织你的音乐库。

### 推荐的文件夹结构

```
/music/
  Artist Name/
    Album Name (Year)/
      01 - Track Name.flac
      02 - Track Name.flac
      cover.jpg
```

### 支持的元数据标签

| 标签 | 来源 | 重要性 |
|------|------|--------|
| Title | 曲目名称 | 高 |
| Artist | 演奏者 | 高 |
| Album | 专辑名称 | 高 |
| AlbumArtist | 专辑艺术家 | 中等 |
| Year | 发行年份 | 中等 |
| Genre | 音乐流派 | 中等 |
| Track | 曲目编号 | 中等 |

### 封面要求

| 文件名 | 尺寸 | 格式 | 优先级 |
|--------|------|------|--------|
| cover.jpg | 600x600+ | JPEG | 最高 |
| folder.jpg | 600x600+ | JPEG | 高 |
| front.jpg | 600x600+ | JPEG | 中等 |
| 内嵌 | 不定 | 任意 | 最低 |

### 库扫描类型

| 类型 | 触发条件 | 范围 |
|------|----------|------|
| 全量扫描 | 手动或首次运行 | 整个库 |
| 增量扫描 | 定时 | 仅变更文件 |
| 快速扫描 | 新文件 | 最近添加 |

### 元数据编辑工具

| 工具 | 平台 | 功能 |
|------|------|------|
| MusicBrainz Picard | 跨平台 | 自动标签 |
| Mp3tag | Windows | 批量编辑 |
| Beets | CLI | 自动标签 |
| Kid3 | 跨平台 | 手动编辑 |

---

## 客户端应用

Navidrome 通过 Subsonic API 支持众多客户端应用。

### Web 界面

| 功能 | 描述 |
|------|------|
| 播放器 | 内置音频播放器 |
| 浏览 | 艺术家、专辑、歌曲 |
| 搜索 | 全文搜索 |
| 播放列表 | 创建和管理 |
| 收藏 | 标记收藏 |

### 移动客户端

| 客户端 | 平台 | 功能 |
|--------|------|------|
| Symfonium | Android | Material Design，离线 |
| Ultrasonic | Android | 开源 |
| play:Sub | iOS | 原生 iOS 应用 |
| Amperfy | iOS | 现代界面 |

### 桌面客户端

| 客户端 | 平台 | 功能 |
|--------|------|------|
| Sonixd | 跨平台 | 基于 Electron |
| Sublime Music | Linux | GTK 应用 |
| Supersonic | 跨平台 | 原生性能 |

### API 配置

| 设置 | 值 | 用途 |
|------|-----|------|
| Server URL | http://your-server:4533 | 连接 |
| Username | 你的用户名 | 认证 |
| Password | 你的密码 | 认证 |
| API | Subsonic 1.16.1 | 协议版本 |

---

## 用户管理

Navidrome 支持多个用户各自拥有独立设置和库。

### 用户角色

| 角色 | 权限 | 用途 |
|------|------|------|
| Admin | 完全控制 | 服务器拥有者 |
| Regular | 浏览、播放 | 家庭成员 |
| Read-only | 仅浏览 | 访客访问 |

### 创建用户

| 步骤 | 操作 | 详情 |
|------|------|------|
| 1 | 进入管理后台 | 以管理员登录 |
| 2 | 导航到用户 | 设置菜单 |
| 3 | 添加新用户 | 填写表单 |
| 4 | 设置权限 | 分配角色 |
| 5 | 保存 | 用户创建完成 |

### 用户设置

| 设置 | 描述 | 每用户独立 |
|------|------|------------|
| 语言 | 界面语言 | 是 |
| 主题 | 浅色/深色 | 是 |
| 转码 | 质量设置 | 是 |
| 收藏 | 个人收藏 | 是 |
| 播放列表 | 用户播放列表 | 是 |

### 访问控制

| 控制 | 描述 | 实施方式 |
|------|------|----------|
| 密码 | 用户认证 | 必需 |
| API Key | 编程访问 | 可选 |
| IP 限制 | 网络限制 | 可选 |

---

## 高级功能

Navidrome 高级功能面向进阶用户。

### 网络电台

| 设置 | 描述 | 示例 |
|------|------|------|
| Stream URL | 电台 URL | http://stream.example.com |
| Name | 电台名称 | "Jazz FM" |
| Homepage | 电台网站 | http://example.com |

### 播客

| 功能 | 描述 | 配置 |
|------|------|------|
| 订阅 | 添加播客源 | RSS URL |
| 下载 | 自动下载剧集 | 设置 |
| 播放 | 串流剧集 | 内置播放器 |

### 智能播放列表

| 规则类型 | 操作符 | 示例 |
|----------|--------|------|
| 流派 | is, is not | 流派 is "Rock" |
| 年份 | before, after | 年份 after 2020 |
| 评分 | greater than | 评分 > 4 |
| 播放次数 | equals, greater than | 播放 > 10 |

### 分享

| 方式 | 描述 | 安全性 |
|------|------|--------|
| 公开链接 | 通过 URL 分享 | 可选密码 |
| 直接分享 | 分享给用户 | 用户权限 |
| 嵌入 | iframe 播放器 | 域名限制 |

### 书签

| 功能 | 描述 | 用途 |
|------|------|------|
| 保存位置 | 书签播放位置 | 播客收听 |
| 恢复 | 从书签继续 | 多设备 |
| 管理 | 编辑/删除书签 | 整理 |

---

## 维护与备份

保持 Navidrome 安装运行顺畅。

### 备份组件

| 组件 | 位置 | 频率 |
|------|------|------|
| 数据库 | /data/navidrome.db | 每天 |
| 配置 | /data/navidrome.toml | 变更时 |
| 音乐文件 | /music/ | 定期 |
| 缓存 | /data/cache/ | 可选 |

### 数据库备份

```bash
# SQLite backup (while running)
sqlite3 /data/navidrome.db ".backup '/backup/navidrome.db'"

# Docker backup
docker exec navidrome sqlite3 /data/navidrome.db ".backup '/data/backup.db'"
docker cp navidrome:/data/backup.db ./backup.db
```

### 性能优化

| 方面 | 操作 | 效果 |
|------|------|------|
| 数据库 | 定期 vacuum | 更快查询 |
| 缓存 | 清理旧缓存 | 释放空间 |
| 索引 | 为大型库启用 | 更快搜索 |
| 转码 | 缓存转码文件 | 节省 CPU |

### 监控

| 指标 | 工具 | 阈值 |
|------|------|------|
| CPU 使用率 | 系统监控 | < 80% |
| 内存 | 系统监控 | < 80% |
| 磁盘空间 | df 命令 | > 20% 可用 |
| 连接数 | Navidrome 日志 | < 100 |

### 故障排除

| 问题 | 可能原因 | 解决方案 |
|------|----------|----------|
| 找不到音乐 | 路径错误 | 检查 MusicFolder |
| 扫描慢 | 库太大 | 增加资源 |
| 播放问题 | 缺少编解码器 | 安装 FFmpeg |
| 连接被拒 | 防火墙 | 检查端口 |

---

## 总结

| 主题 | 核心要点 |
|------|----------|
| 安装 | 推荐 Docker 简化设置 |
| 配置 | 环境变量或配置文件 |
| 库 | 有序的文件夹结构有帮助 |
| 客户端 | 多款应用支持 Subsonic API |
| 用户 | 多用户支持及角色管理 |
| 维护 | 定期备份和监控 |


---

## 来源：media.md

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


---

## 来源：media2.md

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


---

## 来源：stream.md

## 简介

Spotube 是一个轻量级、开源的 Spotify 客户端，使用 Spotify API 获取元数据，使用公共音频源进行播放。它不需要 Spotify Premium 订阅即可播放。

| 属性 | 详情 |
|----------|--------|
| 仓库 | KRTirtho/spotube |
| 许可证 | BSD-4-Clause |
| 语言 | Dart, Flutter |
| 平台 | Windows, macOS, Linux, Android, iOS |
| API | Spotify Web API |

## 主要功能

| 功能 | 描述 |
|---------|-------------|
| 免费播放 | 无需 Spotify Premium 即可播放音乐 |
| 跨平台 | 支持桌面和移动端 |
| 轻量级 | 占用空间小，资源消耗低 |
| 无广告 | 播放过程中无广告 |
| 离线 | 下载曲目供离线收听 |
| 歌词 | 同步歌词显示 |
| 播放列表 | 完整的播放列表管理 |
| 搜索 | 搜索 Spotify 目录 |

## 安装

### Android

从 GitHub 发布页面下载 APK 或从 F-Droid 安装。

```bash
# 通过 F-Droid
# 将 Spotube 仓库添加到 F-Droid 或直接下载
```

### Windows

从 GitHub 发布页面下载安装程序。

### macOS

```bash
brew install --cask spotube
```

### Linux

```bash
# Flatpak
flatpak install com.github.KRTirtho.Spotube

# AppImage
# 从 GitHub 发布页面下载
```

## 设置

### 第 1 步：创建 Spotify 开发者账户

1. 访问 developer.spotify.com。
2. 使用您的 Spotify 账户登录。
3. 创建一个新应用程序。
4. 记下 Client ID 和 Client Secret。

### 第 2 步：配置 Spotube

1. 启动 Spotube。
2. 输入您的 Spotify Client ID 和 Client Secret。
3. 使用您的 Spotify 账户登录。
4. 配置音频源偏好。

| 设置 | 描述 |
|---------|-------------|
| Client ID | 来自 Spotify Developer Dashboard |
| Client Secret | 来自 Spotify Developer Dashboard |
| Audio Source（音频源） | YouTube, JioSaavn 或 Piped |
| Quality（质量） | Low, Medium, High |

## 音频源

Spotube 从公共源获取音频，而不是从 Spotify 串流服务获取。

| 源 | 描述 |
|--------|-------------|
| YouTube | 将曲目与 YouTube 视频匹配 |
| Piped | 注重隐私的 YouTube 前端 |
| JioSaavn | 印度音乐串流服务 |

## 使用 Spotube

### 播放控制

| 控制 | 描述 |
|---------|-------------|
| Play/Pause（播放/暂停） | 开始或停止播放 |
| Next（下一首） | 跳到下一首曲目 |
| Previous（上一首） | 返回上一首曲目 |
| Shuffle（随机） | 随机化曲目顺序 |
| Repeat（重复） | 重复当前曲目或播放列表 |
| Volume（音量） | 调整播放音量 |
| Queue（队列） | 查看和管理播放队列 |

### 库管理

| 功能 | 描述 |
|---------|-------------|
| Playlists（播放列表） | 创建、编辑和删除播放列表 |
| Liked Songs（喜欢的歌曲） | 保存喜欢的曲目 |
| Albums（专辑） | 浏览和保存专辑 |
| Artists（艺术家） | 关注艺术家并查看其唱片目录 |
| Search（搜索） | 搜索曲目、专辑、艺术家、播放列表 |

### 歌词

Spotube 可以为正在播放的曲目显示同步歌词。

| 功能 | 描述 |
|---------|-------------|
| Auto-fetch（自动获取） | 自动加载歌词 |
| Sync（同步） | 高亮当前行 |
| Manual Search（手动搜索） | 手动搜索歌词 |

## 配置选项

### 音频设置

| 设置 | 描述 |
|---------|-------------|
| Audio Source（音频源） | 选择元数据和音频提供者 |
| Audio Quality（音频质量） | 选择串流质量 |
| Normalize Volume（标准化音量） | 均衡曲目间的音量差异 |
| Crossfade（交叉淡入淡出） | 曲目间平滑过渡 |

### 外观设置

| 设置 | 描述 |
|---------|-------------|
| Theme（主题） | 浅色或深色模式 |
| Accent Color（强调色） | 自定义界面颜色 |
| Layout（布局） | 调整窗口布局 |

### 下载设置

| 设置 | 描述 |
|---------|-------------|
| Download Location（下载位置） | 保存下载文件的位置 |
| File Format（文件格式） | MP3, OGG 或原始格式 |
| Filename Pattern（文件名模式） | 下载文件名的模板 |

## 命令行使用

Spotube 可以在桌面平台上从命令行控制。

| 命令 | 描述 |
|---------|-------------|
| spotube | 启动应用程序 |
| spotube --version | 显示版本信息 |
| spotube --help | 显示帮助信息 |

## 故障排除

| 问题 | 解决方案 |
|-------|----------|
| 无音频 | 检查音频源设置 |
| 登录失败 | 验证 Client ID 和 Secret |
| 加载缓慢 | 切换音频源 |
| 缺少歌词 | 尝试不同的歌词提供者 |
| 崩溃 | 更新到最新版本 |

## 与 Spotify 客户端的比较

| 方面 | Spotube | Spotify |
|--------|---------|---------|
| 费用 | 免费 | 免费含广告或 Premium |
| 音频源 | 公共源 | Spotify 服务器 |
| 离线 | 支持 | 仅 Premium |
| 资源占用 | 轻量 | 较重 |
| 播客 | 不支持 | 支持 |
| 社交功能 | 有限 | 完整 |

## 隐私

| 方面 | 描述 |
|--------|-------------|
| 数据收集 | 与官方客户端相比极少 |
| 跟踪 | 无广告跟踪 |
| 音频源 | 使用公共、非 DRM 源 |

## 结论

Spotube 提供了一个轻量级且免费的替代方案来替代官方 Spotify 客户端。它非常适合希望在没有 Premium 订阅的情况下访问 Spotify 目录并偏好更注重隐私体验的用户。


---
