# Wallabag：稍后阅读应用教程

## 简介

Wallabag 是一个自托管的稍后阅读应用。它保存网页文章供离线阅读，去除广告和干扰。本教程涵盖安装、配置、浏览器集成和高级功能。

## Wallabag 与 Pocket、Instapaper 对比

| 功能 | Wallabag | Pocket | Instapaper |
|------|----------|--------|------------|
| 自托管 | 是 | 否 | 否 |
| 开源 | 是 | 否 | 否 |
| 导出格式 | EPUB、PDF、MOBI、CSV、JSON、XML | EPUB、PDF | EPUB、PDF |
| API | 是 | 是 | 是 |
| 标签 | 是 | 是 | 是 |
| 标注 | 是 | 是（高级版） | 是 |
| 全文搜索 | 是 | 是 | 是 |
| 价格 | 免费 | 免费增值 | 免费增值 |

## 安装

### Docker Compose

```yaml
version: '3'
services:
  wallabag:
    image: wallabag/wallabag:latest
    container_name: wallabag
    restart: unless-stopped
    environment:
      - SYMFONY__ENV__DOMAIN_NAME=https://read.example.com
      - SYMFONY__ENV__SERVER_NAME=Wallabag
      - SYMFONY__ENV__DATABASE_DRIVER=pdo_sqlite
      - SYMFONY__ENV__FOSUSER_REGISTRATION=false
    volumes:
      - ./wallabag-images:/var/www/wallabag/web/assets/images
      - ./wallabag-data:/var/www/wallabag/data
    ports:
      - "8080:80"
```

### 手动安装

```bash
git clone https://github.com/wallabag/wallabag.git
cd wallabag
composer install --no-dev -o --prefer-dist
php bin/console wallabag:install
```

## 核心功能

### 保存文章

| 方式 | 方法 |
|------|------|
| 浏览器扩展 | 点击 Wallabag 图标 |
| 书签工具 | JavaScript 书签 |
| URL 提交 | 在 Web 界面粘贴 URL |
| API | POST 到 /api/entries |
| RSS 导入 | 从 feed 导入 |
| Pocket 导入 | 从 Pocket 导入 |
| Instapaper 导入 | 从 Instapaper 导入 |
| Pinboard 导入 | 从 Pinboard 导入 |

### 文章属性

| 属性 | 描述 |
|------|------|
| Title | 文章标题 |
| URL | 原始链接 |
| Content | 清理后的文章文本 |
| Preview picture | 主图 |
| Reading time | 预计阅读分钟数 |
| Tags | 用户分配的标签 |
| Starred | 收藏状态 |
| Archived | 已读状态 |
| Annotations | 用户高亮和笔记 |

## Web 界面

### 导航

| 部分 | 用途 |
|------|------|
| Unread | 待读的新文章 |
| Starred | 收藏文章 |
| Archive | 已读文章 |
| Tags | 按标签浏览 |
| Search | 全文搜索 |
| Config | 账户设置 |

### 文章操作

| 操作 | 方法 |
|------|------|
| 收藏 | 点击星标图标 |
| 归档 | 点击归档图标 |
| 添加标签 | 给文章添加标签 |
| 删除 | 点击删除图标 |
| 分享 | 生成公开链接 |
| 打开原文 | 访问源 URL |
| 编辑 | 修改标题或内容 |

## 浏览器扩展

| 浏览器 | 安装 |
|--------|------|
| Chrome | Chrome Web Store |
| Firefox | Firefox Add-ons |
| Safari | Mac App Store |
| Opera | Opera Add-ons |

### 扩展功能

| 功能 | 描述 |
|------|------|
| 一键保存 | 保存当前页面 |
| 保存选区 | 保存选中的文本 |
| 带标签保存 | 保存时添加标签 |
| 自动归档 | 保存后归档 |
| 徽章计数 | 显示未读数量 |

## 移动应用

| 平台 | 应用名称 |
|------|---------|
| Android | Wallabag（F-Droid、Play Store） |
| iOS | Wallabag（App Store） |

### 应用配置

| 设置 | 值 |
|------|-----|
| Server URL | https://your-wallabag-instance.com |
| Username | 你的 Wallabag 用户名 |
| Password | 你的 Wallabag 密码 |
| Client ID | 来自 API 客户端管理 |
| Client Secret | 来自 API 客户端管理 |

## 标签

### 标签管理

| 操作 | 方法 |
|------|------|
| 添加标签 | 在文章的标签字段中输入 |
| 移除标签 | 点击标签上的 X |
| 重命名标签 | 标签管理页面 |
| 删除标签 | 标签管理页面 |
| 合并标签 | 标签管理页面 |

### 标签策略

| 策略 | 示例 |
|------|------|
| 按主题 | programming、design、science |
| 按优先级 | read-later、urgent、reference |
| 按来源 | newsletter、twitter、reddit |
| 按状态 | to-review、archived-reference |

## 标注

### 创建标注

1. 打开一篇文章。
2. 选择文本。
3. 点击"Annotate"。
4. 添加你的笔记。
5. 保存标注。

### 标注类型

| 类型 | 用途 |
|------|------|
| Highlight（高亮） | 标记重要文本 |
| Note（笔记） | 添加评论 |

## API 参考

### 认证

```bash
# 获取 OAuth2 令牌
curl -X POST https://read.example.com/oauth/v2/token \
  -d "grant_type=password" \
  -d "client_id=YOUR_CLIENT_ID" \
  -d "client_secret=YOUR_CLIENT_SECRET" \
  -d "username=YOUR_USERNAME" \
  -d "password=YOUR_PASSWORD"
```

### API 端点

| 方法 | 端点 | 描述 |
|------|------|------|
| GET | /api/entries | 列出所有条目 |
| POST | /api/entries | 创建条目 |
| GET | /api/entries/{id} | 获取条目 |
| PUT | /api/entries/{id} | 更新条目 |
| DELETE | /api/entries/{id} | 删除条目 |
| GET | /api/tags | 列出所有标签 |
| POST | /api/entries/{id}/tags | 给条目添加标签 |
| GET | /api/entries/{id}/export | 导出条目 |

### 导出格式

| 格式 | 扩展名 | 用例 |
|------|--------|------|
| EPUB | .epub | 电子阅读器 |
| PDF | .pdf | 打印 |
| MOBI | .mobi | Kindle |
| CSV | .csv | 数据分析 |
| JSON | .json | API 集成 |
| XML | .xml | 数据交换 |

## 导入和导出

### 导入来源

| 来源 | 方法 |
|------|------|
| Pocket | CSV 文件 |
| Instapaper | CSV 文件 |
| Pinboard | JSON/CSV 文件 |
| Readability | JSON 文件 |
| Firefox | JSON 书签 |
| Chrome | HTML 书签 |
| Wallabag | JSON 导出 |

### 导出

| 格式 | 命令 |
|------|------|
| 所有条目 | Settings > Export > 选择格式 |
| 按标签 | 按标签过滤，然后导出 |
| 按状态 | 过滤未读/收藏/归档，然后导出 |

## 配置

### 环境变量

| 变量 | 用途 | 默认值 |
|------|------|--------|
| SYMFONY__ENV__DOMAIN_NAME | 公开 URL | 必填 |
| SYMFONY__ENV__DATABASE_DRIVER | 数据库类型 | pdo_sqlite |
| SYMFONY__ENV__DATABASE_HOST | 数据库主机 | localhost |
| SYMFONY__ENV__DATABASE_NAME | 数据库名称 | wallabag |
| SYMFONY__ENV__DATABASE_USER | 数据库用户 | wallabag |
| SYMFONY__ENV__DATABASE_PASSWORD | 数据库密码 | wallabag |
| SYMFONY__ENV__FOSUSER_REGISTRATION | 允许注册 | false |

### 数据库选项

| 数据库 | 驱动 | 用例 |
|--------|------|------|
| SQLite | pdo_sqlite | 单用户，简单设置 |
| MySQL/MariaDB | pdo_mysql | 多用户，生产环境 |
| PostgreSQL | pdo_pgsql | 多用户，生产环境 |

## 自定义

### 自定义 CSS

在 Configuration > Settings > Custom CSS 中添加自定义样式。

### 阅读设置

| 设置 | 选项 |
|------|------|
| 字体 | Serif、Sans-serif |
| 字体大小 | Small、Medium、Large |
| 行高 | Compact、Normal、Relaxed |
| 暗色模式 | 开、关、自动 |

## 故障排除

| 问题 | 原因 | 解决方案 |
|------|------|---------|
| 无法保存文章 | JavaScript 密集型网站 | 尝试阅读模式 |
| 图片缺失 | 热链保护 | 检查代理设置 |
| 导入缓慢 | 文件过大 | 分批导入 |
| 登录失败 | 凭据错误 | 通过 CLI 重置密码 |
| API 401 | 令牌无效 | 重新生成 OAuth 凭据 |

## 总结

Wallabag 提供了一个自托管的、尊重隐私的稍后阅读解决方案。其浏览器扩展、移动应用和 API 让你在任何设备上轻松保存和阅读文章。导出选项、标签系统和标注功能使其成为研究和知识管理的强大工具。
