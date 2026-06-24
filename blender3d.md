# Armory：Blender 用 3D 游戏引擎

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
