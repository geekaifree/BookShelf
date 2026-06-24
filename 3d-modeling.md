# 3D 建模

> 本文档整合了以下源文件：blender.md, blender3d.md, opensubdiv.md, openvdb.md, subdiv.md

---

## 来源：blender.md

## 简介

Blender 是一款免费开源的 3D 创作套件，支持整个 3D 管线：建模、绑定、动画、模拟、渲染、合成、运动追踪和视频编辑。它被专业人士和爱好者用于创建动画电影、视觉特效、艺术作品、3D 打印模型、动态图形、交互式 3D 应用和虚拟现实。

Blender 由 Blender Foundation 开发，可在 Windows、macOS 和 Linux 上使用。

## 为什么使用 Blender？

| 特性 | Blender | Maya | 3ds Max | Cinema 4D |
|------|---------|------|---------|-----------|
| 费用 | 免费 | $1,785/年 | $1,785/年 | $719/年 |
| 开源 | 是 | 否 | 否 | 否 |
| 平台 | 全部 | Win/Mac | Windows | Win/Mac |
| 建模 | 优秀 | 优秀 | 优秀 | 良好 |
| 动画 | 优秀 | 优秀 | 良好 | 良好 |
| 渲染 | Cycles, EEVEE | Arnold | Arnold | Redshift |
| 视频编辑 | 内置 | 否 | 否 | 否 |
| 游戏引擎 | UPBGE | 否 | 否 | 否 |

## 核心功能

| 功能 | 描述 |
|------|------|
| 建模 | 多边形、曲线和曲面建模 |
| 雕刻 | 使用笔刷的数字雕刻 |
| 动画 | 关键帧、程序和物理动画 |
| 渲染 | Cycles（光线追踪）和 EEVEE（实时） |
| 模拟 | 布料、流体、烟雾、粒子 |
| 合成 | 基于节点的后期处理 |
| 视频编辑 | 非线性视频编辑器 |
| 脚本 | Python API 自动化 |
| UV 展开 | 纹理映射工具 |
| 纹理化 | PBR 材质系统 |

## 安装

### Windows

1. 从 blender.org 下载
2. 运行安装程序
3. 按照安装向导操作

### macOS

```bash
# Homebrew
brew install --cask blender

# 或从 blender.org 下载
```

### Linux

```bash
# Snap
sudo snap install blender --classic

# Flatpak
flatpak install flathub org.blender.Blender

# Ubuntu/Debian
sudo apt install blender
```

### 系统要求

| 组件 | 最低 | 推荐 |
|------|------|------|
| CPU | 64 位双核 | 64 位四核 |
| 内存 | 4GB | 16GB+ |
| GPU | OpenGL 3.3 | NVIDIA GTX 1060+ |
| 存储 | 500MB | SSD 10GB+ |
| 显示 | 1280x768 | 1920x1080+ |

## 界面概述

### 主要区域

| 区域 | 用途 |
|------|------|
| 3D 视口 | 主工作区 |
| 属性 | 对象和场景设置 |
| 大纲 | 场景层级 |
| 时间线 | 动画时间线 |
| 信息栏 | 状态和菜单 |

### 编辑器类型

| 编辑器 | 用途 |
|-------|------|
| 3D 视口 | 建模、雕刻、动画 |
| UV 编辑器 | 纹理映射 |
| 着色器编辑器 | 材质节点 |
| 合成器 | 后期处理节点 |
| 视频编辑器 | 视频编辑 |
| 动作摄影表 | 动画时间 |
| 图形编辑器 | 动画曲线 |
| 文本编辑器 | 脚本编辑 |
| 控制台 | Python 控制台 |

### 工作区

| 工作区 | 用途 |
|-------|------|
| 布局 | 通用工作 |
| 建模 | 网格编辑 |
| 雕刻 | 数字雕刻 |
| UV 编辑 | 纹理映射 |
| 纹理绘制 | 纹理绘制 |
| 着色 | 材质创建 |
| 动画 | 动画工作 |
| 渲染 | 渲染设置 |
| 合成 | 后期处理 |
| 脚本 | Python 脚本 |

## 3D 视口导航

### 视图控制

| 操作 | 快捷键 | 鼠标 |
|------|-------|------|
| 旋转 | 中键 | MMB 拖动 |
| 平移 | Shift+中键 | Shift+MMB 拖动 |
| 缩放 | 滚轮 | Ctrl+MMB 拖动 |
| 查看选中 | 小键盘 . | - |
| 查看全部 | Home | - |

### 正交视图

| 视图 | 快捷键 |
|------|-------|
| 前 | 小键盘 1 |
| 后 | Ctrl+小键盘 1 |
| 右 | 小键盘 3 |
| 左 | Ctrl+小键盘 3 |
| 顶 | 小键盘 7 |
| 底 | Ctrl+小键盘 7 |
| 摄像机 | 小键盘 0 |

## 建模

### 网格编辑工具

| 工具 | 快捷键 | 描述 |
|------|-------|------|
| 挤出 | E | 延伸几何体 |
| 内插 | I | 创建内部面 |
| 倒角 | Ctrl+B | 平滑边 |
| 环切 | Ctrl+R | 添加边循环 |
| 切割 | K | 自定义切割边 |
| 合并 | M | 合并顶点 |
| 分离 | P | 分割网格 |
| 填充 | F | 从边创建面 |

### 选择模式

| 模式 | 快捷键 | 选择 |
|------|-------|------|
| 顶点 | 1 | 单个顶点 |
| 边 | 2 | 边循环 |
| 面 | 3 | 多边形面 |
| 全部 | A | 所有 |
| 框选 | B | 矩形区域 |
| 圈选 | C | 笔刷选择 |

### 修改器

| 修改器 | 类别 | 用途 |
|-------|------|------|
| 细分曲面 | 生成 | 平滑网格 |
| 镜像 | 生成 | 对称建模 |
| 阵列 | 生成 | 重复几何体 |
| 布尔 | 生成 | 合并网格 |
| 倒角 | 修改 | 平滑边 |
| 实体化 | 修改 | 添加厚度 |
| 缩裹 | 修改 | 投射到表面 |
| 晶格 | 变形 | 有机变形 |
| 骨架 | 变形 | 骨骼动画 |
| 布料 | 物理 | 织物模拟 |
| 流体 | 物理 | 液体模拟 |
| 烟雾 | 物理 | 烟雾模拟 |

## 雕刻

### 雕刻笔刷

| 笔刷 | 快捷键 | 用途 |
|------|-------|------|
| 绘制 | X | 添加/减去粘土 |
| 粘土条 | C | 平坦笔刷笔触 |
| 膨胀 | I | 扩展表面 |
| 抓取 | G | 移动几何体 |
| 平滑 | S | 平滑表面 |
| 抖平 | Shift+T | 水平表面 |
| 折痕 | Shift+C | 锐利折痕 |
| 夹捏 | P | 拉近顶点 |

### 雕刻模式

| 模式 | 描述 |
|------|------|
| 雕刻 | 完整网格雕刻 |
| 动态拓扑 | 雕刻时自动重新网格化 |
| 多分辨率 | 多个细分级别 |

## 动画

### 关键帧动画

| 操作 | 快捷键 | 描述 |
|------|-------|------|
| 插入关键帧 | I | 添加关键帧 |
| 删除关键帧 | Alt+I | 移除关键帧 |
| 自动关键帧 | 在时间线中启用 | 自动记录更改 |

### 关键帧类型

| 类型 | 插值 | 使用场景 |
|------|------|---------|
| 恒定 | 无 | 瞬间变化 |
| 线性 | 直线 | 机械运动 |
| 贝塞尔 | 平滑曲线 | 自然运动 |
| 弹跳 | 弹性 | 二级运动 |
| 弹性 | 弹簧 | 过冲效果 |

### 动画编辑器

| 编辑器 | 用途 |
|-------|------|
| 时间线 | 总体时间 |
| 动作摄影表 | 关键帧时间 |
| 图形编辑器 | 动画曲线 |
| NLA 编辑器 | 非线性动画 |

## 材质和纹理

### 材质属性

| 属性 | 描述 |
|------|------|
| 基础颜色 | 表面颜色 |
| 金属度 | 金属 vs 电介质 |
| 粗糙度 | 表面光滑度 |
| 法线 | 表面细节 |
| 自发光 | 自发光 |
| Alpha | 透明度 |
| 次表面 | 光散射 |

### 着色器节点

| 节点 | 用途 |
|------|------|
| Principled BSDF | 主要材质着色器 |
| Image Texture | 加载纹理文件 |
| Noise Texture | 程序化噪波 |
| Color Ramp | 颜色映射 |
| Math | 数学运算 |
| Mix Shader | 混合材质 |
| Mapping | 纹理坐标 |
| Texture Coordinate | UV 和对象坐标 |

## 渲染

### Cycles 渲染器

| 功能 | 描述 |
|------|------|
| 光线追踪 | 物理精确 |
| GPU 支持 | CUDA, OptiX, Metal |
| 降噪 | AI 驱动降噪 |
| 自适应采样 | 高效渲染时间 |
| 运动模糊 | 动画对象 |
| 景深 | 摄像机模糊 |

### EEVEE 渲染器

| 功能 | 描述 |
|------|------|
| 实时 | 即时反馈 |
| 屏幕空间 | 近似效果 |
| 辉光 | 发光效果 |
| 环境遮蔽 | 接触阴影 |
| 屏幕空间反射 | 近似反射 |
| 体积效果 | 雾和烟雾 |

### 渲染设置

| 设置 | 描述 | 建议 |
|------|------|------|
| 分辨率 | 图像大小 | 1920x1080 或 3840x2160 |
| 采样 | 渲染质量 | 128-1024 |
| 降噪 | 降噪 | Cycles 启用 |
| 胶片 | 透明度 | 合成时启用 |

## 物理模拟

### 模拟类型

| 类型 | 描述 | 使用场景 |
|------|------|---------|
| 布料 | 织物模拟 | 服装、旗帜 |
| 流体 | 液体模拟 | 水、岩浆 |
| 烟雾 | 气体模拟 | 火、雾 |
| 刚体 | 固体 | 碰撞、堆叠 |
| 软体 | 可变形 | 橡胶、果冻 |
| 粒子 | 点系统 | 雨、火花、毛发 |

### 布料设置

| 设置 | 描述 |
|------|------|
| 质量 | 织物重量 |
| 刚度 | 弯曲阻力 |
| 阻尼 | 运动衰减 |
| 碰撞 | 对象交互 |

## 脚本

### Python API

```python
import bpy

# 创建立方体
bpy.ops.mesh.primitive_cube_add(size=2, location=(0, 0, 0))

# 获取活动对象
obj = bpy.context.active_object

# 修改对象
obj.name = "MyCube"
obj.location.x = 5

# 创建材质
mat = bpy.data.materials.new(name="RedMaterial")
mat.use_nodes = True
nodes = mat.node_tree.nodes
principled = nodes.get("Principled BSDF")
principled.inputs["Base Color"].default_value = (1, 0, 0, 1)

# 分配材质
obj.data.materials.append(mat)
```

### 脚本控制台

| 命令 | 描述 |
|------|------|
| `bpy.ops` | 操作符函数 |
| `bpy.data` | 数据访问 |
| `bpy.context` | 当前上下文 |
| `bpy.types` | 类型定义 |

## 键盘快捷键

| 操作 | 快捷键 |
|------|-------|
| 搜索菜单 | F3 |
| 添加对象 | Shift+A |
| 删除 | X |
| 移动 | G |
| 旋转 | R |
| 缩放 | S |
| 撤销 | Ctrl+Z |
| 重做 | Ctrl+Y |
| 保存 | Ctrl+S |
| 渲染 | F12 |
| 渲染动画 | Ctrl+F12 |

## 更多资源

| 资源 | URL |
|------|-----|
| 官方网站 | blender.org |
| 文档 | docs.blender.org |
| 开发者 Wiki | wiki.blender.org |
| 社区 | blender.org/community |


---

## 来源：blender3d.md

## 简介

Armory 是一款直接集成到 Blender 中的开源 3D 游戏引擎。它允许游戏开发者使用 Blender 熟悉的界面创建 3D 游戏，无需离开应用程序。Armory 提供完整的游戏开发环境，包含渲染、物理、逻辑和脚本功能。

通过利用 Blender 现有的工具，Armory 消除了学习单独游戏引擎的需要，同时提供专业级功能。

## 为什么使用 Armory？

| 特性 | Armory | Unity | Unreal | Godot |
|------|--------|-------|--------|-------|
| Blender 集成 | 原生 | 导出 | 导出 | 导出 |
| 费用 | 免费 | 免费增值 | 5% 版税 | 免费 |
| 开源 | 是 | 否 | 源码可用 | 是 |
| 学习曲线 | 低（Blender 用户） | 中等 | 高 | 中等 |
| 工作流 | 集成 | 独立 | 独立 | 独立 |
| 2D 支持 | 是 | 是 | 有限 | 是 |

## 核心功能

| 功能 | 描述 |
|------|------|
| Blender 集成 | 无需导出/导入 |
| PBR 渲染 | 基于物理的渲染 |
| 基于节点的逻辑 | 可视化编程系统 |
| 物理引擎 | 刚体、软体、布料 |
| 脚本 | Haxe、Python、JavaScript |
| 网络 | 多人游戏支持 |
| 音频 | 3D 空间音频 |
| 动画 | 骨骼和混合形状 |
| 粒子 | GPU 粒子系统 |
| UI 系统 | 游戏内用户界面 |

## 安装

### 系统要求

| 要求 | 版本 |
|------|------|
| Blender | 3.0+ |
| 操作系统 | Windows、macOS、Linux |
| GPU | OpenGL 3.3+ 或 Vulkan |
| 内存 | 最低 4GB |
| 存储 | 引擎 2GB |

### 安装 Armory

1. 从 armory3d.org 下载 Armory
2. 解压归档文件
3. 在 Blender 中：Edit > Preferences > Add-ons
4. 点击"Install"并选择 Armory zip 文件
5. 启用"Armory"插件

### 验证安装

| 步骤 | 操作 |
|------|------|
| 1 | 打开 Blender |
| 2 | 检查属性面板中是否有"Armory"标签 |
| 3 | 选择渲染引擎：Armory |
| 4 | 验证游戏逻辑节点是否可用 |

## 项目设置

### 创建新项目

| 步骤 | 操作 |
|------|------|
| 1 | 打开 Blender |
| 2 | 将渲染引擎设为"Armory" |
| 3 | 配置项目设置 |
| 4 | 保存 .blend 文件 |
| 5 | 点击"Play"进行测试 |

### 项目结构

| 文件夹 | 内容 |
|--------|------|
| /blends | Blender 文件 |
| /build | 编译后的游戏文件 |
| /kha | 引擎源码 |
| /libraries | 外部库 |

### 构建目标

| 目标 | 平台 | 输出 |
|------|------|------|
| Browser | Web | HTML5/JavaScript |
| Windows | 桌面 | .exe |
| macOS | 桌面 | .app |
| Linux | 桌面 | 二进制文件 |
| Android | 移动 | .apk |
| iOS | 移动 | .ipa |

## 渲染

### 渲染设置

| 设置 | 描述 | 选项 |
|------|------|------|
| 渲染器 | 渲染方法 | Forward、Deferred |
| 阴影 | 阴影质量 | 无、低、中、高 |
| 抗锯齿 | 边缘平滑 | 无、FXAA、MSAA |
| 反射 | 反射质量 | 无、SSR、平面 |
| 全局光照 | 间接照明 | 无、GI 探针 |
| 体积效果 | 雾、云 | 开/关 |

### 材质系统

| 材质类型 | 描述 | 使用场景 |
|----------|------|----------|
| PBR | 基于物理 | 写实表面 |
| Unlit | 无照明 | UI、特效 |
| Decal | 投射纹理 | 损坏、污渍 |
| Terrain | 地形 | 地面表面 |

### PBR 材质属性

| 属性 | 描述 | 贴图 |
|------|------|------|
| Albedo | 基础颜色 | 颜色纹理 |
| Normal | 表面细节 | 法线贴图 |
| Metallic | 金属 vs 电介质 | 值或纹理 |
| Roughness | 表面光滑度 | 值或纹理 |
| Ambient Occlusion | 接触阴影 | AO 贴图 |
| Emission | 自发光 | 发光贴图 |

## 逻辑节点

### 节点类别

| 类别 | 用途 | 示例 |
|------|------|------|
| Event | 触发器 | On start、On update、On key |
| Logic | 条件 | Branch、Boolean、Gate |
| Math | 计算 | Add、Multiply、Vector |
| Transform | 对象移动 | Set position、Rotate |
| Animation | 播放动画 | Action、Blend |
| Physics | 物理交互 | Apply force、Raycast |
| Audio | 声音播放 | Play sound、Listener |
| UI | 用户界面 | Set text、Button |
| Variable | 数据存储 | Get/Set variable |

### 基本移动示例

| 节点 | 连接 | 用途 |
|------|------|------|
| On Update | -> | 每帧运行 |
| Keyboard (W) | -> | 检测 W 键 |
| Get Location | -> | 获取当前位置 |
| Vector Math (Add) | -> | 添加移动 |
| Set Location | -> | 应用新位置 |

### 基于节点的逻辑示例

```
[On Keyboard] -> [Branch (Is Down)] -> [Apply Force]
                      ↓
              [Get Forward Vector] -> [Multiply Scalar] -> [Force Input]
```

## 物理

### 物理类型

| 类型 | 描述 | 使用场景 |
|------|------|----------|
| Static | 不移动 | 墙壁、地板 |
| Kinematic | 脚本控制移动 | 玩家控制器 |
| Dynamic | 物理驱动 | 道具、碎片 |
| Rigid Body | 完整物理 | 有质量的物体 |
| Soft Body | 可变形 | 布料、果冻 |
| Vehicle | 汽车物理 | 汽车、自行车 |

### 物理属性

| 属性 | 描述 |
|------|------|
| Mass | 物体重量 |
| Friction | 表面阻力 |
| Restitution | 弹性 |
| Damping | 运动衰减 |
| Collision shape | 碰撞形状（盒子、球体、网格） |

### 碰撞设置

| 步骤 | 操作 |
|------|------|
| 1 | 选择对象 |
| 2 | 添加物理类型（Rigid Body） |
| 3 | 设置碰撞形状 |
| 4 | 配置质量和摩擦 |
| 5 | 在游戏中测试 |

## 脚本

### Haxe 脚本

Haxe 是 Armory 的主要脚本语言。

```haxe
import iron.Scene;
import iron.object.Object;

class MyBehavior extends iron.Trait {
    var speed:Float = 5.0;
    
    public function new() {
        super();
        notifyOnInit(init);
        notifyOnUpdate(update);
    }
    
    function init() {
        trace("Object initialized");
    }
    
    function update() {
        if (iron.system.Input.getKeyboard().down("w")) {
            object.transform.move(0, speed * iron.system.Time.delta, 0);
        }
    }
}
```

### 脚本 API

| 函数 | 描述 |
|------|------|
| `notifyOnInit()` | 对象创建时运行 |
| `notifyOnUpdate()` | 每帧运行 |
| `notifyOnRemove()` | 销毁时运行 |
| `object.transform` | 访问变换 |
| `iron.system.Input` | 输入处理 |
| `iron.system.Time` | 时间工具 |

## 动画

### 动画类型

| 类型 | 描述 | 使用场景 |
|------|------|----------|
| Skeletal | 基于骨骼 | 角色 |
| Shape keys | 变形目标 | 面部表情 |
| Material | 属性动画 | 颜色、发光 |
| Object | 变换动画 | 移动、旋转 |

### 动画设置

| 步骤 | 操作 |
|------|------|
| 1 | 在 Blender 中创建骨架 |
| 2 | 绑定角色网格 |
| 3 | 创建动作条 |
| 4 | 在逻辑中使用 Animation 节点 |
| 5 | 在动画之间混合 |

## 音频

### 音频功能

| 功能 | 描述 |
|------|------|
| 3D 空间音频 | 空间中定位的声音 |
| 距离衰减 | 基于距离的音量 |
| 多普勒效应 | 移动时的音调变化 |
| 混响区域 | 环境音频 |
| 背景音乐 | 非定位音频 |

### 音频设置

| 步骤 | 操作 |
|------|------|
| 1 | 导入音频文件 |
| 2 | 创建扬声器对象 |
| 3 | 添加 Play Sound 节点 |
| 4 | 配置 3D 属性 |
| 5 | 在摄像机上设置监听器 |

## 用户界面

### UI 元素

| 元素 | 描述 |
|------|------|
| Text | 显示文本 |
| Button | 可点击按钮 |
| Image | 显示图片 |
| Progress bar | 加载/生命条 |
| Slider | 数值输入 |

### UI 设置

| 步骤 | 操作 |
|------|------|
| 1 | 创建 UI 画布 |
| 2 | 添加 UI 元素 |
| 3 | 在屏幕空间中定位 |
| 4 | 连接到逻辑节点 |
| 5 | 使用材质设置样式 |

## 性能优化

| 优化 | 技术 | 影响 |
|------|------|------|
| LOD | 细节层次 | 高 |
| 遮挡剔除 | 隐藏不可见对象 | 高 |
| 实例化 | 复用网格数据 | 高 |
| 纹理图集 | 合并纹理 | 中 |
| 烘焙 | 预计算照明 | 高 |
| 压缩 | 减少资源大小 | 中 |

## 故障排除

| 问题 | 原因 | 解决方案 |
|------|------|----------|
| 黑屏 | 摄像机错误 | 设置活动摄像机 |
| 无物理 | 缺少碰撞 | 添加物理类型 |
| FPS 低 | 对象过多 | 优化场景 |
| 纹理缺失 | 路径错误 | 检查纹理路径 |
| 构建错误 | 代码问题 | 检查脚本语法 |

## 更多资源

| 资源 | URL |
|------|-----|
| 官方网站 | armory3d.org |
| GitHub | github.com/armory3d/armory |
| 文档 | armory3d.org/manual |
| 社区 | armory3d.org/forum |


---

## 来源：opensubdiv.md

## 简介

OpenSubdiv 是一套开源库，用于在大规模并行 CPU 和 GPU 架构上求值和渲染细分曲面。由 Pixar 开发，现由 Academy Software Foundation 维护，它是细分曲面计算的行业标准。

细分曲面允许艺术家使用简单的控制笼对复杂的有机形状进行建模，在渲染时进行平滑细分。

## 什么是细分曲面？

细分曲面由粗糙的控制网格和一组细分规则定义。在每个级别，网格通过根据这些规则添加新的顶点和面来进行细化。

| 模型类型 | 控制网格 | 细分结果 |
|----------|----------|----------|
| 简单立方体 | 6 个面，8 个顶点 | 平滑的类球体形状 |
| 角色头部 | ~500 个面 | 数百万个平滑多边形 |
| 车辆 | ~2000 个面 | 平滑的面板和曲线 |

### 为什么使用细分曲面？

| 优势 | 描述 |
|------|------|
| 平滑曲面 | 在奇异点处 C2 连续 |
| 拓扑灵活性 | 任何网格拓扑都适用 |
| 内存效率 | 小控制笼，详细结果 |
| 动画友好 | 变形控制网格，而非密集网格 |
| 行业标准 | 所有主要 DCC 工具都使用 |

## 细分方案

OpenSubdiv 支持多种细分方案。

| 方案 | 创建者 | 属性 | 用例 |
|------|--------|------|------|
| Catmull-Clark | Catmull & Clark | 规则处 C2，奇异处 C1 | 电影角色 |
| Loop | Charles Loop | 基于三角形，规则处 C2 | 游戏角色 |
| Bilinear | - | 简单边分割 | 平面面板 |

### Catmull-Clark 规则

| 元素 | 规则 | 结果 |
|------|------|------|
| 面点 | 面顶点的平均值 | 每个面的中心 |
| 边点 | 边端点 + 相邻面点的平均值 | 平滑的边中点 |
| 顶点点 | 邻域的加权平均值 | 平滑的顶点位置 |

## 求值模式

OpenSubdiv 提供多种求值方法。

| 模式 | 描述 | 性能 | 用例 |
|------|------|------|------|
| CPU Uniform | 标准 CPU 细分 | 良好 | 离线渲染 |
| CPU Feature Adaptive | 自适应细化 | 更好 | 动画 |
| GPU Compute | OpenCL/CUDA 内核 | 最快 | 实时预览 |
| GPU Vertex | 顶点着色器方法 | 快 | 游戏引擎 |

## 安装

### 从源码构建

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

### 依赖项

| 依赖 | 必需 | 用途 |
|------|------|------|
| CMake | 是 | 构建系统 |
| TBB | 可选 | 多线程 |
| OpenCL | 可选 | GPU 计算 |
| CUDA | 可选 | NVIDIA GPU 计算 |
| OpenGL | 可选 | GPU 渲染 |
| GLFW | 可选 | 示例 |

### 包管理器

| 平台 | 命令 |
|------|------|
| macOS | `brew install opensubdiv` |
| Ubuntu | `sudo apt install libopensubdiv-dev` |
| vcpkg | `vcpkg install opensubdiv` |

## 核心概念

### 拓扑细化

拓扑细化决定网格连接在每个级别如何变化。

| 级别 | 描述 | 顶点数倍增 |
|------|------|------------|
| 0 | 控制笼 | 1x |
| 1 | 第一次细分 | ~4x (Catmull-Clark) |
| 2 | 第二次细分 | ~16x |
| N | 第 N 次细分 | ~4^N x |

### 面片表

面片表存储细分面片的求值数据。它们对于高效的 GPU 求值至关重要。

| 面片类型 | 顶点数 | 形状 | 用途 |
|----------|--------|------|------|
| Regular | 16 | 4x4 网格 | 内部面片 |
| Boundary | 12 | 边面片 | 网格边界 |
| Corner | 9 | 角面片 | 网格角落 |
| Gregory | 20 | Gregory 面片 | 奇异点 |

### 特征自适应细化

特征自适应细化不是均匀地细分整个网格，而是仅在奇异顶点和锐利特征附近进行细分。

| 区域 | 细分 | 原因 |
|------|------|------|
| 规则内部 | 解析面片 | 高效 GPU 求值 |
| 奇异点附近 | 额外级别 | 平滑收敛 |
| 锐利折痕 | 额外级别 | 精确折痕求值 |
| 边界 | 额外级别 | 正确的边界行为 |

## API 概览

### 模板表

模板表预先计算求值曲面上任意点所需的权重。

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

| 层 | 用例 |
|----|------|
| HBR | 正确性测试、旧版兼容 |
| FAR | 生产细分、CPU 渲染 |
| OSD | 实时预览、游戏引擎 |

## GPU 求值

OpenSubdiv 通过多种后端支持 GPU 加速求值。

| 后端 | API | 供应商支持 | 性能 |
|------|-----|------------|------|
| OpenGL Compute | GLSL 4.3+ | 全部 | 非常快 |
| OpenCL | OpenCL 1.2+ | 全部 | 非常快 |
| CUDA | CUDA | NVIDIA | 最快 |
| DirectX Compute | HLSL | Windows | 非常快 |

### OpenGL 计算着色器示例

```cpp
#include <opensubdiv/osd/glPatchTable.h>
#include <opensubdiv/osd/glVertexBuffer.h>

// 创建 GPU 缓冲区
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

折痕定义平滑曲面上的锐利边。

| 折痕权重 | 效果 |
|----------|------|
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
|------|-----------------|------|
| Maya | 原生 Viewport 2.0 | GPU 细分显示 |
| Houdini | 视口细分 | 实时反馈 |
| Blender | 细分修改器 | CPU 和 GPU 模式 |
| Katana | 渲染时细分 | 属性驱动 |
| 3ds Max | TurboSmooth 集成 | 基于插件 |

## 性能比较

| 配置 | 细分时间（1M 面到 4M 面） | 内存 |
|------|---------------------------|------|
| CPU 单线程 (HBR) | 1200ms | 低 |
| CPU 多线程 (FAR) | 180ms | 中 |
| GPU Compute (OSD) | 8ms | 较高 |
| 特征自适应 (FAR) | 90ms | 中 |
| 特征自适应 (OSD) | 4ms | 较高 |

## 最佳实践

| 实践 | 建议 |
|------|------|
| 拓扑 | 保持控制笼尽可能简单 |
| 折痕 | 谨慎使用，优先使用平滑过渡 |
| 级别 | 显示用 3-4 级，渲染用更多 |
| 面片 | 启用面片表以进行 GPU 求值 |
| 自适应 | 对复杂网格使用特征自适应 |
| 内存 | 高细分级别时监控 GPU 内存 |

## 附加资源

| 资源 | URL |
|------|-----|
| 文档 | opensubdiv.org |
| GitHub | github.com/AcademySoftwareFoundation/OpenSubdiv |
| Pixar 技术备忘录 | Graphics.pixar.com/opensubdiv |
| SIGGRAPH 论文 | Graphics.pixar.com |


---

## 来源：openvdb.md

## 简介

OpenVDB 是一个用于存储、操作和渲染稀疏体积数据的开源库。由 DreamWorks Animation 开发，现由 Academy Software Foundation 维护，它已成为电影和视觉效果中体积效果的行业标准。

OpenVDB 使用分层数据结构，仅高效存储包含数据的空间区域，使得处理极大的体积数据集而不耗尽内存成为可能。

## 为什么体积数据很重要

许多自然现象本质上是三维的，无法用表面网格表示。体积数据可以准确捕捉这些效果。

| 现象 | 传统方法 | OpenVDB 方法 |
|------|----------|--------------|
| 烟雾 | Billboard 精灵 | 完整 3D 模拟 |
| 火焰 | 2D 纹理 | 体积发射 |
| 云 | 分层卡片 | 真实 3D 密度场 |
| 液体 | 表面网格 | SDF + 速度场 |
| 雾 | 均匀密度 | 空间变化密度 |
| 爆炸 | 粒子精灵 | 动态体积网格 |

## 核心数据结构

OpenVDB 使用具有三级节点的 B+ 树结构。

| 级别 | 节点大小 | 用途 | 典型数量 |
|------|----------|------|----------|
| 根 | 512^3（坐标范围） | 顶层索引 | 1 |
| 内部 | 4^3 或 8^3 | 中层分支 | 数千 |
| 叶 | 8^3（512 体素） | 实际体素数据 | 数百万 |

### 稀疏 vs 密集存储

| 存储类型 | 内存 | 数据访问 | 用例 |
|----------|------|----------|------|
| 密集 | O(n^3) | 直接索引 | 小体积 |
| 稀疏 (VDB) | O(活跃体素) | 树遍历 | VFX 体积 |
| 稀疏（自适应） | 不定 | 多分辨率 | 水平集 |

### 网格类型

| 网格类型 | 值类型 | 典型用途 |
|----------|--------|----------|
| FloatGrid | float | 密度、温度 |
| Vec3fGrid | Vector3f | 速度、颜色 |
| Int32Grid | int32_t | 标签、ID |
| BoolGrid | bool | 蒙版 |
| DoubleGrid | double | 高精度标量 |
| HalfGrid | half | 节省内存的浮点 |

## 安装

### 从源码构建

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

### 依赖项

| 依赖 | 必需 | 用途 |
|------|------|------|
| Boost | 是 | 智能指针、IO |
| TBB | 是 | 多线程 |
| OpenEXR | 是 | 半精度浮点支持 |
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

### 读取和写入 VDB 文件

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

### 过滤操作

| 操作 | 函数 | 用例 |
|------|------|------|
| 均值 | `tools::mean` | 平滑 |
| 高斯 | `tools::gaussian` | 模糊 |
| 中值 | `tools::median` | 降噪 |
| 膨胀 | `tools::dilate` | 扩展区域 |
| 腐蚀 | `tools::erode` | 收缩区域 |
| 偏移 | `tools::offset` | 水平集偏移 |

### 转换工具

| 转换 | 从 | 到 | 用例 |
|------|------|------|------|
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

| 功能 | 描述 |
|------|------|
| 多网格 | 每个文件多个网格 |
| 压缩 | Blosc、ZIP 或无 |
| 元数据 | 每个网格的键值对 |
| 部分 I/O | 读取/写入特定网格 |
| 流式传输 | 顺序读取支持 |

### 文件结构

| 部分 | 内容 | 描述 |
|------|------|------|
| 头部 | 魔数、版本 | 文件标识 |
| 网格描述符 | 名称、类型、变换 | 网格元数据 |
| 树数据 | B+ 树节点 | 体素数据 |
| 元数据 | 键值对 | 自定义属性 |
| 尾部 | 校验和 | 完整性验证 |

## 与 VFX 工具的集成

| 工具 | OpenVDB 集成 | 备注 |
|------|--------------|------|
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

# 写入以进行网格化
openvdb.write("levelset.vdb", sphere)
```

## 性能优化

| 优化 | 技术 | 影响 |
|------|------|------|
| 体素大小 | 使用可接受的最大尺寸 | 高 |
| 压缩 | 启用 Blosc 压缩 | 中 |
| 稀疏访问 | 使用访问器，而非直接迭代 | 高 |
| 变换 | 在变换中使用适当的体素大小 | 中 |
| 背景值 | 设置为空空间的典型值 | 低 |
| 线程数 | TBB 自动检测核心数 | 高 |

## 最佳实践

| 实践 | 建议 |
|------|------|
| 网格命名 | 为每个网格使用描述性名称 |
| 体素大小 | 匹配所需的细节级别 |
| 压缩 | 文件存储时启用，计算时禁用 |
| 水平集 | 保持窄带宽度一致 |
| 元数据 | 在网格元数据中存储模拟参数 |
| 内存 | 模拟期间监控活跃体素数量 |

## 附加资源

| 资源 | URL |
|------|-----|
| 文档 | openvdb.org |
| GitHub | github.com/AcademySoftwareFoundation/openvdb |
| API 参考 | openvdb.org/documentation |
| SIGGRAPH 课程 | openvdb.org/documentation |


---

## 来源：subdiv.md

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


---
