# PhotoPrism：自托管照片管理

## 简介

PhotoPrism 是一个开源的自托管照片管理应用，使用人工智能来组织、浏览和分享你的照片库。它提供了以隐私为中心的替代方案，取代 Google Photos 等云端照片服务。

## 目录

- [安装](#安装)
- [配置](#配置)
- [AI 功能](#ai-功能)
- [人脸识别](#人脸识别)
- [地理位置](#地理位置)
- [搜索](#搜索)
- [相册](#相册)
- [分享](#分享)
- [移动应用](#移动应用)
- [备份](#备份)
- [从 Google Photos 迁移](#从-google-photos-迁移)
- [故障排除](#故障排除)

---

## 安装

PhotoPrism 可以使用 Docker 安装，这是大多数用户的推荐方式。

### 系统要求

| 组件 | 最低要求 | 推荐配置 |
|------|----------|----------|
| CPU | 2 核 | 4+ 核 |
| 内存 | 2 GB | 4+ GB |
| 存储 | 10 GB + 照片存储 | SSD 用于数据库 |
| 操作系统 | Linux、macOS、Windows | Linux（Ubuntu/Debian） |
| Docker | 17.06+ | 最新稳定版 |

### Docker 安装

**docker-compose.yml：**

```yaml
version: '3.5'

services:
  photoprism:
    image: photoprism/photoprism:latest
    container_name: photoprism
    restart: unless-stopped
    security_opt:
      - seccomp:unconfined
      - apparmor:unconfined
    ports:
      - "2342:2342"
    environment:
      PHOTOPRISM_ADMIN_PASSWORD: "your-secure-password"
      PHOTOPRISM_SITE_URL: "http://localhost:2342/"
      PHOTOPRISM_ORIGINALS_PATH: "/photoprism/originals"
      PHOTOPRISM_STORAGE_PATH: "/photoprism/storage"
      PHOTOPRISM_DATABASE_DRIVER: "sqlite"
      PHOTOPRISM_DISABLE_CHOWN: "false"
      PHOTOPRISM_DISABLE_WEBDAV: "false"
      PHOTOPRISM_DISABLE_SETTINGS: "false"
      PHOTOPRISM_DISABLE_TENSORFLOW: "false"
      PHOTOPRISM_DARKMODE: "true"
    volumes:
      - "./originals:/photoprism/originals"
      - "./storage:/photoprism/storage"

  mariadb:
    image: mariadb:10.11
    container_name: photoprism-mariadb
    restart: unless-stopped
    security_opt:
      - seccomp:unconfined
      - apparmor:unconfined
    environment:
      MARIADB_ROOT_PASSWORD: "your-mariadb-password"
      MARIADB_DATABASE: "photoprism"
      MARIADB_USER: "photoprism"
      MARIADB_PASSWORD: "your-mariadb-password"
    volumes:
      - "./database:/var/lib/mysql"
```

### 启动 PhotoPrism

```bash
# 创建目录结构
mkdir -p originals storage database

# 启动服务
docker-compose up -d

# 查看日志
docker-compose logs -f photoprism

# 访问 Web 界面
# 在浏览器中打开 http://localhost:2342
```

### 安装方式对比

| 方式 | 难度 | 性能 | 维护 |
|------|------|------|------|
| Docker Compose | 低 | 好 | 更新容易 |
| Docker CLI | 低 | 好 | 更新容易 |
| 原生构建 | 高 | 最佳 | 手动更新 |
| Kubernetes | 高 | 好 | 复杂 |

---

## 配置

PhotoPrism 通过环境变量进行配置。

### 核心配置

| 变量 | 描述 | 默认值 | 示例 |
|------|------|--------|------|
| PHOTOPRISM_ADMIN_PASSWORD | 管理员密码 | （必填） | "secure-password" |
| PHOTOPRISM_SITE_URL | 公开 URL | http://localhost:2342/ | "https://photos.example.com/" |
| PHOTOPRISM_ORIGINALS_PATH | 照片路径 | /photoprism/originals | "/mnt/photos" |
| PHOTOPRISM_STORAGE_PATH | 存储路径 | /photoprism/storage | "/mnt/storage" |
| PHOTOPRISM_DATABASE_DRIVER | 数据库类型 | sqlite | "mysql" |

### 数据库配置

| 变量 | 描述 | 默认值 |
|------|------|--------|
| PHOTOPRISM_DATABASE_DRIVER | sqlite、mysql 或 mariadb | sqlite |
| PHOTOPRISM_DATABASE_SERVER | 数据库主机:端口 | （无） |
| PHOTOPRISM_DATABASE_NAME | 数据库名称 | photoprism |
| PHOTOPRISM_DATABASE_USER | 数据库用户名 | photoprism |
| PHOTOPRISM_DATABASE_PASSWORD | 数据库密码 | （无） |

### 性能调优

| 变量 | 描述 | 建议 |
|------|------|------|
| PHOTOPRISM_WORKERS | 索引工作线程数 | CPU 核数 - 1 |
| PHOTOPRISM_HTTP_COMPRESSION | 启用 gzip 压缩 | "gzip" |
| PHOTOPRISM_THUMB_FILTER | 缩略图重采样滤镜 | "lanczos" |
| PHOTOPRISM_THUMB_SIZE | 最大缩略图尺寸 | 2048 |
| PHOTOPRISM_JPEG_QUALITY | JPEG 压缩质量 | 92 |

### 安全配置

| 变量 | 描述 | 建议 |
|------|------|------|
| PHOTOPRISM_ADMIN_PASSWORD | 管理员密码 | 强密码、唯一密码 |
| PHOTOPRISM_DISABLE_WEBDAV | 禁用 WebDAV 访问 | "false"（保持启用以同步） |
| PHOTOPRISM_PUBLIC | 允许公开访问 | "false"（需要登录） |

---

## AI 功能

PhotoPrism 使用机器学习自动组织和分类你的照片。

### AI 能力

| 功能 | 描述 | 技术 |
|------|------|------|
| 图像分类 | 自动场景/物体识别 | TensorFlow、MobileNet |
| 人脸检测 | 查找照片中的人脸 | TensorFlow |
| 图像标签 | 自动生成描述性标签 | TensorFlow |
| OCR | 从图像中提取文字 | TensorFlow |
| 位置估算 | 从视觉线索估算位置 | TensorFlow |
| 质量评分 | 评估图像质量 | 自定义算法 |

### AI 索引工作原理

1. **照片导入**：照片从原文件复制或索引
2. **缩略图生成**：创建多种尺寸用于快速浏览
3. **元数据提取**：读取 EXIF、IPTC、XMP 数据
4. **AI 分类**：TensorFlow 分析图像内容
5. **人脸检测**：检测和提取人脸
6. **索引**：所有数据存储到数据库
7. **分类**：按检测到的内容组织照片

### 控制 AI 功能

| 变量 | 描述 | 默认值 |
|------|------|--------|
| PHOTOPRISM_DISABLE_TENSORFLOW | 禁用所有 AI 功能 | "false" |
| PHOTOPRISM_DISABLE_CLASSIFICATION | 禁用图像分类 | "false" |
| PHOTOPRISM_DISABLE_FACES | 禁用人脸检测 | "false" |
| PHOTOPRISM_DISABLE_VECTORS | 禁用向量搜索 | "false" |

### AI 性能

| 硬件 | 每小时处理照片数 | 备注 |
|------|-----------------|------|
| 4 核 CPU | 200-400 | 取决于照片分辨率 |
| 8 核 CPU | 400-800 | 大型库推荐 |
| GPU 加速 | 暂不支持 | 计划中 |

---

## 人脸识别

PhotoPrism 包含人脸检测和识别功能，可按人物分组照片。

### 人脸识别工作原理

1. **检测**：在每张照片中检测人脸
2. **聚类**：将相似的人脸分组
3. **命名**：你为人脸簇分配名字
4. **匹配**：新照片与已知人脸匹配
5. **审核**：你可以批准或拒绝匹配

### 管理人物

| 操作 | 方法 |
|------|------|
| 查看检测到的人脸 | 进入侧边栏的"人物"部分 |
| 命名人脸簇 | 点击簇，输入名字 |
| 合并人脸簇 | 选择多个簇，合并 |
| 移除误判 | 拒绝匹配 |
| 隐藏人物 | 在设置中标记为隐藏 |

### 人脸识别设置

| 设置 | 描述 | 建议 |
|------|------|------|
| 人脸检测 | 启用/禁用人脸检测 | 启用 |
| 人脸聚类 | 分组相似人脸 | 启用 |
| 簇大小 | 形成簇的最少照片数 | 5-10 |
| 匹配阈值 | 自动匹配置信度 | 0.75 |

### 提升人脸识别效果的技巧

- 确保照片有良好的光线和分辨率
- 定期审核和纠正误判
- 簇出现时尽快命名
- 更大的簇产生更准确的匹配
- 正面照片效果最好

---

## 地理位置

PhotoPrism 使用照片中的 GPS 数据按位置组织照片。

### 地理位置工作原理

1. **EXIF GPS 数据**：从照片元数据读取 GPS 坐标
2. **反向地理编码**：将坐标转换为地名
3. **位置聚类**：将同一地点拍摄的照片分组
4. **地图显示**：在交互式地图上展示照片

### 地理位置功能

| 功能 | 描述 |
|------|------|
| 自动地点 | 照片自动分配到地点 |
| 地点搜索 | 按城市、州、国家搜索 |
| 地图视图 | 带照片簇的交互式地图 |
| 路线追踪 | 查看沿旅行路线的照片 |
| 位置编辑 | 手动设置或纠正位置 |

### 反向地理编码提供商

| 提供商 | 描述 | 设置 |
|--------|------|------|
| 本地（默认） | 内置数据库 | 无需设置 |
| Google Maps API | 高精度 | 需要 API 密钥 |
| OpenStreetMap | 免费、开放数据 | 需要 API 密钥 |
| Nominatim | 免费地理编码 | 可自托管 |

### 地理位置配置

| 变量 | 描述 |
|------|------|
| PHOTOPRISM_DISABLE_PLACES | 禁用地图功能 |
| PHOTOPRISM_MAPS_TOKEN | 地图 API 令牌 |
| PHOTOPRISM_MAPS_STYLE | 地图瓦片样式 |

---

## 搜索

PhotoPrism 提供强大的搜索功能，覆盖整个照片库。

### 搜索语法

| 搜索词 | 描述 | 示例 |
|--------|------|------|
| 文本 | 在标题、描述、标签中搜索 | "birthday" |
| 地点 | 按位置名称搜索 | "Paris" |
| 相机 | 按相机型号搜索 | "iPhone 14" |
| 镜头 | 按镜头搜索 | "50mm" |
| 年份 | 按年份搜索 | "2024" |
| 月份 | 按月份搜索 | "January" |
| 日期 | 按日期搜索 | "Monday" |
| 颜色 | 按主色调搜索 | "blue" |
| 质量 | 按质量评分搜索 | "quality:3" |
| 类型 | 按文件类型搜索 | "type:video" |
| 收藏 | 搜索收藏 | "favorite:true" |
| 私密 | 搜索私密照片 | "private:true" |

### 高级搜索

| 过滤器 | 语法 | 示例 |
|--------|------|------|
| 之前日期 | before:2024-01-01 | "before:2024-01-01" |
| 之后日期 | after:2023-12-31 | "after:2023-12-31" |
| 日期范围 | after:2023-01-01 before:2023-12-31 | 日期范围 |
| 有人脸 | faces:yes | "faces:yes" |
| 无人脸 | faces:no | "faces:no" |
| 风景 | landscape:true | "landscape:true" |
| 人像 | portrait:true | "portrait:true" |
| 堆叠 | stack:true | "stack:true" |

---

## 相册

相册让你将照片组织成集合。

### 相册类型

| 类型 | 描述 | 使用场景 |
|------|------|----------|
| 相册 | 手动照片集合 | 策展集合 |
| 时刻 | 按日期/位置自动生成 | 自动组织 |
| 状态 | 按状态/流程收集 | 工作流管理 |

### 创建相册

| 方法 | 操作 |
|------|------|
| 从选择 | 选择照片，点击"添加到相册" |
| 从搜索 | 搜索，全选，添加到相册 |
| 空相册 | 在相册部分点击"+" |
| 从地图 | 在地图上选择照片，添加到相册 |

### 相册管理

| 操作 | 方法 |
|------|------|
| 重命名 | 点击相册标题，编辑 |
| 添加照片 | 拖放或使用"添加"按钮 |
| 移除照片 | 选择照片，点击"从相册移除" |
| 排序 | 按日期、标题或手动 |
| 设置封面 | 选择照片，设为封面 |
| 删除相册 | 相册设置，删除 |

### 时刻

时刻根据以下条件自动创建：

- **日期**：同一天或连续几天拍摄的照片
- **位置**：同一地点拍摄的照片
- **事件**：具有相似元数据的照片

---

## 分享

PhotoPrism 提供多种分享照片的方式。

### 分享方式

| 方式 | 描述 | 访问权限 |
|------|------|----------|
| 分享链接 | 相册或照片的公开 URL | 任何有链接的人 |
| WebDAV | 挂载为网络驱动器 | 经过认证的用户 |
| 下载 | 下载原始文件 | 经过认证的用户 |
| 嵌入 | 嵌入网站 | 可配置 |

### 创建分享链接

1. 选择照片或打开相册
2. 点击分享按钮
3. 配置分享设置
4. 复制生成的链接

### 分享链接设置

| 设置 | 描述 |
|------|------|
| 密码 | 需要密码才能查看 |
| 过期时间 | 设置链接过期日期 |
| 下载 | 允许/不允许下载 |
| 全分辨率 | 显示原始或优化版本 |
| 描述 | 添加描述 |

---

## 移动应用

PhotoPrism 提供渐进式 Web 应用（PWA）用于移动访问。

### 移动应用功能

| 功能 | 描述 |
|------|------|
| 浏览 | 在移动设备上查看照片 |
| 搜索 | 完整搜索功能 |
| 上传 | 从手机上传照片 |
| 收藏 | 标记照片为收藏 |
| 相册 | 创建和管理相册 |
| 离线 | PWA 缓存支持离线访问 |

### 设置移动访问

1. **需要 HTTPS**：移动访问需要 HTTPS
2. **反向代理**：设置 Nginx 或 Caddy 并配置 SSL
3. **PWA 安装**：从浏览器添加到主屏幕
4. **上传**：启用相机上传以自动备份

### 反向代理设置（Nginx）

```nginx
server {
    listen 443 ssl http2;
    server_name photos.example.com;

    ssl_certificate /etc/letsencrypt/live/photos.example.com/fullchain.pem;
    ssl_certificate_key /etc/letsencrypt/live/photos.example.com/privkey.pem;

    client_max_body_size 500M;

    location / {
        proxy_pass http://127.0.0.1:2342;
        proxy_set_header Host $host;
        proxy_set_header X-Real-IP $remote_addr;
        proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
        proxy_set_header X-Forwarded-Proto $scheme;
    }
}
```

---

## 备份

用合适的备份策略保护你的照片库。

### 备份组件

| 组件 | 包含内容 | 备份优先级 |
|------|----------|-----------|
| originals | 你的实际照片和视频 | 关键 |
| storage | 缩略图、缓存、附属文件 | 中等（可重新生成） |
| 数据库 | 元数据、相册、人脸数据 | 高 |
| 配置 | Docker compose、env 文件 | 高 |

### 备份策略

| 策略 | 方法 | 频率 |
|------|------|------|
| 3-2-1 法则 | 3 份副本、2 种介质、1 份异地 | 持续 |
| Rsync | 增量文件同步 | 每天 |
| Restic | 去重备份 | 每天 |
| Btrfs 快照 | 文件系统快照 | 每小时 |
| 云同步 | 上传到云存储 | 持续 |

### 备份脚本示例

```bash
#!/bin/bash
# PhotoPrism 备份脚本

BACKUP_DIR="/backup/photoprism"
DATE=$(date +%Y%m%d_%H%M%S)

# 停止 PhotoPrism 以确保一致性备份
docker-compose stop photoprism

# 备份原始文件
rsync -av --delete ./originals/ ${BACKUP_DIR}/originals/

# 备份数据库
if [ "$DATABASE_DRIVER" = "sqlite" ]; then
    cp ./database/photoprism.db ${BACKUP_DIR}/database_${DATE}.db
fi

# 备份存储
rsync -av ./storage/ ${BACKUP_DIR}/storage/

# 备份配置
cp docker-compose.yml ${BACKUP_DIR}/
cp .env ${BACKUP_DIR}/

# 重启 PhotoPrism
docker-compose start photoprism

# 清理旧备份（保留最近 30 份）
find ${BACKUP_DIR} -name "*.db" -mtime +30 -delete
```

### 从备份恢复

1. 停止 PhotoPrism
2. 将原始文件恢复到 originals 目录
3. 恢复数据库文件
4. 恢复 storage 目录
5. 启动 PhotoPrism
6. 如需运行索引：`photoprism index --cleanup`

---

## 从 Google Photos 迁移

从 Google Photos 迁移到 PhotoPrism。

### 第 1 步：从 Google Photos 导出

使用 Google Takeout 导出你的照片：

1. 访问 takeout.google.com
2. 选择 Google Photos
3. 选择导出格式（建议 .zip）
4. 下载所有部分

### 第 2 步：准备导出文件

| 任务 | 工具 | 命令 |
|------|------|------|
| 解压 | unzip | `unzip '*.zip' -d ./photos` |
| 删除空目录 | find | `find ./photos -type d -empty -delete` |
| 验证文件数 | find | `find ./photos -type f \| wc -l` |

### 第 3 步：处理 Google Photos 元数据

Google Photos 将元数据存储在 JSON 附属文件中：

| 问题 | 解决方案 |
|------|----------|
| JSON 附属文件 | PhotoPrism 自动读取 |
| 编辑过的照片 | 原始和编辑版本都保留 |
| 实况照片 | 视频部分保留 |
| 相册 | 手动重建或使用脚本 |
| 位置数据 | 通常保留在 EXIF 中 |

### 第 4 步：导入到 PhotoPrism

```bash
# 将照片复制到 originals 目录
cp -r /path/to/google-photos/ ./originals/

# 开始索引
docker-compose exec photoprism photoprism index --cleanup

# 监控进度
docker-compose logs -f photoprism
```

### 迁移对比

| 功能 | Google Photos | PhotoPrism |
|------|---------------|------------|
| 存储 | 云端（15GB 免费） | 自托管（无限） |
| 隐私 | Google 可访问 | 完全控制 |
| AI 功能 | 高级 | 良好，持续改进 |
| 人脸识别 | 优秀 | 良好 |
| 搜索 | 优秀 | 很好 |
| 分享 | 简单 | 灵活 |
| 成本 | 免费层 + 付费 | 硬件 + 电费 |
| 移动应用 | 原生 | PWA |

---

## 故障排除

常见问题和解决方案。

### 性能问题

| 问题 | 原因 | 解决方案 |
|------|------|----------|
| 索引缓慢 | 工作线程太多 | 减少 PHOTOPRISM_WORKERS |
| CPU 占用高 | AI 处理 | 在非高峰时段索引 |
| 搜索缓慢 | 数据库太大 | 使用 MySQL/MariaDB 替代 SQLite |
| 内存不足 | 大缩略图 | 减少 PHOTOPRISM_THUMB_SIZE |

### 常见错误

| 错误 | 原因 | 解决方案 |
|------|------|----------|
| "权限被拒" | 文件权限 | 修复所有权：`chown -R 1000:1000` |
| "数据库锁定" | 并发访问 | 使用 MySQL/MariaDB |
| "无法读取文件" | 文件损坏 | 检查文件完整性 |
| "磁盘空间不足" | 存储已满 | 清理缓存，扩展存储 |

### 维护任务

| 任务 | 命令 | 频率 |
|------|------|------|
| 索引新照片 | `photoprism index` | 添加照片后 |
| 清理孤立文件 | `photoprism index --cleanup` | 每月 |
| 备份数据库 | 复制数据库文件 | 每周 |
| 更新 PhotoPrism | `docker-compose pull && docker-compose up -d` | 每月 |
| 查看日志 | `docker-compose logs --tail=100` | 按需 |

---

## 总结

PhotoPrism 是一个强大的、以隐私为中心的照片管理解决方案，让你完全掌控自己的照片库。关键要点：

- **自托管**：你的照片留在你的硬件上
- **AI 驱动**：自动组织、人脸识别和标签
- **可搜索**：跨元数据、位置和内容的强大搜索
- **可访问**：Web 界面在任何设备上工作
- **可扩展**：WebDAV、分享链接和 API 访问
- **免费**：开源，可选付费支持
