# 系统化交易资源大全

本文档整理了系统化交易（量化交易）领域的核心资源，包括开源库、学术策略、书籍、视频和课程，供系统化学习使用。

---

## 目录

- [一、开发库与工具包（97个）](#一开发库与工具包97个)
  - [1.1 回测与实盘框架](#11-回测与实盘框架)
  - [1.2 交易机器人](#12-交易机器人)
  - [1.3 分析工具](#13-分析工具)
  - [1.4 券商API](#14-券商api)
  - [1.5 数据源](#15-数据源)
  - [1.6 数据科学基础库](#16-数据科学基础库)
  - [1.7 数据库](#17-数据库)
  - [1.8 图计算](#18-图计算)
  - [1.9 机器学习](#19-机器学习)
  - [1.10 时间序列分析](#110-时间序列分析)
  - [1.11 可视化](#111-可视化)
- [二、学术策略（40+）](#二学术策略40)
- [三、书籍推荐（55本）](#三书籍推荐55本)
- [四、视频与课程](#四视频与课程)
- [五、博客](#五博客)
- [六、核心要点总结](#六核心要点总结)

---

## 一、开发库与工具包（97个）

### 1.1 回测与实盘框架

#### 通用 - 事件驱动框架

| 项目 | 说明 | 语言 |
|------|------|------|
| [vnpy](https://github.com/vnpy/vnpy) | Python开源量化交易系统开发框架，2015年发布，功能全面 | Python |
| [zipline](https://github.com/quantopian/zipline) | Python算法交易库，事件驱动回测系统 | Python |
| [backtrader](https://github.com/mementum/backtrader) | 事件驱动的Python回测库 | Python |
| [QUANTAXIS](https://github.com/QUANTAXIS/QUANTAXIS) | 支持股票/期货/期权/港股/虚拟货币的数据、回测、模拟、交易、可视化、多账户纯本地方案 | Python |
| [QuantConnect Lean](https://github.com/QuantConnect/Lean) | QuantConnect算法交易引擎，支持Python和C# | Python/C# |
| [Rqalpha](https://github.com/ricequant/rqalpha) | 可扩展的Python算法回测与交易框架，支持多种证券 | Python |
| [finmarketpy](https://github.com/cuemacro/finmarketpy) | Python金融回测与市场分析库 | Python |
| [backtesting.py](https://github.com/kernc/backtesting.py) | 轻量、快速、用户友好的Python回测框架 | Python |
| [zvt](https://github.com/zvtvz/zvt) | 模块化量化框架 | Python |
| [WonderTrader](https://github.com/wondertrader/wondertrader) | 量化研发交易一站式框架 | Python |
| [nautilus_trader](https://github.com/nautechsystems/nautilus_trader) | 高性能算法交易平台与事件驱动回测器 | Python |
| [PandoraTrader](https://github.com/pegasusTrader/PandoraTrader) | 基于C++的高频量化交易平台，支持多交易API和跨平台 | C++ |
| [HFTBacktest](https://github.com/nkaz001/hftbacktest) | 使用Python+Numba实现高精度HFT数据回测 | Python |
| [aat](https://github.com/AsyncAlgoTrading/aat) | 异步事件驱动框架，支持多品种多策略，可选C++加速 | Python |
| [lumibot](https://github.com/Lumiwealth/lumibot) | 简单实用的回测与实盘交易框架 | Python |
| [quanttrader](https://github.com/letianzj/quanttrader) | 基于事件的Python回测与实盘交易框架 | Python |
| [gobacktest](https://github.com/gobacktest/gobacktest) | Go语言事件驱动回测框架 | Go |
| [FlashFunk](https://github.com/HFQR/FlashFunk) | Rust高性能运行时 | Rust |

#### 通用 - 向量化框架

| 项目 | 说明 | 语言 |
|------|------|------|
| [vectorbt](https://github.com/polakowo/vectorbt) | 基于Pandas和NumPy，Numba加速，可在数秒内测试数千种策略 | Python |
| [pysystemtrade](https://github.com/robcarver17/pysystemtrade) | Rob Carver《Systematic Trading》一书配套的Python系统化交易实现 | Python |
| [bt](https://github.com/pmorissette/bt) | 基于策略树的灵活Python回测库 | Python |

#### 加密货币框架

| 项目 | 说明 | 语言 |
|------|------|------|
| [Freqtrade](https://github.com/freqtrade/freqtrade) | 免费开源加密货币交易机器人，支持Telegram控制、回测、ML策略优化 | Python |
| [Jesse](https://github.com/jesse-ai/jesse) | 加密货币交易框架，简化策略研究与定义 | Python |
| [OctoBot](https://github.com/Drakkar-Software/OctoBot) | 支持技术分析、套利和社交交易的加密货币交易机器人 | Python |
| [Kelp](https://github.com/stellar/kelp) | Stellar DEX和100+中心化交易所的交易机器人 | Go |
| [openlimits](https://github.com/nash-io/openlimits) | Rust高性能加密货币交易API，支持多交易所 | Rust |
| [Hummingbot](https://github.com/CoinAlpha/hummingbot) | 加密货币做市客户端 | Python |
| [bTrader](https://github.com/gabriel-milan/btrader) | Binance三角套利交易机器人 | Rust |
| [crypto-crawler-rs](https://github.com/crypto-crawler/crypto-crawler-rs) | 爬取加密交易所订单簿和交易数据 | Rust |

### 1.2 交易机器人

| 项目 | 说明 | 语言 |
|------|------|------|
| [Blackbird](https://github.com/butor/blackbird) | 比特币套利：多空中性策略 | C++ |
| [bitcoin-arbitrage](https://github.com/maxme/bitcoin-arbitrage) | 比特币套利机会检测器 | Python |
| [ThetaGang](https://github.com/brndnmtthws/thetagang) | IBKR期权Theta策略机器人 | TypeScript |
| [czsc](https://github.com/waditu/czsc) | 缠中说禅技术分析工具，支持股票/期货 | Python |
| [R2 Bitcoin Arbitrager](https://github.com/bitrinjani/r2) | Node.js+TypeScript自动比特币套利系统 | TypeScript |
| [PyTrendFollow](https://github.com/chrism2671/PyTrendFollow) | 基于趋势跟踪的系统化期货交易 | Python |

### 1.3 分析工具

#### 技术指标库

| 项目 | 说明 | 语言 |
|------|------|------|
| [ta-lib](https://github.com/mrjbq7/ta-lib) | 金融市场数据技术分析库 | Python |
| [go-tart](https://github.com/iamjinlei/go-tart) | Go语言ta-lib实现，支持流式更新 | Go |
| [pandas-ta](https://github.com/twopirllc/pandas-ta) | 130+指标和60+K线形态模式 | Python |
| [finta](https://github.com/peerchemist/finta) | 基于Pandas的常用金融技术指标实现 | Python |
| [ta-rust](https://github.com/greyblake/ta-rs) | Rust技术分析库 | Rust |

#### 指标计算

| 项目 | 说明 | 语言 |
|------|------|------|
| [quantstats](https://github.com/ranaroussi/quantstats) | 量化投资组合分析工具 | Python |
| [ffn](https://github.com/pmorissette/ffn) | Python金融函数库 | Python |

#### 组合优化

| 项目 | 说明 | 语言 |
|------|------|------|
| [PyPortfolioOpt](https://github.com/robertmartin8/PyPortfolioOpt) | 包含经典有效前沿、Black-Litterman、层次风险平价等方法 | Python |
| [Riskfolio-Lib](https://github.com/dcajasn/Riskfolio-Lib) | 投资组合优化与量化战略资产配置 | Python |
| [empyrial](https://github.com/ssantoshp/Empyrial) | 面向机构和散户的开源量化投资库 | Python |
| [Deepdow](https://github.com/jankrepl/deepdow) | 结合组合优化与深度学习，单次前向传播完成权重分配 | Python |
| [spectre](https://github.com/Heerozh/spectre) | 投资组合优化与量化战略资产配置 | Python |

#### 定价

| 项目 | 说明 | 语言 |
|------|------|------|
| [tf-quant-finance](https://github.com/google/tf-quant-finance) | Google出品的高性能TensorFlow量化金融库 | Python |
| [FinancePy](https://github.com/domokane/FinancePy) | 聚焦衍生品定价与风险管理（固收、权益、外汇、信用） | Python |
| [PyQL](https://github.com/enthought/pyql) | 著名定价库QuantLib的Python封装 | Python |

#### 风险管理

| 项目 | 说明 | 语言 |
|------|------|------|
| [pyfolio](https://github.com/quantopian/pyfolio) | Python投资组合与风险分析 | Python |

### 1.4 券商API

| 项目 | 说明 | 语言 |
|------|------|------|
| [ccxt](https://github.com/ccxt/ccxt) | 支持100+加密交易所的统一交易API | Python/JS/PHP |
| [Ib_insync](https://github.com/erdewit/ib_insync) | Interactive Brokers的Python同步/异步框架 | Python |
| [Coinnect](https://github.com/hugues31/coinnect) | Rust加密货币交易所REST API客户端库 | Rust |
| [PENDAX](https://github.com/CompendiumFi/PENDAX-SDK) | 支持FTX、OKX、Bybit等交易所的JavaScript SDK | JavaScript |

### 1.5 数据源

#### 通用数据

| 项目 | 说明 | 语言 |
|------|------|------|
| [OpenBB Terminal](https://github.com/OpenBB-finance/OpenBBTerminal) | 开源投资研究终端 | Python |
| [TuShare](https://github.com/waditu/tushare) | 中国股票历史数据爬取工具 | Python |
| [yfinance](https://github.com/ranaroussi/yfinance) | 从Yahoo Finance下载市场数据 | Python |
| [AkShare](https://github.com/akfamily/akshare) | Python金融数据接口库 | Python |
| [pandas-datareader](https://github.com/pydata/pandas-datareader) | Pandas远程数据访问工具 | Python |
| [Quandl](https://github.com/quandl/quandl-python) | 通过单一API获取数百万金融和经济数据集 | Python |
| [findatapy](https://github.com/cuemacro/findatapy) | 统一高层API下载多源市场数据（Quandl、Bloomberg、Yahoo等） | Python |
| [Investpy](https://github.com/alvarobartt/investpy) | 从Investing.com提取金融数据 | Python |
| [Fundamental Analysis](https://github.com/JerBouma/FundamentalAnalysis) | 收集20000+公司20年的财务数据、比率和股票数据 | Python |
| [Wallstreet](https://github.com/mcdallas/wallstreet) | 实时股票和期权工具 | Python |

#### 加密货币数据

| 项目 | 说明 | 语言 |
|------|------|------|
| [Cryptofeed](https://github.com/bmoscon/cryptofeed) | 加密交易所WebSocket数据处理器 | Python |
| [Gekko-Datasets](https://github.com/xFFFFF/Gekko-Datasets) | Gekko交易机器人历史数据集（SQLite格式） | Python |
| [CryptoInscriber](https://github.com/Optixal/CryptoInscriber) | 加密货币实时历史交易数据记录器 | Python |
| [Crypto Lake](https://github.com/crypto-lake/lake-api) | 高频订单簿与加密货币交易数据 | Python |

### 1.6 数据科学基础库

| 项目 | 说明 | 语言 |
|------|------|------|
| [TensorFlow](https://github.com/tensorflow/tensorflow) | 科学计算基础算法库 | Python |
| [PyTorch](https://github.com/pytorch/pytorch) | 强GPU加速的张量与动态神经网络库 | Python |
| [Keras](https://github.com/keras-team/keras) | 用户友好的深度学习库 | Python |
| [Scikit-learn](https://github.com/scikit-learn/scikit-learn) | Python机器学习库 | Python |
| [Pandas](https://github.com/pandas-dev/pandas) | 强大的数据分析与操作库 | Python |
| [NumPy](https://github.com/numpy/numpy) | Python科学计算基础包 | Python |
| [SciPy](https://github.com/scipy/scipy) | 科学计算基础算法库 | Python |
| [PyMC](https://github.com/pymc-devs/pymc) | 概率编程：贝叶斯建模与概率机器学习 | Python |
| [CVXPY](https://github.com/cvxpy/cvxpy) | Python凸优化建模语言 | Python |

### 1.7 数据库

| 项目 | 说明 | 语言 |
|------|------|------|
| [Marketstore](https://github.com/alpacahq/marketstore) | 金融时序数据的DataFrame服务器 | Go |
| [Tectonicdb](https://github.com/0b01/tectonicdb) | 快速、高压缩的订单簿tick数据独立数据库 | Rust |
| [ArcticDB](https://github.com/man-group/arcticdb) | Man Group出品的高性能时序与tick数据存储 | Python |

### 1.8 图计算

| 项目 | 说明 | 语言 |
|------|------|------|
| [Ray](https://github.com/ray-project/ray) | 构建分布式应用的通用API框架 | Python |
| [Dask](https://github.com/dask/dask) | 类Pandas API的Python并行计算库 | Python |
| [Incremental (JaneStreet)](https://github.com/janestreet/incremental) | 高效响应输入变化的增量计算库 | OCaml |
| [Man MDF](https://github.com/man-group/mdf) | Python数据流编程工具包 | Python |
| [GraphKit](https://github.com/yahoo/graphkit) | 轻量级Python有序计算图模块 | Python |
| [Tributary](https://github.com/timkpaine/tributary) | Python流式响应与数据流图库 | Python |

### 1.9 机器学习

| 项目 | 说明 | 语言 |
|------|------|------|
| [QLib (Microsoft)](https://github.com/microsoft/qlib) | 微软AI量化投资平台，集成前沿量化研究成果 | Python |
| [FinRL](https://github.com/AI4Finance-Foundation/FinRL) | 首个将深度强化学习应用于量化金融的开源框架 | Python |
| [MlFinLab (Hudson & Thames)](https://github.com/hudson-and-thames/mlfinlab) | 为组合经理和交易者提供可复现、可解释的ML工具 | Python |
| [TradingGym](https://github.com/Yvictor/TradingGym) | 用于训练RL代理或规则算法的交易与回测环境 | Python |
| [Deep Q-Learning Trading Bot](https://github.com/pskrunner14/trading-bot) | 基于深度Q学习的股票交易机器人 | Python |

### 1.10 时间序列分析

| 项目 | 说明 | 语言 |
|------|------|------|
| [Facebook Prophet](https://github.com/facebook/prophet) | 高质量时序预测工具，支持多重季节性和线性/非线性增长 | Python |
| [statsmodels](https://github.com/statsmodels/statsmodels) | 数据探索、统计模型估计与统计检验 | Python |
| [tsfresh](https://github.com/blue-yonder/tsfresh) | 时序数据自动相关特征提取 | Python |
| [pmdarima](https://github.com/alkaline-ml/pmdarima) | 等价于R的auto.arima的Python统计库 | Python |

### 1.11 可视化

| 项目 | 说明 | 语言 |
|------|------|------|
| [D-Tale (Man Group)](https://github.com/man-group/dtale) | Flask后端+React前端的Pandas数据查看与分析工具 | Python |
| [mplfinance](https://github.com/matplotlib/mplfinance) | 基于Matplotlib的金融市场数据可视化 | Python |
| [btplotting](https://github.com/happydasch/btplotting) | Backtrader回测结果、优化结果和实盘数据绘图工具 | Python |

---

## 二、学术策略（40+）

以下策略均来自学术论文，按资产类别分类，按夏普比率降序排列。

### 跨资产类别策略

#### 债券、商品、货币、股票

| 策略名称 | 夏普比率 | 波动率 | 调仓频率 | 论文来源 |
|----------|---------|--------|---------|---------|
| 时间序列动量效应 | 0.576 | 20.5% | 月度 | [论文](https://pages.stern.nyu.edu/~lpederse/papers/TimeSeriesMomentum.pdf) |
| 期货短期反转 | -0.05 | 12.3% | 周度 | [论文](https://ideas.repec.org/a/eee/jbfina/v28y2004i6p1337-1361.html) |

#### 债券、商品、股票、REITs

| 策略名称 | 夏普比率 | 波动率 | 调仓频率 | 论文来源 |
|----------|---------|--------|---------|---------|
| 资产类别趋势跟踪 | 0.502 | 10.4% | 月度 | [论文](https://papers.ssrn.com/sol3/papers.cfm?abstract_id=962461) |
| 动量资产配置策略 | 0.321 | 11% | 月度 | [论文](https://papers.ssrn.com/sol3/papers.cfm?abstract_id=1585517) |

#### 债券、股票

| 策略名称 | 夏普比率 | 波动率 | 调仓频率 | 论文来源 |
|----------|---------|--------|---------|---------|
| 配对切换策略 | 0.691 | 9.5% | 季度 | [论文](https://papers.ssrn.com/sol3/papers.cfm?abstract_id=1917044) |
| FED模型 | 0.369 | 14.3% | 月度 | [论文](https://www.researchgate.net/publication/228267011_The_FED_Model_and_Expected_Asset_Returns) |

#### 债券、股票、REITs

| 策略名称 | 夏普比率 | 波动率 | 调仓频率 | 论文来源 |
|----------|---------|--------|---------|---------|
| 跨资产价值与动量因子 | 0.155 | 9.8% | 月度 | [论文](https://papers.ssrn.com/sol3/papers.cfm?abstract_id=1079975) |

### 商品策略

| 策略名称 | 夏普比率 | 波动率 | 调仓频率 | 论文来源 |
|----------|---------|--------|---------|---------|
| 商品偏度效应 | 0.482 | 17.7% | 月度 | [论文](https://papers.ssrn.com/sol3/papers.cfm?abstract_id=2671165) |
| 商品期货收益不对称效应 | 0.239 | 13.4% | 月度 | [论文](https://papers.ssrn.com/sol3/papers.cfm?abstract_id=3918896) |
| 商品动量效应 | 0.14 | 20.3% | 月度 | [论文](https://papers.ssrn.com/sol3/papers.cfm?abstract_id=702281) |
| 商品期限结构效应 | 0.128 | 23.1% | 月度 | [论文](https://papers.ssrn.com/sol3/papers.cfm?abstract_id=1127213) |
| WTI/BRENT价差交易 | -0.199 | 11.6% | 日度 | [论文](https://link.springer.com/article/10.1057/jdhf.2009.24) |

### 加密货币策略

| 策略名称 | 夏普比率 | 波动率 | 调仓频率 | 论文来源 |
|----------|---------|--------|---------|---------|
| 比特币隔夜季节性 | 0.892 | 20.8% | 日内 | [论文](https://papers.ssrn.com/sol3/papers.cfm?abstract_id=4081000) |
| 加密货币再平衡溢价 | 0.698 | 27.5% | 日度 | [论文](https://papers.ssrn.com/sol3/papers.cfm?abstract_id=3982120) |

### 货币策略

| 策略名称 | 夏普比率 | 波动率 | 调仓频率 | 论文来源 |
|----------|---------|--------|---------|---------|
| 外汇套息交易 | 0.254 | 7.8% | 月度 | [论文](http://globalmarkets.db.com/new/docs/dbCurrencyReturns_March2009.pdf) |
| 美元套息交易 | 0.113 | 5.8% | 月度 | [论文](https://papers.ssrn.com/sol3/papers.cfm?abstract_id=1541230) |
| 货币动量因子 | -0.01 | 6.7% | 月度 | [论文](http://globalmarkets.db.com/new/docs/dbCurrencyReturns_March2009.pdf) |
| 货币价值因子（PPP策略） | -0.103 | 5% | 季度 | [论文](http://globalmarkets.db.com/new/docs/dbCurrencyReturns_March2009.pdf) |

### 股票策略

| 策略名称 | 夏普比率 | 波动率 | 调仓频率 | 论文来源 |
|----------|---------|--------|---------|---------|
| 资产增长效应 | 0.835 | 10.2% | 年度 | [论文](https://papers.ssrn.com/sol3/papers.cfm?abstract_id=1335524) |
| 股票短期反转效应 | 0.816 | 21.4% | 周度 | [论文](https://papers.ssrn.com/sol3/papers.cfm?abstract_id=1605049) |
| 财报公告期反转 | 0.785 | 25.7% | 日度 | [论文](https://papers.ssrn.com/sol3/papers.cfm?abstract_id=2275982) |
| 小盘股溢价（规模因子） | 0.747 | 11.1% | 年度 | [论文](https://papers.ssrn.com/sol3/papers.cfm?abstract_id=3177539) |
| 低波动因子效应 | 0.717 | 11.5% | 月度 | [论文](https://papers.ssrn.com/sol3/papers.cfm?abstract_id=980865) |
| 公司文件词汇密度 | 0.688 | 10.4% | 月度 | [论文](https://papers.ssrn.com/sol3/papers.cfm?abstract_id=3921091) |
| 波动率风险溢价效应 | 0.637 | 13.2% | 月度 | [论文](https://papers.ssrn.com/sol3/papers.cfm?abstract_id=189840) |
| 股票配对交易 | 0.634 | 8.5% | 日度 | [论文](https://papers.ssrn.com/sol3/papers.cfm?abstract_id=141615) |
| 原油预测股票收益 | 0.599 | 11.5% | 月度 | [论文](https://papers.ssrn.com/sol3/papers.cfm?abstract_id=460500) |
| 做空Beta因子 | 0.594 | 18.9% | 月度 | [论文](https://pages.stern.nyu.edu/~lpederse/papers/BettingAgainstBeta.pdf) |
| 股票趋势跟踪效应 | 0.569 | 15.2% | 日度 | [论文](https://www.cis.upenn.edu/~mkearns/finread/trend.pdf) |
| ESG因子动量策略 | 0.559 | 21.8% | 月度 | [论文](https://www.semanticscholar.org/paper/Can-ESG-Add-Alpha-An-Analysis-of-ESG-Tilt-and-Nagy-Kassam/64f77da4f8ce5906a73ffe4e9eec7c49c0960acc) |
| 价值因子（账面市值比） | 0.526 | 11.9% | 月度 | [论文](https://papers.ssrn.com/sol3/papers.cfm?abstract_id=2595747) |
| 足球俱乐部股票套利 | 0.515 | 14.2% | 日度 | [论文](https://papers.ssrn.com/sol3/papers.cfm?abstract_id=1343685) |
| 合成贷款利率预测市场收益 | 0.494 | 13.7% | 日度 | [论文](https://papers.ssrn.com/sol3/papers.cfm?abstract_id=3976307) |
| 期权到期周效应 | 0.452 | 5% | 周度 | [论文](https://papers.ssrn.com/sol3/papers.cfm?abstract_id=1571786) |
| 离散度交易 | 0.432 | 8.1% | 月度 | [论文](https://www.academia.edu/16327015/EQUILIBRIUM_INDEX_AND_SINGLE_STOCK_VOLATILITY_RISK_PREMIA) |
| 共同基金收益动量 | 0.414 | 13.6% | 季度 | [论文](https://papers.ssrn.com/sol3/papers.cfm?abstract_id=1462408) |
| 板块动量轮动系统 | 0.401 | 14.1% | 月度 | [论文](https://papers.ssrn.com/sol3/papers.cfm?abstract_id=1585517) |
| 智能因子动量与市场组合 | 0.388 | 8.2% | 月度 | [论文](https://papers.ssrn.com/sol3/papers.cfm?abstract_id=3745517) |
| 动量+反转+波动率效应组合 | 0.375 | 17% | 月度 | [论文](https://papers.ssrn.com/sol3/papers.cfm?abstract_id=1679464) |
| 市场情绪与隔夜异常 | 0.369 | 3.6% | 日度 | [论文](https://papers.ssrn.com/sol3/papers.cfm?abstract_id=3829582) |
| 一月晴雨表 | 0.365 | 7.4% | 月度 | [论文](https://papers.ssrn.com/sol3/papers.cfm?abstract_id=1436516) |
| R&D支出与股票收益 | 0.354 | 8.1% | 年度 | [论文](https://papers.ssrn.com/sol3/papers.cfm?abstract_id=227564) |
| 价值因子（各国CAPE效应） | 0.351 | 20.2% | 年度 | [论文](https://papers.ssrn.com/sol3/papers.cfm?abstract_id=2129474) |
| 股票截面12个月周期 | 0.34 | 43.7% | 月度 | [论文](https://papers.ssrn.com/sol3/papers.cfm?abstract_id=687022) |
| 股票指数月末效应 | 0.305 | 7.2% | 日度 | [论文](https://papers.ssrn.com/sol3/papers.cfm?abstract_id=917884) |
| 发薪日异常 | 0.269 | 3.8% | 日度 | [论文](https://papers.ssrn.com/sol3/papers.cfm?abstract_id=3257064) |
| 国家ETF配对交易 | 0.257 | 5.7% | 日度 | [论文](https://papers.ssrn.com/sol3/papers.cfm?abstract_id=1958546) |
| 残差动量因子 | 0.24 | 9.7% | 月度 | [论文](https://papers.ssrn.com/sol3/papers.cfm?abstract_id=2319861) |
| 财报公告溢价 | 0.192 | 3.7% | 月度 | [论文](https://www.nber.org/system/files/working_papers/w13090/w13090.pdf) |
| ROA效应 | 0.155 | 8.7% | 月度 | [论文](https://static1.squarespace.com/static/5e6033a4ea02d801f37e15bb/t/5f61583e88f43b7d5b7196b5/1600215105801/Chen_Zhang_JF.pdf) |
| 52周新高效应 | 0.153 | 19% | 月度 | [论文](https://papers.ssrn.com/sol3/papers.cfm?abstract_id=1787378) |
| FSCORE与短期反转组合 | 0.153 | 17.6% | 月度 | [论文](https://papers.ssrn.com/sol3/papers.cfm?abstract_id=3097420) |
| 国际股票做空Beta因子 | 0.142 | 9.1% | 月度 | [论文](https://pages.stern.nyu.edu/~lpederse/papers/BettingAgainstBeta.pdf) |
| 一致性动量策略 | 0.128 | 28.8% | 半年 | [论文](https://papers.ssrn.com/sol3/papers.cfm?abstract_id=2652592) |
| 做空利息效应（多空版） | 0.079 | 6.6% | 月度 | [论文](https://www.semanticscholar.org/paper/Why-Do-Short-Interest-Levels-Predict-Stock-Returns-Boehmer-Erturk/06418ef437dc7156229532a97d0f8392373eb297?p2df) |
| 动量+资产增长效应组合 | 0.058 | 25.1% | 月度 | [论文](https://papers.ssrn.com/sol3/papers.cfm?abstract_id=1684767) |
| 动量因子效应 | -0.008 | 21.8% | 月度 | [论文](https://papers.ssrn.com/sol3/papers.cfm?abstract_id=2435323) |
| 动量因子与风格轮动效应 | -0.056 | 10% | 月度 | [论文](https://papers.ssrn.com/sol3/papers.cfm?abstract_id=1276815) |
| 财报公告+股票回购组合 | -0.16 | 0.1% | 日度 | [论文](https://papers.ssrn.com/sol3/papers.cfm?abstract_id=2589966) |
| 盈利质量因子 | -0.18 | 28.7% | 年度 | [论文](https://papers.ssrn.com/sol3/papers.cfm?abstract_id=2179247) |
| 应计异常 | -0.272 | 13.7% | 年度 | [论文](https://papers.ssrn.com/sol3/papers.cfm?abstract_id=546108) |

---

## 三、书籍推荐（55本）

### 入门

| 书名 | 评分 |
|------|------|
| A Beginner's Guide to the Stock Market - Matthew R. Kratter | 4.4 |
| How to Day Trade for a Living - Andrew Aziz | 4.5 |
| The Little Book of Common Sense Investing - John C. Bogle | 4.7 |
| Investing QuickStart Guide - Ted D. Snow | 4.5 |
| Day Trading QuickStart Guide - Troy Noonan | 4.4 |
| Introduction To Algo Trading - Kevin J Davey | 4.0 |
| Algorithmic Trading and DMA - Barry Johnson | 4.4 |

### 传记

| 书名 | 评分 |
|------|------|
| My Life as a Quant - Emanuel Derman | 4.3 |
| How I Became a Quant - Barry Schachter | 3.7 |

### 编程

| 书名 | 评分 |
|------|------|
| Python for Finance - Yves Hilpisch | 4.6 |
| Trading Evolved - Andreas F. Clenow | 4.3 |
| Python for Algorithmic Trading - Yves Hilpisch | 4.4 |
| Algorithmic Trading with Python - Chris Conlan | 4.2 |
| Learn Algorithmic Trading - Sebastien Donadio | 4.1 |

### 加密货币

| 书名 | 评分 |
|------|------|
| The Bitcoin Standard - Saifedean Ammous | 4.7 |
| Bitcoin Billionaires - Ben Mezrich | 4.5 |
| Mastering Bitcoin - Andreas M. Antonopoulos | 4.7 |
| Why Buy Bitcoin - Andy Edstrom | 4.7 |

### 综合/进阶

| 书名 | 评分 |
|------|------|
| The Intelligent Investor - Benjamin Graham | 4.6 |
| How I Invest My Money - Joshua Brown, Brian Portnoy | 4.3 |
| Naked Forex - Alex Nekritin | 4.7 |
| The Four Pillars of Investing - William J. Bernstein | 4.7 |
| Option Volatility and Pricing - Sheldon Natenberg | 4.6 |
| The Art and Science of Technical Analysis - Adam Grimes | 4.7 |
| The New Trading for a Living - Alexander Elder | 4.5 |
| Building Winning Algorithmic Trading Systems - Kevin J Davey | 4.2 |
| Systematic Trading - Robert Carver | 4.2 |
| Quantitative Momentum - Wesley R. Gray, Jack R. Vogel | 4.3 |
| Algorithmic Trading: Winning Strategies and Their Rationale - Ernest P. Chan | 4.3 |
| Leveraged Trading - Robert Carver | 4.4 |
| Trading Systems - Emilio Tomasini, Urban Jaekle | 4.3 |
| Trading and Exchanges - Larry Harris | 4.3 |
| Machine Trading - Ernest P. Chan | 4.0 |
| Quantitative Equity Portfolio Management - Ludwig B Chincarini | 4.5 |
| Active Portfolio Management - Richard Grinold, Ronald Kahn | 4.0 |
| Quantitative Technical Analysis - Dr Howard B Bandy | 3.8 |
| Advances in Active Portfolio Management - Richard Grinold, Ronald Kahn | 4.7 |
| Professional Automated Trading - Eugene A. Durenard | 4.3 |
| Algorithmic Trading and Quantitative Strategies - Raja Velu等 | 4.2 |

### 高频交易

| 书名 | 评分 |
|------|------|
| Inside the Black Box - Rishi K. Narang | 4.3 |
| Algorithmic and High-Frequency Trading - Cartea, Jaimungal, Penalva | 4.1 |
| The Problem of HFT - Haim Bodek | 4.0 |
| An Introduction to High-Frequency Finance - Genay等 | 4.6 |
| Market Microstructure in Practice - Lehalle, Laruelle | 3.9 |
| The Financial Mathematics of Market Liquidity - Olivier Gueant | 4.6 |

### 机器学习与金融

| 书名 | 评分 |
|------|------|
| Dark Pools - Scott Patterson | 4.5 |
| Advances in Financial Machine Learning - Marcos Lopez de Prado | 4.4 |
| Machine Learning for Algorithmic Trading - Stefan Jansen | 4.4 |
| Machine Learning for Asset Managers - Marcos Lopez de Prado | 4.6 |
| Machine Learning in Finance - Dixon, Halperin, Bilokon | 4.6 |
| Artificial Intelligence in Finance - Yves Hilpisch | 4.3 |
| Algorithmic Trading Methods - Robert Kissell | 4.7 |

---

## 四、视频与课程

### 视频

| 主题 | 链接 |
|------|------|
| 机器学习在股票预测中的应用 | [Krish Naik](https://www.youtube.com/watch?v=H6du_pfuznE) |
| 机器学习交易网络研讨会 | [QuantInsti](https://www.youtube.com/user/quantinsti/search?query=machine+learning) |
| 深度学习预测股票市场 | [Siraj Raval](https://www.youtube.com/channel/UCWN3xxRkmTPmbKwht9FuE5A/search?query=trading) |
| 机器学习交易网络研讨会 | [Quantopian](https://www.youtube.com/channel/UC606MUq45P3zFLa4VGKbxsg/search?query=machine+learning) |
| 外汇和股票ML分析与算法交易 | [Sentdex](https://www.youtube.com/watch?v=v_L9jR8P-54&list=PLQVvvaa0QuDe6ZBtkCNWNUbdaBo2vA4RO) |
| ML算法交易3部曲 | [QuantNews](https://www.youtube.com/playlist?list=PLHJACfjILJ-91qkw5YC83S6COKGscctzz) |
| Python金融编程 | [Sentdex](https://www.youtube.com/watch?v=Z-5wNWgRJpk&index=9&list=PLQVvvaa0QuDcOdF96TBtRtuQksErCEBYZ) |
| 深度强化学习在交易中的应用 | [Tucker Balch](https://www.youtube.com/watch?v=Pka0DC_P17k) |
| 量化交易中的机器学习 | [Ernie Chan](https://www.youtube.com/watch?v=72aEDjwGMr8&t=1023s) |
| 限价订单簿深度学习分析 | [Essex大学硕士论文](https://www.youtube.com/watch?v=qxSh2VFmRGw) |
| ML交易系统开发 | [Howard Bandy](https://www.youtube.com/watch?v=v729evhMpYk&t=1s) |
| 深度学习在金融中的应用 | [Alpaca CTO](https://www.youtube.com/watch?v=FoQKCeDuPiY) |
| Python金融深度学习 | [Prediction Machines](https://www.youtube.com/watch?v=xvm-M-R2fZY) |

### 课程

| 课程名称 | 平台 |
|---------|------|
| AI in Finance | [CFTE](https://cfte.education/) |
| AI与系统化交易 | [paperswithbacktest](https://paperswithbacktest.com/course) |
| Python加密货币算法交易 | [GitHub教程](https://github.com/tudorelu/tudorials/tree/master/trading) |
| 金融中的机器学习导览 | [Coursera/NYU](https://www.coursera.org/learn/guided-tour-machine-learning-finance) |
| 金融机器学习基础 | [Coursera/NYU](https://www.coursera.org/learn/fundamentals-machine-learning-in-finance) |
| 金融中的强化学习 | [Coursera/NYU](https://www.coursera.org/learn/reinforcement-learning-in-finance) |
| 金融强化学习高级方法 | [Coursera/NYU](https://www.coursera.org/learn/advanced-methods-reinforcement-learning-finance) |
| Hudson and Thames量化研究 | [GitHub](https://github.com/hudson-and-thames) |
| AI交易 | [Udacity](https://www.udacity.com/course/ai-for-trading--nd880) |
| 机器学习交易 | [Udacity/Georgia Tech](https://www.udacity.com/course/machine-learning-for-trading--ud501) |

---

## 五、博客

| 博客名称 | 链接 |
|---------|------|
| AAA Quants (Tom Starke) | [aaaquants.com](http://aaaquants.com/category/blog/) |
| AI与系统化交易 | [paperswithbacktest](https://blog.paperswithbacktest.com/) |
| Blackarbs | [blackarbs.com](http://www.blackarbs.com/blog/) |
| Hardik Patel | [hardikp.com](https://www.hardikp.com/) |
| Max Dama on Automated Trading | [链接](https://bit.ly/3wVZbh9) |
| Medallion.Club (法语) | [medallion.club](https://medallion.club/trading-algorithmique-quantitatif-systematique/) |
| Proof Engineering | [链接](https://bit.ly/3lX7zYN) |
| Quantsportal (Jacques Joubert) | [quantsportal.com](http://www.quantsportal.com/blog-page/) |
| Quantstart | [quantstart.com](https://www.quantstart.com/articles) |
| RobotWealth (Kris Longmore) | [robotwealth.com](https://robotwealth.com/blog/) |

---

## 六、核心要点总结

1. **入门路径**：从Python入手，掌握Pandas/NumPy基础 -> 学习backtrader或vectorbt进行回测 -> 用yfinance/TuShare获取数据 -> 实践简单策略（动量、均值回归等）。

2. **框架选型**：事件驱动框架（backtrader、vnpy）适合精细模拟；向量化框架（vectorbt）适合快速批量测试。加密货币交易首选Freqtrade。

3. **策略研究**：夏普比率>0.5的策略值得关注，包括时间序列动量、资产增长效应、短期反转、低波动因子等。但需注意历史表现不等于未来收益。

4. **机器学习应用**：QLib（微软）和FinRL是当前最活跃的ML量化开源项目。《Advances in Financial Machine Learning》是该领域必读书籍。

5. **风险管理**：任何策略都需配合严格的风险管理。波动率、最大回撤、夏普比率是核心评估指标。

6. **数据质量**：数据是量化交易的基础。建议使用多个数据源交叉验证，关注数据清洗和异常值处理。
