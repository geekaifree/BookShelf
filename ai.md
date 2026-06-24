# 人工智能

> 本文档整合了以下源文件：llm.md, latent.md, intelligence.md, machine.md

---

## 来源：llm.md

## 目录

1. [大语言模型简介](#introduction)
2. [Transformer 架构](#transformer-architecture)
3. [分词方法](#tokenization)
4. [预训练基础](#pre-training)
5. [微调技术](#fine-tuning)
6. [提示工程](#prompt-engineering)
7. [模型评估](#evaluation)
8. [部署策略](#deployment)

---

## 简介

大语言模型（LLM）代表了自然语言处理领域的重大突破。这些模型从海量文本语料库中学习模式，能够生成类人文本、回答问题并执行各种语言任务。

### 核心概念

| 概念 | 描述 | 示例 |
|------|------|------|
| 参数 | 模型中的可学习权重 | GPT-3 拥有 175B 参数 |
| 上下文窗口 | 最大输入长度 | GPT-3.5 为 4096 tokens |
| Tokens | 文本的子词单元 | "unhappiness" → ["un", "happiness"] |
| 嵌入 | 密集向量表示 | 768 维向量 |
| 注意力机制 | 加权输入相关性的机制 | Transformer 中的自注意力 |

### 模型规模对比

| 模型 | 参数量 | 训练数据 | 发布年份 |
|------|--------|----------|----------|
| GPT-2 | 1.5B | 40GB 文本 | 2019 |
| GPT-3 | 175B | 570GB 文本 | 2020 |
| LLaMA-2 | 70B | 2T tokens | 2023 |
| Mistral | 7B | - | 2023 |

---

## Transformer 架构

Transformer 架构是现代大语言模型的基础，使用自注意力机制并行处理输入序列。

### 核心组件

| 组件 | 用途 | 实现方式 |
|------|------|----------|
| 多头注意力 | 捕获 token 之间的关系 | 并行注意力头 |
| 前馈网络 | 变换注意力输出 | 两层线性层加激活函数 |
| 层归一化 | 稳定训练 | 跨特征归一化 |
| 位置编码 | 注入序列顺序信息 | 正弦或可学习嵌入 |

### 自注意力机制

注意力机制基于 query-key 相似度计算值的加权和：

```
Attention(Q, K, V) = softmax(QK^T / √d_k)V
```

| 符号 | 含义 | 典型值 |
|------|------|--------|
| Q | Query 矩阵 | 输入投影 |
| K | Key 矩阵 | 输入投影 |
| V | Value 矩阵 | 输入投影 |
| d_k | Key 维度 | 64 或 128 |

### Encoder vs Decoder 架构

| 特性 | 仅 Encoder | 仅 Decoder | Encoder-Decoder |
|------|-----------|------------|-----------------|
| 示例 | BERT | GPT | T5 |
| 任务 | 理解 | 生成 | 翻译 |
| 注意力 | 双向 | 因果 | 交叉注意力 |
| 用途 | 分类 | 文本生成 | 序列到序列任务 |

---

## 分词

分词将原始文本转换为模型可处理的数字 token。不同方法在词汇量和 token 粒度之间提供不同的权衡。

### 分词方法

| 方法 | 描述 | 词汇量 | 示例 |
|------|------|--------|------|
| 词级 | 按空格分割 | 100K+ | "hello world" → [hello, world] |
| 字符级 | 单个字符 | 256 | "hello" → [h, e, l, l, o] |
| BPE | 字节对编码 | 32K-50K | 合并频繁出现的词对 |
| WordPiece | 类似 BERT | 30K | 基于似然的合并 |
| SentencePiece | 语言无关 | 32K | 处理空格 |

### BPE 算法步骤

1. 用单个字符初始化词汇表
2. 统计所有相邻符号对
3. 合并最频繁的符号对
4. 重复直到达到目标词汇量

| 步骤 | 词对 | 频率 | 操作 |
|------|------|------|------|
| 1 | (t, h) | 1000 | 合并 → "th" |
| 2 | (th, e) | 800 | 合并 → "the" |
| 3 | (i, n) | 600 | 合并 → "in" |

---

## 预训练

预训练让模型接触大量文本，以学习语言模式、世界知识和推理能力。

### 预训练目标

| 目标 | 描述 | 模型类型 |
|------|------|----------|
| 因果语言模型 | 预测下一个 token | GPT, LLaMA |
| 掩码语言模型 | 预测被掩码的 token | BERT, RoBERTa |
| 序列到序列 | 将输入转换为输出 | T5, BART |

### 训练超参数

| 参数 | 典型范围 | 影响 |
|------|----------|------|
| 学习率 | 1e-5 到 3e-4 | 收敛速度 |
| 批次大小 | 256 到 4M tokens | 训练稳定性 |
| 序列长度 | 2048 到 8192 | 上下文理解 |
| 预热步数 | 1000 到 5000 | 防止早期发散 |
| 权重衰减 | 0.01 到 0.1 | 正则化 |

### 训练数据来源

| 来源 | 规模 | 质量 | 多样性 |
|------|------|------|--------|
| Common Crawl | PB 级 | 不稳定 | 高 |
| Wikipedia | ~20GB | 高 | 中等 |
| 书籍 | ~100GB | 高 | 中等 |
| 代码 (GitHub) | ~500GB | 不稳定 | 专业 |
| 学术论文 | ~100GB | 高 | 专业 |

---

## 微调

微调使用更小、更专注的数据集将预训练模型适配到特定任务或领域。

### 微调方法

| 方法 | 描述 | 成本 | 质量 |
|------|------|------|------|
| 全量微调 | 更新所有参数 | 高 | 最佳 |
| LoRA | 低秩适配 | 低 | 良好 |
| QLoRA | 量化 LoRA | 极低 | 良好 |
| 前缀调优 | 学习前缀嵌入 | 低 | 中等 |
| Adapter 层 | 插入小型可训练层 | 低 | 良好 |

### LoRA 配置

| 参数 | 描述 | 推荐值 |
|------|------|--------|
| Rank (r) | 低秩维度 | 8-64 |
| Alpha | 缩放因子 | 16-32 |
| 目标模块 | 适配哪些层 | q_proj, v_proj |
| Dropout | 正则化 | 0.05-0.1 |

### 训练数据格式

```json
{
  "instruction": "Summarize the following text",
  "input": "Long article text here...",
  "output": "Concise summary here..."
}
```

---

## 提示工程

提示工程通过精心设计有效输入来引导模型产生期望行为，而无需修改模型权重。

### 提示策略

| 策略 | 描述 | 示例用例 |
|------|------|----------|
| 零样本 | 不提供示例 | 简单分类 |
| 少样本 | 包含示例 | 复杂任务 |
| 思维链 | 逐步推理 | 数学问题 |
| 自洽性 | 多条推理路径 | 验证 |

### 提示模板结构

```
[System]: You are a helpful assistant specialized in [domain].

[Context]: {relevant background information}

[Instruction]: {clear task description}

[Input]: {user query}

[Output Format]: {expected response structure}
```

### 提示优化技巧

| 技巧 | 描述 | 效果 |
|------|------|------|
| 具体明确 | 清晰、详细的指令 | 减少歧义 |
| 使用分隔符 | 清晰分隔各部分 | 改善解析 |
| 指定格式 | 定义输出结构 | 一致的响应 |
| 添加约束 | 限制响应范围 | 聚焦输出 |

---

## 评估

评估大语言模型需要多种指标和基准来衡量不同能力。

### 评估指标

| 指标 | 衡量内容 | 范围 | 用途 |
|------|----------|------|------|
| 困惑度 | 预测置信度 | 越低越好 | 语言建模 |
| BLEU | N-gram 重叠 | 0-1 | 翻译 |
| ROUGE | 摘要质量 | 0-1 | 摘要生成 |
| MMLU | 知识广度 | 0-100 | 通用知识 |
| HumanEval | 代码生成 | 0-100 | 编程 |

### 基准对比

| 基准 | 任务类型 | GPT-3.5 | GPT-4 | LLaMA-2 70B |
|------|----------|---------|-------|-------------|
| MMLU | 知识 | 70% | 86% | 69% |
| HumanEval | 代码 | 48% | 67% | 29% |
| GSM8K | 数学 | 57% | 92% | 56% |
| HellaSwag | 推理 | 85% | 95% | 85% |

### 评估最佳实践

| 实践 | 描述 |
|------|------|
| 多指标评估 | 不要依赖单一指标 |
| 多样化测试集 | 覆盖各种场景 |
| 人工评估 | 补充自动化指标 |
| 失败分析 | 研究错误输出 |

---

## 部署

高效部署大语言模型需要优化推理速度、内存使用和成本。

### 优化技术

| 技术 | 描述 | 加速比 | 质量影响 |
|------|------|--------|----------|
| 量化 | 降低精度 (FP16 到 INT4) | 2-4x | 极小 |
| KV Cache | 缓存 key-value 对 | 2-3x | 无 |
| 批处理 | 处理多个请求 | 吞吐量 | 无 |
| 剪枝 | 移除冗余权重 | 1.5-2x | 略有下降 |

### 部署平台

| 平台 | 类型 | 成本模式 | 易用性 |
|------|------|----------|--------|
| vLLM | 自托管 | 计算成本 | 中等 |
| TGI | 自托管 | 计算成本 | 中等 |
| OpenAI API | 云 API | 按 token 计费 | 简单 |
| AWS Bedrock | 云 API | 按 token 计费 | 简单 |

### 硬件要求

| 模型规模 | 最低 GPU | 推荐 GPU | 内存 |
|----------|----------|----------|------|
| 7B | 1x A10 24GB | 1x A100 40GB | 32GB |
| 13B | 1x A100 40GB | 1x A100 80GB | 64GB |
| 70B | 2x A100 80GB | 4x A100 80GB | 128GB |

---

## 总结

| 主题 | 核心要点 |
|------|----------|
| 架构 | 基于自注意力的 Transformer |
| 分词 | BPE 平衡词汇量和粒度 |
| 预训练 | 从海量文本语料库学习 |
| 微调 | 高效适配特定任务 |
| 评估 | 使用多种指标和基准 |
| 部署 | 优化速度和成本 |


---

## 来源：latent.md

**Source:** https://github.com/latentcat/latentbox

## Overview

This tutorial covers the key resources and tools from the [latentcat/latentbox](https://github.com/latentcat/latentbox) project.

## Introduction

Latent Box is a reinvented resource site, maintained by Latent Cat. Why are we doing this? We have a few pursuits:

- Bridging the information gap with high-quality content.
  We don't need another search engine, a massive collection of websites and products, or complex automation, retrieval, and user systems - because no one will look at those. We hope that when we curate a thousand sites, a hundred of them will be genuinely good things that users will open, try, and remember.

- Promoting diversity and interdisciplinary collaboration as much as possible.
  We believe that a good product, good technology, and a good team involve a broad range of disciplinary knowledge and professional skills. We hope that this collection can cover as many creative fields as possible. Therefore, it is suitable for those who are equally enthusiastic about breaking through themselves.

- Maintaining updates and engaging in community co-creation.
  Keeping updates is challenging, and the community will be our motivation to persist. Therefore, we have open-sourced the entire website on GitHub and established Twitter and Xiaohongshu accounts, as well as Discord and WeChat groups. You can share content with us on any platform and directly submit pull requests on GitHub, add contributor names. Besides, your every 'like' will be our greatest encouragement.

This is the original intention of setting up Latent Box, and we hope to bring some help to everyone!

## 介绍

Latent Box 是一个重新构想的聚合站，由 Latent Cat 组织维护。为什么要做这件事情？我们有下面几个小小的追求：

- 通过高质量的内容抹平信息差。
  我们不需要另一个搜索引擎、收录大量的网站、产品，配置复杂的自动化、检索和用户系统——因为那根本没人会看。我希望当我们收录一千个站点时，其中的一百个都是用户会打开试试并记住的、真正好的东西。

- 尽可能多元、跨界。
  我们认为一个好的产品、好的技术、好的团队，所涉及的学科知识、专业技能都是非常宽广的，希望这份合集能涵盖尽可能多的创意领域。因此，它适合同样热衷于突破自我的你。

- 保持更新、社区共创。
  保持更新非常难，社区会是我们坚持下去的动力。所以，我们在 GitHub 开源了整个网站，并建立了 Twitter、小红书账号，和 Discord、微信群。你可以在任何一个平台与我们分享内容，并可以直接在 GitHub 上提交 pull requests、添加贡献者名字。除此之外，你的每次点赞都会是对我们最大的鼓励。

这就我们设立 Latent Box 的初心，希望能给大家带来一点帮助！

## Contributors

Troy Ni
      cpunisher
      shichen
      Chang
      SuiyuanV
      Zhaohan Wang
      chty627
    
    
      Stefano
      MrHOW
      枯白子
      JOJOZ
      avantcontra
      Simian Luo
      Haofan Wang
    
    
      op7418
      onemachi
      ZHO-ZHO-ZHO
      Anthony Fu
      Ju Huo
      Dango233
      Darwish
    
    
      Mog
      LionelZ
      Leozzz7988
      Hu Ye
      青龍聖者@bdsqlsz
      Echo_Sculpture
      Leo
    
    
      IDKiro
      Yangzehao
      BbuBbu
      RayJason

## License

This work is licensed under a
[Creative Commons Attribution-NonCommercial-NoDerivs 4.0 International License][cc-by-nc-nd].

[![CC BY-NC-ND 4.0][cc-by-nc-nd-image]][cc-by-nc-nd]

[cc-by-nc-nd]: http://creativecommons.org/licenses/by-nc-nd/4.0/
[cc-by-nc-nd-image]: https://licensebuttons.net/l/by-nc-nd/4.0/88x31.png
[cc-by-nc-nd-shield]: https://img.shields.io/badge/License-CC%20BY--NC--ND%204.0-lightgrey.svg



---

## 来源：intelligence.md

**来源：** https://github.com/mxm0z/awesome-intelligence-writing

＃＃ 概述

本教程涵盖 [mxm0z/awesome-intelligence-writing](https://github.com/mxm0z/awesome-intelligence-writing) 项目中的关键资源和工具。

## 很棒的情报写作

**情报写作资源精选集**

*良好的情报在很大程度上取决于清晰、简洁的写作。*——中央情报局

[手册](#-official-manuals--guides) · [文章](#-articles) · [视频](#-videos--talks) · [书籍](#-books) · [课程](#-trainings--courses)

---

＃＃ 内容

- [官方手册和指南](#-official-manuals--guides)
  - [中央情报局 (CIA)](#central-intelligence-agency-cia)
  - [国防情报局 (DIA)](#defense-intelligence-agency-dia)
  - [国家情报总监办公室 (DNI)](#office-of-the-director-of-national-intelligence-dni)
  - [美国陆军情报卓越中心](#us-army-intelligence-center-of-excellence)
  - [司法部 (DOJ)](#department-of-justice-doj)
  - [梅西赫斯特学院](#mercyhurst-college---institute-for-intelligence-studies)
- [文章和博客文章](#-articles--blog-posts)
- [快速提示](#-quick-tips)
- [指南](#-指南)
- [视频和讲座](#-videos--talks)
- [播客](#-播客)
- [演示文稿](#-演示文稿--幻灯片)
- [书籍](#-书籍)
- [培训和课程](#-trainings--courses)
- [奖励资源](#-bonus-resources)
- [贡献](#-贡献)

---

## 中央情报局 (CIA)

| Resource | Description |
|----------|-------------|
| [Style Manual & Writers Guide for Intelligence Publications](https://fas.org/irp/cia/product/style.pdf) | The foundational CIA style guide |
| [Analytic Thinking and Presentation for Intelligence Producers](https://cryptome.org/cia-ath-pt1.htm) | Guide on analytical presentation |
| [Thinking and Writing: Cognitive Science and Intelligence Analysis](https://www.cia.gov/resources/csi/books-monographs/thinking-and-writing/) | Cognitive approach to intel writing |
| [CIA - IC Writing Style (2017)](https://contentsparks.com/wp-content/uploads/2022/01/cia-writing_guide2017.pdf) | Updated IC writing style guide |

有关 CIA 风格手册的文章

- [中情局无情风格手册中的写作技巧](https://qz.com/231110/writing-tips-from-the-cias-ruthless-style-manual/) — Quartz
- [中央情报局风格指南上线：现在你可以学习像间谍一样写作](https://www.theguardian.com/world/shortcuts/2014/jul/09/cia-writers-guide-leaked-online) — 《卫报》
- [中央情报局发布了他们的风格指南，这绝对令人着迷](https://blog.hubspot.com/marketing/cia-style-guide) — HubSpot
- [任务语法：中央情报局有 185 页的写作风格书](https://abcnews.go.com/blogs/headlines/2014/07/mission-grammatical-cia-has-185-page-writing-style-book) — ABC 新闻
- [中央情报局和言语的力量](https://hyperallergic.com/136974/the-cia-and-the-power-of-words/) — 过敏
- [泄露的 CIA 风格书中的 11 堂语法课](https://www.mentalfloss.com/article/57743/11-grammar-lessons-leaked-cia-style-book) — Mental Floss

## 国防情报局 (DIA)

| Resource | Source |
|----------|--------|
| [DIA's Style Manual for Intelligence Production](https://www.governmentattic.org/23docs/DIAstyleManualIntelProd_2016.pdf) | Government Attic |
| [DIA's Style Manual for Intelligence Production](https://www.dia.mil/FOIA/FOIA-Electronic-Reading-Room/FileId/149619/) | DIA Official |

## 国家情报总监办公室 (DNI)

| Document | Description |
|----------|-------------|
| [ICD 203 - Analytic Standards](https://www.dni.gov/files/documents/ICD/ICD%20203%20Analytic%20Standards.pdf) | Standards for analytic products |
| [ICD 206 - Sourcing Requirements](https://www.dni.gov/files/documents/ICD/ICD%20206.pdf) | Requirements for sourcing in disseminated products |
| [ICD 208 - Maximizing Utility of Analytic Products](https://www.dni.gov/files/documents/ICD/ICD%20208%20-%20Maximizing%20the%20Utility%20of%20Analytic%20Products%20(09%20Jan%202017).pdf) | Guidance on product utility |

## 美国陆军情报卓越中心

- [USAICoE 写作计划资源](https://intellibrary.libguides.com/c.php?g=654854&p=6527880)
- [增强智力写作指南](https://intellibrary.libguides.com/ld.php?content_id=53826333)

## 司法部 (DOJ)

- [如何以 BLUF 格式编写智能产品](http://dixon.hh.se/urbi/SCADA/BLUF%20Writing%20Format.pdf)
- [情报报告写作](https://www.ojp.gov/ncjrs/virtual-library/abstracts/intelligence-report-writing-criminal-intelligence-analysis-p-181)

## 梅西赫斯特学院 - 情报研究所

- [分析师风格手册](https://ncirc.bja.ojp.gov/sites/g/files/xyckuh326/files/media/document/analysts_style_manual.pdf)

↑ 返回顶部

---

## 关键资源

| Resource | Link |
|----------|------|
| Style Manual & Writers Guide for Intelligence Publications | [https://fas.org/irp/cia/product/style.pdf](https://fas.org/irp/cia/product/style.pdf) |
| Analytic Thinking and Presentation for Intelligence Producers | [https://cryptome.org/cia-ath-pt1.htm](https://cryptome.org/cia-ath-pt1.htm) |
| Thinking and Writing: Cognitive Science and Intelligence Analysis | [https://www.cia.gov/resources/csi/books-monographs/thinking-and-writing/](https://www.cia.gov/resources/csi/books-monographs/thinking-and-writing/) |
| CIA - IC Writing Style (2017) | [https://contentsparks.com/wp-content/uploads/2022/01/cia-writing_guide2017.pdf](https://contentsparks.com/wp-content/uploads/2022/01/cia-writing_guide2017.pdf) |
| Writing Tips from the CIA's Ruthless Style Manual | [https://qz.com/231110/writing-tips-from-the-cias-ruthless-style-manual/](https://qz.com/231110/writing-tips-from-the-cias-ruthless-style-manual/) |
| The CIA style guide goes online: now you can learn to write like a spy | [https://www.theguardian.com/world/shortcuts/2014/jul/09/cia-writers-guide-leaked-online](https://www.theguardian.com/world/shortcuts/2014/jul/09/cia-writers-guide-leaked-online) |
| The CIA Released Their Style Guide, and It's Absolutely Fascinating | [https://blog.hubspot.com/marketing/cia-style-guide](https://blog.hubspot.com/marketing/cia-style-guide) |
| Mission Grammatical: CIA Has 185-Page Writing Style Book | [https://abcnews.go.com/blogs/headlines/2014/07/mission-grammatical-cia-has-185-page-writing-style-book](https://abcnews.go.com/blogs/headlines/2014/07/mission-grammatical-cia-has-185-page-writing-style-book) |



---

## 来源：machine.md

## 简介

LinuxCNC 是一个开源软件系统，用于计算机控制铣床、车床、等离子切割机和机器人等机床。它提供步进电机和伺服电机的实时控制。

### 什么是 CNC？

计算机数控 (CNC) 使用计算机控制机床。LinuxCNC 解释 G-code 指令并将其转换为精确的电机运动。

| 组件 | 功能 |
|------|------|
| 计算机 | 运行 LinuxCNC 软件 |
| 运动控制器 | 生成步进脉冲 |
| 电机 | 驱动机床轴 |
| 机床 | 物理切削工具 |

### LinuxCNC 特性

| 特性 | 描述 |
|------|------|
| 实时控制 | 精确的电机控制时序 |
| G-code 解释器 | 处理加工指令 |
| 刀路显示 | 切削路径可视化 |
| 配置工具 | 机床设置向导 |
| HAL | 硬件抽象层 |

## 系统要求

### 硬件要求

| 组件 | 最低 | 推荐 |
|------|------|------|
| CPU | 1 GHz | 2+ GHz 多核 |
| 内存 | 1 GB | 4 GB |
| 存储 | 10 GB | 50 GB |
| 网络 | 可选 | 远程以太网 |

### 实时要求

| 方面 | 要求 |
|------|------|
| 延迟 | < 50 微秒抖动 |
| 内核 | PREEMPT_RT 补丁内核 |
| BIOS | 禁用电源管理 |
| USB | 避免 USB 用于运动控制 |

### 支持的硬件

| 硬件类型 | 示例 |
|----------|------|
| 步进驱动 | TB6600、DM542、Gecko G203V |
| 伺服驱动 | Mesa 7i77、Granite Devices |
| 转接板 | Mesa 7i76、C10 |
| 接口卡 | Mesa 5i25、6i25 |

## 安装

### 安装 LinuxCNC

```bash
# 下载 LinuxCNC ISO
# 从 USB 启动安装
# 或在现有 Debian/Ubuntu 上安装
sudo apt update
sudo apt install linuxcnc-uspace
```

### 安装后设置

```bash
# 检查延迟
latency-test

# 验证安装
linuxcnc --version
```

### 延迟测试

| 延迟值 | 质量 | 用例 |
|--------|------|------|
| < 15,000 ns | 优秀 | 伺服系统 |
| 15,000-30,000 ns | 良好 | 步进系统 |
| 30,000-100,000 ns | 一般 | 基本操作 |
| > 100,000 ns | 差 | 不推荐 |

## 配置

### 配置向导

LinuxCNC 包含分步配置向导：

| 向导 | 用途 |
|------|------|
| 步进配置 | 配置步进电机系统 |
| 伺服配置 | 配置伺服电机系统 |
| 主轴配置 | 配置主轴速度控制 |
| 车床配置 | 配置车床特定设置 |

### INI 文件结构

```ini
[EMC]
MACHINE = My Mill
VERSION = 1.0

[DISPLAY]
DISPLAY = axis
POSITION_OFFSET = RELATIVE
POSITION_FEEDBACK = ACTUAL

[TRAJ]
AXES = 3
COORDINATES = X Y Z
LINEAR_UNITS = inch
ANGULAR_UNITS = degree

[EMCIO]
EMCIO = io
CYCLE_TIME = 0.100
TOOL_TABLE = tool.tbl
```

### 轴配置

```ini
[AXIS_0]
TYPE = LINEAR
HOME = 0.0
MAX_VELOCITY = 5.0
MAX_ACCELERATION = 50.0
SCALE = 4000
MIN_LIMIT = -10.0
MAX_LIMIT = 10.0
```

| 参数 | 描述 |
|------|------|
| TYPE | LINEAR（线性）或 ANGULAR（角度） |
| HOME | 原点位置 |
| MAX_VELOCITY | 最大速度（单位/秒） |
| MAX_ACCELERATION | 最大加速度 |
| SCALE | 每单位步数 |

## 硬件抽象层 (HAL)

### 什么是 HAL？

HAL 允许将软件组件连接在一起，创建自定义控制配置。

| 组件类型 | 示例 |
|----------|------|
| Pin | 输入/输出信号 |
| Signal | 引脚之间的连接 |
| Function | 处理模块 |
| Thread | 执行时序 |

### 基本 HAL 命令

```bash
# 列出所有引脚
halcmd show pin

# 连接信号
halcmd net signal-name pin1 pin2

# 设置值
halcmd setp pin-name value

# 加载组件
halcmd loadrt component_name
```

### HAL 文件示例

```hal
# 加载实时组件
loadrt stepper_gen step_type=0,0,0
loadrt pid names=pid.x,pid.y,pid.z

# 连接步进发生器到位置命令
net x-pos-cmd joint.0.motor-pos-cmd => stepgen.0.position-cmd
net x-pos-fb stepgen.0.position-fb => joint.0.motor-pos-fb

# 连接 PID 控制器
net x-pos-cmd pid.x.command
net x-pos-fb pid.x.feedback
net x-output pid.x.output => stepgen.0.velocity-cmd
```

## G-code 编程

### 基本 G-code 命令

| 代码 | 功能 | 示例 |
|------|------|------|
| G0 | 快速移动 | G0 X10 Y10 |
| G1 | 直线插补 | G1 X10 Y10 F100 |
| G2 | 顺时针圆弧 | G2 X10 Y10 I5 J0 |
| G3 | 逆时针圆弧 | G3 X10 Y10 I5 J0 |
| G90 | 绝对定位 | G90 |
| G91 | 增量定位 | G91 |

### 常用 M-code

| 代码 | 功能 |
|------|------|
| M0 | 程序停止 |
| M1 | 选择性停止 |
| M2 | 程序结束 |
| M3 | 主轴正转 (CW) |
| M4 | 主轴反转 (CCW) |
| M5 | 主轴停止 |
| M6 | 换刀 |
| M8 | 冷却液开 |
| M9 | 冷却液关 |

### 示例程序

```gcode
(Header)
G21 G90 G17

(Tool change)
T1 M6
S1000 M3

(First cut)
G0 X0 Y0 Z5
G1 Z-2 F100
G1 X50 F200
G1 Y50
G1 X0
G1 Y0

(End)
G0 Z25
M5
M2
```

## 刀具管理

### 刀具表

| 刀具 | 描述 | 直径 | 长度 |
|------|------|------|------|
| T1 | 立铣刀 6mm | 6.0 mm | 50 mm |
| T2 | 钻头 3mm | 3.0 mm | 40 mm |
| T3 | 球头铣刀 4mm | 4.0 mm | 45 mm |

### 刀具长度补偿

```gcode
G43 H1 (应用 T1 刀具长度补偿)
G49 (取消刀具长度补偿)
```

## 坐标系

### 工件坐标系

| 代码 | 描述 |
|------|------|
| G54 | 工件坐标系 1 |
| G55 | 工件坐标系 2 |
| G56 | 工件坐标系 3 |
| G57 | 工件坐标系 4 |
| G58 | 工件坐标系 5 |
| G59 | 工件坐标系 6 |

### 设置工件零点

```gcode
G10 L20 P1 X0 Y0 Z0 (将 G54 设为当前位置)
```

## 安全功能

### 急停

| 组件 | 功能 |
|------|------|
| 急停按钮 | 立即停止所有运动 |
| 软件急停 | 软件触发的停止 |
| 限位开关 | 防止超程 |

### 安全配置

```ini
[EMC]
EMCIO = io

[TRAJ]
MAX_VELOCITY = 10.0
MAX_ACCELERATION = 100.0
```

## 常见操作

### 回零序列

```gcode
G28.1 (所有轴回零)
G28 X0 Y0 (返回原点)
```

### 探测

```gcode
G38.2 Z-10 F100 (向下探测)
G92 Z0 (将当前位置设为零)
```

## 故障排除

### 常见问题

| 问题 | 可能原因 | 解决方案 |
|------|----------|----------|
| 丢步 | 加速度太高 | 降低最大加速度 |
| 表面质量差 | 振动 | 检查机械刚性 |
| 通信错误 | USB 延迟 | 使用并口或 Mesa 卡 |
| 急停触发 | 限位开关 | 检查接线和配置 |

### 诊断命令

```bash
# 检查 HAL 状态
halcmd show

# 实时监控引脚
halcmd show pin -t

# 查看错误日志
dmesg | grep -i linuxcnc
```

## 总结

| 概念 | 描述 |
|------|------|
| INI 文件 | 机床配置 |
| HAL 文件 | 硬件连接 |
| G-code | 加工指令 |
| 实时 | 精确运动控制 |
| 安全 | 急停和限位开关 |


---
