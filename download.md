# 使用 Cobalt 进行媒体下载

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
