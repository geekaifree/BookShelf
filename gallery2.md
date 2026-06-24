# 使用 Immich 进行照片管理

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
