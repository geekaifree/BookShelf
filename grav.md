# Grav 教程：扁平文件 CMS

## 简介

Grav 是一个现代的扁平文件内容管理系统，将内容存储在 Markdown 文件中，而不是数据库中。它提供快速的性能、简便的部署和灵活的 Twig 模板系统，无需数据库开销即可构建网站。

## 系统要求

| 组件 | 最低配置 | 推荐配置 |
|------|---------|---------|
| PHP 版本 | 7.3.6 | 8.1+ |
| Web 服务器 | Apache 2.4 | Nginx 1.18+ |
| 内存 | 64 MB | 256 MB |
| 磁盘空间 | 30 MB | 500 MB |
| 扩展 | mbstring, xml, curl, zip | +gd, +intl, +json |

## 安装

### 手动安装

```bash
cd /var/www/html
wget https://getgrav.org/download/core/grav/latest
unzip latest -d grav
mv grav grav-site
chown -R www-data:www-data /var/www/html/grav-site
```

### 安装 Admin 插件

```bash
cd /var/www/html/grav-site
bin/gpm install admin
```

### Docker 安装

```bash
docker run -d \
  --name grav \
  -p 8080:80 \
  -v /path/to/grav:/var/www/html \
  ricardoamaro/gravcms:latest
```

## 目录结构

| 目录 | 用途 |
|------|------|
| `pages/` | 所有内容（Markdown 文件） |
| `themes/` | 已安装的主题 |
| `plugins/` | 已安装的插件 |
| `config/` | 系统和插件配置 |
| `assets/` | 编译后的 CSS、JS、图片 |
| `images/` | 上传的图片 |
| `accounts/` | 用户账户数据 |
| `backup/` | 站点备份 |
| `cache/` | 编译后的 Twig 缓存 |
| `logs/` | 系统日志 |
| `user/` | 用户自定义 |

## 内容结构

### 页面组织

```
pages/
  01.home/
    default.md
  02.about/
    default.md
  03.blog/
    item1/
      item.md
    item2/
      item.md
    blog.md
  04.contact/
    form.md
```

### 页面排序

| 前缀 | 排序顺序 | 导航 |
|------|---------|------|
| `01.` | 第一 | 第一项 |
| `02.` | 第二 | 第二项 |
| `01.` vs `02.` | 数字排序 | 控制菜单顺序 |
| 无前缀 | 默认 | 列表末尾 |

## Frontmatter

Frontmatter 是每个 Markdown 文件顶部的 YAML 元数据。

### 基本 Frontmatter

```yaml
---
title: About Us
menu: About
slug: about
template: default
visible: true
published: true
date: 2024-01-15
---
```

### Frontmatter 字段

| 字段 | 说明 | 示例 |
|------|------|------|
| `title` | 页面标题 | "About Us" |
| `menu` | 导航标签 | "About" |
| `slug` | URL slug | "about" |
| `template` | Twig 模板 | "default" |
| `visible` | 在导航中显示 | `true` |
| `published` | 页面已发布 | `true` |
| `date` | 发布日期 | 2024-01-15 |
| `taxonomy` | 分类和标签 | category: blog |
| `metadata` | SEO 元数据 | description, og tags |
| `order` | 自定义排序 | alphabetical, date |
| `redirect` | URL 重定向 | "/new-page" |

### 分类配置

```yaml
---
taxonomy:
  category: blog
  tag: [php, grav, tutorial]
---
```

## Markdown 内容

### 标准 Markdown

```markdown
# 标题 1
## 标题 2
### 标题 3

**粗体文本** 和 *斜体文本*

- 无序列表项
- 另一项

1. 有序列表项
2. 另一项

[链接文本](https://example.com)

![图片替代文字](image.jpg)
```

### 代码块

````markdown
```php
<?php echo "Hello World"; ?>
```
````

### 表格

```markdown
| 表头 1 | 表头 2 | 表头 3 |
|--------|--------|--------|
| 单元格 1 | 单元格 2 | 单元格 3 |
| 单元格 4 | 单元格 5 | 单元格 6 |
```

## 主题

### 热门主题

| 主题 | 风格 | 功能 |
|------|------|------|
| Quark | 简洁、现代 | 默认主题，响应式 |
| Learn2 | 文档 | 侧边栏导航，搜索 |
| Helium | 博客 | 多作者，分类 |
| Flavor | 作品集 | 网格布局，画廊 |
| Bookworm | 文档 | 章节导航 |

### 安装主题

```bash
# 通过 CLI
bin/gpm install quark

# 通过管理面板
# 导航到 Themes > Add
```

### 主题结构

```
themes/
  my-theme/
    blueprints.yaml     # 主题元数据
    my-theme.yaml       # 主题配置
    css/                # 样式表
    js/                 # JavaScript
    images/             # 主题图片
    templates/          # Twig 模板
      default.html.twig
      blog.html.twig
      partials/
        base.html.twig
        navigation.html.twig
```

### 自定义主题模板

```twig
{# templates/default.html.twig #}
{% extends 'partials/base.html.twig' %}

{% block content %}
  <h1>{{ page.title }}</h1>
  {{ page.content|raw }}
{% endblock %}
```

## 插件

### 基础插件

| 插件 | 用途 | 分类 |
|------|------|------|
| Admin | Web 管理界面 | 管理 |
| Form | 表单构建器 | 内容 |
| Email | 邮件发送 | 通信 |
| Markdown Notices | 样式化通知 | 内容 |
| Error | 自定义错误页面 | 导航 |
| Problems | 站点诊断 | 管理 |
| Login | 用户认证 | 安全 |
| Flex Objects | 自定义内容类型 | 内容 |

### 安装插件

```bash
# 通过 CLI
bin/gpm install form

# 通过管理面板
# 导航到 Plugins > Add
```

## 表单插件

### 表单定义（在页面 frontmatter 中）

```yaml
---
title: Contact
form:
  name: contact
  fields:
    - name: name
      label: Name
      type: text
      validate:
        required: true

    - name: email
      label: Email
      type: email
      validate:
        required: true

    - name: message
      label: Message
      type: textarea
      validate:
        required: true

  buttons:
    - type: submit
      value: Send
      classes: btn btn-primary

  process:
    - email:
        from: "{{ form.value.email }}"
        to: admin@example.com
        subject: "Contact Form"
    - message: Thank you for contacting us!
    - display: thankyou
---
```

### 表单字段类型

| 字段类型 | 说明 | 验证选项 |
|---------|------|---------|
| `text` | 单行文本 | required, pattern |
| `email` | 邮箱输入 | required, 邮箱格式 |
| `textarea` | 多行文本 | required, minlength |
| `select` | 下拉菜单 | required, options |
| `checkbox` | 复选框 | required |
| `radio` | 单选按钮 | required |
| `file` | 文件上传 | accept, maxsize |
| `hidden` | 隐藏值 | - |
| `date` | 日期选择器 | required |

## 配置

### 系统配置（config/system.yaml）

```yaml
pages:
  theme: quark
  markdown:
    extra: true
  process:
    markdown: true
    twig: false

cache:
  enabled: true
  driver: auto
  prefix: g

session:
  enabled: true
  timeout: 1800
```

### 站点配置（config/site.yaml）

```yaml
title: My Grav Site
default_lang: en
author:
  name: Site Owner
  email: owner@example.com
metadata:
  description: "Site description for SEO"
taxonomies:
  - category
  - tag
```

## 性能

| 优化 | 配置 | 影响 |
|------|------|------|
| Twig 缓存 | `cache.enabled: true` | 更快渲染 |
| Gzip | Web 服务器配置 | 更小传输 |
| OPcache | `php.ini` | 更快 PHP 执行 |
| CDN | 外部 CDN | 全球分发 |
| 图片优化 | Grav 图片处理 | 更小图片 |
| 资源管道 | CSS/JS 压缩 | 更少请求 |

### 资源管道

```twig
{# 在基础模板中 #}
{% do assets.addCss('theme://css/custom.css') %}
{% do assets.addJs('theme://js/app.js', {group: 'bottom'}) %}
{{ assets.css() }}
{{ assets.js() }}
```

## CLI 命令

| 命令 | 用途 |
|------|------|
| `bin/grav install` | 安装依赖 |
| `bin/gpm install <package>` | 安装主题或插件 |
| `bin/gpm update` | 更新所有包 |
| `bin/gpm selfupgrade` | 升级 Grav 核心 |
| `bin/grav clear-cache` | 清除所有缓存 |
| `bin/grav sandbox` | 检查系统要求 |

## 备份与迁移

| 组件 | 方法 | 说明 |
|------|------|------|
| 页面 | 文件复制 | 整个 `pages/` 目录 |
| 配置 | 文件复制 | `config/` 目录 |
| 主题 | `bin/gpm` 或文件复制 | 可重新安装 |
| 插件 | `bin/gpm` 或文件复制 | 可重新安装 |
| 用户数据 | 文件复制 | `user/` 目录 |
| 完整备份 | zip 整个目录 | 完整站点备份 |

### 迁移步骤

1. 复制整个 Grav 目录到新服务器
2. 设置 Web 服务器文档根目录
3. 配置 PHP 版本
4. 设置文件权限
5. 清除缓存：`bin/grav clear-cache`

## 安全

| 措施 | 实现方式 |
|------|---------|
| HTTPS | Web 服务器 SSL 配置 |
| Admin 插件 | 强管理员密码 |
| 文件权限 | 限制写入访问 |
| PHP 版本 | 保持 PHP 更新 |
| 插件更新 | 定期 `bin/gpm update` |
| 备份 | 定期备份 |
| 登录保护 | 管理端速率限制 |

## 故障排除

| 问题 | 原因 | 解决方案 |
|------|------|---------|
| 500 错误 | PHP 版本 | 检查 PHP 兼容性 |
| 空白页 | Twig 错误 | 启用调试模式 |
| 样式缺失 | 资源管道 | 清除缓存 |
| 页面 404 | URL 重写 | 检查 .htaccess 或 nginx 配置 |
| 加载缓慢 | 缓存禁用 | 在配置中启用缓存 |

## 总结

Grav 提供了一个快速、灵活的扁平文件 CMS，消除了数据库开销，同时保持强大的内容管理能力。其基于 Markdown 的内容、Twig 模板和丰富的插件生态系统，使其成为寻求轻量但功能丰富的 CMS 的开发者的理想选择。
