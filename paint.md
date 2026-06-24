# Krita：专业数字绘画

## 简介

Krita 是一款免费、开源的数字绘画应用程序，专为概念艺术、纹理绘制、插画和漫画设计。它为各级技能水平的艺术家提供专业级工具集。

| 属性 | 详情 |
|----------|--------|
| 仓库 | KDE/krita |
| 许可证 | GPL-3.0 |
| 语言 | C++, Python |
| 平台 | Windows, macOS, Linux |
| 文件格式 | .kra（原生）, PSD, PNG, JPEG, TIFF, OpenEXR |

## 安装

### Linux

```bash
# Ubuntu/Debian
sudo apt install krita

# Fedora
sudo dnf install krita

# Flatpak
flatpak install org.kde.krita
```

### macOS 和 Windows

从 Krita 官方网站或 Steam 下载。

## 界面概览

| 区域 | 描述 |
|------|-------------|
| Canvas（画布） | 中央绘图区域 |
| Toolbox（工具箱） | 工具选择面板（左侧） |
| Tool Options（工具选项） | 活动工具的设置 |
| Brush Presets（画笔预设） | 快速访问画笔库 |
| Layers Panel（图层面板） | 图层管理（右侧） |
| Color Selector（颜色选择器） | 取色工具 |
| Docker Panels（停靠面板） | 可配置的实用面板 |

## 基本工具

| 工具 | 快捷键 | 用途 |
|------|----------|---------|
| Freehand Brush（手绘画笔） | B | 主要绘画工具 |
| Line Tool（线条工具） | L | 绘制直线 |
| Rectangle（矩形） | R | 绘制矩形 |
| Ellipse（椭圆） | E | 绘制椭圆 |
| Fill Tool（填充工具） | F | 填充区域 |
| Gradient（渐变） | G | 创建渐变 |
| Transform（变换） | Ctrl+T | 缩放、旋转、倾斜 |
| Crop（裁剪） | C | 裁剪画布 |
| Selection（选区） | S | 选择区域 |
| Move（移动） | M | 移动图层或选区 |
| Text（文本） | T | 添加文本 |

## 画笔

### 画笔引擎

Krita 支持多种画笔引擎，每种提供不同的功能。

| 引擎 | 描述 |
|--------|-------------|
| Pixel Brush（像素画笔） | 标准绘画画笔 |
| Color Smudge（颜色涂抹） | 绘画时混合颜色 |
| Shape Brush（形状画笔） | 使用矢量形状绘画 |
| Sketch Brush（素描画笔） | 铅笔式素描 |
| Spray Brush（喷雾画笔） | 散射粒子 |
| Hatching（影线） | 交叉影线笔触 |
| Chalk（粉笔） | 纹理粉笔效果 |
| Filter Brush（滤镜画笔） | 将滤镜作为绘画应用 |

### 画笔设置

| 设置 | 描述 |
|---------|-------------|
| Size（大小） | 画笔直径（像素） |
| Opacity（不透明度） | 笔触的透明度 |
| Flow（流量） | 每次点触的颜料量 |
| Spacing（间距） | 点触之间的距离 |
| Hardness（硬度） | 边缘柔和度 |
| Rotation（旋转） | 画笔笔尖角度 |
| Scatter（散布） | 随机化点触位置 |

### 画笔预设

Krita 包含数百个按类别组织的预配置画笔预设。

| 类别 | 示例 |
|----------|----------|
| Ink（墨水） | 钢笔、马克笔、书法 |
| Paint（颜料） | 油画、丙烯、水彩 |
| Sketch（素描） | 铅笔、炭笔、蜡笔 |
| Smudge（涂抹） | 混合器、搅拌器 |
| Effects（效果） | 粒子、纹理、图案 |

## 图层

### 图层类型

| 类型 | 描述 |
|------|-------------|
| Paint Layer（绘画图层） | 标准光栅图层 |
| Vector Layer（矢量图层） | 包含矢量形状 |
| Group Layer（组图层） | 其他图层的容器 |
| Clone Layer（克隆图层） | 另一图层的链接副本 |
| Filter Layer（滤镜图层） | 非破坏性滤镜效果 |
| Fill Layer（填充图层） | 纯色或图案填充 |
| File Layer（文件图层） | 引用外部文件 |

### 图层操作

| 操作 | 描述 |
|-----------|-------------|
| Add（添加） | 创建新图层 |
| Duplicate（复制） | 复制当前图层 |
| Merge Down（向下合并） | 与下方图层合并 |
| Flatten（展平） | 合并所有可见图层 |
| Lock（锁定） | 防止编辑 |
| Opacity（不透明度） | 调整图层透明度 |
| Blending Mode（混合模式） | 图层与下方图层的合成方式 |

### 混合模式

| 模式 | 描述 |
|------|-------------|
| Normal（正常） | 标准绘画 |
| Multiply（正片叠底） | 通过相乘颜色变暗 |
| Screen（滤色） | 通过反转和相乘变亮 |
| Overlay（叠加） | 结合正片叠底和滤色 |
| Soft Light（柔光） | 轻柔变亮或变暗 |
| Hard Light（强光） | 强烈变亮或变暗 |
| Color Dodge（颜色减淡） | 基于混合颜色提亮 |
| Color Burn（颜色加深） | 基于混合颜色加深 |
| Darken（变暗） | 保留两种颜色中较暗的 |
| Lighten（变亮） | 保留两种颜色中较亮的 |

## 选区

| 选区模式 | 描述 |
|----------------|-------------|
| Replace（替换） | 替换当前选区 |
| Add（添加） | 添加到当前选区 |
| Subtract（减去） | 从当前选区中移除 |
| Intersect（相交） | 仅保留重叠区域 |

### 选区工具

| 工具 | 描述 |
|------|-------------|
| Rectangular（矩形） | 选择矩形区域 |
| Elliptical（椭圆） | 选择椭圆区域 |
| Polygonal（多边形） | 用直线边缘选择 |
| Freehand（手绘） | 用手绘方式选择 |
| Contiguous（连续） | 按颜色相似性选择 |
| Similar（相似） | 选择所有匹配的颜色 |
| Bezier（贝塞尔） | 用贝塞尔曲线选择 |

## 变换工具

| 变换模式 | 描述 |
|----------------|-------------|
| Scale（缩放） | 调整选区或图层大小 |
| Rotate（旋转） | 围绕中心旋转 |
| Shear（剪切） | 倾斜选区 |
| Perspective（透视） | 应用透视变形 |
| Warp（弯曲） | 自由变形 |
| Cage（笼形） | 基于网格的变形 |
| Liquify（液化） | 推拉像素 |

## 颜色管理

| 功能 | 描述 |
|---------|-------------|
| Color Selector（颜色选择器） | 可视化选取颜色 |
| Color Sliders（颜色滑块） | 按通道调整（RGB, HSV, CMYK） |
| Color History（颜色历史） | 最近使用的颜色 |
| Palette（调色板） | 保存的颜色集 |
| Color Space（色彩空间） | 在 RGB、CMYK 或 Lab 中工作 |
| HDR Painting（HDR 绘画） | 高动态范围支持 |

## 辅助线

Krita 提供绘图辅助线，帮助处理透视、对称和其他几何约束。

| 辅助线 | 描述 |
|-----------|-------------|
| Parallel（平行） | 线条汇聚到消失点 |
| Concentric（同心） | 圆共享共同中心 |
| Vanishing Point（消失点） | 两点透视 |
| Fish Eye（鱼眼） | 弯曲透视 |
| Spline（样条） | 通过点的平滑曲线 |
| Ellipse（椭圆） | 完美的椭圆 |
| Mirror（镜像） | 跨轴对称 |

## 动画

Krita 包含逐帧动画支持。

| 功能 | 描述 |
|---------|-------------|
| Timeline（时间轴） | 帧管理的可视化时间轴 |
| Onion Skinning（洋葱皮） | 查看前后帧 |
| Playback（播放） | 实时预览动画 |
| Export（导出） | 导出为 GIF、MP4 或图像序列 |

## 滤镜

| 滤镜 | 描述 |
|--------|-------------|
| Blur（模糊） | 高斯、运动、镜头模糊 |
| Sharpen（锐化） | 增加边缘对比度 |
| Adjust Levels（调整色阶） | 修改色调范围 |
| Adjust Curves（调整曲线） | 精细色调控制 |
| HSV Adjustment（HSV 调整） | 修改色相、饱和度、明度 |
| Color Balance（色彩平衡） | 调整颜色通道 |
| Emboss（浮雕） | 创建浮雕效果 |
| Pixelize（像素化） | 创建马赛克效果 |

## 数字绘画技巧

| 技巧 | 说明 |
|-----|-------------|
| 使用图层 | 分离元素以便编辑 |
| 设置辅助线 | 使用透视辅助线提高准确性 |
| 保存画笔预设 | 保持自定义画笔有序 |
| 使用颜色管理 | 在正确的色彩空间中工作 |
| 使用参考图片 | 将参考图作为文件图层导入 |
| 学习快捷键 | 加快工作流程 |

## 结论

Krita 是一款功能丰富的数字绘画应用程序，可与商业替代品媲美。其广泛的画笔引擎、图层系统和动画支持使其适用于各种艺术工作流程。
