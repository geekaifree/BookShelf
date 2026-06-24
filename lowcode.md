# 低代码

> 本文档整合了以下源文件：lowcode.md

---

## 来源：lowcode.md

## 简介

Budibase 是一款开源低代码平台，让你无需大量编码即可快速构建业务应用。它提供可视化界面来创建内部工具、管理面板、仪表板和 CRUD 应用，内置数据库、自动化和用户管理。

Budibase 面向开发者和非开发者设计，使创建生产就绪的应用从数周缩短到数分钟。

## 为什么使用 Budibase？

| 特性 | Budibase | Retool | Appsmith | OutSystems |
|------|----------|--------|---------|------------|
| 费用 | 免费/OSS | $10/用户/月 | 免费/OSS | $1,500+/月 |
| 开源 | 是 | 否 | 是 | 否 |
| 自托管 | 是 | 是 | 是 | 是 |
| 内置数据库 | 是 | 否 | 否 | 是 |
| 自动化 | 是 | 是 | 是 | 是 |
| 自定义插件 | 是 | 有限 | 是 | 有限 |
| SSO/SAML | 是 | 付费 | 是 | 是 |

## 核心功能

| 功能 | 描述 |
|------|------|
| 可视化构建器 | 拖拽式 UI 创建 |
| 内置数据库 | 集成数据存储 |
| 外部数据源 | 连接现有数据库 |
| 自动化 | 工作流自动化 |
| 用户管理 | 角色和权限 |
| API 生成 | 自动生成 REST API |
| 自定义插件 | 扩展功能 |
| 自托管 | 完全控制部署 |

## 安装

### Docker 部署

```bash
# 创建目录
mkdir -p /opt/budibase/data

# 运行 Budibase
docker run -d \
  --name budibase \
  -p 80:80 \
  -v /opt/budibase/data:/data \
  budibase/budibase
```

### Docker Compose

```yaml
version: '3'
services:
  budibase:
    image: budibase/budibase
    container_name: budibase
    restart: unless-stopped
    ports:
      - "80:80"
    volumes:
      - ./data:/data
```

### Kubernetes

```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: budibase
spec:
  replicas: 1
  selector:
    matchLabels:
      app: budibase
  template:
    metadata:
      labels:
        app: budibase
    spec:
      containers:
      - name: budibase
        image: budibase/budibase
        ports:
        - containerPort: 80
```

### 系统要求

| 要求 | 最低 | 推荐 |
|------|------|------|
| CPU | 2 核 | 4 核 |
| 内存 | 2GB | 8GB |
| 存储 | 10GB | 50GB |
| 网络 | 端口 80 | SSL 反向代理 |

## 快速上手

### 初始设置

| 步骤 | 操作 |
|------|------|
| 1 | 访问 Web 界面 |
| 2 | 创建管理员账户 |
| 3 | 创建第一个应用 |
| 4 | 选择数据源 |
| 5 | 设计 UI |

### 应用创建流程

| 步骤 | 描述 |
|------|------|
| 1 | 定义数据模型 |
| 2 | 创建页面 |
| 3 | 添加组件 |
| 4 | 配置绑定 |
| 5 | 设置自动化 |
| 6 | 发布应用 |

## 数据源

### 内置数据库

Budibase 包含内置数据库用于快速原型设计。

| 功能 | 描述 |
|------|------|
| 表 | 结构化数据存储 |
| 关系 | 链接表 |
| 类型 | 文本、数字、日期、布尔等 |
| 索引 | 性能优化 |
| 验证 | 数据完整性规则 |

### 外部数据源

| 数据库 | 支持 |
|-------|------|
| PostgreSQL | 是 |
| MySQL | 是 |
| MongoDB | 是 |
| SQL Server | 是 |
| Oracle | 是 |
| REST API | 是 |
| Google Sheets | 是 |
| Airtable | 是 |
| CouchDB | 是 |
| Elasticsearch | 是 |

### 数据类型映射

| Budibase 类型 | PostgreSQL | MySQL | MongoDB |
|-------------|-----------|-------|---------|
| Text | varchar | VARCHAR | String |
| Number | integer | INT | Number |
| Boolean | boolean | BOOLEAN | Boolean |
| Date | timestamp | DATETIME | Date |
| JSON | jsonb | JSON | Object |
| File | text | TEXT | String |

## UI 组件

### 布局组件

| 组件 | 用途 |
|------|------|
| 容器 | 分组元素 |
| 区域 | 页面区域 |
| 行 | 水平布局 |
| 列 | 垂直布局 |
| 卡片 | 内容卡片 |
| 表单 | 输入表单 |
| 表格 | 数据网格 |
| 循环 | 遍历数据 |

### 输入组件

| 组件 | 用途 |
|------|------|
| 文本字段 | 文本输入 |
| 数字字段 | 数字输入 |
| 日期选择器 | 日期选择 |
| 下拉选择 | 单选下拉 |
| 多选 | 多选 |
| 复选框 | 布尔切换 |
| 单选组 | 单选 |
| 文件上传 | 文件附件 |
| 富文本 | 所见即所得编辑器 |

### 显示组件

| 组件 | 用途 |
|------|------|
| 文本 | 显示文本 |
| 标题 | 区域标题 |
| 图片 | 显示图片 |
| 图标 | 显示图标 |
| 表格 | 数据网格 |
| 图表 | 数据可视化 |
| Markdown | 富内容 |
| HTML | 自定义 HTML |

### 操作组件

| 组件 | 用途 |
|------|------|
| 按钮 | 触发操作 |
| 链接 | 导航 |
| 导航 | 菜单链接 |
| 菜单 | 下拉菜单 |

## 数据绑定

### 绑定类型

| 绑定 | 语法 | 描述 |
|------|------|------|
| 当前用户 | `{{ Current User.email }}` | 用户属性 |
| 状态 | `{{ State.page }}` | 应用状态 |
| URL | `{{ URL.id }}` | URL 参数 |
| 数据 | `{{ Employee.name }}` | 数据上下文 |
| 辅助函数 | `{{ Helpers.uuid }}` | 工具函数 |

### 常用绑定

| 绑定 | 描述 |
|------|------|
| `{{ Current User.email }}` | 当前用户邮箱 |
| `{{ Current User.role }}` | 当前用户角色 |
| `{{ State.selectedRow }}` | 选中的表行 |
| `{{ URL.query.search }}` | URL 查询参数 |
| `{{ Form.value.name }}` | 表单输入值 |
| `{{ Repeater.index }}` | 循环索引 |

## 自动化

### 自动化触发器

| 触发器 | 描述 |
|-------|------|
| 行已创建 | 新数据添加 |
| 行已更新 | 数据已更改 |
| 行已删除 | 数据已移除 |
| 应用操作 | 按钮点击 |
| Cron | 定时任务 |
| Webhook | 外部 API 调用 |
| 应用已加载 | 页面打开 |

### 自动化步骤

| 步骤 | 描述 |
|------|------|
| 查询行 | 从表获取数据 |
| 创建行 | 添加新数据 |
| 更新行 | 修改现有数据 |
| 删除行 | 移除数据 |
| 发送邮件 | 邮件通知 |
| 外部请求 | 调用外部 API |
| 过滤 | 条件逻辑 |
| JavaScript | 自定义代码 |
| Bash | 系统命令 |

### 自动化示例

| 步骤 | 配置 |
|------|------|
| 1 | 触发器：订单表中行已创建 |
| 2 | 过滤：状态 = "新建" |
| 3 | 查询行：获取客户信息 |
| 4 | 发送邮件：通知客户 |
| 5 | 更新行：设置状态为"处理中" |

## 用户管理

### 用户角色

| 角色 | 权限 |
|------|------|
| 管理员 | 完全系统访问 |
| 高级用户 | 应用构建 + 使用 |
| 应用用户 | 使用已发布应用 |
| 自定义 | 定义特定权限 |

### 角色配置

| 权限 | 选项 |
|------|------|
| 读取 | 查看数据 |
| 写入 | 创建/更新数据 |
| 删除 | 移除数据 |
| 执行 | 运行自动化 |
| 管理员 | 完全访问 |

## 自定义插件

### 插件类型

| 类型 | 描述 |
|------|------|
| 组件 | 自定义 UI 组件 |
| 数据源 | 新数据连接 |
| 自动化 | 自定义自动化步骤 |

### 创建插件

| 步骤 | 操作 |
|------|------|
| 1 | 创建插件目录 |
| 2 | 定义 schema.json |
| 3 | 实现组件 |
| 4 | 打包为 zip |
| 5 | 上传到 Budibase |

## API

### 自动生成 API

Budibase 自动为所有数据表生成 REST API。

| 端点 | 方法 | 描述 |
|------|------|------|
| `/api/tables/:id` | GET | 列出行 |
| `/api/tables/:id/:rowId` | GET | 获取单行 |
| `/api/tables/:id` | POST | 创建行 |
| `/api/tables/:id/:rowId` | PUT | 更新行 |
| `/api/tables/:id/:rowId` | DELETE | 删除行 |

### API 认证

```bash
# 获取 API 密钥
curl -X POST https://your-app.com/api/auth \
  -H "Content-Type: application/json" \
  -d '{"username":"admin","password":"password"}'

# 使用 API 密钥
curl -H "Authorization: Bearer YOUR_API_KEY" \
  https://your-app.com/api/tables/employees
```

## 部署

### 导出/导入

| 操作 | 描述 |
|------|------|
| 导出应用 | 下载应用为 JSON |
| 导入应用 | 从 JSON 上传应用 |
| 克隆应用 | 复制现有应用 |

### 生产部署

| 考量 | 建议 |
|------|------|
| SSL | 使用 Let's Encrypt 反向代理 |
| 数据库 | 使用外部 PostgreSQL |
| 备份 | 定期自动备份 |
| 监控 | 健康检查和告警 |

## 故障排除

| 问题 | 原因 | 解决方案 |
|------|------|---------|
| 应用无法加载 | 构建错误 | 检查应用预览 |
| 数据未保存 | 验证错误 | 检查字段设置 |
| 性能缓慢 | 数据集过大 | 添加分页 |
| 插件错误 | 版本不兼容 | 更新插件 |

## 更多资源

| 资源 | URL |
|------|-----|
| 官方网站 | budibase.com |
| GitHub | github.com/Budibase/budibase |
| 文档 | docs.budibase.com |
| 社区 | community.budibase.com |


---
