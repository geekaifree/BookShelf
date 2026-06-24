# 数据库与后端

> 本文档整合了以下源文件：database.md, nocode.md, supabase.md, pocket.md, backend.md

---

## 来源：database.md

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


---

## 来源：nocode.md

## 目录

1. [NocoDB 简介](#introduction)
2. [安装与设置](#installation)
3. [创建表格](#tables)
4. [字段类型与配置](#fields)
5. [视图与筛选](#views)
6. [协作与分享](#collaboration)
7. [API 与集成](#api)
8. [高级功能](#advanced)

---

## 简介

NocoDB 将现有数据库转换为智能电子表格，提供类似 Airtable 的界面而无供应商锁定。它连接 MySQL、PostgreSQL、SQLite 等。

### NocoDB 核心功能

| 功能 | 描述 | 好处 |
|------|------|------|
| 无代码界面 | 可视化数据库管理 | 无需 SQL |
| 多种视图 | 网格、画廊、看板、表单 | 灵活展示 |
| API 自动生成 | 每个表格的 REST API | 易于集成 |
| 自托管 | 完全数据控制 | 隐私 |
| 开源 | 免费使用 | 无供应商锁定 |

### NocoDB vs 替代方案

| 功能 | NocoDB | Airtable | Google Sheets |
|------|--------|----------|---------------|
| 自托管 | 是 | 否 | 否 |
| 开源 | 是 | 否 | 否 |
| 数据库支持 | MySQL, PG, SQLite | 专有 | 专有 |
| API | 自动生成 | 手动 | 有限 |
| 成本 | 免费 | 订阅 | 免费/订阅 |

### 支持的数据库

| 数据库 | 版本 | 连接方式 |
|--------|------|----------|
| MySQL | 5.7+ | 直连 |
| PostgreSQL | 10+ | 直连 |
| SQLite | 3+ | 文件 |
| SQL Server | 2017+ | 直连 |
| MariaDB | 10.3+ | 直连 |

---

## 安装与设置

NocoDB 可以通过 Docker、npm 或独立应用安装。

### Docker 安装

```yaml
# docker-compose.yml
version: '3'
services:
  nocodb:
    image: nocodb/nocodb:latest
    ports:
      - "8080:8080"
    volumes:
      - nocodb:/usr/app/data
    environment:
      - NC_DB=pg://db:5432?u=nocodb&p=password&d=nocodb
    depends_on:
      - db
  
  db:
    image: postgres:14
    volumes:
      - db:/var/lib/postgresql/data
    environment:
      - POSTGRES_PASSWORD=password
      - POSTGRES_USER=nocodb
      - POSTGRES_DB=nocodb

volumes:
  nocodb:
  db:
```

### npm 安装

```bash
# Install globally
npm install -g nocodb

# Run
nocodb
```

### 系统要求

| 组件 | 最低 | 推荐 |
|------|------|------|
| CPU | 1 核 | 2 核 |
| 内存 | 1GB | 2GB |
| 存储 | 1GB | 10GB |
| Node.js | v16 | v18 LTS |

### 首次设置

| 步骤 | 操作 | 备注 |
|------|------|------|
| 1 | 访问 UI | http://localhost:8080 |
| 2 | 创建超级管理员 | 邮箱和密码 |
| 3 | 创建项目 | 新项目 |
| 4 | 连接数据库 | 已有或新建 |
| 5 | 开始创建表格 | 可视化编辑器 |

---

## 创建表格

表格是 NocoDB 数据库的基础。

### 创建新表格

| 步骤 | 操作 | 选项 |
|------|------|------|
| 1 | 点击 "+" | 添加新表格 |
| 2 | 命名表格 | 描述性名称 |
| 3 | 添加列 | 定义字段 |
| 4 | 设置主键 | ID 或自定义 |
| 5 | 创建 | 表格就绪 |

### 表格操作

| 操作 | 描述 | 快捷方式 |
|------|------|----------|
| 重命名 | 更改表格名称 | 右键菜单 |
| 复制 | 复制结构 | 右键菜单 |
| 删除 | 移除表格 | 右键菜单 |
| 导出 | 下载为 CSV | 文件菜单 |

### 导入数据

| 来源 | 格式 | 步骤 |
|------|------|------|
| CSV | .csv | 上传文件 |
| JSON | .json | 上传文件 |
| Excel | .xlsx | 上传文件 |
| Airtable | API | 导入向导 |

### 表格模板

| 模板 | 用途 | 包含字段 |
|------|------|----------|
| 项目跟踪 | 任务管理 | 任务、状态、负责人 |
| 库存 | 库存管理 | 物品、数量、价格 |
| CRM | 联系人管理 | 姓名、邮箱、电话 |
| 活动策划 | 活动管理 | 活动、日期、地点 |

---

## 字段类型与配置

NocoDB 支持多种字段类型以满足不同数据需求。

### 基本字段类型

| 类型 | 描述 | 示例 |
|------|------|------|
| SingleLineText | 短文本 | 姓名、标题 |
| LongText | 段落 | 描述、备注 |
| Number | 数值 | 价格、数量 |
| Checkbox | 布尔值 | 是/否 |
| SingleSelect | 下拉菜单 | 状态、类别 |
| MultiSelect | 多选 | 标签、标记 |

### 高级字段类型

| 类型 | 描述 | 用途 |
|------|------|------|
| Date | 日期选择器 | 生日、截止日期 |
| DateTime | 日期和时间 | 约会 |
| Email | 邮箱验证 | 联系信息 |
| URL | 链接验证 | 网站 |
| Phone | 电话号码 | 联系信息 |
| Currency | 货币值 | 价格、成本 |

### 计算字段

| 类型 | 描述 | 示例 |
|------|------|------|
| Formula | 计算值 | 价格 * 数量 |
| Lookup | 引用其他表格 | 关联记录 |
| Rollup | 聚合数据 | 求和、平均 |
| Count | 计数记录 | 物品数量 |

### 字段配置选项

| 选项 | 适用类型 | 描述 |
|------|----------|------|
| 必填 | 所有类型 | 必须填写 |
| 默认值 | 大多数类型 | 预填 |
| 唯一 | 文本、数字 | 不允许重复 |
| 最小/最大 | 数字 | 值范围 |
| 选项 | 选择 | 选项列表 |

### 字段类型对比

| 类型 | 存储 | 验证 | 显示 |
|------|------|------|------|
| SingleLineText | 字符串 | 长度限制 | 单行 |
| LongText | 文本 | 无 | 多行 |
| Number | 数字 | 仅数字 | 格式化 |
| Email | 字符串 | 邮箱格式 | 可点击链接 |
| URL | 字符串 | URL 格式 | 可点击链接 |

---

## 视图与筛选

视图控制你如何可视化和交互数据。

### 视图类型

| 视图 | 布局 | 最适合 |
|------|------|--------|
| Grid | 电子表格 | 通用数据 |
| Gallery | 卡片网格 | 可视化项目 |
| Kanban | 列 | 状态追踪 |
| Form | 输入表单 | 数据收集 |

### 创建视图

| 步骤 | 操作 | 结果 |
|------|------|------|
| 1 | 点击视图菜单 | 打开选项 |
| 2 | 选择视图类型 | Grid、Gallery 等 |
| 3 | 命名视图 | 描述性名称 |
| 4 | 配置 | 排序、筛选、字段 |
| 5 | 保存 | 视图创建完成 |

### 数据筛选

| 操作符 | 类型 | 示例 |
|--------|------|------|
| 等于 | 文本、数字 | 状态等于 "Done" |
| 不等于 | 文本、数字 | 状态不等于 "Done" |
| 包含 | 文本 | 名称包含 "test" |
| 大于 | 数字 | 价格 > 100 |
| 为空 | 所有 | 字段为空 |
| 不为空 | 所有 | 字段有值 |

### 排序

| 设置 | 选项 | 用途 |
|------|------|------|
| 字段 | 任意字段 | 排序依据 |
| 方向 | 升序/降序 | 顺序 |
| 多重 | 链式排序 | 复杂排序 |

### 分组

| 设置 | 描述 | 示例 |
|------|------|------|
| 分组依据 | 分组字段 | 按状态 |
| 子分组 | 额外分组 | 按负责人 |
| 折叠 | 隐藏分组 | 聚焦特定 |

---

## 协作与分享

NocoDB 支持多种分享选项的团队协作。

### 用户角色

| 角色 | 权限 | 可以做 |
|------|------|--------|
| Super Admin | 完全控制 | 一切 |
| Admin | 项目管理 | 创建、编辑、删除 |
| Editor | 数据编辑 | 添加、编辑记录 |
| Commenter | 仅评论 | 读取、评论 |
| Viewer | 只读 | 查看数据 |

### 添加协作者

| 步骤 | 操作 | 备注 |
|------|------|------|
| 1 | 打开项目设置 | 齿轮图标 |
| 2 | Team & Auth | 协作部分 |
| 3 | 通过邮箱邀请 | 输入邮箱 |
| 4 | 分配角色 | 选择权限 |
| 5 | 发送邀请 | 邮件通知 |

### 分享视图

| 分享类型 | 访问 | 安全性 |
|----------|------|--------|
| 私有 | 仅团队 | 认证 |
| 公开链接 | 有链接的人 | 可选密码 |
| 嵌入 | iframe | 域名限制 |

### 评论与提及

| 功能 | 描述 | 通知 |
|------|------|------|
| 评论 | 添加到记录 | 团队通知 |
| 提及 | @username | 直接通知 |
| 回复 | 话题回复 | 话题通知 |

---

## API 与集成

NocoDB 为所有表格自动生成 REST API。

### API 访问

| 方法 | 端点 | 描述 |
|------|------|------|
| GET | /api/v1/tables/{id}/records | 列出记录 |
| POST | /api/v1/tables/{id}/records | 创建记录 |
| GET | /api/v1/tables/{id}/records/{id} | 获取记录 |
| PATCH | /api/v1/tables/{id}/records/{id} | 更新记录 |
| DELETE | /api/v1/tables/{id}/records/{id} | 删除记录 |

### API 认证

| 方式 | Header | 用途 |
|------|--------|------|
| API Token | xc-auth | 服务间通信 |
| JWT | Authorization | 用户会话 |

### 生成 API Token

| 步骤 | 操作 | 结果 |
|------|------|------|
| 1 | 打开项目设置 | 齿轮图标 |
| 2 | API Tokens | Token 管理 |
| 3 | 添加新 token | 生成 |
| 4 | 复制 token | 在请求中使用 |

### 集成选项

| 集成 | 方式 | 用途 |
|------|------|------|
| Zapier | Webhook | 自动化 |
| Make | Webhook | 复杂工作流 |
| n8n | API | 自托管自动化 |
| 自定义 | REST API | 任意应用 |

### API 示例

```bash
# List all records
curl -X GET 'https://your-nocodb.com/api/v1/tables/tableId/records' \
  -H 'xc-auth: your-token'

# Create a record
curl -X POST 'https://your-nocodb.com/api/v1/tables/tableId/records' \
  -H 'xc-auth: your-token' \
  -H 'Content-Type: application/json' \
  -d '{"Name": "New Item", "Status": "Active"}'
```

---

## 高级功能

NocoDB 高级功能面向进阶用户。

### 公式

| 函数 | 描述 | 示例 |
|------|------|------|
| CONCAT | 连接文本 | CONCAT(First, " ", Last) |
| IF | 条件 | IF(Status="Done", 100, 0) |
| SUM | 求和 | SUM(Price, Tax) |
| AVG | 平均 | AVG(Scores) |
| COUNT | 计数 | COUNT(Items) |

### Lookup 字段

| 配置 | 描述 | 示例 |
|------|------|------|
| 链接表格 | 关联表格 | Orders → Customers |
| Lookup 字段 | 要检索的字段 | Customer Name |
| 聚合 | 如何组合 | First, List |

### Webhooks

| 事件 | 触发 | 用途 |
|------|------|------|
| 插入后 | 新记录 | 通知 |
| 更新后 | 记录变更 | 同步数据 |
| 删除后 | 记录移除 | 清理 |
| 手动 | 按钮点击 | 自定义操作 |

### 审计日志

| 记录的操作 | 信息 | 保留 |
|------------|------|------|
| 记录创建 | 谁、何时、数据 | 可配置 |
| 记录更新 | 谁、何时、变更 | 可配置 |
| 记录删除 | 谁、何时 | 可配置 |
| 视图变更 | 谁、何时 | 可配置 |

### 数据验证

| 验证 | 字段类型 | 规则 |
|------|----------|------|
| 必填 | 所有 | 必须填写 |
| 唯一 | 文本、数字 | 不允许重复 |
| 模式 | 文本 | 正则匹配 |
| 范围 | 数字 | 最小/最大值 |

---

## 总结

| 主题 | 核心要点 |
|------|----------|
| 安装 | Docker 简化部署 |
| 表格 | 可视化数据库管理 |
| 字段 | 多种类型带验证 |
| 视图 | Grid、Gallery、Kanban、Form |
| API | 自动生成 REST API |
| 协作 | 团队角色和分享 |


---

## 来源：supabase.md

## 简介

Supabase 是一个基于 PostgreSQL 构建的开源 Firebase 替代方案。它提供数据库、认证、实时订阅、存储和边缘函数。本教程涵盖各个功能以及如何使用 Supabase 构建应用。

## Supabase 与 Firebase 对比

| 功能 | Supabase | Firebase |
|------|----------|----------|
| 数据库 | PostgreSQL（关系型） | Firestore（文档型） |
| 认证 | GoTrue（OAuth、MFA、SSO） | Firebase Auth |
| 实时 | PostgreSQL 逻辑复制 | Cloud Firestore 流 |
| 存储 | S3 兼容 | Cloud Storage |
| 函数 | Edge Functions（Deno） | Cloud Functions（Node.js） |
| 开源 | 是 | 否 |
| 定价 | 免费层 + 按量计费 | 免费层 + 按量计费 |

## 快速开始

### 创建项目

1. 在 supabase.com 注册。
2. 创建新项目。
3. 记下项目 URL 和 anon key。

### 安装客户端库

| 语言 | 命令 |
|------|------|
| JavaScript | npm install @supabase/supabase-js |
| Python | pip install supabase |
| Dart | pub add supabase_flutter |
| Swift | 通过 Swift Package Manager 添加 |
| Kotlin | 通过 Gradle 添加 |

### 初始化客户端

```javascript
import { createClient } from '@supabase/supabase-js'

const supabase = createClient(
  'https://your-project.supabase.co',
  'your-anon-key'
)
```

## 数据库功能

### 表管理

| 操作 | SQL | 控制面板 |
|------|-----|---------|
| 创建表 | CREATE TABLE ... | Table Editor |
| 添加列 | ALTER TABLE ... ADD COLUMN ... | 列编辑器 |
| 设置关系 | 外键约束 | 可视化关系构建器 |
| 创建索引 | CREATE INDEX ... | 索引编辑器 |

### 行级安全（RLS）

| 策略类型 | 用途 |
|----------|------|
| SELECT | 控制谁可以读取行 |
| INSERT | 控制谁可以创建行 |
| UPDATE | 控制谁可以修改行 |
| DELETE | 控制谁可以删除行 |

在表上启用 RLS：

```sql
ALTER TABLE posts ENABLE ROW LEVEL SECURITY;

CREATE POLICY "Users can read own posts"
ON posts FOR SELECT
USING (auth.uid() = user_id);
```

### 数据库函数

| 函数类型 | 用例 |
|----------|------|
| 存储过程 | 复杂业务逻辑 |
| 触发器函数 | 自动更新时间戳 |
| 计算列 | 派生值 |
| RPC | 可从客户端 SDK 调用 |

## 认证

### 支持的方式

| 方式 | 设置 |
|------|------|
| 邮箱/密码 | 内置，无需配置 |
| Magic Link | 基于邮箱的无密码登录 |
| OAuth（Google、GitHub 等） | 配置提供商凭据 |
| 手机/短信 OTP | Twilio 集成 |
| SAML SSO | 企业身份提供商 |
| 匿名 | 无需注册的访客访问 |

### 认证操作

| 操作 | 客户端方法 |
|------|-----------|
| 注册 | supabase.auth.signUp({ email, password }) |
| 登录 | supabase.auth.signInWithPassword({ email, password }) |
| 登出 | supabase.auth.signOut() |
| 获取用户 | supabase.auth.getUser() |
| 获取会话 | supabase.auth.getSession() |
| 重置密码 | supabase.auth.resetPasswordForEmail(email) |

### 会话管理

| 功能 | 描述 |
|------|------|
| JWT 令牌 | 短期访问令牌 |
| 刷新令牌 | 用于续期的长期令牌 |
| 自动刷新 | 客户端 SDK 处理令牌续期 |
| 持久化 | LocalStorage 或自定义适配器 |

## 实时订阅

### 订阅变更

| 事件 | 描述 |
|------|------|
| INSERT | 新行添加 |
| UPDATE | 现有行修改 |
| DELETE | 行删除 |
| * | 所有变更 |

### 示例

```javascript
const channel = supabase
  .channel('posts-changes')
  .on('postgres_changes',
    { event: 'INSERT', schema: 'public', table: 'posts' },
    (payload) => console.log('New post:', payload.new)
  )
  .subscribe()
```

### 在线状态（Presence）

实时跟踪在线用户：

```javascript
const channel = supabase.channel('online-users')
channel.on('presence', { event: 'sync' }, () => {
  const state = channel.presenceState()
  console.log('Online:', state)
})
channel.subscribe(async (status) => {
  if (status === 'SUBSCRIBED') {
    await channel.track({ user_id: user.id, online_at: new Date() })
  }
})
```

## 存储

### 存储桶类型

| 类型 | 访问权限 | 用例 |
|------|---------|------|
| Public（公开） | 任何人可读 | 公开资源、头像 |
| Private（私有） | 认证 + RLS | 用户文档、私有媒体 |

### 操作

| 操作 | 方法 |
|------|------|
| 上传 | supabase.storage.from('bucket').upload(path, file) |
| 下载 | supabase.storage.from('bucket').download(path) |
| 获取 URL | supabase.storage.from('bucket').getPublicUrl(path) |
| 签名 URL | supabase.storage.from('bucket').createSignedUrl(path, expiresIn) |
| 列表 | supabase.storage.from('bucket').list(folder) |
| 删除 | supabase.storage.from('bucket').remove([path]) |

### 图片转换

| 参数 | 效果 |
|------|------|
| width | 调整为指定宽度 |
| height | 调整为指定高度 |
| resize | cover、contain 或 fill |
| quality | 压缩质量（1-100） |
| format | origin、webp、avif |

## Edge Functions

Edge Functions 在 Deno 运行时上运行服务端逻辑。

### 常见 Edge Function 用例

| 用例 | 描述 |
|------|------|
| Webhooks | 处理 Stripe、GitHub 事件 |
| 定时任务 | 类似 Cron 的后台任务 |
| API 代理 | 安全地调用第三方 API |
| 图片处理 | 调整大小或转换上传内容 |
| 邮件发送 | 通过 Resend/SendGrid 发送事务邮件 |

## 客户端 SDK 查询

### 查询数据

| 查询 | 示例 |
|------|------|
| 所有行 | .from('posts').select('*') |
| 特定列 | .from('posts').select('title, body') |
| 包含关联 | .from('posts').select('*, author(name)') |
| 过滤 | .from('posts').select('*').eq('status', 'published') |
| 分页 | .from('posts').select('*').range(0, 9) |

### 过滤运算符

| 运算符 | 方法 | 示例 |
|--------|------|------|
| 等于 | .eq() | .eq('status', 'draft') |
| 不等于 | .neq() | .neq('status', 'archived') |
| 大于 | .gt() | .gt('views', 100) |
| 小于 | .lt() | .lt('price', 50) |
| Like | .like() | .like('title', '%supabase%') |
| 在数组中 | .in() | .in('category', ['tech', 'news']) |
| 为空 | .is() | .is('deleted_at', null) |

## 迁移

| 命令 | 用途 |
|------|------|
| supabase migration new <name> | 创建迁移文件 |
| supabase db push | 将本地迁移应用到远程 |
| supabase db pull | 将远程 schema 拉取到本地 |
| supabase db reset | 重置本地数据库 |
| supabase db diff | 比较本地和远程 schema |

## 定价

| 计划 | 数据库 | 存储 | 带宽 | 价格 |
|------|--------|------|------|------|
| Free | 500 MB | 1 GB | 2 GB | $0 |
| Pro | 8 GB | 100 GB | 250 GB | $25/月 |
| Team | 8 GB | 100 GB | 250 GB | $599/月 |
| Enterprise | 自定义 | 自定义 | 自定义 | 联系销售 |

## 总结

Supabase 提供了一个以 PostgreSQL 为核心的完整后端平台。数据库、认证、实时、存储和边缘函数的组合，让开发者无需管理基础设施即可构建全栈应用。其开源特性和 PostgreSQL 基础给予开发者对数据的完全控制和可移植性。


---

## 来源：pocket.md

## 简介

PocketBase 是一个开源后端，由嵌入式 SQLite 数据库、实时订阅、REST API 和管理仪表盘组成。它在一个可执行文件中提供完整的后端解决方案。

## 目录

1. [核心功能](#核心功能)
2. [入门指南](#入门指南)
3. [数据集合](#数据集合)
4. [记录字段](#记录字段)
5. [REST API](#rest-api)
6. [认证](#认证)
7. [实时订阅](#实时订阅)
8. [文件存储](#文件存储)
9. [自定义代码](#自定义代码)

## 核心功能

| 功能 | 说明 |
|------|------|
| 嵌入式数据库 | SQLite，无外部依赖 |
| REST API | 从集合自动生成 |
| 管理 UI | 内置仪表盘 |
| 认证系统 | 邮箱/密码、OAuth2 |
| 实时 | 基于 SSE 的订阅 |
| 文件存储 | 本地或 S3 兼容存储 |
| 单一二进制 | 无运行时依赖 |

## 入门指南

### 安装

| 方式 | 命令 |
|------|------|
| 下载二进制 | 访问 GitHub releases |
| Go install | `go install github.com/pocketbase/pocketbase@latest` |
| Docker | `docker run -p 8090:8090 ghcr.io/pocketbase/pocketbase` |

### 目录结构

| 路径 | 用途 |
|------|------|
| `pb_data/` | SQLite 数据库和数据 |
| `pb_migrations/` | 模式迁移文件 |
| `pb_public/` | 静态文件服务 |
| `pb_hooks/` | 自定义 Go/JS 钩子 |

### 快速开始

```bash
# 下载并解压
wget https://github.com/pocketbase/pocketbase/releases/latest/download/pocketbase_0.22.0_linux_amd64.zip
unzip pocketbase_*.zip

# 启动服务器
./pocketbase serve --http=0.0.0.0:8090
```

## 数据集合

### 集合类型

| 类型 | 用途 | 认证 | API |
|------|------|------|-----|
| Base | 普通数据 | 否 | CRUD |
| Auth | 用户账户 | 是 | CRUD + 认证 |
| View | SQL 视图 | 否 | 只读 |

### 创建集合

| 步骤 | 操作 |
|------|------|
| 1 | 打开管理 UI /_ |
| 2 | 导航到 Collections |
| 3 | 点击 New Collection |
| 4 | 设置名称和类型 |
| 5 | 添加字段 |
| 6 | 配置规则 |
| 7 | 保存集合 |

### 集合设置

| 设置 | 说明 |
|------|------|
| 名称 | 集合标识符 |
| 类型 | Base、Auth 或 View |
| 列出规则 | 谁可以列出记录 |
| 查看规则 | 谁可以查看记录 |
| 创建规则 | 谁可以创建记录 |
| 更新规则 | 谁可以更新记录 |
| 删除规则 | 谁可以删除记录 |

## 记录字段

### 可用字段类型

| 字段类型 | 数据类型 | 选项 |
|----------|----------|------|
| Text | 字符串 | 最小/最大长度、模式 |
| Number | 整数/浮点 | 最小、最大 |
| Bool | 布尔 | - |
| Email | 字符串 | 格式验证 |
| URL | 字符串 | 格式验证 |
| Date | 日期时间 | 最小、最大 |
| Select | 字符串 | 预设值 |
| JSON | 对象 | 模式验证 |
| File | 文件路径 | MIME 类型、最大大小 |
| Relation | 记录 ID | 关联集合 |
| Autocomplete | 字符串 | 建议值 |

### 字段选项

| 选项 | 说明 | 示例 |
|------|------|------|
| 必填 | 必须有值 | true |
| 唯一 | 无重复 | true |
| 隐藏 | 不在 API 响应中 | false |
| 系统 | 自动管理 | false |
| 主键 | 记录 ID | Auto |

### 关联

| 关联类型 | 说明 | 示例 |
|----------|------|------|
| 单个 | 一对一 | 用户有一个档案 |
| 多个 | 一对多 | 作者有多篇文章 |
| 反向 | 反向查找 | 文章属于作者 |

## REST API

### API 端点

| 端点 | 方法 | 用途 |
|------|------|------|
| `/api/collections/{name}/records` | GET | 列出记录 |
| `/api/collections/{name}/records/{id}` | GET | 获取单条记录 |
| `/api/collections/{name}/records` | POST | 创建记录 |
| `/api/collections/{name}/records/{id}` | PATCH | 更新记录 |
| `/api/collections/{name}/records/{id}` | DELETE | 删除记录 |

### 查询参数

| 参数 | 示例 | 说明 |
|------|------|------|
| `page` | `?page=2` | 分页页码 |
| `perPage` | `?perPage=20` | 每页条目 |
| `sort` | `?sort=-created` | 排序方式 |
| `filter` | `?filter=status='active'` | 过滤记录 |
| `fields` | `?fields=id,name` | 选择字段 |
| `expand` | `?expand=author` | 展开关联 |

### 过滤语法

| 操作符 | 示例 | 说明 |
|--------|------|------|
| `=` | `status='active'` | 等于 |
| `!=` | `status!='deleted'` | 不等于 |
| `>` | `price>100` | 大于 |
| `<` | `price<500` | 小于 |
| `~` | `name~'john'` | 包含 |
| `!~` | `name!~'test'` | 不包含 |
| `?= ` | `tags?='featured'` | 数组包含 |

### 响应格式

```json
{
  "page": 1,
  "perPage": 30,
  "totalItems": 150,
  "totalPages": 5,
  "items": [
    {
      "id": "abc123",
      "collectionId": "xyz789",
      "collectionName": "posts",
      "title": "Hello World",
      "created": "2024-01-15 10:30:00.000Z",
      "updated": "2024-01-15 10:30:00.000Z"
    }
  ]
}
```

## 认证

### 认证方式

| 方式 | 配置 | 用户操作 |
|------|------|----------|
| 邮箱/密码 | 内置 | 注册/登录 |
| OAuth2 | 提供商设置 | 社交登录 |
| OTP | 基于邮箱 | 一次性密码 |

### OAuth2 提供商

| 提供商 | 所需设置 |
|--------|----------|
| Google | Client ID/Secret |
| GitHub | Client ID/Secret |
| Facebook | Client ID/Secret |
| Twitter | API Key/Secret |
| Discord | Client ID/Secret |
| Microsoft | Client ID/Secret |

### 认证 API 端点

| 端点 | 方法 | 用途 |
|------|------|------|
| `/api/collections/{auth}/records` | POST | 注册 |
| `/api/collections/{auth}/auth-with-password` | POST | 登录 |
| `/api/collections/{auth}/auth-refresh` | POST | 刷新令牌 |
| `/api/collections/{auth}/records/{id}` | PATCH | 更新档案 |
| `/api/collections/{auth}/request-password-reset` | POST | 重置密码 |
| `/api/collections/{auth}/confirm-password-reset` | POST | 确认重置 |

### 令牌管理

| 令牌 | 持续时间 | 用途 |
|------|----------|------|
| Auth token | 2 周（可配置） | API 认证 |
| Refresh token | 长期有效 | 获取新的 auth token |

## 实时订阅

### 订阅类型

| 类型 | 说明 | 过滤器 |
|------|------|--------|
| Subscribe | 所有记录 | 无 |
| Subscribe to record | 特定记录 | 记录 ID |
| Subscribe with filter | 过滤记录 | 过滤表达式 |

### SSE 连接

```javascript
// 连接到实时
const eventSource = new EventSource(
  '/api/realtime?token=YOUR_AUTH_TOKEN'
);

// 订阅集合
fetch('/api/realtime', {
  method: 'POST',
  headers: {
    'Content-Type': 'application/json',
  },
  body: JSON.stringify({
    action: 'subscribe',
    collection: 'posts',
    filter: 'status="published"'
  })
});

// 监听事件
eventSource.onmessage = (event) => {
  const data = JSON.parse(event.data);
  console.log(data.action, data.record);
};
```

### 事件类型

| 事件 | 触发条件 |
|------|----------|
| `create` | 新记录已创建 |
| `update` | 记录已修改 |
| `delete` | 记录已删除 |

## 文件存储

### 存储选项

| 选项 | 配置 | 使用场景 |
|------|------|----------|
| 本地文件系统 | 默认 | 开发 |
| S3 | 环境变量 | 生产 |
| S3 兼容 | MinIO, R2 等 | 自托管 |

### 文件上传

```bash
# 上传文件到记录
curl -X POST http://localhost:8090/api/collections/posts/records \
  -H "Authorization: Bearer YOUR_TOKEN" \
  -F "title=My Post" \
  -F "attachment=@file.pdf"
```

### S3 配置

| 变量 | 说明 |
|------|------|
| `PB_S3_ENDPOINT` | S3 端点 URL |
| `PB_S3_REGION` | S3 区域 |
| `PB_S3_BUCKET` | 存储桶名称 |
| `PB_S3_ACCESS_KEY` | 访问密钥 |
| `PB_S3_SECRET` | 密钥 |
| `PB_S3_FORCE_PATH_STYLE` | 路径风格访问 |

## 自定义代码

### Go 钩子

```go
// hooks/main.go
package hooks

import (
    "github.com/pocketbase/pocketbase"
    "github.com/pocketbase/pocketcore/core"
)

func init() {
    app := pocketbase.New()
    
    app.OnRecordBeforeCreateRequest("posts").Add(func(e *core.RecordCreateEvent) error {
        // 记录创建前的自定义逻辑
        return nil
    })
}
```

### JavaScript 钩子

```javascript
// pb_hooks/main.pb.js
routerAdd("GET", "/api/hello", (c) => {
    return c.json(200, {"message": "Hello World"})
})

onRecordBeforeCreateRequest("posts", (e) => {
    // 记录创建前的自定义逻辑
    console.log("Creating post:", e.record.get("title"))
})
```

### 定时任务

```javascript
// pb_hooks/scheduled.pb.js
cronAdd("cleanup", "0 0 * * *", () => {
    // 每天午夜运行
    const records = $app.dao().findRecordsByFilter(
        "posts",
        "created < @7DaysAgo"
    )
    records.forEach(record => {
        $app.dao().deleteRecord(record)
    })
})
```

## 管理仪表盘

### 仪表盘功能

| 功能 | 路径 | 说明 |
|------|------|------|
| 集合 | `/_/#/collections` | 管理模式 |
| 记录 | `/_/#/collections/{id}` | 浏览数据 |
| 用户 | `/_/#/users` | 管理用户 |
| 日志 | `/_/#/logs` | 请求日志 |
| 设置 | `/_/#/settings` | 应用配置 |
| API 规则 | `/_/#/collections/{id}/rules` | 访问控制 |

### API 规则

| 规则 | 何时应用 | 默认 |
|------|----------|------|
| List | GET /records | 仅管理员 |
| View | GET /records/:id | 仅管理员 |
| Create | POST /records | 仅管理员 |
| Update | PATCH /records/:id | 仅管理员 |
| Delete | DELETE /records/:id | 仅管理员 |

## 总结

PocketBase 在单一二进制文件中提供完整的后端解决方案，消除了对外部数据库、API 服务器或管理面板的需求。其嵌入式 SQLite 数据库、自动生成的 REST API、实时订阅和内置认证使其成为快速原型开发和中小型应用的理想选择。


---

## 来源：backend.md

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


---
