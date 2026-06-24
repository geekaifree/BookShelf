# Bolt CMS：构建扁平文件内容管理系统

## 简介

Bolt CMS（也称为 Bolt）是一个轻量级的开源内容管理系统，专为开发者和内容编辑者设计。它使用扁平文件方式进行配置，同时将内容存储在数据库中。本教程涵盖安装、内容建模、主题和日常使用。

## 架构

| 组件 | 技术 | 用途 |
|------|------|------|
| 后端 | Symfony (PHP) | 应用框架 |
| 存储 | SQLite/MySQL/PostgreSQL | 内容存储 |
| 模板 | Twig | HTML 渲染 |
| 管理 | 内置面板 | 内容管理 |
| API | REST 端点 | 无头访问 |

## 安装

### Composer

```bash
composer create-project bolt/project mysite
cd mysite
php bin/console bolt:setup
```

### Docker

```yaml
version: "3"
services:
  bolt:
    image: bolt/core:latest
    ports:
      - "80:80"
    volumes:
      - ./bolt-data:/var/www/html
    depends_on:
      - database
  database:
    image: mariadb:10
    environment:
      MYSQL_ROOT_PASSWORD: root
      MYSQL_DATABASE: bolt
      MYSQL_USER: bolt
      MYSQL_PASSWORD: bolt
```

### Web 服务器配置

```nginx
server {
    listen 80;
    server_name mysite.example.com;
    root /var/www/html/public;
    index index.php;

    location / {
        try_files $uri $uri/ /index.php?$query_string;
    }

    location ~ \.php$ {
        fastcgi_pass php:9000;
        fastcgi_param SCRIPT_FILENAME $document_root$fastcgi_script_name;
        include fastcgi_params;
    }
}
```

## 内容类型

内容类型定义内容的结构。它们在 YAML 配置文件中定义。

### 定义内容类型

```yaml
# config/bolt/contenttypes.yaml
pages:
    name: Pages
    singular_name: Page
    fields:
        title:
            type: text
            class: large
            group: content
        slug:
            type: slug
            uses: title
        body:
            type: html
            height: 300px
        image:
            type: image
    taxonomy: [ groups ]
    listing_records: 10
    default_status: published
    sort: -datepublish
```

### 字段类型

| 类型 | 描述 | 使用场景 |
|------|------|----------|
| text | 单行文本 | 标题、名称 |
| html | 富文本编辑器 | 正文内容 |
| markdown | Markdown 编辑器 | 技术内容 |
| image | 图片上传 | 特色图片 |
| file | 文件上传 | 文档、下载 |
| video | 视频嵌入 | YouTube、Vimeo |
| textarea | 纯文本多行 | 描述 |
| date | 日期选择器 | 活动、截止日期 |
| datetime | 日期和时间选择器 | 日程安排 |
| select | 下拉选择 | 类别、状态 |
| checkbox | 布尔开关 | 精选、已发布 |
| number | 数值 | 价格、数量 |
| email | 邮箱地址 | 联系信息 |
| embed | OEmbed | 社交媒体嵌入 |
| geolocation | 地图坐标 | 位置数据 |
| repeater | 可重复字段 | 多个条目 |
| block | 内容块 | 灵活布局 |

### 多个内容类型

```yaml
blogposts:
    name: Blog Posts
    singular_name: Blog Post
    fields:
        title:
            type: text
            class: large
        slug:
            type: slug
            uses: title
        image:
            type: image
        body:
            type: html
        tags:
            type: taxonomy
            taxonomy: tags
    relations:
        pages:
            multiple: false
    taxonomy: [ categories, tags ]
    record_template: blogpost.twig

entries:
    name: Entries
    singular_name: Entry
    fields:
        title:
            type: text
        body:
            type: markdown
    listing_records: 20
```

## 模板（主题）

### 主题结构

```
mytheme/
  index.twig
  record.twig
  listing.twig
  _header.twig
  _footer.twig
  _aside.twig
  css/
    style.css
  js/
    main.js
```

### 基础模板

```twig
{# index.twig #}
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>{{ config.get('general/sitename') }}</title>
    <link rel="stylesheet" href="{{ asset('css/style.css', 'theme') }}">
</head>
<body>
    {% include '_header.twig' %}

    <main>
        {% block content %}
            {% for record in records %}
                <article>
                    <h2><a href="{{ record|link }}">{{ record.title }}</a></h2>
                    {{ record|excerpt(300) }}
                </article>
            {% endfor %}
        {% endblock %}
    </main>

    {% include '_footer.twig' %}
</body>
</html>
```

### 记录模板

```twig
{# record.twig #}
{% extends 'index.twig' %}

{% block content %}
<article class="record">
    <h1>{{ record.title }}</h1>
    <time>{{ record.datepublish|date('F j, Y') }}</time>

    {% if record.image %}
        <img src="{{ record.image|thumbnail(800, 600) }}"
             alt="{{ record.title }}">
    {% endif %}

    <div class="body">
        {{ record.body }}
    </div>

    {% if record.taxonomy.tags is defined %}
        <div class="tags">
            {% for tag in record.taxonomy.tags %}
                <span class="tag">{{ tag }}</span>
            {% endfor %}
        </div>
    {% endif %}
</article>
{% endblock %}
```

### 列表模板

```twig
{# listing.twig #}
{% extends 'index.twig' %}

{% block content %}
{% for record in records %}
    <div class="card">
        <h2><a href="{{ record|link }}">{{ record.title }}</a></h2>
        <p>{{ record|excerpt(200) }}</p>
    </div>
{% endfor %}

{{ pager(records, template='helpers/_pager.html') }}
{% endblock %}
```

## Twig 函数和过滤器

### 常用过滤器

| 过滤器 | 描述 | 示例 |
|--------|------|------|
| `\|link` | 获取记录 URL | `{{ record\|link }}` |
| `\|excerpt` | 截断文本 | `{{ record\|excerpt(300) }}` |
| `\|date` | 格式化日期 | `{{ record.datepublish\|date('Y-m-d') }}` |
| `\|raw` | 输出未转义的 HTML | `{{ record.body\|raw }}` |
| `\|thumbnail` | 调整图片大小 | `{{ image\|thumbnail(400, 300) }}` |
| `\|markdown` | 解析 markdown | `{{ text\|markdown }}` |
| `\|json_decode` | 解析 JSON 字符串 | `{{ data\|json_decode }}` |

### 常用函数

| 函数 | 描述 | 示例 |
|------|------|------|
| `path()` | 生成 URL | `{{ path('homepage') }}` |
| `url()` | 绝对 URL | `{{ url('page', {'slug': 'about'}) }}` |
| `asset()` | 主题资源路径 | `{{ asset('css/style.css', 'theme') }}` |
| `menu()` | 渲染导航 | `{{ menu('main') }}` |
| `pager()` | 分页控件 | `{{ pager(records) }}` |
| `dump()` | 调试变量 | `{{ dump(record) }}` |

## 分类法

### 定义分类法

```yaml
# config/bolt/taxonomy.yaml
categories:
    name: Categories
    slug: categories
    singular_name: Category
    behaves_like: categories
    options: [ news, tutorials, reviews ]

tags:
    name: Tags
    slug: tags
    singular_name: Tag
    behaves_like: tags
    allow_spaces: true

groups:
    name: Groups
    slug: groups
    singular_name: Group
    behaves_like: grouping
    options: [ content, meta ]
```

### 在模板中使用分类法

```twig
{# 显示记录的标签 #}
{% if record.taxonomy.tags is defined %}
    <div class="tags">
        {% for tag in record.taxonomy.tags %}
            <a href="{{ path('taxonomy', {'taxonomytype': 'tags', 'slug': tag}) }}">
                {{ tag }}
            </a>
        {% endfor %}
    </div>
{% endif %}
```

## 菜单

### 定义菜单

```yaml
# config/bolt/menu.yaml
main:
    - label: Home
      title: Welcome
      path: homepage
      class: first
    - label: Blog
      path: listing/blogposts
    - label: About
      link: /page/about
    - label: Contact
      path: page/contact
```

### 渲染菜单

```twig
<nav>
    {{ menu('main', 'helpers/_menu.twig') }}
</nav>
```

### 菜单模板

```twig
{# helpers/_menu.twig #}
<ul class="nav">
    {% for item in menu %}
        <li class="{{ item.class|default('') }}">
            <a href="{{ item.link }}" title="{{ item.title }}">
                {{ item.label }}
            </a>
        </li>
    {% endfor %}
</ul>
```

## 配置

### 常规设置

```yaml
# config/bolt/config.yaml
sitename: My Site
payoff: A great website
description: This is my website
locale: en_US
timezone: America/New_York
theme: mytheme
record_template: record.twig
listing_template: listing.twig
```

### 数据库配置

```yaml
# .env
DATABASE_DRIVER=mysql
DATABASE_HOST=localhost
DATABASE_NAME=bolt
DATABASE_USER=bolt
DATABASE_PASSWORD=bolt
```

## 用户角色和权限

| 角色 | 描述 |
|------|------|
| Developer | 完全访问所有设置 |
| Chief Editor | 管理所有内容和用户 |
| Editor | 编辑和发布内容 |
| Author | 创建和编辑自己的内容 |
| Guest | 对管理面板的只读访问 |
| Anonymous | 公共前端访问 |

## 扩展

### 安装扩展

```bash
composer require bolt/thumbs
```

### 常用扩展

| 扩展 | 用途 |
|------|------|
| bolt/thumbs | 图片缩略图生成 |
| bolt/sitemap | XML 站点地图生成 |
| bolt/seo | SEO 元数据管理 |
| bolt/comments | 评论系统 |
| bolt/redactor | 增强的富文本编辑器 |

## API 访问

### REST API 端点

| 端点 | 方法 | 描述 |
|------|------|------|
| `/api/contents` | GET | 列出所有内容 |
| `/api/content/{type}` | GET | 按内容类型列出 |
| `/api/content/{type}/{id}` | GET | 获取单条记录 |
| `/api/content/{type}` | POST | 创建新记录 |
| `/api/content/{type}/{id}` | PUT | 更新记录 |

## 总结

Bolt CMS 提供了一个对开发者友好的扁平文件 CMS，具有灵活的内容建模系统。在 YAML 中定义内容类型，使用 Twig 构建模板，通过内置管理面板管理内容。它在编辑者的简洁性和开发者的能力之间取得了平衡。
