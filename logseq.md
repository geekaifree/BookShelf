# 使用 Logseq 进行知识管理

## 简介

Logseq 是一个隐私优先的开源知识管理平台。它将笔记、大纲和知识图谱功能结合在一个应用中。

### 什么是 Logseq？

Logseq 是一个本地优先的知识库，使用纯文本文件，提供双向链接、块级引用和强大的图谱视图。

| 特性 | 描述 |
|------|------|
| 大纲 | 层级化项目符号编辑 |
| 双向链接 | 自然地连接笔记 |
| 知识图谱 | 连接的可视化表示 |
| 本地优先 | 文件存储在设备上 |
| Markdown/Org-mode | 纯文本格式 |

### 与其他工具的比较

| 特性 | Logseq | Obsidian | Roam |
|------|--------|----------|------|
| 开源 | 是 | 否 | 否 |
| 本地优先 | 是 | 是 | 否 |
| 大纲 | 是 | 部分 | 是 |
| 图谱视图 | 是 | 是 | 是 |
| 免费 | 是 | 免费增值 | 否 |

## 安装

### 系统要求

| 平台 | 要求 |
|------|------|
| Windows | Windows 10+ |
| macOS | macOS 10.15+ |
| Linux | Ubuntu 18.04+ |
| 移动端 | iOS 14+ / Android 8+ |

### 安装方式

```bash
# macOS (Homebrew)
brew install --cask logseq

# Linux (Flatpak)
flatpak install flathub com.logseq.Logseq

# Windows (Winget)
winget install Logseq.Logseq
```

### 下载

访问 https://logseq.com/downloads 获取官方安装包。

## 核心概念

### 页面和块

| 概念 | 描述 |
|------|------|
| 页面 | 文档或主题 |
| 块 | 项目符号或内容单元 |
| 属性 | 附加到块的元数据 |
| 命名空间 | 层级化页面组织 |

### 块结构

```
- Block 1
  - Child block 1.1
  - Child block 1.2
    - Grandchild block
- Block 2
  - Child block 2.1
```

### 页面链接

```markdown
This is a link to [[Another Page]]
This references [[Another Page]] with more context
```

## 日志和每日笔记

### 日志结构

Logseq 自动创建每日日志页面：

```
Journal
├── 2024-01-15
├── 2024-01-14
├── 2024-01-13
└── ...
```

### 日志模板

```markdown
- ## Morning
  - Today's priorities
- ## Notes
  - Meeting notes
- ## Evening
  - Reflections
```

### 每日笔记配置

| 设置 | 描述 |
|------|------|
| 首选格式 | Markdown 或 Org-mode |
| 日志页面标题格式 | 日期格式 |
| 默认模板 | 自动应用的模板 |

## 双向链接

### 创建链接

| 语法 | 结果 |
|------|------|
| `[[Page Name]]` | 链接到页面 |
| `[[Page Name][Display Text]]` | 自定义显示文本的链接 |
| `#Tag` | 标签链接 |
| `#[[Multi Word Tag]]` | 多词标签 |

### 反向链接

当您链接到某个页面时，被链接的页面会自动显示反向引用。

| 功能 | 描述 |
|------|------|
| 链接引用 | 链接到当前页面的页面 |
| 未链接引用 | 没有显式链接的提及 |
| 过滤引用 | 缩小引用列表 |

## 知识图谱

### 图谱视图

图谱视图可视化页面之间的连接：

| 元素 | 含义 |
|------|------|
| 节点 | 页面 |
| 边 | 页面之间的链接 |
| 大小 | 连接数量 |
| 颜色 | 页面类型或标签 |

### 图谱过滤器

| 过滤器 | 用途 |
|--------|------|
| 页面过滤器 | 显示特定页面 |
| 标签过滤器 | 显示带标签的页面 |
| 属性过滤器 | 按属性过滤 |
| 时间过滤器 | 显示日期范围内的页面 |

## 模板

### 创建模板

```markdown
- template:: Meeting Notes
  - Date: 
  - Attendees: 
  - Agenda: 
  - Notes: 
  - Action Items: 
```

### 使用模板

输入 `/Template` 并从可用模板中选择。

### 模板示例

| 模板 | 用例 |
|------|------|
| Meeting Notes | 记录会议详情 |
| Book Notes | 结构化读书笔记 |
| Project Plan | 项目组织 |
| Daily Review | 每日回顾反思 |

## 属性

### 添加属性

```markdown
- type:: book
  author:: [[Author Name]]
  rating:: 4
  status:: reading
```

### 属性类型

| 类型 | 示例 |
|------|------|
| 文本 | `title:: My Note` |
| 数字 | `rating:: 5` |
| 日期 | `date:: [[2024-01-15]]` |
| 页面 | `author:: [[Author]]` |
| 复选框 | `done:: true` |
| URL | `url:: https://example.com` |

### 查询属性

```markdown
{{query (property type book)}}
{{query (property status reading)}}
```

## 查询

### 基本查询

```markdown
{{query (page [[Tag Name]])}}
{{query (property type book)}}
```

### 高级查询

```clojure
#+BEGIN_QUERY
{:title "Books to read"
 :query [:find (pull ?b [*])
         :in $ ?type
         :where [?b :block/properties ?props]
                [(get ?props :type) ?type]
                [(= ?type "book")]]
 :inputs ["book"]}
#+END_QUERY
```

### 查询示例

| 查询 | 结果 |
|------|------|
| `{{query (page [[TODO]])}}` | 所有待办事项 |
| `{{query (property status done)}}` | 已完成项目 |
| `{{query (between -7d today)}}` | 最近 7 天 |

## 任务管理

### TODO 系统

```markdown
- TODO Buy groceries
  SCHEDULED: <2024-01-15>
- DOING Write report
- DONE Submit assignment
```

### 任务状态

| 状态 | 含义 |
|------|------|
| `TODO` | 未开始 |
| `DOING` | 进行中 |
| `DONE` | 已完成 |
| `LATER` | 以后再做 |
| `NOW` | 当前优先 |

### 调度

```markdown
- TODO Task name
  SCHEDULED: <2024-01-15>
  DEADLINE: <2024-01-20>
```

## 插件

### 热门插件

| 插件 | 功能 |
|------|------|
| TODO Master | 增强任务管理 |
| Agenda | 日历集成 |
| Markdown Table Editor | 表格编辑 |
| Zotero | 参考文献管理 |
| GitHub Sync | 版本控制 |

### 安装插件

1. 打开设置
2. 导航到插件
3. 浏览市场
4. 点击安装

## 导入和导出

### 支持的格式

| 格式 | 导入 | 导出 |
|------|------|------|
| Markdown | 是 | 是 |
| Org-mode | 是 | 是 |
| Roam JSON | 是 | 否 |
| Notion | 是 | 否 |
| HTML | 否 | 是 |

### 从 Roam 导入

```bash
# 从 Roam 导出为 JSON
# 在 Logseq 中使用导入功能
# 选择 Roam JSON 格式
```

## 同步

### Git 同步

```bash
# 在图谱文件夹初始化 git
cd ~/logseq/graphs/my-graph
git init
git add .
git commit -m "Initial commit"
```

### 同步选项

| 方式 | 描述 |
|------|------|
| Git | 版本控制 |
| Syncthing | 点对点同步 |
| iCloud | Apple 设备 |
| Google Drive | 云同步 |
| Logseq Sync | 官方同步服务 |

## 自定义

### 主题

| 主题 | 风格 |
|------|------|
| Light | 默认亮色主题 |
| Dark | 暗色模式 |
| Dracula | 紫色暗色主题 |
| Solarized | 柔和对比 |
| Custom | 用户自定义 CSS |

### 自定义 CSS

```css
/* Custom styling */
.ls-block {
  font-size: 16px;
}

.page-title {
  color: #4a90d9;
}
```

## 键盘快捷键

### 常用快捷键

| 操作 | Windows/Linux | macOS |
|------|--------------|-------|
| 新建页面 | Ctrl+Shift+N | Cmd+Shift+N |
| 搜索 | Ctrl+K | Cmd+K |
| 粗体 | Ctrl+B | Cmd+B |
| 斜体 | Ctrl+I | Cmd+I |
| 链接 | Ctrl+L | Cmd+L |

## 总结

| 概念 | 用途 |
|------|------|
| 页面 | 组织知识主题 |
| 块 | 内容的基本单元 |
| 链接 | 连接相关信息 |
| 图谱 | 可视化知识网络 |
| 查询 | 检索信息 |
| 模板 | 标准化笔记格式 |
