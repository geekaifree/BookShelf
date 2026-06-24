# 使用 Kanboard 看板工具

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
