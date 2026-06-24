# 使用 Hoppscotch 进行 API 测试

## 简介

Hoppscotch 是一个开源的 API 开发和测试平台。它提供了一个轻量级的基于 Web 的界面，用于构建 HTTP 请求、检查响应和组织 API 工作流。本教程涵盖设置、请求构建、测试和协作功能。

## 平台概览

| 功能 | 描述 | 优势 |
|------|------|------|
| REST Client | HTTP 请求构建器 | 测试任何 REST API |
| GraphQL Client | GraphQL 查询编辑器 | 查询 GraphQL 端点 |
| WebSocket | 实时连接测试 | 测试 WebSocket API |
| SSE | Server-Sent Events | 监控事件流 |
| Socket.IO | Socket.IO 测试 | 测试 Socket.IO 服务器 |
| Collections | 请求组织 | 分组相关请求 |
| Environments | 变量集 | 在不同上下文间切换 |
| Team Collaboration | 共享工作空间 | 协作开发 API |

## 快速开始

### 访问方式

| 方式 | URL | 数据存储 |
|------|-----|----------|
| Web App | hoppscotch.io | 浏览器存储 |
| Self-hosted | 您的服务器 | 服务器数据库 |
| Desktop App | 下载 | 本地存储 |

### 使用 Docker 自托管

```yaml
version: "3.8"
services:
  hoppscotch:
    image: hoppscotch/hoppscotch:latest
    container_name: hoppscotch
    ports:
      - "3000:3000"
    environment:
      - DATABASE_URL=postgresql://user:pass@db:5432/hoppscotch
      - SESSION_SECRET=your-secret-key
    depends_on:
      - db

  db:
    image: postgres:15
    volumes:
      - postgres_data:/var/lib/postgresql/data
    environment:
      - POSTGRES_DB=hoppscotch
      - POSTGRES_USER=user
      - POSTGRES_PASSWORD=pass

volumes:
  postgres_data:
```

## 构建 HTTP 请求

### 请求方法

| 方法 | 用途 | 幂等 | 有请求体 |
|------|------|------|----------|
| GET | 获取资源 | 是 | 否 |
| POST | 创建资源 | 否 | 是 |
| PUT | 替换资源 | 是 | 是 |
| PATCH | 更新资源 | 否 | 是 |
| DELETE | 删除资源 | 是 | 可选 |
| HEAD | 仅获取头部 | 是 | 否 |
| OPTIONS | 检查允许的方法 | 是 | 否 |

### 请求组件

| 组件 | 描述 | 示例 |
|------|------|------|
| Method | HTTP 动词 | GET, POST, PUT |
| URL | 端点地址 | https://api.example.com/users |
| Headers | 键值元数据 | Content-Type: application/json |
| Parameters | URL 查询字符串 | ?page=1&limit=10 |
| Body | 请求负载 | JSON、表单数据、原始文本 |
| Auth | 认证 | Bearer token, Basic auth |

### 构建 GET 请求

1. 从方法下拉菜单中选择 GET
2. 输入 URL：`https://api.example.com/users`
3. 在 Parameters 标签页添加查询参数
4. 在 Headers 标签页添加头部
5. 点击 Send

### 构建 POST 请求

1. 从方法下拉菜单中选择 POST
2. 输入 URL：`https://api.example.com/users`
3. 设置 Content-Type 头为 `application/json`
4. 在 Body 标签页输入 JSON 请求体：

```json
{
  "name": "John Doe",
  "email": "john@example.com",
  "role": "admin"
}
```

5. 点击 Send

## 认证方式

| 方式 | 配置 | 使用场景 |
|------|------|----------|
| None | 无需认证 | 公共 API |
| Basic | 用户名和密码 | 遗留 API |
| Bearer | Authorization 头中的 Token | JWT, OAuth tokens |
| API Key | 头或查询参数中的 Key | 第三方 API |
| OAuth 2.0 | 带 Token 的 OAuth 流程 | 复杂认证流程 |

### Bearer Token 示例

1. 在 Auth 标签页选择 "Bearer Token"
2. 输入 Token 值
3. Hoppscotch 会自动在请求中添加 `Authorization: Bearer <token>`

### API Key 示例

1. 在 Auth 标签页选择 "API Key"
2. 输入 Key 名称和值
3. 选择放置位置：Header 或 Query 参数

## 响应检查

### 响应部分

| 部分 | 内容 | 用途 |
|------|------|------|
| Body | 响应内容 | 查看返回数据 |
| Headers | 响应元数据 | 检查内容类型、缓存 |
| Status | HTTP 状态码 | 验证成功或失败 |
| Time | 响应耗时 | 性能分析 |
| Size | 响应大小 | 带宽分析 |

### HTTP 状态码

| 范围 | 分类 | 示例 |
|------|------|------|
| 1xx | 信息 | 100 Continue |
| 2xx | 成功 | 200 OK, 201 Created, 204 No Content |
| 3xx | 重定向 | 301 Moved, 304 Not Modified |
| 4xx | 客户端错误 | 400 Bad Request, 401 Unauthorized, 404 Not Found |
| 5xx | 服务器错误 | 500 Internal Error, 503 Unavailable |

## 环境变量

环境变量用于在不同上下文间切换：

### 创建环境

创建 "Development" 环境：

| 变量 | 值 |
|------|-----|
| base_url | http://localhost:3000 |
| api_key | dev-key-123 |
| user_id | 1 |

创建 "Production" 环境：

| 变量 | 值 |
|------|-----|
| base_url | https://api.example.com |
| api_key | prod-key-456 |
| user_id | 1 |

### 在请求中使用变量

使用双花括号引用变量：

```
{{base_url}}/api/users/{{user_id}}
Authorization: Bearer {{api_key}}
```

### 变量类型

| 类型 | 范围 | 语法 | 示例 |
|------|------|------|------|
| Environment | 选定的环境 | `{{var}}` | `{{base_url}}` |
| Global | 所有环境 | `{{var}}` | `{{api_version}}` |
| Secret | 隐藏值 | `{{var}}` | `{{api_key}}` |

## 集合

将请求组织为逻辑分组：

### 集合结构

```
My API
├── Authentication
│   ├── Login
│   ├── Refresh Token
│   └── Logout
├── Users
│   ├── List Users
│   ├── Get User
│   ├── Create User
│   ├── Update User
│   └── Delete User
└── Products
    ├── List Products
    └── Get Product
```

### 集合功能

| 功能 | 描述 | 优势 |
|------|------|------|
| 嵌套 | 文件夹中的文件夹 | 层级组织 |
| 共享认证 | 继承的认证 | DRY 配置 |
| 共享头部 | 继承的头部 | 一致的请求 |
| 运行全部 | 执行所有请求 | 批量测试 |
| 导出 | JSON/CSV 导出 | 备份和分享 |

## 预请求脚本

在发送请求前执行 JavaScript：

### 常见预请求任务

| 任务 | 代码 | 目的 |
|------|------|------|
| 设置时间戳 | `pw.env.set("timestamp", Date.now())` | 动态值 |
| 生成 UUID | `pw.env.set("uuid", crypto.randomUUID())` | 唯一标识符 |
| 创建签名 | 计算 HMAC | 请求签名 |
| 读取 Token | `pw.env.set("token", storedToken)` | Token 管理 |

### 示例：生成认证签名

```javascript
const secret = pw.env.get("api_secret");
const timestamp = Date.now();
const message = `${timestamp}GET/users`;
const signature = await crypto.subtle.digest(
  "SHA-256",
  new TextEncoder().encode(secret + message)
);
pw.env.set("signature", btoa(String.fromCharCode(...new Uint8Array(signature))));
```

## 请求后脚本（测试）

在收到响应后执行 JavaScript：

### 测试脚本示例

```javascript
// Check status code
pw.test("Status is 200", () => {
  pw.expect(pw.response.status).toBe(200);
});

// Check response time
pw.test("Response is fast", () => {
  pw.expect(pw.response.time).toBeLessThan(1000);
});

// Check response body
pw.test("Has correct name", () => {
  const data = pw.response.json();
  pw.expect(data.name).toBe("John Doe");
});

// Check header
pw.test("Content type is JSON", () => {
  pw.expect(pw.response.headers.get("content-type")).toContain("application/json");
});
```

### 断言类型

| 断言 | 方法 | 示例 |
|------|------|------|
| 等于 | `toBe()` | `pw.expect(val).toBe(200)` |
| 包含 | `toContain()` | `pw.expect(str).toContain("error")` |
| 大于 | `toBeGreaterThan()` | `pw.expect(val).toBeGreaterThan(0)` |
| 小于 | `toBeLessThan()` | `pw.expect(time).toBeLessThan(500)` |
| 真值 | `toBeTruthy()` | `pw.expect(val).toBeTruthy()` |
| 已定义 | `toBeDefined()` | `pw.expect(val).toBeDefined()` |

## GraphQL 测试

### GraphQL 请求结构

```graphql
query GetUser($id: ID!) {
  user(id: $id) {
    id
    name
    email
    posts {
      id
      title
    }
  }
}
```

### 变量面板

```json
{
  "id": "123"
}
```

### GraphQL 功能

| 功能 | 描述 |
|------|------|
| Schema 内省 | 发现可用的查询和变更 |
| 查询自动补全 | 来自 Schema 的类型建议 |
| 变量面板 | 传递动态值 |
| 订阅支持 | 通过 WebSocket 获取实时数据 |

## WebSocket 测试

### 连接设置

1. 从协议菜单中选择 WebSocket
2. 输入 WebSocket URL：`ws://localhost:8080/ws`
3. 点击 Connect
4. 从消息面板发送消息
5. 在日志中查看接收的消息

### WebSocket 消息类型

| 类型 | 方向 | 描述 |
|------|------|------|
| Text | 发送/接收 | UTF-8 字符串消息 |
| Binary | 发送/接收 | 二进制数据帧 |
| Ping | 客户端 | 连接保活 |
| Pong | 服务器 | 保活响应 |

## 导入和导出

### 支持的格式

| 格式 | 导入 | 导出 | 备注 |
|------|------|------|------|
| Postman Collection v2 | 是 | 是 | 完全兼容 |
| OpenAPI/Swagger | 是 | 是 | API 规范 |
| cURL | 是 | 是 | 命令行请求 |
| Insomnia | 是 | 否 | 有限支持 |
| HAR | 是 | 否 | 浏览器网络日志 |

### 导入 Postman 集合

1. 点击侧边栏的 "Import"
2. 选择 "Import from Postman"
3. 上传 `.json` 集合文件
4. 审查并确认导入

### 导出集合

1. 右键点击集合
2. 选择 "Export"
3. 选择格式
4. 下载文件

## 团队协作

### 工作空间类型

| 类型 | 访问权限 | 使用场景 |
|------|----------|----------|
| Personal | 仅自己 | 个人工作 |
| Team | 共享成员 | 协作 API 开发 |
| Public | 任何有链接的人 | 开放 API 文档 |

### 协作功能

| 功能 | 描述 |
|------|------|
| 共享集合 | 团队成员访问相同集合 |
| 共享环境 | 一致的变量集 |
| 实时同步 | 变更对所有成员可见 |
| 基于角色的访问 | 控制谁可以编辑或查看 |

## 键盘快捷键

| 操作 | Windows/Linux | macOS |
|------|---------------|-------|
| 发送请求 | Ctrl+Enter | Cmd+Enter |
| 保存请求 | Ctrl+S | Cmd+S |
