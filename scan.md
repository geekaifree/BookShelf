# 使用 Paperless-ngx 进行文档管理

## 简介

Paperless-ngx 是一款开源文档管理系统，用于索引和归档纸质文档。它使用 OCR 技术使扫描文档可搜索，并通过标签、通信方和文档类型进行组织管理。

## 目录

1. [系统要求](#系统要求)
2. [安装方式](#安装方式)
3. [初始配置](#初始配置)
4. [文档导入](#文档导入)
5. [标签与组织](#标签与组织)
6. [搜索与检索](#搜索与检索)
7. [自动化规则](#自动化规则)
8. [用户管理](#用户管理)

## 系统要求

| 组件 | 最低要求 | 推荐配置 |
|------|----------|----------|
| CPU | 2 核 | 4 核 |
| 内存 | 2 GB | 4 GB |
| 存储 | 10 GB | 50 GB+ |
| 操作系统 | Linux, macOS, Windows | Ubuntu 22.04+ |
| Docker | 20.10+ | 最新稳定版 |
| Python | 3.9+ (裸机安装) | 3.11+ |

## 安装方式

### Docker Compose

推荐使用 Docker Compose，包含以下服务：

| 服务 | 用途 | 端口 |
|------|------|------|
| webserver | Paperless-ngx 应用 | 8000 |
| broker | Redis 任务队列 | 6379 |
| db | PostgreSQL 数据库 | 5432 |
| gotenberg | 文档转换 | 3000 |
| tika | 内容提取 | 9998 |

```yaml
# docker-compose.yml
services:
  broker:
    image: redis:7
    volumes:
      - redisdata:/data

  db:
    image: postgres:15
    volumes:
      - pgdata:/var/lib/postgresql/data
    environment:
      POSTGRES_DB: paperless
      POSTGRES_USER: paperless
      POSTGRES_PASSWORD: paperless

  webserver:
    image: ghcr.io/paperless-ngx/paperless-ngx:latest
    volumes:
      - data:/usr/src/paperless/data
      - media:/usr/src/paperless/media
      - ./export:/usr/src/paperless/export
      - ./consume:/usr/src/paperless/consume
    environment:
      PAPERLESS_REDIS: redis://broker:6379
      PAPERLESS_DBHOST: db
      PAPERLESS_TIME_ZONE: America/New_York
    ports:
      - "8000:8000"
    depends_on:
      - db
      - broker

volumes:
  data:
  media:
  pgdata:
  redisdata:
```

### 裸机安装

| 步骤 | 命令 | 用途 |
|------|------|------|
| 1 | `git clone https://github.com/paperless-ngx/paperless-ngx` | 获取源码 |
| 2 | `cd paperless-ngx && pip install -r requirements.txt` | 安装依赖 |
| 3 | `cp paperless.conf.example paperless.conf` | 配置模板 |
| 4 | `python manage.py migrate` | 数据库设置 |
| 5 | `python manage.py createsuperuser` | 创建管理员账户 |
| 6 | `python manage.py runserver` | 启动服务器 |

## 初始配置

### 环境变量

| 变量 | 说明 | 默认值 |
|------|------|--------|
| `PAPERLESS_TIME_ZONE` | 服务器时区 | UTC |
| `PAPERLESS_OCR_LANGUAGE` | OCR 语言 | eng |
| `PAPERLESS_CONSUMPTION_DIR` | 监视文件夹 | ../consume |
| `PAPERLESS_MEDIA_ROOT` | 存储位置 | ../media |
| `PAPERLESS_SECRET_KEY` | Django 密钥 | 自动生成 |
| `PAPERLESS_URL` | 公共 URL | http://localhost:8000 |

### OCR 配置

| 设置 | 说明 | 可选值 |
|------|------|--------|
| `PAPERLESS_OCR_MODE` | OCR 执行时机 | force, skip, redo |
| `PAPERLESS_OCR_LANGUAGE` | Tesseract 语言 | eng, deu, fra 等 |
| `PAPERLESS_OCR_DESKEW` | 纠正扫描倾斜 | true, false |
| `PAPERLESS_OCR_ROTATE_PAGES` | 自动旋转 | true, false |
| `PAPERLESS_OCR_CLEAN` | 清理图像 | true, false |

## 文档导入

### 支持的文件格式

| 格式 | 类型 | 说明 |
|------|------|------|
| PDF | 文档 | 主要格式，应用 OCR |
| JPEG | 图像 | 转换为 PDF |
| PNG | 图像 | 转换为 PDF |
| TIFF | 图像 | 支持多页 |
| Office | 文档 | 通过 Gotenberg/Tika |
| 纯文本 | 文本 | 直接索引 |
| HTML | 网页 | 通过 Tika 提取 |

### 导入方式

| 方式 | 说明 | 使用场景 |
|------|------|----------|
| Web UI | 通过浏览器上传 | 手动上传 |
| 监视文件夹 | 将文件放入 consume 目录 | 扫描仪集成 |
| 邮件 | IMAP 轮询 | 邮件附件 |
| API | REST 端点 | 自动化脚本 |
| 移动端 | 响应式 Web UI | 手机扫描 |

### 使用 API

```bash
# 上传文档
curl -X POST http://localhost:8000/api/documents/post_document/ \
  -H "Authorization: Token YOUR_API_TOKEN" \
  -F "document=@/path/to/invoice.pdf" \
  -F "title=Electric Bill June 2024"

# 列出文档
curl http://localhost:8000/api/documents/ \
  -H "Authorization: Token YOUR_API_TOKEN"
```

## 标签与组织

### 核心实体

| 实体 | 用途 | 示例 |
|------|------|------|
| 标签 | 灵活的标签 | 重要、税务、医疗 |
| 通信方 | 文档来源 | 电力公司、银行 |
| 文档类型 | 分类 | 发票、信函、收据 |
| 存储路径 | 文件位置 | Finance/, Medical/ |

### 自动分类

Paperless-ngx 从您的标签模式中学习：

| 设置 | 说明 |
|------|------|
| 匹配算法 | 机器学习分类器 |
| 训练数据 | 您手动标记的文档 |
| 最少样本 | 每个类别需要 1+ 个示例 |
| 自动应用 | 导入时自动分配标签 |

### 批量操作

| 操作 | 说明 | 步骤 |
|------|------|------|
| 批量编辑 | 更改标签/类型 | 选择文档，编辑 |
| 批量删除 | 删除文档 | 选择，删除 |
| 合并 | 合并 PDF | 选择，合并 |
| 批量下载 | 导出为 ZIP | 选择，下载 |

## 搜索与检索

### 搜索语法

| 操作符 | 示例 | 结果 |
|--------|------|------|
| 纯文本 | `invoice electric` | 全文搜索 |
| 精确短语 | `"annual report"` | 短语匹配 |
| 字段搜索 | `tag:important` | 按标签过滤 |
| 日期范围 | `created:[2024-01-01 TO 2024-06-30]` | 日期过滤 |
| 包含标签 | `has:tag` | 已标记文档 |
| 仅标题 | `title:contract` | 标题搜索 |

### 保存的视图

| 组件 | 说明 |
|------|------|
| 名称 | 描述性视图名称 |
| 过滤器 | 条件组合 |
| 排序方式 | 日期、标题、相关性 |
| 显示模式 | 列表、网格或卡片 |
| 共享 | 私有或与组共享 |

## 自动化规则

### 规则组件

| 组件 | 说明 | 示例 |
|------|------|------|
| 触发器 | 规则何时触发 | 文档上传时 |
| 条件 | 匹配条件 | 标题包含 "invoice" |
| 动作 | 执行操作 | 设置标签 "Finances" |

### 规则示例

| 规则名称 | 条件 | 动作 |
|----------|------|------|
| 自动标记发票 | 标题包含 "invoice" | 添加标签: Invoice |
| 银行对账单 | 发件人为 "Bank of America" | 设置类型: Statement |
| 归档旧文档 | 创建时间超过 365 天 | 添加标签: Archive |

## 用户管理

### 权限模型

| 级别 | 访问权限 | 说明 |
|------|----------|------|
| 管理员 | 完全访问 | 系统配置 |
| 用户 | 标准访问 | 查看和编辑自己的文档 |
| 组 | 共享访问 | 共享权限 |

### 组权限

| 权限 | 说明 |
|------|------|
| 查看文档 | 只读访问 |
| 编辑文档 | 修改元数据 |
| 创建文档 | 上传新文件 |
| 删除文档 | 删除文件 |
| 管理标签 | 创建/编辑标签 |
| 管理通信方 | 创建/编辑来源 |

## 备份与恢复

| 组件 | 位置 | 方法 |
|------|------|------|
| 数据库 | PostgreSQL 卷 | pg_dump |
| 媒体文件 | Media 卷 | 文件复制 |
| 配置 | 环境变量文件 | 文件复制 |
| 完整备份 | 所有卷 | Docker 卷导出 |

```bash
# 创建备份
docker compose exec webserver document_exporter ../export

# 从备份恢复
docker compose exec webserver document_importer ../export
```

## 总结

Paperless-ngx 将纸质文档管理转变为可搜索的数字档案。其 OCR 功能、自动分类和灵活的标签系统使其适用于个人和小型企业的文档工作流。
