# 国际象棋

> 本文档整合了以下源文件：chess.md, lichess.md

---

## 来源：chess.md

## 简介

Awesome Chess 是一个精心策划的象棋相关资源、工具、库和教学材料合集。本教程提供了一个结构化的指南，涵盖学习、对弈和开发象棋应用的最佳资源。

## 资源分类

awesome-chess 仓库将资源分为以下几个关键领域：

| 分类 | 描述 | 受众 |
|------|------|------|
| 象棋引擎 | 下象棋的计算机程序 | 开发者、高级玩家 |
| 开局数据库 | 开局理论合集 | 所有玩家 |
| 残局资源 | 残局技巧和残局库 | 中级到高级 |
| UI 库 | 棋盘前端组件 | Web 开发者 |
| API | 象棋数据和对弈服务 | 开发者 |
| PGN 工具 | 棋谱记法工具 | 所有玩家 |
| 学习平台 | 学习网站和应用 | 所有水平 |

## 象棋引擎

象棋引擎使用搜索算法和评估函数计算最佳走法。

### 顶级引擎

| 引擎 | 语言 | 许可证 | 强度 (ELO) | 特点 |
|------|------|--------|-----------|------|
| Stockfish | C++ | GPL-3.0 | 3550+ | NNUE，最强开源引擎 |
| Leela Chess Zero | C++ | GPL-3.0 | 3500+ | 基于神经网络 |
| Komodo | C++ | 专有 | 3400+ | 提供 MCTS 模式 |
| Ethereal | C++ | GPL-3.0 | 3300+ | 代码简洁、文档完善 |
| Fairy-Stockfish | C++ | GPL-3.0 | 多种 | 支持象棋变体 |

### 引擎集成

| 集成方式 | 使用场景 | 复杂度 |
|----------|----------|--------|
| UCI 协议 | 标准引擎通信 | 中等 |
| Python-chess | 带引擎绑定的 Python 库 | 低 |
| WASM 编译 | 基于浏览器的引擎 | 高 |
| REST API | 远程引擎访问 | 低 |

## 开局资源

### 推荐数据库

| 资源 | 类型 | 规模 | 访问方式 |
|------|------|------|----------|
| Lichess Open Database | 对局 | 50 亿+ | 免费下载 |
| ChessBase MegaBase | 带注释 | 1000 万+ | 商业 |
| TWIC Archives | 每周对局 | 100 万+ | 免费 |
| FICS Games DB | 在线对局 | 300 万+ | 免费下载 |

### 开局学习工具

| 工具 | 平台 | 功能 | 费用 |
|------|------|------|------|
| ChessBase | 桌面 | 深度分析，开局库构建 | 商业 |
| ChessTempo | Web | 间隔重复开局学习 | 免费增值 |
| OpeningTree | Web | 开局树状可视化 | 免费 |
| Scid vs. PC | 桌面 | 数据库和分析 | 免费 |

## 残局资源

### 残局库

| 残局库 | 覆盖棋子数 | 大小 | 格式 |
|--------|-----------|------|------|
| Syzygy | 最多 7 子 | 18 TB | 紧凑、快速 |
| Nalimov | 最多 6 子 | 1.2 TB | 传统 |
| Lomonosov | 最多 7 子 | 140 TB | 基于云端 |
| Gaviota | 最多 5 子 | 7 GB | 均衡 |

### 残局学习材料

| 资源 | 格式 | 重点 | 水平 |
|------|------|------|------|
| Silman's Complete Endcourse | 书籍 | 渐进式学习 | 初级到高级 |
| Dvoretsky's Endgame Manual | 书籍 | 全面理论 | 高级 |
| Endgame Flashcards | Web/App | 模式识别 | 所有水平 |
| Lichess Practice | Web | 交互式局面 | 初级到中级 |

## 棋盘 UI 库

面向开发象棋应用的开发者：

| 库 | 语言 | 功能 | 许可证 |
|----|------|------|--------|
| chessboard.js | JavaScript | 轻量级棋盘组件 | MIT |
| chessground | TypeScript | Lichess 棋盘组件 | GPL-3.0 |
| react-chessboard | React | React 组件封装 | MIT |
| vue-chessboard | Vue | Vue.js 集成 | MIT |
| chess.js | JavaScript | 走法验证、PGN | MIT |

### chessboard.js 基本设置

```html
<div id="board" style="width: 400px"></div>
<script src="chessboard.js"></script>
<script>
  var board = Chessboard('board', {
    position: 'start',
    draggable: true,
    onDrop: function(source, target) {
      // Validate and process move
    }
  });
</script>
```

## 象棋 API

| API | 提供者 | 功能 | 速率限制 |
|-----|--------|------|----------|
| Lichess API | Lichess | 对局、谜题、锦标赛 | 15 请求/秒 |
| Chess.com API | Chess.com | 玩家数据、对局 | 1 请求/秒 |
| Chess-Servers | 多种 | 实时对弈 | 不同 |
| Cloud Eval | Lichess | 引擎评估 | 10 请求/秒 |

### API 对比

| 功能 | Lichess | Chess.com |
|------|---------|-----------|
| 认证 | OAuth2 | OAuth2 |
| 对局导出 | PGN, JSON | PGN, JSON |
| 实时对弈 | WebSocket | 非公开 |
| Bot 对弈 | 完全支持 | 有限 |
| 谜题 API | 是 | 有限 |
| 开源 | 是 | 否 |

## PGN 和记谱

### PGN 工具

| 工具 | 功能 | 平台 |
|------|------|------|
| pgn-extract | 过滤和转换 PGN | 命令行 |
| python-chess | PGN 解析和操作 | Python |
| Scid | 数据库管理 | 桌面 |
| ChessBase | 专业数据库 | 桌面 |

### PGN 格式示例

```
[Event "Example Game"]
[Site "Online"]
[Date "2026.01.01"]
[White "Player A"]
[Black "Player B"]
[Result "1-0"]

1. e4 e5 2. Nf3 Nc6 3. Bb5 a6 4. Ba4 Nf6 5. O-O 1-0
```

## 学习平台

| 平台 | 类型 | 费用 | 最适合 |
|------|------|------|--------|
| Lichess | Web/App | 免费 | 对弈、谜题、学习 |
| Chess.com | Web/App | 免费增值 | 课程、对弈、分析 |
| Chessable | Web/App | 免费增值 | 开局学习 |
| Chess Tempo | Web | 免费增值 | 战术训练 |
| Magnus Trainer | App | 订阅 | 结构化学习 |

### 学习方法对比

| 方法 | 时间投入 | 技能重点 | 最适合水平 |
|------|----------|----------|-----------|
| 战术谜题 | 每天 15-30 分钟 | 计算 | 所有水平 |
| 残局学习 | 每天 30 分钟 | 技巧 | 中级以上 |
| 开局复习 | 每周 20 分钟 | 开局库 | 中级以上 |
| 完整对局分析 | 每周 1 小时 | 理解 | 中级以上 |
| 大师对局研究 | 每天 30 分钟 | 模式吸收 | 所有水平 |

## 象棋变体

非标准象棋的资源：

| 变体 | 棋盘大小 | 主要区别 | 资源 |
|------|----------|----------|------|
| Chess960 | 8x8 | 随机初始位置 | Lichess |
| Atomic | 8x8 | 吃子引发爆炸 | Lichess |
| Crazyhouse | 8x8 | 吃掉的棋子可放置 | Lichess |
| Xiangqi | 9x10 | 中国象棋规则 | 多种 |
| Shogi | 9x9 | 日本将棋，棋子可放置 | 多种 |

## 构建象棋应用

### 技术栈推荐

| 组件 | 推荐 | 备选 |
|------|------|------|
| 棋盘 UI | chessground | chessboard.js |
| 走法逻辑 | chess.js | 自定义实现 |
| 引擎 | Stockfish WASM | Leela WASM |
| 后端 | Python + FastAPI | Node.js + Express |
| 数据库 | PostgreSQL | MongoDB |
| 实时通信 | WebSocket | Server-Sent Events |

### 开发流程

| 阶段 | 任务 | 时长 |
|------|------|------|
| 规划 | 定义功能、选择技术栈 | 1-2 天 |
| 核心棋盘 | 实现棋盘 UI 和走法输入 | 2-3 天 |
| 游戏逻辑 | 添加规则验证和游戏状态 | 2-3 天 |
| 引擎集成 | 连接 Stockfish 进行分析 | 1-2 天 |
| 多人对战 | 通过 WebSocket 添加实时对弈 | 3-5 天 |
| 打磨 | 响应式设计、测试、部署 | 2-3 天 |

## 参与象棋开源项目

| 项目 | 语言 | 适合新手的 Issue | 文档 |
|------|------|------------------|------|
| Lichess | Scala, TypeScript | 有 | 优秀 |
| Stockfish | C++ | 偶尔有 | 良好 |
| python-chess | Python | 有 | 优秀 |
| chessboard.js | JavaScript | 有 | 良好 |

## 总结

象棋生态系统为玩家和开发者提供了丰富的资源。无论是构建应用、研究开局还是分析对局，awesome-chess 合集都提供了一个全面的起点。

关键建议：

- 使用 Lichess 作为免费开源的对弈和学习平台
- 通过 UCI 协议集成 Stockfish 进行引擎分析
- 利用 python-chess 处理游戏逻辑和 PGN
- 每天练习战术以持续提升
- 使用 chessboard.js 或 chessground 构建应用的棋盘 UI


---

## 来源：lichess.md

## 简介

Lichess 是一个免费、开源的在线国际象棋服务器。Lichess 代码库 (lila) 提供了一个完整的在线国际象棋平台，支持实时对弈、残局练习、锦标赛和分析工具。

### 什么是 Lichess？

Lichess 是一个非营利性国际象棋服务器，采用现代 Web 技术构建，提供完整的国际象棋体验，无广告或付费限制。

| 特性 | 描述 |
|------|------|
| 实时对弈 | 与他人实时下棋 |
| 残局练习 | 战术训练残局 |
| 锦标赛 | 有组织的竞技活动 |
| 分析 | 引擎辅助的棋盘分析 |
| 变体 | 支持多种国际象棋变体 |

### 架构概述

| 组件 | 技术 | 用途 |
|------|------|------|
| 后端 | Scala (Play Framework) | 游戏逻辑、API |
| 数据库 | MongoDB + Redis | 数据持久化、缓存 |
| 搜索 | Elasticsearch | 游戏和玩家搜索 |
| 实时 | WebSocket | 实时游戏通信 |
| 前端 | TypeScript | Web 界面 |

## 搭建开发环境

### 前置要求

| 要求 | 版本 |
|------|------|
| JDK | 17 或更高 |
| sbt | 最新版 |
| MongoDB | 6.0 或更高 |
| Redis | 7.0 或更高 |
| Node.js | 18 或更高 |
| yarn | 最新版 |

### 克隆和构建

```bash
git clone https://github.com/lichess-org/lila.git
cd lila
./lila
```

### 配置

```conf
# application.conf
mongodb.uri = "mongodb://localhost:27017/lichess"
redis.uri = "redis://localhost:6379"
```

## 游戏系统

### 游戏类型

| 类型 | 时间控制 | 描述 |
|------|----------|------|
| UltraBullet | 15+0 | 极速对弈 |
| Bullet | 1+0, 2+1 | 超快棋 |
| Blitz | 3+0, 5+0 | 快棋 |
| Rapid | 10+0, 15+10 | 中等节奏 |
| Classical | 30+0, 60+30 | 慢棋，战略性 |
| Correspondence | 每步数天 | 通信棋 |

### 游戏状态

| 状态 | 描述 |
|------|------|
| Created | 游戏已创建，等待玩家 |
| Started | 游戏进行中 |
| Aborted | 游戏在完成前取消 |
| Mate | 将杀 |
| Draw | 和棋 |
| Resign | 认输 |
| Timeout | 超时 |

### 游戏流程

```
创建游戏 → 匹配 → 游戏开始 → 走子 → 游戏结束 → 分析
```

## 国际象棋变体

### 支持的变体

| 变体 | 描述 | 棋盘 |
|------|------|------|
| Standard | 传统国际象棋 | 8x8 |
| Chess960 | 随机初始布局 | 8x8 |
| King of the Hill | 王到达中心即胜 | 8x8 |
| Three-check | 将军三次即胜 | 8x8 |
| Atomic | 吃子引发爆炸 | 8x8 |
| Horde | 兵对棋子 | 8x8 |
| Racing Kings | 王赛跑至第八行 | 8x8 |
| Crazyhouse | 放下已吃棋子 | 8x8 |

## 锦标赛系统

### 锦标赛类型

| 类型 | 描述 |
|------|------|
| Arena | 尽可能多得分 |
| Swiss | 固定轮次 |
| Simul | 一对多 |
| Team Battle | 团队积分竞赛 |

### 创建锦标赛

```json
POST /api/tournament
{
  "name": "Daily Blitz",
  "clock": {
    "limit": 300,
    "increment": 0
  },
  "variant": "standard",
  "minutes": 60,
  "berserkable": true
}
```

### 锦标赛计分

| 结果 | 积分 | 狂暴奖励 |
|------|------|----------|
| 胜 | 2 | +1 |
| 和 | 1 | 0 |
| 负 | 0 | 0 |
| 连胜奖励 | +1 | N/A |

## 残局练习和训练

### 残局系统

| 功能 | 描述 |
|------|------|
| 评分残局 | 带评分系统的残局 |
| 残局主题 | 按战术主题分组 |
| 残局风暴 | 尽可能多地解答 |
| 残局竞速 | 与他人竞赛 |

### 常见战术主题

| 主题 | 描述 |
|------|------|
| 双攻 | 一个棋子攻击两个 |
| 牵制 | 棋子不能移动 |
| 穿透 | 穿过有价值的棋子攻击 |
| 闪击 | 揭开攻击 |
| 双将 | 两个棋子同时将军 |
| N步杀 | N步内强制将杀 |

## 分析棋盘

### 引擎分析

| 功能 | 描述 |
|------|------|
| 评估 | 局面评估条 |
| 最佳着法 | 引擎推荐着法 |
| Multi-PV | 多线路分析 |
| 深度 | 分析深度控制 |

### 开局浏览器

| 数据库 | 描述 |
|--------|------|
| Lichess | 所有 Lichess 游戏 |
| Masters | 大师级游戏 |
| Player | 特定玩家游戏 |

## API 访问

### REST API

| 端点 | 方法 | 描述 |
|------|------|------|
| `/api/account` | GET | 用户账户信息 |
| `/api/game/export/{id}` | GET | 导出游戏 PGN |
| `/api/challenge/{user}` | POST | 挑战用户 |
| `/api/board/game/{id}/move/{move}` | POST | 走子 |
| `/api/puzzle/daily` | GET | 每日残局 |

### 身份验证

```bash
# 生成个人 API 令牌
# 访问：https://lichess.org/account/oauth/token/create
```

### WebSocket 事件

| 事件 | 描述 |
|------|------|
| `gameStart` | 游戏开始 |
| `gameFinish` | 游戏结束 |
| `challenge` | 收到新挑战 |
| `challengeDeclined` | 挑战被拒绝 |

## 数据库 Schema

### 核心集合

| 集合 | 用途 |
|------|------|
| `game5` | 游戏记录 |
| `user4` | 用户资料 |
| `puzzle2` | 残局数据 |
| `tournament` | 锦标赛数据 |
| `team` | 团队信息 |

### 游戏文档结构

```json
{
  "_id": "gameId",
  "players": [
    { "uid": "userId", "rating": 1500, "color": "white" },
    { "uid": "userId", "rating": 1500, "color": "black" }
  ],
  "turns": 40,
  "status": "mate",
  "winner": "white",
  "moves": "e2e4 e7e5 ..."
}
```

## 性能和扩展

### 缓存策略

| 缓存 | 技术 | 用途 |
|------|------|------|
| 游戏状态 | Redis | 活跃游戏数据 |
| 用户数据 | Redis | 资料信息 |
| 排行榜 | Redis | 排名计算 |
| 会话 | Redis | 认证会话 |

### 扩展考量

| 组件 | 扩展策略 |
|------|----------|
| 应用 | 水平扩展 |
| 数据库 | 按游戏 ID 分片 |
| WebSocket | 负载均衡器 + 会话粘性 |
| 搜索 | Elasticsearch 集群 |

## 部署

### Docker 设置

```yaml
version: '3'
services:
  lila:
    image: lichess/lila
    ports:
      - "9663:9663"
    depends_on:
      - mongodb
      - redis

  mongodb:
    image: mongo:6.0
    volumes:
      - mongo_data:/data/db

  redis:
    image: redis:7.0

volumes:
  mongo_data:
```

### 生产配置

| 设置 | 建议 |
|------|------|
| JVM 堆 | 4-8 GB |
| MongoDB | 副本集 |
| Redis | 集群模式 |
| 负载均衡器 | HAProxy 或 Nginx |

## 总结

| 组件 | 角色 |
|------|------|
| 游戏引擎 | 实时国际象棋逻辑 |
| 锦标赛系统 | 竞技管理 |
| 残局系统 | 训练和提升 |
| 分析工具 | 赛后复盘 |
| API | 外部集成 |


---
