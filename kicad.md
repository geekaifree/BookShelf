# KiCad：开源 PCB 设计套件

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
