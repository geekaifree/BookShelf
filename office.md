# ONLYOFFICE 文档服务器教程

## 简介

ONLYOFFICE Document Server 是一款自托管办公套件，提供文本文档、电子表格和演示文稿的在线编辑器。它支持协同编辑，并兼容 Microsoft Office 格式。

| 特性 | 描述 |
|---------|-------------|
| 文档编辑 | 具有格式化工具的全功能文字处理器 |
| 电子表格编辑 | 计算、图表、数据透视表和公式 |
| 演示文稿编辑 | 创建带有过渡和动画的幻灯片 |
| 协作 | 多用户实时协同编辑 |
| 兼容性 | 原生支持 DOCX、XLSX、PPTX 格式 |

## 架构

### 系统组件

| 组件 | 用途 |
|-----------|---------|
| Document Manager | 文件操作和文档存储接口 |
| Document Server | 处理文档的核心编辑引擎 |
| File Converter | 在办公文件格式之间进行转换 |
| Database | PostgreSQL 用于存储元数据和设置 |
| Cache | Redis 或 RabbitMQ 用于实时协作数据 |
| Nginx | 反向代理用于服务应用 |

### 支持的格式

| 类别 | 读/写 | 只读 |
|----------|-----------|-----------|
| 文本 | DOCX、DOC、ODT、RTF、TXT、HTML、EPUB | PDF、DJVU |
| 电子表格 | XLSX、XLS、ODS、CSV | PDF |
| 演示文稿 | PPTX、PPT、ODP | PDF |

## 安装

### Docker 部署

```bash
# 使用 Docker Compose 拉取并运行
git clone https://github.com/ONLYOFFICE/Docker-DocumentServer.git
cd Docker-DocumentServer
docker-compose up -d
```

### Docker Compose 配置

```yaml
version: '3.8'
services:
  onlyoffice-documentserver:
    image: onlyoffice/documentserver:latest
    container_name: onlyoffice
    ports:
      - "8080:80"
    environment:
      - JWT_SECRET=your_secret_key
    volumes:
      - document_data:/var/www/onlyoffice/Data
      - document_log:/var/log/onlyoffice
    restart: unless-stopped

volumes:
  document_data:
  document_log:
```

### 系统要求

| 组件 | 最低要求 | 推荐配置 |
|-----------|---------|-------------|
| CPU | 2 核 | 4+ 核 |
| 内存 | 4 GB | 8+ GB |
| 存储 | 40 GB | 100+ GB |
| 操作系统 | Linux (64-bit) | Ubuntu 20.04+ 或 Debian 10+ |
| Docker | 20.10+ | 最新稳定版 |

## 文档编辑器

### 功能

| 功能 | 描述 |
|---------|-------------|
| 文本格式化 | 字体、大小、颜色、样式和段落设置 |
| 表格 | 插入和格式化表格，支持单元格合并和边框 |
| 图片 | 插入、调整大小和文字环绕图片 |
| 页眉/页脚 | 页码、日期和自定义内容 |
| 目录 | 从标题样式自动生成 |
| 修订 | 记录和审阅协作者的编辑 |
| 评论 | 添加线程化评论以获取反馈 |
| 邮件合并 | 从数据源生成个性化文档 |

### 协作工具

| 工具 | 功能 |
|------|----------|
| 实时编辑 | 多用户同时编辑 |
| 审阅模式 | 建议修改而不修改原文 |
| 评论 | 添加备注并解决讨论 |
| 版本历史 | 查看和恢复以前的文档版本 |
| 聊天 | 协作者之间的内置消息功能 |
| 用户颜色 | 每个编辑者分配唯一的颜色 |

## 电子表格编辑器

### 功能

| 功能 | 描述 |
|---------|-------------|
| 公式 | 跨类别的 400+ 内置函数 |
| 图表 | 柱状图、折线图、饼图、散点图和专业图表类型 |
| 数据透视表 | 汇总和分析大型数据集 |
| 条件格式 | 根据单元格值应用格式规则 |
| 数据验证 | 将输入限制为特定条件 |
| 筛选器 | 自动筛选和高级筛选选项 |
| 命名范围 | 定义可重用的单元格引用 |
| 宏 | 基于 JavaScript 的自动化脚本 |

### 公式类别

| 类别 | 示例 |
|----------|---------|
| 数学 | SUM、AVERAGE、ROUND、MOD |
| 文本 | CONCATENATE、LEFT、FIND、SUBSTITUTE |
| 日期 | NOW、DATE、DATEDIF、WEEKDAY |
| 逻辑 | IF、AND、OR、NOT、SWITCH |
| 查找 | VLOOKUP、INDEX、MATCH、XLOOKUP |
| 统计 | COUNTIF、AVERAGEIF、STDEV、MEDIAN |

## 演示文稿编辑器

### 功能

| 功能 | 描述 |
|---------|-------------|
| 幻灯片布局 | 预设计的常用布局模板 |
| 过渡效果 | 幻灯片之间的动画效果 |
| 动画 | 对象的进入、强调和退出效果 |
| 演讲者备注 | 演示期间可见的私人备注 |
| 母版幻灯片 | 所有幻灯片的一致设计 |
| 图表 | 链接到电子表格数据的嵌入式图表 |
| 媒体 | 插入音频和视频文件 |

## 集成

### 集成方式

| 方式 | 描述 |
|--------|-------------|
| API | 用于在 Web 应用中嵌入编辑器的 JavaScript API |
| 插件 | 使用自定义插件扩展功能 |
| Webhooks | 接收文档事件通知 |
| WOPI | Web Application Open Platform Interface 协议 |
| JWT | 使用 JSON Web Token 进行安全文档访问 |

### API 集成示例

```html
<!DOCTYPE html>
<html>
<head>
  <script src="http://documentserver/web-apps/apps/api/documents/api.js"></script>
</head>
<body>
  <div id="placeholder"></div>
  <script>
    var config = {
      document: {
        fileType: "docx",
        key: "unique_document_key",
        title: "My Document.docx",
        url: "http://example.com/path/to/document.docx"
      },
      documentType: "word",
      editorConfig: {
        callbackUrl: "http://example.com/callback",
        user: {
          id: "user1",
          name: "John Smith"
        }
      }
    };
    var docEditor = new DocsAPI.DocEditor("placeholder", config);
  </script>
</body>
</html>
```

### 集成平台

| 平台 | 集成类型 |
|----------|-----------------|
| Nextcloud | 官方连接器应用 |
| ownCloud | 社区连接器 |
| SharePoint | Microsoft SharePoint 集成 |
| Confluence | Atlassian Confluence 插件 |
| Moodle | 面向教育的 LMS 集成 |
| WordPress | 用于嵌入文档的插件 |

## 安全

### 安全功能

| 功能 | 描述 |
|---------|-------------|
| JWT 认证 | 安全的基于令牌的访问控制 |
| HTTPS/TLS | 加密通信 |
| 访问权限 | 查看、编辑、审阅、评论和填写表单 |
| 水印 | 在文档上显示用户信息 |
| IP 过滤 | 按 IP 地址限制访问 |
| LDAP | 目录服务集成 |

### 权限级别

| 权限 | 功能 |
|-----------|-------------|
| 查看 | 文档只读访问 |
| 评论 | 查看和添加评论 |
| 审阅 | 建议修改和跟踪更改 |
| 填写表单 | 仅填写表单字段 |
| 编辑 | 完全编辑功能 |

## 插件系统

### 插件开发

插件可扩展 ONLYOFFICE 的自定义功能。

| 组件 | 用途 |
|-----------|---------|
| config.json | 插件元数据和配置 |
| index.html | 插件用户界面 |
| plugin.js | 插件逻辑和 API 交互 |

### 可用插件

| 插件 | 功能 |
|--------|----------|
| OCR | 从图片中提取文字 |
| Translator | 翻译文档内容 |
| Thesaurus | 查找同义词和相关词 |
| YouTube | 嵌入 YouTube 视频 |
| Photo Editor | 在文档中编辑图片 |
| Macros | 编写和运行 JavaScript 宏 |

## 管理

### 备份和恢复

```bash
# 备份数据库
docker exec onlyoffice pg_dump -U onlyoffice onlyoffice > backup.sql

# 备份文档数据
tar -czf document_data_backup.tar.gz /var/www/onlyoffice/Data

# 恢复数据库
cat backup.sql | docker exec -i onlyoffice psql -U onlyoffice onlyoffice
```

### 监控

| 指标 | 工具 |
|--------|------|
| 服务器状态 | 内置健康检查端点 |
| 活跃连接 | Prometheus 指标 |
| 文档处理 | 转换服务日志 |
| 资源使用 | Docker stats 或系统监控 |

## 总结

| 主题 | 核心要点 |
|-------|-------------|
| 架构 | 多组件系统，包含转换器和协作引擎 |
| 编辑器 | 全功能的文档、电子表格和演示文稿编辑器 |
| 协作 | 实时协同编辑，配合审阅和评论工具 |
| 集成 | API、插件、WOPI 协议和平台连接器 |
| 安全 | JWT 认证、细粒度权限和加密 |
| 部署 | 基于 Docker，依赖 PostgreSQL 和 Redis |
