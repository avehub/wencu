![文促](./logo.png)

目录

- [文促](#intro)
  - [技术栈](#stack)
  - [开源地址](#opensource)
  - [使用手册](#manual)
  - [环境要求](#dev-env)
  - [目录结构](#dev-tree)
  - [app.toml](#dev-config)
  - [初始化](#dev-init)
  - [License](#license)
  - [鸣谢](#thanks)

<a name="intro"></a>

# 文促

    文促-是在[魔豆文库](https://github.com/mnt-ltd/moredoc)的基础实现， 使用 Golang 开发的开源文库系统，支持个人或企业团队 `TXT`、`PDF`、`EPUB`、`MOBI`、`Office` 等格式文档的在线预览与管理，整个项目开源并切支持二开，欢迎热心市民参与项目功能拓展及问题优化！

<a name="stack"></a>

## 技术栈

- Golang ：gin + gRPC + GORM
- Vue.js : nuxt2 + element-ui
- Database : MySQL 5.7

<a name="opensource"></a>

## 开源地址

- Github - https://github.com/avehub/wencu
- Gitee - https://github.com/avehub/wencu
- MNT.Ltd - https://git.mnt.ltd/mnt-ltd/moredoc

**前端Web页面**

- Github - https://github.com/mnt-ltd/moredoc-web
- Gitee - https://gitee.com/mnt-ltd/moredoc-web
- MNT.Ltd - https://git.mnt.ltd/mnt-ltd/moredoc-web

<a name="manual"></a>

## 使用手册

关于魔豆文库安装部署以及使用和二次开发等更详细的教程，详见书栈网[《魔豆文库使用手册》](https://www.bookstack.cn/books/moredoc)



<a name="dev-env"></a>

### 环境要求

- Golang 1.18+
- Node.js 14.16.0 (可用 nvm 管理)
- MySQL 5.7+

**请自行配置相应环境。如在此过程中遇到错误，请根据错误提示自行通过 Google 或者百度解决。**

<a name="dev-tree"></a>

### 目录结构

> 部分目录，在程序运行时自动生成，不需要手动创建

```bash
.
├── LICENSE                 # 开源协议
├── Makefile                # 编译脚本
├── README.md               # 项目说明
├── api                     # proto api， API协议定义
├── app.example.toml        # 配置文件示例，需要复制为 app.toml
├── biz                     # 业务逻辑层，主要处理业务逻辑，实现api接口
├── cmd                     # 命令行工具
├── cache                   # 缓存相关
├── conf                    # 配置定义
├── dict                    # 结巴分词字典，用于给文档自动进行分词
├── dist                    # 前端打包后的文件
├── docs                    # API文档等
├── documents               # 用户上传的文档存储目录
├── go.mod                  # go依赖管理
├── go.sum                  # go依赖管理
├── main.go                 # 项目入口
├── middleware              # 中间件
├── model                   # 数据库模型，使用gorm对数据库进行操作
├── release                 # 版本发布生成的版本会放到这里
├── service                 # 服务层，衔接cmd与biz
├── sitemap                 # 站点地图
├── third_party             # 第三方依赖，主要是proto文件
├── uploads                 # 文档文件之外的其他文件存储目录
├── util                    # 工具函数
└── web                     # 前端Web
```

<a name="dev-config"></a>

### app.toml

```
# 程序运行级别：debug、info、warn、error
level="debug"

# 日志编码方式，支持：json、console
logEncoding="console"

# 后端监听端口
port="8880"

# 数据库配置
[database]
    driver="mysql"
    dsn="root:root@tcp(localhost:3306)/moredoc?charset=utf8mb4&loc=Local&parseTime=true"
    showSQL=true
    maxOpen=10
    maxIdle=10

# jwt 配置
[jwt]
    secret="moredoc"
    expireDays=365
```

<a name="dev-init"></a>

### 初始化

**后端初始化**

```
# 安装go依赖
go mod tidy

# 初始化工程依赖
make init

# 编译proto api
make api

# 修改 app.toml 文件配置
cp app.example.toml app.toml

# 编译后端
go build -o moredoc main.go

# 初始化数据库结构
./moredoc syncdb

# 运行后端(可用其他热编译工具)，监听8880端口
go run main.go serve
```

<a name="license"></a>

## License

开源版本基于 [Apache License 2.0](./LICENSE) 协议发布。

<a name="thanks"></a>

## 鸣谢

