# 点分类帐

**来源：** https://github.com/dotledger/dotledger

＃＃ 概述

本教程涵盖了 [dotledger/dotledger](https://github.com/dotledger/dotledger) 项目中的关键资源和工具。

## 点分类帐

**[Dot Ledger](http://www.dotledger.com/)** 是一款免费开源的个人财务管理工具。

该项目的目的是创建一个稳定的、自由和开源的替代品 [Xero Personal](https://www.xero.com/personal/)
于 2014 年 11 月[关闭](http://blog.xero.com/2013/08/winding-down-xero-personal-in-november-2014/)。

＃＃ 设置

点分类账要求：

- [PostgreSQL](https://www.postgresql.org/)（使用 9.6 测试）
- [Ruby](https://www.ruby-lang.org/)（使用 2.3 测试）
- [RubyGems](https://rubygems.org/)
- [Ruby on Rails](http://rubyonrails.org/)
- [捆绑器](https://bundler.io/)
- [Git](https://git-scm.com/)

基本设置步骤是：

- `git 克隆 https://github.com/dotledger/dotledger.git`
- `cd dotledger`
- `cp config/database.yml.example config/database.yml`

您必须在 config/database.yml 中修改 postgres 用户名和密码。

- `捆绑安装`
- `bundle exec rake db:setup`
-`捆绑执行rails服务器`

## 运行所有测试

```
bundle exec rake spec spec:javascript
```

## 运行 ruby​​ 测试 ([RSpec](http://rspec.info/))

```
bundle exec rake spec
```

## 运行 javascript 测试 ([Jasmine](http://jasmine.github.io/))

```
bundle exec rake spec:javascript
```

## 截图

请参阅 [Dot Ledger 网站](http://www.dotledger.com/) 的[屏幕截图部分](http://www.dotledger.com/#screenshots)。

＃＃ 执照

版权所有 2013 - 2018，Kale Worsley，BitBot Limited。

Dot Ledger 根据 Apache 许可证版本 2.0 提供。有关详细信息，请参阅[许可证]（许可证）。

## 关键资源

|资源 |链接 |
|----------|------|
|点分类帐| [http://www.dotledger.com/](http://www.dotledger.com/) |
| Xero 个人 | [https://www.xero.com/personal/](https://www.xero.com/personal/) |
|关闭| [http://blog.xero.com/2013/08/winding-down-xero-personal-in-november-2014/](http://blog.xero.com/2013/08/winding-down-xero-personal-in-november-2014/) |
| PostgreSQL | [https://www.postgresql.org/](https://www.postgresql.org/) |
|红宝石 | [https://www.ruby-lang.org/](https://www.ruby-lang.org/) |
|红宝石 | [https://rubygems.org/](https://rubygems.org/) |
| Ruby on Rails | Ruby on Rails [http://rubyonrails.org/](http://rubyonrails.org/) |
|捆绑器 | [https://bundler.io/](https://bundler.io/) |
| git | git [https://git-scm.com/](https://git-scm.com/) |
|规格| [http://rspec.info/](http://rspec.info/) |
|茉莉花| [http://jasmine.github.io/](http://jasmine.github.io/) |
|截图部分| [http://www.dotledger.com/#screenshots](http://www.dotledger.com/#screenshots) |
|点分类网站 | [http://www.dotledger.com/](http://www.dotledger.com/) |

