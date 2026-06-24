# ToolJet 内部工具构建器教程

## 简介

ToolJet 是一款开源低代码平台，用于构建内部工具和仪表板。它连接各种数据源，提供拖拽式界面，无需大量编码即可创建应用。

| 特性 | 描述 |
|---------|-------------|
| 可视化构建器 | 拖拽式界面构建 UI |
| 数据源 | 连接数据库、API 和服务 |
| 组件 | 预构建的 UI 组件加速开发 |
| 工作流 | 自动化和业务逻辑功能 |
| 自托管 | 在您自己的基础设施上部署 |

## 架构

### 系统组件

| 组件 | 用途 |
|-----------|---------|
| Frontend | 基于 React 的可视化应用构建器 |
| Backend | 基于 Node.js 的 API 服务器处理业务逻辑 |
| Database | PostgreSQL 存储应用配置 |
| Redis | 缓存和实时功能 |
| Plugins | 数据源连接器和集成 |

### 数据源

| 类别 | 示例 |
|----------|---------|
| 数据库 | PostgreSQL、MySQL、MongoDB、Redis、MSSQL |
| API | REST API、GraphQL、gRPC |
| 云服务 | AWS S3、Google Sheets、Airtable |
| SaaS | Stripe、Slack、Twilio |
| 文件 | CSV、JSON 文件上传 |

## 安装

### Docker 部署

```bash
docker run -d \
  --name=tooljet \
  -p 3000:3000 \
  -e TOOLJET_DB=postgresql://tooljet:password@db:5432/tooljet_production \
  -e LOCKBOX_MASTER_KEY=your_lockbox_key \
  -e SECRET_KEY_BASE=your_secret_key_base \
  --restart unless-stopped \
  tooljet/tooljet:latest
```

### Docker Compose

```yaml
version: "3.8"
services:
  tooljet:
    image: tooljet/tooljet:latest
    container_name: tooljet
    ports:
      - "3000:3000"
    environment:
      - TOOLJET_DB=postgresql://tooljet:password@db:5432/tooljet_production
      - LOCKBOX_MASTER_KEY=your_lockbox_key
      - SECRET_KEY_BASE=your_secret_key_base
      - PG_HOST=db
    depends_on:
      - db
    restart: unless-stopped

  db:
    image: postgres:15
    container_name: tooljet-db
    environment:
      - POSTGRES_USER=tooljet
      - POSTGRES_PASSWORD=password
      - POSTGRES_DB=tooljet_production
    volumes:
      - postgres_data:/var/lib/postgresql/data
    restart: unless-stopped

volumes:
  postgres_data:
```

## 应用构建器

### 构建器界面

| 区域 | 描述 |
|---------|-------------|
| Canvas | 放置 UI 组件的可视区域 |
| 组件面板 | 可拖拽到 Canvas 上的可用 UI 组件 |
| 属性面板 | 配置选中组件的属性 |
| 查询面板 | 创建和管理数据查询 |
| 状态面板 | 查看应用状态和变量 |

### UI 组件

| 组件 | 使用场景 |
|-----------|----------|
| Button | 触发操作和查询 |
| Text Input | 收集用户文本输入 |
| Dropdown | 从预定义选项中选择 |
| Table | 显示表格数据 |
| Chart | 使用图表可视化数据 |
| Form | 收集结构化数据 |
| Modal | 用于编辑的弹出对话框 |
| Tabs | 将内容组织到标签页中 |
| Image | 显示图片 |
| Rich Text | 格式化文本编辑器 |
| File Picker | 上传文件 |
| Date Picker | 选择日期 |

### 组件属性

| 属性 | 描述 |
|----------|-------------|
| Text | 显示文本内容 |
| Style | CSS 样式（颜色、大小、位置） |
| Events | 用户交互时触发的操作 |
| Visibility | 基于条件显示/隐藏 |
| Loading | 显示加载状态 |
| Validation | 输入验证规则 |

## 数据源配置

### 连接 PostgreSQL

| 字段 | 描述 | 示例 |
|-------|-------------|---------|
| Host | 数据库服务器地址 | localhost |
| Port | 数据库端口 | 5432 |
| Database | 数据库名称 | myapp_db |
| Username | 数据库用户 | app_user |
| Password | 数据库密码 | secure_password |
| SSL | 启用 SSL 连接 | true |

### 连接 REST API

| 字段 | 描述 | 示例 |
|-------|-------------|---------|
| Base URL | API 基础 URL | https://api.example.com |
| Headers | 默认请求头 | Authorization: Bearer token |
| Auth | 认证类型 | API Key、OAuth2、Basic |

### 连接 Google Sheets

| 步骤 | 操作 |
|------|--------|
| 1 | 创建 Google Cloud 项目 |
| 2 | 启用 Google Sheets API |
| 3 | 创建服务账户凭证 |
| 4 | 与服务账户邮箱共享电子表格 |
| 5 | 在 ToolJet 中配置凭证 |

## 查询

### 查询类型

| 类型 | 描述 |
|------|-------------|
| SQL | 为数据库编写 SQL 查询 |
| REST | 发起 HTTP API 请求 |
| GraphQL | 执行 GraphQL 查询 |
| Transformation | 使用 JavaScript 转换数据 |
| Run JS | 执行自定义 JavaScript 代码 |

### 查询编辑器

| 功能 | 描述 |
|---------|-------------|
| 代码编辑器 | 语法高亮的查询编辑器 |
| 预览 | 预览查询结果 |
| 参数 | 向查询传递动态参数 |
| 转换 | 在显示前转换结果 |
| 事件 | 查询完成时触发操作 |

### 查询参数

```javascript
// 在查询中使用组件值
SELECT * FROM users WHERE name LIKE '%{{textInput1.value}}%'

// 使用 URL 参数
SELECT * FROM orders WHERE id = {{params.orderId}}
```

### 数据转换

```javascript
// 转换查询结果
return data.map(row => ({
  ...row,
  fullName: `${row.firstName} ${row.lastName}`,
  isActive: row.status === 'active'
}));
```

## 工作流

### 工作流概念

| 概念 | 描述 |
|---------|-------------|
| Trigger | 启动工作流的事件 |
| Node | 工作流中的单个步骤 |
| Connection | 节点之间的流程 |
| Variables | 节点之间传递的数据 |

### 工作流触发器

| 触发器 | 描述 |
|---------|-------------|
| Webhook | 外部 HTTP 请求 |
| Schedule | 基于时间的触发器 |
| App event | UI 组件事件 |
| Manual | 用户发起的触发器 |

### 工作流节点

| 节点类型 | 描述 |
|-----------|-------------|
| Query | 执行数据源查询 |
| Condition | 基于条件分支 |
| Loop | 遍历数据 |
| Transformation | 使用 JavaScript 转换数据 |
| Notification | 发送通知 |
| HTTP | 发起 HTTP 请求 |

## 用户管理

### 用户角色

| 角色 | 权限 |
|------|-------------|
| Admin | 完全访问所有应用和设置 |
| Developer | 创建和编辑应用 |
| Viewer | 查看和使用已发布的应用 |
| Custom | 定义细粒度权限 |

### 权限

| 权限 | 描述 |
|-----------|-------------|
| App create | 创建新应用 |
| App edit | 修改现有应用 |
| App view | 查看已发布的应用 |
| Data source create | 添加新数据源 |
| Folder manage | 将应用组织到文件夹中 |

## 部署

### 应用发布

| 状态 | 描述 |
|-------|-------------|
| Draft | 开发版本，不公开访问 |
| Published | 用户可访问的上线版本 |
| Archived | 已禁用的应用 |

### 环境变量

| 变量 | 描述 |
|----------|-------------|
| TOOLJET_DB | PostgreSQL 连接字符串 |
| LOCKBOX_MASTER_KEY | 密钥加密密钥 |
| SECRET_KEY_BASE | 应用密钥 |
| NODE_ENV | 环境（production/development） |

## 导入和导出

### 应用导出

| 格式 | 描述 |
|--------|-------------|
| JSON | 包含查询和组件的完整应用定义 |
| Template | 可复用的应用模板 |

### 应用导入

| 来源 | 描述 |
|--------|-------------|
| JSON 文件 | 从导出的 JSON 导入 |
| Template | 从模板库导入 |
| Clone | 克隆现有应用 |

## API 访问

### REST API 端点

| 端点 | 方法 | 描述 |
|----------|--------|-------------|
| `/api/apps` | GET | 列出应用 |
| `/api/apps/{id}` | GET | 获取应用详情 |
| `/api/apps/{id}/export` | GET | 导出应用 |
| `/api/data_sources` | GET | 列出数据源 |
| `/api/users` | GET | 列出用户 |

## 总结

| 主题 | 核心要点 |
|-------|-------------|
| 用途 | 低代码平台，构建内部工具 |
| 构建器 | 带预构建组件的拖拽式 UI |
| 数据 | 连接数据库、API 和 SaaS 服务 |
| 查询 | SQL、REST、GraphQL 和 JavaScript 转换 |
| 工作流 | 带触发器、条件和循环的自动化 |
| 部署 | 自托管，带基于角色的访问控制 |
