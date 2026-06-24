# Elasticsearch 教程：全文搜索引擎

## 简介

Elasticsearch 是一个基于 Apache Lucene 构建的分布式 RESTful 搜索和分析引擎。它擅长全文搜索、日志分析和实时数据探索，是 Elastic Stack 的核心组件。

## 架构概述

| 组件 | 角色 |
|------|------|
| Cluster（集群） | 协同工作的节点集合 |
| Node（节点） | 集群中的单个服务器实例 |
| Index（索引） | 具有相似结构的文档集合 |
| Shard（分片） | 存储在节点上的索引子集 |
| Replica（副本） | 用于冗余和性能的分片副本 |
| Document（文档） | 以 JSON 存储的基本信息单元 |

## 安装

### 使用 Docker

```bash
docker run -d \
  --name elasticsearch \
  -p 9200:9200 \
  -p 9300:9300 \
  -e "discovery.type=single-node" \
  -e "xpack.security.enabled=false" \
  docker.elastic.co/elasticsearch/elasticsearch:8.13.0
```

### 使用 APT（Debian/Ubuntu）

```bash
wget -qO - https://artifacts.elastic.co/GPG-KEY-elasticsearch | sudo apt-key add -
sudo apt-get install apt-transport-https
echo "deb https://artifacts.elastic.co/packages/8.x/apt stable main" | \
  sudo tee /etc/apt/sources.list.d/elastic-8.x.list
sudo apt-get update && sudo apt-get install elasticsearch
sudo systemctl start elasticsearch
```

## 集群健康状态

| 状态 | 含义 | 需要的操作 |
|------|------|-----------|
| Green（绿色） | 所有主分片和副本分片均活跃 | 无 |
| Yellow（黄色） | 所有主分片活跃，部分副本缺失 | 检查节点可用性 |
| Red（红色） | 部分主分片未活跃 | 立即排查 |

```bash
curl -X GET "localhost:9200/_cluster/health?pretty"
```

## 索引管理

### 创建索引

```bash
curl -X PUT "localhost:9200/products" -H 'Content-Type: application/json' -d'
{
  "settings": {
    "number_of_shards": 3,
    "number_of_replicas": 1
  }
}'
```

### 索引设置

| 设置 | 默认值 | 说明 |
|------|--------|------|
| `number_of_shards` | 1 | 主分片数量 |
| `number_of_replicas` | 1 | 副本分片数量 |
| `refresh_interval` | 1s | 新数据可搜索的刷新间隔 |
| `max_result_window` | 10000 | 最大 from + size 值 |

## 映射（Mapping）

映射定义了文档及其字段的存储和索引方式。

| 字段类型 | 用途 | 示例 |
|---------|------|------|
| `text` | 全文可搜索字符串 | 产品描述 |
| `keyword` | 精确匹配字符串 | 分类名称 |
| `integer` | 整数 | 数量 |
| `float` | 小数 | 价格 |
| `date` | 日期/时间值 | 创建时间戳 |
| `boolean` | 布尔值 | 有货标志 |
| `nested` | 对象数组 | 产品变体 |
| `geo_point` | 经纬度对 | 商店位置 |

### 定义映射

```bash
curl -X PUT "localhost:9200/products/_mapping" -H 'Content-Type: application/json' -d'
{
  "properties": {
    "name": { "type": "text", "analyzer": "standard" },
    "category": { "type": "keyword" },
    "price": { "type": "float" },
    "description": { "type": "text" },
    "created_at": { "type": "date" },
    "in_stock": { "type": "boolean" }
  }
}'
```

## 文档操作

### 索引文档

```bash
curl -X POST "localhost:9200/products/_doc" -H 'Content-Type: application/json' -d'
{
  "name": "Wireless Keyboard",
  "category": "Electronics",
  "price": 49.99,
  "description": "Ergonomic wireless keyboard with backlight",
  "created_at": "2024-01-15",
  "in_stock": true
}'
```

### CRUD 操作汇总

| 操作 | HTTP 方法 | 端点 | 说明 |
|------|----------|------|------|
| 创建 | POST | `/{index}/_doc` | 索引新文档 |
| 读取 | GET | `/{index}/_doc/{id}` | 获取文档 |
| 更新 | POST | `/{index}/_update/{id}` | 部分更新 |
| 删除 | DELETE | `/{index}/_doc/{id}` | 删除文档 |

## 查询 DSL

### 匹配查询

```bash
curl -X GET "localhost:9200/products/_search" -H 'Content-Type: application/json' -d'
{
  "query": {
    "match": {
      "description": "wireless keyboard"
    }
  }
}'
```

### 查询类型参考

| 查询 | 用途 | 最佳场景 |
|------|------|---------|
| `match` | 全文搜索 | 搜索文本字段 |
| `term` | 精确匹配 | 关键词过滤 |
| `range` | 数值/日期范围 | 价格或日期筛选 |
| `bool` | 组合条件 | 复杂查询 |
| `multi_match` | 跨字段搜索 | 广泛文本搜索 |
| `fuzzy` | 容错搜索 | 用户输入查询 |

### Bool 查询结构

```bash
curl -X GET "localhost:9200/products/_search" -H 'Content-Type: application/json' -d'
{
  "query": {
    "bool": {
      "must": [
        { "match": { "description": "wireless" } }
      ],
      "filter": [
        { "term": { "category": "Electronics" } },
        { "range": { "price": { "gte": 20, "lte": 100 } } }
      ]
    }
  }
}'
```

| 子句 | 行为 | 影响相关性评分 |
|------|------|---------------|
| `must` | 文档必须匹配 | 是 |
| `should` | 文档应该匹配 | 是 |
| `must_not` | 文档必须不匹配 | 否 |
| `filter` | 文档必须匹配（无评分） | 否 |

## 聚合（Aggregations）

聚合提供对搜索结果的分析和汇总。

### 桶聚合

```bash
curl -X GET "localhost:9200/products/_search" -H 'Content-Type: application/json' -d'
{
  "size": 0,
  "aggs": {
    "by_category": {
      "terms": { "field": "category" }
    }
  }
}'
```

### 聚合类型

| 聚合 | 类别 | 用途 |
|------|------|------|
| `terms` | 桶 | 按字段值分组 |
| `histogram` | 桶 | 数值间隔 |
| `date_histogram` | 桶 | 基于时间的间隔 |
| `avg` | 指标 | 计算平均值 |
| `sum` | 指标 | 计算总和 |
| `min` / `max` | 指标 | 查找极值 |
| `percentiles` | 指标 | 分布分析 |
| `cardinality` | 指标 | 统计唯一值数量 |

## 分页方法

| 方法 | 参数 | 最佳场景 |
|------|------|---------|
| From/Size | `from`, `size` | 浅层分页 |
| Search After | `sort`, `search_after` | 深层分页 |
| Scroll | `scroll` 参数 | 批量数据导出 |
| Point in Time | `pit`, `search_after` | 一致性深层分页 |

## 分析器（Analyzers）

分析器在索引和搜索期间处理文本，以实现全文搜索。

| 分析器 | 小写化 | 词干提取 | 停用词 | 用途 |
|--------|--------|---------|--------|------|
| standard | 是 | 否 | 否 | 通用 |
| simple | 是 | 否 | 否 | 基本分词 |
| whitespace | 否 | 否 | 否 | 保留大小写 |
| english | 是 | 是 | 是 | 英文文本 |
| keyword | 否 | 否 | 否 | 精确匹配 |

## 节点类型

| 节点类型 | 角色 | 使用场景 |
|---------|------|---------|
| Master（主节点） | 管理集群状态 | 大型集群中需专用 |
| Data（数据节点） | 存储和查询数据 | 始终需要 |
| Ingest（预处理节点） | 预处理文档 | 大量写入工作负载 |
| Coordinating（协调节点） | 路由和聚合 | 高查询量场景 |
| Machine Learning（机器学习节点） | 运行 ML 任务 | 异常检测 |

## 性能最佳实践

| 方面 | 建议 |
|------|------|
| 分片大小 | 每个分片 10-50 GB |
| 映射 | 仅用于过滤的字段使用 `keyword` |
| 查询 | 使用 `filter` 上下文跳过评分 |
| 批量写入 | 使用 bulk API 写入多个文档 |
| 刷新间隔 | 批量加载时增大间隔 |
| 缓存 | 依赖过滤缓存处理重复查询 |

## 监控命令

```bash
# 集群健康状态
curl -X GET "localhost:9200/_cluster/health"

# 节点统计
curl -X GET "localhost:9200/_nodes/stats"

# 索引统计
curl -X GET "localhost:9200/products/_stats"

# 待处理任务
curl -X GET "localhost:9200/_cluster/pending_tasks"

# 索引恢复状态
curl -X GET "localhost:9200/_cat/recovery?v"
```

## 总结

Elasticsearch 是一个强大的搜索引擎，适用于全文搜索、日志分析和实时数据探索。理解其查询 DSL、映射系统和集群架构对于构建大规模高性能搜索应用至关重要。
