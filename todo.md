# Vikunja：任务管理教程

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
