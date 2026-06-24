# Bruno：API 客户端教程

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
