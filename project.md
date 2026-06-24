# Leantime：面向非项目经理的项目管理

## 简介

Leantime 是一个开源的项目管理系统，专为非项目经理设计。它将战略规划、任务管理和团队协作结合在一个直观的界面中。

| 属性 | 详情 |
|----------|--------|
| 仓库 | Leantime/leantime |
| 许可证 | AGPL-3.0 |
| 语言 | PHP, JavaScript |
| 平台 | 基于 Web |
| 数据库 | MySQL, MariaDB |

## 主要功能

| 功能 | 描述 |
|---------|-------------|
| 战略规划 | 定义目标并将其与项目关联 |
| 看板 | 可视化任务管理 |
| 甘特图 | 基于时间线的项目规划 |
| 时间跟踪 | 记录任务工时 |
| 创意管理 | 捕获和评估创意 |
| 回顾 | 审查已完成的工作 |
| 报告 | 项目和团队绩效指标 |
| 多项目 | 同时管理多个项目 |

## 使用 Docker 安装

### Docker Compose 配置

```yaml
version: "3.8"

services:
  leantime:
    image: leantime/leantime:latest
    ports:
      - "8080:80"
    environment:
      LEAN_DB_HOST: db
      LEAN_DB_USER: leantime
      LEAN_DB_PASSWORD: secret
      LEAN_DB_DATABASE: leantime
      LEAN_APP_URL: http://localhost:8080
    volumes:
      - leantime_data:/var/www/html/userfiles
    depends_on:
      - db

  db:
    image: mariadb:10
    environment:
      MYSQL_ROOT_PASSWORD: rootsecret
      MYSQL_DATABASE: leantime
      MYSQL_USER: leantime
      MYSQL_PASSWORD: secret
    volumes:
      - db_data:/var/lib/mysql

volumes:
  leantime_data:
  db_data:
```

### 初始设置

1. 运行 `docker compose up -d`。
2. 访问 `http://localhost:8080`。
3. 创建第一个用户账户。
4. 配置公司设置。

## 核心工作流程

### 项目生命周期

| 阶段 | 描述 |
|-------|-------------|
| Strategy（战略） | 定义目标和目的 |
| Planning（规划） | 将工作分解为里程碑和任务 |
| Execution（执行） | 使用看板或列表视图处理任务 |
| Monitoring（监控） | 用报告和图表跟踪进度 |
| Review（审查） | 进行回顾 |

## 战略规划

### 设定目标

目标将日常工作与业务目标联系起来。

| 字段 | 描述 |
|-------|-------------|
| Goal Name（目标名称） | 清晰、可衡量的目标 |
| Description（描述） | 详细说明 |
| Start Date（开始日期） | 目标开始时间 |
| End Date（结束日期） | 目标完成日期 |
| Metrics（指标） | 如何衡量成功 |

### 创意管理

在承诺项目之前捕获和评估创意。

| 阶段 | 描述 |
|-------|-------------|
| New（新建） | 最近提交的创意 |
| Validation（验证） | 评估中 |
| Approved（已批准） | 准备实施 |
| Rejected（已拒绝） | 不予采纳 |

## 项目管理

### 创建项目

| 字段 | 描述 |
|-------|-------------|
| Project Name（项目名称） | 描述性项目标题 |
| Description（描述） | 项目概述 |
| Start Date（开始日期） | 项目开始日期 |
| End Date（结束日期） | 目标完成日期 |
| Team（团队） | 分配的团队成员 |
| Budget（预算） | 项目预算（可选） |

### 里程碑

里程碑标记项目时间线中的重要节点。

| 字段 | 描述 |
|-------|-------------|
| Name（名称） | 里程碑描述 |
| Date（日期） | 目标日期 |
| Status（状态） | 未开始、进行中、已完成 |
| Assigned To（分配给） | 负责人 |

## 任务管理

### 看板

看板为任务提供可视化工作流。

| 列 | 描述 |
|--------|-------------|
| Backlog（待办） | 尚未开始的任务 |
| In Progress（进行中） | 当前正在处理 |
| Review（审查） | 等待审查 |
| Done（完成） | 已完成的任务 |

### 任务属性

| 字段 | 描述 |
|-------|-------------|
| Title（标题） | 任务描述 |
| Priority（优先级） | 高、中或低 |
| Assigned To（分配给） | 负责的团队成员 |
| Milestone（里程碑） | 关联的里程碑 |
| Due Date（截止日期） | 任务截止时间 |
| Effort（工作量） | 预估工时或故事点 |
| Status（状态） | 当前工作流状态 |
| Tags（标签） | 用于过滤的标签 |

### 任务依赖

| 依赖类型 | 描述 |
|-----------------|-------------|
| Blocked By（被阻塞） | 依赖项完成前无法开始 |
| Blocks（阻塞） | 阻止另一个任务开始 |
| Related To（相关） | 关联但不依赖 |

## 时间跟踪

| 功能 | 描述 |
|---------|-------------|
| Manual Entry（手动录入） | 手动记录工时 |
| Timer（计时器） | 在任务上启动/停止计时器 |
| Timesheets（时间表） | 每周时间录入视图 |
| Reports（报告） | 按项目或人员的时间分析 |

### 录入时间

| 字段 | 描述 |
|-------|-------------|
| Date（日期） | 工作完成时间 |
| Task（任务） | 关联的任务 |
| Hours（小时） | 花费的时间 |
| Description（描述） | 完成了什么 |

## 甘特图

甘特图视图在时间线上显示任务。

| 功能 | 描述 |
|---------|-------------|
| Drag and Drop（拖放） | 可视化调整任务日期 |
| Dependencies（依赖） | 显示任务关系 |
| Milestones（里程碑） | 标记关键日期 |
| Critical Path（关键路径） | 高亮最长路径 |

## 回顾

进行团队回顾以改进流程。

| 列 | 描述 |
|--------|-------------|
| What Went Well（做得好的） | 需要继续保持的积极成果 |
| What Needs Improvement（需要改进的） | 需要解决的问题 |
| Action Items（行动项） | 要实施的具体变更 |

## 报告

| 报告 | 描述 |
|--------|-------------|
| Project Status（项目状态） | 整体项目健康状况 |
| Task Completion（任务完成） | 随时间完成的任务 |
| Time Tracking（时间跟踪） | 按项目或人员记录的工时 |
| Milestone Progress（里程碑进度） | 里程碑完成状态 |
| Team Workload（团队工作量） | 团队工作分配 |

## 用户角色

| 角色 | 权限 |
|------|-------------|
| Admin（管理员） | 完全系统访问 |
| Manager（经理） | 创建和管理项目 |
| Editor（编辑） | 编辑任务和记录时间 |
| Read-Only（只读） | 查看项目信息 |

## 团队管理

| 功能 | 描述 |
|---------|-------------|
| Users（用户） | 添加和管理团队成员 |
| Teams（团队） | 将用户分组为团队 |
| Roles（角色） | 分配权限 |
| Invitations（邀请） | 通过邮件邀请新用户 |

## 集成

| 集成 | 描述 |
|-------------|-------------|
| Slack | 向 Slack 频道发送通知 |
| Email | 更新的邮件通知 |
| Calendar（日历） | 截止日期的日历集成 |
| Webhooks | 自定义集成 |

## 自定义

| 设置 | 描述 |
|---------|-------------|
| Labels（标签） | 自定义任务标签 |
| Statuses（状态） | 自定义工作流状态 |
| Priority Levels（优先级） | 自定义优先级设置 |
| Custom Fields（自定义字段） | 额外的任务属性 |

## 有效使用的技巧

| 技巧 | 说明 |
|-----|-------------|
| 从战略开始 | 在创建任务前定义目标 |
| 使用里程碑 | 将项目分解为可管理的阶段 |
| 每天记录时间 | 准确的时间跟踪需要持续性 |
| 定期审查 | 使用回顾来改进 |
| 保持任务小型化 | 大任务应分解为子任务 |
| 明确分配 | 每个任务都应有明确的负责人 |

## 备份

| 组件 | 方法 |
|-----------|--------|
| 数据库 | MySQL dump |
| 文件 | 备份 userfiles 卷 |
| 配置 | 备份环境文件 |

```bash
# 数据库备份
docker compose exec db mysqldump -u leantime -psecret leantime > backup.sql
```

## 结论

Leantime 弥合了复杂项目管理工具和简单待办事项列表之间的差距。其对战略规划和非技术用户的关注使其成为需要结构化但又不想被过度复杂性压垮的团队的绝佳选择。
