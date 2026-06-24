# Cobalt：媒体下载工具

## 简介

Cobalt 是一款现代化的开源媒体下载工具，允许用户从各种在线平台下载视频、音频和图片。它提供简洁、无广告的界面，没有追踪、弹窗或误导性按钮。Cobalt 支持数十个平台，提供灵活的质量和格式选项。

**核心功能：**

- 支持从 20+ 个平台下载
- 无广告或追踪
- 简洁极简的界面
- 多种格式和质量选项
- 提供 API 用于编程访问
- 可自托管
- 提供浏览器扩展
- 支持批量下载

---

## 支持的平台

| 平台 | 视频 | 音频 | 图片 | 备注 |
|----------|-------|-------|--------|-------|
| YouTube | 是 | 是 | 否 | 最高 8K |
| Twitter/X | 是 | 是 | 是 | 视频和图片 |
| Instagram | 是 | 否 | 是 | 帖子和故事 |
| TikTok | 是 | 是 | 否 | 有或无水印 |
| Reddit | 是 | 是 | 是 | 含音频的视频 |
| SoundCloud | 否 | 是 | 否 | 高质量音频 |
| Vimeo | 是 | 是 | 否 | 最高 4K |
| Twitch | 是 | 是 | 否 | 片段和 VOD |
| Facebook | 是 | 是 | 否 | 公开视频 |
| Pinterest | 否 | 否 | 是 | 全分辨率 |
| Tumblr | 是 | 是 | 是 | 所有媒体类型 |
| Vine Archive | 是 | 是 | 否 | 旧内容 |
| Streamable | 是 | 是 | 否 | 直接下载 |
| Rutube | 是 | 是 | 否 | 俄罗斯平台 |
| Bilibili | 是 | 是 | 否 | 中国平台 |
| OK.ru | 是 | 是 | 否 | 俄罗斯平台 |
| Dailymotion | 是 | 是 | 否 | 最高 1080p |

---

## 安装

### 使用 Docker（推荐）

运行 Cobalt 最简单的方式是使用 Docker：

```bash
docker pull ghcr.io/imputnet/cobalt:latest
docker run -d \
  --name cobalt \
  -p 9000:9000 \
  -e API_URL="http://localhost:9000" \
  ghcr.io/imputnet/cobalt:latest
```

### Docker Compose

创建 `docker-compose.yml` 文件：

```yaml
version: "3.8"
services:
  cobalt:
    image: ghcr.io/imputnet/cobalt:latest
    container_name: cobalt
    ports:
      - "9000:9000"
    environment:
      - API_URL=http://localhost:9000
    restart: unless-stopped
```

启动服务：

```bash
docker-compose up -d
```

### 从源码构建

依赖要求：

| 工具 | 版本 |
|------|---------|
| Node.js | 18.0+ |
| pnpm | 8.0+ |
| Git | 任意近期版本 |

步骤：

```bash
git clone https://github.com/imputnet/cobalt.git
cd cobalt
pnpm install
pnpm build
pnpm start
```

### 系统要求

| 组件 | 最低 | 推荐 |
|-----------|---------|-------------|
| CPU | 1 核 | 2 核 |
| 内存 | 512 MB | 1 GB |
| 存储 | 1 GB | 5 GB |
| 网络 | 10 Mbps | 100 Mbps |

---

## 自托管

### 配置选项

Cobalt 使用环境变量进行配置：

| 变量 | 描述 | 默认值 |
|----------|-------------|---------|
| `API_URL` | API 的公共 URL | 必填 |
| `API_PORT` | 监听端口 | 9000 |
| `API_NAME` | 实例名称 | cobalt |
| `CORS_WILDCARD` | 允许所有来源 | true |
| `PROCESSING_PRIORITY` | 进程的 Nice 值 | 10 |
| `DURATION_LIMIT` | 最大视频时长（秒） | 10800 |
| `TUNNEL_PROXY` | 隧道请求的代理 | 无 |
| `TUNNEL_IP_FAMILY` | 隧道的 IP 版本 | 0（自动） |
| `FREEBIND_CIDR` | FreeBind CIDR 范围 | 无 |

### Nginx 反向代理

```nginx
server {
    listen 80;
    server_name cobalt.example.com;

    location / {
        proxy_pass http://localhost:9000;
        proxy_set_header Host $host;
        proxy_set_header X-Real-IP $remote_addr;
        proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
        proxy_set_header X-Forwarded-Proto $scheme;
    }
}
```

### 使用 Let's Encrypt 配置 SSL/TLS

```bash
sudo apt install certbot python3-certbot-nginx
sudo certbot --nginx -d cobalt.example.com
```

---

## API 使用

### 基本请求

通过发送 POST 请求下载视频：

```bash
curl -X POST "http://localhost:9000/" \
  -H "Content-Type: application/json" \
  -d '{"url": "https://www.youtube.com/watch?v=example"}'
```

### 响应格式

**成功响应：**

```json
{
  "status": "tunnel",
  "url": "https://stream.example.com/video.mp4",
  "filename": "video.mp4"
}
```

**错误响应：**

```json
{
  "status": "error",
  "error": {
    "code": "error.invalid-url",
    "context": "The provided URL is not supported"
  }
}
```

### API 参数

| 参数 | 类型 | 描述 |
|-----------|------|-------------|
| `url` | string | 要下载的 URL（必填） |
| `vCodec` | string | 视频编解码器（h264、av1、vp9） |
| `vQuality` | string | 视频质量（144-4320） |
| `aFormat` | string | 音频格式（mp3、ogg、wav、opus） |
| `isAudioOnly` | boolean | 仅下载音频 |
| `filenameStyle` | string | 文件名样式（basic、pretty、basic） |

### 质量选项

| 质量值 | 分辨率 | 使用场景 |
|---------------|------------|----------|
| 144 | 256x144 | 最低质量，最小文件 |
| 240 | 426x240 | 低质量 |
| 360 | 640x360 | 标清 |
| 480 | 854x480 | DVD 画质 |
| 720 | 1280x720 | 高清 |
| 1080 | 1920x1080 | 全高清 |
| 1440 | 2560x1440 | 2K / QHD |
| 2160 | 3840x2160 | 4K UHD |
| 4320 | 7680x4320 | 8K UHD |
| max | 最高可用 | 最佳质量 |

### 音频格式选项

| 格式 | 质量 | 文件大小 | 兼容性 |
|--------|---------|-----------|---------------|
| mp3 | 良好 | 中等 | 通用 |
| ogg | 优秀 | 小 | 大多数播放器 |
| wav | 无损 | 大 | 通用 |
| opus | 优秀 | 小 | 现代播放器 |
| best | 不定 | 不定 | 不定 |

---

## Web 界面

### 使用官方实例

1. 在浏览器中打开 Cobalt 网站
2. 粘贴要下载的媒体 URL
3. 配置质量和格式选项
4. 点击下载按钮
5. 等待处理
6. 下载文件

### 界面功能

| 功能 | 描述 |
|---------|-------------|
| URL 输入 | 粘贴任何支持的 URL |
| 质量选择器 | 选择视频分辨率 |
| 格式选择器 | 选择输出格式 |
| 音频切换 | 切换到纯音频模式 |
| 下载历史 | 查看最近下载 |
| 暗色模式 | 自动主题切换 |

---

## 浏览器扩展

### 安装

安装 Cobalt 浏览器扩展以快速下载：

| 浏览器 | 安装方式 |
|---------|-------------------|
| Chrome | Chrome Web Store |
| Firefox | Firefox Add-ons |
| Edge | Edge Add-ons（Chrome 商店） |

### 扩展功能

| 功能 | 描述 |
|---------|-------------|
| 右键菜单 | 从上下文菜单下载 |
| 工具栏按钮 | 快速访问下载 |
| 自动检测 | 检测页面上的媒体 |
| 自定义实例 | 连接到自托管实例 |
| 键盘快捷键 | 快速下载热键 |

### 扩展配置

1. 点击扩展图标
2. 打开设置
3. 输入您的 Cobalt 实例 URL
4. 配置默认质量偏好
5. 启用或禁用自动检测

---

## 批量下载

### 使用 API

按顺序处理多个 URL：

```python
import requests

urls = [
    "https://youtube.com/watch?v=video1",
    "https://youtube.com/watch?v=video2",
    "https://youtube.com/watch?v=video3",
]

for url in urls:
    response = requests.post(
        "http://localhost:9000/",
        json={
            "url": url,
            "vQuality": "720",
            "aFormat": "mp3"
        }
    )
    data = response.json()
    if data["status"] == "tunnel":
        print(f"Download: {data['url']}")
```

### 速率限制

| 设置 | 值 |
|---------|-------|
| 每分钟请求数 | 20 |
| 并发下载数 | 3 |
| 冷却时间 | 10 秒 |

---

## 高级配置

### 编解码器选择

| 编解码器 | 质量 | 文件大小 | 兼容性 |
|-------|---------|-----------|---------------|
| h264 | 良好 | 中等 | 通用 |
| av1 | 优秀 | 小 | 现代设备 |
| vp9 | 优秀 | 中等 | 大多数浏览器 |

### 隧道模式

Cobalt 可以通过服务器隧道下载：

| 模式 | 描述 | 使用场景 |
|------|-------------|----------|
| 隧道 | 通过服务器串流 | 隐私、绕过限制 |
| 重定向 | 直接下载链接 | 更快、服务器负载更低 |

在 API 请求中设置：

```json
{
  "url": "https://youtube.com/watch?v=example",
  "downloadMode": "tunnel"
}
```

### 代理配置

通过代理路由请求：

```bash
export HTTP_PROXY="http://proxy:8080"
export HTTPS_PROXY="http://proxy:8080"
pnpm start
```

---

## 故障排除

### 常见问题

| 问题 | 原因 | 解决方案 |
|-------|-------|----------|
| 下载失败 | 不支持的 URL | 检查支持的平台列表 |
| 下载缓慢 | 服务器带宽 | 增加服务器资源 |
| 音频缺失 | 编解码器问题 | 尝试不同的音频格式 |
| API 错误 | 无效请求 | 检查请求格式 |
| 扩展不工作 | 实例 URL | 验证实例配置 |

### 错误代码

| 代码 | 描述 | 解决方案 |
|------|-------------|----------|
| `error.invalid-url` | URL 不支持 | 使用支持的平台 |
| `error.fetch.fail` | 获取内容失败 | 稍后重试 |
| `error.content.too-long` | 视频超过时长限制 | 缩短视频或增加限制 |
| `error.unsupported` | 功能不支持 | 检查平台功能 |
| `error.rate-limit` | 请求过多 | 等待后重试 |

### 日志

查看 Docker 日志：

```bash
docker logs cobalt
docker logs -f cobalt  # 跟踪日志
```

---

## 安全注意事项

| 事项 | 建议 |
|---------|---------------|
| 公共实例 | 设置速率限制和 CORS |
| 认证 | 为私用添加 API 密钥 |
| SSL/TLS | 生产环境始终使用 HTTPS |
| 更新 | 定期保持 Cobalt 更新 |
| 防火墙 | 限制访问可信 IP |

---

## 与同类工具对比

| 功能 | Cobalt | yt-dlp | JDownloader |
|---------|--------|--------|-------------|
| Web 界面 | 是 | 否 | 是 |
| API | 是 | 仅 CLI | 有限 |
| 可自托管 | 是 | 仅本地 | 否 |
| 浏览器扩展 | 是 | 否 | 是 |
| 批量下载 | 是 | 是 | 是 |
| 无广告 | 是 | 是 | 否 |
| 平台数 | 20+ | 1000+ | 100+ |
| 易用性 | 高 | 中等 | 中等 |

---

## 总结

Cobalt 为从热门平台下载媒体提供了现代化、注重隐私的解决方案。其简洁的界面、灵活的 API 和自托管能力使其适合个人使用和集成到其他应用程序中。该项目持续定期添加新平台和功能。
