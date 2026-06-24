# Strapi：无头 CMS 教程

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
