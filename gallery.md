# Ente 教程：自托管照片画廊

## 简介

Ente 是一个开源的端到端加密照片存储和分享平台。它以隐私为先，作为云照片服务的替代方案，支持自托管和跨平台客户端。

## 架构

| 组件 | 用途 |
|------|------|
| Museum | 后端 API 服务器 |
| PostgreSQL | 元数据库 |
| Object Storage | 照片和视频存储 |
| Ente 客户端 | iOS、Android、Web、桌面应用 |
| CLI | 命令行上传工具 |

## 系统要求

| 组件 | 最低配置 | 推荐配置 |
|------|---------|---------|
| CPU | 2 核 | 4 核 |
| 内存 | 2 GB | 4 GB |
| 存储 | 50 GB | 500 GB 或更多 |
| 数据库 | PostgreSQL 13 | PostgreSQL 15 |
| 网络 | 10 Mbps | 100 Mbps |

## Docker 安装

### Docker Compose 配置

```yaml
version: '3.8'
services:
  museum:
    image: ghcr.io/ente-io/server:latest
    ports:
      - "8080:8080"
    volumes:
      - ./museum-data:/data
    environment:
      - ENTE_API_ORIGIN=http://localhost:8080
    depends_on:
      - db
    restart: unless-stopped

  db:
    image: postgres:15
    volumes:
      - ./pg-data:/var/lib/postgresql/data
    environment:
      - POSTGRES_DB=ente_db
      - POSTGRES_USER=ente
      - POSTGRES_PASSWORD=changeme
    restart: unless-stopped
```

### 初始配置

在 `museum-data/config.yaml` 创建配置文件：

```yaml
db:
  host: db
  port: 5432
  name: ente_db
  user: ente
  password: changeme

s3:
  are_local_buckets: true
  use_path_style_urls: true
  b2-eu-cen:
    key: "local"
    secret: "local"
    endpoint: "http://minio:9000"
    region: "eu-central-2"
    bucket: "b2-eu-cen"
```

## 存储后端选项

| 后端 | 类型 | 配置复杂度 |
|------|------|-----------|
| 本地 MinIO | S3 兼容，自托管 | 简单 |
| AWS S3 | 云存储 | 中等 |
| Backblaze B2 | 云存储 | 中等 |
| Cloudflare R2 | 云存储 | 中等 |
| Wasabi | 云存储 | 中等 |

### MinIO 本地存储

```yaml
  minio:
    image: minio/minio
    ports:
      - "9000:9000"
      - "9001:9001"
    volumes:
      - ./minio-data:/data
    environment:
      - MINIO_ROOT_USER=minioadmin
      - MINIO_ROOT_PASSWORD=minioadmin
    command: server /data --console-address ":9001"
```

## 用户管理

| 操作 | 方法 | 端点 |
|------|------|------|
| 注册 | 邮箱验证 | `/users/verify/email` |
| 登录 | 邮箱加 OTP | `/users/two-factor/verify` |
| 家庭计划 | 多用户订阅 | 管理面板 |
| 删除账户 | 符合 GDPR | 设置页面 |

## 加密模型

Ente 对存储在服务器上的所有照片和视频使用端到端加密。

| 层级 | 算法 | 用途 |
|------|------|------|
| 文件加密 | XChaCha20 | 加密文件内容 |
| 密钥加密 | AES-256-GCM | 加密文件密钥 |
| 密钥交换 | X25519 | 在设备间共享密钥 |
| 认证 | SRP | 密码验证 |
| 恢复 | BIP39 | 恢复密钥生成 |

### 加密流程

| 步骤 | 操作 | 保护的数据 |
|------|------|-----------|
| 1 | 生成唯一文件密钥 | 每个文件的加密密钥 |
| 2 | 用密钥加密文件 | 照片或视频内容 |
| 3 | 用集合密钥加密文件密钥 | 密钥本身 |
| 4 | 将加密数据上传到服务器 | 服务器永远看不到明文 |
| 5 | 通过重新加密密钥来共享集合 | 接收者访问权限 |

## Web 客户端功能

| 功能 | 状态 | 说明 |
|------|------|------|
| 照片上传 | 支持 | 拖放界面 |
| 相册管理 | 支持 | 创建、编辑、分享相册 |
| 搜索 | 支持 | 设备端机器学习 |
| 地图视图 | 支持 | 基于位置的浏览 |
| 分享 | 支持 | 基于链接或基于用户 |
| 收藏 | 支持 | 快速访问集合 |
| 回收站 | 支持 | 30 天保留期 |

### 快捷键

| 操作 | 快捷键 |
|------|--------|
| 选择照片 | 单击或空格键 |
| 多选 | Shift + 单击 |
| 删除 | Delete 键 |
| 切换收藏 | F 键 |
| 下载 | D 键 |
| 显示信息 | I 键 |
| 放大/缩小 | 滚轮 |

## CLI 工具

### 安装

```bash
# macOS
brew install ente-cli

# Linux
curl -sL https://github.com/ente-io/ente/releases/latest/download/ente-cli-linux-amd64 \
  -o /usr/local/bin/ente-cli
chmod +x /usr/local/bin/ente-cli
```

### CLI 命令

| 命令 | 用途 |
|------|------|
| `ente account add` | 添加账户配置 |
| `ente upload` | 上传照片到账户 |
| `ente album list` | 列出所有相册 |
| `ente album create` | 创建新相册 |
| `ente version` | 显示 CLI 版本 |

### 批量上传示例

```bash
# 配置账户
ente account add --email user@example.com --password "pass" \
  --endpoint http://localhost:8080

# 上传目录到相册
ente upload --dir /path/to/photos --album "Vacation"

# 使用文件模式上传
ente upload --dir /path --include "*.jpg" --exclude "*.png"
```

## 移动应用

| 平台 | 应用商店 | 主要功能 |
|------|---------|---------|
| iOS | App Store | 完整功能，Live Photos |
| Android | Play Store / F-Droid | 完整功能 |
| 桌面 | 直接下载 | 基于 Web 或原生客户端 |

### 移动端专属功能

| 功能 | iOS | Android |
|------|-----|---------|
| 后台上传 | 是 | 是 |
| 人脸识别 | 是 | 是 |
| Live Photos | 是 | 否 |
| HEIC 支持 | 是 | 是 |
| 分享扩展 | 是 | 是 |

## 相册与分享

| 相册类型 | 分享方式 | 加密 |
|---------|---------|------|
| 个人 | 无 | 仅所有者 |
| 共享 | 邮箱邀请 | 共享密钥 |
| 公开链接 | URL 可选密码 | 链接密钥 |
| 收藏 | 无 | 仅所有者 |

### 分享工作流

| 步骤 | 操作 | 安全性 |
|------|------|--------|
| 1 | 创建分享链接 | 生成链接密钥 |
| 2 | 设置可选过期时间 | 限时访问 |
| 3 | 设置可选密码 | 密码保护 |
| 4 | 与接收者分享 URL | 用链接密钥加密 |
| 5 | 接收者在浏览器中查看 | 客户端解密 |

## 备份配置

| 设置 | 选项 | 建议 |
|------|------|------|
| 网络 | 仅 WiFi / 始终 | 仅 WiFi |
| 质量 | 原始 / 压缩 | 原始 |
| 计划 | 持续 / 手动 | 持续 |
| 排除项 | 文件夹或相册 | 截图文件夹 |

## 监控

```bash
# 检查服务器健康状态
curl http://localhost:8080/ping

# 查看服务器日志
docker logs ente-museum -f --tail 100

# 数据库统计
docker exec ente-db psql -U ente -d ente_db \
  -c "SELECT count(*) FROM files;"
```

## 性能优化

| 方面 | 设置 | 影响 |
|------|------|------|
| 缩略图 | 上传时预生成 | 更快的画廊加载 |
| CDN | Cloudflare 或 CloudFront | 全球内容分发 |
| 数据库 | 连接池 | 处理并发用户 |
| 存储 | 分片上传 | 大文件支持 |

## 故障排除

| 问题 | 原因 | 解决方案 |
|------|------|---------|
| 上传失败 | 文件过大 | 检查上传大小限制 |
| 同步卡住 | 网络问题 | 验证连接稳定性 |
| 登录失败 | 端点错误 | 确认配置中的 API URL |
| 加载缓慢 | 缺少缩略图 | 重新生成缩略图缓存 |

## 总结

Ente 提供了一个以隐私为核心的端到端加密照片存储解决方案。其自托管能力确保对个人照片的完全控制，而跨平台客户端在各设备间提供无缝体验。
