# API 测试

> 本文档整合了以下源文件：apitest.md, http.md, bruno.md, api.md

---

## 来源：apitest.md

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


---

## 来源：http.md

## 简介

HTTPie 是一个命令行 HTTP 客户端，专为与 Web 服务和 API 交互而设计。它提供了富有表现力的语法、格式化输出和内置的现代 API 开发功能。本教程涵盖安装、使用模式和高级功能。

## 安装

### 包管理器

| 平台 | 命令 |
|------|------|
| macOS (Homebrew) | `brew install httpie` |
| Ubuntu/Debian | `apt install httpie` |
| Fedora | `dnf install httpie` |
| Windows (Scoop) | `scoop install httpie` |
| pip | `pip install httpie` |
| Snap | `snap install http` |

### 验证安装

```bash
http --version
http --help
```

## 基本语法

### 命令结构

```
http [flags] [METHOD] URL [ITEM [ITEM...]]
```

### 组件

| 组件 | 描述 | 示例 |
|------|------|------|
| METHOD | HTTP 方法（默认：GET） | GET, POST, PUT, DELETE |
| URL | 目标端点 | api.example.com/users |
| ITEM | 请求数据 | headers, params, body |
| FLAGS | 行为修饰符 | --verbose, --headers |

### 简单 GET 请求

```bash
http GET https://api.example.com/users
```

或直接：

```bash
http https://api.example.com/users
```

## 请求方法

### 方法快捷方式

| 快捷方式 | 方法 | 示例 |
|----------|------|------|
| `http URL` | GET | `http api.example.com/users` |
| `http POST URL` | POST | `http POST api.example.com/users` |
| `http PUT URL` | PUT | `http PUT api.example.com/users/1` |
| `http PATCH URL` | PATCH | `http PATCH api.example.com/users/1` |
| `http DELETE URL` | DELETE | `http DELETE api.example.com/users/1` |
| `http HEAD URL` | HEAD | `http HEAD api.example.com/users` |
| `http OPTIONS URL` | OPTIONS | `http OPTIONS api.example.com/users` |

## 发送数据

### 请求项类型

| 语法 | 类型 | 示例 |
|------|------|------|
| `key=value` | JSON 字符串字段 | `name=John` |
| `key:=value` | JSON 非字符串 | `age:=30` |
| `key@value` | 文件上传 | `avatar@photo.jpg` |
| `key:value` | HTTP 头 | `Authorization:Bearer token` |
| `key==value` | URL 参数 | `page==1` |

### JSON 数据

```bash
# 字符串值（自动加引号）
http POST api.example.com/users name="John Doe" email="john@example.com"

# 非字符串值（使用 :=）
http POST api.example.com/users name="John" age:=30 active:=true

# 嵌套 JSON
http POST api.example.com/users name="John" address[city]="New York" address[zip]="10001"

# 数组值
http POST api.example.com/users names[]="John" names[]="Jane"
```

### 原始 JSON 请求体

```bash
# 从 stdin 管道传入 JSON
echo '{"name": "John", "age": 30}' | http POST api.example.com/users

# 使用 --raw 标志
http --raw='{"name": "John", "age": 30}' POST api.example.com/users
```

### 表单数据

```bash
# URL 编码表单
http --form POST api.example.com/login username=admin password=secret

# 带文件的多部分表单
http --form POST api.example.com/upload file@document.pdf description="My file"
```

## 请求头

### 设置请求头

```bash
# 自定义头部
http api.example.com X-Custom-Header:value

# Authorization 头
http api.example.com Authorization:"Bearer eyJhbGci..."

# Content-Type 覆盖
http POST api.example.com/data Content-Type:text/xml '<data>hello</data>'
```

### 默认请求头

| 头部 | 默认值 | 覆盖方式 |
|------|--------|----------|
| User-Agent | HTTPie/version | `User-Agent:CustomAgent` |
| Accept | application/json | `Accept:text/html` |
| Content-Type | 自动检测 | `Content-Type:text/xml` |
| Host | 来自 URL | `Host:custom.host` |

### 移除请求头

```bash
# 移除头部
http api.example.com Header-Name:
```

## 认证

### 内置认证方式

| 方式 | 标志 | 示例 |
|------|------|------|
| Basic | `-a user:pass` | `http -a admin:secret api.example.com` |
| Bearer | `Authorization:Bearer TOKEN` | `http api.example.com Authorization:"Bearer abc123"` |
| Digest | `--auth-type=digest -a user:pass` | `http --auth-type=digest -a admin:secret api.example.com` |

### 认证插件示例

```bash
# 安装认证插件
pip install httpie-jwt-auth
pip install httpie-api-key

# JWT 认证
http --auth-type=jwt --auth=TOKEN api.example.com

# 头部中的 API key
http api.example.com X-API-Key:your-key
```

## 输出控制

### 输出标志

| 标志 | 描述 | 示例 |
|------|------|------|
| `-v` | 详细（头部 + 请求体） | `http -v api.example.com` |
| `-h` | 仅头部 | `http -h api.example.com` |
| `-b` | 仅请求体 | `http -b api.example.com` |
| `-p H` | 打印特定部分 | `http -p Hh api.example.com` |
| `-S` | 流式输出 | `http -S api.example.com` |
| `-o FILE` | 保存到文件 | `http -o output.json api.example.com` |

### 打印部分标志

| 标志 | 含义 |
|------|------|
| `H` | 请求头 |
| `B` | 请求体 |
| `h` | 响应头 |
| `b` | 响应体 |

```bash
# 打印请求和响应头部
http -p Hh api.example.com

# 仅打印响应体
http -p b api.example.com
```

## 会话

会话在请求间持久化 Cookie、头部和认证信息：

```bash
# 创建/使用命名会话
http --session=mysession api.example.com/login username=admin password=secret

# 后续请求使用存储的 Cookie
http --session=mysession api.example.com/dashboard

# 自定义文件路径的会话
http --session=/path/to/session.json api.example.com
```

### 会话文件内容

| 数据 | 持久化 | 目的 |
|------|--------|------|
| Cookies | 是 | 认证状态 |
| Auth 头部 | 是 | 复用凭据 |
| 自定义头部 | 是 | 一致的请求头 |
| 代理设置 | 是 | 网络配置 |

## 下载文件

```bash
# 使用原始文件名下载
http --download https://example.com/file.pdf

# 使用自定义名称下载
http --download --output=report.pdf https://example.com/file.pdf

# 带进度条下载
http --download --progress https://example.com/large-file.zip
```

## 代理配置

```bash
# HTTP 代理
http --proxy=http:http://proxy:8080 api.example.com

# SOCKS 代理
http --proxy=http:socks5://proxy:1080 api.example.com

# 带认证的代理
http --proxy=http:http://user:pass@proxy:8080 api.example.com
```

## SSL/TLS 选项

| 标志 | 描述 | 使用场景 |
|------|------|----------|
| `--verify=no` | 跳过证书验证 | 自签名证书（测试） |
| `--verify=yes` | 强制验证 | 生产环境 |
| `--ssl=TLSv1.2` | 强制 TLS 版本 | 兼容性测试 |
| `--cert=CERT` | 客户端证书 | 双向 TLS |
| `--cert-key=KEY` | 客户端证书密钥 | 双向 TLS |

```bash
# 跳过验证（仅测试）
http --verify=no https://self-signed.example.com

# 客户端证书
http --cert=client.pem --cert-key=key.pem https://mtls.example.com
```

## 查询字符串参数

```bash
# URL 参数
http api.example.com/users page==1 limit==10 sort==name

# 编码参数
http api.example.com/search q=="hello world"

# 与请求体数据结合
http POST api.example.com/users?page==1 name="John" age:=30
```

## 重定向

| 标志 | 描述 | 默认值 |
|------|------|--------|
| `--follow` | 跟随重定向 | GET 请求默认是 |
| `--max-redirects=N` | 限制重定向次数 | 30 |
| `--all` | 显示中间重定向 | 关闭 |

```bash
# 显式跟随重定向
http --follow api.example.com/old-path

# 显示所有重定向步骤
http --follow --all api.example.com/old-path
```

## 配置文件

创建 `~/.config/httpie/config.json`：

```json
{
  "default_options": [
    "--session=default",
    "--print=HhBb",
    "--style=monokai"
  ]
}
```

### 配置选项

| 设置 | 描述 | 示例 |
|------|------|------|
| default_options | 始终应用的标志 | `["--verbose"]` |
| output_options | 默认输出设置 | `["--format=json"]` |
| style | 语法高亮 | monokai, fruity, monochrome |

## 实际示例

### REST API 工作流

```bash
# 列出资源
http GET api.example.com/users

# 创建资源
http POST api.example.com/users name="John" email="john@example.com"

# 更新资源
http PUT api.example.com/users/1 name="John Smith"

# 部分更新
http PATCH api.example.com/users/1 email="newemail@example.com"

# 删除资源
http DELETE api.example.com/users/1
```

### 分页

```bash
# 分页浏览结果
http api.example.com/users page==1 per_page==10
http api.example.com/users page==2 per_page==10
```

### 条件请求

```bash
# If-None-Match (ETag)
http api.example.com/users/1 If-None-Match:'"abc123"'

# If-Modified-Since
http api.example.com/users/1 If-Modified-Since:"Wed, 01 Jan 2026 00:00:00 GMT"
```

## 与 cURL 对比

| 功能 | HTTPie | cURL |
|------|--------|------|
| 语法 | 直观 | 冗长 |
| JSON 支持 | 自动 | 手动 |
| 输出格式化 | 彩色 | 原始 |
| 会话 | 内置 | Cookie 文件 |
| 认证 | 简化 | 标志 |
| 表单数据 | `--form` 标志 | `-F` 标志 |
| 学习曲线 | 低 | 中等 |

### 等效命令

| 任务 | HTTPie | cURL |
|------|--------|------|
| GET 请求 | `http api.example.com/users` | `curl https://api.example.com/users` |
| POST JSON | `http POST url name=John` | `curl -X POST -H 'Content-Type: application/json' -d '{"name":"John"}' url` |
| 认证 | `http -a user:pass url` | `curl -u user:pass url` |
| 头部 | `http url X-Header:val` | `curl -H 'X-Header:val' url` |

## 总结

HTTPie 提供了一个富有表现力、人性化的 HTTP 通信界面。其自动 JSON 处理、格式化输出和会话管理使其成为 API 开发和测试的高效工具。

关键实践：

- 使用会话在请求间维护认证状态
- 利用 `:=` 语法处理非字符串 JSON 值
- 在配置文件中配置默认选项
- 使用 `--download` 进行带进度跟踪的文件下载
- 结合 Shell 脚本实现自动化 API 工作流


---

## 来源：bruno.md

## 简介

Bruno 是一个开源的 API 客户端，旨在替代 Postman。它使用一种名为 Bru 的纯文本标记语言，将集合直接存储在文件系统的文件夹中。本教程涵盖安装、创建请求、组织集合以及与版本控制的集成。

## 为什么选择 Bruno

| 功能 | Bruno | Postman | Insomnia |
|------|-------|---------|----------|
| 开源 | 是（MIT） | 否 | 部分 |
| 数据存储 | 文件系统（Git 友好） | 云端 | 云端/本地 |
| 离线模式 | 完整 | 有限 | 部分 |
| 集合格式 | 纯文本（.bru） | JSON | YAML |
| 协作 | 基于 Git | 云端同步 | 云端同步 |
| 定价 | 免费 | 免费增值 | 免费增值 |

## 安装

| 平台 | 方法 |
|------|------|
| Windows | 从 releases 下载安装程序 |
| macOS | Homebrew：brew install --cask bruno |
| Linux | 从 releases 下载 AppImage、Flatpak 或 Snap |
| 源码 | 使用 npm 克隆并构建 |

## 用户界面

| 面板 | 位置 | 用途 |
|------|------|------|
| 集合侧边栏 | 左侧 | 浏览和组织集合 |
| 请求编辑器 | 中央 | 构建和配置请求 |
| 响应面板 | 底部/右侧 | 查看响应数据 |
| 环境选择器 | 顶栏 | 切换环境 |
| 变量面板 | 侧边栏 | 管理集合变量 |

## 创建请求

### HTTP 方法

| 方法 | 用例 |
|------|------|
| GET | 从服务器获取数据 |
| POST | 创建新资源 |
| PUT | 替换整个资源 |
| PATCH | 部分更新资源 |
| DELETE | 删除资源 |
| HEAD | 仅获取头部信息 |
| OPTIONS | 检查允许的方法 |

### 请求配置

| 标签页 | 用途 |
|--------|------|
| Params | URL 查询参数 |
| Auth | 认证头部 |
| Headers | 自定义 HTTP 头部 |
| Body | 请求体（JSON、表单等） |
| Scripts | 请求前和响应后脚本 |
| Tests | 断言脚本 |
| Vars | 从响应中提取变量 |

### 请求体类型

| 类型 | Content-Type | 用例 |
|------|-------------|------|
| JSON | application/json | REST API |
| Form URL Encoded | application/x-www-form-urlencoded | 传统表单 |
| Multipart Form | multipart/form-data | 文件上传 |
| XML | application/xml | SOAP API |
| Plain Text | text/plain | 原始文本 |
| None | - | GET/HEAD 请求 |

## 集合

### 集合结构

```
my-api/
  environments/
    local.bru
    production.bru
  requests/
    users/
      get-users.bru
      create-user.bru
    posts/
      get-posts.bru
  collection.bru
```

### Bru 文件格式

.bru 文件使用纯文本格式：

```
meta {
  name: Get Users
  type: http
  seq: 1
}

get {
  url: https://api.example.com/users
  body: none
  auth: none
}

headers {
  Content-Type: application/json
  Authorization: Bearer {{token}}
}

query {
  page: 1
  limit: 10
}

tests {
  test: should return 200
  code: expect(res.status).to.equal(200)
}
```

### 集合操作

| 操作 | 方法 |
|------|------|
| 创建 | File > New Collection |
| 导入 | File > Import Collection（Postman、Insomnia、OpenAPI） |
| 导出 | 右键 > Export |
| 复制 | 右键 > Duplicate |
| 删除 | 右键 > Delete |

## 环境

### 环境类型

| 类型 | 用途 |
|------|------|
| Local | 开发机器设置 |
| Development | 共享开发服务器 |
| Staging | 预生产测试 |
| Production | 生产服务器 |

### 环境变量

| 变量 | 示例 | 用途 |
|------|------|------|
| base_url | https://api.dev.example.com | API 端点 |
| api_key | sk_test_abc123 | 认证 |
| user_id | 42 | 测试数据 |
| timeout | 5000 | 请求超时 |

### 切换环境

1. 点击顶栏的环境下拉菜单。
2. 选择所需的环境。
3. 所有 {{variable}} 引用将从该环境解析。

## 认证

### 认证方式

| 方式 | 配置 |
|------|------|
| Bearer Token | 设置 Authorization: Bearer <token> 头部 |
| Basic Auth | 用户名和密码字段 |
| API Key | 自定义头部或查询参数 |
| OAuth 2.0 | 配置 client ID、secret 和流程 |
| Digest Auth | 用户名、密码、realm |

### OAuth 2.0 流程

| 流程 | 用例 |
|------|------|
| Authorization Code | 服务端 Web 应用 |
| Client Credentials | 机器对机器 |
| Implicit（已弃用） | SPA（改用 PKCE） |
| Password | 遗留应用 |

## 脚本

### 请求前脚本

在请求发送前运行。

| 用例 | 示例 |
|------|------|
| 生成时间戳 | bru.setVar("timestamp", Date.now()) |
| 设置动态认证 | bru.setVar("token", generateToken()) |
| 记录请求 | console.log("Sending to:", req.getUrl()) |

### 响应后脚本

在收到响应后运行。

| 用例 | 示例 |
|------|------|
| 提取令牌 | bru.setVar("token", res.body.token) |
| 验证状态 | expect(res.status).to.equal(200) |
| 记录响应 | console.log("Status:", res.status) |

### 断言示例

| 断言 | 代码 |
|------|------|
| 状态码 | expect(res.status).to.equal(200) |
| 响应时间 | expect(res.responseTime).to.be.below(1000) |
| Body 字段 | expect(res.body.data.name).to.equal("John") |
| 头部存在 | expect(res.headers["content-type"]).to.exist |
| JSON schema | expect(res.body).to.have.jsonSchema(schema) |

## 导入和导出

### 支持的格式

| 格式 | 导入 | 导出 |
|------|------|------|
| Postman Collection v2.1 | 是 | 否 |
| Insomnia | 是 | 否 |
| OpenAPI/Swagger | 是 | 否 |
| Bruno（.bru） | 是 | 是 |
| cURL | 是 | 否 |

## 版本控制集成

### Git 工作流程

| 步骤 | 操作 |
|------|------|
| 1 | 在集合文件夹中初始化 git |
| 2 | 将 .bru 文件作为普通文本提交 |
| 3 | 单独共享环境（排除密钥） |
| 4 | 对敏感环境使用 .gitignore |

### Bruno 的 .gitignore

```
# 忽略生产环境密钥
environments/production.bru
# 保留其他所有文件
!*.bru
```

## 快捷键

| 快捷键 | 操作 |
|--------|------|
| Ctrl+N | 新建请求 |
| Ctrl+Enter | 发送请求 |
| Ctrl+S | 保存请求 |
| Ctrl+Shift+E | 切换环境 |
| Ctrl+L | 聚焦 URL 栏 |
| Ctrl+Shift+P | 命令面板 |

## Bruno CLI

从命令行运行集合。

```bash
npm install -g @usebruno/cli
bru run --env production
```

| 命令 | 用途 |
|------|------|
| bru run | 执行集合中的所有请求 |
| bru run --env local | 使用特定环境运行 |
| bru run --folder users | 运行文件夹中的请求 |

## 与其他工具的对比

| 功能 | Bruno | Postman | Insomnia |
|------|-------|---------|----------|
| 数据所有权 | 文件系统 | 云端 | 混合 |
| Git 支持 | 原生 | 导入/导出 | 导入/导出 |
| 团队协作 | 基于 Git | 基于云端 | 基于云端 |
| 脚本 | JavaScript | JavaScript | JavaScript |
| GraphQL | 是 | 是 | 是 |
| gRPC | 即将支持 | 是 | 是 |
| WebSocket | 即将支持 | 是 | 是 |
| Mock 服务器 | 即将支持 | 是 | 否 |

## 总结

Bruno 提供了一个开发者友好的 API 客户端，将集合存储为文件系统上的纯文本文件。其原生 Git 协作方式、简洁的 Bru 格式和开源特性，使其成为偏好版本控制 API 工作流程而非依赖云端方案的团队的理想选择。


---

## 来源：api.md

## 简介

Insomnia 是一款强大的开源 API 客户端，用于设计、测试和调试 API。它支持 REST、GraphQL、gRPC 和 WebSocket 协议。

| 属性 | 详情 |
|----------|--------|
| 仓库 | Kong/insomnia |
| 许可证 | Apache-2.0 |
| 语言 | TypeScript, JavaScript |
| 平台 | Windows, macOS, Linux |
| 协议 | REST, GraphQL, gRPC, WebSocket |

## 安装

### Linux

```bash
# Ubuntu/Debian (deb 包)
# 从 GitHub 发布页面下载

# Snap
sudo snap install insomnia

# Flatpak
flatpak install rest.insomnia.Insomnia
```

### macOS

```bash
brew install --cask insomnia
```

### Windows

从 Insomnia 官方网站下载安装程序。

## 核心功能

| 功能 | 描述 |
|---------|-------------|
| Request Builder（请求构建器） | HTTP 请求的可视化编辑器 |
| Environments（环境） | 管理不同上下文的变量 |
| Collections（集合） | 将请求组织到文件夹中 |
| Authentication（认证） | 内置认证辅助工具 |
| Response Viewer（响应查看器） | 格式化和检查响应 |
| Code Generation（代码生成） | 为各种语言生成代码片段 |
| Testing（测试） | 编写和运行 API 测试 |
| Mock Servers（模拟服务器） | 为开发创建模拟 API |

## 界面概览

| 面板 | 描述 |
|-------|-------------|
| Sidebar（侧边栏） | 请求集合和文件夹树 |
| Request Tab（请求选项卡） | 构建和配置请求 |
| Response Tab（响应选项卡） | 查看响应体、头信息和状态 |
| Environment（环境） | 选择和管理环境 |
| Timeline（时间线） | 请求/响应时间线 |

## 创建请求

### HTTP 方法

| 方法 | 描述 |
|--------|-------------|
| GET | 获取资源 |
| POST | 创建新资源 |
| PUT | 更新整个资源 |
| PATCH | 部分更新资源 |
| DELETE | 删除资源 |
| HEAD | 仅获取头信息 |
| OPTIONS | 获取允许的方法 |

### 请求配置

| 选项卡 | 描述 |
|-----|-------------|
| Parameters（参数） | 查询字符串参数 |
| Headers（头信息） | HTTP 请求头 |
| Body（请求体） | 请求体（JSON, form, file） |
| Auth（认证） | 认证设置 |
| Docs（文档） | 请求文档 |

### 示例：创建 GET 请求

1. 点击 "+" 按钮创建新请求。
2. 将方法设置为 GET。
3. 输入 URL：`https://api.example.com/users`
4. 添加任何查询参数。
5. 点击 "Send" 执行。

## 环境

环境允许您在不同配置（开发、预发布、生产）之间切换。

### 环境变量

| 变量 | 示例 |
|----------|---------|
| base_url | `https://api.example.com` |
| api_key | `your-api-key-here` |
| user_id | `12345` |

### 使用变量

在请求中使用双花括号引用变量。

```
{{ base_url }}/users/{{ user_id }}
Authorization: Bearer {{ api_key }}
```

### 环境类型

| 类型 | 描述 |
|------|-------------|
| Base（基础） | 所有环境共享的变量 |
| Sub Environment（子环境） | 特定于单个环境 |

## 认证

Insomnia 支持多种认证方式。

| 类型 | 描述 |
|------|-------------|
| Basic Auth | 用户名和密码 |
| Bearer Token | Authorization 头中的 token |
| OAuth 2.0 | 完整的 OAuth 流程支持 |
| API Key | 自定义头或查询参数 |
| AWS IAM | AWS Signature Version 4 |
| NTLM | Windows NT LAN Manager |
| Digest | 摘要访问认证 |
| Atlassian ASAP | Atlassian token 认证 |

## GraphQL 支持

### 功能

| 功能 | 描述 |
|---------|-------------|
| Schema Introspection（模式自省） | 自动发现 GraphQL 模式 |
| Query Builder（查询构建器） | 可视化查询构建 |
| Autocomplete（自动完成） | 模式感知的建议 |
| Variables（变量） | 支持查询变量 |
| Fragments（片段） | 可重用的查询片段 |

### 示例 GraphQL 查询

```graphql
query GetUser($id: ID!) {
  user(id: $id) {
    name
    email
    posts {
      title
      createdAt
    }
  }
}
```

## gRPC 支持

| 功能 | 描述 |
|---------|-------------|
| Proto Files（Proto 文件） | 导入 .proto 定义 |
| Services（服务） | 浏览可用服务 |
| Methods（方法） | 调用单个 RPC 方法 |
| Streaming（流） | 支持所有流类型 |
| Metadata（元数据） | 添加 gRPC 元数据头 |

### gRPC 流类型

| 类型 | 描述 |
|------|-------------|
| Unary（一元） | 单个请求，单个响应 |
| Server Streaming（服务端流） | 单个请求，多个响应 |
| Client Streaming（客户端流） | 多个请求，单个响应 |
| Bidirectional（双向） | 多个请求和响应 |

## WebSocket 支持

| 功能 | 描述 |
|---------|-------------|
| Connection（连接） | 连接到 WebSocket 服务器 |
| Messages（消息） | 发送和接收消息 |
| History（历史） | 查看消息历史 |
| Protocols（协议） | 指定 WebSocket 子协议 |

## 测试

Insomnia 允许使用 JavaScript 编写测试。

### 测试示例

```javascript
// 检查状态码
expect(response.status).to.equal(200);

// 检查响应体
expect(response.body.name).to.equal("John");

// 检查头信息
expect(response.headers["content-type"]).to.include("application/json");
```

### 测试结果

测试在每次请求后自动运行，并在响应面板中显示结果。

## 代码生成

为各种编程语言生成代码片段。

| 语言 | 框架 |
|----------|-----------|
| cURL | 命令行 |
| Python | requests |
| JavaScript | fetch, axios |
| Java | OkHttp |
| C# | HttpClient |
| Go | net/http |
| Ruby | net/http |
| PHP | cURL |
| Swift | URLSession |

## 环境和子环境

| 级别 | 描述 |
|-------|-------------|
| Base Environment（基础环境） | 所有环境共享的公共变量 |
| Sub Environment（子环境） | 环境特定的覆盖 |
| Private Environment（私有环境） | 仅本地变量（不同步） |

## 设计文档

Insomnia 包含 API 设计功能，用于在实现前定义 API。

| 功能 | 描述 |
|---------|-------------|
| OpenAPI | 使用 OpenAPI 3.0 规范设计 |
| Endpoints（端点） | 可视化定义 API 端点 |
| Schemas（模式） | 定义请求和响应模式 |
| Documentation（文档） | 生成 API 文档 |

## 插件

Insomnia 支持插件系统以扩展功能。

| 插件 | 描述 |
|--------|-------------|
| insomnia-plugin-jwt | JWT token 解码器 |
| insomnia-plugin-random | 生成随机数据 |
| insomnia-plugin-base64 | Base64 编码/解码 |

## 技巧和最佳实践

| 技巧 | 说明 |
|-----|-------------|
| 使用环境 | 分离开发、预生产和生产配置 |
| 组织请求 | 使用文件夹和标签进行组织 |
| 文档化请求 | 为请求添加描述 |
| 使用变量 | 避免硬编码 URL 和 token |
| 导出集合 | 与团队成员分享集合 |
| 运行测试 | 自动验证 API 响应 |

## 结论

Insomnia 是一款多功能的 API 客户端，简化了设计、测试和调试 API 的过程。其对多种协议的支持和内置的测试功能使其成为 API 开发人员的必备工具。


---
