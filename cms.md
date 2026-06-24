# Cockpit CMS: 无头内容管理系统

## 简介

Cockpit 是一款自托管的无头内容管理系统 (CMS)，专注于结构化内容管理。与传统 CMS 平台不同，Cockpit 仅提供后端 API，允许开发者使用任何技术栈构建自定义前端。

Cockpit 轻量、灵活，专为希望完全控制内容分发而无需传统 CMS 开销的开发者设计。

## 为什么使用无头 CMS？

| 方式 | 传统 CMS | 无头 CMS |
|------|---------|---------|
| 前端 | 内置模板 | 任何框架 |
| 内容分发 | HTML 页面 | API (JSON) |
| 灵活性 | 有限 | 完全控制 |
| 多平台 | 困难 | 容易 |
| 性能 | 服务器渲染 | 优化分发 |
| 开发 | 耦合 | 解耦 |

## 为什么选择 Cockpit？

| 特性 | Cockpit | Strapi | Contentful | Sanity |
|------|---------|--------|------------|--------|
| 费用 | 免费 | 免费/OSS | 付费 | 免费增值 |
| 自托管 | 是 | 是 | 否 | 否 |
| 开源 | 是 | 是 | 否 | 否 |
| 轻量 | 非常 | 中等 | 不适用 | 不适用 |
| 学习曲线 | 低 | 中 | 中 | 中 |
| API 优先 | 是 | 是 | 是 | 是 |

## 核心功能

| 功能 | 描述 |
|------|------|
| 集合 | 结构化内容类型 |
| 内容树 | 层次化内容 |
| 表单 | 表单构建器 |
| 资源 | 媒体管理 |
| API | RESTful 和 GraphQL |
| Webhooks | 事件通知 |
| 用户和角色 | 访问控制 |
| 本地化 | 多语言内容 |
| 自定义插件 | 可扩展性 |

## 安装

### Docker 部署

```bash
# 创建目录
mkdir -p /opt/cockpit/storage

# 运行 Cockpit
docker run -d \
  --name cockpit \
  -p 8080:80 \
  -v /opt/cockpit/storage:/var/www/html/storage \
  agentejo/cockpit
```

### Docker Compose

```yaml
version: '3'
services:
  cockpit:
    image: agentejo/cockpit
    container_name: cockpit
    restart: unless-stopped
    ports:
      - "8080:80"
    volumes:
      - ./storage:/var/www/html/storage
```

### 手动安装

```bash
# 下载最新版本
wget https://github.com/agentejo/cockpit/releases/latest/download/cockpit.zip

# 解压到 Web 目录
unzip cockpit.zip -d /var/www/html/cockpit

# 设置权限
chmod -R 777 /var/www/html/cockpit/storage
```

### 系统要求

| 要求 | 最低 | 推荐 |
|------|------|------|
| PHP | 7.4+ | 8.0+ |
| 扩展 | json, gd, mbstring | +curl, +zip |
| Web 服务器 | Apache/Nginx | Nginx |
| 存储 | 50MB | 500MB |

## 快速上手

### 初始设置

| 步骤 | 操作 |
|------|------|
| 1 | 访问 Web 界面 |
| 2 | 创建管理员账户 |
| 3 | 设置站点名称 |
| 4 | 创建第一个集合 |
| 5 | 添加内容 |
| 6 | 通过 API 访问 |

### 仪表板概述

| 区域 | 用途 |
|------|------|
| 集合 | 管理内容类型 |
| 内容树 | 层次化内容 |
| 资源 | 媒体库 |
| 表单 | 表单提交 |
| 账户 | 用户管理 |
| 设置 | 系统配置 |

## 集合

集合是 Cockpit 的核心内容类型。

### 字段类型

| 类型 | 描述 | 使用场景 |
|------|------|---------|
| 文本 | 单行文本 | 标题、名称 |
| 文本区域 | 多行文本 | 描述 |
| WYSIWYG | 富文本编辑器 | 正文内容 |
| 布尔 | 真/假切换 | 发布状态 |
| 选择 | 下拉选择 | 分类 |
| 标签 | 多标签 | 关键词 |
| 图片 | 图片上传 | 特色图片 |
| 画廊 | 多图片 | 图片画廊 |
| 文件 | 文件上传 | 文档 |
| 日期 | 日期选择器 | 发布日期 |
| 时间 | 时间选择器 | 活动时间 |
| 颜色 | 颜色选择器 | 主题颜色 |
| 对象 | JSON 对象 | 自定义数据 |
| 数组 | 项目列表 | 重复字段 |

### 创建集合

| 步骤 | 操作 |
|------|------|
| 1 | 导航到集合 |
| 2 | 点击"创建集合" |
| 3 | 输入集合名称 |
| 4 | 添加字段 |
| 5 | 配置字段设置 |
| 6 | 保存集合 |

### 集合设置

| 设置 | 描述 |
|------|------|
| 名称 | 集合标识符 |
| 可排序 | 启用拖拽排序 |
| 排序字段 | 默认排序列 |
| 在 API 中 | 包含在 API 输出中 |
| 预览 URL | 内容预览链接 |

## 内容树

内容树提供层次化内容组织。

| 功能 | 描述 |
|------|------|
| 嵌套结构 | 父子关系 |
| 拖拽 | 重新排序内容 |
| 多根 | 独立层级 |
| 基于路径 | URL 友好路径 |

### 使用场景

| 使用场景 | 示例 |
|---------|------|
| 导航菜单 | 主菜单、页脚菜单 |
| 页面层级 | 关于 > 团队 > 成员 |
| 分类 | 产品 > 电子产品 > 手机 |
| 站点地图 | 网站结构 |

## 资源管理

### 支持的文件类型

| 类别 | 格式 |
|------|------|
| 图片 | JPG, PNG, GIF, WebP, SVG |
| 文档 | PDF, DOC, XLS |
| 视频 | MP4, WebM |
| 音频 | MP3, OGG |
| 归档 | ZIP, RAR |

### 图片功能

| 功能 | 描述 |
|------|------|
| 缩略图 | 自动生成预览 |
| 图片信息 | 尺寸、文件大小 |
| 替代文本 | 无障碍元数据 |
| 焦点 | 裁剪锚点 |

### 资源组织

| 方式 | 描述 |
|------|------|
| 文件夹 | 目录结构 |
| 标签 | 分类 |
| 搜索 | 全文搜索 |
| 过滤 | 类型、日期、大小 |

## API

### REST API 端点

| 端点 | 方法 | 描述 |
|------|------|------|
| `/api/content/get/{collection}` | POST | 获取内容项 |
| `/api/content/item/{collection}` | POST | 获取单个项 |
| `/api/content/items/{collection}` | POST | 获取多个项 |
| `/api/assets` | POST | 获取资源 |
| `/api/forms/submit/{form}` | POST | 提交表单 |

### API 认证

```bash
# 获取 API 令牌
curl -X POST https://your-cockpit.com/api/auth/token \
  -H "Content-Type: application/json" \
  -d '{"user":"admin","password":"password"}'

# 使用 API 令牌
curl -H "Cockpit-Token: YOUR_API_TOKEN" \
  https://your-cockpit.com/api/content/get/articles
```

### GraphQL API

```graphql
# 查询内容
query {
  articles(limit: 10, sort: {_created: -1}) {
    title
    content
    image {
      path
    }
  }
}
```

### 过滤和排序

```json
{
  "filter": {
    "published": true,
    "category": "news"
  },
  "sort": {
    "_created": -1
  },
  "limit": 10,
  "skip": 0
}
```

## Webhooks

### Webhook 事件

| 事件 | 触发 |
|------|------|
| collection.save.before | 保存项之前 |
| collection.save.after | 保存项之后 |
| collection.remove.before | 移除项之前 |
| collection.remove.after | 移除项之后 |
| assets.save.before | 保存资源之前 |
| assets.save.after | 保存资源之后 |

### Webhook 配置

| 设置 | 描述 |
|------|------|
| 名称 | Webhook 标识符 |
| URL | 回调 URL |
| 头部 | 自定义头部 |
| 内容类型 | JSON 或表单数据 |
| 触发器 | 监听的事件 |

## 用户和角色

### 用户角色

| 角色 | 权限 |
|------|------|
| 管理员 | 完全访问 |
| 编辑 | 内容管理 |
| 作者 | 创建/编辑自己的内容 |
| 查看者 | 只读访问 |

### 权限级别

| 级别 | 描述 |
|------|------|
| 集合 | 每集合访问 |
| 内容树 | 每树访问 |
| 资源 | 媒体库访问 |
| 表单 | 表单管理 |
| 设置 | 系统配置 |

## 本地化

### 多语言内容

| 功能 | 描述 |
|------|------|
| 语言 | 定义支持的语言 |
| 字段 | 每语言字段值 |
| 回退 | 默认语言回退 |
| API | 按语言查询 |

### 语言配置

| 设置 | 描述 |
|------|------|
| 默认 | 主要语言 |
| 语言 | 支持的语言列表 |
| 可本地化字段 | 带翻译的字段 |

## 自定义插件

### 插件类型

| 类型 | 描述 |
|------|------|
| 集合 | 自定义字段类型 |
| 控制器 | API 端点 |
| 命令 | CLI 命令 |
| 管理 | 仪表板组件 |

### 创建插件

| 步骤 | 操作 |
|------|------|
| 1 | 创建插件目录 |
| 2 | 定义 bootstrap.php |
| 3 | 实现功能 |
| 4 | 注册到 Cockpit |
| 5 | 测试插件 |

## 集成示例

### JavaScript (Fetch)

```javascript
// 从 Cockpit 获取内容
const response = await fetch('https://your-cockpit.com/api/content/get/articles', {
  method: 'POST',
  headers: {
    'Content-Type': 'application/json',
    'Cockpit-Token': 'YOUR_API_TOKEN'
  },
  body: JSON.stringify({
    filter: { published: true },
    limit: 10
  })
});

const articles = await response.json();
```

### PHP

```php
// 从 Cockpit 获取内容
$ch = curl_init('https://your-cockpit.com/api/content/get/articles');
curl_setopt($ch, CURLOPT_POST, true);
curl_setopt($ch, CURLOPT_HTTPHEADER, [
    'Content-Type: application/json',
    'Cockpit-Token: YOUR_API_TOKEN'
]);
curl_setopt($ch, CURLOPT_POSTFIELDS, json_encode([
    'filter' => ['published' => true],
    'limit' => 10
]));
$response = curl_exec($ch);
```

### Python

```python
import requests

response = requests.post(
    'https://your-cockpit.com/api/content/get/articles',
    headers={
        'Content-Type': 'application/json',
        'Cockpit-Token': 'YOUR_API_TOKEN'
    },
    json={
        'filter': {'published': True},
        'limit': 10
    }
)

articles = response.json()
```

## 故障排除

| 问题 | 原因 | 解决方案 |
|------|------|---------|
| 无法安装 | PHP 版本 | 升级 PHP |
| API 错误 | 令牌错误 | 验证 API 令牌 |
| 上传失败 | 文件权限 | 检查存储权限 |
| API 缓慢 | 无缓存 | 启用 API 缓存 |

## 更多资源

| 资源 | URL |
|------|-----|
| 官方网站 | cockpitcms.com |
| GitHub | github.com/agentejo/cockpit |
| 文档 | cockpitcms.com/documentation |
| 社区 | cockpitcms.com/community |
