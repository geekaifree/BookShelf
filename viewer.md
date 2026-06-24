# 使用 qView 查看图片

## 简介

qView 是一个极简的开源图片查看器，专为速度和简洁而设计。它专注于提供纯净的查看体验，没有多余的功能。本教程涵盖安装、导航、配置和键盘快捷键。

## 设计理念

| 原则 | 实现 |
|------|------|
| Minimalism | 默认无工具栏或面板 |
| Speed | 快速图片加载和切换 |
| Focus | 内容优先的查看体验 |
| Native | 平台特定的外观和感觉 |

## 安装

### 平台特定

| 平台 | 方式 | 命令/来源 |
|------|------|-----------|
| macOS | Homebrew | `brew install --cask qview` |
| macOS | DMG | 从 GitHub releases 下载 |
| Windows | Installer | 从 GitHub releases 下载 |
| Windows | Scoop | `scoop install qview` |
| Linux | Flatpak | `flatpak install com.github.jurple-l.qview` |
| Linux | AppImage | 从 GitHub releases 下载 |

### 验证安装

从应用菜单打开 qView 或从终端运行：

```bash
qview /path/to/image.jpg
```

## 支持格式

### 图片格式

| 格式 | 扩展名 | 支持级别 |
|------|--------|----------|
| JPEG | .jpg, .jpeg | 完全 |
| PNG | .png | 完全 |
| GIF | .gif | 完全，动画 |
| BMP | .bmp | 完全 |
| WebP | .webp | 完全 |
| TIFF | .tiff, .tif | 完全 |
| SVG | .svg | 完全 |
| ICO | .ico | 完全 |
| AVIF | .avif | 完全 |
| HEIF | .heif, .heic | 完全 |

### 格式能力

| 能力 | 支持的格式 |
|------|-----------|
| Animation | GIF, WebP, APNG |
| Transparency | PNG, GIF, WebP, SVG |
| Metadata | JPEG, PNG, TIFF |
| High bit depth | PNG, TIFF, WebP |

## 界面

### 窗口元素

| 元素 | 可见性 | 功能 |
|------|--------|------|
| Title bar | 始终 | 显示文件名 |
| Menu bar | 切换 | 文件、编辑、视图菜单 |
| Image area | 始终 | 主查看区域 |
| Info overlay | 切换 | 文件信息显示 |
| Window controls | 始终 | 最小化、最大化、关闭 |

### 显示模式

| 模式 | 描述 | 快捷键 |
|------|------|--------|
| Window | 可调大小窗口 | 默认 |
| Fullscreen | 全屏视图 | F11 |
| Frameless | 无窗口边框 | F10 |
| Always on Top | 保持可见 | Ctrl+Shift+T |

## 导航

### 打开图片

| 方法 | 描述 |
|------|------|
| File > Open | 浏览并选择文件 |
| Drag and drop | 拖放到窗口 |
| Command line | `qview image.jpg` |
| File association | 双击图片文件 |
| Recent files | File > Open Recent |

### 浏览图片

| 操作 | 方法 | 快捷键 |
|------|------|--------|
| 下一张 | 右箭头或点击 | Right |
| 上一张 | 左箭头或点击 | Left |
| 第一张 | Home | Home |
| 最后一张 | End | End |
| 跳转到 | 输入文件名 | Ctrl+G |

### 文件夹导航

打开图片时，qView 会加载同一文件夹中的所有图片：

| 行为 | 描述 |
|------|------|
| Sequential | 浏览文件夹内容 |
| Sorted | 按字母或日期排序 |
| Filtered | 仅显示支持的格式 |

## 缩放和平移

### 缩放控制

| 操作 | 方法 | 快捷键 |
|------|------|--------|
| 放大 | 向上滚动或 Ctrl++ | + |
| 缩小 | 向下滚动或 Ctrl+- | - |
| 适合窗口 | 双击 | F |
| 适合宽度 | Ctrl+W | W |
| 适合高度 | Ctrl+H | H |
| 原始大小 (100%) | Ctrl+0 | 0 |
| 自定义缩放 | Ctrl+滚动 | - |

### 平移控制

| 操作 | 方法 |
|------|------|
| 平移图片 | 点击并拖动 |
| 滚动平移 | 滚轮（缩放时） |
| 重置位置 | 双击 |

## 图片操作

### 旋转和翻转

| 操作 | 快捷键 | 效果 |
|------|--------|------|
| 右旋转 | R | 顺时针 90 度 |
| 左旋转 | Shift+R | 逆时针 90 度 |
| 水平翻转 | H | 左右镜像 |
| 垂直翻转 | V | 上下镜像 |
| 重置 | Ctrl+R | 返回原始 |

### 变换行为

| 变换 | 持久性 | 文件修改 |
|------|--------|----------|
| Rotation | 仅会话 | 否 |
| Flip | 仅会话 | 否 |
| Zoom | 仅会话 | 否 |

## 信息显示

### 文件信息

| 信息 | 描述 | 切换 |
|------|------|------|
| Filename | 当前文件名 | 始终可见 |
| Dimensions | 宽 x 高 | I 键 |
| File size | 字节、KB、MB | I 键 |
| Format | 图片类型 | I 键 |
| Color depth | 每通道位数 | I 键 |

### 信息覆盖

按 I 切换信息覆盖：

```
image.jpg
4000 x 3000
12.5 MB
JPEG
```

## 幻灯片

### 幻灯片控制

| 操作 | 快捷键 | 描述 |
|------|--------|------|
| 开始幻灯片 | S | 开始自动推进 |
| 停止幻灯片 | S 或 Esc | 结束幻灯片 |
| 下一张 | Right | 手动前进 |
| 上一张 | Left | 返回 |

### 幻灯片设置

| 设置 | 选项 | 默认值 |
|------|------|--------|
| Interval | 1-60 秒 | 5 秒 |
| Loop | 是/否 | 是 |
| Random order | 是/否 | 否 |
| Transition | 无、淡入淡出 | 无 |

## 配置

### 设置分类

| 分类 | 选项 |
|------|------|
| General | 启动行为、文件关联 |
| Interface | 窗口、工具栏、覆盖 |
| Controls | 鼠标、键盘、手势 |
| Image | 加载、缓存、质量 |
| Slideshow | 计时、过渡 |

### 关键设置

| 设置 | 描述 | 建议 |
|------|------|------|
| Startup image | 启动时的图片 | 上次查看或无 |
| Window remember | 保存位置 | 启用 |
| Filtering | 图片缩放 | 照片用双线性 |
| Bilinear | 平滑缩放 | 大图片启用 |
| Preloading | 加载相邻图片 | 速度启用 |

## 键盘快捷键

### 基本快捷键

| 操作 | 快捷键 | 分类 |
|------|--------|------|
| 打开文件 | Ctrl+O | 文件 |
| 退出 | Ctrl+Q | 文件 |
| 全屏 | F11 | 视图 |
| 信息切换 | I | 视图 |
| 放大 | + | 缩放 |
| 缩小 | - | 缩放 |
| 适合窗口 | F | 缩放 |
| 原始大小 | 0 | 缩放 |
| 下一张图片 | Right | 导航 |
| 上一张图片 | Left | 导航 |
| 右旋转 | R | 变换 |
| 左旋转 | Shift+R | 变换 |
| 水平翻转 | H | 变换 |
| 垂直翻转 | V | 变换 |
| 幻灯片 | S | 功能 |
| 删除 | Delete | 文件 |

### 快捷键参考

| 分类 | 快捷键 |
|------|--------|
| File | Ctrl+O, Ctrl+S, Delete, Ctrl+Q |
| View | F11, F10, I, B |
| Zoom | +, -, 0, F, W, H |
| Navigate | Right, Left, Home, End |
| Transform | R, Shift+R, H, V, Ctrl+R |
| Slideshow | S, Esc |

## 文件操作

### 快速操作

| 操作 | 快捷键 | 描述 |
|------|--------|------|
| Open location | Ctrl+L | 打开包含文件夹 |
| Copy path | Ctrl+Shift+C | 复制文件路径 |
| Copy image | Ctrl+C | 复制到剪贴板 |
| Rename | F2 | 重命名当前文件 |
| Delete | Delete | 移到回收站 |
| Properties | Ctrl+I | 文件属性 |

## 性能

### 优化提示

| 提示 | 描述 | 影响 |
|------|------|------|
| SSD storage | 将图片存储在 SSD | 更快加载 |
| Hardware acceleration | GPU 渲染 | 更流畅缩放/平移 |
| Memory cache | 保留在 RAM | 更快导航 |
| Image preloading | 加载相邻文件 | 即时切换 |

### 资源使用

| 指标 | 典型使用 |
|------|----------|
| Memory | 50-200 MB |
| CPU | 空闲 < 1%，缩放时 5-10% |
| Disk | 加载后最小 |

## 故障排除

| 问题 | 可能原因 | 解决方案 |
|------|----------|----------|
| 图片未加载 | 不支持的格式 | 检查格式支持 |
| 加载慢 | 大文件 | 启用硬件加速 |
| 无动画 | 静态查看器 | 验证 GIF/APNG 支持 |
| 图片模糊 | 缩放滤镜 | 调整缩放设置 |
| 文件关联 | 系统设置 | 设置 qView 为默认 |

## 与其他查看器对比

| 功能 | qView | IrfanView | Preview | feh |
|------|-------|-----------|---------|-----|
| Speed | 快 | 快 | 快 | 最快 |
| Interface | 极简 | 完整 | 简洁 | CLI |
| Editing | 无 | 基本 | 基本 | 无 |
| Format support | 良好 | 优秀 | 良好 | 良好 |
| Platform | 全部 | Windows | macOS | Linux |
| Price | 免费 | 免费 | 免费 | 免费 |

## 总结

qView 提供了一个专注、快速的图片查看体验，没有完整图片编辑器的复杂性。其极简界面和键盘驱动的导航使其非常适合快速图片浏览和审查。

关键实践：

- 使用键盘快捷键高效导航
- 启用硬件加速以获得流畅性能
- 设置为默认图片查看器以便快速访问
- 使用全屏模式进行无干扰查看
- 利用幻灯片功能进行演示
