# 3D 打印与硬件制造

> 本文档整合了以下源文件：cad.md, cad2.md, model.md, slicer.md, prusa.md, orca.md, firmware.md, printer.md, pcb.md, kicad.md, cnc.md, machine.md

---

## 来源：cad.md

## 简介

FreeCAD 是一款通用参数化 3D CAD 建模器，主要用于设计任意尺寸的真实物体。它开源、高度可定制，可在 Windows、macOS 和 Linux 上运行。

| 属性 | 详情 |
|----------|--------|
| 仓库 | FreeCAD/FreeCAD |
| 许可证 | LGPL-2.1 |
| 语言 | Python, C++ |
| 平台 | Windows, macOS, Linux |
| 文件格式 | FCStd（原生）, STEP, IGES, STL |

## 安装

### Linux

```bash
# Ubuntu/Debian
sudo apt install freecad

# Fedora
sudo dnf install freecad

# Snap
sudo snap install freecad
```

### macOS

```bash
brew install freecad
```

### Windows

从 GitHub 上的官方 FreeCAD 发布页面下载安装程序。

## 核心概念

### 参数化建模

参数化建模是指物体的形状由参数（如数值或约束）控制。更改参数会自动更新模型。

| 概念 | 描述 |
|---------|-------------|
| Parameter（参数） | 驱动几何形状的数值或尺寸值 |
| Constraint（约束） | 限制或定义关系的规则 |
| Sketch（草图） | 用于创建 3D 特征的 2D 轮廓 |
| Feature（特征） | 模型历史中的单个操作 |
| Body（主体） | 单个连续 3D 实体 |

### 工作台

FreeCAD 使用工作台按任务组织工具。用户根据要执行的操作在工作台之间切换。

| 工作台 | 用途 |
|-----------|---------|
| Part Design | 使用草图和特征创建复杂零件 |
| Part | 构造实体几何操作 |
| Sketcher | 绘制和约束 2D 草图 |
| Arch | 建筑设计和 BIM |
| Mesh | 基于网格的建模，用于 STL 文件 |
| Draft | 2D 绘图和标注 |
| TechDraw | 技术制图和尺寸标注 |
| FEM | 有限元分析 |

## Part Design 工作流程

### 第 1 步：创建新主体

导航到 Part Design 工作台并创建一个新的 Body。Body 容器包含构成单个实体的所有特征。

### 第 2 步：创建草图

1. 选择一个平面（XY、XZ 或 YZ）。
2. 进入 Sketcher 模式。
3. 使用直线、圆弧、圆和矩形绘制几何图形。
4. 应用尺寸和几何约束。

### 第 3 步：应用特征

| 特征 | 描述 |
|---------|-------------|
| Pad（拉伸） | 将草图拉伸为 3D 实体 |
| Pocket（口袋） | 通过向内拉伸草图来去除材料 |
| Revolve（旋转） | 围绕轴旋转草图创建实体 |
| Fillet（圆角） | 以指定半径对边进行圆角处理 |
| Chamfer（倒角） | 以指定角度和距离对边进行倒角 |
| Mirror（镜像） | 跨平面反射特征 |
| Pattern（阵列） | 创建特征的线性或极坐标阵列 |

### 第 4 步：导出模型

以所需格式导出最终模型，用于制造或共享。

| 格式 | 用途 |
|--------|----------|
| STEP | 与其他 CAD 软件交换 |
| STL | 3D 打印 |
| IGES | 旧版 CAD 交换 |
| OBJ | 渲染和可视化 |

## 使用 Sketcher

### 几何约束

| 约束 | 效果 |
|------------|--------|
| Horizontal（水平） | 使线条水平 |
| Vertical（垂直） | 使线条垂直 |
| Tangent（相切） | 使两条曲线相切 |
| Coincident（重合） | 合并两个点 |
| Equal（等长） | 使两段长度相等 |
| Parallel（平行） | 使两条线平行 |
| Perpendicular（垂直） | 使两条线垂直 |
| Symmetric（对称） | 关于线或点镜像几何图形 |

### 尺寸约束

| 约束 | 效果 |
|------------|--------|
| Length（长度） | 设置线段的长度 |
| Radius（半径） | 设置圆或圆弧的半径 |
| Diameter（直径） | 设置圆的直径 |
| Angle（角度） | 设置两条线之间的角度 |
| Distance（距离） | 设置两个实体之间的距离 |

## 构造实体几何（Part 工作台）

Part 工作台提供直接的 CSG 操作来组合基本形状。

| 操作 | 描述 |
|-----------|-------------|
| Union（并集） | 将两个实体合并为一个 |
| Cut（差集） | 从一个实体中减去另一个 |
| Common（交集） | 仅保留重叠部分 |

## 装配

FreeCAD 0.21 及更高版本包含装配功能。Assembly 工作台允许用户使用关节和约束将多个零件组合成完整的机构。

| 关节类型 | 自由度 |
|------------|-------------------|
| Fixed（固定） | 0（锁定所有运动） |
| Revolute（旋转） | 1（绕一个轴旋转） |
| Prismatic（棱柱） | 1（沿一个轴线性运动） |
| Cylindrical（圆柱） | 2（沿一个轴旋转和平移） |
| Spherical（球形） | 3（绕三个轴旋转） |

## 有限元分析（FEM）

FEM 工作台允许在 FreeCAD 中直接进行基本的结构、热和模态分析。

### 工作流程

1. 创建或导入几何体。
2. 定义材料属性。
3. 应用边界条件和载荷。
4. 生成网格。
5. 运行求解器。
6. 可视化结果。

| 求解器 | 类型 |
|--------|------|
| CalculiX | 结构和热分析 |
| Elmer | 多物理场仿真 |
| Z88 | 结构分析 |

## 宏和脚本

FreeCAD 有一个嵌入式 Python 解释器。几乎每个操作都可以通过脚本自动化。

```python
import FreeCAD
import Part

doc = FreeCAD.newDocument("MyPart")
box = doc.addObject("Part::Box", "Cube")
box.Length = 20
box.Width = 10
box.Height = 5
doc.recompute()
Part.export([box], "/tmp/cube.step")
```

## 技巧和最佳实践

| 技巧 | 原因 |
|-----|--------|
| 完全约束草图 | 防止意外的几何变化 |
| 使用命名参数 | 使模型更易于修改 |
| 保持特征历史简短 | 提高复杂模型的性能 |
| 经常保存 | FreeCAD 在非常大的模型上可能不稳定 |
| 使用 STEP 进行协作 | 它是支持最广泛的交换格式 |

## 结论

FreeCAD 是一款功能强大且灵活的 CAD 工具，适用于机械工程、产品设计、建筑和 3D 打印。其参数化特性和 Python 脚本支持使其成为初学者和高级用户的通用平台。


---

## 来源：cad2.md

## 目录

1. [OpenSCAD 简介](#introduction)
2. [安装](#installation)
3. [基本语法](#syntax)
4. [2D 形状](#2d-shapes)
5. [3D 形状](#3d-shapes)
6. [变换](#transformations)
7. [模块与函数](#modules)
8. [导出模型](#exporting)

---

## 简介

OpenSCAD 是一个基于脚本的 3D CAD 建模器。与传统 CAD 工具不同，OpenSCAD 通过代码描述对象，非常适合精确的参数化设计。

### OpenSCAD 核心功能

| 功能 | 描述 | 好处 |
|------|------|------|
| 基于脚本 | 代码驱动建模 | 精确控制 |
| 参数化 | 基于变量的设计 | 易于修改 |
| 跨平台 | Windows, macOS, Linux | 广泛兼容 |
| 免费 | 开源 | 无费用 |
| 程序员友好 | 代码语法 | 开发者熟悉 |

### OpenSCAD vs 传统 CAD

| 功能 | OpenSCAD | Fusion 360 | FreeCAD |
|------|----------|------------|---------|
| 界面 | 代码编辑器 | 可视化 | 可视化 |
| 学习曲线 | 中等 | 中等 | 高 |
| 精确度 | 精确 | 良好 | 良好 |
| 参数化 | 原生 | 是 | 是 |
| 成本 | 免费 | 免费增值 | 免费 |

### 系统要求

| 组件 | 最低 | 推荐 |
|------|------|------|
| CPU | 任何现代 CPU | 多核 |
| 内存 | 1GB | 4GB |
| GPU | OpenGL 2.0 | OpenGL 3.3+ |
| 显示 | 1024x768 | 1920x1080 |

---

## 安装

在你的操作系统上安装 OpenSCAD。

### 下载选项

| 平台 | 来源 | 文件类型 |
|------|------|----------|
| Windows | openscad.org | .exe 安装程序 |
| macOS | openscad.org | .dmg 文件 |
| Linux | 包管理器 | apt, dnf, flatpak |

### 安装步骤

| 步骤 | 操作 | 备注 |
|------|------|------|
| 1 | 下载 | 官方网站 |
| 2 | 运行安装程序 | 接受提示 |
| 3 | 选择位置 | 默认路径 |
| 4 | 完成 | 启动 OpenSCAD |

### Linux 安装

```bash
# Ubuntu/Debian
sudo apt install openscad

# Fedora
sudo dnf install openscad

# Flatpak
flatpak install flathub org.openscad.OpenSCAD
```

### 界面概述

| 区域 | 位置 | 用途 |
|------|------|------|
| 编辑器 | 左侧 | 代码输入 |
| 预览 | 右侧 | 3D 视图 |
| 控制台 | 底部 | 错误消息 |
| 工具栏 | 顶部 | 常用操作 |

---

## 基本语法

理解 OpenSCAD 脚本语言基础。

### 代码结构

```openscad
// Comments
/* Block comments */

// Variables
radius = 10;
height = 20;

// Shapes
sphere(r = radius);

// Transformations
translate([0, 0, height])
    cylinder(r = radius, h = height);
```

### 数据类型

| 类型 | 描述 | 示例 |
|------|------|------|
| Number | 数值 | 10, 3.14 |
| String | 文本 | "hello" |
| Boolean | 真/假 | true, false |
| Vector | 数组 | [1, 2, 3] |
| Range | 序列 | [0:10] |

### 运算符

| 运算符 | 描述 | 示例 |
|--------|------|------|
| + | 加法 | 5 + 3 |
| - | 减法 | 5 - 3 |
| * | 乘法 | 5 * 3 |
| / | 除法 | 6 / 2 |
| % | 取模 | 7 % 3 |

### 注释

| 类型 | 语法 | 示例 |
|------|------|------|
| 单行 | // | // This is a comment |
| 多行 | /* */ | /* Block comment */ |

### 变量

```openscad
// Simple variable
size = 10;

// Computed variable
area = size * size;

// Using variables
cube(size);
```

---

## 2D 形状

创建用于拉伸或投影的二维形状。

### 基本 2D 形状

| 形状 | 函数 | 参数 |
|------|------|------|
| Circle | circle() | r (半径), $fn (分辨率) |
| Square | square() | size, center |
| Polygon | polygon() | points, paths |
| Text | text() | text, size, font |

### Circle

```openscad
// Simple circle
circle(r = 10);

// Circle with resolution
circle(r = 10, $fn = 100);

// Ellipse
scale([2, 1])
    circle(r = 10);
```

### Square

```openscad
// Simple square
square(20);

// Centered square
square(20, center = true);

// Rectangle
square([20, 10]);

// Centered rectangle
square([20, 10], center = true);
```

### Polygon

```openscad
// Triangle
polygon(points = [[0,0], [10,0], [5,10]]);

// Square
polygon(points = [[0,0], [10,0], [10,10], [0,10]]);

// Complex shape
polygon(points = [
    [0, 0],
    [10, 0],
    [10, 10],
    [5, 15],
    [0, 10]
]);
```

### Text

```openscad
// Simple text
text("Hello");

// Sized text
text("Hello", size = 20);

// Custom font
text("Hello", font = "Arial:style=Bold");
```

---

## 3D 形状

创建三维实体对象。

### 基本 3D 形状

| 形状 | 函数 | 参数 |
|------|------|------|
| Cube | cube() | size, center |
| Sphere | sphere() | r, $fn |
| Cylinder | cylinder() | r, h, center |
| Polyhedron | polyhedron() | points, faces |

### Cube

```openscad
// Simple cube
cube(20);

// Centered cube
cube(20, center = true);

// Box (different dimensions)
cube([20, 10, 5]);

// Centered box
cube([20, 10, 5], center = true);
```

### Sphere

```openscad
// Simple sphere
sphere(r = 10);

// High resolution sphere
sphere(r = 10, $fn = 100);

// Low resolution (faceted)
sphere(r = 10, $fn = 8);
```

### Cylinder

```openscad
// Simple cylinder
cylinder(r = 10, h = 20);

// Centered cylinder
cylinder(r = 10, h = 20, center = true);

// Cone
cylinder(r1 = 10, r2 = 0, h = 20);

// Truncated cone
cylinder(r1 = 10, r2 = 5, h = 20);
```

### Polyhedron

```openscad
// Simple tetrahedron
polyhedron(
    points = [
        [0, 0, 0],
        [10, 0, 0],
        [5, 10, 0],
        [5, 5, 10]
    ],
    faces = [
        [0, 1, 2],
        [0, 1, 3],
        [1, 2, 3],
        [0, 2, 3]
    ]
);
```

---

## 变换

使用几何变换修改形状。

### 平移

```openscad
// Move in X
translate([10, 0, 0])
    cube(10);

// Move in multiple axes
translate([10, 20, 30])
    cube(10);
```

### 旋转

```openscad
// Rotate around Z axis
rotate([0, 0, 45])
    cube(10);

// Rotate around multiple axes
rotate([45, 45, 0])
    cube(10);
```

### 缩放

```openscad
// Scale uniformly
scale([2, 2, 2])
    cube(10);

// Scale non-uniformly
scale([2, 1, 0.5])
    cube(10);
```

### 镜像

```openscad
// Mirror across XZ plane
mirror([0, 1, 0])
    cube(10);

// Mirror across XY plane
mirror([0, 0, 1])
    cube(10);
```

### 颜色

```openscad
// Set color
color("red")
    cube(10);

// RGB color
color([1, 0, 0])
    cube(10);

// RGBA color
color([1, 0, 0, 0.5])
    cube(10);
```

### Hull

```openscad
// Convex hull of two shapes
hull() {
    sphere(5);
    translate([20, 0, 0])
        sphere(5);
}
```

---

## 模块与函数

创建可复用的代码组件。

### 模块

```openscad
// Simple module
module box(size) {
    cube(size, center = true);
}

// Using the module
box(20);

// Module with default parameters
module cylinder_custom(r = 10, h = 20) {
    cylinder(r = r, h = h, center = true);
}

// Using with custom values
cylinder_custom(r = 15, h = 30);
```

### 函数

```openscad
// Simple function
function area(r) = PI * r * r;

// Using the function
a = area(10);

// Function with multiple parameters
function volume(r, h) = PI * r * r * h;

v = volume(10, 20);
```

### 条件语句

```openscad
// If statement
if (size > 10) {
    cube(size);
} else {
    sphere(size / 2);
}

// Ternary operator
shape = (type == "cube") ? cube(10) : sphere(5);
```

### 循环

```openscad
// For loop
for (i = [0:10]) {
    translate([i * 15, 0, 0])
        cube(10);
}

// For loop with list
for (i = [10, 20, 30]) {
    translate([i, 0, 0])
        cube(10);
}
```

### Include 和 Use

```openscad
// Include file (executes code)
include <library.scad>;

// Use file (imports modules/functions only)
use <library.scad>;
```

---

## 导出模型

导出你的 3D 模型用于打印或分享。

### 导出格式

| 格式 | 扩展名 | 用途 |
|------|--------|------|
| STL | .stl | 3D 打印 |
| OFF | .off | 学术用途 |
| AMF | .amf | 高级打印 |
| 3MF | .3mf | 现代打印 |
| DXF | .dxf | 2D 切割 |
| SVG | .svg | 2D 图形 |
| PNG | .png | 图片 |

### 导出流程

| 步骤 | 操作 | 备注 |
|------|------|------|
| 1 | 设计模型 | 编写代码 |
| 2 | 预览 | F5 键 |
| 3 | 渲染 | F6 键 |
| 4 | 导出 | File → Export |
| 5 | 选择格式 | STL 用于打印 |

### 渲染质量

| 设置 | 描述 | 推荐 |
|------|------|------|
| $fn | 分辨率 | 曲线用 100 |
| $fa | 最小角度 | 1（默认） |
| $fs | 最小尺寸 | 0.1（默认） |

### 打印准备

| 步骤 | 操作 | 工具 |
|------|------|------|
| 1 | 导出 STL | OpenSCAD |
| 2 | 检查网格 | MeshLab 或 Netfabb |
| 3 | 如需修复 | 网格修复工具 |
| 4 | 切片 | Cura, PrusaSlicer |
| 5 | 打印 | 3D 打印机 |

### 常见问题

| 问题 | 原因 | 解决方案 |
|------|------|----------|
| 非流形 | 开放边缘 | 检查几何 |
| 孔洞 | 缺失面 | 检查 polyhedron |
| 交叉 | 重叠形状 | 使用 union() |
| 太大 | 单位错误 | 适当缩放 |

---

## 总结

| 主题 | 核心要点 |
|------|----------|
| 界面 | 代码编辑器 + 3D 预览 |
| 语法 | 类 C 脚本语言 |
| 2D 形状 | 圆、方、多边形 |
| 3D 形状 | 立方体、球、圆柱 |
| 变换 | 平移、旋转、缩放 |
| 模块 | 可复用代码组件 |
| 导出 | STL 用于 3D 打印 |


---

## 来源：model.md

## 简介

Solvespace 是一款免费、开源的参数化 2D/3D CAD 工具。它支持基于约束的建模，适用于机械零件、连杆分析和 3D 实体几何。本教程涵盖在 Solvespace 中设计模型的基础知识。

## 系统要求

| 组件 | 最低要求 | 推荐配置 |
|------|---------|---------|
| 操作系统 | Windows 7+、macOS 10.12+、Linux | 最新稳定版 |
| 内存 | 512 MB | 2 GB 或更多 |
| 磁盘空间 | 30 MB | 100 MB |
| GPU | OpenGL 2.0 | OpenGL 3.0+ |
| 显示器 | 1024x768 | 1920x1080 |

## 安装

| 平台 | 方法 |
|------|------|
| Windows | 从 releases 页面下载安装程序 |
| macOS | Homebrew：`brew install --cask solvespace` |
| Ubuntu/Debian | `sudo apt install solvespace` |
| Fedora | `sudo dnf install solvespace` |
| 源码 | 使用 CMake 克隆并构建 |

## 核心概念

Solvespace 使用基于约束的方法。你绘制 2D 轮廓，添加几何约束，然后通过拉伸或旋转生成 3D 模型。

| 概念 | 描述 |
|------|------|
| 草图（Sketch） | 包含几何实体的 2D 绘图平面 |
| 约束（Constraint） | 限制实体行为的规则 |
| 组（Group） | 操作的集合（拉伸、旋转等） |
| 工作平面（Workplane） | 用于草图绘制的参考平面 |
| 实体（Entity） | 点、线、弧或圆 |
| 参数（Parameter） | 驱动模型的尺寸或变量 |

## 用户界面概览

| 面板 | 位置 | 用途 |
|------|------|------|
| 文本窗口 | 左侧 | 显示约束、属性和组信息 |
| 图形窗口 | 中央 | 主 3D/2D 视口 |
| 工具栏 | 顶部 | 绘图和约束工具 |
| 样式窗口 | 右侧 | 线条样式、颜色和可见性 |

## 创建 2D 草图

### 第 1 步：选择工作平面

| 操作 | 方法 |
|------|------|
| 默认 XY 平面 | 点击"New Group > Sketch in New Workplane" |
| 自定义平面 | 选择面或边，然后创建工作平面 |
| 对齐平面 | 使用现有几何体作为参考 |

### 第 2 步：绘制实体

| 实体 | 工具 | 用法 |
|------|------|------|
| 线段 | Line 工具 | 点击起点和终点 |
| 矩形 | Rectangle 工具 | 点击两个对角 |
| 圆 | Circle 工具 | 点击圆心，然后半径点 |
| 弧 | Arc 工具 | 点击起点、终点，然后中点 |
| 贝塞尔曲线 | Bezier 工具 | 依次点击控制点 |

### 第 3 步：添加约束

约束定义实体之间的关系。

| 约束 | 符号 | 功能 |
|------|------|------|
| 水平 | H | 使线条水平 |
| 垂直 | V | 使线条垂直 |
| 距离 | D | 设置精确长度或位置 |
| 角度 | A | 设置两条线之间的角度 |
| 垂直 | Perp | 使两条线垂直 |
| 平行 | Par | 使两条线平行 |
| 等长 | Equal | 使两段长度相等 |
| 相切 | T | 使弧与线相切 |
| 重合 | Coinc | 使两点共享位置 |
| 对称 | Sym | 沿轴镜像 |

## 参数化尺寸

| 类型 | 示例 | 行为 |
|------|------|------|
| 固定距离 | 50.0 mm | 值锁定为字面数字 |
| 变量关联 | d = width / 2 | 由命名变量驱动 |
| 表达式 | 2 * base + 10 | 由参数计算 |

### 定义变量

1. 打开文本窗口（T 键）。
2. 导航到"Parametric > Add New Parameter"。
3. 命名变量并设置其值。
4. 通过名称将约束链接到变量。

## 3D 操作

### 拉伸（Extrude）

| 选项 | 描述 |
|------|------|
| Extrude | 沿平面垂直方向延伸草图 |
| Distance | 数值设置拉伸深度 |
| Symmetric | 在两个方向上等量拉伸 |
| Cut | 从现有实体中减去体积 |

### 旋转（Revolve）

| 选项 | 描述 |
|------|------|
| Axis | 选择一条线作为旋转轴 |
| Angle | 设置旋转角度（360 为完整旋转） |
| Direction | 顺时针或逆时针 |

### 其他操作

| 操作 | 用例 |
|------|------|
| Helix（螺旋） | 弹簧、螺纹、螺旋线 |
| Loft（放样） | 两个轮廓之间的平滑过渡 |
| 布尔合并 | 合并两个实体 |
| 布尔差集 | 从一个实体中减去另一个 |

## 装配与组

| 组类型 | 用途 |
|--------|------|
| Sketch | 工作平面中的 2D 绘图 |
| Extrude | 从草图生成 3D 实体 |
| Revolve | 通过旋转生成 3D 实体 |
| Link/Assembly | 导入并定位外部零件 |
| Difference | 布尔减法 |

## 实例：轴承座

| 步骤 | 操作 |
|------|------|
| 1 | 在 XY 平面上创建矩形（80 mm x 60 mm） |
| 2 | 将尺寸约束为精确值 |
| 3 | 使用弧约束添加圆角 |
| 4 | 在矩形中心绘制圆（直径 30 mm） |
| 5 | 将轮廓拉伸至 40 mm |
| 6 | 对圆进行贯穿拉伸切割 |
| 7 | 添加安装孔作为单独的拉伸切割组 |

## 文件格式

| 格式 | 方向 | 备注 |
|------|------|------|
| .slvs | 原生格式 | 完整参数化数据 |
| .dxf | 导出 | 2D 绘图交换 |
| .svg | 导出 | 用于文档的矢量图形 |
| .stl | 导出 | 用于 3D 打印的网格 |
| .step | 导出 | 标准 CAD 交换格式 |
| .obj | 导出 | 支持材质的网格 |

## 快捷键

| 按键 | 操作 |
|------|------|
| L | 画线 |
| R | 画矩形 |
| C | 画圆 |
| A | 画弧 |
| D | 添加距离约束 |
| O | 添加角度约束 |
| G | 切换构造几何体 |
| N | 新建组 |
| Delete | 删除选中的实体 |
| Ctrl+Z | 撤销 |
| Ctrl+S | 保存 |

## 故障排除

| 问题 | 原因 | 解决方案 |
|------|------|---------|
| 草图过约束 | 约束过多 | 移除冗余约束 |
| 草图欠约束 | 缺少约束 | 添加尺寸或几何约束 |
| 拉伸失败 | 草图轮廓未封闭 | 关闭草图中的所有轮廓 |
| 导出缺少面 | 实体不完整 | 检查零厚度几何体 |
| 渲染缓慢 | 模型复杂 | 隐藏未使用的组，降低网格密度 |

## 最佳实践

| 实践 | 原因 |
|------|------|
| 为参数命名 | 便于后续修改尺寸 |
| 逻辑使用组 | 每组一个操作，保持清晰 |
| 完全约束 | 防止模型意外变化 |
| 经常保存 | Solvespace 不会自动保存 |
| 用变量测试 | 最终确定前验证参数化行为 |

## 总结

Solvespace 提供了一个轻量但强大的参数化 CAD 设计环境。通过掌握基于约束的草图绘制、拉伸和组管理，你可以创建精确的机械零件和装配体，适用于 3D 打印和制造。


---

## 来源：slicer.md

## 简介

Ultimaker Cura 是一款开源 3D 打印切片软件。它将 3D 模型（STL、OBJ、3MF 文件）转换为 3D 打印机可理解的 G-code 指令，提供丰富的打印质量和材料使用配置选项。

| 特性 | 描述 |
|---------|-------------|
| 切片引擎 | 将 3D 模型转换为打印机指令 |
| 打印配置 | 预配置的质量设置 |
| 材料支持 | 各种耗材类型的配置文件 |
| 插件系统 | 可通过社区插件扩展 |
| 多打印机 | 支持多个打印机配置文件 |

## 核心概念

### 3D 打印术语

| 术语 | 定义 |
|------|------------|
| Slicing | 将 3D 模型转换为打印机指令（G-code） |
| Layer height | 每层打印的厚度 |
| Infill | 打印件的内部结构密度 |
| Shell | 打印件的外壁 |
| Support | 用于悬垂特征的临时结构 |
| Raft | 用于改善平台附着力的底层 |
| Skirt | 开始前在物体周围打印的轮廓 |
| Brim | 用于平台附着力的扩展首层 |

### 打印质量级别

| 配置 | 层高 | 使用场景 |
|---------|-------------|----------|
| Extra Fine | 0.1 mm | 高细节，慢速打印 |
| Fine | 0.15 mm | 良好细节，中等速度 |
| Standard | 0.2 mm | 质量和速度的平衡 |
| Draft | 0.3 mm | 快速打印，较低细节 |
| Extra Draft | 0.4 mm | 快速原型，最少细节 |

## 安装

### 下载和安装

| 平台 | 方法 |
|----------|--------|
| Windows | 从 ultimaker.com 下载安装程序 |
| macOS | 从 ultimaker.com 下载 DMG |
| Linux | AppImage 或包管理器 |
| Ubuntu/Debian | `sudo apt install cura` |

### 系统要求

| 组件 | 最低要求 | 推荐配置 |
|-----------|---------|-------------|
| CPU | 64 位处理器 | 多核 |
| 内存 | 4 GB | 8 GB+ |
| 显卡 | OpenGL 2.0 | 独立 GPU |
| 存储 | 500 MB | 2 GB+ |
| 显示 | 1280x720 | 1920x1080+ |

## 打印机配置

### 添加打印机

| 步骤 | 操作 |
|------|--------|
| 1 | 打开 Cura，进入设置 > 打印机 > 添加打印机 |
| 2 | 选择打印机制造商和型号 |
| 3 | 或选择自定义进行手动配置 |
| 4 | 设置构建体积尺寸 |
| 5 | 配置喷嘴直径 |
| 6 | 保存打印机配置文件 |

### 打印机设置

| 设置 | 描述 | 常用值 |
|---------|-------------|---------------|
| 构建体积 | 最大打印尺寸 | 220x220x250 mm |
| 喷嘴直径 | 打印喷嘴直径 | 0.4 mm（标准） |
| 加热平台 | 打印机是否有加热平台 | 是/否 |
| 耗材直径 | 耗材直径 | 1.75 mm 或 2.85 mm |
| 挤出头数量 | 打印头数量 | 1 或 2 |

### 热门打印机配置

| 打印机 | 构建体积 | 喷嘴 |
|---------|-------------|--------|
| Ender 3 | 220x220x250 mm | 0.4 mm |
| Prusa i3 MK3S | 250x210x210 mm | 0.4 mm |
| Ultimaker S5 | 330x240x300 mm | 0.4/0.8 mm |
| Anycubic i3 Mega | 210x210x205 mm | 0.4 mm |
| Creality CR-10 | 300x300x400 mm | 0.4 mm |

## 打印设置

### 质量设置

| 设置 | 描述 | 范围 |
|---------|-------------|-------|
| 层高 | 每层厚度 | 0.05-0.4 mm |
| 首层高度 | 第一层高度 | 0.2-0.3 mm |
| 线宽 | 挤出线宽度 | 0.3-0.5 mm |

### 外壳设置

| 设置 | 描述 | 典型值 |
|---------|-------------|---------------|
| 壁厚 | 外壁总厚度 | 0.8-1.6 mm |
| 壁线数 | 外壁线数 | 2-4 |
| 顶层层数 | 顶部实心层数 | 3-6 |
| 底层层数 | 底部实心层数 | 3-6 |

### 填充设置

| 填充密度 | 使用场景 | 强度 |
|---------------|----------|----------|
| 0-10% | 装饰性打印、原型 | 低 |
| 10-20% | 标准打印 | 中 |
| 20-40% | 功能性部件 | 高 |
| 40-100% | 最大强度 | 非常高 |

### 填充图案

| 图案 | 描述 | 最佳用途 |
|---------|-------------|----------|
| Grid | 简单网格图案 | 通用 |
| Lines | 每层平行线 | 快速打印 |
| Triangular | 基于三角形的图案 | 各方向强度 |
| Gyroid | 弯曲有机结构 | 高强度、低重量 |
| Cubic | 3D 立方体图案 | 各向同性强度 |
| Concentric | 向内螺旋线 | 柔性部件 |

### 温度设置

| 材料 | 喷嘴温度 | 平台温度 |
|----------|-------------------|-----------------|
| PLA | 190-220 C | 50-60 C |
| ABS | 230-260 C | 90-110 C |
| PETG | 220-250 C | 70-80 C |
| TPU | 210-230 C | 40-60 C |
| Nylon | 240-270 C | 70-90 C |

### 速度设置

| 设置 | 描述 | 典型范围 |
|---------|-------------|---------------|
| 打印速度 | 一般移动速度 | 40-60 mm/s |
| 填充速度 | 填充速度 | 60-100 mm/s |
| 壁速 | 外壁速度 | 25-45 mm/s |
| 移动速度 | 非打印移动 | 120-150 mm/s |
| 首层速度 | 第一层速度 | 20-30 mm/s |

## 支撑设置

### 支撑类型

| 类型 | 描述 | 使用场景 |
|------|-------------|----------|
| Normal | 标准支撑结构 | 一般悬垂 |
| Tree | 分支状支撑结构 | 复杂几何形状 |

### 支撑设置

| 设置 | 描述 | 典型值 |
|---------|-------------|---------------|
| 支撑悬垂角度 | 需要支撑的角度 | 45-60 度 |
| 支撑密度 | 支撑的填充密度 | 10-20% |
| 支撑 Z 距离 | 支撑和打印件之间的间隙 | 0.2-0.4 mm |
| 支撑图案 | 支撑结构的图案 | Lines 或 Zig Zag |

### 平台附着

| 类型 | 描述 | 使用场景 |
|------|-------------|----------|
| None | 无附着辅助 | 平台附着力已好 |
| Brim | 扩展首层 | 防止翘曲 |
| Raft | 完整底层 | 平台附着困难 |
| Skirt | 打印件周围轮廓 | 喷嘴预热 |

## 材料配置

### PLA 配置

| 设置 | 值 |
|---------|-------|
| 喷嘴温度 | 200 C |
| 平台温度 | 60 C |
| 打印速度 | 50 mm/s |
| 回抽距离 | 5 mm |
| 回抽速度 | 45 mm/s |
| 风扇 | 100% |

### ABS 配置

| 设置 | 值 |
|---------|-------|
| 喷嘴温度 | 240 C |
| 平台温度 | 100 C |
| 打印速度 | 50 mm/s |
| 回抽距离 | 5 mm |
| 回抽速度 | 45 mm/s |
| 风扇 | 0-30% |
| 封闭空间 | 推荐 |

### PETG 配置

| 设置 | 值 |
|---------|-------|
| 喷嘴温度 | 235 C |
| 平台温度 | 75 C |
| 打印速度 | 45 mm/s |
| 回抽距离 | 4 mm |
| 回抽速度 | 40 mm/s |
| 风扇 | 50% |

## 插件

### 热门插件

| 插件 | 描述 |
|--------|-------------|
| OctoPrint | 直接将打印发送到 OctoPrint |
| CuraEngine | 高级切片选项 |
| Settings Guide | 所有设置的工具提示 |
| Mesh Tools | 分析和修复 3D 模型 |
| Printer Settings | 额外的打印机配置选项 |

## G-code 预览

### 预览功能

| 功能 | 描述 |
|---------|-------------|
| 层视图 | 逐层查看打印 |
| 线类型 | 按线类型着色（壁、填充、支撑） |
| 速度视图 | 按打印速度着色 |
| 厚度 | 按线厚度着色 |
| 模拟 | 打印过程动画预览 |

### 线类型颜色

| 颜色 | 线类型 |
|-------|-----------|
| 红色 | 外壁 |
| 橙色 | 内壁 |
| 黄色 | 皮肤（顶/底） |
| 绿色 | 填充 |
| 青色 | 支撑 |
| 蓝色 | 移动 |
| 白色 | 支撑界面 |

## 故障排除

### 常见打印问题

| 问题 | 原因 | 需调整的设置 |
|-------|-------|-------------------|
| 平台附着差 | 首层太高或太冷 | 首层高度、平台温度 |
| 拉丝 | 回抽不足 | 回抽距离和速度 |
| 翘曲 | 材料冷却太快 | 平台温度、封闭空间 |
| 层偏移 | 皮带松或速度太快 | 打印速度、检查硬件 |
| 欠挤出 | 耗材流量不足 | 温度、流量率 |
| 过挤出 | 耗材过多 | 流量率、耗材直径 |

## 总结

| 主题 | 核心要点 |
|-------|-------------|
| 切片 | 将 3D 模型转换为 G-code 打印机指令 |
| 配置 | 质量级别的预配置设置 |
| 材料 | 不同材料使用不同的温度和速度设置 |
| 支撑 | 悬垂自动生成支撑 |
| 预览 | 打印前逐层可视化 |
| 插件 | 可通过社区开发的插件扩展 |


---

## 来源：prusa.md

## 简介

PrusaSlicer 是一款开源切片软件，可将 3D 模型转换为打印机指令（G-code）。它支持 FDM 和树脂打印机，具有优化打印质量和可靠性的高级功能。

## 目录

1. [安装](#安装)
2. [界面概览](#界面概览)
3. [打印机设置](#打印机设置)
4. [耗材配置](#耗材配置)
5. [打印设置](#打印设置)
6. [模型准备](#模型准备)
7. [支撑结构](#支撑结构)
8. [填充与外壳](#填充与外壳)
9. [高级功能](#高级功能)

## 安装

### 下载选项

| 平台 | 来源 | 大小 |
|------|------|------|
| Windows | GitHub releases | ~60 MB |
| macOS | GitHub releases | ~60 MB |
| Linux | AppImage/Flatpak | ~60 MB |

### 系统要求

| 组件 | 最低要求 | 推荐配置 |
|------|----------|----------|
| CPU | 双核 | 四核 |
| 内存 | 4 GB | 8 GB |
| GPU | OpenGL 2.0 | 独立 GPU |
| 存储 | 500 MB | 2 GB |
| 显示 | 1280x720 | 1920x1080 |

## 界面概览

### 主要区域

| 区域 | 位置 | 用途 |
|------|------|------|
| 3D 视图 | 中央 | 模型预览和操作 |
| 打印板 | 左面板 | 对象列表和设置 |
| 设置 | 右面板 | 打印/耗材/打印机设置 |
| 预览 | 顶部标签 | 层视图和 G-code 预览 |
| 信息栏 | 底部 | 打印时间和材料估算 |

### 视图控制

| 控制 | 操作 |
|------|------|
| 左键 + 拖动 | 旋转视图 |
| 中键 + 拖动 | 平移视图 |
| 滚轮 | 缩放 |
| 右键 | 上下文菜单 |
| R | 重置视图 |

## 打印机设置

### 支持的打印机

| 类别 | 示例 |
|------|------|
| Prusa | MK3S+, MK4, MINI+, XL |
| Creality | Ender 3, CR-10 |
| Anycubic | Kobra, Mega |
| Bambu Lab | X1, P1P, P1S |
| 自定义 | 任何 FDM 打印机 |

### 打印机配置

| 设置 | 说明 | 示例 |
|------|------|------|
| 热床形状 | 构建板尺寸 | 220x220 mm |
| 最大高度 | 最大 Z 高度 | 250 mm |
| 喷嘴直径 | 打印喷嘴大小 | 0.4 mm |
| 固件 | 打印机固件类型 | Marlin, RepRap |
| G-code 风格 | 命令集 | Marlin 2 |

### 添加自定义打印机

| 步骤 | 操作 |
|------|------|
| 1 | Configuration > Printer > Add |
| 2 | 选择 "Custom Printer" |
| 3 | 输入热床尺寸 |
| 4 | 设置喷嘴直径 |
| 5 | 配置 G-code 风格 |
| 6 | 添加起始/结束 G-code |

### 起始 G-code 模板

```gcode
; Start G-code
G28 ; Home all axes
G29 ; Auto bed leveling (if available)
G1 Z5 F3000 ; Raise nozzle
G1 X0 Y0 F5000 ; Move to origin
M104 S{temperature[0]} ; Set extruder temp
M190 S{bed_temperature[0]} ; Wait for bed temp
M109 S{temperature[0]} ; Wait for extruder temp
G1 E2 F300 ; Prime nozzle
G92 E0 ; Reset extruder
```

## 耗材配置

### 常见耗材类型

| 耗材 | 喷嘴温度 | 热床温度 | 速度 | 回抽 |
|------|----------|----------|------|------|
| PLA | 200-220°C | 50-60°C | 60 mm/s | 0.8 mm |
| PETG | 230-250°C | 70-80°C | 45 mm/s | 0.8 mm |
| ABS | 240-260°C | 100-110°C | 50 mm/s | 0.8 mm |
| TPU | 220-240°C | 40-60°C | 25 mm/s | 1.2 mm |
| ASA | 240-260°C | 100-110°C | 50 mm/s | 0.8 mm |

### 耗材设置

| 设置 | 说明 | 典型范围 |
|------|------|----------|
| 挤出倍率 | 流量 | 0.95-1.05 |
| 回抽距离 | 耗材回拉 | 0.5-2.0 mm |
| 回抽速度 | 回拉速度 | 30-60 mm/s |
| Z 抬升 | 移动时抬升喷嘴 | 0-0.4 mm |
| 冷却风扇速度 | 层冷却 | 0-100% |

### 温度塔

| 用途 | 方法 |
|------|------|
| 找到最佳温度 | 打印温度塔 |
| 测试范围 | 10°C 递增 |
| 评估 | 悬垂、拉丝、层质量 |

## 打印设置

### 质量设置

| 参数 | 粗糙 | 正常 | 精细 |
|------|------|------|------|
| 层高 | 0.30 mm | 0.20 mm | 0.10 mm |
| 首层高度 | 0.35 mm | 0.25 mm | 0.15 mm |
| 外壳数 | 2 | 3 | 4 |
| 顶层层数 | 3 | 4 | 5 |
| 底层层数 | 3 | 4 | 5 |

### 速度设置

| 参数 | 慢速 | 正常 | 快速 |
|------|------|------|------|
| 外壳 | 30 mm/s | 45 mm/s | 60 mm/s |
| 填充 | 40 mm/s | 80 mm/s | 120 mm/s |
| 移动 | 100 mm/s | 150 mm/s | 200 mm/s |
| 首层 | 20 mm/s | 25 mm/s | 30 mm/s |

### 层高指南

| 喷嘴 | 最小层高 | 最佳 | 最大层高 |
|------|----------|------|----------|
| 0.25 mm | 0.06 mm | 0.10 mm | 0.15 mm |
| 0.40 mm | 0.10 mm | 0.20 mm | 0.28 mm |
| 0.60 mm | 0.15 mm | 0.30 mm | 0.42 mm |
| 0.80 mm | 0.20 mm | 0.40 mm | 0.56 mm |

## 模型准备

### 文件格式

| 格式 | 说明 | 支持 |
|------|------|------|
| STL | 标准网格 | 完全 |
| OBJ | 带材质的网格 | 完全 |
| 3MF | 带元数据的现代格式 | 完全 |
| AMF | 增材制造 | 完全 |
| STEP | CAD 格式 | 通过转换 |

### 模型修复

| 问题 | 检测 | 修复 |
|------|------|------|
| 非流形边缘 | 视觉检查 | NetFabb 修复 |
| 网格孔洞 | 切片器警告 | 闭合孔洞 |
| 法线反转 | 里外翻转外观 | 翻转法线 |
| 自相交 | 打印伪影 | 布尔清理 |

### 模型操作

| 操作 | 工具 | 快捷键 |
|------|------|--------|
| 移动 | 放置工具 | M |
| 旋转 | 旋转工具 | R |
| 缩放 | 缩放工具 | S |
| 镜像 | 镜像工具 | - |
| 切割 | 切割工具 | - |

## 支撑结构

### 支撑类型

| 类型 | 说明 | 最佳用途 |
|------|------|----------|
| 网格 | 垂直柱体 | 简单悬垂 |
| 贴合 | 轮廓跟随 | 复杂几何 |
| 有机 | 树状 | 最小接触 |
| 手绘 | 手动放置 | 选择性支撑 |

### 支撑设置

| 设置 | 说明 | 典型值 |
|------|------|--------|
| 悬垂角度 | 需要支撑的角度 | 45° |
| 接触 Z 距离 | 与模型的间隙 | 0.2 mm |
| 图案间距 | 支撑密度 | 2.5 mm |
| 接触层 | 顶部支撑层 | 2-3 |

### 何时使用支撑

| 悬垂角度 | 是否需要支撑 |
|----------|-------------|
| 0-30° | 不需要 |
| 30-45° | 视情况而定，测试打印 |
| 45-60° | 通常需要 |
| 60-90° | 总是需要 |

## 填充与外壳

### 填充图案

| 图案 | 强度 | 速度 | 材料 | 最佳用途 |
|------|------|------|------|----------|
| 直线 | 中等 | 快 | 低 | 通用 |
| 螺旋体 | 高 | 中等 | 中等 | 结构件 |
| 蜂窝 | 高 | 慢 | 中等 | 强度 |
| 立方 | 高 | 中等 | 中等 | 3D 强度 |
| 闪电 | 低 | 快 | 极低 | 草稿 |

### 填充密度

| 密度 | 使用场景 | 打印时间 |
|------|----------|----------|
| 0% | 空心、装饰 | 最快 |
| 10-15% | 原型 | 快 |
| 20-30% | 功能件 | 中等 |
| 40-60% | 高强度 | 慢 |
| 100% | 实心件 | 最慢 |

### 外壳设置

| 设置 | 说明 | 影响 |
|------|------|------|
| 外壳数 | 外壁 | 表面质量 |
| 顶层层数 | 水平顶面 | 顶部质量 |
| 底层层数 | 水平底面 | 热床附着 |
| 外壳厚度 | 总壁厚 | 强度 |

## 高级功能

### 可变层高

| 功能 | 说明 |
|------|------|
| 自适应 | 基于几何自动调整 |
| 手动 | 绘制层高 |
| 范围 | 0.07 mm 到 0.30 mm |
| 优势 | 需要处保证质量，其他处保证速度 |

### 多材料打印

| 方式 | 设置 |
|------|------|
| 单喷嘴 | 手动换料 |
| MMU/MMU2S | 自动换料 |
| 双喷嘴 | 两个独立喷嘴 |

### 打印时间估算

| 因素 | 影响 |
|------|------|
| 层高 | 更低 = 更多时间 |
| 填充密度 | 更高 = 更多时间 |
| 外壳数 | 更多 = 更多时间 |
| 移动速度 | 更慢 = 更多时间 |
| 加速度 | 更低 = 更多时间 |

### 常用打印设置预设

| 预设 | 层高 | 填充 | 速度 | 使用场景 |
|------|------|------|------|----------|
| 草稿 | 0.30 mm | 10% | 快 | 原型 |
| 质量 | 0.15 mm | 20% | 正常 | 最终件 |
| 结构 | 0.20 mm | 40% | 慢 | 承重件 |
| 快速 | 0.28 mm | 15% | 快 | 快速打印 |

## G-code 预览

### 预览功能

| 功能 | 说明 |
|------|------|
| 层滑块 | 查看单个层 |
| 特征着色 | 按特征类型着色 |
| 移动可视化 | 显示非打印移动 |
| 宽度可视化 | 显示挤出宽度 |
| 速度可视化 | 按打印速度着色 |

### 特征颜色编码

| 颜色 | 特征 |
|------|------|
| 黄色 | 外壳 |
| 橙色 | 内壳 |
| 绿色 | 填充 |
| 蓝色 | 支撑 |
| 红色 | 桥接 |

## 总结

PrusaSlicer 提供了全面的工具来准备 3D 模型进行打印。其直观的界面、广泛的打印机支持以及可变层高和有机支撑等高级功能，使其适合寻求精确控制打印设置的初学者和有经验的用户。


---

## 来源：orca.md

## 简介

OrcaSlicer 是一款开源的 FDM 3D 打印机切片器，最初从 BambuStudio 分叉而来。它提供高级功能，包括自动校准、多打印机支持和优化的切片算法，以提高打印质量和速度。

## 目录

1. [核心功能](#核心功能)
2. [安装](#安装)
3. [打印机配置](#打印机配置)
4. [耗材设置](#耗材设置)
5. [打印配置](#打印配置)
6. [模型准备](#模型准备)
7. [校准工具](#校准工具)
8. [高级功能](#高级功能)

## 核心功能

| 功能 | 说明 |
|------|------|
| 自动校准 | 内置校准测试 |
| 多打印机 | 支持多台打印机 |
| 自适应层 | 可变层高 |
| 树状支撑 | 有机支撑结构 |
| 接缝绘制 | 控制接缝位置 |
| 多材料 | AMS/MMU 支持 |
| Klipper 原生 | 直接 Klipper 支持 |

## 安装

### 平台支持

| 平台 | 下载 | 大小 |
|------|------|------|
| Windows | GitHub releases | ~80 MB |
| macOS | GitHub releases | ~80 MB |
| Linux | AppImage/Flatpak | ~80 MB |

### 系统要求

| 组件 | 最低要求 | 推荐配置 |
|------|----------|----------|
| CPU | 双核 | 四核 |
| 内存 | 4 GB | 8 GB |
| GPU | OpenGL 3.3 | 独立 GPU |
| 显示 | 1280x720 | 1920x1080 |
| 存储 | 500 MB | 2 GB |

### 安装方式

| 方式 | 命令/操作 |
|------|-----------|
| AppImage (Linux) | `chmod +x OrcaSlicer.AppImage && ./OrcaSlicer.AppImage` |
| Flatpak (Linux) | `flatpak install com.bambulab.OrcaSlicer` |
| Windows | 运行安装程序 .exe |
| macOS | 挂载 .dmg 并拖到 Applications |

## 打印机配置

### 内置打印机配置文件

| 制造商 | 型号 | 说明 |
|--------|------|------|
| Bambu Lab | X1, X1C, P1P, P1S, A1 | 原生支持 |
| Creality | Ender 3, K1, CR-10 | 社区配置 |
| Prusa | MK3S+, MK4 | 社区配置 |
| Voron | V2.4, Trident | Klipper 配置 |
| Anycubic | Kobra, Vyper | 社区配置 |
| 自定义 | 任何打印机 | 手动设置 |

### 添加打印机

| 步骤 | 操作 |
|------|------|
| 1 | 打开配置向导 |
| 2 | 选择打印机制造商 |
| 3 | 选择具体型号 |
| 4 | 导入或创建配置文件 |
| 5 | 配置热床大小和形状 |
| 6 | 设置喷嘴直径 |
| 7 | 配置 G-code 风格 |

### 自定义打印机设置

| 设置 | 说明 | 示例 |
|------|------|------|
| 热床形状 | 构建板尺寸 | 220x220 mm |
| 最大高度 | 最大 Z 高度 | 250 mm |
| 喷嘴直径 | 打印喷嘴大小 | 0.4 mm |
| 固件 | 打印机固件 | Marlin, Klipper |
| G-code 风格 | 命令方言 | RepRap, Marlin |

### Klipper 配置

| 设置 | 值 |
|------|-----|
| G-code 风格 | Klipper |
| 固件回抽 | 如已配置则启用 |
| Input shaper | 自动检测 |
| Pressure advance | 建议校准 |

## 耗材设置

### 支持的材料

| 材料 | 喷嘴温度 | 热床温度 | 回抽 | 说明 |
|------|----------|----------|------|------|
| PLA | 190-220°C | 50-60°C | 0.8 mm | 易打印 |
| PETG | 230-250°C | 70-80°C | 0.8 mm | 强度好 |
| ABS | 240-260°C | 100-110°C | 0.8 mm | 需要封闭 |
| TPU | 220-240°C | 40-60°C | 1.2 mm | 柔性 |
| ASA | 240-260°C | 100-110°C | 0.8 mm | 抗 UV |
| Nylon | 250-270°C | 70-90°C | 1.0 mm | 强度高、吸湿 |

### 耗材设置

| 设置 | 说明 | 范围 |
|------|------|------|
| 流量比 | 挤出倍率 | 0.95-1.05 |
| Pressure advance | 补偿因子 | 0.0-0.1 |
| 回抽距离 | 耗材回拉 | 0.5-2.0 mm |
| 回抽速度 | 回拉速度 | 30-60 mm/s |
| Z-hop | 移动时抬升 | 0-0.4 mm |
| 风扇速度 | 冷却百分比 | 0-100% |

### 耗材校准

| 测试 | 用途 | 结果 |
|------|------|------|
| 温度塔 | 最佳温度 | 最佳外观范围 |
| 流量校准 | 挤出精度 | 流量比 |
| Pressure advance | 拐角质量 | PA 值 |
| 回抽测试 | 拉丝 | 距离/速度 |
| 最大体积速度 | 流量限制 | mm³/s |

## 打印配置

### 质量预设

| 预设 | 层高 | 壁数 | 填充 | 速度 | 使用场景 |
|------|------|------|------|------|----------|
| 草稿 | 0.28 mm | 2 | 10% | 快 | 原型 |
| 标准 | 0.20 mm | 3 | 15% | 正常 | 通用 |
| 精细 | 0.12 mm | 4 | 20% | 慢 | 细节 |
| 超精细 | 0.08 mm | 5 | 25% | 最慢 | 微缩模型 |

### 速度设置

| 参数 | 保守 | 标准 | 激进 |
|------|------|------|------|
| 外壁 | 30 mm/s | 60 mm/s | 100 mm/s |
| 内壁 | 40 mm/s | 80 mm/s | 120 mm/s |
| 填充 | 50 mm/s | 100 mm/s | 200 mm/s |
| 移动 | 100 mm/s | 200 mm/s | 300 mm/s |
| 首层 | 20 mm/s | 30 mm/s | 40 mm/s |

### 层高指南

| 喷嘴 | 最小层高 | 最佳 | 最大层高 |
|------|----------|------|----------|
| 0.2 mm | 0.05 mm | 0.10 mm | 0.14 mm |
| 0.4 mm | 0.10 mm | 0.20 mm | 0.28 mm |
| 0.6 mm | 0.15 mm | 0.30 mm | 0.42 mm |
| 0.8 mm | 0.20 mm | 0.40 mm | 0.56 mm |
| 1.0 mm | 0.25 mm | 0.50 mm | 0.70 mm |

## 模型准备

### 支持的文件格式

| 格式 | 说明 | 导入 |
|------|------|------|
| STL | 标准网格 | 完全支持 |
| OBJ | 带材质的网格 | 完全支持 |
| 3MF | 现代格式 | 完全支持 |
| STEP | CAD 格式 | 通过转换 |
| AMF | 增材制造 | 完全支持 |

### 模型操作

| 操作 | 工具 | 快捷键 |
|------|------|--------|
| 移动 | 选择工具 | M |
| 旋转 | 旋转工具 | R |
| 缩放 | 缩放工具 | S |
| 镜像 | 翻转工具 | - |
| 平放 | 自动定向 | - |
| 切割 | 切割工具 | - |

### 自动定向

| 功能 | 说明 |
|------|------|
| 最小化支撑 | 定向以减少悬垂 |
| 最小化层时间 | 优化速度 |
| 最佳表面 | 定向以保证质量 |

## 支撑结构

### 支撑类型

| 类型 | 说明 | 最佳用途 |
|------|------|----------|
| 普通 | 基于网格 | 简单零件 |
| 树状 | 有机分支 | 复杂几何 |
| 混合 | 组合 | 混合特征 |
| 手绘 | 手动放置 | 选择性支撑 |

### 树状支撑设置

| 设置 | 说明 | 默认值 |
|------|------|--------|
| 分支角度 | 最大分支角度 | 40° |
| 分支距离 | 分支间距 | 1 mm |
| 顶端直径 | 分支端点大小 | 0.8 mm |
| 主干直径 | 主支撑柱 | 2 mm |
| 分支密度 | 支撑厚度 | 15% |

### 支撑设置

| 设置 | 说明 | 值 |
|------|------|-----|
| 悬垂角度 | 需要支撑的阈值 | 45° |
| 接触 Z 距离 | 与模型的间隙 | 0.2 mm |
| 接触层 | 顶部支撑层 | 2 |
| 接触层密度 | 支撑顶密度 | 50% |

## 校准工具

### 内置校准测试

| 测试 | 用途 | 结果 |
|------|------|------|
| 温度塔 | 最佳温度 | 最佳温度范围 |
| 流量率 | 挤出校准 | 流量比 |
| Pressure advance | 拐角质量 | PA 值 |
| 回抽 | 拉丝测试 | 距离/速度 |
| 最大流量 | 体积限制 | mm³/s |
| VFA | 垂直精细伪影 | 速度限制 |
| Input shaper | 共振补偿 | 频率 |

### 运行校准

| 步骤 | 操作 |
|------|------|
| 1 | 打开校准菜单 |
| 2 | 选择测试类型 |
| 3 | 配置参数 |
| 4 | 生成测试打印 |
| 5 | 打印并评估 |
| 6 | 将结果应用到配置文件 |

### 校准工作流

| 测试 | 时机 | 频率 |
|------|------|------|
| 温度 | 新耗材 | 每卷 |
| 流量率 | 新耗材 | 每卷 |
| Pressure advance | 新耗材 | 每卷 |
| 回抽 | 拉丝问题 | 按需 |
| Input shaper | 打印质量问题 | 每月 |

## 高级功能

### 自适应层高

| 功能 | 说明 |
|------|------|
| 自动模式 | 自动选择高度 |
| 手动模式 | 绘制高度 |
| 最小高度 | 最矮层 |
| 最大高度 | 最高层 |
| 步长 | 高度增量 |

### 接缝绘制

| 选项 | 说明 |
|------|------|
| 最近 | 最接近上一位置 |
| 对齐 | 一致放置 |
| 随机 | 每层随机 |
| 绘制 | 手动接缝放置 |

### 多材料打印

| 功能 | 说明 |
|------|------|
| AMS 支持 | 自动材料系统 |
| MMU 支持 | 多材料单元 |
| 耗材绘制 | 将材料分配到区域 |
| 清洗塔 | 清洁换料 |
| 擦拭塔 | 预备耗材 |

### 可变打印设置

| 功能 | 说明 |
|------|------|
| 修改器网格 | 将设置应用到区域 |
| 高度范围 | 按层高设置 |
| 层相关 | 每层更改设置 |
| 区域特定 | 每区域不同设置 |

### 网络功能

| 功能 | 说明 |
|------|------|
| 打印机发现 | 自动检测网络打印机 |
| 远程监控 | 查看打印状态 |
| 文件传输 | 无线发送 G-code |
| 摄像头视图 | 实时摄像头画面 |

### G-code 预览

| 视图 | 说明 |
|------|------|
| 线类型 | 按特征类型着色 |
| 速度 | 按打印速度着色 |
| 层 | 查看单个层 |
| 路径 | 显示打印路径 |

### 特征颜色编码

| 颜色 | 特征 |
|------|------|
| 黄色 | 外壳 |
| 橙色 | 内壳 |
| 绿色 | 填充 |
| 蓝色 | 支撑 |
| 青色 | 支撑接触层 |
| 红色 | 桥接 |
| 白色 | 移动 |

## 键盘快捷键

| 快捷键 | 操作 |
|--------|------|
| Ctrl+I | 导入模型 |
| Ctrl+L | 切片打印板 |
| Ctrl+P | 打印打印板 |
| Ctrl+Shift+P | 发送到打印机 |
| Tab | 切换预览 |
| R | 旋转工具 |
| S | 缩放工具 |
| M | 移动工具 |

## 总结

OrcaSlicer 提供了先进的切片功能，内置校准工具并支持广泛的 3D 打印机。其自动校准功能、树状支撑和多材料支持使其适合寻求简单设置的初学者和需要精确控制打印设置的有经验用户。


---

## 来源：firmware.md

## 简介

Klipper 是一款 3D 打印机固件，结合了主机计算机（如 Raspberry Pi）的处理能力和微控制器的实时能力。它将计算卸载到主机，从而实现传统固件无法支持的功能。

| 属性 | 详情 |
|----------|--------|
| 仓库 | Klipper3d/klipper |
| 许可证 | GPL-3.0 |
| 语言 | C, Python |
| 主机 | Linux (Raspberry Pi, PC) |
| MCU | AVR, STM32, RP2040 等 |

## Klipper 工作原理

Klipper 使用两部分架构。

| 组件 | 角色 |
|-----------|------|
| Host (Linux) | 运行运动学、G-code 处理和 Web 界面 |
| MCU（打印机主板） | 执行实时步进生成和读取传感器 |

主机软件计算步进电机运动，并通过串行或 USB 连接向 MCU 发送定时命令。

## 主要功能

| 功能 | 描述 |
|---------|-------------|
| 高步进速率 | 实现比传统固件更高的步进速率 |
| 精确定时 | Linux 主机提供微秒级精确定时 |
| Input Shaper（输入整形） | 减少振铃和重影伪影 |
| Pressure Advance（压力补偿） | 补偿耗材压力变化 |
| Firmware Retraction（固件回抽） | 软件控制的回抽 |
| Bed Mesh Leveling（床网调平） | 自动热床补偿 |
| Multi-MCU Support（多 MCU 支持） | 控制多个微控制器 |
| Macros（宏） | 用 Jinja2 编写的自定义 G-code 命令 |

## 安装

### 前提条件

| 要求 | 描述 |
|-------------|-------------|
| 主机计算机 | Raspberry Pi 3+ 或 Linux PC |
| MicroSD 卡 | 8 GB 或更大，用于主机操作系统 |
| 网络 | Wi-Fi 或以太网连接 |
| 打印机主板 | 兼容的微控制器 |

### 第 1 步：在主机上安装

```bash
# 克隆仓库
git clone https://github.com/Klipper3d/klipper
cd klipper

# 运行安装脚本
./scripts/install-octopi.sh
```

### 第 2 步：配置 MCU

```bash
# 配置固件
make menuconfig

# 构建固件
make

# 刷写固件（因主板而异）
make flash FLASH_DEVICE=/dev/ttyUSB0
```

### 第 3 步：配置打印机

编辑配置文件 `~/printer_data/config/printer.cfg`。

## 配置

### 基本打印机配置

```ini
[printer]
kinematics: cartesian
max_velocity: 300
max_accel: 3000
max_z_velocity: 5
max_z_accel: 100

[stepper_x]
step_pin: PF0
dir_pin: PF1
enable_pin: !PD7
microsteps: 16
rotation_distance: 40
endstop_pin: ^PE5
position_endstop: 0
position_max: 220

[stepper_y]
step_pin: PF6
dir_pin: !PF7
enable_pin: !PF2
microsteps: 16
rotation_distance: 40
endstop_pin: ^PJ1
position_endstop: 0
position_max: 220

[stepper_z]
step_pin: PL3
dir_pin: PL1
enable_pin: !PK0
microsteps: 16
rotation_distance: 8
endstop_pin: ^PD3
position_endstop: 0.5
position_max: 250

[extruder]
step_pin: PA4
dir_pin: !PA6
enable_pin: !PA2
microsteps: 16
rotation_distance: 33.500
nozzle_diameter: 0.400
filament_diameter: 1.750
heater_pin: PB4
sensor_type: ATC Semitec 104NT-4-R025H42G
sensor_pin: PK5
min_temp: 0
max_temp: 260

[heater_bed]
heater_pin: PH5
sensor_type: EPCOS 100K B57560G104F
sensor_pin: PK6
min_temp: 0
max_temp: 130
```

### 运动学类型

| 类型 | 描述 |
|------|-------------|
| cartesian | 标准 X/Y/Z 运动（如 Ender 3） |
| corexy | CoreXY 运动系统（如 Voron） |
| delta | Delta 打印机几何 |
| rotary_delta | 旋转 Delta 机构 |
| polar | 极坐标系统 |
| winch | 绳索驱动系统 |
| none | 无运动学（仅手动控制） |

## 温度配置

### 热敏电阻类型

| 类型 | 描述 |
|------|-------------|
| EPCOS 100K | 常见 NTC 热敏电阻 |
| ATC Semitec 104GT-2 | 高温热敏电阻 |
| SliceEngineering 450C | 高温热电偶 |
| PT100 | 铂金 RTD 传感器 |
| PT1000 | 铂金 RTD 传感器（更高电阻） |

### PID 调参

```bash
# 调整热端 PID
PID_CALIBRATE HEATER=extruder TARGET=210

# 调整热床 PID
PID_CALIBRATE HEATER=heater_bed TARGET=60

# 保存配置
SAVE_CONFIG
```

## Input Shaper（输入整形）

输入整形通过补偿机械共振来减少振铃伪影。

### 校准

```bash
# 测量共振频率
SHAPER_CALIBRATE

# 测试特定轴
SHAPER_CALIBRATE AXIS=X
SHAPER_CALIBRATE AXIS=Y
```

### 整形器类型

| 类型 | 描述 |
|------|-------------|
| mzv | 适用于大多数打印机 |
| ei | 更适合较高频率 |
| 2hump_ei | 用于多个共振峰 |
| 3hump_ei | 用于复杂的共振模式 |

## Pressure Advance（压力补偿）

压力补偿在加速和减速期间补偿耗材流动的延迟。

```ini
[extruder]
pressure_advance: 0.04
pressure_advance_smooth_time: 0.040
```

### 校准

```bash
# 运行测试图案
TUNING_TOWER COMMAND=SET_VELOCITY_LIMIT PARAMETER=VELOCITY START=50 FACTOR=2
```

## Bed Mesh Leveling（床网调平）

```ini
[bed_mesh]
probe_count: 5, 5
speed: 120
horizontal_move_z: 5
mesh_min: 30, 30
mesh_max: 190, 190
```

### 使用

```bash
# 探测热床
BED_MESH_CALIBRATE

# 加载已保存的网格
BED_MESH LOAD=default

# 清除网格
BED_MESH CLEAR
```

## Web 界面

Klipper 与 Web 界面配合使用，实现远程控制。

| 界面 | 描述 |
|-----------|-------------|
| Mainsail | 现代、响应式 Web 界面 |
| Fluidd | 功能丰富的 Web 界面 |
| OctoPrint | 基于插件的 Web 界面 |

## 宏

自定义宏扩展了 Klipper 的功能。

```ini
[gcode_macro START_PRINT]
gcode:
    G28                           ; 归位所有轴
    BED_MESH_CALIBRATE            ; 热床调平
    G1 Z5 F3000                  ; 抬高喷嘴
    M109 S{params.EXTRUDER_TEMP} ; 等待热端
    M190 S{params.BED_TEMP}      ; 等待热床

[gcode_macro END_PRINT]
gcode:
    M104 S0                      ; 关闭热端
    M140 S0                      ; 关闭热床
    G91                          ; 相对定位
    G1 Z10 F3000                ; 抬高喷嘴
    G90                          ; 绝对定位
    G1 X0 Y200 F5000            ; 展示打印件
    M84                          ; 禁用步进电机
```

## 故障排除

| 问题 | 解决方案 |
|-------|----------|
| MCU 连接错误 | 检查 USB 线和串口 |
| 温度失控 | 验证热敏电阻接线 |
| 层偏移 | 降低加速度或检查皮带张力 |
| 附着力差 | 校准 Z 偏移和床网 |
| 拉丝 | 调整回抽和压力补偿 |

## 与传统固件的比较

| 方面 | Klipper | Marlin |
|--------|---------|--------|
| 处理 | 主机 CPU | 仅 MCU |
| 步进速率 | 非常高 | 受 MCU 速度限制 |
| 配置 | 文本文件，热重载 | 重新编译固件 |
| Input Shaper | 内置 | 手动或不可用 |
| Web 界面 | 原生支持 | 需要 OctoPrint |
| 可扩展性 | Python 宏 | 有限 |

## 结论

Klipper 为 3D 打印机控制提供了一个强大而灵活的平台。其架构利用主机计算机的处理能力来提供改进打印质量和简化配置的高级功能。


---

## 来源：printer.md

## 简介

Marlin 是使用最广泛的开源 3D 打印机固件。它运行在基于 AVR 和 ARM 的微控制器上，支持大量打印机配置。

| 属性 | 详情 |
|----------|--------|
| 仓库 | MarlinFirmware/Marlin |
| 许可证 | GPL-3.0 |
| 语言 | C++ |
| 平台 | AVR (ATmega), ARM (STM32, SAM, LPC, ESP32) |
| IDE | PlatformIO, Arduino IDE |

## 主要功能

| 功能 | 描述 |
|---------|-------------|
| Cartesian Support | 标准 XYZ 运动 |
| Delta Support | Delta 打印机运动学 |
| CoreXY Support | CoreXY 运动系统 |
| Auto Bed Leveling | 基于探针的热床补偿 |
| Linear Advance | 压力补偿 |
| S-Curve Acceleration | 更平滑的运动曲线 |
| Trinamic Support | TMC 步进驱动集成 |
| Dual Extrusion | 多挤出头支持 |
| LCD Support | 各种显示器类型 |
| SD Card | 从 SD 卡打印 |

## 支持的硬件

### 微控制器板

| 板 | MCU | 备注 |
|-------|-----|-------|
| RAMPS 1.4 | ATmega2560 | 经典 Arduino 板 |
| SKR 1.4 | LPC1768 | 流行的 32 位板 |
| SKR 2.0 | STM32 | 现代 32 位板 |
| SKR Mini E3 | STM32 | Ender 3 直接替换升级 |
| MKS Robin Nano | STM32 | 彩色触摸屏板 |
| Duet 2 | SAM4E8E | 高端板 |
| Einsy Rambo | ATmega2560 | 原装 Prusa 板 |

### 步进驱动

| 驱动 | 特性 |
|--------|----------|
| A4988 | 基础，1/16 微步 |
| DRV8825 | 1/32 微步 |
| TMC2208 | 静音，UART 模式 |
| TMC2209 | 静音，无传感器归位 |
| TMC2226 | TMC2209 变体 |
| TMC5160 | 大电流，SPI 模式 |

## 安装

### 前提条件

| 工具 | 描述 |
|------|-------------|
| PlatformIO | 构建系统（推荐） |
| Arduino IDE | 替代构建环境 |
| VS Code | 带 PlatformIO 扩展的代码编辑器 |
| Git | 版本控制 |

### 使用 PlatformIO 构建

```bash
# 克隆仓库
git clone https://github.com/MarlinFirmware/Marlin.git
cd Marlin

# 编辑配置文件
# Configuration.h
# Configuration_adv.h

# 为您的板构建
pio run -e mega2560

# 上传到打印机
pio run -e mega2560 --target upload
```

### 使用 Arduino IDE 构建

1. 安装 Arduino IDE。
2. 添加您的 MCU 的板定义。
3. 打开 Marlin.ino。
4. 选择正确的板和端口。
5. 编辑 Configuration.h 和 Configuration_adv.h。
6. 点击上传。

## 配置

### Configuration.h

主配置文件定义打印机硬件。

| 部分 | 设置 |
|---------|----------|
| Serial（串口） | 串口配置 |
| Motherboard（主板） | 板类型定义 |
| Temperature（温度） | 热敏电阻类型和 PID 设置 |
| Extruder（挤出头） | 挤出头数量和配置 |
| Bed Size（热床尺寸） | 打印区域尺寸 |
| Kinematics（运动学） | 运动系统类型 |
| Auto Leveling（自动调平） | 热床探针配置 |
| LCD | 显示器类型选择 |

### 基本配置

```cpp
// 主板
#define MOTHERBOARD BOARD_BTT_SKR_V1_4

// 串口
#define SERIAL_PORT 0
#define BAUDRATE 115200

// 挤出头
#define EXTRUDERS 1
#define DEFAULT_NOMINAL_FILAMENT_DIA 1.75

// 热床尺寸
#define X_BED_SIZE 220
#define Y_BED_SIZE 220
#define Z_MAX_POS 250

// 温度
#define TEMP_SENSOR_0 1    // 热端热敏电阻类型
#define TEMP_SENSOR_BED 1  // 热床热敏电阻类型

// PID 设置
#define PIDTEMP
#define DEFAULT_Kp 22.2
#define DEFAULT_Ki 1.08
#define DEFAULT_Kd 114
```

### Configuration_adv.h

用于微调的高级设置。

| 部分 | 设置 |
|---------|----------|
| Thermal（热保护） | 热失控保护 |
| Stepper（步进） | 驱动特定设置 |
| LCD | 显示器自定义 |
| SD Card | SD 卡支持 |
| WiFi | 网络连接 |
| Trinamic | TMC 驱动配置 |

## 自动热床调平

### 探针类型

| 探针 | 描述 |
|-------|-------------|
| BLTouch | 机械可伸缩探针 |
| Inductive（电感） | 电磁接近传感器 |
| Capacitive（电容） | 电容接近传感器 |
| Piezo（压电） | 压力敏感传感器 |
| Strain Gauge（应变片） | 力敏感传感器 |

### 调平方法

| 方法 | 描述 |
|--------|-------------|
| Linear（线性） | 3 点调平 |
| Bilinear（双线性） | 基于网格的调平 |
| Unified Bed Mesh（统一床网） | 高级网格调平 |
| 3-Point（3 点） | 三角调平 |

### 配置

```cpp
// 启用自动热床调平
#define AUTO_BED_LEVELING_BILINEAR

// 探针设置
#define BLTOUCH
#define Z_PROBE_OFFSET_FROM_EXTRUDER { 0, 0, -1.5 }

// 热床调平网格
#define GRID_MAX_POINTS_X 5
#define GRID_MAX_POINTS_Y 5

// 探针边距
#define LEFT_PROBE_BED_POSITION 30
#define RIGHT_PROBE_BED_POSITION 190
#define FRONT_PROBE_BED_POSITION 30
#define BACK_PROBE_BED_POSITION 190
```

## Linear Advance（线性推进）

线性推进在加速和减速期间补偿喷嘴中的压力变化。

```cpp
#define LIN_ADVANCE
#define LIN_ADVANCE_K 0.0
```

### 校准

1. 打印线性推进校准图案。
2. 根据结果调整 K 值。
3. 直驱挤出头使用较低的 K 值。
4. Bowden 挤出头使用较高的 K 值。

| 挤出头类型 | 典型 K 值 |
|---------------|-----------------|
| Direct Drive（直驱） | 0.0 - 0.2 |
| Bowden (short)（短） | 0.2 - 0.7 |
| Bowden (long)（长） | 0.7 - 2.0 |

## S-Curve Acceleration（S 曲线加速度）

S 曲线加速度提供比梯形加速度更平滑的运动。

```cpp
#define S_CURVE_ACCELERATION
```

## Trinamic 驱动配置

### TMC2209 UART 配置

```cpp
#define X_DRIVER_TYPE  TMC2209
#define Y_DRIVER_TYPE  TMC2209
#define Z_DRIVER_TYPE  TMC2209
#define E0_DRIVER_TYPE TMC2209

// UART 连接
#define X_SLAVE_ADDRESS  0
#define Y_SLAVE_ADDRESS  0
#define Z_SLAVE_ADDRESS  0
#define E0_SLAVE_ADDRESS 0

// StealthChop（静音模式）
#define STEALTHCHOP_XY
#define STEALTHCHOP_Z

// 无传感器归位
#define SENSORLESS_HOMING
#define X_STALL_SENSITIVITY  80
#define Y_STALL_SENSITIVITY  80
```

### 电流设置

| 轴 | 典型电流 (mA) |
|------|---------------------|
| X | 800 |
| Y | 800 |
| Z | 800 |
| E0 | 600 |

## LCD 和显示器

### 支持的显示器

| 显示器 | 类型 |
|---------|------|
| RepRapDiscount 12864 | 字符 LCD |
| RepRapDiscount Full Graphic | 单色图形 |
| TFT Color | 彩色触摸屏 |
| DWIN T5 | DGUS 触摸屏 |
| Fysetc Mini 12864 | RGB 背光 |

## G-Code 命令

### 运动命令

| 命令 | 描述 |
|---------|-------------|
| G28 | 归位所有轴 |
| G29 | 自动热床调平 |
| G1 | 线性移动 |
| G0 | 快速移动 |
| G92 | 设置位置 |

### 温度命令

| 命令 | 描述 |
|---------|-------------|
| M104 | 设置热端温度 |
| M109 | 等待热端温度 |
| M140 | 设置热床温度 |
| M190 | 等待热床温度 |
| M106 | 设置风扇速度 |

### 配置命令

| 命令 | 描述 |
|---------|-------------|
| M500 | 保存设置到 EEPROM |
| M501 | 从 EEPROM 加载设置 |
| M502 | 恢复出厂默认 |
| M503 | 报告当前设置 |
| M851 | 设置 Z 探针偏移 |

## PID 调参

```bash
# 调整热端 PID
M303 E0 C8 S210

# 调整热床 PID
M303 E-1 C8 S60

# 保存 PID 值
M301 P22.2 I1.08 D114
M500
```

## 故障排除

| 问题 | 解决方案 |
|-------|----------|
| 热失控 | 检查热敏电阻接线 |
| 层偏移 | 检查皮带张力和驱动电流 |
| 附着力差 | 校准 Z 偏移和热床水平 |
| 拉丝 | 调整回抽和温度 |
| 欠挤出 | 校准 e-steps 和流量率 |
| 过挤出 | 降低流量率 |

## 技巧和最佳实践

| 技巧 | 说明 |
|-----|-------------|
| 备份配置 | 保存配置文件的副本 |
| 启用热保护 | 安全功能，始终保持启用 |
| 使用 S 曲线 | 更平滑的运动减少伪影 |
| 调参 PID | 稳定的温度提高打印质量 |
| 逐步测试 | 一次只更改一个设置 |
| 使用版本控制 | 用 Git 跟踪配置更改 |

## 与 Klipper 的比较

| 方面 | Marlin | Klipper |
|--------|--------|---------|
| 处理 | 仅 MCU | 主机 + MCU |
| 配置 | 重新编译固件 | 编辑文本文件，重启 |
| 步进速率 | 受 MCU 限制 | 非常高（主机 CPU） |
| Web 界面 | 需要 OctoPrint | 内置支持 |
| Input Shaper | 手动校准 | 自动校准 |
| 社区 | 最大的用户群 | 增长中的社区 |

## 结论

Marlin 是最成熟、支持最广泛的 3D 打印机固件。其广泛的配置选项和广泛的硬件支持使其适用于几乎任何 3D 打印机设计，从入门级机器到高级自定义构建。


---

## 来源：pcb.md

## 简介

Fritzing 是一款开源电子设计工具，支持电路设计、PCB 布局和面包板可视化。它被爱好者、教育者和创客广泛用于记录和分享电子项目。

| 属性 | 详情 |
|----------|--------|
| 仓库 | Fritzing/fritzing-app |
| 许可证 | GPL-3.0 |
| 语言 | C++, Qt |
| 平台 | Windows, macOS, Linux |
| 文件格式 | .fzz（Fritzing 项目） |

## 安装

### 从源码安装

```bash
git clone https://github.com/fritzing/fritzing-app.git
cd fritzing-app
git submodule update --init
qmake
make
```

### 预编译二进制文件

预编译二进制文件可从 Fritzing 网站获取。

## 三种视图

Fritzing 提供同一电路的三种同步视图。

| 视图 | 用途 |
|------|---------|
| Breadboard（面包板） | 物理面包板布局的可视化表示 |
| Schematic（原理图） | 用于分析的传统电路原理图 |
| PCB | 用于制造的印刷电路板布局 |

在一个视图中的更改会自动反映在其他两个视图中。

## 核心工作流程

### 第 1 步：选择零件

使用零件面板搜索并将元件拖到画布上。

| 元件类别 | 示例 |
|--------------------|----------|
| 电阻 | 直插式、贴片式、可变 |
| 电容 | 陶瓷、电解、可变 |
| 集成电路 | ATmega, ESP32, NE555 |
| 连接器 | 排针, USB, 圆形电源插孔 |
| 模块 | Arduino, Raspberry Pi, 传感器 |
| 有源器件 | 晶体管、二极管、LED |

### 第 2 步：放置和连线

1. 将元件从面板拖到画布上。
2. 单击一个引脚并拖到另一个引脚以创建导线。
3. 使用布线工具清理导线路径。
4. 添加标签和注释以提高清晰度。

### 第 3 步：设计 PCB

切换到 PCB 视图，在电路板上排列元件。

| PCB 参数 | 描述 |
|---------------|-------------|
| Board Size（板尺寸） | 定义 PCB 的宽度和高度 |
| Layer Count（层数） | 单面或双面 |
| Trace Width（走线宽度） | 铜走线的宽度 |
| Clearance（间距） | 走线之间的最小距离 |
| Via Size（过孔尺寸） | 通孔过孔的直径 |

### 第 4 步：导出用于制造

| 导出格式 | 用途 |
|---------------|----------|
| Gerber | PCB 制造商的标准格式 |
| SVG | 可视化文档 |
| PDF | 打印和文档 |
| PNG | 在线分享图片 |
| BOM | 采购用物料清单 |

## 使用零件编辑器

零件编辑器允许用户创建标准库中未包含的自定义元件。

### 创建自定义零件

1. 从菜单打开零件编辑器。
2. 为每个视图导入 SVG 图片（面包板、原理图、PCB）。
3. 定义连接器引脚及其位置。
4. 设置元数据，如系列、属性和标签。
5. 将零件保存到个人库。

| 视图 | 所需 SVG |
|------|-------------|
| Breadboard（面包板） | 逼真的俯视图 |
| Schematic（原理图） | 标准原理图符号 |
| PCB | 带焊盘布局的封装 |

## PCB 设计规则

遵循正确的设计规则可确保 PCB 功能正常且可制造。

| 规则 | 推荐值 |
|------|-------------------|
| 最小走线宽度 | 0.25 mm (10 mil) |
| 最小间距 | 0.25 mm (10 mil) |
| 最小钻孔尺寸 | 0.3 mm (12 mil) |
| 铺铜间距 | 0.5 mm |
| 板边间距 | 1.0 mm |

## 自动布线

Fritzing 包含一个自动布线器，尝试自动连接所有未布线的走线。

| 自动布线设置 | 描述 |
|--------------------|-------------|
| Router Type（布线器类型） | 选择布线算法 |
| Max Retries（最大重试次数） | 布线尝试次数 |
| Via Usage（过孔使用） | 允许或禁止过孔 |
| Preferred Layer（首选层） | 顶层或底层偏好 |

自动布线器对简单电路板效果良好。对于复杂设计，建议手动布线。

## 成功 PCB 设计的技巧

| 技巧 | 说明 |
|-----|-------------|
| 从原理图开始 | 在布局前确保电路正确 |
| 合理放置元件 | 将相关元件分组在一起 |
| 最小化走线长度 | 较短的走线可减少噪声和电阻 |
| 使用地平面 | 坚实的地层可改善信号完整性 |
| 检查 DRC | 导出前运行设计规则检查 |
| 查看 Gerber 文件 | 使用 Gerber 查看器验证输出 |

## 面包板原型制作

Fritzing 的面包板视图对于记录原型构建特别有用。

| 功能 | 优势 |
|---------|---------|
| 彩色编码导线 | 便于视觉识别 |
| 逼真的元件 | 与实物零件匹配 |
| 跳线管理 | 整理导线布线 |
| Arduino 集成 | 直接支持 Arduino 板 |

## 分享和社区

| 资源 | 描述 |
|----------|-------------|
| Fritzing 网站 | 下载零件和分享项目 |
| 社区论坛 | 提问和获取帮助 |
| 零件库 | 可搜索的自定义零件数据库 |
| 项目示例 | 从社区项目中学习 |

## 结论

Fritzing 对于任何从事电子工作的人来说都是一个有价值的工具，无论是构建第一个电路的初学者还是为制造创建 PCB 的经验丰富的设计师。其三视图方法弥合了原型制作和生产之间的差距。


---

## 来源：kicad.md

## 简介

KiCad 是一款免费、开源的电子设计自动化套件。它包含原理图捕获、PCB 布局、3D 可视化和制造文件生成工具。

| 属性 | 详情 |
|----------|--------|
| 仓库 | KiCad/kicad-source-mirror |
| 许可证 | GPL-3.0 |
| 语言 | C++, Python |
| 平台 | Windows, macOS, Linux |
| 文件格式 | .kicad_sch, .kicad_pcb, .kicad_pro |

## 安装

### Linux

```bash
# Ubuntu/Debian
sudo apt install kicad

# Fedora
sudo dnf install kicad

# Flatpak
flatpak install org.kicad.KiCad
```

### macOS 和 Windows

从 KiCad 官方网站下载。

## 套件组件

| 工具 | 用途 |
|------|---------|
| KiCad Project Manager | 管理项目文件和启动工具 |
| Eeschema | 原理图编辑器 |
| PCBnew | PCB 布局编辑器 |
| Symbol Editor | 创建和编辑原理图符号 |
| Footprint Editor | 创建和编辑 PCB 封装 |
| 3D Viewer | 3D 可视化 PCB |
| Gerber Viewer | 预览制造文件 |
| Bitmap to Component | 将图片转换为封装 |
| Calculator | 电气和 PCB 计算器 |

## 项目结构

| 文件 | 描述 |
|------|-------------|
| .kicad_pro | 项目文件 |
| .kicad_sch | 原理图文件 |
| .kicad_pcb | PCB 布局文件 |
| .kicad_sym | 符号库 |
| .kicad_mod | 封装模块 |
| .kicad_dru | 设计规则文件 |

## 原理图设计（Eeschema）

### 工作流程

1. 创建新项目。
2. 打开原理图编辑器。
3. 从符号库放置元件。
4. 将元件连线。
5. 为符号分配封装。
6. 运行电气规则检查（ERC）。
7. 生成网表。

### 原理图工具

| 工具 | 快捷键 | 描述 |
|------|----------|-------------|
| Place Symbol（放置符号） | A | 添加元件 |
| Place Wire（放置导线） | W | 绘制导线 |
| Place Bus（放置总线） | B | 绘制总线 |
| Place Power（放置电源） | P | 添加电源符号 |
| Place Net Label（放置网络标签） | L | 添加网络标签 |
| Place Junction（放置节点） | J | 添加导线节点 |
| Annotate（标注） | | 分配参考标识符 |
| ERC | | 运行电气规则检查 |

### 符号库

| 库 | 内容 |
|---------|----------|
| Device | 电阻、电容、电感 |
| Connector | 排针、插头、插座 |
| MCU | 微控制器 |
| Power | 电源符号和稳压器 |
| 74xx | 7400 系列逻辑 IC |
| Amplifier | 运算放大器 |

## PCB 布局（PCBnew）

### 工作流程

1. 从原理图导入网表。
2. 定义电路板轮廓。
3. 在电路板上放置元件。
4. 配置设计规则。
5. 手动或使用自动布线器布线。
6. 添加铜填充（地平面）。
7. 运行设计规则检查（DRC）。
8. 生成制造文件。

### PCB 工具

| 工具 | 快捷键 | 描述 |
|------|----------|-------------|
| Place Footprint（放置封装） | F | 添加封装 |
| Route Tracks（布线） | X | 手动布线 |
| Add Via（添加过孔） | V | 放置过孔 |
| Draw Zone（绘制区域） | Z | 创建铺铜区域 |
| Draw Edge（绘制边缘） | | 定义电路板轮廓 |
| Measure（测量） | | 测量距离 |
| DRC | | 运行设计规则检查 |

### 层叠结构

| 层 | 描述 |
|-------|-------------|
| F.Cu | 前铜层 |
| B.Cu | 后铜层 |
| F.SilkS | 前丝印层 |
| B.SilkS | 后丝印层 |
| F.Mask | 前阻焊层 |
| B.Mask | 后阻焊层 |
| Edge.Cuts | 电路板轮廓 |
| F.Paste | 前锡膏层 |
| B.Paste | 后锡膏层 |

## 设计规则

| 规则 | 典型值 |
|------|---------------|
| 最小走线宽度 | 0.2 mm (8 mil) |
| 最小间距 | 0.2 mm (8 mil) |
| 最小钻孔直径 | 0.3 mm (12 mil) |
| 最小过孔环宽 | 0.15 mm (6 mil) |
| 铺铜间距 | 0.5 mm |
| 板边间距 | 1.0 mm |

## 3D 可视化

KiCad 包含内置的 3D 查看器，可以渲染带元件的 PCB。

| 功能 | 描述 |
|---------|-------------|
| Realistic Rendering（逼真渲染） | 显示元件形状和颜色 |
| Raytracing（光线追踪） | 高质量渲染模式 |
| VRML Export（VRML 导出） | 导出用于外部 3D 工具 |
| Rotation（旋转） | 从任意角度旋转视图 |
| Cross-Section（截面） | 查看内部层 |

## 制造输出

### Gerber 文件

| 文件 | 层 |
|------|-------|
| F.Cu.gbr | 前铜层 |
| B.Cu.gbr | 后铜层 |
| F.SilkS.gbr | 前丝印层 |
| F.Mask.gbr | 前阻焊层 |
| Edge.Cuts.gbr | 电路板轮廓 |

### 其他输出

| 输出 | 描述 |
|--------|-------------|
| Drill Files（钻孔文件） | Excellon 格式钻孔数据 |
| BOM | 物料清单（CSV） |
| Pick and Place（贴片） | 装配用元件放置 |
| Netlist（网表） | 用于测试和验证 |

## Python 脚本

KiCad 通过其 API 支持 Python 脚本。

```python
import pcbnew

board = pcbnew.GetBoard()
for footprint in board.GetFootprints():
    print(footprint.GetReference(), footprint.GetValue())
```

## 技巧和最佳实践

| 技巧 | 说明 |
|-----|-------------|
| 使用层次化图页 | 组织复杂原理图 |
| 尽早定义设计规则 | 在布线前设置走线宽度和间距 |
| 使用地平面 | 改善信号完整性并减少 EMI |
| 经常检查 DRC | 在制造前发现错误 |
| 使用 3D 查看器 | 验证元件放置和间距 |
| 保存自定义封装 | 建立个人库以供重用 |

## 社区和资源

| 资源 | 描述 |
|----------|-------------|
| 官方文档 | 全面的用户手册 |
| 论坛 | 社区支持和讨论 |
| 库 | 官方元件库 |
| 教程 | 视频和文本教程 |
| 插件 | 第三方扩展 |

## 结论

KiCad 是一款专业级的 PCB 设计套件，提供了设计和制造印刷电路板所需的所有工具。其开源特性和活跃的社区使其成为爱好者和专业人士的绝佳选择。


---

## 来源：cnc.md

## 简介

GRBL 是一个开源的嵌入式高性能 G-code 解析器和 CNC 铣削控制器。它运行在基于 Arduino 的开发板上，将 G-code 命令转换为精确的步进电机运动，适用于 CNC 机床、激光雕刻机和 3D 打印机。

## 支持的硬件

| 开发板 | 处理器 | 轴数 | 最大步/秒 | 最佳场景 |
|--------|--------|------|----------|---------|
| Arduino Uno | ATmega328P | 3 | 30,000 | 入门级 CNC |
| Arduino Mega | ATmega2560 | 3+ | 30,000 | 扩展功能 |
| ESP32 | Xtensa | 3+ | 100,000+ | 高速，WiFi |
| STM32 | ARM Cortex | 3+ | 100,000+ | 专业用途 |

## 系统要求

| 组件 | 最低配置 | 推荐配置 |
|------|---------|---------|
| 控制器 | Arduino Uno | Arduino Mega 或 ESP32 |
| 步进驱动 | A4988 | TMC2209 或 DM542 |
| 电源 | 12V 5A | 24V 10A |
| 连接 | USB | USB 或串口 |

## 安装

### 从源码编译

```bash
git clone https://github.com/gnea/grbl.git
cd grbl
# 在 Arduino IDE 中打开
# 选择开发板：Arduino Uno
# 上传 sketch
```

### 预编译固件

```bash
# 从 releases 下载 .hex 文件
# 通过 XLoader 或 avrdude 上传
avrdude -p atmega328p -c arduino -P /dev/ttyACM0 \
  -U flash:w:grbl_v1.1f.hex:i
```

### ESP32 版本（grblHAL）

```bash
# 使用 PlatformIO
git clone https://github.com/grblHAL/ESP32.git
cd ESP32
pio run -t upload
```

## G-Code 参考

### 运动命令

| 代码 | 说明 | 示例 |
|------|------|------|
| G0 | 快速移动（最快速度） | `G0 X10 Y20` |
| G1 | 直线插补 | `G1 X10 Y20 F500` |
| G2 | 顺时针圆弧 | `G2 X10 Y10 R5` |
| G3 | 逆时针圆弧 | `G3 X10 Y10 R5` |
| G28 | 回原点 | `G28` |
| G90 | 绝对定位 | `G90` |
| G91 | 相对定位 | `G91` |
| G92 | 设置位置 | `G92 X0 Y0 Z0` |

### 进给速度命令

| 代码 | 说明 | 示例 |
|------|------|------|
| F | 设置进给速度 | `F500`（mm/min） |
| G0 | 快速（无需进给） | `G0 X10` |
| G1 | 使用设定的进给速度 | `G1 X10 F500` |

### 主轴和冷却液

| 代码 | 说明 | 示例 |
|------|------|------|
| M3 | 主轴正转 | `M3 S1000` |
| M5 | 主轴停止 | `M5` |
| M7 | 雾化冷却液开 | `M7` |
| M8 | 大流量冷却液开 | `M8` |
| M9 | 冷却液关 | `M9` |
| S | 设置主轴转速 | `S12000`（RPM） |

### 程序控制

| 代码 | 说明 | 示例 |
|------|------|------|
| M0 | 程序暂停 | `M0` |
| M2 | 程序结束 | `M2` |
| M30 | 程序结束并回卷 | `M30` |

## GRBL 设置

### 查看和更改设置

```bash
# 查看所有设置
$$

# 更改设置
$0=10       # 步进脉冲时间（微秒）
$1=25       # 步进空闲延迟（毫秒）
$2=0        # 步进端口反转掩码
$3=0        # 方向端口反转掩码
$4=0        # 步进使能反转
$5=0        # 限位引脚反转
$6=0        # 探针引脚反转
$10=1       # 状态报告掩码
$11=0.010   # 交汇偏差（mm）
$12=0.002   # 圆弧容差（mm）
$13=0       # 英寸报告
$20=0       # 软限位
$21=0       # 硬限位
$22=1       - 回原点循环使能
$23=0       - 回原点方向反转
$24=25.0    - 回原点定位进给速度
$25=500.0   - 回原点搜索进给速度
$26=250     - 回原点开关消抖延迟
$27=1.000   - 回原点开关回退距离
$30=1000    - 最大主轴转速
$31=0       - 最小主轴转速
$32=0       - 激光模式使能
$100=250.000 - X 轴每毫米步数
$101=250.000 - Y 轴每毫米步数
$102=250.000 - Z 轴每毫米步数
$110=500.000 - X 轴最大速率（mm/min）
$111=500.000 - Y 轴最大速率（mm/min）
$112=500.000 - Z 轴最大速率（mm/min）
$120=10.000 - X 轴加速度（mm/sec^2）
$121=10.000 - Y 轴加速度（mm/sec^2）
$122=10.000 - Z 轴加速度（mm/sec^2）
$130=200.000 - X 轴最大行程（mm）
$131=200.000 - Y 轴最大行程（mm）
$132=200.000 - Z 轴最大行程（mm）
```

### 关键设置参考

| 设置 | 参数 | 说明 |
|------|------|------|
| $100-$102 | Steps/mm | 每个轴每毫米步数 |
| $110-$112 | Max rate | 最大速度（mm/min） |
| $120-$122 | Acceleration | 加速度（mm/sec^2） |
| $130-$132 | Max travel | 最大行程距离 |
| $20 | Soft limits | 防止超过最大行程 |
| $21 | Hard limits | 限位开关紧急停止 |
| $22 | Homing | 启用回原点循环 |
| $30 | Max spindle | 最大主轴 RPM |
| $32 | Laser mode | 启用激光模式 |

## 接线

### 步进电机连接（A4988）

| A4988 引脚 | Arduino 引脚 | 说明 |
|-----------|-------------|------|
| STEP | D2 (X), D3 (Y), D4 (Z) | 步进信号 |
| DIR | D5 (X), D6 (Y), D7 (Z) | 方向信号 |
| ENABLE | D8 | 使能所有驱动 |
| VDD | 5V | 逻辑电源 |
| VMOT | 12-24V | 电机电源 |
| GND | GND | 接地 |
| 1A, 1B, 2A, 2B | 电机线 | 步进线圈 |

### 限位开关接线

| 开关 | Arduino 引脚 | 功能 |
|------|-------------|------|
| X 限位 | D9 | X 轴原点/限位 |
| Y 限位 | D10 | Y 轴原点/限位 |
| Z 限位 | D11 | Z 轴原点/限位 |
| 公共 | GND | 接地 |

### 主轴控制

| 组件 | 连接 | 说明 |
|------|------|------|
| 主轴 PWM | D12 | 速度控制 |
| 主轴使能 | D13 | 开/关继电器 |
| VFD 信号 | 0-10V 模拟 | 变频器驱动 |

## 每毫米步数计算

### 公式

```
Steps/mm = (每转步数 * 微步) / (丝杆螺距 * 齿轮比)
```

### 常见配置

| 电机 | 微步 | 丝杆 | Steps/mm |
|------|------|------|----------|
| 200 步/转 | 1/16 | 2mm 螺距 | 1600 |
| 200 步/转 | 1/16 | 4mm 螺距 | 800 |
| 200 步/转 | 1/32 | 2mm 螺距 | 3200 |
| 200 步/转 | 1/16 | T8 (8mm) | 400 |
| 200 步/转 | 1/32 | T8 (8mm) | 800 |

## 回原点循环

### 回原点序列

| 步骤 | 操作 | 说明 |
|------|------|------|
| 1 | Z 轴上移 | 先将 Z 移到顶部（安全） |
| 2 | X 轴回原点 | 将 X 移到限位开关 |
| 3 | Y 轴回原点 | 将 Y 移到限位开关 |
| 4 | 回退 | 从开关处移开 |
| 5 | 设置零点 | 设置机器零点 |

### 回原点命令

```bash
$H          # 启动回原点循环
$X          - 消除报警锁定
$N          - 查看启动块
$N0=G28     - 设置启动块 0
```

## 进给速度和转速

### 材料建议

| 材料 | 进给速度 | 主轴 RPM | 切削深度 |
|------|---------|---------|---------|
| 软木 | 1000-3000 mm/min | 10,000-20,000 | 2-5 mm |
| 硬木 | 500-1500 mm/min | 10,000-18,000 | 1-3 mm |
| MDF | 1000-2500 mm/min | 12,000-20,000 | 2-4 mm |
| 亚克力 | 500-1500 mm/min | 10,000-16,000 | 1-2 mm |
| 铝 | 200-500 mm/min | 8,000-15,000 | 0.5-1 mm |
| 钢 | 100-300 mm/min | 5,000-10,000 | 0.2-0.5 mm |

### 进给速度公式

```
进给速度 = RPM x 刃数 x 切屑厚度
```

## 激光模式

### 启用激光模式

```bash
$32=1       # 启用激光模式
$30=1000    # 最大主轴速度（S 值）
$31=0       - 最小主轴速度
```

### 激光功率控制

| S 值 | 功率 | 用途 |
|------|------|------|
| 0 | 关 | 不发射 |
| 1-100 | 低 | 雕刻 |
| 500 | 中 | 切割薄材料 |
| 1000 | 最大 | 全功率切割 |

### 激光 G-Code 示例

```gcode
G90         ; 绝对模式
G0 X0 Y0   ; 移动到起点
M3 S800     ; 激光开启 80%
G1 X50 F300 ; 切割线
G1 Y50      ; 切割角
G1 X0       ; 切割线
G1 Y0       ; 返回
M5          ; 激光关闭
G0 X0 Y0   ; 回原点
```

## 状态报告

### 启用状态报告

```bash
$10=1       # 启用状态报告
?           ; 请求状态
```

### 状态报告格式

```
<Idle|MPos:0.000,0.000,0.000|FS:0,0|WCO:0.000,0.000,0.000>
```

| 字段 | 说明 |
|------|------|
| Idle/Run/Alarm | 机器状态 |
| MPos | 机器位置（X,Y,Z） |
| WPos | 工件位置 |
| FS | 进给速度和主轴转速 |
| WCO | 工件坐标偏移 |

## 控制软件

| 软件 | 平台 | 功能 |
|------|------|------|
| Universal G-Code Sender | 跨平台 | 功能全面 |
| Candle | 跨平台 | 3D 可视化 |
| CNCjs | 基于 Web | 浏览器控制 |
| bCNC | 跨平台 | 高级功能 |
| LaserGRBL | Windows | 激光专用 |
| LightBurn | 跨平台 | 激光雕刻 |

## 故障排除

| 问题 | 原因 | 解决方案 |
|------|------|---------|
| 电机不动 | 接线错误 | 检查电机连接 |
| 方向错误 | 方向反转 | 更改 $3 设置 |
| 丢步 | 速度/加速度过快 | 降低速度或加速度 |
| 报警状态 | 限位开关触发 | 检查接线，$X 解锁 |
| 切割有噪音 | 机械松动 | 拧紧龙门架和联轴器 |
| 尺寸不准确 | steps/mm 错误 | 校准 $100-$102 |

### 校准流程

1. 命令已知距离：`G91 G1 X100 F500`
2. 用卡尺测量实际距离
3. 计算：`new_steps = old_steps * commanded / actual`
4. 更新：`$100=new_value`
5. 重复直到准确

## 安全

| 预防措施 | 实现方式 |
|---------|---------|
| 急停 | 物理急停按钮 |
| 限位开关 | 所有轴接线 |
| 软限位 | 启用 $20 |
| 硬限位 | 启用 $21 |
| 回原点 | 启用 $22 并运行 $H |
| Z 探针 | 设置刀具高度 |
| 消防安全 | 监控激光操作 |

## 总结

GRBL 为基于 Arduino 的系统提供了可靠的高性能 CNC 控制器。其 G-code 兼容性、可配置设置和广泛的工具支持，使其适用于爱好者和专业 CNC 机床、激光雕刻机以及类似的运动控制应用。


---

## 来源：machine.md

## 简介

LinuxCNC 是一个开源软件系统，用于计算机控制铣床、车床、等离子切割机和机器人等机床。它提供步进电机和伺服电机的实时控制。

### 什么是 CNC？

计算机数控 (CNC) 使用计算机控制机床。LinuxCNC 解释 G-code 指令并将其转换为精确的电机运动。

| 组件 | 功能 |
|------|------|
| 计算机 | 运行 LinuxCNC 软件 |
| 运动控制器 | 生成步进脉冲 |
| 电机 | 驱动机床轴 |
| 机床 | 物理切削工具 |

### LinuxCNC 特性

| 特性 | 描述 |
|------|------|
| 实时控制 | 精确的电机控制时序 |
| G-code 解释器 | 处理加工指令 |
| 刀路显示 | 切削路径可视化 |
| 配置工具 | 机床设置向导 |
| HAL | 硬件抽象层 |

## 系统要求

### 硬件要求

| 组件 | 最低 | 推荐 |
|------|------|------|
| CPU | 1 GHz | 2+ GHz 多核 |
| 内存 | 1 GB | 4 GB |
| 存储 | 10 GB | 50 GB |
| 网络 | 可选 | 远程以太网 |

### 实时要求

| 方面 | 要求 |
|------|------|
| 延迟 | < 50 微秒抖动 |
| 内核 | PREEMPT_RT 补丁内核 |
| BIOS | 禁用电源管理 |
| USB | 避免 USB 用于运动控制 |

### 支持的硬件

| 硬件类型 | 示例 |
|----------|------|
| 步进驱动 | TB6600、DM542、Gecko G203V |
| 伺服驱动 | Mesa 7i77、Granite Devices |
| 转接板 | Mesa 7i76、C10 |
| 接口卡 | Mesa 5i25、6i25 |

## 安装

### 安装 LinuxCNC

```bash
# 下载 LinuxCNC ISO
# 从 USB 启动安装
# 或在现有 Debian/Ubuntu 上安装
sudo apt update
sudo apt install linuxcnc-uspace
```

### 安装后设置

```bash
# 检查延迟
latency-test

# 验证安装
linuxcnc --version
```

### 延迟测试

| 延迟值 | 质量 | 用例 |
|--------|------|------|
| < 15,000 ns | 优秀 | 伺服系统 |
| 15,000-30,000 ns | 良好 | 步进系统 |
| 30,000-100,000 ns | 一般 | 基本操作 |
| > 100,000 ns | 差 | 不推荐 |

## 配置

### 配置向导

LinuxCNC 包含分步配置向导：

| 向导 | 用途 |
|------|------|
| 步进配置 | 配置步进电机系统 |
| 伺服配置 | 配置伺服电机系统 |
| 主轴配置 | 配置主轴速度控制 |
| 车床配置 | 配置车床特定设置 |

### INI 文件结构

```ini
[EMC]
MACHINE = My Mill
VERSION = 1.0

[DISPLAY]
DISPLAY = axis
POSITION_OFFSET = RELATIVE
POSITION_FEEDBACK = ACTUAL

[TRAJ]
AXES = 3
COORDINATES = X Y Z
LINEAR_UNITS = inch
ANGULAR_UNITS = degree

[EMCIO]
EMCIO = io
CYCLE_TIME = 0.100
TOOL_TABLE = tool.tbl
```

### 轴配置

```ini
[AXIS_0]
TYPE = LINEAR
HOME = 0.0
MAX_VELOCITY = 5.0
MAX_ACCELERATION = 50.0
SCALE = 4000
MIN_LIMIT = -10.0
MAX_LIMIT = 10.0
```

| 参数 | 描述 |
|------|------|
| TYPE | LINEAR（线性）或 ANGULAR（角度） |
| HOME | 原点位置 |
| MAX_VELOCITY | 最大速度（单位/秒） |
| MAX_ACCELERATION | 最大加速度 |
| SCALE | 每单位步数 |

## 硬件抽象层 (HAL)

### 什么是 HAL？

HAL 允许将软件组件连接在一起，创建自定义控制配置。

| 组件类型 | 示例 |
|----------|------|
| Pin | 输入/输出信号 |
| Signal | 引脚之间的连接 |
| Function | 处理模块 |
| Thread | 执行时序 |

### 基本 HAL 命令

```bash
# 列出所有引脚
halcmd show pin

# 连接信号
halcmd net signal-name pin1 pin2

# 设置值
halcmd setp pin-name value

# 加载组件
halcmd loadrt component_name
```

### HAL 文件示例

```hal
# 加载实时组件
loadrt stepper_gen step_type=0,0,0
loadrt pid names=pid.x,pid.y,pid.z

# 连接步进发生器到位置命令
net x-pos-cmd joint.0.motor-pos-cmd => stepgen.0.position-cmd
net x-pos-fb stepgen.0.position-fb => joint.0.motor-pos-fb

# 连接 PID 控制器
net x-pos-cmd pid.x.command
net x-pos-fb pid.x.feedback
net x-output pid.x.output => stepgen.0.velocity-cmd
```

## G-code 编程

### 基本 G-code 命令

| 代码 | 功能 | 示例 |
|------|------|------|
| G0 | 快速移动 | G0 X10 Y10 |
| G1 | 直线插补 | G1 X10 Y10 F100 |
| G2 | 顺时针圆弧 | G2 X10 Y10 I5 J0 |
| G3 | 逆时针圆弧 | G3 X10 Y10 I5 J0 |
| G90 | 绝对定位 | G90 |
| G91 | 增量定位 | G91 |

### 常用 M-code

| 代码 | 功能 |
|------|------|
| M0 | 程序停止 |
| M1 | 选择性停止 |
| M2 | 程序结束 |
| M3 | 主轴正转 (CW) |
| M4 | 主轴反转 (CCW) |
| M5 | 主轴停止 |
| M6 | 换刀 |
| M8 | 冷却液开 |
| M9 | 冷却液关 |

### 示例程序

```gcode
(Header)
G21 G90 G17

(Tool change)
T1 M6
S1000 M3

(First cut)
G0 X0 Y0 Z5
G1 Z-2 F100
G1 X50 F200
G1 Y50
G1 X0
G1 Y0

(End)
G0 Z25
M5
M2
```

## 刀具管理

### 刀具表

| 刀具 | 描述 | 直径 | 长度 |
|------|------|------|------|
| T1 | 立铣刀 6mm | 6.0 mm | 50 mm |
| T2 | 钻头 3mm | 3.0 mm | 40 mm |
| T3 | 球头铣刀 4mm | 4.0 mm | 45 mm |

### 刀具长度补偿

```gcode
G43 H1 (应用 T1 刀具长度补偿)
G49 (取消刀具长度补偿)
```

## 坐标系

### 工件坐标系

| 代码 | 描述 |
|------|------|
| G54 | 工件坐标系 1 |
| G55 | 工件坐标系 2 |
| G56 | 工件坐标系 3 |
| G57 | 工件坐标系 4 |
| G58 | 工件坐标系 5 |
| G59 | 工件坐标系 6 |

### 设置工件零点

```gcode
G10 L20 P1 X0 Y0 Z0 (将 G54 设为当前位置)
```

## 安全功能

### 急停

| 组件 | 功能 |
|------|------|
| 急停按钮 | 立即停止所有运动 |
| 软件急停 | 软件触发的停止 |
| 限位开关 | 防止超程 |

### 安全配置

```ini
[EMC]
EMCIO = io

[TRAJ]
MAX_VELOCITY = 10.0
MAX_ACCELERATION = 100.0
```

## 常见操作

### 回零序列

```gcode
G28.1 (所有轴回零)
G28 X0 Y0 (返回原点)
```

### 探测

```gcode
G38.2 Z-10 F100 (向下探测)
G92 Z0 (将当前位置设为零)
```

## 故障排除

### 常见问题

| 问题 | 可能原因 | 解决方案 |
|------|----------|----------|
| 丢步 | 加速度太高 | 降低最大加速度 |
| 表面质量差 | 振动 | 检查机械刚性 |
| 通信错误 | USB 延迟 | 使用并口或 Mesa 卡 |
| 急停触发 | 限位开关 | 检查接线和配置 |

### 诊断命令

```bash
# 检查 HAL 状态
halcmd show

# 实时监控引脚
halcmd show pin -t

# 查看错误日志
dmesg | grep -i linuxcnc
```

## 总结

| 概念 | 描述 |
|------|------|
| INI 文件 | 机床配置 |
| HAL 文件 | 硬件连接 |
| G-code | 加工指令 |
| 实时 | 精确运动控制 |
| 安全 | 急停和限位开关 |


---
