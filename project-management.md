# 项目与任务管理

> 本文档整合了以下源文件：todo.md, project.md, kanban.md, board.md, board2.md, wekan.md

---

## 来源：todo.md

## 简介

Vikunja 是一个开源的自托管任务管理应用。它支持列表、看板和团队协作。本教程涵盖安装、任务组织、团队工作流程和 API 使用。

## Vikunja 与其他任务管理器对比

| 功能 | Vikunja | Todoist | Trello | Nextcloud Tasks |
|------|---------|---------|--------|-----------------|
| 自托管 | 是 | 否 | 否 | 是 |
| 开源 | 是 | 否 | 否 | 是 |
| 看板视图 | 是 | 是 | 是 | 否 |
| CalDAV | 是 | 是 | 否 | 是 |
| 团队 | 是 | 是 | 是 | 否 |
| API | REST + CalDAV | REST | REST | CalDAV |
| Webhooks | 是 | 是 | 是 | 否 |

## 安装

### Docker Compose

```yaml
version: '3'
services:
  vikunja:
    image: vikunja/vikunja
    container_name: vikunja
    restart: unless-stopped
    environment:
      VIKUNJA_SERVICE_PUBLICURL: https://tasks.example.com
      VIKUNJA_SERVICE_JWTSECRET: your-secret-key
      VIKUNJA_DATABASE_SQLITE_PATH: /app/vikunja.db
      VIKUNJA_SERVICE_ENABLEREGISTRATION: "true"
    volumes:
      - ./vikunja-files:/app/vikunja/files
      - ./vikunja-db:/app/vikunja.db
    ports:
      - "3456:3456"
```

### 二进制安装

```bash
# 从 releases 下载
wget https://dl.vikunja.io/vikunja/$(VERSION)/vikunja-$(VERSION)-linux-amd64.tar.gz
tar -xzf vikunja-*.tar.gz
./vikunja
```

## 核心概念

### 层级结构

| 级别 | 描述 |
|------|------|
| 命名空间（Namespace） | 顶层分组（如工作、个人） |
| 列表（List） | 命名空间内的任务集合 |
| 任务（Task） | 单个工作项 |
| 子任务（Subtask） | 父任务内的子任务 |

### 任务属性

| 属性 | 类型 | 描述 |
|------|------|------|
| Title | Text | 任务名称 |
| Description | Markdown | 详细信息 |
| Due Date | Date | 截止日期 |
| Start Date | Date | 开始日期 |
| Priority | 1-5 | 重要程度 |
| Labels | Tags | 分类 |
| Assignees | Users | 负责人 |
| List | Reference | 所属列表 |
| Repeat | Rule | 重复计划 |
| Attachments | Files | 相关文件 |

## 创建和管理任务

### 创建任务

1. 导航到一个列表。
2. 点击"New Task"或按 Q 键。
3. 输入标题和可选详情。
4. 设置截止日期、优先级和负责人。
5. 按 Enter 或点击"Create"。

### 任务操作

| 操作 | 快捷键 | 方法 |
|------|--------|------|
| 创建任务 | Q | 快速添加按钮 |
| 编辑任务 | 点击 | 打开任务详情 |
| 完成任务 | 点击复选框 | 切换完成状态 |
| 删除任务 | Delete 键 | 任务菜单 |
| 移动任务 | 拖放 | 列表间移动 |
| 分配 | 点击负责人 | 用户选择器 |
| 设置优先级 | P 键 | 优先级选择器 |
| 设置截止日期 | D 键 | 日期选择器 |

### 优先级

| 级别 | 颜色 | 含义 |
|------|------|------|
| 1 | 灰色 | 最低 |
| 2 | 蓝色 | 低 |
| 3 | 黄色 | 中等 |
| 4 | 橙色 | 高 |
| 5 | 红色 | 紧急 |

## 视图

### 可用视图

| 视图 | 显示方式 | 最佳用途 |
|------|---------|---------|
| List（列表） | 任务表格 | 快速概览 |
| Kanban（看板） | 列式面板 | 工作流程可视化 |
| Gantt（甘特图） | 时间线图表 | 项目规划 |
| Table（表格） | 电子表格样式 | 数据分析 |

### 看板

| 列 | 用途 |
|------|------|
| Open | 新建和未开始的任务 |
| In Progress | 进行中的工作 |
| Done | 已完成的任务 |
| Custom | 自定义阶段 |

## 命名空间和列表

### 命名空间组织

| 命名空间 | 列表 |
|----------|------|
| Work（工作） | 项目、会议、报告 |
| Personal（个人） | 跑腿、健康、学习 |
| Home（家庭） | 家务、装修、购物 |

### 列表设置

| 设置 | 选项 |
|------|------|
| 默认视图 | List、Kanban、Gantt、Table |
| 背景颜色 | 十六进制颜色代码 |
| 共享 | 团队或个人访问 |
| 位置 | 侧边栏排序 |

## 标签

标签提供跨列表的分类。

| 标签 | 颜色 | 用例 |
|------|------|------|
| Bug | 红色 | 缺陷跟踪 |
| Feature | 蓝色 | 新功能 |
| Urgent | 橙色 | 时间敏感 |
| Blocked | 灰色 | 等待依赖 |
| Review | 紫色 | 需要审查 |

## 团队与共享

### 团队角色

| 角色 | 权限 |
|------|------|
| Admin（管理员） | 对团队和共享列表的完全控制 |
| Member（成员） | 可以查看和编辑共享列表 |
| Read-only（只读） | 可以查看但不能编辑 |

### 共享方式

| 方式 | 方法 |
|------|------|
| 团队共享 | 与整个团队共享列表 |
| 个人共享 | 与特定用户共享 |
| 链接共享 | 公开 URL（只读） |
| CalDAV | 通过日历应用访问 |

## CalDAV 集成

### 连接 CalDAV 客户端

| 客户端 | 配置 |
|--------|------|
| macOS Calendar | 使用 Vikunja URL 添加 CalDAV 账户 |
| Thunderbird | 添加 CalDAV 日历 |
| DAVx5（Android） | 同步任务到手机 |
| iOS Reminders | 添加 CalDAV 账户 |

### CalDAV URL 格式

```
https://tasks.example.com/dav/users/username
```

## 重复任务

| 模式 | 示例 |
|------|------|
| 每天 | 每天上午 9 点 |
| 每周 | 每周一 |
| 每月 | 每月第一天 |
| 每年 | 1 月 1 日 |
| 自定义 | 每 2 周周三 |

## 过滤器和搜索

| 过滤器 | 语法 |
|--------|------|
| 按负责人 | assignee:username |
| 按优先级 | priority:5 |
| 按标签 | label:bug |
| 按截止日期 | due:2024-01-15 |
| 按列表 | list:My List |
| 按状态 | done:true |
| 文本搜索 | 任意文本 |

## API 使用

### REST API 端点

| 方法 | 端点 | 描述 |
|------|------|------|
| GET | /api/v1/tasks | 列出所有任务 |
| POST | /api/v1/tasks | 创建任务 |
| GET | /api/v1/tasks/{id} | 获取任务详情 |
| PUT | /api/v1/tasks/{id} | 更新任务 |
| DELETE | /api/v1/tasks/{id} | 删除任务 |

### 认证

```bash
# 从用户设置获取 API 令牌
curl -H "Authorization: Bearer YOUR_TOKEN" \
  https://tasks.example.com/api/v1/tasks
```

## Webhooks

| 事件 | 触发条件 |
|------|---------|
| task.created | 新任务添加 |
| task.updated | 任务修改 |
| task.deleted | 任务删除 |
| task.comment.created | 评论添加 |
| task.assignee.created | 用户分配 |

## 迁移

| 来源 | 方法 |
|------|------|
| Todoist | 通过 API 导入 |
| Trello | 导出 JSON，导入 |
| Todo.txt | 直接文件导入 |
| Microsoft To Do | 手动或 API |

## 快捷键

| 快捷键 | 操作 |
|--------|------|
| Q | 快速添加任务 |
| / | 聚焦搜索 |
| 1-5 | 设置优先级 |
| D | 设置截止日期 |
| L | 添加标签 |
| A | 分配用户 |
| N | 新建命名空间 |
| Ctrl+Enter | 保存任务 |

## 总结

Vikunja 提供了一个全面的自托管任务管理解决方案，支持多种视图、团队协作和 CalDAV 集成。其简洁的界面、REST API 和灵活的组织系统，使其适用于个人生产力和团队项目管理。


---

## 来源：project.md

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


---

## 来源：kanban.md

## 简介

Kanboard 是一个免费开源的看板项目管理工具。它提供可视化的任务板，用于组织工作、跟踪进度和管理工作流。本教程涵盖安装、看板配置、任务管理和自动化。

## 架构概览

| 组件 | 描述 | 角色 |
|------|------|------|
| Web Application | PHP 应用 | 用户界面 |
| Database | SQLite 或 MySQL | 数据存储 |
| Plugins | 扩展 | 附加功能 |
| API | JSON-RPC | 编程访问 |

## 安装

### 系统要求

| 组件 | 最低配置 | 推荐配置 |
|------|----------|----------|
| PHP | 7.4+ | 8.0+ |
| Web Server | Apache, Nginx | Nginx + PHP-FPM |
| Database | SQLite | MySQL/MariaDB |
| Extensions | pdo, gd, json, mbstring | 全部必需 |
| Disk | 50 MB | 100 MB |

### Docker 安装

```yaml
version: "3.8"

services:
  kanboard:
    image: kanboard/kanboard:latest
    container_name: kanboard
    restart: unless-stopped
    ports:
      - "8080:80"
    volumes:
      - ./data:/var/www/app/data
      - ./plugins:/var/www/app/plugins
    environment:
      - DATABASE_URL=sqlite:///var/www/app/data/db.sqlite
```

### 手动安装

```bash
# 下载最新版本
wget https://github.com/kanboard/kanboard/archive/refs/heads/main.zip
unzip main.zip
mv kanboard-main /var/www/kanboard

# 设置权限
chmod -R 755 /var/www/kanboard/data
chmod -R 755 /var/www/kanboard/plugins

# 配置 Web 服务器
# 将文档根目录指向 /var/www/kanboard
```

### 初始设置

1. 访问 `http://your-server:8080`
2. 使用默认凭据登录（admin/admin）
3. 更改管理员密码
4. 创建第一个项目

## 项目管理

### 创建项目

| 字段 | 描述 | 示例 |
|------|------|------|
| Name | 项目标题 | Website Redesign |
| Identifier | URL 友好的标识符 | website-redesign |
| Description | 项目详情 | 重新设计公司网站 |
| Owner | 项目经理 | admin |

### 项目设置

| 设置 | 选项 | 默认值 |
|------|------|--------|
| Public project | 是/否 | 否 |
| Priority default | 0-3 | 0 |
| Task limit per column | 数字 | 无限 |
| Swimlane | 启用/禁用 | 禁用 |

## 看板配置

### 列

默认列表示工作流阶段：

| 列 | 用途 | WIP 限制 |
|----|------|----------|
| Backlog | 计划的工作 | 无限 |
| Ready | 准备开始 | 5 |
| Work in Progress | 活跃工作 | 3 |
| Done | 已完成工作 | 无限 |

### 自定义列

| 步骤 | 操作 |
|------|------|
| 1 | 前往 Project Settings > Columns |
| 2 | 点击 "Add Column" |
| 3 | 输入列名 |
| 4 | 设置 WIP（在制品）限制 |
| 5 | 设置列位置 |
| 6 | 保存 |

### 列属性

| 属性 | 描述 | 用途 |
|------|------|------|
| Name | 列标题 | 显示标签 |
| Position | 看板上的顺序 | 视觉排列 |
| Task limit | 最大并发任务 | 防止过载 |
| Description | 列用途 | 悬停信息 |

### 泳道

泳道将看板分为水平行：

| 使用场景 | 配置 |
|----------|------|
| 按优先级 | 高、中、低泳道 |
| 按团队 | 前端、后端、设计泳道 |
| 按类型 | 功能、Bug、任务泳道 |
| 按负责人 | 个人贡献者泳道 |

## 任务管理

### 创建任务

| 字段 | 描述 | 必填 |
|------|------|------|
| Title | 任务名称 | 是 |
| Description | 详细信息 | 否 |
| Assignee | 负责人 | 否 |
| Color | 可视化分类 | 否 |
| Priority | 0（低）到 3（紧急） | 否 |
| Due date | 截止日期 | 否 |
| Tags | 标签 | 否 |
| Category | 分组 | 否 |
| Story points | 工作量估算 | 否 |

### 任务属性

| 属性 | 描述 | 值 |
|------|------|-----|
| Status | 当前状态 | Open, Closed |
| Assignee | 所有者 | 用户列表 |
| Priority | 重要性 | 0-3 |
| Color | 分类 | 6 种颜色 |
| Due date | 截止日期 | 日期 |
| Tags | 标签 | 多个 |
| Category | 分组 | 项目类别 |
| Score | 工作量点数 | 数字 |
| Reference | 外部链接 | URL 或 ID |

### 移动任务

| 操作 | 方法 |
|------|------|
| 更改列 | 拖放 |
| 重新分配 | 编辑任务，选择用户 |
| 更改优先级 | 编辑任务，设置优先级 |
| 添加到分类 | 编辑任务，选择分类 |

### 任务操作

| 操作 | 描述 | 快捷键 |
|------|------|--------|
| Edit | 修改任务详情 | 点击任务 |
| Close | 标记为完成 | 移到 Done |
| Duplicate | 复制任务 | 任务菜单 |
| Move | 转移到项目 | 任务菜单 |
| Delete | 永久删除 | 任务菜单 |
| Comment | 添加讨论 | 任务详情 |
| Subtask | 添加子项 | 任务详情 |
| Link | 连接到另一个任务 | 任务详情 |

## 分类

### 分类管理

| 字段 | 描述 | 示例 |
|------|------|------|
| Name | 分类标签 | Bug, Feature, Improvement |
| Description | 用途 | 分类详情 |
| Color | 可视化标识符 | 分配的颜色 |

### 使用分类

| 用途 | 优势 |
|------|------|
| Grouping | 组织相关任务 |
| Filtering | 快速分类视图 |
| Reporting | 基于分类的指标 |
| Visual | 颜色编码标识 |

## 标签

### 标签功能

| 功能 | 描述 |
|------|------|
| Multiple tags | 每个任务 |
| Auto-suggest | 显示现有标签 |
| Color support | 可视化编码 |
| Searchable | 按标签筛选 |

### 标签最佳实践

| 实践 | 示例 | 优势 |
|------|------|------|
| 一致命名 | 小写、连字符 | 统一性 |
| 每任务限制 | 3-5 个标签 | 清晰 |
| 描述性 | `frontend`, `urgent`, `review` | 快速识别 |

## 子任务

### 子任务属性

| 属性 | 描述 |
|------|------|
| Title | 子任务名称 |
| Status | 待办、进行中、已完成 |
| Assignee | 负责人 |
| Time estimate | 预估小时数 |
| Time spent | 已记录小时数 |

### 子任务工作流

1. 打开任务详情
2. 添加子任务
3. 设置标题和状态
4. 如需分配
5. 跟踪进度

## 自动化

### 自动操作

Kanboard 支持由事件触发的自动操作：

| 触发器 | 操作 | 示例 |
|--------|------|------|
| Task moved | 分配用户 | 移到审查时自动分配 |
| Task created | 设置颜色 | 按分类着色 |
| Task closed | 移到列 | 归档已完成任务 |
| Due date passed | 更改颜色 | 高亮逾期任务 |

### 配置自动化

1. 前往 Project Settings > Automatic Actions
2. 选择触发事件
3. 选择操作
4. 配置参数
5. 保存

### 可用触发器

| 触发器 | 描述 |
|--------|------|
| Task creation | 新任务添加 |
| Task modification | 任何更改 |
| Task move | 列更改 |
| Task close | 标记完成 |
| Task assign | 用户分配 |
| Column change | WIP 限制达到 |

### 可用操作

| 操作 | 描述 |
|------|------|
| Assign user | 设置任务所有者 |
| Change color | 更新任务颜色 |
| Change priority | 设置优先级 |
| Set due date | 更新截止日期 |
| Move to column | 更改位置 |
| Close task | 标记完成 |
| Send notification | 邮件提醒 |

## 筛选和搜索

### 筛选选项

| 筛选 | 语法 | 示例 |
|------|------|------|
| Status | `status:open` | 未完成任务 |
| Assignee | `assignee:admin` | 分配给 admin 的任务 |
| Priority | `priority:3` | 紧急任务 |
| Category | `category:bug` | Bug 分类 |
| Tag | `tag:frontend` | Frontend 标签 |
| Due date | `due:today` | 今天到期 |
| Color | `color:yellow` | 黄色任务 |

### 搜索运算符

| 运算符 | 描述 | 示例 |
|--------|------|------|
| `:` | 等于 | `status:open` |
| `!` | 不等于 | `!status:closed` |
| `>` | 大于 | `priority>1` |
| `<` | 小于 | `priority<3` |

## 分析

### 内置报表

| 报表 | 描述 | 用途 |
|------|------|------|
| Board summary | 各列任务计数 | 概览 |
| User summary | 每人任务数 | 工作量 |
| Category summary | 每分类任务数 | 分布 |
| Cumulative flow | 任务流随时间变化 | 趋势 |
| Burndown | 剩余工作 | 进度跟踪 |
| Lead time | 从创建到完成的时间 | 效率 |
| Cycle time | 活跃工作中的时间 | 性能 |

### 指标

| 指标 | 计算 | 目标 |
|------|------|------|
| Lead time | 创建到完成 | 最小化 |
| Cycle time | 开始到完成 | 一致 |
| Throughput | 每期完成任务数 | 最大化 |
| WIP | 当前活跃任务 | 在限制内 |

## API 访问

### JSON-RPC API

```bash
# 获取所有项目
curl -X POST http://your-server:8080/jsonrpc.php \
  -H "Content-Type: application/json" \
  -u admin:password \
  -d '{"jsonrpc":"2.0","method":"getAllProjects","id":1}'

# 获取所有任务
curl -X POST http://your-server:8080/jsonrpc.php \
  -H "Content-Type: application/json" \
  -u admin:password \
  -d '{"jsonrpc":"2.0","method":"getAllTasks","params":[1,""],"id":2}'
```

### API 方法

| 方法 | 描述 | 参数 |
|------|------|------|
| `getAllProjects` | 列出项目 | 无 |
| `getProjectById` | 获取项目 | project_id |
| `getAllTasks` | 列出任务 | project_id, status |
| `getTaskById` | 获取任务 | task_id |
| `createTask` | 新建任务 | task_params |
| `updateTask` | 修改任务 | task_params |
| `removeTask` | 删除任务 | task_id |

## 插件

### 基本插件

| 插件 | 用途 | 分类 |
|------|------|------|
| Customizer | UI 自定义 | 界面 |
| Calendar | 截止日期日历 | 可视化 |
| Gantt | 甘特图视图 | 规划 |
| Markdown editor | 富文本编辑 | 编辑器 |
| Budget | 成本跟踪 | 财务 |
| Time tracking | 记录工时 | 生产力 |

### 安装插件

1. 从仓库下载插件
2. 解压到 `/plugins` 目录
3. 在 Settings > Plugins 中启用
4. 根据需要配置

## 键盘快捷键

| 操作 | 快捷键 | 上下文 |
|------|--------|--------|
| 新建任务 | N | 看板视图 |
| 搜索 | / | 全局 |
| 保存 | Ctrl+S | 编辑表单 |
| 关闭 | Esc | 模态/对话框 |

## 多用户功能

### 用户角色

| 角色 | 权限 | 用途 |
|------|------|------|
| Admin | 完全控制 | 系统管理 |
| Manager | 项目管理 | 团队领导 |
| User | 任务操作 | 团队成员 |
| Viewer | 只读访问 | 利益相关者 |

## 总结

Kanboard 提供了一个简洁高效的看板项目管理解决方案。其可视化任务板、自动化功能和 API 访问使其适合个人和团队使用。

关键实践：

- 使用 WIP 限制防止团队过载
- 设置自动化规则减少手动操作
- 使用标签和分类保持任务组织
- 定期查看分析报表优化工作流
- 使用 API 集成其他工具


---

## 来源：board.md

## 简介

Focalboard 是一个开源项目管理工具，提供看板、表格和日历来追踪任务和项目。它是 Trello、Notion 和 Asana 的自托管替代方案，支持个人服务器和 Mattermost 集成选项。

## 系统要求

| 组件 | 最低配置 | 推荐配置 |
|------|---------|---------|
| CPU | 1 核 | 2 核 |
| 内存 | 512 MB | 2 GB |
| 磁盘 | 100 MB | 1 GB |
| 数据库 | SQLite | PostgreSQL 或 MySQL |
| 操作系统 | Linux, macOS, Windows | Linux |

## 安装

### Docker 安装

```bash
docker run -d \
  --name focalboard \
  -p 8000:8000 \
  -v /path/to/data:/opt/focalboard/data \
  mattermost/focalboard:latest
```

### Docker Compose 搭配 PostgreSQL

```yaml
version: '3.8'
services:
  focalboard:
    image: mattermost/focalboard:latest
    ports:
      - "8000:8000"
    volumes:
      - ./focalboard-data:/opt/focalboard/data
    environment:
      - FOCALBOARD_DB_TYPE=postgres
      - FOCALBOARD_DB_HOST=db
      - FOCALBOARD_DB_PORT=5432
      - FOCALBOARD_DB_USER=focalboard
      - FOCALBOARD_DB_PASSWORD=focalboard
      - FOCALBOARD_DB_NAME=focalboard
    depends_on:
      - db
    restart: unless-stopped

  db:
    image: postgres:15
    volumes:
      - pg-data:/var/lib/postgresql/data
    environment:
      - POSTGRES_USER=focalboard
      - POSTGRES_PASSWORD=focalboard
      - POSTGRES_DB=focalboard
    restart: unless-stopped

volumes:
  pg-data:
```

### 手动安装

```bash
# 下载最新版本
wget https://github.com/mattermost/focalboard/releases/latest/download/focalboard-linux-amd64.tar.gz
tar -xzf focalboard-linux-amd64.tar.gz
cd focalboard
./bin/focalboard-server
```

## 配置

### config.json 关键设置

```json
{
  "serverRoot": "http://localhost:8000",
  "port": 8000,
  "dbtype": "postgres",
  "dbconfig": "postgres://focalboard:focalboard@db:5432/focalboard?sslmode=disable",
  "useSSL": false,
  "session_expire_time": 2592000,
  "session_refresh_time": 18000
}
```

### 配置选项

| 设置 | 说明 | 默认值 |
|------|------|--------|
| `serverRoot` | 服务器基础 URL | `http://localhost:8000` |
| `port` | 服务器监听端口 | `8000` |
| `dbtype` | 数据库后端 | `sqlite3` |
| `dbconfig` | 数据库连接字符串 | SQLite 文件路径 |
| `useSSL` | 启用 HTTPS | `false` |
| `session_expire_time` | 会话持续时间（秒） | 2592000（30 天） |

## 看板概念

### 看板类型

| 类型 | 说明 | 用途 |
|------|------|------|
| 私有 | 仅邀请的成员 | 个人任务 |
| 公开 | 所有工作区成员可见 | 团队项目 |
| 模板 | 可复用的看板结构 | 标准化工作流 |

### 视图类型

| 视图 | 布局 | 最佳场景 |
|------|------|---------|
| 看板 | 看板列 | 任务工作流管理 |
| 表格 | 电子表格行 | 详细数据追踪 |
| 日历 | 月历 | 基于日期的规划 |
| 画廊 | 卡片网格 | 可视化项目概览 |

## 卡片属性

### 属性类型

| 属性 | 类型 | 用途 |
|------|------|------|
| 文本 | 字符串 | 描述、备注 |
| 数字 | 整数或浮点数 | 故事点、优先级 |
| 选择 | 下拉列表 | 状态、类别 |
| 多选 | 多标签 | 标签 |
| 日期 | 日期选择器 | 截止日期、里程碑 |
| 人员 | 用户选择器 | 负责人 |
| 复选框 | 布尔值 | 完成标志 |
| URL | 网页链接 | 参考链接 |
| 邮箱 | 邮箱地址 | 联系信息 |
| 电话 | 电话号码 | 联系信息 |
| 创建时间 | 自动生成 | 创建时间戳 |
| 更新时间 | 自动生成 | 最后修改时间 |
| 创建者 | 自动生成 | 卡片创建者 |

### 默认卡片模板

| 属性 | 类型 | 默认值 |
|------|------|--------|
| 状态 | 选择 | To Do, In Progress, Done |
| 优先级 | 选择 | Low, Medium, High, Urgent |
| 截止日期 | 日期 | （空） |
| 负责人 | 人员 | （空） |
| 描述 | 文本 | （空） |

## 工作流管理

### 看板设置

| 列 | 状态 | 用途 |
|----|------|------|
| 待办池 | Backlog | 想法和未来任务 |
| 待办 | To Do | 准备开始 |
| 进行中 | In Progress | 正在处理 |
| 审核 | Review | 等待审核或批准 |
| 完成 | Done | 已完成的任务 |

### 卡片管理

| 操作 | 方法 | 快捷键 |
|------|------|--------|
| 创建卡片 | 点击加号按钮 | C 键 |
| 编辑卡片 | 点击卡片 | Enter 键 |
| 移动卡片 | 拖放 | - |
| 复制卡片 | 卡片菜单 | - |
| 删除卡片 | 卡片菜单 | - |
| 添加评论 | 卡片详情视图 | - |

## 模板

### 内置模板

| 模板 | 用途 |
|------|------|
| 项目路线图 | 追踪项目里程碑 |
| 会议记录 | 记录会议结果 |
| 个人任务 | 个人任务管理 |
| Bug 追踪 | 软件缺陷追踪 |
| 内容日历 | 内容规划 |
| 销售漏斗 | 线索追踪 |
| 目标和 OKR | 目标追踪 |

### 创建自定义模板

1. 创建一个具有所需结构的看板
2. 添加所有必需的属性和视图
3. 点击看板菜单并选择 **Save as Template**
4. 模板即可用于新看板

## Mattermost 集成

### 作为插件安装

1. 导航到 **System Console > Plugin Management**
2. 上传 Focalboard 插件
3. 启用插件
4. 从 Mattermost 侧边栏访问看板

### 集成功能

| 功能 | 说明 |
|------|------|
| 侧边栏访问 | 可从频道侧边栏访问看板 |
| 频道看板 | 与特定频道关联的看板 |
| 通知 | Mattermost 通知卡片更新 |
| 提及 | 在卡片评论中 @提及用户 |
| 分享 | 与频道成员分享看板 |

## 分组和筛选

### 分组选项

| 分组依据 | 创建的列 | 用途 |
|---------|---------|------|
| 状态 | 每个状态值一列 | 看板工作流 |
| 优先级 | 每个优先级一列 | 基于优先级的视图 |
| 负责人 | 每人一列 | 工作量分配 |
| 日期 | 日历或时间线 | 日程管理 |

### 筛选选项

| 筛选 | 操作符 | 示例 |
|------|--------|------|
| 状态 | 是，不是 | 状态是 "In Progress" |
| 优先级 | 是，不是 | 优先级是 "High" |
| 负责人 | 是，不是，已设置 | 负责人是 "John" |
| 日期 | 是，之前，之后 | 截止日期在 "2024-02-01" 之前 |
| 文本 | 包含，不包含 | 标题包含 "bug" |

## 搜索

| 搜索类型 | 范围 | 结果 |
|---------|------|------|
| 看板搜索 | 所有看板 | 匹配的看板名称 |
| 卡片搜索 | 当前看板 | 匹配的卡片标题和内容 |
| 全局搜索 | 所有内容 | 跨所有看板的卡片 |

## 数据库选项

| 数据库 | 用途 | 备份方法 |
|--------|------|---------|
| SQLite | 个人使用 | 复制 .db 文件 |
| PostgreSQL | 团队部署 | pg_dump |
| MySQL | 团队部署 | mysqldump |

## 备份与恢复

| 组件 | 方法 | 频率 |
|------|------|------|
| 数据库 | pg_dump 或 mysqldump | 每日 |
| 文件上传 | rsync 或文件复制 | 每日 |
| 配置 | config.json 备份 | 每周 |

### 备份脚本

```bash
#!/bin/bash
DATE=$(date +%Y%m%d)
BACKUP_DIR="/var/backups/focalboard"

pg_dump -U focalboard focalboard > "$BACKUP_DIR/board-$DATE.sql"
cp -r /opt/focalboard/data "$BACKUP_DIR/data-$DATE"
find "$BACKUP_DIR" -mtime +30 -delete
```

## 安全

| 措施 | 配置 |
|------|------|
| HTTPS | 使用 SSL 的反向代理 |
| 认证 | 内置用户账户 |
| 会话管理 | 可配置的会话过期 |
| 访问控制 | 看板级权限 |
| 速率限制 | 基于代理的限制 |

## 反向代理

### Nginx 配置

```nginx
server {
    listen 80;
    server_name board.example.com;

    location / {
        proxy_pass http://localhost:8000;
        proxy_set_header Host $host;
        proxy_set_header X-Real-IP $remote_addr;
        proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
        proxy_set_header X-Forwarded-Proto $scheme;
    }

    location /ws {
        proxy_pass http://localhost:8000;
        proxy_http_version 1.1;
        proxy_set_header Upgrade $http_upgrade;
        proxy_set_header Connection "upgrade";
    }
}
```

## API

### REST API 端点

| 端点 | 方法 | 用途 |
|------|------|------|
| `/api/v1/boards` | GET | 列出所有看板 |
| `/api/v1/boards/{id}` | GET | 获取看板详情 |
| `/api/v1/boards/{id}/blocks` | GET | 获取看板块 |
| `/api/v1/boards/{id}/blocks` | POST | 创建块 |
| `/api/v1/boards/{id}/blocks/{id}` | PATCH | 更新块 |

## 故障排除

| 问题 | 原因 | 解决方案 |
|------|------|---------|
| 无法创建看板 | 权限问题 | 检查用户角色 |
| 性能缓慢 | SQLite 瓶颈 | 切换到 PostgreSQL |
| WebSocket 错误 | 代理配置 | 配置 WebSocket 头 |
| 导入失败 | 格式不匹配 | 检查支持的格式 |

## 总结

Focalboard 提供了一个灵活的项目管理解决方案，具有看板、表格和日历功能。其 Mattermost 集成、模板系统和多种视图类型使其适合各种规模的团队，作为自托管项目追踪工具。


---

## 来源：board2.md

## 简介

Planka 是一款免费开源的项目跟踪工具，提供看板风格的任务管理面板。它提供简洁的界面和实时协作功能，适合各种规模的团队。

## 目录

1. [功能概览](#功能概览)
2. [安装](#安装)
3. [看板配置](#看板配置)
4. [卡片管理](#卡片管理)
5. [标签与过滤](#标签与过滤)
6. [团队协作](#团队协作)
7. [集成](#集成)

## 功能概览

| 功能 | 说明 |
|------|------|
| 看板 | 拖放式卡片管理 |
| 实时更新 | 用户间即时同步 |
| 卡片附件 | 文件上传和链接 |
| 标签 | 颜色编码分类 |
| 截止日期 | 截止时间跟踪 |
| 评论 | 卡片上的团队讨论 |
| Markdown 支持 | 描述中的富文本 |
| 用户角色 | 管理员、经理、成员权限 |

## 安装

### Docker Compose

```yaml
# docker-compose.yml
services:
  planka:
    image: ghcr.io/plankanban/planka:latest
    restart: unless-stopped
    volumes:
      - ./user-avatars:/app/public/user-avatars
      - ./background-images:/app/public/background-images
      - ./attachments:/app/private/attachments
    ports:
      - "1337:1337"
    environment:
      BASE_URL: http://localhost:1337
      DATABASE_URL: postgres://planka:planka@postgres/planka
      SECRET_KEY: your-secret-key-change-me
      DEFAULT_ADMIN_EMAIL: admin@example.com
      DEFAULT_ADMIN_PASSWORD: admin
      DEFAULT_ADMIN_NAME: Admin
    depends_on:
      postgres:
        condition: service_healthy

  postgres:
    image: postgres:15-alpine
    restart: unless-stopped
    volumes:
      - ./pgdata:/var/lib/postgresql/data
    environment:
      POSTGRES_DB: planka
      POSTGRES_USER: planka
      POSTGRES_PASSWORD: planka
    healthcheck:
      test: ["CMD-SHELL", "pg_isready -U planka"]
      interval: 10s
      timeout: 5s
      retries: 5
```

### 环境变量

| 变量 | 说明 | 必需 |
|------|------|------|
| `BASE_URL` | 公共 URL | 是 |
| `DATABASE_URL` | PostgreSQL 连接 | 是 |
| `SECRET_KEY` | 会话加密 | 是 |
| `DEFAULT_ADMIN_EMAIL` | 初始管理员邮箱 | 是 |
| `DEFAULT_ADMIN_PASSWORD` | 初始管理员密码 | 是 |

## 看板配置

### 项目结构

| 层级 | 组件 | 说明 |
|------|------|------|
| 1 | 工作区 | 顶层容器 |
| 2 | 项目 | 相关看板分组 |
| 3 | 看板 | 看板任务面板 |
| 4 | 列表 | 卡片列 |
| 5 | 卡片 | 单个任务 |

### 看板设置

| 设置 | 选项 | 说明 |
|------|------|------|
| 背景 | 颜色、图片 | 看板外观 |
| 可见性 | 私有、项目、公开 | 访问控制 |
| 列表 | 自定义列 | 工作流阶段 |
| 默认列表 | 自动选择 | 新卡片目标 |

### 列表管理

| 操作 | 方法 |
|------|------|
| 添加列表 | 点击列表末尾的 + |
| 重命名列表 | 点击列表标题 |
| 移动列表 | 拖动列表标题 |
| 归档列表 | 列表菜单 > 归档 |
| 复制列表 | 列表菜单 > 复制 |

## 卡片管理

### 卡片属性

| 属性 | 说明 | 必需 |
|------|------|------|
| 标题 | 简要任务描述 | 是 |
| 描述 | 详细信息 | 否 |
| 负责人 | 团队成员 | 否 |
| 标签 | 分类 | 否 |
| 截止日期 | 截止时间 | 否 |
| 附件 | 文件和链接 | 否 |
| 检查清单 | 子任务 | 否 |

### 卡片操作

| 操作 | 方法 |
|------|------|
| 创建 | 点击列表中的 + |
| 编辑 | 点击卡片打开 |
| 移动 | 在列表间拖动 |
| 复制 | 卡片菜单 > 复制 |
| 归档 | 卡片菜单 > 归档 |
| 删除 | 卡片菜单 > 删除 |

### 描述 Markdown

| 语法 | 示例 | 结果 |
|------|------|------|
| 粗体 | `**text**` | **text** |
| 斜体 | `*text*` | *text* |
| 链接 | `[text](url)` | 超链接 |
| 列表 | `- item` | 项目列表 |
| 代码 | `` `code` `` | 行内代码 |
| 代码块 | ` ```code``` ` | 代码块 |

### 检查清单

| 操作 | 方法 |
|------|------|
| 添加检查清单 | 卡片 > 添加 > 检查清单 |
| 添加项目 | 输入并按回车 |
| 切换完成 | 点击复选框 |
| 删除项目 | 悬停时点击 X |
| 删除检查清单 | 检查清单菜单 > 删除 |

## 标签与过滤

### 标签管理

| 操作 | 方法 |
|------|------|
| 创建标签 | 看板菜单 > 标签 |
| 编辑标签 | 点击标签 > 编辑 |
| 设置颜色 | 编辑中的颜色选择器 |
| 删除标签 | 标签菜单 > 删除 |
| 应用到卡片 | 卡片 > 标签 > 选择 |

### 建议标签颜色

| 颜色 | 建议用途 |
|------|----------|
| 红色 | 紧急、阻碍 |
| 橙色 | 高优先级 |
| 黄色 | 中优先级 |
| 绿色 | 低优先级、已完成 |
| 蓝色 | 功能、增强 |
| 紫色 | Bug、问题 |
| 灰色 | 文档 |

### 过滤卡片

| 过滤类型 | 选项 |
|----------|------|
| 按标签 | 选择特定标签 |
| 按负责人 | 选择团队成员 |
| 按截止日期 | 已过期、即将到期、无 |
| 按文本 | 搜索卡片标题 |
| 组合 | 同时使用多个过滤器 |

## 团队协作

### 用户角色

| 角色 | 权限 |
|------|------|
| 管理员 | 完全系统访问、用户管理 |
| 经理 | 项目和看板管理 |
| 成员 | 卡片和评论管理 |
| 查看者 | 只读访问 |

### 用户管理

| 操作 | 路径 |
|------|------|
| 添加用户 | 设置 > 用户 > 添加 |
| 编辑角色 | 用户菜单 > 编辑 |
| 停用 | 用户菜单 > 停用 |
| 重置密码 | 用户菜单 > 重置 |

### 评论

| 功能 | 说明 |
|------|------|
| 添加评论 | 卡片 > 评论 > 输入 |
| 编辑评论 | 评论菜单 > 编辑 |
| 删除评论 | 评论菜单 > 删除 |
| Markdown | 完整 Markdown 支持 |
| 提及 | @用户名 发送通知 |

### 活动日志

| 事件 | 跟踪信息 |
|------|----------|
| 卡片已创建 | 谁、何时、哪个列表 |
| 卡片已移动 | 从哪个列表、到哪个列表 |
| 卡片已编辑 | 什么更改了 |
| 评论已添加 | 谁、内容预览 |
| 附件已添加 | 文件名、上传者 |

## 集成

### Webhooks

| 设置 | 说明 |
|------|------|
| URL | Webhook 端点 |
| 事件 | 哪些事件触发 |
| 格式 | JSON 负载结构 |

### Webhook 事件

| 事件 | 触发条件 |
|------|----------|
| cardCreate | 新卡片已创建 |
| cardUpdate | 卡片已修改 |
| cardMove | 卡片在列表间移动 |
| cardDelete | 卡片已删除 |
| commentCreate | 评论已添加 |

### API 访问

| 端点 | 方法 | 用途 |
|------|------|------|
| `/api/boards` | GET | 列出看板 |
| `/api/boards/:id/cards` | GET | 列出卡片 |
| `/api/cards` | POST | 创建卡片 |
| `/api/cards/:id` | PATCH | 更新卡片 |
| `/api/cards/:id` | DELETE | 删除卡片 |

## 备份与恢复

| 组件 | 位置 | 方法 |
|------|------|------|
| 数据库 | PostgreSQL 卷 | pg_dump |
| 附件 | /app/private/attachments | 文件同步 |
| 头像 | /app/public/user-avatars | 文件同步 |
| 配置 | 环境变量 | 单独记录 |

## 总结

Planka 提供了一个简单直接的看板解决方案，用于项目跟踪和团队协作。其实时更新、灵活的卡片管理和简单的部署方式，使其适合寻求商业项目管理工具自托管替代方案的团队。


---

## 来源：wekan.md

## 简介

Wekan 是一个开源的自托管看板应用。它提供类似 Trello 的功能，同时完全掌控数据。本教程涵盖安装、看板管理、团队工作流程和自动化。

## Wekan 与 Trello、Taiga 对比

| 功能 | Wekan | Trello | Taiga |
|------|-------|--------|-------|
| 自托管 | 是 | 否 | 是 |
| 开源 | 是 | 否 | 是 |
| 看板 | 是 | 是 | 是 |
| Scrum | 部分 | 否 | 是 |
| 泳道 | 是 | 否 | 是 |
| 自定义字段 | 是 | 是（Power-Up） | 是 |
| API | REST | REST | REST |
| 价格 | 免费 | 免费增值 | 免费/付费 |

## 安装

### Docker

```bash
docker run -d \
  --name wekan \
  --restart=unless-stopped \
  -p 8080:8080 \
  -e ROOT_URL=https://boards.example.com \
  -e MONGO_URL=mongodb://wekan-db:27017/wekan \
  wekanteam/wekan
```

### Docker Compose

```yaml
version: '3'
services:
  wekan-db:
    image: mongo:6.0
    container_name: wekan-db
    restart: unless-stopped
    volumes:
      - ./wekan-db:/data/db

  wekan:
    image: wekanteam/wekan
    container_name: wekan
    restart: unless-stopped
    depends_on:
      - wekan-db
    environment:
      - ROOT_URL=https://boards.example.com
      - MONGO_URL=mongodb://wekan-db:27017/wekan
      - WITH_API=true
    ports:
      - "8080:8080"
```

## 核心概念

### 层级结构

| 级别 | 描述 |
|------|------|
| Board（看板） | 项目或工作流程容器 |
| Swimlane（泳道） | 看板内的水平分组 |
| List（列表） | 代表阶段的列 |
| Card（卡片） | 单个任务或项目 |
| Checklist（清单） | 卡片内的子项 |
| Attachment（附件） | 链接到卡片的文件 |

## 看板

### 看板类型

| 类型 | 可见性 | 用例 |
|------|--------|------|
| Private（私有） | 所有者和受邀成员 | 个人任务 |
| Team（团队） | 所有团队成员 | 团队项目 |
| Public（公开） | 任何有链接的人 | 公开协作 |

### 看板模板

| 模板 | 用例 |
|------|------|
| Simple Board | 待办、进行中、已完成 |
| Bug Tracking | 已报告、已确认、进行中、已验证 |
| Project Planning | 待办池、Sprint、评审、完成 |
| Sales Pipeline | 线索、联系、提案、关闭 |

## 列表

### 默认列表结构

| 列表 | 用途 |
|------|------|
| Backlog | 未来的工作项 |
| To Do | 当前 Sprint 项目 |
| In Progress | 进行中的工作 |
| Review | 等待评审 |
| Done | 已完成的项目 |

### 列表操作

| 操作 | 方法 |
|------|------|
| 创建 | 点击"Add a list"按钮 |
| 重命名 | 点击列表标题，编辑 |
| 移动 | 拖动列表头部 |
| 归档 | 列表菜单 > Archive |
| 复制 | 列表菜单 > Copy |

## 卡片

### 卡片属性

| 属性 | 描述 |
|------|------|
| Title | 卡片名称 |
| Description | Markdown 内容 |
| Members | 分配的用户 |
| Labels | 颜色编码的标签 |
| Due Date | 截止日期 |
| Checklist | 子任务列表 |
| Attachments | 文件和图片 |
| Comments | 讨论线程 |
| Custom Fields | 额外数据 |
| Swimlane | 水平泳道 |

### 卡片操作

| 操作 | 快捷键 | 方法 |
|------|--------|------|
| 创建 | N | 点击"Add a card" |
| 编辑 | 点击 | 打开卡片详情 |
| 移动 | 拖动 | 列表或泳道间 |
| 归档 | C | 卡片菜单 |
| 复制 | Ctrl+C | 卡片菜单 > Copy |
| 分配 | M | 点击成员图标 |
| 设置截止日期 | D | 点击截止日期 |
| 添加标签 | L | 点击标签图标 |

### 标签

| 颜色 | 默认用途 |
|------|---------|
| Green（绿色） | 就绪 |
| Yellow（黄色） | 进行中 |
| Orange（橙色） | 阻塞 |
| Red（红色） | 紧急 |
| Purple（紫色） | 评审 |
| Blue（蓝色） | 功能 |
| Sky（天蓝） | Bug |
| Lime（青绿） | 增强 |
| Pink（粉色） | 设计 |
| Black（黑色） | 严重 |

## 泳道

泳道将看板水平分割。

| 用例 | 示例泳道 |
|------|---------|
| 按团队 | 前端、后端、设计 |
| 按优先级 | 高、中、低 |
| 按类别 | Bug、功能、任务 |
| 按人员 | Alice、Bob、Charlie |

## 清单

### 清单功能

| 功能 | 描述 |
|------|------|
| 多个清单 | 每个主题创建单独的清单 |
| 进度条 | 可视化完成百分比 |
| 分配项目 | 分配个别清单项 |
| 截止日期 | 为每个项目设置截止日期 |
| 重新排序 | 拖动重新排序项目 |

## 自定义字段

| 字段类型 | 用例 |
|----------|------|
| Text | 短文本值 |
| Number | 数值 |
| Date | 日期选择器 |
| Dropdown | 从选项中选择 |
| Checkbox | 布尔开关 |
| Currency | 货币值 |

## 自动化

### 卡片操作

| 触发器 | 操作 |
|--------|------|
| 卡片创建 | 分配成员、添加标签 |
| 卡片移动 | 更新截止日期、发送通知 |
| 标签添加 | 移动到特定列表 |
| 截止日期到期 | 标记为逾期、通知 |

### 规则

| 规则类型 | 示例 |
|----------|------|
| 当卡片移到"Done" | 归档卡片 |
| 当添加"Urgent"标签 | 分配给团队负责人 |
| 当设置截止日期 | 添加清单模板 |
| 当清单完成 | 移到"Review" |

## 团队管理

### 角色

| 角色 | 权限 |
|------|------|
| Admin（管理员） | 完全看板控制 |
| Member（成员） | 创建和编辑卡片 |
| Commenter（评论者） | 仅添加评论 |
| Viewer（查看者） | 只读访问 |

### 邀请成员

1. 打开看板设置。
2. 点击"Members"。
3. 输入用户名或邮箱。
4. 选择角色。
5. 发送邀请。

## 导入和导出

### 导入来源

| 来源 | 方法 |
|------|------|
| Trello | JSON 导出导入 |
| Wekan | JSON 导出导入 |
| CSV | CSV 文件导入 |

### 导出格式

| 格式 | 内容 |
|------|------|
| JSON | 完整看板数据 |
| CSV | 带属性的卡片列表 |

## 快捷键

| 快捷键 | 操作 |
|--------|------|
| N | 新建卡片 |
| Enter | 打开卡片 |
| C | 归档卡片 |
| M | 分配成员 |
| L | 添加标签 |
| D | 设置截止日期 |
| F | 过滤卡片 |
| Escape | 关闭对话框 |

## 集成

| 集成 | 方法 |
|------|------|
| Webhooks | 在看板设置中配置 |
| REST API | Bearer 令牌认证 |
| Email | 通过邮件发送卡片 |
| Chat | Mattermost、Rocket.Chat |

## API 使用

### 认证

```bash
# 获取认证令牌
curl -X POST https://boards.example.com/users/login \
  -H "Content-Type: application/json" \
  -d '{"username":"admin","password":"password"}'
```

### 常用端点

| 方法 | 端点 | 描述 |
|------|------|------|
| GET | /api/boards | 列出看板 |
| GET | /api/boards/{id}/lists | 获取看板列表 |
| GET | /api/boards/{id}/cards | 获取看板卡片 |
| POST | /api/boards/{id}/lists/{id}/cards | 创建卡片 |
| PUT | /api/cards/{id} | 更新卡片 |
| DELETE | /api/cards/{id} | 删除卡片 |

## 故障排除

| 问题 | 原因 | 解决方案 |
|------|------|---------|
| 无法加载看板 | MongoDB 连接 | 检查 MONGO_URL |
| 性能缓慢 | 看板过大 | 归档旧卡片 |
| 导入失败 | 格式错误 | 验证 JSON 结构 |
| 通知不工作 | 邮件配置 | 检查 SMTP 设置 |
| API 401 | 令牌无效 | 重新认证 |

## 总结

Wekan 提供了一个功能齐全的看板解决方案，支持自托管。其泳道、自定义字段和自动化规则提供了超越基础看板的功能。REST API 和 webhook 集成使其适合与其他开发工具连接。


---
