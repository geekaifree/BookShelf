# 量化金融资源大全

本文整理了量化金融领域中最重要的开源库、工具和学习资源，覆盖从基础数据处理到策略回测的完整工作流。

## 目录

1. [数值计算与数据结构](#1-数值计算与数据结构)
2. [金融工具与定价](#2-金融工具与定价)
3. [技术指标](#3-技术指标)
4. [交易与回测](#4-交易与回测)
5. [组合优化与风险分析](#5-组合优化与风险分析)
6. [因子分析](#6-因子分析)
7. [情绪分析与另类数据](#7-情绪分析与另类数据)
8. [时间序列分析](#8-时间序列分析)
9. [市场数据源](#9-市场数据源)
10. [预测市场](#10-预测市场)
11. [日历与交易时间](#11-日历与交易时间)
12. [可视化](#12-可视化)
13. [Excel 集成](#13-excel-集成)
14. [量化研究环境](#14-量化研究环境)
15. [跨语言框架](#15-跨语言框架)
16. [学习资料与书籍](#16-学习资料与书籍)
17. [商业服务](#17-商业服务)
18. [核心要点总结](#18-核心要点总结)

---

## 1. 数值计算与数据结构

量化金融的基础设施层，提供矩阵运算、时间序列存储和统计计算能力。

### Python

| 名称 | 说明 | 链接 |
|------|------|------|
| NumPy | 科学计算基础包，提供多维数组和数学函数 | [官网](https://www.numpy.org) / [GitHub](https://github.com/numpy/numpy) |
| SciPy | 科学计算生态，涵盖优化、积分、插值、信号处理等 | [官网](https://www.scipy.org) / [GitHub](https://github.com/scipy/scipy) |
| pandas | 高性能数据分析工具，DataFrame 是量化分析的核心数据结构 | [官网](https://pandas.pydata.org) / [GitHub](https://github.com/pandas-dev/pandas) |
| Polars | 极速 DataFrame 库，适合大规模结构化数据处理 | [官网](https://docs.pola.rs/) / [GitHub](https://github.com/pola-rs/polars) |
| SymPy | 符号数学库，支持代数运算和解析解 | [官网](https://www.sympy.org/) / [GitHub](https://github.com/sympy/sympy) |
| PyMC3 | 概率编程框架，支持贝叶斯建模和概率机器学习 | [官网](https://docs.pymc.io/) / [GitHub](https://github.com/pymc-devs/pymc) |
| quantdsl | 金融量化分析领域特定语言 | [GitHub](https://github.com/johnbywater/quantdsl) |
| modelx | 公式驱动的电子表格替代方案，与 pandas 互操作 | [官网](https://docs.modelx.io/) / [GitHub](https://github.com/fumitoh/modelx) |
| ArcticDB | 高性能时序和逐笔数据存储 | [GitHub](https://github.com/man-group/ArcticDB) |
| CRNG | 生成具有真实金融市场统计特征（肥尾、波动聚集、峰度）的随机数 | [GitHub](https://github.com/brotto/crng) |
| statistics | Python 内置统计库，覆盖基础统计计算 | [文档](https://docs.python.org/3/library/statistics.html) |

### R

| 名称 | 说明 | 链接 |
|------|------|------|
| xts | 可扩展时间序列，统一处理 R 中不同时间类 | [GitHub](https://github.com/joshuaulrich/xts) |
| data.table | 大数据高性能聚合、有序连接和快速列操作 | [GitHub](https://github.com/Rdatatable/data.table) |
| zoo | 规则和不规则时间序列基础架构 | [CRAN](https://cran.r-project.org/web/packages/zoo/index.html) |
| tseries | 时间序列分析与计算金融 | [CRAN](https://cran.r-project.org/web/packages/tseries/index.html) |
| TSdbi | 时间序列数据库统一接口 | [官网](http://tsdbi.r-forge.r-project.org/) |
| sparseEigen | 稀疏主成分分析 | [GitHub](https://github.com/dppalomar/sparseEigen) |
| tis / tfplot / tframe | 时间索引序列、绘图和编程辅助工具 | [CRAN](https://cran.r-project.org/web/packages/tis/index.html) |

### Julia

| 名称 | 说明 | 链接 |
|------|------|------|
| Temporal.jl | 灵活高效的时序数据类 | [GitHub](https://github.com/dysonance/Temporal.jl) |
| DataFrames.jl | 内存表格数据处理 | [GitHub](https://github.com/JuliaData/DataFrames.jl) |
| TSFrames.jl | 基于 DataFrames.jl 的时序数据处理 | [GitHub](https://github.com/xKDR/TSFrames.jl) |

---

## 2. 金融工具与定价

覆盖期权、固定收益、衍生品等各类金融工具的定价和风险度量。

### Python

| 名称 | 说明 | 链接 |
|------|------|------|
| FinancePy | 综合金融衍生品定价库（固收、权益、外汇、信用衍生品） | [GitHub](https://github.com/domokane/FinancePy) |
| gs-quant | 高盛开源量化金融工具包 | [GitHub](https://github.com/goldmansachs/gs-quant) |
| tf-quant-finance | 谷歌基于 TensorFlow 的高性能量化金融库 | [GitHub](https://github.com/google/tf-quant-finance) |
| rateslib | 固收定价库（债券、期货、IRS、交叉货币掉期） | [GitHub](https://github.com/attack68/rateslib) |
| PyQL | QuantLib 的 Python 移植 | [GitHub](https://github.com/enthought/pyql) |
| vollib / py_vollib | 期权价格、隐含波动率和希腊值计算 | [GitHub](https://github.com/vollib/vollib) |
| pysabr | SABR 模型 Python 实现 | [GitHub](https://github.com/ynouri/pysabr) |
| ffn | 金融函数库 | [GitHub](https://github.com/pmorissette/ffn) |
| pynance | 轻量级金融数据分析库 | [GitHub](https://github.com/GriffinAustin/pynance) |
| willowtree | 柳树格点法衍生品定价 | [GitHub](https://github.com/federicomariamassari/willowtree) |
| AbsBox | 资产支持证券 (ABS) 和抵押贷款支持证券 (MBS) 现金流建模 | [GitHub](https://github.com/yellowbean/AbsBox) |
| Intrinsic-Value-Calculator | 基于 DCF 的股票内在价值计算 | [GitHub](https://github.com/akashaero/Intrinsic-Value-Calculator) |
| Kelly-Criterion | 凯利公式仓位管理 | [GitHub](https://github.com/deltaray-io/kelly-criterion) |
| fypy | 香草和奇异期权定价，支持 Heston 等模型校准 | [GitHub](https://github.com/jkirkby3/fypy) |
| Pyderivatives | 期权定价、隐含波动率曲面和风险中性密度 | [GitHub](https://github.com/Julian-Beatty/Pyderivatives) |
| optionlab | 期权交易策略评估 | [GitHub](https://github.com/rgaveiga/optionlab) |
| quantra | 基于 QuantLib 的高性能定价引擎（gRPC/REST API） | [GitHub](https://github.com/joseprupi/quantraserver) |
| QuantOracle | 免费量化金融 API，含期权定价、蒙特卡洛、VaR 等 63 个端点 | [官网](https://quantoracle.dev) |
| mortgagemath | 精确到分的抵押贷款摊销计算 | [GitHub](https://github.com/murraystokely/mortgagemath) |

### R

| 名称 | 说明 | 链接 |
|------|------|------|
| RQuantLib | R 与 QuantLib 的连接 | [GitHub](https://github.com/eddelbuettel/rquantlib) |
| quantmod | 量化金融建模框架 | [CRAN](https://cran.r-project.org/web/packages/quantmod/index.html) |
| Rmetrics | 开源量化金融教学套件 | [官网](https://www.rmetrics.org) |
| YieldCurve | 收益率曲线建模与估计 | [CRAN](https://cran.r-project.org/web/packages/YieldCurve/index.html) |
| LSMonteCarlo | 最小二乘蒙特卡洛法美式期权定价 | [CRAN](https://cran.r-project.org/web/packages/LSMonteCarlo/index.html) |
| OptionPricing | 高效模拟算法期权定价 | [CRAN](https://cran.r-project.org/web/packages/OptionPricing/index.html) |
| credule | 信用违约掉期 (CDS) 函数 | [GitHub](https://github.com/blenezet/credule) |
| fmbasics | 金融市场基础构件 | [GitHub](https://github.com/imanuelcostigan/fmbasics) |

### 其他语言

| 名称 | 语言 | 说明 | 链接 |
|------|------|------|------|
| QuantLib.jl | Julia | QuantLib 的 Julia 实现 | [GitHub](https://github.com/pazzo83/QuantLib.jl) |
| Miletus.jl | Julia | 金融合约定义、建模语言和估值框架 | [GitHub](https://github.com/JuliaComputing/Miletus.jl) |
| Strata | Java | OpenGamma 现代开源分析和市场风险库 | [官网](http://strata.opengamma.io/) |
| JQuantLib | Java | 100% Java 编写的综合量化金融框架 | [GitHub](https://github.com/frgomes/jquantlib) |
| finmath.net | Java | 数学金融算法和方法库 | [官网](http://finmath.net) |
| QuantMath | Rust | 风险中性定价和风险计算库 | [GitHub](https://github.com/MarcusRainbow/QuantMath) |
| RustQuant | Rust | Rust 量化金融库 | [GitHub](https://github.com/avhz/RustQuant) |
| finance.js | JavaScript | 常用金融计算 | [GitHub](https://github.com/ebradyjobory/finance.js) |

---

## 3. 技术指标

技术分析指标库，用于趋势识别、动量分析和交易信号生成。

| 名称 | 语言 | 说明 | 链接 |
|------|------|------|------|
| TA-Lib | Python | 最权威的技术分析库（C 库的 Python 封装） | [GitHub](https://github.com/mrjbq7/ta-lib) |
| ta | Python | 基于 Pandas 的技术分析库 | [GitHub](https://github.com/bukosabino/ta) |
| finta | Python | 常用金融技术分析指标的 Pandas 实现 | [GitHub](https://github.com/peerchemist/finta) |
| pandas_talib | Python | Pandas 实现的技术分析指标 | [GitHub](https://github.com/femtotrader/pandas_talib) |
| Tulipy | Python | tulipindicators 的 Python 绑定 | [GitHub](https://github.com/cirla/tulipy) |
| talipp | Python | 增量式技术分析库（支持流式数据） | [GitHub](https://github.com/nardew/talipp) |
| streaming_indicators | Python | 流式数据技术分析指标 | [GitHub](https://github.com/mr-easy/streaming_indicators) |
| bta-lib | Python | pandas 技术分析库，用于回测 | [GitHub](https://github.com/mementum/bta-lib) |
| TuneTA | Python | 基于距离相关性优化技术指标 | [GitHub](https://github.com/jmrichardson/tuneta) |
| lppls | Python | 对数周期幂律奇异性 (LPPLS) 模型拟合 | [GitHub](https://github.com/Boulder-Investment-Technologies/lppls) |
| TTR | R | 技术交易规则 | [GitHub](https://github.com/joshuaulrich/TTR) |
| Indicators.jl | Julia | 基于 Temporal 的技术分析指标 | [GitHub](https://github.com/dysonance/Indicators.jl) |
| MarketTechnicals.jl | Julia | 基于 TimeSeries 的技术分析 | [GitHub](https://github.com/JuliaQuant/MarketTechnicals.jl) |
| OnlineTechnicalIndicators.jl | Julia | 在线算法技术指标 | [GitHub](https://github.com/femtotrader/OnlineTechnicalIndicators.jl) |
| ta4j | Java | Java 技术分析库 | [GitHub](https://github.com/ta4j/ta4j) |
| IndicatorTS | JavaScript/TypeScript | 股票技术分析指标、策略和回测框架 | [GitHub](https://github.com/cinar/indicatorts) |
| IndicatorGo | Golang | Go 语言技术分析指标和策略 | [GitHub](https://github.com/cinar/indicator) |
| fin-primitives | Rust | 金融原语：价格/数量/符号类型、订单簿、OHLCV 聚合、SMA/EMA/RSI | [GitHub](https://github.com/Mattbusel/fin-primitives) |

---

## 4. 交易与回测

策略开发、回测引擎和实盘交易框架。

### Python 综合框架

| 名称 | 说明 | 链接 |
|------|------|------|
| Qlib | 微软 AI 量化投资平台，覆盖 alpha 挖掘到订单执行全链路 | [GitHub](https://github.com/microsoft/qlib) |
| Lean | QuantConnect 算法交易引擎（Python + C#） | [GitHub](https://github.com/QuantConnect/Lean) |
| zipline / zipline-reloaded | Pythonic 算法交易库（Quantopian 出品） | [GitHub](https://github.com/quantopian/zipline) |
| backtrader | Python 回测库，社区活跃 | [GitHub](https://github.com/backtrader/backtrader) |
| vnpy | VeighNa 量化交易系统开发框架 | [GitHub](https://github.com/vnpy/vnpy) |
| nautilus_trader | 高性能算法交易平台和事件驱动回测器 | [GitHub](https://github.com/nautechsystems/nautilus_trader) |
| Lumibot | 统一回测和实盘的算法交易框架，支持多券商 | [GitHub](https://github.com/Lumiwealth/lumibot) |
| freqtrade | 免费开源加密货币交易机器人 | [GitHub](https://github.com/freqtrade/freqtrade) |
| jesse | 高级加密货币交易机器人 | [GitHub](https://github.com/jesse-ai/jesse) |
| rqalpha | 可扩展的 Python 算法回测和交易框架 | [GitHub](https://github.com/ricequant/rqalpha) |
| FinRL-Library | 深度强化学习自动交易库 (NeurIPS 2020) | [GitHub](https://github.com/AI4Finance-LLC/FinRL-Library) |
| vectorbt | 高性能回测、算法交易和研究工具包 | [GitHub](https://github.com/polakowo/vectorbt) |
| pysystemtrade | Robert Carver 的开源回测和交易引擎 | [GitHub](https://github.com/robcarver17/pysystemtrade) |
| Hikyuu | Python/C++ 高性能量化框架 | [GitHub](https://github.com/fasiondog/hikyuu) |
| ccxt | 支持 100+ 加密货币交易所的统一 API | [GitHub](https://github.com/ccxt/ccxt) |

### Python 专用工具

| 名称 | 说明 | 链接 |
|------|------|------|
| bt | 灵活的 Python 回测框架 | [GitHub](https://github.com/pmorissette/bt) |
| QSTrader | 回测模拟引擎 | [GitHub](https://github.com/mhallsmoore/qstrader) |
| Blankly | 集成回测、纸盘和实盘部署 | [GitHub](https://github.com/Blankly-Finance/Blankly) |
| Backtesting.py | Python 回测策略 | [官网](https://kernc.github.io/backtesting.py/) |
| quantstats | 量化组合分析 | [GitHub](https://github.com/ranaroussi/quantstats) |
| fastquant | 3 行代码即可回测投资策略 | [GitHub](https://github.com/enzoampil/fastquant) |
| AutoTrader | 从回测到优化到实盘的开发平台 | [GitHub](https://github.com/kieran-mackle/AutoTrader) |
| PyBroker | 机器学习算法交易 | [GitHub](https://github.com/edtechre/pybroker) |
| hftbacktest | 高频交易和做市回测工具 | [GitHub](https://github.com/nkaz001/hftbacktest) |
| qf-lib | 高质量量化金融工具库 | [GitHub](https://github.com/quarkfin/qf_lib) |
| investing-algorithm-framework | 自动交易算法开发、回测和部署框架 | [GitHub](https://github.com/coding-kitties/investing-algorithm-framework) |
| the0 | 多语言算法交易机器人自托管执行引擎 | [GitHub](https://github.com/alexanderwanyoike/the0) |
| StrateQueue | 从任意回测引擎无缝部署到实盘交易 | [GitHub](https://github.com/StrateQueue/StrateQueue) |
| antback | 轻量级事件循环式回测引擎 | [GitHub](https://github.com/ts-kontakt/antback) |
| backtester-mcp | 本地优先回测引擎，内置过拟合检查 | [PyPI](https://pypi.org/project/backtester-mcp/) |
| PyLOB | 完整的限价订单簿实现 | [GitHub](https://github.com/DrAshBooth/PyLOB) |
| Sextant | 本地事件驱动回测引擎，无代码策略构建 | [GitHub](https://github.com/raphaub-hub/SEXTANT) |

### AI 驱动交易

| 名称 | 说明 | 链接 |
|------|------|------|
| AI Quant Agents | 多智能体 LLM 交易分析（12 个 AI 代理辩论选股） | [GitHub](https://github.com/demandai/ai-quant-agents) |
| Vibe-Trading | 自然语言多智能体金融研究（7 回测引擎、29 预设） | [GitHub](https://github.com/HKUDS/Vibe-Trading) |
| TradeSight | 自托管 AI 交易平台 | [GitHub](https://github.com/rmbell09-lang/tradesight) |
| DeepAlpha | AI 加密货币交易机器人（70.9% 样本外准确率） | [官网](https://deepalphabot.com) |
| OpenFinClaw | AI 原生对冲基金平台，自然语言生成策略 | [GitHub](https://github.com/cryptoSUN2049/openFinclaw) |

### R / Julia / 其他语言

| 名称 | 语言 | 说明 | 链接 |
|------|------|------|------|
| quantstrat | R | 交易系统构建和模拟基础设施 | [GitHub](https://github.com/braverock/quantstrat) |
| blotter | R | 交易基础设施（工具、交易、组合、账户） | [GitHub](https://github.com/braverock/blotter) |
| Fastback.jl | Julia | 极速回测器 | [GitHub](https://github.com/rbeeli/Fastback.jl) |
| Strategems.jl | Julia | 量化系统化策略开发和回测 | [GitHub](https://github.com/dysonance/Strategems.jl) |
| StockSharp | C# | 算法和量化交易平台 | [GitHub](https://github.com/StockSharp/StockSharp) |
| Barter | Rust | 事件驱动实盘交易和回测框架 | [GitHub](https://github.com/barter-rs/barter-rs) |
| Kelp | Golang | 加密货币算法交易机器人 | [GitHub](https://github.com/stellar/kelp) |
| Tai | Elixir | 实时市场数据和交易执行工具 | [GitHub](https://github.com/fremantle-capital/tai) |
| TradeFrame | C++ | 基于 C++17 的期权自动交易框架 | [GitHub](https://github.com/rburkholder/trade-frame) |

---

## 5. 组合优化与风险分析

投资组合构建、风险度量和绩效分析。

### Python

| 名称 | 说明 | 链接 |
|------|------|------|
| PyPortfolioOpt | 经典有效前沿和高级组合优化方法 | [GitHub](https://github.com/robertmartin8/PyPortfolioOpt) |
| Riskfolio-Lib | 组合优化和战略资产配置 | [GitHub](https://github.com/dcajasn/Riskfolio-Lib) |
| skfolio | 基于 scikit-learn 的组合优化库 | [GitHub](https://github.com/skfolio/skfolio) |
| pyfolio / pyfolio-reloaded | 组合和风险分析 | [GitHub](https://github.com/quantopian/pyfolio) |
| empyrical / empyrical-reloaded | 常用金融风险和绩效指标 | [GitHub](https://github.com/quantopian/empyrical) |
| mlfinlab | Marcos Lopez de Prado《金融机器学习》实现 | [GitHub](https://github.com/hudson-and-thames/mlfinlab) |
| riskparity.py | 基于 TensorFlow 的风险平价组合设计 | [GitHub](https://github.com/dppalomar/riskparity.py) |
| DeepDow | 深度学习组合优化 | [GitHub](https://github.com/jankrepl/deepdow) |
| Eiten | 特征组合、最小方差组合、最大夏普比组合等 | [GitHub](https://github.com/tradytics/eiten) |
| FinQuant | 金融组合管理、分析和优化 | [GitHub](https://github.com/fmilthaler/FinQuant) |
| fortitudo.tech | CVaR 组合优化和熵池视图/压力测试 | [GitHub](https://github.com/fortitudo-tech/fortitudo.tech) |
| universal-portfolios | 在线组合选择算法集合 | [GitHub](https://github.com/Marigold/universal-portfolios) |
| QuantLibRisks | QuantLib 快速风险计算 | [GitHub](https://github.com/auto-differentiation/QuantLib-Risks-Py) |
| XAD | 自动微分 (AAD) 库 | [GitHub](https://github.com/auto-differentiation/xad-py) |
| AutoHypothesis | 模拟真实量化交易流水线的智能体框架 | [GitHub](https://github.com/arteemg/AutoHypothesis) |
| etfray | 终端 ETF 研究和组合分析工具 | [GitHub](https://github.com/alwank/etfray) |

### R / Julia / JavaScript

| 名称 | 语言 | 说明 | 链接 |
|------|------|------|------|
| PortfolioAnalytics | R | 组合分析与数值优化 | [GitHub](https://github.com/braverock/PortfolioAnalytics) |
| PerformanceAnalytics | R | 绩效和风险分析计量工具 | [GitHub](https://github.com/braverock/PerformanceAnalytics) |
| riskParityPortfolio | R | 极速风险平价组合设计 | [GitHub](https://github.com/dppalomar/riskParityPortfolio) |
| OnlinePortfolioAnalytics.jl | Julia | 在线算法组合分析 | [GitHub](https://github.com/femtotrader/OnlinePortfolioAnalytics.jl) |
| RiskPerf.jl | Julia | 时序风险和绩效分析 | [GitHub](https://github.com/rbeeli/RiskPerf.jl) |
| portfolio-allocation | JavaScript | 多资产组合构建 | [GitHub](https://github.com/lequant40/portfolio_allocation_js) |
| Ghostfolio | JavaScript | 财富管理软件，跟踪股票、ETF、加密货币 | [GitHub](https://github.com/ghostfolio/ghostfolio) |

---

## 6. 因子分析

Alpha 因子研究、挖掘和评估。

| 名称 | 语言 | 说明 | 链接 |
|------|------|------|------|
| alphalens / alphalens-reloaded | Python | 预测性 alpha 因子绩效分析 | [GitHub](https://github.com/quantopian/alphalens) |
| Spectre | Python | GPU 加速因子分析和回测 | [GitHub](https://github.com/Heerozh/spectre) |
| Alpha Skills | Python | AI 驱动量化因子研究技能集 | [GitHub](https://github.com/VernonOY/alpha-skills) |
| QuantGPT | Python | 智能体驱动 A 股因子研究引擎 | [GitHub](https://github.com/Miasyster/QuantGPT) |
| FactorAnalytics | R | 三种因子模型（基本面、时序、统计）的拟合和分析 | [GitHub](https://github.com/braverock/FactorAnalytics) |
| covFactorModel | R | 因子模型协方差矩阵估计 | [GitHub](https://github.com/dppalomar/covFactorModel) |
| Expected Returns | R | 组合多元化增强和经典论文复现 | [GitHub](https://github.com/JustinMShea/ExpectedReturns) |

---

## 7. 情绪分析与另类数据

市场情绪、社交媒体分析和非传统数据源。

| 名称 | 语言 | 说明 | 链接 |
|------|------|------|------|
| Asset News Sentiment Analyzer | Python | 基于 GPT 的金融资产情绪分析和报告生成 | [GitHub](https://github.com/KVignesh122/AssetNewsSentimentAnalyzer) |
| Social Stock Sentiment API | Python | Reddit 和 X/Twitter 股票提及和情绪 REST API | [官网](https://api.adanos.org/docs) |
| CoWorker Fin-Agent | Python | LLM 驱动 A 股分析（P2P 代理协作） | [GitHub](https://github.com/ZiwayZhao/agent-coworker) |
| StockKit | TypeScript | AI 驱动美股/港股/A 股研究报告 | [官网](https://stockkit.net/) |

---

## 8. 时间序列分析

时间序列建模、预测和平滑。

### Python

| 名称 | 说明 | 链接 |
|------|------|------|
| statsmodels | 统计模型探索、估计和检验 | [官网](http://statsmodels.sourceforge.net) |
| ARCH | ARCH/GARCH 模型 | [GitHub](https://github.com/bashtage/arch) |
| Facebook Prophet | 多季节性高质量时序预测 | [GitHub](https://github.com/facebook/prophet) |
| pmdarima | Python 自动 ARIMA（类似 R 的 auto.arima） | [GitHub](https://github.com/alkaline-ml/pmdarima) |
| tsfresh | 时序数据自动特征提取 | [GitHub](https://github.com/blue-yonder/tsfresh) |
| PyFlux | 时序建模和推断（频率和贝叶斯） | [GitHub](https://github.com/RJT1990/pyflux) |
| gluon-ts | 概率时序建模 | [GitHub](https://github.com/awslabs/gluon-ts) |
| tsmoothie | 时序平滑和异常检测 | [GitHub](https://github.com/cerlymarco/tsmoothie) |
| functime | 基于 Polars 的大规模时序机器学习 | [GitHub](https://github.com/functime-org/functime) |
| OmniOracle | 500+ 时序数据自动非平凡统计关系发现 | [GitHub](https://github.com/cesabici-bit/omni-oracle) |

### R / Julia

| 名称 | 语言 | 说明 | 链接 |
|------|------|------|------|
| rugarch | R | 单变量 GARCH 模型 | [GitHub](https://github.com/alexiosg/rugarch) |
| rmgarch | R | 多变量 GARCH 模型 | [GitHub](https://github.com/alexiosg/rmgarch) |
| tidyquant | R | 将金融分析引入 tidyverse | [GitHub](https://github.com/business-science/tidyquant) |
| timetk | R | 时序处理工具包 | [GitHub](https://github.com/business-science/timetk) |
| matrixprofile | R | 基于 Matrix Profile 的时序数据挖掘 | [GitHub](https://github.com/matrix-profile-foundation/matrixprofile) |
| TimeSeries.jl | Julia | Julia 时序工具包 | [GitHub](https://github.com/JuliaStats/TimeSeries.jl) |

---

## 9. 市场数据源

数据获取、下载和 API 封装。

### 综合数据源

| 名称 | 语言 | 说明 | 链接 |
|------|------|------|------|
| yfinance | Python | Yahoo Finance 数据下载器 | [GitHub](https://github.com/ranaroussi/yfinance) |
| akshare | Python | 优雅简洁的金融数据接口库 | [GitHub](https://github.com/jindaxiang/akshare) |
| FinanceDataReader | Python | 美股/韩股/日股/港股/越南股数据读取 | [GitHub](https://github.com/FinanceData/FinanceDataReader) |
| pandas-datareader | Python | 多源数据（Google/Yahoo/FRED/OECD 等）获取 | [GitHub](https://github.com/pydata/pandas-datareader) |
| findatapy | Python | Bloomberg/Quandl/Yahoo 等多源下载 | [GitHub](https://github.com/cuemacro/findatapy) |
| investpy | Python | Investing.com 数据提取 | [GitHub](https://github.com/alvarobartt/investpy) |
| FinanceDatabase | Python | 30 万+ 证券符号数据库 | [GitHub](https://github.com/JerBouma/FinanceDatabase) |
| tushare | Python | A 股历史和实时行情数据 | [PyPI](https://pypi.org/project/tushare/) |
| alpaca-trade-api | Python | Alpaca API 实时/历史价格和交易执行 | [GitHub](https://github.com/alpacahq/alpaca-trade-api-python) |
| tiingo | Python | 日复合价格/OHLC/成交量 + 实时新闻 | [GitHub](https://github.com/hydrosquall/tiingo-python) |
| iexfinance / pyEX | Python | IEX 交易所实时/历史数据 | [GitHub](https://github.com/addisonlynch/iexfinance) |
| polygon.io | Python | Polygon.io 金融数据 API | [GitHub](https://github.com/polygon-io/client-python) |
| alpha_vantage | Python | Alpha Vantage API 封装 | [GitHub](https://github.com/RomelTorres/alpha_vantage) |
| finagg | Python | 免费金融 API 实现、SQL 聚合和特征转换 | [GitHub](https://github.com/theOGognf/finagg) |
| edgartools | Python | AI 原生 SEC EDGAR 库（XBRL 财务数据） | [GitHub](https://github.com/dgunning/edgartools) |
| fedfred | Python | FRED 和 GeoFRED 经济数据 API | [官网](https://nikhilxsunder.github.io/fedfred/) |

### 加密货币

| 名称 | 语言 | 说明 | 链接 |
|------|------|------|------|
| coinpaprika-api-python-client | Python | 免费加密货币市场数据 API（12000+ 币种） | [GitHub](https://github.com/coinpaprika/coinpaprika-api-python-client) |
| dexpaprika-sdk-python | Python | 免费 DEX 数据 API（34 条链、3000 万+ 池） | [GitHub](https://github.com/coinpaprika/dexpaprika-sdk-python) |
| pricehub | Python | 统一多交易所 OHLC 价格采集 | [GitHub](https://github.com/eslazarev/pricehub) |
| coinmarketcap | Python | CoinMarketCap API 封装 | [GitHub](https://github.com/barnumbirr/coinmarketcap) |
| Trading Strategy | Python | 去中心化交易所和借贷协议价格数据 | [GitHub](https://github.com/tradingstrategy-ai/trading-strategy/) |
| tardis-python | Python | 高频加密货币市场数据 | [GitHub](https://github.com/tardis-dev/tardis-python) |

### R 数据接口

| 名称 | 说明 | 链接 |
|------|------|------|
| IBrokers | Interactive Brokers TWS API 原生 R 访问 | [CRAN](https://cran.r-project.org/web/packages/IBrokers/index.html) |
| Rblpapi | Bloomberg R 接口 | [GitHub](https://github.com/Rblp/Rblpapi) |
| tidyfinance | Tidy Finance 辅助函数 | [GitHub](https://github.com/tidy-finance/r-tidyfinance) |

### 日本市场

| 名称 | 说明 | 链接 |
|------|------|------|
| edinetdb | 日本公司财务免费 API（3800+ 上市公司） | [官网](https://edinetdb.com/) |
| edinet-mcp | 日本 XBRL 财务报表解析 | [GitHub](https://github.com/ajtgjmdjp/edinet-mcp) |
| tdnet-disclosure-mcp | 日本上市公司及时披露信息 | [GitHub](https://github.com/ajtgjmdjp/tdnet-disclosure-mcp) |
| estat-mcp | 日本政府统计数据（人口、GDP、CPI 等） | [GitHub](https://github.com/ajtgjmdjp/estat-mcp) |

### MCP 服务器（AI 代理集成）

| 名称 | 说明 | 链接 |
|------|------|------|
| financekit-mcp | 17 个工具：实时报价、技术分析、风险指标、期权链等 | [GitHub](https://github.com/vdalhambra/financekit-mcp) |
| Helium MCP | 实时股票/ETF/加密货币数据 + ML 期权定价 | [官网](https://heliumtrades.com/mcp-page/) |
| Horus Flow | 亚秒级 L2 订单流情报 | [GitHub](https://github.com/horustechltd/horus-flow-mcp) |
| Chart Library MCP | 2400 万+ 预计算嵌入的历史图表模式搜索 | [官网](https://chartlibrary.io) |
| FilingFirehose | SEC EDGAR JSON API | [官网](https://filingfirehose.com) |
| SwapAPI | 免费 DEX 聚合 API（46 条 EVM 链） | [官网](https://swapapi.dev) |

---

## 10. 预测市场

预测市场数据、交易和套利工具。

| 名称 | 语言 | 说明 | 链接 |
|------|------|------|------|
| pmxt | Python/JS | 预测市场统一 API（Polymarket、Kalshi 等） | [GitHub](https://github.com/pmxt-dev/pmxt) |
| polymarket-whales | Python | Polymarket 大户交易实时追踪 | [GitHub](https://github.com/al1enjesus/polymarket-whales) |
| Polymarket Scanner API | Python | Polymarket 12000+ 市场实时套利检测 | [GitHub](https://github.com/vesper-astrena/polymarket-scanner-api) |
| SimpleFunctions | JS | Kalshi 和 Polymarket 预测市场智能 CLI | [GitHub](https://github.com/spfunctions/simplefunctions-cli) |
| PolyMind | Python | 多 AI 分析的 Polymarket 实时交易提醒 | [官网](https://polyminds.netlify.app/) |
| Oracle3 | Python | Kalshi/Polymarket/Solana 自主交易代理 | [GitHub](https://github.com/YichengYang-Ethan/oracle3) |

---

## 11. 日历与交易时间

交易所日历和营业日计算。

| 名称 | 语言 | 说明 | 链接 |
|------|------|------|------|
| exchange_calendars | Python | 股票交易所交易日历 | [GitHub](https://github.com/gerrymanoim/exchange_calendars) |
| pandas_market_calendars | Python | 适用于 pandas 的交易所日历 | [GitHub](https://github.com/rsheftel/pandas_market_calendars) |
| bizdays | Python | 营业日计算 | [GitHub](https://github.com/wilsonfreitas/python-bizdays) |
| timeDate | R | 时间和日历对象 | [CRAN](https://cran.r-project.org/web/packages/timeDate/index.html) |

---

## 12. 可视化

金融数据可视化工具。

| 名称 | 语言 | 说明 | 链接 |
|------|------|------|------|
| mplfinance | Python | matplotlib 金融数据可视化 | [GitHub](https://github.com/matplotlib/mplfinance) |
| D-Tale | Python | pandas DataFrame 可视化工具 | [GitHub](https://github.com/man-group/dtale) |
| finplot | Python | 高性能金融绘图 | [GitHub](https://github.com/highfestiva/finplot) |
| finvizfinance | Python | Finviz 分析库 | [GitHub](https://github.com/lit26/finvizfinance) |
| QuantInvestStrats | Python | 量化投资策略可视化和绩效报告 | [GitHub](https://github.com/ArturSepp/QuantInvestStrats) |
| LightweightCharts.jl | Julia | TradingView Lightweight Charts 的 Julia 封装 | [GitHub](https://github.com/bhftbootcamp/LightweightCharts.jl) |
| dxcharts-lite | JavaScript | 基于 HTML5 Canvas 的灵活金融图表库 | [GitHub](https://github.com/devexperts/dxcharts-lite) |

---

## 13. Excel 集成

Python 与 Excel 的集成方案。

| 名称 | 说明 | 链接 |
|------|------|------|
| xlwings | 用 Python 驱动 Excel | [官网](https://www.xlwings.org/) |
| openpyxl | 读写 Excel 2007 xlsx/xlsm 文件 | [文档](https://openpyxl.readthedocs.io/en/latest/) |
| xlsxwriter | 写 Excel 2007+ XLSX 文件 | [文档](https://xlsxwriter.readthedocs.io/) |
| xlrd | 从 Excel 文件提取数据 | [GitHub](https://github.com/python-excel/xlrd) |
| pyxll | Excel 插件，用 Python 扩展 Excel | [官网](https://www.pyxll.com) |
| Bilig | 公式工作底稿和 XLSX 重算运行时 | [GitHub](https://github.com/proompteng/bilig) |

---

## 14. 量化研究环境

开箱即用的量化研究开发环境。

| 名称 | 说明 | 链接 |
|------|------|------|
| Jupyter Quant | Docker 化 Jupyter 量化研究环境（预装 statsmodels、pymc、arch、zipline 等） | [GitHub](https://github.com/gnzsnz/jupyter-quant) |

---

## 15. 跨语言框架

在多种编程语言中均可使用的核心量化库。

| 名称 | 说明 | 链接 |
|------|------|------|
| QuantLib | 最全面的量化金融软件框架 | [GitHub](https://github.com/lballabio/QuantLib) |
| TA-Lib | 技术分析 C 库，提供多语言绑定 | [官网](https://ta-lib.org) |
| RunMat | MATLAB 语法高性能运行时（Rust 实现） | [官网](https://runmat.org) |

**QuantLib 生态：**

| 移植语言 | 项目 | 链接 |
|----------|------|------|
| Python | PyQL | [GitHub](https://github.com/enthought/pyql) |
| R | RQuantLib | [GitHub](https://github.com/eddelbuettel/rquantlib) |
| Java | JQuantLib | [GitHub](https://github.com/frgomes/jquantlib) |
| Julia | QuantLib.jl | [GitHub](https://github.com/pazzo83/QuantLib.jl) |
| .NET | QLNet | [GitHub](https://github.com/amaggiulli/qlnet) |
| Excel | QuantLibAddin / QuantLibXL | [官网](https://www.quantlib.org/quantlibaddin/) |

---

## 16. 学习资料与书籍

量化金融学习资源，包括教程、代码复现和书籍配套代码。

### 入门与综合教程

| 名称 | 说明 | 链接 |
|------|------|------|
| QuantEcon | 经济学、金融、计量经济学和数据科学讲座 | [官网](https://quantecon.org/) |
| Tidy Finance | 可复现金融研究的 Python/R 实现 | [官网](https://www.tidy-finance.org/) |
| J.P. Morgan Python Training | 摩根大通面向业务分析师和交易员的 Python 培训 | [GitHub](https://github.com/jpmorganchase/python-training) |
| QuantFinance | 量化金融培训材料 | [GitHub](https://github.com/PythonCharmers/QuantFinance) |
| IPythonScripts | Python 和 QuantLib 量化金融教程 | [GitHub](https://github.com/mgroncki/IPythonScripts) |
| Computational-Finance-Course | 计算金融课程材料 | [GitHub](https://github.com/LechGrzelak/Computational-Finance-Course) |
| Quantitative-Notebooks | 量化金融、算法交易和投资策略教育笔记本 | [GitHub](https://github.com/LongOnly/Quantitative-Notebooks) |
| Finance | 150+ 量化金融 Python 程序 | [GitHub](https://github.com/shashankvemuri/Finance) |

### 书籍配套代码

| 名称 | 对应书籍 | 链接 |
|------|----------|------|
| py4fi2nd | Python for Finance (2nd ed., O'Reilly) | [GitHub](https://github.com/yhilpisch/py4fi2nd) |
| aiif | Artificial Intelligence in Finance (O'Reilly) | [GitHub](https://github.com/yhilpisch/aiif) |
| py4at | Python for Algorithmic Trading (O'Reilly) | [GitHub](https://github.com/yhilpisch/py4at) |
| dawp | Derivatives Analytics with Python (Wiley) | [GitHub](https://github.com/yhilpisch/dawp) |
| machine-learning-for-trading | Machine Learning for Algorithmic Trading | [GitHub](https://github.com/stefan-jansen/machine-learning-for-trading) |
| algorithmic-trading-with-python | Algorithmic Trading with Python (2020) | [GitHub](https://github.com/chrisconlan/algorithmic-trading-with-python) |
| Python-for-Finance-Cookbook | Python for Finance Cookbook (Packt) | [GitHub](https://github.com/PacktPublishing/Python-for-Finance-Cookbook) |
| NMOF | Numerical Methods and Optimization in Finance | [GitHub](https://github.com/enricoschumann/NMOF) |
| ML_Finance_Codes | Machine Learning in Finance: From Theory to Practice | [GitHub](https://github.com/mfrdixon/ML_Finance_Codes) |
| AFML | Advances in Financial Machine Learning 习题答案 | [GitHub](https://github.com/boyboi86/AFML) |
| systematictradingexamples | Systematic Trading 配套示例 | [GitHub](https://github.com/robcarver17/systematictradingexamples) |
| QuantFinanceBook | 量化金融书籍 | [GitHub](https://github.com/LechGrzelak/QuantFinanceBook) |
| Portfolio Optimization Book | 组合优化书籍 | [官网](https://portfoliooptimizationbook.com/) |
| book_irds3 | Pricing and Trading Interest Rate Derivatives | [GitHub](https://github.com/attack68/book_irds3) |

### 经典论文复现

| 名称 | 说明 | 链接 |
|------|------|------|
| Derman Papers | Emanuel Derman 量化金融论文复现 | [GitHub](https://github.com/MarcosCarreira/DermanPapers) |
| volatility-trading | Euan Sinclair 波动率交易完整估计器 | [GitHub](https://github.com/jasonstrimpel/volatility-trading) |
| 101_formulaic_alphas | 101 个公式化 alpha 实现 | [GitHub](https://github.com/ram-ki/101_formulaic_alphas) |
| Autoencoder-Asset-Pricing-Models | 自编码器资产定价模型复现 | [GitHub](https://github.com/RichardS0268/Autoencoder-Asset-Pricing-Models) |
| Differential Machine Learning | 微分机器学习论文复现 | [GitHub](https://github.com/differential-machine-learning/notebooks) |
| RoughVolatilityWorkshop | 2024 QuantMind 粗糙波动率研讨会 | [GitHub](https://github.com/jgatheral/RoughVolatilityWorkshop) |
| MesoSim Options Strategy Library | 免费期权交易策略库 | [GitHub](https://github.com/deltaray-io/strategy-library) |
| Machine Learning Asset Management | 机器学习在资产管理中的应用 | [GitHub](https://github.com/firmai/machine-learning-asset-management) |
| Technical Analysis and Feature Engineering | 机器学习在金融市场的特征工程 | [GitHub](https://github.com/jo-cho/Technical_Analysis_and_Feature_Engineering) |
| AlgoTradingLib | 算法交易库、框架、策略和教育材料目录 | [官网](https://github.com/usdaud/algotradinglib.github.io) |
| cipher-starter | 加密货币量化入门套件 | [GitHub](https://github.com/cryptomotifs/cipher-starter) |

---

## 17. 商业服务

商业数据、分析和交易平台。

| 名称 | 说明 | 链接 |
|------|------|------|
| Nasdaq Data Link | 金融数据 API（前身为 Quandl） | [官网](https://data.nasdaq.com/tools/full-list) |
| SaxoOpenAPI | 盛宝银行金融数据 API | [官网](https://www.developer.saxo/) |
| Portfolio Optimizer | 组合分析和优化 Web API | [官网](https://portfoliooptimizer.io/) |
| Parsec | 预测市场 API（5 个交易所数据和执行） | [官网](https://parsecfinance.com) |
| Chartscout | 加密货币图表模式实时检测 | [官网](https://chartscout.io) |
| DayTradingBench | LLM 交易绩效实时自主基准 | [官网](https://daytradingbench.com) |
| CoinTester | 无代码加密货币回测平台 | [官网](https://cointester.io) |
| goMacro.ai | AI 驱动经济日历 | [官网](https://gomacro.ai) |
| StockAInsights | AI 提取的财务报表 API | [官网](https://stockainsights.com) |
| StockVektor | 免费美股研究（Piotroski F-Score 等质量评分） | [官网](https://stockvektor.com) |
| brapi.dev | 巴西股票市场数据 API | [官网](https://brapi.dev/) |
| 13F Insight | 机构投资者 13F 持仓跟踪 | [官网](https://13finsight.com/) |
| Earnings Feed | 实时 SEC 文件、内部交易和机构持仓 API | [官网](https://earningsfeed.com/api) |
| Financial Data | 股票市场和金融数据 API | [官网](https://financialdata.net/) |
| RealMarketAPI | 超低延迟黄金、外汇、加密货币和股票数据 | [官网](https://realmarketapi.com/) |
| Sharpe | AI 驱动加密货币交易智能终端 | [官网](https://www.sharpe.ai/) |
| ValueRay | 技术/量化/情绪数据 + AI 代理优化 | [官网](https://www.valueray.com/api) |
| VertData | 机构级金融情报（国会交易、SEC 内部文件等） | [官网](https://vertdata.com) |
| ML-Quant | 顶级量化资源汇总 | [官网](https://www.ml-quant.com/) |
| GitDealFlow | 替代数据信号平台（GitHub stars、招聘速度等） | [官网](https://gitdealflow.com) |
| KeepRule | 巴菲特和芒格等大师决策原则库 | [官网](https://keeprule.com/) |
| FXMacroData | 实时外汇宏观经济 API | [官网](https://fxmacrodata.com/) |
| The Stock Radar | 每日多语言股票分析报告（6 个市场、6 种语言） | [官网](https://thestockradar.com) |
| Webb Database | 港交所/英国公司注册处等公开金融数据聚合 | [官网](https://webb-database.com/) |
| bolsai | 巴西股票市场数据 REST API 和 MCP 服务器 | [官网](https://usebolsai.com) |
| RTPR | 实时新闻稿 API（Business Wire/PR Newswire 等） | [官网](https://rtpr.io) |
| System R | AI 原生风险智能 API | [官网](https://agents.systemr.ai) |
| Telonex | 逐笔预测市场数据 | [官网](https://telonex.io) |
| Reddit WallstreetBets API | Reddit WallstreetBets 每日热门股票和情绪 | [官网](https://dashboard.nbshare.io/apps/reddit/api/) |

---

## 18. 核心要点总结

### 技术栈推荐

| 用途 | 推荐工具 |
|------|----------|
| 数据处理基础 | pandas + NumPy（Python）/ data.table（R） |
| 技术指标 | TA-Lib（最全）、ta / finta（纯 Python） |
| 策略回测 | backtrader（入门）、zipline-reloaded（进阶）、Qlib（AI 驱动）、Lean（多语言） |
| 期权定价 | FinancePy、QuantLib 生态 |
| 组合优化 | PyPortfolioOpt（入门）、Riskfolio-Lib（高级）、skfolio（ML 集成） |
| 风险分析 | pyfolio + empyrical |
| 因子分析 | alphalens-reloaded |
| 时序建模 | statsmodels + Prophet + pmdarima |
| 数据获取 | yfinance（免费）、akshare（A 股）、Bloomberg（专业） |
| 可视化 | mplfinance + D-Tale |
| 加密货币交易 | ccxt（统一 API）、freqtrade（机器人） |

### 学习路径

1. **基础**：NumPy/pandas --> 技术指标（TA-Lib）--> 简单策略回测（backtrader）
2. **进阶**：组合优化（PyPortfolioOpt）--> 因子分析（alphalens）--> 风险度量（pyfolio）
3. **高级**：机器学习交易（Qlib、FinRL）--> 高频交易 --> 自建交易系统
4. **持续学习**：QuantEcon 讲座 --> 经典书籍配套代码 --> 论文复现

### 关键原则

- 优先选择社区活跃、文档完善的开源项目
- 回测结果不代表实盘表现，需考虑滑点、手续费和市场冲击
- 多数据源交叉验证，避免单一数据源偏差
- 风险管理始终优先于收益追求
