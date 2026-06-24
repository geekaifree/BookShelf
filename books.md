# Readarr 书籍收藏管理教程

## 简介

Readarr 是一款面向 Usenet 和 BitTorrent 用户的书籍收藏管理器。它监控 RSS 源以获取新书，并自动下载、排序和重命名。它支持电子书和有声书，与下载客户端和电子书管理工具集成。

| 特性 | 描述 |
|---------|-------------|
| 书籍监控 | 跟踪想要的书籍并搜索可用发布 |
| 有声书支持 | 与电子书并行管理有声书收藏 |
| 质量配置文件 | 定义首选格式和质量级别 |
| 作者监控 | 关注作者以自动获取新发布 |
| 元数据管理 | 从多个来源获取书籍信息 |

## 架构

### 系统组件

| 组件 | 角色 |
|-----------|------|
| Readarr | 书籍监控和管理应用 |
| 索引器 | 查找书籍发布的来源 |
| 下载客户端 | 执行下载的软件 |
| Calibre | 可选的电子书管理和转换 |
| Audiobookshelf | 可选的有声书服务器 |

### 工作流程

| 步骤 | 描述 |
|------|-------------|
| 1 | 用户向 Readarr 添加作者或书籍 |
| 2 | Readarr 在索引器中监控匹配的发布 |
| 3 | 根据质量配置文件评估发布 |
| 4 | 将下载请求发送到已配置的下载客户端 |
| 5 | 文件被下载并导入 |
| 6 | 获取并应用元数据 |
| 7 | 可选：将文件发送到 Calibre 进行转换 |

## 安装

### Docker 部署

```bash
docker run -d \
  --name=readarr \
  -p 8787:8787 \
  -v /path/to/config:/config \
  -v /path/to/books:/books \
  -v /path/to/downloads:/downloads \
  -e PUID=1000 \
  -e PGID=1000 \
  -e TZ=UTC \
  --restart unless-stopped \
  lscr.io/linuxserver/readarr:develop
```

### Docker Compose

```yaml
version: "3.8"
services:
  readarr:
    image: lscr.io/linuxserver/readarr:develop
    container_name: readarr
    environment:
      - PUID=1000
      - PGID=1000
      - TZ=UTC
    volumes:
      - ./config:/config
      - /path/to/books:/books
      - /path/to/audiobooks:/audiobooks
      - /path/to/downloads:/downloads
    ports:
      - "8787:8787"
    restart: unless-stopped

  calibre:
    image: lscr.io/linuxserver/calibre
    container_name: calibre
    environment:
      - PUID=1000
      - PGID=1000
      - TZ=UTC
    volumes:
      - ./calibre-config:/config
      - /path/to/books:/books
    ports:
      - "8080:8080"
    restart: unless-stopped
```

## 配置

### 添加作者

| 方式 | 描述 |
|--------|-------------|
| 搜索 | 在 Readarr 界面中按作者名搜索 |
| Goodreads | 从 Goodreads 作者页面导入 |
| 手动 | 通过作者元数据 ID 添加 |

### 添加书籍

| 方式 | 描述 |
|--------|-------------|
| 作者页面 | 浏览作者目录并选择书籍 |
| 搜索 | 按书名或 ISBN 搜索 |
| 导入 | 从库文件夹导入现有书籍 |

### 质量配置文件

| 配置文件 | 使用场景 |
|---------|----------|
| 仅电子书 | 仅下载电子书格式 |
| 仅有声书 | 仅有声书格式 |
| 混合 | 接受电子书和有声书发布 |
| 自定义 | 定义特定格式偏好 |

### 书籍格式

| 格式 | 类型 | 典型用途 |
|--------|------|-------------|
| EPUB | 电子书 | 标准电子书格式，广泛支持 |
| MOBI | 电子书 | Kindle 兼容格式 |
| PDF | 电子书 | 固定版式文档 |
| AZW3 | 电子书 | Amazon Kindle 格式 |
| MP3 | 有声书 | 压缩有声书 |
| M4A | 有声书 | AAC 有声书 |
| M4B | 有声书 | 带章节的有声书 |
| FLAC | 有声书 | 无损有声书 |

### 质量定义

| 质量 | 描述 | 优先级 |
|---------|-------------|----------|
| EPUB | 标准电子书 | 高 |
| AZW3 | Kindle 格式 | 中 |
| MOBI | 旧版 Kindle 格式 | 低 |
| M4B | 带章节有声书 | 高 |
| MP3 | 压缩音频 | 中 |
| FLAC | 无损音频 | 最高 |

## 下载客户端

### 支持的客户端

| 客户端 | 协议 | 备注 |
|--------|----------|-------|
| qBittorrent | Torrent | 推荐的 Torrent 客户端 |
| Transmission | Torrent | 轻量级选项 |
| Deluge | Torrent | 基于插件的架构 |
| SABnzbd | Usenet | 流行的 Usenet 下载器 |
| NZBGet | Usenet | 高效的 Usenet 客户端 |
| Flood | Torrent | rTorrent 的现代 Web UI |

### 客户端配置

| 设置 | 描述 |
|---------|-------------|
| 主机 | 下载客户端的 IP 地址或主机名 |
| 端口 | API 访问的端口号 |
| 用户名 | 认证用户名 |
| 密码 | 认证密码 |
| 分类 | Readarr 项目的下载分类 |
| 优先级 | 下载优先级 |

## Calibre 集成

### Calibre 功能

| 功能 | 描述 |
|---------|-------------|
| 格式转换 | 在电子书格式之间转换 |
| 元数据编辑 | 编辑书籍元数据和封面 |
| 库管理 | 组织和编目电子书收藏 |
| 内容服务器 | 通过 HTTP 提供书籍服务 |

### 集成设置

| 步骤 | 操作 |
|------|--------|
| 1 | 安装并配置 Calibre，启用内容服务器 |
| 2 | 在 Readarr 中，导航到设置 > Calibre |
| 3 | 输入 Calibre 内容服务器 URL 和端口 |
| 4 | 配置 Calibre 的自动添加文件夹 |
| 5 | 设置格式转换偏好 |

### Calibre 内容服务器

| 设置 | 描述 |
|---------|-------------|
| 端口 | 默认 8080 |
| 认证 | 可选的用户名/密码 |
| 库路径 | Calibre 库文件夹路径 |
| 自动添加 | 监视新书籍的文件夹 |

## 文件管理

### 命名模式

| 标记 | 描述 | 示例 |
|-------|-------------|---------|
| {Author Name} | 作者姓名 | Stephen King |
| {Book Title} | 书名 | It |
| {Release Year} | 出版年份 | 1986 |
| {Quality} | 质量/格式名称 | EPUB |
| {Book ISBN} | ISBN 标识符 | 978-0-670-81302-4 |

### 推荐模式

| 类型 | 模式 | 示例 |
|------|---------|---------|
| 单作者 | `{Author Name}/{Book Title}` | Stephen King/It.epub |
| 带年份 | `{Author Name}/{Book Title} ({Release Year})` | Stephen King/It (1986).epub |
| 带质量 | `{Author Name}/{Book Title} {Quality}` | Stephen King/It EPUB.epub |

### 文件夹结构

```
/books/
  Stephen King/
    It (1986).epub
    The Shining (1977).epub
    Pet Sematary (1983).epub
  Terry Pratchett/
    The Colour of Magic (1983).epub
    Mort (1987).epub
/audiobooks/
  Stephen King/
    It (1986)/
      Chapter 01.mp3
      Chapter 02.mp3
```

## 元数据来源

### 支持的来源

| 来源 | 提供的数据 |
|--------|---------------|
| Goodreads | 评分、评论、类似书籍 |
| Google Books | 书籍详情、描述、封面 |
| Open Library | 免费书籍数据和封面 |
| ISBNdb | 基于 ISBN 的书籍信息 |
| WorldCat | 图书馆目录数据 |

### 元数据字段

| 字段 | 描述 |
|-------|-------------|
| Title | 书名 |
| Author | 作者姓名 |
| Publisher | 出版社 |
| Publication date | 原始出版年份 |
| ISBN | 国际标准书号 |
| Description | 书籍简介 |
| Genre | 书籍分类 |
| Cover | 书籍封面图片 |

## 通知

### 支持的服务

| 服务 | 配置 |
|---------|--------------|
| Email | SMTP 服务器设置 |
| Discord | Webhook URL |
| Telegram | Bot Token 和 Chat ID |
| Slack | Webhook URL |
| Webhook | 自定义 HTTP 端点 |

### 通知事件

| 事件 | 描述 |
|-------|-------------|
| 抓取 | 当发布发送到下载客户端时 |
| 导入 | 当书籍成功导入时 |
| 升级 | 当书籍升级到更好质量时 |
| 重命名 | 当书籍文件被重命名时 |
| 作者添加 | 当添加新作者时 |
| 健康 | 当健康检查出现问题时 |

## API 访问

### 关键端点

| 端点 | 方法 | 描述 |
|----------|--------|-------------|
| `/api/v1/book` | GET | 列出所有书籍 |
| `/api/v1/author` | GET | 列出所有作者 |
| `/api/v1/book/{id}` | GET | 获取特定书籍 |
| `/api/v1/command` | POST | 触发命令 |
| `/api/v1/calendar` | GET | 获取即将发布的书籍 |

## 故障排除

### 常见问题

| 问题 | 原因 | 解决方案 |
|-------|-------|----------|
| 未找到结果 | 未配置索引器 | 添加支持书籍的索引器 |
| 下载了错误格式 | 质量配置文件过于宽松 | 调整质量定义 |
| 元数据缺失 | 元数据来源不可用 | 检查 Goodreads/Google Books 访问 |
| Calibre 未导入 | 内容服务器未运行 | 启动 Calibre 内容服务器 |
| 重复下载 | 多个索引器返回同一本书 | 启用首选词设置 |

## 总结

| 主题 | 核心要点 |
|-------|-------------|
| 用途 | 自动化书籍和有声书收藏管理 |
| 格式 | 支持 EPUB、MOBI、PDF、M4B、MP3 等 |
| 集成 | 与 Calibre 配合进行格式转换和管理 |
| 索引器 | 使用 Torrent 和 Usenet 索引器获取书籍来源 |
| 组织 | 基于作者的自动文件夹结构 |
| 元数据 | 从 Goodreads 和 Google Books 获取书籍信息 |
