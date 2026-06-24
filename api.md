# Insomnia：API 设计和测试客户端

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
