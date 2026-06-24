# Qlib：量化投资平台

## 简介

Qlib 是由微软研究院开发的开源、面向 AI 的量化投资平台。它为量化研究提供了全面的基础设施，包括数据管理、模型训练、回测和投资组合优化。Qlib 支持机器学习工作流，使研究人员和从业者能够开发和评估交易策略。

**核心功能：**

- 端到端量化研究平台
- 高性能数据管理
- 机器学习模型集成
- 回测框架
- 投资组合优化
- 风险分析工具
- 因子分析能力
- 可扩展架构

---

## 安装

### 系统要求

| 组件 | 最低 | 推荐 |
|-----------|---------|-------------|
| Python | 3.7 | 3.9+ |
| 内存 | 4 GB | 16 GB |
| 存储 | 10 GB | 50 GB |
| CPU | 2 核 | 8 核 |
| 操作系统 | Linux、macOS、Windows | Linux |

### 通过 pip 安装

```bash
pip install pyqlib
```

### 从源码安装

```bash
git clone https://github.com/microsoft/qlib.git
cd qlib
pip install -e ".[dev]"
```

### 安装附加依赖

```bash
# 完整安装，包含所有功能
pip install pyqlib[dev,plot]

# 安装特定 ML 框架
pip install pyqlib torch
pip install pyqlib tensorflow
```

### 验证安装

```python
import qlib
print(qlib.__version__)

# 初始化 Qlib
qlib.init(provider_uri='~/.qlib/qlib_data/cn_data')
```

---

## 数据准备

### 下载市场数据

Qlib 提供内置脚本下载市场数据：

**中国 A 股市场：**
```bash
python scripts/get_data.py qlib_data --target_dir ~/.qlib/qlib_data/cn_data --region cn
```

**美国股票市场：**
```bash
python scripts/get_data.py qlib_data --target_dir ~/.qlib/qlib_data/us_data --region us
```

### 数据结构

| 组件 | 描述 |
|-----------|-------------|
| `calendars/` | 交易日历文件 |
| `instruments/` | 股票池定义 |
| `features/` | 价格和特征数据 |
| `raw/` | 原始下载数据 |

### 支持的数据源

| 来源 | 类型 | 覆盖范围 |
|--------|------|----------|
| Yahoo Finance | 历史价格 | 全球市场 |
| Tushare | 中国市场数据 | 中国 A 股 |
| AKShare | 金融数据 | 中国市场 |
| 自定义 CSV | 用户提供 | 任何市场 |

### 数据格式

Qlib 使用特定的二进制格式以提高效率：

| 文件 | 内容 |
|------|---------|
| `.day.bin` | 每日价格数据 |
| `features/*.bin` | 单个特征数据 |
| `instruments/all.txt` | 工具列表 |

### 自定义数据准备

准备您自己的数据以在 Qlib 中使用：

```python
import pandas as pd
from qlib.data.storage import CalendarStorage, InstrumentStorage

# 加载自定义 CSV 数据
df = pd.read_csv('my_data.csv')

# 必需列
# date, instrument, open, high, low, close, volume
```

---

## 配置

### Qlib 初始化

```python
import qlib
from qlib.config import REG_CN, REG_US

# 初始化中国市场
qlib.init(
    provider_uri='~/.qlib/qlib_data/cn_data',
    region=REG_CN,
)

# 初始化美国市场
qlib.init(
    provider_uri='~/.qlib/qlib_data/us_data',
    region=REG_US,
)
```

### 配置参数

| 参数 | 描述 | 默认值 |
|-----------|-------------|---------|
| `provider_uri` | 数据目录路径 | 必填 |
| `region` | 市场区域（CN、US） | REG_CN |
| `expression_cache` | 缓存表达式 | True |
| `dataset_cache` | 缓存数据集 | True |
| `kernels` | 并行工作线程 | 1 |
| `mem_cache_size_limit` | 内存缓存限制 | 2GB |

---

## 特征工程

### 内置特征

Qlib 提供丰富的内置特征：

**价格特征：**

| 特征 | 表达式 | 描述 |
|---------|------------|-------------|
| 开盘价 | `$open` | 开盘价格 |
| 最高价 | `$high` | 最高价格 |
| 最低价 | `$lowest` | 最低价格 |
| 收盘价 | `$close` | 收盘价格 |
| 成交量 | `$volume` | 交易量 |
| VWAP | `$vwap` | 成交量加权平均价 |

**技术指标：**

| 指标 | 表达式 | 描述 |
|-----------|------------|-------------|
| MA5 | `Mean($close, 5)` | 5 日移动平均 |
| RSI | `Ref($close, 1) / $close` | 相对强弱 |
| MACD | 自定义表达式 | 移动平均收敛 |
| 布林带 | 自定义表达式 | 布林带 |

### 自定义特征

使用 Qlib 表达式定义自定义特征：

```python
from qlib.data import D

# 定义自定义特征
expressions = [
    'Ref($close, 1)',           # 前收盘价
    'Mean($close, 5)',          # 5 日 MA
    'Std($close, 20)',          # 20 日标准差
    '$close / Ref($close, 1)',  # 日收益率
]

# 获取特征数据
df = D.features(
    instruments=['SH000001'],
    expressions=expressions,
    start_time='2020-01-01',
    end_time='2023-12-31',
)
```

---

## 模型训练

### 内置模型

| 模型 | 类型 | 描述 |
|-------|------|-------------|
| LightGBM | 基于树 | 梯度提升 |
| XGBoost | 基于树 | 极端梯度提升 |
| CatBoost | 基于树 | 类别提升 |
| LSTM | 深度学习 | 长短期记忆网络 |
| GRU | 深度学习 | 门控循环单元 |
| Transformer | 深度学习 | 基于注意力的模型 |
| ALSTM | 深度学习 | 注意力 LSTM |
| TRA | 深度学习 | 基于轨迹 |

### 训练 LightGBM 模型

```python
import qlib
from qlib.contrib.model.gbdt import LGBModel
from qlib.data.dataset import DatasetH

# 初始化
qlib.init(provider_uri='~/.qlib/qlib_data/cn_data')

# 定义数据集
dataset_config = {
    "class": "DatasetH",
    "module_path": "qlib.data.dataset",
    "kwargs": {
        "handler": {
            "class": "Alpha158",
            "module_path": "qlib.contrib.data.handler",
            "kwargs": {
                "start_time": "2008-01-01",
                "end_time": "2020-12-31",
                "fit_start_time": "2008-01-01",
                "fit_end_time": "019-12-31",
                "instruments": "csi300",
            },
        },
        "segments": {
            "train": ("2008-01-01", "2019-12-31"),
            "valid": ("2020-01-01", "2020-12-31"),
            "test": ("2021-01-01", "2021-12-31"),
        },
    },
}

dataset = DatasetH(**dataset_config["kwargs"])

# 定义模型
model = LGBModel()

# 训练模型
model.fit(dataset)
```

### 训练深度学习模型

```python
from qlib.contrib.model.pytorch_lstm import LSTM

model_config = {
    "class": "LSTM",
    "module_path": "qlib.contrib.model.pytorch_lstm",
    "kwargs": {
        "d_feat": 6,
        "hidden_size": 64,
        "num_layers": 2,
        "dropout": 0.0,
        "n_epochs": 200,
        "lr": 0.001,
        "batch_size": 2000,
    },
}

model = LSTM(**model_config["kwargs"])
model.fit(dataset)
```

### 模型评估

| 指标 | 描述 | 理想值 |
|--------|-------------|-------------|
| IC | 信息系数 | > 0.05 |
| Rank IC | 排名信息系数 | > 0.05 |
| ICIR | IC 信息比率 | > 0.5 |
| 收益 | 年化收益 | 越高越好 |
| 最大回撤 | 最大回撤 | 越低越好 |
| 夏普比率 | 夏普比率 | > 1.0 |

---

## 回测

### 运行回测

```python
from qlib.contrib.evaluate import backtest_daily
from qlib.contrib.strategy import TopkDropoutStrategy

# 定义策略
strategy_config = {
    "class": "TopkDropoutStrategy",
    "module_path": "qlib.contrib.strategy",
    "kwargs": {
        "topk": 50,
        "n_drop": 5,
    },
}

# 运行回测
portfolio_metric, indicator = backtest_daily(
    start_time="2021-01-01",
    end_time="2021-12-31",
    strategy=strategy_config,
    executor={
        "class": "SimulatorExecutor",
        "module_path": "qlib.backtest.executor",
        "kwargs": {
            "time_per_step": "day",
            "generate_portfolio_metrics": True,
        },
    },
    model=model,
    dataset=dataset,
)
```

### 回测结果

| 指标 | 描述 |
|--------|-------------|
| 年化收益 | 年收益率百分比 |
| 年化波动率 | 年波动率 |
| 夏普比率 | 风险调整后收益 |
| 最大回撤 | 最大峰谷下降 |
| 卡玛比率 | 收益 / 最大回撤 |
| 胜率 | 盈利交易百分比 |
| 盈亏比 | 总盈利 / 总亏损 |

### 策略类型

| 策略 | 描述 |
|----------|-------------|
| TopkDropout | 选择前 K 只股票，每日卖出 N 只 |
| WeightStrategyBase | 基于权重的投资组合 |
| EnhancedIndexStrategy | 用 alpha 跟踪指数 |

---

## 投资组合优化

### 均值-方差优化

```python
from qlib.contrib.portfolio.optimizer import MeanVarianceOptimizer

optimizer = MeanVarianceOptimizer(
    lam=0.5,           # 风险厌恶参数
    tau=0.05,          # 预期收益的不确定性
    method='inv',      # 协方差反转方法
)

weights = optimizer.get_weight(
    expected_returns=expected_returns,
    cov_matrix=covariance_matrix,
)
```

### 优化方法

| 方法 | 描述 | 使用场景 |
|--------|-------------|----------|
| 均值-方差 | 经典 Markowitz | 通用 |
| 风险平价 | 等风险贡献 | 分散化 |
| 最小方差 | 最小化投资组合方差 | 保守型 |
| 最大夏普 | 最大化夏普比率 | 激进型 |

---

## 风险分析

### 风险指标

| 指标 | 公式 | 描述 |
|--------|---------|-------------|
| VaR | 收益的百分位数 | 风险价值 |
| CVaR | 尾部损失的均值 | 条件风险价值 |
| Beta | 与市场的协方差 | 市场敏感度 |
| Alpha | 超越基准的超额收益 | 技能收益 |
| 跟踪误差 | 超额收益的标准差 | 主动风险 |

### 计算风险指标

```python
from qlib.contrib.evaluate import risk_analysis

# 分析回测结果
risk_report = risk_analysis(portfolio_metric)

print(risk_report)
```

---

## 因子分析

### 因子评估

评估因子的预测能力：

```python
from qlib.contrib.evaluate import backtest_daily

# 单因子分析
factor_data = D.features(
    instruments='csi300',
    expressions=['$close / Ref($close, 5)'],
    start_time='2020-01-01',
    end_time='2021-12-31',
)

# 计算 IC
ic = factor_data.corrwith(returns)
print(f"IC: {ic.mean():.4f}")
print(f"ICIR: {ic.mean() / ic.std():.4f}")
```

### 因子类别

| 类别 | 示例 |
|----------|----------|
| 动量 | 价格动量、成交量动量 |
| 价值 | 市盈率、市净率 |
| 质量 | ROE、利润率 |
| 波动率 | 历史波动率、Beta |
| 流动性 | 换手率、Amihud 非流动性 |
| 规模 | 市值 |

---

## ML 模型对比

| 模型 | 速度 | 准确性 | 可解释性 | 内存 |
|-------|-------|----------|-----------------|--------|
| LightGBM | 快 | 高 | 中等 | 低 |
| XGBoost | 快 | 高 | 中等 | 低 |
| CatBoost | 中等 | 高 | 中等 | 中等 |
| LSTM | 慢 | 中等 | 低 | 高 |
| GRU | 慢 | 中等 | 低 | 高 |
| Transformer | 慢 | 高 | 低 | 高 |
| ALSTM | 慢 | 中等 | 低 | 高 |

---

## API 使用

### 数据 API

```python
from qlib.data import D

# 获取工具
instruments = D.instruments('csi300')
inst_list = D.list_instruments(instruments=instruments)

# 获取特征
features = D.features(
    instruments=['SH600000'],
    expressions=['$close', '$volume', 'Ref($close, 1)'],
    start_time='2020-01-01',
    end_time='2021-12-31',
)

# 获取日历
calendar = D.calendar(start_time='2020-01-01', end_time='2021-12-31')
```

### 模型 API

```python
# 预测
predictions = model.predict(dataset)

# 评估
from qlib.contrib.evaluate import backtest_daily
metrics = backtest_daily(predictions)
```

---

## 工作流自动化

### 使用 YAML 配置

Qlib 支持通过 YAML 进行工作流自动化：

```yaml
qlib_init:
    provider_uri: ~/.qlib/qlib_data/cn_data

data_handler_config: &data_handler_config
    start_time: 2008-01-01
    end_time: 2020-12-31
    fit_start_time: 2008-01-01
    fit_end_time: 2019-12-31
    instruments: csi300

task:
    model:
        class: LGBModel
        module_path: qlib.contrib.model.gbdt
        kwargs:
            loss: mse
            colsample_bytree: 0.8879
            learning_rate: 0.0421
            subsample: 0.8789
            lambda_l1: 205.6999
            lambda_l2: 580.9768
            max_depth: 8
            num_leaves: 210
    dataset:
        class: DatasetH
        module_path: qlib.data.dataset
        kwargs:
            handler:
                class: Alpha158
                module_path: qlib.contrib.data.handler
                kwargs: *data_handler_config
            segments:
                train: [2008-01-01, 2019-12-31]
                valid: [2020-01-01, 2020-12-31]
                test: [2021-01-01, 2021-12-31]
```

### 运行工作流

```bash
python qlib/cli/run_workflow.py --config workflow_config.yaml
```

---

## 故障排除

### 常见问题

| 问题 | 解决方案 |
|-------|----------|
| 数据下载失败 | 检查网络，尝试其他数据源 |
| 内存错误 | 减少数据量，增加内存 |
| 训练缓慢 | 减少特征，使用 GPU |
| 导入错误 | 重新安装依赖 |
| CUDA 错误 | 检查 GPU 驱动，使用 CPU 回退 |

### 性能建议

1. 使用 SSD 存储数据
2. 增加内存缓存大小
3. 启用并行处理
4. 使用适当的数据粒度
5. 分析代码以识别瓶颈

---

## 总结

Qlib 是一个强大的量化投资平台，为研究和交易提供端到端的基础设施。其数据管理、特征工程、模型训练和回测的集成使其成为量化研究人员的综合解决方案。该平台支持传统金融模型和现代机器学习方法，并为高级用户提供广泛的自定义选项。
