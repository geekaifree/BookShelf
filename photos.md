# LibrePhotos：自托管照片管理

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
