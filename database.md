# Baserow：构建无代码数据库

## 简介

Baserow 是一个开源的无代码数据库和 Airtable 替代方案。它提供类似电子表格的界面来创建数据库、定义关系和构建应用程序，无需编写代码。本教程涵盖设置、数据建模、视图和 API 集成。

## 架构

| 组件 | 技术 | 用途 |
|------|------|------|
| 后端 | Django (Python) | API 和业务逻辑 |
| 前端 | Nuxt.js (Vue) | Web 界面 |
| 数据库 | PostgreSQL | 数据存储 |
| 缓存 | Redis | 缓存和实时 |
| 队列 | Celery | 后台任务 |

## 安装

### Docker Compose

```yaml
version: "3"
services:
  baserow:
    image: baserow/baserow:latest
    ports:
      - "80:80"
      - "443:443"
    volumes:
      - baserow_data:/baserow/data
    environment:
      BASEROW_PUBLIC_URL: https://baserow.example.com
      SECRET_KEY: your-secret-key
      DATABASE_PASSWORD: your-db-password
volumes:
  baserow_data:
```

### 云部署

| 提供商 | 方式 | 备注 |
|--------|------|------|
| Baserow.io | 托管 SaaS | 提供免费套餐 |
| DigitalOcean | Droplet | 基于 Docker |
| AWS | EC2/ECS | 自定义部署 |
| Railway | 一键部署 | 简化部署 |

## 核心概念

### 工作区

| 层级 | 描述 |
|------|------|
| Workspace | 团队或项目的顶级容器 |
| Database | 一组相关表 |
| Table | 行和字段的结构化集合 |
| Row | 表中的单条记录 |
| Field | 具有特定类型的列定义 |

### 字段类型

| 类型 | 描述 | 示例 |
|------|------|------|
| Text | 单行或长文本 | 名称、描述 |
| Number | 整数或小数 | 价格、数量 |
| Boolean | 勾选框 | 已激活、已批准 |
| Date | 日期和时间 | 创建日期、截止日期 |
| Single Select | 下拉选项 | 状态、类别 |
| Multi Select | 多个下拉选项 | 标签、技能 |
| Link | 与其他表的关系 | 客户订单 |
| Formula | 计算字段 | 总价 = 单价 * 数量 |
| Lookup | 引用字段值 | 订单客户名称 |
| Rollup | 聚合相关记录 | 订单总额之和 |
| File | 文件附件 | 文档、图片 |
| URL | 网址 | 网站链接 |
| Email | 邮箱地址 | 联系邮箱 |
| Phone | 电话号码 | 联系电话 |
| Rating | 星级评分 | 评价分数 |
| Created On | 自动时间戳 | 记录创建时间 |
| Last Modified | 自动时间戳 | 最后编辑时间 |

## 创建数据库

### 步骤 1：创建工作区

1. 点击侧边栏中的"Create workspace"。
2. 输入工作区名称。
3. 添加具有适当角色的团队成员。

### 步骤 2：创建数据库

1. 在工作区内点击"Add database"。
2. 选择"Start from scratch"或使用模板。
3. 命名数据库（例如"Project Management"）。

### 步骤 3：定义表和字段

创建一个"Tasks"表，包含以下字段：

| 字段名 | 类型 | 配置 |
|--------|------|------|
| Title | Text | 必填 |
| Status | Single Select | To Do、In Progress、Done |
| Priority | Single Select | Low、Medium、High |
| Assignee | Link | 链接到 Team Members 表 |
| Due Date | Date | 包含时间选项 |
| Estimated Hours | Number | 小数格式 |
| Description | Long Text | 启用富文本 |
| Attachments | File | 多文件 |

## 关系

### 链接字段

连接表以建模关系。

| 关系类型 | 配置 | 示例 |
|----------|------|------|
| 一对多 | 在"多"方设置链接字段 | 客户有多个订单 |
| 多对多 | 链接字段启用"允许多个" | 任务分配给多个用户 |
| 自引用 | 链接到同一张表 | 子任务 |

### Lookup 字段

从链接记录中拉取数据。

```
Orders 表：
  - Customer（链接到 Customers 表）
  - Customer Email（Lookup：Customer > Email）
  - Customer Phone（Lookup：Customer > Phone）
```

### Rollup 字段

聚合链接记录中的数据。

| Rollup 函数 | 描述 | 示例 |
|-------------|------|------|
| Count | 计数链接记录 | 订单数量 |
| Sum | 数值求和 | 总收入 |
| Average | 数值平均 | 平均订单价值 |
| Min | 最小值 | 最早订单日期 |
| Max | 最大值 | 最新订单日期 |

## 视图

### 视图类型

| 类型 | 描述 | 最适用于 |
|------|------|----------|
| Grid | 类似电子表格的表格 | 通用数据管理 |
| Gallery | 卡片式布局 | 可视化项目、个人资料 |
| Form | 数据录入表单 | 收集新记录 |
| Kanban | 基于列的看板 | 任务管理、工作流 |
| Calendar | 基于日期的日历 | 日程安排、截止日期 |

### 筛选

根据条件筛选记录。

| 操作符 | 字段类型 | 示例 |
|--------|----------|------|
| Equals | 全部 | Status = "Done" |
| Contains | Text | Title 包含 "urgent" |
| Greater than | Number、Date | Price > 100 |
| Is empty | 全部 | Description 为空 |
| Has all of | Multi Select | Tags 包含全部 "bug, critical" |

### 排序

| 排序 | 方向 | 示例 |
|------|------|------|
| 按字段 | 升序/降序 | 按 Due Date 排序（升序） |
| 多级 | 主要/次要 | 先按 Priority 排序，再按 Due Date |

### 分组

按字段值分组记录。

```
按 Status 分组：
  To Do（5 条记录）
    - Task 1
    - Task 2
  In Progress（3 条记录）
    - Task 3
    - Task 4
  Done（8 条记录）
    - Task 5
```

## 公式

Baserow 支持类似电子表格语法的公式字段。

### 常用公式

| 公式 | 描述 | 示例 |
|------|------|------|
| `field('Name')` | 引用字段 | `field('First') + ' ' + field('Last')` |
| `if(condition, true, false)` | 条件判断 | `if(field('Age') >= 18, 'Adult', 'Minor')` |
| `concat(text, ...)` | 拼接文本 | `concat('#', field('ID'))` |
| `length(text)` | 字符串长度 | `length(field('Name'))` |
| `round(number, decimals)` | 四舍五入 | `round(field('Price'), 2)` |
| `days(date1, date2)` | 日期间隔天数 | `days(field('Start'), field('End'))` |

## API 访问

### 认证

```bash
# 在 Settings > API Tokens 中创建 token
# 在请求中使用 token
curl -H "Authorization: Token YOUR_TOKEN" \
  https://baserow.example.com/api/database/rows/table/1/
```

### CRUD 操作

| 操作 | 方法 | 端点 |
|------|------|------|
| 列出行 | GET | `/api/database/rows/table/{id}/` |
| 创建行 | POST | `/api/database/rows/table/{id}/` |
| 获取行 | GET | `/api/database/rows/table/{id}/{row_id}/` |
| 更新行 | PATCH | `/api/database/rows/table/{id}/{row_id}/` |
| 删除行 | DELETE | `/api/database/rows/table/{id}/{row_id}/` |

### 示例：创建行

```bash
curl -X POST https://baserow.example.com/api/database/rows/table/1/ \
  -H "Authorization: Token YOUR_TOKEN" \
  -H "Content-Type: application/json" \
  -d '{
    "field_1": "New Task",
    "field_2": "To Do",
    "field_3": "High"
  }'
```

### Webhooks

配置 webhooks 以通知外部系统数据变更。

| 触发器 | 描述 |
|--------|------|
| Row created | 添加新行时触发 |
| Row updated | 修改行时触发 |
| Row deleted | 删除行时触发 |

## 权限

| 角色 | 权限 |
|------|------|
| Admin | 完全工作区控制 |
| Builder | 创建和修改数据库 |
| Editor | 编辑指定数据库中的数据 |
| Viewer | 只读访问 |
| Guest | 对特定表的有限访问 |

## 模板

| 模板 | 使用场景 |
|------|----------|
| Project Management | 任务、里程碑、团队跟踪 |
| Applicant Tracking | 招聘流程 |
| CRM | 客户关系管理 |
| Inventory | 库存和产品管理 |
| Event Planning | 活动组织和日程安排 |
| Bug Tracker | 问题跟踪和解决 |

## 总结

Baserow 提供了一个灵活的无代码数据库平台，具有类似电子表格的界面。定义表和字段，使用链接字段创建关系，为数据的不同视角构建视图，并通过 REST API 访问所有内容。它是一个实用的 Airtable 替代方案，可以自托管以完全控制数据。
