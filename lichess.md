# 使用 Lichess 在线下棋

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
