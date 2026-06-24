# 加密货币与区块链

> 本文档整合了以下源文件：crypto.md, chain.md, mining.md, mintable.md

---

## 来源：crypto.md

加密货币、区块链技术和你需要导航加密生态系统的资源综合教程。从基础到高级交易，本指南涵盖一切。

## 目录

- [区块链基础](#区块链基础)
- [钱包](#钱包)
- [交易所](#交易所)
- [DeFi](#defi)
- [NFT](#nft)
- [交易](#交易)
- [挖矿](#挖矿)
- [安全](#安全)
- [监管](#监管)
- [研究工具](#研究工具)
- [新闻来源](#新闻来源)
- [社区](#社区)

---

## 区块链基础

### 什么是区块链

区块链是一个分布式、不可变的账本，记录计算机网络中的交易。每个区块包含前一个区块的密码学哈希，形成链式结构。

### 核心概念

| 概念 | 描述 |
|---------|-------------|
| 区块 | 一组打包在一起的交易 |
| 链 | 链接的区块序列 |
| 节点 | 维护区块链副本的计算机 |
| 共识 | 节点间的协议机制 |
| 哈希 | 来自输入数据的固定长度字符串 |
| 私钥 | 用于签名交易的密钥 |
| 公钥 | 从私钥派生，用于接收 |
| 地址 | 公钥的缩短形式 |
| 交易 | 地址间的价值转移 |
| Gas | 执行交易的费用（Ethereum） |

### 主要区块链

| 区块链 | 原生代币 | 共识 | TPS | 智能合约 |
|-----------|-------------|-----------|-----|-----------------|
| Bitcoin | BTC | PoW | 7 | 否 |
| Ethereum | ETH | PoS | 30 | 是 |
| Solana | SOL | PoH | 65,000 | 是 |
| Cardano | ADA | PoS | 250 | 是 |
| Polkadot | DOT | NPoS | 1,000 | 是 |
| Avalanche | AVAX | PoS | 4,500 | 是 |
| BNB Chain | BNB | PoSA | 160 | 是 |
| Polygon | MATIC | PoS | 7,000 | 是 |
| Arbitrum | ETH | Optimistic | 4,000 | 是 |
| Optimism | ETH | Optimistic | 2,000 | 是 |

### 共识机制

| 机制 | 描述 | 示例 | 能源使用 |
|-----------|-------------|----------|------------|
| 工作量证明 (PoW) | 矿工解决复杂难题 | Bitcoin | 高 |
| 权益证明 (PoS) | 验证者质押代币 | Ethereum | 低 |
| 委托 PoS | 代币持有者投票选验证者 | EOS、Tron | 低 |
| 历史证明 | 可验证的时间排序 | Solana | 低 |
| 权威证明 | 可信验证者 | 私有链 | 极低 |

---

## 钱包

### 钱包类型

| 类型 | 描述 | 安全性 | 便利性 |
|------|-------------|----------|-------------|
| 硬件 | 物理设备 | 最高 | 低 |
| 软件 | 桌面/移动应用 | 中等 | 高 |
| Web | 浏览器扩展 | 中等 | 高 |
| 纸质 | 打印的密钥 | 高 | 极低 |
| 托管 | 第三方持有密钥 | 低 | 最高 |

### 硬件钱包

| 钱包 | 价格 | 币种 | 特性 |
|--------|-------|-------|----------|
| Ledger Nano S Plus | $79 | 5,500+ | 经济实惠、安全 |
| Ledger Nano X | $149 | 5,500+ | 蓝牙、更多存储 |
| Trezor Model One | $69 | 1,000+ | 开源 |
| Trezor Model T | $219 | 1,000+ | 触摸屏 |
| KeepKey | $49 | 40+ | 预算选择 |
| GridPlus Lattice1 | $399 | 无限 | 大屏幕 |

### 软件钱包

| 钱包 | 平台 | 链 | 特性 |
|--------|----------|--------|----------|
| MetaMask | 浏览器/移动 | Ethereum、EVM | 最流行、DeFi |
| Phantom | 浏览器/移动 | Solana | Solana 生态 |
| Trust Wallet | 移动 | 多链 | Binance 支持 |
| Exodus | 桌面/移动 | 多链 | 内置兑换 |
| Electrum | 桌面 | Bitcoin | 仅 Bitcoin |
| Sparrow | 桌面 | Bitcoin | 高级 Bitcoin |
| BlueWallet | 移动 | Bitcoin/Lightning | Lightning Network |
| Rainbow | 移动 | Ethereum | NFT 聚焦 |
| Rabby | 浏览器 | EVM | 多链 |

### 选择钱包

| 需求 | 推荐钱包 |
|------|-------------------|
| 最高安全性 | 硬件钱包（Ledger/Trezor） |
| 日常 DeFi 使用 | MetaMask 或 Rabby |
| 仅 Bitcoin | Sparrow 或 Electrum |
| Solana 生态 | Phantom |
| 移动便利 | Trust Wallet |
| 多链 | Trust Wallet 或 Exodus |

### 钱包安全最佳实践

| 实践 | 描述 |
|----------|-------------|
| 写下助记词 | 12-24 词恢复短语 |
| 离线存储助记词 | 永远不要数字化存储 |
| 使用多个位置 | 防火保险箱、银行金库 |
| 永远不要分享助记词 | 没有合法服务会要求 |
| 验证地址 | 发送前仔细检查 |
| 使用硬件钱包 | 大额资金 |
| 启用 2FA | 可用时 |
| 测试小额 | 首笔交易验证 |

---

## 交易所

### 中心化交易所 (CEX)

| 交易所 | 交易量 | 币种 | 费用 | 特性 |
|----------|--------|-------|------|----------|
| Binance | 最高 | 600+ | 0.1% | 最大选择 |
| Coinbase | 高 | 200+ | 0.5% | 美国监管 |
| Kraken | 高 | 200+ | 0.16% | 安全聚焦 |
| Bybit | 高 | 400+ | 0.1% | 衍生品 |
| OKX | 高 | 300+ | 0.1% | 高级交易 |
| KuCoin | 中等 | 700+ | 0.1% | 山寨币多样 |
| Bitfinex | 中等 | 200+ | 0.1% | 专业交易者 |
| Gate.io | 中等 | 1,700+ | 0.2% | 大量山寨币 |

### 去中心化交易所 (DEX)

| 交易所 | 链 | 类型 | 特性 |
|----------|-------|------|----------|
| Uniswap | Ethereum 等 | AMM | 最大 DEX |
| PancakeSwap | BNB Chain | AMM | 低费用 |
| SushiSwap | 多链 | AMM | 跨链 |
| dYdX | Ethereum | 订单簿 | 永续合约 |
| Curve | Ethereum | Stableswap | 稳定币兑换 |
| Jupiter | Solana | 聚合器 | 最佳 Solana 汇率 |
| 1inch | 多链 | 聚合器 | 最佳汇率 |
| Raydium | Solana | AMM | Solana DeFi |

### 交易所对比

| 因素 | CEX | DEX |
|--------|-----|-----|
| 托管 | 交易所持有资金 | 你持有资金 |
| KYC | 必需 | 不必需 |
| 速度 | 快 | 取决于区块链 |
| 费用 | 交易费 | Gas + 兑换费 |
| 选择 | 策划的 | 任何代币 |
| 隐私 | 低 | 高 |
| 安全 | 取决于交易所 | 你的责任 |

---

## DeFi

### DeFi 协议

| 类别 | 协议 | 链 | 描述 |
|----------|----------|-------|-------------|
| 借贷 | Aave | 多链 | 借贷 |
| 借贷 | Compound | Ethereum | 算法借贷 |
| DEX | Uniswap | Ethereum 等 | 自动做市商 |
| DEX | Curve | Ethereum | 稳定币交易 |
| 衍生品 | dYdX | Ethereum | 永续合约 |
| 衍生品 | GMX | Arbitrum | 永续交易所 |
| 稳定币 | MakerDAO | Ethereum | DAI 稳定币 |
| 收益 | Yearn | Ethereum | 收益聚合 |
| 桥接 | Wormhole | 多链 | 跨链转移 |

### DeFi 概念

| 概念 | 描述 |
|---------|-------------|
| 流动性挖矿 | 通过提供流动性赚取奖励 |
| 流动性池 | 用于交易的代币对 |
| 无常损失 | 提供流动性造成的损失 |
| 闪电贷 | 无抵押贷款（同一区块） |
| 抵押品 | 用于借贷的锁定资产 |
| 清算 | 抵押不足时强制出售 |
| 滑点 | 大额交易的价格影响 |
| MEV | 矿工/最大可提取价值 |

### 如何使用 DeFi

| 步骤 | 操作 | 工具 |
|------|--------|-------|
| 1 | 获取钱包 | MetaMask、Rabby |
| 2 | 充值钱包 | 从交易所转入 |
| 3 | 连接协议 | 访问协议网站 |
| 4 | 授权代币 | 一次性许可 |
| 5 | 执行交易 | 兑换、借出、借入 |
| 6 | 监控仓位 | 投资组合跟踪 |

### DeFi 风险

| 风险 | 描述 | 缓解措施 |
|------|-------------|------------|
| 智能合约 | 代码漏洞 | 使用已审计协议 |
| 跑路 | 团队放弃项目 | 研究团队、审计 |
| 无常损失 | 价格偏离 | 稳定币对 |
| 预言机操纵 | 价格馈送攻击 | 多预言机 |
| 清算 | 抵押品下降 | 超额抵押 |
| 监管 | 政府行动 | 分散管辖权 |

---

## NFT

### 什么是 NFT

非同质化代币是区块链上的独特数字资产。它们代表数字或物理物品的所有权。

### NFT 市场

| 市场 | 链 | 重点 | 费用 |
|-------------|-------|-------|------|
| OpenSea | 多链 | 通用 | 2.5% |
| Blur | Ethereum | 交易 | 0% |
| Magic Eden | Solana、Bitcoin | Solana、Ordinals | 2% |
| Rarible | 多链 | 艺术、收藏品 | 1% |
| Foundation | Ethereum | 策展艺术 | 5% |
| SuperRare | Ethereum | 数字艺术 | 3% |
| LooksRare | Ethereum | 社区 | 2% |

### NFT 类别

| 类别 | 示例 | 知名系列 |
|----------|----------|-------------------|
| PFP | 头像 | Bored Apes、CryptoPunks |
| 艺术 | 数字艺术品 | Art Blocks、Fidenza |
| 游戏 | 游戏内物品 | Axie Infinity、Gods Unchained |
| 音乐 | 音乐版权 | Royal、Sound.xyz |
| 域名 | Web3 域名 | ENS、Unstoppable |
| 会员 | 通行证 | VeeFriends、Proof |
| 实物 | 物理资产 | 房地产、奢侈品 |

### 创建 NFT

| 步骤 | 平台 | 描述 |
|------|----------|-------------|
| 1 | 创建艺术品 | 数字艺术、音乐、视频 |
| 2 | 选择市场 | OpenSea、Rarible、Foundation |
| 3 | 连接钱包 | MetaMask、Phantom |
| 4 | 上传文件 | 图片、视频、音频 |
| 5 | 设置元数据 | 名称、描述、属性 |
| 6 | 选择区块链 | Ethereum、Polygon、Solana |
| 7 | 设置版税 | 未来销售百分比 |
| 8 | 铸造 | 创建 NFT |

### NFT 估值因素

| 因素 | 描述 |
|--------|-------------|
| 稀有度 | 特征的独特程度 |
| 社区 | 社区的力量 |
| 实用性 | 现实世界的好处 |
| 艺术家 | 创作者声誉 |
| 地板价 | 最低挂牌价 |
| 交易量 | 交易活动 |
| 历史意义 | 文化重要性 |

---

## 交易

### 交易类型

| 类型 | 描述 | 时间框架 |
|------|-------------|-----------|
| 现货 | 买卖实际加密货币 | 任何 |
| 杠杆 | 用借入资金交易 | 短期 |
| 期货 | 未来价格的合约 | 短期 |
| 期权 | 以特定价格买卖的权利 | 不定 |
| 永续 | 无到期的期货 | 短期 |

### 技术分析

| 指标 | 描述 | 用途 |
|-----------|-------------|-----|
| 移动平均线 (MA) | 时间段平均价格 | 趋势方向 |
| RSI | 相对强弱指标 | 超买/超卖 |
| MACD | 移动平均收敛发散 | 趋势变化 |
| 布林带 | 价格波动 | 波动性 |
| 成交量 | 交易活动 | 确认 |
| 支撑/阻力 | 价格水平 | 入场/出场点 |
| 斐波那契 | 回撤水平 | 回调目标 |

### 交易策略

| 策略 | 描述 | 风险级别 |
|----------|-------------|------------|
| HODL | 长期持有 | 低 |
| DCA | 定投 | 低 |
| 波段交易 | 中期趋势 | 中等 |
| 日内交易 | 日内持仓 | 高 |
| 炒单 | 超短期 | 极高 |
| 套利 | 交易所间价差 | 低 |

### 投资组合管理

| 原则 | 描述 |
|-----------|-------------|
| 分散化 | 分散到不同资产 |
| 仓位管理 | 每笔交易的风险 |
| 止损 | 限制下行 |
| 止盈 | 锁定收益 |
| 再平衡 | 维持目标配置 |
| 风险回报比 | 最低 1:2 风险回报 |

### 投资组合追踪

| 工具 | 平台 | 特性 |
|------|----------|----------|
| CoinGecko | Web/移动 | 免费投资组合追踪 |
| CoinMarketCap | Web/移动 | 市场数据 + 投资组合 |
| DeBank | Web | DeFi 投资组合 |
| Zapper | Web | DeFi + NFT 投资组合 |
| Koinly | Web | 税务报告 |
| CoinTracker | Web | 税务 + 投资组合 |

---

## 挖矿

### 挖矿方式

| 方式 | 硬件 | 币种 | 盈利性 |
|--------|----------|-------|---------------|
| ASIC 挖矿 | 专用硬件 | BTC、LTC | 高（有竞争力时） |
| GPU 挖矿 | 显卡 | ETH Classic、RVN | 中等 |
| CPU 挖矿 | 处理器 | XMR、RTM | 低 |
| 云挖矿 | 租用硬件 | 各种 | 通常不盈利 |
| 质押 | 锁定代币 | ETH、SOL、ADA | 中等 |

### 挖矿硬件

| 硬件 | 算法 | 算力 | 功耗 | 价格 |
|----------|----------|----------|-------|-------|
| Antminer S19 XP | SHA-256 | 140 TH/s | 3010W | $5,000+ |
| Antminer L7 | Scrypt | 9.5 GH/s | 3425W | $10,000+ |
| RTX 4090 | 各种 | 不定 | 450W | $1,600 |
| RTX 3080 | 各种 | 不定 | 320W | $500 |

### 矿池

| 矿池 | 币种 | 费用 | 支付 |
|------|-------|-----|--------|
| Foundry USA | BTC | 0% | PPS+ |
| Antpool | BTC、LTC | 2% | PPLNS |
| F2Pool | 多种 | 2.5% | PPS+ |
| Ethermine | ETH Classic | 1% | PPLNS |
| ViaBTC | 多种 | 2% | PPS+ |

### 权益证明

| 网络 | 最低质押 | 年化收益 | 锁定期 |
|---------|--------------|--------------|-------------|
| Ethereum | 32 ETH | 4-5% | 不定 |
| Cardano | 无 | 4-5% | 无 |
| Solana | 无 | 6-7% | ~3 天 |
| Polkadot | 10 DOT | 14% | 28 天 |
| Cosmos | 无 | 15-20% | 21 天 |

### 挖矿盈利因素

| 因素 | 影响 |
|--------|--------|
| 电费 | 最大开支 |
| 硬件效率 | 每瓦算力 |
| 网络难度 | 随时间增加 |
| 币价 | 收入变化 |
| 矿池费用 | 减少收益 |
| 散热成本 | 额外开支 |

---

## 安全

### 常见骗局

| 骗局 | 描述 | 预防 |
|------|-------------|------------|
| 钓鱼 | 假网站/邮件 | 验证 URL、使用书签 |
| 跑路 | 团队放弃项目 | 研究团队、审计 |
| 拉高出货 | 人为抬高价格 | 避免炒作 |
| 假客服 | 冒充支持 | 永远不要分享助记词 |
| 庞氏骗局 | 新投资者的回报 | 好得难以置信 |
| SIM 卡劫持 | 接管手机号 | 使用认证器应用 |
| 假空投 | 偷取的免费代币 | 永远不要授权未知代币 |

### 安全清单

| 实践 | 描述 |
|----------|-------------|
| 使用硬件钱包 | 大额资金 |
| 启用 2FA | 所有账户 |
| 使用唯一密码 | 密码管理器 |
| 验证地址 | 发送前 |
| 检查 URL | 钓鱼网站看起来很像 |
| 审查权限 | 撤销未使用的授权 |
| 小额测试交易 | 大额转账前 |
| 保持软件更新 | 钱包和系统更新 |

### DeFi 安全

| 实践 | 描述 |
|----------|-------------|
| 检查审计 | 查看安全审计 |
| 从小额开始 | 用小额测试 |
| 分散投资 | 不要把所有放在一个协议 |
| 监控仓位 | 定期检查 |
| 使用知名协议 | 成熟的记录 |
| 了解风险 | 阅读文档 |

### 被入侵后怎么办

| 步骤 | 操作 |
|------|--------|
| 1 | 将剩余资金转移到新钱包 |
| 2 | 撤销所有代币授权 |
| 3 | 更改密码 |
| 4 | 启用新的 2FA |
| 5 | 向相关平台报告 |
| 6 | 记录一切 |
| 7 | 向当局报告 |

---

## 监管

### 监管格局

| 地区 | 状态 | 要点 |
|--------|--------|------------|
| 美国 | 不断演变 | SEC 监管、州法律 |
| 欧盟 | MiCA 框架 | 综合监管 |
| 英国 | 发展中 | FCA 监管 |
| 日本 | 先进 | 持牌交易所 |
| 新加坡 | 渐进式 | MAS 监管 |
| 阿联酋 | 支持性 | 迪拜自由区 |
| 中国 | 限制性 | 挖矿禁令、交易禁令 |
| 印度 | 征税 | 30% 收益税 |

### 税务考虑

| 事件 | 应税 | 报告 |
|-------|---------|-----------|
| 购买加密 | 否 | 跟踪成本基础 |
| 出售加密 | 是 | 资本利得 |
| 交易加密 | 是 | 资本利得 |
| 接收付款 | 是 | 收入 |
| 挖矿奖励 | 是 | 收入 |
| 质押奖励 | 是 | 收入 |
| 空投 | 是 | 收入 |
| 礼物 | 不定 | 礼物税规则 |

### 合规建议

| 实践 | 描述 |
|----------|-------------|
| 保留记录 | 每笔交易 |
| 使用税务软件 | Koinly、CoinTracker |
| 报告所有收入 | 即使小额 |
| 咨询专业人士 | 熟悉加密的税务顾问 |
| 保存报表 | 交易所报告 |
| 跟踪成本基础 | FIFO、LIFO 或特定识别 |

---

## 研究工具

### 市场数据

| 工具 | 特性 | 费用 |
|------|----------|------|
| CoinGecko | 价格、市值、交易量 | 免费 |
| CoinMarketCap | 市场数据、排名 | 免费 |
| Messari | 研究、数据、新闻 | 免费增值 |
| TradingView | 图表、技术分析 | 免费增值 |
| Glassnode | 链上分析 | 免费增值 |
| Dune Analytics | 自定义区块链查询 | 免费 |

### 链上分析

| 工具 | 重点 | 特性 |
|------|-------|----------|
| Etherscan | Ethereum | 交易、合约 |
| Solscan | Solana | 交易、代币 |
| Blockchain.com | Bitcoin | 交易、图表 |
| Whale Alert | 大额交易 | 巨鲸追踪 |
| Arkham | 实体标签 | 谁在买卖 |

### 研究平台

| 平台 | 重点 | 内容 |
|----------|-------|---------|
| Messari | 研究报告 | 机构研究 |
| Delphi Digital | 研究 | 深度分析 |
| The Block Research | 新闻和数据 | 行业研究 |
| Galaxy Digital Research | 机构 | 市场分析 |
| a16z Crypto | VC 研究 | 行业趋势 |

### 代币分析

| 指标 | 描述 | 来源 |
|--------|-------------|--------|
| 市值 | 总价值 | CoinGecko |
| 完全稀释价值 | 如果所有代币都存在 | CoinGecko |
| 交易量/市值 | 交易活动 | CoinGecko |
| TVL | 总锁仓价值（DeFi） | DefiLlama |
| 活跃地址 | 网络使用 | Glassnode |
| 算力 | 网络安全 | Blockchain.com |

---

## 新闻来源

### 加密新闻网站

| 来源 | 重点 | 风格 |
|--------|-------|-------|
| CoinDesk | 通用加密新闻 | 专业 |
| The Block | 行业新闻 | 深度 |
| Decrypt | 通用加密新闻 | 易读 |
| Cointelegraph | 通用加密新闻 | 视觉化 |
| Blockworks | 机构聚焦 | 专业 |
| The Defiant | DeFi 新闻 | DeFi 聚焦 |
| DL News | 行业新闻 | 调查性 |

### 通讯

| 通讯 | 重点 | 频率 |
|------------|-------|-----------|
| Bankless | DeFi、Ethereum | 每日/每周 |
| The Daily Gwei | Ethereum、DeFi | 每日 |
| Milk Road | 通用加密 | 每日 |
| CoinSnacks | 市场回顾 | 每周 |
| Messari Daily | 市场分析 | 每日 |
| The Pomp Letter | 宏观、Bitcoin | 每日 |

### 播客

| 播客 | 重点 | 主持 |
|---------|-------|------|
| Bankless | DeFi、Ethereum | Ryan Sean Adams |
| Unchained | 行业新闻 | Laura Shin |
| What Bitcoin Did | Bitcoin | Peter McCormack |
| The Delphi Podcast | 行业分析 | Delphi Digital |
| Empire | 加密商业 | Jason Yanowitz |
| On The Brink | Bitcoin、宏观 | Castle Island |

### YouTube 频道

| 频道 | 重点 | 风格 |
|---------|-------|-------|
| Coin Bureau | 市场分析 | 教育 |
| Whiteboard Crypto | 概念讲解 | 动画 |
| Finematics | DeFi 讲解 | 动画 |
| Benjamin Cowen | 市场分析 | 数据驱动 |
| InvestAnswers | 市场分析 | 数据驱动 |

---

## 社区

### 在线社区

| 平台 | 社区 | 重点 |
|----------|-----------|-------|
| Reddit | r/cryptocurrency | 通用讨论 |
| Reddit | r/bitcoin | Bitcoin 讨论 |
| Reddit | r/ethereum | Ethereum 讨论 |
| Twitter/X | Crypto Twitter | 新闻、观点 |
| Discord | 协议服务器 | 项目社区 |
| Telegram | 各种群组 | 实时聊天 |
| Farcaster | Web3 社交 | 去中心化社交 |

### 开发者社区

| 社区 | 平台 | 重点 |
|-----------|----------|-------|
| Ethereum Stack Exchange | Stack Exchange | Ethereum 开发 |
| Solidity docs | 文档 | 智能合约 |
| Alchemy University | 在线课程 | Web3 开发 |
| Chainlink | Discord | 预言机开发 |
| OpenZeppelin | GitHub | 智能合约安全 |

### 会议

| 会议 | 地点 | 重点 |
|------------|----------|-------|
| Consensus | 美国 | 行业 |
| Token2049 | 新加坡/伦敦 | 行业 |
| ETHDenver | 美国 | Ethereum |
| Bitcoin Miami | 美国 | Bitcoin |
| Devcon | 各地 | Ethereum 开发 |
| Solana Breakpoint | 各地 | Solana |

### 教育平台

| 平台 | 重点 | 类型 |
|----------|-------|------|
| Binance Academy | 通用加密 | 免费课程 |
| CoinGecko Learn | 通用加密 | 免费课程 |
| Coinbase Learn | 通用加密 | 免费课程 |
| Bankless | DeFi、Ethereum | 付费会员 |
| Messari Hub | 研究 | 免费增值 |

---

## 入门指南

### 分步指南

| 步骤 | 操作 | 推荐 |
|------|--------|----------------|
| 1 | 学习基础 | 阅读本指南、观看视频 |
| 2 | 选择交易所 | Coinbase（美国）、Binance（全球） |
| 3 | 验证身份 | 完成 KYC |
| 4 | 充值 | 银行转账或卡 |
| 5 | 购买 Bitcoin/Ethereum | 从主流币开始 |
| 6 | 获取硬件钱包 | Ledger 或 Trezor |
| 7 | 转移到钱包 | 自我托管 |
| 8 | 继续学习 | 投入更多前先研究 |

### 投资原则

| 原则 | 描述 |
|-----------|-------------|
| 只投资你能承受损失的 | 加密波动大 |
| 做自己的研究 | 永远不要盲目跟风 |
| 从小额开始 | 学习后再投入更多 |
| 分散投资 | 不要把所有鸡蛋放一个篮子 |
| 长期思考 | 短期交易风险大 |
| 忽略 FOMO | 错失恐惧导致糟糕决策 |
| 保持信息 | 关注新闻和发展 |

### 危险信号

| 危险信号 | 描述 |
|----------|-------------|
| 保证回报 | 没有投资保证利润 |
| 名人代言 | 通常是付费推广 |
| 匿名团队 | 无问责 |
| 无可用产品 | 只有承诺 |
| 购买压力 | 紧迫感策略 |
| 不切实际的承诺 | 好得难以置信 |
| 无审计 | 未测试的代码 |

---

## 总结

加密货币生态系统庞大且快速发展。本指南涵盖了你需要安全有效地导航它的基本资源和概念。

关键要点：
- 从理解区块链基础开始
- 使用硬件钱包保障安全
- 选择信誉良好的交易所
- 投资前研究任何项目
- 保留税务记录
- 与社区保持联系
- 永远不要投资超过你能承受损失的

这个领域奖励持续学习。保持好奇、保持谨慎，始终做自己的研究。


---

## 来源：chain.md

## 一、核心安全法则

| 法则 | 含义 |
|------|------|
| **零信任** | 保持怀疑，始终保持怀疑 |
| **持续验证** | 对怀疑的点有能力去验证，并养成习惯 |

---

## 二、整体流程概览

加密货币安全涉及三大流程：

```
创建钱包 → 备份钱包 → 使用钱包
```

每个流程都有对应的安全要点，下文逐一展开。

---

## 三、创建钱包

### 3.1 核心概念

钱包的核心是**私钥**（或**助记词**）。

| 类型 | 示例 |
|------|------|
| 私钥 | `0xa164d4767469de4faf09793ceea07d5a2f5d3cef7f6a9658916c581829ff5584` |
| 助记词 | `cruel weekend spike point innocent dizzy alien use evoke shed adjust wrong` |

**关键原则**：私钥即身份。私钥丢失或被盗 = 身份丧失。

### 3.2 钱包分类

| 类型 | 说明 | 特点 |
|------|------|------|
| PC 钱包 | 桌面端应用 | 功能丰富，需注意系统安全 |
| 浏览器扩展钱包 | 如 MetaMask | 便捷，需从官方商店下载 |
| 移动端钱包 | 手机 App | 随身携带，注意应用商店分区 |
| 硬件钱包 | 如 Ledger、Trezor | 离线存储私钥，安全性高 |
| 网页钱包 | 在线使用 | 风险最高，不建议长期使用 |

按联网状态分为：

| 类型 | 说明 |
|------|------|
| 冷钱包 | 不联网，安全性高 |
| 热钱包 | 联网，使用便捷 |

**安全原则**：做好隔离，鸡蛋不要放在一个篮子里。

### 3.3 下载安全

**问题**：许多人找不到正确官网，安装了假钱包。

**验证官网的方法**：

| 方法 | 说明 |
|------|------|
| Google 搜索 | 注意搜索结果中的广告条目不可靠 |
| CoinMarketCap | 行业知名收录平台 |
| 多方验证 | 询问多个可信来源，互相佐证 |

**文件完整性校验**：

| 方式 | 说明 |
|------|------|
| 哈希校验 | 使用 SHA256 验证文件未被篡改 |
| GPG 签名校验 | 使用 GPG 工具验证签名 |

**各平台下载注意事项**：

| 平台 | 注意事项 |
|------|----------|
| PC 钱包 | 下载后做完整性校验 |
| 浏览器扩展 | 查看用户数、评分，如 MetaMask 超千万用户 |
| 移动端 | iPhone 注意 App Store 分区，中国区可能下不到正版 |
| 硬件钱包 | 从官网购买，到手后检查是否被拆封 |
| 网页钱包 | 尽量避免使用，如必须则速战速决 |

### 3.4 助记词标准

助记词遵循 BIP39 标准：

| 规格 | 说明 |
|------|------|
| 单词数量 | 12/15/18/21/24 个（3 的倍数，不超过 24） |
| 常用数量 | 12 位（安全性足够），24 位（如 Ledger） |
| 语言 | 英文、中文、日文、韩文等 |
| 词表 | 固定 2048 个单词 |

**创建时注意事项**：

- 确保身边无人、无摄像头等偷窥风险
- 确认助记词随机性足够
- 如作为冷钱包使用，可考虑断网创建

### 3.5 Keyless 方案

| 类型 | 说明 | 示例 |
|------|------|------|
| Custodial（托管） | 用户不拥有私钥，依托中心化平台 | 中心化交易所 |
| Non-Custodial（非托管） | 用户掌握类似私钥的权力，但非直接私钥 | MPC 方案、Cloud 托管 |

**MPC（安全多方计算）优势**：

- 私钥从不出现，通过多方计算解决单点风险
- 一套方案可通用多链多签
- 结合知名云平台，安全与体验兼顾

**MPC 代表项目**：ZenGo、Fireblocks、Safeheron

---

## 四、备份钱包

### 4.1 备份类型

| 类型 | 说明 | 风险 |
|------|------|------|
| **明文** | 直接记录助记词 | 可考虑乱序或替换单词，但需牢记规律 |
| **带密码** | 助记词 + 密码生成种子 | 密码也需备份，忘记则无法恢复 |
| **多签** | 多人签名授权才能使用 | 避免单点风险，但管理复杂 |
| **SSS** | 秘密共享方案，分片存储 | 恢复需指定数量分片 |

**SSS 参考**：
- Keystone SSS 指南: https://guide.keyst.one/zh/docs/shamir-backup
- Trezor SSS 指南: https://wiki.trezor.io/Shamir_backup

### 4.2 加密与备份位置

**加密建议**：使用 GPG 加密后存储备份。

**备份位置**：

| 位置 | 说明 | 注意事项 |
|------|------|----------|
| **Cloud** | Google、Apple、微软等云服务 | 加密后再上传，GPG 私钥和密码也要备份 |
| **Paper** | 纸质/钢板抄写 | 寿命长于电子设备，存放在安全位置 |
| **Device** | 电脑、U盘、移动硬盘等 | 每年至少检查一次，传输用 AirDrop/USB |
| **Brain** | 脑记 | 存在记忆淡忘/错乱风险，存在意外风险 |

**灾备原则**：

- 避免单点风险
- 重要数据多处备份
- 设有灾备人

**定期验证**：根据安全法则"持续验证"，定期检查备份是否可用。

---

## 五、使用钱包

### 5.1 AML（反洗钱）

持有的加密货币可能存在 AML 风险：

| 风险 | 说明 |
|------|------|
| 资金来源不干净 | 交易对手的币可能涉及非法活动 |
| 链上冻结 | USDT 等可被发行方冻结 |

**USDT 冻结查询**：
- 在 Etherscan USDT 合约的 `isBlackListed` 输入地址查询
- 地址: https://etherscan.io/token/0xdac17f958d2ee523a2206206994597c13d831ec7#readContract

**防御建议**：选择口碑好的平台和个人作为交易对手。

### 5.2 冷钱包使用

**接收**：配合观察钱包（如 imToken、OneKey、Trust Wallet）即可。

**发送流程**：

```
Light App（联网）→ 待签名内容 → 冷钱包（离线签名）→ 签名内容 → Light App → 广播上链
```

传输方式：QRCode、USB、Bluetooth。

**冷钱包风险**：

| 风险 | 说明 |
|------|------|
| 目标地址被替换 | 坏人生成头尾相似的地址进行替换 |
| 无限授权 | 未限制 approve 数量，代币可被转走 |
| 盲签陷阱 | 签名内容不透明，藏有恶意操作 |
| 信息展示不足 | 冷钱包屏幕有限，可能遗漏关键信息 |

**核心原则**：所见即所签。

### 5.3 热钱包使用

热钱包在冷钱包风险基础上，额外存在**助记词/私钥被盗风险**。

**热钱包版本风险**：

| 作恶方式 | 说明 |
|----------|------|
| 助记词上传 | 恶意代码将助记词打包上传到黑客服务器 |
| 替换转账信息 | 后台偷偷替换目标地址和金额 |
| 破坏随机数 | 让生成的助记词容易被破解 |

**安全建议**：对存有重要资产的钱包，不做轻易更新，够用就好。

### 5.4 DeFi 安全

DeFi 安全至少包括七个方面：

| 方面 | 说明 |
|------|------|
| 智能合约安全 | 安全审计的核心切入点 |
| 区块链基础安全 | 共识账本、虚拟机安全 |
| 前端安全 | 防止页面被篡改、注入恶意代码 |
| 通信安全 | HTTPS、防中间人攻击 |
| 人性安全 | 防止内部作恶、社会工程学 |
| 金融安全 | 防止不公平启动、巨鲸攻击、闪电贷攻击等 |
| 合规安全 | AML、KYC、制裁地区限制等 |

#### 智能合约权限风险

**问题**：项目方权限过大可能作恶。

**缓解方案**：

| 方案 | 说明 | 示例 |
|------|------|------|
| Timelock（时间锁） | 关键操作延迟执行，用户有时间反应 | Compound 的 48 小时时间锁 |
| 多签 | 多人签名才能执行关键操作 | Gnosis Safe |

**注意**：多签和 Timelock 都可能存在"皇帝的新衣"问题——表面合规，实际有后门。

#### 前端安全风险

| 风险类型 | 说明 |
|----------|------|
| 内部作恶 | 开发人员替换合约地址或植入钓鱼脚本 |
| 供应链作恶 | 第三方依赖被植入后门 |
| 远程 JS 作恶 | 引入的外部 JavaScript 文件被篡改 |

**防御机制**：使用 SRI（Subresource Integrity）完整性校验。

```html
<script src="https://example.com/lib.js" integrity="sha384-..." crossorigin="anonymous"></script>
```

参考：https://developer.mozilla.org/zh-CN/docs/Web/Security/Subresource_Integrity

#### 通信安全

**核心规则**：遇到 HTTPS 证书错误，立即停止访问。

**历史案例**：2018 年 MyEtherWallet 遭 BGP 劫持，用户忽略证书错误后私钥被盗。

**项目方应配置 HSTS**（HTTP Strict Transport Security），强制浏览器在证书错误时阻止访问。

### 5.5 NFT 安全

NFT 在 DeFi 安全基础上，额外关注：

| 方面 | 说明 |
|------|------|
| Metadata 安全 | 图片 URI 应使用 IPFS/Arweave 等去中心化存储 |
| 签名安全 | 防止盲签导致 NFT 被盗 |

**Metadata 标准参考**：https://docs.opensea.io/docs/metadata-standards

### 5.6 签名安全

**最大原则**：所见即所签。

**盲签问题**：

MetaMask 弹出的签名窗口显示信息有限（账户、余额、来源网站、签名消息），用户无法判断签名的真实含义。

**历史事件**：2022 年 2 月 OpenSea 集中爆发 NFT 被盗事件，根因是用户盲签。

**防御措施**：

| 措施 | 说明 |
|------|------|
| 拒绝盲签 | 确保了解签名内容的真实含义 |
| 使用 EIP-712 | 结构化签名，显示可读内容 |
| 取消授权 | 使用工具检查并取消不必要的授权 |

**授权检查/取消工具**：

| 工具 | 地址 |
|------|------|
| Token Approvals（Etherscan） | https://etherscan.io/tokenapprovalchecker |
| Revoke.cash | https://revoke.cash/ |
| Rabby 钱包 | https://rabby.io/ |

### 5.7 反常识签名风险

**问题**：不同链的签名机制不同，跨链时容易因惯性思维中招。

**案例**：Solana 上的授权钓鱼

- 恶意合约在用户 Approve 后可转走原生资产（SOL）
- 这在以太坊上不可能（以太坊授权只能钓走 Token，不能钓走 ETH）
- Phantom 钱包在"所见即所签"上存在缺陷

**教训**：跨链时不要用惯性思维，需了解目标链的特殊机制。

### 5.8 高级攻击方式

| 攻击方式 | 说明 |
|----------|------|
| 邮件钓鱼 | 附带恶意文档（Office 宏/0day），植入木马 |
| 钱包替换 | 木马将 MetaMask 替换为有后门的版本 |
| 域名钓鱼 | 使用 Punycode 注册相似域名（如 trezor 的变体） |
| Cloudflare Workers 劫持 | 控制项目方 Cloudflare 账号后注入恶意脚本 |
| XSS/CSRF/Reverse Proxy | 结合多种 Web 攻击技巧 |

**木马常见功能**：

| 功能 | 说明 |
|------|------|
| 凭证采集 | 浏览器密码、SSH 密钥等 |
| 键盘记录 | 采集密码等敏感输入 |
| 截屏/文件采集 | 获取敏感信息 |
| 钱包定向攻击 | 替换钱包应用、篡改转账信息 |

---

## 六、传统隐私保护

### 6.1 操作系统

| 系统 | 建议 |
|------|------|
| Windows 10+ | 安全性足够，及时更新 |
| macOS | 安全性足够，及时更新 |
| Linux | 适合高级用户，如 Ubuntu、Tails、Whonix |

**安全措施**：

| 措施 | 说明 |
|------|------|
| 系统更新 | 有安全更新立即安装 |
| 杀毒软件 | 卡巴斯基、BitDefender 等 |
| 磁盘加密 | Windows: BitLocker；macOS: FileVault |
| BIOS/固件密码 | 防止物理接触后的攻击 |

### 6.2 手机

| 平台 | 建议 |
|------|------|
| iPhone | 安全性较高，建议使用 |
| Android | 安全性逐步改善，注意版本碎片化 |

**注意事项**：

- 不要越狱/Root
- 不从非官方市场下载 App
- 云同步需确保账号安全

### 6.3 网络

| 建议 | 说明 |
|------|------|
| 不连陌生 Wi-Fi | 优先使用 4G/5G |
| HTTPS 优先 | 遇到证书错误立即停止 |
| 敏感设备独立网络 | 高安全需求时考虑 |

### 6.4 浏览器

| 建议 | 说明 |
|------|------|
| 及时更新 | 有更新就安装 |
| 谨慎安装扩展 | 来自官方商店，查看口碑和用户量 |
| 浏览器隔离 | 重要操作用一个浏览器，日常用另一个 |
| 隐私扩展 | uBlock Origin、HTTPS Everywhere、ClearURLs 等 |

### 6.5 密码管理器

**推荐工具**：1Password、Bitwarden

| 工具 | 特点 |
|------|------|
| 1Password | 闭源，安全审计报告公开，支持 2FA |
| Bitwarden | 全开源（含服务端），可自行验证 |

**注意事项**：

- 千万别忘记主密码
- 确保注册邮箱安全
- 做好 2FA 备份

### 6.6 双因素认证（2FA）

| 工具 | 说明 |
|------|------|
| Google Authenticator | 最常用 |
| Microsoft Authenticator | 微软出品 |
| 1Password | 自带 2FA 功能 |

**注意**：2FA 丢失很麻烦，务必做好备份。

### 6.7 邮箱

| 类型 | 推荐 |
|------|------|
| 主流邮箱 | Gmail、Outlook、QQ 邮箱 |
| 隐私邮箱 | ProtonMail、Tutanota（用于敏感服务注册） |

**安全提醒**：

- 警惕邮件中的钓鱼链接和附件
- 长期不活跃的免费邮箱可能被回收

### 6.8 SIM 卡

**风险**：SIM Port Attack（SIM 卡转移攻击）

攻击者通过社会工程学获取用户隐私，到运营商骗取新 SIM 卡，进而接管用户账号。

**防御措施**：

| 措施 | 说明 |
|------|------|
| 启用 2FA | 使用独立 2FA 工具，不依赖短信验证码 |
| SIM 卡 PIN 码 | 设置 SIM 卡密码，防止手机丢失后被使用 |

### 6.9 GPG

**概念区分**：

| 名称 | 说明 |
|------|------|
| PGP | 商用加密软件，在赛门铁克麾下 |
| OpenPGP | 加密标准，衍生自 PGP |
| GPG (GnuPG) | 基于 OpenPGP 的开源加密软件 |

**用途**：

- 文件加密（备份钱包时使用）
- 签名验证（验证下载文件完整性）

**入门参考**：https://www.ruanyifeng.com/blog/2013/07/gpg.html

### 6.10 隔离环境

**核心思想**：零信任思维，被黑时损失仅限于被黑目标。

| 隔离方式 | 说明 |
|----------|------|
| 密码隔离 | 不同账号使用不同密码 |
| 钱包隔离 | 不同用途使用不同钱包 |
| 设备隔离 | 敏感操作与日常操作分开 |
| 虚拟机 | 使用 VMware、Parallels 等 |

---

## 七、人性安全

### 7.1 Telegram 风险

| 风险 | 说明 |
|------|------|
| 假客服私聊 | 任意私聊是 Telegram 机制，无需好友 |
| 群克隆 | 拉你进群，除你之外全是仿冒账号 |
| 钓鱼 Bot | 定制化 Bot 服务进行诈骗 |

### 7.2 Discord 风险

**核心风险**：Discord Token

- Discord Token 是 HTTP 请求头中的 authorization 字段
- 拿到 Token 即可几乎完全控制目标账号
- **2FA 对此攻击无效**

**防御措施**：

- 不急不贪、多方验证
- 如中招，立即更改 Discord 密码（Token 会刷新）

### 7.3 来自"官方"的钓鱼

| 手法 | 说明 |
|------|------|
| 域名后缀不同 | 如 trezor.us 代替 trezor.io |
| Punycode | 使用 Unicode 相似字符，如特殊字符代替正常字母 |
| 邮件伪造 | SPF 配置问题导致的邮件伪造 |
| 内部人作恶 | 项目方人员安全意识差 |

### 7.4 Web3 隐私问题

将各种 Web3 项目玩一遍后，碎片信息可拼出完整画像：

- 收藏哪些 NFT
- 加入哪些社群
- 在哪些白名单里
- 绑定了哪些 Web2 账号
- 活跃时间段

**建议**：谨慎对待新事物，保持隔离身份的好习惯。

---

## 八、电脑中毒应急处理

### 常见投毒手法

| 手法 | 说明 |
|------|------|
| 假会议软件 | 假装投资人/记者/HR，诱导安装 |
| Telegram Safeguard | 诱导黏贴恶意代码运行 |
| Cloudflare 验证 | 诱导黏贴恶意代码运行 |

### 中毒后处理步骤

| 步骤 | 操作 |
|------|------|
| 1. 转移资金 | 钱包内资金立即安全转移 |
| 2. 更改密码 | 所有重要账号改密码、改 2FA，排查未知登录 |
| 3. 查杀病毒 | 使用 AVG/Bitdefender/Kaspersky/Malwarebytes |
| 4. 重置系统 | 如不放心，备份重要文件后重置电脑 |

**注意**：Mac 电脑同样可能中毒，不限于 Windows。

---

## 九、被盗应急处理

### 9.1 止损

| 阶段 | 操作 |
|------|------|
| 眼前阶段 | 抢着转移剩余资产，联系冻结，联系中心化平台风控 |
| 控制后阶段 | 防止二次、三次伤害 |

### 9.2 保护现场

| 操作 | 说明 |
|------|------|
| 断网不关机 | 联网设备立即断网，保持电源供电 |
| 等待取证 | 除非自己有能力，否则等待专业安全人员 |

### 9.3 分析原因

**事故报告要素**：

| 要素 | 内容 |
|------|------|
| 概要 1 | 什么人、什么时间、什么事、总损失 |
| 概要 2 | 钱包地址、黑客地址、币种、数量（表格形式） |
| 过程描述 | 事故过程细节，输出黑客画像 |

### 9.4 追踪溯源

| 类型 | 内容 |
|------|------|
| 链上情报 | 资金走向分析、交易所/混币平台监控 |
| 链下情报 | IP、设备信息、邮箱、行为信息 |

### 9.5 需要掌握的能力

- 智能合约安全分析及取证
- 链上资金转移分析及取证
- Web/服务器/系统安全分析及取证
- 恶意代码分析及取证
- 人员安全分析及取证

---

## 十、常见误区

| 误区 | 真相 |
|------|------|
| **Code Is Law** | 被黑或跑路时，受害者最终依赖真法律 |
| **Not Your Keys, Not Your Coins** | 拿到私钥却驾驭不好，币反而更危险；大平台有时更安全 |
| **In Blockchain We Trust** | 不是所有区块链都安全，人性是最大突破点 |
| **密码学安全 = 安全** | 密码学安全不等于系统安全，攻击面远不止密码学 |
| **被黑很丢人** | 被黑是 100% 普遍现象，丢人的是傲慢 |
| **立即更新总是对的** | 更新可能引入新问题；重要钱包不做轻易更新 |

---

## 十一、安全法则与原则汇总

### 两大法则

| 法则 | 含义 |
|------|------|
| 零信任 | 保持怀疑，始终保持怀疑 |
| 持续验证 | 有能力验证怀疑的点，养成习惯 |

### 安全原则

| 原则 | 说明 |
|------|------|
| 多源验证 | 网络知识参考至少两个来源，互相佐证 |
| 隔离 | 鸡蛋不放在一个篮子里 |
| 谨慎更新 | 重要资产钱包不做轻易更新 |
| 所见即所签 | 签名内容与预期一致 |
| 及时更新系统 | 系统安全更新立即安装 |
| 不乱下载 | 杜绝大多数风险 |

---

## 十二、推荐资源

### 官方网站

| 项目 | 地址 |
|------|------|
| SlowMist | https://www.slowmist.com |
| CoinMarketCap | https://coinmarketcap.com/ |
| MetaMask | https://metamask.io/ |
| imToken | https://token.im/ |
| Trust Wallet | https://trustwallet.com/ |
| OneKey | https://onekey.so/ |
| Rabby | https://rabby.io/ |
| Ledger | https://www.ledger.com/ |
| Trezor | https://trezor.io/ |
| Keystone | https://keyst.one/ |
| Gnosis Safe | https://gnosis-safe.io/ |
| ZenGo | https://zengo.com/ |
| Fireblocks | https://www.fireblocks.com/ |
| Safeheron | https://www.safeheron.com/ |
| Phantom | https://phantom.app/ |
| EdgeWallet | https://edge.app/ |
| MyEtherWallet | https://www.myetherwallet.com/ |
| OpenSea | https://opensea.io/ |
| Revoke.cash | https://revoke.cash/ |
| Compound | https://compound.finance/ |
| SushiSwap | https://www.sushi.com/ |
| Tornado Cash | https://tornado.cash/ |
| Binance | https://www.binance.com/ |
| Coinbase | https://coinbase.com |

### 安全工具

| 工具 | 地址 | 用途 |
|------|------|------|
| Scam Sniffer | https://www.scamsniffer.io/ | 钓鱼检测 |
| Wallet Guard | https://www.walletguard.app/ | 钱包安全扩展 |
| Pocket Universe | https://www.pocketuniverse.app/ | 交易安全 |
| 1Password | https://1password.com/ | 密码管理 |
| Bitwarden | https://bitwarden.com/ | 密码管理（开源） |
| Google Authenticator | https://support.google.com/accounts/answer/1066447 | 2FA |
| Microsoft Authenticator | https://www.microsoft.com/en-us/security/mobile-authenticator-app | 2FA |

### 杀毒软件

| 软件 | 地址 |
|------|------|
| AVG | https://www.avg.com/ |
| Bitdefender | https://www.bitdefender.com/ |
| Kaspersky | https://www.kaspersky.com.cn/ |
| Malwarebytes | https://www.malwarebytes.com/ |

### 隐私工具

| 工具 | 地址 | 用途 |
|------|------|------|
| GPG | https://gnupg.org/ | 加密/签名 |
| GPG Suite | https://gpgtools.org/ | macOS GPG |
| Gpg4win | https://www.gpg4win.org/ | Windows GPG |
| ProtonMail | https://protonmail.com/ | 隐私邮箱 |
| Tutanota | https://tutanota.com/ | 隐私邮箱 |
| EFF SSD | https://ssd.eff.org/ | 监控自卫指南 |
| Privacy Guide | https://www.privacytools.io/ | 隐私工具集 |

### 虚拟机

| 工具 | 地址 |
|------|------|
| VMware Workstation | https://www.vmware.com/products/workstation-pro.html |
| Parallels | https://www.parallels.com/ |

### 被黑档案库

| 资源 | 地址 |
|------|------|
| SlowMist Hacked | https://hacked.slowmist.io/ |
| 区块链作恶思维导图 | https://github.com/slowmist/Knowledge-Base/blob/master/mindmaps/evil_blockchain.png |


---

## 来源：mining.md

## 目录

1. [加密挖矿简介](#introduction)
2. [NiceHash 平台概述](#nicehash)
3. [QuickMiner 安装](#installation)
4. [配置与优化](#configuration)
5. [挖矿算法](#algorithms)
6. [盈利能力与收益](#profitability)
7. [硬件推荐](#hardware)
8. [故障排除](#troubleshooting)

---

## 简介

加密货币挖矿利用计算能力验证交易并获得奖励。NiceHash 提供一个市场，矿工在其中出售算力给买家。

### 挖矿基础

| 概念 | 描述 | 示例 |
|------|------|------|
| 算力 | 计算速度 | MH/s, GH/s |
| 算法 | 工作量证明方法 | DaggerHashimoto |
| 矿池 | 矿工群体 | NiceHash 矿池 |
| 奖励 | 工作报酬 | 比特币支付 |
| 难度 | 网络挑战级别 | 自动调整 |

### 挖矿 vs 购买加密货币

| 方面 | 挖矿 | 购买 |
|------|------|------|
| 初始成本 | 硬件投资 | 交易所购买 |
| 持续成本 | 电费 | 无 |
| 风险 | 硬件折旧 | 价格波动 |
| 收入 | 稳定（如果盈利） | 投机性 |
| 控制 | 完全硬件 | 无硬件 |

### NiceHash 工作原理

| 步骤 | 操作 | 结果 |
|------|------|------|
| 1 | 安装 QuickMiner | 软件就绪 |
| 2 | 硬件基准测试 | 最优算法 |
| 3 | 开始挖矿 | 出售算力 |
| 4 | 赚取比特币 | 每日支付 |

---

## NiceHash 平台概述

NiceHash 是一个连接矿工和买家的算力市场。

### NiceHash 服务

| 服务 | 描述 | 用途 |
|------|------|------|
| QuickMiner | 简单挖矿软件 | 初学者 |
| Miner | 高级挖矿 | 有经验的矿工 |
| Marketplace | 买卖算力 | 交易者 |
| Exchange | 加密货币交易 | 交易者 |
| Wallet | 存储收益 | 所有用户 |

### 账号设置

| 步骤 | 操作 | 要求 |
|------|------|------|
| 1 | 注册 | 邮箱地址 |
| 2 | 验证邮箱 | 确认链接 |
| 3 | 设置 2FA | 安全 |
| 4 | 配置钱包 | 比特币地址 |
| 5 | 下载矿工 | QuickMiner |

### 支付方式

| 方式 | 最低金额 | 费用 | 速度 |
|------|----------|------|------|
| Bitcoin | 0.001 BTC | 低 | 1-2 天 |
| Lightning | 0.00001 BTC | 极低 | 即时 |
| Coinbase | $1 | 免费 | 即时 |

### NiceHash 费用

| 费用类型 | 费率 | 描述 |
|----------|------|------|
| 挖矿费 | 2% | 从收益中扣除 |
| 提现 | 不定 | 网络费 |
| 交易 | 0.1-0.5% | 交易所交易 |

---

## QuickMiner 安装

QuickMiner 是使用 NiceHash 开始挖矿最简单的方式。

### 系统要求

| 组件 | 最低 | 推荐 |
|------|------|------|
| 操作系统 | Windows 10 | Windows 11 |
| GPU | NVIDIA GTX 1060 | RTX 3060+ |
| 内存 | 4GB | 8GB+ |
| 存储 | 500MB | 1GB |
| 网络 | 1 Mbps | 5+ Mbps |

### 安装步骤

| 步骤 | 操作 | 备注 |
|------|------|------|
| 1 | 下载 | nicehash.com/download |
| 2 | 运行安装程序 | 接受提示 |
| 3 | 登录 | NiceHash 账号 |
| 4 | 基准测试 | 自动检测 GPU |
| 5 | 开始挖矿 | 点击按钮 |

### 首次运行配置

| 设置 | 默认值 | 推荐 |
|------|--------|------|
| 算法 | 自动 | 让基准测试决定 |
| 强度 | 中等 | 从低开始，逐步增加 |
| 风扇控制 | 自动 | 手动以提高稳定性 |
| 功率限制 | 100% | 降低以提高效率 |

### 杀毒软件注意事项

| 问题 | 原因 | 解决方案 |
|------|------|----------|
| 被阻止 | 检测到挖矿 | 添加例外 |
| 被隔离 | 误报 | 恢复文件 |
| 变慢 | 实时扫描 | 排除文件夹 |

---

## 配置与优化

优化挖矿设置以获得最大盈利能力。

### GPU 超频设置

| 设置 | 效果 | 典型范围 |
|------|------|----------|
| 核心频率 | 算力 | +100 到 +200 MHz |
| 显存频率 | 取决于算法 | +500 到 +1500 MHz |
| 功率限制 | 效率 | 60-80% |
| 风扇速度 | 温度 | 70-100% |

### 算法特定设置

| 算法 | 核心频率 | 显存频率 | 功率限制 |
|------|----------|----------|----------|
| DaggerHashimoto | 中等 | 高 | 70-80% |
| KawPow | 高 | 中等 | 80-90% |
| Autolykos | 低 | 高 | 60-70% |
| Octopus | 中等 | 中等 | 70-80% |

### 温度管理

| 温度 | 状态 | 操作 |
|------|------|------|
| < 60°C | 优秀 | 无需操作 |
| 60-70°C | 良好 | 监控 |
| 70-80°C | 可接受 | 增加风扇 |
| > 80°C | 太热 | 降低功率/频率 |

### 功率效率

| 指标 | 计算 | 目标 |
|------|------|------|
| 效率 | 算力 / 功率 | 越高越好 |
| 每 MH 成本 | 电费 / 算力 | 越低越好 |
| 盈亏平衡 | 日收益 > 日成本 | 必须为正 |

### QuickMiner 优化模式

| 模式 | 描述 | 用途 |
|------|------|------|
| Lite | 保守 | 稳定性优先 |
| Medium | 平衡 | 默认选择 |
| High | 激进 | 最大性能 |
| Manual | 自定义设置 | 有经验的用户 |

---

## 挖矿算法

不同的算法适合不同的硬件和加密货币。

### 常见算法

| 算法 | 币种 | GPU 偏好 | 显存密集 |
|------|------|----------|----------|
| DaggerHashimoto | ETH (历史) | NVIDIA/AMD | 是 |
| KawPow | RVN | AMD 偏好 | 中等 |
| Autolykos | ERGO | NVIDIA 偏好 | 是 |
| Octopus | CFX | NVIDIA | 中等 |
| ZHash | ZEC | NVIDIA | 低 |

### 算法盈利因素

| 因素 | 影响 | 考虑 |
|------|------|------|
| 币价 | 高 | 市场波动 |
| 网络难度 | 高 | 随时间调整 |
| 区块奖励 | 中等 | 减半事件 |
| 硬件效率 | 高 | GPU 能力 |

### 切换算法

| 方式 | 描述 | 好处 |
|------|------|------|
| 自动切换 | NiceHash 选择 | 最大利润 |
| 手动 | 用户选择 | 特定币种 |
| 双挖 | 两种算法 | 额外收入 |

### 基准测试结果

| GPU | DaggerHashimoto | KawPow | Autolykos |
|-----|-----------------|--------|-----------|
| RTX 3060 | 50 MH/s | 25 MH/s | 100 MH/s |
| RTX 3070 | 62 MH/s | 30 MH/s | 130 MH/s |
| RTX 3080 | 100 MH/s | 45 MH/s | 200 MH/s |
| RTX 3090 | 120 MH/s | 55 MH/s | 260 MH/s |

---

## 盈利能力与收益

理解挖矿经济学和预期回报。

### 盈利计算

```
Daily Revenue = Hash Rate × Algorithm Price × 24 hours
Daily Cost = Power (kW) × 24 × Electricity Rate
Daily Profit = Daily Revenue - Daily Cost
```

### 收入因素

| 因素 | 影响 | 波动性 |
|------|------|--------|
| 加密货币价格 | 高 | 非常高 |
| 网络难度 | 高 | 中等 |
| 算力 | 直接 | 低 |
| 算法需求 | 中等 | 中等 |

### 成本因素

| 成本 | 计算 | 占比 |
|------|------|------|
| 电费 | kWh x 费率 | 30-60% |
| 硬件 | 摊销成本 | 20-40% |
| 散热 | 额外功率 | 5-10% |
| 网络 | 固定费率 | 1-2% |

### 盈亏平衡分析

| 场景 | 投资 | 日利润 | 盈亏平衡 |
|------|------|--------|----------|
| 单 GPU | $500 | $2-4 | 125-250 天 |
| 6 GPU 矿机 | $3,000 | $12-24 | 125-250 天 |
| ASIC 矿机 | $5,000 | $10-20 | 250-500 天 |

### 支付计划

| 阈值 | 频率 | 方式 |
|------|------|------|
| 0.001 BTC | 每天 | Bitcoin |
| 0.00001 BTC | 即时 | Lightning |
| $1 | 即时 | Coinbase |

---

## 硬件推荐

选择合适的挖矿硬件。

### GPU 对比

| GPU | 算力 | 功率 | 效率 | 价格 |
|-----|------|------|------|------|
| RTX 3060 | 50 MH/s | 120W | 良好 | $300 |
| RTX 3070 | 62 MH/s | 130W | 非常好 | $500 |
| RTX 3080 | 100 MH/s | 230W | 良好 | $700 |
| RTX 3090 | 120 MH/s | 300W | 一般 | $1,500 |
| RTX 4070 | 60 MH/s | 100W | 优秀 | $600 |

### 矿机组件

| 组件 | 推荐 | 备注 |
|------|------|------|
| CPU | 基础 | 不用于挖矿 |
| 内存 | 8GB | 需求极低 |
| 电源 | 80+ Gold | 总功率 1.5 倍 |
| 主板 | 多 PCIe | 支持 6+ GPU |
| 转接卡 | USB 3.0 | GPU 间距 |

### 电源功率

| GPU 数量 | 总功率 | 电源大小 | 效率 |
|----------|--------|----------|------|
| 1 | 200W | 450W | 最佳 |
| 2 | 400W | 750W | 良好 |
| 4 | 800W | 1200W | 良好 |
| 6 | 1200W | 1600W | 必需 |

### 散热方案

| 方式 | 成本 | 效果 | 噪音 |
|------|------|------|------|
| 开放式 | 低 | 良好 | 中等 |
| 电风扇 | 极低 | 中等 | 高 |
| 空调 | 高 | 优秀 | 中等 |
| 定制水冷 | 极高 | 优秀 | 低 |

---

## 故障排除

常见挖矿问题及解决方案。

### 常见问题

| 问题 | 可能原因 | 解决方案 |
|------|----------|----------|
| 算力低 | 热节流 | 降低温度 |
| 崩溃 | 超频不稳定 | 降低频率 |
| 无份额 | 算法错误 | 重新基准测试 |
| 被拒份额 | 网络问题 | 检查连接 |

### 温度问题

| 症状 | 原因 | 解决方案 |
|------|------|----------|
| 高温 | 气流差 | 改善散热 |
| 节流 | 功率限制太高 | 降低功率 |
| 风扇噪音 | 积尘 | 清洁硬件 |
| 关机 | 临界温度 | 紧急散热 |

### 稳定性测试

| 测试 | 持续时间 | 成功标准 |
|------|----------|----------|
| 快速 | 10 分钟 | 无崩溃 |
| 标准 | 1 小时 | 稳定算力 |
| 扩展 | 24 小时 | 无错误 |
| 压力 | 48 小时 | 最大稳定性 |

### 错误信息

| 错误 | 含义 | 操作 |
|------|------|------|
| "CUDA error" | GPU 驱动问题 | 更新驱动 |
| "Out of memory" | 显存耗尽 | 降低强度 |
| "Connection refused" | 网络问题 | 检查网络 |
| "Invalid share" | 算法不匹配 | 重新基准测试 |

### 诊断工具

| 工具 | 用途 | 何时使用 |
|------|------|----------|
| GPU-Z | GPU 监控 | 性能检查 |
| HWiNFO | 系统监控 | 温度检查 |
| MSI Afterburner | 超频 | 优化 |
| NiceHash logs | 错误分析 | 故障排除 |

---

## 总结

| 主题 | 核心要点 |
|------|----------|
| 平台 | NiceHash 是算力出售市场 |
| 安装 | QuickMiner 简化入门 |
| 优化 | 平衡算力和功率效率 |
| 盈利 | 电费是关键因素 |
| 硬件 | 推荐 NVIDIA RTX 系列 |
| 稳定性 | 24/7 运行前充分测试 |


---

## 来源：mintable.md

**Source:** https://github.com/kevinschaich/mintable

## Overview

This tutorial covers the key resources and tools from the [kevinschaich/mintable](https://github.com/kevinschaich/mintable) project.

## Quickstart

Requires `node >= v11.0.0`.

1. Sign up for [Plaid's Free Plan](https://plaid.com/pricing/).
2. Install Mintable:

    ```bash
    npm install -g mintable
    mintable setup
    ```

3. Update your account balances/transactions:

    ```
    mintable fetch
    ```

> **Note:** If you're already a version `1.x.x` user, you can [migrate your existing configuration to version `2.x.x`](./docs/README.md#migrating-from-v1xx).

## Documentation

Check out the full documentation [in the `./docs` folder](./docs/README.md).

## FAQs

**WTF is 'Mintable'?!**

> **min·ta·ble**: _noun._
> 1. An open-source tool to automate your personal finances – for free, with no ads, and no data collection. Derived from *mint* (the [wildly popular personal finance app from Intuit](https://www.mint.com/)) + *table* (a spreadsheet).

**Do I have to use Plaid?**

* Nope. You can [import transactions from a CSV bank statement](./docs/README.md#manually--on-your-local-machine--via-csv-bank-statements) exclusively on your local machine. We also have [templates](./docs/templates) to get you started.

**Do I have to use Google Sheets?**

* Nope. You can [export your account balances & transactions to a CSV file](./docs/README.md#on-your-local-machine--via-csv-files) exclusively on your local machine.

**Do I have to manually run this every time I want new transactions in my spreadsheet?**

* Nope. You can automate it for free using [BitBar](./docs/README.md#automatically-in-your-macs-menu-bar--via-bitbar), [`cron`](./docs/README.md#automatically-in-your-local-machines-terminal--via-cron), or [GitHub Actions](./docs/README.md#automatically-in-the-cloud--via-github-actions).

**How do I use it with banks outside the US?**

* Fork & edit the [country codes here](https://github.com/kevinschaich/mintable/blob/377257a6040ed9b6dd93d88435e53c48108b5806/src/integrations/plaid/plaidIntegration.ts#L126). Default support is for US banks.

**How do I use it with Windows?**

* Windows is not natively supported but you can try [this](https://github.com/kevinschaich/mintable/issues/125#issuecomment-1253961155).

**It's not working!**

- [File an issue](https://github.com/kevinschaich/mintable/issues)

## Alternatives

- [**Money in Excel**](https://www.microsoft.com/en-us/microsoft-365/blog/2020/06/15/introducing-money-excel-easier-manage-finances/): Recently announced partnership between Microsoft/Plaid. Requires a Microsoft 365 subscription ($70+/year).
- [**Mint**](https://www.mint.com/): Owned by Intuit (TurboTax). Apps for iOS/Android/Web.
- [**build-your-own-mint**](https://github.com/yyx990803/build-your-own-mint): Some assembly required. More flexible.

## Key Resources

| Resource | Link |
|----------|------|
| Plaid's Free Plan | [https://plaid.com/pricing/](https://plaid.com/pricing/) |
| wildly popular personal finance app from Intuit | [https://www.mint.com/](https://www.mint.com/) |
| country codes here | [https://github.com/kevinschaich/mintable/blob/377257a6040ed9b6dd93d88435e53c48108b5806/src/integrations/plaid/plaidIntegration.ts#L126](https://github.com/kevinschaich/mintable/blob/377257a6040ed9b6dd93d88435e53c48108b5806/src/integrations/plaid/plaidIntegration.ts#L126) |
| this | [https://github.com/kevinschaich/mintable/issues/125#issuecomment-1253961155](https://github.com/kevinschaich/mintable/issues/125#issuecomment-1253961155) |
| File an issue | [https://github.com/kevinschaich/mintable/issues](https://github.com/kevinschaich/mintable/issues) |
| **Money in Excel** | [https://www.microsoft.com/en-us/microsoft-365/blog/2020/06/15/introducing-money-excel-easier-manage-finances/](https://www.microsoft.com/en-us/microsoft-365/blog/2020/06/15/introducing-money-excel-easier-manage-finances/) |
| **Mint** | [https://www.mint.com/](https://www.mint.com/) |
| **build-your-own-mint** | [https://github.com/yyx990803/build-your-own-mint](https://github.com/yyx990803/build-your-own-mint) |



---
