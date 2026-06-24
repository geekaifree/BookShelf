# Dashy - 自托管仪表盘指南

## 目录

- [什么是 Dashy](#什么是-dashy)
- [安装](#安装)
- [基本配置](#基本配置)
- [添加服务](#添加服务)
- [小组件](#小组件)
- [主题和外观](#主题和外观)
- [状态检查](#状态检查)
- [认证](#认证)
- [备份和恢复](#备份和恢复)
- [自定义](#自定义)
- [故障排除](#故障排除)

---

## 什么是 Dashy

Dashy 是一个自托管仪表盘，用于组织和访问你的服务。它提供了一个简洁、可定制的界面来管理所有自托管应用。

### 功能

| 功能 | 说明 |
|---------|-------------|
| 服务链接 | 快速访问所有服务 |
| 状态监控 | 检查服务是否在线 |
| 小组件 | 显示来自各种来源的信息 |
| 主题 | 多种内置主题 |
| 认证 | 保护你的仪表盘 |
| 备份/恢复 | 导出和导入配置 |
| 多页面 | 将服务分组到不同区域 |
| 搜索 | 跨服务快速搜索 |
| 键盘快捷键 | 快速导航 |

### 要求

| 要求 | 最低 |
|-------------|---------|
| RAM | 256MB |
| CPU | 1 核 |
| 存储 | 100MB |
| Docker | 20.10+ |
| Node.js | 16+（不使用 Docker 时） |

---

## 安装

### Docker（推荐）

**基本 Docker 运行：**

    docker run -d --name dashy -p 8080:80 -v /path/to/config.yml:/app/user-data/conf.yml --restart unless-stopped lissy93/dashy

**Docker Compose：**

    version: "3"

    services:
      dashy:
        image: lissy93/dashy
        ports:
          - "8080:80"
        volumes:
          - ./config.yml:/app/user-data/conf.yml
        restart: unless-stopped

### 访问 Dashy

安装后，通过以下地址访问：http://localhost:8080

---

## 基本配置

### 配置文件位置

| 方式 | 路径 |
|--------|------|
| Docker 卷 | /app/user-data/conf.yml |
| Node.js | ./user-data/conf.yml |
| 环境变量 | DASHY_CONFIG_DIR |

### 配置结构

    pageInfo:
      title: My Dashboard
      description: My self-hosted services
      logo: https://example.com/logo.png

    sections:
      - name: Media
        icon: fas fa-play
        items:
          - title: Jellyfin
            description: Media server
            icon: hl-jellyfin
            url: https://jellyfin.example.com

    appConfig:
      theme: default
      language: en

### 基本设置

| 设置 | 说明 | 示例 |
|---------|-------------|---------|
| pageInfo.title | 仪表盘标题 | My Dashboard |
| pageInfo.description | 页面描述 | Self-hosted services |
| pageInfo.logo | Logo 图片 URL | URL 或路径 |
| appConfig.theme | 颜色主题 | default |
| appConfig.language | 界面语言 | en |

---

## 添加服务

### 基本服务条目

    sections:
      - name: Media
        items:
          - title: Jellyfin
            description: Media server for movies and TV
            url: https://jellyfin.example.com
            icon: hl-jellyfin

### 服务属性

| 属性 | 说明 | 必填 |
|----------|-------------|----------|
| title | 服务名称 | 是 |
| description | 简要描述 | 否 |
| url | 服务 URL | 是 |
| icon | 服务图标 | 否 |
| target | 链接行为 | 否 |
| tags | 可搜索标签 | 否 |
| statusCheck | 启用可用性检查 | 否 |

### 链接目标

| 值 | 行为 |
|-------|----------|
| sametab | 在同一标签页打开 |
| newtab | 在新标签页打开（默认） |
| modal | 在弹窗中打开 |
| workspace | 在工作区视图中打开 |

### 图标选项

| 类型 | 格式 | 示例 |
|------|--------|---------|
| Font Awesome | fas fa-icon | fas fa-home |
| Simple Icons | si-iconname | si-jellyfin |
| Home Lab Icons | hl-appname | hl-jellyfin |
| Emoji | Unicode emoji | |
| 图片 URL | 完整 URL | https://example.com/icon.png |
| Material | mdi-icon | mdi-home |

### 分区配置

| 属性 | 说明 |
|----------|-------------|
| name | 分区标题 |
| icon | 分区图标 |
| display | 布局：grid、list 或 row |
| collapsed | 初始折叠 |
| items | 服务列表 |

---

## 小组件

小组件显示来自外部来源的动态信息。

### 可用小组件

| 小组件 | 说明 |
|--------|-------------|
| clock | 当前时间 |
| weather | 天气信息 |
| date-time | 日期和时间 |
| search-bar | Web 搜索 |
| notes | 便签 |
| todo-list | 待办清单 |
| website-monitor | 可用性监控 |
| cctv-feed | 摄像头画面 |
| health-checks | Healthchecks.io |
| sports-scores | 体育比分 |
| stock-price | 股票价格 |
| crypto-price | 加密货币价格 |
| news-feed | RSS 新闻 |
| xkcd-comic | 每日 XKCD 漫画 |
| embed | 嵌入外部内容 |
| iframe | 嵌入网页 |

### 添加小组件

    widgets:
      - type: clock
        options:
          timeZone: UTC
          format: 12

      - type: weather
        options:
          APIKey: your-api-key
          city: New York
          units: metric

### 小组件配置

| 属性 | 说明 |
|----------|-------------|
| type | 小组件类型 |
| options | 小组件特定选项 |
| position | 网格位置 |
| width | 小组件宽度 |
| height | 小组件高度 |

---

## 主题和外观

### 内置主题

| 主题 | 说明 |
|-------|-------------|
| default | 简洁的亮色主题 |
| dark | 暗黑模式 |
| colorful | 鲜艳色彩 |
| minimal | 简约设计 |
| nord | Nord 色板 |
| dracula | Dracula 配色 |
| catppuccin | Catppuccin 色彩 |
| solarized | Solarized 亮/暗 |
| matrix | Matrix 风格绿色 |
| cyberpunk | 霓虹赛博朋克风格 |
| retro | 复古计算风格 |

### 设置主题

    appConfig:
      theme: dark

### 自定义 CSS

    appConfig:
      customCss: |
        :root {
          --primary: #ff6b6b;
          --background: #1a1a2e;
          --text: #eee;
        }

### CSS 变量

| 变量 | 说明 |
|----------|-------------|
| --primary | 主题强调色 |
| --background | 背景颜色 |
| --text | 文字颜色 |
| --item-background | 项目背景 |
| --item-border | 项目边框颜色 |
| --nav-background | 导航背景 |

### 布局选项

    appConfig:
      layout: auto
      iconSize: medium
      fontSize: small
      themeColorPrimary: "#ff6b6b"
      themeColorSecondary: "#4ecdc4"

---

## 状态检查

Dashy 可以监控你的服务是否在线。

### 启用状态检查

    appConfig:
      statusCheck: true
      statusCheckInterval: 60
      statusCheckAllowInsecure: false

### 单服务状态检查

    items:
      - title: Jellyfin
        url: https://jellyfin.example.com
        statusCheck: true

### 自定义状态检查 URL

    items:
      - title: API
        url: https://example.com
        statusCheck: true
        statusCheckUrl: https://example.com/api/health

### 状态指示器

| 指示器 | 含义 |
|-----------|---------|
| 绿点 | 服务在线 |
| 红点 | 服务离线 |
| 黄点 | 状态检查中 |
| 无圆点 | 状态检查已禁用 |

---

## 认证

### 内置认证

    appConfig:
      auth:
        users:
          - user: admin
            hash: \$...
            type: admin
          - user: guest
            hash: \$...
            type: guest

### 生成密码哈希

    # 使用 htpasswd
    htpasswd -nbBC 10 "" yourpassword | tr -d ":\n" | sed "s/\$/y/"

    # 使用 Node.js
    node -e "console.log(require('bcryptjs').hashSync('yourpassword', 10))"

### 访问控制

| 类型 | 权限 |
|------|-------------|
| admin | 完全访问，可编辑配置 |
| local | 可查看和使用服务 |
| guest | 只读访问 |

### 使用反向代理的简单认证

    # Nginx 基本认证
    location / {
        auth_basic "Dashboard";
        auth_basic_user_file /etc/nginx/.htpasswd;
        proxy_pass http://localhost:8080;
    }

---

## 备份和恢复

### 导出配置

**方法 1：复制配置文件**

    cp /path/to/config.yml /backup/dashy-config.yml

**方法 2：使用 Dashy UI**

1. 打开 Dashy
2. 进入设置（齿轮图标）
3. 点击导出配置
4. 保存 JSON 文件

### 导入配置

**方法 1：替换配置文件**

    cp /backup/dashy-config.yml /path/to/config.yml
    docker restart dashy

**方法 2：使用 Dashy UI**

1. 打开 Dashy
2. 进入设置
3. 点击导入配置
4. 选择你的 JSON 文件

### 自动备份脚本

    #!/bin/bash

    BACKUP_DIR="/backups/dashy"
    DATE=$(date +%Y-%m-%d)
    CONFIG_PATH="/path/to/config.yml"

    mkdir -p $BACKUP_DIR
    cp $CONFIG_PATH $BACKUP_DIR/config-$DATE.yml

    # 仅保留最近 30 份备份
    ls -t $BACKUP_DIR/config-*.yml | tail -n +31 | xargs rm -f 2>/dev/null

---

## 自定义

### 自定义图标

**使用图标 URL：**

    items:
      - title: My App
        icon: https://example.com/icon.png

**挂载自定义图标：**

    services:
      dashy:
        volumes:
          - ./icons:/app/public/icons

### 自定义字体

    appConfig:
      customCss: |
        @import url('https://fonts.googleapis.com/css2?family=Inter:wght@400;600&display=swap');
        * {
          font-family: 'Inter', sans-serif;
        }

### 键盘快捷键

| 快捷键 | 操作 |
|----------|--------|
| Ctrl + K | 打开搜索 |
| Ctrl + , | 打开设置 |
| Ctrl + E | 切换编辑模式 |
| Ctrl + S | 保存配置 |
| Esc | 关闭弹窗 |

### 多页面设置

    pages:
      - name: Home
        path: /
        sections:
          - name: Quick Access
            items:
              - title: Email
                url: https://mail.example.com

      - name: Media
        path: /media
        sections:
          - name: Streaming
            items:
              - title: Jellyfin
                url: https://jellyfin.example.com

### 环境变量

| 变量 | 说明 |
|----------|-------------|
| DASHY_CONFIG_DIR | 配置目录路径 |
| DASHY_CONFIG_PATH | 配置文件路径 |
| PORT | 服务器端口 |
| HOSTNAME | 服务器主机名 |
| NODE_ENV | Node 环境 |

---

## 故障排除

### 常见问题

| 问题 | 原因 | 解决方案 |
|---------|-------|----------|
| 空白页 | 配置语法错误 | 检查 YAML 语法 |
| 服务加载失败 | URL 错误 | 验证服务 URL |
| 图标缺失 | 图标引用无效 | 检查图标名称 |
| 状态检查失败 | 网络问题 | 检查连接 |
| 更改未保存 | 文件权限 | 检查配置文件权限 |
| 加载缓慢 | 小组件太多 | 减少小组件或优化 |

### 查看日志

    docker logs dashy
    docker logs -f dashy
    docker logs --tail 100 dashy

### 性能问题

| 问题 | 解决方案 |
|-------|----------|
| 首次加载慢 | 减少小组件数量 |
| CPU 占用高 | 禁用状态检查或增加间隔 |
| 内存占用 | 减少项目、优化图片 |
| 网络错误 | 检查 CORS 设置 |

### 恢复默认

    docker stop dashy
    rm /path/to/config.yml
    docker start dashy

---

## 最佳实践

| 实践 | 说明 |
|----------|-------------|
| 组织分区 | 将相关服务分组 |
| 使用图标 | 方便识别服务 |
| 启用状态检查 | 监控服务健康 |
| 定期备份 | 修改前备份配置 |
| 保持简洁 | 不要过度使用小组件 |
| 使用有意义的标题 | 清晰、描述性的服务名称 |
| 添加描述 | 帮助用户理解每个服务 |
| 使用标签 | 方便搜索 |
| 测试链接 | 验证所有 URL 可用 |
| 定期更新 | 保持 Dashy 更新 |
