# 搜索引擎

> 本文档整合了以下源文件：search.md, meili.md

---

## 来源：search.md

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


---

## 来源：meili.md

## 简介

Meilisearch 是一个开源、闪电般快速的搜索引擎。它提供即时搜索结果，具有容错功能，并支持多种语言。

### 什么是 Meilisearch？

Meilisearch 是一个面向用户应用的搜索引擎。它提供即时搜索结果，具有容错、过滤和排序等功能。

| 特性 | 描述 |
|------|------|
| 即时搜索 | 毫秒级结果 |
| 容错 | 处理拼写错误 |
| 过滤 | 高级过滤选项 |
| 排序 | 自定义排序规则 |
| 多语言 | 支持多种语言 |

### 与其他方案的比较

| 特性 | Meilisearch | Elasticsearch | Algolia |
|------|------------|---------------|---------|
| 速度 | 非常快 | 快 | 快 |
| 易用性 | 高 | 低 | 高 |
| 自托管 | 是 | 是 | 否 |
| 容错 | 内置 | 手动 | 内置 |
| 费用 | 免费 | 免费 | 付费 |

## 安装

### 系统要求

| 要求 | 最低 | 推荐 |
|------|------|------|
| CPU | 1 核 | 2+ 核 |
| 内存 | 256 MB | 1+ GB |
| 存储 | 100 MB | 1+ GB |

### Docker 安装

```bash
docker run -d \
  --name meilisearch \
  -p 7700:7700 \
  -v meilisearch_data:/meili_data \
  getmeili/meilisearch:latest
```

### Docker Compose

```yaml
version: '3'
services:
  meilisearch:
    image: getmeili/meilisearch:latest
    ports:
      - "7700:7700"
    volumes:
      - meilisearch_data:/meili_data
    environment:
      - MEILI_MASTER_KEY=your-master-key
    restart: unless-stopped

volumes:
  meilisearch_data:
```

### 手动安装

```bash
# Linux
curl -L https://install.meilisearch.com | sh

# macOS
brew install meilisearch

# 启动服务器
./meilisearch --master-key=your-master-key
```

### 环境变量

```env
MEILI_MASTER_KEY=your-master-key
MEILI_ENV=production
MEILI_NO_ANALYTICS=true
```

## 索引管理

### 创建索引

```bash
curl -X POST 'http://localhost:7700/indexes' \
  -H 'Content-Type: application/json' \
  -H 'Authorization: Bearer your-master-key' \
  -d '{"uid": "movies", "primaryKey": "id"}'
```

### 索引属性

| 属性 | 描述 |
|------|------|
| uid | 唯一标识符 |
| primaryKey | 文档标识字段 |
| createdAt | 创建时间戳 |
| updatedAt | 最后更新时间戳 |

### 列出索引

```bash
curl -H 'Authorization: Bearer your-master-key' \
  'http://localhost:7700/indexes'
```

## 文档管理

### 添加文档

```bash
curl -X POST 'http://localhost:7700/indexes/movies/documents' \
  -H 'Content-Type: application/json' \
  -H 'Authorization: Bearer your-master-key' \
  -d '[
    {
      "id": 1,
      "title": "Solaris",
      "genre": "science fiction",
      "rating": 8.1
    },
    {
      "id": 2,
      "title": "Interstellar",
      "genre": "science fiction",
      "rating": 8.6
    }
  ]'
```

### 文档结构

| 字段类型 | 描述 |
|----------|------|
| String | 用于搜索的文本字段 |
| Number | 用于过滤/排序的数值字段 |
| Boolean | 真/假值 |
| Array | 值列表 |
| Object | 嵌套对象 |

### 更新文档

```bash
# 更新特定文档
curl -X PUT 'http://localhost:7700/indexes/movies/documents' \
  -H 'Content-Type: application/json' \
  -H 'Authorization: Bearer your-master-key' \
  -d '[{"id": 1, "rating": 8.5}]'

# 删除文档
curl -X POST 'http://localhost:7700/indexes/movies/documents/delete-batch' \
  -H 'Content-Type: application/json' \
  -H 'Authorization: Bearer your-master-key' \
  -d '[1, 2]'
```

## 搜索

### 基本搜索

```bash
curl -X POST 'http://localhost:7700/indexes/movies/search' \
  -H 'Content-Type: application/json' \
  -H 'Authorization: Bearer your-master-key' \
  -d '{"q": "solaris"}'
```

### 搜索参数

| 参数 | 描述 |
|------|------|
| q | 搜索查询 |
| offset | 跳过的结果数 |
| limit | 最大结果数 |
| attributesToRetrieve | 返回的字段 |
| attributesToHighlight | 高亮的字段 |
| filter | 过滤表达式 |
| sort | 排序规则 |

### 搜索响应

```json
{
  "hits": [
    {
      "id": 1,
      "title": "Solaris",
      "genre": "science fiction",
      "rating": 8.1
    }
  ],
  "nbHits": 1,
  "page": 0,
  "nbPages": 1,
  "hitsPerPage": 20,
  "processingTimeMs": 1
}
```

## 过滤

### 过滤语法

```bash
# 简单过滤
curl -X POST 'http://localhost:7700/indexes/movies/search' \
  -H 'Content-Type: application/json' \
  -d '{"q": "space", "filter": "genre = \"science fiction\""}'

# 多重过滤
curl -X POST 'http://localhost:7700/indexes/movies/search' \
  -H 'Content-Type: application/json' \
  -d '{"q": "space", "filter": "genre = \"science fiction\" AND rating > 8"}'
```

### 过滤运算符

| 运算符 | 描述 | 示例 |
|--------|------|------|
| `=` | 等于 | `genre = "sci-fi"` |
| `!=` | 不等于 | `genre != "horror"` |
| `>` | 大于 | `rating > 7` |
| `<` | 小于 | `rating < 5` |
| `>=` | 大于等于 | `rating >= 8` |
| `<=` | 小于等于 | `rating <= 3` |
| `TO` | 范围 | `rating 7 TO 9` |
| `EXISTS` | 有值 | `genre EXISTS` |
| `IN` | 在列表中 | `genre IN ["sci-fi", "action"]` |

### 配置可过滤属性

```bash
curl -X PUT 'http://localhost:7700/indexes/movies/settings' \
  -H 'Content-Type: application/json' \
  -H 'Authorization: Bearer your-master-key' \
  -d '{"filterableAttributes": ["genre", "rating"]}'
```

## 排序

### 排序语法

```bash
curl -X POST 'http://localhost:7700/indexes/movies/search' \
  -H 'Content-Type: application/json' \
  -d '{"q": "space", "sort": ["rating:desc"]}'
```

### 配置可排序属性

```bash
curl -X PUT 'http://localhost:7700/indexes/movies/settings' \
  -H 'Content-Type: application/json' \
  -H 'Authorization: Bearer your-master-key' \
  -d '{"sortableAttributes": ["rating", "release_date"]}'
```

## 容错

### 配置

```bash
curl -X PATCH 'http://localhost:7700/indexes/movies/settings' \
  -H 'Content-Type: application/json' \
  -H 'Authorization: Bearer your-master-key' \
  -d '{
    "typoTolerance": {
      "enabled": true,
      "minWordSizeForTypos": {
        "oneTypo": 5,
        "twoTypos": 9
      }
    }
  }'
```

### 容错设置

| 设置 | 描述 |
|------|------|
| enabled | 启用/禁用 |
| minWordSizeForTypos | 容错的最小单词长度 |
| disableOnWords | 禁用容错的单词 |
| disableOnAttributes | 禁用容错的属性 |

## 可搜索属性

### 配置

```bash
curl -X PUT 'http://localhost:7700/indexes/movies/settings' \
  -H 'Content-Type: application/json' \
  -H 'Authorization: Bearer your-master-key' \
  -d '{"searchableAttributes": ["title", "description", "genre"]}'
```

### 属性优先级

| 顺序 | 优先级 |
|------|--------|
| 最前 | 最高优先级 |
| 最后 | 最低优先级 |

## 显示属性

### 配置

```bash
curl -X PUT 'http://localhost:7700/indexes/movies/settings' \
  -H 'Content-Type: application/json' \
  -H 'Authorization: Bearer your-master-key' \
  -d '{"displayedAttributes": ["title", "genre", "rating"]}'
```

## 分页

### 分页参数

| 参数 | 描述 | 默认 |
|------|------|------|
| offset | 跳过的结果 | 0 |
| limit | 最大结果 | 20 |
| page | 页码 | 0 |
| hitsPerPage | 每页结果 | 20 |

### 示例

```bash
curl -X POST 'http://localhost:7700/indexes/movies/search' \
  -H 'Content-Type: application/json' \
  -d '{"q": "space", "page": 2, "hitsPerPage": 10}'
```

## 多索引搜索

### 搜索多个索引

```bash
curl -X POST 'http://localhost:7700/multi-search' \
  -H 'Content-Type: application/json' \
  -H 'Authorization: Bearer your-master-key' \
  -d '{
    "queries": [
      {"indexUid": "movies", "q": "space"},
      {"indexUid": "books", "q": "space"}
    ]
  }'
```

## API 密钥

### 密钥类型

| 类型 | 描述 |
|------|------|
| Master key | 完全访问 |
| Search key | 仅搜索 |
| Custom keys | 有限访问 |

### 创建密钥

```bash
curl -X POST 'http://localhost:7700/keys' \
  -H 'Content-Type: application/json' \
  -H 'Authorization: Bearer your-master-key' \
  -d '{
    "description": "Search key",
    "actions": ["search"],
    "indexes": ["movies"],
    "expiresAt": "2025-01-01T00:00:00Z"
  }'
```

## Web 界面

### 内置仪表盘

访问 `http://localhost:7700` 的 Web 界面：

| 功能 | 描述 |
|------|------|
| 索引管理 | 创建、删除索引 |
| 文档浏览器 | 查看、编辑文档 |
| 搜索测试 | 测试搜索 |
| 设置 | 配置索引 |

## SDK

### 官方 SDK

| 语言 | 包 |
|------|------|
| JavaScript | meilisearch |
| Python | meilisearch-python |
| PHP | meilisearch-php |
| Ruby | meilisearch-ruby |
| Go | meilisearch-go |
| Rust | meilisearch-rust |
| Swift | meilisearch-swift |

### JavaScript 示例

```javascript
import { MeiliSearch } from 'meilisearch'

const client = new MeiliSearch({
  host: 'http://localhost:7700',
  apiKey: 'your-search-key'
})

// 搜索
const results = await client.index('movies').search('space')

// 添加文档
await client.index('movies').addDocuments([
  { id: 1, title: 'Solaris', genre: 'sci-fi' }
])
```

### Python 示例

```python
from meilisearch import Client

client = Client('http://localhost:7700', 'your-search-key')

# 搜索
results = client.index('movies').search('space')

# 添加文档
client.index('movies').add_documents([
    {'id': 1, 'title': 'Solaris', 'genre': 'sci-fi'}
])
```

## 性能调优

### 优化技巧

| 技巧 | 描述 |
|------|------|
| 限制可搜索字段 | 仅索引可搜索文本 |
| 合理使用过滤 | 在索引字段上过滤 |
| 批量更新 | 批量添加文档 |
| 设置最大值 | 限制分页 |

### 性能指标

| 指标 | 描述 |
|------|------|
| processingTimeMs | 搜索时间 |
| nbHits | 总结果数 |
| queryTime | 索引查询时间 |

## 备份和恢复

### 创建备份

```bash
# 创建 dump
curl -X POST 'http://localhost:7700/dumps' \
  -H 'Authorization: Bearer your-master-key'

# 检查 dump 状态
curl -H 'Authorization: Bearer your-master-key' \
  'http://localhost:7700/dumps/dump-uid/status'
```

### 导入 Dump

```bash
./meilisearch --import-dump dump-file.dump
```

## 总结

| 功能 | 用途 |
|------|------|
| 索引 | 组织文档 |
| 搜索 | 全文搜索 |
| 过滤 | 缩小结果范围 |
| 排序 | 排列结果 |
| 容错 | 处理拼写错误 |
| API 密钥 | 访问控制 |


---
