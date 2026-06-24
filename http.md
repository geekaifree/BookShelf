# 使用 HTTPie 作为 HTTP 客户端

## 简介

HTTPie 是一个命令行 HTTP 客户端，专为与 Web 服务和 API 交互而设计。它提供了富有表现力的语法、格式化输出和内置的现代 API 开发功能。本教程涵盖安装、使用模式和高级功能。

## 安装

### 包管理器

| 平台 | 命令 |
|------|------|
| macOS (Homebrew) | `brew install httpie` |
| Ubuntu/Debian | `apt install httpie` |
| Fedora | `dnf install httpie` |
| Windows (Scoop) | `scoop install httpie` |
| pip | `pip install httpie` |
| Snap | `snap install http` |

### 验证安装

```bash
http --version
http --help
```

## 基本语法

### 命令结构

```
http [flags] [METHOD] URL [ITEM [ITEM...]]
```

### 组件

| 组件 | 描述 | 示例 |
|------|------|------|
| METHOD | HTTP 方法（默认：GET） | GET, POST, PUT, DELETE |
| URL | 目标端点 | api.example.com/users |
| ITEM | 请求数据 | headers, params, body |
| FLAGS | 行为修饰符 | --verbose, --headers |

### 简单 GET 请求

```bash
http GET https://api.example.com/users
```

或直接：

```bash
http https://api.example.com/users
```

## 请求方法

### 方法快捷方式

| 快捷方式 | 方法 | 示例 |
|----------|------|------|
| `http URL` | GET | `http api.example.com/users` |
| `http POST URL` | POST | `http POST api.example.com/users` |
| `http PUT URL` | PUT | `http PUT api.example.com/users/1` |
| `http PATCH URL` | PATCH | `http PATCH api.example.com/users/1` |
| `http DELETE URL` | DELETE | `http DELETE api.example.com/users/1` |
| `http HEAD URL` | HEAD | `http HEAD api.example.com/users` |
| `http OPTIONS URL` | OPTIONS | `http OPTIONS api.example.com/users` |

## 发送数据

### 请求项类型

| 语法 | 类型 | 示例 |
|------|------|------|
| `key=value` | JSON 字符串字段 | `name=John` |
| `key:=value` | JSON 非字符串 | `age:=30` |
| `key@value` | 文件上传 | `avatar@photo.jpg` |
| `key:value` | HTTP 头 | `Authorization:Bearer token` |
| `key==value` | URL 参数 | `page==1` |

### JSON 数据

```bash
# 字符串值（自动加引号）
http POST api.example.com/users name="John Doe" email="john@example.com"

# 非字符串值（使用 :=）
http POST api.example.com/users name="John" age:=30 active:=true

# 嵌套 JSON
http POST api.example.com/users name="John" address[city]="New York" address[zip]="10001"

# 数组值
http POST api.example.com/users names[]="John" names[]="Jane"
```

### 原始 JSON 请求体

```bash
# 从 stdin 管道传入 JSON
echo '{"name": "John", "age": 30}' | http POST api.example.com/users

# 使用 --raw 标志
http --raw='{"name": "John", "age": 30}' POST api.example.com/users
```

### 表单数据

```bash
# URL 编码表单
http --form POST api.example.com/login username=admin password=secret

# 带文件的多部分表单
http --form POST api.example.com/upload file@document.pdf description="My file"
```

## 请求头

### 设置请求头

```bash
# 自定义头部
http api.example.com X-Custom-Header:value

# Authorization 头
http api.example.com Authorization:"Bearer eyJhbGci..."

# Content-Type 覆盖
http POST api.example.com/data Content-Type:text/xml '<data>hello</data>'
```

### 默认请求头

| 头部 | 默认值 | 覆盖方式 |
|------|--------|----------|
| User-Agent | HTTPie/version | `User-Agent:CustomAgent` |
| Accept | application/json | `Accept:text/html` |
| Content-Type | 自动检测 | `Content-Type:text/xml` |
| Host | 来自 URL | `Host:custom.host` |

### 移除请求头

```bash
# 移除头部
http api.example.com Header-Name:
```

## 认证

### 内置认证方式

| 方式 | 标志 | 示例 |
|------|------|------|
| Basic | `-a user:pass` | `http -a admin:secret api.example.com` |
| Bearer | `Authorization:Bearer TOKEN` | `http api.example.com Authorization:"Bearer abc123"` |
| Digest | `--auth-type=digest -a user:pass` | `http --auth-type=digest -a admin:secret api.example.com` |

### 认证插件示例

```bash
# 安装认证插件
pip install httpie-jwt-auth
pip install httpie-api-key

# JWT 认证
http --auth-type=jwt --auth=TOKEN api.example.com

# 头部中的 API key
http api.example.com X-API-Key:your-key
```

## 输出控制

### 输出标志

| 标志 | 描述 | 示例 |
|------|------|------|
| `-v` | 详细（头部 + 请求体） | `http -v api.example.com` |
| `-h` | 仅头部 | `http -h api.example.com` |
| `-b` | 仅请求体 | `http -b api.example.com` |
| `-p H` | 打印特定部分 | `http -p Hh api.example.com` |
| `-S` | 流式输出 | `http -S api.example.com` |
| `-o FILE` | 保存到文件 | `http -o output.json api.example.com` |

### 打印部分标志

| 标志 | 含义 |
|------|------|
| `H` | 请求头 |
| `B` | 请求体 |
| `h` | 响应头 |
| `b` | 响应体 |

```bash
# 打印请求和响应头部
http -p Hh api.example.com

# 仅打印响应体
http -p b api.example.com
```

## 会话

会话在请求间持久化 Cookie、头部和认证信息：

```bash
# 创建/使用命名会话
http --session=mysession api.example.com/login username=admin password=secret

# 后续请求使用存储的 Cookie
http --session=mysession api.example.com/dashboard

# 自定义文件路径的会话
http --session=/path/to/session.json api.example.com
```

### 会话文件内容

| 数据 | 持久化 | 目的 |
|------|--------|------|
| Cookies | 是 | 认证状态 |
| Auth 头部 | 是 | 复用凭据 |
| 自定义头部 | 是 | 一致的请求头 |
| 代理设置 | 是 | 网络配置 |

## 下载文件

```bash
# 使用原始文件名下载
http --download https://example.com/file.pdf

# 使用自定义名称下载
http --download --output=report.pdf https://example.com/file.pdf

# 带进度条下载
http --download --progress https://example.com/large-file.zip
```

## 代理配置

```bash
# HTTP 代理
http --proxy=http:http://proxy:8080 api.example.com

# SOCKS 代理
http --proxy=http:socks5://proxy:1080 api.example.com

# 带认证的代理
http --proxy=http:http://user:pass@proxy:8080 api.example.com
```

## SSL/TLS 选项

| 标志 | 描述 | 使用场景 |
|------|------|----------|
| `--verify=no` | 跳过证书验证 | 自签名证书（测试） |
| `--verify=yes` | 强制验证 | 生产环境 |
| `--ssl=TLSv1.2` | 强制 TLS 版本 | 兼容性测试 |
| `--cert=CERT` | 客户端证书 | 双向 TLS |
| `--cert-key=KEY` | 客户端证书密钥 | 双向 TLS |

```bash
# 跳过验证（仅测试）
http --verify=no https://self-signed.example.com

# 客户端证书
http --cert=client.pem --cert-key=key.pem https://mtls.example.com
```

## 查询字符串参数

```bash
# URL 参数
http api.example.com/users page==1 limit==10 sort==name

# 编码参数
http api.example.com/search q=="hello world"

# 与请求体数据结合
http POST api.example.com/users?page==1 name="John" age:=30
```

## 重定向

| 标志 | 描述 | 默认值 |
|------|------|--------|
| `--follow` | 跟随重定向 | GET 请求默认是 |
| `--max-redirects=N` | 限制重定向次数 | 30 |
| `--all` | 显示中间重定向 | 关闭 |

```bash
# 显式跟随重定向
http --follow api.example.com/old-path

# 显示所有重定向步骤
http --follow --all api.example.com/old-path
```

## 配置文件

创建 `~/.config/httpie/config.json`：

```json
{
  "default_options": [
    "--session=default",
    "--print=HhBb",
    "--style=monokai"
  ]
}
```

### 配置选项

| 设置 | 描述 | 示例 |
|------|------|------|
| default_options | 始终应用的标志 | `["--verbose"]` |
| output_options | 默认输出设置 | `["--format=json"]` |
| style | 语法高亮 | monokai, fruity, monochrome |

## 实际示例

### REST API 工作流

```bash
# 列出资源
http GET api.example.com/users

# 创建资源
http POST api.example.com/users name="John" email="john@example.com"

# 更新资源
http PUT api.example.com/users/1 name="John Smith"

# 部分更新
http PATCH api.example.com/users/1 email="newemail@example.com"

# 删除资源
http DELETE api.example.com/users/1
```

### 分页

```bash
# 分页浏览结果
http api.example.com/users page==1 per_page==10
http api.example.com/users page==2 per_page==10
```

### 条件请求

```bash
# If-None-Match (ETag)
http api.example.com/users/1 If-None-Match:'"abc123"'

# If-Modified-Since
http api.example.com/users/1 If-Modified-Since:"Wed, 01 Jan 2026 00:00:00 GMT"
```

## 与 cURL 对比

| 功能 | HTTPie | cURL |
|------|--------|------|
| 语法 | 直观 | 冗长 |
| JSON 支持 | 自动 | 手动 |
| 输出格式化 | 彩色 | 原始 |
| 会话 | 内置 | Cookie 文件 |
| 认证 | 简化 | 标志 |
| 表单数据 | `--form` 标志 | `-F` 标志 |
| 学习曲线 | 低 | 中等 |

### 等效命令

| 任务 | HTTPie | cURL |
|------|--------|------|
| GET 请求 | `http api.example.com/users` | `curl https://api.example.com/users` |
| POST JSON | `http POST url name=John` | `curl -X POST -H 'Content-Type: application/json' -d '{"name":"John"}' url` |
| 认证 | `http -a user:pass url` | `curl -u user:pass url` |
| 头部 | `http url X-Header:val` | `curl -H 'X-Header:val' url` |

## 总结

HTTPie 提供了一个富有表现力、人性化的 HTTP 通信界面。其自动 JSON 处理、格式化输出和会话管理使其成为 API 开发和测试的高效工具。

关键实践：

- 使用会话在请求间维护认证状态
- 利用 `:=` 语法处理非字符串 JSON 值
- 在配置文件中配置默认选项
- 使用 `--download` 进行带进度跟踪的文件下载
- 结合 Shell 脚本实现自动化 API 工作流
