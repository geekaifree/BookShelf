# XWiki：企业 Wiki 平台教程

## 简介

XWiki 是一个用 Java 编写的开源企业 Wiki 平台。它支持结构化内容、脚本编写、应用开发和广泛的自定义。本教程涵盖安装、内容管理、脚本编写和管理。

## XWiki 与其他企业 Wiki 对比

| 功能 | XWiki | Confluence | SharePoint | Notion |
|------|-------|------------|------------|--------|
| 开源 | 是 | 否 | 否 | 否 |
| 自托管 | 是 | Server 版 | 是 | 否 |
| 脚本 | Groovy、Velocity、JavaScript | 有限 | Power Automate | 否 |
| 应用构建器 | 是 | 市场 | Power Apps | 有限 |
| 数据库 | MySQL、PostgreSQL、Oracle、HQL | PostgreSQL | SQL Server | 专有 |
| REST API | 是 | 是 | 是 | 是 |
| 扩展 | 900+ | 3000+ | SPFx | 有限 |
| 价格 | 免费 | 免费增值 | 许可证 | 免费增值 |

## 系统要求

| 组件 | 最低要求 | 推荐配置 |
|------|---------|---------|
| Java | JDK 11 | JDK 17 |
| 内存 | 2 GB | 4 GB+ |
| 数据库 | MySQL 8、PostgreSQL 12 | PostgreSQL 15 |
| Servlet | Tomcat 9+ | Tomcat 10 |
| 磁盘 | 2 GB | 20 GB |
| CPU | 2 核 | 4+ 核 |

## 安装

### 独立版（XAR）

```bash
# 下载 WAR 和 Jetty JAR
wget https://nexus.xwiki.org/.../xwiki-platform-distribution-war-*.war

# 使用 Jetty 启动
java -jar xwiki-jetty-runner.jar --port 8080 xwiki.war
```

### Docker

```bash
docker run -d \
  --name xwiki \
  -p 8080:8080 \
  -e DB_DATABASE=xwiki \
  -e DB_USER=xwiki \
  -e DB_PASSWORD=xwiki \
  -e DB_HOST=xwiki-db \
  xwiki:lts-mysql-tomcat
```

### Docker Compose

```yaml
version: '3'
services:
  xwiki-db:
    image: mysql:8.0
    container_name: xwiki-db
    restart: unless-stopped
    environment:
      - MYSQL_ROOT_PASSWORD=root
      - MYSQL_DATABASE=xwiki
      - MYSQL_USER=xwiki
      - MYSQL_PASSWORD=xwiki
    volumes:
      - xwiki-db:/var/lib/mysql

  xwiki:
    image: xwiki:lts-mysql-tomcat
    container_name: xwiki
    restart: unless-stopped
    depends_on:
      - xwiki-db
    environment:
      - DB_DATABASE=xwiki
      - DB_USER=xwiki
      - DB_PASSWORD=xwiki
      - DB_HOST=xwiki-db
    ports:
      - "8080:8080"
    volumes:
      - xwiki-data:/usr/local/xwiki

volumes:
  xwiki-db:
  xwiki-data:
```

## 核心概念

### 内容层级

| 级别 | 描述 | 示例 |
|------|------|------|
| Wiki | 顶层容器 | 公司 Wiki |
| Space | 逻辑分组 | 工程、市场 |
| Page | 单个内容页 | API 文档 |
| Child Page | 嵌套页面 | REST API 参考 |

### 页面属性

| 属性 | 描述 |
|------|------|
| Title | 显示名称 |
| Content | Wiki 标记或渲染后的 HTML |
| Syntax | 渲染语法（XWiki、Markdown） |
| Parent | 父页面引用 |
| Tags | 分类标签 |
| Author | 创建者和最后编辑者 |
| Created | 创建时间戳 |
| Modified | 最后修改时间戳 |

## 内容编辑

### 语法选项

| 语法 | 描述 | 最佳用途 |
|------|------|---------|
| XWiki 2.1 | 原生 Wiki 语法 | XWiki 特有功能 |
| Markdown | 标准 Markdown | 技术内容 |
| HTML | 原始 HTML | 自定义布局 |
| Creole | Creole Wiki 语法 | 跨平台兼容 |

### XWiki 语法

| 元素 | 语法 |
|------|------|
| 标题 1 | = Heading 1 = |
| 标题 2 | == Heading 2 == |
| 粗体 | **bold** |
| 斜体 | //italic// |
| 下划线 | __underline__ |
| 删除线 | ~~strike~~ |
| 链接 | [[label>>URL]] |
| 图片 | image:url |
| 表格 | \|cell1\|cell2\| |
| 列表 | * item |
| 代码 | {{code}}...{{/code}} |
| 宏 | {{macro parameter="value"}}...{{/macro}} |

### 所见即所得编辑器

| 功能 | 描述 |
|------|------|
| 富文本 | 类似 Word 的编辑 |
| 工具栏 | 格式按钮 |
| 表格 | 可视化表格编辑 |
| 图片 | 拖放上传 |
| 宏 | 通过对话框插入 |
| 源码 | 切换到 Wiki 语法 |

## 宏

宏扩展页面功能。

### 内置宏

| 宏 | 用途 |
|----|------|
| {{toc}} | 目录 |
| {{children}} | 列出子页面 |
| {{include}} | 嵌入另一个页面 |
| {{velocity}} | Velocity 脚本块 |
| {{groovy}} | Groovy 脚本块 |
| {{html}} | 原始 HTML 块 |
| {{code}} | 语法高亮代码 |
| {{table}} | 动态表格 |
| {{gallery}} | 图片库 |
| {{box}} | 样式化内容框 |

### 宏参数

| 参数 | 常用选项 |
|------|---------|
| id | 唯一标识符 |
| output | rendered、wiki |
| scope | current、all |
| sort | name、date |
| limit | 结果数量 |

## 脚本编写

### Velocity 脚本

```velocity
{{velocity}}
#set($docs = $xwiki.searchDocuments("space = 'Main'"))
#foreach($doc in $docs)
  * [[$doc]]
#end
{{/velocity}}
```

### Groovy 脚本

```groovy
{{groovy}}
def docs = xwiki.searchDocuments("space = 'Main'")
docs.each { doc ->
  println("* [[" + doc + "]]")
}
{{/groovy}}
```

### JavaScript

```javascript
{{javascript}}
require(['jquery'], function($) {
  $('.xwikidocumentcontainer').addClass('custom-style');
});
{{/javascript}}
```

## App Within Minutes

无需编码即可创建数据库驱动的应用。

### 应用结构

| 组件 | 用途 |
|------|------|
| Class | 数据结构定义 |
| Properties | 字段（文本、数字、日期等） |
| Sheets | 显示模板 |
| Templates | 新条目表单 |
| Livetables | 带过滤器的数据列表 |

### 属性类型

| 类型 | 用例 |
|------|------|
| String | 文本字段 |
| Number | 整数、浮点数 |
| Date | 日期和时间 |
| Boolean | 真/假 |
| Static List | 下拉选项 |
| Database List | 外键引用 |
| TextArea | 长文本、富文本 |
| File | 文件上传 |
| Email | 邮箱地址 |
| URL | 网址 |

## 访问控制

### 权限模型

| 级别 | 范围 |
|------|------|
| Wiki | 全局 Wiki 权限 |
| Space | 空间级权限 |
| Page | 单个页面权限 |

### 权限类型

| 权限 | 描述 |
|------|------|
| View | 查看页面 |
| Edit | 修改页面 |
| Delete | 删除页面 |
| Admin | 管理设置 |
| Comment | 添加评论 |
| Script | 运行脚本 |

### 用户组

| 组 | 默认角色 |
|----|---------|
| XWikiAdminGroup | 完全管理 |
| XWikiAllGroup | 所有注册用户 |
| 自定义组 | 自行定义 |

## 扩展

### 扩展管理器

| 操作 | 方法 |
|------|------|
| 浏览 | 搜索扩展仓库 |
| 安装 | 点击安装按钮 |
| 更新 | 检查更新 |
| 卸载 | 移除扩展 |
| 配置 | 扩展设置 |

### 热门扩展

| 扩展 | 用途 |
|------|------|
| Flamingo Theme | 现代 UI 主题 |
| Markdown Support | Markdown 语法 |
| Diagram Application | Draw.io 集成 |
| File Manager | 文件管理 |
| Calendar | 活动安排 |
| Meeting Notes | 会议模板 |
| Idea Management | 想法跟踪 |

## 主题

### Flamingo 主题

| 自定义 | 选项 |
|--------|------|
| 颜色 | 主色、辅色、强调色 |
| Logo | 上传自定义 Logo |
| Favicon | 自定义网站图标 |
| Footer | 自定义页脚内容 |
| CSS | 额外样式表 |

## 搜索

### 搜索方式

| 方式 | 语法 |
|------|------|
| 全文搜索 | 头部搜索框 |
| HQL | 高级 HQL 查询 |
| SOLR | 基于 SOLR 的搜索 |
| Livetable | 带过滤器的表格 |

### HQL 查询示例

| 查询 | 用途 |
|------|------|
| space = 'Main' | Main 空间中的页面 |
| doc.author = 'Admin' | 按作者筛选页面 |
| doc.creationDate > '2024-01-01' | 最近的页面 |
| doc.tags = 'important' | 带标签的页面 |

## 导入/导出

| 格式 | 方向 | 内容 |
|------|------|------|
| XAR | 导出/导入 | 完整 Wiki 或空间 |
| HTML | 导出 | 页面为 HTML |
| PDF | 导出 | 页面为 PDF |
| ODT | 导出 | OpenDocument |
| RTF | 导出 | 富文本格式 |

## 备份

### 备份策略

| 组件 | 方法 | 频率 |
|------|------|------|
| 数据库 | pg_dump/mysqldump | 每天 |
| 附件 | 文件系统备份 | 每天 |
| 配置 | Git 仓库 | 变更时 |
| 扩展 | 扩展列表导出 | 每周 |

## REST API

### 端点

| 方法 | 端点 | 描述 |
|------|------|------|
| GET | /rest/wikis | 列出 Wiki |
| GET | /rest/wikis/{wiki}/spaces | 列出空间 |
| GET | /rest/wikis/{wiki}/spaces/{space}/pages | 列出页面 |
| GET | /rest/wikis/{wiki}/pages/{space}/{page} | 获取页面 |
| PUT | /rest/wikis/{wiki}/pages/{space}/{page} | 更新页面 |
| POST | /rest/wikis/{wiki}/spaces/{space}/pages | 创建页面 |
| DELETE | /rest/wikis/{wiki}/pages/{space}/{page} | 删除页面 |

## 性能调优

| 设置 | 建议 |
|------|------|
| JVM Heap | 生产环境 2-4 GB |
| 数据库 | 连接池 |
| 缓存 | 启用页面缓存 |
| SOLR | 索引以加速搜索 |
| GZIP | 启用响应压缩 |
| CDN | 提供静态资源 |

## 总结

XWiki 提供了一个强大的企业 Wiki 平台，通过脚本编写、应用构建和丰富的扩展生态系统实现广泛自定义。其结构化内容模型、细粒度访问控制和 REST API 使其适合需要灵活知识管理和协作平台的大型组织。
