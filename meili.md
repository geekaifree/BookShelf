# 使用 Meilisearch 搭建搜索引擎

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
