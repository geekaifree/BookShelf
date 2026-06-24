# Etherpad 教程：协作实时编辑器

## 简介

Etherpad 是一个高度可定制的开源在线编辑器，支持实时协作文档编辑。多个用户可以同时编辑同一文档，带有实时光标、变更追踪和内置聊天功能。

## 系统要求

| 组件 | 最低配置 | 推荐配置 |
|------|---------|---------|
| Node.js | 18.0 | 20 LTS |
| 内存 | 512 MB | 2 GB |
| CPU | 1 核 | 2 核 |
| 磁盘 | 1 GB | 10 GB |
| 数据库 | DirtyDB（内置） | PostgreSQL 或 MySQL |

## 安装

### 使用 Git 和 npm

```bash
git clone https://github.com/ether/etherpad-lite.git
cd etherpad-lite
bin/run.sh
```

### Docker 安装

```bash
docker pull etherpad/etherpad:latest
docker run -d \
  --name etherpad \
  -p 9001:9001 \
  -e ADMIN_PASSWORD=admin123 \
  etherpad/etherpad:latest
```

### Docker Compose 搭配 PostgreSQL

```yaml
version: '3.8'
services:
  etherpad:
    image: etherpad/etherpad:latest
    ports:
      - "9001:9001"
    environment:
      - ADMIN_PASSWORD=admin123
      - DB_TYPE=postgres
      - DB_HOST=db
      - DB_PORT=5432
      - DB_USER=etherpad
      - DB_PASS=etherpad
      - DB_NAME=etherpad
    depends_on:
      - db
    restart: unless-stopped

  db:
    image: postgres:15
    volumes:
      - pg-data:/var/lib/postgresql/data
    environment:
      - POSTGRES_USER=etherpad
      - POSTGRES_PASSWORD=etherpad
      - POSTGRES_DB=etherpad
    restart: unless-stopped

volumes:
  pg-data:
```

## 配置

### settings.json 关键选项

```json
{
  "title": "My Etherpad Instance",
  "favicon": "favicon.ico",
  "ip": "0.0.0.0",
  "port": 9001,
  "showSettingsInAdminPage": true,
  "dbType": "dirty",
  "dbSettings": {
    "filename": "var/dirty.db"
  },
  "defaultPadText": "Welcome to Etherpad!\n\n",
  "padOptions": {
    "noColors": false,
    "showControls": true,
    "showChat": true,
    "showLineNumbers": true,
    "useMonospaceFont": false
  }
}
```

### 数据库选项

| 数据库 | 模块 | 用途 |
|--------|------|------|
| DirtyDB | 内置 | 开发和测试 |
| PostgreSQL | ueberDB2 | 生产部署 |
| MySQL | ueberDB2 | 生产部署 |
| MongoDB | ueberDB2 | 生产部署 |
| SQLite | ueberDB2 | 小型部署 |

## 认证

### 管理员认证方式

| 方式 | 配置 | 用途 |
|------|------|------|
| Basic Auth | `ADMIN_USER` / `ADMIN_PASSWORD` 环境变量 | 简单管理访问 |
| LDAP | `ep_ldapauth` 插件 | 企业目录 |
| OAuth | 各种认证插件 | 单点登录 |
| API Key | 配置中的 `APIKEY` 设置 | 编程访问 |

### 用户认证插件

| 插件 | 协议 | 功能 |
|------|------|------|
| ep_auth_session | 基于会话 | 简单用户管理 |
| ep_ldapauth | LDAP / Active Directory | 目录集成 |
| ep_oauth2 | OAuth 2.0 | SSO 支持 |
| ep_saml | SAML 2.0 | 企业单点登录 |

## Pad 管理

### Pad URL 操作

| 操作 | URL 格式 | 说明 |
|------|---------|------|
| 创建新 pad | `/p/padname` | 首次访问时自动创建 |
| 只读视图 | `/p/padname?showChat=false` | 只读访问 |
| 导出 pad | `/p/padname/export/{format}` | 以各种格式下载 |
| 导入到 pad | `/p/padname/import` | 上传文档到 pad |
| 查看历史 | `/p/padname/timeslider` | 版本历史查看器 |

### 导出格式

| 格式 | 扩展名 | 说明 |
|------|--------|------|
| 纯文本 | `.txt` | 基本文本内容 |
| PDF | `.pdf` | 格式化文档 |
| OpenDocument | `.odt` | 兼容 LibreOffice |
| HTML | `.html` | Web 可用格式 |
| Markdown | `.md` | Markdown 语法 |
| DokuWiki | `.txt` | Wiki 标记 |

## 插件系统

### 基础插件

| 插件 | 用途 | 分类 |
|------|------|------|
| ep_adminpads2 | 从管理面板管理所有 pad | 管理 |
| ep_delete_pad | 从 UI 删除 pad | 管理 |
| ep_headings2 | 标题支持（H1-H6） | 格式 |
| ep_markdown | Markdown 导入和导出 | 格式 |
| ep_tables2 | 表格创建和编辑 | 格式 |
| ep_image_upload | 在 pad 中嵌入图片 | 媒体 |
| ep_comments | 行内评论 | 协作 |
| ep_align | 文本对齐选项 | 格式 |
| ep_font_color | 字体颜色选择器 | 格式 |
| ep_author_neat | 清晰的作者名称显示 | 外观 |

### 安装插件

```bash
# 通过管理面板在 /admin/plugins 安装
# 或通过命令行：
cd etherpad-lite
pnpm run plugins i ep_headings2
```

### 插件配置

```json
{
  "ep_headings2": {
    "defaultHeading": "h2"
  },
  "ep_comments": {
    "defaultShow": true
  }
}
```

## API 参考

### API 端点格式

```
http://localhost:9001/api/1/{functionName}?apikey=YOUR_APIKEY
```

### 常用 API 函数

| 函数 | 参数 | 说明 |
|------|------|------|
| `createPad` | `padID`, `text` | 创建新 pad |
| `getText` | `padID` | 获取 pad 内容 |
| `setText` | `padID`, `text` | 替换 pad 内容 |
| `getHTML` | `padID` | 获取 pad 的 HTML |
| `setHTML` | `padID`, `html` | 从 HTML 设置 pad |
| `getRevisionsCount` | `padID` | 统计修订次数 |
| `getUsers` | `padID` | 列出活跃用户 |
| `deletePad` | `padID` | 删除 pad |
| `listPads` | 无 | 列出所有 pad |
| `getPublicStatus` | `padID` | 检查公开状态 |

### API 使用示例

```bash
# 创建带初始文本的 pad
curl "http://localhost:9001/api/1/createPad?apikey=KEY&padID=test&text=Hello"

# 获取 pad 文本内容
curl "http://localhost:9001/api/1/getText?apikey=KEY&padID=test"

# 设置 pad 文本内容
curl "http://localhost:9001/api/1/setText?apikey=KEY&padID=test&text=Updated"
```

## 实时功能

| 功能 | 说明 |
|------|------|
| 实时光标 | 实时查看其他用户的光标位置 |
| 作者颜色 | 每个作者分配唯一颜色 |
| 聊天 | 内置聊天侧边栏用于沟通 |
| 行号 | 可选的行号显示 |
| 版本历史 | 带可视化时间滑块的完整编辑历史 |
| 撤销/重做 | 每个用户的独立撤销栈 |

## 主题自定义

### 自定义皮肤目录结构

```
etherpad-lite/
  src/
    static/
      skins/
        my-skin/
          index.css
          pad.css
          timeslider.css
```

### CSS 变量主题

| 变量 | 默认值 | 用途 |
|------|--------|------|
| `--bg-color` | `#ffffff` | 页面背景色 |
| `--text-color` | `#333333` | 文字颜色 |
| `--toolbar-bg` | `#f7f7f7` | 工具栏背景 |
| `--link-color` | `#3498db` | 链接颜色 |

## 性能调优

| 设置 | 位置 | 影响 |
|------|------|------|
| 压缩资源 | `settings.json` | 减少页面加载时间 |
| Gzip 压缩 | Nginx 反向代理 | 减少带宽 |
| 数据库 | 使用 PostgreSQL | 更好的并发性 |
| Node.js workers | 集群模式 | 水平扩展 |
| Socket.io 传输 | 优先使用 WebSocket | 更低延迟 |

### Nginx 反向代理配置

```nginx
server {
    listen 80;
    server_name pad.example.com;

    location / {
        proxy_pass http://localhost:9001;
        proxy_http_version 1.1;
        proxy_set_header Upgrade $http_upgrade;
        proxy_set_header Connection "upgrade";
        proxy_set_header Host $host;
        proxy_set_header X-Real-IP $remote_addr;
    }
}
```

## 安全

| 措施 | 配置 |
|------|------|
| HTTPS | 使用 SSL 证书的反向代理 |
| 认证 | 要求登录才能创建 pad |
| 速率限制 | Nginx 或 Express 中间件 |
| Pad 过期 | 自动删除不活跃的 pad |
| 内容安全 | 代理中的 CSP 头 |
| API Key | 安全保管和轮换 API 密钥 |

## 备份脚本

```bash
#!/bin/bash
BACKUP_DIR="/var/backups/etherpad"
DATE=$(date +%Y%m%d)

# 数据库备份
pg_dump -U etherpad etherpad > "$BACKUP_DIR/pads-$DATE.sql"

# 基于文件的备份
tar -czf "$BACKUP_DIR/etherpad-$DATE.tar.gz" \
  /opt/etherpad-lite/var/
```

## 监控

| 指标 | 工具 | 阈值 |
|------|------|------|
| 活跃用户 | API `/stats` 端点 | 每实例 100 以下 |
| 内存使用 | 系统监控 | 80% 以下 |
| 响应时间 | 负载均衡器日志 | 200ms 以下 |
| 错误率 | 日志分析 | 1% 以下 |

## 故障排除

| 问题 | 原因 | 解决方案 |
|------|------|---------|
| 性能缓慢 | 使用 DirtyDB | 切换到 PostgreSQL |
| 连接断开 | Socket.io 代理问题 | 检查 WebSocket 代理配置 |
| 插件加载错误 | 版本不匹配 | 更新插件以匹配版本 |
| 导出失败 | 缺少依赖 | 在服务器上安装 LibreOffice |
| API 返回错误 | API Key 错误 | 验证 settings 中的 `APIKEY` |

## 总结

Etherpad 提供了一个强大的协作编辑平台，支持实时同步。其插件系统、全面的 API 和灵活的配置使其适合教育机构、开发团队以及任何需要实时文档协作的组织。
