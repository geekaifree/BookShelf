# 游戏

> 本文档整合了以下源文件：game.md, gameart.md, games.md, gameDev.md

---

## 来源：game.md

## 简介

Armory 是一款直接集成到 Blender 中的开源 3D 游戏引擎。它允许游戏开发者使用 Blender 熟悉的界面创建 3D 游戏，无需离开应用程序。Armory 提供完整的游戏开发环境，包括渲染、物理、逻辑和脚本功能。

通过利用 Blender 现有的工具，Armory 消除了学习单独游戏引擎的需要，同时提供专业级功能。

## 为什么使用 Armory？

| 特性 | Armory | Unity | Unreal | Godot |
|------|--------|-------|--------|-------|
| Blender 集成 | 原生 | 导出 | 导出 | 导出 |
| 费用 | 免费 | 免费增值 | 5% 版税 | 免费 |
| 开源 | 是 | 否 | 源码可用 | 是 |
| 学习曲线 | 低（Blender 用户） | 中 | 高 | 中 |
| 工作流 | 集成 | 分离 | 分离 | 分离 |
| 2D 支持 | 是 | 是 | 有限 | 是 |

## 核心功能

| 功能 | 描述 |
|------|------|
| Blender 集成 | 无需导出/导入 |
| PBR 渲染 | 基于物理的渲染 |
| 节点逻辑 | 可视化编程系统 |
| 物理引擎 | 刚体、软体、布料 |
| 脚本 | Haxe、Python、JavaScript |
| 网络 | 多人游戏支持 |
| 音频 | 3D 空间音频 |
| 动画 | 骨骼和混合形状 |
| 粒子 | GPU 粒子系统 |
| UI 系统 | 游戏内用户界面 |

## 安装

### 要求

| 要求 | 版本 |
|------|------|
| Blender | 3.0+ |
| 操作系统 | Windows, macOS, Linux |
| GPU | OpenGL 3.3+ 或 Vulkan |
| 内存 | 4GB 最低 |
| 存储 | 2GB 用于引擎 |

### 安装 Armory

1. 从 armory3d.org 下载 Armory
2. 解压归档文件
3. 在 Blender 中：编辑 > 偏好设置 > 插件
4. 点击"安装"并选择 Armory zip
5. 启用 "Armory" 插件

### 验证安装

| 步骤 | 操作 |
|------|------|
| 1 | 打开 Blender |
| 2 | 检查属性面板中是否有 "Armory" 选项卡 |
| 3 | 选择渲染引擎：Armory |
| 4 | 验证游戏逻辑节点可用 |

## 项目设置

### 创建新项目

| 步骤 | 操作 |
|------|------|
| 1 | 打开 Blender |
| 2 | 设置渲染引擎为 "Armory" |
| 3 | 配置项目设置 |
| 4 | 保存 .blend 文件 |
| 5 | 点击"播放"测试 |

### 项目结构

| 文件夹 | 内容 |
|-------|------|
| /blends | Blender 文件 |
| /build | 编译后的游戏文件 |
| /kha | 引擎源码 |
| /libraries | 外部库 |

### 构建目标

| 目标 | 平台 | 输出 |
|------|------|------|
| 浏览器 | Web | HTML5/JavaScript |
| Windows | 桌面 | .exe |
| macOS | 桌面 | .app |
| Linux | 桌面 | 二进制 |
| Android | 移动 | .apk |
| iOS | 移动 | .ipa |

## 渲染

### 渲染设置

| 设置 | 描述 | 选项 |
|------|------|------|
| 渲染器 | 渲染方法 | Forward, Deferred |
| 阴影 | 阴影质量 | 无, 低, 中, 高 |
| 抗锯齿 | 边缘平滑 | 无, FXAA, MSAA |
| 反射 | 反射质量 | 无, SSR, 平面 |
| 全局光照 | 间接光照 | 无, GI 探针 |
| 体积效果 | 雾、云 | 开/关 |

### 材质系统

| 材质类型 | 描述 | 使用场景 |
|---------|------|---------|
| PBR | 基于物理 | 真实表面 |
| Unlit | 无光照 | UI、特效 |
| 贴花 | 投射纹理 | 损坏、污垢 |
| 地形 | 景观 | 地面 |

### PBR 材质属性

| 属性 | 描述 | 贴图 |
|------|------|------|
| Albedo | 基础颜色 | 颜色纹理 |
| Normal | 表面细节 | 法线贴图 |
| Metallic | 金属 vs 电介质 | 值或纹理 |
| Roughness | 表面光滑度 | 值或纹理 |
| 环境遮蔽 | 接触阴影 | AO 贴图 |
| Emission | 自发光 | 发光贴图 |

## 逻辑节点

### 节点类别

| 类别 | 用途 | 示例 |
|------|------|------|
| 事件 | 触发器 | 开始时、更新时、按键时 |
| 逻辑 | 条件 | 分支、布尔、门 |
| 数学 | 计算 | 加、乘、向量 |
| 变换 | 对象移动 | 设置位置、旋转 |
| 动画 | 播放动画 | 动作、混合 |
| 物理 | 物理交互 | 施加力、射线检测 |
| 音频 | 声音播放 | 播放声音、监听器 |
| UI | 用户界面 | 设置文本、按钮 |
| 变量 | 数据存储 | 获取/设置变量 |

### 基本移动示例

| 节点 | 连接 | 用途 |
|------|------|------|
| 更新时 | → | 每帧运行 |
| 键盘 (W) | → | 检测 W 键 |
| 获取位置 | → | 获取当前位置 |
| 向量数学 (加法) | → | 添加移动 |
| 设置位置 | → | 应用新位置 |

### 节点逻辑示例

```
[键盘按下] → [分支 (是否按下)] → [施加力]
                      ↓
              [获取前方向量] → [标量乘法] → [力输入]
```

## 物理

### 物理类型

| 类型 | 描述 | 使用场景 |
|------|------|---------|
| 静态 | 不移动 | 墙壁、地板 |
| 运动学 | 脚本控制移动 | 玩家控制器 |
| 动态 | 物理驱动 | 道具、碎片 |
| 刚体 | 完全物理 | 有质量的物体 |
| 软体 | 可变形 | 布料、果冻 |
| 车辆 | 汽车物理 | 汽车、自行车 |

### 物理属性

| 属性 | 描述 |
|------|------|
| 质量 | 物体重量 |
| 摩擦 | 表面阻力 |
| 恢复系数 | 弹性 |
| 阻尼 | 运动衰减 |
| 碰撞形状 | 盒、球、网格 |

### 碰撞设置

| 步骤 | 操作 |
|------|------|
| 1 | 选择对象 |
| 2 | 添加物理类型（刚体） |
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
|------|------|---------|
| 骨骼 | 基于骨骼 | 角色 |
| 形状键 | 变形目标 | 面部表情 |
| 材质 | 属性动画 | 颜色、发光 |
| 对象 | 变换动画 | 移动、旋转 |

### 动画设置

| 步骤 | 操作 |
|------|------|
| 1 | 在 Blender 中创建骨架 |
| 2 | 绑定角色网格 |
| 3 | 创建动作片段 |
| 4 | 在逻辑中使用动画节点 |
| 5 | 在动画间混合 |

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
| 3 | 添加播放声音节点 |
| 4 | 配置 3D 属性 |
| 5 | 在摄像机上设置监听器 |

## 用户界面

### UI 元素

| 元素 | 描述 |
|------|------|
| 文本 | 显示文本 |
| 按钮 | 可点击按钮 |
| 图片 | 显示图片 |
| 进度条 | 加载/血条 |
| 滑块 | 值输入 |

### UI 设置

| 步骤 | 操作 |
|------|------|
| 1 | 创建 UI 画布 |
| 2 | 添加 UI 元素 |
| 3 | 在屏幕空间定位 |
| 4 | 连接到逻辑节点 |
| 5 | 用材质样式化 |

## 性能优化

| 优化 | 技术 | 影响 |
|------|------|------|
| LOD | 细节层次 | 高 |
| 遮挡剔除 | 隐藏不可见对象 | 高 |
| 实例化 | 重用网格数据 | 高 |
| 纹理图集 | 合并纹理 | 中 |
| 烘焙 | 预计算光照 | 高 |
| 压缩 | 减少资源大小 | 中 |

## 故障排除

| 问题 | 原因 | 解决方案 |
|------|------|---------|
| 黑屏 | 摄像机错误 | 设置活动摄像机 |
| 无物理 | 缺少碰撞 | 添加物理类型 |
| 帧率低 | 对象太多 | 优化场景 |
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

## 来源：gameart.md

## 简介

SteamGridDB 是一个自定义游戏封面的数据库和社区，包括横幅、海报、Logo 和图标。它主要用于自定义 Steam、Playnite 和 GOG Galaxy 等启动器中游戏库的视觉外观。

| 特性 | 描述 |
|---------|-------------|
| 封面数据库 | 大量的自定义游戏封面收藏 |
| 多种格式 | 横幅、海报、Logo、Hero 和图标 |
| 社区贡献 | 用户上传的封面，带有质量评分 |
| API 访问 | 通过 API 编程式访问封面数据库 |
| 启动器集成 | 与 Steam、Playnite、GOG Galaxy 等配合使用 |

## 封面类型

### Steam 封面分类

| 分类 | 尺寸 | 使用场景 |
|----------|-----------|----------|
| Grid (横向) | 460x215 | 库网格视图横幅 |
| Grid (纵向) | 342x482 | 库网格视图海报 |
| Hero | 1920x620 | 库页面背景 |
| Logo | 可变 | Hero 上的游戏 Logo 叠加 |
| Icon | 可变 | 小型游戏图标 |

### 封面尺寸

| 类型 | 宽度 | 高度 | 宽高比 |
|------|-------|--------|-------------|
| 横向 Grid | 460 | 215 | ~2.14:1 |
| 纵向 Grid | 342 | 482 | ~0.71:1 |
| Hero | 1920 | 620 | ~3.1:1 |
| Logo | 可变 | 可变 | 透明 PNG |
| Icon | 256 | 256 | 1:1 |

## 使用 SteamGridDB

### Web 界面

| 区域 | 描述 |
|---------|-------------|
| 搜索 | 按标题查找游戏 |
| 游戏页面 | 查看特定游戏的所有封面 |
| 上传 | 向数据库提交新封面 |
| 评分 | 对封面质量进行评分（1-5 星） |
| 筛选器 | 按风格、尺寸和类型筛选 |

### 搜索封面

| 步骤 | 操作 |
|------|--------|
| 1 | 访问 SteamGridDB 网站 |
| 2 | 在搜索栏中输入游戏标题 |
| 3 | 从结果中选择游戏 |
| 4 | 选择封面类型（Grid、Hero、Logo、Icon） |
| 5 | 浏览可用的封面选项 |
| 6 | 下载首选封面 |

## API 访问

### API 概述

| 特性 | 描述 |
|---------|-------------|
| Base URL | https://www.steamgriddb.com/api/v2 |
| 认证 | 需要 API 密钥（从账户设置中获取） |
| 速率限制 | 基于账户类型的请求限制 |
| 格式 | JSON 响应 |

### API 端点

| 端点 | 方法 | 描述 |
|----------|--------|-------------|
| `/games/steam/{appid}` | GET | 通过 Steam App ID 获取游戏 |
| `/games/name/{name}` | GET | 按名称搜索游戏 |
| `/grids/game/{id}` | GET | 获取游戏的 Grid 封面 |
| `/heroes/game/{id}` | GET | 获取游戏的 Hero 封面 |
| `/logos/game/{id}` | GET | 获取游戏的 Logo |
| `/icons/game/{id}` | GET | 获取游戏的 Icon |

### API 认证

```bash
# 在请求头中使用 API 密钥
curl -H "Authorization: Bearer YOUR_API_KEY" \
  https://www.steamgriddb.com/api/v2/games/steam/730
```

### 示例：获取游戏封面

```python
import requests

API_KEY = "your_api_key"
BASE_URL = "https://www.steamgriddb.com/api/v2"

headers = {"Authorization": f"Bearer {API_KEY}"}

# 搜索游戏
response = requests.get(f"{BASE_URL}/games/name/Half-Life", headers=headers)
games = response.json()["data"]

# 获取第一个结果的 Grid 封面
game_id = games[0]["id"]
grids = requests.get(f"{BASE_URL}/grids/game/{game_id}", headers=headers)

for grid in grids.json()["data"]:
    print(grid["url"], grid["width"], grid["height"])
```

## Steam 集成

### 自定义 Steam 游戏库

| 步骤 | 操作 |
|------|--------|
| 1 | 在 SteamGridDB 上找到封面 |
| 2 | 下载所需的图片 |
| 3 | 打开 Steam 并进入游戏库 |
| 4 | 右键点击游戏 |
| 5 | 选择管理 > 设置自定义封面 |
| 6 | 选择下载的图片 |

### Steam 封面类型

| Steam 设置 | 封面类型 | 显示位置 |
|--------------|-------------|------------------|
| Capsule | 横向 Grid | 库网格视图 |
| Vertical Capsule | 纵向 Grid | 库网格视图（新版） |
| Hero | Hero | 游戏详情页背景 |
| Logo | Logo | 叠加在 Hero 上 |
| Icon | Icon | 游戏列表和桌面 |

## Playnite 集成

### 自动封面下载

Playnite 可以自动从 SteamGridDB 获取封面。

| 步骤 | 操作 |
|------|--------|
| 1 | 为 Playnite 安装 SteamGridDB 插件 |
| 2 | 在插件设置中配置 API 密钥 |
| 3 | 选择要更新的游戏 |
| 4 | 运行所选游戏的封面下载 |

### 插件配置

| 设置 | 描述 |
|---------|-------------|
| API 密钥 | SteamGridDB API 认证密钥 |
| 封面类型 | 选择要下载的类型（Grid、Hero、Logo、Icon） |
| 风格偏好 | 偏好官方或自定义封面 |
| 尺寸 | 首选图片尺寸 |
| 覆盖 | 是否替换现有封面 |

## 上传封面

### 封面指南

| 指南 | 描述 |
|-----------|-------------|
| 质量 | 高分辨率，无压缩伪影 |
| 准确性 | 正确的游戏，无错误归属的封面 |
| 格式 | 透明图推荐 PNG，JPG 可接受 |
| 尺寸 | 遵循封面类型的标准尺寸 |
| 原创性 | 尽可能注明原作者 |

### 上传流程

| 步骤 | 操作 |
|------|--------|
| 1 | 创建 SteamGridDB 账户 |
| 2 | 导航到游戏页面 |
| 3 | 选择要上传的封面类型 |
| 4 | 选择图片文件 |
| 5 | 添加标签和风格信息 |
| 6 | 提交审核 |

### 封面风格

| 风格 | 描述 |
|-------|-------------|
| Official | 开发商/发行商提供的封面 |
| Alternate | 粉丝制作的替代设计 |
| Animated | GIF 或 APNG 动画封面 |
| Blurred | 模糊背景版本 |
| White | 简洁的白色/透明设计 |
| Material | Google Material Design 风格 |
| N64 | Nintendo 64 包装盒风格 |
| NSFW | 不适合工作场合的内容 |

## 社区功能

### 评分系统

| 评分 | 含义 |
|--------|---------|
| 5 星 | 优秀质量，完美可用 |
| 4 星 | 良好质量，有小问题 |
| 3 星 | 一般质量，可接受 |
| 2 星 | 低于平均，有明显问题 |
| 1 星 | 质量差，有严重问题 |

### 用户贡献

| 功能 | 描述 |
|---------|-------------|
| 上传封面 | 向数据库提交新封面 |
| 评价现有 | 对封面质量进行评分 |
| 报告问题 | 标记错误或有问题的封面 |
| 请求游戏 | 请求缺失游戏的封面 |

## 工具和实用程序

### 第三方工具

| 工具 | 描述 |
|------|-------------|
| SGDBoop | Steam 一键封面应用 |
| SteamGridDB Manager | 批量封面管理工具 |
| BoilR | 多启动器封面管理器 |

### SGDBoop 使用

| 步骤 | 操作 |
|------|--------|
| 1 | 在系统上安装 SGDBoop |
| 2 | 将其与 steamgriddb:// URL 关联 |
| 3 | 在 SteamGridDB 网站上点击 Boop 按钮 |
| 4 | 封面自动应用到 Steam |

## 总结

| 主题 | 核心要点 |
|-------|-------------|
| 数据库 | 多种格式的游戏封面大量收藏 |
| 格式 | Grid、Hero、Logo 和 Icon，具有特定尺寸 |
| 集成 | 与 Steam、Playnite、GOG Galaxy 和其他启动器配合使用 |
| API | RESTful API 编程式访问封面 |
| 社区 | 用户上传封面，带评分系统 |
| 工具 | SGDBoop 和 BoilR 实现一键封面应用 |


---

## 来源：games.md

## 策略游戏

| 游戏 | 人数 | 时长 | 说明 |
|------|---------|----------|-------------|
| Catan | 3-4 | 60-120 min | 资源 management and trading |
| Ticket to Ride | 2-5 | 30-60 min | 铁路建设 |
| Carcassonne | 2-5 | 30-45 min | 地图拼接 |
| Pandemic | 2-4 | 45-90 min | 合作对抗疾病 |
| Risk | 2-6 | 120+ min | 世界征服 |
| Terraforming Mars | 1-5 | 120+ min | 火星殖民 |

## 卡牌游戏

| 游戏 | 人数 | 时长 | 说明 |
|------|---------|----------|-------------|
| Dominion | 2-4 | 30 min | 卡牌构建 |
| 7 Wonders | 2-7 | 30 min | 文明建设 |
| Sushi Go! | 2-5 | 15 min | 卡牌选取 |
| Love Letter | 2-4 | 20 min | 推理卡牌游戏 |
| The Crew | 2-5 | 20 min | 合作 trick-taking |

## 派对游戏

| 游戏 | 人数 | 时长 | 说明 |
|------|---------|----------|-------------|
| Codenames | 4-8 | 15 min | 词语联想 |
| Dixit | 3-6 | 30 min | 故事讲述 |
| Wits & Wagers | 3-7 | 25 min | 知识竞猜 |
| Just One | 3-7 | 20 min | 合作文字游戏 |
| Telestrations | 4-8 | 30 min | 绘画电话游戏 |

## 合作游戏

| 游戏 | 人数 | 时长 | 说明 |
|------|---------|----------|-------------|
| Forbidden Island | 2-4 | 30 min | 合作冒险 |
| Flash Point | 2-6 | 45 min | 消防救援 |
| Hanabi | 2-5 | 25 min | 合作卡牌游戏 |
| Spirit Island | 1-4 | 90-120 min | 岛屿防御 |
| Gloomhaven | 1-4 | 60-120 min | 战术战斗 |

## 抽象游戏

| 游戏 | 人数 | 时长 | 说明 |
|------|---------|----------|-------------|
| Chess | 2 | 60+ min | 经典策略 |
| Go | 2 | 60+ min | 领地控制 |
| Azul | 2-4 | 30-45 min | 瓷砖拼接 |
| Santorini | 2-4 | 20 min | 3D 策略 |
| Hive | 2 | 20 min | 虫子主题策略 |

## 家庭游戏

| 游戏 | 人数 | 时长 | 说明 |
|------|---------|----------|-------------|
| Ticket to Ride: First Journey | 2-4 | 15-30 min | 儿童铁路 |
| Rhino Hero | 2-5 | 15 min | 卡牌堆叠 |
| Animal Upon Animal | 2-4 | 15 min | 动物堆叠 |
| Icecool | 2-4 | 20 min | 弹射游戏 |
| Dragomino | 2-4 | 15 min | 龙多米诺 |

## 单人游戏

| 游戏 | 时长 | 说明 |
|------|----------|-------------|
| Friday | 30 min | 单人卡牌游戏 |
| Onirim | 15 min | 单人解谜 |
| Sprawlopolis | 15-30 min | 单人城市建设 |
| Warp's Edge | 30-45 min | 单人太空战斗 |
| Under Falling Skies | 30-60 min | 单人骰子放置 |

## 主题游戏

| 游戏 | 人数 | 时长 | 说明 |
|------|---------|----------|-------------|
| Wingspan | 1-5 | 40-70 min | 鸟类收集 |
| Everdell | 1-4 | 40-80 min | 森林生物 |
| Root | 2-4 | 60-90 min | 非对称策略 |
| Scythe | 1-5 | 70-120 min | 架空历史 |
| Spirit Island | 1-4 | 90-120 min | 岛屿防御 |

## 快速游戏

| 游戏 | 人数 | 时长 | 说明 |
|------|---------|----------|-------------|
| Sushi Go! | 2-5 | 15 min | 卡牌选取 |
| Love Letter | 2-4 | 20 min | Deduction |
| The Crew | 2-5 | 20 min | 合作 trick-taking |
| Coup | 2-6 | 15 min | 虚张声势 |
| No Thanks! | 3-7 | 20 min | Card game |

## Usage Recommendations

| 场景 | Recommended 游戏s |
|-----------|-------------------|
| Family Night | Ticket to Ride, Catan, Codenames |
| Two 人数 | Patchwork, 7 Wonders Duel, Jaipur |
| Party | Codenames, Dixit, Just One |
| Solo | Friday, Onirim, Sprawlopolis |
| 策略 | Terraforming Mars, Spirit Island |
| Quick 游戏 | Sushi Go!, Love Letter, Coup |


---

## 来源：gameDev.md

本文档整理了游戏开发过程中常用的工具、引擎、素材、音效、学习资源等，按类别分类，便于快速查阅和选型。

**图例说明：**

| 标记 | 含义 |
|------|------|
| 免费 | 完全免费使用 |
| 开源 | 开源项目 |
| 付费 | 需要购买授权 |
| 部分免费 | 基础功能免费，高级功能收费 |

---

## 一、图形资源

### 1.1 素材与占位资源

| 资源 | 类型 | 说明 | 链接 |
|------|------|------|------|
| 2D Cartoon Mobile Game UI Pack | 免费 | 卡通风格 UI 素材包，PSD 分层文件 | [链接](http://graphicburger.com/mobile-game-gui/) |
| 420 Pixel Art Icons for RPGs | 免费 | 420 个 RPG 像素图标，可商用 | [链接](http://7soul1.deviantart.com/art/420-Pixel-Art-Icons-for-RPG-129892453) |
| Blender 3D Models | 免费 | 3D 模型与粒子特效 | [链接](https://www.blender-models.com/) |
| CGTextures | 部分免费 | 大型纹理素材库 | [链接](http://www.textures.com) |
| GameDev Market | 部分免费 | 独立开发者与素材创作者的社区市场 | [链接](https://www.gamedevmarket.net/) |
| Games-Icons Set | 免费 | 游戏图标素材集 | [链接](http://game-icons.net/) |
| Iconmonstr | 免费 | 免费图标资源 | [链接](http://iconmonstr.com/) |
| Kenney Assets | 部分免费 | 免版税游戏素材 | [链接](http://kenney.nl/assets) |
| Liberated Pixel Cup | 免费 | OpenGameArt 论坛的免费图形素材 | [链接](http://lpc.opengameart.org) |
| Matcaps | 免费 | 大型 MatCap 纹理库（PNG/ZMT） | [链接](https://github.com/nidorx/matcaps#matcaps) |
| OpenGameArt | 免费 | 自由软件游戏项目的媒体素材库 | [链接](http://opengameart.org/) |
| Oryx Design Lab | 付费 | 高质量免版税精灵素材 | [链接](http://oryxdesignlab.com/) |
| PlainTextures | 部分免费 | 高分辨率纹理、笔刷和照片 | [链接](http://www.plaintextures.com/) |
| Pixelicious | 免费 | 图片转像素画工具 | [链接](https://www.pixelicious.xyz/) |
| Poly Pizza | 免费 | 6000+ 低多边形免费模型 | [链接](https://poly.pizza) |
| Quaternius | 免费 | 数千个 CC0 低多边形 3D 模型和动画角色 | [链接](https://quaternius.com/) |
| Reiner's Tilesets | 免费 | 2D/3D 免费图形素材博客 | [链接](http://www.reinerstilesets.de/) |
| Sketchfab | 免费 | 3D 模型发布与嵌入平台 | [链接](https://sketchfab.com/) |
| SpriteLib | 免费 | 静态与动画图形对象（精灵）集合 | [链接](http://www.widgetworx.com/spritelib/) |
| StickyPNG | 免费 | 免费透明 PNG 图片 | [链接](http://www.stickpng.com/) |
| TextureHaven | 免费 | 免费纹理，含置换贴图、凹凸贴图及 HDRI | [链接](https://texturehaven.com/) |
| TextureKing | 免费 | 免费材质纹理素材 | [链接](http://www.textureking.com/) |
| Vecteezy | 部分免费 | 免费矢量艺术素材 | [链接](http://www.vecteezy.com/) |

### 1.2 精灵表工具

| 资源 | 类型 | 说明 | 链接 |
|------|------|------|------|
| Cheetah-Texture-Packer | 开源 | 高效快速的 2D 装箱工具 | [链接](https://github.com/scriptum/Cheetah-Texture-Packer) |
| EzSpriteSheet | 开源 | 从 GIF 动画等创建精灵表 | [链接](https://github.com/z64me/EzSpriteSheet) |
| Libgdx Texture Packer | 开源 | LibGDX 内置纹理打包器 | [链接](https://github.com/libgdx/libgdx/wiki/Texture-packer) |
| Littera | 免费 | 位图字体生成器 | [链接](http://kvazars.com/littera) |
| SnowB Bitmap Font | 开源 | 位图字体生成器 | [链接](https://snowb.org/) |
| ShoeBox | 免费 | 基于 Adobe Air 的游戏与 UI 工具集 | [链接](http://renderhjs.net/shoebox/) |
| TexturePacker | 部分免费 | 专业精灵表创建编辑器 | [链接](https://www.codeandweb.com/texturepacker) |
| Tilesplit | 开源 | CLI 精灵表拆分工具，支持模板和非统一尺寸 | [链接](https://github.com/AlexPoulsen/tilesplit) |

### 1.3 位图压缩

| 资源 | 类型 | 说明 | 链接 |
|------|------|------|------|
| ImageAlpha | 开源 | macOS 上 pngquant 的 GUI 工具 | [链接](http://pngmini.com/) |
| Photo Resizer In KB | 免费 | 在线图片压缩工具 | [链接](https://photoresizerinkb.com/) |
| PNGGauntlet | 免费 | PNG 压缩工具，加速网站加载 | [链接](http://pnggauntlet.com/) |
| PNGoo | 免费 | Windows 批量 PNG 转换 GUI | [链接](https://pngquant.org/PNGoo.0.1.1.zip) |
| Pngyu | 开源 | 简洁的 PNG 图片压缩工具 | [链接](http://nukesaq88.github.io/Pngyu/) |
| TinyPNG | 部分免费 | 高级有损压缩，保留完整 Alpha 透明度 | [链接](https://tinypng.com/) |

### 1.4 纹理工具

| 资源 | 类型 | 说明 | 链接 |
|------|------|------|------|
| FilterForge | 付费 | Photoshop 插件，可自建滤镜 | [链接](https://www.filterforge.com/) |
| Live Normal | 免费 | 移动端无缝材质生成工具，支持 PBR 贴图输出 | [链接](https://tenebrislab.github.io/livenormal/) |
| PixPlant | 付费 | 从照片生成法线、置换、高光贴图及无缝纹理 | [链接](http://www.pixplant.com/) |

### 1.5 角色生成器

| 资源 | 类型 | 说明 | 链接 |
|------|------|------|------|
| Charas | 免费 | RPG Maker 角色集生成器 | [链接](http://charas-project.net/index.php) |

### 1.6 瓦片/关卡编辑器

| 资源 | 类型 | 说明 | 链接 |
|------|------|------|------|
| AutoTileGen | 付费 | 2D 地形自动瓦片集生成器 | [链接](http://pixelatto.com) |
| LDtk | 开源 | 面向独立开发者的 2D 关卡编辑器，注重易用性 | [链接](https://deepnight.net/tools/ldtk-2d-level-editor/) |
| MapperMate | 部分免费 | 基于浏览器的云瓦片地图编辑器 | [链接](https://mappermate.com/) |
| Material Maker | 开源 | 基于 Godot 的程序化纹理创建工具 | [链接](https://github.com/RodZill4/material-maker) |
| OGMO Editor | 开源 | 通用关卡编辑器 | [链接](https://ogmo-editor-3.github.io/) |
| Overlap2D | 开源 | 引擎无关的 2D 关卡与 UI 编辑器 | [链接](https://github.com/UnderwaterApps/overlap2d/) |
| Sprite Fusion | 免费 | 浏览器端 2D 瓦片地图关卡设计工具 | [链接](https://spritefusion.com/) |
| Tiled | 开源 | 免费、易用、灵活的瓦片地图编辑器 | [链接](http://www.mapeditor.org/) |

### 1.7 动画工具

| 资源 | 类型 | 说明 | 链接 |
|------|------|------|------|
| Cascadeur | 部分免费 | 基于物理的 3D 角色动画工具 | [链接](https://cascadeur.com/) |
| LWF | 开源 | 轻量级动画引擎，支持 HTML5/Unity/Cocos2d-x 等 | [链接](http://gree.github.io/lwf/) |
| Fusion Character Animator | 付费 | Clickteam Fusion 2.5 的 2D 角色动画工具 | [链接](http://loopengo.free.fr/) |
| GraphicsGale | 免费 | 精灵与像素画动画工具 | [链接](https://graphicsgale.com/us/) |
| Mixamo | 付费 | 3D 人形模型自动绑定与动画工具 | [链接](https://www.mixamo.com/#/) |
| Pixel Composer | 开源 | 像素画节点式 VFX 编辑器 | [链接](https://github.com/Ttanasart-pt/Pixel-Composer) |
| Spine | 付费 | 专业 2D 骨骼动画工具 | [链接](http://esotericsoftware.com/) |
| Spriter Pro | 付费 | 现代精灵动画工具 | [链接](https://brashmonkey.com/download-spriter-pro/) |

### 1.8 矢量/图像编辑器

| 资源 | 类型 | 说明 | 链接 |
|------|------|------|------|
| Affinity Designer | 付费 | 矢量图形编辑器，支持 Adobe 文件格式 | [链接](https://affinity.serif.com/de/designer) |
| Affinity Photo | 付费 | 照片与光栅图形编辑器 | [链接](https://affinity.serif.com/de/photo) |
| Aseprite | 部分免费 | 动画精灵编辑器与像素画工具 | [链接](http://www.aseprite.org/) |
| GIMP | 开源 | GNU 图像处理程序，免费图像编辑 | [链接](http://www.gimp.org/) |
| Inkscape | 开源 | 开源矢量图形编辑器 | [链接](https://inkscape.org/en/) |
| Krita | 开源 | 专业免费开源绘画程序 | [链接](https://krita.org/) |
| LibreSprite | 开源 | Aseprite 的开源分支 | [链接](https://libresprite.github.io/) |
| Paint.NET | 部分免费 | Windows 免费图像编辑软件 | [链接](http://www.getpaint.net/) |
| PiskelApp | 免费 | 在线像素画与动画精灵工具 | [链接](http://www.piskelapp.com/) |
| Squoosh | 开源 | 浏览器端图片压缩工具 | [链接](https://squoosh.app) |
| SVGcode | 开源 | 将光栅图片转换为 SVG 矢量图的 PWA 工具 | [链接](https://svgco.de/) |
| Vector Magic | 部分免费 | 光栅转矢量图形工具 | [链接](https://vectormagic.com/) |
| VTracer | 开源 | 基于 visioncortex 的光栅转矢量工具 | [链接](https://www.visioncortex.org/vtracer/) |

### 1.9 建模工具

| 资源 | 类型 | 说明 | 链接 |
|------|------|------|------|
| 3ds Max | 付费 | Autodesk 专业 3D 建模软件 | [链接](http://www.autodesk.com/products/3ds-max/overview) |
| Blender | 开源 | 免费开源 3D 创作套件 | [链接](http://www.blender.org/) |
| Daz 3D | 部分免费 | 快速创建自定义场景和角色的 3D 软件 | [链接](https://www.daz3d.com/) |
| MakeHuman | 免费 | 开源人形角色创建工具 | [链接](http://www.makehumancommunity.org/) |
| Maya | 付费 | Autodesk 专业 3D 动画与建模软件 | [链接](http://www.autodesk.com/products/maya/overview) |
| Spline | 部分免费 | 实时协作 3D 设计工具 | [链接](https://spline.design/) |
| ZBrush | 付费 | 专业数字雕刻工具 | [链接](https://pixologic.com/) |

### 1.10 地形生成器

| 资源 | 类型 | 说明 | 链接 |
|------|------|------|------|
| Canyon Terrain Editor | 免费 | 快速直观地创建高质量逼真地形 | [链接](https://entardev.wordpress.com/other-projects/canyon-terrain-editor/) |
| DEM Net Elevation API | 开源 | 基于真实数据的实时 3D 纹理地形生成 | [链接](https://elevationapi.com) |
| Fracplanet | 开源 | 分形行星与地形生成器 | [链接](https://sourceforge.net/projects/fracplanet/) |
| World Creator | 付费 | GPU 实时程序化地形与景观生成 | [链接](https://www.world-creator.com/) |
| World Machine | 付费 | 程序化地形创建与自然模拟 | [链接](http://www.world-machine.com/) |

### 1.11 体素编辑器

| 资源 | 类型 | 说明 | 链接 |
|------|------|------|------|
| goxel | 开源 | 开源体素编辑器 | [链接](https://github.com/guillaumechereau/goxel) |
| MagicaVoxel | 免费 | 轻量体素编辑器 | [链接](https://ephtracy.github.io/) |
| Sproxel | 免费 | 体素编辑器 | [链接](http://sproxel.blogspot.com.br/) |
| Voxelle Desktop | 免费 | 桌面体素编辑器 | [链接](https://github.com/Velfi/Voxelle-Desktop) |

---

## 二、代码与引擎

### 2.1 游戏引擎与框架

以下按编程语言分类整理主流游戏引擎和框架。

#### C/C++

| 引擎 | 类型 | 说明 | 链接 |
|------|------|------|------|
| Allegro | 开源 | 跨平台游戏编程库 | [链接](http://liballeg.org/) |
| Astera | 开源 | 2D C99 跨平台游戏库 | [链接](https://github.com/tek256/astera) |
| bgfx | 开源 | 跨平台、图形 API 无关的渲染库 | [链接](https://github.com/bkaradzic/bgfx) |
| Box2D | 开源 | 2D 物理引擎 | [链接](http://box2d.org/) |
| Bullet | 开源 | 实时物理模拟引擎 | [链接](http://bulletphysics.org/wordpress/) |
| Chipmunk2D | 开源 | 轻量级 2D 物理库 | [链接](https://chipmunk-physics.net/) |
| Cinder | 开源 | 专业创意编码 C++ 库 | [链接](https://libcinder.org/) |
| Cocos2d-x | 开源 | C++ OpenGL 2D/3D 引擎，支持 JS 和 Lua | [链接](http://cocos2d-x.org/) |
| Diligent Engine | 开源 | 跨平台底层图形库（DX11/DX12/OpenGL/Vulkan） | [链接](https://github.com/DiligentGraphics/DiligentEngine) |
| EnTT | 开源 | 现代 C++ ECS 框架 | [链接](https://github.com/skypjack/entt) |
| Flax Engine | 开源/部分免费 | 多平台 3D 游戏引擎 | [链接](https://flaxengine.com/) |
| gameplay | 开源 | 跨平台 2D+3D C++ 游戏框架 | [链接](http://gameplay3d.io/) |
| Horde3D | 开源 | 小型开源 3D 渲染引擎 | [链接](http://www.horde3d.org/) |
| Irrlicht | 开源 | 高性能实时 3D 引擎 | [链接](http://irrlicht.sourceforge.net/) |
| LumixEngine | 开源 | C++ 3D 游戏引擎 | [链接](https://github.com/nem0/LumixEngine) |
| Magnum | 开源 | 轻量模块化 2D/3D 图形引擎 | [链接](http://magnum.graphics/) |
| nCine | 开源 | 高性能跨平台 2D 引擎，支持 Lua 脚本 | [链接](https://ncine.github.io/) |
| Ogre3D | 开源 | 场景导向的实时 3D 渲染引擎 | [链接](http://www.ogre3d.org/) |
| openFrameworks | 开源 | 创意编码 C++ 工具包 | [链接](https://openframeworks.cc/) |
| ORX | 开源 | 数据驱动的 2.5D C/C++ 引擎 | [链接](https://orx-project.org/) |
| Panda3D | 开源 | Python/C++ 3D 渲染与游戏开发框架 | [链接](https://www.panda3d.org/) |
| raylib | 开源 | 简洁易用的游戏编程库，支持 OpenGL | [链接](https://www.raylib.com/) |
| SDL | 开源 | 跨平台底层多媒体访问库 | [链接](http://libsdl.org/) |
| SFML | 开源 | 简洁快速的多媒体库 | [链接](http://www.sfml-dev.org/) |
| Solarus | 开源 | 跨平台 2D 动作/冒险引擎，Lua API | [链接](https://www.solarus-games.org/) |
| Spring | 开源 | 强大的跨平台 RTS 引擎 | [链接](http://springrts.com/) |
| Urho3D | 开源 | 跨平台渲染与游戏引擎 | [链接](http://urho3d.github.io/) |

#### C#/.NET

| 引擎 | 类型 | 说明 | 链接 |
|------|------|------|------|
| MonoGame | 开源 | Microsoft XNA 4 的开源实现 | [链接](http://www.monogame.net/) |
| Stride | 开源 | 开源 C# 游戏引擎 | [链接](https://stride3d.net/) |
| Unity 3D | 部分免费 | 主流 2D/3D 游戏开发引擎 | [链接](http://unity3d.com/) |
| Wave | 开源 | 跨平台 C# 引擎 | [链接](http://waveengine.net/) |
| Foster | 开源 | 小型跨平台 2D C# 游戏框架 | [链接](https://github.com/FosterFramework/Foster) |

#### Java/Kotlin

| 引擎 | 类型 | 说明 | 链接 |
|------|------|------|------|
| FXGL | 开源 | JavaFX/Kotlin 游戏引擎 | [链接](https://github.com/AlmasB/FXGL) |
| jMonkeyEngine 3 | 开源 | 3D Java 开源游戏引擎 | [链接](http://jmonkeyengine.org/) |
| LibGDX | 开源 | 强大的 Java 跨平台游戏库 | [链接](https://libgdx.com/) |
| LITIengine | 开源 | 基于 Java 的 2D 瓦片游戏引擎 | [链接](http://litiengine.com/) |
| KogGE | 开源 | Kotlin 多平台游戏引擎 | [链接](https://korge.soywiz.com) |

#### JavaScript/TypeScript

| 引擎 | 类型 | 说明 | 链接 |
|------|------|------|------|
| Babylon.js | 开源 | JavaScript 3D 库 | [链接](https://www.babylonjs.com/) |
| boardgame.io | 开源 | 回合制游戏的状态管理与多人联网 | [链接](https://github.com/boardgameio/boardgame.io) |
| ct.js | 开源 | 可视化 2D 游戏引擎 | [链接](https://ctjs.rocks/) |
| ImpactJS | 开源 | HTML5 JavaScript 游戏引擎 | [链接](http://impactjs.com/) |
| Matter.js | 开源 | Web 端 2D 物理引擎 | [链接](http://brm.io/matter-js/) |
| MelonJS | 开源 | 轻量级 HTML5 游戏引擎 | [链接](http://melonjs.org) |
| Phaser | 开源 | 快速 2D HTML5 游戏框架 | [链接](http://phaser.io/) |
| PixiJS | 开源 | WebGL 优先的 HTML5 游戏渲染器 | [链接](http://www.pixijs.com/) |
| Three.js | 开源 | JavaScript 3D 库 | [链接](http://threejs.org/) |
| PlayCanvas | 部分免费 | WebGL 游戏引擎 | [链接](https://playcanvas.com/) |

#### Python

| 引擎 | 类型 | 说明 | 链接 |
|------|------|------|------|
| Kivy | 开源 | 跨平台 Python 应用与游戏框架 | [链接](http://kivy.org) |
| PyGame-CE | 开源 | Python 多媒体库（SDL 封装） | [链接](https://pyga.me/docs/index.html) |
| Pyxel | 开源 | Python 复古游戏引擎 | [链接](https://github.com/kitao/pyxel) |
| ursina | 开源 | 基于 Panda3D 的 Python 游戏引擎 | [链接](https://www.ursinaengine.org/) |

#### Rust

| 引擎 | 类型 | 说明 | 链接 |
|------|------|------|------|
| Bevy | 开源 | 数据驱动的 Rust 游戏引擎 | [链接](https://bevyengine.org/) |
| ggez | 开源 | Rust 轻量游戏库 | [链接](http://ggez.rs/) |
| macroquad | 开源 | 跨平台 Rust 游戏引擎 | [链接](https://github.com/not-fl3/macroquad) |
| Piston | 开源 | 模块化 Rust 游戏引擎 | [链接](http://www.piston.rs/) |

#### Go

| 引擎 | 类型 | 说明 | 链接 |
|------|------|------|------|
| Ebiten | 开源 | 极简 Go 2D 游戏库 | [链接](https://ebiten.org/) |
| ENGi | 开源 | 多平台 Go 2D 游戏库 | [链接](https://github.com/ajhager/engi) |
| engo | 开源 | Go 2D 游戏引擎 | [链接](https://engoengine.github.io/) |

#### Lua

| 引擎 | 类型 | 说明 | 链接 |
|------|------|------|------|
| Defold | 开源 | 免费跨平台 2D 引擎 | [链接](http://www.defold.com/) |
| LÖVE | 开源 | Lua 2D 游戏引擎 | [链接](http://love2d.org) |
| Solar2D | 开源 | Lua 游戏引擎，注重迭代效率 | [链接](https://solar2d.com/) |

#### 可视化/无代码

| 引擎 | 类型 | 说明 | 链接 |
|------|------|------|------|
| Construct | 付费 | HTML5 可视化游戏制作工具 | [链接](https://www.scirra.com/) |
| GDevelop | 开源 | 跨平台 2D 引擎，无需编程基础 | [链接](https://gdevelop-app.com/) |
| GameMaker | 部分免费 | 支持拖拽和脚本的跨平台游戏引擎 | [链接](https://gamemaker.io/) |
| GB Studio | 开源 | 复古掌机游戏创建工具 | [链接](https://www.gbstudio.dev/) |
| Ren'Py | 开源 | 视觉小说引擎，基于简化 Python | [链接](http://www.renpy.org/) |
| Twine | 开源 | 互动叙事游戏开发平台 | [链接](http://twinery.org/) |

#### 3A/商业级引擎

| 引擎 | 类型 | 说明 | 链接 |
|------|------|------|------|
| Unreal Engine | 部分免费 | Epic Games 开发的 3A 级游戏引擎 | [链接](https://www.unrealengine.com/) |
| Lumberyard (O3DE) | 免费 | Amazon 3A 级游戏引擎 | [链接](https://aws.amazon.com/lumberyard/) |

### 2.2 游戏 AI

| 资源 | 类型 | 说明 | 链接 |
|------|------|------|------|
| AI Game Developer | 开源 | Unity 编辑器与运行时 AI 集成 | [链接](https://github.com/IvanMurzak/Unity-MCP) |
| Coplay | 部分免费 | Unity AI 副驾驶 | [链接](https://coplay.dev) |
| Fluent Behaviour Tree | 开源 | C# 行为树库 | [链接](https://github.com/codecapers/Fluent-Behaviour-Tree) |
| SimpleAI | 开源 | C++11 行为树库，含 Qt5 调试器 | [链接](https://github.com/mgerhardy/simpleai/) |

---

## 三、音频

### 3.1 音效素材库

| 资源 | 类型 | 说明 | 链接 |
|------|------|------|------|
| Free Game Sounds | 免费 | 免版税游戏音效存档 | [链接](https://gamesounds.xyz/) |
| Freesound | 免费 | Creative Commons 协作音效数据库 | [链接](http://www.freesound.org/) |
| Musopen | 免费 | 免版税音乐 | [链接](https://musopen.org/) |
| Octave | 免费 | 免费 UI 音效库 | [链接](http://raisedbeaches.com/octave/index.html) |
| PacDV | 免费 | 免版税音效集合 | [链接](http://www.pacdv.com/sounds/index.html) |
| SoundBible.com | 免费 | 可搜索的免版税音效存档 | [链接](http://soundbible.com/) |

### 3.2 音乐与音效编辑器

| 资源 | 类型 | 说明 | 链接 |
|------|------|------|------|
| Audacity | 开源 | 跨平台录音与音频编辑软件 | [链接](http://sourceforge.net/projects/audacity/) |
| Audiosauna | 免费 | 浏览器端音乐制作工作室 | [链接](http://www.audiosauna.com/) |
| Audiotool | 免费 | 在线音乐制作工具 | [链接](http://www.audiotool.com/app) |
| Bfxr | 免费 | 游戏音效制作工具 | [链接](https://www.bfxr.net/) |
| Bosca Ceoil | 免费 | 简洁直观的在线音乐制作工具 | [链接](http://boscaceoil.net/) |
| ChipTone | 免费 | 在线音效生成器 | [链接](http://sfbgames.com/chiptone/) |
| FamiStudio | 免费 | NES 音乐编辑器 | [链接](https://github.com/BleuBleu/FamiStudio) |
| FamiTracker | 免费 | NES/Famicom 音乐追踪器 | [链接](https://github.com/Dn-Programming-Core-Management/Dn-FamiTracker) |
| jfxr | 开源 | Bfxr 的 JavaScript 移植版 | [链接](http://jfxr.frozenfractal.com) |
| LMMS | 开源 | 跨平台音乐制作软件 | [链接](https://lmms.io/) |
| MilkyTracker | 开源 | 跨平台开源音乐追踪器 | [链接](https://github.com/milkytracker/MilkyTracker) |
| musagi | 开源 | 功能丰富的音乐编辑器与合成器 | [链接](http://www.drpetter.se/project_musagi.html) |
| Resemble | 付费 | Unity 内语音克隆引擎 | [链接](https://www.resemble.ai/unity) |
| Soundation | 免费 | 在线专业音乐工作室 | [链接](https://soundation.com/) |
| SunVox | 免费 | 小巧强大的模块化合成器与追踪器 | [链接](http://www.warmplace.ru/soft/sunvox/) |

---

## 四、桌面游戏

| 资源 | 类型 | 说明 | 链接 |
|------|------|------|------|
| Iterary | 免费 | 桌游设计工具 | [链接](http://www.iterary.com) |
| RPTools | 开源 | 增强传统纸笔角色扮演的开源工具集 | [链接](http://www.rptools.net/) |

---

## 五、学习与社区

### 5.1 博客与门户网站

| 网站 | 说明 | 链接 |
|------|------|------|
| Amit's Game Programming | 游戏编程资源 | [链接](http://www-cs-students.stanford.edu/~amitp/gameprog.html) |
| Designer Notes | 游戏设计笔记 | [链接](http://www.designer-notes.com/) |
| Emanuele Feronato's Blog | 游戏开发博客 | [链接](http://www.emanueleferonato.com/) |
| GameIdea | 游戏创意 | [链接](https://gameidea.org) |
| Gamasutra | 游戏开发行业媒体 | [链接](http://www.gamasutra.com/) |
| Game Development StackExchange | 游戏开发问答社区 | [链接](http://gamedev.stackexchange.com/) |
| GameDevs.org | 游戏开发者社区 | [链接](http://gamedevs.org/) |
| GameJolt | 独立游戏平台 | [链接](http://gamejolt.com/) |
| HTML5 Game Devs Forum | HTML5 游戏开发论坛 | [链接](http://www.html5gamedevs.com/) |
| HobbyGameDev | 业余游戏开发 | [链接](http://www.hobbygamedev.com/) |
| IndieDB | 独立游戏数据库 | [链接](http://www.indiedb.com/) |
| Lost Garden | 游戏设计文章 | [链接](http://www.lostgarden.com/) |
| Polygon | 游戏新闻媒体 | [链接](http://www.polygon.com/) |
| Real-Time Rendering | 实时渲染技术资源 | [链接](http://www.realtimerendering.com/) |
| TIGSource | 独立游戏源 | [链接](http://www.tigsource.com/) |

### 5.2 推荐书籍

| 书名 | 领域 |
|------|------|
| 2D Game Development: From Zero To Hero（免费） | 2D 游戏入门 |
| 3D Math Primer for Graphics and Game Development | 3D 数学 |
| Artificial Intelligence for Games | 游戏 AI |
| Designing Games: A Guide to Engineering Experiences | 游戏设计 |
| Essential Mathematics for Games and Interactive Applications | 游戏数学 |
| Game Coding Complete | 游戏编程 |
| Game Engine Architecture | 引擎架构 |
| Game Programming Patterns | 编程模式 |
| Geometry for Programmers | 几何编程 |
| Learn OpenGL | OpenGL 入门 |
| Mathematics For 3D Game Programming And Computer Graphics | 3D 数学 |
| Nature of Code | 代码与自然模拟 |
| Physics for Game Developers | 游戏物理 |
| Real-Time Rendering | 实时渲染 |
| The Art of Game Design | 游戏设计艺术 |
| Theory of Fun | 游戏乐趣理论 |
| Unity in Action | Unity 实战 |

### 5.3 杂志

| 资源 | 类型 | 链接 |
|------|------|------|
| Game Developer Magazine | 免费 | [链接](http://www.gdcvault.com/gdmag) |
| IndieMag | 免费 | [链接](https://www.indiemag.fr/) |

### 5.4 视频/播客

| 资源 | 说明 | 链接 |
|------|------|------|
| awesome-gametalks | GDC 等游戏演讲精选 | [链接](https://github.com/hzoo/awesome-gametalks) |
| Twitch GameDev | Twitch 游戏开发直播 | [链接](http://www.twitch.tv/directory/game/Game%20Development) |

### 5.5 Game Jam

| 活动 | 说明 | 链接 |
|------|------|------|
| itch.io Game Jams | itch.io 游戏 Jam 列表 | [链接](https://itch.io/jams) |
| Game Off | GitHub 官方游戏 Jam | [链接](https://gameoff.github.com) |
| GMTK Game Jam | 年度热门游戏 Jam | [链接](https://itch.io/jam/gmtk-jam-2022) |
| Indie Game Jams | 独立游戏 Jam 列表 | [链接](http://www.indiegamejams.com/) |
| Ludum Dare | 极受欢迎的游戏 Jam | [链接](http://ludumdare.com/) |
| One Hour Game Jam | 每周 1 小时游戏 Jam | [链接](http://onehourgamejam.com/) |

### 5.6 项目管理

| 工具 | 类型 | 说明 | 链接 |
|------|------|------|------|
| Casual | 付费 | 可视化项目管理 | [链接](https://casual.pm/) |
| Codecks | 部分免费 | 卡牌式游戏开发项目管理 | [链接](https://www.codecks.io) |
| HacknPlan | 部分免费 | 游戏开发者专用项目管理 | [链接](http://hacknplan.com/) |
| Questlog | 部分免费 | 内置 GDD 编辑器的游戏项目管理 | [链接](https://www.questlog.build) |
| Taiga | 部分免费 | 敏捷开发项目管理平台 | [链接](https://taiga.io/) |
| Trello | 部分免费 | 通用看板式项目管理 | [链接](https://trello.com/) |

### 5.7 完整游戏源码（学习参考）

| 项目 | 说明 | 链接 |
|------|------|------|
| Barotrauma | 开源潜艇模拟游戏 | [链接](https://github.com/Regalis11/Barotrauma) |
| Canabalt iOS | 经典跑酷游戏 iOS 版 | [链接](https://github.com/ericjohnson/canabalt-ios) |
| Doom | id Software 经典 FPS | [链接](https://github.com/id-Software/DOOM) |
| Doom 3 | id Software 3D FPS | [链接](https://github.com/id-Software/DOOM-3) |
| NetHack | 经典 Roguelike | [链接](https://github.com/NetHack/NetHack) |
| OpenRA | 开源 RTS 引擎 | [链接](https://github.com/OpenRA/OpenRA) |
| OpenTTD | 开源运输模拟 | [链接](https://github.com/OpenTTD/OpenTTD) |
| Prince of Persia | 波斯王子 Apple II 版源码 | [链接](https://github.com/jmechner/Prince-of-Persia-Apple-II) |
| Quake | id Software 经典 FPS | [链接](https://github.com/id-Software/Quake) |
| Quake 2 | Quake 续作 | [链接](https://github.com/id-Software/Quake-2) |
| Quake III Arena | 竞技场 FPS | [链接](https://github.com/id-Software/Quake-III-Arena) |
| SimCity | 模拟城市开源版 | [链接](https://github.com/simhacker/micropolis) |
| VVVVVV | 独立平台跳跃游戏 | [链接](https://github.com/TerryCavanagh/VVVVVV) |
| Wolfenstein 3D | id Software 经典 FPS | [链接](https://github.com/id-Software/wolf3d) |

### 5.8 开发者社区

| 社区 | 链接 |
|------|------|
| Reddit r/gamedev | [链接](https://www.reddit.com/r/gamedev/) |
| Reddit r/IndieGaming | [链接](https://www.reddit.com/r/IndieGaming/) |
| Game Dev League (Discord) | [链接](https://discord.com/invite/gamedev) |
| Brackeys Discord | [链接](https://discord.gg/brackeys) |
| Brackeys Forum | [链接](https://forum.brackeys.com/) |
| GameDev.tv | [链接](https://community.gamedev.tv/) |

---

## 六、广告与变现

| 平台 | 说明 | 链接 |
|------|------|------|
| AdMob by Google | Google 移动广告与变现服务 | [链接](https://www.google.com/admob/) |
| AdColony | 移动视频广告服务 | [链接](http://www.adcolony.com/) |
| Appodeal | 移动应用程序化广告中介 | [链接](http://www.appodeal.com/) |
| ChartBoost | 变现与分析平台 | [链接](https://www.chartboost.com/) |
| Unity Ads | Unity3D 官方广告 SDK | [链接](https://unity.com/products/unity-ads) |
| Vungle | 视频广告服务 | [链接](https://vungle.com/) |

---

## 七、学习资源

### 7.1 通用游戏开发

| 资源 | 类型 | 说明 | 链接 |
|------|------|------|------|
| Chris Courses | 部分免费 | 2D 游戏完整课程 | [链接](https://chriscourses.com/) |
| HandmadeHero | 免费 | 从零制作 2D 游戏的实战教程 | [链接](https://handmadehero.org/) |
| Khan Academy | 免费 | 高级 JS 游戏与可视化 | [链接](https://www.khanacademy.org/computing/cs/programming-games-visualizations) |
| Simple HTML5 Canvas Game | 免费 | HTML5 Canvas 游戏入门 | [链接](http://www.lostdecadegames.com/how-to-make-a-simple-html5-canvas-game/) |
| miloyip/game-programmer | 免费 | 游戏程序员学习路径 | [链接](https://github.com/miloyip/game-programmer) |
| TheChernoProject | 免费 | 游戏引擎开发 YouTube 频道 | [链接](https://www.youtube.com/user/TheChernoProject) |
| Udacity: HTML5 Game Dev | 免费 | HTML5 游戏开发课程 | [链接](https://www.udacity.com/course/html5-game-development--cs255) |

### 7.2 计算机图形学

| 资源 | 类型 | 说明 | 链接 |
|------|------|------|------|
| 3D Game Shaders For Beginners | 免费 | 3D 游戏着色器入门 | [链接](https://github.com/lettier/3d-game-shaders-for-beginners) |
| Interactive 3D Graphics | 免费 | 交互式 3D 图形课程 | [链接](https://www.udacity.com/course/interactive-3d-graphics--cs291) |
| Interactive Computer Graphics | 付费 | 交互式计算机图形学 | [链接](https://www.coursera.org/learn/interactive-computer-graphics) |

---

## 关键要点

1. **引擎选型**：根据项目规模和目标平台选择引擎。小型/独立项目推荐 Godot、GDevelop、Phaser；中型项目推荐 Unity、Defold；3A 级项目推荐 Unreal Engine。
2. **素材获取**：Kenney Assets、OpenGameArt、Poly Pizza 是免费素材的优质来源，适合原型开发和独立项目。
3. **音效制作**：Bfxr 和 ChipTone 可快速生成游戏音效；Audacity 用于后期处理；Freesound 提供大量免费音效。
4. **学习路径**：从 HandmadeHero 或简单 HTML5 Canvas 游戏入手，逐步学习引擎架构（Game Engine Architecture）和图形学（Learn OpenGL）。
5. **物理引擎**：Box2D（2D）和 Bullet（3D）是最成熟的开源物理引擎选择。
6. **项目管理**：HacknPlan 和 Codecks 是游戏开发专用的项目管理工具，比通用工具更贴合游戏开发流程。
7. **社区参与**：加入 Reddit r/gamedev 和相关 Discord 社区，参与 Game Jam 是提升技能和结识同行的有效途径。


---
