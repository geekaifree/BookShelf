# Awesome Biomechanics

**来源：** https://github.com/modenaxe/awesome-biomechanics

＃＃ 概述

本教程涵盖了 [modenaxe/awesome-biomechanics](https://github.com/modenaxe/awesome-biomechanics) 项目中的关键资源和工具。

## 仍在进行中（可能包括不完整的描述），但在任何阶段都欢迎贡献！ :心眼:

请参阅[如何贡献](#contributing)，这很简单！

＃＃ 目录

- [Learning](#learning)
  - [Online Courses :clapper:](#online-courses-clapper)
  - [YouTube Channels :tv: ](#youtube-channels-tv-)
    - [Researchers](#researchers)
  - [Videos 🎥](#videos-)
  - [Learning to Code :construction:](#learning-to-code-construction)
    - [Python](#python)
    - [Julia](#julia)
    - [Git (source version control)](#git-source-version-control)
  - [Teaching Resources :triangular\_ruler:](#teaching-resources-triangular_ruler)
  - [Books :blue\_book:](#books-blue_book)
- [Datasets 📀](#datasets-)
  - [Human Anatomy :bone:](#human-anatomy-bone)
    - [Full Body](#full-body)
    - [Lower Limb Anatomy](#lower-limb-anatomy)
    - [Upper Extremity and Spine](#upper-extremity-and-spine)
    - [Muscle Anatomy and Parameters](#muscle-anatomy-and-parameters)
  - [Animal Anatomy and Anthropology :crocodile:](#animal-anatomy-and-anthropology-crocodile)
  - [Balance :balance\_scale:](#balance-balance_scale)
  - [Energetics :fire:](#energetics-fire)
  - [Walking :walking:](#walking-walking)
  - [Running :running:](#running-running)
  - [Instrumented Prostheses :chart\_with\_upwards\_trend:](#instrumented-prostheses-chart_with_upwards_trend)
  - [Upper Limb Movements 💪](#upper-limb-movements-)
  - [Hand :palms\_up\_together:](#hand-palms_up_together)
  - [Soft Tissue Artefacts :leg:](#soft-tissue-artefacts-leg)
  - [Reference Joint Kinematics](#reference-joint-kinematics)
  - [Health Datasets :heart:](#health-datasets-heart)
  - [Rugby :rugby\_football:](#rugby-rugby_football)
  - [EMG 🔌💪](#emg-)
- [Gait Analysis and Motion Capture :cartwheeling:](#gait-analysis-and-motion-capture-cartwheeling)
  - [Gait Analysis Markersets :globe\_with\_meridians:](#gait-analysis-markersets-globe_with_meridians)
  - [Motion Capture Data Import and Processing](#motion-capture-data-import-and-processing)
    - [Marker Trajectory Gap filling](#marker-trajectory-gap-filling)
    - [Inertial Measurement Units](#inertial-measurement-units)
    - [2D video analysis](#2d-video-analysis)
    - [3D video analysis](#3d-video-analysis)
  - [Videoradiography (Model-based and Marker-based Tracking)](#videoradiography-model-based-and-marker-based-tracking)
- [Tracking in Ultrasound Video Frames](#tracking-in-ultrasound-video-frames)
  - [Fascicle Tracking](#fascicle-tracking)
  - [Muscle-Tendon Junction Tracking](#muscle-tendon-junction-tracking)
- [Muscle Parameter Segmentation in Ultrasound Images](#muscle-parameter-segmentation-in-ultrasound-images)
  - [Anatomical Cross Sectional Area](#anatomical-cross-sectional-area)
- [Modelling and Simulation 💻](#modelling-and-simulation-)
  - [Anthropometric Models :standing\_person:](#anthropometric-models-standing_person)
  - [Multibody and Physics Engines :sleeping::arrow\_lower\_left::apple:](#multibody-and-physics-engines-sleepingarrow_lower_leftapple)
  - [Computational Muscle Models 	:mechanical\_arm:](#computational-muscle-models-mechanical_arm)
  - [Biomechanical and Neuro-musculoskeletal Simulation Software :brain::arrow\_right::leg:](#biomechanical-and-neuro-musculoskeletal-simulation-software-brainarrow_rightleg)
  - [Real-Time Neuro-musculoskeletal Simulation Software](#real-time-neuro-musculoskeletal-simulation-software)
  - [Neuro-musculoskeletal Simulation Tools :brain::hammer:](#neuro-musculoskeletal-simulation-tools-brainhammer)
  - [Biomechanical Models](#biomechanical-models)
- [Optimal Control and Trajectory Optimization :rocket:](#optimal-control-and-trajectory-optimization-rocket)
- [Subject-Specific Modelling](#subject-specific-modelling)
  - [Segmentation of Medical Images :artist:](#segmentation-of-medical-images-artist)
  - [Automatic Segmentation :mage\_man:](#automatic-segmentation-mage_man)
  - [Manipulation, Processing and Comparison of Surface Meshes](#manipulation-processing-and-comparison-of-surface-meshes)
  - [Resources for Building Biomechanical Models from Medical Images :woman\_technologist:](#resources-for-building-biomechanical-models-from-medical-images-woman_technologist)
  - [Automatic Definition of Bony Landmarks and Reference Systems :skull:](#automatic-definition-of-bony-landmarks-and-reference-systems-skull)
  - [Uncertainty Quantification in Musculoskeletal Simulations :question:](#uncertainty-quantification-in-musculoskeletal-simulations-question)
  - [Volumetric Meshers of Surface Models](#volumetric-meshers-of-surface-models)
    - [Tetrahedral meshers](#tetrahedral-meshers)
    - [Hexahedral meshers](#hexahedral-meshers)
    - [Commercial meshers](#commercial-meshers)
  - [Statistical Shape Modelling :bone:](#statistical-shape-modelling-bone)
    - [Tools](#tools)
    - [Shape Models](#shape-models)
- [Finite Element Analysis](#finite-element-analysis)
  - [Finite Element Analysis Software](#finite-element-analysis-software)
  - [Finite Element Libraries](#finite-element-libraries)
  - [Finite Element Analysis Software Tools](#finite-element-analysis-software-tools)
  - [Finite Element Models](#finite-element-models)
- [Statistical Analysis](#statistical-analysis)
- [Scientific Data Visualization](#scientific-data-visualization)
- [Reproducibility :gem:](#reproducibility-gem)
- [Good practices for credible modeling](#good-practices-for-credible-modeling)
- [Societies and Initiatives :classical\_building:](#societies-and-initiatives-classical_building)
- [Miscellaneous Online Resources](#miscellaneous-online-resources)
  - [Blogging platforms](#blogging-platforms)
- [More Datasets and repositories](#more-datasets-and-repositories)
- [Contributing](#contributing)
  - [How to contribute](#how-to-contribute)
  - [Resources for learning how to contribute](#resources-for-learning-how-to-contribute)
  - [Items suggested template](#items-suggested-template)
- [License](#license)

----

## 在线课程 :clapper:

- [动物运动讲座](https://mchenrylab.bio.uci.edu/e139)，作者：曼尼·阿齐兹 (Manny Azizi) 和马特·麦克亨利 (Matt McHenry)，加州大学欧文分校 (2020)。
- [Jason Moore](https://www.moorepants.info/) 在加州大学戴维斯分校的[多体动力学讲座](https://www.youtube.com/watch?v=1Tyxgv7RUdk&list=PLzAwokZEM7auZEBOJKNa_lCgz2rdgpYLL) (2017)。
- [KNES 789W - 运动学高级项目；人体运动建模与仿真](https://www.youtube.com/watch?v=JXz5BHQBJhk&list=PLFNfmB3IG2Cf_0V5N9w_ZBKIHD2xg1H_g) 作者：Ross Miller，马里兰大学 (2020)。
- [神经科学数学工具（哈佛大学的 Neurobio 212）](https://github.com/ebatty/MathToolsforNeuroscience)，作者：Ella Batty 等人。 （2021）。
- [机械系统设计](https://biomechatronics.stanford.edu/mechanical-systems-design)，作者：Steve Collins（斯坦福大学生物机电实验室）。初级课程，培养以下方面的经验和信心： 1. 一种机械系统设计方法，其中包含构思、粗略分析、计算分析和原型设计，迭代并在领域中保持适当的平衡。 2. 设计定制机械部件，查找和选择通用机器元件，并选择电动机和传动元件，以满足性能、效率和可靠性目标。描述这些材料的 Twitter 可以在[此处](https://twitter.com/StevenHCollins/status/1401204277373067266)获得。
- [神经力学课程材料](https://github.com/joshcash9/Neuromechanics_Course) 作者：[Joshua Cashaback](https://github.com/joshcash9)（特拉华大学）。
- [带有生物医学工程示例的研究生水平统计学课程](https://github.com/joshcash9/Statistics_BME)，作者：[Joshua Cashaback](https://github.com/joshcash9)（特拉华大学）。
- [Neuromatch Academy](https://www.youtube.com/channel/UC4LoD4yNBuLKQwDOV6t-KPw)：[Neuromatch Academy](https://www.neuromatchacademy.org/) 旨在向学员介绍计算神经科学的传统和新兴工具。
- [机器人 101：计算线性代数](https://robotics.umich.edu/2020/now-available-robotics-101-online/)，密歇根大学机器人研究所（2020 年秋季）。该课程包括[讲座视频](https://www.youtube.com/playlist?list=PLdPQZLMHRjDK8ZbLIcq1Q2PQobIi68dpv)和[GitHub资源](https://github.com/michiganrobotics/rob101)，包括[讲座笔记](https://github.com/michiganrobotics/rob101/tree/main/Lecture%20Notes)。
- [生物医学定量方法](https://campbell-muscle-lab.github.io/teaching_PGY630_QM/)：肯塔基大学 Ken Campbell 教授的 16 周课程。研究生级别课程，专为博士生和其他希望培养数据分析和解释相关技能的人而设计，包括数据处理、绘图、统计和图像分析。本课程使用 MATLAB，材料可在 [GitHub](https://github.com/Campbell-Muscle-Lab/teaching_PGY630_QM) 上获取。
- [运动生物力学讲座系列](https://www.youtube.com/channel/UCmG-bd1JL1ACP7hMzIUXwOg) 由 Stuart McErlain-Naylor 策划。包括介绍性主题，例如 Vicon 介绍的动作捕捉技术（[讲座 1](https://www.youtube.com/watch?v=1zJ14cW-JqY) 和[讲座 2](https://www.youtube.com/watch?v=hM7xEoyP-4o)) 以及 [简介](https://www.youtube.com/watch?v=2xgyTpsa14M#) Delsys 的肌电图 (EMG)。
- [BPK 409：可穿戴技术与人类生理学](https://www.youtube.com/channel/UClU9XVBC0mDwJBIVJTUbtwg/videos)，作者：Max Donelan（西蒙弗雷泽大学）。该课程教授如何使用最先进的可穿戴技术来测量、分析和理解人体生理系统，包括肌肉、神经和心血管系统。
📄 [实验室说明](https://docs.google.com/document/d/e/2PACX-1vTr1zOyrUedA1yx76olfDe5jn88miCNb3EJcC3INmy8nDmbJ8N5Y0B30EBoOunsWbA2DGOVWpgJzIs9/pub) |
💾 [代码](https://github.com/patmorli/BPK-409)
- [David Silver 强化学习简介](https://deepmind.com/learning-resources/-introduction-reinforcement-learning-david-silver)，作者：David Silver，DeepMind (2015)。
- 巴塞尔大学[图形与视觉研究小组](https://gravis.dmi.unibas.ch/)的[统计形状建模](https://shapemodelling.cs.unibas.ch/ssm-course/)。这是统计形状建模的入门课程（部分托管在 Futurelearn 上）。它的重点在于高斯过程的概念，以及如何使用它们来模拟形状变化。它还讨论了将模型拟合到表面和图像的简单算法。

## YouTube 频道：电视：

- [AnyBody 技术视频和网络广播](https://www.youtube.com/channel/UCbgDnEKXyYOETR_Nb6YdehA)
- [美国生物力学协会 (ASB)](https://www.youtube.com/@AmSocBiomech)
- [动态行走](https://www.youtube.com/@dynamicwalking4049)
- [Biomch-V](https://www.youtube.com/channel/UCcv9iv6v4_l9dfDDW1PTZCA)：包括 2015 年国际生物力学学会大会的视频。
- [BOOM：我们心中的生物力学](https://www.youtube.com/@biomechanicsonourminds9735/videos)：由 Melissa Boswell 和 Hannah O'Day（斯坦福大学）主持的 postcad 视频。他们与世界各地的研究人员谈论令人兴奋的生物力学领域。它们还涵盖克服失败、合作、开放科学、领导力等等。
- [欧洲生物力学学会 (ESB)](https://www.youtube.com/@ESBiomech)
- [国际运动生物力学学会 (ISBS)](https://www.youtube.com/@ISBSOFFICIAL)：来自 ISBS2020 虚拟会议的视频。
- [足踝研究杂志](https://www.youtube.com/@JFootAnkleRes)
- [Neuromech TV](https://www.youtube.com/@NeuromechTV) 由巴西潘帕联邦大学应用神经力学研究小组制作。它旨在帮助对人类运动及其相关主题的研究感兴趣的学生和科学家。
- [OpenSim 视频和网络研讨会](https://www.youtube.com/user/OpenSimVideos/videos)
- [UCalgary Human Performance Lab](https://www.youtube.com/channel/UCxAOMJHF-5xQMFkLAutV7Dg/videos)：来自 ISB/ASB2019（国际生物力学学会和美国生物力学学会联合大会）和 Dynamic Walking 2019 会议的许多非常有趣的视频。

## 研究人员

- [BassettBiomechanics](https://www.youtube.com/c/Bassettbiomechanics/videos)：包括_肌肉骨骼系统生物力学_课程和 Visual3D 教程。
- [Manoj Srinivasan 的频道](https://www.youtube.com/user/sjonam/videos)
- [罗斯·米勒的频道](https://www.youtube.com/channel/UCO_H7aZoIcwZiNc4KjiQQkg/videos)
- [Stuart McErlain-Naylor 频道](https://www.youtube.com/channel/UCmG-bd1JL1ACP7hMzIUXwOg)
- [Luca Modenese 的频道](https://www.youtube.com/channel/UCp08ZXIV056MxvOvdMeowtA)
- [Thomas Geijtenbeek 频道 (HyFyDy / SCONE)](https://www.youtube.com/@goatstream)

## 视频🎥

- [对诱导加速分析的批评](https://www.youtube.com/watch?v=2EmwIM_uQnk&t=18s)，作者：Andy Ruina (WCB2014)。
- [用力平台分析直立姿势（葡萄牙语，英文字幕）](https://www.youtube.com/playlist?list=PLw8zLrKDgyofy14nXcU1o4GyDEwmhi1nT)：Felipe Fava de Lima 制作的有关使用力平台的视频。
- [生物力学播放列表](https://www.youtube.com/playlist?list=PLH144fs5LXOPFtafyiTVpXQBEpdrnfn3m) 作者：Kath Boyer。与生物力学相关的 YouTube 视频播放列表。
- [CNB-ASB 肌肉研讨会](https://www.youtube.com/watch?v=Ur9wYYR0nac&feature=youtu.be)：关于“神经力学综合肌肉建模”主题的演示。
- [F8 2019 - VR 全身跟踪和头像](https://www.youtube.com/watch?v=FhiAFo9U_sM) 和 [博客文章](https://uploadvr.com/facebook-f8-2019-body-tracking/)
- [用骨钉跑步](https://www.youtube.com/watch?v=nf6jkyNgkwE)：Ton Van den Bogert 分享的受试者用骨钉跑步的数据收集视频。
- [轨迹优化简介](https://www.youtube.com/watch?v=wlkRYMVUZTs) 作者：[Matthew Kelly](http://www.matthewpeterkelly.com/index.html)。非常清晰地介绍了该主题，并在视频说明中链接了 MATLAB 资源。
- [从 CT 扫描到 FEA 的免费/开源工作流程](https://peterfalkingham.com/2020/11/06/a-free-opensource-workflow-from-ct-scan-to-fea/)，作者：[Peter L. Falkingham](https://peterfalkingham.com/)：使用免费开源软件（用于分割的 Dragonfly、用于网格细化的 Blender 和用于有限元分析的 FEBio 主要步骤的快速概述。

## 学习编码：构造：

该路段正在建设中

## 关键资源

| Resource | Link |
|----------|------|

