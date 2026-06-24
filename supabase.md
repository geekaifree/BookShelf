# Supabase：后端即服务教程

## 简介

Supabase 是一个基于 PostgreSQL 构建的开源 Firebase 替代方案。它提供数据库、认证、实时订阅、存储和边缘函数。本教程涵盖各个功能以及如何使用 Supabase 构建应用。

## Supabase 与 Firebase 对比

| 功能 | Supabase | Firebase |
|------|----------|----------|
| 数据库 | PostgreSQL（关系型） | Firestore（文档型） |
| 认证 | GoTrue（OAuth、MFA、SSO） | Firebase Auth |
| 实时 | PostgreSQL 逻辑复制 | Cloud Firestore 流 |
| 存储 | S3 兼容 | Cloud Storage |
| 函数 | Edge Functions（Deno） | Cloud Functions（Node.js） |
| 开源 | 是 | 否 |
| 定价 | 免费层 + 按量计费 | 免费层 + 按量计费 |

## 快速开始

### 创建项目

1. 在 supabase.com 注册。
2. 创建新项目。
3. 记下项目 URL 和 anon key。

### 安装客户端库

| 语言 | 命令 |
|------|------|
| JavaScript | npm install @supabase/supabase-js |
| Python | pip install supabase |
| Dart | pub add supabase_flutter |
| Swift | 通过 Swift Package Manager 添加 |
| Kotlin | 通过 Gradle 添加 |

### 初始化客户端

```javascript
import { createClient } from '@supabase/supabase-js'

const supabase = createClient(
  'https://your-project.supabase.co',
  'your-anon-key'
)
```

## 数据库功能

### 表管理

| 操作 | SQL | 控制面板 |
|------|-----|---------|
| 创建表 | CREATE TABLE ... | Table Editor |
| 添加列 | ALTER TABLE ... ADD COLUMN ... | 列编辑器 |
| 设置关系 | 外键约束 | 可视化关系构建器 |
| 创建索引 | CREATE INDEX ... | 索引编辑器 |

### 行级安全（RLS）

| 策略类型 | 用途 |
|----------|------|
| SELECT | 控制谁可以读取行 |
| INSERT | 控制谁可以创建行 |
| UPDATE | 控制谁可以修改行 |
| DELETE | 控制谁可以删除行 |

在表上启用 RLS：

```sql
ALTER TABLE posts ENABLE ROW LEVEL SECURITY;

CREATE POLICY "Users can read own posts"
ON posts FOR SELECT
USING (auth.uid() = user_id);
```

### 数据库函数

| 函数类型 | 用例 |
|----------|------|
| 存储过程 | 复杂业务逻辑 |
| 触发器函数 | 自动更新时间戳 |
| 计算列 | 派生值 |
| RPC | 可从客户端 SDK 调用 |

## 认证

### 支持的方式

| 方式 | 设置 |
|------|------|
| 邮箱/密码 | 内置，无需配置 |
| Magic Link | 基于邮箱的无密码登录 |
| OAuth（Google、GitHub 等） | 配置提供商凭据 |
| 手机/短信 OTP | Twilio 集成 |
| SAML SSO | 企业身份提供商 |
| 匿名 | 无需注册的访客访问 |

### 认证操作

| 操作 | 客户端方法 |
|------|-----------|
| 注册 | supabase.auth.signUp({ email, password }) |
| 登录 | supabase.auth.signInWithPassword({ email, password }) |
| 登出 | supabase.auth.signOut() |
| 获取用户 | supabase.auth.getUser() |
| 获取会话 | supabase.auth.getSession() |
| 重置密码 | supabase.auth.resetPasswordForEmail(email) |

### 会话管理

| 功能 | 描述 |
|------|------|
| JWT 令牌 | 短期访问令牌 |
| 刷新令牌 | 用于续期的长期令牌 |
| 自动刷新 | 客户端 SDK 处理令牌续期 |
| 持久化 | LocalStorage 或自定义适配器 |

## 实时订阅

### 订阅变更

| 事件 | 描述 |
|------|------|
| INSERT | 新行添加 |
| UPDATE | 现有行修改 |
| DELETE | 行删除 |
| * | 所有变更 |

### 示例

```javascript
const channel = supabase
  .channel('posts-changes')
  .on('postgres_changes',
    { event: 'INSERT', schema: 'public', table: 'posts' },
    (payload) => console.log('New post:', payload.new)
  )
  .subscribe()
```

### 在线状态（Presence）

实时跟踪在线用户：

```javascript
const channel = supabase.channel('online-users')
channel.on('presence', { event: 'sync' }, () => {
  const state = channel.presenceState()
  console.log('Online:', state)
})
channel.subscribe(async (status) => {
  if (status === 'SUBSCRIBED') {
    await channel.track({ user_id: user.id, online_at: new Date() })
  }
})
```

## 存储

### 存储桶类型

| 类型 | 访问权限 | 用例 |
|------|---------|------|
| Public（公开） | 任何人可读 | 公开资源、头像 |
| Private（私有） | 认证 + RLS | 用户文档、私有媒体 |

### 操作

| 操作 | 方法 |
|------|------|
| 上传 | supabase.storage.from('bucket').upload(path, file) |
| 下载 | supabase.storage.from('bucket').download(path) |
| 获取 URL | supabase.storage.from('bucket').getPublicUrl(path) |
| 签名 URL | supabase.storage.from('bucket').createSignedUrl(path, expiresIn) |
| 列表 | supabase.storage.from('bucket').list(folder) |
| 删除 | supabase.storage.from('bucket').remove([path]) |

### 图片转换

| 参数 | 效果 |
|------|------|
| width | 调整为指定宽度 |
| height | 调整为指定高度 |
| resize | cover、contain 或 fill |
| quality | 压缩质量（1-100） |
| format | origin、webp、avif |

## Edge Functions

Edge Functions 在 Deno 运行时上运行服务端逻辑。

### 常见 Edge Function 用例

| 用例 | 描述 |
|------|------|
| Webhooks | 处理 Stripe、GitHub 事件 |
| 定时任务 | 类似 Cron 的后台任务 |
| API 代理 | 安全地调用第三方 API |
| 图片处理 | 调整大小或转换上传内容 |
| 邮件发送 | 通过 Resend/SendGrid 发送事务邮件 |

## 客户端 SDK 查询

### 查询数据

| 查询 | 示例 |
|------|------|
| 所有行 | .from('posts').select('*') |
| 特定列 | .from('posts').select('title, body') |
| 包含关联 | .from('posts').select('*, author(name)') |
| 过滤 | .from('posts').select('*').eq('status', 'published') |
| 分页 | .from('posts').select('*').range(0, 9) |

### 过滤运算符

| 运算符 | 方法 | 示例 |
|--------|------|------|
| 等于 | .eq() | .eq('status', 'draft') |
| 不等于 | .neq() | .neq('status', 'archived') |
| 大于 | .gt() | .gt('views', 100) |
| 小于 | .lt() | .lt('price', 50) |
| Like | .like() | .like('title', '%supabase%') |
| 在数组中 | .in() | .in('category', ['tech', 'news']) |
| 为空 | .is() | .is('deleted_at', null) |

## 迁移

| 命令 | 用途 |
|------|------|
| supabase migration new <name> | 创建迁移文件 |
| supabase db push | 将本地迁移应用到远程 |
| supabase db pull | 将远程 schema 拉取到本地 |
| supabase db reset | 重置本地数据库 |
| supabase db diff | 比较本地和远程 schema |

## 定价

| 计划 | 数据库 | 存储 | 带宽 | 价格 |
|------|--------|------|------|------|
| Free | 500 MB | 1 GB | 2 GB | $0 |
| Pro | 8 GB | 100 GB | 250 GB | $25/月 |
| Team | 8 GB | 100 GB | 250 GB | $599/月 |
| Enterprise | 自定义 | 自定义 | 自定义 | 联系销售 |

## 总结

Supabase 提供了一个以 PostgreSQL 为核心的完整后端平台。数据库、认证、实时、存储和边缘函数的组合，让开发者无需管理基础设施即可构建全栈应用。其开源特性和 PostgreSQL 基础给予开发者对数据的完全控制和可移植性。
