# 使用 Huginn 进行任务自动化

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
