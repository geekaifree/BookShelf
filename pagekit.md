# Pagekit 内容管理系统

使用 Pagekit 构建和管理网站的完整指南，这是一个基于现代 PHP 和 Vue.js 的模块化 CMS。

## 目录

- [安装](#installation)
- [仪表板](#dashboard)
- [页面](#pages)
- [博客](#blog)
- [菜单](#menus)
- [组件](#widgets)
- [主题](#themes)
- [扩展](#extensions)
- [用户](#users)
- [权限](#permissions)
- [SEO](#seo)
- [备份](#backup)

---

## 安装

### 要求

| 要求 | 最低版本 | 推荐 |
|------|----------|------|
| PHP | 7.2+ | 8.1+ |
| 数据库 | MySQL 5.7+ / SQLite 3.8+ / PostgreSQL 9.4+ | MySQL 8.0 |
| Web 服务器 | Apache 2.4+ / Nginx 1.14+ | Nginx |
| Composer | 2.0+ | 最新 |
| PHP 扩展 | PDO, Mbstring, Tokenizer, XML, JSON | 所有列出 |

### 通过 Composer 安装

```bash
composer create-project pagekit/pagekit mysite
cd mysite
```

### 手动安装

1. 从 https://pagekit.com 下载最新版本。
2. 解压到 Web 服务器的文档根目录。
3. 确保 Web 服务器可以写入 `storage` 和 `tmp` 目录。

```bash
chmod -R 775 storage tmp
chown -R www-data:www-data storage tmp
```

### Web 安装器

1. 在浏览器中访问你的站点 URL。
2. 安装器检查系统要求。
3. 配置数据库连接：

| 字段 | 示例 |
|------|------|
| Database Type | MySQL |
| Host | localhost |
| Database Name | pagekit |
| Username | pagekit_user |
| Password | secure_password |

4. 创建管理员账号：

| 字段 | 描述 |
|------|------|
| Site Title | 你的网站名称 |
| Username | 管理员用户名 |
| Password | 管理员密码 |
| Email | 管理员邮箱 |

5. 点击 `Install` 完成设置。

### Web 服务器配置

**Apache（已包含 .htaccess）：**
```apache
<VirtualHost *:80>
    ServerName mysite.com
    DocumentRoot /var/www/mysite
    <Directory /var/www/mysite>
        AllowOverride All
        Require all granted
    </Directory>
</VirtualHost>
```

**Nginx：**
```nginx
server {
    listen 80;
    server_name mysite.com;
    root /var/www/mysite;
    index index.php;

    location / {
        try_files $uri $uri/ /index.php?$query_string;
    }

    location ~ \.php$ {
        fastcgi_pass unix:/var/run/php/php8.1-fpm.sock;
        fastcgi_param SCRIPT_FILENAME $document_root$fastcgi_script_name;
        include fastcgi_params;
    }
}
```

### 安装后

| 任务 | 方法 |
|------|------|
| 移除安装器 | 删除 `install` 目录 |
| 设置权限 | 限制 `storage` 和 `tmp` 访问 |
| 配置缓存 | 在 System 设置中启用缓存 |
| 设置时区 | Settings > System > Timezone |

---

## 仪表板

仪表板是管理 Pagekit 站点的中心枢纽。

### 仪表板概述

| 区域 | 用途 |
|------|------|
| Site Info | 显示站点名称、版本和状态 |
| Recent Activity | 显示最新内容变更 |
| Quick Actions | 常用任务快捷方式 |
| System Updates | 可用更新通知 |

### 导航

主管理侧边栏包含：

| 菜单项 | 描述 |
|--------|------|
| Dashboard | 概览和快捷操作 |
| Site | 页面、博客、菜单、组件 |
| Extensions | 管理已安装扩展 |
| System | 用户、设置、存储、信息 |

### 系统设置

| 设置 | 描述 |
|------|------|
| Site Title | 浏览器标签和标题中显示的名称 |
| Site Description | 默认 meta 描述 |
| Application | 调试模式、维护模式 |
| Cache | 启用/禁用页面缓存 |
| Timezone | 日期显示的服务器时区 |
| Locale | 默认语言 |

### 维护模式

在更新期间启用维护模式以限制访问：

1. 前往 `System > Settings > Application`。
2. 切换 `Maintenance Mode`。
3. 管理员仍可访问仪表板。
4. 访客看到维护页面。

---

## 页面

页面是构成网站结构的静态内容。

### 创建页面

1. 前往 `Site > Pages`。
2. 点击 `Add Page`。
3. 输入页面标题。
4. 配置页面设置。
5. 使用编辑器添加内容。
6. 点击 `Save` 或 `Save and Close`。

### 页面设置

| 设置 | 描述 |
|------|------|
| Title | 页面标题和浏览器标签标题 |
| Slug | URL 友好的标识符 |
| Status | 草稿、已发布或未发布 |
| Access | 谁可以查看页面 |
| Redirect | 重定向 URL（可选） |
| Layout | 使用的模板布局 |

### 内容编辑器

Pagekit 提供支持 Markdown 的富文本编辑器。

| 功能 | 描述 |
|------|------|
| Rich Text | 所见即所得编辑工具栏 |
| Markdown | 直接 Markdown 输入 |
| HTML | 原始 HTML 编辑 |
| Media | 插入图片和文件 |
| Widgets | 嵌入组件内容 |

### 页面模板

| 模板 | 描述 |
|------|------|
| Default | 标准页面布局 |
| Full Width | 无侧边栏 |
| Sidebar | 带侧边栏的内容 |
| Landing | 自定义着陆页布局 |

### 管理页面

| 操作 | 方法 |
|------|------|
| 编辑 | 点击列表中的页面标题 |
| 复制 | 选择页面 > Actions > Duplicate |
| 删除 | 选择页面 > Actions > Delete |
| 重排序 | 在页面列表中拖放 |
| 批量操作 | 选择多个页面 > 选择操作 |

### 页面路由

为页面配置 URL 模式：

| 设置 | 示例 |
|------|------|
| Default | `/about` |
| Custom slug | `/about-us` |
| Nested | `/company/about` |
| Redirect | 将 `/old-page` 重定向到 `/new-page` |

---

## 博客

博客模块提供完整的博客平台。

### 创建博客文章

1. 前往 `Site > Blog`。
2. 点击 `Add Post`。
3. 输入文章标题和内容。
4. 配置文章设置。
5. 点击 `Publish` 或 `Save as Draft`。

### 文章设置

| 设置 | 描述 |
|------|------|
| Title | 文章标题 |
| Slug | URL 友好的标识符 |
| Content | 文章正文（富文本或 Markdown） |
| Excerpt | 列表视图的简短摘要 |
| Status | 草稿、已发布、已排期 |
| Publish Date | 发布日期和时间 |
| Categories | 分配到分类 |
| Tags | 添加标签用于筛选 |
| Access | 谁可以查看文章 |

### 分类

将文章组织到分类：

| 操作 | 方法 |
|------|------|
| 创建分类 | Blog > Categories > Add |
| 分配分类 | 在文章设置中选择分类 |
| 编辑分类 | 分类列表 > Edit |
| 删除分类 | 分类列表 > Delete |

### 标签

标签为文章提供灵活的标记：

| 功能 | 描述 |
|------|------|
| 自动创建 | 首次使用时创建标签 |
| 多标签 | 每篇文章可分配多个标签 |
| 标签云 | 在前端显示热门标签 |
| 筛选 | 按标签筛选文章 |

### 博客设置

| 设置 | 描述 |
|------|------|
| Posts per page | 列表页每页文章数 |
| Date format | 日期显示格式 |
| Comments | 启用/禁用评论 |
| RSS feed | 启用 RSS 输出 |
| Share buttons | 社交分享选项 |

### 博客显示

配置博客在前端的显示方式：

| 选项 | 描述 |
|------|------|
| List view | 以列表显示文章摘要 |
| Grid view | 以卡片网格显示文章 |
| Full posts | 显示完整文章内容 |
| Excerpts | 显示摘要加阅读更多链接 |

---

## 菜单

菜单定义网站的导航结构。

### 创建菜单

1. 前往 `Site > Menus`。
2. 点击 `Add Menu`。
3. 输入菜单名称。
4. 添加菜单项。
5. 将菜单分配到主题位置。

### 菜单项

| 类型 | 描述 | 示例 |
|------|------|------|
| URL | 链接到任意 URL | `https://example.com` |
| Page | 链接到现有页面 | About, Contact |
| Blog | 链接到博客列表 | 博客首页 |
| Category | 链接到博客分类 | News, Updates |
| Separator | 菜单中的视觉分隔线 | --- |

### 添加菜单项

1. 在菜单编辑器中点击 `Add Item`。
2. 选择项目类型。
3. 配置项目：

| 设置 | 描述 |
|------|------|
| Title | 菜单中显示的文字 |
| URL | 目标 URL 或页面 |
| Icon | 可选图标类 |
| Target | 同一窗口或新标签 |
| Access | 谁可以看到此项 |

### 菜单结构

通过拖放组织项目：

```
Home
About
  Our Team
  History
Services
  Consulting
  Development
Blog
Contact
```

### 菜单位置

将菜单分配到主题位置：

| 位置 | 典型位置 |
|------|----------|
| `logo` | 站点头部 logo 区域 |
| `menu` | 主导航栏 |
| `offcanvas` | 移动端滑出菜单 |
| `footer` | 页脚导航 |

### 菜单设置

| 设置 | 描述 |
|------|------|
| Dropdown | 为子项启用下拉 |
| Dropdown style | 悬停或点击打开 |
| Active trail | 高亮活动页面的父项 |
| Max depth | 限制嵌套层级 |

---

## 组件

组件是放置在主题位置的可复用内容块。

### 创建组件

1. 前往 `Site > Widgets`。
2. 点击 `Add Widget`。
3. 选择组件类型。
4. 配置组件。
5. 分配到主题位置。
6. 点击 `Save`。

### 组件类型

| 类型 | 描述 | 用途 |
|------|------|------|
| Text | 自定义文本和 HTML | 页脚内容、通知 |
| Menu | 显示导航菜单 | 侧边栏导航 |
| System | 系统生成内容 | 登录、搜索 |
| Custom | HTML/JS 代码块 | 嵌入、脚本 |

### 组件设置

| 设置 | 描述 |
|------|------|
| Title | 组件标题 |
| Type | 组件内容类型 |
| Position | 显示的主题位置 |
| Access | 谁可以看到组件 |
| Pages | 仅在特定页面显示 |

### 组件位置

可用位置取决于活动主题：

| 位置 | 典型用途 |
|------|----------|
| `sidebar` | 右或左侧边栏 |
| `footer` | 页面页脚区域 |
| `header` | 主内容上方 |
| `content_top` | 主内容之前 |
| `content_bottom` | 主内容之后 |

### 页面特定组件

控制哪些页面显示组件：

| 设置 | 描述 |
|------|------|
| All pages | 组件在所有地方显示 |
| Selected pages | 选择特定页面 |
| Exclude pages | 除选定外都显示 |

---

## 主题

主题控制网站的视觉外观和布局。

### 安装主题

1. 前往 `System > Extensions`。
2. 点击 `Add Extensions`。
3. 浏览或搜索主题。
4. 点击 `Install`。
5. 前往 `System > Settings > Site`。
6. 选择新主题。

### 主题设置

| 设置 | 描述 |
|------|------|
| Logo | 上传站点 logo |
| Favicon | 浏览器标签图标 |
| Primary Color | 主强调色 |
| Font | 默认正文字体 |
| Layout | 页面布局样式 |
| Custom CSS | 附加 CSS 样式 |

### 主题位置

主题定义可放置组件和菜单位置：

| 位置名称 | 位置 |
|----------|------|
| `logo` | 站点头部 |
| `menu` | 导航栏 |
| `hero` | Hero/Banner 区域 |
| `sidebar` | 左或右侧边栏 |
| `content` | 主内容区域 |
| `footer` | 页面页脚 |
| `copyright` | 版权栏 |

### 创建子主题

自定义主题而不修改原始主题：

```
themes/
  my-child/
    index.php          # Theme registration
    theme.json         # Theme configuration
    templates/         # Override templates
    styles/            # Custom styles
```

### 主题配置 (theme.json)

```json
{
  "name": "my-child",
  "version": "1.0.0",
  "parent": "theme-flavor",
  "positions": {
    "sidebar": "Sidebar",
    "footer": "Footer"
  }
}
```

---

## 扩展

扩展为 Pagekit 安装添加功能。

### 安装扩展

| 方式 | 方法 |
|------|------|
| Marketplace | System > Extensions > Add Extensions |
| Upload | System > Extensions > Upload ZIP |
| Composer | `composer require vendor/package` |

### 管理扩展

| 操作 | 方法 |
|------|------|
| 启用 | Extensions > Toggle on |
| 禁用 | Extensions > Toggle off |
| 更新 | Extensions > Update（如有） |
| 卸载 | Extensions > Remove |

### 热门扩展类别

| 类别 | 示例 |
|------|------|
| SEO | Sitemap 生成器、meta 标签管理器 |
| Forms | 联系表单、调查 |
| E-commerce | 购物车、产品目录 |
| Social | 社交媒体 feed、分享按钮 |
| Analytics | Google Analytics、访客追踪 |
| Security | 双因素认证、防火墙 |

### 扩展设置

每个扩展有自己的配置：

1. 前往 `System > Extensions`。
2. 点击扩展旁的齿轮图标。
3. 根据需要配置设置。
4. 点击 `Save`。

### 开发自定义扩展

扩展结构：

```
packages/
  vendor/
    extension-name/
      index.php           # Extension entry point
      src/                # PHP source files
      views/              # Templates
      assets/             # CSS, JS, images
      extension.json      # Extension metadata
```

---

## 用户

管理用户账号和角色。

### 用户管理

| 操作 | 方法 |
|------|------|
| 查看用户 | System > Users |
| 添加用户 | Users > Add User |
| 编辑用户 | 点击用户名 > Edit |
| 删除用户 | 选择用户 > Actions > Delete |
| 封禁用户 | 选择用户 > Actions > Block |

### 用户字段

| 字段 | 描述 |
|------|------|
| Username | 唯一登录名 |
| Email | 用户邮箱 |
| Password | 账号密码 |
| Display Name | 公开显示名称 |
| Avatar | 头像 |
| Roles | 分配的角色 |
| Status | 活动或封禁 |

### 用户角色

| 角色 | 默认权限 |
|------|----------|
| Administrator | 所有功能完全访问 |
| Editor | 创建、编辑、发布内容 |
| Author | 创建和编辑自己的内容 |
| Subscriber | 只读前端访问 |

### 创建自定义角色

1. 前往 `System > Users > Roles`。
2. 点击 `Add Role`。
3. 输入角色名称。
4. 选择权限。
5. 点击 `Save`。

### 用户注册

| 设置 | 描述 |
|------|------|
| Allow registration | 启用公开注册 |
| Email verification | 需要邮箱确认 |
| Default role | 分配给新注册的角色 |
| Approval | 需要管理员批准 |

---

## 权限

控制对内容和功能的访问。

### 权限系统

| 级别 | 描述 |
|------|------|
| Global | 系统范围权限 |
| Component | 每模块权限 |
| Content | 每项访问控制 |

### 全局权限

| 权限 | 描述 |
|------|------|
| `system: access admin area` | 访问管理仪表板 |
| `system: manage settings` | 更改系统设置 |
| `system: manage extensions` | 安装/移除扩展 |
| `system: manage storage` | 管理文件存储 |

### 内容权限

| 设置 | 选项 |
|------|------|
| Public | 任何人都可查看 |
| Registered | 仅登录用户 |
| Author | 仅内容作者 |
| Custom | 特定角色或用户 |

### 分配权限

1. 前往 `System > Users > Permissions`。
2. 选择角色。
3. 勾选/取消每个组件的权限。
4. 点击 `Save`。

### 权限矩阵示例

| 权限 | Admin | Editor | Author | Subscriber |
|------|-------|--------|--------|------------|
| 访问管理 | 是 | 是 | 是 | 否 |
| 管理页面 | 是 | 是 | 否 | 否 |
| 编辑自己的内容 | 是 | 是 | 是 | 否 |
| 发布内容 | 是 | 是 | 否 | 否 |
| 管理用户 | 是 | 否 | 否 | 否 |
| 管理设置 | 是 | 否 | 否 | 否 |

---

## SEO

为搜索引擎优化你的 Pagekit 站点。

### 基本 SEO 设置

| 设置 | 位置 | 描述 |
|------|------|------|
| Site Title | System > Settings | 出现在搜索结果中 |
| Meta Description | System > Settings | 默认页面描述 |
| Permalink Structure | System > Settings | 内容 URL 格式 |
| Sitemap | Extensions | 自动生成的 XML sitemap |

### URL 结构

配置简洁 URL：

| 格式 | 示例 |
|------|------|
| Default | `/index.php?id=123` |
| Clean | `/about` |
| Blog | `/blog/post-title` |
| Category | `/blog/category/news` |

### 页面级 SEO

每页和文章都有 SEO 字段：

| 字段 | 描述 |
|------|------|
| Title Tag | 浏览器标签和搜索结果标题 |
| Meta Description | 搜索结果中显示的摘要 |
| Slug | URL 路径组件 |
| Canonical URL | 重复内容的首选 URL |
| Robots | Index/noindex, follow/nofollow |

### SEO 最佳实践

| 实践 | 实施方式 |
|------|----------|
| 独特标题 | 每页有不同标题 |
| Meta 描述 | 150-160 字符摘要 |
| 简洁 URL | 描述性、关键词丰富的 slug |
| 标题层级 | 正确的 H1, H2, H3 结构 |
| 图片 alt 文本 | 描述性 alt 属性 |
| 内部链接 | 相关内容之间链接 |
| Sitemap | 向搜索引擎提交 XML sitemap |

### SEO 扩展

| 扩展 | 功能 |
|------|------|
| SEO Pack | Meta 标签、sitemap、robots.txt |
| Google Analytics | 访客追踪集成 |
| Schema Markup | 富摘要的结构化数据 |
| Redirect Manager | 301/302 重定向管理 |

---

## 备份

通过定期备份保护站点数据。

### 备份内容

| 组件 | 位置 | 方法 |
|------|------|------|
| Database | MySQL/PostgreSQL/SQLite | 数据库导出 |
| Files | `/storage` 目录 | 文件复制 |
| Configuration | `/config` 目录 | 文件复制 |
| Extensions | `/packages` 目录 | 文件复制 |
| Themes | `/themes` 目录 | 文件复制 |

### 数据库备份

**MySQL:**
```bash
mysqldump -u username -p pagekit_db > backup_$(date +%Y%m%d).sql
```

**PostgreSQL:**
```bash
pg_dump -U username pagekit_db > backup_$(date +%Y%m%d).sql
```

**SQLite:**
```bash
cp storage/database.sqlite backup_$(date +%Y%m%d).sqlite
```

### 文件备份

```bash
tar -czf pagekit_files_$(date +%Y%m%d).tar.gz \
  storage/ \
  config/ \
  packages/ \
  themes/
```

### 自动备份脚本

```bash
#!/bin/bash
BACKUP_DIR="/backups/pagekit"
DATE=$(date +%Y%m%d_%H%M%S)

# Database backup
mysqldump -u root -p pagekit_db | gzip > $BACKUP_DIR/db_$DATE.sql.gz

# File backup
tar -czf $BACKUP_DIR/files_$DATE.tar.gz /var/www/pagekit/storage

# Cleanup old backups (keep 30 days)
find $BACKUP_DIR -type f -mtime +30 -delete
```

### 恢复流程

| 步骤 | 命令 |
|------|------|
| 1. 恢复数据库 | `mysql -u root -p pagekit_db < backup.sql` |
| 2. 恢复文件 | `tar -xzf files_backup.tar.gz -C /var/www/pagekit` |
| 3. 清除缓存 | 删除 `storage/cache` 内容 |
| 4. 验证 | 浏览站点并检查功能 |

### 备份计划

| 频率 | 保留 | 用途 |
|------|------|------|
| 每天 | 7 天 | 经常变更的活跃站点 |
| 每周 | 30 天 | 标准站点 |
| 每月 | 12 个月 | 归档 |
| 更新前 | 永久 | 更新前安全网 |

### 备份验证

定期通过恢复到暂存环境测试备份：

1. 设置暂存服务器。
2. 恢复最新备份。
3. 验证所有内容正确加载。
4. 测试关键功能（登录、表单、导航）。
5. 记录发现的任何问题。
