# 音乐制作资源大全

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
