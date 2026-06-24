# yt-dlp：视频下载教程

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
