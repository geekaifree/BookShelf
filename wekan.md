# Wekan：看板工具教程

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
