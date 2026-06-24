# CryptPad：加密协作编辑

## 简介

CryptPad 是一个开源的端到端加密协作编辑平台。它提供实时文档编辑、电子表格、演示文稿和其他生产力工具，同时确保服务器永远无法访问未加密的内容。本教程涵盖设置、功能和用法。

## 架构

| 组件 | 技术 | 用途 |
|------|------|------|
| 后端 | Node.js | API 和 WebSocket 服务器 |
| 数据库 | MongoDB/SQLite | 元数据存储 |
| 存储 | 基于文件 | 加密文档存储 |
| 前端 | JavaScript | 协作编辑 UI |
| 加密 | NaCl | 端到端加密 |

## 安装

### Docker Compose

```yaml
version: "3"
services:
  cryptpad:
    image: cryptpad/cryptpad:latest
    ports:
      - "3000:3000"
      - "3001:3001"
    volumes:
      - cryptpad_data:/cryptpad/data
      - cryptpad_blob:/cryptpad/blob
      - cryptpad_block:/cryptpad/block
    environment:
      - CPAD_MAIN_DOMAIN=https://cryptpad.example.com
      - CPAD_CONF=/cryptpad/config/config.js
    restart: unless-stopped
volumes:
  cryptpad_data:
  cryptpad_blob:
  cryptpad_block:
```

### Docker Run

```bash
docker run -d \
  -p 3000:3000 \
  -p 3001:3001 \
  -v cryptpad_data:/cryptpad/data \
  -v cryptpad_blob:/cryptpad/blob \
  -e CPAD_MAIN_DOMAIN=https://cryptpad.example.com \
  cryptpad/cryptpad:latest
```

## 文档类型

### 可用应用

| 应用 | 描述 | 文件扩展名 |
|------|------|-----------|
| Rich Text | 协作文档编辑器 | .doc |
| Spreadsheet | 协作电子表格 | .sheet |
| Presentation | 幻灯片编辑器 | .slides |
| Kanban | 任务管理看板 | .board |
| Form | 数据收集表单 | .form |
| Code | 语法高亮编辑器 | .code |
| Diagram | 流程图和图表工具 | .draw |
| Markdown | Markdown 编辑器 | .md |
| Poll | 日程投票 | .poll |
| Whiteboard | 协作绘画 | .whiteboard |
| File Upload | 加密文件存储 | 各种 |

## 端到端加密

### 工作原理

| 步骤 | 描述 |
|------|------|
| 1 | 用户创建或打开文档 |
| 2 | 加密密钥在浏览器中生成 |
| 3 | 密钥嵌入 URL 中（# 之后） |
| 4 | 内容在发送到服务器前加密 |
| 5 | 服务器仅存储加密的 blob |
| 6 | 其他用户使用 URL 中的密钥解密 |

### 密钥结构

```
https://cryptpad.example.com/doc/#/2/edit/
  <channel_key>/
  <key>/
  <version>
```

`#` 之后的密钥永远不会发送到服务器。只有拥有完整 URL 的用户才能解密内容。

### 安全属性

| 属性 | 描述 |
|------|------|
| 零知识 | 服务器无法读取内容 |
| 密钥在 URL 中 | 密钥从不传输到服务器 |
| 客户端加密 | 加密/解密在浏览器中进行 |
| 无密钥托管 | 密钥丢失无法恢复 |

## 协作功能

### 实时协作

| 功能 | 描述 |
|------|------|
| 在线状态 | 查看谁在线 |
| 光标跟踪 | 查看协作者的光标 |
| 即时同步 | 更改实时出现 |
| 冲突解决 | 自动合并同时编辑 |
| 聊天 | 每个文档内置聊天 |

### 共享选项

| 方法 | 描述 | 安全性 |
|------|------|--------|
| 仅查看 | 只读访问 | 带查看密钥的链接 |
| 编辑访问 | 完全编辑权限 | 带编辑密钥的链接 |
| 嵌入 | 嵌入其他页面 | 仅查看 iframe |
| 密码保护 | 附加访问控制 | 链接加密码 |

## 用户账户

### 账户功能

| 功能 | 访客 | 注册用户 |
|------|------|----------|
| 创建文档 | 是 | 是 |
| 持久存储 | 否（基于会话） | 是 |
| 云盘组织 | 否 | 是 |
| 存储配额 | 有限 | 可配置 |
| 团队功能 | 否 | 是 |
| 个人资料 | 否 | 是 |

### 注册

1. 导航到 CryptPad 实例。
2. 点击"Sign Up"。
3. 输入用户名和密码。
4. 完成注册。

注意：密码无法恢复。没有密码重置功能。

## 云盘组织

### 云盘结构

```
My Drive/
  Documents/
    Meeting Notes.doc
    Project Plan.sheet
  Media/
    Photos/
    Files/
  Shared with Me/
    Team Docs/
    Client Files/
  Trash/
```

### 组织功能

| 功能 | 描述 |
|------|------|
| 文件夹 | 创建嵌套文件夹结构 |
| 标签 | 添加彩色标签 |
| 模板 | 保存文档模板 |
| 回收站 | 恢复已删除文档 |
| 搜索 | 跨云盘全文搜索 |

## 团队

### 团队功能

| 功能 | 描述 |
|------|------|
| 共享云盘 | 团队可访问的文档空间 |
| 成员 | 邀请团队成员 |
| 角色 | Owner、admin、member |
| 聊天 | 团队范围通信 |
| 置顶 | 置顶重要文档 |

### 创建团队

1. 导航到侧边栏中的 Teams。
2. 点击"Create a Team"。
3. 设置团队名称和头像。
4. 通过用户名邀请成员。
5. 将文档添加到团队云盘。

## 表单

### 创建表单

| 字段类型 | 描述 |
|----------|------|
| Text Input | 单行文本 |
| Text Area | 多行文本 |
| Radio | 单选 |
| Checkbox | 多选 |
| Dropdown | 选择菜单 |
| Date | 日期选择器 |
| Email | 邮箱输入 |
| Number | 数字输入 |
| Scale | 评分量表 |

### 表单设置

| 设置 | 描述 |
|------|------|
| 匿名回复 | 无用户跟踪 |
| 每人一次 | 限制一次提交 |
| 截止日期 | 日期后自动关闭 |
| 通知 | 新回复时发邮件 |

## 管理

### 管理面板

访问 `/admin` 的管理面板。

| 部分 | 描述 |
|------|------|
| General | 实例设置 |
| User Management | 管理注册用户 |
| Storage | 监控存储使用 |
| Network | 性能设置 |
| Security | 访问控制 |
| Customize | 品牌和外观 |

### 实例配置

```javascript
// config/config.js
module.exports = {
    httpAddress: '0.0.0.0',
    httpPort: 3000,
    httpUnsafeOrigin: 'https://cryptpad.example.com',
    httpSafeOrigin: 'https://cryptpad-csp.example.com',
    adminKeys: ['your-admin-public-key'],
    defaultStorageLimit: 100 * 1024 * 1024, // 100MB
    maxUploadSize: 50 * 1024 * 1024, // 50MB
};
```

### 存储限制

| 用户类型 | 默认限制 | 可配置 |
|----------|----------|--------|
| 访客 | 5 MB | 是 |
| 注册用户 | 50 MB | 是 |
| 高级用户 | 1 GB+ | 是 |
| 管理员 | 无限 | 不适用 |

## API 访问

### REST API

```bash
# 获取文档信息
curl https://cryptpad.example.com/api/document?channel=CHANNEL_ID

# 获取存储配额
curl -H "Authorization: Bearer TOKEN" \
  https://cryptpad.example.com/api/quota
```

## 备份

### 备份组件

| 组件 | 位置 | 方法 |
|------|------|------|
| 文档 | `/cryptpad/blob/` | 文件复制 |
| 元数据 | `/cryptpad/data/` | 文件复制 |
| 数据库 | MongoDB 导出 | mongodump |
| 配置 | `/cryptpad/config/` | 文件复制 |

### 备份脚本

```bash
#!/bin/bash
BACKUP_DIR="/backups/cryptpad/$(date +%Y%m%d)"
mkdir -p "$BACKUP_DIR"

# 备份数据
docker cp cryptpad:/cryptpad/data "$BACKUP_DIR/data"
docker cp cryptpad:/cryptpad/blob "$BACKUP_DIR/blob"
docker cp cryptpad:/cryptpad/block "$BACKUP_DIR/block"

# 备份配置
docker cp cryptpad:/cryptpad/config "$BACKUP_DIR/config"

# 清理旧备份
find /backups/cryptpad -maxdepth 1 -mtime +30 -exec rm -rf {} \;
```

## 反向代理

### Nginx 配置

```nginx
server {
    listen 443 ssl;
    server_name cryptpad.example.com;

    ssl_certificate /etc/letsencrypt/live/cryptpad.example.com/fullchain.pem;
    ssl_certificate_key /etc/letsencrypt/live/cryptpad.example.com/privkey.pem;

    location / {
        proxy_pass http://localhost:3000;
        proxy_set_header Host $host;
        proxy_set_header X-Real-IP $remote_addr;
        proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
        proxy_set_header X-Forwarded-Proto $scheme;
        proxy_http_version 1.1;
        proxy_set_header Upgrade $http_upgrade;
        proxy_set_header Connection "upgrade";
    }
}
```

## 自定义

### 品牌

| 设置 | 描述 |
|------|------|
| 实例名称 | 显示名称 |
| Logo | 自定义 logo 图片 |
| 配色方案 | 主色和强调色 |
| 页脚 | 自定义页脚文本 |
| 隐私政策 | 自定义隐私页面 |
| 服务条款 | 自定义条款页面 |

## 移动支持

### 响应式设计

CryptPad 的 Web 界面是响应式的，可在移动浏览器上工作。

| 功能 | 移动支持 |
|------|----------|
| 文档编辑 | 是 |
| 电子表格编辑 | 是 |
| 演示文稿查看 | 是 |
| 文件管理 | 是 |
| 实时协作 | 是 |

## 限制

| 限制 | 描述 |
|------|------|
| 无密码恢复 | 密码丢失意味着数据丢失 |
| 无离线编辑 | 需要活动连接 |
| 文件大小限制 | 可配置的上传限制 |
| 搜索限制 | 仅客户端搜索 |

## 总结

CryptPad 提供端到端加密的协作编辑，具有零知识架构。服务器永远看不到未加密的内容，因为所有加密都在浏览器中进行。它支持文档、电子表格、演示文稿、表单和其他生产力工具。使用 Docker 部署，作为商业协作平台的隐私保护替代方案。
