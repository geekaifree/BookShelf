# Appwrite：构建后端服务器

## 简介

Appwrite 是一个开源后端服务器，提供一组 API 和工具用于构建 Web 和移动应用程序。它处理认证、数据库、存储、函数和实时消息。本教程涵盖设置、核心服务和集成模式。

## 架构概览

| 组件 | 描述 | 用途 |
|------|------|------|
| API 服务器 | RESTful API 层 | 处理所有客户端请求 |
| 数据库 | 带有抽象层的 MariaDB | 基于文档的数据存储 |
| 存储 | 文件管理 | 上传、下载、转换文件 |
| 函数 | 无服务器计算 | 自定义后端逻辑 |
| 消息 | 实时事件 | WebSocket 和推送通知 |

## 安装

### Docker Compose

```yaml
version: "3"
services:
  appwrite:
    image: appwrite/appwrite:latest
    restart: unless-stopped
    ports:
      - "80:80"
      - "443:443"
    volumes:
      - /var/run/docker.sock:/var/run/docker.sock
      - appwrite-uploads:/storage/uploads
      - appwrite-cache:/storage/cache
    environment:
      - APPWRITE_ENDPOINT=http://localhost:80
      - APPWRITE_SECRET=your-secret-key
```

### Docker 单行命令

```bash
docker run -it --rm \
  --volume /var/run/docker.sock:/var/run/docker.sock \
  --volume "$(pwd)"/appwrite:/usr/src/code/appwrite:rw \
  --entrypoint="install" \
  appwrite/appwrite:latest
```

## 核心服务

### 认证

Appwrite 提供多种认证方式。

| 方式 | 描述 | 使用场景 |
|------|------|----------|
| 邮箱/密码 | 传统登录 | 标准 Web 应用 |
| OAuth2 | Google、GitHub、Facebook 等 | 社交登录 |
| 匿名 | 临时会话 | 访客访问 |
| Magic URL | 基于邮箱的登录链接 | 无密码登录 |
| 手机（短信） | OTP 验证 | 移动应用 |
| 自定义 Token | JWT 或自定义提供者 | 企业 SSO |

### SDK 集成

```javascript
import { Client, Account } from 'appwrite';

const client = new Client();
client
  .setEndpoint('https://cloud.appwrite.io/v1')
  .setProject('your-project-id');

const account = new Account(client);

// 注册新用户
await account.create(
  'unique()',
  'user@example.com',
  'securePassword123',
  'John Doe'
);

// 登录
await account.createEmailSession(
  'user@example.com',
  'securePassword123'
);
```

### 数据库

数据库服务以 JSON 文档形式在集合中存储数据。

| 操作 | 方法 | 描述 |
|------|------|------|
| 创建 | `databases.createDocument()` | 插入新文档 |
| 读取 | `databases.getDocument()` | 通过 ID 获取文档 |
| 更新 | `databases.updateDocument()` | 修改现有文档 |
| 删除 | `databases.deleteDocument()` | 删除文档 |
| 列表 | `databases.listDocuments()` | 带筛选和分页的查询 |

#### 数据模型

| 概念 | 描述 |
|------|------|
| Database | 集合的顶级容器 |
| Collection | 文档类型的架构定义 |
| Document | 集合中的单条记录 |
| Attributes | 集合架构中的类型化字段 |

#### 创建集合

```javascript
// 定义属性
await databases.createStringAttribute(
  'database-id',
  'collection-id',
  'title',
  256,
  true  // 必填
);

await databases.createIntegerAttribute(
  'database-id',
  'collection-id',
  'price',
  true,
  0,    // 最小值
  99999 // 最大值
);
```

#### 查询文档

```javascript
import { Query } from 'appwrite';

const results = await databases.listDocuments(
  'database-id',
  'collection-id',
  [
    Query.equal('category', 'electronics'),
    Query.greaterThan('price', 100),
    Query.orderDesc('createdAt'),
    Query.limit(20)
  ]
);
```

### 存储

| 功能 | 描述 |
|------|------|
| 上传 | 存储文件，大小限制可配置 |
| 下载 | 通过 ID 获取文件 |
| 预览 | 生成缩略图和预览图 |
| 压缩 | 自动图片压缩 |
| 加密 | 文件静态加密 |

```javascript
import { Storage } from 'appwrite';

const storage = new Storage(client);

// 上传文件
const response = await storage.createFile(
  'bucket-id',
  'unique()',
  document.getElementById('file').files[0]
);

// 获取文件预览
const preview = storage.getFilePreview('bucket-id', 'file-id');
```

### 函数

无服务器函数响应事件或 API 调用运行自定义代码。

| 运行时 | 语言 | 状态 |
|--------|------|------|
| Node.js | JavaScript/TypeScript | 稳定 |
| Python | Python 3.x | 稳定 |
| PHP | PHP 8.x | 稳定 |
| Ruby | Ruby 3.x | 稳定 |
| Dart | Dart | 稳定 |
| Swift | Swift | Beta |
| .NET | C# | Beta |

#### 函数示例（Node.js）

```javascript
module.exports = async (req, res) => {
  const payload = JSON.parse(req.payload);

  // 处理数据
  const result = {
    message: `Hello, ${payload.name}!`,
    timestamp: new Date().toISOString()
  };

  return res.json(result);
};
```

## 权限和角色

| 级别 | 描述 | 示例 |
|------|------|------|
| Collection | 所有文档的默认权限 | 读取：any，写入：users |
| Document | 每个文档的覆盖设置 | 读取：特定用户 ID |
| Bucket | 文件访问控制 | 读取：team:admin |
| Function | 谁可以执行 | 执行：any、team:dev |

### 角色语法

| 角色 | 格式 | 含义 |
|------|------|------|
| Any | `any` | 所有用户，包括访客 |
| User | `user:{userId}` | 特定已认证用户 |
| Team | `team:{teamId}` | 团队成员 |
| 带角色的 Team | `team:{teamId}/{role}` | 具有特定角色的团队成员 |
| Label | `label:{labelName}` | 具有特定标签的用户 |

## 实时事件

订阅跨服务的变更。

```javascript
client.subscribe('documents', (response) => {
  console.log(response.events);  // 例如 'documents.*.create'
  console.log(response.payload);
});

// 订阅特定集合
client.subscribe('databases.db1.collections.col1.documents', (response) => {
  // 处理文档变更
});
```

## 环境变量

| 变量 | 描述 | 默认值 |
|------|------|--------|
| `_APP_OPENSSL_KEY_V1` | 加密密钥 | 自动生成 |
| `_APP_DOMAIN` | 服务器域名 | localhost |
| `_APP_DOMAIN_TARGET` | 重定向目标 | CNAME |
| `_APP_DB_HOST` | 数据库主机 | mariadb |
| `_APP_STORAGE_LIMIT` | 最大上传大小 | 30MB |
| `_APP_FUNCTIONS_TIMEOUT` | 函数超时 | 15s |

## 项目配置

| 设置 | 描述 |
|------|------|
| 项目名称 | 应用的显示名称 |
| 项目 ID | 唯一标识符 |
| 平台 | Web、Flutter、React Native 等 |
| API 端点 | 请求的服务器 URL |
| 认证提供者 | 启用 OAuth 提供者 |
| 自定义域名 | 映射你自己的域名 |

## 客户端 SDK

| 平台 | 包名 | 语言 |
|------|------|------|
| Web | `appwrite` | JavaScript |
| Flutter | `appwrite` | Dart |
| Android | `appwrite` | Kotlin |
| iOS | `appwrite` | Swift |
| React Native | `appwrite` | JavaScript |
| Apple | `appwrite` | Swift |

## 总结

Appwrite 提供完整的后端即服务，包含认证、数据库、存储、函数和实时功能。它作为一组 Docker 容器运行，支持多个客户端 SDK。使用它可以加速开发，同时通过自托管完全控制你的数据。
