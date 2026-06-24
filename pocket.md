# 使用 PocketBase 进行后端开发

## 简介

PocketBase 是一个开源后端，由嵌入式 SQLite 数据库、实时订阅、REST API 和管理仪表盘组成。它在一个可执行文件中提供完整的后端解决方案。

## 目录

1. [核心功能](#核心功能)
2. [入门指南](#入门指南)
3. [数据集合](#数据集合)
4. [记录字段](#记录字段)
5. [REST API](#rest-api)
6. [认证](#认证)
7. [实时订阅](#实时订阅)
8. [文件存储](#文件存储)
9. [自定义代码](#自定义代码)

## 核心功能

| 功能 | 说明 |
|------|------|
| 嵌入式数据库 | SQLite，无外部依赖 |
| REST API | 从集合自动生成 |
| 管理 UI | 内置仪表盘 |
| 认证系统 | 邮箱/密码、OAuth2 |
| 实时 | 基于 SSE 的订阅 |
| 文件存储 | 本地或 S3 兼容存储 |
| 单一二进制 | 无运行时依赖 |

## 入门指南

### 安装

| 方式 | 命令 |
|------|------|
| 下载二进制 | 访问 GitHub releases |
| Go install | `go install github.com/pocketbase/pocketbase@latest` |
| Docker | `docker run -p 8090:8090 ghcr.io/pocketbase/pocketbase` |

### 目录结构

| 路径 | 用途 |
|------|------|
| `pb_data/` | SQLite 数据库和数据 |
| `pb_migrations/` | 模式迁移文件 |
| `pb_public/` | 静态文件服务 |
| `pb_hooks/` | 自定义 Go/JS 钩子 |

### 快速开始

```bash
# 下载并解压
wget https://github.com/pocketbase/pocketbase/releases/latest/download/pocketbase_0.22.0_linux_amd64.zip
unzip pocketbase_*.zip

# 启动服务器
./pocketbase serve --http=0.0.0.0:8090
```

## 数据集合

### 集合类型

| 类型 | 用途 | 认证 | API |
|------|------|------|-----|
| Base | 普通数据 | 否 | CRUD |
| Auth | 用户账户 | 是 | CRUD + 认证 |
| View | SQL 视图 | 否 | 只读 |

### 创建集合

| 步骤 | 操作 |
|------|------|
| 1 | 打开管理 UI /_ |
| 2 | 导航到 Collections |
| 3 | 点击 New Collection |
| 4 | 设置名称和类型 |
| 5 | 添加字段 |
| 6 | 配置规则 |
| 7 | 保存集合 |

### 集合设置

| 设置 | 说明 |
|------|------|
| 名称 | 集合标识符 |
| 类型 | Base、Auth 或 View |
| 列出规则 | 谁可以列出记录 |
| 查看规则 | 谁可以查看记录 |
| 创建规则 | 谁可以创建记录 |
| 更新规则 | 谁可以更新记录 |
| 删除规则 | 谁可以删除记录 |

## 记录字段

### 可用字段类型

| 字段类型 | 数据类型 | 选项 |
|----------|----------|------|
| Text | 字符串 | 最小/最大长度、模式 |
| Number | 整数/浮点 | 最小、最大 |
| Bool | 布尔 | - |
| Email | 字符串 | 格式验证 |
| URL | 字符串 | 格式验证 |
| Date | 日期时间 | 最小、最大 |
| Select | 字符串 | 预设值 |
| JSON | 对象 | 模式验证 |
| File | 文件路径 | MIME 类型、最大大小 |
| Relation | 记录 ID | 关联集合 |
| Autocomplete | 字符串 | 建议值 |

### 字段选项

| 选项 | 说明 | 示例 |
|------|------|------|
| 必填 | 必须有值 | true |
| 唯一 | 无重复 | true |
| 隐藏 | 不在 API 响应中 | false |
| 系统 | 自动管理 | false |
| 主键 | 记录 ID | Auto |

### 关联

| 关联类型 | 说明 | 示例 |
|----------|------|------|
| 单个 | 一对一 | 用户有一个档案 |
| 多个 | 一对多 | 作者有多篇文章 |
| 反向 | 反向查找 | 文章属于作者 |

## REST API

### API 端点

| 端点 | 方法 | 用途 |
|------|------|------|
| `/api/collections/{name}/records` | GET | 列出记录 |
| `/api/collections/{name}/records/{id}` | GET | 获取单条记录 |
| `/api/collections/{name}/records` | POST | 创建记录 |
| `/api/collections/{name}/records/{id}` | PATCH | 更新记录 |
| `/api/collections/{name}/records/{id}` | DELETE | 删除记录 |

### 查询参数

| 参数 | 示例 | 说明 |
|------|------|------|
| `page` | `?page=2` | 分页页码 |
| `perPage` | `?perPage=20` | 每页条目 |
| `sort` | `?sort=-created` | 排序方式 |
| `filter` | `?filter=status='active'` | 过滤记录 |
| `fields` | `?fields=id,name` | 选择字段 |
| `expand` | `?expand=author` | 展开关联 |

### 过滤语法

| 操作符 | 示例 | 说明 |
|--------|------|------|
| `=` | `status='active'` | 等于 |
| `!=` | `status!='deleted'` | 不等于 |
| `>` | `price>100` | 大于 |
| `<` | `price<500` | 小于 |
| `~` | `name~'john'` | 包含 |
| `!~` | `name!~'test'` | 不包含 |
| `?= ` | `tags?='featured'` | 数组包含 |

### 响应格式

```json
{
  "page": 1,
  "perPage": 30,
  "totalItems": 150,
  "totalPages": 5,
  "items": [
    {
      "id": "abc123",
      "collectionId": "xyz789",
      "collectionName": "posts",
      "title": "Hello World",
      "created": "2024-01-15 10:30:00.000Z",
      "updated": "2024-01-15 10:30:00.000Z"
    }
  ]
}
```

## 认证

### 认证方式

| 方式 | 配置 | 用户操作 |
|------|------|----------|
| 邮箱/密码 | 内置 | 注册/登录 |
| OAuth2 | 提供商设置 | 社交登录 |
| OTP | 基于邮箱 | 一次性密码 |

### OAuth2 提供商

| 提供商 | 所需设置 |
|--------|----------|
| Google | Client ID/Secret |
| GitHub | Client ID/Secret |
| Facebook | Client ID/Secret |
| Twitter | API Key/Secret |
| Discord | Client ID/Secret |
| Microsoft | Client ID/Secret |

### 认证 API 端点

| 端点 | 方法 | 用途 |
|------|------|------|
| `/api/collections/{auth}/records` | POST | 注册 |
| `/api/collections/{auth}/auth-with-password` | POST | 登录 |
| `/api/collections/{auth}/auth-refresh` | POST | 刷新令牌 |
| `/api/collections/{auth}/records/{id}` | PATCH | 更新档案 |
| `/api/collections/{auth}/request-password-reset` | POST | 重置密码 |
| `/api/collections/{auth}/confirm-password-reset` | POST | 确认重置 |

### 令牌管理

| 令牌 | 持续时间 | 用途 |
|------|----------|------|
| Auth token | 2 周（可配置） | API 认证 |
| Refresh token | 长期有效 | 获取新的 auth token |

## 实时订阅

### 订阅类型

| 类型 | 说明 | 过滤器 |
|------|------|--------|
| Subscribe | 所有记录 | 无 |
| Subscribe to record | 特定记录 | 记录 ID |
| Subscribe with filter | 过滤记录 | 过滤表达式 |

### SSE 连接

```javascript
// 连接到实时
const eventSource = new EventSource(
  '/api/realtime?token=YOUR_AUTH_TOKEN'
);

// 订阅集合
fetch('/api/realtime', {
  method: 'POST',
  headers: {
    'Content-Type': 'application/json',
  },
  body: JSON.stringify({
    action: 'subscribe',
    collection: 'posts',
    filter: 'status="published"'
  })
});

// 监听事件
eventSource.onmessage = (event) => {
  const data = JSON.parse(event.data);
  console.log(data.action, data.record);
};
```

### 事件类型

| 事件 | 触发条件 |
|------|----------|
| `create` | 新记录已创建 |
| `update` | 记录已修改 |
| `delete` | 记录已删除 |

## 文件存储

### 存储选项

| 选项 | 配置 | 使用场景 |
|------|------|----------|
| 本地文件系统 | 默认 | 开发 |
| S3 | 环境变量 | 生产 |
| S3 兼容 | MinIO, R2 等 | 自托管 |

### 文件上传

```bash
# 上传文件到记录
curl -X POST http://localhost:8090/api/collections/posts/records \
  -H "Authorization: Bearer YOUR_TOKEN" \
  -F "title=My Post" \
  -F "attachment=@file.pdf"
```

### S3 配置

| 变量 | 说明 |
|------|------|
| `PB_S3_ENDPOINT` | S3 端点 URL |
| `PB_S3_REGION` | S3 区域 |
| `PB_S3_BUCKET` | 存储桶名称 |
| `PB_S3_ACCESS_KEY` | 访问密钥 |
| `PB_S3_SECRET` | 密钥 |
| `PB_S3_FORCE_PATH_STYLE` | 路径风格访问 |

## 自定义代码

### Go 钩子

```go
// hooks/main.go
package hooks

import (
    "github.com/pocketbase/pocketbase"
    "github.com/pocketbase/pocketcore/core"
)

func init() {
    app := pocketbase.New()
    
    app.OnRecordBeforeCreateRequest("posts").Add(func(e *core.RecordCreateEvent) error {
        // 记录创建前的自定义逻辑
        return nil
    })
}
```

### JavaScript 钩子

```javascript
// pb_hooks/main.pb.js
routerAdd("GET", "/api/hello", (c) => {
    return c.json(200, {"message": "Hello World"})
})

onRecordBeforeCreateRequest("posts", (e) => {
    // 记录创建前的自定义逻辑
    console.log("Creating post:", e.record.get("title"))
})
```

### 定时任务

```javascript
// pb_hooks/scheduled.pb.js
cronAdd("cleanup", "0 0 * * *", () => {
    // 每天午夜运行
    const records = $app.dao().findRecordsByFilter(
        "posts",
        "created < @7DaysAgo"
    )
    records.forEach(record => {
        $app.dao().deleteRecord(record)
    })
})
```

## 管理仪表盘

### 仪表盘功能

| 功能 | 路径 | 说明 |
|------|------|------|
| 集合 | `/_/#/collections` | 管理模式 |
| 记录 | `/_/#/collections/{id}` | 浏览数据 |
| 用户 | `/_/#/users` | 管理用户 |
| 日志 | `/_/#/logs` | 请求日志 |
| 设置 | `/_/#/settings` | 应用配置 |
| API 规则 | `/_/#/collections/{id}/rules` | 访问控制 |

### API 规则

| 规则 | 何时应用 | 默认 |
|------|----------|------|
| List | GET /records | 仅管理员 |
| View | GET /records/:id | 仅管理员 |
| Create | POST /records | 仅管理员 |
| Update | PATCH /records/:id | 仅管理员 |
| Delete | DELETE /records/:id | 仅管理员 |

## 总结

PocketBase 在单一二进制文件中提供完整的后端解决方案，消除了对外部数据库、API 服务器或管理面板的需求。其嵌入式 SQLite 数据库、自动生成的 REST API、实时订阅和内置认证使其成为快速原型开发和中小型应用的理想选择。
