# 书籍与资源

> 本文档整合了以下源文件：books.md, book.md, awesome.md, papers.md, index.md

---

## 来源：books.md

## 简介

Readarr 是一款面向 Usenet 和 BitTorrent 用户的书籍收藏管理器。它监控 RSS 源以获取新书，并自动下载、排序和重命名。它支持电子书和有声书，与下载客户端和电子书管理工具集成。

| 特性 | 描述 |
|---------|-------------|
| 书籍监控 | 跟踪想要的书籍并搜索可用发布 |
| 有声书支持 | 与电子书并行管理有声书收藏 |
| 质量配置文件 | 定义首选格式和质量级别 |
| 作者监控 | 关注作者以自动获取新发布 |
| 元数据管理 | 从多个来源获取书籍信息 |

## 架构

### 系统组件

| 组件 | 角色 |
|-----------|------|
| Readarr | 书籍监控和管理应用 |
| 索引器 | 查找书籍发布的来源 |
| 下载客户端 | 执行下载的软件 |
| Calibre | 可选的电子书管理和转换 |
| Audiobookshelf | 可选的有声书服务器 |

### 工作流程

| 步骤 | 描述 |
|------|-------------|
| 1 | 用户向 Readarr 添加作者或书籍 |
| 2 | Readarr 在索引器中监控匹配的发布 |
| 3 | 根据质量配置文件评估发布 |
| 4 | 将下载请求发送到已配置的下载客户端 |
| 5 | 文件被下载并导入 |
| 6 | 获取并应用元数据 |
| 7 | 可选：将文件发送到 Calibre 进行转换 |

## 安装

### Docker 部署

```bash
docker run -d \
  --name=readarr \
  -p 8787:8787 \
  -v /path/to/config:/config \
  -v /path/to/books:/books \
  -v /path/to/downloads:/downloads \
  -e PUID=1000 \
  -e PGID=1000 \
  -e TZ=UTC \
  --restart unless-stopped \
  lscr.io/linuxserver/readarr:develop
```

### Docker Compose

```yaml
version: "3.8"
services:
  readarr:
    image: lscr.io/linuxserver/readarr:develop
    container_name: readarr
    environment:
      - PUID=1000
      - PGID=1000
      - TZ=UTC
    volumes:
      - ./config:/config
      - /path/to/books:/books
      - /path/to/audiobooks:/audiobooks
      - /path/to/downloads:/downloads
    ports:
      - "8787:8787"
    restart: unless-stopped

  calibre:
    image: lscr.io/linuxserver/calibre
    container_name: calibre
    environment:
      - PUID=1000
      - PGID=1000
      - TZ=UTC
    volumes:
      - ./calibre-config:/config
      - /path/to/books:/books
    ports:
      - "8080:8080"
    restart: unless-stopped
```

## 配置

### 添加作者

| 方式 | 描述 |
|--------|-------------|
| 搜索 | 在 Readarr 界面中按作者名搜索 |
| Goodreads | 从 Goodreads 作者页面导入 |
| 手动 | 通过作者元数据 ID 添加 |

### 添加书籍

| 方式 | 描述 |
|--------|-------------|
| 作者页面 | 浏览作者目录并选择书籍 |
| 搜索 | 按书名或 ISBN 搜索 |
| 导入 | 从库文件夹导入现有书籍 |

### 质量配置文件

| 配置文件 | 使用场景 |
|---------|----------|
| 仅电子书 | 仅下载电子书格式 |
| 仅有声书 | 仅有声书格式 |
| 混合 | 接受电子书和有声书发布 |
| 自定义 | 定义特定格式偏好 |

### 书籍格式

| 格式 | 类型 | 典型用途 |
|--------|------|-------------|
| EPUB | 电子书 | 标准电子书格式，广泛支持 |
| MOBI | 电子书 | Kindle 兼容格式 |
| PDF | 电子书 | 固定版式文档 |
| AZW3 | 电子书 | Amazon Kindle 格式 |
| MP3 | 有声书 | 压缩有声书 |
| M4A | 有声书 | AAC 有声书 |
| M4B | 有声书 | 带章节的有声书 |
| FLAC | 有声书 | 无损有声书 |

### 质量定义

| 质量 | 描述 | 优先级 |
|---------|-------------|----------|
| EPUB | 标准电子书 | 高 |
| AZW3 | Kindle 格式 | 中 |
| MOBI | 旧版 Kindle 格式 | 低 |
| M4B | 带章节有声书 | 高 |
| MP3 | 压缩音频 | 中 |
| FLAC | 无损音频 | 最高 |

## 下载客户端

### 支持的客户端

| 客户端 | 协议 | 备注 |
|--------|----------|-------|
| qBittorrent | Torrent | 推荐的 Torrent 客户端 |
| Transmission | Torrent | 轻量级选项 |
| Deluge | Torrent | 基于插件的架构 |
| SABnzbd | Usenet | 流行的 Usenet 下载器 |
| NZBGet | Usenet | 高效的 Usenet 客户端 |
| Flood | Torrent | rTorrent 的现代 Web UI |

### 客户端配置

| 设置 | 描述 |
|---------|-------------|
| 主机 | 下载客户端的 IP 地址或主机名 |
| 端口 | API 访问的端口号 |
| 用户名 | 认证用户名 |
| 密码 | 认证密码 |
| 分类 | Readarr 项目的下载分类 |
| 优先级 | 下载优先级 |

## Calibre 集成

### Calibre 功能

| 功能 | 描述 |
|---------|-------------|
| 格式转换 | 在电子书格式之间转换 |
| 元数据编辑 | 编辑书籍元数据和封面 |
| 库管理 | 组织和编目电子书收藏 |
| 内容服务器 | 通过 HTTP 提供书籍服务 |

### 集成设置

| 步骤 | 操作 |
|------|--------|
| 1 | 安装并配置 Calibre，启用内容服务器 |
| 2 | 在 Readarr 中，导航到设置 > Calibre |
| 3 | 输入 Calibre 内容服务器 URL 和端口 |
| 4 | 配置 Calibre 的自动添加文件夹 |
| 5 | 设置格式转换偏好 |

### Calibre 内容服务器

| 设置 | 描述 |
|---------|-------------|
| 端口 | 默认 8080 |
| 认证 | 可选的用户名/密码 |
| 库路径 | Calibre 库文件夹路径 |
| 自动添加 | 监视新书籍的文件夹 |

## 文件管理

### 命名模式

| 标记 | 描述 | 示例 |
|-------|-------------|---------|
| {Author Name} | 作者姓名 | Stephen King |
| {Book Title} | 书名 | It |
| {Release Year} | 出版年份 | 1986 |
| {Quality} | 质量/格式名称 | EPUB |
| {Book ISBN} | ISBN 标识符 | 978-0-670-81302-4 |

### 推荐模式

| 类型 | 模式 | 示例 |
|------|---------|---------|
| 单作者 | `{Author Name}/{Book Title}` | Stephen King/It.epub |
| 带年份 | `{Author Name}/{Book Title} ({Release Year})` | Stephen King/It (1986).epub |
| 带质量 | `{Author Name}/{Book Title} {Quality}` | Stephen King/It EPUB.epub |

### 文件夹结构

```
/books/
  Stephen King/
    It (1986).epub
    The Shining (1977).epub
    Pet Sematary (1983).epub
  Terry Pratchett/
    The Colour of Magic (1983).epub
    Mort (1987).epub
/audiobooks/
  Stephen King/
    It (1986)/
      Chapter 01.mp3
      Chapter 02.mp3
```

## 元数据来源

### 支持的来源

| 来源 | 提供的数据 |
|--------|---------------|
| Goodreads | 评分、评论、类似书籍 |
| Google Books | 书籍详情、描述、封面 |
| Open Library | 免费书籍数据和封面 |
| ISBNdb | 基于 ISBN 的书籍信息 |
| WorldCat | 图书馆目录数据 |

### 元数据字段

| 字段 | 描述 |
|-------|-------------|
| Title | 书名 |
| Author | 作者姓名 |
| Publisher | 出版社 |
| Publication date | 原始出版年份 |
| ISBN | 国际标准书号 |
| Description | 书籍简介 |
| Genre | 书籍分类 |
| Cover | 书籍封面图片 |

## 通知

### 支持的服务

| 服务 | 配置 |
|---------|--------------|
| Email | SMTP 服务器设置 |
| Discord | Webhook URL |
| Telegram | Bot Token 和 Chat ID |
| Slack | Webhook URL |
| Webhook | 自定义 HTTP 端点 |

### 通知事件

| 事件 | 描述 |
|-------|-------------|
| 抓取 | 当发布发送到下载客户端时 |
| 导入 | 当书籍成功导入时 |
| 升级 | 当书籍升级到更好质量时 |
| 重命名 | 当书籍文件被重命名时 |
| 作者添加 | 当添加新作者时 |
| 健康 | 当健康检查出现问题时 |

## API 访问

### 关键端点

| 端点 | 方法 | 描述 |
|----------|--------|-------------|
| `/api/v1/book` | GET | 列出所有书籍 |
| `/api/v1/author` | GET | 列出所有作者 |
| `/api/v1/book/{id}` | GET | 获取特定书籍 |
| `/api/v1/command` | POST | 触发命令 |
| `/api/v1/calendar` | GET | 获取即将发布的书籍 |

## 故障排除

### 常见问题

| 问题 | 原因 | 解决方案 |
|-------|-------|----------|
| 未找到结果 | 未配置索引器 | 添加支持书籍的索引器 |
| 下载了错误格式 | 质量配置文件过于宽松 | 调整质量定义 |
| 元数据缺失 | 元数据来源不可用 | 检查 Goodreads/Google Books 访问 |
| Calibre 未导入 | 内容服务器未运行 | 启动 Calibre 内容服务器 |
| 重复下载 | 多个索引器返回同一本书 | 启用首选词设置 |

## 总结

| 主题 | 核心要点 |
|-------|-------------|
| 用途 | 自动化书籍和有声书收藏管理 |
| 格式 | 支持 EPUB、MOBI、PDF、M4B、MP3 等 |
| 集成 | 与 Calibre 配合进行格式转换和管理 |
| 索引器 | 使用 Torrent 和 Usenet 索引器获取书籍来源 |
| 组织 | 基于作者的自动文件夹结构 |
| 元数据 | 从 Goodreads 和 Google Books 获取书籍信息 |


---

## 来源：book.md

## 简介

本指南涵盖按主题和技能水平组织的推荐编程书籍。该收藏包括基础文本、语言特定参考书以及面向各阶段软件开发者的高级主题。

## 目录

1. [编程基础](#编程基础)
2. [语言特定书籍](#语言特定书籍)
3. [算法与数据结构](#算法与数据结构)
4. [软件设计](#软件设计)
5. [系统编程](#系统编程)
6. [Web 开发](#web-开发)
7. [数据库与存储](#数据库与存储)
8. [机器学习](#机器学习)

## 编程基础

### 入门书籍

| 书籍 | 作者 | 主题 | 级别 |
|------|------|------|------|
| Structure and Interpretation of Computer Programs | Abelson, Sussman | 编程范式 | 中级 |
| The Pragmatic Programmer | Hunt, Thomas | 专业实践 | 入门 |
| Code Complete | McConnell | 软件构建 | 入门 |
| Clean Code | Martin | 代码质量 | 入门 |
| Think Python | Downey | Python 基础 | 入门 |

### 理论与概念

| 书籍 | 作者 | 主题 |
|------|------|------|
| Introduction to the Theory of Computation | Sipser | 自动机、复杂度 |
| Types and Programming Languages | Pierce | 类型系统 |
| Concepts of Programming Languages | Sebesta | 语言设计 |
| Programming Language Pragmatics | Scott | 语言实现 |

## 语言特定书籍

### Python

| 书籍 | 作者 | 重点 |
|------|------|------|
| Fluent Python | Ramalho | 高级 Python |
| Python Cookbook | Beazley, Jones | 配方和模式 |
| Effective Python | Slatkin | 最佳实践 |
| Python Crash Course | Matthes | 入门介绍 |
| Learning Python | Lutz | 综合参考 |

### JavaScript

| 书籍 | 作者 | 重点 |
|------|------|------|
| JavaScript: The Good Parts | Crockford | 核心语言 |
| Eloquent JavaScript | Haverbeke | Web 编程 |
| You Don't Know JS | Simpson | 深入理解 |
| JavaScript Patterns | Stefanov | 设计模式 |
| Learning JavaScript | Shelley | 现代 JavaScript |

### Rust

| 书籍 | 作者 | 重点 |
|------|------|------|
| The Rust Programming Language | Klabnik, Nichols | 官方参考 |
| Rust in Action | McNamara | 系统编程 |
| Programming Rust | Blandy, Orendorff, Tindall | 综合指南 |
| Zero To Production In Rust | Palmieri | Web 开发 |

### Go

| 书籍 | 作者 | 重点 |
|------|------|------|
| The Go Programming Language | Donovan, Kernighan | 官方参考 |
| Go in Practice | Butcher, Farina | 实践模式 |
| Concurrency in Go | Cox-Buday | 并发模式 |
| Go Web Programming | Chang | Web 开发 |

### Java

| 书籍 | 作者 | 重点 |
|------|------|------|
| Effective Java | Bloch | 最佳实践 |
| Head First Java | Sierra, Bates | 入门友好 |
| Java Concurrency in Practice | Goetz | 并发 |
| Modern Java in Action | Fusco | 函数式编程 |

## 算法与数据结构

### 基础文本

| 书籍 | 作者 | 级别 |
|------|------|------|
| Introduction to Algorithms (CLRS) | Cormen 等 | 大学 |
| Algorithm Design Manual | Skiena | 实践 |
| Algorithms | Sedgewick, Wayne | 可视化方法 |
| The Art of Computer Programming | Knuth | 参考书 |

### 问题解决

| 书籍 | 作者 | 重点 |
|------|------|------|
| Competitive Programming | Halim | 竞赛准备 |
| Cracking the Coding Interview | McDowell | 面试准备 |
| Elements of Programming | Stepanov, McJones | 泛型编程 |
| Algorithmic Puzzles | Levitin, Ainuzzada | 问题解决 |

### 主题覆盖

| 主题 | 最佳覆盖 |
|------|----------|
| 排序 | CLRS, Sedgewick |
| 图算法 | CLRS, Skiena |
| 动态规划 | Skiena |
| 字符串算法 | Gusfield |
| 计算几何 | de Berg 等 |

## 软件设计

### 设计模式

| 书籍 | 作者 | 模式 |
|------|------|------|
| Design Patterns | Gang of Four | 经典模式 |
| Head First Design Patterns | Freeman, Robson | 可视化学习 |
| Pattern-Oriented Software Architecture | Buschmann 等 | 架构模式 |
| Patterns of Enterprise Application Architecture | Fowler | 企业模式 |

### 架构

| 书籍 | 作者 | 重点 |
|------|------|------|
| Clean Architecture | Martin | 系统设计 |
| Software Architecture in Practice | Bass 等 | 架构基础 |
| Building Microservices | Newman | 微服务设计 |
| Designing Data-Intensive Applications | Kleppmann | 数据系统 |

### 代码质量

| 书籍 | 作者 | 主题 |
|------|------|------|
| Refactoring | Fowler | 代码改进 |
| Working Effectively with Legacy Code | Feathers | 遗留系统 |
| The Art of Readable Code | Boswell, Foucher | 代码可读性 |
| Beautiful Code | Oram, Wilson | 优雅解决方案 |

## 系统编程

### 操作系统

| 书籍 | 作者 | 主题 |
|------|------|------|
| Operating Systems: Three Easy Pieces | Arpaci-Dusseau | OS 基础 |
| Modern Operating Systems | Tanenbaum | OS 设计 |
| Linux Kernel Development | Love | 内核内部 |
| Understanding the Linux Kernel | Bovet, Cesati | 内核深入 |

### 计算机体系结构

| 书籍 | 作者 | 主题 |
|------|------|------|
| Computer Systems: A Programmer's Perspective | Bryant, O'Hallaron | 系统视角 |
| Computer Organization and Design | Patterson, Hennessy | 硬件/软件 |
| Computer Architecture | Hennessy, Patterson | 高级体系结构 |

### 编译器

| 书籍 | 作者 | 主题 |
|------|------|------|
| Compilers: Principles, Techniques, and Tools | Aho 等 | 编译器设计 |
| Crafting Interpreters | Nystrom | 解释器实现 |
| Writing An Interpreter In Go | Ball | 实践解释器 |
| Writing A Compiler In Go | Ball | 编译器实现 |

## Web 开发

### 前端

| 书籍 | 作者 | 重点 |
|------|------|------|
| JavaScript: The Definitive Guide | Flanagan | 综合 JS |
| CSS: The Definitive Guide | Meyer, Weyl | CSS 精通 |
| Learning React | Banks, Porcello | React 框架 |
| You Don't Know JS | Simpson | JS 内部 |

### 后端

| 书籍 | 作者 | 重点 |
|------|------|------|
| Node.js Design Patterns | Casciaro, Mamino | Node 模式 |
| Web Development with Go | Shirdi | Go Web 应用 |
| Django for Professionals | Feldroy | Django 框架 |
| Rails Tutorial | Hartl | Ruby on Rails |

### API 设计

| 书籍 | 作者 | 主题 |
|------|------|------|
| RESTful Web APIs | Richardson, Amundsen | REST 设计 |
| API Design Patterns | Jin 等 | API 模式 |
| Building Microservices | Newman | 服务架构 |

## 数据库与存储

### 数据库内部

| 书籍 | 作者 | 主题 |
|------|------|------|
| Database Internals | Petrov | 存储引擎 |
| Designing Data-Intensive Applications | Kleppmann | 数据系统 |
| Database System Concepts | Silberschatz 等 | 基础 |
| SQL Performance Explained | Winand | SQL 优化 |

### 特定数据库

| 书籍 | 数据库 | 作者 |
|------|--------|------|
| Learning SQL | 通用 | Beaulieu |
| PostgreSQL | PostgreSQL | Obe, Hsu |
| MongoDB: The Definitive Guide | MongoDB | Chodorow |
| Redis in Action | Redis | Carlson |

## 机器学习

### 基础 ML

| 书籍 | 作者 | 级别 |
|------|------|------|
| Pattern Recognition and Machine Learning | Bishop | 高级 |
| The Elements of Statistical Learning | Hastie 等 | 高级 |
| An Introduction to Statistical Learning | James 等 | 入门 |
| Hands-On Machine Learning | Geron | 实践 |

### 深度学习

| 书籍 | 作者 | 重点 |
|------|------|------|
| Deep Learning | Goodfellow 等 | 理论 |
| Deep Learning with Python | Chollet | Keras 实践 |
| Programming PyTorch | Stevens | PyTorch 实践 |
| Natural Language Processing | Jurafsky, Martin | NLP 理论 |

### 实践 ML

| 书籍 | 作者 | 重点 |
|------|------|------|
| Python Machine Learning | Raschka | Scikit-learn |
| Machine Learning Engineering | Huyen | 生产 ML |
| Designing Machine Learning Systems | Huyen | 系统设计 |
| Feature Engineering for Machine Learning | Zheng, Casari | 特征工程 |

## 阅读建议

### 按经验水平

| 级别 | 推荐书籍 |
|------|----------|
| 入门 | Clean Code, Python Crash Course, Head First Java |
| 中级 | CLRS, Design Patterns, Effective Java |
| 高级 | Structure and Interpretation, TAOCP, DDIA |

### 按职业路径

| 路径 | 推荐书籍 |
|------|----------|
| Web 开发者 | Eloquent JavaScript, Node.js Design Patterns |
| 系统程序员 | Computer Systems, Operating Systems: Three Easy Pieces |
| 数据工程师 | Designing Data-Intensive Applications, Database Internals |
| ML 工程师 | Hands-On ML, Deep Learning, ML Engineering |

## 总结

本收藏为各级软件开发者提供了综合阅读列表。从基础开始，逐步深入语言特定文本、算法和系统设计，为软件开发生涯奠定坚实基础。


---

## 来源：awesome.md

## 简介

Awesome 列表是社区策划的高质量资源集合，涵盖特定主题。Sindre Sorhus 的 awesome 项目建立了在编程、技术和其他领域创建组织良好、维护良好的列表的标准。

## 目录

1. [什么是 Awesome 列表](#什么是-awesome-列表)
2. [发现 Awesome 列表](#发现-awesome-列表)
3. [热门类别](#热门类别)
4. [为列表贡献](#为列表贡献)
5. [创建自己的列表](#创建自己的列表)
6. [列表质量标准](#列表质量标准)
7. [自动化工具](#自动化工具)

## 什么是 Awesome 列表

### 特点

| 特点 | 说明 |
|------|------|
| 精选 | 按质量而非数量选择 |
| 社区驱动 | 开放贡献 |
| 维护良好 | 定期更新 |
| 专注 | 每个列表单一主题 |
| 链接 | 每个条目都有描述和 URL |

### 优势

| 优势 | 说明 |
|------|------|
| 发现 | 快速找到相关资源 |
| 质量 | 经社区预先审核 |
| 组织 | 按类别结构化 |
| 时效 | 定期维护 |
| 免费 | 开源且可访问 |

## 发现 Awesome 列表

### 发现方式

| 方式 | 说明 |
|------|------|
| Awesome Search | https://awesome.re |
| GitHub Topics | 搜索 "awesome" 主题 |
| Awesome Index | https://github.com/sindresorhus/awesome |
| Awesome Search | https://awesomelists.top |

### 搜索技巧

| 技巧 | 示例 |
|------|------|
| GitHub 搜索 | `awesome TOPIC in:name` |
| 主题浏览 | github.com/topics/awesome |
| 网页搜索 | `awesome list TOPIC` |

## 热门类别

### 编程语言

| 列表 | 仓库 | Star 数 |
|------|------|---------|
| Awesome Python | vinta/awesome-python | 200k+ |
| Awesome JavaScript | sindresorhus/awesome-javascript | 30k+ |
| Awesome Rust | rust-unofficial/awesome-rust | 40k+ |
| Awesome Go | avelino/awesome-go | 120k+ |
| Awesome Java | akullpp/awesome-java | 40k+ |

### Web 开发

| 列表 | 仓库 | 重点 |
|------|------|------|
| Awesome React | brillout/awesome-react-components | React |
| Awesome Vue | vuejs/awesome-vue | Vue.js |
| Awesome Node | sindresorhus/awesome-nodejs | Node.js |
| Awesome CSS | awesome-css-group/awesome-css | CSS |
| Awesome TypeScript | dzharii/awesome-typescript | TypeScript |

### DevOps 与基础设施

| 列表 | 仓库 | 重点 |
|------|------|------|
| Awesome Docker | veggiemonk/awesome-docker | Docker |
| Awesome Kubernetes | ramitsurana/awesome-kubernetes | K8s |
| Awesome Terraform | shuaibiyy/awesome-terraform | IaC |
| Awesome Selfhosted | awesome-selfhosted/awesome-selfhosted | 自托管 |
| Awesome Sysadmin | awesome-foss/awesome-sysadmin | 系统管理 |

### 数据科学与 ML

| 列表 | 仓库 | 重点 |
|------|------|------|
| Awesome Machine Learning | josephmisiti/awesome-machine-learning | ML |
| Awesome Data Science | academic/awesome-datascience | 数据科学 |
| Awesome Deep Learning | ChristosChristofidis/awesome-deep-learning | 深度学习 |
| Awesome NLP | keon/awesome-nlp | NLP |

### 移动开发

| 列表 | 仓库 | 重点 |
|------|------|------|
| Awesome Android | JStumpp/awesome-android | Android |
| Awesome iOS | vsouza/awesome-ios | iOS |
| Awesome Flutter | Solido/awesome-flutter | Flutter |
| Awesome React Native | jondot/awesome-react-native | React Native |

### 安全

| 列表 | 仓库 | 重点 |
|------|------|------|
| Awesome Security | sbilly/awesome-security | 通用 |
| Awesome Appsec | paragonie/awesome-appsec | 应用 |
| Awesome Hacking | Hack-with-Github/Awesome-Hacking | 黑客 |
| Awesome Malware Analysis | rshipp/awesome-malware-analysis | 恶意软件 |

### 职业与学习

| 列表 | 仓库 | 重点 |
|------|------|------|
| Awesome Interviews | DopplerHQ/awesome-interview-questions | 面试 |
| Awesome Learning | learn-anything/learning | 学习路径 |
| Awesome Certifications | cloudcommunity/Free-Certifications | 认证 |
| Awesome Courses | prakhar1989/awesome-courses | CS 课程 |

## 为列表贡献

### 贡献流程

| 步骤 | 操作 |
|------|------|
| 1 | 找到您专业领域的列表 |
| 2 | 阅读贡献指南 |
| 3 | 检查是否有重复 |
| 4 | 以正确格式添加条目 |
| 5 | 提交 pull request |
| 6 | 回应审查反馈 |

### 条目格式

```markdown
- [资源名称](https://example.com) - 资源的简要描述。
```

### 质量标准

| 标准 | 说明 |
|------|------|
| 活跃 | 仓库或网站仍在维护 |
| 有文档 | 有 README 或文档 |
| 有用 | 提供明确价值 |
| 可访问 | 大多数用户可用 |
| 非推广 | 不以营销为主 |

### Pull Request 最佳实践

| 实践 | 说明 |
|------|------|
| 每个 PR 一个条目 | 便于审查 |
| 正确放置 | 在适当类别中 |
| 描述 | 清晰、简洁 |
| 链接质量 | 可用、永久链接 |
| 无重复 | 检查现有条目 |

## 创建自己的列表

### 规划阶段

| 步骤 | 操作 |
|------|------|
| 1 | 选择特定主题 |
| 2 | 检查是否有现有列表 |
| 3 | 定义范围和类别 |
| 4 | 收集初始资源 |
| 5 | 编写贡献指南 |

### 仓库结构

```
awesome-topic/
├── README.md
├── CONTRIBUTING.md
├── .github/
│   └── ISSUE_TEMPLATE.md
└── .pull_request_template.md
```

### README 模板

```markdown
# Awesome Topic [![Awesome](https://awesome.re/badge.svg)](https://awesome.re)

> [主题] 的精选资源列表

## 目录

- [类别 1](#类别-1)
- [类别 2](#类别-2)

## 类别 1

- [资源](https://example.com) - 描述。

## 贡献

请先阅读 [CONTRIBUTING.md](CONTRIBUTING.md)。
```

### 类别组织

| 方式 | 示例 |
|------|------|
| 按类型 | 库、工具、教程 |
| 按级别 | 初级、中级、高级 |
| 按用途 | Web、移动、桌面 |
| 按功能 | 认证、数据库、UI |

## 列表质量标准

### Awesome 列表要求

| 要求 | 说明 |
|------|------|
| 专注 | 单一、明确的主题 |
| 精选 | 质量优于数量 |
| 有描述 | 每个条目都有描述 |
| 格式一致 | 一致的 markdown |
| 维护良好 | 定期更新 |
| 有贡献指南 | 明确的贡献规则 |

### 条目质量

| 方面 | 好 | 差 |
|------|----|----|
| 描述 | "快速、轻量的 Go HTTP 框架" | "一个 Go 框架" |
| 链接 | 直接指向项目 | 链接到博客文章 |
| 格式 | 与列表一致 | 随意格式 |
| 相关性 | 核心主题 | 边缘相关 |

### 反模式

| 模式 | 为什么不好 |
|------|------------|
| 链接堆积 | 无策划或描述 |
| 自我推广 | 营销而非价值 |
| 死链 | 维护不善 |
| 过时内容 | 降低实用性 |
| 范围太广 | 失去焦点 |

## 自动化工具

### 链接检查

| 工具 | 用途 | 平台 |
|------|------|------|
| awesome-lint | 验证 awesome 列表 | Node.js |
| markdown-link-check | 检查死链 | Node.js |
| lychee | 快速链接检查器 | Rust |

### CI/CD 集成

```yaml
# .github/workflows/check.yml
name: Check Links
on:
  push:
    paths:
      - 'README.md'
  pull_request:
    paths:
      - 'README.md'

jobs:
  check:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v3
      - uses: lycheeverse/lychee-action@v1
        with:
          args: README.md
```

### Awesome Lint

| 检查 | 说明 |
|------|------|
| 标题结构 | 正确的标题层级 |
| 列表格式 | 一致的列表标记 |
| 链接有效性 | 可用链接 |
| 描述质量 | 非空描述 |
| 目录匹配 | 目录部分与标题匹配 |

### GitHub Actions for Awesome 列表

| Action | 用途 |
|--------|------|
| Stale issues | 关闭不活跃的 issue |
| PR labeler | 自动标记 PR |
| Link checker | 推送时验证链接 |
| Awesome lint | 验证格式 |

## 维护列表

### 定期任务

| 任务 | 频率 |
|------|------|
| 检查死链 | 每月 |
| 审查开放 PR | 每周 |
| 更新描述 | 按需 |
| 移除过时条目 | 每季度 |
| 添加新资源 | 发现时 |

### 社区管理

| 活动 | 响应时间 |
|------|----------|
| Issue 分类 | 1-2 天 |
| PR 审查 | 3-5 天 |
| 反馈回复 | 1 周 |
| 文档更新 | 按需 |

### 增长策略

| 策略 | 说明 |
|------|------|
| 社交媒体 | 在 Twitter、Reddit 分享 |
| 交叉链接 | 从相关列表链接 |
| 会议演讲 | 在聚会上展示 |
| 通讯 | 精选邮件更新 |

## 总结

Awesome 列表提供了一种结构化的、社区驱动的方式来策划特定主题的高质量资源。遵循既定的格式、贡献指南和质量标准，可确保列表在增长过程中保持有用和可维护。


---

## 来源：papers.md

## 概述

**Papers We Love (PWL)** 是一个围绕计算机科学学术论文展开的社区，专注于论文的阅读、讨论和学习。该社区整理了一份高质量论文目录，汇集了散布在网络各处的经典文档。

- **社区网站**: [paperswelove.org](http://paperswelove.org/)
- **视频资源**: [YouTube 频道](https://www.youtube.com/user/PapersWeLove) -- 包含演讲视频和播放列表
- **社区讨论**: [Discord 服务器](https://discord.gg/Tu2VynkRWV)

> 注意：受版权限制，部分论文无法直接托管，但均提供了外部链接。

---

## 论文查找资源

以下平台和资源库可用于查找计算机科学领域的学术论文：

### 综合论文平台

| 平台 | 链接 | 说明 |
|------|------|------|
| arXiv | [arxiv.org](http://arxiv.org/) | 最大的预印本论文仓库，涵盖计算机科学各领域 |
| Google Scholar | [scholar.google.com](http://scholar.google.com/citations?view_op=top_voices&hl=en&vq=eng) | 学术搜索引擎，可按子类别筛选 |
| SciRate | [scirate.com](https://scirate.com/) | arXiv 论文评分和推荐平台 |
| alphaXiv | [alphaxiv.org](https://www.alphaxiv.org/) | 在 arXiv 论文基础上增加讨论层（将 URL 中的 "arxiv" 替换为 "alphaxiv"） |

### 企业研究机构

| 机构 | 链接 | 说明 |
|------|------|------|
| Microsoft Research | [microsoft.com/research](https://www.microsoft.com/en-us/research/publications/) | 微软研究院论文库 |
| Facebook Research | [research.facebook.com](https://research.facebook.com/publications/) | Meta/Facebook 研究论文 |
| Bell Labs | [bell-labs.com](https://www.bell-labs.com/our-research/technical-journal/) | 贝尔实验室技术期刊 (1922-1983) |

### 学术机构

| 机构 | 链接 | 说明 |
|------|------|------|
| MIT AI Lab | [dspace.mit.edu](http://dspace.mit.edu/handle/1721.1/39813) | MIT 人工智能实验室论文 |
| MIT 分布式系统阅读组 | [dsrg.pdos.csail.mit.edu](http://dsrg.pdos.csail.mit.edu/) | MIT 分布式系统研究组推荐阅读 |
| CMU Robert Harper 论文集 | [cs.cmu.edu/~rwh/papers](https://www.cs.cmu.edu/~rwh/papers/index.html) | 卡内基梅隆大学 Robert Harper 教授的研究论文 |

### 专题资源

| 主题 | 链接 | 说明 |
|------|------|------|
| 分布式系统 | [Readings in Distributed Systems](http://christophermeiklejohn.com/distributed/systems/2013/07/12/readings-in-distributed-systems.html) | 分布式系统经典论文阅读清单 |
| 安全数据科学 | [covert.io](http://www.covert.io/the-definitive-security-datascience-and-machinelearning-guide/) | 安全领域数据科学与机器学习论文 |
| 服务工程 | [services-engineering](https://github.com/mmcgrana/services-engineering) | 服务工程领域阅读清单 |
| 函数式编程 | [Functional Programming Books Review](http://alexott.net/en/fp/books/) | 函数式编程书籍和论文评审 |
| 渐进类型 | [Gradual Typing Bibliography](http://samth.github.io/gradual-typing-bib/) | 渐进类型系统文献目录 |
| 应用机器学习 | [eugeneyan/applied-ml](https://github.com/eugeneyan/applied-ml) | 工业界应用 ML 论文和案例 |

### 论文聚合与社区

| 来源 | 链接 | 说明 |
|------|------|------|
| 2 Minute Papers | [YouTube](https://www.youtube.com/user/keeroyz) | 用短视频快速解读最新论文 |
| The Morning Paper | [blog.acolyer.org](http://blog.acolyer.org/) | 每天解读一篇计算机科学论文 |
| Best Paper Awards | [jeffhuang.com](http://jeffhuang.com/best_paper_awards.html) | 计算机科学领域最佳论文奖汇总 |
| y-archive | [yarchive.net](http://yarchive.net/comp/index.html) | 计算机科学经典文章存档 |
| cat-v.org | [doc.cat-v.org](http://doc.cat-v.org/) | 计算机科学文档集合 |
| netlib | [netlib.org](http://www.netlib.org/) | 数学和数值计算软件库 |
| Lobste.rs PDF | [lobste.rs/t/pdf](https://lobste.rs/t/pdf) | Lobste.rs 社区标记为 PDF 的文章 |

---

## 论文阅读方法

阅读学术论文与阅读博客或书籍不同。以下资源提供了系统的论文阅读方法论：

| 资源 | 链接 | 核心要点 |
|------|------|----------|
| How to read an academic article | [链接](http://organizationsandmarkets.com/2010/08/31/how-to-read-an-academic-article/) | 学术文章阅读技巧 |
| Advice on reading academic papers | [链接](https://userpages.umbc.edu/~akmassey/posts/2012-02-15-advice-on-reading-academic-papers.html) | 学术论文阅读建议 |
| How to read and understand a scientific paper | [链接](http://violentmetaphors.com/2013/08/25/how-to-read-and-understand-a-scientific-paper-2/) | 科学论文理解方法 |
| Should I Read Papers? | [链接](http://michaelrbernste.in/2014/10/21/should-i-read-papers.html) | 论文阅读的价值探讨 |
| The Refreshingly Rewarding Realm of Research Papers | [YouTube](https://www.youtube.com/watch?v=8eRx5Wo3xYA) | 研究论文的视频讲解 |
| How to read a paper (Keshav) | [PDF](http://ccr.sigcomm.org/online/files/p83-keshavA.pdf) | 三遍阅读法：略读、精读、总结 |

### 论文阅读三遍法 (Keshav 方法)

| 阶段 | 目标 | 时间 | 方法 |
|------|------|------|------|
| 第一遍 | 鸟瞰全文 | 5-10 分钟 | 阅读标题、摘要、引言、各节标题、结论 |
| 第一遍后 | 决定是否继续 | - | 判断论文与研究方向的相关性 |
| 第二遍 | 理解核心内容 | 最多 1 小时 | 精读全文，忽略证明细节，标注关键引用 |
| 第三遍 | 虚拟重现论文 | 4-5 小时 | 尝试从零重构论文，识别创新点和隐含假设 |

---

## 批量下载论文

PWL 提供了脚本工具，可批量下载仓库中链接的 PDF 论文：

```bash
./scripts/download.sh
```

该脚本会解析 Markdown 文件中的 PDF 链接，并将论文下载到对应目录。详见仓库中的 `scripts/README.md`。

---

## 关键要点

1. **PWL 是起点，不是终点** -- 该仓库提供了精选论文目录，但更多论文散布在各类平台和机构网站上
2. **掌握阅读方法比大量阅读更重要** -- Keshav 的三遍阅读法是高效阅读论文的基础框架
3. **利用视频资源降低入门门槛** -- 2 Minute Papers 和 PWL YouTube 频道提供了直观的论文解读
4. **按专题深入** -- 分布式系统、安全数据科学、服务工程等领域都有专门的阅读清单
5. **结合讨论深化理解** -- 加入 Discord 社区或本地分会，通过讨论加深对论文的理解


---

## 来源：index.md

## 简介

"Awesome"运动起源于 GitHub，是一种为任何主题精选最佳资源的方式。本指南从最大的 awesome 列表中提炼出最重要的类别，为开发者、设计师和学习者提供一个有组织的参考。

## 目录

- [平台](#平台)
- [编程语言](#编程语言)
- [前端开发](#前端开发)
- [后端开发](#后端开发)
- [计算机科学](#计算机科学)
- [数据科学](#数据科学)
- [理论](#理论)
- [书籍](#书籍)
- [编辑器](#编辑器)
- [游戏开发](#游戏开发)
- [开发环境](#开发环境)
- [媒体](#媒体)
- [商业](#商业)
- [工作](#工作)
- [网络](#网络)
- [安全](#安全)
- [内容管理系统](#内容管理系统)
- [硬件](#硬件)
- [其他](#其他)

---

## 平台

主要操作系统和平台的资源。

### 操作系统

| 操作系统 | 类型 | 最佳资源 | 重点方向 |
|----------|------|----------|----------|
| Linux | 开源 | kernel.org、Arch Wiki | 系统管理、内核开发 |
| macOS | 专有 | developer.apple.com | 应用开发、SwiftUI |
| Windows | 专有 | docs.microsoft.com | .NET、Azure 集成 |
| FreeBSD | 开源 | freebsd.org | 网络、安全 |

### 移动平台

| 平台 | 语言 | IDE | 关键资源 |
|------|------|-----|----------|
| iOS | Swift、Objective-C | Xcode | HIG、Swift 文档 |
| Android | Kotlin、Java | Android Studio | Material Design、Jetpack |
| Flutter | Dart | VS Code、Android Studio | 跨平台 UI |
| React Native | JavaScript | VS Code | 使用 React 的跨平台开发 |

### 云平台

| 提供商 | 优势 | 免费层 |
|--------|------|--------|
| AWS | 最广泛的服务目录 | 12 个月有限免费 |
| Google Cloud | AI/ML、Kubernetes | 永久免费层 |
| Azure | 企业级、.NET 集成 | 12 个月有限免费 |
| DigitalOcean | 简单、定价透明 | $200 额度 |
| Vercel | 前端托管 | 慷慨的免费层 |
| Cloudflare | CDN、安全 | 有免费层 |

---

## 编程语言

流行编程语言的核心资源。

### 语言概览

| 语言 | 类型 | 主要用途 | 学习曲线 |
|------|------|----------|----------|
| Python | 解释型 | 数据科学、Web、自动化 | 低 |
| JavaScript | 解释型 | Web（前后端） | 低-中 |
| TypeScript | 编译型 | 类型安全的 JavaScript | 中 |
| Rust | 编译型 | 系统编程、高性能 | 高 |
| Go | 编译型 | 后端服务、CLI 工具 | 中 |
| Java | 编译型 | 企业级、Android | 中 |
| C# | 编译型 | 企业级、游戏开发 (.NET) | 中 |
| C++ | 编译型 | 系统编程、游戏引擎 | 高 |
| Swift | 编译型 | iOS、macOS 开发 | 中 |
| Kotlin | 编译型 | Android、服务端 | 中 |

### 语言专属资源

| 语言 | 必读资源 | 练习平台 |
|------|----------|----------|
| Python | Python.org 教程 | LeetCode、HackerRank |
| JavaScript | MDN Web Docs | freeCodeCamp |
| Rust | The Rust Book | Exercism |
| Go | Go Tour、Go by Example | Exercism |
| Java | Oracle 教程 | CodeGym |

---

## 前端开发

构建用户界面和 Web 体验的资源。

### 框架和库

| 框架 | 类型 | 语言 | 最佳用途 |
|------|------|------|----------|
| React | 库 | JavaScript | 组件化 UI |
| Vue.js | 框架 | JavaScript | 渐进式增强 |
| Angular | 框架 | TypeScript | 企业级应用 |
| Svelte | 框架 | JavaScript | 最小运行时 |
| Next.js | 框架 | React | 全栈 React 应用 |
| Nuxt.js | 框架 | Vue | 全栈 Vue 应用 |
| Astro | 框架 | 多语言 | 内容为主的网站 |

### CSS 资源

| 工具/方法 | 描述 | 使用时机 |
|-----------|------|----------|
| Tailwind CSS | 工具优先的 CSS | 快速原型、一致设计 |
| CSS Modules | 作用域 CSS | 组件化应用 |
| Styled Components | CSS-in-JS | React 应用 |
| Sass | CSS 预处理器 | 大型样式表 |
| PostCSS | CSS 转换器 | 自定义处理流程 |

### JavaScript 核心知识

| 概念 | 描述 | 资源 |
|------|------|------|
| ES6+ 特性 | 现代 JavaScript 语法 | MDN、javascript.info |
| 异步编程 | Promises、async/await | javascript.info |
| DOM 操作 | 操作 HTML 元素 | MDN |
| 模块系统 | import/export 模式 | MDN |
| 构建工具 | Webpack、Vite、esbuild | 官方文档 |

### 无障碍

| 标准 | 描述 | 关键要求 |
|------|------|----------|
| WCAG 2.1 | Web 内容无障碍指南 | 可感知、可操作、可理解、健壮性 |
| WAI-ARIA | 无障碍富互联网应用 | 角色、状态、属性 |
| Section 508 | 美国联邦无障碍法 | 政府网站合规 |

---

## 后端开发

服务端编程、API 和基础设施的资源。

### 后端框架

| 框架 | 语言 | 类型 | 最佳用途 |
|------|------|------|----------|
| Express.js | JavaScript | 极简 | REST API、微服务 |
| Django | Python | 全功能 | 快速开发 |
| Flask | Python | 极简 | API、微服务 |
| Spring Boot | Java | 全功能 | 企业级应用 |
| Ruby on Rails | Ruby | 全功能 | 创业公司、快速原型 |
| FastAPI | Python | 现代 | 高性能 API |
| Gin | Go | 极简 | 高性能 API |
| Actix | Rust | 高性能 | 极致性能 |

### API 设计

| 风格 | 描述 | 最佳用途 |
|------|------|----------|
| REST | 基于资源、HTTP 方法 | CRUD 操作、公开 API |
| GraphQL | API 查询语言 | 复杂数据需求 |
| gRPC | Protocol Buffers、HTTP/2 | 微服务通信 |
| WebSocket | 持久连接 | 实时应用 |

### 数据库

| 类型 | 示例 | 最佳用途 |
|------|------|----------|
| 关系型 | PostgreSQL、MySQL、SQLite | 结构化数据、事务 |
| 文档型 | MongoDB、CouchDB | 灵活模式、JSON 数据 |
| 键值型 | Redis、DynamoDB | 缓存、会话 |
| 图数据库 | Neo4j、ArangoDB | 关系、网络 |
| 时序数据库 | InfluxDB、TimescaleDB | 指标、监控 |
| 搜索引擎 | Elasticsearch、Meilisearch | 全文搜索 |

---

## 计算机科学

基础计算机科学资源。

### 算法和数据结构

| 类别 | 关键主题 | 资源 |
|------|----------|------|
| 排序 | QuickSort、MergeSort、HeapSort | CLRS、Sedgewick 算法 |
| 搜索 | 二分查找、哈希表 | VisuAlgo |
| 树 | BST、AVL、红黑树、B 树 | CS201 课程 |
| 图 | BFS、DFS、Dijkstra、A* | Khan Academy、MIT OCW |
| 动态规划 | 记忆化、制表 | LeetCode、NeetCode |

### 操作系统

| 主题 | 核心概念 | 资源 |
|------|----------|------|
| 进程管理 | 线程、调度、同步 | OSTEP 教材 |
| 内存管理 | 虚拟内存、分页、缓存 | OSTEP 教材 |
| 文件系统 | inode、日志、RAID | OSTEP 教材 |
| 并发 | 锁、信号量、条件变量 | OSTEP 教材 |

### 计算机网络

| 层级 | 协议 | 资源 |
|------|------|------|
| 应用层 | HTTP、DNS、SMTP、FTP | Computer Networking: A Top-Down Approach |
| 传输层 | TCP、UDP | Beej's Guide to Network Programming |
| 网络层 | IP、ICMP、路由 | Computer Networks by Tanenbaum |
| 数据链路层 | Ethernet、WiFi | IEEE 802 标准 |

---

## 数据科学

数据分析、机器学习和人工智能的资源。

### 机器学习

| 类别 | 算法 | 库 |
|------|------|-----|
| 监督学习 | 线性回归、SVM、随机森林 | scikit-learn、XGBoost |
| 无监督学习 | K-means、PCA、DBSCAN | scikit-learn |
| 深度学习 | CNN、RNN、Transformer | PyTorch、TensorFlow |
| 强化学习 | Q-learning、策略梯度 | OpenAI Gym、Stable Baselines |

### 数据可视化

| 工具 | 类型 | 最佳用途 |
|------|------|----------|
| Matplotlib | Python 库 | 统计图表 |
| Seaborn | Python 库 | 统计可视化 |
| D3.js | JavaScript 库 | 自定义 Web 可视化 |
| Plotly | 多语言 | 交互式图表 |
| Tableau | 桌面/云 | 商业仪表板 |
| Observable | Web | 数据笔记本 |

### 数据工程

| 工具 | 用途 | 类别 |
|------|------|------|
| Apache Spark | 大规模数据处理 | 处理 |
| Apache Kafka | 事件流 | 流处理 |
| Apache Airflow | 工作流编排 | 编排 |
| dbt | 数据转换 | 转换 |
| Snowflake | 云数据仓库 | 存储 |

---

## 理论

理论计算机科学和基础概念。

### 复杂性理论

| 类别 | 描述 | 示例 |
|------|------|------|
| P | 多项式时间可解 | 排序、最短路径 |
| NP | 多项式时间可验证 | SAT、旅行商问题 |
| NP-Complete | NP 中最难的问题 | 布尔可满足性 |
| NP-Hard | 至少和 NP-Complete 一样难 | 停机问题 |

### 形式语言

| 类型 | 文法 | 自动机 | 示例 |
|------|------|--------|------|
| 正则 | 类型 3 | 有限自动机 | 邮箱验证 |
| 上下文无关 | 类型 2 | 下推自动机 | 编程语言 |
| 上下文相关 | 类型 1 | 线性有界自动机 | 自然语言 |
| 递归可枚举 | 类型 0 | 图灵机 | 通用计算 |

---

## 书籍

开发者和技术人员的必读书籍。

### 必读技术书籍

| 书籍 | 主题 | 级别 |
|------|------|------|
| Structure and Interpretation of Computer Programs | 计算机科学基础 | 中级 |
| Clean Code | 编写可读代码 | 初级-中级 |
| Design Patterns | 软件架构 | 中级 |
| The Pragmatic Programmer | 软件工匠精神 | 中级 |
| Introduction to Algorithms (CLRS) | 算法 | 中级-高级 |
| The Art of Computer Programming | 算法深入 | 高级 |
| Refactoring | 代码改进 | 中级 |
| Working Effectively with Legacy Code | 维护现有代码 | 中级 |

### 职业和软技能

| 书籍 | 主题 |
|------|------|
| The Mythical Man-Month | 软件项目管理 |
| Peopleware | 团队生产力 |
| The Cathedral and the Bazaar | 开源开发 |
| Coders at Work | 优秀程序员访谈 |
| Apprenticeship Patterns | 开发者职业成长 |

---

## 编辑器

文本编辑器和集成开发环境。

### 编辑器对比

| 编辑器 | 类型 | 平台 | 价格 | 最佳用途 |
|--------|------|------|------|----------|
| VS Code | 编辑器 | 跨平台 | 免费 | 通用开发 |
| Vim/Neovim | 编辑器 | 跨平台 | 免费 | 终端编辑 |
| JetBrains IDEs | IDE | 跨平台 | 付费 | 语言专属 IDE |
| Sublime Text | 编辑器 | 跨平台 | 付费 | 快速编辑 |
| Emacs | 编辑器 | 跨平台 | 免费 | 可扩展性 |
| Zed | 编辑器 | 跨平台 | 免费 | 现代、快速 |

### VS Code 提效扩展

| 扩展 | 用途 |
|------|------|
| GitLens | 增强 Git 集成 |
| ESLint | JavaScript 代码检查 |
| Prettier | 代码格式化 |
| Docker | 容器管理 |
| Remote SSH | 编辑远程服务器上的文件 |
| Thunder Client | API 测试 |

---

## 游戏开发

游戏开发资源。

### 游戏引擎

| 引擎 | 语言 | 平台 | 最佳用途 |
|------|------|------|----------|
| Unity | C# | 全平台 | 2D/3D 独立和移动游戏 |
| Unreal Engine | C++、蓝图 | 全平台 | AAA 和高保真 3D |
| Godot | GDScript、C# | 全平台 | 开源 2D/3D |
| GameMaker | GML | 全平台 | 2D 游戏 |
| Bevy | Rust | 全平台 | 基于 ECS 的 2D/3D |

### 游戏开发资源

| 类别 | 资源 | 类型 |
|------|------|------|
| 图形 | Learn OpenGL | 教程 |
| 物理 | Game Physics Engine Development | 书籍 |
| AI | AI for Games by Ian Millington | 书籍 |
| 美术 | OpenGameArt.org | 素材 |
| 音效 | Freesound.org | 音频 |

---

## 开发环境

高效开发的工具和配置。

### 终端和 Shell

| 工具 | 类型 | 核心功能 |
|------|------|----------|
| Zsh + Oh My Zsh | Shell | 可定制、插件丰富 |
| Fish | Shell | 用户友好、自动建议 |
| tmux | 终端复用器 | 会话管理 |
| Kitty | 终端模拟器 | GPU 加速 |
| Alacritty | 终端模拟器 | 快速、极简 |

### 版本控制

| 工具 | 类型 | 最佳用途 |
|------|------|----------|
| Git | 分布式版本控制 | 所有项目 |
| GitHub | 托管 | 开源、协作 |
| GitLab | 托管 | 自托管、CI/CD |
| Bitbucket | 托管 | Atlassian 生态系统 |

### 容器化

| 工具 | 类型 | 最佳用途 |
|------|------|----------|
| Docker | 容器运行时 | 应用打包 |
| Podman | 容器运行时 | 无 root 容器 |
| Docker Compose | 多容器 | 开发环境 |
| Kubernetes | 编排 | 生产部署 |

---

## 媒体

媒体创作和消费的资源。

### 图像工具

| 工具 | 类型 | 平台 | 价格 |
|------|------|------|------|
| GIMP | 图片编辑 | 跨平台 | 免费 |
| Inkscape | 矢量编辑 | 跨平台 | 免费 |
| Krita | 数字绘画 | 跨平台 | 免费 |
| Figma | UI 设计 | Web | 免费版 |
| Blender | 3D 创作 | 跨平台 | 免费 |

### 视频工具

| 工具 | 类型 | 价格 |
|------|------|------|
| OBS Studio | 屏幕录制/直播 | 免费 |
| DaVinci Resolve | 视频编辑 | 免费版 |
| FFmpeg | 视频处理 CLI | 免费 |
| Kdenlive | 视频编辑 | 免费 |

### 音频工具

| 工具 | 类型 | 价格 |
|------|------|------|
| Audacity | 音频编辑 | 免费 |
| Ardour | DAW | 免费/付费 |
| LMMS | 音乐制作 | 免费 |
| OBS Studio | 音频捕获 | 免费 |

---

## 商业

科技商业和创业资源。

### 创业资源

| 类别 | 资源 | 类型 |
|------|------|------|
| 商业模式 | Business Model Canvas | 框架 |
| 精益创业 | The Lean Startup by Eric Ries | 书籍 |
| 增长 | Traction by Gabriel Weinberg | 书籍 |
| 融资 | Venture Deals by Brad Feld | 书籍 |
| 指标 | Lean Analytics by Alistair Croll | 书籍 |

### SaaS 指标

| 指标 | 公式 | 良好基准 |
|------|------|----------|
| MRR | 月经常性收入总和 | 逐月增长 |
| 流失率 | (流失客户 / 总数) x 100 | < 5% 月 |
| LTV | ARPU / 流失率 | > 3x CAC |
| CAC | 总营销费用 / 新客户 | 取决于上下文 |
| NRR | (期初 MRR + 扩展 - 收缩 - 流失) / 期初 MRR | > 100% |

---

## 工作

远程工作、生产力和职业发展资源。

### 远程工作工具

| 类别 | 工具 |
|------|------|
| 沟通 | Slack、Discord、Microsoft Teams |
| 视频 | Zoom、Google Meet、Whereby |
| 项目管理 | Linear、Jira、Notion、Trello |
| 文档 | Notion、Confluence、GitBook |
| 设计 | Figma、Miro、FigJam |
| 时间追踪 | Toggl、Clockify |

### 效率方法

| 方法 | 描述 | 最佳用途 |
|------|------|----------|
| 番茄工作法 | 25 分钟工作，5 分钟休息 | 专注时段 |
| Getting Things Done | 捕获、澄清、组织、反思、执行 | 任务管理 |
| 时间块 | 为特定工作安排时间块 | 深度工作 |
| 艾森豪威尔矩阵 | 紧急/重要优先级 | 优先级决策 |
| 看板 | 可视化看板 + WIP 限制 | 团队工作流 |

---

## 网络

计算机网络和基础设施资源。

### 网络工具

| 工具 | 用途 | 平台 |
|------|------|------|
| Wireshark | 数据包分析 | 跨平台 |
| nmap | 网络扫描 | 跨平台 |
| tcpdump | 数据包捕获 | Linux/macOS |
| curl | HTTP 客户端 | 跨平台 |
| Postman | API 测试 | 跨平台 |
| ngrok | 本地隧道 | 跨平台 |

### 网络协议

| 协议 | 端口 | 用途 |
|------|------|------|
| HTTP/HTTPS | 80/443 | Web 流量 |
| SSH | 22 | 安全 Shell |
| DNS | 53 | 域名解析 |
| SMTP | 25 | 邮件发送 |
| FTP | 21 | 文件传输 |
| WebSocket | 80/443 | 实时通信 |

---

## 安全

网络安全和安全开发资源。

### 安全工具

| 工具 | 用途 | 类型 |
|------|------|------|
| OWASP ZAP | Web 应用安全测试 | 扫描器 |
| Burp Suite | Web 应用渗透测试 | 代理/扫描器 |
| Metasploit | 渗透测试框架 | 框架 |
| Nmap | 网络发现 | 扫描器 |
| John the Ripper | 密码破解 | 破解器 |
| Hashcat | 密码破解 | 破解器 |

### 安全最佳实践

| 类别 | 实践 |
|------|------|
| 认证 | 使用多因素认证 |
| 密码 | 使用 bcrypt/argon2 哈希，永远不要存储明文 |
| 输入 | 验证和清理所有用户输入 |
| HTTPS | 加密所有传输中的流量 |
| 依赖 | 定期更新和审计依赖 |
| 密钥 | 使用环境变量，永远不要提交密钥 |
| 头部 | 设置安全头（CSP、HSTS、X-Frame-Options） |

---

## 内容管理系统

CMS 平台和内容管理资源。

### CMS 对比

| CMS | 类型 | 语言 | 最佳用途 |
|-----|------|------|----------|
| WordPress | 传统 | PHP | 博客、小型企业网站 |
| Strapi | 无头 | JavaScript | API 优先的内容 |
| Ghost | 混合 | JavaScript | 出版、新闻通讯 |
| Contentful | 无头 SaaS | N/A | 企业内容 |
| Sanity | 无头 SaaS | JavaScript | 结构化内容 |
| Directus | 无头 | JavaScript | 数据库驱动的内容 |

---

## 硬件

硬件、嵌入式系统和物理计算资源。

### 单板计算机

| 开发板 | CPU | 价格 | 最佳用途 |
|--------|-----|------|----------|
| Raspberry Pi | ARM | $5-80 | 教育、IoT、家庭服务器 |
| Arduino | AVR/ARM | $3-30 | 电子、嵌入式 |
| ESP32 | Xtensa | $3-10 | WiFi/BLE IoT 项目 |
| BeagleBone | ARM | $50+ | 工业、实时 |

### 电子资源

| 主题 | 资源 | 类型 |
|------|------|------|
| 电路设计 | KiCad | 开源 EDA |
| PCB 制造 | JLCPCB、OSH Park | 服务 |
| 学习 | SparkFun、Adafruit | 教程、元件 |
| 仿真 | Tinkercad Circuits | 浏览器仿真器 |

---

## 其他

不适合归入其他类别的资源。

### 实用列表

| 列表 | 主题 | Stars |
|------|------|-------|
| awesome-selfhosted | 自托管软件 | 200k+ |
| awesome-python | Python 资源 | 220k+ |
| awesome-javascript | JavaScript 资源 | 33k+ |
| awesome-go | Go 资源 | 130k+ |
| awesome-rust | Rust 资源 | 47k+ |
| awesome-react | React 资源 | 65k+ |
| awesome-vue | Vue 资源 | 70k+ |
| awesome-machine-learning | ML 资源 | 65k+ |
| awesome-sysadmin | 系统管理 | 25k+ |

### 学习平台

| 平台 | 类型 | 费用 | 最佳用途 |
|------|------|------|----------|
| freeCodeCamp | 交互式 | 免费 | Web 开发 |
| The Odin Project | 课程 | 免费 | 全栈 |
| CS50 (Harvard) | 课程 | 免费 | 计算机科学 |
| MIT OpenCourseWare | 大学课程 | 免费 | CS 理论 |
| Exercism | 练习 | 免费 | 语言学习 |
| LeetCode | 练习 | 免费/付费 | 面试准备 |

---

## 总结

Awesome 列表生态系统代表了开发者社区的集体知识。关键要点：

- **从基础开始**：先掌握一门语言和一个框架再扩展
- **使用精选列表**：Awesome 列表节省了大量搜索优质资源的时间
- **回馈社区**：如果你发现好的资源，添加到相关列表中
- **保持更新**：技术变化快；定期重新审视资源
- **构建项目**：光读资源不够；要应用所学
- **加入社区**：最好的学习发生在协作和讨论中


---
