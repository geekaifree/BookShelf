# n8n：工作流自动化平台

## 目录

1. [n8n 简介](#introduction)
2. [安装与设置](#installation)
3. [核心概念](#core-concepts)
4. [构建工作流](#building-workflows)
5. [常用集成](#integrations)
6. [高级功能](#advanced-features)
7. [错误处理](#error-handling)
8. [部署与扩展](#deployment)

---

## 简介

n8n 是一个可扩展的工作流自动化工具，通过可视化的节点界面连接各种服务并自动化任务。用户无需大量编码即可构建复杂的自动化流程。

### n8n 核心功能

| 功能 | 描述 | 好处 |
|------|------|------|
| 可视化编辑器 | 拖拽式工作流构建 | 易于学习 |
| 自托管 | 在自己的服务器上运行 | 数据控制 |
| 400+ 集成 | 预建连接器 | 快速设置 |
| 自定义代码 | JavaScript/Python 节点 | 灵活性 |
| Webhooks | 从外部事件触发 | 实时自动化 |

### n8n vs 其他平台

| 功能 | n8n | Zapier | Make |
|------|-----|--------|------|
| 自托管 | 是 | 否 | 否 |
| 开源 | 是 | 否 | 否 |
| 定价 | 免费 / 公平定价 | 按任务计费 | 按操作计费 |
| 自定义代码 | 完整 JS/Python | 有限 | 有限 |
| 学习曲线 | 中等 | 简单 | 中等 |

### 用例

| 类别 | 示例工作流 |
|------|------------|
| 营销 | 社交媒体发布自动化 |
| 销售 | CRM 线索管理 |
| DevOps | 部署通知 |
| 数据 | ETL 管道自动化 |
| 客服 | 工单路由和响应 |

---

## 安装与设置

n8n 可以通过 Docker、npm 或云托管方式安装。

### 安装方式

| 方式 | 命令 | 最适合 |
|------|------|--------|
| Docker | `docker run -it --rm n8nio/n8n` | 生产环境 |
| npm | `npm install n8n -g` | 开发环境 |
| 桌面应用 | 从 n8n.io 下载 | 个人使用 |
| 云 | n8n.cloud | 托管服务 |

### Docker 安装

```bash
# Basic Docker run
docker run -it --rm \
  --name n8n \
  -p 5678:5678 \
  -v n8n_data:/home/node/.n8n \
  n8nio/n8n

# Docker Compose
version: '3'
services:
  n8n:
    image: n8nio/n8n
    ports:
      - "5678:5678"
    volumes:
      - n8n_data:/home/node/.n8n
    environment:
      - N8N_BASIC_AUTH_ACTIVE=true
      - N8N_BASIC_AUTH_USER=admin
      - N8N_BASIC_AUTH_PASSWORD=secure_password
volumes:
  n8n_data:
```

### 系统要求

| 组件 | 最低 | 推荐 |
|------|------|------|
| CPU | 1 核 | 2+ 核 |
| 内存 | 2GB | 4GB+ |
| 磁盘 | 10GB | 50GB+ |
| Node.js | v18 | v20 LTS |

### 初始配置

| 设置 | 位置 | 用途 |
|------|------|------|
| 基础 URL | N8N_HOST | 服务器地址 |
| 端口 | N8N_PORT | 访问端口 |
| 数据库 | DB_TYPE | SQLite 或 PostgreSQL |
| 加密 | N8N_ENCRYPTION_KEY | 数据加密 |
| 时区 | GENERIC_TIMEZONE | 调度准确性 |

---

## 核心概念

理解 n8n 核心概念有助于构建有效的工作流。

### 工作流组件

| 组件 | 描述 | 示例 |
|------|------|------|
| 节点 | 单个操作或触发器 | 发送邮件、HTTP 请求 |
| 连接 | 节点间的数据流 | 节点之间的连线 |
| 工作流 | 完整的自动化流程 | 多步骤过程 |
| 执行 | 单次工作流运行 | 一次触发的实例 |

### 节点类型

| 类型 | 用途 | 示例 |
|------|------|------|
| 触发器 | 启动工作流 | Webhook、定时、邮件 |
| 操作 | 执行操作 | HTTP 请求、数据库、邮件 |
| 转换 | 修改数据 | Set、Merge、Split |
| 流程 | 控制逻辑 | IF、Switch、Loop |

### 数据结构

```json
{
  "json": {
    "key": "value",
    "nested": {
      "data": "here"
    }
  },
  "binary": {
    "data": "base64_encoded"
  }
}
```

### 执行模式

| 模式 | 描述 | 用途 |
|------|------|------|
| 手动 | 点击运行 | 测试 |
| 触发 | 自动 | 生产环境 |
| Webhook | HTTP 请求 | API 集成 |
| 定时 | 基于时间 | 定期任务 |

---

## 构建工作流

创建有效自动化工作流的分步指南。

### 工作流设计流程

| 步骤 | 操作 | 考虑因素 |
|------|------|----------|
| 1 | 定义目标 | 明确目标 |
| 2 | 确定触发器 | 何时启动 |
| 3 | 规划步骤 | 逻辑流程 |
| 4 | 添加节点 | 实施操作 |
| 5 | 测试工作流 | 验证行为 |
| 6 | 部署 | 激活用于生产 |

### 常见工作流模式

| 模式 | 描述 | 示例 |
|------|------|------|
| 线性 | 顺序步骤 | 获取 → 转换 → 存储 |
| 分支 | 条件路径 | IF → 发送 A 或 B |
| 循环 | 重复操作 | 处理列表项 |
| 错误路径 | 处理失败 | Try → Catch → 通知 |

### 节点配置

| 参数 | 描述 | 示例 |
|------|------|------|
| 名称 | 节点标识符 | "发送邮件" |
| 操作 | 要执行的操作 | 创建、读取、更新 |
| 凭据 | 认证 | API 密钥、OAuth |
| 参数 | 操作设置 | URL、body、headers |

### 表达式语法

```
// Access previous node data
{{ $json.fieldName }}

// Access specific node
{{ $('Node Name').item.json.field }}

// Transform data
{{ $json.items.length }}

// Date operations
{{ $now.format('yyyy-MM-dd') }}
```

---

## 常用集成

n8n 支持与数百种流行服务的集成。

### 通信服务

| 服务 | 操作 | 常见用途 |
|------|------|----------|
| Slack | 发送消息、创建频道 | 团队通知 |
| Email (SMTP) | 发送、接收 | 邮件自动化 |
| Telegram | 发送消息、文件 | 机器人交互 |
| Discord | 发送消息、管理服务器 | 社区管理 |

### 云存储

| 服务 | 操作 | 常见用途 |
|------|------|----------|
| Google Drive | 上传、下载、分享 | 文件管理 |
| Dropbox | 上传、下载 | 备份 |
| S3 | 上传、下载、列出 | 对象存储 |
| OneDrive | 上传、下载 | Microsoft 生态 |

### 数据库

| 数据库 | 操作 | 常见用途 |
|--------|------|----------|
| PostgreSQL | 查询、插入、更新 | 数据存储 |
| MySQL | 查询、插入、更新 | Web 应用 |
| MongoDB | 查询、插入、更新 | 文档存储 |
| Airtable | CRUD 操作 | 无代码数据库 |

### 开发工具

| 服务 | 操作 | 常见用途 |
|------|------|----------|
| GitHub | Issues、PRs、webhooks | DevOps 自动化 |
| GitLab | Issues、MRs、pipelines | CI/CD 集成 |
| Jira | Issues、transitions | 项目管理 |
| Notion | Pages、databases | 文档 |

### 示例：Slack 通知工作流

| 节点 | 类型 | 配置 |
|------|------|------|
| Webhook | 触发器 | POST 端点 |
| IF | 条件 | 检查数据有效性 |
| Slack | 操作 | 发送到频道 |
| Respond | 响应 | 返回状态 |

---

## 高级功能

n8n 高级功能用于复杂自动化场景。

### 子工作流

| 功能 | 描述 | 用途 |
|------|------|------|
| 执行工作流 | 调用另一个工作流 | 可复用组件 |
| 错误工作流 | 单独处理错误 | 集中错误处理 |
| Wait | 暂停执行 | 长时间运行的过程 |

### 代码节点

| 节点 | 语言 | 用途 |
|------|------|------|
| Code | JavaScript | 复杂转换 |
| Python | Python | 数据处理 |
| Function | JavaScript | 快速操作 |

### 代码节点示例

```javascript
// JavaScript Code Node
const items = $input.all();
const results = [];

for (const item of items) {
  results.push({
    json: {
      ...item.json,
      processed: true,
      timestamp: new Date().toISOString()
    }
  });
}

return results;
```

### 数据合并

| 策略 | 描述 | 用途 |
|------|------|------|
| 追加 | 合并所有项 | 简单合并 |
| 按位置合并 | 按索引匹配 | 并行流 |
| 按字段合并 | 按值匹配 | 关联数据 |

### Webhook 配置

| 设置 | 描述 | 示例 |
|------|------|------|
| HTTP 方法 | GET、POST、PUT、DELETE | POST |
| 路径 | URL 端点 | /webhook/my-workflow |
| 认证 | 安全方式 | Header 认证 |
| 响应 | 返回数据 | JSON 响应 |

---

## 错误处理

健壮的错误处理确保工作流在出现故障时继续运行。

### 错误处理策略

| 策略 | 实施方式 | 用途 |
|------|----------|------|
| 失败时继续 | 节点设置 | 非关键操作 |
| 错误工作流 | 独立错误处理器 | 集中处理 |
| Try-Catch | IF 节点检查 | 条件恢复 |
| 重试 | 自动重试 | 临时故障 |

### 错误工作流设置

| 步骤 | 操作 | 配置 |
|------|------|------|
| 1 | 创建错误工作流 | 新工作流 |
| 2 | 添加错误触发器 | 捕获错误 |
| 3 | 添加通知 | 告警团队 |
| 4 | 设置为错误处理器 | 主工作流设置 |

### 常见错误类型

| 错误 | 原因 | 解决方案 |
|------|------|----------|
| 连接被拒 | 服务不可用 | 检查服务状态 |
| 超时 | 响应太慢 | 增加超时时间 |
| 认证 | 凭据无效 | 刷新令牌 |
| 频率限制 | 请求过多 | 添加延迟 |

### 日志与监控

| 工具 | 用途 | 设置 |
|------|------|------|
| 执行历史 | 追踪运行 | 内置 |
| 调试模式 | 详细输出 | 节点设置 |
| 外部日志 | 集中日志 | Sentry、LogRocket |

---

## 部署与扩展

n8n 的生产部署考虑因素。

### 部署选项

| 选项 | 优点 | 缺点 |
|------|------|------|
| Docker | 简单、隔离 | 需要 Docker 知识 |
| Kubernetes | 可扩展 | 复杂设置 |
| PM2 | 简单、进程管理 | 单服务器 |
| 云 (n8n.cloud) | 托管 | 成本较高 |

### 性能优化

| 因素 | 影响 | 优化方式 |
|------|------|----------|
| 数据库 | 存储速度 | 使用 PostgreSQL |
| 并发 | 并行执行 | Worker 进程 |
| 内存 | 工作流复杂度 | 增加限制 |
| 网络 | API 调用 | 连接池 |

### 扩展配置

```yaml
# Docker Compose with scaling
services:
  n8n:
    image: n8nio/n8n
    deploy:
      replicas: 3
    environment:
      - EXECUTIONS_MODE=queue
      - QUEUE_BULL_REDIS_HOST=redis
  redis:
    image: redis:alpine
```

### 备份策略

| 组件 | 方法 | 频率 |
|------|------|------|
| 工作流 | 导出 JSON | 每天 |
| 凭据 | 加密备份 | 每天 |
| 数据库 | pg_dump | 每天 |
| 文件 | 卷备份 | 每天 |

### 安全清单

| 实践 | 实施方式 | 优先级 |
|------|----------|--------|
| HTTPS | SSL 证书 | 关键 |
| 认证 | 基础认证或 SSO | 关键 |
| 网络 | 防火墙规则 | 高 |
| 凭据 | 加密存储 | 高 |
| 更新 | 定期更新 | 中等 |

---

## 总结

| 主题 | 核心要点 |
|------|----------|
| 安装 | 生产环境推荐 Docker |
| 概念 | 节点、连接和工作流 |
| 构建 | 先设计再实施 |
| 集成 | 400+ 服务可用 |
| 错误 | 实施适当的错误处理 |
| 扩展 | 生产环境使用 PostgreSQL 和 Redis |
