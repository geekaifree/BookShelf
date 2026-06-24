# 音乐制作

> 本文档整合了以下源文件：musicProduction.md, production.md, synths.md, score.md, dj.md, drums.md, daw.md, audio.md, music.md, tenacity.md

---

## 来源：musicProduction.md

本文档整理了音乐制作领域的软件、硬件、服务和学习资源，涵盖从入门到专业的完整工具链。

---

## 目录

1. [数字音频工作站 (DAW)](#1-数字音频工作站-daw)
2. [编程库与开发工具](#2-编程库与开发工具)
3. [现场编码音乐](#3-现场编码音乐)
4. [合成器（软件）](#4-合成器软件)
5. [音乐制作应用](#5-音乐制作应用)
6. [在线 Web 应用](#6-在线-web-应用)
7. [AI 音乐创作服务](#7-ai-音乐创作服务)
8. [音乐发行与推广](#8-音乐发行与推广)
9. [音色与采样资源](#9-音色与采样资源)
10. [数据集](#10-数据集)
11. [硬件：合成器与乐器](#11-硬件合成器与乐器)
12. [硬件：MIDI 控制器](#12-硬件midi-控制器)
13. [社区与标准](#13-社区与标准)
14. [学习资源](#14-学习资源)
15. [研究论文](#15-研究论文)

---

## 1. 数字音频工作站 (DAW)

DAW 是音乐制作的核心软件，用于录音、编曲、混音和母带处理。

| 名称 | 说明 | 平台 | 费用 |
|------|------|------|------|
| [Ableton Live](https://www.ableton.com/en/live/) | 支持 Session View 的片段式现场表演与即兴创作 | Win/Mac | 付费 |
| [ACID](https://web.archive.org/web/20231221120049/https://www.magix.com/us/music-editing/acid/) | 以循环制作为特色的 DAW | Win | 付费 |
| [Ardour](https://ardour.org) | 开源跨平台 DAW，支持录音、编辑和混音 | Win/Mac/Linux | 免费 |
| [Bitwig](https://www.bitwig.com/) | 模块化 DAW，支持丰富的调制功能 | Win/Mac/Linux | 付费 |
| [Cakewalk](https://www.bandlab.com/products/cakewalk) | BandLab 出品的全功能免费 DAW | Win | 免费 |
| [Cubase](https://www.steinberg.net/cubase/) | Steinberg 出品的专业级 DAW | Win/Mac | 付费 |
| [Digital Performer](https://motu.com/en-us/products/software/dp/) | MOTU 出品，深度 MIDI 编辑与乐谱功能 | Win/Mac | 付费 |
| [FamiStudio](https://bleubleu.itch.io/famistudio) | NES 风格音乐编辑器 | 多平台 | 免费 |
| [FL Studio](https://www.image-line.com/fl-studio/) | 完整的音乐制作环境 | Win/Mac | 付费 |
| [GarageBand](https://www.apple.com/mac/garageband/) | macOS/iOS 免费 DAW，内置乐器和教程 | Mac/iOS | 免费 |
| [Giada](https://www.giadamusic.com) | 极简音频工具，适合 DJ 和现场表演 | 多平台 | 免费 |
| [GridSound](https://github.com/gridsound/daw) | 基于 Web Audio API 的在线免费 DAW | 浏览器 | 免费 |
| [Helio](https://helio.fm/) | 自由音乐作曲软件 | 多平台 | 免费 |
| [LMMS](https://lmms.io/) | 开源跨平台综合 DAW | Win/Mac/Linux | 免费 |
| [Logic Pro X](https://www.apple.com/logic-pro/) | 专业 macOS DAW，大量内置乐器和效果器 | Mac | 付费 |
| [Meadowlark](https://github.com/MeadowlarkDAW) | 开源跨平台 DAW | 多平台 | 免费 |
| [MilkyTracker](https://milkytracker.org/) | 继承 Fasttracker II 传统的多平台音乐应用 | 多平台 | 免费 |
| [Mixcraft](https://acoustica.com/products/mixcraft) | Windows DAW 软件 | Win | 付费 |
| [Pro Tools](https://www.avid.com/pro-tools) | Avid 出品的行业标准 DAW | Win/Mac | 付费 |
| [Reaper](http://reaper.fm) | 完整的数字音频制作应用 | Win/Mac | 付费 |
| [Reason](https://www.reasonstudios.com/) | 模拟真实硬件机架的虚拟乐器与效果器 DAW | Win/Mac | 付费 |
| [Renoise](https://www.renoise.com) | 基于 Tracker 模式的多平台 DAW | Win/Mac/Linux | 付费 |
| [Stargate DAW](https://github.com/stargatedaw/stargate) | 一体化 DAW 及插件套件 | Win/Mac/Linux | 免费 |
| [Studio One Pro](https://www.fender.com/pages/fender-studio-pro) | 完整 DAW 与现场演出编排 | Win/Mac | 付费 |
| [SunVox](https://nightradio.itch.io/sunvox) | 轻量快速的模块化合成器与 Tracker | 多平台 | 免费 |
| [TuneFlow](https://tuneflow.com) | AI 驱动的免费 DAW，支持歌词/音乐生成、人声分离、MIDI 转录 | 多平台 | 免费 |
| [Waveform Pro](https://www.tracktion.com/products/waveform-pro) | 面向现代制作人的 DAW | Win/Mac | 付费 |
| [Zrythm](https://www.zrythm.org/en/index.html) | 跨平台 DAW | 多平台 | 免费 |

---

## 2. 编程库与开发工具

面向开发者的音乐编程语言、音频处理库和算法作曲工具。

| 名称 | 说明 | 语言/平台 |
|------|------|-----------|
| [Alda](https://github.com/alda-lang/alda) | 面向音乐家的音乐编程语言 | 多语言 |
| [ATM CLI](https://github.com/allthemusicllc/atm-cli) | 命令行 MIDI 文件生成与处理工具 | CLI |
| [Aubio](https://aubio.org) | 音频分割、音高检测、节拍追踪与 MIDI 流生成 | C/Python |
| [Augmented Audio](https://github.com/yamadapc/augmented-audio) | Rust 音频编程库 | Rust |
| [Band.js](https://github.com/meenie/band.js) | Web Audio API 音乐作曲接口 | JavaScript |
| [Blip](https://jshanley.github.io/blip/) | Web Audio API 循环与采样 | JavaScript |
| [Cane](https://github.com/tarpit-collective/cane) | 基于向量和欧几里得节奏的 MIDI 音序器 DSL | DSL |
| [CSound](https://csound.com/index.html) | 声音与音乐计算系统 | 独立 |
| [Dplug](https://github.com/AuburnSounds/dplug) | 用 D 语言制作音频插件的库 | D |
| [Euterpea](https://www.euterpea.com/) | Haskell 嵌入式计算机音乐语言 | Haskell |
| [Faust](https://faust.grame.fr) | 声音合成与音频处理的函数式编程语言 | 独立 |
| [FourVoices](https://github.com/erickim555/FourVoices) | 四声部自动音乐生成器 | 多语言 |
| [Gwion](https://github.com/Gwion/Gwion) | 强类型定时编程语言，受 ChucK 启发 | 独立 |
| [Houdini Music Toolset](https://github.com/andrew-lowell/HMT) | 为 3D 软件 Houdini 添加 MIDI 功能 | Houdini 插件 |
| [Kord](https://github.com/twitchax/kord) | Rust 和 JavaScript 的乐理二进制工具与库 | Rust/JS |
| [LatentScore](https://github.com/prabal-rje/latentscore) | 无需 GPU 的 Python 文本转环境音乐工具 | Python |
| [Leipzig](https://github.com/ctford/leipzig) | Clojure/ClojureScript 作曲库 | Clojure |
| [libsoundio](http://libsound.io) | 跨平台音频输入输出库 | C |
| [Magenta](https://magenta.tensorflow.org) | 基于机器学习的音乐与艺术生成 | Python/TF |
| [Megra.rs](https://github.com/the-drunk-coder/megra.rs) | Rust 算法作曲库 | Rust |
| [mididings](https://github.com/mididings/mididings) | Python MIDI 路由与处理器（Linux/macOS） | Python |
| [Music Suite](https://music-suite.github.io/) | Haskell 音乐描述语言 | Haskell |
| [Nashville](https://github.com/sgoudie/nashville) | 纳什维尔数字系统 (NNS) 转和弦工具 | 多语言 |
| [Octavian](https://github.com/stevekinney/octavian) | 音符、频率和音程推理工具 | JavaScript |
| [Orca](https://hundredrabbits.itch.io/orca) | 用于创建程序化音序器的深奥编程语言 | 独立 |
| [Overtone](https://github.com/overtone/overtone) | 开源合成器设计与音乐协作工具包 | Clojure |
| [Pippi](https://pippi.world) | Python 计算机音乐库 | Python |
| [PitchFinder](https://github.com/peterkhayes/pitchfinder) / [Node PitchFinder](https://github.com/cristovao-trevisan/node-pitchfinder) | JavaScript 音高检测算法库 | JavaScript |
| [Pop2Piano](https://sweetcocoa.github.io/pop2piano_samples/) | 流行音频转钢琴翻奏生成 | Python |
| [Scribbletune](https://github.com/scribbletune/scribbletune) | 用 JavaScript 创建音乐 | JavaScript |
| [Sharp11](https://github.com/jsrmath/sharp11) | 音乐理论化与即兴演奏引擎 | JavaScript |
| [Slang](http://slang.kylestetz.com) | JavaScript 简单音频编程语言 | JavaScript |
| [Spectmorph](https://www.spectmorph.org/) | 乐器采样分析与变形 | 独立 |
| [Spleeter](https://github.com/deezer/spleeter) | 音源分离库（如从混音中提取鼓轨） | Python |
| [Tonal](https://github.com/tonaljs/tonal) | 函数式音乐理论库 | JavaScript |
| [Tone.js](https://github.com/Tonejs/Tone.js) | Web Audio 框架，用于浏览器交互式音乐 | JavaScript |
| [Tuna](https://github.com/Theodeus/tuna) | Web Audio API 音频效果库 | JavaScript |
| [VCV Rack](https://vcvrack.com) | 开源虚拟模块化合成器 | 多平台 |
| [Verovio](https://www.verovio.org) | 音乐记谱排版库 | 多语言 |
| [Vivid](https://hackage.haskell.org/package/vivid) | Haskell + SuperCollider 高质量音频 | Haskell |
| [xenharmlib](https://xenharmlib.readthedocs.io/en/latest/index.html) | Python 微分音音乐作曲库 | Python |

---

## 3. 现场编码音乐

现场编码 (Live Coding) 是通过编写代码实时生成音乐的表演形式。

| 名称 | 说明 |
|------|------|
| [Glicol](https://github.com/chaosprint/glicol) | Rust 编写的图形化现场编码语言与音频 DSP 库 |
| [Klangmeister](https://ctford.github.io/klangmeister/) | 浏览器端现场编码环境 |
| [Line](https://github.com/pd3v/line) | 面向现场编码的命令行 MIDI 音序器与语言 |
| [Pattrns](https://pattrns.renoise.com/) | 算法或现场音乐编码的音乐序列生成器 |
| [Sardine](https://github.com/Bubobubobubobubo/sardine) | Python 现场编码音乐库 |
| [Sonic Pi](https://github.com/sonic-pi-net/sonic-pi) | 面向所有人的现场编码音乐合成器 |
| [Strudel](https://strudel.cc) | 基于 Web 的算法模式现场编码环境 |
| [TidalCycles](https://tidalcycles.org) | 描述复调、复合节奏和生成式音乐序列的编程语言 |

更多资源参见 [Awesome Livecoding](https://github.com/toplap/awesome-livecoding)。

---

## 4. 合成器（软件）

独立的软件合成器和虚拟乐器。

| 名称 | 说明 | 费用 |
|------|------|------|
| [Altitude](https://nakst.gitlab.io/altitude/) | 高级混合合成工作站 | 免费 |
| [Amsynth](https://amsynth.github.io) | 经典减法合成器拓扑结构 | 免费 |
| [Apricot](https://nakst.gitlab.io/apricot/) | 高效混合合成器，音色宏大 | 免费 |
| [Fluctus](https://nakst.gitlab.io/fluctus/) | 简单的 3 算子 FM 合成器 | 免费 |
| [Helm](https://tytel.org/helm/) | GPL 授权的复调合成器，丰富调制 | 免费 |
| [Mika Micro](https://tesselode.itch.io/mika-micro) | 免费开源减法合成器 VST | 免费 |
| [NSynth Super](https://experiments.withgoogle.com/nsynth-super) | Google Magenta 团队的开源 AI 合成器 | 免费 |
| [OpenUtau](https://www.openutau.com) | 开源歌声合成平台 | 免费 |
| [SAW](https://handmade.network/p/432/saw) | 简洁 UI 的直觉式合成器 | 免费 |
| [Surge Synthesizer](https://surge-synthesizer.github.io) | 开源数字合成器 | 免费 |
| [Yoshimi](https://yoshimi.github.io/) | 软件音频合成器 | 免费 |
| [Substation for VCV Rack](https://slimechildaudio.itch.io/substation) | 复合节奏、次谐波合成工具包 | 付费 |

---

## 5. 音乐制作应用

各类辅助音乐制作的桌面和移动端应用。

| 名称 | 说明 | 费用 |
|------|------|------|
| [1BITDRAGON](https://1bitdragon.itch.io/1bitdragon) | 易用的音乐创作工具，200+ 乐器和鼓采样 | 付费 |
| [Captain Plugins](https://mixedinkey.com/captain-plugins/) | 和弦进行、旋律、贝斯线和节拍生成插件套件 | 付费 |
| [ChipTone](https://sfbgames.itch.io/chiptone) | 免费音效生成工具 | 免费 |
| [Composer's Sketchpad](http://composerssketchpad.com) | 结合五线谱与速写本的音序器 (iOS) | 付费 |
| [Dragonfly Reverb](https://github.com/michaelwillis/dragonfly-reverb) | 开源混响效果器 | 免费 |
| [FreeEQ8](https://github.com/GareBear99/FreeEQ8) | 免费开源 8 段参量均衡插件 (VST3/AU) | 免费 |
| [Graillon](https://auburnsounds.itch.io/graillon) | 人声音高校正、共振峰偏移和实时变声插件 | 付费 |
| [JJazzLab](https://www.jjazzlab.org/en/) | 轻松为任意歌曲生成动态伴奏 | 免费 |
| [Max](https://cycling74.com/products/max) | 音乐与多媒体创作的可视化编程语言 | 付费 |
| [Melodics](https://melodics.com) | 桌面应用，教授 MIDI 键盘、打击垫和电子鼓的演奏 | 付费 |
| [Orb Producer Suite](https://www.landr.com/plugins/landr-composer) | AI 辅助的旋律、贝斯线、和弦和琶音生成插件套件 | 付费 |
| [Ossia Score](https://ossia.io) | 音视觉和互动演出的音序器 | 免费 |
| [Polyphone](https://www.polyphone.io/) | SoundFont 编辑器 | 免费 |
| [Sonic Visualiser](https://sonicvisualiser.org) | 音频录音的可视化、分析和标注 | 免费 |
| [Transcribe!](https://www.seventhstring.com/xscribe/overview.html) | 辅助转录录制音乐的应用 | 付费 |
| [Ultimate Vocal Remover](https://ultimatevocalremover.com/) | AI 驱动的人声移除工具 | 免费 |

---

## 6. 在线 Web 应用

无需安装，在浏览器中即可使用的音乐工具。

| 名称 | 说明 | 费用 |
|------|------|------|
| [AI Duet](https://experiments.withgoogle.com/ai-duet) | 智能钢琴，会回应你的演奏 | 免费 |
| [Beat Push](https://beatpush.com/) | 在线音乐制作，内置鼓机和合成器 | 免费 |
| [Circle of 5ths Explorer](https://www.frazierpianostudio.com/resources/circle-of-fifths-explorer/) | 五度圈交互探索工具 | 免费 |
| [Frequency Explorer](https://github.com/ellamenop/frex) | 微分音加法合成器 + 音序器 | 免费 |
| [Funklet](https://goodhertz.com/funklet/) | 鼓机与经典鼓节奏库 | 免费 |
| [Hookpad](https://www.hooktheory.com/hookpad) | 歌曲创作工具，基于 TheoryTab 数据库提供和弦、旋律和理论辅助 | 付费 |
| [Loudness Penalty](https://www.loudnesspenalty.com/) | 检查音轨响度及流媒体平台的惩罚幅度 | 免费 |
| [mix check studio](https://mixcheckstudio.roexaudio.com/) | 检查混音和母带的常见问题 | 免费 |
| [MyNoise](https://mynoise.net/) | 背景噪音与交互式声景 | 免费 |
| [Piano Genie](https://magenta.tensorflow.org/pianogenie) | 机器学习增强的钢琴应用 | 免费 |
| [Roland 50 Studio](https://roland50.studio) | 经典 Roland 设备模拟在线工作台 | 免费 |
| [Scale Explorer](https://www.frazierpianostudio.com/resources/scale-explorer/) | 音阶可视化探索工具 | 免费 |
| [Song Maker](https://musiclab.chromeexperiments.com/Song-Maker/) | 简单的步进音序器 | 免费 |
| [Splice](https://splice.com) | 音乐创作与协作平台 | 付费 |
| [SuperCollider](https://supercollider.github.io) | 音频合成与算法作曲平台 | 免费 |
| [Tap Tempo](https://tapbpmhub.com/) | 免费 BPM 测试工具，支持 Web MIDI 同步硬件 | 免费 |
| [Tonalux](https://tonalux.org) | 免费音频工具：频谱分析仪、插件比较器和媒体转换器 | 免费 |
| [WhatChord](https://whatchord.earthmanmuons.com/) | 实时 MIDI 和弦识别与和弦构建探索 | 免费 |

---

## 7. AI 音乐创作服务

| 名称 | 说明 | 费用 |
|------|------|------|
| [ILLUGEN](https://www.waves.com/illugen) | AI 文本转采样引擎 | 付费 |
| [LAIVE](https://www.laive.io) | AI 音乐创作平台 | 付费 |
| [LatentScore Live](https://latentscore.com) | 浏览器端文本生成环境音乐 | 免费 |
| [MemoTune](https://memotune.com) | 文本或歌词转完整歌曲，含 AI 人声 | 付费 |
| [OBSIDIAN Neural](https://obsidian-neural.com) | 实时 AI 循环生成 VST3 插件，支持 MIDI 触发 | 付费 |
| [Omnizart](https://github.com/Music-and-Culture-Technology-Lab/omnizart) | 人声、鼓、和弦、节拍等自动转录 | 免费 |
| [Splash](https://www.splashmusic.com) | AI 音乐创作平台 | 免费 |
| [Suno AI](https://suno.com/) | AI 音乐作曲与制作平台 | 付费 |

---

## 8. 音乐发行与推广

### 音乐发行平台

| 名称 | 费用 |
|------|------|
| [Amuse](https://www.amuse.io/en/) | 免费 |
| [BandCamp](https://bandcamp.com) | 免费 |
| [DistroKid](https://distrokid.com) | 付费 |
| [DittoMusic](https://dittomusic.com/en) | 付费 |
| [MDIIO](https://www.wearemdiio.com) | 免费 |
| [Octiive](https://www.octiive.com) | 付费 |
| [RecordJet](https://recordjet.com/) | 付费 |
| [ReverbNation](https://www.reverbnation.com) | 免费 |
| [SoundCloud](https://artists.soundcloud.com) | 免费 |
| [TuneCore](https://www.tunecore.com) | 付费 |

### 音乐推广

| 名称 | 说明 | 费用 |
|------|------|------|
| [SubmitHub](https://www.submithub.com) | 向博主和策展人提交音乐 | 付费 |

---

## 9. 音色与采样资源

| 名称 | 说明 | 费用 |
|------|------|------|
| [BigSoundBank](https://bigsoundbank.com/) | 2800+ 免费免版税音效 | 免费 |
| [Musical Artifacts](https://musical-artifacts.com/) | 音乐相关软件、采样、预设的分享与保存平台 | 免费 |
| [PremiumBeat](https://www.premiumbeat.com) | 精选高品质音乐和音效 | 付费 |
| [Soundstripe](https://www.soundstripe.com) | 视频用免版税音乐和音效 | 付费 |
| [Splice](https://splice.com/features/sounds) | 免版税采样、One-Shot、循环、MIDI 和预设 | 付费 |

---

## 10. 数据集

| 名称 | 说明 |
|------|------|
| [Free MIDI Chords](https://github.com/ldrolez/free-midi-chords) | 免费 MIDI 和弦与进行合集 |
| [SigSep](https://sigsep.github.io/) | 音源分离研究的公开数据集 |

---

## 11. 硬件：合成器与乐器

### 合成器（硬件）

| 名称 | 说明 | 费用 |
|------|------|------|
| [dadamachines](https://dadamachines.com) | 自动化模拟声音创作工具包 | 付费 |
| [LittleBits Electronic Music Inventor Kit](https://sphero.com/collections/littlebits) | 电子音乐发明套件 | 付费 |
| [OP-1](https://teenage.engineering/products/op-1) | 便携式音乐工作站，含采样器、多轨支持和内置合成 | 付费 |
| [Organelle](https://www.critterandguitari.com/organelle) | 直觉控制与强大灵活的声音引擎 | 付费 |
| [Pocket Operators](https://teenage.engineering/products/po) | 小巧低价的数字乐器系列 | 付费 |
| [ZynAddSubFX](https://github.com/zynaddsubfx/zynaddsubfx) | 复调全功能软件合成器 | 免费 |
| [Zynthian](https://zynthian.org/) | 开源硬件合成器，多引擎、滤波器和效果器 | 开源 |

### 乐器

| 名称 | 说明 | 费用 |
|------|------|------|
| [Chapman Stick](https://stick.com/) | 8/10/12 弦指板敲击乐器 | 付费 |
| [Harpejji](https://www.marcodi.com/products) | 电弦乐器 | 付费 |
| [Orba](https://web.archive.org/web/20241216222921/https://artiphon.com/pages/orba-family) | 球形手持乐器 | 付费 |
| [OTTO](https://github.com/bitfieldaudio/OTTO) | 采样器、音序器、多引擎合成器和效果器一体化设备 | 开源 |
| [Oxi One](https://oxiinstruments.com/oxi-one/) | 便携式网格音序器和合成器 | 付费 |
| [Pocket Piano](https://www.critterandguitari.com/201-pocket-piano) | 紧凑设计的钢琴和多种音色 | 付费 |

---

## 12. 硬件：MIDI 控制器

| 名称 | 说明 | 费用 |
|------|------|------|
| [Artiphon](https://www.artiphon.com/) | 吉他式 MPE 控制器 | 付费 |
| [Bela](https://bela.io) | 创建响应式交互应用的计算平台 | 付费 |
| [Continuum Fingerboard](https://www.hakenaudio.com/) | 线性钢琴式 MPE 演奏表面 | 付费 |
| [Eigenharp](https://web.archive.org/web/20250227113752/http://www.eigenlabs.com/info/) | 网格、呼吸管和触控条 MPE 乐器 | 付费 |
| [Haxophone](https://github.com/cardonabits/haxo-hw) | 类似萨克斯的电子乐器 | 开源 |
| [Joue](https://jouemusic.com/) | 富有表现力的模块化 MPE 控制器 | 付费 |
| [LinnStrument](https://www.rogerlinndesign.com/linnstrument) | 基于网格的表现力 MPE 控制器 | 付费 |
| [Lumatone](https://www.lumatone.io) | 六角形等音程键盘 | 付费 |
| [Morph](https://sensel.com/pages/the-sensel-morph) | 可更换硬件界面的表现力 MPE 触控控制器 | 付费 |
| [MPK Mini](https://www.akaipro.com/mpk-mini-mk3/) | 经济实用的小型键盘控制器 | 付费 |
| [OpenDeck](https://shanteacontrols.com) | 构建自定义 MIDI 控制器的硬件平台 | 开源 |
| [QuNexus](https://web.archive.org/web/20241106143831/https://www.musekinetics.com/products/qunexus/) | 小巧便携的 MPE 键盘 | 付费 |
| [ROLI Blocks](https://roli.com/eu/product/collection/create) | 可拼接的便携 MIDI 控制器 | 付费 |
| [Striso](https://www.striso.org) | 基于网格布局的表现力 MPE 控制器 | 付费 |

---

## 13. 社区与标准

| 名称 | 说明 |
|------|------|
| [Music Encoding Initiative](https://music-encoding.org) | 社区驱动的开源机器可读音乐记谱编码标准 |
| [Poly Expression](https://community.polyexpression.com) | 富有表现力的乐器和控制器论坛 |

---

## 14. 学习资源

### 乐理与教程

| 名称 | 说明 |
|------|------|
| [Integrated Musicianship](https://intmus.github.io/) | 免费开源的大学级音乐理论和听觉训练教材 |
| [Know Your Theory](https://knowyourtheory.com) | 乐理基础交互教程 |
| [Learning Synths](https://learningsynths.ableton.com/) | 合成器基础知识学习（Ableton 出品） |
| [Lightnote](https://www.lightnote.co/) | 通过动画和音频交互式学习乐理基础 |
| [Music Theory](https://ianring.com/musictheory/) | 音乐理论探索 |
| [muted.io](https://muted.io) | 交互式音乐理论工具与可视化参考 |
| [Theory Pages](https://tobyrush.com/theorypages/index.html) | 面向音乐人的乐理页面 |

### 技术文章

| 名称 | 说明 |
|------|------|
| [DeepAudioClassification](https://hackernoon.com/finding-the-genre-of-a-song-with-deep-learning-da8f59a61194) | 深度学习识别歌曲风格 |
| [Detecting piano notes with web audio](https://web.archive.org/web/20170215172439/https://hackernoon.com/a-web-audio-experiment-666743e16679) | Web Audio API 检测钢琴音符 |
| [Modeling Music with algebraic data types](https://reasonablypolymorphic.com/blog/modeling-music/) | 用代数数据类型建模音乐 |
| [Music Theory for Nerds](https://eev.ee/blog/2016/09/15/music-theory-for-nerds/) | 面向程序员的乐理概述 |
| [Musimathics](http://www.musimathics.com/) | 音乐的数学基础 |
| [Terry Riley's "In C"](https://teropa.info/blog/2017/01/23/terry-rileys-in-c.html) | 音乐可能性空间之旅 |
| [Training a Recurrent Neural Network to Compose Music](https://maraoz.com/2016/02/02/abc-rnn/) | 训练 RNN 作曲 |
| [Visual Music & Machine Learning Workshop for Kids](https://web.archive.org/web/20250105155027/https://becominghuman.ai/visual-music-machine-learning-workshop-for-kids-a90c957dab33) | 儿童视觉音乐与机器学习工作坊 |

### 工具参考

| 名称 | 说明 |
|------|------|
| [Audio Working Group](https://www.w3.org/groups/wg/audio/) | W3C 音频工作组，为 Web 平台添加高级音频合成能力 |
| [Awesome Sheet Music](https://github.com/ad-si/awesome-sheet-music) | 创建、编辑和显示乐谱的工具列表 |
| [Awesome WebAudio](https://github.com/notthetup/awesome-webaudio) | WebAudio 包和演示精选列表 |
| [Digital Filters Introduction](https://karlhiner.com/jupyter_notebooks/intro_to_digital_filters/) | 数字滤波器的 Jupyter Notebook 与几何解释 |
| [Linux DAW](https://linuxdaw.org/) | Linux 开源音频软件列表 |
| [SFZ Format](https://sfzformat.com) | SFZ 格式乐器创建的主要参考 |
| [Music Production Chips](https://music-chips.com/) | 社区管理的音乐制作技巧与窍门合集 |

---

## 15. 研究论文

| 名称 | 说明 |
|------|------|
| [Anticipatory Music Transformer](https://crfm.stanford.edu/2023/06/16/anticipatory-music-transformer.html) | 可控的音乐填充模型 |
| [Centre for Digital Music](https://c4dm.eecs.qmul.ac.uk) | 音乐与音频技术研究组 |
| [Harmony Explained](https://arxiv.org/abs/1202.4212v2) | 迈向科学音乐理论的进展 |
| [Musical User Interfaces](https://www.arthurcarabott.com/mui/) | 重新思考音频软件的设计方式 |
| [Universal Music Translation Network](https://research.facebook.com/publications/a-universal-music-translation-network/) | 通用音乐翻译网络 |
| [Virtual Reality Musical Instruments](https://doi.org/10.1162/COMJ_a_00372) | VR 乐器的现状、设计原则与未来方向 |

---

## 关键要点

1. **DAW 选择**：入门推荐免费的 LMMS、GarageBand 或 Cakewalk；专业制作推荐 Ableton Live、Logic Pro X 或 Pro Tools。
2. **AI 工具兴起**：Suno AI、TuneFlow、Spleeter 等 AI 工具正在改变音乐创作和后期处理的工作流程。
3. **现场编码**：Sonic Pi 和 TidalCycles 是入门现场编码音乐的良好起点。
4. **开源生态丰富**：从 DAW（Ardour、LMMS）到合成器（Surge、VCV Rack）再到效果器（Dragonfly Reverb），开源工具覆盖了音乐制作的各个环节。
5. **MPE 表现力控制**：LinnStrument、Joue、Morph 等 MPE 控制器代表了音乐演奏交互的前沿方向。
6. **Web 平台能力增强**：基于 Web Audio API 的工具（Tone.js、GridSound）使浏览器成为可行的音乐创作环境。
7. **音源分离技术**：Spleeter 和 Ultimate Vocal Remover 等工具让混音中的音轨分离变得简单。


---

## 来源：production.md

## 简介

awesome-music-production 仓库是音乐制作资源、工具和参考的精选集合。它涵盖数字音频工作站、合成器、采样、插件以及各级别制作者的学习材料。

| 类别 | 描述 |
|----------|-------------|
| DAW | 用于创作音乐的数字音频工作站 |
| 合成器 | 软件和硬件合成器 |
| 采样 | 采样库和音色包 |
| 插件 | VST、AU 和其他音频插件 |
| 学习 | 教程、课程和教育资源 |

## 数字音频工作站 (DAW)

### DAW 对比

| DAW | 平台 | 价格 | 最佳用途 |
|-----|----------|-------|----------|
| Ableton Live | Win/Mac | 付费 | 电子音乐、现场表演 |
| FL Studio | Win/Mac | 付费 | 节拍制作、Hip-hop |
| Logic Pro | Mac | 付费 | 所有风格、专业制作 |
| Pro Tools | Win/Mac | 付费 | 录音、混音、母带 |
| Reaper | Win/Mac/Linux | 平价 | 预算制作、灵活性 |
| GarageBand | Mac/iOS | 免费 | 初学者、学习 |
| Audacity | Win/Mac/Linux | 免费 | 基础编辑、播客 |
| LMMS | Win/Mac/Linux | 免费 | 电子音乐、开源 |

### DAW 功能对比

| 功能 | Ableton | FL Studio | Logic | Reaper |
|---------|---------|-----------|-------|--------|
| MIDI 编辑 | 优秀 | 优秀 | 优秀 | 良好 |
| 音频录制 | 良好 | 良好 | 优秀 | 优秀 |
| 内置乐器 | 优秀 | 优秀 | 优秀 | 基础 |
| 插件支持 | VST、AU | VST、AU | AU、VST | VST、AU |
| 价格范围 | $99-$749 | $99-$499 | $199 | $60-$225 |

## 合成器

### 软件合成器

| 合成器 | 类型 | 价格 | 描述 |
|-------------|------|-------|-------------|
| Serum | Wavetable | 付费 | 行业标准 Wavetable 合成器 |
| Vital | Wavetable | 免费/付费 | 强大的免费 Wavetable 合成器 |
| Massive X | Wavetable | 付费 | 高级 Wavetable 合成 |
| Sylenth1 | Subtractive | 付费 | 经典虚拟模拟 |
| Diva | 模拟建模 | 付费 | 精确的模拟仿真 |
| Dexed | FM | 免费 | Yamaha DX7 仿真 |
| Surge | 混合 | 免费 | 开源混合合成器 |
| Helm | Subtractive | 免费 | 开源减法合成器 |

### 合成器类型

| 类型 | 描述 | 示例音色 |
|------|-------------|----------------|
| Subtractive | 从振荡器过滤谐波 | Bass、Lead、Pad |
| Wavetable | 循环波形表 | 演变纹理、Lead |
| FM | 频率调制合成 | 钟声、金属音、Bass |
| Additive | 组合正弦波 | 类管风琴音、复杂音色 |
| Granular | 操纵音频颗粒 | 纹理、氛围 |
| 物理建模 | 模拟物理乐器 | 弦乐、木管、打击乐 |

## 音频效果

### 效果类别

| 类别 | 示例 | 用途 |
|----------|----------|---------|
| 动态 | Compressor、Limiter、Gate | 控制音量范围 |
| EQ | Parametric、Graphic | 塑造频率平衡 |
| 混响 | Room、Hall、Plate | 添加空间和深度 |
| 延迟 | Echo、Ping-pong、Tape | 创建重复 |
| 调制 | Chorus、Flanger、Phaser | 添加运动感 |
| 失真 | Overdrive、Saturation、Fuzz | 添加谐波 |
| 滤波器 | Low-pass、High-pass、Band-pass | 塑造音色 |

### 基本效果链

| 位置 | 效果 | 用途 |
|----------|--------|---------|
| 1 | EQ（减法） | 移除不需要的频率 |
| 2 | Compressor | 控制动态 |
| 3 | EQ（加法） | 增强所需频率 |
| 4 | Saturation | 添加温暖感和谐波 |
| 5 | Reverb/Delay | 添加空间感 |

## 采样库

### 免费采样来源

| 来源 | 描述 |
|--------|-------------|
| Splice | 基于订阅的采样市场 |
| Loopcloud | 采样管理和发现 |
| FreeSound | 社区贡献的采样 |
| NASA Audio | 太空相关音频采样 |
| BBC Sound Effects | BBC 音效库 |

### 采样类型

| 类型 | 描述 | 使用场景 |
|------|-------------|----------|
| One-shot | 单次采样 | 鼓、打击乐 |
| Loop | 重复的音乐片段 | 伴奏、节拍 |
| Multi-sample | 多力度层 | 真实乐器音色 |
| Foley | 现实世界音效 | 电影配乐、声音设计 |
| Vocal | 人声短语和即兴 | 人声制作 |

## MIDI 控制器

### 控制器类型

| 类型 | 示例 | 最佳用途 |
|------|----------|----------|
| 键盘 | Akai MPK、Novation Launchkey | 旋律和和弦输入 |
| 垫片 | Akai MPC、Native Instruments Maschine | 节拍制作 |
| 混音器 | Behringer X-Touch、Mackie Control | 混音和推子控制 |
| 吹奏 | Akai EWI、Roland Aerophone | 管乐器输入 |
| 吉他 | Fishman TriplePlay、Roland GR | 吉他 MIDI 输入 |

### 热门 MIDI 控制器

| 控制器 | 特性 | 价格范围 |
|-----------|----------|-------------|
| Akai MPK Mini | 25 键、8 垫片、8 旋钮 | $100-$150 |
| Novation Launchkey | 25-61 键、垫片、推子 | $150-$300 |
| Arturia KeyLab | 25-61 键、高级做工 | $200-$500 |
| Native Instruments Komplete Kontrol | 25-88 键、灯光指引 | $200-$700 |
| Akai MPC One | 独立制作 | $700-$1000 |

## 音乐理论资源

### 学习资源

| 资源 | 类型 | 费用 |
|----------|------|------|
| musictheory.net | 网站 | 免费 |
| Teoria | 网站 | 免费 |
| Hooktheory | 互动 | 免费增值 |
| Syntorial | 合成器训练 | 付费 |
| Ableton Learning Music | 互动 | 免费 |

### 音乐理论基础

| 概念 | 描述 |
|---------|-------------|
| 音阶 | 音符集合（大调、小调、五声） |
| 和弦 | 三个或更多音符同时演奏 |
| 进行 | 和弦序列 |
| 节奏 | 节拍和细分的模式 |
| 和声 | 音符之间的纵向关系 |
| 旋律 | 音符的横向序列 |

## 混音和母带

### 混音概念

| 概念 | 描述 |
|---------|-------------|
| 电平 | 音轨之间的音量平衡 |
| 声像 | 声音的立体声位置 |
| EQ | 频率平衡调整 |
| 压缩 | 动态范围控制 |
| 混响/深度 | 在混音中创造空间 |

### 母带处理链

| 步骤 | 处理 | 用途 |
|------|---------|---------|
| 1 | EQ | 最终音色调整 |
| 2 | 压缩 | 将混音粘合在一起 |
| 3 | 限幅 | 最大化响度 |
| 4 | 抖动 | 为最终格式准备 |

### 参考曲目

| 用途 | 描述 |
|---------|-------------|
| 频率平衡 | 对比音色质量 |
| 响度 | 匹配感知音量 |
| 立体声宽度 | 对比空间特性 |
| 编排 | 学习歌曲结构 |

## 制作技巧

### 编排结构

| 段落 | 小节数 | 用途 |
|---------|------|---------|
| Intro | 8-16 | 设定氛围 |
| Verse | 16-32 | 主叙事 |
| Chorus | 8-16 | 亮点和能量 |
| Bridge | 8-16 | 对比和变化 |
| Outro | 8-16 | 结尾 |

### 声音设计工作流

| 步骤 | 操作 |
|------|--------|
| 1 | 从基本波形开始 |
| 2 | 用滤波器和包络塑形 |
| 3 | 添加效果（混响、延迟等） |
| 4 | 调制参数以产生运动感 |
| 5 | 用额外效果处理 |

## 总结

| 主题 | 核心要点 |
|-------|-------------|
| DAW | 根据工作流、风格和预算选择 |
| 合成器 | Vital 和 Surge 等免费选项很强大 |
| 效果 | 理解信号链顺序 |
| 采样 | 使用来自可靠来源的高质量采样 |
| 控制器 | 物理输入改善工作流 |
| 学习 | 持续练习和参考曲目是关键 |


---

## 来源：synths.md

**来源：** https://github.com/Atarity/diy-synths

＃＃ 概述

本教程涵盖了 [Atarity/diy-synths](https://github.com/Atarity/diy-synths) 项目中的关键资源和工具。

## [网页版本](https://diy-synths.snnkv.com/) / [提交设计](https://github.com/Atarity/diy-synths/discussions) / [讨论](https://github.com/Atarity/diy-synths/discussions)

这是您可以构建的合成器和相关硬件的列表
靠你自己。所有设计都是开源的，包括固件。
[提交设计](https://github.com/Atarity/diy-synths/discussions) 这不是
在列表和[讨论](https://github.com/Atarity/diy-synths/discussions)
您的建筑经验。

1. [ATtiny Punk Console](https://github.com/noisio/ATtiny-Punk-Console) — ATtiny85 implementation of Atari Punk Console
1. [Acid Drip](https://github.com/lonesoulsurfer/Acid_Drip_Bassline_and_Drum_Synth) — Acid bassline synth and drum machine
1. [Aciduino](https://github.com/midilab/aciduino/tree/master/v1/) — Roland TB-303 step sequencer clone aimed for live interaction
1. [Ambika](https://mutable-instruments.net/archive/) — Multi-voice, hybrid synthesizer. Descendant of Shruthi.
1. [Anushri](https://mutable-instruments.net/archive/) — Analog monosynth with a lo-fi digital drums
1. [ArduTouch](https://github.com/maltman23/ArduTouch) — Arduino-compatible music synthesizer
1. [Arpie](https://six4pix.com/product/arpie/) — Compact, highly-functional, MIDI arpeggiator
1. [Beam Catcher](https://github.com/uvknhn/Beam-Catcher) — Analog light-based synthesizer
1. [Bread Modular](https://www.breadmodular.com/) — Affordable, compact modular synth platform
1. [Coron DS7 (DS8)](http://m.bareille.free.fr/ds7clone/ds8.htm) — Percussion & drum synth
1. [Drone & Drama](https://github.com/bjc01/D-D_Teensy) — Simple Teensy-based drone synth
1. [DrumKid](https://github.com/mattybrad/drumkid) — Lo-fi aleatoric Arduino drum machine
1. [Echo Rockit](https://musicfromouterspace.com/index.php?CATPARTNO=PCBMFECHONONE01&PROJARG=ECHOROCKIT%2FECHOROCKIT.php&MAINTAB=SYNTHDIY&SONGID=NONE&VPW=1331&VPH=1233) — Compact synth/effect processor
1. [Faderbank 16n](https://github.com/16n-faderbank/16n) — 16 faders MIDI-controller compatible with modular world
1. [Fasma Festival](https://github.com/ghztomash/fasma_drum) — Yet another Teensy drum machine with clock sync
1. [Flounder](https://github.com/MattKuebrich/flounder) — Teensy based USB midi keyboard + controls + stereo audio
1. [Grandbot](https://github.com/handeyeco/Grandbot) — Generative, pattern-based MIDI arpeggiator
1. [Hidden Sound Explorer](https://github.com/pangrus/HSE-Hidden_Sound_Explorer) — Electromagnetic fields analog transducer
1. [Hog](https://github.com/shmoergh/hog/) — Double-voice analog monophonic synthesizer with two oscillators
1. [Hypjolin](https://github.com/triglav-modular/Hypjolin) — Cross-modulating ultra-chaos generator
1. [Kastle 2](https://github.com/bastl-instruments/kastle2) — Patchable, pocketable and open platforrm
1. [Kastle](https://github.com/bastl-instruments/kastle) — Lo-fi, pocketable modular synth
1. [Keep](https://github.com/poetaster/keep) — Self-modulating analog synth based on the ancient XR 2206 IC
1. [Kelpie](https://github.com/friedpies/kelpie-pocket-synth) — Portable polyphonic digital synthesizer
1. [LMN-3](https://github.com/FundamentalFrequency) — OP-1 inspired DAW-in-a-box
1. [Le Strum](https://github.com/hotchk155/Voici-Le-Strum) — Compact and simple yet funny MIDI strummer
1. [Lil' mono](https://github.com/diysynth/STANDALONE-DEVICES) — Simple east-coast style analog synthesizer
1. [Lunchbeat](https://github.com/buranelectrix/lunchbeat-PCB) — 1-bit percussion sounds and a sequencer
1. [MIDIbox](http://ucapps.de/) — MIDI hardware platform
1. [MIDIvampire II](http://wiki.openmusiclabs.com/wiki/MidiVamp2) — 4 voice drum machine that is powered from the MIDI data line
1. [Matrix sequencer](https://github.com/CaratacusPotts/Matrix-Sequencer) — Standalone MIDI sequencer
1. [Meeblip Micro](https://github.com/MeeBlip/meeblip-circuits) — Hackable monophonic synth
1. [Meeblip SE](https://github.com/MeeBlip/meeblip-circuits) — Hackable monophonic synth
1. [Meeblip Triode](https://github.com/MeeBlip/meeblip-triode) — Hackable monophonic synth based on ATmega32
1. [Mega MIDI](https://github.com/AidanHockey5/MegaMIDI) — MIDI-compatible Sega Genesis/Megadrive synthesizer with real sound chips
1. [Mini Dexed](https://github.com/probonopd/MiniDexed) — FM synthesizer closely modeled on the famous DX7
1. [MiniMO](https://github.com/enveloop/miniMO) — ATtiny85 mini modular system
1. [Minichord](https://github.com/BenjaminPoilve/minichord) — Suzuki's Omnichord-like pocket instrument based on Teensy
1. [Mixtape Alpha](http://wiki.openmusiclabs.com/wiki/MixtapeAlpha) — Credit-card sized ATmega328 4 voice synth
1. [Moduleur](https://github.com/shmoergh/moduleur) — Double-voice analog modular design with a touch of digital magic
1. [Mozard](https://github.com/thomasfredericks/Mozard) — Arduino, Mozzi -based, 6 engines synth
1. [Multi](https://github.com/pangrus/multi/) — Generative sequencer with swappable synth engines
1. [Mushsynth-8](https://oshwlab.com/eugeniy.carlo/touchdrone_copy_copy_copy_copy) — 8-voice polyphonic drone synth with a touch keyboard
1. [N32B](https://github.com/Shik-Tech/N32B) — Hi-res macro MIDI controller
1. [NESizer2](https://github.com/Jaffe-/NESizer2/tree/master) — NES 2A03 chip controlled by ATmega328 with battery backed patch memory
1. [NSynth Super](https://github.com/googlecreativelab/open-nsynth-super) — An experimental physical interface for the NSynth AI algorithm
1. [NTH synth](https://github.com/NTHSynth/NTH_DSP) — 8-bit hackable mono synth
1. [Nano minipops](https://github.com/NANOmodules/NANO-Minipops) — Korg Minipops drum machine made around Arduino
1. [Nava](https://github.com/e-licktronic/Nava-v1.0) — Clone of Roland TR-909 drum machine
1. [Noise Toaster](https://musicfromouterspace.com/index.php?CATPARTNO=PCBMFNTSTNONE01&PROJARG=NOISETOASTER/NOISETOASTER.php&MAINTAB=SYNTHDIY&SONGID=NONE&VPW=1331&VPH=1233) — Simple, full analog noise synth
1. [NoiseLab](https://oshwlab.com/eugeniy.carlo/noisebox-1-0_copy) — Analog noise synthesizer
1. [Norns shield](https://github.com/monome/norns-shield) — Dynamic instrument, creation platform and musical computer 
1. [Nyblcore](https://github.com/schollz/nyblcore) — Tiny ATtiny85-based sample player device
1. [OP-Synth](https://github.com/thomasfredericks/Op-Synth) — Modular micro analog synth
1. [OTTO](https://github.com/bitfieldaudio/OTTO) — Digital groovebox with synths, looper, samplers, effects and a sequencer
1. [OpenDeck](https://github.com/shanteacontrols/OpenDeck) — Platform for ultimate MIDI control deck building
1. [Ottopot](https://gerotakke.de/ottopot/) — Hi-res USB-MIDI controller
1. [Overcycler](https://github.com/gligli/overcycler) — Polyphonic hybrid single cycle / analog synthesizer
1. [POLY555](https://github.com/oskitone/poly555) — Polyphonic, analog, square wave synth based on the 555 timer
1. [Paper Bits](https://paperpcb.dernulleffekt.de/doku.php?id=paper_bits:paper_bits_main) — Small, modular synthesizer system. Voltage controlled, stripboard compatible.
1. [PicoStepSeq](https://github.com/todbot/picostepseq) — 8-step MIDI sequencer
1. [PicoTracker](https://github.com/xiphonics/picoTracker) — Low cost music tracker platform
1. [Pikocore](https://github.com/schollz/pikocore) — Hackable, lo-fi music mangler based on the Raspberry Pi Pico
1. [Plinky](https://github.com/plinkysynth/plinky_public/tree/main) — 8-voice polyphonic touch synthesizer that specializes in fragile, melancholic sounds
1. [Polaron](https://github.com/zueblin/Polaron) — Digital drum machine based on Teensy 3
1. [Polykit X1](https://github.com/polykit/polykit-x-monosynth) — Full analog, semi modular synthesizer
1. [Portable synth](https://github.com/prajwal1121/Portable-Synth) — OP-1 style portable groovebox based on Teensy 4
1. [PreenFM 2](https://github.com/Ixox/preenfm2) — Beloved old FM synthesis in small, modern DIY box
1. [Protean](https://github.com/pangrus/Protean) — CMOS-based motion texture source
1. [Quantum DJ](https://warmplace.ru/hard/qdj/?fbclid=IwAR3kJHlGsxXUGChfXL_qjapHxT5TMV6Du6AfpE0VJ6x5OJzYAFS-qSvjPYk) — Electromagnetic noise to 1-bit sound converter
1. [Real SID shield](https://github.com/emceha/RealSIDShield) — Digital interface to SID chip of Commodore 64
1. [Roundabout](https://github.com/MattKuebrich/roundabout) — Compact, CMOS-based, patchable synth
1. [S54 Liv's Synth](https://github.com/SloBloLabs/LivSynth) — Hybrid mono synth with full analogue signal path
1. [SC1000](https://github.com/rasteri/SC1000/tree/master) — Portable digital scratch instrument
1. [Shruthi](https://mutable-instruments.net/archive/shruthi/build/) — Hybrid synth with digital generators and swappable analog filter boards
1. [Sigma-6](https://www.mjbauer.biz/Sigma6_M0_synth_weblog.htm) — Low-cost digital mono-synth
1. [Sound Lab Mini-Synth MkII](https://musicfromouterspace.com/index.php?CATPARTNO=SLMSMARKIIPCB&PROJARG=SOUNDLABMINIMARKII/page1.php&MAINTAB=SYNTHDIY&SONGID=NONE&VPW=1071&VPH=1229) — Full analog descendant of Sound Lab Mini-Synth
1. [Sound Lab Mini-Synth](https://musicfromouterspace.com/index.php?CATPARTNO=PCBMFSLMS&PROJARG=SOUNDLABMINISYNTH/page1.html&MAINTAB=SYNTHDIY&SONGID=NONE&VPW=1071&VPH=1229) — Full analog legendary MFOS design
1. [Spires](https://github.com/poetaster/spires) — Laser arpeggiator
1. [Teensy Audio FX](https://github.com/mattvenn/teensy-audio-fx) — Playable effects modeled on the Teenage Engineering PO series
1. [Teensy Beats Shield](https://github.com/trailhead/teensy-beats) — Handheld audio sequencer in PO style
1. [Totoro](https://github.com/Atarity/totoro-synth) — Cheap and easy to solder 2 oscillators synth on single IC
1. [WTPA2 (Where is the party at 2)](http://blog.narrat1ve.com/wtpa2/) — 8-bit audio sampler kit
1. [Wee Noise Maker](https://hackaday.io/project/19326-wee-noise-maker) — Pocket size sampler/sequencer with DAC, headphone amplifier and audio input
1. [Wirehead Freaq FM](https://github.com/Meebleeps/MeeBleeps-Freaq-FM-Synth) — Dual-voice, 2 operator, 8-bit FM synth in Volca form-factor
1. [Wirehead Mutant](https://github.com/Meebleeps/MeeBleeps-Mutant-Synth) — 8-bit, 2-oscillator subtractive Arduino synth for generative techno in Volca form-factor
1. [YM2149 Synth](https://github.com/trash80/Ym2149Synth) — Little chip that was used in various retro arcade machines and consoles now ready to serve
1. [Yocto](https://github.com/e-licktronic/Yocto-V2.0) — Clone of Roland TR-808 drum machine
1. [Yowler](https://github.com/cfoge/the_Yowler) — Compact and versatile noise/drone synth
1. [ZeKit](https://github.com/Marzac/zekit) — 4 voice paraphonic synth
1. [Zeptocore](https://github.com/schollz/_core) — Player and synthesizer, featuring stereo playback
1. [Zynthian](https://zynthian.org/) — Open platform for sound synthesis & processing
1. [x0xb0x](https://www.ladyada.net/make/x0xb0x/index.html) — Full reproduction of the original Roland TB-303 synthesizer, with fully functional sequencer

> 更新：2026-06-20

## 关键资源

|资源 |链接 |
|----------|------|
|网页版 | [https://diy-synths.snnkv.com/](https://diy-synths.snnkv.com/) |
|提交设计 | [https://github.com/Atarity/diy-synths/discussions](https://github.com/Atarity/diy-synths/discussions) |
|讨论| [https://github.com/Atarity/diy-synths/discussions](https://github.com/Atarity/diy-synths/discussions) |
|提交设计 | [https://github.com/Atarity/diy-synths/discussions](https://github.com/Atarity/diy-synths/discussions) |
|讨论 | [https://github.com/Atarity/diy-synths/discussions](https://github.com/Atarity/diy-synths/discussions) |
| ATtiny Punk 控制台 | [https://github.com/noisio/ATtiny-Punk-Console](https://github.com/noisio/ATtiny-Punk-Console) |
|酸滴| [https://github.com/lonesoulsurfer/Acid_Drip_Bassline_and_Drum_Synth](https://github.com/lonesoulsurfer/Acid_Drip_Bassline_and_Drum_Synth) |
|酸杜伊诺 | [https://github.com/midilab/aciduino/tree/master/v1/](https://github.com/midilab/aciduino/tree/master/v1/) |
|安比卡 | [https://mutable-instruments.net/archive/](https://mutable-instruments.net/archive/) |
|阿努什里 | [https://mutable-instruments.net/archive/](https://mutable-instruments.net/archive/) |
| ArduTouch | [https://github.com/maltman23/ArduTouch](https://github.com/maltman23/ArduTouch) |
|阿皮| [https://six4pix.com/product/arpie/](https://six4pix.com/product/arpie/) |
|光束捕捉器| [https://github.com/uvknhn/Beam-Catcher](https://github.com/uvknhn/Beam-Catcher) |
|面包模块| [https://www.breadmodular.com/](https://www.breadmodular.com/) |
|科龙 DS7 (DS8) | [http://m.bareille.free.fr/ds7clone/ds8.htm](http://m.bareille.free.fr/ds7clone/ds8.htm) |
|无人机与戏剧 | [https://github.com/bjc01/D-D_Teensy](https://github.com/bjc01/D-D_Teensy) |
|鼓童 | [https://github.com/mattybrad/drumkid](https://github.com/mattybrad/drumkid) |
|回声摇滚 | [https://musicfromouterspace.com/index.php?CATPARTNO=PCBMFECHONONE01&PROJARG=ECHOROCKIT%2FECHOROCKIT.php&MAINTAB=SYNTHDIY&SONGID=NONE&VPW=1331&VPH=1233] (https://musicfromouterspace.com/index.php?CATPARTNO=PCBMFECHONONE01&PROJARG=ECHOROCKIT%2FECHOROCKIT.php&MAINTAB=SYNTHDIY&SONGID=NONE&VPW=1331&VPH=1233) |
|法德银行 16n | [https://github.com/16n-faderbank/16n](https://github.com/16n-faderbank/16n) |
|法斯玛节| [https://github.com/ghztomash/fasma_drum](https://github.com/ghztomash/fasma_drum) |
|比目鱼 | [https://github.com/MattKuebrich/flounder](https://github.com/MattKuebrich/flounder) |
|机器人| [https://github.com/handeyeco/Grandbot](https://github.com/handeyeco/Grandbot) |
|隐藏的声音探索者 | [https://github.com/pangrus/HSE-Hidden_​​Sound_Explorer](https://github.com/pangrus/HSE-Hidden_​​Sound_Explorer) |
|猪| [https://github.com/shmoergh/hog/](https://github.com/shmoergh/hog/) |
|催眠素 | [https://github.com/triglav-modular/Hypjolin](https://github.com/triglav-modular/Hypjolin) |
|城堡2 | [https://github.com/bastl-instruments/kastle2](https://github.com/bastl-instruments/kastle2) |
|卡斯特尔 | [https://github.com/bastl-instruments/kastle](https://github.com/bastl-instruments/kastle) |
|保留| [https://github.com/poetaster/keep](https://github.com/poetaster/keep) |
|水鬼 | [https://github.com/friedpies/kelpie-pocket-synth](https://github.com/friedpies/kelpie-pocket-synth) |
| LMN-3 | [https://github.com/FundamentalFrequency](https://github.com/FundamentalFrequency) |



---

## 来源：score.md

## 目录

1. [MuseScore 简介](#introduction)
2. [界面与导航](#interface)
3. [音符输入方法](#note-input)
4. [乐谱格式化](#score-formatting)
5. [表情与力度记号](#expressions)
6. [分谱与乐器](#parts)
7. [回放与音频](#playback)
8. [发布与分享](#publishing)

---

## 简介

MuseScore 是一款免费、开源的乐谱软件，允许作曲家、编曲家和音乐家创建、编辑和打印专业品质的乐谱。

### MuseScore 核心功能

| 功能 | 描述 | 好处 |
|------|------|------|
| 所见即所得编辑器 | 可视化乐谱编辑 | 直觉化的作曲 |
| MIDI 输入 | 在 MIDI 键盘上演奏音符 | 快速音符输入 |
| 音频回放 | 听到你的作品 | 验证编曲 |
| 分谱提取 | 生成各声部分谱 | 管弦乐准备 |
| MusicXML 支持 | 标准文件格式 | 软件互操作性 |

### 系统要求

| 组件 | 最低 | 推荐 |
|------|------|------|
| 操作系统 | Windows 10, macOS 10.15, Linux | 最新版本 |
| 内存 | 4GB | 8GB 或更多 |
| 磁盘空间 | 500MB | 1GB |
| 显示 | 1280x720 | 1920x1080 |

### 文件格式

| 格式 | 扩展名 | 用途 |
|------|--------|------|
| MuseScore | .mscz | 原生格式（压缩） |
| MusicXML | .xml, .mxl | 标准交换格式 |
| MIDI | .mid | 音频数据交换 |
| PDF | .pdf | 打印就绪输出 |
| Audio | .mp3, .wav | 音频导出 |

---

## 界面与导航

了解 MuseScore 界面有助于高效处理复杂乐谱。

### 主界面组件

| 组件 | 位置 | 功能 |
|------|------|------|
| 菜单栏 | 顶部 | 文件、编辑、视图菜单 |
| 工具栏 | 菜单下方 | 常用工具和操作 |
| 乐谱视图 | 中央 | 主编辑区域 |
| 调色板 | 左侧 | 符号和标记 |
| 检查器 | 右侧 | 元素属性 |
| 状态栏 | 底部 | 光标位置信息 |

### 乐谱视图模式

| 模式 | 描述 | 用途 |
|------|------|------|
| 页面视图 | 完整页面布局 | 最终格式化 |
| 连续视图 | 水平滚动 | 作曲 |
| 单页 | 所有页面垂直排列 | 总览 |

### 导航工具

| 工具 | 快捷键 | 操作 |
|------|--------|------|
| 放大 | Ctrl+= | 放大乐谱 |
| 缩小 | Ctrl+- | 缩小乐谱 |
| 页面选择 | 导航器 | 跳转到页面 |
| 查找 | Ctrl+F | 搜索元素 |

### 选择方法

| 选择类型 | 方法 | 用途 |
|----------|------|------|
| 单个元素 | 点击 | 编辑一个元素 |
| 范围 | Shift+点击 | 选择小节范围 |
| 多选 | Ctrl+点击 | 选择特定元素 |
| 全部同类 | 右键 | 选择所有同类型 |

---

## 音符输入方法

MuseScore 提供多种输入音符的方式。

### 输入模式

| 模式 | 描述 | 速度 | 学习曲线 |
|------|------|------|----------|
| 步进 | 逐个输入音符 | 慢 | 简单 |
| 重新音高 | 更改现有音符的音高 | 中等 | 简单 |
| 节奏 | 先输入节奏再输入音高 | 快 | 中等 |
| 实时 | 实时演奏输入 | 最快 | 难 |

### 步进输入工作流

| 步骤 | 操作 | 快捷键 |
|------|------|--------|
| 1 | 选择音符时值 | 1-9 键 |
| 2 | 选择音高 | A-G 键 |
| 3 | 添加变音记号 | 上/下箭头 |
| 4 | 移动到下一位置 | 空格或右箭头 |
| 5 | 添加休止符 | 0（零） |

### 音符时值快捷键

| 快捷键 | 时值 | 符号 |
|--------|------|------|
| 1 | 64 分音符 |  |
| 2 | 32 分音符 |  |
| 3 | 16 分音符 |  |
| 4 | 8 分音符 |  |
| 5 | 4 分音符 |  |
| 6 | 2 分音符 |  |
| 7 | 全音符 |  |
| 8 | 二全音符 |  |
| 9 | 倍全音符 |  |

### 变音记号与修饰符

| 快捷键 | 符号 | 效果 |
|--------|------|------|
| 上箭头 | 升号 | 升高半音 |
| 下箭头 | 降号 | 降低半音 |
| = | 还原号 | 取消变音记号 |
| Shift+上 | 重升号 | 升高全音 |
| Shift+下 | 重降号 | 降低全音 |

---

## 乐谱格式化

正确的格式化确保乐谱可读且专业。

### 页面布局设置

| 设置 | 默认值 | 选项 | 用途 |
|------|--------|------|------|
| 页面大小 | A4 | Letter, A3, 自定义 | 打印格式 |
| 页边距 | 15mm | 10-30mm | 空白控制 |
| 谱线间距 | 1.75mm | 1.0-3.0mm | 谱表间距 |
| 每页行数 | 自动 | 固定或自动 | 布局密度 |

### 谱表属性

| 属性 | 描述 | 选项 |
|------|------|------|
| 线数 | 每个谱表的线数 | 1-5 |
| 谱表类型 | 标准、吉他谱、打击乐 | 根据乐器 |
| 小谱表 | 缩小尺寸 | 提示音、ossia |
| 隐藏谱表 | 空白时 | 减少翻页 |

### 小节格式化

| 操作 | 方法 | 快捷键 |
|------|------|--------|
| 添加小节 | 编辑 > 小节 | Ctrl+B（追加） |
| 删除小节 | 选择 + 删除 | Ctrl+Delete |
| 拆分小节 | 编辑 > 小节 | - |
| 合并小节 | 选择范围 + 编辑 | - |

### 文本格式化

| 文本类型 | 样式 | 字号 | 位置 |
|----------|------|------|------|
| 标题 | 粗体 | 22-24pt | 顶部居中 |
| 副标题 | 斜体 | 14-16pt | 标题下方 |
| 作曲者 | 正常 | 12pt | 右侧 |
| 歌词 | 正常 | 10pt | 谱表下方 |

---

## 表情与力度记号

音乐表情记号向演奏者传达演奏指示。

### 力度标记

| 符号 | 含义 | 力度等级 |
|------|------|----------|
| ppp | 极弱 | 非常非常轻 |
| pp | 很弱 | 非常轻 |
| p | 弱 | 轻 |
| mp | 中弱 | 中等偏轻 |
| mf | 中强 | 中等偏响 |
| f | 强 | 响 |
| ff | 很强 | 非常响 |
| fff | 极强 | 非常非常响 |

### 添加力度记号

| 步骤 | 操作 | 位置 |
|------|------|------|
| 1 | 选择音符 | 目标位置 |
| 2 | 打开调色板 | 左侧面板 |
| 3 | 找到力度记号 | 演奏法部分 |
| 4 | 双击符号 | 添加到乐谱 |

### 演奏法记号

| 符号 | 名称 | 效果 |
|------|------|------|
| > | 重音 | 强调音符 |
| . | 断音 | 缩短音符 |
| - | 保持音 | 完整时值 |
| ^ | 强重音 | 强烈强调 |
| ~ | 回音 | 装饰音 |

### 速度标记

| 标记 | 速度 | BPM 范围 |
|------|------|----------|
| Largo | 极慢 | 40-60 |
| Adagio | 慢 | 60-80 |
| Andante | 行板 | 80-100 |
| Moderato | 中速 | 100-120 |
| Allegro | 快 | 120-160 |
| Presto | 极快 | 160-200 |

---

## 分谱与乐器

处理多种乐器并为演奏者提取分谱。

### 乐器设置

| 操作 | 菜单路径 | 结果 |
|------|----------|------|
| 添加乐器 | 编辑 > 乐器 | 添加新乐器 |
| 移除乐器 | 选择 + 移除 | 移除乐器 |
| 更改顺序 | 上移/下移 | 重新排序 |
| 更移调 | 谱表属性 | 实际音高/移调音高 |

### 常见乐器族

| 乐器族 | 示例 | 谱号 | 移调 |
|--------|------|------|------|
| 弦乐 | 小提琴、大提琴 | 高音、低音 | 无 |
| 木管 | 长笛、单簧管 | 高音 | 不定 |
| 铜管 | 小号、长号 | 高音、低音 | 不定 |
| 打击 | 鼓、定音鼓 | 打击乐 | 不适用 |
| 键盘 | 钢琴、管风琴 | 大谱表 | 无 |

### 分谱提取

| 步骤 | 操作 | 结果 |
|------|------|------|
| 1 | 文件 > 分谱 | 打开分谱对话框 |
| 2 | 选择乐器 | 为每个分谱选择 |
| 3 | 生成分谱 | 创建独立乐谱 |
| 4 | 编辑分谱 | 独立编辑 |
| 5 | 打印或导出 | 各声部分谱 |

### 分谱格式选项

| 选项 | 描述 | 用途 |
|------|------|------|
| 隐藏空谱表 | 移除空白行 | 紧凑乐谱 |
| 显示所有谱表 | 完整管弦乐 | 研究乐谱 |
| 提示音 | 显示其他声部 | 声部意识 |
| 多小节休止 | 合并休止 | 更清晰的分谱 |

---

## 回放与音频

MuseScore 提供音频回放功能以预览作品。

### 回放控制

| 控制 | 快捷键 | 功能 |
|------|--------|------|
| 播放/暂停 | 空格 | 切换回放 |
| 停止 | Esc | 停止并重置 |
| 倒回 | Home | 回到开头 |
| 循环 | 循环按钮 | 重复选区 |

### 声音配置

| 设置 | 选项 | 用途 |
|------|------|------|
| SoundFont | 默认、自定义 | 乐器音色 |
| 混响 | 量滑块 | 房间氛围 |
| 合唱 | 量滑块 | 合奏效果 |
| 音量 | 主滑块 | 整体响度 |

### 速度与拍号

| 功能 | 控制 | 效果 |
|------|------|------|
| 速度标记 | 添加 > 文本 > 速度 | 设置 BPM |
| 拍号 | 添加 > 拍号 | 定义节拍 |
| 渐慢 | 速度变化 | 逐渐减速 |
| 渐快 | 速度变化 | 加速 |

### 音频导出

| 格式 | 质量 | 文件大小 | 用途 |
|------|------|----------|------|
| MP3 | 可变 | 小 | 分享 |
| WAV | 无损 | 大 | 专业 |
| FLAC | 无损 | 中等 | 归档 |
| OGG | 可变 | 小 | 网页 |

---

## 发布与分享

MuseScore 支持多种输出格式以分享你的作品。

### 打印选项

| 选项 | 描述 | 设置 |
|------|------|------|
| 页面范围 | 选择页面 | 全部或指定 |
| 份数 | 打印份数 | 1-99 |
| 方向 | 纵向/横向 | 根据乐谱 |
| 缩放 | 适应页面 | 调整大小 |

### 导出格式

| 格式 | 用途 | 质量 |
|------|------|------|
| PDF | 打印就绪 | 高 |
| PNG | 网页图片 | 可配置 |
| SVG | 矢量图 | 可缩放 |
| MusicXML | 软件交换 | 完整 |
| MIDI | 音频数据 | 仅音符数据 |

### 在线分享

| 平台 | 方式 | 受众 |
|------|------|------|
| MuseScore.com | 直接上传 | 社区 |
| YouTube | 音频 + 视频 | 大众 |
| SoundCloud | 仅音频 | 音乐人 |
| 个人网站 | 嵌入代码 | 自定义 |

### 协作功能

| 功能 | 描述 | 限制 |
|------|------|------|
| 评论 | 乐谱反馈 | 注册用户 |
| 版本历史 | 追踪变更 | 仅在线 |
| 复刻 | 复制并修改 | 公开乐谱 |
| 群组 | 团队协作 | 手动设置 |

---

## 总结

| 主题 | 核心要点 |
|------|----------|
| 输入 | 不同工作流的多种方法 |
| 格式化 | 正确间距的专业布局 |
| 力度记号 | 为演奏者提供富有表现力的标记 |
| 分谱 | 从总谱提取各声部分谱 |
| 回放 | 通过音频反馈预览作品 |
| 发布 | 导出用于打印、网页和协作 |


---

## 来源：dj.md

## 简介

Mixxx 是一款免费、开源的 DJ 软件，提供音乐混合、节拍匹配和现场 DJ 表演的工具。它支持多种硬件控制器和音频格式。

| 特性 | 描述 |
|---------|-------------|
| 跨平台 | 支持 Windows、macOS 和 Linux |
| 硬件支持 | 原生支持 90+ 款 DJ 控制器 |
| 音频格式 | MP3、OGG、FLAC、WAV、AIFF 等 |
| 许可证 | GNU GPL v2 |
| 社区 | 活跃开发，定期发布更新 |

## 核心概念

### 数字 DJ 术语

| 术语 | 定义 |
|------|------------|
| Deck | 虚拟唱盘，每次播放一首曲目 |
| Crossfader | 在两个 Deck 之间混合音频的滑块 |
| EQ (均衡器) | 调节低音、中音和高音频段的控制器 |
| BPM | 每分钟节拍数，曲目的速度 |
| Beatgrid | 将节拍标记与音频波形对齐 |
| Hotcue | 曲目中保存的位置，可即时跳转 |
| Loop | 连续重复播放一段音频 |
| Sync | Deck 之间的自动速度和相位匹配 |

### 界面布局

| 区域 | 用途 |
|---------|---------|
| Deck 面板 | 显示波形、播放控制和曲目信息 |
| 混音器区域 | 音量推子、EQ 旋钮和 Crossfader |
| 曲库面板 | 浏览和加载收藏中的曲目 |
| 效果区域 | 为每个 Deck 应用音频效果 |
| 采样器面板 | 在表演中触发短音频片段 |

## 入门

### 安装

| 平台 | 方法 |
|----------|--------|
| Windows | 从官网下载安装程序 |
| macOS | 下载 DMG 或使用 Homebrew：`brew install mixxx` |
| Ubuntu/Debian | `sudo apt install mixxx` |
| Fedora | `sudo dnf install mixxx` |
| Arch Linux | `sudo pacman -S mixxx` |

### 初始配置

1. 启动 Mixxx 并打开偏好设置
2. 配置音频输出（声卡选择）
3. 如有 DJ 控制器则进行设置
4. 配置音乐库文件夹

| 设置项 | 推荐值 |
|---------|-------------------|
| 采样率 | 44100 Hz 或 48000 Hz |
| 音频 API | ASIO (Windows)、CoreAudio (macOS)、ALSA (Linux) |
| 缓冲区大小 | 256-512 采样以获得低延迟 |
| 音高锁定 | 启用（调整速度时防止音高变化） |

## 曲库管理

### 添加音乐

```bash
# Mixxx 原生支持以下音频格式：
# - MP3、OGG Vorbis、OGG Opus、FLAC、WAV、AIFF
# - AAC（需要平台编解码器）
# - WMA（仅 Windows）
```

### 曲目组织

| 功能 | 描述 |
|---------|-------------|
| 播放列表 | 用于计划演出的有序曲目列表 |
| 灵感箱 | 无特定顺序的灵活收藏 |
| Auto DJ | 从播放列表自动播放并交叉淡入淡出 |
| 搜索 | 按标题、艺术家、BPM、调式或流派筛选曲目 |
| 历史记录 | 过往演出的曲目列表记录 |

### 分析曲目

在表演之前，分析曲目以启用高级功能。

| 分析类型 | 用途 |
|--------------|---------|
| BPM 检测 | 识别速度以用于同步和节拍匹配 |
| 调式检测 | 确定音乐调式以用于和声混音 |
| Beatgrid | 创建节拍标记以实现精确循环和效果 |
| ReplayGain | 跨曲目标准化音量电平 |

## 混音技巧

### 节拍匹配

节拍匹配是将两首曲目的速度和相位对齐的基本 DJ 技能。

| 步骤 | 操作 |
|------|--------|
| 1 | 将曲目加载到 Deck A 和 Deck B |
| 2 | 使用速度滑块匹配 BPM 值 |
| 3 | 使用波形显示对齐节拍 |
| 4 | 使用 Jog Wheel 微调曲目 |
| 5 | 使用 Sync 进行自动匹配 |

### EQ 混音

| 频段 | 范围 | DJ 用途 |
|-----------|-------|--------|
| 低频 (低音) | 20-250 Hz | 在曲目之间切换低音线 |
| 中频 | 250-4000 Hz | 混合人声和乐器 |
| 高频 (高音) | 4000-20000 Hz | 混合踩镲和镲片 |

### 交叉淡入淡出技巧

| 技巧 | 描述 |
|-----------|-------------|
| 切换 | 从一个 Deck 突然切换到另一个 |
| 淡入淡出 | 逐渐将 Crossfader 从一侧移动到另一侧 |
| 低音交换 | 保留一首曲目的低音同时播放另一首的中/高频 |
| EQ 混合 | 使用 EQ 旋钮创建平滑的频率过渡 |

## 效果

### 内置效果

| 效果 | 描述 |
|--------|-------------|
| Echo | 添加音频的延迟重复 |
| Reverb | 模拟房间声学效果 |
| Flanger | 创建扫频梳状滤波器效果 |
| Phaser | 类似 Flanger 但音色不同 |
| Filter | 低通或高通频率滤波 |
| Bitcrusher | 降低音频质量以产生 Lo-Fi 效果 |
| Delay | 速度同步的回声重复 |
| Autopan | 在左右声道之间循环音频 |

### 效果链

Mixxx 允许将多个效果组合成效果链。

| 配置 | 使用场景 |
|--------------|----------|
| 单效果 | 过渡期间的简单滤波器扫描 |
| 双效果 | Echo 加 Reverb 用于构建段 |
| 三效果 | 用于 Breakdown 的复杂纹理 |

## 控制器映射

### 支持的硬件

| 控制器类型 | 示例 |
|----------------|---------|
| 入门级 | Numark Mixtrack、Hercules DJControl |
| 中端 | Pioneer DDJ-400、Traktor S2 |
| 专业级 | Pioneer DDJ-1000、Denon MC7000 |
| 模块化 | Allen&Hone Xone:K2、MIDI fighters |

### 映射配置

控制器映射定义硬件控件如何与 Mixxx 交互。

| 控件类型 | 典型映射 |
|-------------|-----------------|
| Jog Wheel | 曲目拖拽和音高弯曲 |
| 推子 | 音量、速度和 Crossfader |
| 旋钮 | EQ、滤波器和效果参数 |
| 按钮 | 播放、Cue、Sync、Hotcue、Loop |
| 垫片 | Hotcue、采样和 Loop 触发 |

## 录制和广播

### 录制演出

| 设置 | 描述 |
|---------|-------------|
| 格式 | OGG Vorbis、MP3、WAV 或 FLAC |
| 质量 | 可配置比特率（有损格式 128-320 kbps） |
| 分割 | 按时间或大小分割录制的选项 |
| 元数据 | 自动标记曲目信息 |

### 直播广播

| 平台 | 协议 |
|----------|----------|
| Icecast | 通过 HTTP 流传输到 Icecast 服务器 |
| SHOUTcast | 传统流媒体协议 |

## 键盘快捷键

| 功能 | 默认快捷键 |
|----------|-----------------|
| 加载曲目到 Deck 1 | 从曲库拖拽 |
| 播放/暂停 Deck 1 | D |
| Cue Deck 1 | F |
| Sync Deck 1 | Shift+Q |
| Crossfader 左移 | 左箭头 |
| Crossfader 右移 | 右箭头 |
| 耳机 Cue Deck 1 | T |
| Loop 入点 | Shift+I |
| Loop 出点 | Shift+O |

## 总结

| 主题 | 核心要点 |
|-------|-------------|
| 设置 | 在表演前配置音频输出和控制器 |
| 曲库 | 分析曲目的 BPM、调式和 Beatgrid 数据 |
| 混音 | 掌握节拍匹配和 EQ 混合以实现平滑过渡 |
| 效果 | 恰当地使用效果来增强过渡 |
| 硬件 | 映射控制器以实现手动表演控制 |
| 录制 | 捕获演出用于回顾和分享 |


---

## 来源：drums.md

## 简介

Hydrogen 是一个高级的开源鼓机，适用于 GNU/Linux、macOS 和 Windows。它提供基于模式的鼓编程、基于采样的声音生成和 MIDI 支持，用于创建鼓轨道和节奏。本教程涵盖安装、界面导航、模式创建和歌曲编排。

## 系统要求

| 组件 | 最低配置 | 推荐配置 |
|------|----------|----------|
| CPU | 1 GHz | 2+ GHz |
| RAM | 512 MB | 2 GB |
| 磁盘 | 100 MB | 500 MB |
| 音频 | ALSA 或 JACK | JACK 或 PulseAudio |
| 显示 | 1024x768 | 1280x800+ |
| 操作系统 | Linux, macOS 10.12+, Windows 7+ | 最新版本 |

## 安装

### Linux

```bash
# Ubuntu/Debian
sudo apt install hydrogen

# Fedora
sudo dnf install hydrogen

# Arch
sudo pacman -S hydrogen

# Flatpak（通用）
flatpak install org.hydrogenmusic.Hydrogen
```

### macOS

```bash
# Homebrew
brew install hydrogen
```

或从发布页面下载 `.dmg` 文件。

### Windows

从官方发布页面下载安装程序并运行安装向导。

## 界面概览

### 主要部分

| 部分 | 位置 | 用途 |
|------|------|------|
| Pattern Editor | 中央 | 创建和编辑鼓模式 |
| Song Editor | 底部 | 将模式编排成歌曲 |
| Mixer | 右侧 | 调整音量和声像 |
| Instrument List | 左侧 | 选择鼓乐器 |
| Transport Bar | 顶部 | 播放、停止、录制控制 |
| BPM Display | 顶部 | 设置速度 |

### Pattern Editor 模式

| 模式 | 视图 | 用途 |
|------|------|------|
| Drum Pattern | 网格视图 | 在网格上放置打击 |
| Piano Roll | 音符视图 | 旋律打击乐编辑 |

## 创建基本节拍

### 步骤 1：设置速度

| 设置 | 位置 | 默认值 | 更改方法 |
|------|------|--------|----------|
| BPM | 传输栏 | 120 | 点击并输入新值 |
| Time Signature | Pattern Editor | 4/4 | 右键点击模式区域 |
| Pattern Length | Pattern Editor | 1 小节 | 在模式设置中调整 |

### 步骤 2：选择乐器

左侧的乐器列表显示可用的鼓声音：

| 乐器 | 典型声音 | 常见用途 |
|------|----------|----------|
| Kick | 底鼓 | 下拍，节奏基础 |
| Snare | 军鼓 | 反拍（第 2 和第 4 拍） |
| Closed Hi-Hat | 闭合踩镲 | 持续节奏 |
| Open Hi-Hat | 开放踩镲 | 强调，过渡 |
| Crash | 碎音镲 | 歌曲开始，强调 |
| Ride | 叮叮镲 | 持续节奏 |
| Tom High | 高音嗵鼓 | 过门 |
| Tom Mid | 中音嗵鼓 | 过门 |
| Tom Low | 低音嗵鼓 | 过门 |
| Clap | 拍手 | 强调叠加 |

### 步骤 3：放置鼓打击

点击网格放置打击：

```
Pattern: Basic Rock Beat (4/4)
Step:    1 . 2 . 3 . 4 . 5 . 6 . 7 . 8 . 9 . 10. 11. 12. 13. 14. 15. 16.
Kick:    X . . . . . . . X . . . . . . .
Snare:   . . . . X . . . . . . . X . . .
Hi-Hat:  X . X . X . X . X . X . X . X .
```

### 步骤 4：调整力度

每个打击可以有不同的力度（音量）：

| 力度范围 | 级别 | 音乐效果 |
|----------|------|----------|
| 0-40 | 柔和 | 鬼音，微妙 |
| 41-80 | 中等 | 正常演奏 |
| 81-110 | 强力 | 强烈强调 |
| 111-127 | 最大 | 最强打击 |

右键点击已放置的打击来调整力度。

## 模式属性

### 模式长度

| 长度 | 步数（16 分音符） | 音乐小节 |
|------|-------------------|----------|
| 1 小节 | 16 | 1 |
| 2 小节 | 32 | 2 |
| 4 小节 | 64 | 4 |
| 自定义 | 可变 | 灵活 |

### 分辨率

| 分辨率 | 网格划分 | 用途 |
|--------|----------|------|
| 1/4 | 四分音符 | 基本节拍 |
| 1/8 | 八分音符 | 标准摇滚 |
| 1/16 | 十六分音符 | 复杂模式 |
| 1/32 | 三十二分音符 | 详细编程 |

## 常见鼓模式

### 基本摇滚

```
Kick:      X---X---
Snare:     ----X---
Hi-Hat:    X-X-X-X-
```

### 基本爵士

```
Kick:      X---X---
Snare:     -X-X-X-X
Ride:      X-X-X-X-
```

### 基本嘻哈

```
Kick:      X-----X-
Snare:     ----X---
Hi-Hat:    X-X-X-X-
```

### 基本放克

```
Kick:      X--X--X-
Snare:     --X---X-
Hi-Hat:    X-X-X-X-
```

### 拉丁：Son Clave

```
Kick:      X---X---X-X---X-
Cowbell:   X---X---X-X---X-
```

## 混音器

### 混音器控制

| 控制 | 每乐器 | 描述 |
|------|--------|------|
| Volume | 是 | 输出电平（0-1.0） |
| Pan | 是 | 左右位置 |
| Mute | 是 | 静音乐器 |
| Solo | 是 | 隔离乐器 |
| FX Send | 是 | 效果路由 |

### 混音器路由

| 输出 | 目标 |
|------|------|
| Master | 主音频输出 |
| FX Send 1 | 效果总线 1 |
| FX Send 2 | 效果总线 2 |
| Individual | 独立输出（JACK） |

## 歌曲编排

### Song Editor 概览

Song Editor 将模式编排成完整歌曲：

| 元素 | 描述 |
|------|------|
| Pattern Blocks | 代表模式的彩色块 |
| Timeline | 块的水平排列 |
| Tracks | 每种模式类型的行 |
| Transport | 在编排中播放 |

### 构建歌曲结构

| 部分 | 模式 | 典型小节数 |
|------|------|-----------|
| 前奏 | Pattern 1 | 4-8 |
| 主歌 | Pattern 2 | 8-16 |
| 副歌 | Pattern 3 | 8-16 |
| 过渡 | Pattern 4 | 4-8 |
| 主歌 2 | Pattern 2 | 8-16 |
| 副歌 | Pattern 3 | 8-16 |
| 尾声 | Pattern 5 | 4-8 |

### 编辑歌曲

| 操作 | 方法 |
|------|------|
| 添加模式 | 在空网格区域点击 |
| 删除模式 | 右键点击并删除 |
| 复制模式 | 按住 Ctrl 拖动 |
| 移动模式 | 拖动到新位置 |
| 设置长度 | 拖动模式边缘 |

## 乐器包

### 加载乐器包

| 操作 | 步骤 |
|------|------|
| 加载乐器包 | Drumkits > Load |
| 保存乐器包 | Drumkits > Save As |
| 导入采样 | 拖放到乐器上 |
| 浏览乐器包 | Drumkits > System > Browse |

### 乐器包分类

| 分类 | 内容 | 用途 |
|------|------|------|
| Acoustic | 真实鼓录音 | 摇滚、爵士、流行 |
| Electronic | 合成鼓 | 电子、舞曲 |
| Percussion | 世界乐器 | 拉丁、世界音乐 |
| 808/909 | 经典机器声音 | 嘻哈、电子乐 |

## 效果

### 内置效果

| 效果 | 参数 | 用途 |
|------|------|------|
| Compressor | 阈值、比率、起音 | 动态控制 |
| Delay | 时间、反馈、混合 | 回声效果 |
| Reverb | 房间大小、阻尼 | 空间感和深度 |
| Distortion | 驱动、音色 | 粗犷声音 |
| EQ | 频段 | 音色塑造 |
| Filter | 截止、共振 | 频率操作 |

### 添加效果

1. 在混音器中选择乐器
2. 点击 FX 按钮
3. 从列表中添加所需效果
4. 调整参数
5. 设置干湿混合

## MIDI 集成

### MIDI 输入

| 设置 | 描述 |
|------|------|
| MIDI In | 接收 MIDI 音符 |
| Channel | MIDI 通道（1-16） |
| Map | 音符到乐器的映射 |

### MIDI 映射

| MIDI 音符 | 默认映射 |
|-----------|----------|
| C1 (36) | Kick |
| D1 (38) | Snare |
| F#1 (42) | Closed Hi-Hat |
| A#1 (46) | Open Hi-Hat |
| C#2 (49) | Crash |
| D#2 (51) | Ride |

### MIDI 导出

将模式导出为 MIDI 文件：

| 格式 | 用途 |
|------|------|
| SMF Type 0 | 单轨道 |
| SMF Type 1 | 多轨道 |

## 音频导出

### 导出选项

| 选项 | 格式 | 质量 |
|------|------|------|
| WAV | 无损 | 最佳质量 |
| FLAC | 无损压缩 | 良好质量，更小 |
| OGG | 有损 | 更小文件 |
| MP3 | 有损 | 通用兼容 |

### 导出设置

| 设置 | 推荐值 |
|------|--------|
| 采样率 | 44100 Hz（CD 质量） |
| 位深 | 16 位（标准）或 24 位（专业） |
| 声道 | 立体声或单声道 |

## 键盘快捷键

| 操作 | 快捷键 |
|------|--------|
| 播放/停止 | Space |
| 录制 | Ctrl+R |
| 新建模式 | Ctrl+N |
| 保存 | Ctrl+S |
| 撤销 | Ctrl+Z |
| 重做 | Ctrl+Y |
| 放大 | Ctrl++ |
| 缩小 | Ctrl+- |

## 更好鼓编程的技巧

| 技巧 | 描述 | 效果 |
|------|------|------|
| 力度变化 | 改变打击力度 | 人性化感觉 |
| 鬼音 | 非常轻柔的军鼓打击 | 律动深度 |
| Swing | 偏移弱拍音符 | 律动变化 |
| 开放踩镲变化 | 混合开放/闭合踩镲 | 节奏趣味 |
| 过门 | 段落结尾的嗵鼓模式 | 过渡 |
| 叠加 | 每次打击多个声音 | 更饱满的声音 |

## 总结

Hydrogen 提供了一个全面的鼓编程环境，适合初学者和有经验的音乐家。其基于模式的工作流、混音器功能和 MIDI 支持使其成为创建鼓轨道的多功能工具。

关键实践：

- 从基本模式开始，逐步增加复杂度
- 使用力度变化创建自然的律动
- 通过编排不同的主歌、副歌和过渡模式来组织歌曲
- 导出 MIDI 以便与数字音频工作站集成
- 探索不同的鼓乐器包以匹配您的音乐风格


---

## 来源：daw.md

## 简介

Ardour 是一款专业的开源数字音频工作站 (DAW)，用于录制、编辑、混音和母带处理音频。它提供专业音乐制作、播客编辑、声音设计和电影配乐所需的工具，无需商业替代品的高昂成本。

Ardour 运行在 Linux、macOS 和 Windows 上，是最易获得的专业 DAW 之一。

## 为什么使用 Ardour？

| 特性 | Ardour | Pro Tools | Logic Pro | Ableton |
|------|--------|-----------|-----------|---------|
| 费用 | 免费/随心付费 | $600+ | $200 | $450+ |
| 开源 | 是 | 否 | 否 | 否 |
| 无限轨道 | 是 | 受版本限制 | 是 | 是 |
| 插件支持 | VST, LV2, AU | AAX | AU | VST, AU |
| 平台 | Linux/Mac/Win | Mac/Win | 仅 Mac | Mac/Win |
| MIDI 支持 | 是 | 是 | 是 | 是 |

## 核心功能

| 功能 | 描述 |
|------|------|
| 多轨录制 | 录制无限音频轨道 |
| 非破坏性编辑 | 不修改原始文件进行编辑 |
| 混音台 | 带效果的完整混音器 |
| MIDI 编排 | 编写和编辑 MIDI |
| 自动化 | 自动化任何参数 |
| 插件托管 | VST、LV2、AU 插件支持 |
| 视频时间线 | 音频与视频同步 |
| 会话管理 | 保存和恢复会话 |

## 安装

### Linux

```bash
# Ubuntu/Debian
sudo apt install ardour

# Fedora
sudo dnf install ardour

# Arch
sudo pacman -S ardour

# Flatpak（推荐）
flatpak install flathub org.ardour.Ardour
```

### macOS

| 方式 | 命令 |
|------|------|
| 直接下载 | ardour.org/download |
| Homebrew | `brew install --cask ardour` |

### Windows

1. 从 ardour.org 下载安装程序
2. 以管理员身份运行安装程序
3. 按照安装向导操作

### 系统要求

| 要求 | 最低 | 推荐 |
|------|------|------|
| CPU | 双核 | 四核+ |
| 内存 | 4GB | 16GB+ |
| 存储 | 10GB | SSD 100GB+ |
| 音频接口 | 任何 | ASIO 兼容 |
| 采样率 | 44.1kHz | 48kHz 或 96kHz |

## 音频接口设置

### JACK Audio Connection Kit

Ardour 在 Linux 上使用 JACK 进行音频路由。

| 设置 | 描述 | 建议 |
|------|------|------|
| 缓冲大小 | 延迟 vs CPU | 128-512 采样 |
| 采样率 | 音频质量 | 44100 或 48000 |
| 周期 | 缓冲数量 | 2-3 |
| 实时 | 优先级调度 | 启用 |

### ALSA（替代方案）

用于不需要 JACK 的简单设置。

| 设置 | 值 |
|------|---|
| 设备 | 你的音频接口 |
| 采样率 | 44100 |
| 缓冲大小 | 256 |

### macOS/Windows

| 平台 | 音频系统 | 设置 |
|------|---------|------|
| macOS | CoreAudio | 自动检测 |
| Windows | ASIO | 如需要安装 ASIO4ALL |

## 会话管理

### 创建新会话

| 设置 | 描述 | 默认 |
|------|------|------|
| 会话名称 | 项目名称 | 未命名 |
| 文件夹 | 存储位置 | ~/Documents/ardour |
| 采样率 | 音频质量 | 48000 |
| 位深度 | 分辨率 | 32 位浮点 |

### 会话结构

| 组件 | 用途 |
|------|------|
| 会话文件夹 | 包含所有会话文件 |
| Interchange | 音频和 MIDI 文件 |
| 会话文件 | .ardour XML 文件 |
| 峰值文件 | 波形显示数据 |
| 备份文件 | 自动会话备份 |

## 录制

### 轨道设置

| 轨道类型 | 使用场景 | 配置 |
|---------|---------|------|
| 音频轨道 | 录制音频 | 单声道或立体声 |
| MIDI 轨道 | MIDI 乐器 | MIDI 通道 |
| 音频总线 | 路由 | 不录制 |
| MIDI 总线 | MIDI 路由 | 不录制 |

### 录制设置

| 设置 | 描述 | 建议 |
|------|------|------|
| 输入源 | 音频接口输入 | 选择正确输入 |
| 监听 | 录制时听到输入 | 自动或外部 |
| 录制模式 | 录制方式 | 非破坏性 |
| 穿入/穿出 | 自动开始/停止录制 | 设置标记 |

### 录制工作流

| 步骤 | 操作 |
|------|------|
| 1 | 创建音频轨道 |
| 2 | 设置输入源 |
| 3 | 为录制启用轨道 |
| 4 | 设置电平（避免削波） |
| 5 | 按录制 |
| 6 | 表演 |
| 7 | 按停止 |

## 编辑

### 编辑工具

| 工具 | 快捷键 | 用途 |
|------|-------|------|
| 选择 | `e` | 选择区域 |
| 范围 | `r` | 选择时间范围 |
| 剪切 | `c` | 分割区域 |
| 绘制 | `d` | 绘制 MIDI 音符 |
| 试听 | `a` | 听区域 |

### 区域操作

| 操作 | 快捷键 | 描述 |
|------|-------|------|
| 分割 | `S` | 在光标处分割 |
| 修剪 | 拖动边缘 | 调整区域长度 |
| 淡入/淡出 | 拖动角落 | 添加淡变 |
| 复制 | `D` | 复制区域 |
| 删除 | `Delete` | 移除区域 |
| 移动 | 拖动 | 重新定位区域 |

### 网格和对齐

| 设置 | 描述 |
|------|------|
| 网格 | 对齐到拍/小节边界 |
| 无网格 | 自由移动 |
| 磁性 | 接近时对齐 |
| 三连音 | 对齐到三连音细分 |

## 混音

### 混音台

| 控制 | 功能 |
|------|------|
| 推子 | 音量电平 |
| 声像 | 立体声位置 |
| 静音 | 静音轨道 |
| 独奏 | 仅听该轨道 |
| 录音启用 | 启用录制 |
| 插件槽 | 插入效果 |
| 发送 | 路由到总线 |

### 信号流

```
输入 → 轨道 → 插件 → 推子 → 声像 → 输出总线 → 主输出
```

### 总线路由

| 总线类型 | 用途 | 使用场景 |
|---------|------|---------|
| 辅助发送 | 并行处理 | 混响、延迟 |
| 编组总线 | 多轨道 | 鼓组总线、人声总线 |
| 主总线 | 最终输出 | 立体声混音 |

## 插件

### 支持格式

| 格式 | 平台 | 描述 |
|------|------|------|
| LV2 | Linux | 开放标准 |
| VST2/VST3 | 全部 | Steinberg 标准 |
| AU | macOS | Apple 标准 |
| LADSPA | Linux | 旧版 Linux 格式 |
| Lua | 全部 | 脚本插件 |

### 必备插件

| 插件类型 | 用途 | 示例 |
|---------|------|------|
| EQ | 频率塑形 | 参数式、图形 |
| 压缩器 | 动态控制 | VCA、光学、FET |
| 混响 | 空间模拟 | 板式、大厅、房间 |
| 延迟 | 回声效果 | 磁带、数字、乒乓 |
| 限幅器 | 峰值控制 | 砖墙限幅器 |
| 饱和 | 谐波染色 | 磁带、电子管 |

### 插件链顺序

| 位置 | 插件 | 用途 |
|------|------|------|
| 1 | EQ | 清理频率 |
| 2 | 压缩器 | 控制动态 |
| 3 | 齿音消除 | 减少齿音 |
| 4 | 饱和 | 添加温暖感 |
| 5 | 混响/延迟 | 添加空间感 |

## 自动化

### 自动化通道

| 参数 | 类型 | 描述 |
|------|------|------|
| 音量 | 连续 | 轨道电平随时间变化 |
| 声像 | 连续 | 立体声位置 |
| 插件参数 | 连续/离散 | 任何效果参数 |
| 静音 | 离散 | 开/关状态 |

### 自动化模式

| 模式 | 描述 |
|------|------|
| 读取 | 播放现有自动化 |
| 写入 | 录制新自动化 |
| 触摸 | 触摸控件时写入 |
| 锁定 | 触摸后持续写入 |

## MIDI

### MIDI 编辑

| 功能 | 描述 |
|------|------|
| 钢琴卷帘 | 音符编辑视图 |
| 力度 | 每个音符的音量 |
| 量化 | 对齐音符到网格 |
| 移调 | 改变音高 |
| 人性化 | 添加时间变化 |

### MIDI 乐器

| 类型 | 描述 |
|------|------|
| 合成器 | 从 MIDI 生成声音 |
| 采样器 | 回放音频采样 |
| 鼓机 | 基于模式的鼓 |

## 导出

### 导出设置

| 设置 | 选项 |
|------|------|
| 格式 | WAV, FLAC, MP3, OGG |
| 采样率 | 44100, 48000, 96000 |
| 位深度 | 16, 24, 32 |
| 声道 | 单声道, 立体声 |
| 标准化 | 峰值/RMS 标准化 |

### 导出预设

| 预设 | 格式 | 质量 |
|------|------|------|
| CD 品质 | WAV 44.1/16 | 无损 |
| 母带 | WAV 48/24 | 高品质 |
| 流媒体 | MP3 320kbps | 压缩 |
| 播客 | MP3 128kbps | 人声优化 |

## 键盘快捷键

| 操作 | 快捷键 |
|------|-------|
| 播放/停止 | 空格 |
| 录制 | R |
| 撤销 | Ctrl+Z |
| 重做 | Ctrl+Y |
| 保存 | Ctrl+S |
| 放大 | + |
| 缩小 | - |
| 添加轨道 | Ctrl+Shift+T |

## 故障排除

| 问题 | 原因 | 解决方案 |
|------|------|---------|
| 没有声音 | 输出错误 | 检查音频设置 |
| 高延迟 | 缓冲大小 | 减小缓冲大小 |
| 爆音/杂音 | CPU 过载 | 增加缓冲大小 |
| 插件崩溃 | 插件不兼容 | 移除插件 |
| JACK 错误 | 配置问题 | 重启 JACK |

## 更多资源

| 资源 | URL |
|------|-----|
| 官方网站 | ardour.org |
| 手册 | manual.ardour.org |
| 论坛 | ardour.org/forum |
| 教程 | ardour.org/tutorials |


---

## 来源：audio.md

## 简介

Audacity 是一款免费、开源的数字音频编辑器和录音应用。它提供专业级音频编辑工具，用于录制、编辑、混音和导出音频文件。Audacity 广泛用于播客、音乐制作、声音设计和音频修复。

Audacity 运行在 Windows、macOS 和 Linux 上，是最易获得的音频编辑工具之一。

## 为什么使用 Audacity？

| 特性 | Audacity | Adobe Audition | GarageBand |
|------|----------|---------------|------------|
| 费用 | 免费 | $20/月 | 免费（仅 Mac） |
| 开源 | 是 | 否 | 否 |
| 平台 | 全部 | Windows/Mac | 仅 Mac |
| 多轨 | 是 | 是 | 是 |
| 插件支持 | VST, LV2, Nyquist | VST, AU | AU |
| 学习曲线 | 低 | 中 | 低 |

## 核心功能

| 功能 | 描述 |
|------|------|
| 录制 | 从任何音频输入录制 |
| 编辑 | 剪切、复制、粘贴、删除 |
| 效果 | 降噪、EQ、压缩 |
| 多轨 | 混合多个音频轨道 |
| 分析 | 频谱图、频率分析 |
| 批处理 | 自动化重复任务 |
| 插件支持 | VST、LV2、Nyquist 插件 |
| 导出 | WAV, MP3, OGG, FLAC |

## 安装

### Windows

1. 从 audacityteam.org 下载
2. 运行安装程序
3. 按照安装向导操作
4. 启动 Audacity

### macOS

| 方式 | 命令 |
|------|------|
| 直接下载 | audacityteam.org |
| Homebrew | `brew install --cask audacity` |

### Linux

```bash
# Ubuntu/Debian
sudo apt install audacity

# Fedora
sudo dnf install audacity

# Flatpak
flatpak install flathub org.audacityteam.Audacity
```

### 系统要求

| 要求 | 最低 | 推荐 |
|------|------|------|
| CPU | 1GHz | 2GHz+ |
| 内存 | 2GB | 8GB |
| 存储 | 200MB | 1GB |
| 声卡 | 任何 | ASIO 兼容 |

## 界面概述

### 主要组件

| 组件 | 用途 |
|------|------|
| 工具栏 | 快速访问功能 |
| 轨道面板 | 轨道控制和信息 |
| 时间线 | 音频波形显示 |
| 混音器 | 音量和声像控制 |
| 电平表 | 输入/输出电平 |

### 工具栏概述

| 工具栏 | 功能 |
|-------|------|
| 传输 | 播放、停止、录制 |
| 工具 | 选择、包络、绘制 |
| 电平表 | 电平监测 |
| 混音器 | 音量控制 |
| 编辑 | 剪切、复制、粘贴 |
| 转录 | 播放速度 |

## 录制

### 音频设置

| 设置 | 描述 | 建议 |
|------|------|------|
| 宿主 | 音频 API | WASAPI (Windows), CoreAudio (Mac) |
| 录制设备 | 输入源 | 你的麦克风 |
| 播放设备 | 输出源 | 你的扬声器/耳机 |
| 声道 | 单声道/立体声 | 人声用单声道，音乐用立体声 |
| 采样率 | 音频质量 | 44100Hz 或 48000Hz |

### 录制工作流

| 步骤 | 操作 |
|------|------|
| 1 | 选择输入设备 |
| 2 | 设置录制电平 |
| 3 | 点击录制按钮 |
| 4 | 说话或演奏 |
| 5 | 完成后点击停止 |
| 6 | 检查录制 |

### 录制技巧

| 技巧 | 用途 |
|------|------|
| 监测电平 | 避免削波（红色） |
| 使用耳机 | 防止反馈 |
| 在安静空间录制 | 减少背景噪音 |
| 经常保存 | 防止数据丢失 |

## 编辑

### 选择工具

| 工具 | 快捷键 | 用途 |
|------|-------|------|
| 选择 | F1 | 选择时间范围 |
| 包络 | F2 | 随时间调整音量 |
| 绘制 | F3 | 直接编辑波形 |
| 缩放 | F4 | 放大/缩小 |
| 时间偏移 | F5 | 在时间上移动轨道 |
| 多工具 | F6 | 上下文敏感 |

### 基本编辑操作

| 操作 | 快捷键 | 描述 |
|------|-------|------|
| 剪切 | Ctrl+X | 移除并复制选择 |
| 复制 | Ctrl+C | 复制选择 |
| 粘贴 | Ctrl+V | 从剪贴板粘贴 |
| 删除 | Delete | 移除选择 |
| 撤销 | Ctrl+Z | 撤销上一操作 |
| 重做 | Ctrl+Y | 重做已撤销操作 |
| 全选 | Ctrl+A | 选择整个轨道 |
| 裁剪 | Ctrl+T | 仅保留选择 |

### 高级编辑

| 操作 | 描述 |
|------|------|
| 分割 | 在光标处分割轨道 |
| 合并 | 合并选定片段 |
| 复制 | 将选择复制到新轨道 |
| 标签轨道 | 添加标记和标签 |
| 同步锁定 | 保持轨道同步 |

## 效果

### 内置效果

| 效果 | 类别 | 使用场景 |
|------|------|---------|
| 增益 | 音量 | 调整音量 |
| 低音和高音 | EQ | 频率调整 |
| 压缩器 | 动态 | 减少动态范围 |
| 回声 | 时间 | 添加重复 |
| 均衡 | EQ | 塑形频率响应 |
| 淡入/淡出 | 音量 | 平滑过渡 |
| 降噪 | 修复 | 移除背景噪音 |
| 标准化 | 音量 | 标准化电平 |
| 混响 | 空间 | 添加房间氛围 |
| 截断静音 | 时间 | 移除安静部分 |

### 降噪工作流

| 步骤 | 操作 |
|------|------|
| 1 | 选择仅有噪音的区域 |
| 2 | 效果 > 降噪 > 获取噪音配置 |
| 3 | 选择整个轨道 |
| 4 | 效果 > 降噪 > 确定 |
| 5 | 如需要调整设置 |

### 效果设置

| 设置 | 描述 |
|------|------|
| 预览 | 应用前试听 |
| 设置 | 调整参数 |
| 管理 | 保存/加载预设 |
| 撤销 | 反转效果应用 |

## 多轨混音

### 轨道操作

| 操作 | 描述 |
|------|------|
| 添加轨道 | 轨道 > 添加新轨道 |
| 复制轨道 | 轨道 > 复制 |
| 删除轨道 | 轨道 > 移除轨道 |
| 静音 | 独奏或静音轨道 |
| 声像 | 调整立体声位置 |
| 音量 | 设置轨道电平 |

### 混音工作流

| 步骤 | 操作 |
|------|------|
| 1 | 导入或录制所有轨道 |
| 2 | 使用时间偏移对齐轨道 |
| 3 | 设置各轨道音量 |
| 4 | 调整声像 |
| 5 | 为每个轨道应用效果 |
| 6 | 导出最终混音 |

## 频谱图视图

### 切换视图

| 视图 | 描述 | 使用场景 |
|------|------|---------|
| 波形 | 振幅随时间 | 通用编辑 |
| 频谱图 | 频率随时间 | 噪音识别 |

### 频谱分析

| 颜色 | 含义 |
|------|------|
| 蓝/黑 | 低能量 |
| 绿色 | 中等能量 |
| 黄色 | 高能量 |
| 红色 | 极高能量 |

## 导出和格式

### 导出选项

| 格式 | 质量 | 文件大小 | 使用场景 |
|------|------|---------|---------|
| WAV | 无损 | 大 | 母带文件 |
| MP3 | 有损 | 小 | 分发 |
| OGG | 有损 | 小 | Web 音频 |
| FLAC | 无损 | 中 | 归档 |
| M4A | 有损 | 小 | Apple 设备 |

### 导出设置

| 设置 | 描述 | 建议 |
|------|------|------|
| 比特率 | MP3 质量 | 192kbps 或更高 |
| 采样率 | 音频质量 | 44100Hz |
| 声道 | 单声道/立体声 | 基于内容 |
| 质量 | OGG 质量 | 10 分中的 5-7 分 |

### 元数据

| 字段 | 描述 |
|------|------|
| 标题 | 曲目名称 |
| 艺术家 | 表演者名称 |
| 专辑 | 专辑名称 |
| 年份 | 发行年份 |
| 流派 | 音乐类型 |
| 评论 | 附加信息 |

## 键盘快捷键

| 操作 | 快捷键 |
|------|-------|
| 播放/停止 | 空格 |
| 录制 | R |
| 暂停 | P |
| 跳到开头 | Home |
| 跳到结尾 | End |
| 放大 | Ctrl+1 |
| 缩小 | Ctrl+3 |
| 适应窗口 | Ctrl+F |

## 插件

### 支持格式

| 格式 | 平台 | 描述 |
|------|------|------|
| VST2/VST3 | 全部 | Steinberg 标准 |
| LV2 | Linux | 开放标准 |
| Nyquist | 全部 | 内置脚本 |
| LADSPA | Linux | 旧版 Linux 格式 |

### 安装插件

| 步骤 | 操作 |
|------|------|
| 1 | 下载插件文件 |
| 2 | 放入 Audacity 插件文件夹 |
| 3 | 效果 > 添加/移除插件 |
| 4 | 启用新插件 |
| 5 | 重启 Audacity |

## 故障排除

| 问题 | 原因 | 解决方案 |
|------|------|---------|
| 没有声音 | 输出设备错误 | 检查音频偏好 |
| 削波 | 输入太大 | 降低录制电平 |
| 回声 | 监听已启用 | 禁用软件播放 |
| 崩溃 | 偏好损坏 | 重置偏好 |
| 效果缺失 | 插件未启用 | 在插件管理器中启用 |

## 更多资源

| 资源 | URL |
|------|-----|
| 官方网站 | audacityteam.org |
| 手册 | manual.audacityteam.org |
| 论坛 | forum.audacityteam.org |
| 教程 | audacityteam.org/tutorials |


---

## 来源：music.md

## 简介

LMMS（Linux MultiMedia Studio）是一款免费、开源的数字音频工作站（DAW），用于音乐制作。它允许用户通过创作旋律、混合音轨和应用效果来创建音乐。

| 属性 | 详情 |
|----------|--------|
| 仓库 | LMMS/lmms |
| 许可证 | GPL-2.0 |
| 语言 | C++, Qt |
| 平台 | Windows, macOS, Linux |
| 文件格式 | .mmp（原生）, .mmpz（压缩） |

## 安装

### Linux

```bash
# Ubuntu/Debian
sudo apt install lmms

# Fedora
sudo dnf install lmms

# Flatpak
flatpak install io.lmms.LMMS
```

### macOS 和 Windows

从 LMMS 官方网站下载。

## 界面概览

| 窗口 | 描述 |
|--------|-------------|
| Song Editor（歌曲编辑器） | 在时间线上排列模式和音轨 |
| Beat+Bassline Editor（节拍+贝斯编辑器） | 创建鼓模式和贝斯循环 |
| Piano Roll（钢琴卷帘） | 编辑旋律和音符序列 |
| Mixer（混音器） | 调整音量、声像和效果 |
| Instrument Plugins（乐器插件） | 配置合成器和采样器 |
| Effects Rack（效果架） | 为音轨添加音频效果 |

## 核心概念

| 概念 | 描述 |
|---------|-------------|
| Track（音轨） | 单个乐器或音频通道 |
| Pattern（模式） | 乐句或循环 |
| Song（歌曲） | 排列好的模式集合 |
| Instrument（乐器） | 声音生成器（合成器或采样器） |
| Effect（效果） | 音频处理（混响、延迟、EQ） |
| Automation（自动化） | 随时间编排的参数变化 |

## 歌曲编辑器

歌曲编辑器是排列音乐的主要工作区。

| 功能 | 描述 |
|---------|-------------|
| Track List（音轨列表） | 所有乐器和模式音轨的列表 |
| Timeline（时间线） | 排列的水平视图 |
| Pattern Blocks（模式块） | 代表模式的可视化块 |
| Playhead（播放头） | 当前播放位置 |
| Loop Region（循环区域） | 定义要循环的部分 |

### 添加音轨

1. 在音轨列表中点击 "+" 按钮。
2. 选择乐器音轨或自动化音轨。
3. 选择乐器插件。

## 钢琴卷帘

钢琴卷帘用于编辑旋律和和弦进行。

| 工具 | 快捷键 | 描述 |
|------|----------|-------------|
| Draw（绘制） | D | 放置音符 |
| Erase（擦除） | E | 移除音符 |
| Select（选择） | S | 选择音符进行编辑 |
| Move（移动） | M | 移动选中的音符 |

### 音符编辑

| 操作 | 描述 |
|--------|-------------|
| 点击 | 放置音符 |
| 拖动 | 调整音符长度 |
| 右键点击 | 删除音符 |
| Ctrl+点击 | 添加到选区 |
| 方向键 | 移动选中的音符 |

## 节拍+贝斯编辑器

此编辑器专为创建鼓模式和重复贝斯线设计。

| 功能 | 描述 |
|---------|-------------|
| Step Sequencer（步进音序器） | 点击切换节拍开关 |
| Pattern Length（模式长度） | 设置步数 |
| Instrument Slots（乐器槽） | 为每行分配乐器 |
| Mute/Solo（静音/独奏） | 启用或禁用单个乐器 |

### 常见鼓模式

| 模式 | 步数 |
|---------|-------|
| Four on Floor | 每拍都有底鼓 |
| Basic Rock | 底鼓在 1,3；军鼓在 2,4 |
| Hip-Hop | 底鼓在 1,3；军鼓在 2,4；踩镲在每个 8 分音符 |
| Breakbeat | 切分的底鼓和军鼓 |

## 内置乐器

### 合成器

| 乐器 | 类型 | 描述 |
|------------|------|-------------|
| Triple Oscillator | 减法 | 三个带滤波器的振荡器 |
| ZynAddSubFX | 加法/减法 | 强大的开源合成器 |
| Organic | 加法 | 类风琴声音 |
| Mallets | 物理建模 | 打击乐器 |
| Bit Invader | 波表 | 数字波表合成器 |
| SID | 芯片 | Commodore SID 模拟器 |
| Vibed | 物理建模 | 弦乐器 |

### 采样器

| 乐器 | 描述 |
|------------|-------------|
| AudioFile Processor | 加载和播放音频采样 |
| SF2 Player | 播放 SoundFont 文件 |
| Slicer | 切割和重新排列音频 |

## 混音器

混音器控制每个音轨的音量和效果。

| 功能 | 描述 |
|---------|-------------|
| Channel Strips（通道条） | 每个通道的音量、声像和静音 |
| Effects Slots（效果槽） | 在每个通道上插入效果 |
| Sends（发送） | 将音频路由到辅助通道 |
| Master（主输出） | 带主效果的最终输出 |

### 常见效果

| 效果 | 描述 |
|--------|-------------|
| Reverb（混响） | 模拟房间声学 |
| Delay（延迟） | 回声和重复效果 |
| EQ（均衡器） | 调整频率平衡 |
| Compressor（压缩器） | 控制动态范围 |
| Distortion（失真） | 添加谐波饱和 |
| Chorus（合唱） | 用失谐副本加厚声音 |
| Flanger（镶边） | 扫频梳状滤波器效果 |
| Phaser（相移） | 扫频陷波滤波器效果 |
| Limiter（限制器） | 防止削波 |

## 自动化

自动化允许参数随时间变化。

### 创建自动化

1. 右键点击参数。
2. 选择 "Create Automation"。
3. 在自动化轨道中绘制自动化曲线。

### 自动化点

| 操作 | 描述 |
|--------|-------------|
| 点击 | 添加点 |
| 拖动 | 移动点 |
| 右键点击 | 删除点 |

## 内置效果

| 效果 | 类别 | 描述 |
|--------|----------|-------------|
| Calf Reverb | 混响 | 房间模拟 |
| Calf Delay | 延迟 | 回声效果 |
| Calf Equalizer | EQ | 5 频段参数均衡器 |
| Calf Compressor | 动态 | 压缩 |
| Calf Limiter | 动态 | 峰值限制 |
| Calf Phaser | 调制 | 相移 |
| Calf Flanger | 调制 | 镶边效果 |
| Calf Chorus | 调制 | 合唱效果 |
| Calf Exciter | 增强 | 谐波增强 |
| Calf Stereo Spread | 立体声 | 立体声宽度控制 |

## VST 插件支持

LMMS 通过兼容层支持 VST2 插件。

| 步骤 | 描述 |
|------|-------------|
| 1 | 安装 Wine（Linux）或使用原生（Windows） |
| 2 | 将 VST DLL 放入插件目录 |
| 3 | 将 VeSTige 乐器添加到音轨 |
| 4 | 加载 VST 插件 |

## 项目结构

| 元素 | 描述 |
|---------|-------------|
| Tracks（音轨） | 单个乐器或自动化通道 |
| Patterns（模式） | 分配给音轨的乐句 |
| Song Arrangement（歌曲排列） | 模式的顺序和时间 |
| Mixer Settings（混音器设置） | 音量、效果、路由 |
| Instruments（乐器） | 插件配置 |

## 文件格式

| 格式 | 描述 |
|--------|-------------|
| .mmp | LMMS 项目（基于 XML） |
| .mmpz | LMMS 项目（压缩） |
| .wav | 导出的音频（未压缩） |
| .ogg | 导出的音频（压缩） |
| .mid | MIDI 导入/导出 |
| .sf2 | SoundFont 文件 |
| .wav | 采样文件 |

## 音乐制作技巧

| 技巧 | 说明 |
|-----|-------------|
| 从鼓模式开始 | 先构建节奏部分 |
| 使用模板 | 保存项目模板以便重用 |
| 叠加乐器 | 组合多种声音以增加丰富度 |
| 使用自动化 | 添加运动和动态 |
| 低音量混音 | 防止听觉疲劳并改善混音 |
| 经常保存 | LMMS 在复杂项目上可能崩溃 |
| 学习键盘快捷键 | 加快工作流程 |

## 导出

| 设置 | 描述 |
|---------|-------------|
| Format（格式） | WAV, OGG 或 MP3 |
| Quality（质量） | 采样率和位深度 |
| Range（范围） | 导出整首歌曲或选区 |
| Tracks（音轨） | 导出单独音轨或混音 |

## 结论

LMMS 是一款功能强大的音乐制作工具，免费提供合成器、采样器、效果和编曲功能。它是初学者学习音乐制作的绝佳起点，也是经验丰富的音乐人的实用工具。


---

## 来源：tenacity.md

## 简介

Tenacity 是一款免费、开源的音频编辑器，用于录制和编辑声音。它是 Audacity 的一个分支，具有改进的功能和社区治理。本教程涵盖录音、编辑、效果和导出音频。

## 系统要求

| 组件 | 最低要求 | 推荐配置 |
|------|---------|---------|
| 操作系统 | Windows 8+、macOS 10.13+、Linux | 最新稳定版 |
| 内存 | 2 GB | 4 GB 或更多 |
| 磁盘空间 | 200 MB | 1 GB（大型项目） |
| CPU | 双核 | 四核或更高 |
| 音频 | 任何 ASIO/WASAPI/CoreAudio 设备 | 专用音频接口 |

## 安装

| 平台 | 方法 |
|------|------|
| Windows | 从 releases 下载安装程序 |
| macOS | 从 releases 下载 DMG |
| Ubuntu/Debian | 从源码构建或使用 PPA |
| Flatpak | flatpak install flathub org.tenacityaudio.Tenacity |
| 源码 | 克隆仓库，使用 CMake 构建 |

## 用户界面

| 组件 | 位置 | 用途 |
|------|------|------|
| 轨道面板 | 每个轨道左侧 | 静音、独奏、增益控制 |
| 波形显示 | 中央 | 可视化音频表示 |
| 时间轴 | 顶部 | 带标记的时间标尺 |
| 传输工具栏 | 顶部 | 播放、录制、停止按钮 |
| 工具工具栏 | 左上 | 选择、包络、绘制工具 |
| 混音器工具栏 | 右上 | 输入/输出音量表 |
| 编辑工具栏 | 传输栏下方 | 剪切、复制、粘贴、撤销 |

## 音频格式

| 格式 | 扩展名 | 用例 |
|------|--------|------|
| WAV | .wav | 未压缩，高质量 |
| MP3 | .mp3 | 压缩，通用支持 |
| FLAC | .lossless | 无损压缩 |
| OGG Vorbis | .ogg | 开源压缩格式 |
| Opus | .opus | 现代压缩格式，低延迟 |
| AIFF | .aiff | Apple 未压缩格式 |

## 录制音频

### 设置

| 步骤 | 操作 |
|------|------|
| 1 | 从下拉菜单选择输入设备 |
| 2 | 设置采样率（44100 Hz 为 CD 品质） |
| 3 | 选择单声道或立体声 |
| 4 | 使用电平表测试输入 |
| 5 | 调整输入增益以避免削波 |

### 录制控制

| 按钮 | 快捷键 | 操作 |
|------|--------|------|
| 录制 | R | 开始录制 |
| 暂停 | P | 暂停录制 |
| 停止 | 空格 | 停止录制 |
| 播放 | 空格 | 从光标处播放 |

### 录制设置

| 设置 | 选项 | 建议 |
|------|------|------|
| 采样率 | 8000 - 192000 Hz | 44100 Hz（CD）或 48000 Hz（视频） |
| 位深度 | 16-bit、24-bit、32-bit float | 录制用 24-bit |
| 声道 | 单声道、立体声 | 语音用单声道，音乐用立体声 |

## 编辑基础

### 选择工具

| 工具 | 快捷键 | 功能 |
|------|--------|------|
| Selection（选择） | I | 选择时间范围 |
| Envelope（包络） | J | 调整音量包络 |
| Draw（绘制） | D | 绘制波形点 |
| Zoom（缩放） | Z | 放大/缩小 |
| Time Shift（时间偏移） | T | 移动轨道时间 |
| Multi-tool（多工具） | M | 所有工具组合 |

### 常用编辑

| 编辑 | 快捷键 | 描述 |
|------|--------|------|
| 剪切 | Ctrl+X | 移除并复制选区 |
| 复制 | Ctrl+C | 复制选区到剪贴板 |
| 粘贴 | Ctrl+V | 从剪贴板插入 |
| 删除 | Del | 移除选区但不复制 |
| 撤销 | Ctrl+Z | 撤销上一步操作 |
| 重做 | Ctrl+Y | 重做已撤销的操作 |
| 全选 | Ctrl+A | 选择整个轨道 |
| 分割 | Ctrl+I | 在光标处分割片段 |

### 片段管理

| 操作 | 方法 |
|------|------|
| 移动片段 | Time Shift 工具，拖动片段 |
| 分割片段 | 放置光标，Edit > Clip Boundaries > Split |
| 合并片段 | 跨片段选择，Edit > Clip Boundaries > Join |
| 复制 | 选择后按 Ctrl+D |

## 轨道

### 轨道类型

| 类型 | 颜色 | 用途 |
|------|------|------|
| 波形 | 蓝/绿 | 标准音频 |
| 频谱图 | 热力图 | 频率分析 |
| 标签 | 标记 | 标注时间点 |

### 轨道操作

| 操作 | 菜单 | 快捷键 |
|------|------|--------|
| 添加新轨道 | Tracks > Add New | Ctrl+Shift+N |
| 删除轨道 | Tracks > Remove | （无默认） |
| 复制轨道 | Tracks > Duplicate | Ctrl+D |
| 分割立体声 | Tracks > Split Stereo | （无默认） |
| 立体声转单声道 | Tracks > Mix > Stereo to Mono | （无默认） |

## 效果

### 内置效果

| 效果 | 用途 | 关键参数 |
|------|------|---------|
| Amplify（放大） | 更改音量 | 量（dB）、削波 |
| Compressor（压缩器） | 减小动态范围 | 阈值、比率、起始时间 |
| Equalization（均衡） | 调整频率平衡 | 曲线或图形均衡 |
| Noise Reduction（降噪） | 去除背景噪声 | 噪声轮廓、灵敏度 |
| Reverb（混响） | 添加房间氛围 | 房间大小、阻尼、干湿比 |
| Echo（回声） | 添加延迟重复 | 延迟时间、衰减系数 |
| Fade In（渐入） | 音量逐渐增大 | 持续时间 |
| Fade Out（渐出） | 音量逐渐减小 | 持续时间 |
| Normalize（标准化） | 标准化峰值电平 | 目标峰值 dB |
| Truncate Silence（截断静音） | 移除静音部分 | 阈值、最短持续时间 |
| Change Pitch（变调） | 不改变速度的音调偏移 | 半音或频率 |
| Change Speed（变速） | 改变播放速度 | 速度因子 |
| Change Tempo（变节拍） | 不改变音调的速度变化 | 百分比 |

### 降噪工作流程

| 步骤 | 操作 |
|------|------|
| 1 | 选择一段纯噪声（无语音/音乐） |
| 2 | 进入 Effects > Noise Reduction > Get Noise Profile |
| 3 | 选择整个轨道 |
| 4 | 进入 Effects > Noise Reduction > OK |
| 5 | 如果出现伪影，调整灵敏度 |

## 标签和标记

| 标签类型 | 用例 |
|----------|------|
| 点标签 | 标记单个时刻 |
| 区域标签 | 标记时间范围 |

### 标签操作

| 操作 | 快捷键 |
|------|--------|
| 在光标处添加标签 | Ctrl+B |
| 为选区添加标签 | Ctrl+B（有选区时） |
| 编辑标签文本 | 点击标签，输入 |
| 导出标签 | File > Export > Export Labels |

## 音频分析

| 分析工具 | 用途 |
|----------|------|
| Plot Spectrum | 频率内容可视化 |
| Contrast | 比较两个选区的响度 |
| Find Clipping | 检测失真样本 |
| Measure RMS | 平均响度电平 |
| Sound Finder | 在静音中检测音频 |

## 导出

### 导出选项

| 格式 | 质量设置 |
|------|---------|
| WAV | 16-bit、24-bit、32-bit float |
| MP3 | 比特率：128-320 kbps，VBR 或 CBR |
| FLAC | 压缩级别 0-8 |
| OGG | 质量 0-10 |

### 导出命令

| 命令 | 快捷键 | 范围 |
|------|--------|------|
| Export Audio | Ctrl+Shift+E | 整个项目 |
| Export Selection | （通过对话框） | 仅选区 |
| Export Multiple | （通过菜单） | 按标签或轨道分割 |

## 快捷键参考

| 类别 | 快捷键 | 操作 |
|------|--------|------|
| 传输 | 空格 | 播放/停止 |
| 传输 | R | 录制 |
| 传输 | Shift+空格 | 循环播放 |
| 编辑 | Ctrl+Z | 撤销 |
| 编辑 | Ctrl+Y | 重做 |
| 编辑 | Ctrl+X | 剪切 |
| 编辑 | Ctrl+C | 复制 |
| 编辑 | Ctrl+V | 粘贴 |
| 视图 | Ctrl+1 | 放大 |
| 视图 | Ctrl+2 | 缩小 |
| 视图 | Ctrl+3 | 缩放至适合 |
| 视图 | Ctrl+F | 适合窗口 |

## 插件

| 插件格式 | 平台 | 示例 |
|----------|------|------|
| LADSPA | Linux、跨平台 | TAP、SWH 插件 |
| VST/VST3 | Windows、macOS、Linux | 第三方效果 |
| Nyquist | 跨平台 | 内置脚本 |
| LV2 | Linux、跨平台 | 现代插件标准 |

## 总结

Tenacity 提供了一个全面的音频编辑环境，适用于播客制作、音乐编辑和声音设计。其非破坏性工作流程、广泛的格式支持和丰富的效果库，使其成为初学者和经验丰富的音频编辑者都能胜任的工具。


---
