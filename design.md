# 开发者设计资源：精选指南

## 简介

design-resources-for-developers 仓库是一个为开发者精选的免费设计资源集合。它包括 UI 套件、模板、图标、字体、颜色和工具，帮助开发者在没有专业设计师的情况下创建专业外观的应用程序。本教程组织并解释了关键资源类别。

## 为什么开发者需要设计资源

| 挑战 | 解决方案 |
|------|----------|
| 没有设计团队 | 使用预制 UI 套件和模板 |
| 样式不一致 | 采用设计系统和调色板 |
| 时间紧迫 | 从模板开始并自定义 |
| 技能差距 | 使用内置最佳实践的工具 |

## 资源类别

| 类别 | 数量 | 描述 |
|------|------|------|
| UI 套件 | 100+ | 用于界面的组件库 |
| 模板 | 200+ | 现成的页面布局 |
| 图标 | 50+ | 图标库和集合 |
| 字体 | 30+ | 免费的 Web 字体 |
| 颜色 | 20+ | 调色板和生成器 |
| 插图 | 30+ | SVG 和 PNG 图形 |
| 图片素材 | 20+ | 免费使用的摄影 |
| 工具 | 40+ | 设计和原型工具 |

## UI 组件库

### CSS 框架

| 框架 | 风格 | 最适用于 |
|------|------|----------|
| Bootstrap | 基于组件 | 快速原型 |
| Tailwind CSS | 实用工具优先 | 自定义设计 |
| Bulma | 基于 Flexbox | 简洁界面 |
| Material UI | Google Material | Android 风格应用 |
| Chakra UI | 模块化 React | React 应用 |
| Ant Design | 企业级 | 管理仪表板 |

### Tailwind CSS 示例

```html
<!-- Tailwind 卡片组件 -->
<div class="max-w-sm rounded overflow-hidden shadow-lg">
  <img class="w-full" src="/img/card-top.jpg" alt="Card image">
  <div class="px-6 py-4">
    <div class="font-bold text-xl mb-2">Card Title</div>
    <p class="text-gray-700 text-base">
      Card description goes here.
    </p>
  </div>
  <div class="px-6 pt-4 pb-2">
    <span class="inline-block bg-gray-200 rounded-full px-3 py-1 text-sm font-semibold text-gray-700 mr-2">#tag</span>
  </div>
</div>
```

### Bootstrap 示例

```html
<!-- Bootstrap 卡片组件 -->
<div class="card" style="width: 18rem;">
  <img src="/img/card-top.jpg" class="card-img-top" alt="Card image">
  <div class="card-body">
    <h5 class="card-title">Card Title</h5>
    <p class="card-text">Card description goes here.</p>
    <a href="#" class="btn btn-primary">Go somewhere</a>
  </div>
</div>
```

## 模板来源

### 免费模板网站

| 来源 | 类型 | 许可证 |
|------|------|--------|
| HTML5 UP | HTML 模板 | Creative Commons |
| Start Bootstrap | Bootstrap 主题 | MIT |
| Tailwind UI | Tailwind 组件 | 免费 + 付费 |
| Creative Tim | UI 套件 | 免费 + 付费 |
| ThemeWagon | 模板 | MIT |
| Cruip | 落地页 | 免费 + 付费 |

### 模板类型

| 类型 | 使用场景 | 示例 |
|------|----------|------|
| 落地页 | 产品营销 | SaaS、应用发布 |
| 管理仪表板 | 后端管理 | 分析、CRUD |
| 作品集 | 个人展示 | 开发者、设计师 |
| 博客 | 内容发布 | 技术博客、文档 |
| 电商 | 在线商店 | 产品列表 |
| 文档 | 技术文档 | API 文档、指南 |

## 图标库

### 常用图标集

| 库 | 数量 | 风格 | 格式 |
|----|------|------|------|
| Font Awesome | 2000+ | Solid、regular、brands | SVG、webfont |
| Feather Icons | 280+ | 极简线条 | SVG |
| Heroicons | 300+ | 轮廓、实心 | SVG |
| Material Icons | 2000+ | 填充、轮廓 | SVG、webfont |
| Ionicons | 1300+ | 轮廓、填充 | SVG |
| Tabler Icons | 4000+ | 轮廓 | SVG |
| Lucide | 1000+ | Feather 分支 | SVG |

### 使用图标

```html
<!-- Font Awesome -->
<i class="fas fa-home"></i>
<i class="fab fa-github"></i>

<!-- Feather Icons (JavaScript) -->
<feather-icon name="home"></feather-icon>

<!-- Heroicons (SVG inline) -->
<svg xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24" stroke-width="1.5" stroke="currentColor" class="w-6 h-6">
  <path stroke-linecap="round" stroke-linejoin="round" d="M2.25 12l8.954-8.955a1.126 1.126 0 011.591 0L21.75 12M4.5 9.75v10.125c0 .621.504 1.125 1.125 1.125H9.75v-4.875c0-.621.504-1.125 1.125-1.125h2.25c.621 0 1.125.504 1.125 1.125V21h4.125c.621 0 1.125-.504 1.125-1.125V9.75M8.25 21h8.25" />
</svg>
```

## 调色板

### 调色板工具

| 工具 | 用途 | URL |
|------|------|-----|
| Coolors | 生成调色板 | coolors.co |
| Color Hunt | 浏览调色板 | colorhunt.co |
| Adobe Color | 创建调色板 | color.adobe.com |
| Paletton | 颜色关系 | paletton.com |
| Tailwind Colors | Tailwind 调色板 | tailwindcss.com/docs/colors |

### 常用配色方案

| 方案 | 颜色 | 使用场景 |
|------|------|----------|
| 单色 | 单一色调变化 | 简洁、极简 |
| 互补色 | 对比色 | 高对比度 |
| 类似色 | 相邻色 | 和谐 |
| 三色 | 三个等距色 | 鲜艳 |
| 分裂互补 | 一个基色 + 互补色两侧 | 平衡 |

### CSS 自定义属性

```css
:root {
  --color-primary: #3b82f6;
  --color-primary-dark: #2563eb;
  --color-secondary: #10b981;
  --color-accent: #f59e0b;
  --color-text: #1f2937;
  --color-text-light: #6b7280;
  --color-bg: #ffffff;
  --color-bg-alt: #f9fafb;
  --color-border: #e5e7eb;
  --color-error: #ef4444;
  --color-success: #22c55e;
}
```

## 字体排版

### 免费字体来源

| 来源 | 字体数 | 质量 |
|------|--------|------|
| Google Fonts | 1500+ | 高 |
| Font Squirrel | 1000+ | 精选 |
| DaFont | 5000+ | 参差不齐 |
| Fontsquirrel | 1000+ | 商业免费 |

### 字体搭配

| 标题字体 | 正文字体 | 风格 |
|----------|----------|------|
| Inter | Inter | 现代、简洁 |
| Playfair Display | Source Sans Pro | 优雅、编辑风格 |
| Montserrat | Open Sans | 专业、友好 |
| Poppins | Lato | 几何、易读 |
| Roboto | Roboto | 中性、通用 |

### 字体比例

```css
/* 模块化比例（1.25 比率） */
.text-xs { font-size: 0.75rem; }     /* 12px */
.text-sm { font-size: 0.875rem; }    /* 14px */
.text-base { font-size: 1rem; }      /* 16px */
.text-lg { font-size: 1.125rem; }    /* 18px */
.text-xl { font-size: 1.25rem; }     /* 20px */
.text-2xl { font-size: 1.5rem; }     /* 24px */
.text-3xl { font-size: 1.875rem; }   /* 30px */
.text-4xl { font-size: 2.25rem; }    /* 36px */
.text-5xl { font-size: 3rem; }       /* 48px */
```

## 插图

### 免费插图来源

| 来源 | 风格 | 格式 |
|------|------|------|
| unDraw | 极简、可自定义颜色 | SVG |
| Humaaans | 模块化人物 | SVG、Figma |
| Blush | 插画场景 | SVG、Figma |
| Open Peeps | 人物插图 | SVG、PNG |
| Storyset | 动画插图 | SVG、GIF |
| DrawKit | 手绘风格 | SVG、PNG |

### 使用 unDraw

```html
<!-- 带自定义颜色的内联 SVG -->
<img src="https://undraw.co/api/illustrations/your-id/svg?color=3b82f6"
     alt="插图描述"
     class="w-96 h-auto">
```

## 图片素材

### 免费图片来源

| 来源 | 许可证 | 质量 |
|------|--------|------|
| Unsplash | 免费使用 | 高 |
| Pexels | 免费使用 | 高 |
| Pixabay | 免费使用 | 参差不齐 |
| Burst (Shopify) | 免费使用 | 电商导向 |
| StockSnap | Creative Commons | 高 |

## 设计工具

### 免费设计工具

| 工具 | 用途 | 平台 |
|------|------|------|
| Figma | UI 设计和原型 | Web、桌面 |
| Penpot | 开源设计工具 | Web、桌面 |
| Inkscape | 矢量图形 | 桌面 |
| GIMP | 图片编辑 | 桌面 |
| Canva | 快速设计和图形 | Web |
| Excalidraw | 手绘图表 | Web |

### 原型工具

| 工具 | 保真度 | 最适用于 |
|------|--------|----------|
| Figma | 高 | 交互式原型 |
| Framer | 高 | 动画原型 |
| Balsamiq | 低 | 线框图 |
| Whimsical | 中 | 流程和线框图 |

## 响应式设计

### 断点参考

| 断点 | 宽度 | 设备 |
|------|------|------|
| sm | 640px | 小手机（横屏） |
| md | 768px | 平板 |
| lg | 1024px | 小笔记本 |
| xl | 1280px | 桌面 |
| 2xl | 1536px | 大屏幕 |

### CSS Grid 示例

```css
.grid-container {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(300px, 1fr));
  gap: 2rem;
  padding: 2rem;
}

.card {
  background: white;
  border-radius: 8px;
  box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
  padding: 1.5rem;
}
```

## 无障碍

### 基本实践

| 实践 | 描述 |
|------|------|
| 颜色对比 | 文本最低 4.5:1 比率 |
| 替代文本 | 描述所有图片 |
| 键盘导航 | 所有交互元素可聚焦 |
| ARIA 标签 | 为图标按钮添加标签 |
| 焦点可见 | 显示焦点指示器 |
| 语义化 HTML | 使用正确的标题层次 |

### 对比度检查

```javascript
// 检查对比度比率
function getContrastRatio(hex1, hex2) {
  const l1 = getLuminance(hex1);
  const l2 = getLuminance(hex2);
  const lighter = Math.max(l1, l2);
  const darker = Math.min(l1, l2);
  return (lighter + 0.05) / (darker + 0.05);
}
```

## 总结

design-resources-for-developers 集合提供了在没有设计背景的情况下构建专业界面所需的一切。使用 UI 组件库构建结构，使用图标集进行视觉传达，使用颜色工具保持调色板一致，使用字体排版指南确保文本可读。结合这些资源创建精美的、无障碍的应用程序。
