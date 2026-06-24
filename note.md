# Trilium：个人知识库指南

Trilium（现为 TriliumNext）综合教程，这是一个用于构建个人知识库的分层笔记应用。用强大的功能组织你的想法、研究和知识。

## 目录

- [什么是 Trilium](#什么是-trilium)
- [安装](#安装)
- [笔记类型](#笔记类型)
- [属性](#属性)
- [关系](#关系)
- [脚本](#脚本)
- [同步](#同步)
- [分享](#分享)
- [搜索](#搜索)
- [模板](#模板)
- [API](#api)
- [备份](#备份)
- [移动端访问](#移动端访问)

---

## 什么是 Trilium

### 概述

Trilium 是一个分层笔记应用，专注于构建大型个人知识库。它使用树形结构组织笔记，支持脚本、属性和关系等丰富功能。

### 核心特性

| 特性 | 描述 |
|---------|-------------|
| 分层笔记 | 无限嵌套深度 |
| 富文本编辑器 | 所见即所得编辑 |
| 代码笔记 | 代码语法高亮 |
| 属性 | 笔记的元数据和属性 |
| 关系 | 笔记间的链接 |
| 脚本 | JavaScript 自动化 |
| 全文搜索 | 快速搜索所有笔记 |
| 同步 | 多设备同步 |
| 分享 | 将笔记发布为网页 |
| 版本控制 | 笔记历史和修订 |
| 加密 | 密码保护笔记 |
| API | REST API 集成 |

### 与其他工具对比

| 特性 | Trilium | Obsidian | Notion | Joplin | Logseq |
|---------|---------|----------|--------|--------|--------|
| 自托管 | 是 | 否 | 否 | 是 | 否 |
| 开源 | 是 | 否 | 否 | 是 | 是 |
| 分层 | 是 | 有限 | 是 | 扁平 | 大纲 |
| 脚本 | 是 | 插件 | 有限 | 否 | 否 |
| Web 访问 | 是 | 否 | 是 | 否 | 否 |
| 离线优先 | 是 | 是 | 否 | 是 | 是 |
| 关系 | 是 | 链接 | 链接 | 链接 | 链接 |
| API | 是 | 否 | 是 | 是 | 否 |

---

## 安装

### 安装方式

| 方式 | 最适合 | 难度 |
|--------|----------|------------|
| Docker | 自托管、服务器 | 简单 |
| 桌面应用 | 个人使用 | 简单 |
| Snap | Ubuntu/Linux | 简单 |
| 手动 | 自定义设置 | 中等 |

### Docker 安装

```bash
# 创建数据目录
mkdir -p ~/trilium-data

# 运行 Trilium
docker run -d \
  --name trilium \
  --restart=always \
  -p 8080:8080 \
  -v ~/trilium-data:/home/node/trilium-data \
  triliumnext/notes:latest
```

### Docker Compose

```yaml
version: "3.8"

services:
  trilium:
    image: triliumnext/notes:latest
    container_name: trilium
    ports:
      - "8080:8080"
    volumes:
      - trilium-data:/home/node/trilium-data
    environment:
      - TRILIUM_DATA_DIR=/home/node/trilium-data
    restart: unless-stopped

volumes:
  trilium-data:
```

### 桌面应用

| 平台 | 下载来源 |
|----------|----------------|
| Windows | GitHub releases (.exe) |
| macOS | GitHub releases (.dmg) |
| Linux | GitHub releases (.AppImage) |
| Flatpak | `flatpak install com.github.TriliumNext.Notes` |
| Snap | `sudo snap install trilium` |

### 系统要求

| 要求 | 最低 | 推荐 |
|-------------|---------|-------------|
| RAM | 512 MB | 2 GB |
| 存储 | 100 MB + 数据 | 1 GB + 数据 |
| CPU | 1 核 | 2 核 |
| 浏览器 | 现代浏览器 | Chrome、Firefox、Edge |

---

## 笔记类型

### 可用笔记类型

| 类型 | 描述 | 用例 |
|------|-------------|----------|
| 文本 | 带格式的富文本 | 通用笔记、文档 |
| 代码 | 语法高亮代码 | 编程、脚本 |
| 画布 | 无限绘图画布 | 图表、草图 |
| Mermaid | 文本生成图表 | 流程图、时序图 |
| 关系图 | 可视化关系图 | 知识可视化 |
| 书籍 | 子笔记容器 | 组织章节 |
| 搜索 | 保存的搜索结果 | 动态集合 |
| 渲染笔记 | 渲染的 HTML | 自定义视图 |
| 文件 | 上传的文件附件 | 文档、图片 |
| 图片 | 图片笔记 | 截图、照片 |

### 创建笔记

| 操作 | 方法 |
|--------|--------|
| 创建子笔记 | 右键笔记 > 添加子笔记 |
| 创建同级笔记 | 右键笔记 > 添加同级笔记 |
| 在根目录创建 | 点击笔记树中的"+" |
| 快速创建 | Ctrl+O > 输入新名称 |

### 笔记属性

| 属性 | 描述 |
|----------|-------------|
| 标题 | 笔记名称 |
| 类型 | 笔记内容类型 |
| MIME | 内容 MIME 类型 |
| 创建时间 | 创建日期 |
| 修改时间 | 最后修改日期 |
| 笔记 ID | 唯一标识符 |
| 受保护 | 加密状态 |

### 富文本编辑器功能

| 功能 | 快捷键 | 描述 |
|---------|----------|-------------|
| 粗体 | Ctrl+B | 粗体文本 |
| 斜体 | Ctrl+I | 斜体文本 |
| 下划线 | Ctrl+U | 下划线文本 |
| 删除线 | Ctrl+Shift+S | 删除线 |
| 标题 | Ctrl+1-6 | 标题级别 |
| 无序列表 | Ctrl+Shift+8 | 项目符号 |
| 有序列表 | Ctrl+Shift+9 | 有序列表 |
| 复选框 | Ctrl+Shift+C | 任务复选框 |
| 行内代码 | Ctrl+` | 行内代码 |
| 代码块 | Ctrl+Shift+` | 代码块 |
| 链接 | Ctrl+L | 插入链接 |
| 表格 | - | 插入表格 |
| 图片 | - | 插入图片 |
| 数学公式 | - | LaTeX 数学公式 |

---

## 属性

### 什么是属性

属性是附加到笔记的元数据。它们提供属性、标签和关系，丰富你的笔记并启用高级功能。

### 属性类型

| 类型 | 前缀 | 示例 | 描述 |
|------|--------|---------|-------------|
| 标签 | `#` | `#favorite` | 简单标签或标志 |
| 带值标签 | `#` | `#priority=high` | 键值元数据 |
| 关系 | `~` | `~relatedNote` | 链接到另一笔记 |
| 带值关系 | `~` | `~author=NoteID` | 带值链接 |

### 内置属性

| 属性 | 类型 | 描述 |
|-----------|------|-------------|
| `#readOnly` | 标签 | 设为只读 |
| `#autoReadOnlyDisabled` | 标签 | 禁用自动只读 |
| `#hiddenLinks` | 标签 | 隐藏出站链接 |
| `#hidePromoted` | 标签 | 隐藏提升的属性 |
| `#cssClass` | 标签 | 自定义 CSS 类 |
| `#iconClass` | 标签 | 自定义图标 |
| `#color` | 标签 | 树中的笔记颜色 |
| `#run` | 标签 | 自动运行脚本 |
| `#sorted` | 标签 | 按字母排序子项 |
| `#top` | 标签 | 置顶 |
| `#excludeFromExport` | 标签 | 导出时跳过 |
| `#template` | 标签 | 标记为模板 |
| `#disableVersioning` | 标签 | 禁用笔记历史 |
| `#shareHiddenFromTree` | 标签 | 从共享树中隐藏 |
| `#shareAlias` | 标签 | 自定义分享 URL |

### 提升的属性

提升的属性显示在笔记的属性面板中，方便编辑。

```javascript
// 要提升属性，将其添加到笔记：
#priority(promoted, number)
#status(promoted, label=pending/in-progress/done)
#dueDate(promoted, date)
~assignedTo(promoted, relation)
```

### 属性继承

属性由子笔记继承：

| 行为 | 描述 |
|----------|-------------|
| 向下 | 子项继承父项属性 |
| 覆盖 | 子项可以覆盖继承的值 |
| 累积 | 可以存在多个值 |
| 深度优先 | 更近的父项优先 |

### 使用属性进行组织

| 系统 | 属性 | 描述 |
|--------|-----------|-------------|
| GTD | `#status=next/waiting/someday` | Getting Things Done |
| PARA | `#type=project/area/resource/archive` | PARA 方法 |
| Zettelkasten | `#type=fleeting/literature/permanent` | Zettelkasten 方法 |
| Cornell Notes | `#type=note/cue/summary` | Cornell 方法 |

---

## 关系

### 什么是关系

关系是笔记间的链接。与简单的超链接不同，关系是结构化的，可用于导航、脚本和可视化。

### 关系类型

| 类型 | 语法 | 描述 |
|------|--------|-------------|
| 出站 | `~targetNote` | 从本笔记出发 |
| 入站 | 显示在目标上 | 指向本笔记 |
| 双向 | 双向 | 相互关系 |

### 创建关系

| 方法 | 操作 |
|--------|--------|
| 自动完成 | 输入 `~` 并开始输入笔记名称 |
| 属性面板 | 在属性中添加关系 |
| 拖放 | 将笔记拖到关系图 |
| 脚本 | 使用 API 编程创建 |

### 内置关系

| 关系 | 描述 |
|----------|-------------|
| `~template` | 笔记使用此模板 |
| `~run` | 要运行的脚本 |
| `~iconClass` | 自定义图标类 |

### 关系图

关系图提供笔记关系的可视化图：

| 功能 | 描述 |
|---------|-------------|
| 可视化图 | 一览所有关系 |
| 拖动节点 | 重新排列布局 |
| 添加关系 | 在节点间画线 |
| 缩放和平移 | 导航大型图表 |
| 导出 | 保存为图片 |

---

## 脚本

### 脚本类型

| 类型 | 作用域 | 触发器 |
|------|-------|---------|
| 后端脚本 | 服务器端 | 手动、定时 |
| 前端脚本 | 客户端 | UI 事件 |
| 关系图脚本 | 可视化 | 手动 |
| 小部件 | 自定义 UI | 自动加载 |
| 自定义请求处理 | HTTP 端点 | HTTP 请求 |

### 后端脚本

```javascript
// 示例：列出具有特定标签的所有笔记
const notes = await api.searchForNotes('#status/todo');
for (const note of notes) {
    api.log(`Note: ${note.title}`);
}

// 示例：创建新笔记
const note = await api.createNote({
    parentNoteId: 'root',
    title: 'New Note',
    content: 'Hello, World!',
    type: 'text'
});

// 示例：更新笔记内容
const note = await api.getNote('noteId');
await note.setContent('Updated content');

// 示例：搜索笔记
const results = await api.searchForNotes({
    query: 'search term',
    ancestorNoteId: 'parentNoteId'
});
```

### 前端脚本

```javascript
// 示例：显示通知
api.showMessage('Hello from script!');

// 示例：获取当前笔记
const currentNote = api.getActiveTabNote();

// 示例：在新标签页打开笔记
api.openNoteInNewTab('noteId');

// 示例：监听事件
api.addEventListener('noteSwitched', ({noteId}) => {
    api.log(`Switched to note: ${noteId}`);
});
```

### 定时脚本

```javascript
// 设置定时脚本
// 使用 #run=backend 和 #schedule 属性

// 脚本笔记上的属性：
// #run=backend
// #schedule=daily 09:00

const notes = await api.searchForNotes('#reminder');
for (const note of notes) {
    // 处理提醒
    api.log(`Reminder: ${note.title}`);
}
```

### API 方法

| 方法 | 描述 |
|--------|-------------|
| `api.getNote(noteId)` | 按 ID 获取笔记 |
| `api.createNote(opts)` | 创建新笔记 |
| `api.updateNote(noteId, opts)` | 更新笔记 |
| `api.deleteNote(noteId)` | 删除笔记 |
| `api.searchForNotes(query)` | 搜索笔记 |
| `api.getNotePath(noteId)` | 获取笔记路径 |
| `api.log(message)` | 记录消息 |
| `api.showMessage(message)` | 显示 UI 消息 |
| `api.getActiveTabNote()` | 获取当前笔记 |
| `api.openNoteInNewTab(noteId)` | 打开笔记 |

---

## 同步

### 同步选项

| 方式 | 描述 | 最适合 |
|--------|-------------|----------|
| 内置同步 | Trilium 自己的同步协议 | 多设备 |
| 自托管同步 | 运行同步服务器 | 完全控制 |
| 文件同步 | 使用 Syncthing/rsync | 简单设置 |
| Web 访问 | 通过浏览器访问 | 任何设备 |

### 设置同步

#### 同步服务器设置

```bash
# 运行同步服务器
docker run -d \
  --name trilium-sync \
  --restart=always \
  -p 8081:8080 \
  -v trilium-sync-data:/home/node/trilium-data \
  triliumnext/notes:latest \
  --no-cert-check
```

#### 客户端配置

| 步骤 | 操作 |
|------|--------|
| 1 | 打开 Trilium 桌面应用 |
| 2 | 转到选项 > 同步 |
| 3 | 输入同步服务器 URL |
| 4 | 输入同步密码 |
| 5 | 等待初始同步 |

### 同步冲突解决

| 场景 | 解决方案 |
|----------|------------|
| 同一笔记被编辑 | 最后写入获胜 |
| 一侧删除笔记 | 删除传播 |
| 结构更改 | 结构合并 |
| 附件更改 | 最新版本获胜 |

### 基于文件的同步

```bash
# 使用 Syncthing
# 在所有设备上安装 Syncthing
# 将 Trilium 数据文件夹添加到 Syncthing
# 在所有设备上设为"发送和接收"

# 使用 rsync
rsync -avz ~/trilium-data/ user@remote:~/trilium-data/
```

---

## 分享

### 分享选项

| 类型 | 描述 | 访问 |
|------|-------------|--------|
| 单个笔记 | 分享一个笔记 | 直接 URL |
| 子树 | 分享笔记和子项 | 树视图 |
| 自定义布局 | 自定义 HTML | 嵌入 |

### 发布笔记

| 步骤 | 操作 |
|------|--------|
| 1 | 右键笔记 > 分享 |
| 2 | 选择分享类型 |
| 3 | 配置选项 |
| 4 | 获取分享 URL |

### 分享配置

| 设置 | 描述 |
|---------|-------------|
| 包含子项 | 分享子树 |
| 自定义 CSS | 设置分享页面样式 |
| 自定义头部 | 添加头部内容 |
| 自定义底部 | 添加底部内容 |
| 密码保护 | 需要密码 |
| 过期日期 | 自动过期分享 |

### 自定义分享主题

```css
/* 分享笔记的自定义 CSS */
body {
    font-family: 'Inter', sans-serif;
    max-width: 800px;
    margin: 0 auto;
    padding: 20px;
}

.note-content {
    line-height: 1.6;
}

h1 {
    color: #2563eb;
}
```

---

## 搜索

### 搜索方式

| 方式 | 描述 | 示例 |
|--------|-------------|---------|
| 全文 | 搜索笔记内容 | `search term` |
| 仅标题 | 搜索笔记标题 | `note.title=search` |
| 属性 | 按属性搜索 | `#tag` 或 `#key=value` |
| 关系 | 按关系搜索 | `~relation` |
| 路径 | 按路径搜索 | `path=/root/folder` |
| 正则 | 正则表达式 | `regex=/pattern/` |
| 快速搜索 | 快速查找 | Ctrl+O |

### 搜索语法

| 语法 | 描述 | 示例 |
|--------|-------------|---------|
| `text` | 全文搜索 | `machine learning` |
| `#label` | 有标签 | `#important` |
| `#key=value` | 带值标签 | `#status=active` |
| `~relation` | 有关系 | `~author` |
| `note.title=X` | 标题匹配 | `note.title=API` |
| `note.type=X` | 笔记类型 | `note.type=code` |
| `note.dateCreated>X` | 创建于之后 | `note.dateCreated>2024-01-01` |
| `note.dateModified>X` | 修改于之后 | `note.dateModified>LAST_WEEK` |
| `note.content=X` | 内容匹配 | `note.content=TODO` |
| `AND` | 逻辑与 | `#tag1 AND #tag2` |
| `OR` | 逻辑或 | `#tag1 OR #tag2` |
| `NOT` | 逻辑非 | `#tag NOT #exclude` |
| `*` | 通配符 | `program*` |

### 搜索快捷键

| 快捷键 | 操作 |
|----------|--------|
| Ctrl+O | 快速搜索（笔记切换器） |
| Ctrl+S | 在当前笔记中搜索 |
| Ctrl+Shift+F | 全局搜索 |

### 保存的搜索

```javascript
// 创建保存的搜索笔记
// 类型：search
// 内容：#status/todo AND #priority=high

// 这将创建匹配笔记的动态列表
// 随笔记变化自动更新
```

---

## 模板

### 什么是模板

模板是为新笔记定义默认属性、内容和行为的笔记。

### 创建模板

| 步骤 | 操作 |
|------|--------|
| 1 | 创建具有所需内容的笔记 |
| 2 | 添加 `#template` 标签 |
| 3 | 设置所需属性 |
| 4 | 在目标笔记上使用 `~template` 关系 |

### 模板结构

```markdown
## 模板：每日日志

#template
#iconClass="bx bx-calendar"

---

### 日期：${date}

### 任务
- [ ] 

### 笔记


### 反思


### 链接
- 上一篇：~previousDay
```

### 模板属性

| 属性 | 描述 |
|-----------|-------------|
| `#template` | 标记笔记为模板 |
| `#autoCreate` | 自动创建子笔记 |
| `#inherit` | 继承到子项 |
| `#clone` | 克隆而非引用 |

### 使用模板

| 方式 | 描述 |
|--------|-------------|
| 手动 | 将模板应用到笔记 |
| 自动 | 带 `#autoCreate` 的模板 |
| 继承 | 子项继承模板 |
| 克隆 | 复制模板内容 |

---

## API

### REST API

Trilium 提供 REST API 用于外部集成。

### API 端点

| 方法 | 端点 | 描述 |
|--------|----------|-------------|
| GET | /api/notes/{noteId} | 获取笔记 |
| POST | /api/create-note | 创建笔记 |
| PUT | /api/notes/{noteId} | 更新笔记 |
| DELETE | /api/notes/{noteId} | 删除笔记 |
| GET | /api/search | 搜索笔记 |
| GET | /api/notes/{noteId}/content | 获取笔记内容 |
| PUT | /api/notes/{noteId}/content | 设置笔记内容 |
| GET | /api/notes/{noteId}/attributes | 获取属性 |
| POST | /api/notes/{noteId}/attributes | 创建属性 |
| GET | /api/notes/{noteId}/relations | 获取关系 |
| POST | /api/notes/{noteId}/relations | 创建关系 |

### API 认证

```bash
# 在 Options > API 生成 API token
# 使用 ETAPI token 进行认证

curl -H "Authorization: YOUR_ETAPI_TOKEN" \
  http://localhost:8080/api/notes/root
```

### ETAPI（外部 API）

```python
import requests

BASE_URL = "http://localhost:8080"
TOKEN = "your_etapi_token"

headers = {
    "Authorization": TOKEN
}

# 获取笔记
response = requests.get(
    f"{BASE_URL}/api/notes/noteId",
    headers=headers
)

# 创建笔记
data = {
    "parentNoteId": "root",
    "title": "New Note",
    "type": "text",
    "content": "Hello from API!"
}
response = requests.post(
    f"{BASE_URL}/api/create-note",
    headers=headers,
    json=data
)
```

### WebSocket API

| 事件 | 描述 |
|-------|-------------|
| `noteCreated` | 创建新笔记 |
| `noteUpdated` | 笔记已修改 |
| `noteDeleted` | 笔记已删除 |
| `attributeChanged` | 属性已修改 |
| `syncStarted` | 同步已开始 |
| `syncCompleted` | 同步已完成 |

---

## 备份

### 备份方式

| 方式 | 描述 | 自动化 |
|--------|-------------|------------|
| 内置导出 | 导出为 ZIP | 手动 |
| 数据库复制 | 复制 SQLite 文件 | 脚本化 |
| Docker 卷 | 备份卷 | Docker 工具 |
| rsync | 增量复制 | Cron 任务 |

### 内置导出

| 导出类型 | 描述 | 格式 |
|-------------|-------------|--------|
| HTML | 导出为网页 | .html 文件 |
| Markdown | 导出为 markdown | .md 文件 |
| OPML | 导出大纲 | .opml |
| ZIP | 完整导出 | .zip 归档 |

### 自动备份脚本

```bash
#!/bin/bash
# backup-trilium.sh

BACKUP_DIR="/backups/trilium"
DATE=$(date +%Y%m%d_%H%M%S)
TRILIUM_DATA="/home/node/trilium-data"

# 创建备份目录
mkdir -p $BACKUP_DIR

# 复制数据库
cp $TRILIUM_DATA/document.db $BACKUP_DIR/document_$DATE.db

# 复制日志
cp $TRILIUM_DATA/log.db $BACKUP_DIR/log_$DATE.db

# 仅保留最近 30 个备份
ls -t $BACKUP_DIR/document_*.db | tail -n +31 | xargs -r rm

echo "备份完成：$DATE"
```

### 备份频率

| 频率 | 保留 | 存储 |
|-----------|-----------|---------|
| 每天 | 7 天 | 本地 |
| 每周 | 4 周 | 本地 + 远程 |
| 每月 | 12 个月 | 远程 |
| 重大更改前 | - | 本地 |

---

## 移动端访问

### 移动端访问选项

| 方式 | 描述 | 最适合 |
|--------|-------------|----------|
| Web 浏览器 | 通过浏览器访问 | 任何移动设备 |
| TriliumNext Mobile | 原生应用 | Android |
| PWA | 渐进式 Web 应用 | iOS、Android |

### Web 访问设置

| 步骤 | 操作 |
|------|--------|
| 1 | 在服务器上安装 Trilium |
| 2 | 配置反向代理（Nginx/Caddy） |
| 3 | 设置 SSL 证书 |
| 4 | 通过移动浏览器访问 |
| 5 | 添加到主屏幕 |

### Nginx 反向代理

```nginx
server {
    listen 443 ssl;
    server_name notes.example.com;

    ssl_certificate /etc/letsencrypt/live/notes.example.com/fullchain.pem;
    ssl_certificate_key /etc/letsencrypt/live/notes.example.com/privkey.pem;

    location / {
        proxy_pass http://localhost:8080;
        proxy_set_header Host $host;
        proxy_set_header X-Real-IP $remote_addr;
        proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
        proxy_set_header X-Forwarded-Proto $scheme;
        
        # WebSocket 支持
        proxy_http_version 1.1;
        proxy_set_header Upgrade $http_upgrade;
        proxy_set_header Connection "upgrade";
    }
}
```

### 移动端友好技巧

| 技巧 | 描述 |
|-----|-------------|
| 使用 PWA | 添加到主屏幕获得应用体验 |
| 启用离线 | 配置离线访问 |
| 使用书签 | 收藏常用笔记 |
| 简化 UI | 使用移动端优化主题 |
| 快速捕获 | 设置快速笔记创建 |

---

## 最佳实践

### 组织结构

| 结构 | 描述 | 最适合 |
|-----------|-------------|----------|
| 按主题 | 主题作为分支 | 研究 |
| 按项目 | 每个项目一个分支 | 工作 |
| 按时间 | 每日/每周/每月笔记 | 日记 |
| 按类型 | 笔记、任务等分开 | 混合使用 |

### 命名约定

| 约定 | 示例 | 用例 |
|-----------|---------|----------|
| 日期前缀 | 2024-01-15 会议笔记 | 按时间排序 |
| 类型前缀 | [PROJECT] 网站改版 | 分类 |
| 使用一致格式 | API - 认证指南 | 参考 |
| CamelCase | myNoteTitle | 通用 |

### 属性系统

| 用途 | 属性 | 描述 |
|---------|-----------|-------------|
| 状态 | `#status=todo/doing/done` | 任务跟踪 |
| 优先级 | `#priority=low/medium/high` | 优先级排序 |
| 类型 | `#type=note/reference/task` | 分类 |
| 日期 | `#dueDate=2024-01-15` | 截止日期 |
| 人员 | `~author`、`~assignedTo` | 人员 |

---

## 总结

Trilium 是构建个人知识库的强大工具。其分层结构结合属性和关系，提供了灵活的系统来组织任何类型的信息。

关键要点：
- 使用 Docker 或桌面应用轻松安装
- 使用笔记类型处理不同内容
- 利用属性进行元数据和组织
- 在笔记间创建关系形成知识图谱
- 使用脚本实现自动化
- 设置同步实现多设备访问
- 定期备份

从简单开始，随着知识库的增长逐步采用更高级的功能。
