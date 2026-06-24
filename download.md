# 下载工具

> 本文档整合了以下源文件：download.md, ytdl.md, proxy.md

---

## 来源：download.md

## 简介

Cobalt 是一个开源的媒体下载服务，支持众多平台的内容。它提供了简洁的 Web 界面和 API，用于从社交媒体和内容平台下载视频、音频和图片。本教程涵盖安装、配置、支持平台和使用模式。

## 架构概览

| 组件 | 描述 | 角色 |
|------|------|------|
| Web Frontend | Svelte 应用 | 用户界面 |
| API Server | Node.js 后端 | 处理请求 |
| Workers | 后台进程 | 下载和转换 |
| Cache | Redis | 速率限制和缓存 |

## 支持平台

### 视频平台

| 平台 | 内容类型 | 质量选项 |
|------|----------|----------|
| YouTube | 视频、Shorts、音乐 | 最高 8K |
| Vimeo | 视频 | 最高 4K |
| Dailymotion | 视频 | 最高 1080p |
| TikTok | 视频 | 原始质量 |
| Instagram | Reels、Stories、Posts | 原始质量 |
| Twitter/X | 视频、GIF | 原始质量 |
| Reddit | 视频、GIF | 原始质量 |

### 音频平台

| 平台 | 内容类型 | 质量选项 |
|------|----------|----------|
| SoundCloud | 曲目、专辑 | 原始质量 |
| YouTube Music | 歌曲、专辑 | 最高 256kbps |
| Bandcamp | 曲目、专辑 | 原始质量 |
| Spotify | 仅元数据 | 不适用 |

### 图片平台

| 平台 | 内容类型 | 质量选项 |
|------|----------|----------|
| Instagram | Posts、Stories | 原始质量 |
| Pinterest | Pins | 原始质量 |
| Tumblr | Posts | 原始质量 |
| Bluesky | Posts | 原始质量 |

## 安装

### Docker Compose 设置

```yaml
version: "3.8"

services:
  cobalt-api:
    image: ghcr.io/imputnet/cobalt:latest
    container_name: cobalt-api
    restart: unless-stopped
    ports:
      - "9000:9000"
    environment:
      - API_URL=http://localhost:9000
      - CORS_WILDCARD=1
      - API_AUTH_REQUIRED=0
      - TURNSTILE_SECRET=optional

  cobalt-frontend:
    image: ghcr.io/imputnet/cobalt-frontend:latest
    container_name: cobalt-frontend
    restart: unless-stopped
    ports:
      - "3000:3000"
    environment:
      - API_URL=http://localhost:9000
```

### 环境变量

| 变量 | 描述 | 默认值 |
|------|------|--------|
| API_URL | 后端 API 地址 | http://localhost:9000 |
| CORS_WILDCARD | 允许所有来源 | 0 |
| API_AUTH_REQUIRED | 要求认证 | 0 |
| TURNSTILE_SECRET | Cloudflare Turnstile 密钥 | 空 |
| PROCESSING_PRIORITY | FFmpeg 优先级 | 10 |
| MAX_FILE_SIZE | 最大下载大小 | 1 GB |
| TTL_CACHE | 缓存时长 | 300 秒 |

### 初始设置

1. 访问 `http://localhost:3000`
2. 在输入框中粘贴支持的 URL
3. 配置下载选项
4. 点击下载

## 使用 Web 界面

### 输入方式

| 方式 | 描述 | 示例 |
|------|------|------|
| URL paste | 输入内容 URL | 粘贴 YouTube 链接 |
| Direct input | 手动输入 URL | 在框中输入 URL |
| Browser extension | 自动检测 | 点击扩展按钮 |

### 下载选项

| 选项 | 描述 | 值 |
|------|------|-----|
| Quality | 视频分辨率 | 360p, 480p, 720p, 1080p, 4K, 8K |
| Audio only | 提取音轨 | 是/否 |
| Format | 文件格式 | mp4, webm, mp3, ogg |
| Filename | 自定义文件名 | 文本输入 |
| Save metadata | 嵌入元数据 | 是/否 |

### 质量选择

| 质量 | 使用场景 | 文件大小 |
|------|----------|----------|
| 360p | 快速预览、慢速连接 | 小 |
| 720p | 标准观看 | 中 |
| 1080p | 高质量观看 | 大 |
| 4K | 最高质量 | 非常大 |
| Audio only | 音乐提取 | 小 |

## API 使用

### API 端点

```
POST /api/json
```

### 请求体

```json
{
  "url": "https://www.youtube.com/watch?v=example",
  "quality": 720,
  "isAudioOnly": false,
  "filenameStyle": "basic"
}
```

### 请求参数

| 参数 | 类型 | 描述 | 默认值 |
|------|------|------|--------|
| url | string | 内容 URL | 必填 |
| quality | number | 视频质量 | 720 |
| isAudioOnly | boolean | 仅提取音频 | false |
| filenameStyle | string | 文件名格式 | basic |
| downloadMode | string | 下载类型 | auto |

### 响应格式

```json
{
  "status": "tunnel",
  "url": "https://download-url.example.com/file.mp4",
  "filename": "video_title.mp4"
}
```

### 响应状态

| 状态 | 含义 | 操作 |
|------|------|------|
| tunnel | 直接下载 URL 可用 | 使用提供的 URL |
| redirect | 重定向到下载 | 跟随 URL |
| error | 请求失败 | 检查错误消息 |
| rate-limit | 请求过多 | 等待并重试 |

### API 示例

```bash
# 下载视频
curl -X POST http://localhost:9000/api/json \
  -H "Content-Type: application/json" \
  -d '{"url": "https://youtube.com/watch?v=example", "quality": 1080}'

# 仅音频
curl -X POST http://localhost:9000/api/json \
  -H "Content-Type: application/json" \
  -d '{"url": "https://youtube.com/watch?v=example", "isAudioOnly": true}'
```

## 浏览器扩展

### 安装

| 浏览器 | 商店 | 安装 |
|--------|------|------|
| Chrome | Chrome Web Store | 搜索 "Cobalt" |
| Firefox | Add-ons | 搜索 "Cobalt" |
| Edge | Edge Add-ons | 搜索 "Cobalt" |

### 扩展功能

| 功能 | 描述 |
|------|------|
| Auto-detect | 识别支持的 URL |
| Quick download | 一键下载 |
| Context menu | 右键集成 |
| Settings sync | 与自托管实例同步 |

## 高级配置

### 认证

启用 API 认证以保护您的实例：

```yaml
environment:
  - API_AUTH_REQUIRED=1
  - API_AUTH_KEY=your-secret-key
```

在 API 请求中包含密钥：

```bash
curl -X POST http://localhost:9000/api/json \
  -H "Content-Type: application/json" \
  -H "Authorization: Bearer your-secret-key" \
  -d '{"url": "https://youtube.com/watch?v=example"}'
```

### 速率限制

| 设置 | 描述 | 默认值 |
|------|------|--------|
| Rate limit window | 时间段 | 60 秒 |
| Max requests per window | 请求数 | 10 |
| Max concurrent downloads | 并行下载 | 3 |

### 代理配置

通过代理路由下载：

```yaml
environment:
  - HTTP_PROXY=http://proxy:8080
  - HTTPS_PROXY=http://proxy:8080
  - NO_PROXY=localhost,127.0.0.1
```

### Cookie 支持

为需要认证的内容提供 Cookie：

```yaml
# 在 docker-compose.yml 中
volumes:
  - ./cookies.txt:/app/cookies.txt
environment:
  - COOKIE_PATH=/app/cookies.txt
```

## 内容处理

### 视频处理

| 处理 | 描述 | 工具 |
|------|------|------|
| Transcoding | 格式转换 | FFmpeg |
| Remuxing | 容器更换 | FFmpeg |
| Quality selection | 分辨率匹配 | FFmpeg |
| HDR handling | 色调映射 | FFmpeg |

### 音频处理

| 处理 | 描述 | 输出 |
|------|------|------|
| Extraction | 从视频提取音频 | mp3, ogg, wav |
| Normalization | 音量调整 | 一致的电平 |
| Metadata | 嵌入标签 | 标题、艺术家 |

## 自托管注意事项

### 服务器要求

| 用户 | CPU | RAM | 存储 | 带宽 |
|------|-----|-----|------|------|
| 1-5 | 1 核 | 1 GB | 10 GB | 100 GB/月 |
| 5-20 | 2 核 | 2 GB | 50 GB | 500 GB/月 |
| 20-100 | 4 核 | 4 GB | 200 GB | 2 TB/月 |
| 100+ | 8 核 | 8 GB | 500 GB | 5+ TB/月 |

### 安全加固

| 实践 | 实施方式 | 优先级 |
|------|----------|--------|
| HTTPS | 带 TLS 的反向代理 | 高 |
| Authentication | 启用 API 认证 | 高 |
| Rate limiting | 配置限制 | 高 |
| IP filtering | 允许特定 IP | 中 |
| Uptime monitoring | 健康检查 | 中 |

## 反向代理设置

### Nginx 配置

```nginx
server {
    listen 443 ssl;
    server_name cobalt.example.com;

    ssl_certificate /path/to/cert.pem;
    ssl_certificate_key /path/to/key.pem;

    location / {
        proxy_pass http://localhost:3000;
        proxy_set_header Host $host;
        proxy_set_header X-Real-IP $remote_addr;
    }

    location /api/ {
        proxy_pass http://localhost:9000;
        proxy_set_header Host $host;
        proxy_set_header X-Real-IP $remote_addr;
    }
}
```

### Caddy 配置

```
cobalt.example.com {
    reverse_proxy / localhost:3000
    reverse_proxy /api/* localhost:9000
}
```

## 故障排除

| 问题 | 可能原因 | 解决方案 |
|------|----------|----------|
| 下载失败 | 平台变更 | 更新到最新版本 |
| 下载慢 | 服务器带宽 | 检查网络限制 |
| 音频质量 | 源限制 | 尝试不同源 |
| API 错误 | 无效 URL | 验证 URL 格式 |
| CORS 错误 | 来源配置错误 | 设置 CORS_WILDCARD=1 |

## 总结

Cobalt 提供了一个简洁高效的解决方案，用于从支持的平台下载媒体。其 Web 界面和 API 使其对普通用户和开发者都易于使用。

关键实践：

- 使用 Docker 部署以便管理
- 为公共实例配置认证
- 使用 API 实现自动化下载工作流
- 设置适当的速率限制以管理资源使用
- 保持实例更新以获得持续的平台支持
- 使用带 HTTPS 的反向代理以安全访问


---

## 来源：ytdl.md

## 简介

yt-dlp 是一个功能丰富的命令行工具，用于从 YouTube 和数百个其他网站下载视频。它是 youtube-dl 的一个分支，具有额外功能和活跃开发。本教程涵盖安装、使用、配置和高级功能。

## yt-dlp 与 youtube-dl 对比

| 功能 | yt-dlp | youtube-dl |
|------|--------|------------|
| 速度 | 更快（多线程） | 较慢 |
| 开发 | 活跃 | 缓慢 |
| SponsorBlock | 内置 | 需要插件 |
| 格式选择 | 高级 | 基础 |
| 输出模板 | 扩展 | 基础 |
| 插件 | 是 | 有限 |
| Cookies | 多浏览器支持 | 手动提取 |

## 安装

### 包管理器

| 平台 | 命令 |
|------|------|
| pip | pip install yt-dlp |
| Homebrew（macOS） | brew install yt-dlp |
| Winget（Windows） | winget install yt-dlp |
| Chocolatey（Windows） | choco install yt-dlp |
| Arch Linux | pacman -S yt-dlp |
| Debian/Ubuntu | sudo apt install yt-dlp |
| Fedora | sudo dnf install yt-dlp |

### 手动安装

```bash
# 下载二进制文件
wget https://github.com/yt-dlp/yt-dlp/releases/latest/download/yt-dlp
chmod +x yt-dlp
sudo mv yt-dlp /usr/local/bin/
```

### 更新

```bash
yt-dlp -U
# 或
pip install -U yt-dlp
```

## 基本使用

### 下载视频

```bash
# 简单下载
yt-dlp https://www.youtube.com/watch?v=VIDEO_ID

# 仅下载音频
yt-dlp -x https://www.youtube.com/watch?v=VIDEO_ID

# 下载指定质量
yt-dlp -f "bestvideo[height<=1080]+bestaudio" URL
```

### 常用命令

| 命令 | 描述 |
|------|------|
| yt-dlp URL | 下载视频 |
| yt-dlp -x URL | 仅提取音频 |
| yt-dlp -f FORMAT URL | 下载指定格式 |
| yt-dlp --list-formats URL | 列出可用格式 |
| yt-dlp -o "OUTPUT" URL | 设置输出文件名 |
| yt-dlp --cookies-from-browser chrome URL | 使用浏览器 Cookies |

## 格式选择

### 格式过滤器

| 过滤器 | 示例 | 描述 |
|--------|------|------|
| height | height<=720 | 最大分辨率 |
| width | width>=1280 | 最小宽度 |
| fps | fps>=30 | 最小帧率 |
| codec | vcodec:h264 | 指定编码器 |
| ext | ext:mp4 | 文件扩展名 |
| filesize | filesize<100M | 文件大小限制 |
| tbr | tbr>=1000 | 总码率 |

### 格式示例

```bash
# 最佳质量，最高 1080p
yt-dlp -f "bestvideo[height<=1080]+bestaudio/best[height<=1080]" URL

# 仅 MP4
yt-dlp -f "bestvideo[ext=mp4]+bestaudio[ext=m4a]/best[ext=mp4]" URL

# 最差质量（节省带宽）
yt-dlp -f "worst" URL

# 仅音频，最佳质量
yt-dlp -f "bestaudio" URL

# 指定格式 ID
yt-dlp -f "137+140" URL
```

### 格式选择优先级

| 优先级 | 选择 |
|--------|------|
| 1 | 请求的格式（-f） |
| 2 | 默认格式（best） |
| 3 | 单一格式（无需合并） |
| 4 | 最佳视频 + 最佳音频 |

## 输出模板

### 模板变量

| 变量 | 描述 | 示例 |
|------|------|------|
| %(title)s | 视频标题 | My Video |
| %(id)s | 视频 ID | dQw4w9WgXcQ |
| %(ext)s | 扩展名 | mp4 |
| %(uploader)s | 上传者名称 | Channel Name |
| %(upload_date)s | 上传日期 | 20240115 |
| %(resolution)s | 分辨率 | 1920x1080 |
| %(fps)s | 帧率 | 30 |
| %(duration)s | 时长（秒） | 300 |
| %(playlist)s | 播放列表名称 | My Playlist |
| %(playlist_index)s | 播放列表中的索引 | 1 |

### 输出示例

```bash
# 包含上传者和标题
yt-dlp -o "%(uploader)s - %(title)s.%(ext)s" URL

# 按上传者组织
yt-dlp -o "%(uploader)s/%(title)s.%(ext)s" URL

# 包含日期
yt-dlp -o "%(upload_date)s_%(title)s.%(ext)s" URL

# 播放列表带索引
yt-dlp -o "%(playlist)s/%(playlist_index)s_%(title)s.%(ext)s" URL
```

## 播放列表

### 播放列表操作

| 操作 | 命令 |
|------|------|
| 下载整个播放列表 | yt-dlp PLAYLIST_URL |
| 下载范围 | yt-dlp --playlist-start 1 --playlist-end 10 URL |
| 下载特定项目 | yt-dlp --playlist-items 1,3,5 URL |
| 反转顺序 | yt-dlp --playlist-reverse URL |
| 扁平播放列表 | yt-dlp --flat-playlist URL |

### 播放列表选项

| 选项 | 描述 |
|------|------|
| --playlist-start N | 从第 N 项开始 |
| --playlist-end N | 到第 N 项结束 |
| --playlist-items ITEMS | 特定项目（1,3,5） |
| --playlist-reverse | 反转下载顺序 |
| --lazy-playlist | 收到时即处理条目 |

## 字幕

### 字幕操作

| 操作 | 命令 |
|------|------|
| 下载字幕 | yt-dlp --write-subs URL |
| 下载自动字幕 | yt-dlp --write-auto-subs URL |
| 特定语言 | yt-dlp --sub-langs en,es URL |
| 嵌入字幕 | yt-dlp --embed-subs URL |
| 字幕格式 | yt-dlp --sub-format srt URL |

### 字幕语言

| 代码 | 语言 |
|------|------|
| en | 英语 |
| es | 西班牙语 |
| fr | 法语 |
| de | 德语 |
| ja | 日语 |
| zh | 中文 |
| ko | 韩语 |
| all | 所有可用 |

## SponsorBlock

SponsorBlock 跳过 YouTube 视频中的赞助片段。

| 类别 | 描述 |
|------|------|
| sponsor | 付费推广 |
| intro | 间歇/动画 |
| outro | 结尾卡/片尾 |
| selfpromo | 自我推广 |
| preview | 预告/回顾 |
| interaction | 点赞/订阅提醒 |
| music_offtopic | 非音乐部分 |

### SponsorBlock 使用

```bash
# 移除赞助片段
yt-dlp --sponsorblock-remove sponsor URL

# 移除多个类别
yt-dlp --sponsorblock-remove "sponsor,intro,outro" URL

# 标记而非移除
yt-dlp --sponsorblock-mark "all" URL
```

## 认证

### Cookie 方式

| 方式 | 命令 |
|------|------|
| 浏览器 Cookies | --cookies-from-browser chrome |
| Cookie 文件 | --cookies cookies.txt |
| 用户名/密码 | -u USER -p PASS |

### 年龄限制内容

```bash
yt-dlp --cookies-from-browser chrome URL
```

## 配置文件

### 配置位置

| 平台 | 路径 |
|------|------|
| Linux | ~/.config/yt-dlp/config |
| macOS | ~/Library/Application Support/yt-dlp/config |
| Windows | %APPDATA%\yt-dlp\config.txt |

### 示例配置

```
# 输出模板
-o "%(uploader)s/%(title)s.%(ext)s"

# 最佳质量
-f "bestvideo[height<=2160]+bestaudio/best"

# 嵌入元数据
--embed-metadata

# 嵌入缩略图
--embed-thumbnail

# 字幕
--write-subs
--write-auto-subs
--sub-langs en

# SponsorBlock
--sponsorblock-remove sponsor,intro,outro
```

## 后处理

### 后处理器选项

| 选项 | 描述 |
|------|------|
| -x | 提取音频 |
| --audio-format FORMAT | 转换为 mp3、flac 等 |
| --audio-quality QUALITY | 0（最佳）到 10（最差） |
| --embed-metadata | 嵌入元数据 |
| --embed-thumbnail | 嵌入缩略图 |
| --embed-subs | 嵌入字幕 |
| --merge-output-format FORMAT | 合并格式（mp4、mkv） |

### 音频转换

```bash
# 转换为 MP3
yt-dlp -x --audio-format mp3 URL

# 转换为 FLAC
yt-dlp -x --audio-format flac URL

# 最佳音频质量
yt-dlp -x --audio-format mp3 --audio-quality 0 URL
```

## 缩略图

| 选项 | 描述 |
|------|------|
| --write-thumbnail | 将缩略图保存为文件 |
| --embed-thumbnail | 嵌入到媒体文件中 |
| --convert-thumbnails FORMAT | 转换为 jpg/png |

## 批量下载

### 从文件

```bash
# 从文件下载所有 URL
yt-dlp -a urls.txt

# 每行一个 URL
# 以 # 开头的行为注释
```

### 使用过滤器

```bash
# 仅下载匹配的 URL
yt-dlp --match-filter "duration < 600" URL
yt-dlp --match-filter "view_count > 1000000" URL
yt-dlp --match-filter "upload_date >= 20240101" URL
```

## 网络选项

| 选项 | 描述 |
|------|------|
| --proxy URL | 使用 HTTP/SOCKS 代理 |
| --geo-bypass | 绕过地理限制 |
| --geo-bypass-country CODE | 为特定国家绕过 |
| --socket-timeout SECONDS | 连接超时 |
| --retries RETRIES | 重试次数 |
| --limit-rate RATE | 下载速度限制 |

## 快捷键（配合 --console-title）

| 按键 | 操作 |
|------|------|
| q | 退出下载 |
| Ctrl+C | 中断当前下载 |

## 故障排除

| 问题 | 原因 | 解决方案 |
|------|------|---------|
| "Sign in to confirm" | 机器人检测 | 使用 --cookies-from-browser |
| 下载缓慢 | 限速 | 使用 --extractor-args |
| 格式不可用 | 地理限制 | 使用 --geo-bypass |
| 年龄限制 | 年龄门槛 | 使用 Cookies |
| 私有视频 | 访问被拒 | 使用有访问权限的 Cookies |

## 支持的网站

yt-dlp 支持 1000+ 个网站，包括：

| 类别 | 网站 |
|------|------|
| 视频 | YouTube、Vimeo、Dailymotion |
| 社交 | Twitter、Instagram、TikTok、Reddit |
| 音乐 | SoundCloud、Bandcamp、Spotify（有限） |
| 直播 | Twitch、Picarto |
| 新闻 | BBC、CNN、ARD、ZDF |
| 教育 | Khan Academy、Coursera |

## 总结

yt-dlp 是目前最强大的命令行视频下载工具。其广泛的格式选择、SponsorBlock 集成、播放列表处理和广泛的网站支持使其成为视频下载的标准工具。配置文件和输出模板为常规使用提供了强大的自动化能力。


---

## 来源：proxy.md

## 简介

AllInOne 是一组媒体代理工具和配置，用于优化媒体流、下载和代理。本教程涵盖媒体代理服务的设置、配置和使用模式。

## 概览

| 功能 | 描述 |
|------|------|
| 媒体代理 | 通过你的服务器代理媒体流 |
| CDN 集成 | 通过 CDN 分发媒体 |
| 格式转换 | 实时转换媒体格式 |
| 缓存 | 缓存频繁访问的媒体 |
| 速率限制 | 控制带宽使用 |
| 访问控制 | 限制媒体访问 |

## 系统要求

| 组件 | 最低要求 | 推荐配置 |
|------|---------|---------|
| CPU | 2 核 | 4+ 核 |
| 内存 | 1 GB | 4 GB |
| 磁盘 | 10 GB | 100 GB SSD |
| 网络 | 100 Mbps | 1 Gbps |
| 操作系统 | Linux | Ubuntu 22.04 LTS |

## 安装

### Docker 设置

```bash
docker run -d \
  --name media-proxy \
  -p 8080:8080 \
  -v ./config:/config \
  -v ./cache:/cache \
  media-proxy:latest
```

### Nginx 代理配置

```nginx
server {
    listen 80;
    server_name media.example.com;

    location /proxy/ {
        proxy_pass https://upstream-media-server/;
        proxy_set_header Host $host;
        proxy_set_header X-Real-IP $remote_addr;
        proxy_buffering on;
        proxy_cache media_cache;
        proxy_cache_valid 200 24h;
    }

    proxy_cache_path /var/cache/nginx/media
        levels=1:2
        keys_zone=media_cache:100m
        max_size=10g
        inactive=60m;
}
```

## 代理类型

### 正向代理

| 功能 | 描述 |
|------|------|
| 方向 | 客户端到服务器 |
| 用例 | 隐藏客户端身份 |
| 认证 | 用户名/密码 |
| 缓存 | 响应缓存 |

### 反向代理

| 功能 | 描述 |
|------|------|
| 方向 | 服务端 |
| 用例 | 负载均衡、SSL 终止 |
| 认证 | 服务端认证 |
| 缓存 | 内容缓存 |

### 透明代理

| 功能 | 描述 |
|------|------|
| 方向 | 无需配置即可拦截 |
| 用例 | 网络级代理 |
| 认证 | 基于 IP |
| 缓存 | 网络级缓存 |

## 媒体格式

### 支持的格式

| 格式 | 类型 | 扩展名 |
|------|------|--------|
| MP4 | 视频 | .mp4 |
| HLS | 流媒体 | .m3u8、.ts |
| DASH | 流媒体 | .mpd |
| MP3 | 音频 | .mp3 |
| FLAC | 音频 | .flac |
| AAC | 音频 | .aac |
| WebM | 视频 | .webm |
| MKV | 视频 | .mkv |

### 流媒体协议

| 协议 | 描述 | 用例 |
|------|------|------|
| HLS | HTTP Live Streaming | Apple 设备、Web |
| DASH | 动态自适应流 | 跨平台 |
| RTMP | 实时消息协议 | 直播 |
| RTSP | 实时流协议 | IP 摄像头 |
| WebRTC | Web 实时通信 | 低延迟 |

## 缓存策略

### 缓存层级

| 层级 | 位置 | 持续时间 |
|------|------|---------|
| 浏览器 | 客户端缓存 | 分钟到小时 |
| CDN | 边缘服务器 | 小时到天 |
| 代理 | 你的服务器 | 小时到周 |
| 源站 | 源服务器 | 永久 |

### 缓存配置

| 设置 | 值 | 用途 |
|------|-----|------|
| max_size | 10 GB | 最大缓存大小 |
| inactive | 60 分钟 | 驱逐前的时间 |
| valid 200 | 24 小时 | OK 响应的缓存时间 |
| valid 404 | 1 分钟 | 未找到的缓存时间 |

## 速率限制

### 速率限制层级

| 层级 | 请求数/分钟 | 带宽 |
|------|-----------|------|
| Free | 60 | 1 Mbps |
| Basic | 300 | 10 Mbps |
| Premium | 1000 | 100 Mbps |
| Enterprise | 无限制 | 无限制 |

### Nginx 速率限制

```nginx
limit_req_zone $binary_remote_addr zone=media:10m rate=10r/s;

location /media/ {
    limit_req zone=media burst=20 nodelay;
    proxy_pass http://backend;
}
```

## 访问控制

### 认证方式

| 方式 | 描述 |
|------|------|
| API Key | 查询参数或头部 |
| Token | JWT 或 Bearer 令牌 |
| IP Whitelist | 允许的 IP 地址 |
| Referrer | 检查 referer 头部 |
| Signed URL | 有时限的 URL |

### 签名 URL 示例

```
https://media.example.com/video.mp4?token=abc123&expires=1700000000
```

| 参数 | 用途 |
|------|------|
| token | HMAC 签名 |
| expires | Unix 时间戳过期时间 |

## 转码

### FFmpeg 集成

| 操作 | 命令 |
|------|------|
| 转码 | ffmpeg -i input.mp4 -c:v h264 output.mp4 |
| 缩放 | ffmpeg -i input.mp4 -vf scale=1280:720 output.mp4 |
| 提取音频 | ffmpeg -i input.mp4 -vn output.mp3 |
| HLS 转换 | ffmpeg -i input.mp4 -hls_time 10 output.m3u8 |

### 转码配置

| 配置 | 分辨率 | 码率 | 用例 |
|------|--------|------|------|
| 4K | 3840x2160 | 20 Mbps | 高级品质 |
| 1080p | 1920x1080 | 8 Mbps | 标准品质 |
| 720p | 1280x720 | 4 Mbps | 移动/带宽 |
| 480p | 854x480 | 2 Mbps | 低带宽 |
| 仅音频 | N/A | 128 kbps | 音乐流 |

## 监控

### 需要跟踪的指标

| 指标 | 工具 | 阈值 |
|------|------|------|
| 请求速率 | Prometheus | < 1000 req/s |
| 错误率 | Prometheus | < 1% |
| 缓存命中率 | Nginx | > 80% |
| 带宽 | vnStat | < 80% 容量 |
| 磁盘使用 | df | < 80% 满 |
| 延迟 | ping | < 100ms |

### 日志

| 日志 | 内容 |
|------|------|
| Access log | 请求 URL、状态、大小 |
| Error log | 错误、警告 |
| Cache log | 缓存命中、未命中 |
| Transcode log | 转换状态 |

## 安全

| 实践 | 实施 |
|------|------|
| HTTPS | 使用 Let's Encrypt 的 SSL 证书 |
| 速率限制 | Nginx limit_req 模块 |
| 输入验证 | 清理 URL 和参数 |
| 访问控制 | 基于令牌的认证 |
| CORS | 限制允许的来源 |
| CSP | 内容安全策略头部 |

## 故障排除

| 问题 | 原因 | 解决方案 |
|------|------|---------|
| 流媒体缓慢 | 带宽低 | 启用缓存，使用 CDN |
| 缓冲 | 服务器过载 | 添加速率限制，优化 |
| 403 Forbidden | 访问控制 | 检查认证 |
| 缓存未命中 | 配置错误 | 验证缓存设置 |
| 转码失败 | FFmpeg 错误 | 检查输入格式 |
| 高延迟 | 网络问题 | 使用更近的 CDN 边缘 |

## 总结

媒体代理解决方案为媒体流提供内容分发、缓存和访问控制。正确配置缓存、速率限制和安全措施可确保可靠高效的媒体传输。与 FFmpeg 等转码工具的集成支持格式转换和自适应比特率流。


---
