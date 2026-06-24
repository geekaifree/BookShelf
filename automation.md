# 自动化工具

> 本文档整合了以下源文件：workflow.md, automate.md, node.md, builder.md, app.md

---

## 来源：workflow.md

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


---

## 来源：automate.md

## 简介

Huginn 是一个用于构建在线自动化任务代理的开源系统。它创建能够监控事件、处理数据并根据定义条件触发操作的代理。本教程涵盖安装、代理配置、事件处理和常见自动化工作流。

## 架构概览

| 组件 | 描述 | 角色 |
|------|------|------|
| Agents | 处理单元 | 接收、处理和发送事件 |
| Events | 数据负载 | 作为消息在代理间流动 |
| Scenarios | 代理组 | 组织相关代理 |
| Web UI | 管理界面 | 配置和监控代理 |

## 安装

### Docker Compose 设置

```yaml
version: "3.8"
services:
  huginn:
    image: ghcr.io/huginn/huginn:latest
    container_name: huginn
    ports:
      - "3000:3000"
    environment:
      - DATABASE_ADAPTER=mysql2
      - DATABASE_HOST=db
      - DATABASE_NAME=huginn
      - DATABASE_USERNAME=huginn
      - DATABASE_PASSWORD=changeme
      - HUGINN_INVITATION_CODE=join-huginn
    depends_on:
      - db

  db:
    image: mysql:8.0
    volumes:
      - mysql_data:/var/lib/mysql
    environment:
      - MYSQL_ROOT_PASSWORD=rootpassword
      - MYSQL_DATABASE=huginn
      - MYSQL_USER=huginn
      - MYSQL_PASSWORD=changeme

volumes:
  mysql_data:
```

### 初始设置

1. 访问 `http://localhost:3000`
2. 使用邀请码注册
3. 完成设置向导
4. 导航到 Agents 部分

## 代理类型

Huginn 提供多种内置代理类型：

### 数据源

| 代理 | 用途 | 输出 |
|------|------|------|
| Website Agent | 抓取网页 | 提取的内容 |
| RSS Agent | 监控 RSS/Atom 订阅 | 订阅条目 |
| Weather Agent | 获取天气数据 | 天气状况 |
| Post Agent | 发送 HTTP 请求 | 响应数据 |
| Twilio Agent | 短信交互 | 消息数据 |
| Email Agent | 接收邮件 | 邮件内容 |

### 数据处理器

| 代理 | 用途 | 输入/输出 |
|------|------|-----------|
| Trigger Agent | 过滤事件 | 条件转发 |
| JavaScript Agent | 自定义逻辑 | 编程处理 |
| Event Formatting Agent | 转换数据 | 格式化事件 |
| DeDuplication Agent | 去重 | 唯一事件 |
| Digest Agent | 聚合事件 | 汇总数据 |
| Email Digest Agent | 邮件摘要 | 邮件通知 |

### 动作

| 代理 | 用途 | 动作 |
|------|------|------|
| Send Email Agent | 发送邮件 | 邮件投递 |
| Webhook Agent | 调用 Webhook | HTTP 请求 |
| Shell Command Agent | 运行命令 | 系统执行 |
| Slack Agent | 发送到 Slack | 频道消息 |
| Data Output Agent | API 端点 | 通过 HTTP 提供数据 |

## 创建代理

### 代理配置字段

| 字段 | 描述 | 必填 |
|------|------|------|
| Name | 代理标识符 | 是 |
| Type | 代理类 | 是 |
| Schedule | 运行频率 | 取决于类型 |
| Sources | 输入代理 | 取决于类型 |
| Options | 类型特定配置 | 是 |
| Keep Events | 事件保留 | 建议 |

### Website Agent 示例

配置网页抓取代理：

```json
{
  "expected_update_period_in_days": "1",
  "url": "https://example.com/news",
  "type": "html",
  "mode": "on_change",
  "extract": {
    "title": {
      "css": "h2.article-title",
      "value": "string(.)"
    },
    "link": {
      "css": "h2.article-title a",
      "value": "@href"
    },
    "summary": {
      "css": "p.article-summary",
      "value": "string(.)"
    }
  }
}
```

### 提取配置

| 字段 | 描述 | 示例 |
|------|------|------|
| css | CSS 选择器 | `h2.title`, `div.content > p` |
| value | XPath 表达式 | `string(.)`, `@href`, `@src` |
| hidden | 是否包含在输出中 | `true` 或 `false` |

## 事件流

### 事件如何移动

```
Source Agent -> Event -> Processing Agent -> Event -> Action Agent
```

### 事件结构

| 字段 | 描述 | 自动填充 |
|------|------|----------|
| payload | 事件数据 | 用户定义 |
| agent | 来源代理 | 是 |
| created_at | 时间戳 | 是 |
| expires_at | 删除时间 | 基于保留策略 |

### 链接代理

1. 打开目标代理配置
2. 在 Sources 字段中选择源代理
3. 保存配置
4. 源代理的事件现在流向目标

## 调度选项

| 调度 | 描述 | 使用场景 |
|------|------|----------|
| Every X minutes | 固定间隔 | 频繁检查 |
| Every X hours | 小时间隔 | 周期任务 |
| Every X days | 天间隔 | 每日报告 |
| Cron expression | 自定义调度 | 复杂时间安排 |
| Never | 仅手动 | 触发式代理 |
| Every midnight | 每天 00:00 | 每日汇总 |

### Cron 示例

| 表达式 | 调度 |
|--------|------|
| `0 9 * * 1-5` | 工作日上午 9 点 |
| `0 */2 * * *` | 每 2 小时 |
| `0 0 1 * *` | 每月 1 号 |
| `30 18 * * 5` | 每周五下午 6:30 |

## JavaScript 代理

编写自定义处理逻辑：

```javascript
Agent.receive = function() {
  var events = this.incomingEvents();
  var self = this;

  events.forEach(function(event) {
    var data = event.payload;

    // Process data
    var result = {
      title: data.title.toUpperCase(),
      word_count: data.content.split(/\s+/).length,
      processed_at: new Date().toISOString()
    };

    // Create output event
    self.createEvent({ payload: result });
  });
};
```

### JavaScript 代理 API

| 方法 | 描述 | 返回值 |
|------|------|--------|
| `this.incomingEvents()` | 获取源事件 | Array |
| `this.createEvent(payload)` | 发送新事件 | Event |
| `this.memory(key)` | 从内存读取 | Value |
| `this.setMemory(key, value)` | 写入内存 | void |
| `this.log(message)` | 写入日志 | void |
| `this.error(message)` | 记录错误 | void |

## Trigger 代理

根据条件过滤事件：

```json
{
  "expected_receive_period_in_days": "1",
  "rules": {
    "type": "and",
    "conditions": [
      {
        "path": "title",
        "type": "regex",
        "value": "important|urgent"
      },
      {
        "path": "priority",
        "type": "field>",
        "value": "5"
      }
    ]
  },
  "message": "Matched: {{title}}"
}
```

### 条件类型

| 类型 | 描述 | 示例 |
|------|------|------|
| regex | 正则匹配 | `"value": "pattern"` |
| field> | 大于 | `"value": "100"` |
| field< | 小于 | `"value": "50"` |
| field>= | 大于等于 | `"value": "10"` |
| field<= | 小于等于 | `"value": "100"` |
| not_regex | 不匹配正则 | `"value": "spam"` |

## Event Formatting 代理

使用 Liquid 模板转换事件数据：

```json
{
  "expected_receive_period_in_days": "1",
  "instructions": {
    "message": "New article: {{title}} ({{word_count}} words)",
    "url": "{{link}}",
    "summary": "{{summary | truncate: 200}}",
    "formatted_date": "{{created_at | date: '%B %d, %Y'}}"
  },
  "mode": "merge"
}
```

### Liquid 模板过滤器

| 过滤器 | 描述 | 示例 |
|--------|------|------|
| `truncate` | 限制文本长度 | `{{text | truncate: 100}}` |
| `date` | 格式化日期 | `{{date | date: '%Y-%m-%d'}}` |
| `upcase` | 大写 | `{{text | upcase}}` |
| `downcase` | 小写 | `{{text | downcase}}` |
| `strip` | 去除空白 | `{{text | strip}}` |
| `replace` | 查找替换 | `{{text | replace: 'old', 'new'}}` |
| `split` | 分割字符串 | `{{csv | split: ','}}` |

## 常见自动化工作流

### 新闻监控

| 代理 | 类型 | 用途 |
|------|------|------|
| 1 | RSS Agent | 监控新闻订阅 |
| 2 | Trigger Agent | 按关键词过滤 |
| 3 | Event Formatting | 格式化显示 |
| 4 | Digest Agent | 每日摘要 |
| 5 | Send Email Agent | 投递摘要 |

### 价格追踪

| 代理 | 类型 | 用途 |
|------|------|------|
| 1 | Website Agent | 抓取产品页面 |
| 2 | Trigger Agent | 价格低于阈值 |
| 3 | Send Email Agent | 告警通知 |
| 4 | DeDuplication | 防止重复告警 |

### 网站监控

| 代理 | 类型 | 用途 |
|------|------|------|
| 1 | Website Agent | 检查页面状态 |
| 2 | Trigger Agent | 状态已变化 |
| 3 | JavaScript Agent | 与之前比较 |
| 4 | Slack Agent | 发布告警 |

### 社交媒体聚合

| 代理 | 类型 | 用途 |
|------|------|------|
| 1 | RSS Agent | 订阅源 1 |
| 2 | RSS Agent | 订阅源 2 |
| 3 | RSS Agent | 订阅源 3 |
| 4 | DeDuplication | 去重 |
| 5 | Event Formatting | 统一格式 |
| 6 | Digest Agent | 每周摘要 |
| 7 | Webhook Agent | 发布到博客 |

## 场景

场景将相关代理分组以便组织和分享：

| 功能 | 描述 |
|------|------|
| 分组 | 逻辑组织代理 |
| 分享 | 导出和导入场景 |
| 文档 | 为分组添加描述 |
| 可视化布局 | 在 UI 中排列代理 |

## Webhook 和 API

### 传入 Webhook

创建 Webhook 代理接收外部数据：

```json
{
  "secret": "your-webhook-secret",
  "expected_receive_period_in_days": 1
}
```

Webhook URL: `http://your-huginn:3000/users/1/web_requests/AGENT_ID?secret=your-webhook-secret`

### Data Output 代理

将事件暴露为 API：

```json
{
  "secrets": ["api-key-123"],
  "expected_receive_period_in_days": 1
}
```

API URL: `http://your-huginn:3000/users/1/web_requests/AGENT_ID?secret=api-key-123`

## 性能和维护

### 事件保留

| 设置 | 建议 |
|------|------|
| 关键代理 | 保留 500+ 事件 |
| 监控代理 | 保留 50-100 事件 |
| 高频代理 | 保留 10-20 事件 |
| 临时代理 | 保留 5-10 事件 |

### 系统资源

| 用户 | 代理 | CPU | RAM | 数据库 |
|------|------|-----|-----|--------|
| 1-5 | 10-50 | 1 核 | 1 GB | SQLite |
| 5-20 | 50-200 | 2 核 | 2 GB | MySQL/PostgreSQL |
| 20+ | 200+ | 4 核 | 4 GB | PostgreSQL |

## 故障排除

| 问题 | 可能原因 | 解决方案 |
|------|----------|----------|
| 代理未运行 | 调度设为 Never | 设置调度 |
| 无事件产生 | CSS 选择器错误 | 检查页面结构 |
| 内存错误 | 事件负载过大 | 减少数据量 |


---

## 来源：node.md

## 目录

1. [Node-RED 简介](#introduction)
2. [安装与设置](#installation)
3. [核心概念](#core-concepts)
4. [构建流程](#building-flows)
5. [常用节点](#common-nodes)
6. [IoT 协议](#protocols)
7. [仪表板与 UI](#dashboard)
8. [部署与安全](#deployment)

---

## 简介

Node-RED 是一个基于流程的编程工具，用于将硬件设备、API 和在线服务连接在一起。它提供基于浏览器的编辑器，可可视化构建自动化工作流。

### Node-RED 核心功能

| 功能 | 描述 | 好处 |
|------|------|------|
| 可视化编辑器 | 拖拽式流程构建 | 易于学习 |
| 基于浏览器 | 无需客户端安装 | 随处访问 |
| 可扩展 | 数千个节点 | 连接一切 |
| 轻量级 | 可运行在树莓派 | IoT 就绪 |
| JSON 流程 | 可移植配置 | 易于备份 |

### Node-RED vs 其他工具

| 功能 | Node-RED | Home Assistant | n8n |
|------|----------|----------------|-----|
| 重点 | IoT/自动化 | 家庭自动化 | 工作流 |
| 学习曲线 | 低 | 中等 | 低 |
| 可视化编辑器 | 是 | 有限 | 是 |
| 可扩展性 | 高 | 高 | 高 |
| 资源使用 | 极低 | 中等 | 中等 |

### 常见用例

| 类别 | 示例 |
|------|------|
| 家庭自动化 | 灯光控制、恒温器 |
| IoT 传感器 | 温度、湿度监控 |
| API 集成 | Webhook 处理 |
| 数据处理 | ETL 管道 |
| 消息 | 聊天机器人、通知 |

---

## 安装与设置

Node-RED 可以安装在各种平台上。

### 安装方式

| 平台 | 方式 | 命令 |
|------|------|------|
| npm (全局) | npm | `npm install -g node-red` |
| Docker | Docker | `docker run -p 1880:1880 nodered/node-red` |
| Raspberry Pi | 脚本 | `bash <(curl -sL https://raw.githubusercontent.com/node-red/linux-installers/master/deb/update-nodejs-and-nodered)` |
| Snap | Snap | `sudo snap install node-red` |

### Docker 安装

```yaml
# docker-compose.yml
version: '3'
services:
  node-red:
    image: nodered/node-red:latest
    ports:
      - "1880:1880"
    volumes:
      - node-red-data:/data
    environment:
      - TZ=UTC

volumes:
  node-red-data:
```

### 系统要求

| 组件 | 最低 | 推荐 |
|------|------|------|
| CPU | 1 核 | 2 核 |
| 内存 | 256MB | 1GB |
| 存储 | 100MB | 1GB |
| Node.js | v14 | v18 LTS |

### 首次访问

| 步骤 | 操作 | URL |
|------|------|-----|
| 1 | 启动 Node-RED | `node-red` |
| 2 | 打开浏览器 | http://localhost:1880 |
| 3 | 访问编辑器 | 可视化流程编辑器 |
| 4 | 创建第一个流程 | 拖拽节点 |

---

## 核心概念

理解 Node-RED 基础以有效构建流程。

### 流程组件

| 组件 | 描述 | 示例 |
|------|------|------|
| 节点 | 单个功能 | HTTP 请求、开关 |
| 连线 | 节点间的连接 | 数据流路径 |
| 流程 | 节点集合 | 完整工作流 |
| Tab | 流程组织 | 分离关注点 |

### 消息结构

```json
{
  "payload": "Main data",
  "topic": "Message topic",
  "_msgid": "Unique ID",
  "custom": "Any additional data"
}
```

### 节点属性

| 属性 | 描述 | 示例 |
|------|------|------|
| 名称 | 显示名称 | "获取天气" |
| 类型 | 节点功能 | http request |
| 配置 | 节点设置 | URL、方法 |
| 连线 | 输出连接 | 下一个节点 |

### 流程生命周期

| 事件 | 触发 | 操作 |
|------|------|------|
| 部署 | 保存变更 | 流程重启 |
| 启动 | Node-RED 启动 | 流程初始化 |
| 停止 | Node-RED 停止 | 清理 |
| 消息 | 接收输入 | 处理数据 |

---

## 构建流程

创建自动化流程的分步指南。

### 流程设计流程

| 步骤 | 操作 | 考虑因素 |
|------|------|----------|
| 1 | 定义目标 | 自动化什么 |
| 2 | 确定触发器 | 何时启动 |
| 3 | 添加处理 | 转换数据 |
| 4 | 添加输出 | 发送到哪里 |
| 5 | 测试 | 验证行为 |
| 6 | 部署 | 激活流程 |

### 基本流程模式

```
[触发] → [处理] → [输出]

Example:
[Inject] → [Function] → [Debug]
```

### 常见流程模式

| 模式 | 描述 | 使用的节点 |
|------|------|------------|
| 线性 | 顺序处理 | Inject → Function → Debug |
| 分支 | 条件逻辑 | Switch → 多个输出 |
| 合并 | 合并输入 | 多个 → Join |
| 循环 | 重复操作 | Function 带计数器 |

### 节点配置

| 步骤 | 操作 | 备注 |
|------|------|------|
| 1 | 拖拽节点 | 从调色板 |
| 2 | 双击 | 打开设置 |
| 3 | 配置 | 设置属性 |
| 4 | 连线 | 连接到其他节点 |
| 5 | 部署 | 应用变更 |

### 调试流程

| 工具 | 描述 | 用途 |
|------|------|------|
| Debug 节点 | 输出到侧边栏 | 查看消息 |
| Status 节点 | 节点状态 | 监控健康 |
| Catch 节点 | 错误处理 | 处理失败 |
| Complete 节点 | 流程完成 | 后处理 |

---

## 常用节点

构建 Node-RED 流程的必备节点。

### 输入节点

| 节点 | 用途 | 配置 |
|------|------|------|
| Inject | 手动/定时触发 | 间隔、payload |
| HTTP Request | API 调用 | URL、方法 |
| MQTT In | MQTT 消息 | Broker、topic |
| WebSocket | 实时数据 | URL、events |

### 处理节点

| 节点 | 用途 | 用例 |
|------|------|------|
| Function | 自定义 JavaScript | 复杂逻辑 |
| Switch | 条件路由 | If/else |
| Change | 修改消息 | 转换数据 |
| JSON | 解析/序列化 | 数据转换 |
| Delay | 速率限制 | 节流消息 |

### 输出节点

| 节点 | 用途 | 配置 |
|------|------|------|
| Debug | 在侧边栏查看 | 显示选项 |
| HTTP Response | API 响应 | 状态、headers |
| MQTT Out | 发布 MQTT | Broker、topic |
| Email | 发送邮件 | SMTP 设置 |
| File | 写入文件 | 路径、格式 |

### 存储节点

| 节点 | 用途 | 存储类型 |
|------|------|----------|
| File | 读写文件 | 本地文件系统 |
| SQLite | 数据库操作 | SQLite 数据库 |
| Context | 内存存储 | Flow/全局上下文 |
| Redis | 缓存/存储 | Redis 数据库 |

### Function 节点示例

```javascript
// Transform payload
msg.payload = msg.payload.toUpperCase();
return msg;

// Conditional logic
if (msg.payload > 100) {
  return [msg, null]; // First output
} else {
  return [null, msg]; // Second output
}

// Create new message
return {
  payload: {
    temperature: msg.payload,
    timestamp: Date.now()
  }
};
```

---

## IoT 协议

Node-RED 支持各种 IoT 通信协议。

### MQTT

| 设置 | 描述 | 示例 |
|------|------|------|
| Broker | MQTT 服务器 | mqtt://localhost |
| Port | 连接端口 | 1883 |
| Topic | 消息频道 | home/temperature |
| QoS | 服务质量 | 0, 1, 或 2 |

### MQTT 配置

| 属性 | 选项 | 推荐 |
|------|------|------|
| Clean session | True/False | 新连接用 True |
| Keepalive | 秒 | 60 |
| Username | 凭据 | 如需要 |
| Password | 凭据 | 如需要 |

### HTTP/REST

| 方法 | 用途 | 节点 |
|------|------|------|
| GET | 获取数据 | HTTP Request |
| POST | 创建数据 | HTTP Request |
| PUT | 更新数据 | HTTP Request |
| DELETE | 删除数据 | HTTP Request |

### WebSocket

| 模式 | 描述 | 用途 |
|------|------|------|
| Listener | 接受连接 | 服务器 |
| Client | 连接到服务器 | 客户端 |
| 双向 | 双向通信 | 实时 |

### CoAP

| 功能 | 描述 | 用途 |
|------|------|------|
| 轻量级 | 基于 UDP | 受限设备 |
| RESTful | 类似 HTTP | IoT 传感器 |
| Observe | 订阅变更 | 实时更新 |

### 协议对比

| 协议 | 传输 | 开销 | 用途 |
|------|------|------|------|
| MQTT | TCP | 低 | IoT 消息 |
| HTTP | TCP | 中等 | API 集成 |
| WebSocket | TCP | 低 | 实时 Web |
| CoAP | UDP | 极低 | 受限设备 |

---

## 仪表板与 UI

创建用于监控和控制的可视化仪表板。

### 仪表板安装

```bash
# Install dashboard nodes
cd ~/.node-red
npm install node-red-dashboard
```

### 仪表板组件

| 组件 | 用途 | 示例 |
|------|------|------|
| Chart | 数据可视化 | 温度图表 |
| Gauge | 单个值 | 速度计 |
| Switch | 开关控制 | 灯光开/关 |
| Slider | 值输入 | 亮度控制 |
| Text | 显示值 | 状态消息 |

### 仪表板布局

| 元素 | 描述 | 配置 |
|------|------|------|
| Tab | 页面 | 多个标签页 |
| Group | 区域 | 组织组件 |
| Widget | 单个 UI | 大小、位置 |

### 创建仪表板

| 步骤 | 操作 | 结果 |
|------|------|------|
| 1 | 添加标签页 | 仪表板页面 |
| 2 | 添加分组 | 区域 |
| 3 | 添加组件 | UI 元素 |
| 4 | 连接数据 | 连接到流程 |
| 5 | 访问 | http://localhost:1880/ui |

### 仪表板组件

| 组件 | 输入 | 显示 |
|------|------|------|
| Chart | 时间序列 | 折线/柱状图 |
| Gauge | 数字 | 表盘显示 |
| Switch | 布尔 | 切换按钮 |
| Slider | 数字 | 范围输入 |
| Text | 字符串 | 文本显示 |
| Button | 点击 | 操作触发 |

### 样式选项

| 属性 | 选项 | 效果 |
|------|------|------|
| 颜色 | 主题色 | 组件颜色 |
| 大小 | 小、中、大 | 组件大小 |
| 标签 | 自定义文本 | 显示名称 |
| 图标 | Material 图标 | 可视指示器 |

---

## 部署与安全部署

在生产环境中安全部署 Node-RED。

### 部署选项

| 选项 | 优点 | 缺点 |
|------|------|------|
| 本地 | 简单 | 访问受限 |
| Docker | 隔离 | 需要 Docker 知识 |
| 云 | 可扩展 | 成本 |
| Raspberry Pi | 低功耗 | 资源有限 |

### 安全配置

| 设置 | 默认值 | 推荐 |
|------|--------|------|
| 认证 | 无 | 启用 |
| HTTPS | 否 | 启用 |
| API 安全 | 无 | 基于 Token |
| 流程保护 | 无 | 用户只读 |

### 启用认证

```javascript
// settings.js
module.exports = {
  adminAuth: {
    type: "credentials",
    users: [{
      username: "admin",
      password: "$2b$08$...",
      permissions: "*"
    }]
  }
};
```

### HTTPS 配置

```javascript
// settings.js
module.exports = {
  https: {
    key: fs.readFileSync('key.pem'),
    cert: fs.readFileSync('cert.pem')
  },
  requireHttps: true
};
```

### 备份与恢复

| 方式 | 命令 | 频率 |
|------|------|------|
| 导出流程 | 编辑器 → 导出 | 变更前 |
| 导入流程 | 编辑器 → 导入 | 恢复 |
| 文件备份 | 复制 .node-red | 每周 |
| Git | 版本控制 | 持续 |

### 性能优化

| 方面 | 操作 | 效果 |
|------|------|------|
| 内存 | 增加 Node.js 堆 | 处理更多流程 |
| 上下文 | 限制存储大小 | 防止内存泄漏 |
| 日志 | 降低详细度 | 减少 I/O |
| 节点 | 禁用未使用 | 降低 CPU |

### 监控

| 指标 | 工具 | 阈值 |
|------|------|------|
| CPU | 系统工具 | < 80% |
| 内存 | 系统工具 | < 80% |
| 消息 | Debug 节点 | 监控速率 |
| 错误 | Catch 节点 | 理想为零 |

---

## 总结

| 主题 | 核心要点 |
|------|----------|
| 安装 | Docker 简化部署 |
| 概念 | 节点、连线、流程、消息 |
| 构建 | 可视化编辑器创建流程 |
| 协议 | 支持 MQTT、HTTP、WebSocket |
| 仪表板 | 内置可视化 |
| 安全 | 启用认证和 HTTPS |


---

## 来源：builder.md

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


---

## 来源：app.md

## 简介

Appsmith 是一个开源平台，用于构建内部应用程序，如管理面板、仪表板和 CRUD 工具。它连接数据库和 API，提供拖拽式 UI 构建器，并支持 JavaScript 自定义逻辑。本教程涵盖核心概念和实际工作流程。

## 架构概览

| 层级 | 描述 | 主要特性 |
|------|------|----------|
| 前端 | 带有组件画布的可视化编辑器 | 拖拽、实时预览 |
| 后端 | 连接外部数据源 | REST、GraphQL、数据库连接器 |
| 部署 | 自托管或云端 | Docker、Kubernetes、Appsmith Cloud |
| 状态 | 应用内数据管理 | 组件状态、操作、JS 对象 |

## 安装

### Docker 部署

```bash
docker run -d --name appsmith \
  -p 80:80 \
  -v "$PWD/stacks:/appsmith-stacks" \
  appsmith/appsmith-ce
```

### Docker Compose

```yaml
version: "3"
services:
  appsmith:
    image: appsmith/appsmith-ce
    ports:
      - "80:80"
    volumes:
      - ./stacks:/appsmith-stacks
    restart: unless-stopped
```

## 核心概念

### 数据源

Appsmith 连接外部服务以读写数据。

| 类别 | 支持的来源 |
|------|-----------|
| SQL 数据库 | PostgreSQL、MySQL、MongoDB、MSSQL |
| 云服务 | Firestore、DynamoDB、S3、Redis |
| API | REST、GraphQL、需要认证的端点 |
| SaaS 工具 | Google Sheets、Twilio、Stripe |

### 组件

组件是放置在画布上的 UI 元素。

| 组件 | 用途 | 常见使用场景 |
|------|------|-------------|
| Table | 显示表格数据 | 列表、记录、搜索结果 |
| Form | 输入收集 | 数据录入、筛选 |
| Chart | 数据可视化 | 仪表板、分析 |
| Button | 触发操作 | 提交、刷新、导航 |
| Input | 文本输入 | 搜索、筛选、表单 |
| Modal | 覆盖层对话框 | 确认、详情视图 |
| Dropdown | 选择 | 筛选、选项 |

### 操作

操作定义用户与组件交互时的行为。

| 操作类型 | 触发方式 | 示例 |
|----------|----------|------|
| API 查询 | 按钮点击 | 获取用户列表 |
| 数据库查询 | 表单提交 | 插入新记录 |
| JS 函数 | 页面加载 | 初始化变量 |
| 导航 | 链接点击 | 切换页面 |

## 构建管理面板

### 步骤 1：连接数据库

1. 导航到数据源面板。
2. 选择 PostgreSQL（或你的数据库）。
3. 输入主机、端口、数据库名称、用户名和密码。
4. 测试连接并保存。

### 步骤 2：创建查询

创建查询以获取、插入、更新和删除记录。

```sql
-- 获取所有用户
SELECT * FROM users ORDER BY created_at DESC;
```

```sql
-- 插入新用户
INSERT INTO users (name, email, role)
VALUES ({{InputName.text}}, {{InputEmail.text}}, {{DropdownRole.selectedOptionValue}});
```

### 步骤 3：构建 UI

1. 将 **Table** 组件拖到画布上。
2. 将表格数据属性绑定到查询：
   ```
   {{FetchUsers.data}}
   ```
3. 在表格上方添加 **Input** 组件用于搜索筛选。
4. 添加 **Button** 以触发插入查询。

### 步骤 4：添加事件处理器

| 组件 | 事件 | 操作 |
|------|------|------|
| Button（添加用户） | onClick | 运行 InsertUser 查询，然后运行 RefreshUsers |
| Table Row | onRowSelected | 导航到详情页 |
| Search Input | onTextChanged | 运行筛选查询 |

## JavaScript 集成

Appsmith 支持在组件属性和查询中使用内联 JavaScript。

### 示例：条件样式

```javascript
// 根据状态更改行颜色
{{ currentRow.status === 'active' ? '#d4edda' : '#f8d7da' }}
```

### 示例：数据转换

```javascript
// 格式化表格列中的货币
{{ "$" + (currentRow.amount / 100).toFixed(2) }}
```

### 示例：自定义 JS 对象

创建 JS 对象以实现可复用的逻辑：

```javascript
export default {
  formatDate: (dateStr) => {
    return new Date(dateStr).toLocaleDateString('en-US', {
      year: 'numeric',
      month: 'short',
      day: 'numeric'
    });
  },
  validateEmail: (email) => {
    return /^[^\s@]+@[^\s@]+\.[^\s@]+$/.test(email);
  }
};
```

## 多页面应用

| 概念 | 描述 |
|------|------|
| 页面 | 一个应用中的独立屏幕 |
| 导航 | 侧边栏或按钮式的页面切换 |
| URL 参数 | 通过查询字符串在页面间传递数据 |
| 全局状态 | 跨页面共享的 JS 对象 |

## 认证和权限

| 功能 | 描述 |
|------|------|
| 应用级认证 | 访问应用需要登录 |
| 基于角色的访问 | 为用户分配角色（Admin、Viewer） |
| 页面权限 | 按角色限制特定页面 |
| 数据源认证 | 查询使用独立凭证 |

## 部署清单

| 任务 | 详情 |
|------|------|
| 配置域名 | 设置反向代理（Nginx、Traefik） |
| 启用 HTTPS | 使用 Let's Encrypt 或证书 |
| 设置环境变量 | APPSMITH_ENCRYPTION_PASSWORD、APPSMITH_ENCRYPTION_SALT |
| 备份 stacks | 定期备份 stacks 卷 |
| 更新镜像 | 拉取新版本并重启容器 |

## 性能优化

| 技术 | 影响 |
|------|------|
| 服务端分页 | 减少大数据表的数据传输 |
| 防抖搜索 | 防止输入时过多的 API 调用 |
| 索引查询 | 加速数据库查找 |
| 组件懒加载 | 加快初始页面渲染 |

## 故障排除

| 问题 | 解决方案 |
|------|----------|
| 查询超时 | 增加超时限制或优化查询 |
| 组件不渲染 | 检查数据绑定语法 |
| 连接被拒绝 | 验证数据库主机和防火墙规则 |
| CORS 错误 | 在 API 服务器上配置允许的来源 |

## 总结

Appsmith 通过将可视化构建器与直接数据源连接相结合，简化了内部工具的构建。该平台支持快速原型设计和生产级管理面板，无需单独的前端代码库。连接数据、拖拽组件、绑定查询并添加 JavaScript 逻辑，即可创建功能完整的应用程序。


---
