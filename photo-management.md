# 照片管理

> 本文档整合了以下源文件：photos.md, gallery.md, gallery2.md, gallery3.md

---

## 来源：photos.md

## 简介

LibrePhotos 是一个自托管的照片管理应用程序，使用机器学习自动组织照片。它提供人脸识别、物体检测和场景分类。

| 属性 | 详情 |
|----------|--------|
| 仓库 | LibrePhotos/librephotos |
| 许可证 | AGPL-3.0 |
| 语言 | Python, React |
| 平台 | 基于 Web |
| 数据库 | PostgreSQL |

## 主要功能

| 功能 | 描述 |
|---------|-------------|
| 自动组织 | 基于 ML 的照片分类 |
| 人脸识别 | 识别和分组人物 |
| 物体检测 | 检测照片中的物体 |
| 场景分类 | 按场景类型分类 |
| 地图视图 | 在地图上显示照片 |
| 时间线 | 按时间顺序浏览照片 |
| 搜索 | 全文和视觉搜索 |
| 相册 | 创建自定义相册 |
| 分享 | 分享照片和相册 |

## 使用 Docker 安装

### Docker Compose 配置

```yaml
version: "3.8"

services:
  proxy:
    image: reallibrephotos/librephotos-proxy:latest
    ports:
      - "80:80"
    volumes:
      - ./nginx.conf:/etc/nginx/conf.d/default.conf
    depends_on:
      - backend

  backend:
    image: reallibrephotos/librephotos:latest
    environment:
      SECRET_KEY: your-secret-key
      DB_HOST: db
      DB_NAME: librephotos
      DB_USER: librephotos
      DB_PASS: secret
      REDIS_HOST: redis
    volumes:
      - photos:/data
      - ./protected_media:/srv/protected_media
    depends_on:
      - db
      - redis

  db:
    image: postgres:15
    environment:
      POSTGRES_DB: librephotos
      POSTGRES_USER: librephotos
      POSTGRES_PASSWORD: secret
    volumes:
      - db_data:/var/lib/postgresql/data

  redis:
    image: redis:7-alpine
    volumes:
      - redis_data:/data

volumes:
  photos:
  db_data:
  redis_data:
```

### 初始设置

1. 运行 `docker compose up -d`。
2. 访问 `http://localhost`。
3. 创建管理员账户。
4. 配置照片目录。
5. 开始初始扫描。

## 照片管理

### 添加照片

| 方法 | 描述 |
|--------|-------------|
| File Upload（文件上传） | 通过 Web 界面上传 |
| Directory Scan（目录扫描） | 指向服务器上的目录 |
| Automatic Scan（自动扫描） | 定期扫描新照片 |

### 支持的格式

| 格式 | 支持程度 |
|--------|---------------|
| JPEG | 完全支持 |
| PNG | 完全支持 |
| HEIC/HEIF | 完全支持 |
| TIFF | 完全支持 |
| RAW (CR2, NEF, ARW) | 基本支持 |
| GIF | 仅静态帧 |
| WebP | 完全支持 |
| MOV/MP4 | 视频缩略图提取 |

## 机器学习功能

### 人脸识别

| 步骤 | 描述 |
|------|-------------|
| Detection（检测） | 在照片中找到人脸 |
| Clustering（聚类） | 将相似的人脸分组 |
| Labeling（标注） | 为人脸组分配名称 |
| Training（训练） | 随时间提高识别率 |

### 物体检测

检测照片中的常见物体。

| 物体 | 示例 |
|--------|----------|
| Animals（动物） | 狗、猫、鸟、马 |
| Vehicles（车辆） | 汽车、自行车、飞机 |
| Food（食物） | 披萨、蛋糕、水果 |
| Nature（自然） | 树、花、山 |
| Indoor（室内） | 椅子、桌子、笔记本电脑 |

### 场景分类

| 场景 | 示例 |
|-------|----------|
| Landscape（风景） | 山脉、海滩、森林 |
| Urban（城市） | 城市、街道、建筑 |
| Indoor（室内） | 房间、办公室、餐厅 |
| Sports（运动） | 体育场、球场 |
| Social（社交） | 派对、婚礼、聚会 |

## 浏览照片

### 时间线视图

照片按时间顺序显示，按日期和位置分组。

### 地图视图

带有 GPS 数据的照片显示在交互式地图上。

| 功能 | 描述 |
|---------|-------------|
| Clustering（聚类） | 将附近的照片分组 |
| Heatmap（热力图） | 显示照片密度 |
| Filter（过滤） | 按日期或相册过滤 |

### 搜索

| 搜索类型 | 描述 |
|-------------|-------------|
| Text（文本） | 搜索描述和标签 |
| Face（人脸） | 查找特定人物的照片 |
| Object（物体） | 查找包含物体的照片 |
| Location（位置） | 按 GPS 坐标搜索 |
| Date（日期） | 按日期范围过滤 |
| Rating（评分） | 按星级评分过滤 |

## 相册

| 相册类型 | 描述 |
|------------|-------------|
| User Album（用户相册） | 用户手动创建 |
| Auto Album（自动相册） | 自动生成 |
| Shared Album（共享相册） | 与其他用户共享 |

### 创建相册

1. 从任何视图选择照片。
2. 点击 "Add to Album"。
3. 选择现有相册或创建新相册。
4. 设置相册封面和描述。

## 分享

| 分享类型 | 描述 |
|------------|-------------|
| Public Link（公开链接） | 生成可分享的 URL |
| User Share（用户分享） | 与特定用户分享 |
| Album Share（相册分享） | 分享整个相册 |

## 用户管理

| 角色 | 权限 |
|------|-------------|
| Admin（管理员） | 完全系统访问 |
| User（用户） | 管理自己的照片 |
| Guest（访客） | 仅查看共享照片 |

## 配置

### 环境变量

| 变量 | 描述 |
|----------|-------------|
| SECRET_KEY | Django 密钥 |
| DB_HOST | 数据库主机名 |
| DB_NAME | 数据库名称 |
| DB_USER | 数据库用户名 |
| DB_PASS | 数据库密码 |
| REDIS_HOST | Redis 主机名 |
| SCAN_DIRECTORY | 照片目录路径 |

### 扫描设置

| 设置 | 描述 |
|---------|-------------|
| Scan Interval（扫描间隔） | 扫描新照片的频率 |
| Thumbnail Size（缩略图大小） | 生成缩略图的分辨率 |
| Face Clustering（人脸聚类） | 启用自动人脸分组 |
| Object Detection（物体检测） | 启用物体识别 |
| Scene Classification（场景分类） | 启用场景分类 |

## 性能调优

| 设置 | 建议 |
|---------|----------------|
| GPU | 使用 NVIDIA GPU 加速 ML 处理 |
| 内存 | 最低 4 GB，建议 8 GB+ |
| 存储 | SSD 用于数据库，HDD 用于照片 |
| 工作进程 | 增加以加快处理速度 |

## 备份

| 组件 | 方法 |
|-----------|--------|
| 数据库 | PostgreSQL dump |
| 照片 | 标准文件备份 |
| 缩略图 | 备份 protected_media 卷 |
| 配置 | 备份环境文件 |

```bash
# 数据库备份
docker compose exec db pg_dump -U librephotos librephotos > backup.sql
```

## API

LibrePhotos 提供用于集成的 REST API。

| 端点 | 方法 | 描述 |
|----------|--------|-------------|
| /api/photos | GET | 列出照片 |
| /api/albums | GET | 列出相册 |
| /api/faces | GET | 列出人脸聚类 |
| /api/search | GET | 搜索照片 |

## 技巧和最佳实践

| 技巧 | 说明 |
|-----|-------------|
| 按年组织 | 将照片存储在基于年份的文件夹中 |
| 启用 GPU | 显著加快 ML 处理速度 |
| 标注人脸 | 随时间提高人脸识别率 |
| 使用相册 | 按事件或主题组织照片 |
| 定期备份 | 防止数据丢失 |
| 检查扫描日志 | 监控处理错误 |

## 结论

LibrePhotos 提供了一个注重隐私的替代方案来替代商业照片管理服务。其机器学习功能自动化了组织大型照片库的繁琐任务，而自托管特性确保了对个人数据的完全控制。


---

## 来源：gallery.md

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


---

## 来源：gallery2.md

## 简介

Immich 是一个自托管的照片和视频管理解决方案，专为注重隐私的用户设计。它提供从移动设备自动备份、人脸识别、基于地图的浏览和现代 Web 界面。本教程涵盖安装、配置和日常使用。

## 架构

| 组件 | 描述 | 角色 |
|------|------|------|
| Server | Node.js 应用 | 核心 API 和逻辑 |
| Microservices | 后台工作进程 | ML 处理、转码 |
| Web App | SvelteKit 前端 | 浏览器界面 |
| Mobile App | Flutter 应用 | iOS/Android 备份 |
| Database | PostgreSQL | 数据存储 |
| Redis | 缓存层 | 会话和队列管理 |
| ML Models | 机器学习 | 人脸识别、CLIP 搜索 |

## 系统要求

| 组件 | 最低配置 | 推荐配置 |
|------|----------|----------|
| CPU | 2 核 | 4+ 核 |
| RAM | 2 GB | 4+ GB |
| 磁盘 | 20 GB | 100+ GB（取决于库大小） |
| 操作系统 | Linux, macOS | Linux（Docker） |
| Docker | 20.10+ | 24.0+ |
| 架构 | x86_64, ARM64 | x86_64 |

## 安装

### Docker Compose

```yaml
version: "3.8"

services:
  immich-server:
    image: ghcr.io/immich-app/immich-server:release
    container_name: immich-server
    volumes:
      - ${UPLOAD_LOCATION}:/usr/src/app/upload
      - /etc/localtime:/etc/localtime:ro
    env_file:
      - .env
    ports:
      - "2283:3001"
    depends_on:
      - redis
      - database
    restart: unless-stopped

  immich-machine-learning:
    container_name: immich-machine-learning
    image: ghcr.io/immich-app/immich-machine-learning:release
    volumes:
      - model-cache:/cache
    env_file:
      - .env
    restart: unless-stopped

  redis:
    container_name: immich-redis
    image: redis:7-alpine
    restart: unless-stopped

  database:
    container_name: immich-postgres
    image: tensorchord/pgvecto-rs:pg16-v0.2.0
    environment:
      POSTGRES_PASSWORD: ${DB_PASSWORD}
      POSTGRES_USER: ${DB_USERNAME}
      POSTGRES_DB: ${DB_DATABASE_NAME}
    volumes:
      - pgdata:/var/lib/postgresql/data
    restart: unless-stopped

volumes:
  pgdata:
  model-cache:
```

### 环境文件 (.env)

```
UPLOAD_LOCATION=/path/to/photos
DB_PASSWORD=your-secure-password
DB_USERNAME=postgres
DB_DATABASE_NAME=immich
```

### 初始设置

1. 访问 `http://your-server:2283`
2. 创建管理员账户
3. 配置存储路径
4. 安装移动应用并连接

## 移动应用设置

### 连接步骤

| 步骤 | 操作 | 详情 |
|------|------|------|
| 1 | 安装应用 | 从 App Store 或 Play Store 下载 |
| 2 | 输入服务器 URL | `http://your-server:2283` |
| 3 | 登录 | 使用管理员凭据 |
| 4 | 授予权限 | 照片、后台刷新 |
| 5 | 配置备份 | 选择相册、设置偏好 |

### 备份设置

| 设置 | 选项 | 建议 |
|------|------|------|
| 备份方式 | 仅 Wi-Fi, Wi-Fi + 蜂窝 | 仅 Wi-Fi |
| 后台备份 | 开/关 | 开 |
| 原始质量 | 开/关 | 归档用开 |
| 备份相册 | 选择特定 | 选择重要相册 |

## Web 界面

### 主要导航

| 部分 | 用途 | 功能 |
|------|------|------|
| Timeline | 时间线视图 | 浏览所有照片 |
| Albums | 组织的集合 | 创建、分享、协作 |
| Map | 基于位置的视图 | 按 GPS 数据浏览 |
| People | 人脸分组 | 识别人物并标记 |
| Sharing | 共享内容 | 共享相册、链接 |
| Explore | 发现 | 地点、事物、动态照片 |

### 时间线功能

| 功能 | 描述 | 用途 |
|------|------|------|
| Scroll | 连续时间线 | 浏览所有照片 |
| Multi-select | 选择多张照片 | 批量操作 |
| Date jump | 跳转到特定日期 | 快速导航 |
| Filtering | 按媒体类型、日期 | 缩小结果 |

## 相册管理

### 相册类型

| 类型 | 可见性 | 协作 |
|------|--------|------|
| Own Album | 私密 | 仅所有者 |
| Shared Album | 选定用户 | 多个贡献者 |
| Public Link | 任何有链接的人 | 查看或下载 |

### 创建相册

1. 从时间线选择照片
2. 点击 "Add to Album"
3. 选择现有或创建新相册
4. 如需设置分享选项

### 相册操作

| 操作 | 描述 | 批量支持 |
|------|------|----------|
| Add photos | 添加到相册 | 是 |
| Remove photos | 从相册移除 | 是 |
| Share | 生成链接或添加用户 | 否 |
| Set cover | 选择相册缩略图 | 否 |
| Rename | 更改相册标题 | 否 |
| Delete | 删除相册 | 否 |

## 人脸识别

### 工作原理

| 阶段 | 过程 | 自动 |
|------|------|------|
| Detection | 在照片中查找人脸 | 是 |
| Clustering | 将相似人脸分组 | 是 |
| Naming | 为分组分配名称 | 手动 |
| Merging | 合并重复分组 | 手动 |

### 管理人物

| 操作 | 步骤 |
|------|------|
| 查看所有人 | 导航到 People 部分 |
| 命名人物 | 点击人脸分组，输入名称 |
| 合并重复 | 选择分组，选择合并 |
| 设置主照片 | 选择最佳人脸照片 |
| 隐藏人物 | 从建议中移除 |

### 识别设置

| 设置 | 默认值 | 影响 |
|------|--------|------|
| Min faces to show | 3 | 过滤噪音 |
| Max distance | 0.6 | 分组敏感度 |
| Model | buffalo_l | 识别准确度 |

## 搜索

### 搜索类型

| 类型 | 示例 | 描述 |
|------|------|------|
| Text | "beach sunset" | CLIP 驱动的语义搜索 |
| Date | "2026 January" | 基于日期的筛选 |
| Person | "John" | 人脸标记的照片 |
| Location | "Paris" | GPS 标记的照片 |
| Type | "video" | 媒体类型筛选 |
| Camera | "iPhone 15" | 相机型号筛选 |

### 智能搜索

Immich 使用 CLIP（对比语言-图像预训练）进行语义搜索：

| 查询 | 结果 |
|------|------|
| "dog playing in snow" | 匹配概念的照片 |
| "birthday cake" | 蛋糕和庆祝照片 |
| "mountain landscape" | 山景 |
| "group selfie" | 带人脸的合照 |

## 地图视图

### 地图功能

| 功能 | 描述 | 要求 |
|------|------|------|
| Photo clusters | 地图上的照片分组 | 照片中的 GPS 数据 |
| Heatmap | 密度可视化 | 多个位置 |
| Timeline scrub | 滑动浏览日期 | 带日期的照片 |
| Detail view | 点击分组查看照片 | GPS 数据 |

### 添加位置数据

| 方法 | 描述 |
|------|------|
| GPS in EXIF | 来自相机的自动数据 |
| Manual tagging | 手动添加坐标 |
| Reverse geocoding | 自动地名 |

## 存储结构

### 上传目录布局

```
upload/
├── library/
│   ├── user1/
│   │   ├── 2026/
│   │   │   ├── 20260115/
│   │   │   │   ├── photo1.jpg
│   │   │   │   └── photo2.jpg
│   │   │   └── 20260116/
│   │   │       └── photo3.jpg
│   │   └── 2025/
│   └── user2/
├── thumbs/          # 生成的缩略图
├── encoded-video/   # 转码的视频
├── upload/          # 临时上传存储
└── profile/         # 用户头像
```

### 存储需求

| 媒体类型 | 平均大小 | 1000 张照片 |
|----------|----------|-------------|
| JPEG 照片 | 5 MB | 5 GB |
| HEIC 照片 | 3 MB | 3 GB |
| RAW 照片 | 25 MB | 25 GB |
| 1080p 视频 | 150 MB/分钟 | 可变 |
| 4K 视频 | 400 MB/分钟 | 可变 |

## 备份策略

### 数据库备份

```bash
# 备份 PostgreSQL
docker exec immich-postgres pg_dump -U postgres immich > backup.sql

# 恢复
cat backup.sql | docker exec -i immich-postgres psql -U postgres immich
```

### 完整备份

```bash
# 停止服务
docker compose down

# 备份上传和数据库
tar czf immich-backup-$(date +%Y%m%d).tar.gz ./upload ./pgdata

# 重启
docker compose up -d
```

### 备份计划

| 频率 | 操作 | 保留 |
|------|------|------|
| 每天 | 数据库导出 | 7 天 |
| 每周 | 完整备份 | 4 周 |
| 每月 | 归档到外部 | 12 个月 |

## 外部库支持

从现有存储导入照片：

| 功能 | 描述 | 要求 |
|------|------|------|
| External paths | 挂载现有目录 | 读取权限 |
| Import jobs | 后台扫描 | 服务器配置 |
| Read-only | 不修改源文件 | 对现有数据安全 |

### 配置

```yaml
# 在 docker-compose.yml 中
immich-server:
  volumes:
    - /path/to/existing/photos:/external/photos:ro
```

在 Settings > Administration > External Libraries 中添加外部库。

## 用户管理

### 用户角色

| 角色 | 权限 | 用途 |
|------|------|------|
| Admin | 完全系统控制 | 服务器所有者 |
| User | 上传、管理自己的照片 | 家庭成员 |
| Partner | 查看伴侣的时间线 | 配偶/伴侣 |

### 伴侣分享

| 功能 | 描述 |
|------|------|
| Timeline merge | 在你的时间线中查看伴侣的照片 |
| Face sharing | 共享人脸识别 |
| Album collaboration | 联合相册 |

## 性能优化

| 设置 | 影响 | 建议 |
|------|------|------|
| Thumbnail quality | 存储 vs 速度 | 大多数用户用中等 |
| Video transcoding | CPU 使用 | 启用后台工作进程 |
| ML concurrency | 处理速度 | 匹配 CPU 核心数 |
| Hardware acceleration | 转码速度 | 如可用则启用 |
| Reverse geocoding | API 调用 | 使用本地 Nominatim |

## 故障排除

| 问题 | 可能原因 | 解决方案 |
|------|----------|----------|
| 上传失败 | 网络或存储 | 检查连接和磁盘空间 |
| 搜索慢 | ML 模型加载中 | 等待初始索引 |
| 人脸缺失 | 尚未处理 | 检查 ML 容器状态 |
| 转码错误 | 编解码器问题 | 检查 FFmpeg 版本 |
| 数据库错误 | 损坏 | 从备份恢复 |

## 总结

Immich 提供了一个全面的、注重隐私的个人照片和视频管理解决方案。其自动备份、人脸识别和语义搜索的组合使其成为基于云的照片服务的有力替代品。

关键实践：

- 使用 Docker Compose 部署以便管理
- 启用自动移动备份以获得持续保护
- 使用人脸识别按人物组织照片
- 利用智能搜索进行自然语言照片发现
- 在照片存储的同时维护定期数据库备份
- 配置外部库以包含现有照片集合


---

## 来源：gallery3.md

## 简介

PhotoPrism 是一款 AI 驱动的照片管理应用程序，可自动组织和搜索您的照片库。它使用机器学习进行人脸识别、物体检测和基于位置的浏览，无需依赖云服务。

## 目录

1. [系统要求](#系统要求)
2. [安装](#安装)
3. [初始设置](#初始设置)
4. [照片导入](#照片导入)
5. [AI 功能](#ai-功能)
6. [搜索与过滤](#搜索与过滤)
7. [相册与组织](#相册与组织)
8. [共享与访问](#共享与访问)
9. [性能调优](#性能调优)

## 系统要求

| 组件 | 最低要求 | 推荐配置 |
|------|----------|----------|
| CPU | 2 核 | 4 核 |
| 内存 | 2 GB | 4 GB |
| 存储 | 20 GB | 100 GB+ |
| 数据库 | SQLite | MariaDB 10.5+ |
| 操作系统 | Linux, macOS, Windows | Ubuntu 22.04+ |
| Docker | 20.10+ | 最新稳定版 |

## 安装

### Docker Compose

```yaml
# docker-compose.yml
services:
  photoPrism:
    image: photoprism/photoprism:latest
    depends_on:
      - mariadb
    environment:
      PHOTOPRISM_ADMIN_PASSWORD: "your-secure-password"
      PHOTOPRISM_HTTP_PORT: 2342
      PHOTOPRISM_DATABASE_DRIVER: mysql
      PHOTOPRISM_DATABASE_SERVER: mariadb:3306
      PHOTOPRISM_DATABASE_NAME: photoprism
      PHOTOPRISM_DATABASE_USER: photoprism
      PHOTOPRISM_DATABASE_PASSWORD: photoprism
    volumes:
      - ./photos:/photoprism/originals
      - ./storage:/photoprism/storage
    ports:
      - "2342:2342"

  mariadb:
    image: mariadb:10.11
    environment:
      MYSQL_ROOT_PASSWORD: photoprism
      MYSQL_DATABASE: photoprism
      MYSQL_USER: photoprism
      MYSQL_PASSWORD: photoprism
    volumes:
      - ./database:/var/lib/mysql
```

### 安装方式对比

| 方式 | 优点 | 缺点 |
|------|------|------|
| Docker Compose | 易于更新，隔离性好 | 需要 Docker |
| Docker CLI | 快速单命令 | 配置较少 |
| 裸机安装 | 完全控制 | 依赖复杂 |
| NAS 包 | Synology, QNAP | 版本有限 |

## 初始设置

### 首次登录

| 步骤 | 操作 |
|------|------|
| 1 | 访问 http://localhost:2342 |
| 2 | 使用管理员凭据登录 |
| 3 | 完成初始配置向导 |
| 4 | 设置库路径和导入选项 |

### 环境变量

| 变量 | 说明 | 默认值 |
|------|------|--------|
| `PHOTOPRISM_ADMIN_PASSWORD` | 管理员密码 | 随机生成 |
| `PHOTOPRISM_HTTP_PORT` | Web 服务器端口 | 2342 |
| `PHOTOPRISM_SITE_URL` | 公共 URL | http://localhost:2342 |
| `PHOTOPRISM_ORIGINALS_PATH` | 照片位置 | /photoprism/originals |
| `PHOTOPRISM_STORAGE_PATH` | 缓存和数据 | /photoprism/storage |

### 数据库配置

| 设置 | SQLite | MariaDB |
|------|--------|---------|
| 设置复杂度 | 无 | 中等 |
| 性能 | 基础 | 高 |
| 并发用户 | 1-2 | 多个 |
| 库大小 | < 5 万张照片 | 无限制 |
| 备份 | 复制文件 | mysqldump |

## 照片导入

### 支持的格式

| 格式 | 类型 | 读取 | 写入 |
|------|------|------|------|
| JPEG | 光栅 | 是 | 是 |
| PNG | 光栅 | 是 | 否 |
| HEIC/HEIF | 光栅 | 是 | 是 |
| WebP | 光栅 | 是 | 是 |
| RAW | 相机 | 是 | 否 |
| GIF | 动画 | 是 | 否 |
| MP4 | 视频 | 是 | 否 |
| MOV | 视频 | 是 | 否 |

### 导入方式

| 方式 | 说明 | 路径 |
|------|------|------|
| Originals 文件夹 | 直接放置文件 | /photoprism/originals |
| Web 上传 | 基于浏览器的上传 | UI 上传按钮 |
| WebDAV | 远程文件访问 | /originals/ |
| API | 编程导入 | REST 端点 |

### 导入设置

| 设置 | 说明 | 选项 |
|------|------|------|
| 移动与复制 | 文件处理方式 | 移动、复制、跳过 |
| 重复检测 | 处理已存在文件 | 跳过、更新 |
| 附属文件 | XMP, JSON 处理 | 导入、跳过 |
| 分组 | 堆叠相关照片 | 按名称、按时间 |

## AI 功能

### 机器学习模型

| 功能 | 模型 | 用途 |
|------|------|------|
| 分类 | MobileNet | 物体标记 |
| 人脸检测 | RetinaFace | 查找人脸 |
| 人脸聚类 | ArcFace | 人脸分组 |
| 位置 | Places API | 反向地理编码 |
| NSFW 检测 | 自定义模型 | 内容过滤 |

### 分类类别

| 类别 | 示例 | 准确度 |
|------|------|--------|
| 动物 | 狗、猫、鸟 | 高 |
| 交通工具 | 汽车、自行车、卡车 | 高 |
| 自然 | 山、海滩、森林 | 高 |
| 食物 | 披萨、蛋糕、水果 | 中 |
| 建筑 | 建筑物、桥梁、教堂 | 中 |
| 人物 | 成人、儿童 | 高 |

### 索引选项

| 选项 | 说明 | 影响 |
|------|------|------|
| 完整索引 | 完整 AI 分析 | 慢，全面 |
| 跳过未修改 | 仅新照片 | 快 |
| 重新索引现有 | 强制重新分析 | 慢 |
| 人脸识别 | 查找和聚类人脸 | 中等速度 |

## 搜索与过滤

### 搜索过滤器

| 过滤器 | 示例 | 说明 |
|--------|------|------|
| 类型 | `type:video` | 照片、视频、实况 |
| 质量 | `quality:3` | 质量评分 1-7 |
| 相机 | `camera:iphone` | 相机型号 |
| 镜头 | `lens:50mm` | 镜头信息 |
| 国家 | `country:us` | 所在国家 |
| 城市 | `city:paris` | 所在城市 |
| 颜色 | `color:red` | 主要颜色 |
| 年份 | `year:2024` | 拍摄年份 |
| 月份 | `month:12` | 拍摄月份 |

### 高级搜索

| 操作符 | 示例 | 功能 |
|--------|------|------|
| AND | `cat dog` | 两者都包含 |
| OR | `cat\|dog` | 任一包含 |
| NOT | `cat -dog` | 排除术语 |
| 精确 | `"black cat"` | 精确短语 |
| 范围 | `year:2020-2024` | 日期范围 |

### 排序选项

| 排序方式 | 方向 | 使用场景 |
|----------|------|----------|
| 拍摄日期 | 最新优先 | 最近照片 |
| 拍摄日期 | 最早优先 | 历史浏览 |
| 添加日期 | 最新优先 | 最近导入 |
| 名称 | 按字母顺序 | 基于文件查找 |
| 相似度 | 最接近匹配 | 视觉搜索 |

## 相册与组织

### 相册类型

| 类型 | 说明 | 自动填充 |
|------|------|----------|
| 普通相册 | 手动收集 | 否 |
| 时刻 | 基于时间的分组 | 是 |
| 日历 | 年/月视图 | 是 |
| 收藏 | 星标照片 | 手动 |
| 标签 | AI 检测的标签 | 是 |

### 相册管理

| 操作 | 方法 |
|------|------|
| 创建相册 | 相册 > 新建相册 |
| 添加照片 | 选择照片 > 添加到相册 |
| 移除照片 | 打开相册 > 移除 |
| 共享相册 | 相册设置 > 共享 |
| 设置封面 | 选择照片 > 设为封面 |

### 批量操作

| 操作 | 步骤 |
|------|------|
| 归档 | 选择 > 归档 |
| 删除 | 选择 > 删除 |
| 添加到相册 | 选择 > 添加到 |
| 设为收藏 | 选择 > 收藏 |
| 更改日期 | 选择 > 编辑 > 日期 |
| 设置位置 | 选择 > 编辑 > 位置 |

## 共享与访问

### 共享选项

| 方式 | 访问权限 | 需要认证 |
|------|----------|----------|
| 直接链接 | 公共 URL | 否 |
| 密码链接 | 受保护 URL | 是（密码） |
| 相册共享 | 特定相册 | 否 |
| 账户 | 完全访问 | 是 |

### 用户角色

| 角色 | 权限 |
|------|------|
| 管理员 | 完全访问、设置、用户管理 |
| 用户 | 查看、上传、管理自己的照片 |
| 查看者 | 只读访问 |

### API 访问

```bash
# 获取会话令牌
curl -X POST http://localhost:2342/api/v1/session \
  -d '{"username":"admin","password":"your-password"}'

# 搜索照片
curl http://localhost:2342/api/v1/photos?q=cat \
  -H "X-Session-Token: YOUR_TOKEN"

# 下载照片
curl http://localhost:2342/api/v1/photos/PHOTO_UID/download \
  -H "X-Session-Token: YOUR_TOKEN" -o photo.jpg
```

## 性能调优

### 硬件推荐

| 库大小 | CPU | 内存 | 存储 |
|--------|-----|------|------|
| < 5,000 | 2 核 | 2 GB | SSD |
| 5,000 - 50,000 | 4 核 | 4 GB | SSD |
| 50,000 - 200,000 | 8 核 | 8 GB | NVMe |
| 200,000+ | 16 核 | 16 GB | NVMe RAID |

### 索引性能

| 设置 | 影响 |
|------|------|
| 工作线程数 | 更多线程 = 更快索引 |
| JPEG 质量 | 更低 = 更快缩略图 |
| 缩略图大小 | 更小 = 更少存储 |
| 人脸识别 | CPU 密集型 |
| 跳过视频 | 减少索引时间 |

### 数据库优化

| 优化 | SQLite | MariaDB |
|------|--------|---------|
| WAL 模式 | 已启用 | 不适用 |
| 缓冲池 | 不适用 | 设置为 50% 内存 |
| 索引调优 | 自动 | 建议手动 |
| 清理 | 定期 | 自动 |

## 备份与恢复

| 组件 | 位置 | 备份方法 |
|------|------|----------|
| 数据库 | SQLite 或 MariaDB | 转储/备份命令 |
| Originals | Originals 文件夹 | 文件同步 |
| Storage | Storage 文件夹 | 文件同步 |
| 配置 | 环境变量 | 单独记录 |

## 总结

PhotoPrism 提供了一个自托管的云照片服务替代方案，具有强大的 AI 驱动组织功能。其人脸识别、物体检测和灵活的搜索功能使其适合管理大型个人照片库，同时保持对数据的完全控制。


---
