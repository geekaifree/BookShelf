# Homebrew：macOS 和 Linux 的包管理器

## 简介

Homebrew 是 macOS 和 Linux 上最流行的包管理器。它简化了从命令行安装软件的过程，并自动管理依赖关系。

| 属性 | 详情 |
|----------|--------|
| 仓库 | Homebrew/brew |
| 许可证 | BSD-2-Clause |
| 语言 | Ruby, Shell |
| 平台 | macOS, Linux |
| 默认前缀 | /usr/local (macOS Intel), /opt/homebrew (macOS ARM), /home/linuxbrew |

## 安装

### macOS

```bash
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
```

### Linux

```bash
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
```

### 验证安装

```bash
brew --version
brew doctor
```

## 核心概念

| 术语 | 描述 |
|------|-------------|
| Formula（配方） | 包定义（构建软件的配方） |
| Cask（桶） | 二进制包（预构建的应用程序） |
| Tap（水龙头） | 第三方配方仓库 |
| Cellar（酒窖） | 已安装包所在的目录 |
| Keg（桶） | 单个已安装包的目录 |
| Bottle（瓶子） | 预编译的二进制包 |

## 基本命令

### 安装包

| 命令 | 描述 |
|---------|-------------|
| brew install FORMULA | 安装配方 |
| brew install --cask CASK | 安装桶（GUI 应用程序） |
| brew install FORMULA@VERSION | 安装特定版本 |

```bash
# 安装配方
brew install git

# 安装桶
brew install --cask firefox

# 安装特定版本
brew install node@18
```

### 管理包

| 命令 | 描述 |
|---------|-------------|
| brew list | 列出已安装的包 |
| brew list --formula | 列出已安装的配方 |
| brew list --cask | 列出已安装的桶 |
| brew info FORMULA | 显示包信息 |
| brew upgrade FORMULA | 升级特定包 |
| brew upgrade | 升级所有包 |
| brew uninstall FORMULA | 移除包 |
| brew autoremove | 移除未使用的依赖 |

### 搜索和信息

| 命令 | 描述 |
|---------|-------------|
| brew search QUERY | 搜索包 |
| brew info FORMULA | 显示详细包信息 |
| brew deps FORMULA | 列出依赖 |
| brew uses --installed FORMULA | 哪些包使用此包 |

```bash
# 搜索包
brew search python

# 显示包信息
brew info node

# 列出包的依赖
brew deps git
```

## 更新 Homebrew

| 命令 | 描述 |
|---------|-------------|
| brew update | 更新 Homebrew 本身和配方定义 |
| brew outdated | 列出有可用更新的包 |
| brew upgrade | 升级所有过时的包 |
| brew upgrade FORMULA | 升级特定包 |

```bash
# 更新 Homebrew 和所有包
brew update && brew upgrade
```

## Casks（GUI 应用程序）

Cask 是通过 Homebrew 分发的预构建 macOS 应用程序。

| 命令 | 描述 |
|---------|-------------|
| brew install --cask APP | 安装桶 |
| brew list --cask | 列出已安装的桶 |
| brew uninstall --cask APP | 移除桶 |
| brew reinstall --cask APP | 重新安装桶 |

### 常用 Cask

| Cask | 应用程序 |
|------|-------------|
| firefox | Mozilla Firefox |
| google-chrome | Google Chrome |
| visual-studio-code | VS Code |
| docker | Docker Desktop |
| iterm2 | iTerm2 终端 |
| slack | Slack 消息 |
| vlc | VLC 媒体播放器 |
| 1password | 1Password 密码管理器 |

## Taps（第三方仓库）

| 命令 | 描述 |
|---------|-------------|
| brew tap USER/REPO | 添加第三方仓库 |
| brew untap USER/REPO | 移除仓库 |
| brew tap | 列出已添加的仓库 |

```bash
# 添加流行的 tap
brew tap homebrew/cask-fonts

# 从 tap 安装
brew install --cask font-fira-code
```

## Services（后台服务）

Homebrew 可以管理后台服务，类似于 systemd 或 launchctl。

| 命令 | 描述 |
|---------|-------------|
| brew services list | 列出管理的服务 |
| brew services start FORMULA | 启动服务 |
| brew services stop FORMULA | 停止服务 |
| brew services restart FORMULA | 重启服务 |
| brew services run FORMULA | 运行服务但不自动启动 |

```bash
# 将 PostgreSQL 作为服务启动
brew services start postgresql@15

# 检查运行中的服务
brew services list
```

## 环境管理

### 多版本

Homebrew 支持并排安装多个版本的软件。

```bash
# 安装 Python 3.11 和 3.12
brew install python@3.11
brew install python@3.12

# 使用特定版本
brew link python@3.11
```

### 链接

| 命令 | 描述 |
|---------|-------------|
| brew link FORMULA | 将包符号链接到前缀 |
| brew unlink FORMULA | 移除包的符号链接 |
| brew link --overwrite FORMULA | 强制链接，替换现有文件 |

## 清理

| 命令 | 描述 |
|---------|-------------|
| brew cleanup | 移除旧版本和缓存 |
| brew cleanup -n | 模拟运行（显示将被移除的内容） |
| brew cleanup --prune=all | 移除所有缓存的下载 |
| brew doctor | 诊断常见问题 |

## 开发者常用配方

| 配方 | 描述 |
|---------|-------------|
| git | 版本控制 |
| node | JavaScript 运行时 |
| python@3.12 | Python 编程语言 |
| go | Go 编程语言 |
| rust | Rust 编程语言 |
| docker | 容器运行时 |
| kubectl | Kubernetes CLI |
| terraform | 基础设施即代码 |
| jq | JSON 处理器 |
| wget | 文件下载器 |
| curl | URL 传输工具 |

## 配置

### Brewfile（依赖清单）

Brewfile 声明项目或系统的所有依赖。

```ruby
# Brewfile
tap "homebrew/cask-fonts"

brew "git"
brew "node"
brew "python@3.12"
brew "postgresql@15"

cask "visual-studio-code"
cask "docker"
cask "firefox"

mas "Xcode", id: 497799835
```

| 命令 | 描述 |
|---------|-------------|
| brew bundle | 从 Brewfile 安装 |
| brew bundle dump | 从已安装的包生成 Brewfile |
| brew bundle --global | 使用 ~/.Brewfile |
| brew bundle check | 检查是否所有依赖都已满足 |

## 技巧和最佳实践

| 技巧 | 说明 |
|-----|-------------|
| 定期运行 brew update | 保持配方定义最新 |
| 运行 brew doctor | 在问题造成麻烦之前修复常见问题 |
| 使用 Brewfile | 记录和重现您的设置 |
| 固定关键版本 | 使用 @version 语法防止不想要的升级 |
| 定期清理 | 通过移除旧版本释放磁盘空间 |

## 结论

Homebrew 是 macOS 和 Linux 用户从命令行管理软件安装的必备工具。其简单的语法和广泛的配方库使其成为开发者的标准包管理器。
