# 开发者设计资源

精选设计资源集合，涵盖图片素材、配色方案、字体、图标、插画、图案、UI 套件、CSS 框架、动画和响应式设计工具。

---

## 图片素材

| 平台 | 许可证 | 库大小 | 分辨率 | API | 费用 |
|----------|---------|--------------|------------|-----|------|
| Unsplash | Unsplash License | 300 万+ | 最高 5K | 是 | 免费 |
| Pexels | Pexels License | 300 万+ | 最高 4K | 是 | 免费 |
| Pixabay | Pixabay License | 250 万+ | 最高 4K | 是 | 免费 |
| StockSnap | CC0 | 10 万+ | 高分辨率 | 否 | 免费 |
| Burst | Shopify License | 1000+ | 高分辨率 | 否 | 免费 |

**Unsplash** - 高分辨率图片，无需署名，提供嵌入 API。
**Pexels** - 免费图片和视频，精选合集，可编程访问。
**Pixabay** - 图片、插画、矢量图和视频，无需注册。

---

## 配色方案

| 工具 | 类型 | 导出格式 | 协作 | 无障碍检查 | 费用 |
|------|------|----------------|---------------|---------------------|------|
| Coolors | 生成器 | CSS、SCSS、SVG、PDF | 是 | 是 | 免费/专业版 |
| Adobe Color | 色轮 + 提取器 | ASE、CSS、SCSS | 是 | 是 | 免费 |
| Color Hunt | 精选配色 | HEX 代码 | 否 | 否 | 免费 |
| Paletton | 色轮生成器 | CSS、SCSS、XML | 否 | 否 | 免费 |
| Khroma | AI 生成器 | CSS、SCSS、SVG | 否 | 否 | 免费 |

**Coolors** - 按空格键生成配色，锁定颜色，色盲模拟。
**Adobe Color** - 色轮、从图片提取、和谐规则（互补、类似、三色）。
**Color Hunt** - 每日更新配色，简洁界面，一键复制。

**CSS 示例：**
```css
:root {
  --primary: #264653;
  --secondary: #2a9d8f;
  --accent: #e9c46a;
}
```

---

## 字体

| 平台 | 字体数量 | 免费字体 | Web 字体 | 桌面使用 | 费用 |
|----------|------------|------------|-----------|-------------|------|
| Google Fonts | 1500+ | 全部 | 是 | 是 | 免费 |
| Font Squirrel | 1000+ | 大部分 | 部分 | 是 | 免费/商业 |
| DaFont | 60000+ | 许多 | 有限 | 各异 | 免费/付费 |
| Adobe Fonts | 20000+ | CC 附带 | 是 | 是 | CC 订阅 |
| Fontsource | 1500+ | 全部 | 是 | NPM 包 | 免费 |

**Google Fonts** - 最大的免费字体库，CDN 托管，支持可变字体。
```html
<link rel="preconnect" href="https://fonts.googleapis.com">
<link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
<link href="https://fonts.googleapis.com/css2?family=Inter:wght@400;600&display=swap" rel="stylesheet">
```

**Font Squirrel** - 可商用字体，字体识别工具，Web 字体生成器。
**DaFont** - 海量字体库，下载前预览，分类浏览。

---

## 图标

| 库 | 数量 | 格式 | 可定制 | 框架 | 许可证 |
|---------|-------|--------|--------------|------------|---------|
| Font Awesome | 2000+（免费） | SVG、Web Font | 是 | React、Vue、Angular | 免费/专业版 |
| Feather Icons | 280+ | SVG | 是 | React、Vue、Angular | MIT |
| Material Icons | 2500+ | SVG、Web Font | 有限 | React、Flutter | Apache 2.0 |
| Heroicons | 300+ | SVG | 是 | React、Vue | MIT |
| Lucide | 1400+ | SVG | 是 | React、Vue、Svelte | ISC |

**Font Awesome** - 最流行，solid/regular/light 样式，动画图标。
```html
<link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
<i class="fas fa-home"></i>
```

**Feather Icons** - 极简设计，24x24 网格，轻量。
```html
<script src="https://unpkg.com/feather-icons"></script>
<script>feather.replace();</script>
<i data-feather="home"></i>
```

**Material Icons** - Google 的 Material Design，多种样式（填充、轮廓、圆角）。
```html
<link href="https://fonts.googleapis.com/icon?family=Material+Icons" rel="stylesheet">
<span class="material-icons">home</span>
```

---

## 插画

| 库 | 风格 | 可定制 | 格式 | 许可证 | 数量 |
|---------|-------|--------------|---------|---------|-------|
| unDraw | 扁平、现代 | 通过 URL 改色 | SVG | MIT | 1000+ |
| Humaaans | 人物 | 混搭 | SVG、PNG、Figma | CC0 | 模块化 |
| Blush | 多种风格 | 是 | SVG、PNG、Figma | 免费/专业版 | 合集 |
| Storyset | 多种风格 | 颜色、背景 | SVG、PNG | 免费 | 1000+ |
| Open Peeps | 手绘 | 混搭 | SVG、PNG、Sketch | CC0 | 模块化 |

**unDraw** - 通过 URL 自定义颜色，风格统一，无需署名。
```html
<img src="https://undraw.co/illustrations/svg/design_tools.svg" alt="Design">
```

**Humaaans** - 模块化组件（头部、身体、腿部），姿势定制。
**Blush** - 多种艺术风格，Figma 插件，混搭组件。

---

## 图案

| 工具 | 类型 | 可定制 | 格式 | 许可证 | 数量 |
|------|------|--------------|--------|---------|-------|
| Hero Patterns | SVG 图案 | 颜色、透明度 | SVG、CSS | CC0 | 100+ |
| CSS Patterns | 纯 CSS | 颜色、大小 | CSS | MIT | 100+ |
| Pattern.monster | SVG 图案 | 是 | SVG | MIT | 100+ |
| Subtle Patterns | 纹理 | 否 | PNG | CC BY-SA | 400+ |
| Patternico | 生成图案 | 是 | PNG | 免费 | 自定义 |

**Hero Patterns** - 可重复 SVG 图案，颜色和透明度可控。
**CSS Patterns** - 无图片请求，纯 CSS 渐变。
```css
.pattern-stripes {
  background: repeating-linear-gradient(
    45deg, transparent, transparent 10px,
    #f0f0f0 10px, #f0f0f0 20px
  );
}
.pattern-dots {
  background: radial-gradient(circle, #ddd 1px, transparent 1px);
  background-size: 20px 20px;
}
```

---

## UI 套件

| 平台 | 生态 | 格式 | 协作 | 免费套件 | 费用 |
|----------|-----------|---------|---------------|-----------|------|
| Figma Community | Figma | Figma 文件 | 是 | 数千 | 免费 |
| Sketch App Sources | Sketch | Sketch 文件 | 有限 | 数百 | 免费/付费 |
| UI8 | 多平台 | Figma、Sketch、XD | 是 | 有限 | 付费 |
| Freebiesbug | 多平台 | 多种 | 否 | 全部 | 免费 |
| FigmaCrush | Figma | Figma 文件 | 是 | 全部 | 免费 |

**Figma Community** - 直接集成，实时协作，克隆并自定义。
**Sketch App Sources** - 精选质量，Sketch 专用资源，定期更新。

---

## CSS 框架

| 框架 | 方法 | 体积（min+gz） | 可定制 | 学习曲线 | 栅格 |
|-----------|----------|---------------|---------------|----------------|------|
| Bootstrap | 工具类 + 组件 | 22KB | Sass 变量 | 低 | Flexbox/Grid |
| Tailwind CSS | 工具类优先 | 10KB（purged） | 配置文件 | 中等 | Flexbox/Grid |
| Bulma | 基于组件 | 26KB | Sass 变量 | 低 | Flexbox |
| Foundation | 基于组件 | 18KB | Sass 变量 | 中等 | Flexbox |
| Materialize | Material Design | 16KB | Sass 变量 | 低 | Flexbox |

**Bootstrap** - 最流行，响应式栅格，丰富组件。
```html
<link href="https://cdn.jsdelivr.net/npm/bootstrap@5.3.0/dist/css/bootstrap.min.css" rel="stylesheet">
<div class="container">
  <div class="row">
    <div class="col-md-6">Column 1</div>
    <div class="col-md-6">Column 2</div>
  </div>
</div>
```

**Tailwind CSS** - 工具类优先，高度可定制，生产包极小。
```bash
npm install -D tailwindcss
npx tailwindcss init
```
```html
<div class="flex items-center justify-between p-4 bg-white shadow-md">
  <h1 class="text-xl font-bold text-gray-900">Logo</h1>
  <button class="px-4 py-2 text-white bg-blue-500 rounded hover:bg-blue-600">Sign Up</button>
</div>
```

**Bulma** - 纯 CSS（无 JavaScript），基于 Flexbox，类名简洁。

---

## 动画

| 库 | 类型 | 体积 | 易用性 | 性能 | 依赖 |
|---------|------|------|-------------|-------------|--------------|
| Animate.css | CSS 动画 | 80KB | 高 | 好 | 无 |
| AOS | 滚动动画 | 12KB | 高 | 好 | 无 |
| Lottie | JSON 动画 | 50KB+ | 中等 | 优秀 | Bodymovin |
| GSAP | JavaScript 动画 | 30KB | 中等 | 优秀 | 无 |
| Motion One | JavaScript 动画 | 6KB | 高 | 优秀 | 无 |

**Animate.css** - 即用型 CSS 动画，基于类名的 API。
```html
<link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/animate.css/4.1.1/animate.min.css">
<h1 class="animate__animated animate__fadeIn">Hello</h1>
<div class="animate__animated animate__bounceIn animate__delay-1s">Content</div>
```

**AOS** - 滚动触发动画，data 属性 API。
```html
<link href="https://unpkg.com/aos@2.3.1/dist/aos.css" rel="stylesheet">
<script src="https://unpkg.com/aos@2.3.1/dist/aos.js"></script>
<div data-aos="fade-up">Fade Up</div>
<script>AOS.init({ duration: 800, once: true });</script>
```

**Lottie** - After Effects 动画导出为 JSON，文件小，可交互。
```html
<script src="https://unpkg.com/@lottiefiles/lottie-player@latest/dist/lottie-player.js"></script>
<lottie-player src="animation.json" background="transparent" speed="1"
  style="width: 300px; height: 300px" loop autoplay></lottie-player>
```

---

## 响应式设计工具

| 工具 | 类型 | 功能 | 集成 | 费用 |
|------|------|----------|-------------|------|
| Chrome DevTools | 浏览器 | 设备模拟、网络节流 | Chrome | 免费 |
| Responsively | 桌面应用 | 多设备预览 | 所有浏览器 | 免费 |
| BrowserStack | 云 | 真实设备、3000+ 浏览器 | CI/CD | 付费 |
| LambdaTest | 云 | 真实设备、实时测试 | CI/CD | 免费/付费 |
| ScreenFly | Web | 快速设备测试 | 任何浏览器 | 免费 |

**Chrome DevTools** - `Ctrl+Shift+M`（Windows）或 `Cmd+Shift+M`（Mac）进入设备模式。
**Responsively** - 并排多设备预览，同步滚动。

**CSS 媒体查询：**
```css
/* 移动优先 */
.container { width: 100%; padding: 16px; }
@media (min-width: 768px) { .container { max-width: 720px; margin: 0 auto; } }
@media (min-width: 1024px) { .container { max-width: 960px; } }
@media (min-width: 1280px) { .container { max-width: 1200px; } }
```

**常用断点：**

| 设备 | 宽度 | 典型用途 |
|--------|-------|-------------|
| 小屏手机 | 320px | 旧款手机 |
| 大屏手机 | 375px | iPhone SE、12/13 |
| 平板 | 768px | iPad 竖屏 |
| 大平板 | 1024px | iPad 横屏 |
| 笔记本 | 1280px | 小型笔记本 |
| 桌面 | 1440px | 标准桌面 |

---

## 最佳实践

### 性能
- 使用 WebP 格式，JPEG 作为回退
- 使用 `loading="lazy"` 实现懒加载
- 使用 `srcset` 提供响应式图片
- Web 字体使用 `font-display: swap`
- 仅动画化 `transform` 和 `opacity`

### 无障碍
- 普通文本最低 4.5:1 对比度
- 大文本最低 3:1 对比度
- 纯图标按钮添加 `aria-label`
- 不要在没有替代方案的情况下移除 `outline`
```css
:focus-visible { outline: 2px solid #2a9d8f; outline-offset: 2px; }
```

### 许可证

| 许可证 | 商用 | 署名 | 修改 |
|---------|---------------|-------------|--------------|
| MIT | 是 | 需要 | 是 |
| CC0 | 是 | 否 | 是 |
| CC BY | 是 | 是 | 是 |
| CC BY-SA | 是 | 是 | 是（同许可证） |
| CC BY-NC | 否 | 是 | 是 |
| Unsplash | 是 | 否 | 是 |
| Pexels | 是 | 否 | 是 |

---

## 快速参考

- **图片：** [Unsplash](https://unsplash.com)、[Pexels](https://pexels.com)
- **配色：** [Coolors](https://coolors.co)、[Adobe Color](https://color.adobe.com)
- **字体：** [Google Fonts](https://fonts.google.com)、[Font Squirrel](https://www.fontsquirrel.com)
- **图标：** [Font Awesome](https://fontawesome.com)、[Feather Icons](https://feathericons.com)
- **插画：** [unDraw](https://undraw.co)、[Humaaans](https://www.humaaans.com)
- **图案：** [Hero Patterns](https://heropatterns.com)
- **UI 套件：** [Figma Community](https://www.figma.com/community)
- **CSS 框架：** [Bootstrap](https://getbootstrap.com)、[Tailwind CSS](https://tailwindcss.com)
- **动画：** [Animate.css](https://animate.style)、[AOS](https://michalsnik.github.io/aos/)
- **测试：** [Chrome DevTools](https://developer.chrome.com/docs/devtools/)、[Responsively](https://responsively.app)
