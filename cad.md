# FreeCAD：开源参数化 3D CAD 建模器

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
