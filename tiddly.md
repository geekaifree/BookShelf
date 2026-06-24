# TiddlyWiki：个人 Wiki 教程

## 简介

TiddlyWiki 是一个自包含的单文件个人 Wiki。它完全在网页浏览器中运行，无需服务器。本教程涵盖在 TiddlyWiki 中创建、组织和管理知识。

## TiddlyWiki 的独特之处

| 功能 | 描述 |
|------|------|
| 单 HTML 文件 | 整个 Wiki 在一个便携文件中 |
| 无需服务器 | 在任何现代浏览器中运行 |
| 离线优先 | 无需互联网即可工作 |
| 高度可定制 | 内置 JavaScript 和 CSS |
| 非线性 | 以相互关联的 tiddler 组织思路 |
| 开源 | MIT 许可证 |

## 快速开始

### 下载选项

| 选项 | URL | 描述 |
|------|-----|------|
| 空白 Wiki | tiddlywiki.com | 从头开始的空白 Wiki |
| TiddlyWiki on Node.js | npm | 基于服务器的多用户 Wiki |
| TiddlyDesktop | GitHub | 桌面应用封装 |
| Timimi Extension | 浏览器商店 | 从浏览器保存单文件 Wiki |

### Node.js 安装

```bash
npm install -g tiddlywiki
tiddlywiki mywiki --init server
tiddlywiki mywiki --listen
```

| 命令 | 用途 |
|------|------|
| --init server | 创建服务器版 Wiki |
| --init empty | 创建空白 Wiki |
| --listen | 在 8080 端口启动 HTTP 服务器 |
| --build | 构建静态 HTML 输出 |

## 核心概念

### Tiddler

Tiddler 是内容的基本单元。

| 字段 | 类型 | 描述 |
|------|------|------|
| title | String | 唯一标识符（必填） |
| text | String | 主要内容体 |
| tags | List | 分类标签 |
| created | Date | 创建时间戳 |
| modified | Date | 最后修改时间戳 |
| fields | Custom | 任何额外的元数据 |

### 标签

标签创建集合和导航结构。

| 标签 | 用途 |
|------|------|
| GettingStarted | 入门内容 |
| $:/tags/Stylesheet | CSS 自定义 |
| $:/tags/JavaScript | 自定义脚本 |
| $:/tags/Macro | 可复用宏 |
| 自定义标签 | 你的组织系统 |

### 链接和嵌入

| 语法 | 效果 |
|------|------|
| [[Tiddler Title]] | 创建链接 |
| [[Display Text\|Tiddler Title]] | 带自定义文本的链接 |
| {{Tiddler Title}} | 嵌入内容 |
| {{Tiddler Title\|field}} | 嵌入特定字段 |

## 编辑 Tiddler

### 创建 Tiddler

1. 点击侧边栏中的"+"按钮。
2. 输入唯一标题。
3. 使用 wikitext 语法编写内容。
4. 添加标签以便组织。
5. 点击"Done"保存。

### Wikitext 格式

| 语法 | 结果 |
|------|------|
| ''bold'' | 粗体文本 |
| //italic// | 斜体文本 |
| __underline__ | 下划线 |
| ~~strikethrough~~ | 删除线 |
| ^^superscript^^ | 上标 |
| ,,subscript,, | 下标 |
| !Heading 1 | 标题 1 |
| !!Heading 2 | 标题 2 |
| !!!Heading 3 | 标题 3 |
| --- | 水平线 |
| <!-- comment --> | 隐藏注释 |

### 列表

| 语法 | 类型 |
|------|------|
| * Item | 无序列表 |
| # Item | 有序列表 |
| ;Term | 定义术语 |
| :Definition | 定义内容 |

### 代码块

| 语法 | 用途 |
|------|------|
| {{{code}}} | 行内代码 |
| \`\`\` code \`\`\` | 代码块 |
| <pre>code</pre> | 预格式化文本 |

## 宏

宏是可复用的内容模板。

### 内置宏

| 宏 | 用途 | 示例 |
|----|------|------|
| <<now>> | 当前日期/时间 | <<now YYYY-MM-DD>> |
| <<toc>> | 目录 | <<toc "TableOfContents">> |
| <<list-tagged>> | 按标签列出 tiddler | <<list-tagged "Projects">> |
| <<search>> | 搜索框 | <<search>> |
| <<slider>> | 可展开内容 | <<slider "Info">> |

### 自定义宏

```
\rules only filteredtranscludeinline transcludeinline
\define hello(name)
Hello, $name$!
\end

<<hello("World")>>
```

## 插件

### 必备插件

| 插件 | 用途 |
|------|------|
| TiddlyMap | 可视化思维导图和图表 |
| Stroll | 叙事风格布局 |
| TW5-CodeMirror | 更好的代码编辑器 |
| Relink | 自动链接更新 |
| DPL | 动态页面列表 |
| Mermaid | 图表和流程图 |

### 安装插件

1. 打开插件库：$:/core/ui/ControlPanel/Plugins。
2. 浏览或搜索插件。
3. 点击"Install"并重新加载。

## 组织策略

### 基于标签的结构

| 标签 | 内容类型 |
|------|---------|
| Project | 项目描述 |
| Note | 会议记录、想法 |
| Reference | 外部资源 |
| Task | 待办事项 |
| Journal | 每日条目 |
| Template | 可复用模板 |

### 文件夹结构（Node.js 版）

| 文件夹 | 用途 |
|--------|------|
| tiddlers/ | 所有 tiddler 文件 |
| plugins/ | 自定义插件 |
| themes/ | 视觉主题 |
| languages/ | 翻译 |
| output/ | 构建的静态 HTML |

## 过滤器

过滤器用于选择和操作 tiddler。

| 过滤器 | 用途 | 示例 |
|--------|------|------|
| [tag[Project]] | 按标签 | 所有项目 |
| [search[text]] | 全文搜索 | 包含"text" |
| [sort[title]] | 按字母排序 | A-Z 按标题 |
| [limit[10]] | 限制结果 | 前 10 个 |
| [days[-7]] | 最近项目 | 最近 7 天 |
| [is[tiddler]] | 所有 tiddler | 排除系统 |
| [fields:title[My Title]] | 按字段值 | 精确匹配 |
| [!tag[draft]] | 否定 | 排除草稿 |

### 组合过滤器

```
[tag[Project]] +[sort[modified]] +[limit[5]]
// 获取最近修改的 5 个项目
```

## 自定义

### 主题

| 主题 | 风格 |
|------|------|
| Vanilla | 简洁、极简 |
| Snowwhite | 明亮、现代 |
| Plain | 超极简 |
| Custom | 用 CSS 覆盖 |

### 自定义 CSS

创建标记为 $:/tags/Stylesheet 的 tiddler：

```css
.tc-tiddler-title {
  color: #2c3e50;
  font-size: 1.5em;
}
.tc-sidebar {
  background-color: #f8f9fa;
}
```

## 保存和备份

### 单文件 Wiki

| 浏览器 | 保存方法 |
|--------|---------|
| Chrome | Timimi 扩展（推荐） |
| Firefox | Timimi 扩展（推荐） |
| 任意 | 下载按钮，重新上传 |

### Node.js 版

| 方法 | 命令 |
|------|------|
| 自动保存 | 内置，编辑时保存 |
| Git 备份 | git add tiddlers/ && git commit -m "backup" |
| 导出 | tiddlywiki mywiki --build |

## 快捷键

| 快捷键 | 操作 |
|--------|------|
| Ctrl+Enter | 关闭当前 tiddler |
| Ctrl+Shift+E | 编辑当前 tiddler |
| Ctrl+G | 打开搜索 |
| Ctrl+N | 新建 tiddler |
| Ctrl+S | 保存（配合 Timimi） |

## 用例

| 用例 | 组织方式 |
|------|---------|
| 个人知识库 | 按主题标签，日志条目 |
| 项目管理 | 项目标签，任务子标签 |
| 研究笔记 | 来源标签，引用字段 |
| 写作 | 章节标签，草稿/已发布状态 |
| 学习 | 主题标签，间隔重复 |

## 总结

TiddlyWiki 提供了一个独特灵活的个人 Wiki 系统。其单文件便携性、丰富的 wikitext 语法、过滤系统和插件生态系统，使其适用于任何知识管理需求。无论是用作笔记本、项目跟踪器还是研究数据库，TiddlyWiki 都能适应你的工作流程。
