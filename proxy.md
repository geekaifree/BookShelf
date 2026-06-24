# AllInOne：媒体代理教程

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
