# Spotube：开源 Spotify 客户端

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
