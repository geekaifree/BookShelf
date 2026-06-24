# Statamic：扁平文件 CMS 教程

## 简介

Statamic 是一个基于 Laravel 构建的现代扁平文件内容管理系统。它使用 Markdown 和 YAML 文件存储内容，而非数据库。本教程涵盖安装、内容建模以及使用 Statamic 构建完整网站。

## 为什么选择扁平文件 CMS

| 特性 | 扁平文件（Statamic） | 数据库 CMS |
|------|---------------------|-----------|
| 存储 | YAML/Markdown 文件 | MySQL/PostgreSQL |
| 设置 | 无需数据库 | 需要数据库配置 |
| 版本控制 | Git 友好的内容 | 需要导出工具 |
| 性能 | 文件读取，可选缓存 | 基于查询 |
| 托管 | 任何 PHP 主机 | 需要数据库主机 |
| 备份 | 复制文件 | 导出数据库 |

## 系统要求

| 组件 | 最低要求 | 推荐配置 |
|------|---------|---------|
| PHP | 8.1 | 8.2 或 8.3 |
| Composer | 2.x | 最新版 |
| Node.js | 16+ | 18+ LTS |
| Web 服务器 | Apache/Nginx | Nginx + PHP-FPM |
| 扩展 | mbstring、xml、curl、zip | 所有 PHP 扩展 |

## 安装

### 全新安装

```bash
composer create-project statamic/statamic my-site
cd my-site
php artisan statamic:install
```

### 添加到现有 Laravel 项目

```bash
composer require statamic/cms
php artisan statamic:install
```

## 目录结构

| 目录 | 用途 |
|------|------|
| content/ | 所有页面、条目、分类法 |
| resources/ | 视图（Antlers 模板）、CSS、JS |
| public/ | 网站根目录、资源文件 |
| config/ | 站点和插件配置 |
| users/ | 用户账户（YAML 文件） |
| storage/ | 日志、缓存、临时文件 |
| app/ | 自定义 PHP 代码、控制器 |

## 内容架构

### 集合（Collections）

集合将相关内容条目分组。

| 集合类型 | 用例 | 示例 |
|----------|------|------|
| Blog（博客） | 基于时间的文章 | 文章、新闻 |
| Pages（页面） | 静态页面 | 关于、联系 |
| Products（产品） | 电商商品 | 目录条目 |
| Events（活动） | 基于日期的内容 | 会议、聚会 |

### 创建集合

1. 运行 `php please make:collection blog`
2. 编辑 `content/collections/blog.yaml`
3. 定义蓝图字段
4. 以 Markdown 文件形式添加条目

### 条目结构

| 字段 | 格式 | 用途 |
|------|------|------|
| title | String | 条目标题 |
| slug | String | URL 安全标识符 |
| date | Date | 发布日期 |
| author | String | 内容作者 |
| template | String | Antlers 模板名称 |
| body | Markdown | 主要内容 |

### 蓝图（Blueprints）

蓝图定义内容条目的结构。

| 字段类型 | 用例 |
|----------|------|
| text | 标题、名称、短字符串 |
| textarea | 描述、摘要 |
| markdown | 富文本内容 |
| select | 下拉选项 |
| assets | 图片和文件上传 |
| entries | 与其他条目的关联 |
| date | 日期和时间选择器 |
| toggle | 布尔标志 |
| bard | 基于块的富文本编辑器 |
| repeater | 可重复的字段组 |

## 使用 Antlers 模板

Antlers 是 Statamic 的原生模板引擎。

### 基本语法

| 语法 | 用途 |
|------|------|
| {{ title }} | 输出变量 |
| {{ if title }}...{{ /if }} | 条件块 |
| {{ entries }}...{{ /entries }} | 遍历集合 |
| {{ partial "header" }} | 包含局部模板 |
| {{ yield "content" }} | 区域输出 |
| {{ slot }} | 组件插槽 |

### 模板层级

| 模板 | 范围 | 优先级 |
|------|------|--------|
| default.antlers.html | 所有页面的后备模板 | 最低 |
| blog.antlers.html | 博客列表 | 中等 |
| blog/show.antlers.html | 单篇博客文章 | 较高 |
| _entry.antlers.html | 集合级覆盖 | 最高 |

## 导航

### 创建导航

| 导航 | 用途 |
|------|------|
| main | 主站导航 |
| footer | 页脚链接 |
| sidebar | 侧边栏菜单 |

## 分类法（Taxonomies）

分类法对跨集合的条目进行分类。

| 分类法 | 示例 |
|--------|------|
| tags | 技术、设计、新闻 |
| categories | 博客文章分类 |
| colors | 产品颜色选项 |

## 资源与媒体

| 功能 | 描述 |
|------|------|
| Asset Containers | 映射到存储磁盘的文件夹 |
| Glide 集成 | 实时图片处理 |
| Alt Text | 无障碍图片描述 |
| Focal Point | 智能裁剪中心 |

## 表单

| 表单类型 | 用例 |
|----------|------|
| Contact（联系） | 用户咨询 |
| Newsletter（通讯） | 邮件订阅 |
| Search（搜索） | 内容搜索 |

## 用户与权限

| 角色 | 默认权限 |
|------|---------|
| Super Admin（超级管理员） | 完全访问 |
| Editor（编辑） | 编辑和发布内容 |
| Author（作者） | 创建和编辑自己的内容 |
| Viewer（查看者） | 只读访问 |

## 多语言支持

| 功能 | 配置 |
|------|------|
| Locales（区域设置） | 在 config/statamic/sites.php 中定义 |
| Content（内容） | 每个区域设置的 Markdown 文件 |
| Routing（路由） | 自动区域前缀 |
| Fallback（回退） | 翻译缺失时显示默认区域内容 |

## 部署

| 方法 | 步骤 |
|------|------|
| Git | 推送内容和模板，在服务器上拉取 |
| CI/CD | 构建资源、运行迁移、清除缓存 |
| 手动 | 通过 FTP/SFTP 上传文件 |

### 生产环境清单

| 任务 | 命令 |
|------|------|
| 缓存配置 | php artisan config:cache |
| 缓存路由 | php artisan route:cache |
| 缓存视图 | php artisan view:cache |
| 静态缓存 | 在 config/statamic/static_caching.php 中启用 |

## 性能优化

| 技术 | 收益 |
|------|------|
| 静态缓存 | 提供预渲染的 HTML |
| CDN | 全球分发资源 |
| 图片优化 | 减小文件大小 |
| Stache 缓存 | 加速内容索引 |

## 总结

Statamic 将扁平文件存储的简洁性与 Laravel 的强大功能相结合。其 Antlers 模板系统、蓝图机制和 Git 友好的内容管理方式，使其非常适合希望完全掌控内容和基础设施、又不想承担传统数据库开销的开发者。
