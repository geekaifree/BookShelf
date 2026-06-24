# OpenSCAD：程序化 3D CAD 指南

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
