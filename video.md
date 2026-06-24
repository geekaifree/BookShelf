# 使用 Kdenlive 进行视频编辑

使用 Kdenlive 开源非线性视频编辑器的实用指南。

## 目录

- [安装](#安装)
- [界面概览](#界面概览)
- [项目设置](#项目设置)
- [时间线编辑](#时间线编辑)
- [转场](#转场)
- [效果](#效果)
- [颜色校正](#颜色校正)
- [音频编辑](#音频编辑)
- [关键帧](#关键帧)
- [字幕](#字幕)
- [代理编辑](#代理编辑)
- [渲染和导出](#渲染和导出)
- [键盘快捷键](#键盘快捷键)

---

## 安装

### Linux

| 发行版 | 命令 |
|--------|------|
| Ubuntu/Debian | `sudo apt install kdenlive` |
| Fedora | `sudo dnf install kdenlive` |
| Arch Linux | `sudo pacman -S kdenlive` |
| Flatpak（通用） | `flatpak install org.kde.kdenlive` |
| Snap | `sudo snap install kdenlive` |

### macOS

通过 Homebrew 安装：

```bash
brew install --cask kdenlive
```

或从 Kdenlive 官方网站下载 `.dmg` 文件。

### Windows

1. 从 https://kdenlive.org/download/ 下载安装程序。
2. 运行 `.exe` 安装程序。
3. 按照安装向导操作。
4. Kdenlive 将自动安装所需组件（FFmpeg、MLT）。

### 验证安装

启动 Kdenlive 后，检查 `Help > About Kdenlive` 确认版本。确保在 `Settings > Configure Kdenlive > Environment` 中检测到 FFmpeg。

---

## 界面概览

Kdenlive 界面由可配置的面板组成。

### 主要面板

| 面板 | 位置 | 用途 |
|------|------|------|
| Project Bin | 左上 | 导入和组织媒体素材 |
| Clip Monitor | 中上 | 预览源片段 |
| Project Monitor | 中上 | 预览编辑后的时间线 |
| Timeline | 底部 | 在轨道上排列片段 |
| Effects/Properties | 右侧栏 | 应用和配置效果 |
| Audio Mixer | 右下 | 控制每轨道音频电平 |

### 工作空间布局

Kdenlive 提供多种预设工作空间：

| 工作空间 | 最适合 |
|----------|--------|
| Default | 通用编辑 |
| Audio | 音频为主编辑 |
| Effects | 应用和调整效果 |
| Logging | 导入和组织素材 |
| Editing | 完整编辑工作流 |

通过 `View > Workspace` 切换工作空间。

### 自定义界面

- **重新排列面板** - 拖动面板标签。
- **取消停靠面板** - 拖动到主窗口外。
- **保存布局** - 通过 `View > Save Current Layout`。
- **重置布局** - 通过 `View > Workspace > Default`。

---

## 项目设置

### 创建新项目

1. 前往 `Project > New`。
2. 输入项目名称。
3. 选择项目文件夹。
4. 选择项目配置文件（分辨率和帧率）。

### 项目配置文件

| 配置文件 | 分辨率 | 帧率 | 使用场景 |
|----------|--------|------|----------|
| HD 1080p | 1920x1080 | 30fps | 标准网络视频 |
| HD 1080p | 1920x1080 | 24fps | 电影感 |
| 4K UHD | 3840x2160 | 30fps | 高分辨率项目 |
| 720p | 1280x720 | 30fps | 轻量项目 |
| Vertical 9:16 | 1080x1920 | 30fps | 移动/社交媒体 |

### 自动配置文件检测

导入第一个片段时，Kdenlive 可以自动匹配项目配置文件与片段属性。在 `Settings > Configure Kdenlive > Project Defaults` 中启用。

### 项目设置

| 设置 | 位置 | 描述 |
|------|------|------|
| Default duration | Project > Project Settings | 图片段的持续时间 |
| Audio channels | Project > Project Settings | 立体声或单声道 |
| Timeline frames | Project > Project Settings | 每秒帧数 |
| Proxy settings | Project > Project Settings | 启用代理片段 |

---

## 时间线编辑

时间线是您排列和编辑视频项目的地方。

### 将片段添加到时间线

| 方法 | 操作 |
|------|------|
| Drag and drop | 从 Project Bin 拖到时间线 |
| Insert | 选择片段，按 `V` 在播放头插入 |
| Overwrite | 选择片段，按 `B` 在播放头覆盖 |
| Three-point edit | 在片段和时间线上设置入/出点，然后插入 |

### 时间线轨道

| 轨道类型 | 用途 |
|----------|------|
| Video track | 持有视频片段、图片、字幕 |
| Audio track | 持有音频片段、旁白 |
| Transition track | 持有片段间的转场 |

- **添加轨道** - 右键点击轨道头 > Insert Track。
- **删除轨道** - 右键点击轨道头 > Delete Track。
- **重排轨道** - 拖动轨道头。
- **锁定轨道** - 点击轨道头的锁定图标。

### 基本编辑操作

| 操作 | 快捷键 | 描述 |
|------|--------|------|
| Cut/razor | `Shift + R` | 在播放头分割片段 |
| Select | `Shift + S` | 选择模式 |
| Spacer | `Shift + M` | 移动某点之后的所有片段 |
| Delete | `Delete` | 删除选定片段 |
| Ripple delete | `Shift + Delete` | 删除片段并关闭间隙 |
| Copy | `Ctrl + C` | 复制选定片段 |
| Paste | `Ctrl + V` | 在播放头粘贴 |
| Undo | `Ctrl + Z` | 撤销上一操作 |
| Redo | `Ctrl + Shift + Z` | 重做上一撤销操作 |

### 修剪片段

| 修剪类型 | 操作 | 结果 |
|----------|------|------|
| Ripple trim | 拖动片段边缘 | 调整片段，移动后续片段 |
| Roll trim | 拖动两个片段间的编辑点 | 同时调整两个片段 |
| Slip | 拖动片段中间 | 更改入/出点，保持位置 |
| Slide | 用 Ctrl 拖动片段 | 移动片段不影响其他 |

### 时间线导航

| 操作 | 快捷键 |
|------|--------|
| Play/Pause | `Space` |
| Go to start | `Home` |
| Go to end | `End` |
| Step forward one frame | `Right` |
| Step backward one frame | `Left` |
| Step forward 1 second | `Shift + Right` |
| Zoom in timeline | `Ctrl +` |
| Zoom out timeline | `Ctrl -` |

---

## 转场

转场在片段之间创建平滑的视觉变化。

### 添加转场

1. 将两个片段放在同一轨道上使其重叠，或放在相邻轨道上。
2. 右键点击重叠区域。
3. 选择 `Insert Transition`。
4. 选择转场类型。

### 转场类型

| 转场 | 视觉效果 | 持续时间 |
|------|----------|----------|
| Dissolve | 片段间渐变 | 0.5 - 2 秒 |
| Wipe Left | 新片段从右侧滑入 | 可配置 |
| Wipe Right | 新片段从左侧滑入 | 可配置 |
| Wipe Up | 新片段从底部滑入 | 可配置 |
| Dissolve to Black | 淡出后淡入 | 0.5 - 1 秒 |

### 转场属性

| 属性 | 描述 |
|------|------|
| Duration | 转场长度 |
| Direction | 正向或反向 |
| Alignment | 重叠的起始、中心或结束 |

### 自动转场

在 `Settings > Configure Kdenlive > Timeline` 中启用自动转场。启用后，重叠的片段自动获得溶解转场。

---

## 效果

效果修改片段的外观或属性。

### 应用效果

1. 在时间线上选择片段。
2. 打开 Effects 面板（右侧栏）。
3. 浏览或搜索效果。
4. 双击或将效果拖到片段上。
5. 在效果属性中调整参数。

### 视频效果分类

| 分类 | 示例 |
|------|------|
| Transform | Position, Scale, Crop, Rotate |
| Color | Brightness, Contrast, Saturation, White Balance |
| Blur | Gaussian Blur, Box Blur, Average Blur |
| Distort | Fish Eye, Mirror, Wave |
| Keying | Chroma Key（绿幕）, Luma Key |
| Stylize | Cartoon, Charcoal, Glow |

### 音频效果分类

| 分类 | 示例 |
|------|------|
| Volume | Gain, Normalize, Compressor |
| EQ | Equalizer, Band Pass |
| Dynamics | Noise Gate, Limiter, Expander |
| Delay | Echo, Reverb |
| Filters | Noise Reduction, High Pass, Low Pass |

### 效果堆栈

多个效果可以应用到单个片段。它们按从上到下的顺序处理。

| 操作 | 方法 |
|------|------|
| Reorder effects | 在堆栈中拖动效果 |
| Disable effect | 切换眼睛图标 |
| Remove effect | 选择并点击减号按钮 |
| Copy effects | 右键 > Copy Effects |
| Paste effects | 右键另一片段 > Paste Effects |

---

## 颜色校正

Kdenlive 提供调整和校正素材颜色的工具。

### 颜色校正工作流

1. **白平衡** - 使用 White Balance 效果校正色温。
2. **曝光** - 调整亮度和对比度。
3. **饱和度** - 增加或减少颜色强度。
4. **曲线** - 按通道微调色调范围。
5. **示波器** - 使用视频示波器验证校正。

### 视频示波器

| 示波器 | 用途 |
|--------|------|
| RGB Parade | 并排显示红、绿、蓝电平 |
| Waveform | 显示帧内亮度电平 |
| Vectorscope | 显示色相和饱和度 |
| Histogram | 色调值分布 |

通过 `View > Video Scopes` 访问示波器。

### 颜色效果

| 效果 | 控制 | 使用场景 |
|------|------|----------|
| White Balance | Temperature, Tint | 校正灯光颜色 |
| Brightness/Contrast | Brightness, Contrast | 曝光校正 |
| Hue/Saturation | Hue shift, Saturation, Lightness | 颜色强度 |
| Curves | RGB channel curves | 精确色调控制 |
| Color Balance | Shadows, Midtones, Highlights | Lift/Gamma/Gain |
| Levels | Input/Output black/white points | 动态范围调整 |

### LUT 支持

Kdenlive 支持查找表（LUT）用于应用颜色分级。

1. 将 `LUT (3D)` 效果添加到片段。
2. 浏览并选择 `.cube` LUT 文件。
3. 调整强度参数。

常见 LUT 来源包括电影风格、log 到 Rec709 转换和创意分级。

---

## 音频编辑

### 音频轨道管理

| 操作 | 方法 |
|------|------|
| Add audio track | 右键轨道头 > Insert Audio Track |
| Mute track | 点击轨道头的扬声器图标 |
| Solo track | Ctrl+点击扬声器图标 |
| Lock track | 点击锁定图标 |
| Adjust track height | 拖动轨道头边缘 |

### 音频混音器

Audio Mixer 面板提供每轨道的音量和声像控制。

| 控制 | 描述 |
|------|------|
| Volume slider | 以 dB 调整轨道响度 |
| Pan knob | 左右立体声位置 |
| Mute button | 静音轨道 |
| Solo button | 仅听此轨道 |
| Master meter | 总体输出电平 |

### 音频效果

| 效果 | 用途 | 关键参数 |
|------|------|----------|
| Gain | 调整音量 | dB 值 |
| Compressor | 减少动态范围 | Threshold, Ratio, Attack |
| Equalizer | 塑形频率响应 | 频段 |
| Noise Reduction | 去除背景噪音 | Profile, Reduction amount |
| Normalize | 将峰值电平设为目标 dB | Target level |
| Reverb | 添加空间氛围 | Room size, Dampening |

### 音频同步

| 方法 | 操作 |
|------|------|
| Manual sync | 可视对齐波形峰值 |
| Audio alignment | Tools > Align Audio |
| Sync marker | 在两个片段上放置标记，然后对齐 |

### 录制旁白

1. 前往 `Project > Add Clip > Record Audio`。
2. 选择输入设备和设置。
3. 按录制并解说。
4. 停止录制以将片段添加到项目库和时间线。

---

## 关键帧

关键帧允许您随时间动画化属性。

### 添加关键帧

1. 选择应用了效果的片段。
2. 打开效果属性。
3. 点击参数旁的关键帧按钮（菱形图标）。
4. 将播放头移到不同位置。
5. 更改参数值。新关键帧自动创建。

### 关键帧插值

| 类型 | 行为 | 使用场景 |
|------|------|----------|
| Linear | 恒定变化速率 | 均匀运动 |
| Smooth | 缓入/缓出 | 自然运动 |
| Discrete | 瞬间变化 | 阶梯过渡 |

### 常见关键帧动画

| 动画 | 参数 | 示例 |
|------|------|------|
| Fade in/out | Opacity | 1 秒内 0% 到 100% |
| Zoom | Scale | 2 秒内 100% 到 150% |
| Pan | X/Y Position | 帧内移动 |
| Rotate | Rotation angle | 旋转效果 |
| Color shift | Hue/Saturation | 随时间的颜色动画 |

### 关键帧编辑器

| 操作 | 快捷键/方法 |
|------|-------------|
| Add keyframe | 点击菱形图标或 `Ctrl + 点击` 曲线 |
| Delete keyframe | 选择后按 `Delete` |
| Move keyframe | 水平拖动（时间）或垂直拖动（值） |
| Copy keyframe | 选择关键帧后 `Ctrl + C` |
| Adjust curve | 拖动贝塞尔控制柄 |

---

## 字幕

Kdenlive 包含内置字幕编辑器，用于创建文本叠加和图形。

### 创建字幕片段

1. 前往 `Project > Add Title Clip`。
2. 字幕编辑器打开，显示画布。
3. 添加文本、形状或图片。
4. 配置属性（字体、颜色、位置）。
5. 点击 `OK` 将字幕添加到 Project Bin。

### 字幕编辑器工具

| 工具 | 用途 |
|------|------|
| Text | 添加文本，可自定义字体、大小、颜色 |
| Rectangle | 绘制矩形形状 |
| Ellipse | 绘制圆形/椭圆形状 |
| Image | 插入图片文件 |

### 文本属性

| 属性 | 选项 |
|------|------|
| Font | 任何已安装的系统字体 |
| Size | 以像素可调 |
| Color | 完整拾色器带透明度 |
| Alignment | 左、中、右 |
| Shadow | 带偏移和模糊的投影 |
| Outline | 带颜色和宽度的文本边框 |

### 字幕动画

| 动画 | 描述 |
|------|------|
| Scroll | 垂直滚动文本（演职员表） |
| Fade In | 字幕逐渐出现 |
| Fade Out | 字幕逐渐消失 |

### 下三分之一

用于标识发言者的常见字幕样式：

1. 创建字幕片段。
2. 在底部添加半透明矩形。
3. 在矩形上方添加姓名文本。
4. 在姓名下方以较小字体添加头衔/角色文本。
5. 保存并作为模板重用。

---

## 代理编辑

代理编辑创建片段的低分辨率副本以获得更流畅的编辑体验，而渲染使用原始全分辨率文件。

### 启用代理片段

1. 前往 `Project > Project Settings`。
2. 勾选 `Enable Proxy Clips`。
3. 选择代理配置文件（如 MPEG-2 720p）。

### 代理配置文件

| 配置文件 | 分辨率 | 编解码器 | 速度 |
|----------|--------|----------|------|
| MPEG-2 720p | 1280x720 | MPEG-2 | 快 |
| H.264 720p | 1280x720 | H.264 | 中 |
| MJPEG 540p | 960x540 | MJPEG | 非常快 |

### 代理工作流

| 步骤 | 操作 |
|------|------|
| 1 | 导入高分辨率片段（4K, RAW） |
| 2 | Kdenlive 自动生成代理片段 |
| 3 | 使用代理片段编辑（流畅播放） |
| 4 | 渲染使用原始片段（完全质量） |

### 管理代理

| 操作 | 方法 |
|------|------|
| Generate proxies | 右键片段 > Proxy Clip > Create |
| Delete proxies | 右键片段 > Proxy Clip > Remove |
| Toggle proxy/original | Project > Proxy Clip（切换） |

---

## 渲染和导出

### 打开渲染对话框

前往 `Project > Render` 或按 `Ctrl + Enter`。

### 渲染预设

| 预设 | 格式 | 质量 | 使用场景 |
|------|------|------|----------|
| MP4-H264/AAC | MP4 | 高 | 通用、Web 上传 |
| WebM-VP8/Vorbis | WebM | 中 | Web 嵌入 |
| MPEG-2 | MPEG | 高 | DVD 制作 |
| H.265/HEVC | MP4 | 非常高 | 高质量、更小文件 |
| Lossless FFV1 | AVI | 无损 | 归档、中间格式 |
| Audio only | WAV/MP3 | 不同 | 播客、音乐 |

### 自定义渲染设置

| 设置 | 描述 | 建议 |
|------|------|------|
| Resolution | 输出尺寸 | 匹配项目或缩小 |
| Frame rate | 每秒帧数 | 匹配项目配置文件 |
| Bitrate | 视频数据速率 | 1080p 用 8-15 Mbps |
| Codec | 视频压缩格式 | 兼容性用 H.264 |
| Audio bitrate | 音频数据速率 | 192-320 kbps |
| Audio sample rate | 音频频率 | 48000 Hz |

### 渲染选项

| 选项 | 描述 |
|------|------|
| Full project | 渲染整个时间线 |
| Selected zone | 仅渲染选定区域（入/出点） |
| More options | 附加编解码器参数 |

### 批量渲染

1. 设置多个不同设置的渲染任务。
2. 将每个添加到渲染队列。
3. 开始批量处理。所有任务顺序渲染。

---

## 键盘快捷键

### 通用

| 快捷键 | 操作 |
|--------|------|
| `Ctrl + N` | 新建项目 |
| `Ctrl + O` | 打开项目 |
| `Ctrl + S` | 保存项目 |
| `Ctrl + Shift + S` | 另存为 |
| `Ctrl + Z` | 撤销 |
| `Ctrl + Shift + Z` | 重做 |
| `Ctrl + Enter` | 渲染 |
| `F11` | 全屏 |

### 时间线

| 快捷键 | 操作 |
|--------|------|
| `Space` | Play/Pause |
| `J` | 反向播放 |
| `K` | 停止 |
| `L` | 正向播放 |
| `I` | 设置入点 |
| `O` | 设置出点 |
| `Shift + R` | 剃刀工具 |
| `X` | 提取选定范围 |

### 导航

| 快捷键 | 操作 |
|--------|------|
| `Home` | 跳到项目开头 |
| `End` | 跳到项目结尾 |
| `Left` | 上一帧 |
| `Right` | 下一帧 |
| `Shift + Left` | 后退 1 秒 |
| `Shift + Right` | 前进 1 秒 |
| `Ctrl + Left` | 跳到上一个剪切点 |
| `Ctrl + Right` | 跳到下一个剪切点 |

### 编辑

| 快捷键 | 操作 |
|--------|------|
| `V` | 在播放头插入片段 |
| `B` | 在播放头覆盖片段 |
| `Delete` | 删除选区 |
| `Shift + Delete` | 波纹删除 |
| `Ctrl + C` | 复制 |
| `Ctrl + V` | 粘贴 |
| `Ctrl + A` | 全选 |
| `Ctrl + Shift + A` | 取消全选 |
