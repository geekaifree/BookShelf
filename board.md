# Focalboard 教程：项目管理看板

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
