# Directus：无头 CMS 平台

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
