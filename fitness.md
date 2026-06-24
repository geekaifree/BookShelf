# 健身与运动

> 本文档整合了以下源文件：fitness.md, workout.md, biomechanics.md, wger.md, wingfit.md, gym.md

---

## 来源：fitness.md

## 简介

Workout Cool 是一款开源健身平台，提供锻炼跟踪、运动库和训练计划管理。它专为希望跟踪健身进度并遵循结构化锻炼计划的个人设计。

| 特性 | 描述 |
|---------|-------------|
| 运动库 | 包含说明的全面运动数据库 |
| 锻炼跟踪 | 记录锻炼、组数、次数和重量 |
| 训练计划 | 预制和可自定义的锻炼计划 |
| 进度跟踪 | 可视化图表和统计数据 |
| 开源 | 免费使用和自托管 |

## 架构

### 技术栈

| 组件 | 技术 |
|-----------|-----------|
| 前端 | 响应式设计的 JavaScript 框架 |
| 后端 | 基于 Node.js 或 Python 的 API 服务器 |
| 数据库 | PostgreSQL 或 SQLite 数据存储 |
| 认证 | 用户注册和登录系统 |

### 数据模型

| 实体 | 描述 |
|--------|-------------|
| User | 带有个人资料和偏好的账户 |
| Exercise | 包含肌肉群和说明的单个运动 |
| Workout | 一次会话中执行的运动集合 |
| Program | 结构化的多周训练计划 |
| Set | 运动中的单组（次数、重量、时长） |

## 安装

### Docker 部署

```bash
docker run -d \
  --name=workout-cool \
  -p 3000:3000 \
  -v ./data:/app/data \
  -e DATABASE_URL=postgresql://user:pass@db:5432/workout \
  --restart unless-stopped \
  workout-cool/workout-cool:latest
```

### Docker Compose

```yaml
version: "3.8"
services:
  app:
    image: workout-cool/workout-cool:latest
    container_name: workout-cool
    ports:
      - "3000:3000"
    environment:
      - DATABASE_URL=postgresql://workout:password@db:5432/workout
      - SECRET_KEY=your_secret_key
    depends_on:
      - db
    restart: unless-stopped

  db:
    image: postgres:15
    container_name: workout-db
    environment:
      - POSTGRES_USER=workout
      - POSTGRES_PASSWORD=password
      - POSTGRES_DB=workout
    volumes:
      - postgres_data:/var/lib/postgresql/data
    restart: unless-stopped

volumes:
  postgres_data:
```

## 运动库

### 运动分类

| 分类 | 示例运动 |
|----------|------------------|
| 胸部 | 卧推、俯卧撑、飞鸟 |
| 背部 | 引体向上、划船、硬拉 |
| 肩部 | 过头推举、侧平举、面拉 |
| 手臂 | 二头弯举、三头臂屈伸、锤式弯举 |
| 腿部 | 深蹲、弓步、腿举、提踵 |
| 核心 | 平板支撑、卷腹、俄罗斯转体 |
| 有氧 | 跑步、骑行、划船、跳绳 |

### 运动信息

| 字段 | 描述 |
|-------|-------------|
| 名称 | 官方运动名称 |
| 主要肌肉 | 目标肌肉群 |
| 辅助肌肉 | 支撑肌肉群 |
| 器械 | 所需器械（杠铃、哑铃、器械、自重） |
| 难度 | 初级、中级或高级 |
| 说明 | 分步执行指南 |
| 视频 | 示范视频链接 |

### 器械类型

| 器械 | 描述 |
|-----------|-------------|
| 杠铃 | 带杠铃片的长杆 |
| 哑铃 | 手持重量 |
| 器械 | 固定路径的训练器械 |
| 龙门架 | 可调节的绳索器械 |
| 自重 | 无需器械 |
| 壶铃 | 带手柄的球形重量 |
| 弹力带 | 用于阻力的弹性带 |
| TRX | 悬挂训练带 |

## 锻炼跟踪

### 创建锻炼

| 步骤 | 操作 |
|------|--------|
| 1 | 开始新的锻炼会话 |
| 2 | 从运动库中选择运动 |
| 3 | 记录组数、次数、重量和时长 |
| 4 | 为每个运动添加备注 |
| 5 | 完成并保存锻炼 |

### 组类型

| 类型 | 描述 |
|------|-------------|
| 正式组 | 标准重量的标准组 |
| 热身组 | 较轻重量以准备肌肉 |
| 递减组 | 达到力竭后减轻重量 |
| 暂停休息 | 短暂休息后继续同一组 |
| AMRAP | 尽可能多的次数 |
| 计时 | 执行固定时长 |

### 记录字段

| 字段 | 描述 |
|-------|-------------|
| 重量 | 使用的重量（kg 或 lbs） |
| 次数 | 完成的重复次数 |
| 时长 | 计时运动的时间（秒） |
| RPE | 主观疲劳感觉（1-10 分） |
| 备注 | 该组的自由备注 |

## 训练计划

### 计划结构

| 层级 | 描述 |
|-------|-------------|
| Program | 多周训练计划 |
| Week | 锻炼日的集合 |
| Day | 包含运动的具体锻炼 |
| Exercise | 带有规定组数/次数的单个运动 |

### 热门计划模板

| 计划 | 重点 | 频率 |
|---------|-------|-----------|
| Starting Strength | 初学者力量 | 每周 3 天 |
| PPL (推/拉/腿) | 肌肥大 | 每周 6 天 |
| 上肢/下肢 | 均衡训练 | 每周 4 天 |
| 全身 | 综合健身 | 每周 3 天 |
| 5/3/1 | 力量进阶 | 每周 4 天 |

### 计划自定义

| 设置 | 描述 |
|---------|-------------|
| 时长 | 计划的周数 |
| 频率 | 每周锻炼天数 |
| 进阶 | 重量/次数随时间的增长方式 |
| 减载 | 计划中的恢复周 |
| 分化 | 肌肉群在各天的分配方式 |

## 进度跟踪

### 指标

| 指标 | 描述 |
|--------|-------------|
| 总容量 | 所有组的重量 x 次数之和 |
| 最大重量 | 每个运动的最重重量 |
| 总次数 | 完成的总重复次数 |
| 锻炼时长 | 运动花费的时间 |
| 体重 | 随时间的体重测量 |
| 身体围度 | 胸围、腰围、臂围、腿围 |

### 可视化

| 图表类型 | 显示的数据 |
|-----------|---------------|
| 折线图 | 重量随时间的进阶 |
| 柱状图 | 每周每个肌肉群的容量 |
| 热力图 | 锻炼频率日历 |
| 饼图 | 肌肉群分布 |

## 营养集成

### 营养跟踪字段

| 字段 | 描述 |
|-------|-------------|
| 卡路里 | 每日卡路里摄入量 |
| 蛋白质 | 摄入的蛋白质克数 |
| 碳水化合物 | 摄入的碳水化合物克数 |
| 脂肪 | 摄入的脂肪克数 |
| 水 | 每日饮水量（升） |

### 膳食计划

| 餐次 | 典型内容 |
|------|----------------|
| 早餐 | 高蛋白的早晨开始 |
| 午餐 | 均衡宏量营养素搭配蔬菜 |
| 晚餐 | 瘦肉蛋白搭配复合碳水化合物 |
| 加餐 | 正餐之间的健康选择 |
| 训练前 | 训练前的快速能量 |
| 训练后 | 用于恢复的蛋白质和碳水化合物 |

## API 和集成

### API 端点

| 端点 | 方法 | 描述 |
|----------|--------|-------------|
| `/api/workouts` | GET | 列出用户锻炼 |
| `/api/workouts` | POST | 创建新锻炼 |
| `/api/exercises` | GET | 列出运动 |
| `/api/programs` | GET | 列出训练计划 |
| `/api/stats` | GET | 获取用户统计数据 |

## 总结

| 主题 | 核心要点 |
|-------|-------------|
| 运动库 | 包含肌肉群定位的全面数据库 |
| 跟踪 | 记录每个运动的组数、次数、重量和 RPE |
| 计划 | 预制和可自定义的多周计划 |
| 进度 | 可视化图表跟踪随时间的改善 |
| 营养 | 可选的膳食和宏量营养素跟踪集成 |
| 自托管 | 完全控制您的健身数据 |


---

## 来源：workout.md

## 简介

本指南涵盖了锻炼、训练计划和健身的基础知识。它专为想要了解如何有效训练、跟踪进度并建立可持续健身习惯的初学者和中级训练者设计。

## 目录

- [训练计划](#训练计划)
- [动作库](#动作库)
- [进度跟踪](#进度跟踪)
- [肌肉群](#肌肉群)
- [训练分化](#训练分化)
- [热身](#热身)
- [放松](#放松)
- [营养基础](#营养基础)
- [恢复](#恢复)
- [家庭训练](#家庭训练)
- [常见错误](#常见错误)

---

## 训练计划

结构良好的训练计划是健身进步的基础。

### 训练原则

| 原则 | 描述 | 应用 |
|------|------|------|
| 渐进超负荷 | 逐渐增加训练刺激 | 随时间增加重量、次数或组数 |
| 专项性 | 训练你想提高的 | 力量训练用于力量 |
| 恢复 | 肌肉在休息中生长 | 同一肌群训练间隔 48-72 小时 |
| 变化 | 随时间改变刺激 | 每 4-8 周轮换动作 |
| 个性化 | 根据你的需求定制 | 根据目标、经验、恢复调整 |

### 初学者计划结构

| 组成部分 | 详情 |
|----------|------|
| 频率 | 每周 3 天 |
| 类型 | 全身训练 |
| 动作 | 每次 5-7 个复合动作 |
| 组数 | 每个动作 3-4 组 |
| 次数 | 增肌 8-12 次，力量 5-8 次 |
| 休息 | 组间 2-3 分钟 |
| 时长 | 45-60 分钟 |

### 中级计划结构

| 组成部分 | 详情 |
|----------|------|
| 频率 | 每周 4-5 天 |
| 类型 | 上/下半身或推/拉/腿分化 |
| 动作 | 每次 6-8 个动作 |
| 组数 | 每个动作 3-5 组 |
| 次数 | 根据目标变化 |
| 休息 | 复合动作 2-3 分钟，孤立动作 1-2 分钟 |
| 时长 | 60-75 分钟 |

### 初学者示例计划（每周 3 天）

**A 日：**

| 动作 | 组数 | 次数 | 休息 |
|------|------|------|------|
| 深蹲 | 3 | 8-10 | 3 分钟 |
| 卧推 | 3 | 8-10 | 3 分钟 |
| 杠铃划船 | 3 | 8-10 | 3 分钟 |
| 过头推举 | 3 | 8-10 | 2 分钟 |
| 罗马尼亚硬拉 | 3 | 10-12 | 2 分钟 |

**B 日：**

| 动作 | 组数 | 次数 | 休息 |
|------|------|------|------|
| 硬拉 | 3 | 5-8 | 3 分钟 |
| 过头推举 | 3 | 8-10 | 3 分钟 |
| 引体向上/高位下拉 | 3 | 8-10 | 2 分钟 |
| 保加利亚分腿蹲 | 3 | 10-12 | 2 分钟 |
| 哑铃划船 | 3 | 10-12 | 2 分钟 |

**安排：** 周一（A）、周三（B）、周五（A）、周一（B）等。

---

## 动作库

### 复合动作（多关节）

| 动作 | 主要肌肉 | 器械 | 难度 |
|------|----------|------|------|
| 杠铃深蹲 | 股四头肌、臀大肌 | 杠铃、架子 | 中级 |
| 硬拉 | 背部、臀大肌、腘绳肌 | 杠铃 | 中级 |
| 卧推 | 胸部、三头肌 | 杠铃、卧推凳 | 中级 |
| 过头推举 | 肩部、三头肌 | 杠铃 | 中级 |
| 杠铃划船 | 背部、二头肌 | 杠铃 | 中级 |
| 引体向上 | 背部、二头肌 | 引体向上杆 | 中级 |
| 双杠臂屈伸 | 胸部、三头肌 | 双杠 | 中级 |
| 弓步 | 股四头肌、臀大肌 | 哑铃 | 初级 |
| 俯卧撑 | 胸部、三头肌 | 自重 | 初级 |

### 孤立动作（单关节）

| 动作 | 目标肌肉 | 器械 | 难度 |
|------|----------|------|------|
| 二头弯举 | 二头肌 | 哑铃 | 初级 |
| 三头伸展 | 三头肌 | 绳索/哑铃 | 初级 |
| 侧平举 | 三角肌中束 | 哑铃 | 初级 |
| 腿弯举 | 腘绳肌 | 器械 | 初级 |
| 腿屈伸 | 股四头肌 | 器械 | 初级 |
| 提踵 | 小腿 | 器械/自重 | 初级 |
| 面拉 | 三角肌后束 | 绳索 | 初级 |

### 自重动作
### 自重动作

| 动作 | 肌肉 | 进阶 |
|------|------|------|
| 俯卧撑 | 胸部、三头肌 | 上斜 → 标准 → 下斜 → 钻石 → 单手 |
| 引体向上 | 背部、二头肌 | 辅助 → 离心 → 标准 → 负重 |
| 深蹲 | 股四头肌、臀大肌 | 辅助 → 自重 → 跳跃 → 单腿 |
| 双杠臂屈伸 | 胸部、三头肌 | 凳子 → 平行杆 → 吊环 |
| 平板支撑 | 核心 | 跪姿 → 标准 → 负重 → 单臂 |
| 弓步 | 股四头肌、臀大肌 | 原地 → 行走 → 跳跃 |

---

## 进度跟踪

跟踪进度对保持动力和确保计划有效至关重要。

### 跟踪内容

| 指标 | 跟踪方式 | 频率 |
|------|----------|------|
| 举重重量 | 训练日志 | 每次训练 |
| 体重 | 体重秤（每天同一时间） | 每周平均 |
| 身体围度 | 卷尺 | 每 2-4 周 |
| 进度照片 | 相机（相同条件） | 每 4 周 |
| 力量 PR | 训练日志 | 达成时 |
| 训练 RPE | 主观用力程度 | 每次训练 |

### 力量标准（男性，体重倍数）

| 动作 | 入门 | 中级 | 进阶 | 精英 |
|------|------|------|------|------|
| 深蹲 | 0.75x 体重 | 1.25x 体重 | 1.75x 体重 | 2.5x 体重 |
| 卧推 | 0.5x 体重 | 1x 体重 | 1.5x 体重 | 2x 体重 |
| 硬拉 | 1x 体重 | 1.5x 体重 | 2x 体重 | 2.75x 体重 |
| 过头推举 | 0.4x 体重 | 0.75x 体重 | 1x 体重 | 1.35x 体重 |
| 引体向上 | 1-3 | 8-10 | 15-20 | 25+ |

### 力量标准（女性，体重倍数）

| 动作 | 入门 | 中级 | 进阶 | 精英 |
|------|------|------|------|------|
| 深蹲 | 0.5x 体重 | 1x 体重 | 1.5x 体重 | 2x 体重 |
| 卧推 | 0.25x 体重 | 0.5x 体重 | 0.75x 体重 | 1.25x 体重 |
| 硬拉 | 0.75x 体重 | 1.25x 体重 | 1.75x 体重 | 2.5x 体重 |
| 过头推举 | 0.25x 体重 | 0.5x 体重 | 0.75x 体重 | 1x 体重 |
| 引体向上 | 0-1 | 3-5 | 8-10 | 15+ |

### 渐进超负荷方法

| 方法 | 描述 | 使用时机 |
|------|------|----------|
| 增加重量 | 以最小增量增加负荷 | 达到目标次数时 |
| 增加次数 | 相同重量做更多次 | 重量感觉可控时 |
| 增加组数 | 做额外的组 | 容量太低时 |
| 缩短休息 | 缩短休息时间 | 体能重点时 |
| 改善动作 | 更好的幅度、控制 | 始终 |

---

## 肌肉群

了解肌肉群有助于设计均衡的训练计划。

### 主要肌肉群

| 肌肉群 | 位置 | 关键动作 |
|--------|------|----------|
| 胸部（胸大肌） | 上身前侧 | 卧推、俯卧撑、双杠 |
| 背部（背阔肌、斜方肌、菱形肌） | 上背 | 引体向上、划船、硬拉 |
| 肩部（三角肌） | 手臂顶部 | 过头推举、侧平举 |
| 二头肌 | 上臂前侧 | 弯举、反手引体 |
| 三头肌 | 上臂后侧 | 伸展、双杠、窄距卧推 |
| 股四头肌 | 大腿前侧 | 深蹲、腿举、弓步 |
| 腘绳肌 | 大腿后侧 | 硬拉、腿弯举、北欧式弯举 |
| 臀大肌 | 臀部 | 深蹲、臀桥、弓步 |
| 小腿 | 小腿 | 提踵 |
| 核心（腹肌、斜腹） | 腰腹 | 平板支撑、卷腹、抬腿 |

### 肌肉群恢复时间

| 肌肉群 | 恢复时间 | 训练频率 |
|--------|----------|----------|
| 腿部（股四头、腘绳肌） | 48-72 小时 | 每周 2 次 |
| 胸部 | 48-72 小时 | 每周 2 次 |
| 背部 | 48-72 小时 | 每周 2 次 |
| 肩部 | 48-72 小时 | 每周 2 次 |
| 手臂（二头、三头） | 24-48 小时 | 每周 2-3 次 |
| 核心 | 24-48 小时 | 每周 2-3 次 |
| 小腿 | 24-48 小时 | 每周 2-3 次 |

### 次数范围与目标

| 次数范围 | 组数 | 休息 | 主要目标 |
|----------|------|------|----------|
| 1-5 | 3-5 | 3-5 分钟 | 力量 |
| 6-12 | 3-4 | 2-3 分钟 | 增肌（肌肉体积） |
| 12-20 | 3-4 | 1-2 分钟 | 肌肉耐力 |
| 20+ | 2-3 | 1 分钟 | 耐力、体能 |

---

## 训练分化

训练分化决定了你如何在一周内安排训练。

### 常见训练分化

| 分化 | 天数 | 最佳用途 | 安排示例 |
|------|------|----------|----------|
| 全身 | 3 | 入门 | 周一/周三/周五 |
| 上/下半身 | 4 | 中级 | 周一/周二/周四/周五 |
| 推/拉/腿 | 3-6 | 中级-进阶 | 周一/周三/周五或轮换 |
| 兄弟分化 | 5 | 进阶（有争议） | 每天一个部位 |
| 混合 | 4-5 | 运动专项 | 不固定 |

### 全身分化（3 天）

| 天 | 重点 |
|----|------|
| 周一 | 全身 A |
| 周三 | 全身 B |
| 周五 | 全身 A |
| 周一 | 全身 B（重复） |

### 上/下半身分化（4 天）

| 天 | 重点 |
|----|------|
| 周一 | 上半身（力量） |
| 周二 | 下半身（力量） |
| 周四 | 上半身（增肌） |
| 周五 | 下半身（增肌） |

### 推/拉/腿分化（6 天）

| 天 | 重点 |
|----|------|
| 周一 | 推（胸部、肩部、三头肌） |
| 周二 | 拉（背部、二头肌） |
| 周三 | 腿（股四头、腘绳肌、臀大肌、小腿） |
| 周四 | 推 |
| 周五 | 拉 |
| 周六 | 腿 |

### 选择分化方式

| 因素 | 推荐 |
|------|------|
| 入门 | 全身（3 天） |
| 中级 | 上/下半身（4 天） |
| 进阶 | 推/拉/腿（5-6 天） |
| 时间有限 | 全身（2-3 天） |
| 力量重点 | 上/下半身或全身 |
| 体型重点 | 推/拉/腿 |

---

## 热身

正确的热身为运动做好准备并降低受伤风险。

### 热身组成部分

| 组成部分 | 时长 | 目的 |
|----------|------|------|
| 一般有氧 | 5-10 分钟 | 提高心率和体温 |
| 动态拉伸 | 5-10 分钟 | 改善活动范围 |
| 激活 | 3-5 分钟 | 激活目标肌肉 |
| 专项热身 | 5-10 分钟 | 用轻重量练习动作 |

### 动态热身流程

| 动作 | 时长 | 目标 |
|------|------|------|
| 开合跳 | 30 秒 | 全身 |
| 手臂环绕 | 30 秒 | 肩部 |
| 腿摆 | 30 秒/腿 | 髋部 |
| 髋环绕 | 30 秒 | 髋部 |
| 自重深蹲 | 10-15 次 | 腿部 |
| 带转体弓步 | 10 次/腿 | 腿部、脊柱 |
| 俯卧撑 | 10 次 | 上半身 |
| 弹力带拉开 | 15 次 | 上背 |

### 深蹲专项热身

| 组 | 重量 | 次数 | 休息 |
|----|------|------|------|
| 1 | 空杆（20 公斤） | 10 | 1 分钟 |
| 2 | 工作重量 50% | 8 | 1 分钟 |
| 3 | 工作重量 70% | 5 | 2 分钟 |
| 4 | 工作重量 85% | 3 | 2 分钟 |
| 5 | 工作重量 | 第一个工作组 | - |

---

## 放松

放松帮助身体从运动过渡到休息。

### 放松组成部分

| 组成部分 | 时长 | 目的 |
|----------|------|------|
| 轻度有氧 | 5-10 分钟 | 逐渐降低心率 |
| 静态拉伸 | 5-10 分钟 | 改善柔韧性、减少酸痛 |
| 泡沫轴滚压 | 5-10 分钟 | 释放肌肉紧张 |

### 静态拉伸流程

| 拉伸 | 时长 | 目标 |
|------|------|------|
| 股四头拉伸 | 30 秒/腿 | 股四头肌 |
| 腘绳肌拉伸 | 30 秒/腿 | 腘绳肌 |
| 髋屈肌拉伸 | 30 秒/腿 | 髋屈肌 |
| 胸部拉伸 | 30 秒 | 胸部 |
| 肩部拉伸 | 30 秒/臂 | 肩部 |
| 三头肌拉伸 | 30 秒/臂 | 三头肌 |
| 小腿拉伸 | 30 秒/腿 | 小腿 |
| 婴儿式 | 60 秒 | 背部、肩部 |

### 泡沫轴指南

| 身体部位 | 时长 | 技巧 |
|----------|------|------|
| 股四头 | 60 秒/腿 | 慢慢滚动，在痛点暂停 |
| 腘绳肌 | 60 秒/腿 | 从膝盖滚到臀部 |
| IT 束 | 60 秒/腿 | 从髋部滚到膝盖 |
| 小腿 | 60 秒/腿 | 从脚踝滚到膝盖 |
| 上背 | 60 秒 | 从背部中间滚到肩部 |
| 臀部 | 60 秒/侧 | 坐在滚筒上，交叉一条腿 |

---

## 营养基础

营养与训练对实现健身目标同样重要。

### 宏量营养素

| 宏量营养素 | 每克热量 | 主要功能 | 来源 |
|-----------|---------|---------|------|
| 蛋白质 | 4 卡/克 | 肌肉修复和生长 | 肉、鱼、蛋、奶、豆类 |
| 碳水化合物 | 4 卡/克 | 运动能量 | 米饭、面包、面食、水果、蔬菜 |
| 脂肪 | 9 卡/克 | 激素产生、能量 | 坚果、油、牛油果、肥鱼 |

### 每日宏量营养素目标

| 目标 | 蛋白质 | 碳水 | 脂肪 |
|------|--------|------|------|
| 增肌 | 1.6-2.2 克/公斤体重 | 4-6 克/公斤体重 | 0.8-1.2 克/公斤体重 |
| 减脂 | 1.8-2.4 克/公斤体重 | 2-3 克/公斤体重 | 0.7-1 克/公斤体重 |
| 维持 | 1.4-1.8 克/公斤体重 | 3-5 克/公斤体重 | 0.8-1.2 克/公斤体重 |
| 一般健康 | 1.2-1.6 克/公斤体重 | 3-5 克/公斤体重 | 0.8-1.2 克/公斤体重 |

### 热量目标

| 目标 | 方法 |
|------|------|
| 增肌 | 在维持热量基础上盈余 250-500 卡 |
| 减脂 | 在维持热量基础上亏损 300-500 卡 |
| 维持 | 按维持热量进食 |

### 进餐时机

| 时机 | 吃什么 | 原因 |
|------|--------|------|
| 训练前（1-2 小时） | 碳水 + 适量蛋白质 | 训练能量 |
| 训练后（2 小时内） | 蛋白质 + 碳水 | 肌肉恢复 |
| 全天 | 均衡饮食 | 持续营养 |
| 睡前 | 蛋白质（酪蛋白） | 夜间恢复 |

### 水分补充

| 活动水平 | 每日饮水量 |
|----------|-----------|
| 久坐 | 2-2.5 升 |
| 活跃 | 2.5-3.5 升 |
| 非常活跃 / 炎热气候 | 3.5-4.5+ 升 |
| 运动期间 | 每小时活动 500ml |

---

## 恢复

恢复是身体适应训练和变得更强壮的时候。

### 恢复方法

| 方法 | 描述 | 效果 |
|------|------|------|
| 睡眠 | 每晚 7-9 小时 | 非常高 |
| 营养 | 充足的蛋白质和热量 | 非常高 |
| 休息日 | 不训练的日子 | 高 |
| 主动恢复 | 轻度活动（散步、游泳） | 中等 |
| 泡沫轴 | 自我肌筋膜放松 | 中等 |
| 拉伸 | 静态和动态 | 中等 |
| 冷疗 | 冷水浴、冰浴 | 中等（证据不一） |
| 按摩 | 专业按摩 | 中等 |
| 压缩 | 压缩服装 | 低-中 |

### 睡眠与恢复

| 因素 | 建议 |
|------|------|
| 时长 | 每晚 7-9 小时 |
| 一致性 | 固定就寝和起床时间 |
| 环境 | 黑暗、凉爽、安静 |
| 睡前 | 睡前 30 分钟不看屏幕 |
| 咖啡因 | 下午 2 点后不喝咖啡因 |
| 酒精 | 限制（影响睡眠质量） |

### 过度训练信号

| 信号 | 描述 | 行动 |
|------|------|------|
| 持续疲劳 | 尽管休息仍总是累 | 减载一周 |
| 表现下降 | 重量变轻 | 减少训练量 |
| 失眠 | 难以入睡 | 降低训练强度 |
| 情绪变化 | 易怒、抑郁 | 休息和恢复 |
| 生病增多 | 更频繁生病 | 优先睡眠和营养 |
| 关节疼痛 | 持续关节痛 | 检查动作、减轻负荷 |
| 食欲下降 | 不饿 | 可能是过度训练 |

### 减载周

减载周减少训练压力以允许恢复：

| 参数 | 正常周 | 减载周 |
|------|--------|--------|
| 容量 | 100% | 50-60% |
| 强度 | 100% | 60-70% |
| 频率 | 正常 | 相同或减少 |

**何时减载：**

- 每 4-8 周持续训练后
- 出现过度训练信号时
- 比赛或最大努力期后
- 动力显著下降时

---

## 家庭训练

没有健身房也能有效训练。

### 自重动作进阶

**推力进阶：**

| 级别 | 动作 | 组 x 次 |
|------|------|---------|
| 1 | 墙壁俯卧撑 | 3x15 |
| 2 | 上斜俯卧撑 | 3x12 |
| 3 | 跪姿俯卧撑 | 3x12 |
| 4 | 标准俯卧撑 | 3x10 |
| 5 | 钻石俯卧撑 | 3x10 |
| 6 | 下斜俯卧撑 | 3x10 |
| 7 | 弓箭手俯卧撑 | 3x8 |
| 8 | 单手俯卧撑 | 3x5 |

**拉力进阶：**

| 级别 | 动作 | 组 x 次 |
|------|------|---------|
| 1 | 门框划船 | 3x12 |
| 2 | 反向划船（低杆） | 3x10 |
| 3 | 离心引体向上 | 3x5 |
| 4 | 弹力带辅助引体向上 | 3x8 |
| 5 | 标准引体向上 | 3x8 |
| 6 | 反手引体向上 | 3x10 |
| 7 | L 型引体向上 | 3x6 |
| 8 | 负重引体向上 | 3x6 |

**腿部进阶：**

| 级别 | 动作 | 组 x 次 |
|------|------|---------|
| 1 | 辅助深蹲 | 3x15 |
| 2 | 自重深蹲 | 3x15 |
| 3 | 跳跃深蹲 | 3x12 |
| 4 | 保加利亚分腿蹲 | 3x10/腿 |
| 5 | 单腿深蹲离心 | 3x5/腿 |
| 6 | 单腿深蹲 | 3x5/腿 |

### 最小装备家庭健身房

| 装备 | 费用 | 动作 |
|------|------|------|
| 引体向上杆 | $25-50 | 引体向上、反手引体、悬挂抬腿 |
| 弹力带 | $20-40 | 各种动作、辅助 |
| 哑铃（可调） | $100-300 | 所有哑铃动作 |
| 瑜伽垫 | $15-30 | 地面动作、拉伸 |
| 健腹轮 | $10-20 | 核心动作 |

### 家庭训练示例（全身）

| 动作 | 组数 | 次数 | 休息 |
|------|------|------|------|
| 俯卧撑 | 3 | 10-15 | 60 秒 |
| 自重深蹲 | 3 | 15-20 | 60 秒 |
| 引体向上（或划船） | 3 | 8-12 | 60 秒 |
| 弓步 | 3 | 12/腿 | 60 秒 |
| 平板支撑 | 3 | 30-60 秒 | 60 秒 |
| 臀桥 | 3 | 15-20 | 60 秒 |

---

## 常见错误

避免这些常见的训练错误。

### 训练错误

| 错误 | 问题 | 解决方案 |
|------|------|----------|
| 跳过热身 | 增加受伤风险 | 始终热身 10-15 分钟 |
| 动作不标准 | 受伤、效果降低 | 先学习正确动作 |
| 容量过大 | 过度训练、恢复差 | 从少开始，逐渐增加 |
| 无渐进超负荷 | 没有进步 | 跟踪并增加刺激 |
| 忽视腿部 | 体型不均衡 | 每周练腿 2 次 |
| 虚荣重量 | 受伤风险 | 使用合适的重量 |
| 无休息日 | 过度训练 | 每周休息 1-2 天 |
| 跳过放松 | 紧张、酸痛 | 每次训练后拉伸 |

### 营养错误

| 错误 | 问题 | 解决方案 |
|------|------|----------|
| 蛋白质不足 | 恢复差 | 1.6-2.2 克/公斤体重 |
| 跳过餐食 | 能量低、恢复差 | 规律进食 |
| 加工食品太多 | 营养质量差 | 专注于全食物 |
| 饮水不足 | 脱水 | 每天 2.5-3.5 升 |
| 极端饮食 | 不可持续、不健康 | 适度、均衡的方法 |

### 心态错误

| 错误 | 问题 | 解决方案 |
|------|------|----------|
| 与他人比较 | 气馁 | 专注于自己的进步 |
| 期望快速结果 | 挫败感 | 信任过程 |
| 全有或全无思维 | 不一致 | 任何运动都比没有好 |
| 忽视疼痛 | 受伤 | 疼痛时休息 |
| 不坚持 | 没有进步 | 养成习惯 |

---

## 总结

健身是一段奖励坚持和耐心的终身旅程。关键要点：

- **从基础开始**：增加重量前先学习正确动作
- **坚持**：规律训练胜过偶尔的高强度训练
- **渐进超负荷**：随时间逐渐增加挑战
- **恢复很重要**：睡眠、营养和休息日必不可少
- **跟踪进度**：可衡量的才能管理
- **耐心**：真正的成果需要数月和数年，而非数天和数周
- **享受过程**：找到你真正喜欢的活动
- **倾听身体**：需要时休息，适当时推进


---

## 来源：biomechanics.md

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



---

## 来源：wger.md

## 目录

1. [简介](#introduction)
2. [安装](#installation)
3. [训练计划](#workout-plans)
4. [动作数据库](#exercise-database)
5. [营养追踪](#nutrition-tracking)
6. [体重追踪](#weight-tracking)
7. [REST API](#rest-api)
8. [移动端集成](#mobile-integration)
9. [自定义](#customization)
10. [最佳实践](#best-practices)

---

## 简介

wger 是一个开源健身与营养追踪平台，帮助用户管理训练、追踪营养摄入、监控体重，并维护完整的动作数据库。该平台提供 Web 界面和 REST API，可与移动应用及其他工具集成。

### 核心功能

| 功能 | 描述 |
|------|------|
| 训练管理 | 创建和管理训练计划，包含动作、组数和次数 |
| 营养追踪 | 记录饮食，追踪卡路里、宏量和微量营养素 |
| 动作数据库 | 包含详细描述和目标肌群的大量动作 |
| 体重追踪 | 通过图表监控体重变化 |
| REST API | 完整的 API，用于构建移动应用和集成 |
| 多语言 | 支持多种语言 |
| 自托管 | 完全掌控你的数据 |

### 架构概览

wger 使用 Django（Python）构建，数据库为 PostgreSQL。前端结合服务端模板和 JavaScript 实现交互功能。REST API 遵循 Django REST Framework 模式。

```
┌─────────────────────────────────────────────────┐
│                   Frontend                       │
│  ┌─────────────┐  ┌─────────────┐  ┌─────────┐ │
│  │   Templates  │  │  JavaScript │  │   API   │ │
│  └─────────────┘  └─────────────┘  └─────────┘ │
├─────────────────────────────────────────────────┤
│                   Backend                        │
│  ┌─────────────┐  ┌─────────────┐  ┌─────────┐ │
│  │    Django    │  │    REST     │  │ Database│ │
│  │   Views      │  │  Framework  │  │ (PgSQL) │ │
│  └─────────────┘  └─────────────┘  └─────────┘ │
└─────────────────────────────────────────────────┘
```

---

## 安装

### 前置要求

| 要求 | 版本 | 用途 |
|------|------|------|
| Python | 3.8+ | 运行环境 |
| PostgreSQL | 12+ | 数据库 |
| Node.js | 16+ | 前端资源 |
| pip | 最新版 | Python 包管理器 |
| Git | 最新版 | 版本控制 |

### Docker 安装

最简单的运行方式是使用 Docker：

```bash
# 克隆仓库
git clone https://github.com/wger-project/wger.git
cd wger

# 使用 Docker Compose 启动
docker-compose up -d

# 访问应用
# 在浏览器中打开 http://localhost:8000
```

### 手动安装

```bash
# 创建虚拟环境
python -m venv wger-venv
source wger-venv/bin/activate

# 安装依赖
pip install -r requirements.txt

# 配置数据库
# 编辑 wger/settings.py，填入数据库凭据

# 运行数据库迁移
python manage.py migrate

# 创建管理员用户
python manage.py createsuperuser

# 加载初始数据
python manage.py load-exercise-data

# 启动开发服务器
python manage.py runserver
```

### 配置

`settings.py` 中的关键配置项：

| 设置 | 默认值 | 描述 |
|------|--------|------|
| `DATABASES` | SQLite | 数据库配置 |
| `ALLOWED_REGISTRATION` | True | 允许新用户注册 |
| `WGER_SETTINGS` | dict | 应用特定设置 |
| `EMAIL_BACKEND` | console | 邮件配置 |
| `LANGUAGE_CODE` | en | 默认语言 |

### 生产环境部署

生产环境建议使用 Gunicorn 配合 Nginx：

```nginx
# /etc/nginx/sites-available/wger
server {
    listen 80;
    server_name your-domain.com;

    location /static/ {
        alias /path/to/wger/static/;
    }

    location /media/ {
        alias /path/to/wger/media/;
    }

    location / {
        proxy_pass http://127.0.0.1:8000;
        proxy_set_header Host $host;
        proxy_set_header X-Real-IP $remote_addr;
    }
}
```

```bash
# 使用 Gunicorn 启动
gunicorn wger.wsgi:application --bind 0.0.0.0:8000 --workers 4
```

---

## 训练计划

### 创建训练计划

wger 中的训练计划将动作组织成结构化的日常训练。每个计划可包含多天，每天可包含多个动作。

**第一步：创建新计划**

导航到"Workouts"，点击"New Workout Plan"，为其取一个描述性名称。

**第二步：添加训练日**

| 日类型 | 描述 | 示例 |
|--------|------|------|
| 推日 | 胸、肩、三头肌 | 卧推、肩上推举 |
| 拉日 | 背、二头肌 | 划船、引体向上 |
| 腿日 | 股四头肌、腘绳肌、小腿 | 深蹲、硬拉 |
| 全身 | 所有主要肌群 | 复合动作 |
| 休息日 | 恢复 | 轻度拉伸、散步 |

**第三步：为每天添加动作**

为每天添加动作时，设置以下参数：

| 参数 | 描述 | 示例 |
|------|------|------|
| 动作 | 从数据库选择 | 杠铃卧推 |
| 组数 | 组数 | 4 |
| 次数 | 每组重复次数 | 8-12 |
| 休息 | 组间休息（秒） | 90 |
| 重量 | 起始重量（kg/lbs） | 60 |
| RPE | 主观疲劳等级 | 8 |

### 训练模板

为常用训练创建可复用模板：

```
训练计划："增肌计划"
├── 第1天：推
│   ├── 卧推：4x8-12，休息90秒
│   ├── 肩上推举：3x10-12，休息60秒
│   ├── 上斜哑铃卧推：3x12，休息60秒
│   ├── 侧平举：4x15，休息45秒
│   └── 三头下压：3x15，休息45秒
├── 第2天：拉
│   ├── 杠铃划船：4x8-12，休息90秒
│   ├── 引体向上：3x8-10，休息90秒
│   ├── 面拉：3x15，休息45秒
│   ├── 杠铃弯举：3x12，休息60秒
│   └── 锤式弯举：3x12，休息45秒
├── 第3天：腿
│   ├── 深蹲：4x8-12，休息120秒
│   ├── 罗马尼亚硬拉：3x10-12，休息90秒
│   ├── 腿举：3x12-15，休息60秒
│   ├── 腿弯举：3x12，休息60秒
│   └── 提踵：4x15，休息45秒
└── 第4天：休息
```

### 渐进超负荷追踪

wger 支持追踪渐进超负荷：

| 周 | 动作 | 组x次 | 重量 | 总容量 |
|----|------|-------|------|--------|
| 1 | 卧推 | 4x10 | 60kg | 2400kg |
| 2 | 卧推 | 4x10 | 62.5kg | 2500kg |
| 3 | 卧推 | 4x10 | 65kg | 2600kg |
| 4 | 卧推 | 4x12 | 60kg | 2880kg |

### 训练安排

设置周期性训练计划：

- **频率**：每周 3-6 天
- **轮换**：自动循环训练日
- **日历集成**：导出到日历应用
- **提醒**：邮件/推送通知

---

## 动作数据库

### 动作分类

动作数据库按肌群和器械组织：

| 肌群 | 示例动作 | 器械 |
|------|----------|------|
| 胸 | 卧推、飞鸟、俯卧撑 | 杠铃、哑铃、器械 |
| 背 | 划船、引体向上、高位下拉 | 杠铃、绳索、自重 |
| 肩 | 推举、平举、耸肩 | 哑铃、绳索、器械 |
| 腿 | 深蹲、弓步蹲、腿举 | 杠铃、器械、自重 |
| 手臂 | 弯举、臂屈伸、双杠 | 哑铃、绳索、杠铃 |
| 核心 | 卷腹、平板支撑、抬腿 | 自重、绳索、器械 |

### 添加自定义动作

用户可以向动作数据库贡献内容：

```
动作数据结构：
- name: 动作名称
- category: chest
- muscles: [pectoralis_major]
- muscles_secondary: [anterior_deltoid, triceps]
- equipment: [barbell, bench]
- description: 详细动作描述
- instructions: 分步指导
- variations: [variation1, variation2]
```

### 动作变体

每个动作可以有多个变体：

| 基础动作 | 变体 | 区别 |
|----------|------|------|
| 卧推 | 上斜卧推 | 侧重上胸 |
| 卧推 | 下斜卧推 | 侧重下胸 |
| 卧推 | 窄握卧推 | 侧重三头肌 |
| 深蹲 | 前蹲 | 侧重股四头肌 |
| 深蹲 | 保加利亚分腿蹲 | 单侧训练 |

### 筛选和搜索

可按以下条件筛选动作：

- **肌群**：主要和次要肌群
- **器械**：可用的健身器械
- **难度**：初级、中级、高级
- **类型**：复合、孤立、有氧

---

## 营养追踪

### 设置营养目标

定义每日营养目标：

| 营养素 | 目标 | 范围 | 用途 |
|--------|------|------|------|
| 卡路里 | 2500 kcal | 2300-2700 | 能量平衡 |
| 蛋白质 | 180g | 160-200g | 肌肉修复 |
| 碳水化合物 | 300g | 250-350g | 能量 |
| 脂肪 | 70g | 60-80g | 激素、吸收 |
| 膳食纤维 | 30g | 25-35g | 消化健康 |

### 记录饮食

全天追踪饮食：

**早餐示例：**

| 食物 | 份量 | 卡路里 | 蛋白质 | 碳水 | 脂肪 |
|------|------|--------|--------|------|------|
| 燕麦 | 100g | 389 | 16.9g | 66.3g | 6.9g |
| 香蕉 | 1根 | 105 | 1.3g | 27g | 0.4g |
| 乳清蛋白 | 30g | 120 | 24g | 3g | 1.5g |
| **合计** | | **614** | **42.2g** | **96.3g** | **8.8g** |

### 营养数据库

营养数据库包含：

- **品牌食品**：厂商产品
- **普通食品**：常见天然食品
- **餐厅菜品**：快餐和餐厅餐食
- **自定义条目**：用户创建的食物

### 饮食计划

创建可复用的饮食计划：

```
饮食计划："增肌饮食"
├── 第1餐：早餐（7:00）
│   ├── 燕麦配浆果
│   ├── 鸡蛋（3个全蛋）
│   └── 橙汁
├── 第2餐：加餐（10:00）
│   ├── 希腊酸奶
│   └── 混合坚果
├── 第3餐：午餐（13:00）
│   ├── 鸡胸肉
│   ├── 糙米
│   └── 西兰花
├── 第4餐：训练前（16:00）
│   ├── 香蕉
│   └── 蛋白奶昔
└── 第5餐：晚餐（19:00）
    ├── 三文鱼
    ├── 红薯
    └── 蔬菜沙拉
```

### 营养报告

生成详细的营养报告：

| 指标 | 每日 | 每周 | 每月 |
|------|------|------|------|
| 平均卡路里 | 2,450 | 17,150 | 73,500 |
| 平均蛋白质 | 175g | 1,225g | 5,250g |
| 目标达成率 | 92% | 88% | 85% |
| 达标天数 | 6/7 | 28/30 | 85% |

---

## 体重追踪

### 记录体重

追踪体重变化：

| 日期 | 体重 | 变化 | 备注 |
|------|------|------|------|
| 2024-01-01 | 80.0kg | - | 起始体重 |
| 2024-01-08 | 79.5kg | -0.5kg | 表现不错 |
| 2024-01-15 | 79.2kg | -0.3kg | 持续稳定 |
| 2024-01-22 | 79.0kg | -0.2kg | 进展放缓 |
| 2024-01-29 | 78.8kg | -0.2kg | 按计划进行 |

### 体重图表

wger 生成可视化图表，显示：

- **每日体重**：单次测量值
- **移动平均**：7天和30天平均值
- **趋势线**：整体方向
- **目标线**：目标体重轨迹

### 身体围度

追踪额外测量数据：

| 测量项 | 起始 | 当前 | 变化 |
|--------|------|------|------|
| 胸围 | 100cm | 102cm | +2cm |
| 腰围 | 85cm | 82cm | -3cm |
| 臂围 | 35cm | 37cm | +2cm |
| 大腿围 | 55cm | 57cm | +2cm |
| 体脂率 | 18% | 15% | -3% |

### 统计分析

系统计算：

- **体重变化率**：每周公斤数
- **热量盈余/缺口**：根据体重变化估算
- **预测**：预计达成目标日期
- **一致性评分**：追踪规律性

---

## REST API

### 认证

```bash
# 获取 API token
curl -X POST https://wger.example.com/api/v2/token \
  -d "username=your_username" \
  -d "password=your_password"

# 响应
{
    "token": "9944b09199c62bcf9418ad846dd0e4bbdfc6ee4b"
}
```

### API 端点

| 端点 | 方法 | 描述 |
|------|------|------|
| `/api/v2/workout/` | GET/POST | 列出/创建训练 |
| `/api/v2/workout/{id}/` | GET/PUT/DELETE | 管理特定训练 |
| `/api/v2/exercise/` | GET | 列出动作 |
| `/api/v2/nutrition/` | GET/POST | 营养计划 |
| `/api/v2/weight/` | GET/POST | 体重记录 |
| `/api/v2/setting/` | GET/POST | 训练设置 |
| `/api/v2/day/` | GET/POST | 训练日 |
| `/api/v2/set/` | GET/POST | 动作组数 |

### API 调用示例

**获取所有训练：**

```bash
curl -H "Authorization: Token 9944b09199c62bcf9418ad846dd0e4bbdfc6ee4b" \
  https://wger.example.com/api/v2/workout/
```

**创建新训练：**

```bash
curl -X POST \
  -H "Authorization: Token your_token" \
  -H "Content-Type: application/json" \
  -d '{"comment": "My new workout"}' \
  https://wger.example.com/api/v2/workout/
```

**记录体重：**

```bash
curl -X POST \
  -H "Authorization: Token your_token" \
  -H "Content-Type: application/json" \
  -d '{"date": "2024-01-15", "weight": 79.5}' \
  https://wger.example.com/api/v2/weight/
```

### API 响应格式

```json
{
    "count": 42,
    "next": "http://example.com/api/v2/exercise/?page=2",
    "previous": null,
    "results": [
        {
            "id": 1,
            "name": "Barbell Bench Press",
            "category": 10,
            "muscles": [4, 5],
            "equipment": [1, 8]
        }
    ]
}
```

### 速率限制

| 端点类型 | 限制 | 时间窗口 |
|----------|------|----------|
| 读取 | 1000 请求 | 每小时 |
| 写入 | 100 请求 | 每小时 |
| 已认证 | 更高限制 | 每小时 |

---

## 移动端集成

### 官方移动应用

wger 提供以下平台的移动应用：

| 平台 | 功能 | 下载 |
|------|------|------|
| Android | 完整训练追踪，离线模式 | Google Play |
| iOS | 训练记录，体重追踪 | App Store |

### 移动应用功能

- **离线模式**：无网络时也能记录训练
- **同步**：上线后自动同步
- **相机**：拍摄进度照片
- **通知**：训练提醒
- **小组件**：快速记录入口

### 构建自定义移动应用

使用 REST API 构建自定义应用：

```javascript
// React Native 示例
const API_BASE = 'https://wger.example.com/api/v2';

async function getWorkouts(token) {
    const response = await fetch(`${API_BASE}/workout/`, {
        headers: {
            'Authorization': `Token ${token}`,
            'Content-Type': 'application/json'
        }
    });
    return response.json();
}

async function logWeight(token, date, weight) {
    const response = await fetch(`${API_BASE}/weight/`, {
        method: 'POST',
        headers: {
            'Authorization': `Token ${token}`,
            'Content-Type': 'application/json'
        },
        body: JSON.stringify({ date, weight })
    });
    return response.json();
}
```

### 第三方集成

| 集成 | 方向 | 同步数据 |
|------|------|----------|
| Google Fit | 导出 | 训练数据 |
| Apple Health | 导出 | 体重、训练 |
| Fitbit | 导入 | 活动数据 |
| Strava | 导入 | 有氧训练 |

---

## 自定义

### 主题

自定义外观：

```python
# 在 settings.py 中自定义 CSS
WGER_SETTINGS = {
    'theme': 'dark',
    'accent_color': '#4CAF50',
    'logo': '/path/to/logo.png',
    'favicon': '/path/to/favicon.ico'
}
```

### 自定义动作分类

添加组织特定的动作分类：

```python
# 在 Django admin 或通过管理命令
from exercises.models import ExerciseCategory

ExerciseCategory.objects.create(
    name="Functional Training",
    description="Functional movement patterns"
)
```

### 语言配置

| 语言 | 代码 | 状态 |
|------|------|------|
| 英语 | en | 完整 |
| 德语 | de | 完整 |
| 西班牙语 | es | 完整 |
| 法语 | fr | 完整 |
| 葡萄牙语 | pt | 完整 |
| 俄语 | ru | 部分 |

### 用户权限

配置用户角色：

| 角色 | 权限 |
|------|------|
| 用户 | 追踪自己的训练和营养 |
| 教练 | 查看客户训练，创建计划 |
| 管理员 | 完全系统访问 |
| API 用户 | 仅编程访问 |

### 邮件模板

自定义通知邮件：

```html
<!-- templates/emails/workout_reminder.html -->
<h1>训练提醒</h1>
<p>你好 {{ user.username }}，</p>
<p>别忘了今天的 {{ workout.name }} 训练！</p>
<p>动作：</p>
<ul>
{% for exercise in workout.exercises %}
    <li>{{ exercise.name }} - {{ exercise.sets }}x{{ exercise.reps }}</li>
{% endfor %}
</ul>
```

---

## 最佳实践

### 数据备份

定期备份至关重要：

```bash
# 数据库备份
pg_dump wger_db > wger_backup_$(date +%Y%m%d).sql

# 媒体备份
tar -czf wger_media_$(date +%Y%m%d).tar.gz /path/to/media/

# 自动备份脚本
#!/bin/bash
BACKUP_DIR="/backups/wger"
DATE=$(date +%Y%m%d)
pg_dump wger_db | gzip > "$BACKUP_DIR/db_$DATE.sql.gz"
tar -czf "$BACKUP_DIR/media_$DATE.tar.gz" /path/to/media/
```

### 性能优化

| 优化措施 | 实施方式 | 影响 |
|----------|----------|------|
| 缓存 | Redis/Memcached | 高 |
| 数据库索引 | 合理索引 | 中 |
| 静态文件 | CDN 加速 | 中 |
| 查询优化 | select_related/prefetch_related | 高 |

### 安全检查清单

- 生产环境启用 HTTPS
- 设置强密码 SECRET_KEY
- 配置 ALLOWED_HOSTS
- 启用 CSRF 保护
- 设置安全 Cookie 标志
- 定期安全更新
- 数据库静态加密
- API 速率限制

### 常见问题

| 问题 | 解决方案 |
|------|----------|
| 查询慢 | 添加数据库索引 |
| 内存占用高 | 优化 Django 查询 |
| API 错误 | 检查认证 token |
| 同步问题 | 验证网络连接 |

---

## 总结

wger 提供了一个全面的健身与营养追踪平台：

- **灵活的训练管理**：创建和自定义训练计划
- **详细的营养追踪**：监控卡路里和宏量营养素
- **进度监控**：追踪体重和身体围度
- **REST API**：构建自定义集成和移动应用
- **自托管**：完全掌控你的健身数据

该平台适合个人用户、私人教练以及寻求开源健身追踪方案的组织。


---

## 来源：wingfit.md

**Source:** https://github.com/itskovacs/wingfit

## Overview

This tutorial covers the key resources and tools from the [itskovacs/wingfit](https://github.com/itskovacs/wingfit) project.

## 📝 Table of Contents

- 📦 [About](#about)
- 🌱 [Getting Started](#getting_started)
- 📸 [Demo](#Demo)
- 🚧 [Roadmap](#Roadmap)
- 📜 [License](#License)
- 🤝 [Contributing](#Contributing)
- 🛠️ [Tech Stack](#techstack)

## 📦 About

Wingfit is a minimalist fitness app to **plan your workouts**, **track your personal records** and **leverage smartwatch data**.

Demo is worth a thousand words, head to 📸 [Demo](#Demo).

🔒 Privacy-First – No telemetry, no tracking, fully self-hostable. You own your data. Inspect, modify, and contribute freely.

## 🌱 Getting Started

If you need help, feel free to open an [issue](https://github.com/itskovacs/wingfit/issues).

Deployment is designed to be simple using Docker.

## Option 1: Docker Compose (Recommended)

Use the `docker-compose.yml` file provided in this repository. No changes are required, though you may customize it to suit your needs.

Run the container:

```bash
docker-compose up -d
```

## Option 2: Docker Run

```bash

## Ensure you have the latest image

docker pull ghcr.io/itskovacs/wingfit:5

## Run the container

docker run -d -p 8080:8000 -v ./storage:/app/storage ghcr.io/itskovacs/wingfit:5
```

Refer to the [configuration documentation](https://github.com/itskovacs/wingfit/tree/main/docs/config.md) to set up OIDC authentication and other settings.

## 📸 Demo

A demo is available at [Wingfit.fr](https://wingfit.fr).

|         |         |
|:-------:|:-------:|
|  |  |
|  |  |
|  |  |

## 🚧 Roadmap

New features coming soonTM, check out the development plan in the [Roadmap Wiki](https://github.com/itskovacs/wingfit/wiki/Roadmap). If you have ideas 💡, feel free to open an issue.

If you want to develop new feature, feel free to open a pull request (see [🤝 Contributing](#contributing)).

## 📜 License

I decided to license Wingfit under the **CC BY-NC-SA 4.0** – You may use, modify, and share freely with attribution, but **commercial use is prohibited**.

## Key Resources

| Resource | Link |
|----------|------|
| issue | [https://github.com/itskovacs/wingfit/issues](https://github.com/itskovacs/wingfit/issues) |
| configuration documentation | [https://github.com/itskovacs/wingfit/tree/main/docs/config.md](https://github.com/itskovacs/wingfit/tree/main/docs/config.md) |
| Wingfit.fr | [https://wingfit.fr](https://wingfit.fr) |
| Roadmap Wiki | [https://github.com/itskovacs/wingfit/wiki/Roadmap](https://github.com/itskovacs/wingfit/wiki/Roadmap) |



---

## 来源：gym.md

## 简介

wger 是一个开源的自托管健身和锻炼追踪器。它管理锻炼计划、运动数据库、营养追踪和身体测量。本教程涵盖安装、锻炼计划、营养记录和进度跟踪。

## 功能概览

| 功能 | 描述 |
|------|------|
| 锻炼管理器 | 创建和跟踪锻炼计划 |
| 运动数据库 | 300+ 运动及说明 |
| 营养追踪 | 卡路里和宏量营养素追踪 |
| 身体测量 | 体重、体脂等 |
| 日历 | 锻炼安排 |
| REST API | 完整 API 用于集成 |

## 安装

### Docker Compose

```yaml
version: '3'
services:
  wger:
    image: wger/server
    container_name: wger
    restart: unless-stopped
    environment:
      - DJANGO_DB=sqlite
      - SECRET_KEY=your-secret-key
      - ALLOWED_HOSTS=gym.example.com
      - TIME_ZONE=UTC
    volumes:
      - ./wger-static:/home/wger/static
      - ./wger-media:/home/wger/media
      - ./wger-db:/home/wger/db
    ports:
      - "8000:8000"
```

### 手动安装

```bash
pip install wger
wger bootstrap
wger start
```

## 运动

### 运动分类

| 分类 | 示例 |
|------|------|
| 手臂 | 二头弯举、三头伸展 |
| 腿部 | 深蹲、腿举、弓步 |
| 胸部 | 卧推、俯卧撑、飞鸟 |
| 背部 | 引体向上、划船、硬拉 |
| 肩部 | 过头推举、侧平举 |
| 核心 | 平板支撑、卷腹、俄罗斯转体 |
| 有氧 | 跑步、骑车、游泳 |

### 运动属性

| 属性 | 描述 |
|------|------|
| Name | 运动名称 |
| Category | 身体部位分类 |
| Muscles | 主要和次要肌肉 |
| Equipment | 所需器材 |
| Description | 分步说明 |
| Images | 演示图片 |

### 追踪的肌肉

| 肌肉群 | 肌肉 |
|--------|------|
| 上半身 | 胸部、背阔肌、二头肌、三头肌、肩部、前臂 |
| 核心 | 腹肌、斜肌、下背部 |
| 下半身 | 股四头肌、腘绳肌、臀部、小腿 |

## 锻炼计划

### 创建锻炼计划

1. 导航到 Workout > Workout Plans。
2. 点击"New Workout"。
3. 命名锻炼（如"Push Day"）。
4. 添加锻炼日。
5. 为每天添加运动。
6. 设置组数、次数和重量。

### 锻炼结构

| 级别 | 示例 |
|------|------|
| 计划 | 4 天分化 |
| 日 | Day 1：胸部和三头肌 |
| 运动 | 卧推 |
| 组 | 3 组 x 8-10 次 |

### 组类型

| 类型 | 描述 |
|------|------|
| Normal | 标准工作组 |
| Warm-up | 轻重量热身 |
| Drop set | 递减重量组 |
| Failure | 训练至力竭 |
| Rest-Pause | 小组间短休息 |

### 次数设置

| 设置 | 选项 |
|------|------|
| 次数 | 1-100（或最大） |
| 组数 | 1-20 |
| 重量 | kg 或 lbs |
| 组间休息 | 秒 |
| RPE | 主观用力感觉（1-10） |

## 锻炼记录

### 记录锻炼

1. 打开锻炼计划。
2. 选择今天的训练日。
3. 为每个运动输入完成的组数。
4. 记录每组的重量和次数。
5. 保存锻炼会话。

### 会话数据

| 数据点 | 描述 |
|--------|------|
| Date | 锻炼日期 |
| Duration | 总时长 |
| Exercises | 执行的运动列表 |
| Sets | 每组的重量、次数 |
| Notes | 自由格式笔记 |

## 营养追踪

### 营养计划

| 组件 | 描述 |
|------|------|
| Goal | 减重、维持或增重 |
| Calories | 每日卡路里目标 |
| Protein | 每日蛋白质克数 |
| Carbs | 每日碳水克数 |
| Fat | 每日脂肪克数 |
| Meals | 单个餐次条目 |

### 记录食物

| 步骤 | 操作 |
|------|------|
| 1 | 进入 Nutrition > Add Meal |
| 2 | 搜索食物项 |
| 3 | 选择份量 |
| 4 | 添加到餐次 |
| 5 | 对所有项目重复 |

### 营养数据库

| 数据 | 可用信息 |
|------|---------|
| Calories | 每 100g 千卡 |
| Protein | 每 100g 克数 |
| Carbohydrates | 每 100g 克数 |
| Fat | 每 100g 克数 |
| Fiber | 每 100g 克数 |
| Sodium | 每 100g 毫克 |

### 宏量营养素目标

| 目标 | 蛋白质 | 碳水 | 脂肪 |
|------|--------|------|------|
| 减重 | 2.0 g/kg | 2-3 g/kg | 0.8 g/kg |
| 维持 | 1.6 g/kg | 3-5 g/kg | 1.0 g/kg |
| 增肌 | 2.0 g/kg | 4-6 g/kg | 1.0 g/kg |

## 身体测量

### 测量类型

| 测量 | 单位 | 频率 |
|------|------|------|
| 体重 | kg/lbs | 每周 |
| 体脂率 | % | 每月 |
| 胸围 | cm/英寸 | 每月 |
| 腰围 | cm/英寸 | 每月 |
| 臀围 | cm/英寸 | 每月 |
| 臂围 | cm/英寸 | 每月 |
| 大腿围 | cm/英寸 | 每月 |
| 小腿围 | cm/英寸 | 每月 |

### 追踪进度

| 指标 | 图表类型 |
|------|---------|
| 体重变化 | 折线图 |
| 身体测量 | 多线图 |
| 营养摄入 | 柱状图 |
| 锻炼容量 | 柱状图 |

## 排程

### 锻炼日程

| 功能 | 描述 |
|------|------|
| 日历视图 | 在日历上查看锻炼 |
| 重复 | 设置每周日程 |
| 休息日 | 安排休息日 |
| 提醒 | 通知支持 |

## REST API

### 认证

```bash
# 注册
curl -X POST https://gym.example.com/api/v2/register/ \
  -H "Content-Type: application/json" \
  -d '{"username":"user","password":"pass","email":"user@example.com"}'

# 登录
curl -X POST https://gym.example.com/api/v2/login/ \
  -d '{"username":"user","password":"pass"}'
```

### API 端点

| 方法 | 端点 | 描述 |
|------|------|------|
| GET | /api/v2/exercise/ | 列出运动 |
| GET | /api/v2/workout/ | 列出锻炼 |
| POST | /api/v2/workout/ | 创建锻炼 |
| GET | /api/v2/weightentry/ | 列出体重条目 |
| POST | /api/v2/weightentry/ | 添加体重条目 |
| GET | /api/v2/nutritionplan/ | 列出营养计划 |
| GET | /api/v2/ingredient/ | 搜索食物 |

## 数据导入/导出

| 格式 | 方向 | 数据 |
|------|------|------|
| JSON | 导出/导入 | 所有数据 |
| CSV | 导出 | 锻炼日志 |
| CSV | 导出 | 营养数据 |

## 移动访问

| 方式 | 描述 |
|------|------|
| Web 浏览器 | 响应式 Web 界面 |
| REST API | 构建自定义应用 |
| F-Droid | Android 应用可用 |

## 锻炼模板

### 初学者全身（3 天）

| 日 | 运动 | 组数 x 次数 |
|-----|------|------------|
| 周一/三/五 | 深蹲 | 3 x 8-10 |
| | 卧推 | 3 x 8-10 |
| | 俯身划船 | 3 x 8-10 |
| | 过头推举 | 3 x 8-10 |
| | 二头弯举 | 2 x 12 |
| | 平板支撑 | 3 x 30s |

### 中级推/拉/腿

| 日 | 重点 | 示例运动 |
|-----|------|---------|
| 周一 | 推 | 卧推、OHP、三头肌 |
| 周三 | 拉 | 划船、引体向上、二头肌 |
| 周五 | 腿 | 深蹲、硬拉、提踵 |

## 总结

wger 提供了一个全面的健身追踪平台，包含锻炼管理、运动数据库、营养追踪和身体测量记录。其自托管特性确保隐私，而 REST API 支持自定义集成和移动应用开发。


---
