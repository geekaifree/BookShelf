# 使用 KeystoneJS 构建无头 CMS

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
