# 火花健身

**来源：** https://github.com/CodeWithCJ/SparkyFitness

＃＃ 概述

本教程涵盖了 [CodeWithCJ/SparkyFitness](https://github.com/CodeWithCJ/SparkyFitness) 项目中的关键资源和工具。

## 火花健身

MyFitnessPal 的自托管、隐私至上的替代方案。跟踪营养、锻炼、身体指标和健康数据，同时完全控制您的数据。

SparkyFitness 是一个自托管健身跟踪平台，由以下部分组成：

- 后端服务器（API + 数据存储）
- 基于网络的前端
- 适用于 iOS 和 Android 的本机移动应用程序

它在您控制的基础设施上存储和管理健康数据，而不依赖第三方服务。

## 核心特性

- 营养、运动、水分、睡眠、禁食、情绪和身体测量跟踪
- 目标设定和每日签到
- 交互式图表和长期报告
- 多个用户配置文件和家庭访问
- 浅色和深色主题
- OIDC、TOTP、密码、MFA 等。

## 健康与设备集成

SparkyFitness 可以同步多个健康和健身平台的数据：

- **苹果健康**（iOS）
- **Google Health Connect** (Android)
- **Fitbit**
- **Garmin 连接**
- **Withings**
- **极流** 
- **Hevy**（未经测试）
- **OpenFoodFacts**
- **美国农业部**
- **脂肪的秘密**
- **营养x**
- **梅莉**
- **泥炉**
- **Strava**（部分测试）
- **诺里什**
- **Yazio**（使用非官方 API）

集成会自动将步数、锻炼和睡眠等活动数据以及体重和身体测量等健康指标同步到您的 SparkyFitness 服务器。

## 可选的人工智能功能（测试版）

SparkyAI 提供了一个用于记录数据和审查进度的对话界面。

- 通过聊天记录食物、锻炼、身体统计数据和步数
- 上传食物图像以进行自动膳食记录
- 保留对话历史记录以供后续跟进

注意：AI 功能目前处于测试阶段。

＃＃ 安装

选择运行 SparkyFitness 的两种方式之一：

## 1. 自托管

使用 Docker Compose 在几分钟内运行 SparkyFitness 服务器：

```bash

## 1. Create a new folder

mkdir sparkyfitness && cd sparkyfitness

## 2. Download Docker files only

curl -L -o docker-compose.yml https://github.com/CodeWithCJ/SparkyFitness/releases/latest/download/docker-compose.prod.yml
curl -L -o .env https://github.com/CodeWithCJ/SparkyFitness/releases/latest/download/default.env.example

## 4. Start the app

docker compose pull && docker compose up -d

## Key Resources

| Resource | Link |
|----------|------|
| https://codewithcj.github.io/SparkyFitness/ | [https://codewithcj.github.io/SparkyFitness/](https://codewithcj.github.io/SparkyFitness/) |
| PikaPods | [https://pikapods.com/](https://pikapods.com/) |
| Documentation Site | [https://codewithcj.github.io/SparkyFitness/](https://codewithcj.github.io/SparkyFitness/) |
| Installation Guide | [https://codewithcj.github.io/SparkyFitness/install/docker-compose](https://codewithcj.github.io/SparkyFitness/install/docker-compose) |
| Features Overview | [https://codewithcj.github.io/SparkyFitness/features](https://codewithcj.github.io/SparkyFitness/features) |
| Development Workflow | [https://codewithcj.github.io/SparkyFitness/developer/getting-started](https://codewithcj.github.io/SparkyFitness/developer/getting-started) |
| iOS App Info | [https://github.com/CodeWithCJ/SparkyFitness/wiki/Apple-Health-Integration](https://github.com/CodeWithCJ/SparkyFitness/wiki/Apple-Health-Integration) |
| Android App Info | [https://github.com/CodeWithCJ/SparkyFitness/wiki/Android-Mobile-App](https://github.com/CodeWithCJ/SparkyFitness/wiki/Android-Mobile-App) |
| Join our Discord | [https://discord.gg/vcnMT5cPEA](https://discord.gg/vcnMT5cPEA) |
| Weblate Translations | [https://hosted.weblate.org/engage/sparkyfitness](https://hosted.weblate.org/engage/sparkyfitness) |

