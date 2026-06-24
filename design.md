# 设计

> 本文档整合了以下源文件：design.md, designSystems.md, designTools.md, tool.md, color.md, product.md, tools.md

---

## 来源：design.md

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


---

## 来源：designSystems.md

## 概述

设计系统是一套关于原则和最佳实践的文档集合，用于指导团队构建数字产品。通常以 UI 组件库和模式库的形式存在，也可延伸至"语调与风格"等其他领域。

本教程收录了全球各行业领先的设计系统资源，涵盖科技公司、政府机构、开源项目等类别。

### 标签说明

| 标签 | 含义 |
|------|------|
| 组件库 | 包含可复用的代码组件和示例 |
| 语调指南 | 提供语言和文案使用规范 |
| 设计资源 | 提供 Sketch/Figma/Photoshop 等设计文件 |
| 开源代码 | 公开可查看的源代码 |

---

## 一、科技公司设计系统

| 名称 | 组件库 | 语调指南 | 设计资源 | 源代码 |
|------|:------:|:--------:|:--------:|:------:|
| [Adobe Spectrum](https://spectrum.adobe.com) | 有 | 有 | 有 | [GitHub](https://github.com/adobe/react-spectrum) |
| [阿里巴巴 Ant Design](https://ant.design) | 有 | 有 | 有 | [GitHub](https://github.com/ant-design/ant-design/) |
| [Atlassian Design System](https://atlassian.design) | 有 | 有 | 有 | [Bitbucket](https://bitbucket.org/atlassian/atlassian-frontend-mirror/) |
| [AWS Cloudscape](https://cloudscape.design/) | 有 | 有 | 有 | [GitHub](https://github.com/cloudscape-design/components) |
| [GitHub Primer](https://primer.style/) | 有 | - | 有 | [GitHub](https://github.com/primer/) |
| [GitLab Pajamas](https://design.gitlab.com/) | 有 | 有 | 有 | [GitLab](https://gitlab.com/gitlab-org/design.gitlab.com) |
| [Google Material Design](https://material.io/guidelines/#introduction-goals) | 有 | 有 | 有 | [GitHub](https://github.com/material-components/material-components) |
| [HashiCorp Helios](https://helios.hashicorp.design) | 有 | 有 | 有 | [GitHub](https://github.com/hashicorp/design-system) |
| [IBM Carbon](https://www.carbondesignsystem.com/) | 有 | 有 | 有 | [GitHub](https://github.com/ibm/carbon-components) |
| [IBM Design Language](https://www.ibm.com/design/language/) | 有 | 有 | - | - |
| [Microsoft Fluent](https://www.microsoft.com/design/fluent/) | 有 | - | 有 | [GitHub](https://github.com/microsoft/fluentui) |
| [Fluent UI](https://developer.microsoft.com/en-us/fluentui#/) | 有 | 有 | 有 | [GitHub](https://github.com/microsoft/fluentui) |
| [MongoDB Design System](http://mongodb.design) | 有 | - | 有 | [GitHub](https://github.com/mongodb/design) |
| [Oracle Redwood](https://redwood.oracle.com) | 有 | - | 有 | - |
| [SAP Fiori](https://experience.sap.com/fiori-design/) | 有 | - | - | - |
| [SAP Fundamental](https://github.com/SAP/fundamental) | 有 | - | - | [GitHub](https://github.com/SAP/fundamental) |
| [SAP OpenUI](https://github.com/SAP/openui5) | 有 | - | - | [GitHub](https://github.com/SAP/openui5) |
| [Salesforce Lightning](https://www.lightningdesignsystem.com) | 有 | 有 | 有 | [GitHub](https://github.com/salesforce-ux/design-system) |
| [Shopify Polaris](https://polaris.shopify.com) | 有 | 有 | 有 | [GitHub](https://github.com/Shopify/polaris) |
| [Siemens iX](https://ix.siemens.io/) | 有 | 有 | 有 | [GitHub](https://github.com/siemens/ix) |
| [Twilio Paste](https://paste.twilio.design/) | 有 | 有 | 有 | [GitHub](https://github.com/twilio-labs/paste) |
| [Uber Base Web](https://baseweb.design/) | 有 | - | - | [GitHub](https://github.com/uber-web/baseui) |
| [VMware Clarity](https://clarity.design/) | 有 | 有 | 有 | [GitHub](https://github.com/vmware/clarity) |
| [Vercel Geist](https://vercel.com/geist) | 有 | - | - | - |
| [Workday Canvas](https://design.workday.com/) | 有 | 有 | - | [GitHub](https://github.com/Workday/canvas-kit) |

## 二、互联网产品设计系统

| 名称 | 组件库 | 语调指南 | 设计资源 | 源代码 |
|------|:------:|:--------:|:--------:|:------:|
| [Amplify UI](https://ui.docs.amplify.aws/) | 有 | 有 | 有 | [GitHub](https://github.com/aws-amplify/amplify-ui/) |
| [Chakra UI](https://chakra-ui.com/) | 有 | - | - | [GitHub](https://github.com/chakra-ui/chakra-ui) |
| [Contentful Forma 36](https://f36.contentful.com/) | 有 | 有 | 有 | [GitHub](https://github.com/contentful/forma-36) |
| [Duolingo](https://design.duolingo.com/) | - | 有 | - | - |
| [eBay Skin](https://ebay.github.io/skin/) | 有 | - | - | [GitHub](https://github.com/eBay/skin) |
| [Elastic UI](https://elastic.github.io/eui/) | 有 | 有 | 有 | [GitHub](https://github.com/elastic/eui) |
| [Evergreen (Segment)](https://evergreen.surge.sh) | 有 | - | - | [GitHub](https://github.com/segmentio/evergreen) |
| [Flowbite](https://www.figma.com/community/file/1179442320711977498) | 有 | - | 有 | [GitHub](https://github.com/themesberg/flowbite) |
| [Grommet (HP)](https://grommet.github.io) | 有 | - | - | [GitHub](https://github.com/grommet/grommet) |
| [HubSpot Canvas](https://canvas.hubspot.com/) | 有 | 有 | - | [GitHub](https://github.com/HubSpot/canvas) |
| [Intuit Harmony](https://designsystem.quickbooks.com/) | 有 | 有 | 有 | - |
| [JetBrains Ring UI](https://jetbrains.github.io/ring-ui) | 有 | - | - | [GitHub](https://github.com/JetBrains/ring-ui) |
| [Mailchimp Styleguide](https://styleguide.mailchimp.com/) | - | 有 | - | - |
| [Mantine](https://mantine.dev/) | 有 | - | - | [GitHub](https://github.com/mantinedev/mantine) |
| [Mixpanel Design System](https://design.mixpanel.com) | 有 | 有 | - | - |
| [Morningstar Design System](http://designsystem.morningstar.com/) | 有 | 有 | 有 | - |
| [Pinterest Gestalt](https://pinterest.github.io/gestalt/#/) | 有 | - | - | [GitHub](https://github.com/pinterest/gestalt) |
| [Porsche Design System](https://designsystem.porsche.com) | 有 | - | 有 | [GitHub](https://github.com/porsche-design-system/porsche-design-system) |
| [Radix](https://www.radix-ui.com/) | 有 | - | - | [GitHub](https://github.com/radix-ui) |
| [Semi Design](https://semi.design/en-US) | 有 | - | 有 | [GitHub](https://github.com/DouyinFE/semi-design) |
| [Shadcn/ui](https://ui.shadcn.com/) | 有 | - | - | [GitHub](https://github.com/shadcn-ui) |
| [Shoelace](https://shoelace.style) | 有 | 有 | - | [GitHub](https://github.com/shoelace-style/shoelace) |
| [Skyscanner Backpack](https://skyscanner.design/) | 有 | 有 | 有 | [GitHub](https://github.com/skyscanner/backpack) |
| [Help Scout](https://style.helpscout.com/) | 有 | 有 | - | [GitHub](https://github.com/helpscout/seed-framework) |
| [Stacks (Stack Overflow)](https://stackoverflow.design/) | 有 | 有 | - | [GitHub](https://github.com/StackExchange/Stacks) |
| [Sprout Social Seeds](https://sproutsocial.com/seeds) | 有 | 有 | 有 | - |
| [Strapi Design System](https://design-system.strapi.io/) | 有 | - | - | [GitHub](https://github.com/strapi/design-system) |
| [Telefonica Mistica](https://brandfactory.telefonica.com/mistica) | 有 | - | 有 | [GitHub](https://github.com/Telefonica/mistica) |
| [Thumbprint (Thumbtack)](https://thumbprint.design/) | 有 | - | - | [GitHub](https://github.com/thumbtack/thumbprint) |
| [Vimeo Iris](https://vimeo.github.io/iris/) | 有 | - | - | [GitHub](https://github.com/vimeo/iris) |
| [VTEX Styleguide](https://styleguide.vtex.com/) | 有 | - | 有 | [GitHub](https://github.com/vtex/styleguide) |
| [Welcome UI](http://www.welcome-ui.com/) | 有 | - | - | [GitHub](https://github.com/WTTJ/welcome-ui) |
| [Zendesk Garden](https://garden.zendesk.com/) | 有 | - | - | [GitHub](https://github.com/zendeskgarden) |

## 三、政府及公共机构设计系统

| 名称 | 组件库 | 语调指南 | 设计资源 | 源代码 |
|------|:------:|:--------:|:--------:|:------:|
| [BBC GEL](https://www.bbc.co.uk/gel) | 有 | 有 | 有 | - |
| [City of Boston Fleet](https://patterns.boston.gov/) | 有 | 有 | - | [GitHub](https://github.com/CityOfBoston/digital) |
| [Estonia Country Design](https://brand.estonia.ee) | 有 | 有 | 有 | - |
| [芬兰 Toolbox](https://toolbox.finland.fi/) | - | 有 | 有 | - |
| [法国政府设计系统](https://www.systeme-de-design.gouv.fr/) | 有 | 有 | 有 | [GitHub](https://github.com/GouvernementFR/dsfr) |
| [GOV.UK Design System](https://www.gov.uk/design-system) | 有 | - | - | [GitHub](https://github.com/alphagov/govuk-design-system) |
| [韩国设计系统](https://www.krds.go.kr) | 有 | 有 | 有 | [GitHub](https://github.com/KRDS-uiux/krds-uiux) |
| [意大利设计系统](https://designers.italia.it/design-system/) | 有 | 有 | 有 | [GitHub](https://github.com/italia) |
| [NASA Web Design System](https://nasa.github.io/nasawds-site/) | 有 | - | - | [GitHub](https://github.com/nasa/nasawds) |
| [NHS.UK Service Manual](https://service-manual.nhs.uk/) | 有 | 有 | - | - |
| [纽约州设计系统](https://designsystem.ny.gov/components/) | 有 | - | 有 | [GitHub](https://github.com/ITS-HCD/nysds) |
| [安大略设计系统](https://designsystem.ontario.ca/) | 有 | - | 有 | [官网](https://designsystem.ontario.ca/docs/documentation/release-notes.html#latest) |
| [新加坡政府设计系统](https://www.designsystem.tech.gov.sg/) | 有 | 有 | 有 | [GitHub](https://github.com/govtechsg/sgds) |
| [英国 Co-op](https://www.coop.co.uk/experience-library/) | 有 | 有 | 有 | [GitHub](https://github.com/coopdigital/experience-library) |
| [美国 Web Design Standards](https://designsystem.digital.gov/) | 有 | 有 | 有 | [GitHub](https://github.com/uswds/uswds) |
| [美国 CMS.gov](https://design.cms.gov/) | 有 | - | - | - |
| [加拿大 Aurora](https://design.gccollab.ca/) | 有 | 有 | 有 | [GitHub](https://github.com/gctools-outilsgc/design-system) |

## 四、开源及社区驱动设计系统

| 名称 | 组件库 | 语调指南 | 设计资源 | 源代码 |
|------|:------:|:--------:|:--------:|:------:|
| [Blueprint (Palantir)](https://blueprintjs.com/) | 有 | - | 有 | [GitHub](https://github.com/palantir/blueprint) |
| [Braid Design System](https://seek-oss.github.io/braid-design-system/) | 有 | - | - | [GitHub](https://github.com/seek-oss/braid-design-system) |
| [Cedar (REI)](https://rei.github.io/rei-cedar-docs/) | 有 | - | 有 | [GitHub](https://github.com/rei/rei-cedar) |
| [Decathlon Vitamin](https://decathlon.design/) | 有 | - | 有 | [GitHub](https://github.com/decathlon/vitamin-web) |
| [Foundation](https://get.foundation/) | 有 | 有 | 有 | [GitHub](https://github.com/foundation/foundation-sites) |
| [Materialize CSS](https://materializecss.com/) | 有 | - | 有 | [GitHub](https://github.com/Dogfalo/materialize) |
| [Material Minimal](https://material-minimal.com/) | 有 | 有 | 有 | [GitHub](https://github.com/mdbootstrap/mdb-ui-kit) |
| [Mozilla Protocol](https://protocol.mozilla.org/) | 有 | - | - | [GitHub](https://github.com/mozilla/protocol) |
| [Scania DDS](https://digitaldesign.scania.com/home) | 有 | - | 有 | [GitHub](https://github.com/scania-digital-design-system/sdds) |
| [SEEK Style Guide](https://seek-oss.github.io/seek-style-guide/) | 有 | - | - | [GitHub](https://github.com/seek-oss/seek-style-guide) |
| [Semrush Intergalactic](https://i.semrush.com/) | 有 | - | 有 | [GitHub](https://github.com/semrush/intergalactic) |
| [Ubuntu Vanilla](https://vanillaframework.io/) | 有 | 有 | 有 | [GitHub](https://github.com/canonical-web-and-design/vanilla-framework) |
| [Uiverse](https://uiverse.io) | 有 | 有 | 有 | [GitHub](https://github.com/uiverse-io/galaxy) |
| [Vue Design System](https://vueds.com/) | 有 | - | - | [GitHub](https://github.com/viljamis/vue-design-system) |

## 五、其他行业设计系统

| 名称 | 行业 | 组件库 | 语调指南 | 设计资源 | 源代码 |
|------|------|:------:|:--------:|:--------:|:------:|
| [Aalto University](https://brand.aalto.fi/) | 教育 | 有 | 有 | 有 | - |
| [Audi UI Kit](https://www.audi.com/ci/en/guides/user-interface/introduction.html) | 汽车 | 有 | - | 有 | [GitHub](https://github.com/audi/audi-ui) |
| [British Gas Nucleus](https://britishgas.design/) | 能源 | 有 | 有 | - | - |
| [BuzzFeed Solid](https://solid.buzzfeed.com/) | 媒体 | 有 | - | 有 | [GitHub](https://github.com/buzzfeed/solid) |
| [Cloudflare](https://cloudflare.github.io/cf-ui/) | 云服务 | 有 | - | - | [GitHub](https://github.com/cloudflare/cf-ui) |
| [Financial Times Origami](https://origami.ft.com/) | 媒体 | 有 | - | - | [GitHub](https://github.com/Financial-Times/origami) |
| [Firefox Photon](https://design.firefox.com/photon) | 浏览器 | 有 | 有 | 有 | [GitHub](https://github.com/FirefoxUX/photon) |
| [Foyer Design System](https://design.foyer.lu/) | 金融 | 有 | - | 有 | - |
| [Gympass Yoga](https://gympass.github.io/yoga/) | 健身 | 有 | 有 | - | [GitHub](https://github.com/gympass/yoga) |
| [Hudl Uniform](https://uniform.hudl.com/) | 体育 | 有 | 有 | - | - |
| [Just Eat PIE](https://pie.design/) | 外卖 | 有 | - | 有 | [GitHub](https://github.com/justeattakeaway/pie) |
| [Kontur](https://guides.kontur.ru/) | 软件 | 有 | - | 有 | [GitHub](https://github.com/skbkontur/retail-ui/) |
| [Lexicon (Liferay)](https://lexicondesign.io/) | 企业 | 有 | 有 | - | - |
| [Mail.ru Paradigm](https://design.mail.ru/) | 互联网 | 有 | 有 | 有 | - |
| [NationBuilder Radius](https://www.nationbuilder.design/) | 政治 | 有 | - | - | - |
| [Nordhealth](https://nordhealth.design/) | 医疗 | 有 | - | 有 | - |
| [Nordnet](https://brand.nordnet.se/) | 金融 | 有 | 有 | - | - |
| [Okta Odyssey](https://odyssey.okta.design) | 安全 | 有 | - | 有 | [GitHub](https://github.com/okta/odyssey) |
| [Pharos (JSTOR)](https://pharos.jstor.org) | 学术 | 有 | 有 | - | [GitHub](https://github.com/ithaka/pharos) |
| [Pivotal](https://styleguide.pivotal.io/) | 企业 | 有 | - | - | [GitHub](https://github.com/pivotal-cf/pivotal-ui) |
| [Pluralsight](https://design-system.pluralsight.com/) | 教育 | 有 | - | - | [GitHub](https://github.com/pluralsight/design-system) |
| [Priceline](https://priceline.github.io/design-system/) | 旅游 | 有 | 有 | - | [GitHub](https://github.com/priceline/design-system) |
| [Sage (Kajabi)](https://sage.kajabi.com) | 教育 | 有 | - | - | [GitHub](https://github.com/Kajabi/sage-lib) |
| [Samsung Tizen](https://developer.samsung.com/one-ui-watch-tizen) | 硬件 | 有 | - | 有 | [GitHub](https://github.com/Samsung/Tizen.CircularUI) |
| [Starbucks Style Guide](https://creative.starbucks.com) | 餐饮 | 有 | 有 | - | - |
| [Teambition Clarity](https://design.teambition.com/) | 协作 | 有 | - | - | - |
| [Vibe (Monday.com)](https://style.monday.com/) | 协作 | 有 | - | 有 | [GitHub](https://github.com/mondaycom/vibe) |
| [Wix Style React](https://www.wix-style-react.com/storybook/) | 建站 | 有 | - | - | - |
| [Yelp Styleguide](https://www.yelp.com/styleguide) | 本地服务 | 有 | 有 | - | - |

## 六、轻量级设计系统

以下系统以组件库为主，文档较少但代码质量较高：

| 名称 | 源代码 |
|------|:------:|
| [Appear Here Bloom](https://bloom.appearhere.co.uk/) | [GitHub](https://github.com/appearhere/bloom) |
| [Aragon UI](https://ui.aragon.org/) | [GitHub](https://github.com/aragon/ui) |
| [Artsy Palette](https://palette.artsy.net/) | [GitHub](https://github.com/artsy/palette) |
| [Astro UXDS](https://astrouxds.com/) | [GitHub](https://github.com/RocketCommunicationsInc/astro-components) |
| [AT UIKIT](https://at-ui.github.io/at-ui/#/en) | [GitHub](https://github.com/at-ui/at-ui) |
| [AutoGuru Overdrive](http://overdrive.autoguru.io/) | [GitHub](https://github.com/autoguru-au/overdrive) |
| [Basis](https://basis.now.sh) | [GitHub](https://github.com/moroshko/basis) |
| [Bento DS](https://bento-ds.com) | [GitHub](https://github.com/buildo/bento-design-system) |
| [BLiP](https://design.take.net/) | [GitHub](https://github.com/takenet/blip-toolkit) |
| [Bold (Bridge)](https://bold.bridge.ufsc.br/) | [GitHub](https://github.com/laboratoriobridge/bold) |
| [Bolt Design System](https://boltdesignsystem.com/) | [GitHub](https://github.com/boltdesignsystem/bolt) |
| [Bumbag UI](https://bumbag.style/) | [GitHub](https://github.com/bumbag/bumbag-ui) |
| [CA Mineral UI](https://mineral-ui.netlify.app/) | [GitHub](https://github.com/mineral-ui/mineral-ui) |
| [Decentraland UI](https://ui.decentraland.org/) | [GitHub](https://github.com/decentraland/ui) |
| [Enigma Boundless](https://boundless.js.org/) | [GitHub](https://github.com/enigma-io/boundless) |
| [Jobber Atlantis](https://atlantis.getjobber.com) | [GitHub](https://github.com/GetJobber/atlantis) |
| [KoliBri (Public-UI)](https://public-ui.github.io/) | [GitHub](https://github.com/public-ui/kolibri/) |
| [Marvel Styleguide](https://marvelapp.com/styleguide) | - |
| [Pusher Chameleon](https://pusher.github.io/chameleon/) | [GitHub](https://github.com/pusher/chameleon) |
| [Rambler UI](https://rambler-digital-solutions.github.io/rambler-ui/) | [GitHub](https://github.com/rambler-digital-solutions/rambler-ui) |
| [Rendition (Balena)](https://balena-io-modules.github.io/rendition/) | [GitHub](https://github.com/balena-io-modules/rendition/) |
| [Reshaped](https://reshaped.so) | - |
| [Untitled UI](https://www.untitledui.com/react/) | [GitHub](https://github.com/untitleduico/react/) |
| [WeWork Ray](https://ray.wework.com) | [GitHub](https://github.com/wework/ray) |

---

## 关键要点

### 设计系统的核心组成

| 组成部分 | 说明 |
|----------|------|
| 组件库 | 可复用的 UI 组件（按钮、表单、导航等） |
| 设计语言 | 色彩、字体、间距、图标等视觉规范 |
| 语调指南 | 文案风格、术语规范、错误提示措辞 |
| 设计资源 | Figma/Sketch 文件，供设计师直接使用 |
| 模式库 | 常见交互模式和页面模板 |

### 如何选择设计系统

| 考量因素 | 建议 |
|----------|------|
| 技术栈匹配 | 优先选择与项目框架一致的系统（React/Vue/Angular） |
| 社区活跃度 | GitHub star 数、issue 响应速度、版本更新频率 |
| 文档质量 | 是否有完整的组件文档、示例代码、设计指南 |
| 许可证 | 开源不等于可商用，务必检查许可证类型 |
| 定制能力 | 是否支持主题定制、组件扩展 |

### 学习路径建议

| 阶段 | 行动 |
|------|------|
| 入门 | 阅读 Google Material Design 和 IBM Carbon，理解设计系统的基本理念 |
| 实践 | 选择一个开源系统（如 Ant Design、Chakra UI）在项目中使用 |
| 进阶 | 研究 Shopify Polaris 或 Salesforce Lightning 的完整文档体系 |
| 输出 | 参考以上系统，为自己的团队构建设计系统 |

---

*注意：本列表中的"设计系统"、"UI 库"和"模式库"三个概念常被混用，本教程包含这三种类型。标记为开源的项目不一定允许商用，使用前请检查具体许可证。*


---

## 来源：designTools.md

## 概览

本文整理了设计师在日常工作中可能用到的各类工具和资源，涵盖从 UI 设计、原型制作、协作管理到素材资源等多个领域。工具按功能分类，便于快速查找。

> 图例：免费 = 免费工具 | 开源 = 开源工具 | Mac = 仅限 macOS

---

## 目录

1. [无障碍工具](#1-无障碍工具)
2. [动画工具](#2-动画工具)
3. [增强现实工具](#3-增强现实工具)
4. [协作工具](#4-协作工具)
5. [取色工具](#5-取色工具)
6. [设计反馈工具](#6-设计反馈工具)
7. [设计交付工具](#7-设计交付工具)
8. [设计灵感](#8-设计灵感)
9. [设计系统工具](#9-设计系统工具)
10. [设计转代码工具](#10-设计转代码工具)
11. [设计版本控制](#11-设计版本控制)
12. [开发工具](#12-开发工具)
13. [体验监控工具](#13-体验监控工具)
14. [字体工具](#14-字体工具)
15. [渐变工具](#15-渐变工具)
16. [图标工具](#16-图标工具)
17. [插画资源](#17-插画资源)
18. [信息架构工具](#18-信息架构工具)
19. [Logo 设计工具](#19-logo-设计工具)
20. [样机工具](#20-样机工具)
21. [无代码工具](#21-无代码工具)
22. [像素画工具](#22-像素画工具)
23. [原型工具](#23-原型工具)
24. [截图工具](#24-截图工具)
25. [草图工具](#25-草图工具)
26. [社交媒体设计工具](#26-社交媒体设计工具)
27. [音效设计](#27-音效设计)
28. [图片素材](#28-图片素材)
29. [视频素材](#29-视频素材)
30. [设计学习资源](#30-设计学习资源)
31. [UI 设计工具](#31-ui-设计工具)
32. [用户流程工具](#32-用户流程工具)
33. [用户研究工具](#33-用户研究工具)
34. [可视化调试工具](#34-可视化调试工具)
35. [线框图工具](#35-线框图工具)
36. [3D 建模软件](#36-3d-建模软件)

---

## 1. 无障碍工具

用于检测和改善网站/App 的无障碍合规性，确保产品对所有用户可用。

| 工具 | 说明 | 免费/开源 |
|------|------|-----------|
| [A11ygator](https://a11ygator.chialab.io) | 基于 WCAG 规则分析网站，提供 Chrome 扩展 | 免费、开源 |
| [Accessibility Insights](https://accessibilityinsights.io/) | 帮助开发者快速发现和修复无障碍问题 | 免费 |
| [Accessible Palette Builder](https://toolness.github.io/accessible-color-matrix/) | 基于 Elm 构建无障碍调色板的原型工具 | 免费、开源 |
| [AChecker](https://achecker.ca) | 评估 HTML 内容无障碍问题的 Web 应用 | 免费 |
| [ANDI](https://www.ssa.gov/accessibility/andi/help/install.html) | Web 内容无障碍测试工具（书签形式），检查 508 合规性 | 免费、开源 |
| [Axe](https://www.deque.com/axe/) | 适用于所有现代浏览器的自动化无障碍测试引擎 | 免费、开源 |
| [ColorBox](http://www.colorbox.io/) | 通过算法构建无障碍色彩系统（由 Lyft 设计团队开发） | 免费 |
| [Colorable](https://colorable.jxnblk.com/) | 基于 Web 的对比度检测工具 | 免费 |
| [Color Oracle](https://colororacle.org/) | 色盲模拟器 | 免费 |
| [Contrast](https://usecontrast.com/) | macOS 应用，快速查看 WCAG 颜色对比度 | Mac |
| [Contrast Checker](https://contrast-checker.glitch.me/) | 检查元素背景与页面之间的对比度 | 免费 |
| [Contraste](https://contrasteapp.com/) | 检查文本是否符合 WCAG 无障碍标准 | 免费 |
| [Hex Naw](https://hexnaw.com/) | 测试整个色彩系统的对比度和无障碍性 | 免费 |
| [Leonardo](https://leonardocolor.io) | 按目标 WCAG 对比度生成调色板，由 Adobe 开发 | 免费、开源 |
| [PA11Y](http://pa11y.org/) | 命令行无障碍测试工具，支持编程方式报告 | 免费、开源 |
| [Sim Daltonism](https://michelf.ca/projects/sim-daltonism/) | macOS/iOS 色盲模拟器 | 免费、开源 |
| [Stark](https://getstark.co/) | Sketch 插件，模拟不同类型色盲 | 付费 |
| [Toptal Color Filter](https://www.toptal.com/designers/colorfilter) | 测试网站在不同色盲人群中的显示效果 | 免费 |
| [tota11y](http://khan.github.io/tota11y/) | 无障碍可视化工具包 | 免费 |
| [WAVE](https://wave.webaim.org/) | 在 Chrome 和 Firefox 中直接评估网页无障碍问题 | 免费 |
| [90 Examples](http://clrs.cc/a11y/) | 无障碍色彩主题合集 | 免费 |

---

## 2. 动画工具

用于创建交互动画、微交互、滚动动画等，提升用户体验。

| 工具 | 说明 | 免费/开源 |
|------|------|-----------|
| [After Effects](https://www.adobe.com/products/aftereffects.html) | Adobe 视觉特效、动态图形和合成应用 | 付费 |
| [BeatFlyer](https://beatflyer.com/) | 快速从多层合成中创建循环动画的 Web 工具 | 付费 |
| [Flare](https://www.2dimensions.com/about-flare) | 为应用或游戏创建动画的设计和动画工具 | 免费 |
| [Flow](https://createwithflow.com/) | Sketch 设计的专业动画工具，可导出 iOS/Web/SVG 代码 | Mac |
| [GSAP](https://greensock.com/) | 高性能 HTML5 脚本动画套件 | 免费 |
| [Haiku Animator](https://www.haikuforteams.com/) | 基于关键帧的动画工具，连接 UI 工具与代码 | 付费 |
| [Keyshape](https://www.keyshapeapp.com/) | 2D 动画工具，支持导出动画 SVG | Mac |
| [Kite Compositor](https://kiteapp.co/) | Mac 和 iOS 的动画与原型应用 | Mac |
| [LightBox](https://uselightbox.com/) | 2D 手绘动画工具 | 免费、Mac |
| [Lottie](https://airbnb.io/lottie/) | 解析 After Effects 动画 JSON 并在移动端/Web 端原生渲染 | 免费 |
| [Mantra](https://jeremyckahn.github.io/mantra/) | 基于 Web 的时间轴动画工具 | 开源 |
| [OFFEO](https://offeo.com/) | 在线视频制作工具，适合小型企业创建视频广告 | 免费 |
| [Spirit](https://spiritapp.io/) | 在浏览器中实时创建和管理动画 | Mac |
| [Stylie](https://jeremyckahn.github.io/stylie/) | 基于 Web 的 CSS3 图形化动画工具 | 开源 |
| [Tumult Hype](https://tumult.com/hype/) | macOS 的 HTML5 动画和交互内容创建应用 | Mac |

---

## 3. 增强现实工具

用于创建、投射和原型化 AR 应用。

| 工具 | 说明 | 免费/开源 |
|------|------|-----------|
| [Daqri](https://daqri.com/) | 将数字信息叠加到物理环境的专业级 AR | 付费 |
| [EasyAR](https://www.easyar.com/) | 移动应用和 AR 引擎 | 付费 |
| [Lens Studio](https://lensstudio.snapchat.com/) | 为 Snapchat 创建、发布和分享 AR 体验 | 免费 |
| [Spark AR Studio](https://www.sparkar.com) | 为 Instagram 创建 AR 体验，无需编码 | 免费、Mac |
| [Torch](https://www.torch.app/) | 基于云端的 3D 设计和原型工具，专注于移动端 AR | 免费、Mac |
| [Unity](https://unity.com/) | 构建高质量 3D/2D 游戏，部署到移动端、桌面和 VR/AR | 付费 |
| [Vectary](https://www.vectary.com/) | 为网站创建 3D 和 AR 内容 | 付费 |
| [Vuforia](https://www.vuforia.com/) | 移动设备 AR 应用开发 SDK | 付费 |
| [Wikitude](https://www.wikitude.com/) | 为 iOS/Android/智能眼镜提供图像和物体追踪 | 付费 |

---

## 4. 协作工具

团队协作、项目管理和实时沟通工具。

| 工具 | 说明 | 免费/开源 |
|------|------|-----------|
| [Airtable](https://airtable.com/) | 电子表格与数据库结合的灵活组织工具 | 付费 |
| [Asana](https://asana.com/) | 团队工作管理平台 | 付费 |
| [Basecamp](https://basecamp.com/) | 项目管理套件，集中管理员工和任务 | 付费 |
| [Excalidraw](https://excalidraw.com/) | 手绘风格的白板绘图工具 | 免费、开源 |
| [Jira](https://www.atlassian.com/software/jira) | 敏捷团队的软件开发工具 | 付费 |
| [Jitsi](https://jitsi.org/) | 多平台开源视频会议 | 免费、开源 |
| [Miro](https://www.realtimeboard.com/) | 跨职能团队协作白板平台 | 付费 |
| [Notion](https://www.notion.so) | 集写作、计划、协作和组织于一体的工具 | 付费 |
| [Slack](https://slack.com/) | 团队协作和沟通中心 | 付费 |
| [Trello](https://trello.com/) | 基于 Web 的项目管理应用 | 付费 |
| [Witeboard](https://www.witeboard.com/) | 简单的实时协作白板 | 免费 |
| [Zulip](https://zulipchat.com/) | 结合即时聊天和邮件线程模型的开源通讯工具 | 开源 |
| [Mattermost](https://mattermost.com/) | 满足高安全标准的开源消息平台 | 开源 |
| [Nextcloud](https://nextcloud.com) | 开源协作平台，包含文件、看板、聊天等 | 免费、开源 |

---

## 5. 取色工具

取色器、色彩识别和调色板生成工具。

| 工具 | 说明 | 免费/开源 |
|------|------|-----------|
| [BrandColors](https://brandcolors.net/) | 最大的品牌官方色彩代码合集 | 免费 |
| [Color by Adobe](https://color.adobe.com/explore/) | 使用色轮创建配色方案，浏览社区配色 | 免费 |
| [Color Hunt](https://colorhunt.co/) | 免费开放的色彩灵感平台，数千款手工精选调色板 | 免费 |
| [Coolors](https://coolors.co/) | 超快配色方案生成器 | 免费、Mac |
| [Khroma](http://khroma.co/) | 基于 AI 根据个人偏好生成调色板 | 付费 |
| [Paletton](https://paletton.com) | 创建协调配色组合的设计工具 | 免费 |
| [Picular](https://picular.co/) | 利用 Google 图片搜索生成主色调 | 免费 |
| [Pigment](https://pigment.shapefactory.co/) | 提供多种色彩配置方案的调色板生成器 | 免费 |
| [React Color](http://casesandberg.github.io/react-color/) | 来自 Sketch、Photoshop、Chrome 的取色器集合 | 免费、开源 |
| [Sip](https://sipapp.io/) | macOS 全局取色工具，支持收集、组织和分享颜色 | Mac |
| [Skala Color](https://bjango.com/mac/skalacolor/) | 支持多种格式，适用于 Web/iOS/Android/macOS 开发 | 免费、Mac |
| [Viz Palette](https://projects.susielu.com/viz-palette) | 数据可视化专用取色器 | 免费 |

---

## 6. 设计反馈工具

在开发过程中收集和管理设计反馈。

| 工具 | 说明 | 免费/开源 |
|------|------|-----------|
| [Flawless Feedback](https://flawlessapp.io/feedback) | 审查和标注 iOS 应用，分享反馈到 Jira 或 Trello | Mac |
| [GoVisually](https://govisually.com) | 在线校对、设计审查和审批软件 | 付费 |

---

## 7. 设计交付工具

设计师完成工作后向开发者交付设计稿，包含规格、资产和代码片段。

| 工具 | 说明 | 免费/开源 |
|------|------|-----------|
| [Avocode](https://avocode.com) | 无需设计工具即可打开设计稿，自动获取代码 | 付费 |
| [Inspect](https://www.invisionapp.com/feature/inspect/) | InVision 出品，为开发准备设计稿 | 付费 |
| [Sketch Measure](https://github.com/utom/sketch-measure) | Sketch 标注插件，标注元素距离和尺寸 | 免费、开源 |
| [Specctr](https://specctr.com) | 在 PS/AI/ID 中创建红线标注 | 付费 |
| [Sympli](https://sympli.io) | 从 Sketch/Photoshop/Adobe XD 自动交付规格和资产 | 付费 |
| [Zeplin](https://zeplin.io/) | 自动生成准确规格、资产和代码片段的交付工具 | 付费 |

---

## 8. 设计灵感

设计模式、用户流程和创意解决方案的灵感资源。

| 工具 | 说明 | 免费/开源 |
|------|------|-----------|
| [Behance](https://www.behance.net/) | 展示和发现创意作品的在线平台 | 免费 |
| [Dribbble](https://dribbble.com/) | 展示用户创作作品的在线社区 | 付费 |
| [Mobbin](https://mobbin.design/) | 浏览热门应用的移动端设计模式 | 免费 |
| [One Page Love](https://onepagelove.com/gallery) | 单页网站设计灵感合集 | 免费 |
| [Page Flows](https://pageflows.com/) | 用户流程视频和截图，涵盖 160+ 种任务 | 免费 |
| [Really Good Emails](https://reallygoodemails.com/) | 4150+ 手工精选的邮件设计 | 免费 |
| [ReallyGoodUX](https://www.reallygoodux.io/) | 来自真实产品的优秀 UX 示例截图 | 免费 |
| [Typewolf](https://www.typewolf.com/) | 帮助设计师选择完美字体组合 | 免费 |
| [UI Sources](https://www.uisources.com/) | 500+ 来自顶级应用的交互设计 | 免费 |
| [UX Archive](http://uxarchive.com/) | 120+ 移动应用的 400+ 用户流程 | 免费 |
| [Waveguide](https://www.waveguide.io/) | 包含数千个产品和品牌体验示例的设计知识库 | 付费 |
| [Web Design Museum](https://www.webdesignmuseum.org/) | 1994-2006 年间 1200+ 网站设计趋势展览 | 付费 |
| [Lapa Ninja](https://www.lapa.ninja/) | 1800+ 落地页设计灵感，每日更新 | 免费 |
| [Httpster](https://httpster.net/) | 来自全球的优秀网站灵感展示 | 免费 |
| [Collect UI](http://collectui.com/) | 基于 Dribbble 的每日 UI 灵感，14000+ 精选设计 | 免费 |

---

## 9. 设计系统工具

构建、维护和组织设计系统的工具。

| 工具 | 说明 | 免费/开源 |
|------|------|-----------|
| [Catalog](https://www.catalog.style/) | 数字产品的活样式指南，结合文档与实时组件 | 开源 |
| [Design System Manager](https://www.invisionapp.com/design-system-manager/) | InVision 的设计系统管理器 | 付费 |
| [DSK](https://rundsk.com) | 协作创建设计系统的工作台 | 免费、开源 |
| [Eva Design System](https://eva.design/) | 可定制的设计系统，提供移动端和 Web 组件库 | 免费、开源 |
| [Frontify](https://frontify.com/) | 创建图形规范、模式库和设计系统 | 付费 |
| [Lingo](https://www.lingoapp.com/) | 与整个团队创建共享资产库 | Mac |
| [Lucid](https://lucid.style/) | 创建、管理和共享设计系统的工具 | 付费 |
| [Modulz](https://www.modulz.app/) | 无需编码即可设计、构建、文档化和发布设计系统 | 付费 |
| [Specify](https://www.specifyapp.com/) | 创建、扩展和维护设计系统 | 付费 |
| [Storybook](https://storybook.js.org/) | 为 React/Vue/Angular 独立开发 UI 组件的开源工具 | 开源 |
| [Zeroheight](https://www.zeroheight.com/) | 由设计师创建、开发者扩展、所有人可编辑的样式指南 | 付费 |

---

## 10. 设计转代码工具

将设计转换为可运行的网站或应用，无需编写代码。

| 工具 | 说明 | 免费/开源 |
|------|------|-----------|
| [Anima](https://www.animaapp.com/) | 将 Sketch 转换为 HTML 的 Web 应用和 Sketch 插件 | 付费 |
| [Blocs](https://blocsapp.com/) | 可视化 Web 设计工具，无需编码即可创建响应式网站 | Mac |
| [Bootstrap Studio](https://bootstrapstudio.io/) | 基于 Bootstrap 框架的网页设计工具 | 付费 |
| [Draftbit](https://draftbit.com/) | 在浏览器中可视化设计和构建移动应用 | 付费 |
| [EasyLogic Studio](https://www.easylogic.studio/) | CSS+SVG 设计工具，支持代码导出 | 免费、开源 |
| [Mobirise](https://mobirise.com/) | 基于 Bootstrap 的离线拖放式网站构建器 | 免费 |
| [PaintCode](https://www.paintcodeapp.com) | 矢量绘图应用，即时转换为 Swift/ObjC/JS/Java 代码 | Mac |
| [Pinegrow](https://pinegrow.com/) | 支持 CSS Grid、Bootstrap、Foundation 的专业可视化编辑器 | 付费 |
| [Tilda](https://tilda.cc/) | 使用模块化组件免费创建网站、落地页或在线商店 | 付费 |
| [Wix](https://www.wix.com/) | 功能全面的网站构建器 | 付费 |
| [Webflow](https://webflow.com/) | 在浏览器中构建响应式网站，支持导出代码 | 付费 |
| [STUDIO](https://studio.design/) | 从零设计、实时协作并发布网站 | 付费 |

---

## 11. 设计版本控制

管理和追踪设计文件版本的工具。

| 工具 | 说明 | 免费/开源 |
|------|------|-----------|
| [Abstract](https://www.abstract.com/) | 设计团队的 Sketch 文件版本管理和协作平台 | 付费 |
| [Folio](http://folioformac.com/) | 基于 Git 的简单设计版本控制系统 | Mac |
| [Kactus](https://kactus.io/) | 不改变工具的设计版本控制 | 开源、Mac |
| [Plant](https://plantapp.io/) | Mac 应用和 Sketch 插件，提供完整版本控制 | Mac |
| [Versions](https://versions.sympli.io) | 支持可视化差异对比、合并和冲突解决的版本控制工具 | 付费 |

---

## 12. 开发工具

开发浏览器和辅助开发的设计工具。

| 工具 | 说明 | 免费/开源 |
|------|------|-----------|
| [Blisk](https://blisk.io) | 提供开发工作区，加速 Web 应用开发和测试 | 付费 |
| [Firefox Developer Edition](https://www.mozilla.org/en-US/firefox/developer/) | Firefox 浏览器开发者版本 | 免费 |
| [Litmus](https://litmus.com/) | 邮件营销创建平台，预览 HTML 邮件在各客户端的显示效果 | 付费 |
| [Polypane](https://polypane.rocks) | 专为创建和测试网站而构建的浏览器 | 付费 |
| [Storybook](https://storybook.js.org/) | 为 React/Vue/Angular 独立开发 UI 组件的开源工具 | 免费、开源 |
| [Styleguidist](https://github.com/styleguidist/react-styleguidist) | 带活样式指南的独立 React 组件开发环境 | 免费、开源 |

---

## 13. 体验监控工具

分析用户行为、收集反馈的工具。

| 工具 | 说明 | 免费/开源 |
|------|------|-----------|
| [Amplitude](https://amplitude.com/) | 用户行为分析，快速发布更好的产品体验 | 付费 |
| [FullStory](https://www.fullstory.com/) | 在一个平台中捕获所有客户体验数据 | 付费 |
| [Google Analytics](https://analytics.google.com/analytics/web/) | 衡量广告投资回报率，跟踪网站和应用 | 免费 |
| [Heap](https://heapanalytics.com/) | 自动捕获所有交互并回溯分析数据 | 付费 |
| [Hotjar](https://www.hotjar.com/) | 查看访客如何使用网站并收集用户反馈 | 付费 |
| [Inspectlet](https://www.inspectlet.com/) | 录制访客操作视频 | 付费 |
| [LogRocket](https://www.logrocket.com/) | 查看用户在网站上的行为，帮助复现和修复 bug | 付费 |
| [Mixpanel](https://mixpanel.com/) | 跨用户数据获取洞察，做出更明智的决策 | 付费 |
| [Smartlook](https://www.smartlook.com) | 用户会话回放和用户参与度分析 | 付费 |
| [Fathom](https://usefathom.com/) | 不追踪或存储用户个人数据的简单网站统计 | 付费 |

---

## 14. 字体工具

字体管理、发现和使用工具。

| 工具 | 说明 | 免费/开源 |
|------|------|-----------|
| [DaFont](https://www.dafont.com/) | 免费可下载字体存档，支持按风格/作者/人气浏览 | 免费 |
| [Fontbase](https://fontba.se/) | 字体管理工具 | 免费 |
| [FontPair](https://fontpair.co/) | 帮助搭配 Google 字体的简单工具 | 免费 |
| [Font Squirrel](https://www.fontsquirrel.com/) | 免费字体下载，种类丰富 | 免费 |
| [Google Fonts](https://fonts.google.com/) | 通过优质排版让 Web 更美观、快速和开放 | 免费 |
| [LostType](http://losttype.com/) | 首个"按需付费"字体铸造厂 | 付费 |
| [RightFont](https://rightfontapp.com/) | 字体管理应用，支持预览、同步和组织字体 | Mac |
| [Typeface](https://typefaceapp.com/) | 通过实时预览和灵活标签改善设计流程的字体管理器 | Mac |
| [WordMarkIt](https://wordmark.it/) | 用电脑已安装的所有字体显示输入的文字 | 免费 |
| [Fontface Ninja](https://fontface.ninja/) | 浏览器扩展，发现任何网站使用的字体 | 付费 |
| [Google Webfonts Helper](https://google-webfonts-helper.herokuapp.com/) | 自托管 Google Fonts 的辅助工具 | 免费、开源 |

---

## 15. 渐变工具

创建和发现渐变配色方案。

| 工具 | 说明 | 免费/开源 |
|------|------|-----------|
| [Blend](http://www.colinkeany.com/blend/) | 创建和自定义 CSS3 渐变 | 免费 |
| [CSS Gradient](https://cssgradient.io/) | 免费的 CSS 渐变生成器 | 免费 |
| [Grabient](https://www.grabient.com/) | 简洁美观的 Web 渐变生成界面 | 免费 |
| [Gradient Hunt](https://gradienthunt.com/) | 免费开放的渐变灵感平台 | 免费、开源 |
| [UI Gradients](https://uigradients.com/) | 为设计师和开发者精选的美丽渐变合集 | 免费 |
| [Web Gradients](https://webgradients.com/) | 180 个免费线性渐变合集 | 免费 |
| [ColorSpace](https://mycolor.space/) | 为项目生成匹配的配色方案 | 免费 |
| [CoolHue](https://webkul.github.io/coolhue/) | 精选渐变调色板 | 免费 |

---

## 16. 图标工具

图标资源库和管理工具。

| 工具 | 说明 | 免费/开源 |
|------|------|-----------|
| [Feather Icons](https://feathericons.com/) | 基于 24x24 网格设计的简洁图标集 | 免费、开源 |
| [Flaticon](https://www.flaticon.com/) | 159 万+ 矢量图标，支持 SVG/PSD/PNG/EPS 格式 | 付费 |
| [Font Awesome](https://fontawesome.com/) | 最流行的图标集和工具包 | 开源 |
| [Icons8](https://icons8.com/icons) | iOS/Android/Windows 风格的免费图标 | 免费 |
| [Material Design Icons](https://materialdesignicons.com/) | 开源贡献的免费 Material Design 图标 | 免费、开源 |
| [Noun Project](https://thenounproject.com/) | 万物皆有图标 | 付费 |
| [Simple Icons](https://simpleicons.org/) | 流行品牌的免费 SVG 图标 | 免费 |
| [Iconfinder](https://www.iconfinder.com) | 矢量图标市场 | 付费 |
| [Iconmonstr](https://iconmonstr.com/) | 4412+ 免费图标，305 个合集 | 免费 |
| [SVGRepo](https://www.svgrepo.com/) | 30 万+ SVG 矢量和图标 | 免费 |
| [Ionicons](https://ionicons.com/) | 精美的开源图标 | 免费 |
| [Ikonate](https://www.ikonate.com/) | 可自定义的免费矢量图标 | 免费 |

---

## 17. 插画资源

免费和付费的插画素材。

| 工具 | 说明 | 免费/开源 |
|------|------|-----------|
| [Absurd Design](https://absurd.design) | 免费超现实主义插画 | 免费 |
| [Blush](https://blush.design/) | 创建、混合和自定义全球艺术家制作的插画 | 免费 |
| [Humaaans](https://www.humaaans.com/) | 可混合搭配的人物插画库 | 免费 |
| [IRA Design](https://iradesign.io/) | 使用手绘组件和渐变色创建插画 | 免费 |
| [ManyPixels](https://gallery.manypixels.co) | 免版税插画资源 | 免费 |
| [Open Doodles](https://www.opendoodles.com/) | CC0 许可的免费插画集 | 免费 |
| [Ouch](https://icons8.com/ouch) | 提升项目品质的矢量插画 | 免费 |
| [unDraw](https://undraw.co) | 精美的免费 SVG 图片合集 | 免费 |
| [Blobmaker](https://www.blobmaker.app/) | 在浏览器中创建矢量 blob 插画 | 免费 |

---

## 18. 信息架构工具

帮助组织和结构化网站/App 内容的工具。

| 工具 | 说明 | 免费/开源 |
|------|------|-----------|
| [DYNO Mapper](https://dynomapper.com/) | 使用可视化站点地图组织网站项目 | 付费 |
| [Octopus.do](https://octopus.do) | 可视化站点地图构建器，支持实时协作 | 付费 |
| [OmniGraffle](https://www.omnigroup.com/omnigraffle/) | 创建图表和设计的强大应用 | Mac |
| [OptimalSort](https://www.optimalworkshop.com/optimalsort) | 卡片分类工具，帮助理解用户如何分类内容 | 付费 |
| [WriteMaps](https://writemaps.com/) | 创建站点地图，规划页面和内容 | 付费 |

---

## 19. Logo 设计工具

Logo 创建和品牌标识设计工具。

| 工具 | 说明 | 免费/开源 |
|------|------|-----------|
| [Design Evo](https://www.designevo.com/) | 大量矢量图标和形状帮助轻松设计自定义 Logo | 免费 |
| [Free Logo Design](https://www.freelogodesign.org/) | 快速创建专业 Logo | 免费 |
| [Logojoy](https://logojoy.com/) | 使用 AI 即时生成独特的 Logo 创意 | 付费 |
| [Logo Lab](https://logolab.app/home) | 通过自动化视觉实验测试 Logo | 免费 |
| [Logo Maker (Ucraft)](https://www.ucraft.com/free-logo-maker) | 免费 Logo 制作工具 | 免费 |
| [Logo Makr](https://logomakr.com/) | 免费设计 Logo，数百种字体和图标可选 | 免费 |
| [Logo Rank](https://brandmark.io/logo-rank/) | 上传 Logo 查看客观评分 | 免费 |

---

## 20. 样机工具

创建产品样机和设备模型展示。

| 工具 | 说明 | 免费/开源 |
|------|------|-----------|
| [Artboard Studio](https://artboard.studio/) | 专注于产品样机的在线图形设计应用 | 付费 |
| [Devices by Facebook](https://facebook.design/devices) | 流行设备的图片和 Sketch 文件 | 免费 |
| [Mockup World](https://www.mockupworld.co/) | 大量免费、完全分层的逼真 PSD 样机 | 免费 |
| [Moqups](https://moqups.com/) | 实时协作创建线框图、样机、图表和原型 | 付费 |
| [Smartmockups](https://smartmockups.com/) | 几次点击即可创建产品样机 | 付费 |
| [Rotato](https://www.rotato.xyz/) | 为应用设计创建动画 3D 样机 | Mac |
| [Screely](https://www.screely.com/) | 快速将网页设计嵌入极简浏览器窗口 | 免费 |
| [Device Shots](https://deviceshots.com) | 免费创建带设备边框的精美样机 | 免费 |
| [Threed](http://threed.io/) | 在浏览器中生成自定义 3D 设备样机 | 付费 |

---

## 21. 无代码工具

无需编程即可构建网站、应用和自动化流程。

| 工具 | 说明 | 免费/开源 |
|------|------|-----------|
| [Bubble](https://bubble.io/) | 无需编码即可构建和托管 Web 应用 | 付费 |
| [Carrd](https://carrd.co/) | 简单、免费、全响应式单页网站 | 免费 |
| [Coda](https://coda.io) | 融合文档、电子表格和应用功能的新型文档 | 免费 |
| [Retool](https://tryretool.com/) | 提供构建模块，更快速地构建工具 | 付费 |
| [Shopify](https://www.shopify.com/) | 电商和零售功能一体化平台 | 付费 |
| [Thunkable](https://thunkable.com/) | 拖放式原生移动应用构建工具 | 付费 |
| [Remove.bg](https://www.remove.bg/) | 免费去除照片背景 | 免费 |

---

## 22. 像素画工具

创建像素艺术和精灵动画。

| 工具 | 说明 | 免费/开源 |
|------|------|-----------|
| [Aseprite](https://www.aseprite.org/) | 动画精灵编辑器和像素画工具 | 开源 |
| [GraphicsGale](https://graphicsgale.com/us/) | 具有调色板控制等像素画专用功能 | 免费 |
| [Piskel](https://www.piskelapp.com/) | 在线精灵动画和像素画编辑器 | 免费、开源 |
| [Pyxel Edit](https://pyxeledit.com/) | 专注于制作图块集、关卡和动画的像素画编辑器 | 免费、开源 |

---

## 23. 原型工具

创建交互原型以测试设计假设。

| 工具 | 说明 | 免费/开源 |
|------|------|-----------|
| [Axure RP](https://www.axure.com/) | 线框图、原型、协作和规格生成 | 付费 |
| [Figma](https://www.figma.com/) | 基于浏览器的设计工具，支持实时协作和原型 | 付费 |
| [Framer X](https://framer.com/) | 可视化设计逼真交互原型的工具 | Mac |
| [InVision](https://www.invisionapp.com/) | 原型、协作和工作流平台 | 免费 |
| [Flinto](https://www.flinto.com/) | 为应用设计创建交互和动画原型的 Mac 应用 | Mac |
| [Keynote](https://www.apple.com/keynote/) | macOS 内置演示工具，也可用于快速原型 | 免费、Mac |
| [Marvel App](https://marvelapp.com/) | 集线框图、原型、设计和规格于一体的协作设计平台 | 付费 |
| [Origami](https://origami.design/) | 免费的现代 UI 设计工具，支持在 iPhone/iPad 上运行原型 | 免费、Mac |
| [Principle](https://principleformac.com/) | 轻松设计动画和交互式 UI | Mac |
| [ProtoPie](https://www.protopie.io/) | 高保真交互原型，支持传感器辅助 | 付费 |
| [Proto.io](https://proto.io/) | 创建与真实应用完全一致的高保真交互原型 | 付费 |
| [Uizard](https://uizard.io/) | 将线框图转换为高保真交互原型 | 免费 |
| [UXPin](https://www.uxpin.com/) | 使用代码组件、逻辑、状态和设计系统构建逼真原型 | 免费 |

---

## 24. 截图工具

屏幕录制和截图工具。

| 工具 | 说明 | 免费/开源 |
|------|------|-----------|
| [CleanShot](https://getcleanshot.com) | 带标注工具和快速访问覆盖层的截屏工具 | Mac |
| [CloudApp](https://www.getcloudapp.com/) | 录制视频、摄像头，标注截图，创建 GIF | 付费 |
| [Greenshot](https://getgreenshot.org/) | 截取选定区域、窗口或全屏 | 免费 |
| [Kap](https://getkap.co) | 开源录屏工具，支持导出 GIF/MP4/WebM/APNG | 免费、开源、Mac |
| [OBS](https://obsproject.com/) | 视频录制和直播的开源软件 | 免费、开源 |
| [ShareX](https://getsharex.com/) | 屏幕捕获、文件共享和生产力工具 | 免费、开源 |
| [Snagit](https://www.techsmith.com/screen-capture.html) | 捕获图像和视频，创建 GIF，标注和编辑 | 付费 |
| [ScreenToGif](https://www.screentogif.com/) | 录制屏幕部分区域为 GIF | 免费、开源 |
| [Quicktime](https://support.apple.com/quicktime) | macOS 内置的屏幕录制工具 | 免费、Mac |

---

## 25. 草图工具

在线草图和模板工具。

| 工具 | 说明 | 免费/开源 |
|------|------|-----------|
| [Responsive Sketchsheets](https://zurb.com/playground/responsive-sketchsheets) | 自适应预设计模板 | 免费 |
| [Sketchsheets](https://sketchsheets.com/) | 最新设备和平台的免费可打印模板 | 免费、开源 |
| [Sneakpeekit](https://sneakpeekit.com/) | 可打印的笔记网格和设备框架 | 免费 |
| [Sketchize](https://sketchize.com/) | 选择适合项目的草图纸，打印后开始绘制 | 免费 |

---

## 26. 社交媒体设计工具

为社交媒体平台创建营销素材。

| 工具 | 说明 | 免费/开源 |
|------|------|-----------|
| [Canva](https://www.canva.com/) | 为工作和生活创建精美设计 | 付费 |
| [Crello](https://crello.com/) | 创建帖子、封面、图形和海报 | 付费 |
| [Pablo by Buffer](https://pablo.buffer.com/) | 为社交媒体帖子设计引人注目的图片 | 免费 |
| [SocialSizes](https://socialsizes.io/) | 提供社交媒体图片和视频的最佳尺寸参考 | 免费 |
| [Stencil](https://getstencil.com/) | 轻松快速创建社交媒体图片的图形设计工具 | 付费 |

---

## 27. 音效设计

为网站、应用、游戏等产品创建音效。

| 工具 | 说明 | 免费/开源 |
|------|------|-----------|
| [AudioJungle](https://audiojungle.net/) | 83 万+ 曲目和音效 | 付费 |
| [Bensound](https://www.bensound.com/) | 免费知识共享音乐 | 免费 |
| [Freesound](https://freesound.org/) | 知识共享音效的协作数据库 | 免费 |
| [Fugue Music](https://icons8.com/music) | 免费下载视频背景音乐 | 免费 |
| [Sonic Pi](https://sonic-pi.net/) | 实时编码音乐合成器 | 免费、开源 |
| [SoundKit](https://soundkit.io/) | 为界面需求设计的 UI 音效库 | 付费 |
| [YouTube Audio Library](https://www.youtube.com/audiolibrary/music) | 浏览和下载免费项目音乐 | 免费 |

---

## 28. 图片素材

免费和付费的高质量图片资源。

| 工具 | 说明 | 免费/开源 |
|------|------|-----------|
| [Unsplash](https://unsplash.com) | 免费使用的高质量图片 | 免费 |
| [Pexels](https://www.pexels.com/) | 聚合多个免费图片资源 | 免费 |
| [Pixabay](https://pixabay.com/) | 分享图片、插画、矢量图形和视频素材 | 免费 |
| [Burst](https://burst.shopify.com/) | 适用于网站和商业用途的免费图片 | 免费 |
| [FoodiesFeed](https://foodiesfeed.com/) | 数千张精美的免费高清食物图片 | 免费 |
| [Gratisography](https://gratisography.com) | 免费高分辨率图片合集 | 免费 |
| [Kaboom Pics](https://kaboompics.com/) | 包含抽象、城市、时尚、食物等类别的图片 | 免费 |
| [Life of Pix](https://www.lifeofpix.com/) | 免费高分辨率图片 | 免费 |
| [StockSnap.io](https://stocksnap.io/) | 大量免费高分辨率图片 | 免费 |
| [Reshot](https://www.reshot.com/) | 独家精选的免费图片库 | 免费 |
| [UI Faces](https://uifaces.co/) | 聚合各种免费头像源，用于设计样机 | 免费 |

---

## 29. 视频素材

免费和付费的高质量视频素材。

| 工具 | 说明 | 免费/开源 |
|------|------|-----------|
| [Coverr](https://coverr.co/) | 精美的免费视频素材 | 免费 |
| [Mixkit](https://mixkit.co/) | 免费高清视频素材 | 免费 |
| [Pexels Videos](https://www.pexels.com/videos/) | 轻松查找免费视频素材 | 免费 |
| [Pixabay](https://pixabay.com/) | 150 万+ 免版税视频和图片 | 免费 |
| [Videvo](https://www.videvo.net/) | 大量高清视频片段、动态图形和免费素材 | 免费 |
| [Videezy](https://www.videezy.com/) | 下载数百万免费和付费视频素材 | 付费 |

---

## 30. 设计学习资源

学习 UI/UX 设计的课程和平台。

| 工具 | 说明 | 免费/开源 |
|------|------|-----------|
| [Design Better](https://www.designbetter.co/) | 来自顶级设计团队的最佳实践、故事和洞察 | 免费 |
| [Design+Code](https://designcode.io/) | 关于最佳工具和设计系统的完整课程 | 付费 |
| [DesignerUp](https://designerup.co/) | 自学课程和导师指导，掌握产品设计 | 付费 |
| [Figma Training](https://www.figmatraining.com) | Figma 的速成课程 | 付费 |
| [Interaction Design Foundation](https://www.interaction-design.org/) | 学习 UX/UI 技能的行业知名网站 | 付费 |
| [Laws of UX](https://lawsofux.com/) | 设计师在构建 UI 时可参考的法则和原则合集 | 免费 |
| [Learn UX](https://learnux.io/) | 学习 UI 和 UX 工具的完整方法 | 付费 |

---

## 31. UI 设计工具

综合性的 UI/UX 设计工具。

| 工具 | 说明 | 免费/开源 |
|------|------|-----------|
| [Adobe XD](https://www.adobe.com/products/xd.html) | 设计、原型和分享用户体验 | 免费 |
| [Affinity Designer](https://affinity.serif.com/en-gb/designer/) | macOS/iOS/Windows 的矢量图形编辑器 | 付费 |
| [Figma](https://www.figma.com/) | 基于浏览器，支持设计和原型的实时协作工具 | 付费 |
| [GIMP](https://www.gimp.org/) | 免费开源的图像和图形设计软件 | 免费、开源 |
| [Illustrator](https://www.adobe.com/products/illustrator.html) | Adobe 的矢量图形设计工具 | 付费 |
| [Inkscape](https://inkscape.org/) | 免费开源的矢量图形编辑器 | 免费、开源 |
| [Krita](https://krita.org/en/) | 免费绘画和图形设计软件 | 免费、开源 |
| [Lunacy](https://icons8.com/lunacy) | 免费 Windows 原生应用，支持 .sketch 文件 | 免费 |
| [Photopea](https://www.photopea.com/) | 免费的浏览器端图形设计应用（Photoshop 替代品） | 免费 |
| [Photoshop](https://www.adobe.com/products/photoshop.html) | Adobe 图像和图形设计软件 | 付费 |
| [Sketch](https://www.sketchapp.com/) | 专为 Mac 设计的设计工具包 | Mac |
| [InVision Studio](https://www.invisionapp.com/studio) | 集设计、原型和协作于一体 | 付费 |
| [Vectr](https://vectr.com/) | 简单的跨平台矢量图形工具 | 免费 |
| [Gravit](https://designer.io/) | 免费矢量设计应用，支持多平台 | 免费 |

---

## 32. 用户流程工具

规划用户路径和创建流程图。

| 工具 | 说明 | 免费/开源 |
|------|------|-----------|
| [Draw.io](https://www.draw.io/) | 免费在线图表软件，制作流程图、UML 等 | 免费 |
| [Flowmapp](https://flowmapp.com/) | 在线创建站点地图和用户流程 | 付费 |
| [Google Drawings](https://docs.google.com/drawings/) | 在 Google Docs 中免费创建图表 | 免费 |
| [Lucidchart](https://www.lucidchart.com/) | 在线创建图表、流程图、站点地图等 | 付费 |
| [MindNode](https://mindnode.com/) | 让头脑风暴变得简单的思维导图应用 | Mac |
| [Overflow](https://overflow.io/) | 将设计转换为可播放的用户流程图 | 付费 |
| [Whimsical](https://whimsical.co/) | 轻松创建流程图、线框图和便签 | 付费 |
| [XMind: ZEN](https://www.xmind.net/zen/) | 头脑风暴和思维导图工具 | 付费 |
| [yEd](https://www.yworks.com/products/yed) | 免费的桌面图表制作工具，自动布局 | 免费 |

---

## 33. 用户研究工具

理解用户行为、需求和动机的方法与工具。

| 工具 | 说明 | 免费/开源 |
|------|------|-----------|
| [Calendly](https://calendly.com/) | 无需反复邮件沟通即可安排会议 | 付费 |
| [Doodle](https://doodle.com/) | 在线日历工具，用于时间管理和协调会议 | 付费 |
| [JotForm](https://www.jotform.com) | 创建在线表单，收集数据 | 免费 |
| [Lookback](https://lookback.io/) | 远程运行、录制和记录用户研究会话 | 付费 |
| [Survey Monkey](https://www.surveymonkey.com/) | 在线调查工具 | 付费 |
| [Typeform](https://www.typeform.com/) | 拖放式表单、调查和问卷创建工具 | 付费 |
| [User Interviews](https://www.userinterviews.com/) | 从 12.5 万成员社区中招募研究参与者 | 付费 |
| [Zoom](https://zoom.us) | 在线会议服务 | 付费 |

---

## 34. 可视化调试工具

用于前端调试和设计检查。

| 工具 | 说明 | 免费/开源 |
|------|------|-----------|
| [LogRocket](https://logrocket.com/) | 录制用户操作以便复现和修复 bug | 付费 |
| [PixelSnap](https://getpixelsnap.com) | 测量屏幕上任何内容的工具 | Mac |
| [VisBug](https://github.com/GoogleChromeLabs/ProjectVisBug) | 在任何网页上可视化调试、检查样式和无障碍性 | 免费、开源 |
| [Visual Inspector](https://www.canvasflip.com/visual-inspector/) | 网站反馈和设计 bug 修复的协作工具 | 付费 |

---

## 35. 线框图工具

快速勾勒网站/App 的基本结构。

| 工具 | 说明 | 免费/开源 |
|------|------|-----------|
| [Balsamiq Cloud](https://balsamiq.cloud/) | 轻松的 UI 草图工具 | 付费 |
| [BLOKK](http://www.blokkfont.com/) | 用于快速样机和线框图的字体 | 免费 |
| [Gliffy](https://www.gliffy.com/) | 创建框架、UML 图、流程图和线框图 | 付费 |
| [Gridzzly](http://gridzzly.com/) | 最简单的自定义网格纸打印工具 | 免费 |
| [Layoutit](https://grid.layoutit.com/) | CSS Grid 和 Bootstrap 的界面构建器 | 免费 |
| [Wireframe.cc](https://wireframe.cc/) | 简洁的线框图工具 | 免费 |
| [Whimsical Wireframes](https://whimsical.co/wireframes/) | 即时线框图，丰富的可配置元素库 | 付费 |
| [1200px Grid System](https://1200px.com/) | 适用于更宽网站设计的网格系统 | 免费 |

---

## 36. 3D 建模软件

用于游戏、电影、建筑、工程和 3D 打印的 3D 建模工具。

| 工具 | 说明 | 免费/开源 |
|------|------|-----------|
| [Blender](https://www.blender.org/) | 免费开源的 3D 创作软件 | 免费、开源 |
| [FreeCAD](https://www.freecadweb.org/) | 免费开源的多平台 3D 参数化建模器 | 免费、开源 |
| [Maya](https://www.autodesk.com/products/maya/overview) | 动画、环境、动态图形、VR 和角色创建一体化工具 | 付费 |
| [SketchUp](https://www.sketchup.com) | 简单易学的 3D 设计软件 | 付费 |
| [Tinkercad](https://www.tinkercad.com) | 免费易用的 3D 设计、电子和编程应用 | 免费 |
| [Rhino](https://www.rhino3d.com/) | 基于曲线的 3D 建模软件 | 付费 |
| [Vectary](https://www.vectary.com/) | 拖放式 3D 建模工具 | 付费 |
| [Onshape](https://www.onshape.com/) | 专注于技术零件设计的全云端 3D 建模软件 | 付费 |

---

## 要点总结

1. **工具选择原则**：根据项目规模、团队协作需求和预算选择合适工具，不必追求功能最全。
2. **免费资源丰富**：大量高质量工具提供免费版本或开源方案，初学者可零成本入门。
3. **设计系统是趋势**：使用设计系统工具（如 Storybook、Zeroheight）可保持产品一致性和开发效率。
4. **无障碍不可忽视**：在设计阶段就使用无障碍检测工具（如 Axe、WAVE），避免后期返工。
5. **原型验证优于假设**：使用原型工具（如 Figma、ProtoPie）尽早验证设计假设，降低开发成本。
6. **协作优先**：选择支持实时协作的工具（如 Figma、Miro），提升团队沟通效率。


---

## 来源：tool.md

## 简介

设计工具帮助创作者构建数字产品，从初始概念到最终交付。本指南涵盖了数字设计各个类别中最好的工具，帮助你在工作流程的每个阶段找到合适的工具。

## 目录

- [UI/UX 设计](#uiux-设计)
- [原型设计](#原型设计)
- [线框图](#线框图)
- [颜色工具](#颜色工具)
- [字体排版](#字体排版)
- [图标工具](#图标工具)
- [插画](#插画)
- [3D 设计](#3d-设计)
- [动画](#动画)
- [设计交付](#设计交付)
- [无障碍工具](#无障碍工具)
- [AR/VR 设计](#arvr-设计)
- [如何选择合适的工具](#如何选择合适的工具)

---

## UI/UX 设计

UI/UX 设计工具是数字产品创作的基础。它们允许设计师创建界面、构建设计系统，并与团队协作。

### 一体化设计平台

| 工具 | 类型 | 最佳用途 | 核心优势 |
|------|------|----------|----------|
| Figma | Web/桌面 | 团队协作 | 实时多人编辑 |
| Sketch | macOS | UI 设计 | 矢量编辑、插件丰富 |
| Adobe XD | 桌面 | Adobe 生态系统用户 | 与 Creative Cloud 集成 |
| Penpot | Web（开源） | 开源倡导者 | 免费、可自托管 |
| Lunacy | 桌面 | Windows 用户 | 免费、内置素材 |
| InVision Studio | 桌面 | 原型设计 + 设计 | 动画能力强 |

### 各工具使用场景

**Figma** 是大多数团队的行业标准。它在浏览器中运行，支持实时协作，并且有慷慨的免费版。适用场景：

- 你的团队需要实时协作
- 你需要一个跨操作系统的工具
- 你需要庞大的插件生态系统

**Sketch** 适合 macOS 上喜欢原生应用的独立设计师。它自 2010 年推出以来，功能已经非常成熟。

**Penpot** 是领先的开源替代方案。选择它的场景：

- 你的组织需要自托管工具
- 你想避免供应商锁定
- 预算是首要考虑因素

### 设计系统功能

现代 UI 工具通过以下方式支持设计系统：

| 功能 | 描述 | 支持的工具 |
|------|------|-----------|
| 组件 | 可复用的 UI 元素 | Figma、Sketch、XD |
| Tokens | 设计变量（颜色、间距） | Figma、Style Dictionary |
| 自动布局 | 响应式框架行为 | Figma、Sketch |
| 变体 | 组件状态管理 | Figma |
| 库 | 共享组件集合 | Figma、Sketch、XD |

---

## 原型设计

原型设计工具让你创建交互式模型，模拟产品的实际运作方式。从简单的点击模型到高级动画原型，涵盖范围很广。

### 低保真原型

低保真原型侧重于流程和结构，而非视觉细节。

| 工具 | 类型 | 最佳用途 |
|------|------|----------|
| Balsamiq | 桌面/Web | 快速线框原型 |
| Marvel | Web | 简单的点击原型 |
| Overflow | 桌面 | 用户流程图 |

### 高保真原型

高保真原型看起来和行为上都像最终产品。

| 工具 | 类型 | 最佳用途 | 交互级别 |
|------|------|----------|----------|
| Figma（原型功能） | 内置 | 基本交互 | 点击、悬停、拖拽 |
| ProtoPie | 桌面 | 高级交互 | 传感器、变量、条件 |
| Principle | macOS | 动画过渡 | 基于时间轴 |
| Framer | Web | 代码驱动的原型 | React 组件 |
| Axure RP | 桌面 | 复杂逻辑原型 | 条件逻辑、变量 |
| Origami Studio | macOS | Facebook 风格原型 | 基于 Patch 的编程 |

### 选择合适的保真度

| 项目阶段 | 推荐保真度 | 原因 |
|----------|-----------|------|
| 早期探索 | 低 | 快速迭代，聚焦概念 |
| 用户测试 | 中 | 足够的细节以获得真实反馈 |
| 利益相关者演示 | 高 | 视觉精修增强信心 |
| 开发者交付 | 高 | 需要精确的规格说明 |

---

## 线框图

线框图是创建简化布局的过程，专注于结构和内容层级，不包含视觉设计细节。

### 线框图工具

| 工具 | 平台 | 价格 | 核心功能 |
|------|------|------|----------|
| Balsamiq | 桌面/Web | 付费 | 手绘风格 |
| Whimsical | Web | 免费版 | 快速、简洁界面 |
| Wireframe.cc | Web | 免费版 | 超简洁画布 |
| MockFlow | Web | 免费版 | 组件库 |
| Gliffy | Web | 免费版 | 图表 + 线框图 |

### 线框图最佳实践

1. **从内容开始**：在设计布局之前，先确定页面需要什么内容。
2. **使用网格系统**：将元素对齐到一致的网格，保持视觉秩序。
3. **保持简洁**：避免颜色、图片和详细的字体排版。
4. **标注一切**：注释帮助利益相关者理解设计意图。
5. **展示状态**：包括空状态、加载状态和错误状态。

### 常见线框图模式

| 模式 | 描述 | 使用场景 |
|------|------|----------|
| F 型模式 | 内容从左到右、从上到下扫描 | 文本密集的页面 |
| Z 型模式 | 视线呈 Z 形移动 | 落地页、内容较少的页面 |
| 卡片布局 | 内容放在等大的卡片中 | 仪表板、画廊 |
| 单列布局 | 内容垂直堆叠 | 移动端、文章 |

---

## 颜色工具

颜色是设计中最强大的元素之一。这些工具帮助你创建、探索和管理调色板。

### 调色板生成器

| 工具 | 类型 | 核心功能 |
|------|------|----------|
| Coolors | Web | 按空格键生成随机调色板 |
| Adobe Color | Web | 带和谐规则的色轮 |
| Khroma | Web | 基于 AI 的调色板生成 |
| Colormind | Web | 深度学习颜色生成 |
| Paletton | Web | 高级色轮 |
| Color Hunt | Web | 精选调色板集合 |

### 颜色对比度检查器

无障碍设计要求文本和背景颜色之间有足够的对比度。

| 工具 | 标准 | 核心功能 |
|------|------|----------|
| WebAIM Contrast Checker | WCAG 2.1 | 简单的通过/未通过 |
| Colour Contrast Analyzer | WCAG 2.1 | 吸管工具 |
| Stark | 插件 | 集成在设计工具中 |
| Contrast Ratio | WCAG 2.1 | 实时计算 |

### 颜色无障碍指南

| WCAG 级别 | 普通文本 | 大号文本 | 描述 |
|-----------|---------|---------|------|
| AA | 4.5:1 | 3:1 | 最低要求 |
| AAA | 7:1 | 4.5:1 | 增强要求 |

### 颜色模型详解

| 模型 | 使用场景 | 示例 |
|------|----------|------|
| HEX | Web 设计 | #FF5733 |
| RGB | 屏幕显示 | rgb(255, 87, 51) |
| HSL | 直觉编辑 | hsl(14, 100%, 60%) |
| CMYK | 印刷设计 | C0 M80 Y80 K0 |
| LAB | 色彩科学 | L57 a55 b55 |

---

## 字体排版

字体排版工具帮助设计师为项目选择、搭配和管理字体。

### 字体发现与管理

| 工具 | 类型 | 核心功能 |
|------|------|----------|
| Google Fonts | Web | 免费开源字体 |
| Adobe Fonts | Web | 高级字体库 |
| Font Squirrel | Web | 免费商用字体 |
| Fontjoy | Web | AI 字体搭配 |
| Typewolf | Web | 字体灵感与推荐 |
| Fonts in Use | Web | 真实字体排版案例 |

### 字体搭配原则

| 原则 | 描述 | 示例 |
|------|------|------|
| 对比 | 搭配明显不同的字体 | 衬线体 + 无衬线体 |
| 相似 x 高度 | 字母高度相似的字体 | 创造视觉和谐 |
| 同一字族 | 使用同一字体的不同字重 | Roboto Light + Roboto Bold |
| 风格匹配 | 字体应有相似的感觉 | 都专业或都活泼 |

### 字体排版比例

一致的字体比例创造视觉层级：

| 层级 | 大小 (px) | 字重 | 用途 |
|------|-----------|------|------|
| Display | 48-64 | Bold | 主视觉区域 |
| H1 | 32-40 | Bold | 页面标题 |
| H2 | 24-32 | Semi-bold | 区域标题 |
| H3 | 20-24 | Semi-bold | 子区域标题 |
| Body | 16-18 | Regular | 段落文本 |
| Small | 14 | Regular | 说明文字、标签 |
| Micro | 12 | Regular | 法律文本、徽章 |

---

## 图标工具

图标对于在界面中传达操作、状态和导航至关重要。

### 图标库

| 库 | 风格 | 数量 | 许可证 |
|----|------|------|--------|
| Material Icons | 填充、描边 | 2,500+ | Apache 2.0 |
| Feather Icons | 描边 | 280+ | MIT |
| Heroicons | 描边、实心 | 300+ | MIT |
| Phosphor Icons | 多种字重 | 6,000+ | MIT |
| Tabler Icons | 描边 | 4,000+ | MIT |
| Lucide | 描边 | 1,400+ | ISC |
| Ionicons | 描边、填充 | 1,300+ | MIT |

### 图标设计原则

1. **一致的网格**：在相同的网格上设计所有图标（如 24x24px）。
2. **一致的描边粗细**：在所有图标中使用相同的线条粗细。
3. **视觉对齐**：调整形状使其看起来居中，即使数学上不完全居中。
4. **简单形状**：避免不必要的细节；图标通常以小尺寸查看。
5. **清晰的隐喻**：图标应该立即被识别。

### 图标格式对比

| 格式 | 最佳用途 | 可缩放性 | 文件大小 |
|------|----------|----------|----------|
| SVG | Web、应用 | 无限 | 小 |
| 图标字体 | Web | 无限 | 中等（打包） |
| PNG | 旧系统 | 固定 | 中等 |
| PDF | 印刷、iOS | 无限 | 小 |

---

## 插画

插画工具和资源帮助设计师为产品添加个性和视觉叙事。

### 插画库

| 资源 | 风格 | 许可证 | 核心功能 |
|------|------|--------|----------|
| unDraw | 扁平、现代 | 免费 | 可自定义颜色 |
| DrawKit | 多种风格 | 免费/付费 | 多种插画包 |
| Blush | 可定制 | 免费/付费 | 混搭组件 |
| Humaaans | 人物 | 免费 | 可定制的人形 |
| Open Peeps | 手绘 | 免费 | 模块化角色系统 |
| Storyset | 动画 | 免费 | 可定制插画 |

### 插画风格

| 风格 | 描述 | 最佳用途 |
|------|------|----------|
| 扁平 | 简单形状，无阴影 | 现代、简洁的界面 |
| 等距 | 3D 透视，扁平风格 | 技术、建筑类 |
| 手绘 | 草图般的有机线条 | 活泼、亲切的品牌 |
| 3D 渲染 | 逼真的 3D 物体 | 高端、现代产品 |
| 几何 | 抽象形状 | 数据、技术主题 |

---

## 3D 设计

3D 设计工具越来越多地用于 UI 设计、产品可视化和创意项目。

### 3D 设计工具

| 工具 | 平台 | 价格 | 最佳用途 |
|------|------|------|----------|
| Blender | 桌面 | 免费 | 完整的 3D 流程 |
| Spline | Web | 免费版 | Web 设计中的 3D |
| Cinema 4D | 桌面 | 付费 | 动态图形 |
| SketchUp | 桌面/Web | 免费版 | 建筑、快速建模 |
| Three.js | 库 | 免费 | Web 上的 3D |
| Figma (3D) | 插件 | 免费 | 设计文件中的 3D 模型 |

### Web 设计中的 3D

现代 CSS 和 JavaScript 支持 3D 效果：

| 技术 | 使用场景 | 复杂度 |
|------|----------|--------|
| CSS transforms | 卡片翻转、旋转 | 低 |
| CSS 3D transforms | 透视效果 | 中 |
| Three.js | 交互式 3D 场景 | 高 |
| Spline viewer | 嵌入式 3D 模型 | 中 |
| WebGL shaders | 自定义视觉效果 | 高 |

---

## 动画

动画让界面栩栩如生，提供反馈、引导注意力并创造愉悦的体验。

### 动画工具

| 工具 | 平台 | 类型 | 最佳用途 |
|------|------|------|----------|
| After Effects | 桌面 | 动态图形 | 复杂动画 |
| Lottie | 库 | 轻量级 | Web/应用动画 |
| Rive | Web/桌面 | 交互式 | 实时动画 |
| Principle | macOS | UI 过渡 | 应用原型 |
| Motion (Framer Motion) | 库 | 代码 | React 动画 |
| GSAP | 库 | 代码 | Web 动画 |

### UI 动画原则

| 原则 | 描述 | 示例 |
|------|------|------|
| 缓动 | 加速/减速曲线 | 入场使用 ease-in |
| 持续时间 | 动画所需时间 | UI 过渡 200-500ms |
| 延迟 | 组元素的错开时间 | 列表项逐个出现 |
| 反馈 | 用户操作的视觉响应 | 按钮按下效果 |
| 连续性 | 平滑地连接状态 | 页面过渡 |

### 微交互解剖

每个微交互都有四个部分：

1. **触发器**：用户操作或系统事件
2. **规则**：交互过程中发生什么
3. **反馈**：用户如何看到结果
4. **循环/模式**：重复或变化的行为

---

## 设计交付

交付工具弥合了设计与开发之间的差距，提供规格说明、资源和文档。

### 交付工具

| 工具 | 类型 | 核心功能 |
|------|------|----------|
| Figma Inspect | 内置 | CSS、iOS、Android 代码 |
| Zeplin | Web | 详细规格 + 风格指南 |
| Avocode | 桌面 | 图层检查 |
| Storybook | 库 | 组件文档 |
| Supernova | Web | 设计系统文档 |

### 开发者需要的交付物

| 交付物 | 描述 | 格式 |
|--------|------|------|
| 间距 | 边距、内边距、间距 | px/rem 数值 |
| 颜色 | 精确的颜色值 | HEX、RGB、tokens |
| 字体排版 | 字体、大小、字重、行高 | CSS 属性 |
| 资源 | 图标、图片 | SVG、多种尺寸的 PNG |
| 交互 | 动画、过渡 | 持续时间、缓动、触发器 |
| 状态 | 所有组件状态 | 变体或独立屏幕 |

---

## 无障碍工具

无障碍设计确保数字产品可以被所有人使用，包括残障人士。

### 无障碍测试工具

| 工具 | 类型 | 测试内容 |
|------|------|----------|
| axe DevTools | 浏览器扩展 | 自动 WCAG 检查 |
| WAVE | Web | 视觉无障碍反馈 |
| Lighthouse | 浏览器 | 性能 + 无障碍审计 |
| Pa11y | CLI | 自动化测试 |
| Color Oracle | 桌面 | 色盲模拟 |
| NoCoffee | 浏览器扩展 | 视觉障碍模拟 |

### 无障碍清单

| 类别 | 检查项 | 优先级 |
|------|--------|--------|
| 颜色 | 对比度达到 WCAG AA | 高 |
| 键盘 | 所有交互元素可聚焦 | 高 |
| 屏幕阅读器 | 正确的 ARIA 标签 | 高 |
| 文本 | 可放大到 200% 不丢失内容 | 中 |
| 动效 | 尊重减少动效偏好 | 中 |
| 表单 | 错误信息具有描述性 | 高 |
| 媒体 | 视频内容有字幕 | 中 |
| 触摸 | 触摸目标至少 44x44px | 中 |

### 常见无障碍问题

| 问题 | 影响 | 修复方法 |
|------|------|----------|
| 低对比度 | 无法阅读文本 | 提高对比度 |
| 缺少 alt 文本 | 屏幕阅读器跳过图片 | 添加描述性 alt 文本 |
| 无键盘导航 | 无法脱离鼠标使用 | 添加焦点状态、Tab 顺序 |
| 触摸目标太小 | 移动端难以点击 | 增大按钮至 44px+ |
| 自动播放媒体 | 让部分用户困惑 | 提供暂停/停止控制 |

---

## AR/VR 设计

增强现实和虚拟现实设计需要专门的工具和考虑因素。

### AR/VR 设计工具

| 工具 | 平台 | 类型 | 最佳用途 |
|------|------|------|----------|
| Unity | 桌面 | 游戏引擎 | VR 应用 |
| Unreal Engine | 桌面 | 游戏引擎 | 高保真 VR |
| Spark AR | Web | AR 创作 | Instagram/Facebook 滤镜 |
| Lens Studio | 桌面 | AR 创作 | Snapchat 镜头 |
| ShapesXR | VR | 空间设计 | 在 VR 中进行 VR 原型设计 |
| Bezi | Web | 3D/VR 设计 | 协作式 3D 设计 |

### AR/VR 设计原则

| 原则 | 描述 |
|------|------|
| 舒适度 | 避免晕动症；保持稳定的参考点 |
| 比例 | 物体大小应感觉自然 |
| 交互 | 使用直觉手势（抓取、指向、注视） |
| 反馈 | 提供音频和触觉反馈 |
| 性能 | VR 至少保持 90fps |
| 空间音频 | 声音应来自其来源的方向 |

---

## 如何选择合适的工具

### 决策框架

选择设计工具时考虑以下因素：

| 因素 | 需要问的问题 |
|------|-------------|
| 团队规模 | 独立设计师还是大团队？ |
| 预算 | 免费版还是企业定价？ |
| 平台 | Web、macOS、Windows 还是跨平台？ |
| 工作流程 | 线性还是迭代？瀑布式还是敏捷？ |
| 集成 | 你的团队已经在使用什么工具？ |
| 输出 | 开发者需要从你的设计中构建什么？ |

### 推荐工具栈

**创业公司栈（免费/低成本）**

| 角色 | 工具 |
|------|------|
| 设计 | Figma（免费版） |
| 原型设计 | Figma 内置功能 |
| 图标 | Heroicons 或 Lucide |
| 颜色 | Coolors |
| 交付 | Figma inspect |

**企业栈**

| 角色 | 工具 |
|------|------|
| 设计 | Figma（Organization 计划） |
| 原型设计 | ProtoPie |
| 设计系统 | Figma + Supernova |
| 交付 | Zeplin |
| 测试 | UserTesting |

**开源栈**

| 角色 | 工具 |
|------|------|
| 设计 | Penpot |
| 线框图 | Wireframe.cc |
| 图标 | Material Icons |
| 动画 | Lottie + Rive |
| 交付 | Storybook |

---

## 总结

设计工具领域丰富且不断发展。最重要的因素不是你选择哪个工具，而是它如何适应你的工作流程和团队协作需求。从解决你最紧迫问题的工具开始，随着技能和项目的增长扩展你的工具包。

关键要点：

- **Figma** 主导行业是有原因的：协作、跨平台和强大的插件生态系统
- **开源替代方案** 如 Penpot 对于需要自托管或想避免供应商锁定的团队是可行的
- **原型保真度** 应与项目阶段匹配：探索用低保真，验证用高保真
- **无障碍设计** 应从一开始就融入工作流程，而不是事后补充
- **设计系统** 节省时间并确保产品间的一致性


---

## 来源：color.md

## 简介

OpenColorIO (OCIO) 是一个开源色彩管理框架，专为电影、动画和视觉特效工作流设计。它确保在不同应用和制作阶段之间提供一致的色彩处理。

无论你是在 Nuke 中合成、在 Blender 中渲染，还是在 DaVinci Resolve 中调色，OCIO 都能确保颜色显示正确。没有正确的色彩管理，同一张图像在不同工具中可能看起来差异巨大，导致昂贵的返工。

## 为什么色彩管理很重要

在专业的视觉特效管线中，图像会经过多个应用程序。每个工具可能以不同方式解释色彩数据。OCIO 通过集中化色彩变换规则来解决这个问题。

| 问题 | 没有 OCIO | 使用 OCIO |
|------|----------|----------|
| 色彩不一致 | 不同应用间外观不同 | 统一外观 |
| 管线交接 | 手动调整色彩 | 自动变换 |
| 显示准确性 | 靠猜测 | 校准输出 |
| 归档/检索 | 色彩数据可能丢失 | 完整记录的变换 |

## 核心概念

### 色彩空间

色彩空间定义了数值如何映射到实际颜色。OCIO 区分几种类型。

| 色彩空间类型 | 用途 | 示例 |
|------------|------|------|
| 场景参考 | 表示场景中的光线 | ACEScg, Linear sRGB |
| 显示参考 | 表示显示器上的颜色 | sRGB, Rec. 709 |
| 角色 (Role) | 应用的命名引用 | compositing_linear, color_picking |
| 数据 | 非色彩数据（法线、遮罩） | Raw |

### 变换

变换将数据从一个色彩空间转换到另一个。OCIO 支持多种变换类型。

| 变换类型 | 描述 | 使用场景 |
|---------|------|---------|
| MatrixTransform | 3x3 或 4x4 矩阵乘法 | 线性色彩空间转换 |
| ExponentTransform | 幂函数 | Gamma 校正 |
| CDLTransform | Color Decision List | 现场外观管理 |
| LookTransform | 命名创意外观 | 应用节目 LUT |
| FileTransform | 外部 LUT 文件 | 厂商特定 LUT |
| GradingPrimaryTransform | Lift/Gamma/Gain | 调色调整 |

### 角色

角色是色彩空间的命名别名。它们让应用无需知道确切名称即可引用色彩空间。

| 角色名称 | 典型分配 | 用途 |
|---------|---------|------|
| scene_linear | ACEScg 或 Linear | 合成和渲染 |
| compositing_log | ACEScc 或 Log | 对数空间合成 |
| color_picking | sRGB | UI 取色器 |
| texture_paint | sRGB | 纹理绘制 |
| reference | ACES 2065-1 | 归档交换 |

## 安装

### 从源码编译

```bash
git clone https://github.com/AcademySoftwareFoundation/ocio.git
cd ocio
mkdir build && cd build
cmake .. -DCMAKE_INSTALL_PREFIX=/usr/local
make -j$(nproc)
sudo make install
```

### 使用包管理器

| 平台 | 命令 |
|------|------|
| macOS (Homebrew) | `brew install opencolorio` |
| Ubuntu/Debian | `sudo apt install libopencolorio-dev` |
| Windows (vcpkg) | `vcpkg install opencolorio` |
| Python (pip) | `pip install opencolorio` |

## 配置文件

OCIO 使用 YAML 配置文件定义所有色彩空间、变换和角色。

### 基本结构

```yaml
ocio_profile_version: 2

roles:
  scene_linear: acescg
  compositing_log: acescc
  color_picking: srgb_texture

colorspaces:
  - name: acescg
    family: ACES
    description: ACEScg linear color space
    to_reference:
      !<MatrixTransform> {matrix: [1, 0, 0, 0, 0, 1, 0, 0, 0, 0, 1, 0, 0, 0, 0, 1]}

  - name: srgb_texture
    family: sRGB
    description: sRGB texture color space
    to_reference:
      !<FileTransform> {src: srgb_to_linear.spi1d, interpolation: linear}

displays:
  sRGB:
    - !<ViewTransform> {name: ACES, view_transform: aces_output, display_colorspace: srgb_display}
```

### 内置配置

OCIO 附带多个标准配置。

| 配置 | 使用场景 | 包含的色彩空间 |
|------|---------|--------------|
| studio-config | 完整电影管线 | 100+ 空间 |
| cg-config | CG/视觉特效 | ACES, sRGB, Rec.709 |
| nuke-default | Nuke 兼容 | 旧版 Nuke 空间 |
| spi-vfx | SPI 生产 | 工作室特定 |

## Python API

OCIO 提供全面的 Python API 用于程序化色彩管理。

### 列出色彩空间

```python
import PyOpenColorIO as ocio

config = ocio.GetCurrentConfig()

for cs in config.getColorSpaces():
    print(f"Name: {cs.getName()}")
    print(f"Family: {cs.getFamily()}")
    print(f"Description: {cs.getDescription()}")
```

### 应用变换

```python
import PyOpenColorIO as ocio

config = ocio.GetCurrentConfig()

# 从 scene_linear 到 sRGB display 创建处理器
processor = config.getProcessor("scene_linear", "srgb_display")

# 应用到像素值 (R, G, B, A)
cpu = processor.getDefaultCPUProcessor()
pixel = [0.5, 0.3, 0.8, 1.0]
result = cpu.applyRGBA(pixel)
print(f"Input:  {pixel}")
print(f"Output: {result}")
```

### 创建烘焙 LUT

```python
import PyOpenColorIO as ocio

config = ocio.GetCurrentConfig()

# 定义源和目标
src = "acescg"
dst = "srgb_display"

processor = config.getProcessor(src, dst)

# 创建 3D LUT
baker = ocio.Baker()
baker.setConfig(config)
baker.setFormat("cinespace")
baker.setCubeSize(32)
baker.setInputSpace(src)
baker.setTargetSpace(dst)

# 将 LUT 写入文件
with open("aces_to_srgb.cube", "w") as f:
    f.write(baker.bake())
```

## 与视觉特效应用的集成

| 应用 | OCIO 支持 | 集成方式 |
|------|----------|---------|
| Nuke | 完全原生 | 内置 OCIO 节点 |
| Blender | 完全原生 | 色彩管理设置 |
| Houdini | 完全原生 | OCIO VOP 节点 |
| Maya | 部分 | 第三方插件 |
| DaVinci Resolve | 原生 | ACES 和自定义配置 |
| Natron | 完全原生 | OCIOColorSpace 节点 |

## ACES 工作流

学院色彩编码系统 (ACES) 是 OCIO 最常见的用例。

### ACES 管线阶段

| 阶段 | 色彩空间 | 用途 |
|------|---------|------|
| 采集 | 摄像机原生 | 原始传感器数据 |
| 输入变换 | ACES 2065-1 (AP0) | 转换为 ACES 参考 |
| 工作空间 | ACEScg (AP1) | 合成和渲染 |
| 外观 | ACEScc 或 ACEScct | 创意调色 |
| 输出变换 | 显示参考 | 最终显示器输出 |

### 常见 ACES 变换

| 从 | 到 | 变换 |
|----|----|----|
| Camera LogC | ACEScg | 输入设备变换 (IDT) |
| ACEScg | sRGB | 输出变换 (ODT) |
| ACEScg | ACEScc | ACES 转 Log |
| ACES 2065-1 | Rec.2020 | 参考转显示 |

## 命令行工具

OCIO 包含多个命令行实用工具。

| 工具 | 用途 | 示例 |
|------|------|------|
| ociocheck | 验证配置 | `ociocheck config.ocio` |
| ociobakelut | 烘焙 LUT 文件 | `ociobakelut -lut film.look output.cube` |
| ocioperf | 性能测试 | `ocioperf --config config.ocio` |

### 从命令行烘焙 LUT

```bash
# 创建 1D LUT 用于 gamma 校正
ociobakelut --format houdini --shaperspace log --iconfig config.ocio \
  acescg srgb_display output.lut

# 创建 3D LUT
ociobakelut --format cinespace --cubesize 32 \
  acescg srgb_display output_3d.cube
```

## OCIO v2 新特性

版本 2 引入了重大改进。

| 特性 | 描述 | 优势 |
|------|------|------|
| GPU 渲染器 | HLSL/GLSL 着色器生成 | 实时预览 |
| 内置变换 | 按名称引用 | 更小的配置文件 |
| 分级变换 | CDL 和基础调色 | 现场工作流 |
| 动态属性 | 运行时可调值 | 交互式工具 |
| 配置归档 | 自包含包 | 可靠分享 |
| 命名变换 | 面向用户的变换 | 简化 UI |

## 最佳实践

### 配置管理

| 实践 | 建议 |
|------|------|
| 版本控制 | 将配置与项目文件一起存储在 Git 中 |
| 命名规范 | 使用小写加下划线 |
| 角色 | 始终定义常见角色以确保应用兼容性 |
| 显示/视图 | 至少定义 sRGB 和 Rec.709 显示 |
| 文档 | 为所有色彩空间添加描述 |

### 性能优化

| 优化 | 实现方式 |
|------|---------|
| 预烘焙 LUT | 对静态变换使用 ociobakelut |
| 缓存处理器 | 在脚本中重用处理器对象 |
| GPU 着色器 | 为交互式工作启用 GPU 处理 |
| 最小化链深度 | 尽可能简化变换链 |

## 故障排除

| 问题 | 可能原因 | 解决方案 |
|------|---------|---------|
| 配置无法加载 | YAML 语法错误 | 对文件运行 ociocheck |
| 查看器颜色错误 | 显示设置不匹配 | 验证显示/视图分配 |
| 缺少色彩空间 | 配置缺少该空间 | 使用 API 检查可用空间 |
| LUT 色带 | 立方体尺寸太小 | 增加立方体尺寸（32 或 64） |
| 性能问题 | 复杂变换链 | 烘焙中间 LUT |

## 更多资源

| 资源 | URL |
|------|-----|
| 官方文档 | opencolorio.org |
| GitHub 仓库 | github.com/AcademySoftwareFoundation/ocio |
| ACES Central | acescentral.com |
| OCIO 配置仓库 | github.com/AcademySoftwareFoundation/OpenColorIO-Config-ACES |


---

## 来源：product.md

## 简介

产品设计涵盖创建功能性强、美观且以用户为中心的产品的整个过程。本教程介绍设计思维、原型工具、用户研究和现代产品设计工作流程。

## 设计流程概览

| 阶段 | 活动 | 持续时间 |
|------|------|---------|
| 共情（Empathize） | 用户研究、访谈 | 1-2 周 |
| 定义（Define） | 问题陈述、用户画像 | 1 周 |
| 构思（Ideate） | 草图、头脑风暴 | 1-2 周 |
| 原型（Prototype） | 线框图、模型 | 2-4 周 |
| 测试（Test） | 可用性测试、迭代 | 1-2 周 |
| 实施（Implement） | 交接、开发支持 | 持续进行 |
| 迭代（Iterate） | 分析、反馈循环 | 持续进行 |

## 设计思维框架

### 共情阶段

| 方法 | 用途 | 产出 |
|------|------|------|
| 用户访谈 | 了解需求 | 访谈记录 |
| 问卷调查 | 量化偏好 | 统计数据 |
| 情境调查 | 在环境中观察 | 行为笔记 |
| 日记研究 | 长期跟踪 | 使用模式 |
| 卡片分类 | 了解心智模型 | 信息架构 |

### 定义阶段

| 产出物 | 描述 |
|--------|------|
| 用户画像 | 虚构的代表性用户 |
| 共情地图 | 用户所说的、所想的、所做的、所感受的 |
| 旅程地图 | 端到端体验时间线 |
| 问题陈述 | 对挑战的清晰定义 |
| 待完成工作 | 用户试图完成的任务 |

### 构思阶段

| 技术 | 时间 | 小组规模 |
|------|------|---------|
| 头脑风暴 | 30-60 分钟 | 4-8 人 |
| Crazy 8s | 8 分钟 | 个人 |
| How Might We | 30 分钟 | 4-6 人 |
| 故事板 | 45 分钟 | 2-4 人 |
| 思维导图 | 30 分钟 | 个人或小组 |
| SCAMPER | 45 分钟 | 3-6 人 |

## 原型工具

### 数字设计工具

| 工具 | 平台 | 价格 | 最佳用途 |
|------|------|------|---------|
| Figma | Web、桌面 | 免费/付费 | 协作设计 |
| Sketch | macOS | 付费 | UI 设计 |
| Adobe XD | Windows、macOS | 付费 | Adobe 生态系统 |
| Penpot | Web | 免费 | 开源替代方案 |
| InVision | Web | 付费 | 原型设计 |
| Framer | Web | 付费 | 交互式原型 |

### 线框图工具

| 工具 | 保真度 | 速度 |
|------|--------|------|
| Balsamiq | 低 | 快 |
| Whimsical | 低-中 | 快 |
| FigJam | 低 | 快 |
| Excalidraw | 低 | 快 |
| Miro | 低-中 | 中等 |

### 原型保真度

| 保真度 | 用例 | 工具 |
|--------|------|------|
| 纸质 | 早期概念 | 纸、马克笔 |
| 低保真线框图 | 结构验证 | Balsamiq、Whimsical |
| 中保真模型 | 布局确认 | Figma、Sketch |
| 高保真原型 | 用户测试 | Figma、Framer |
| 代码原型 | 交互测试 | HTML/CSS、React |

## 用户研究方法

| 方法 | 时机 | 参与者 | 持续时间 |
|------|------|--------|---------|
| 用户访谈 | 发现阶段 | 5-10 人 | 各 30-60 分钟 |
| 可用性测试 | 验证阶段 | 5-8 人 | 各 45-60 分钟 |
| A/B 测试 | 优化阶段 | 100+ 人 | 1-4 周 |
| 问卷调查 | 量化阶段 | 100+ 人 | 1-2 周 |
| 热力图分析 | 使用模式 | 1000+ 人 | 2-4 周 |
| 树测试 | IA 验证 | 50+ 人 | 1 周 |
| 卡片分类 | IA 创建 | 15-30 人 | 各 30 分钟 |

### 可用性测试脚本

| 步骤 | 持续时间 | 内容 |
|------|---------|------|
| 开场 | 5 分钟 | 说明目的，获取同意 |
| 热身 | 5 分钟 | 背景问题 |
| 任务 | 30 分钟 | 5-7 个具体任务 |
| 跟进 | 10 分钟 | 开放性问题 |
| 收尾 | 5 分钟 | 感谢参与者 |

## UI 设计原则

### 视觉层级

| 原则 | 应用 |
|------|------|
| 大小 | 较大的元素首先吸引注意力 |
| 颜色 | 高对比度突出显示 |
| 位置 | 左上方首先获得注意力（LTR） |
| 间距 | 空白空间隔离重要元素 |
| 排版 | 粗细和样式创建强调 |

### 排版层级

| 级别 | 大小 | 粗细 | 用途 |
|------|------|------|------|
| Display | 32-48px | Bold | 首屏区域 |
| H1 | 28-36px | Bold | 页面标题 |
| H2 | 24-28px | Semibold | 区域标题 |
| H3 | 20-24px | Semibold | 子区域 |
| Body | 16px | Regular | 正文 |
| Small | 14px | Regular | 说明文字 |
| Tiny | 12px | Regular | 标签、元数据 |

### 颜色系统

| 角色 | 用途 | 示例 |
|------|------|------|
| Primary（主色） | 品牌标识、CTA | Blue (#3B82F6) |
| Secondary（辅色） | 辅助操作 | Gray (#6B7280) |
| Success（成功） | 正面反馈 | Green (#10B981) |
| Warning（警告） | 警示状态 | Yellow (#F59E0B) |
| Error（错误） | 错误状态 | Red (#EF4444) |
| Neutral（中性） | 文本、边框、背景 | 灰度 |

### 间距系统

| Token | 值 | 用途 |
|-------|-----|------|
| xs | 4px | 紧凑间距 |
| sm | 8px | 组件内边距 |
| md | 16px | 标准间距 |
| lg | 24px | 区域间距 |
| xl | 32px | 大间距 |
| 2xl | 48px | 页面区域 |

## 设计系统

### 组件

| 组件 | 用途 |
|------|------|
| Button（按钮） | 触发操作 |
| Input（输入框） | 数据输入 |
| Select（选择框） | 从选项中选择 |
| Modal（模态框） | 聚焦对话框 |
| Toast（通知） | 通知提示 |
| Card（卡片） | 内容容器 |
| Table（表格） | 数据展示 |
| Navigation（导航） | 导航指引 |
| Avatar（头像） | 用户标识 |
| Badge（徽章） | 状态指示器 |

### 文档结构

| 部分 | 内容 |
|------|------|
| Foundations（基础） | 颜色、排版、间距、图标 |
| Components（组件） | 单个组件规格 |
| Patterns（模式） | 常见 UI 模式 |
| Accessibility（无障碍） | WCAG 合规指南 |
| Content（内容） | 写作风格指南 |
| Resources（资源） | 下载、链接 |

## 无障碍

### WCAG 2.1 级别

| 级别 | 要求 | 目标 |
|------|------|------|
| A | 最低无障碍 | 法律最低要求 |
| AA | 标准无障碍 | 大多数产品 |
| AAA | 增强无障碍 | 政府、医疗 |

### 关键无障碍实践

| 实践 | 要求 |
|------|------|
| 颜色对比 | 文本 4.5:1，大文本 3:1 |
| 键盘导航 | 所有交互元素可聚焦 |
| 屏幕阅读器 | 语义化 HTML、ARIA 标签 |
| Alt 文本 | 图片的描述性文本 |
| 焦点指示器 | 可见的焦点状态 |
| 表单标签 | 显式的标签-输入关联 |
| 错误消息 | 清晰，与字段关联 |

## 交接给开发

| 交付物 | 格式 | 内容 |
|--------|------|------|
| 设计规格 | Figma inspect | 尺寸、颜色、间距 |
| 资源导出 | SVG、PNG | 图标、插图 |
| 原型链接 | Figma URL | 交互式演示 |
| 标注图 | 截图 | 标注的测量值 |
| 组件规格 | 文档 | 状态、行为、边界情况 |
| 动效规格 | 视频/JSON | 动画时间和曲线 |

## 分析与迭代

| 指标 | 工具 | 用途 |
|------|------|------|
| 转化率 | Mixpanel、Amplitude | 跟踪目标完成 |
| 跳出率 | Google Analytics | 页面参与度 |
| 任务成功率 | 可用性测试 | 任务完成率 |
| 任务时间 | 分析 | 效率测量 |
| NPS | 问卷调查 | 用户满意度 |
| 错误率 | 分析 | 问题识别 |

## 总结

产品设计是一个将共情、创造力和验证相结合的结构化流程。成功取决于通过研究了解用户、通过原型迭代、通过测试验证。维护良好的设计系统确保产品间的一致性，而无障碍实践确保包容性体验。


---

## 来源：tools.md

## 简介

本教程涵盖了 goabstract/Awesome-Design-Tools 仓库中精选的设计工具集合。它按类别组织了最佳设计软件，帮助设计师为工作流选择合适的工具。

## 工具选择指南

| 需求 | 首选工具 | 替代方案 |
|------|---------|---------|
| UI 设计 | Figma | Sketch, Adobe XD |
| 照片编辑 | Adobe Photoshop | GIMP, Affinity Photo |
| 矢量图形 | Adobe Illustrator | Inkscape, Affinity Designer |
| 原型设计 | Figma | InVision, Marvel |
| 动画 | After Effects | Principle, Lottie |
| 3D 设计 | Blender | Cinema 4D, Maya |
| 配色 | Coolors | Adobe Color |
| 字体 | Google Fonts | Font Squirrel |

## UI 设计工具

### 对比

| 工具 | 平台 | 价格 | 协作 | 离线 |
|------|------|------|------|------|
| Figma | Web, 桌面 | 免费 / $12/月 | 实时 | 有限 |
| Sketch | macOS | $12/月 | 通过插件 | 是 |
| Adobe XD | Win, Mac | 包含在 CC 中 | 实时 | 是 |
| Penpot | Web, 桌面 | 免费 | 实时 | 是 |
| Lunacy | Win, Mac, Web | 免费 | 实时 | 是 |

### Figma 核心功能

| 功能 | 说明 |
|------|------|
| Components（组件） | 可复用的设计元素 |
| Auto Layout（自动布局） | 响应式框架布局 |
| Variants（变体） | 组件状态管理 |
| Dev Mode（开发者模式） | 开发者交接工具 |
| Variables（变量） | 设计令牌 |
| Prototyping（原型） | 交互式原型 |
| Plugins（插件） | 丰富的插件生态 |

### Sketch 核心功能

| 功能 | 说明 |
|------|------|
| Symbols（符号） | 可复用组件 |
| Libraries（库） | 共享设计系统 |
| Artboards（画板） | 页面布局 |
| Plugins（插件） | 大型插件生态 |
| Cloud | Sketch Cloud 分享 |

## 原型设计工具

| 工具 | 类型 | 保真度 | 价格 |
|------|------|--------|------|
| Figma | 内置 | 高 | 免费 / 付费 |
| InVision | 云端 | 高 | 免费 / 付费 |
| Marvel | 云端 | 中 | 免费 / 付费 |
| ProtoPie | 桌面 | 高 | $11/月 |
| Principle | macOS | 高 | $129 一次性 |
| Framer | Web | 高 | 免费 / 付费 |
| Origami | macOS | 高 | 免费 |

### 原型设计对比

| 能力 | Figma | InVision | ProtoPie | Framer |
|------|-------|----------|----------|--------|
| 点击触发 | 是 | 是 | 是 | 是 |
| 悬停状态 | 是 | 否 | 是 | 是 |
| 拖拽手势 | 是 | 有限 | 是 | 是 |
| 变量 | 是 | 否 | 是 | 是 |
| 条件逻辑 | 有限 | 否 | 是 | 是 |
| 设备传感器 | 否 | 否 | 是 | 否 |
| 代码导出 | CSS | 否 | 否 | React |

## 平面设计工具

### 矢量图形

| 工具 | 平台 | 价格 | 最佳场景 |
|------|------|------|---------|
| Adobe Illustrator | Win, Mac | $22.99/月 | 专业插画 |
| Affinity Designer | Win, Mac, iPad | $69.99 一次性 | Illustrator 替代 |
| Inkscape | 跨平台 | 免费 | 开源矢量 |
| Sketch | macOS | $12/月 | UI 矢量 |
| Vectornator | Mac, iPad | 免费 | iPad 插画 |

### 位图图形

| 工具 | 平台 | 价格 | 最佳场景 |
|------|------|------|---------|
| Adobe Photoshop | Win, Mac | $22.99/月 | 照片编辑 |
| Affinity Photo | Win, Mac, iPad | $69.99 一次性 | 照片编辑替代 |
| GIMP | 跨平台 | 免费 | 开源编辑 |
| Pixelmator Pro | macOS | $49.99 一次性 | Mac 照片编辑 |
| Photopea | Web | 免费 | 浏览器编辑 |

## 配色工具

### 调色板生成器

| 工具 | 功能 | 价格 |
|------|------|------|
| Coolors | 调色板生成、导出 | 免费 / $3/月 |
| Adobe Color | 色轮、配色方案 | 免费 |
| Color Hunt | 精选调色板 | 免费 |
| Paletton | 高级色轮 | 免费 |
| Khroma | AI 调色板生成 | 免费 |

### 色彩无障碍

| 工具 | 用途 |
|------|------|
| WebAIM Contrast Checker | WCAG 对比度比值 |
| Stark | 色盲模拟 |
| Color Oracle | 色盲模拟器 |
| Who Can Use | 按人群的色彩可见性 |

### 色彩格式参考

| 格式 | 示例 | 用途 |
|------|------|------|
| HEX | #FF5733 | Web 设计 |
| RGB | rgb(255, 87, 51) | 屏幕显示 |
| HSL | hsl(14, 100%, 60%) | 调整颜色 |
| CMYK | cmyk(0, 66, 80, 0) | 印刷设计 |
| LAB | lab(62, 55, 50) | 色彩科学 |

## 字体工具

### 字体来源

| 来源 | 价格 | 许可证 |
|------|------|--------|
| Google Fonts | 免费 | 开源 |
| Font Squirrel | 免费 | 各种 |
| Adobe Fonts | CC 订阅 | 桌面和 Web |
| DaFont | 免费/付费 | 各种 |
| MyFonts | 付费 | 商业 |

### 字体工具

| 工具 | 用途 | 价格 |
|------|------|------|
| Fontjoy | 字体搭配建议 | 免费 |
| Typewolf | 字体灵感 | 免费 |
| Type Scale | 字号比例计算器 | 免费 |
| Wordmark.it | 字体预览 | 免费 |
| Font Playground | 可变字体测试 | 免费 |

### 字体搭配指南

| 主字体 | 副字体 | 风格 |
|--------|--------|------|
| 衬线标题 | 无衬线正文 | 经典 |
| 无衬线标题 | 衬线正文 | 现代 |
| 粗无衬线 | 细无衬线 | 极简 |
| 展示标题 | 中性正文 | 创意 |

## 图标库

| 图标库 | 图标数量 | 风格 | 价格 |
|--------|---------|------|------|
| Material Icons | 2,500+ | Material Design | 免费 |
| Font Awesome | 2,000+ | 各种 | 免费 / Pro |
| Feather Icons | 280+ | 极简线条 | 免费 |
| Lucide | 1,000+ | Feather 分支 | 免费 |
| Heroicons | 300+ | Tailwind 风格 | 免费 |
| Phosphor | 7,000+ | 灵活 | 免费 |
| Tabler Icons | 4,000+ | 轮廓 | 免费 |

## 免费素材资源

### 免费照片

| 来源 | 许可证 | 质量 |
|------|--------|------|
| Unsplash | 免费商用 | 高 |
| Pexels | 免费商用 | 高 |
| Pixabay | 免费商用 | 中高 |
| Burst | 免费商用 | 高 |
| Stocksnap | CC0 | 中高 |

### 免费插画

| 来源 | 风格 | 格式 |
|------|------|------|
| unDraw | 扁平插画 | SVG |
| Humaaans | 可自定义人物 | SVG, Sketch |
| Open Peeps | 手绘人物 | PNG, Sketch |
| Storyset | 动画插画 | SVG, GIF |
| DrawKit | 各种风格 | SVG, PNG |

### 免费 Mockup

| 来源 | 类型 | 格式 |
|------|------|------|
| Mockup World | 设备 mockup | PSD |
| Placeit | 在线生成器 | PNG |
| Smartmockups | 在线工具 | PNG |
| Mockup Photos | 摄影 mockup | PSD |

## 设计系统工具

| 工具 | 用途 | 价格 |
|------|------|------|
| Storybook | 组件文档 | 免费 |
| Zeroheight | 设计系统文档 | 免费 / 付费 |
| Supernova | 设计系统平台 | 免费 / 付费 |
| Specify | 设计令牌 | 免费 / 付费 |
| Style Dictionary | 令牌转换 | 免费 |

## 协作工具

| 工具 | 用途 | 价格 |
|------|------|------|
| Figma | 设计协作 | 免费 / 付费 |
| Zeplin | 开发者交接 | 免费 / 付费 |
| Abstract | 设计版本控制 | 付费 |
| Maze | 用户测试 | 免费 / 付费 |
| UserTesting | 用户研究 | 付费 |
| Lookback | 用户访谈 | 付费 |

## 动画工具

| 工具 | 类型 | 价格 | 最佳场景 |
|------|------|------|---------|
| After Effects | 运动图形 | $22.99/月 | 复杂动画 |
| Principle | 交互设计 | $129 | UI 过渡 |
| Lottie | Web 动画 | 免费 | 轻量动画 |
| Rive | 交互式动画 | 免费 / 付费 | 实时动画 |
| Figma Smart Animate | 内置 | 免费 | 简单过渡 |

## 3D 设计工具

| 工具 | 价格 | 技能级别 | 最佳场景 |
|------|------|---------|---------|
| Blender | 免费 | 高级 | 3D 建模、动画 |
| Cinema 4D | $719/年 | 中级 | 运动图形 |
| SketchUp | 免费 / 付费 | 初级 | 3D 建模 |
| Spline | 免费 / 付费 | 初级 | 3D Web 设计 |
| Three.js | 免费 | 高级 | 3D Web 体验 |

## 设计工作流技巧

| 阶段 | 工具 | 交付物 |
|------|------|--------|
| 研究 | Maze, UserTesting | 用户洞察 |
| 线框图 | Figma, Sketch | 低保真布局 |
| 设计 | Figma, Sketch | 高保真 mockup |
| 原型 | Figma, ProtoPie | 交互式原型 |
| 交接 | Zeplin, Dev Mode | 规格和资源 |
| 测试 | Maze, Lookback | 可用性反馈 |

## 总结

设计工具领域为设计流程的每个阶段都提供了解决方案。选择合适的工具组合取决于团队规模、预算、平台需求和工作流偏好。免费工具如 Figma、GIMP 和 Inkscape 为许多用例提供了可替代商业软件的方案。


---
