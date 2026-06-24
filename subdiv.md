# OpenSubdiv: 细分曲面求值

## 简介

OpenSubdiv 是一组开源库，用于在大规模并行 CPU 和 GPU 架构上求值和渲染细分曲面。由 Pixar 开发，现由 Academy Software Foundation 维护，它是细分曲面计算的行业标准。

细分曲面允许艺术家使用简单的控制笼建模复杂的有机形状，在渲染时进行平滑细分。

## 什么是细分曲面？

细分曲面由粗糙的控制网格和一组细分规则定义。在每个层级，网格根据这些规则通过添加新顶点和面进行细化。

| 模型类型 | 控制网格 | 细分结果 |
|---------|---------|---------|
| 简单立方体 | 6 个面，8 个顶点 | 平滑的类球体 |
| 角色头部 | ~500 个面 | 数百万平滑多边形 |
| 车辆 | ~2000 个面 | 平滑的面板和曲线 |

### 为什么使用细分曲面？

| 优势 | 描述 |
|------|------|
| 平滑表面 | 在非正规点处 C2 连续 |
| 拓扑灵活性 | 任何网格拓扑都适用 |
| 内存效率 | 小控制笼，精细结果 |
| 动画友好 | 变形控制网格而非密集网格 |
| 行业标准 | 所有主要 DCC 工具都使用 |

## 细分方案

OpenSubdiv 支持多种细分方案。

| 方案 | 创建者 | 属性 | 使用场景 |
|------|-------|------|---------|
| Catmull-Clark | Catmull & Clark | 正规处 C2，非正规处 C1 | 电影角色 |
| Loop | Charles Loop | 基于三角形，正规处 C2 | 游戏角色 |
| Bilinear | - | 简单边分裂 | 平面面板 |

### Catmull-Clark 规则

| 元素 | 规则 | 结果 |
|------|------|------|
| 面点 | 面顶点的平均值 | 每个面的中心 |
| 边点 | 边端点 + 相邻面点的平均值 | 平滑边中点 |
| 顶点点 | 邻居的加权平均 | 平滑顶点位置 |

## 求值模式

OpenSubdiv 提供多种求值方式。

| 模式 | 描述 | 性能 | 使用场景 |
|------|------|------|---------|
| CPU Uniform | 标准 CPU 细分 | 良好 | 离线渲染 |
| CPU Feature Adaptive | 自适应细化 | 更好 | 动画 |
| GPU Compute | OpenCL/CUDA 内核 | 最快 | 实时预览 |
| GPU Vertex | 顶点着色器方式 | 快 | 游戏引擎 |

## 安装

### 从源码编译

```bash
git clone https://github.com/AcademySoftwareFoundation/OpenSubdiv.git
cd OpenSubdiv
mkdir build && cd build
cmake .. \
  -DCMAKE_INSTALL_PREFIX=/usr/local \
  -DNO_TBB=OFF \
  -DNO_CUDA=OFF \
  -DNO_OPENCL=OFF
make -j$(nproc)
sudo make install
```

### 依赖

| 依赖 | 必需 | 用途 |
|------|------|------|
| CMake | 是 | 构建系统 |
| TBB | 可选 | 多线程 |
| OpenCL | 可选 | GPU 计算 |
| CUDA | 可选 | NVIDIA GPU 计算 |
| OpenGL | 可选 | GPU 渲染 |
| GLFW | 可选 | 示例程序 |

### 包管理器

| 平台 | 命令 |
|------|------|
| macOS | `brew install opensubdiv` |
| Ubuntu | `sudo apt install libopensubdiv-dev` |
| vcpkg | `vcpkg install opensubdiv` |

## 核心概念

### 拓扑细化

拓扑细化决定网格连通性在每个层级如何变化。

| 层级 | 描述 | 顶点数倍增 |
|------|------|----------|
| 0 | 控制笼 | 1x |
| 1 | 第一次细分 | ~4x (Catmull-Clark) |
| 2 | 第二次细分 | ~16x |
| N | 第 N 次细分 | ~4^N x |

### 面片表

面片表存储细分面片的求值数据。它们对高效的 GPU 求值至关重要。

| 面片类型 | 顶点数 | 形状 | 用途 |
|---------|-------|------|------|
| Regular | 16 | 4x4 网格 | 内部面片 |
| Boundary | 12 | 边面片 | 网格边界 |
| Corner | 9 | 角面片 | 网格角 |
| Gregory | 20 | Gregory 面片 | 非正规点 |

### 特征自适应细化

特征自适应细化不是均匀细分整个网格，而是仅在非正规顶点和锐利特征附近进行细分。

| 区域 | 细分 | 原因 |
|------|------|------|
| 正规内部 | 解析面片 | 高效 GPU 求值 |
| 非正规附近 | 额外层级 | 平滑收敛 |
| 锐利折痕 | 额外层级 | 精确折痕求值 |
| 边界 | 额外层级 | 正确的边界行为 |

## API 概述

### 模板表

模板表预计算求值曲面上任意点所需的权重。

```cpp
#include <opensubdiv/far/topologyDescriptor.h>
#include <opensubdiv/far/stencilTableFactory.h>

using namespace OpenSubdiv;

// 定义网格拓扑
Far::TopologyDescriptor desc;
desc.numVertices = numVertices;
desc.numFaces = numFaces;
desc.numVertsPerFace = vertsPerFace;
desc.vertIndicesPerFace = faceIndices;

// 创建拓扑
Far::TopologyRefiner *refiner = 
    Far::TopologyRefinerFactory<Far::TopologyDescriptor>::Create(desc);

// 细化拓扑
refiner->RefineUniform(Far::TopologyRefiner::UniformOptions(maxLevel));

// 构建模板表
Far::StencilTableFactory::Options options;
options.generateControlVerts = true;
options.generateIntermediateLevels = true;

Far::StencilTable const *stencilTable =
    Far::StencilTableFactory::Create(*refiner, options);
```

### 求值

```cpp
// 在模板点求值位置
std::vector<float> newPositions(stencilTable->GetNumStencils() * 3);

stencilTable->UpdateValues(controlPositions.data(), newPositions.data());
```

## HBR vs FAR vs OSD

OpenSubdiv 有三个主要层。

| 层 | 名称 | 用途 | 性能 |
|----|------|------|------|
| HBR | Hierarchical Boundary Rep | 参考实现 | 慢（单线程） |
| FAR | Feature Adaptive Refinement | 生产细化 | 快（多线程） |
| OSD | OpenSubdiv | GPU 求值 | 最快（并行） |

| 层 | 使用场景 |
|----|---------|
| HBR | 正确性测试、旧版兼容 |
| FAR | 生产细分、CPU 渲染 |
| OSD | 实时预览、游戏引擎 |

## GPU 求值

OpenSubdiv 通过多种后端支持 GPU 加速求值。

| 后端 | API | 厂商支持 | 性能 |
|------|-----|---------|------|
| OpenGL Compute | GLSL 4.3+ | 全部 | 非常快 |
| OpenCL | OpenCL 1.2+ | 全部 | 非常快 |
| CUDA | CUDA | NVIDIA | 最快 |
| DirectX Compute | HLSL | Windows | 非常快 |

### OpenGL Compute Shader 示例

```cpp
#include <opensubdiv/osd/glPatchTable.h>
#include <opensubdiv/osd/glVertexBuffer.h>

// 创建 GPU 缓冲
Osd::GLVertexBuffer *vbo = Osd::GLVertexBuffer::Create(
    numVertices * 3, patchTable->GetPatchArrays());

// 上传控制顶点
vbo->UpdateCpuBuffer(controlPositions);

// 在 GPU 上求值
Osd::GLComputeEvaluator *evaluator = Osd::GLComputeEvaluator::Create(...);
evaluator->EvalPatches(vbo, ...);
```

## 锐利特征

### 折痕

折痕定义了本应平滑的表面上的锐利边。

| 折痕权重 | 效果 |
|---------|------|
| 0.0 | 完全平滑（默认） |
| 1.0 | 略微锐利 |
| 5.0 | 非常锐利 |
| 10.0+ | 接近硬边 |

```cpp
// 设置边折痕权重
desc.numCreases = numCreaseEdges;
desc.creaseVertexIndexPairs = creaseEdges;
desc.creaseWeights = creaseWeights;

// 设置顶点折痕权重
desc.numCorners = numCornerVertices;
desc.cornerIndices = cornerIndices;
desc.cornerWeights = cornerWeights;
```

## 与 DCC 工具的集成

| 工具 | OpenSubdiv 用途 | 备注 |
|------|----------------|------|
| Maya | 原生 Viewport 2.0 | GPU 细分显示 |
| Houdini | 视口细分 | 实时反馈 |
| Blender | 细分修改器 | CPU 和 GPU 模式 |
| Katana | 渲染时细分 | 属性驱动 |
| 3ds Max | TurboSmooth 集成 | 基于插件 |

## 性能对比

| 配置 | 细分时间（100 万面到 400 万面） | 内存 |
|------|-------------------------------|------|
| CPU 单线程 (HBR) | 1200ms | 低 |
| CPU 多线程 (FAR) | 180ms | 中 |
| GPU Compute (OSD) | 8ms | 较高 |
| 特征自适应 (FAR) | 90ms | 中 |
| 特征自适应 (OSD) | 4ms | 较高 |

## 最佳实践

| 实践 | 建议 |
|------|------|
| 拓扑 | 保持控制笼尽可能简单 |
| 折痕 | 谨慎使用，优先选择平滑过渡 |
| 层级 | 显示用 3-4 级，渲染用更多 |
| 面片 | 为 GPU 求值启用面片表 |
| 自适应 | 对复杂网格使用特征自适应 |
| 内存 | 高细分级别时监控 GPU 内存 |

## 更多资源

| 资源 | URL |
|------|-----|
| 文档 | opensubdiv.org |
| GitHub | github.com/AcademySoftwareFoundation/OpenSubdiv |
| Pixar 技术备忘录 | Graphics.pixar.com/opensubdiv |
| SIGGRAPH 论文 | Graphics.pixar.com |
