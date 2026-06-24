# Navidrome：自托管音乐服务器指南

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
