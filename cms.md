# 内容管理系统

> 本文档整合了以下源文件：cms.md, headless.md, flat.md, grav.md, pagekit.md, statamic.md, strapi.md, keystone.md

---

## 来源：cms.md

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


---

## 来源：headless.md

## 简介

Directus 是一个开源的无头 CMS，为任何 SQL 数据库提供实时 REST 和 GraphQL API 包装。它提供无代码管理应用来管理内容，同时让开发者完全控制数据层。本教程涵盖设置、数据建模、API 使用和自定义。

## 架构

| 组件 | 技术 | 用途 |
|------|------|------|
| API | Node.js (Express) | REST 和 GraphQL 端点 |
| Admin App | Vue.js | 无代码管理 UI |
| 数据库 | PostgreSQL/MySQL/SQLite/MS SQL | 数据存储 |
| 实时 | WebSocket | 实时更新 |
| 存储 | 本地/S3/Azure/GCS | 文件管理 |

## 安装

### Docker Compose

```yaml
version: "3"
services:
  directus:
    image: directus/directus:latest
    ports:
      - "8055:8055"
    volumes:
      - directus_uploads:/directus/uploads
      - directus_extensions:/directus/extensions
    environment:
      KEY: "random-key-here"
      SECRET: "random-secret-here"
      DB_CLIENT: "pg"
      DB_HOST: "database"
      DB_PORT: "5432"
      DB_DATABASE: "directus"
      DB_USER: "directus"
      DB_PASSWORD: "secure_password"
      ADMIN_EMAIL: "admin@example.com"
      ADMIN_PASSWORD: "admin_password"
    depends_on:
      - database
  database:
    image: postgres:15
    environment:
      POSTGRES_DB: directus
      POSTGRES_USER: directus
      POSTGRES_PASSWORD: secure_password
    volumes:
      - db_data:/var/lib/postgresql/data
volumes:
  directus_uploads:
  directus_extensions:
  db_data:
```

### NPX

```bash
npx directus bootstrap
npx directus start
```

## 核心概念

### 数据模型

| 概念 | 描述 | SQL 等价物 |
|------|------|-----------|
| Collection | 数据实体 | 表 |
| Field | 集合的属性 | 列 |
| Item | 单条记录 | 行 |
| Relation | 集合间的连接 | 外键 |

### 系统集合

| 集合 | 用途 |
|------|------|
| `directus_users` | 用户账户 |
| `directus_roles` | 用户角色 |
| `directus_permissions` | 访问控制规则 |
| `directus_files` | 上传的文件 |
| `directus_folders` | 文件组织 |
| `directus_presets` | 保存的筛选/视图预设 |
| `directus_activity` | 审计日志 |
| `directus_revisions` | 项目版本历史 |
| `directus_settings` | 系统配置 |

## 数据建模

### 创建集合

1. 导航到 Settings > Data Model。
2. 点击"Create Collection"。
3. 输入集合名称（例如 `articles`）。
4. 配置可选字段（status、sort 等）。
5. 保存。

### 字段类型

| 类型 | 描述 | 示例 |
|------|------|------|
| Input | 单行文本 | 标题、名称 |
| Textarea | 多行文本 | 描述 |
| WYSIWYG | 富文本编辑器 | 正文内容 |
| Markdown | Markdown 编辑器 | 技术内容 |
| Boolean | 真/假开关 | 已发布、精选 |
| Integer | 整数 | 计数、排序 |
| Decimal | 小数 | 价格、评分 |
| DateTime | 日期和时间 | 创建日期 |
| Date | 仅日期 | 生日 |
| Time | 仅时间 | 预约时间 |
| Dropdown | 单选 | 类别、状态 |
| Tags | 多标签 | 标签、关键词 |
| Image | 图片文件引用 | 特色图片 |
| File | 文件引用 | 附件 |
| JSON | 任意 JSON 数据 | 配置 |
| UUID | 自动生成 UUID | 外部引用 |
| Auto Increment | 顺序编号 | 订单号 |

### 创建字段

1. 导航到集合。
2. 点击"Create Field"。
3. 选择字段类型。
4. 配置名称、界面和验证。
5. 设置关系（如适用）。
6. 保存。

### 关系

| 类型 | 描述 | 示例 |
|------|------|------|
| Many-to-One | 多个项目引用一个 | 文章有一个作者 |
| One-to-Many | 一个项目有多个 | 作者有多篇文章 |
| Many-to-Many | 多个项目链接多个 | 文章有多个标签 |
| One-to-One | 一个项目链接一个 | 用户有一个个人资料 |

#### 创建关系

1. 添加类型为"Related to Collection"的新字段。
2. 选择目标集合。
3. 选择关系类型。
4. 配置外键字段。
5. 保存。

## API 访问

### REST API

| 端点 | 方法 | 描述 |
|------|------|------|
| `/items/{collection}` | GET | 列出项目 |
| `/items/{collection}/{id}` | GET | 获取单个项目 |
| `/items/{collection}` | POST | 创建项目 |
| `/items/{collection}/{id}` | PATCH | 更新项目 |
| `/items/{collection}/{id}` | DELETE | 删除项目 |

### 认证

```bash
# 登录
curl -X POST https://directus.example.com/auth/login \
  -H "Content-Type: application/json" \
  -d '{"email": "user@example.com", "password": "password"}'

# 使用 token
curl -H "Authorization: Bearer ACCESS_TOKEN" \
  https://directus.example.com/items/articles
```

### 筛选

```bash
# 按状态筛选
GET /items/articles?filter[status][_eq]=published

# 按日期范围筛选
GET /items/articles?filter[date_published][_gte]=2024-01-01

# 多个条件
GET /items/articles?filter[status][_eq]=published&filter[author][_eq]=5
```

### 筛选操作符

| 操作符 | 描述 | 示例 |
|--------|------|------|
| `_eq` | 等于 | `?filter[status][_eq]=published` |
| `_neq` | 不等于 | `?filter[status][_neq]=draft` |
| `_gt` | 大于 | `?filter[price][_gt]=100` |
| `_gte` | 大于等于 | `?filter[price][_gte]=50` |
| `_lt` | 小于 | `?filter[price][_lt]=200` |
| `_lte` | 小于等于 | `?filter[price][_lte]=150` |
| `_in` | 在列表中 | `?filter[status][_in]=published,featured` |
| `_contains` | 包含文本 | `?filter[title][_contains]=tutorial` |
| `_between` | 在值之间 | `?filter[price][_between]=50,100` |
| `_null` | 为空 | `?filter[deleted_at][_null]=true` |

### 排序和分页

```bash
# 按日期降序排序
GET /items/articles?sort=-date_created

# 分页
GET /items/articles?page=1&limit=20

# 字段选择
GET /items/articles?fields=id,title,author.name
```

### GraphQL

```graphql
query {
  articles(
    filter: { status: { _eq: "published" } }
    sort: ["-date_created"]
    limit: 10
  ) {
    id
    title
    body
    author {
      name
      avatar {
        id
      }
    }
    tags {
      tags_id {
        name
      }
    }
  }
}
```

## 权限

### 基于角色的访问控制

| 级别 | 描述 |
|------|------|
| System Access | 可以访问管理应用 |
| Admin | 完全访问一切 |
| Public | 未认证的 API 访问 |
| Custom Roles | 细粒度的每集合权限 |

### 权限配置

| 权限 | 选项 |
|------|------|
| Create | None、Full、Custom |
| Read | None、Full、Custom |
| Update | None、Full、Custom |
| Delete | None、Full、Custom |

### 自定义权限

使用自定义权限限制对特定项目的访问。

```json
{
  "id": {
    "_eq": "$CURRENT_USER"
  }
}
```

此筛选器允许用户仅读取自己的项目。

## Flows（自动化）

### Flow 组件

| 组件 | 描述 |
|------|------|
| Trigger | 启动 flow 的事件 |
| Operation | 要执行的操作 |
| Condition | if/then 逻辑 |

### 触发器类型

| 类型 | 描述 |
|------|------|
| Event Hook | 在 CRUD 操作时触发 |
| Schedule | 基于 cron 的调度 |
| Webhook | 外部 HTTP 触发 |
| Manual | 用户发起 |

### 操作类型

| 类型 | 描述 |
|------|------|
| Create Item | 添加新记录 |
| Read Item | 获取记录 |
| Update Item | 修改记录 |
| Delete Item | 删除记录 |
| Send Email | 发送通知 |
| Webhook Request | 调用外部 API |
| Run Script | 执行自定义代码 |
| Transform Data | 映射/转换数据 |

### 示例 Flow：自动发布

```
触发器：文章创建（status = "review"）
  |
  v
条件：作者是否受信任？
  |
  是 -> 更新项目：设置 status = "published"
  否 -> 发送邮件：通知编辑审查
```

## 文件和媒体

### 文件上传

| 方法 | 描述 |
|------|------|
| Admin UI | 在 Files 模块中拖拽 |
| API | POST 到 /files 使用 multipart 表单 |
| Relation | 附加到项目字段 |

### 文件配置

| 设置 | 描述 |
|------|------|
| Storage adapter | 本地、S3、Azure、GCS |
| Max file size | 上传限制 |
| Allowed types | MIME 类型限制 |
| Transform | 上传时自动调整大小 |

### 图片转换

```bash
# 调整图片大小
GET /assets/{id}?width=300&height=200&fit=cover

# 格式转换
GET /assets/{id}?format=webp

# 质量调整
GET /assets/{id}?quality=80
```

## 扩展

### 扩展类型

| 类型 | 描述 | 语言 |
|------|------|------|
| Interface | 自定义字段 UI | Vue.js |
| Display | 自定义字段显示 | Vue.js |
| Layout | 自定义集合视图 | Vue.js |
| Module | 自定义管理部分 | Vue.js |
| Hook | API 事件处理器 | JavaScript |
| Endpoint | 自定义 API 路由 | JavaScript |
| Theme | 管理应用主题 | CSS |

### 创建 Hook 扩展

```javascript
// extensions/hooks/auto-slug/index.js
module.exports = function registerHook({ action }) {
  action('items.create', async ({ payload, collection }) => {
    if (collection === 'articles' && payload.title && !payload.slug) {
      payload.slug = payload.title
        .toLowerCase()
        .replace(/[^a-z0-9]+/g, '-')
        .replace(/(^-|-$)/g, '');
    }
  });
};
```

### 创建 Endpoint 扩展

```javascript
// extensions/endpoints/custom-api/index.js
module.exports = function registerEndpoint({ router }) {
  router.get('/stats', async (req, res) => {
    const articles = await req.database('articles').count('* as total');
    const users = await req.database('directus_users').count('* as total');
    res.json({
      articles: articles[0].total,
      users: users[0].total
    });
  });
};
```

## Webhooks 和实时

### Webhooks

在 Settings > Webhooks 中配置 webhooks。

| 设置 | 描述 |
|------|------|
| URL | 要通知的端点 |
| Method | HTTP 方法 |
| Headers | 自定义头 |
| Trigger | 监听哪些事件 |
| Collection | 哪个集合 |

### 实时订阅

```javascript
import { createDirectus, realtime } from '@directus/sdk';

const client = createDirectus('https://directus.example.com')
  .with(realtime());

// 订阅变更
const subscription = client.subscribe('articles', {
  event: 'create',
  query: { fields: ['id', 'title', 'status'] }
});

for await (const item of subscription) {
  console.log('New article:', item.data[0]);
}
```

## 快照和迁移

### 架构快照

```bash
# 导出架构
npx directus schema snapshot ./snapshot.yaml

# 应用架构
npx directus schema apply ./snapshot.yaml
```

## 备份

### 备份组件

| 组件 | 方法 |
|------|------|
| 数据库 | pg_dump、mysqldump |
| 上传文件 | rsync 或 rclone |
| 扩展 | 文件复制 |
| .env | 文件复制 |

## 总结

Directus 提供了一个灵活的无头 CMS，为任何 SQL 数据库提供 REST 和 GraphQL API 包装。通过集合和字段建模数据，配置细粒度权限，使用 Flows 构建自动化工作流程。管理应用提供无代码界面用于内容管理，而开发者获得完全的 API 访问来构建应用程序。


---

## 来源：flat.md

## 简介

Bolt CMS（也称为 Bolt）是一个轻量级的开源内容管理系统，专为开发者和内容编辑者设计。它使用扁平文件方式进行配置，同时将内容存储在数据库中。本教程涵盖安装、内容建模、主题和日常使用。

## 架构

| 组件 | 技术 | 用途 |
|------|------|------|
| 后端 | Symfony (PHP) | 应用框架 |
| 存储 | SQLite/MySQL/PostgreSQL | 内容存储 |
| 模板 | Twig | HTML 渲染 |
| 管理 | 内置面板 | 内容管理 |
| API | REST 端点 | 无头访问 |

## 安装

### Composer

```bash
composer create-project bolt/project mysite
cd mysite
php bin/console bolt:setup
```

### Docker

```yaml
version: "3"
services:
  bolt:
    image: bolt/core:latest
    ports:
      - "80:80"
    volumes:
      - ./bolt-data:/var/www/html
    depends_on:
      - database
  database:
    image: mariadb:10
    environment:
      MYSQL_ROOT_PASSWORD: root
      MYSQL_DATABASE: bolt
      MYSQL_USER: bolt
      MYSQL_PASSWORD: bolt
```

### Web 服务器配置

```nginx
server {
    listen 80;
    server_name mysite.example.com;
    root /var/www/html/public;
    index index.php;

    location / {
        try_files $uri $uri/ /index.php?$query_string;
    }

    location ~ \.php$ {
        fastcgi_pass php:9000;
        fastcgi_param SCRIPT_FILENAME $document_root$fastcgi_script_name;
        include fastcgi_params;
    }
}
```

## 内容类型

内容类型定义内容的结构。它们在 YAML 配置文件中定义。

### 定义内容类型

```yaml
# config/bolt/contenttypes.yaml
pages:
    name: Pages
    singular_name: Page
    fields:
        title:
            type: text
            class: large
            group: content
        slug:
            type: slug
            uses: title
        body:
            type: html
            height: 300px
        image:
            type: image
    taxonomy: [ groups ]
    listing_records: 10
    default_status: published
    sort: -datepublish
```

### 字段类型

| 类型 | 描述 | 使用场景 |
|------|------|----------|
| text | 单行文本 | 标题、名称 |
| html | 富文本编辑器 | 正文内容 |
| markdown | Markdown 编辑器 | 技术内容 |
| image | 图片上传 | 特色图片 |
| file | 文件上传 | 文档、下载 |
| video | 视频嵌入 | YouTube、Vimeo |
| textarea | 纯文本多行 | 描述 |
| date | 日期选择器 | 活动、截止日期 |
| datetime | 日期和时间选择器 | 日程安排 |
| select | 下拉选择 | 类别、状态 |
| checkbox | 布尔开关 | 精选、已发布 |
| number | 数值 | 价格、数量 |
| email | 邮箱地址 | 联系信息 |
| embed | OEmbed | 社交媒体嵌入 |
| geolocation | 地图坐标 | 位置数据 |
| repeater | 可重复字段 | 多个条目 |
| block | 内容块 | 灵活布局 |

### 多个内容类型

```yaml
blogposts:
    name: Blog Posts
    singular_name: Blog Post
    fields:
        title:
            type: text
            class: large
        slug:
            type: slug
            uses: title
        image:
            type: image
        body:
            type: html
        tags:
            type: taxonomy
            taxonomy: tags
    relations:
        pages:
            multiple: false
    taxonomy: [ categories, tags ]
    record_template: blogpost.twig

entries:
    name: Entries
    singular_name: Entry
    fields:
        title:
            type: text
        body:
            type: markdown
    listing_records: 20
```

## 模板（主题）

### 主题结构

```
mytheme/
  index.twig
  record.twig
  listing.twig
  _header.twig
  _footer.twig
  _aside.twig
  css/
    style.css
  js/
    main.js
```

### 基础模板

```twig
{# index.twig #}
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>{{ config.get('general/sitename') }}</title>
    <link rel="stylesheet" href="{{ asset('css/style.css', 'theme') }}">
</head>
<body>
    {% include '_header.twig' %}

    <main>
        {% block content %}
            {% for record in records %}
                <article>
                    <h2><a href="{{ record|link }}">{{ record.title }}</a></h2>
                    {{ record|excerpt(300) }}
                </article>
            {% endfor %}
        {% endblock %}
    </main>

    {% include '_footer.twig' %}
</body>
</html>
```

### 记录模板

```twig
{# record.twig #}
{% extends 'index.twig' %}

{% block content %}
<article class="record">
    <h1>{{ record.title }}</h1>
    <time>{{ record.datepublish|date('F j, Y') }}</time>

    {% if record.image %}
        <img src="{{ record.image|thumbnail(800, 600) }}"
             alt="{{ record.title }}">
    {% endif %}

    <div class="body">
        {{ record.body }}
    </div>

    {% if record.taxonomy.tags is defined %}
        <div class="tags">
            {% for tag in record.taxonomy.tags %}
                <span class="tag">{{ tag }}</span>
            {% endfor %}
        </div>
    {% endif %}
</article>
{% endblock %}
```

### 列表模板

```twig
{# listing.twig #}
{% extends 'index.twig' %}

{% block content %}
{% for record in records %}
    <div class="card">
        <h2><a href="{{ record|link }}">{{ record.title }}</a></h2>
        <p>{{ record|excerpt(200) }}</p>
    </div>
{% endfor %}

{{ pager(records, template='helpers/_pager.html') }}
{% endblock %}
```

## Twig 函数和过滤器

### 常用过滤器

| 过滤器 | 描述 | 示例 |
|--------|------|------|
| `\|link` | 获取记录 URL | `{{ record\|link }}` |
| `\|excerpt` | 截断文本 | `{{ record\|excerpt(300) }}` |
| `\|date` | 格式化日期 | `{{ record.datepublish\|date('Y-m-d') }}` |
| `\|raw` | 输出未转义的 HTML | `{{ record.body\|raw }}` |
| `\|thumbnail` | 调整图片大小 | `{{ image\|thumbnail(400, 300) }}` |
| `\|markdown` | 解析 markdown | `{{ text\|markdown }}` |
| `\|json_decode` | 解析 JSON 字符串 | `{{ data\|json_decode }}` |

### 常用函数

| 函数 | 描述 | 示例 |
|------|------|------|
| `path()` | 生成 URL | `{{ path('homepage') }}` |
| `url()` | 绝对 URL | `{{ url('page', {'slug': 'about'}) }}` |
| `asset()` | 主题资源路径 | `{{ asset('css/style.css', 'theme') }}` |
| `menu()` | 渲染导航 | `{{ menu('main') }}` |
| `pager()` | 分页控件 | `{{ pager(records) }}` |
| `dump()` | 调试变量 | `{{ dump(record) }}` |

## 分类法

### 定义分类法

```yaml
# config/bolt/taxonomy.yaml
categories:
    name: Categories
    slug: categories
    singular_name: Category
    behaves_like: categories
    options: [ news, tutorials, reviews ]

tags:
    name: Tags
    slug: tags
    singular_name: Tag
    behaves_like: tags
    allow_spaces: true

groups:
    name: Groups
    slug: groups
    singular_name: Group
    behaves_like: grouping
    options: [ content, meta ]
```

### 在模板中使用分类法

```twig
{# 显示记录的标签 #}
{% if record.taxonomy.tags is defined %}
    <div class="tags">
        {% for tag in record.taxonomy.tags %}
            <a href="{{ path('taxonomy', {'taxonomytype': 'tags', 'slug': tag}) }}">
                {{ tag }}
            </a>
        {% endfor %}
    </div>
{% endif %}
```

## 菜单

### 定义菜单

```yaml
# config/bolt/menu.yaml
main:
    - label: Home
      title: Welcome
      path: homepage
      class: first
    - label: Blog
      path: listing/blogposts
    - label: About
      link: /page/about
    - label: Contact
      path: page/contact
```

### 渲染菜单

```twig
<nav>
    {{ menu('main', 'helpers/_menu.twig') }}
</nav>
```

### 菜单模板

```twig
{# helpers/_menu.twig #}
<ul class="nav">
    {% for item in menu %}
        <li class="{{ item.class|default('') }}">
            <a href="{{ item.link }}" title="{{ item.title }}">
                {{ item.label }}
            </a>
        </li>
    {% endfor %}
</ul>
```

## 配置

### 常规设置

```yaml
# config/bolt/config.yaml
sitename: My Site
payoff: A great website
description: This is my website
locale: en_US
timezone: America/New_York
theme: mytheme
record_template: record.twig
listing_template: listing.twig
```

### 数据库配置

```yaml
# .env
DATABASE_DRIVER=mysql
DATABASE_HOST=localhost
DATABASE_NAME=bolt
DATABASE_USER=bolt
DATABASE_PASSWORD=bolt
```

## 用户角色和权限

| 角色 | 描述 |
|------|------|
| Developer | 完全访问所有设置 |
| Chief Editor | 管理所有内容和用户 |
| Editor | 编辑和发布内容 |
| Author | 创建和编辑自己的内容 |
| Guest | 对管理面板的只读访问 |
| Anonymous | 公共前端访问 |

## 扩展

### 安装扩展

```bash
composer require bolt/thumbs
```

### 常用扩展

| 扩展 | 用途 |
|------|------|
| bolt/thumbs | 图片缩略图生成 |
| bolt/sitemap | XML 站点地图生成 |
| bolt/seo | SEO 元数据管理 |
| bolt/comments | 评论系统 |
| bolt/redactor | 增强的富文本编辑器 |

## API 访问

### REST API 端点

| 端点 | 方法 | 描述 |
|------|------|------|
| `/api/contents` | GET | 列出所有内容 |
| `/api/content/{type}` | GET | 按内容类型列出 |
| `/api/content/{type}/{id}` | GET | 获取单条记录 |
| `/api/content/{type}` | POST | 创建新记录 |
| `/api/content/{type}/{id}` | PUT | 更新记录 |

## 总结

Bolt CMS 提供了一个对开发者友好的扁平文件 CMS，具有灵活的内容建模系统。在 YAML 中定义内容类型，使用 Twig 构建模板，通过内置管理面板管理内容。它在编辑者的简洁性和开发者的能力之间取得了平衡。


---

## 来源：grav.md

## 简介

Grav 是一个现代的扁平文件内容管理系统，将内容存储在 Markdown 文件中，而不是数据库中。它提供快速的性能、简便的部署和灵活的 Twig 模板系统，无需数据库开销即可构建网站。

## 系统要求

| 组件 | 最低配置 | 推荐配置 |
|------|---------|---------|
| PHP 版本 | 7.3.6 | 8.1+ |
| Web 服务器 | Apache 2.4 | Nginx 1.18+ |
| 内存 | 64 MB | 256 MB |
| 磁盘空间 | 30 MB | 500 MB |
| 扩展 | mbstring, xml, curl, zip | +gd, +intl, +json |

## 安装

### 手动安装

```bash
cd /var/www/html
wget https://getgrav.org/download/core/grav/latest
unzip latest -d grav
mv grav grav-site
chown -R www-data:www-data /var/www/html/grav-site
```

### 安装 Admin 插件

```bash
cd /var/www/html/grav-site
bin/gpm install admin
```

### Docker 安装

```bash
docker run -d \
  --name grav \
  -p 8080:80 \
  -v /path/to/grav:/var/www/html \
  ricardoamaro/gravcms:latest
```

## 目录结构

| 目录 | 用途 |
|------|------|
| `pages/` | 所有内容（Markdown 文件） |
| `themes/` | 已安装的主题 |
| `plugins/` | 已安装的插件 |
| `config/` | 系统和插件配置 |
| `assets/` | 编译后的 CSS、JS、图片 |
| `images/` | 上传的图片 |
| `accounts/` | 用户账户数据 |
| `backup/` | 站点备份 |
| `cache/` | 编译后的 Twig 缓存 |
| `logs/` | 系统日志 |
| `user/` | 用户自定义 |

## 内容结构

### 页面组织

```
pages/
  01.home/
    default.md
  02.about/
    default.md
  03.blog/
    item1/
      item.md
    item2/
      item.md
    blog.md
  04.contact/
    form.md
```

### 页面排序

| 前缀 | 排序顺序 | 导航 |
|------|---------|------|
| `01.` | 第一 | 第一项 |
| `02.` | 第二 | 第二项 |
| `01.` vs `02.` | 数字排序 | 控制菜单顺序 |
| 无前缀 | 默认 | 列表末尾 |

## Frontmatter

Frontmatter 是每个 Markdown 文件顶部的 YAML 元数据。

### 基本 Frontmatter

```yaml
---
title: About Us
menu: About
slug: about
template: default
visible: true
published: true
date: 2024-01-15
---
```

### Frontmatter 字段

| 字段 | 说明 | 示例 |
|------|------|------|
| `title` | 页面标题 | "About Us" |
| `menu` | 导航标签 | "About" |
| `slug` | URL slug | "about" |
| `template` | Twig 模板 | "default" |
| `visible` | 在导航中显示 | `true` |
| `published` | 页面已发布 | `true` |
| `date` | 发布日期 | 2024-01-15 |
| `taxonomy` | 分类和标签 | category: blog |
| `metadata` | SEO 元数据 | description, og tags |
| `order` | 自定义排序 | alphabetical, date |
| `redirect` | URL 重定向 | "/new-page" |

### 分类配置

```yaml
---
taxonomy:
  category: blog
  tag: [php, grav, tutorial]
---
```

## Markdown 内容

### 标准 Markdown

```markdown
# 标题 1
## 标题 2
### 标题 3

**粗体文本** 和 *斜体文本*

- 无序列表项
- 另一项

1. 有序列表项
2. 另一项

[链接文本](https://example.com)

![图片替代文字](image.jpg)
```

### 代码块

````markdown
```php
<?php echo "Hello World"; ?>
```
````

### 表格

```markdown
| 表头 1 | 表头 2 | 表头 3 |
|--------|--------|--------|
| 单元格 1 | 单元格 2 | 单元格 3 |
| 单元格 4 | 单元格 5 | 单元格 6 |
```

## 主题

### 热门主题

| 主题 | 风格 | 功能 |
|------|------|------|
| Quark | 简洁、现代 | 默认主题，响应式 |
| Learn2 | 文档 | 侧边栏导航，搜索 |
| Helium | 博客 | 多作者，分类 |
| Flavor | 作品集 | 网格布局，画廊 |
| Bookworm | 文档 | 章节导航 |

### 安装主题

```bash
# 通过 CLI
bin/gpm install quark

# 通过管理面板
# 导航到 Themes > Add
```

### 主题结构

```
themes/
  my-theme/
    blueprints.yaml     # 主题元数据
    my-theme.yaml       # 主题配置
    css/                # 样式表
    js/                 # JavaScript
    images/             # 主题图片
    templates/          # Twig 模板
      default.html.twig
      blog.html.twig
      partials/
        base.html.twig
        navigation.html.twig
```

### 自定义主题模板

```twig
{# templates/default.html.twig #}
{% extends 'partials/base.html.twig' %}

{% block content %}
  <h1>{{ page.title }}</h1>
  {{ page.content|raw }}
{% endblock %}
```

## 插件

### 基础插件

| 插件 | 用途 | 分类 |
|------|------|------|
| Admin | Web 管理界面 | 管理 |
| Form | 表单构建器 | 内容 |
| Email | 邮件发送 | 通信 |
| Markdown Notices | 样式化通知 | 内容 |
| Error | 自定义错误页面 | 导航 |
| Problems | 站点诊断 | 管理 |
| Login | 用户认证 | 安全 |
| Flex Objects | 自定义内容类型 | 内容 |

### 安装插件

```bash
# 通过 CLI
bin/gpm install form

# 通过管理面板
# 导航到 Plugins > Add
```

## 表单插件

### 表单定义（在页面 frontmatter 中）

```yaml
---
title: Contact
form:
  name: contact
  fields:
    - name: name
      label: Name
      type: text
      validate:
        required: true

    - name: email
      label: Email
      type: email
      validate:
        required: true

    - name: message
      label: Message
      type: textarea
      validate:
        required: true

  buttons:
    - type: submit
      value: Send
      classes: btn btn-primary

  process:
    - email:
        from: "{{ form.value.email }}"
        to: admin@example.com
        subject: "Contact Form"
    - message: Thank you for contacting us!
    - display: thankyou
---
```

### 表单字段类型

| 字段类型 | 说明 | 验证选项 |
|---------|------|---------|
| `text` | 单行文本 | required, pattern |
| `email` | 邮箱输入 | required, 邮箱格式 |
| `textarea` | 多行文本 | required, minlength |
| `select` | 下拉菜单 | required, options |
| `checkbox` | 复选框 | required |
| `radio` | 单选按钮 | required |
| `file` | 文件上传 | accept, maxsize |
| `hidden` | 隐藏值 | - |
| `date` | 日期选择器 | required |

## 配置

### 系统配置（config/system.yaml）

```yaml
pages:
  theme: quark
  markdown:
    extra: true
  process:
    markdown: true
    twig: false

cache:
  enabled: true
  driver: auto
  prefix: g

session:
  enabled: true
  timeout: 1800
```

### 站点配置（config/site.yaml）

```yaml
title: My Grav Site
default_lang: en
author:
  name: Site Owner
  email: owner@example.com
metadata:
  description: "Site description for SEO"
taxonomies:
  - category
  - tag
```

## 性能

| 优化 | 配置 | 影响 |
|------|------|------|
| Twig 缓存 | `cache.enabled: true` | 更快渲染 |
| Gzip | Web 服务器配置 | 更小传输 |
| OPcache | `php.ini` | 更快 PHP 执行 |
| CDN | 外部 CDN | 全球分发 |
| 图片优化 | Grav 图片处理 | 更小图片 |
| 资源管道 | CSS/JS 压缩 | 更少请求 |

### 资源管道

```twig
{# 在基础模板中 #}
{% do assets.addCss('theme://css/custom.css') %}
{% do assets.addJs('theme://js/app.js', {group: 'bottom'}) %}
{{ assets.css() }}
{{ assets.js() }}
```

## CLI 命令

| 命令 | 用途 |
|------|------|
| `bin/grav install` | 安装依赖 |
| `bin/gpm install <package>` | 安装主题或插件 |
| `bin/gpm update` | 更新所有包 |
| `bin/gpm selfupgrade` | 升级 Grav 核心 |
| `bin/grav clear-cache` | 清除所有缓存 |
| `bin/grav sandbox` | 检查系统要求 |

## 备份与迁移

| 组件 | 方法 | 说明 |
|------|------|------|
| 页面 | 文件复制 | 整个 `pages/` 目录 |
| 配置 | 文件复制 | `config/` 目录 |
| 主题 | `bin/gpm` 或文件复制 | 可重新安装 |
| 插件 | `bin/gpm` 或文件复制 | 可重新安装 |
| 用户数据 | 文件复制 | `user/` 目录 |
| 完整备份 | zip 整个目录 | 完整站点备份 |

### 迁移步骤

1. 复制整个 Grav 目录到新服务器
2. 设置 Web 服务器文档根目录
3. 配置 PHP 版本
4. 设置文件权限
5. 清除缓存：`bin/grav clear-cache`

## 安全

| 措施 | 实现方式 |
|------|---------|
| HTTPS | Web 服务器 SSL 配置 |
| Admin 插件 | 强管理员密码 |
| 文件权限 | 限制写入访问 |
| PHP 版本 | 保持 PHP 更新 |
| 插件更新 | 定期 `bin/gpm update` |
| 备份 | 定期备份 |
| 登录保护 | 管理端速率限制 |

## 故障排除

| 问题 | 原因 | 解决方案 |
|------|------|---------|
| 500 错误 | PHP 版本 | 检查 PHP 兼容性 |
| 空白页 | Twig 错误 | 启用调试模式 |
| 样式缺失 | 资源管道 | 清除缓存 |
| 页面 404 | URL 重写 | 检查 .htaccess 或 nginx 配置 |
| 加载缓慢 | 缓存禁用 | 在配置中启用缓存 |

## 总结

Grav 提供了一个快速、灵活的扁平文件 CMS，消除了数据库开销，同时保持强大的内容管理能力。其基于 Markdown 的内容、Twig 模板和丰富的插件生态系统，使其成为寻求轻量但功能丰富的 CMS 的开发者的理想选择。


---

## 来源：pagekit.md

使用 Pagekit 构建和管理网站的完整指南，这是一个基于现代 PHP 和 Vue.js 的模块化 CMS。

## 目录

- [安装](#installation)
- [仪表板](#dashboard)
- [页面](#pages)
- [博客](#blog)
- [菜单](#menus)
- [组件](#widgets)
- [主题](#themes)
- [扩展](#extensions)
- [用户](#users)
- [权限](#permissions)
- [SEO](#seo)
- [备份](#backup)

---

## 安装

### 要求

| 要求 | 最低版本 | 推荐 |
|------|----------|------|
| PHP | 7.2+ | 8.1+ |
| 数据库 | MySQL 5.7+ / SQLite 3.8+ / PostgreSQL 9.4+ | MySQL 8.0 |
| Web 服务器 | Apache 2.4+ / Nginx 1.14+ | Nginx |
| Composer | 2.0+ | 最新 |
| PHP 扩展 | PDO, Mbstring, Tokenizer, XML, JSON | 所有列出 |

### 通过 Composer 安装

```bash
composer create-project pagekit/pagekit mysite
cd mysite
```

### 手动安装

1. 从 https://pagekit.com 下载最新版本。
2. 解压到 Web 服务器的文档根目录。
3. 确保 Web 服务器可以写入 `storage` 和 `tmp` 目录。

```bash
chmod -R 775 storage tmp
chown -R www-data:www-data storage tmp
```

### Web 安装器

1. 在浏览器中访问你的站点 URL。
2. 安装器检查系统要求。
3. 配置数据库连接：

| 字段 | 示例 |
|------|------|
| Database Type | MySQL |
| Host | localhost |
| Database Name | pagekit |
| Username | pagekit_user |
| Password | secure_password |

4. 创建管理员账号：

| 字段 | 描述 |
|------|------|
| Site Title | 你的网站名称 |
| Username | 管理员用户名 |
| Password | 管理员密码 |
| Email | 管理员邮箱 |

5. 点击 `Install` 完成设置。

### Web 服务器配置

**Apache（已包含 .htaccess）：**
```apache
<VirtualHost *:80>
    ServerName mysite.com
    DocumentRoot /var/www/mysite
    <Directory /var/www/mysite>
        AllowOverride All
        Require all granted
    </Directory>
</VirtualHost>
```

**Nginx：**
```nginx
server {
    listen 80;
    server_name mysite.com;
    root /var/www/mysite;
    index index.php;

    location / {
        try_files $uri $uri/ /index.php?$query_string;
    }

    location ~ \.php$ {
        fastcgi_pass unix:/var/run/php/php8.1-fpm.sock;
        fastcgi_param SCRIPT_FILENAME $document_root$fastcgi_script_name;
        include fastcgi_params;
    }
}
```

### 安装后

| 任务 | 方法 |
|------|------|
| 移除安装器 | 删除 `install` 目录 |
| 设置权限 | 限制 `storage` 和 `tmp` 访问 |
| 配置缓存 | 在 System 设置中启用缓存 |
| 设置时区 | Settings > System > Timezone |

---

## 仪表板

仪表板是管理 Pagekit 站点的中心枢纽。

### 仪表板概述

| 区域 | 用途 |
|------|------|
| Site Info | 显示站点名称、版本和状态 |
| Recent Activity | 显示最新内容变更 |
| Quick Actions | 常用任务快捷方式 |
| System Updates | 可用更新通知 |

### 导航

主管理侧边栏包含：

| 菜单项 | 描述 |
|--------|------|
| Dashboard | 概览和快捷操作 |
| Site | 页面、博客、菜单、组件 |
| Extensions | 管理已安装扩展 |
| System | 用户、设置、存储、信息 |

### 系统设置

| 设置 | 描述 |
|------|------|
| Site Title | 浏览器标签和标题中显示的名称 |
| Site Description | 默认 meta 描述 |
| Application | 调试模式、维护模式 |
| Cache | 启用/禁用页面缓存 |
| Timezone | 日期显示的服务器时区 |
| Locale | 默认语言 |

### 维护模式

在更新期间启用维护模式以限制访问：

1. 前往 `System > Settings > Application`。
2. 切换 `Maintenance Mode`。
3. 管理员仍可访问仪表板。
4. 访客看到维护页面。

---

## 页面

页面是构成网站结构的静态内容。

### 创建页面

1. 前往 `Site > Pages`。
2. 点击 `Add Page`。
3. 输入页面标题。
4. 配置页面设置。
5. 使用编辑器添加内容。
6. 点击 `Save` 或 `Save and Close`。

### 页面设置

| 设置 | 描述 |
|------|------|
| Title | 页面标题和浏览器标签标题 |
| Slug | URL 友好的标识符 |
| Status | 草稿、已发布或未发布 |
| Access | 谁可以查看页面 |
| Redirect | 重定向 URL（可选） |
| Layout | 使用的模板布局 |

### 内容编辑器

Pagekit 提供支持 Markdown 的富文本编辑器。

| 功能 | 描述 |
|------|------|
| Rich Text | 所见即所得编辑工具栏 |
| Markdown | 直接 Markdown 输入 |
| HTML | 原始 HTML 编辑 |
| Media | 插入图片和文件 |
| Widgets | 嵌入组件内容 |

### 页面模板

| 模板 | 描述 |
|------|------|
| Default | 标准页面布局 |
| Full Width | 无侧边栏 |
| Sidebar | 带侧边栏的内容 |
| Landing | 自定义着陆页布局 |

### 管理页面

| 操作 | 方法 |
|------|------|
| 编辑 | 点击列表中的页面标题 |
| 复制 | 选择页面 > Actions > Duplicate |
| 删除 | 选择页面 > Actions > Delete |
| 重排序 | 在页面列表中拖放 |
| 批量操作 | 选择多个页面 > 选择操作 |

### 页面路由

为页面配置 URL 模式：

| 设置 | 示例 |
|------|------|
| Default | `/about` |
| Custom slug | `/about-us` |
| Nested | `/company/about` |
| Redirect | 将 `/old-page` 重定向到 `/new-page` |

---

## 博客

博客模块提供完整的博客平台。

### 创建博客文章

1. 前往 `Site > Blog`。
2. 点击 `Add Post`。
3. 输入文章标题和内容。
4. 配置文章设置。
5. 点击 `Publish` 或 `Save as Draft`。

### 文章设置

| 设置 | 描述 |
|------|------|
| Title | 文章标题 |
| Slug | URL 友好的标识符 |
| Content | 文章正文（富文本或 Markdown） |
| Excerpt | 列表视图的简短摘要 |
| Status | 草稿、已发布、已排期 |
| Publish Date | 发布日期和时间 |
| Categories | 分配到分类 |
| Tags | 添加标签用于筛选 |
| Access | 谁可以查看文章 |

### 分类

将文章组织到分类：

| 操作 | 方法 |
|------|------|
| 创建分类 | Blog > Categories > Add |
| 分配分类 | 在文章设置中选择分类 |
| 编辑分类 | 分类列表 > Edit |
| 删除分类 | 分类列表 > Delete |

### 标签

标签为文章提供灵活的标记：

| 功能 | 描述 |
|------|------|
| 自动创建 | 首次使用时创建标签 |
| 多标签 | 每篇文章可分配多个标签 |
| 标签云 | 在前端显示热门标签 |
| 筛选 | 按标签筛选文章 |

### 博客设置

| 设置 | 描述 |
|------|------|
| Posts per page | 列表页每页文章数 |
| Date format | 日期显示格式 |
| Comments | 启用/禁用评论 |
| RSS feed | 启用 RSS 输出 |
| Share buttons | 社交分享选项 |

### 博客显示

配置博客在前端的显示方式：

| 选项 | 描述 |
|------|------|
| List view | 以列表显示文章摘要 |
| Grid view | 以卡片网格显示文章 |
| Full posts | 显示完整文章内容 |
| Excerpts | 显示摘要加阅读更多链接 |

---

## 菜单

菜单定义网站的导航结构。

### 创建菜单

1. 前往 `Site > Menus`。
2. 点击 `Add Menu`。
3. 输入菜单名称。
4. 添加菜单项。
5. 将菜单分配到主题位置。

### 菜单项

| 类型 | 描述 | 示例 |
|------|------|------|
| URL | 链接到任意 URL | `https://example.com` |
| Page | 链接到现有页面 | About, Contact |
| Blog | 链接到博客列表 | 博客首页 |
| Category | 链接到博客分类 | News, Updates |
| Separator | 菜单中的视觉分隔线 | --- |

### 添加菜单项

1. 在菜单编辑器中点击 `Add Item`。
2. 选择项目类型。
3. 配置项目：

| 设置 | 描述 |
|------|------|
| Title | 菜单中显示的文字 |
| URL | 目标 URL 或页面 |
| Icon | 可选图标类 |
| Target | 同一窗口或新标签 |
| Access | 谁可以看到此项 |

### 菜单结构

通过拖放组织项目：

```
Home
About
  Our Team
  History
Services
  Consulting
  Development
Blog
Contact
```

### 菜单位置

将菜单分配到主题位置：

| 位置 | 典型位置 |
|------|----------|
| `logo` | 站点头部 logo 区域 |
| `menu` | 主导航栏 |
| `offcanvas` | 移动端滑出菜单 |
| `footer` | 页脚导航 |

### 菜单设置

| 设置 | 描述 |
|------|------|
| Dropdown | 为子项启用下拉 |
| Dropdown style | 悬停或点击打开 |
| Active trail | 高亮活动页面的父项 |
| Max depth | 限制嵌套层级 |

---

## 组件

组件是放置在主题位置的可复用内容块。

### 创建组件

1. 前往 `Site > Widgets`。
2. 点击 `Add Widget`。
3. 选择组件类型。
4. 配置组件。
5. 分配到主题位置。
6. 点击 `Save`。

### 组件类型

| 类型 | 描述 | 用途 |
|------|------|------|
| Text | 自定义文本和 HTML | 页脚内容、通知 |
| Menu | 显示导航菜单 | 侧边栏导航 |
| System | 系统生成内容 | 登录、搜索 |
| Custom | HTML/JS 代码块 | 嵌入、脚本 |

### 组件设置

| 设置 | 描述 |
|------|------|
| Title | 组件标题 |
| Type | 组件内容类型 |
| Position | 显示的主题位置 |
| Access | 谁可以看到组件 |
| Pages | 仅在特定页面显示 |

### 组件位置

可用位置取决于活动主题：

| 位置 | 典型用途 |
|------|----------|
| `sidebar` | 右或左侧边栏 |
| `footer` | 页面页脚区域 |
| `header` | 主内容上方 |
| `content_top` | 主内容之前 |
| `content_bottom` | 主内容之后 |

### 页面特定组件

控制哪些页面显示组件：

| 设置 | 描述 |
|------|------|
| All pages | 组件在所有地方显示 |
| Selected pages | 选择特定页面 |
| Exclude pages | 除选定外都显示 |

---

## 主题

主题控制网站的视觉外观和布局。

### 安装主题

1. 前往 `System > Extensions`。
2. 点击 `Add Extensions`。
3. 浏览或搜索主题。
4. 点击 `Install`。
5. 前往 `System > Settings > Site`。
6. 选择新主题。

### 主题设置

| 设置 | 描述 |
|------|------|
| Logo | 上传站点 logo |
| Favicon | 浏览器标签图标 |
| Primary Color | 主强调色 |
| Font | 默认正文字体 |
| Layout | 页面布局样式 |
| Custom CSS | 附加 CSS 样式 |

### 主题位置

主题定义可放置组件和菜单位置：

| 位置名称 | 位置 |
|----------|------|
| `logo` | 站点头部 |
| `menu` | 导航栏 |
| `hero` | Hero/Banner 区域 |
| `sidebar` | 左或右侧边栏 |
| `content` | 主内容区域 |
| `footer` | 页面页脚 |
| `copyright` | 版权栏 |

### 创建子主题

自定义主题而不修改原始主题：

```
themes/
  my-child/
    index.php          # Theme registration
    theme.json         # Theme configuration
    templates/         # Override templates
    styles/            # Custom styles
```

### 主题配置 (theme.json)

```json
{
  "name": "my-child",
  "version": "1.0.0",
  "parent": "theme-flavor",
  "positions": {
    "sidebar": "Sidebar",
    "footer": "Footer"
  }
}
```

---

## 扩展

扩展为 Pagekit 安装添加功能。

### 安装扩展

| 方式 | 方法 |
|------|------|
| Marketplace | System > Extensions > Add Extensions |
| Upload | System > Extensions > Upload ZIP |
| Composer | `composer require vendor/package` |

### 管理扩展

| 操作 | 方法 |
|------|------|
| 启用 | Extensions > Toggle on |
| 禁用 | Extensions > Toggle off |
| 更新 | Extensions > Update（如有） |
| 卸载 | Extensions > Remove |

### 热门扩展类别

| 类别 | 示例 |
|------|------|
| SEO | Sitemap 生成器、meta 标签管理器 |
| Forms | 联系表单、调查 |
| E-commerce | 购物车、产品目录 |
| Social | 社交媒体 feed、分享按钮 |
| Analytics | Google Analytics、访客追踪 |
| Security | 双因素认证、防火墙 |

### 扩展设置

每个扩展有自己的配置：

1. 前往 `System > Extensions`。
2. 点击扩展旁的齿轮图标。
3. 根据需要配置设置。
4. 点击 `Save`。

### 开发自定义扩展

扩展结构：

```
packages/
  vendor/
    extension-name/
      index.php           # Extension entry point
      src/                # PHP source files
      views/              # Templates
      assets/             # CSS, JS, images
      extension.json      # Extension metadata
```

---

## 用户

管理用户账号和角色。

### 用户管理

| 操作 | 方法 |
|------|------|
| 查看用户 | System > Users |
| 添加用户 | Users > Add User |
| 编辑用户 | 点击用户名 > Edit |
| 删除用户 | 选择用户 > Actions > Delete |
| 封禁用户 | 选择用户 > Actions > Block |

### 用户字段

| 字段 | 描述 |
|------|------|
| Username | 唯一登录名 |
| Email | 用户邮箱 |
| Password | 账号密码 |
| Display Name | 公开显示名称 |
| Avatar | 头像 |
| Roles | 分配的角色 |
| Status | 活动或封禁 |

### 用户角色

| 角色 | 默认权限 |
|------|----------|
| Administrator | 所有功能完全访问 |
| Editor | 创建、编辑、发布内容 |
| Author | 创建和编辑自己的内容 |
| Subscriber | 只读前端访问 |

### 创建自定义角色

1. 前往 `System > Users > Roles`。
2. 点击 `Add Role`。
3. 输入角色名称。
4. 选择权限。
5. 点击 `Save`。

### 用户注册

| 设置 | 描述 |
|------|------|
| Allow registration | 启用公开注册 |
| Email verification | 需要邮箱确认 |
| Default role | 分配给新注册的角色 |
| Approval | 需要管理员批准 |

---

## 权限

控制对内容和功能的访问。

### 权限系统

| 级别 | 描述 |
|------|------|
| Global | 系统范围权限 |
| Component | 每模块权限 |
| Content | 每项访问控制 |

### 全局权限

| 权限 | 描述 |
|------|------|
| `system: access admin area` | 访问管理仪表板 |
| `system: manage settings` | 更改系统设置 |
| `system: manage extensions` | 安装/移除扩展 |
| `system: manage storage` | 管理文件存储 |

### 内容权限

| 设置 | 选项 |
|------|------|
| Public | 任何人都可查看 |
| Registered | 仅登录用户 |
| Author | 仅内容作者 |
| Custom | 特定角色或用户 |

### 分配权限

1. 前往 `System > Users > Permissions`。
2. 选择角色。
3. 勾选/取消每个组件的权限。
4. 点击 `Save`。

### 权限矩阵示例

| 权限 | Admin | Editor | Author | Subscriber |
|------|-------|--------|--------|------------|
| 访问管理 | 是 | 是 | 是 | 否 |
| 管理页面 | 是 | 是 | 否 | 否 |
| 编辑自己的内容 | 是 | 是 | 是 | 否 |
| 发布内容 | 是 | 是 | 否 | 否 |
| 管理用户 | 是 | 否 | 否 | 否 |
| 管理设置 | 是 | 否 | 否 | 否 |

---

## SEO

为搜索引擎优化你的 Pagekit 站点。

### 基本 SEO 设置

| 设置 | 位置 | 描述 |
|------|------|------|
| Site Title | System > Settings | 出现在搜索结果中 |
| Meta Description | System > Settings | 默认页面描述 |
| Permalink Structure | System > Settings | 内容 URL 格式 |
| Sitemap | Extensions | 自动生成的 XML sitemap |

### URL 结构

配置简洁 URL：

| 格式 | 示例 |
|------|------|
| Default | `/index.php?id=123` |
| Clean | `/about` |
| Blog | `/blog/post-title` |
| Category | `/blog/category/news` |

### 页面级 SEO

每页和文章都有 SEO 字段：

| 字段 | 描述 |
|------|------|
| Title Tag | 浏览器标签和搜索结果标题 |
| Meta Description | 搜索结果中显示的摘要 |
| Slug | URL 路径组件 |
| Canonical URL | 重复内容的首选 URL |
| Robots | Index/noindex, follow/nofollow |

### SEO 最佳实践

| 实践 | 实施方式 |
|------|----------|
| 独特标题 | 每页有不同标题 |
| Meta 描述 | 150-160 字符摘要 |
| 简洁 URL | 描述性、关键词丰富的 slug |
| 标题层级 | 正确的 H1, H2, H3 结构 |
| 图片 alt 文本 | 描述性 alt 属性 |
| 内部链接 | 相关内容之间链接 |
| Sitemap | 向搜索引擎提交 XML sitemap |

### SEO 扩展

| 扩展 | 功能 |
|------|------|
| SEO Pack | Meta 标签、sitemap、robots.txt |
| Google Analytics | 访客追踪集成 |
| Schema Markup | 富摘要的结构化数据 |
| Redirect Manager | 301/302 重定向管理 |

---

## 备份

通过定期备份保护站点数据。

### 备份内容

| 组件 | 位置 | 方法 |
|------|------|------|
| Database | MySQL/PostgreSQL/SQLite | 数据库导出 |
| Files | `/storage` 目录 | 文件复制 |
| Configuration | `/config` 目录 | 文件复制 |
| Extensions | `/packages` 目录 | 文件复制 |
| Themes | `/themes` 目录 | 文件复制 |

### 数据库备份

**MySQL:**
```bash
mysqldump -u username -p pagekit_db > backup_$(date +%Y%m%d).sql
```

**PostgreSQL:**
```bash
pg_dump -U username pagekit_db > backup_$(date +%Y%m%d).sql
```

**SQLite:**
```bash
cp storage/database.sqlite backup_$(date +%Y%m%d).sqlite
```

### 文件备份

```bash
tar -czf pagekit_files_$(date +%Y%m%d).tar.gz \
  storage/ \
  config/ \
  packages/ \
  themes/
```

### 自动备份脚本

```bash
#!/bin/bash
BACKUP_DIR="/backups/pagekit"
DATE=$(date +%Y%m%d_%H%M%S)

# Database backup
mysqldump -u root -p pagekit_db | gzip > $BACKUP_DIR/db_$DATE.sql.gz

# File backup
tar -czf $BACKUP_DIR/files_$DATE.tar.gz /var/www/pagekit/storage

# Cleanup old backups (keep 30 days)
find $BACKUP_DIR -type f -mtime +30 -delete
```

### 恢复流程

| 步骤 | 命令 |
|------|------|
| 1. 恢复数据库 | `mysql -u root -p pagekit_db < backup.sql` |
| 2. 恢复文件 | `tar -xzf files_backup.tar.gz -C /var/www/pagekit` |
| 3. 清除缓存 | 删除 `storage/cache` 内容 |
| 4. 验证 | 浏览站点并检查功能 |

### 备份计划

| 频率 | 保留 | 用途 |
|------|------|------|
| 每天 | 7 天 | 经常变更的活跃站点 |
| 每周 | 30 天 | 标准站点 |
| 每月 | 12 个月 | 归档 |
| 更新前 | 永久 | 更新前安全网 |

### 备份验证

定期通过恢复到暂存环境测试备份：

1. 设置暂存服务器。
2. 恢复最新备份。
3. 验证所有内容正确加载。
4. 测试关键功能（登录、表单、导航）。
5. 记录发现的任何问题。


---

## 来源：statamic.md

## 简介

Statamic 是一个基于 Laravel 构建的现代扁平文件内容管理系统。它使用 Markdown 和 YAML 文件存储内容，而非数据库。本教程涵盖安装、内容建模以及使用 Statamic 构建完整网站。

## 为什么选择扁平文件 CMS

| 特性 | 扁平文件（Statamic） | 数据库 CMS |
|------|---------------------|-----------|
| 存储 | YAML/Markdown 文件 | MySQL/PostgreSQL |
| 设置 | 无需数据库 | 需要数据库配置 |
| 版本控制 | Git 友好的内容 | 需要导出工具 |
| 性能 | 文件读取，可选缓存 | 基于查询 |
| 托管 | 任何 PHP 主机 | 需要数据库主机 |
| 备份 | 复制文件 | 导出数据库 |

## 系统要求

| 组件 | 最低要求 | 推荐配置 |
|------|---------|---------|
| PHP | 8.1 | 8.2 或 8.3 |
| Composer | 2.x | 最新版 |
| Node.js | 16+ | 18+ LTS |
| Web 服务器 | Apache/Nginx | Nginx + PHP-FPM |
| 扩展 | mbstring、xml、curl、zip | 所有 PHP 扩展 |

## 安装

### 全新安装

```bash
composer create-project statamic/statamic my-site
cd my-site
php artisan statamic:install
```

### 添加到现有 Laravel 项目

```bash
composer require statamic/cms
php artisan statamic:install
```

## 目录结构

| 目录 | 用途 |
|------|------|
| content/ | 所有页面、条目、分类法 |
| resources/ | 视图（Antlers 模板）、CSS、JS |
| public/ | 网站根目录、资源文件 |
| config/ | 站点和插件配置 |
| users/ | 用户账户（YAML 文件） |
| storage/ | 日志、缓存、临时文件 |
| app/ | 自定义 PHP 代码、控制器 |

## 内容架构

### 集合（Collections）

集合将相关内容条目分组。

| 集合类型 | 用例 | 示例 |
|----------|------|------|
| Blog（博客） | 基于时间的文章 | 文章、新闻 |
| Pages（页面） | 静态页面 | 关于、联系 |
| Products（产品） | 电商商品 | 目录条目 |
| Events（活动） | 基于日期的内容 | 会议、聚会 |

### 创建集合

1. 运行 `php please make:collection blog`
2. 编辑 `content/collections/blog.yaml`
3. 定义蓝图字段
4. 以 Markdown 文件形式添加条目

### 条目结构

| 字段 | 格式 | 用途 |
|------|------|------|
| title | String | 条目标题 |
| slug | String | URL 安全标识符 |
| date | Date | 发布日期 |
| author | String | 内容作者 |
| template | String | Antlers 模板名称 |
| body | Markdown | 主要内容 |

### 蓝图（Blueprints）

蓝图定义内容条目的结构。

| 字段类型 | 用例 |
|----------|------|
| text | 标题、名称、短字符串 |
| textarea | 描述、摘要 |
| markdown | 富文本内容 |
| select | 下拉选项 |
| assets | 图片和文件上传 |
| entries | 与其他条目的关联 |
| date | 日期和时间选择器 |
| toggle | 布尔标志 |
| bard | 基于块的富文本编辑器 |
| repeater | 可重复的字段组 |

## 使用 Antlers 模板

Antlers 是 Statamic 的原生模板引擎。

### 基本语法

| 语法 | 用途 |
|------|------|
| {{ title }} | 输出变量 |
| {{ if title }}...{{ /if }} | 条件块 |
| {{ entries }}...{{ /entries }} | 遍历集合 |
| {{ partial "header" }} | 包含局部模板 |
| {{ yield "content" }} | 区域输出 |
| {{ slot }} | 组件插槽 |

### 模板层级

| 模板 | 范围 | 优先级 |
|------|------|--------|
| default.antlers.html | 所有页面的后备模板 | 最低 |
| blog.antlers.html | 博客列表 | 中等 |
| blog/show.antlers.html | 单篇博客文章 | 较高 |
| _entry.antlers.html | 集合级覆盖 | 最高 |

## 导航

### 创建导航

| 导航 | 用途 |
|------|------|
| main | 主站导航 |
| footer | 页脚链接 |
| sidebar | 侧边栏菜单 |

## 分类法（Taxonomies）

分类法对跨集合的条目进行分类。

| 分类法 | 示例 |
|--------|------|
| tags | 技术、设计、新闻 |
| categories | 博客文章分类 |
| colors | 产品颜色选项 |

## 资源与媒体

| 功能 | 描述 |
|------|------|
| Asset Containers | 映射到存储磁盘的文件夹 |
| Glide 集成 | 实时图片处理 |
| Alt Text | 无障碍图片描述 |
| Focal Point | 智能裁剪中心 |

## 表单

| 表单类型 | 用例 |
|----------|------|
| Contact（联系） | 用户咨询 |
| Newsletter（通讯） | 邮件订阅 |
| Search（搜索） | 内容搜索 |

## 用户与权限

| 角色 | 默认权限 |
|------|---------|
| Super Admin（超级管理员） | 完全访问 |
| Editor（编辑） | 编辑和发布内容 |
| Author（作者） | 创建和编辑自己的内容 |
| Viewer（查看者） | 只读访问 |

## 多语言支持

| 功能 | 配置 |
|------|------|
| Locales（区域设置） | 在 config/statamic/sites.php 中定义 |
| Content（内容） | 每个区域设置的 Markdown 文件 |
| Routing（路由） | 自动区域前缀 |
| Fallback（回退） | 翻译缺失时显示默认区域内容 |

## 部署

| 方法 | 步骤 |
|------|------|
| Git | 推送内容和模板，在服务器上拉取 |
| CI/CD | 构建资源、运行迁移、清除缓存 |
| 手动 | 通过 FTP/SFTP 上传文件 |

### 生产环境清单

| 任务 | 命令 |
|------|------|
| 缓存配置 | php artisan config:cache |
| 缓存路由 | php artisan route:cache |
| 缓存视图 | php artisan view:cache |
| 静态缓存 | 在 config/statamic/static_caching.php 中启用 |

## 性能优化

| 技术 | 收益 |
|------|------|
| 静态缓存 | 提供预渲染的 HTML |
| CDN | 全球分发资源 |
| 图片优化 | 减小文件大小 |
| Stache 缓存 | 加速内容索引 |

## 总结

Statamic 将扁平文件存储的简洁性与 Laravel 的强大功能相结合。其 Antlers 模板系统、蓝图机制和 Git 友好的内容管理方式，使其非常适合希望完全掌控内容和基础设施、又不想承担传统数据库开销的开发者。


---

## 来源：strapi.md

## 简介

Strapi 是一个开源的无头 CMS，提供 RESTful 和 GraphQL API 来管理内容。它基于 Node.js 构建，允许开发者定义内容结构并从任何前端消费。本教程涵盖设置、内容建模和 API 使用。

## 无头 CMS 与传统 CMS 对比

| 方面 | 无头（Strapi） | 传统（WordPress） |
|------|---------------|-----------------|
| 前端 | 解耦，任意框架 | 内置 PHP 模板 |
| API | REST + GraphQL | 可选插件 |
| 内容交付 | 任何设备或渠道 | 默认仅 Web |
| 灵活性 | 高 | 中等 |
| 开发者体验 | API 优先 | 主题优先 |

## 系统要求

| 组件 | 版本 |
|------|------|
| Node.js | 18.x 或 20.x |
| npm | 9.x+ |
| 数据库 | SQLite（默认）、PostgreSQL、MySQL |
| 内存 | 最低 2 GB |
| 磁盘 | 1 GB 可用空间 |

## 安装

```bash
npx create-strapi-app@latest my-project --quickstart
cd my-project
npm run develop
```

| 标志 | 效果 |
|------|------|
| --quickstart | 使用 SQLite，无需外部数据库 |
| --no-run | 创建项目但不启动服务器 |
| --template | 应用启动模板 |
| --dbclient | 指定数据库类型（postgres、mysql） |

## 项目结构

| 目录 | 用途 |
|------|------|
| src/api/ | 内容类型、控制器、路由、服务 |
| src/admin/ | 管理面板自定义 |
| config/ | 服务器、数据库、中间件配置 |
| database/ | 迁移和种子数据 |
| public/ | 直接提供的静态文件 |
| extensions/ | 插件覆盖 |

## 内容类型

### 集合类型（Collection Types）

用于可重复的内容条目。

| 示例 | 字段 |
|------|------|
| Articles | title、slug、body、author、publishedAt |
| Products | name、price、description、images |
| Categories | name、slug、description |

### 单一类型（Single Types）

用于唯一内容，如站点设置。

| 示例 | 字段 |
|------|------|
| Homepage | heroTitle、heroImage、sections |
| Global | siteName、logo、footerText |

### 创建内容类型

1. 打开管理面板 /admin。
2. 导航到 Content-Type Builder。
3. 点击"Create new collection type"。
4. 添加字段并配置类型。
5. 保存以生成 API 端点。

## 字段类型

| 字段类型 | 描述 | 选项 |
|----------|------|------|
| Text | 短字符串 | maxLength、regex |
| Rich Text | 所见即所得编辑器 | Markdown 或 Quill |
| Number | 整数或小数 | min、max、integer/float |
| Date | 日期或日期时间 | format |
| Boolean | 真/假开关 | 默认值 |
| Enumeration | 下拉选择 | 值列表 |
| Media | 文件上传 | multiple、允许类型 |
| Relation | 链接到其他内容类型 | 多对一、多对多 |
| JSON | 任意 JSON 数据 | schema 验证 |
| UID | URL 友好的 slug | targetField、regex |

## REST API 参考

### CRUD 操作

| 方法 | 端点 | 描述 |
|------|------|------|
| GET | /api/{contentType} | 列出所有条目 |
| GET | /api/{contentType}/:id | 获取单个条目 |
| POST | /api/{contentType} | 创建条目 |
| PUT | /api/{contentType}/:id | 更新条目 |
| DELETE | /api/{contentType}/:id | 删除条目 |

### 查询参数

| 参数 | 用途 | 示例 |
|------|------|------|
| filters | 过滤结果 | filters[title][$contains]=tech |
| sort | 排序结果 | sort=createdAt:desc |
| pagination | 分页 | pagination[page]=1&pagination[pageSize]=25 |
| populate | 包含关联 | populate=author,category |
| fields | 选择特定字段 | fields[0]=title&fields[1]=slug |

### 过滤运算符

| 运算符 | 含义 | 示例 |
|--------|------|------|
| $eq | 等于 | filters[status][$eq]=published |
| $ne | 不等于 | filters[status][$ne]=draft |
| $lt | 小于 | filters[price][$lt]=100 |
| $gt | 大于 | filters[price][$gt]=50 |
| $contains | 包含字符串 | filters[title][$contains]=api |
| $in | 在数组中 | filters[category][$in]=tech,news |
| $null | 为空 | filters[deletedAt][$null]=true |

## GraphQL API

安装插件以启用 GraphQL：

```bash
npm run strapi install graphql
```

| 查询 | 示例 |
|------|------|
| 列表 | query { articles { data { id attributes { title } } } } |
| 单个 | query { article(id: 1) { data { attributes { title body } } } } |
| 创建 | mutation { createArticle(data: { title: "New" }) { data { id } } } |

## 认证与权限

| 功能 | 描述 |
|------|------|
| Public Role | 未认证的 API 访问 |
| Authenticated Role | 已登录用户访问 |
| Custom Roles | 细粒度权限控制 |
| API Tokens | 用于服务端通信的静态令牌 |

### 配置权限

1. 进入 Settings > Roles > Public。
2. 选择内容类型。
3. 切换权限：find、findOne、create、update、delete。
4. 保存更改。

## 生命周期钩子

| 钩子 | 触发时机 |
|------|---------|
| beforeCreate | 条目创建前 |
| afterCreate | 条目创建后 |
| beforeUpdate | 条目更新前 |
| afterUpdate | 条目更新后 |
| beforeDelete | 条目删除前 |
| afterDelete | 条目删除后 |

## 部署

| 平台 | 方法 |
|------|------|
| Strapi Cloud | 推送到 Git，自动部署 |
| Heroku | Git 推送配合 Procfile |
| DigitalOcean | App Platform 或 Droplet |
| Docker | Dockerfile + docker-compose |
| AWS | EC2、ECS 或 Lambda |

### 环境变量

| 变量 | 用途 |
|------|------|
| HOST | 服务器主机（0.0.0.0） |
| PORT | 服务器端口（1337） |
| APP_KEYS | 会话安全密钥 |
| API_TOKEN_SALT | API 令牌加密盐值 |
| ADMIN_JWT_SECRET | 管理面板 JWT 密钥 |
| JWT_SECRET | 用户 JWT 密钥 |
| DATABASE_CLIENT | 数据库类型 |
| DATABASE_URL | 连接字符串 |

## 性能优化建议

| 建议 | 实施方式 |
|------|---------|
| 启用缓存 | 使用 Redis 或内存缓存 |
| 优化查询 | 选择性使用 fields 和 populate |
| 压缩响应 | 启用 gzip 中间件 |
| 使用 CDN | 通过 Cloudflare 或类似服务提供媒体 |
| 数据库索引 | 在常用查询字段上添加索引 |

## 总结

Strapi 提供了一个灵活的、API 优先的内容管理系统，适用于任何前端框架。其内容类型构建器、REST 和 GraphQL API 以及插件生态系统，使其成为需要跨多个平台进行结构化内容交付的项目的理想选择。


---

## 来源：keystone.md

## 简介

KeystoneJS 是一个基于 Node.js 构建的无头内容管理系统。它提供了一个灵活的平台，用于通过 API 创建、管理和交付内容，无需耦合前端。

### 什么是无头 CMS？

无头 CMS 将内容管理与内容展示分离。后端提供 API，任何前端都可以消费这些 API。

| 特性 | 传统 CMS | 无头 CMS |
|------|----------|----------|
| 前端 | 耦合 | 解耦 |
| 内容交付 | HTML 页面 | API 响应 |
| 灵活性 | 有限 | 高 |
| 多渠道 | 困难 | 原生支持 |

### 为什么选择 KeystoneJS？

| 优势 | 描述 |
|------|------|
| Schema 驱动 | 在代码中定义数据模型 |
| Admin UI | 内置管理界面 |
| GraphQL API | 从 Schema 自动生成 API |
| 身份验证 | 内置认证系统 |
| 文件处理 | 集成文件和图片管理 |

## 安装

### 前置要求

| 要求 | 最低版本 |
|------|----------|
| Node.js | 18.0 或更高 |
| npm | 8.0 或更高 |
| 数据库 | PostgreSQL、MySQL 或 SQLite |

### 项目设置

```bash
npm init keystone-app my-cms
cd my-cms
npm install
```

### 项目结构

```
my-cms/
├── keystone.ts        # 主配置
├── schema.ts          # 内容 Schema
├── auth.ts            # 认证配置
├── package.json       # 依赖
└── .env               # 环境变量
```

## Schema 定义

### 定义内容类型

每个内容类型都定义为一个包含字段的 list。

```typescript
import { list } from '@keystone-6/core';
import { text, select, timestamp } from '@keystone-6/core/fields';

export const Post = list({
  fields: {
    title: text({ validation: { isRequired: true } }),
    content: text({ ui: { displayMode: 'textarea' } }),
    status: select({
      options: [
        { label: 'Draft', value: 'draft' },
        { label: 'Published', value: 'published' },
      ],
      defaultValue: 'draft',
    }),
    publishedAt: timestamp(),
  },
});
```

### 常用字段类型

| 字段类型 | 用例 | 示例 |
|----------|------|------|
| `text` | 短文本或长文本 | 标题、描述 |
| `integer` | 整数 | 数量、分数 |
| `float` | 小数 | 价格、评分 |
| `select` | 固定选项 | 状态、分类 |
| `timestamp` | 日期和时间 | 创建日期 |
| `relationship` | 关联记录 | 作者、标签 |
| `checkbox` | 布尔值 | 精选、可见 |
| `image` | 图片上传 | 缩略图、照片 |

### 关联关系

```typescript
import { relationship } from '@keystone-6/core/fields';

export const Post = list({
  fields: {
    title: text(),
    author: relationship({ ref: 'User.posts', many: false }),
    tags: relationship({ ref: 'Tag.posts', many: true }),
  },
});

export const Tag = list({
  fields: {
    name: text(),
    posts: relationship({ ref: 'Post.tags', many: true }),
  },
});
```

| 关系类型 | 基数 | 示例 |
|----------|------|------|
| 一对一 | 单条记录对应单条记录 | 文章对应作者资料 |
| 一对多 | 单条记录对应多条记录 | 用户对应文章 |
| 多对多 | 多条记录对应多条记录 | 文章对应标签 |

## 配置

### 主配置文件

```typescript
import { config } from '@keystone-6/core';
import { Post, Tag, User } from './schema';

export default config({
  db: {
    provider: 'postgresql',
    url: process.env.DATABASE_URL,
  },
  lists: { Post, Tag, User },
  ui: {
    isAccessAllowed: ({ session }) => !!session,
  },
});
```

### 数据库提供者

| 提供者 | 用例 | 性能 |
|--------|------|------|
| PostgreSQL | 生产工作负载 | 高 |
| MySQL | 现有基础设施 | 高 |
| SQLite | 开发和测试 | 中等 |

## 身份验证

### 设置身份验证

```typescript
import { createAuth } from '@keystone-6/auth';

const { withAuth } = createAuth({
  listKey: 'User',
  identityField: 'email',
  secretField: 'password',
  initFirstItem: {
    fields: ['name', 'email', 'password'],
  },
});
```

### 会话管理

```typescript
import { statelessSessions } from '@keystone-6/core/session';

const session = statelessSessions({
  maxAge: 60 * 60 * 24 * 30,
  secret: process.env.SESSION_SECRET,
});
```

| 会话类型 | 描述 | 用例 |
|----------|------|------|
| 无状态 | 基于 JWT 的令牌 | API、可扩展性 |
| 数据库 | 存储在数据库中 | 服务端渲染应用 |

## 访问控制

### 字段级访问

```typescript
export const Post = list({
  fields: {
    title: text({
      access: {
        read: true,
        create: ({ session }) => !!session,
        update: ({ session }) => session?.data.isAdmin,
      },
    }),
  },
});
```

### 列表级访问

```typescript
export const Post = list({
  access: {
    operation: {
      query: true,
      create: ({ session }) => !!session,
      update: ({ session }) => !!session,
      delete: ({ session }) => session?.data.isAdmin,
    },
  },
});
```

| 访问级别 | 范围 | 示例 |
|----------|------|------|
| 操作级 | CRUD 操作 | 谁可以创建文章 |
| 字段级 | 单个字段 | 谁可以查看邮箱 |
| 过滤级 | 记量子集 | 用户只能看到自己的文章 |

## GraphQL API

### 查询内容

```graphql
query {
  posts(where: { status: { equals: "published" } }) {
    id
    title
    content
    author {
      name
    }
    tags {
      name
    }
  }
}
```

### 创建内容

```graphql
mutation {
  createPost(data: {
    title: "New Post"
    content: "Post content here"
    status: "draft"
  }) {
    id
    title
  }
}
```

### 过滤和排序

| 操作 | 语法 | 示例 |
|------|------|------|
| 等于 | `{ equals: value }` | 状态等于 draft |
| 包含 | `{ contains: text }` | 标题包含关键词 |
| 大于 | `{ gt: number }` | 价格大于 100 |
| 列表内 | `{ in: [...] }` | 状态在列表中 |
| 排序 | `orderBy: { field: asc }` | 按日期升序 |

## 文件和图片管理

### 图片配置

```typescript
import { config } from '@keystone-6/core';

export default config({
  images: {
    upload: 'local',
    local: {
      storagePath: 'public/images',
      baseUrl: '/images',
    },
  },
});
```

| 存储选项 | 描述 | 最佳用途 |
|----------|------|----------|
| 本地 | 文件系统 | 开发 |
| S3 | Amazon S3 | 生产 |
| Cloudinary | 云服务 | 图片变换 |

## 部署

### 构建生产版本

```bash
npm run build
npm start
```

### 部署平台

| 平台 | 配置 | 备注 |
|------|------|------|
| Vercel | `vercel.json` | Serverless |
| Railway | `railway.json` | 托管服务 |
| Docker | `Dockerfile` | 自托管 |
| AWS | Elastic Beanstalk | 可扩展 |

### Docker 配置

```dockerfile
FROM node:18-alpine
WORKDIR /app
COPY package*.json ./
RUN npm ci --production
COPY . .
RUN npm run build
EXPOSE 3000
CMD ["npm", "start"]
```

## 最佳实践

| 实践 | 描述 |
|------|------|
| 版本化 Schema | 在版本控制中跟踪 Schema 变更 |
| 使用迁移 | 部署前运行数据库迁移 |
| 验证输入 | 启用字段验证规则 |
| 缓存响应 | 为频繁访问的数据实现缓存 |
| 监控性能 | 跟踪 API 响应时间 |

## 总结

| 概念 | 要点 |
|------|------|
| Schema | 在代码中定义内容类型 |
| 访问控制 | 基于角色的权限管理 |
| API | 自动生成的 GraphQL |
| 身份验证 | 内置用户管理 |
| 部署 | 多平台支持 |


---
