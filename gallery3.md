# 使用 PhotoPrism 进行照片管理

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
