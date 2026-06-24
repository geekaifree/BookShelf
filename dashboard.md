# 使用 Dashy 搭建仪表盘

## 简介

Dashy 是一个高度可定制的自托管仪表盘应用。它提供了一个基于 Web 的界面，用于组织链接、监控服务和展示小部件。

### 什么是 Dashy？

Dashy 是一个个人仪表盘，帮助您将 Web 服务、书签和系统状态集中在一个地方。

| 特性 | 描述 |
|------|------|
| 可定制布局 | 排列小部件和分区 |
| 状态监控 | 检查服务可用性 |
| 主题 | 多个内置主题 |
| 小部件 | 系统信息、天气等 |
| 认证 | 可选登录保护 |

### 为什么要自托管仪表盘？

| 好处 | 描述 |
|------|------|
| 集中访问 | 所有服务的单一入口 |
| 状态概览 | 一目了然的服务健康状况 |
| 定制化 | 根据工作流程定制 |
| 隐私 | 无第三方跟踪 |

## 安装

### 前置要求

| 要求 | 版本 |
|------|------|
| Node.js | 18 或更高 |
| Docker | 20.10 或更高（可选） |
| npm | 8 或更高 |

### Docker 安装

```bash
docker run -d \
  --name dashy \
  -p 8080:8080 \
  -v /path/to/conf.yml:/app/user-data/conf.yml \
  lissy93/dashy
```

### Docker Compose

```yaml
version: '3'
services:
  dashy:
    image: lissy93/dashy
    container_name: dashy
    ports:
      - "8080:8080"
    volumes:
      - ./conf.yml:/app/user-data/conf.yml
    restart: unless-stopped
```

### 手动安装

```bash
git clone https://github.com/Lissy93/dashy.git
cd dashy
yarn install
yarn build
yarn start
```

## 配置

### 配置文件结构

```yaml
pageInfo:
  title: My Dashboard
  description: Personal dashboard
  navLinks:
    - title: GitHub
      path: https://github.com

sections:
  - name: Services
    displayData:
      cols: 3
    items:
      - title: Portainer
        description: Container management
        icon: hl-portainer
        url: https://portainer.example.com
        statusCheck: true
```

### 基本配置选项

| 部分 | 用途 |
|------|------|
| `pageInfo` | 页面标题、描述、导航链接 |
| `sections` | 仪表盘项目分组 |
| `appConfig` | 全局应用设置 |
| `theme` | 外观样式 |

### 分区配置

```yaml
sections:
  - name: Media
    icon: fas fa-play
    displayData:
      cols: 2
      collapsed: false
      itemSize: medium
    items:
      - title: Plex
        url: https://plex.example.com
        icon: hl-plex
```

| 分区属性 | 描述 |
|----------|------|
| `name` | 分区标题 |
| `icon` | 分区图标 |
| `cols` | 列数 |
| `collapsed` | 默认折叠 |
| `itemSize` | 项目显示大小 |

## 添加项目

### 项目配置

```yaml
items:
  - title: Service Name
    description: Brief description
    icon: hl-servicename
    url: https://service.example.com
    target: newtab
    statusCheck: true
    tags:
      - media
      - streaming
```

| 项目属性 | 描述 |
|----------|------|
| `title` | 显示名称 |
| `description` | 悬停文本 |
| `icon` | 图标标识符 |
| `url` | 服务 URL |
| `target` | 打开方式 |
| `statusCheck` | 启用健康检查 |
| `tags` | 可搜索标签 |

### 图标来源

| 来源 | 前缀 | 示例 |
|------|------|------|
| HomeLab 图标 | `hl-` | `hl-portainer` |
| Font Awesome | `fas fa-` | `fas fa-home` |
| Material Design | `mdi-` | `mdi-server` |
| Emoji | 无 | `:rocket:` |
| URL | https:// | 自定义图片 URL |

## 状态监控

### 健康检查

```yaml
items:
  - title: Service
    url: https://service.example.com
    statusCheck: true
    statusCheckUrl: https://service.example.com/health
    statusCheckAllowInsecure: true
```

| 状态 | 颜色 | 含义 |
|------|------|------|
| 在线 | 绿色 | 服务正常响应 |
| 离线 | 红色 | 服务无响应 |
| 未知 | 灰色 | 未配置检查 |

### 状态检查选项

| 选项 | 描述 |
|------|------|
| `statusCheck` | 启用基本检查 |
| `statusCheckUrl` | 自定义端点 |
| `statusCheckAllowInsecure` | 允许自签名证书 |
| `statusCheckHeaders` | 自定义请求头 |

## 主题

### 内置主题

| 主题 | 风格 |
|------|------|
| Default | 简洁、现代 |
| Night | 暗色模式 |
| Dracula | 紫色暗色主题 |
| Nord | 冷色调蓝色主题 |
| Pastel | 柔和色彩 |
| Minimal | 简约、干净 |

### 自定义主题

```yaml
appConfig:
  theme: default
  customCss: |
    :root {
      --primary: #4a90d9;
      --background: #1a1a2e;
    }
```

### CSS 变量

| 变量 | 控制 |
|------|------|
| `--primary` | 强调色 |
| `--background` | 页面背景 |
| `--item-background` | 项目背景 |
| `--text-color` | 文本颜色 |
| `--heading-text` | 分区标题 |

## 小部件

### 可用小部件

| 小部件 | 描述 |
|--------|------|
| `clock` | 当前时间 |
| `weather` | 天气预报 |
| `system-info` | CPU、内存使用率 |
| `search-bar` | Web 搜索 |
| `notes` | 便签 |
| `todo-list` | 任务列表 |
| `iframe` | 嵌入外部页面 |

### 小部件配置

```yaml
sections:
  - name: Widgets
    widgets:
      - type: clock
        options:
          format: 24
          showDate: true

      - type: weather
        options:
          API_KEY: your-key
          city: London
          units: metric

      - type: system-info
        options:
          cpu: true
          memory: true
          disk: true
```

### 自定义小部件

```yaml
- type: iframe
  options:
    url: https://grafana.example.com/d/abc/dashboard
    height: 400
    width: 100%
```

## 认证

### 基本认证

```yaml
appConfig:
  auth:
    enableGuestAccess: false
    users:
      - user: admin
        hash: "$2b$12$..."
        type: admin
      - user: guest
        hash: "$2b$12$..."
        type: guest
```

### 生成密码哈希

```bash
npm install -g bcrypt-cli
bcrypt-cli "your-password"
```

### 访问级别

| 级别 | 权限 |
|------|------|
| Admin | 完全访问，编辑模式 |
| Guest | 只读访问 |
| None | 无访问权限 |

## 多页面支持

### 页面配置

```yaml
pages:
  - name: Home
    path: /
    conf: home.yml

  - name: Services
    path: /services
    conf: services.yml

  - name: Monitoring
    path: /monitoring
    conf: monitoring.yml
```

## 备份和恢复

### 导出配置

```bash
# 复制配置文件
cp /path/to/conf.yml ./backup-conf.yml

# 或从 UI 导出
# Settings → Export Config
```

### 导入配置

```bash
# 从备份恢复
cp ./backup-conf.yml /path/to/conf.yml

# 或从 UI 导入
# Settings → Import Config
```

## Web 服务器配置

### Nginx 反向代理

```nginx
server {
    listen 80;
    server_name dashboard.example.com;

    location / {
        proxy_pass http://localhost:8080;
        proxy_set_header Host $host;
        proxy_set_header X-Real-IP $remote_addr;
    }
}
```

### 使用 Let's Encrypt 配置 SSL

```bash
sudo apt install certbot python3-certbot-nginx
sudo certbot --nginx -d dashboard.example.com
```

## 性能

### 优化技巧

| 技巧 | 描述 |
|------|------|
| 启用缓存 | 配置浏览器缓存 |
| 压缩图片 | 优化图标大小 |
| 限制小部件 | 只使用需要的小部件 |
| 懒加载 | 为分区启用懒加载 |

## 移动端支持

### 响应式设计

Dashy 自动适配移动屏幕：

| 屏幕大小 | 布局 |
|----------|------|
| 桌面 | 多列网格 |
| 平板 | 响应式网格 |
| 手机 | 单列 |

### PWA 支持

Dashy 可以作为 Progressive Web App 安装到移动设备上。

## 总结

| 功能 | 配置 |
|------|------|
| 分区 | 将项目分组 |
| 项目 | 指向服务的链接 |
| 小部件 | 系统信息、天气等 |
| 主题 | 外观定制 |
| 状态检查 | 监控服务健康 |
| 认证 | 可选登录保护 |
