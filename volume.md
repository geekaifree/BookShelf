# 体积数据

> 本文档整合了以下源文件：volume.md

---

## 来源：volume.md

## 简介

OpenVDB 是一个开源库，用于存储、操作和渲染稀疏体积数据。由 DreamWorks Animation 开发，现由 Academy Software Foundation 维护，它已成为电影和视觉特效体积效果的行业标准。

OpenVDB 使用层次数据结构，只高效存储包含数据的空间区域，使得处理极大的体积数据集而不耗尽内存成为可能。

## 为什么体积数据很重要

许多自然现象本质上是三维的，无法用表面网格表示。体积数据能准确捕捉这些效果。

| 现象 | 传统方法 | OpenVDB 方法 |
|------|---------|-------------|
| 烟雾 | 公告板精灵 | 完整 3D 模拟 |
| 火焰 | 2D 纹理 | 体积发射 |
| 云 | 分层卡片 | 真正 3D 密度场 |
| 液体 | 表面网格 | SDF + 速度场 |
| 雾 | 均匀密度 | 空间变化密度 |
| 爆炸 | 粒子精灵 | 动态体积网格 |

## 核心数据结构

OpenVDB 使用三层节点的 B+ 树结构。

| 层级 | 节点大小 | 用途 | 典型数量 |
|------|---------|------|---------|
| 根 | 512^3（坐标范围） | 顶层索引 | 1 |
| 内部 | 4^3 或 8^3 | 中层分支 | 数千 |
| 叶 | 8^3（512 体素） | 实际体素数据 | 数百万 |

### 稀疏与密集存储

| 存储类型 | 内存 | 数据访问 | 使用场景 |
|---------|------|---------|---------|
| 密集 | O(n^3) | 直接索引 | 小体积 |
| 稀疏 (VDB) | O(活动体素) | 树遍历 | 视觉特效体积 |
| 稀疏（自适应） | 变化 | 多分辨率 | 水平集 |

### 网格类型

| 网格类型 | 值类型 | 典型用途 |
|---------|-------|---------|
| FloatGrid | float | 密度、温度 |
| Vec3fGrid | Vector3f | 速度、颜色 |
| Int32Grid | int32_t | 标签、ID |
| BoolGrid | bool | 遮罩 |
| DoubleGrid | double | 高精度标量 |
| HalfGrid | half | 节省内存的浮点 |

## 安装

### 从源码编译

```bash
git clone https://github.com/AcademySoftwareFoundation/openvdb.git
cd openvdb
mkdir build && cd build
cmake .. \
  -DCMAKE_INSTALL_PREFIX=/usr/local \
  -DOPENVDB_BUILD_PYTHON_MODULE=ON \
  -DOPENVDB_BUILD_BINARIES=ON
make -j$(nproc)
sudo make install
```

### 依赖

| 依赖 | 必需 | 用途 |
|------|------|------|
| Boost | 是 | 智能指针、IO |
| TBB | 是 | 多线程 |
| OpenEXR | 是 | Half-float 支持 |
| Zlib | 是 | 压缩 |
| Blosc | 可选 | 体素压缩 |
| Python | 可选 | Python 绑定 |
| NumPy | 可选 | 数组互操作 |
| GLFW | 可选 | 查看器 |

### 包管理器

| 平台 | 命令 |
|------|------|
| macOS | `brew install openvdb` |
| Ubuntu | `sudo apt install libopenvdb-dev` |
| Conda | `conda install -c conda-forge openvdb` |
| vcpkg | `vcpkg install openvdb` |

## Python API

### 创建网格

```python
import openvdb
import numpy as np

# 创建浮点网格
grid = openvdb.FloatGrid()
grid.name = "density"

# 从 numpy 数组创建
data = np.zeros((100, 100, 100), dtype=np.float32)
data[40:60, 40:60, 40:60] = 1.0  # 密度立方体

grid.copyFromArray(data)
print(f"Active voxel count: {grid.activeVoxelCount}")
print(f"Grid bbox: {grid.evalActiveVoxelBoundingBox()}")
```

### 读写 VDB 文件

```python
import openvdb

# 将网格写入文件
density = openvdb.FloatGrid()
velocity = openvdb.Vec3fGrid()

openvdb.write("smoke.vdb", density, velocity)

# 从文件读取网格
grids = openvdb.readAll("smoke.vdb")
for grid in grids:
    print(f"Name: {grid.name}, Type: {grid.type}")
    print(f"Active voxels: {grid.activeVoxelCount}")
```

### 访问体素数据

```python
import openvdb
import numpy as np

grid = openvdb.FloatGrid()
# ... 填充网格 ...

# 转换为 numpy 数组
array = grid.copyToArray()
print(f"Array shape: {array.shape}")

# 访问特定坐标
accessor = grid.getAccessor()
value = accessor.getValue((0, 0, 0))
print(f"Value at (0,0,0): {value}")

# 设置值
accessor.setValueOn((10, 10, 10), 5.0)
```

### 水平集

水平集将表面表示为有符号距离场的零交叉。

```python
import openvdb
import numpy as np

# 创建球体水平集
sphere = openvdb.createLevelSetSphere(
    radius=50.0,
    center=(0.0, 0.0, 0.0),
    voxelSize=1.0
)

print(f"Active voxels: {sphere.activeVoxelCount}")
print(f"BBox: {sphere.evalActiveVoxelBoundingBox()}")

# 布尔操作
cube = openvdb.createLevelSetBox(
    (-30, -30, -30), (30, 30, 30), voxelSize=1.0
)

# 并集
union = openvdb.tools.levelSetUnion(sphere, cube)

# 交集
intersection = openvdb.tools.levelSetIntersection(sphere, cube)

# 差集
difference = openvdb.tools.levelSetDifference(sphere, cube)
```

## C++ API

### 创建和填充网格

```cpp
#include <openvdb/openvdb.h>
#include <openvdb/tools/LevelSetSphere.h>

// 初始化 OpenVDB
openvdb::initialize();

// 创建稀疏网格
openvdb::FloatGrid::Ptr grid = openvdb::FloatGrid::create(0.0);
grid->setName("density");

// 获取访问器以高效访问体素
openvdb::FloatGrid::Accessor accessor = grid->getAccessor();

// 设置单个体素
for (int i = 0; i < 100; ++i) {
    openvdb::Coord xyz(i, i, i);
    accessor.setValue(xyz, 1.0f);
}

// 打印统计
std::cout << "Active voxels: " << grid->activeVoxelCount() << std::endl;
```

### 水平集操作

```cpp
#include <openvdb/tools/LevelSetSphere.h>
#include <openvdb/tools/LevelSetUtil.h>

// 创建球体水平集
openvdb::FloatGrid::Ptr sphere = 
    openvdb::tools::createLevelSetSphere<openvdb::FloatGrid>(
        50.0f, openvdb::Vec3f(0, 0, 0), 1.0f);

// 创建立方体水平集
openvdb::FloatGrid::Ptr box = 
    openvdb::tools::createLevelSetBox<openvdb::FloatGrid>(
        openvdb::BBoxd(openvdb::Vec3d(-30), openvdb::Vec3d(30)), 1.0f);

// 布尔操作
openvdb::FloatGrid::Ptr result = 
    openvdb::tools::csgUnion(*sphere, *box);
```

## 工具和操作

### 滤波操作

| 操作 | 函数 | 使用场景 |
|------|------|---------|
| 均值 | `tools::mean` | 平滑 |
| 高斯 | `tools::gaussian` | 模糊 |
| 中值 | `tools::median` | 降噪 |
| 膨胀 | `tools::dilate` | 扩展区域 |
| 腐蚀 | `tools::erode` | 收缩区域 |
| 偏移 | `tools::offset` | 水平集偏移 |

### 转换工具

| 转换 | 从 | 到 | 使用场景 |
|------|----|----|---------|
| 网格到 VDB | 多边形网格 | 体积 | 模拟设置 |
| VDB 到网格 | 体积 | 多边形网格 | 渲染 |
| 雾到 SDF | 密度场 | 水平集 | 表面提取 |
| SDF 到雾 | 水平集 | 密度 | 体积渲染 |

```python
import openvdb

# 将水平集转换为网格（使用 C++ 绑定）
# mesh = openvdb.tools.volumeToMesh(sphere_grid)

# 将网格转换为水平集
# grid = openvdb.tools.meshToLevelSet(mesh, voxel_size=1.0)
```

## 文件格式

VDB 文件格式存储一个或多个网格及其元数据。

| 特性 | 描述 |
|------|------|
| 多网格 | 每文件多个网格 |
| 压缩 | Blosc、ZIP 或无 |
| 元数据 | 每网格键值对 |
| 部分 I/O | 读写特定网格 |
| 流式 | 顺序读取支持 |

### 文件结构

| 部分 | 内容 | 描述 |
|------|------|------|
| 头部 | 魔数、版本 | 文件标识 |
| 网格描述符 | 名称、类型、变换 | 网格元数据 |
| 树数据 | B+ 树节点 | 体素数据 |
| 元数据 | 键值对 | 自定义属性 |
| 尾部 | 校验和 | 完整性验证 |

## 与视觉特效工具的集成

| 工具 | OpenVDB 集成 | 备注 |
|------|-------------|------|
| Houdini | 原生 | VDB SOP 节点 |
| Blender | 原生 | 体积对象和修改器 |
| Maya | 插件 | Bifrost 集成 |
| Katana | 原生 | 体积渲染 |
| 3ds Max | 插件 | Phoenix FD 集成 |
| Unreal Engine | 插件 | Niagara VDB 支持 |
| Arnold | 原生 | 体积着色器 |
| V-Ray | 原生 | VDB 渲染 |

## 模拟工作流

### 烟雾模拟

```python
import openvdb

# 步骤 1：创建密度网格
density = openvdb.FloatGrid()
density.name = "density"

# 步骤 2：创建速度场
velocity = openvdb.Vec3fGrid()
velocity.name = "velocity"

# 步骤 3：创建温度网格
temperature = openvdb.FloatGrid()
temperature.name = "temperature"

# 步骤 4：通过速度场平流密度
# （模拟在外部发生，VDB 存储数据）

# 步骤 5：写入输出
openvdb.write("smoke_frame001.vdb", density, velocity, temperature)
```

### 水平集工作流

```python
import openvdb

# 创建初始水平集（例如球体）
sphere = openvdb.createLevelSetSphere(5.0, (0, 0, 0), 0.1)

# 跟踪哪些体素发生了变化
sphere.setGridClass(openvdb.GridClass.LEVEL_SET)

# 写入用于网格化
openvdb.write("levelset.vdb", sphere)
```

## 性能优化

| 优化 | 技术 | 影响 |
|------|------|------|
| 体素大小 | 使用可接受的最大尺寸 | 高 |
| 压缩 | 启用 Blosc 压缩 | 中 |
| 稀疏访问 | 使用访问器而非直接迭代 | 高 |
| 变换 | 在变换中使用适当的体素大小 | 中 |
| 背景值 | 设置为空空间的典型值 | 低 |
| 线程数 | TBB 自动检测核心数 | 高 |

## 最佳实践

| 实践 | 建议 |
|------|------|
| 网格命名 | 为每个网格使用描述性名称 |
| 体素大小 | 匹配所需细节级别 |
| 压缩 | 文件存储时启用，计算时禁用 |
| 水平集 | 保持窄带宽度一致 |
| 元数据 | 在网格元数据中存储模拟参数 |
| 内存 | 模拟期间监控活动体素数量 |

## 更多资源

| 资源 | URL |
|------|-----|
| 文档 | openvdb.org |
| GitHub | github.com/AcademySoftwareFoundation/openvdb |
| API 参考 | openvdb.org/documentation |
| SIGGRAPH 课程 | openvdb.org/documentation |


---
