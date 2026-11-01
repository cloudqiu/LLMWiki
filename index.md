# Index — 知识库目录

> 内容目录（content-oriented）：本库所有页面的清单。每次 ingest 后更新；查询时**先读本文件**找候选页面，再深入具体页面。
> 维护规则见 `AGENTS.md`（Codex）与 `CLAUDE.md`（Claude Code）。最近更新：2026-11-01。

## Sources 来源

- [[llm-wiki-pattern]] — Karpathy《LLM Wiki》gist：模式原始定义，本库创世文档。2026-10-01 摄入，派生 8 个页面。
- [[as-we-may-think]] — Vannevar Bush《As We May Think》(The Atlantic, 1945-07)：memex 与关联索引的一手文献。2026-10-01 摄入，派生/更新 6 个页面。
- [[claude-code-obsidian-tutorial]] — RUNOOB 中文教程：Claude Code + Obsidian 从零搭建 LLM Wiki；含主题/插件清单与目录结构变体。2026-10-01 摄入，新建 3 页、更新 6 页。
- [[windows-terminal-tutorial]] — 光影紐扣科普连载：Windows Terminal 入门——「不是新命令，是新窗口」。**本库首份非 PKM 来源**（OS/开发环境层）。2026-10-06 摄入，新建 8 页、更新 1 页。
- [[dissecting-penpot]] — Penpot 2.18 Docker Compose 安装与镜像检查快照：8 个服务、持久化卷及部署边界。2026-10-21 摄入，派生 2 页。
- [[gophernotes-official-research]] — gophernotes 官方 README 与补全源码的查阅记录；本地未取得官方原文副本。2026-10-31 摄入。
- [[chi-official-research]] — chi v5.5.0 官方文档、仓库与作者项目资料的查阅记录；本地未取得官方原文副本。2026-10-31 摄入。
- [[google-uuid-official-research]] — google/uuid v1.6.0 官方文档、项目沿革与贡献者资料的查阅记录；本地未取得官方原文副本。2026-10-31 摄入。
- [[pgx-official-research]] — pgx v5.12.0 官方文档、变更记录与作者关联项目的查阅记录；本地未取得官方原文副本。2026-10-31 摄入。
- [[koanf-toml-v2-official-research]] — koanf TOML parser v2.2.2 的模块、源码与项目作者资料查阅记录；本地未取得官方原文副本。2026-10-31 摄入。

- [[koanf-rawbytes-go-official-research]] — 把内存中的 []byte 作为 koanf 配置源；常与 JSON、TOML 等 parser 配合。 官方页面的 2026-10-31 查阅记录。
- [[koanf-v2-go-official-research]] — 从多种 provider 与 parser 加载、合并和读取配置。 官方页面的 2026-10-31 查阅记录。
- [[zerolog-go-official-research]] — 链式 API 输出结构化 JSON 日志，适合低分配的服务日志。 官方页面的 2026-10-31 查阅记录。
- [[do-go-official-research]] — 使用泛型注册、解析服务及管理依赖注入生命周期。 官方页面的 2026-10-31 查阅记录。
- [[etcd-client-pkg-v3-go-official-research]] — etcd 客户端共享基础包的模块集合，例如 types、fileutil。 官方页面的 2026-10-31 查阅记录。
- [[etcd-server-v3-go-official-research]] — 运行 etcd 服务端及嵌入式服务的模块集合。 官方页面的 2026-10-31 查阅记录。
- [[zap-go-official-research]] — Uber Go 的结构化日志库，以强类型字段记录日志。 官方页面的 2026-10-31 查阅记录。
- [[protobuf-go-official-research]] — Protocol Buffers 的 Go 运行时、反射与代码生成生态。 官方页面的 2026-10-31 查阅记录。
- [[perks-go-official-research]] — 提供流式近似分位数 quantile 等 Go 工具包。 官方页面的 2026-10-31 查阅记录。
- [[xxhash-v2-go-official-research]] — 计算快速的 XXH64 非密码学哈希。 官方页面的 2026-10-31 查阅记录。
- [[go-figure-go-official-research]] — 把文本渲染为终端 ASCII 字画。 官方页面的 2026-10-31 查阅记录。
- [[go-semver-go-official-research]] — 解析和比较 SemVer 版本号。 官方页面的 2026-10-31 查阅记录。
- [[huma-v2-go-official-research]] — 以 Go 类型定义 HTTP API 并生成 OpenAPI 文档与验证逻辑。 官方页面的 2026-10-31 查阅记录。
- [[fsnotify-go-official-research]] — 跨平台文件系统变更通知。 官方页面的 2026-10-31 查阅记录。
- [[mapstructure-v2-go-official-research]] — 将 map 解码到 Go struct，常用于配置处理。 官方页面的 2026-10-31 查阅记录。
- [[pgerrcode-go-official-research]] — 给 PostgreSQL SQLSTATE 错误码提供命名常量。 官方页面的 2026-10-31 查阅记录。
- [[pgpassfile-go-official-research]] — 解析 PostgreSQL .pgpass 密码文件并查找匹配密码。 官方页面的 2026-10-31 查阅记录。
- [[pgservicefile-go-official-research]] — 解析 PostgreSQL .pg_service.conf 服务配置。 官方页面的 2026-10-31 查阅记录。
- [[puddle-v2-go-official-research]] — 以泛型提供最小化的并发资源池。 官方页面的 2026-10-31 查阅记录。
- [[koanf-maps-go-official-research]] — 供 koanf 使用的嵌套 map 复制、合并、展开等工具。 官方页面的 2026-10-31 查阅记录。
- [[koanf-file-go-official-research]] — koanf 文件 provider 的官方包文档、README 与源码查阅记录；版本和监听事件差异已标注。

- [[go-colorable-go-official-research]] — 在 Windows 终端处理 ANSI 色彩输出；适合需要跨平台彩色日志的程序。 2026-11-01 官方资料查阅记录。
- [[go-isatty-go-official-research]] — 检测文件描述符是否连接终端，用于决定颜色、交互提示等输出。 2026-11-01 官方资料查阅记录。
- [[copystructure-go-official-research]] — 递归复制包含 map、slice、指针等引用值的 Go 数据。 2026-11-01 官方资料查阅记录。
- [[reflectwalk-go-official-research]] — 按反射方式遍历复杂 Go 值，并通过 walker 接口处理节点。 2026-11-01 官方资料查阅记录。
- [[goautoneg-go-official-research]] — 根据 HTTP Accept 请求头从候选媒体类型中选择响应 Content-Type。 2026-11-01 官方资料查阅记录。
- [[go-toml-v2-go-official-research]] — 把 TOML 文本解码为 Go 结构，也可将结构编码为 TOML。 2026-11-01 官方资料查阅记录。
- [[prometheus-client-golang-go-official-research]] — 在 Go 服务中创建和收集 Prometheus 指标。 2026-11-01 官方资料查阅记录。
- [[prometheus-client-model-go-official-research]] — Prometheus Go 指标数据模型的 protobuf 类型；供 client_golang 等组件交换指标。 2026-11-01 官方资料查阅记录。
- [[prometheus-common-go-official-research]] — Prometheus 组件共享的 Go 包；expfmt 处理指标文本与格式协商。 2026-11-01 官方资料查阅记录。
- [[prometheus-procfs-go-official-research]] — 读取 Linux /proc 的进程和内核统计数据。 2026-11-01 官方资料查阅记录。
- [[probing-go-official-research]] — 通过 HTTP 健康端点持续探测目标，统计丢包和往返时间。 2026-11-01 官方资料查阅记录。
- [[etcd-api-v3-go-official-research]] — etcd v3 的协议和数据模型包，供客户端、服务端共享。 2026-11-01 官方资料查阅记录。
- [[etcd-pkg-v3-go-official-research]] — etcd 内部和周边使用的通用工具包集合。 2026-11-01 官方资料查阅记录。
- [[yaml-v2-go-official-research]] — 将 YAML 编解码为 Go 值，提供严格解码以发现未知字段和重复键。 2026-11-01 官方资料查阅记录。
- [[x-sync-go-official-research]] — 补充 Go 并发原语；errgroup 汇聚 goroutine 错误并传播取消。 2026-11-01 官方资料查阅记录。
- [[x-sys-go-official-research]] — 提供 Go 标准库之外的系统调用绑定，按操作系统分子包。 2026-11-01 官方资料查阅记录。
- [[x-text-go-official-research]] — 提供国际化、Unicode、字符编码、语言区域等文本处理子包。 2026-11-01 官方资料查阅记录。
- [[x-time-go-official-research]] — 提供时间相关辅助包；rate 用 token bucket 限制事件速率。 2026-11-01 官方资料查阅记录。
- [[latency-percentiles-notes]] — P50/P90/P99 原始说明及完整分布、SLO、类比表述的核对。
- [[single-instance-p99-simulation]] — Go 单实例模拟原文；核对 `Count()`、格式化输出和误差定义。
- [[multi-instance-p99-examples]] — 多实例 P99 原始方案；标注 perks Merge 损坏、t-digest API 不符与 Histogram 查询要求。

- [[gci-go-official-research]] — 按可配置分组确定性整理 Go import，适合代码风格检查。 2026-11-01 官方资料查阅记录。
- [[golangci-lint-v2-go-official-research]] — 聚合多种 Go linter 并统一配置、运行，适合项目和 CI。 2026-11-01 官方资料查阅记录。
- [[mage-go-official-research]] — 用 Go 函数定义项目构建任务，适合替代部分 Makefile 脚本。 2026-11-01 官方资料查阅记录。
- [[gofumpt-go-official-research]] — 在 gofmt 基础上施加更严格的 Go 代码格式规则。 2026-11-01 官方资料查阅记录。
- [[gocheckcompilerdirectives-go-official-research]] — 检查 //go: 编译器指令注释是否有效，适合静态检查。 2026-11-01 官方资料查阅记录。
- [[gochecknoglobals-go-official-research]] — 检测 Go 包级全局变量，帮助限制可变全局状态。 2026-11-01 官方资料查阅记录。
- [[lipgloss-v2-go-official-research]] — 为终端 UI 文本和布局声明样式，适合 Charm 生态 TUI。 2026-11-01 官方资料查阅记录。
- [[garif-go-official-research]] — 构造、修改并输出 SARIF 2.1.0 静态分析结果日志。 2026-11-01 官方资料查阅记录。
- [[go-errorlint-go-official-research]] — 检查 Go 错误比较、类型断言与包装等用法，适合迁移至 errors.Is/As。 2026-11-01 官方资料查阅记录。
- [[mergo-go-official-research]] — 把源结构体或 map 的值合并到目标，常用于填入默认配置。 2026-11-01 官方资料查阅记录。
- [[exhaustruct-v5-go-official-research]] — 检查结构体字面量是否显式初始化全部字段。 2026-11-01 官方资料查阅记录。
- [[golib-gaijin-go-official-research]] — Gaijin 的通用 Go 子包集合，可按需使用构建信息等组件。 2026-11-01 官方资料查阅记录。
- [[tagalign-go-official-research]] — 对齐和整理 Go struct tag，适合格式检查与修复。 2026-11-01 官方资料查阅记录。
- [[dupword-go-official-research]] — 检查 Go 代码或注释中的重复单词。 2026-11-01 官方资料查阅记录。
- [[iota-mixing-go-official-research]] — 识别同一 const 块内把无关常量与 iota 枚举混写的风险。 2026-11-01 官方资料查阅记录。
- [[noinlineerr-go-official-research]] — 检查在 if 语句初始化部分内联声明 err 的写法。 2026-11-01 官方资料查阅记录。
- [[errname-go-official-research]] — 检查哨兵错误 Err 前缀和错误类型 Error 后缀命名。 2026-11-01 官方资料查阅记录。

- [[nilnil-go-official-research]] — 检查同时返回 nil 值和 nil error 的含糊结果。 2026-11-01 官方资料查阅记录。
- [[testifylint-go-official-research]] — 检查 testify 测试断言写法，减少含糊或错误的断言。 2026-11-01 官方资料查阅记录。
- [[burntsushi-toml-go-official-research]] — 把 TOML 文本解码到 Go 结构体并编码回 TOML。 2026-11-01 官方资料查阅记录。
- [[clickhouse-go-linter-go-official-research]] — 检查 ClickHouse 原生 Go API 中 rows.Err 和 batch.Close 遗漏。 2026-11-01 官方资料查阅记录。
- [[go-err113-go-official-research]] — 检查错误直接比较与动态新建错误等 Go 1.13 后错误处理风格。 2026-11-01 官方资料查阅记录。
- [[masterminds-semver-v3-go-official-research]] — 解析 Semantic Version 并检验版本约束。 2026-11-01 官方资料查阅记录。
- [[unqueryvet-go-official-research]] — 检查 SQL 查询中 SELECT * 等不显式选列的写法。 2026-11-01 官方资料查阅记录。
- [[depguard-v2-go-official-research]] — 按 allow/deny 规则检查 Go import。 2026-11-01 官方资料查阅记录。
- [[air-go-official-research]] — 开发时监听 Go 项目变更并自动重新构建、运行。 2026-11-01 官方资料查阅记录。
- [[chroma-v2-go-official-research]] — 以纯 Go lexer 和 formatter 给代码做语法高亮。 2026-11-01 官方资料查阅记录。
- [[go-check-sumtype-go-official-research]] — 检查 Go 模拟 sum type 的 switch 分支是否穷尽。 2026-11-01 官方资料查阅记录。
- [[nakedret-v2-go-official-research]] — 找出超过长度阈值的函数里的裸 return。 2026-11-01 官方资料查阅记录。
- [[prealloc-go-official-research]] — 提示可预分配容量的 slice 构造，减少扩容。 2026-11-01 官方资料查阅记录。
- [[alfatraining-structtag-go-official-research]] — 解析和检查 Go 结构体字段 tag。 2026-11-01 官方资料查阅记录。
- [[asasalint-go-official-research]] — 找出把 any slice 错误地作为单个 any 传入可变参数函数的情况。 2026-11-01 官方资料查阅记录。
- [[nilnesserr-go-official-research]] — 组合 nilness 与 nilerr 检查，找出不一致的 nil/error 返回。 2026-11-01 官方资料查阅记录。
- [[brotli-go-official-research]] — 纯 Go Brotli 编码与解码，适合 HTTP 压缩或文件流。 2026-11-01 官方资料查阅记录。
- [[forbidigo-v2-go-official-research]] — 按规则禁止特定 Go 标识符或调用，例如调试输出。 2026-11-01 官方资料查阅记录。
- [[makezero-v2-go-official-research]] — 检查先创建非零长度 slice 又 append 导致多出零值元素。 2026-11-01 官方资料查阅记录。
- [[godartsass-v2-go-official-research]] — 通过 Dart Sass Embedded 协议从 Go 编译 Sass/SCSS。 2026-11-01 官方资料查阅记录。
- [[golibsass-go-official-research]] — 从 Go 调用 LibSass 编译 SCSS。 2026-11-01 官方资料查阅记录。
- [[bitset-go-official-research]] — 用可扩展位集合存储非负整数的布尔状态。 2026-11-01 官方资料查阅记录。
- [[emotional-control-leadership-clipping]] — 职场压力和分歧中的表达建议；区分作者观点与实证结论。
- [[rust-cell-family-clipping]] — Rust Cell 家族的内部可变性梳理，并按官方文档核对借用与初始化边界。
- [[sqlite-2018-dialect-clipping]] — SQLite 2018 SQL 特性转载；剪藏标题与正文不符，FILTER 结论已过时。

- [[cyclop-go-official-research]] — 检测 Go 函数和包的圈复杂度。 2026-11-01 官方资料查阅记录。
- [[wsl-v5-go-official-research]] — 检查 Go 语句间的空行和分组风格。 2026-11-01 官方资料查阅记录。
- [[bidichk-go-official-research]] — 检测源码中可能改变显示顺序的危险双向 Unicode 控制符。 2026-11-01 官方资料查阅记录。
- [[errchkjson-go-official-research]] — 检查 JSON 编码的不可支持类型与可省略的错误处理。 2026-11-01 官方资料查阅记录。
- [[ireturn-go-official-research]] — 提示函数返回接口类型的设计选择。 2026-11-01 官方资料查阅记录。
- [[mirror-go-official-research]] — 提示可避免 string 与 []byte 转换的对应标准库调用。 2026-11-01 官方资料查阅记录。
- [[perfsprint-go-official-research]] — 找出可用 strconv 等更直接操作替代的 fmt 格式化调用。 2026-11-01 官方资料查阅记录。
- [[zxcvbn-go-official-research]] — 估计密码强度并识别常见词和模式。 2026-11-01 官方资料查阅记录。
- [[durationcheck-go-official-research]] — 检查两个 time.Duration 相乘的可疑写法。 2026-11-01 官方资料查阅记录。
- [[colorprofile-go-official-research]] — 检测终端色彩能力并自动降级颜色输出。 2026-11-01 官方资料查阅记录。
- [[ultraviolet-go-official-research]] — 提供终端 UI 的 cell 绘制、输入和差量渲染原语。 2026-11-01 官方资料查阅记录。
- [[charm-x-ansi-go-official-research]] — 解析、生成和清理 ANSI 终端控制序列。 2026-11-01 官方资料查阅记录。
- [[charm-x-term-go-official-research]] — 跨平台查询终端大小、TTY 状态及原始模式。 2026-11-01 官方资料查阅记录。
- [[charm-x-termios-go-official-research]] — 在 Unix 终端读取或设置 termios 与窗口尺寸。 2026-11-01 官方资料查阅记录。
- [[charm-x-windows-go-official-research]] — 封装 Charm 所需的 Windows Console 输入记录与系统调用。 2026-11-01 官方资料查阅记录。
- [[intrange-go-official-research]] — 找出可改用 Go 1.22 整数 range 的循环。 2026-11-01 官方资料查阅记录。
- [[displaywidth-go-official-research]] — 按 Unicode 字素簇计算等宽终端显示列宽。 2026-11-01 官方资料查阅记录。
- [[uax29-v2-go-official-research]] — 按 Unicode UAX #29 分割字素、单词和句子。 2026-11-01 官方资料查阅记录。

- [[curioswitch-go-reassign-go-official-research]] — 检查对其他包顶层变量的重新赋值：2026-11-01 官方仓库查阅记录。
- [[dave-dst-go-official-research]] — 保留注释和间距地改写 Go 语法树：2026-11-01 官方仓库查阅记录。
- [[denis-tingaikin-go-header-go-official-research]] — 检查 Go 源码的版权头：2026-11-01 官方仓库查阅记录。
- [[dlclark-regexp2-go-official-research]] — 提供兼容 .NET 特性的回溯式正则引擎：2026-11-01 官方仓库查阅记录。
- [[ettle-strcase-go-official-research]] — 转换 snake_case、camelCase 等命名形式：2026-11-01 官方仓库查阅记录。
- [[fatih-color-go-official-research]] — 向终端输出 ANSI 颜色文本：2026-11-01 官方仓库查阅记录。
- [[fatih-structtag-go-official-research]] — 解析和修改 Go struct 字段标签：2026-11-01 官方仓库查阅记录。
- [[firefart-nonamedreturns-go-official-research]] — 检查函数签名中的命名返回值：2026-11-01 官方仓库查阅记录。
- [[fzipp-gocyclo-go-official-research]] — 计算 Go 函数的圈复杂度：2026-11-01 官方仓库查阅记录。
- [[ghostiam-protogetter-go-official-research]] — 检查 protobuf 嵌套字段的直接访问：2026-11-01 官方仓库查阅记录。
- [[go-critic-go-critic-go-official-research]] — 运行可扩展的 Go 代码审查规则：2026-11-01 官方仓库查阅记录。
- [[go-toolsmith-astcast-go-official-research]] — 安全地将 AST 节点转换为具体类型：2026-11-01 官方仓库查阅记录。
- [[go-toolsmith-astequal-go-official-research]] — 比较 Go AST 结构是否相等：2026-11-01 官方仓库查阅记录。
- [[go-toolsmith-astfmt-go-official-research]] — 以 fmt 风格格式化 Go AST 节点：2026-11-01 官方仓库查阅记录。
- [[go-toolsmith-astp-go-official-research]] — 测试 AST 节点类型：2026-11-01 官方仓库查阅记录。
- [[go-toolsmith-strparse-go-official-research]] — 将短字符串解析为 Go 表达式、语句或声明：2026-11-01 官方仓库查阅记录。
- [[go-toolsmith-typep-go-official-research]] — 判断 go/types 类型的性质：2026-11-01 官方仓库查阅记录。
- [[gobwas-glob-go-official-research]] — 编译并匹配 glob 模式：2026-11-01 官方仓库查阅记录。
- [[godoc-lint-godoc-lint-go-official-research]] — 检查 Go 文档注释规范：2026-11-01 官方仓库查阅记录。
- [[gofrs-flock-go-official-research]] — 提供文件锁及非阻塞获取：2026-11-01 官方仓库查阅记录。
- [[gohugoio-hashstructure-go-official-research]] — 为 Go 值生成结构哈希：2026-11-01 官方仓库查阅记录。
- [[gohugoio-hugo-go-official-research]] — 从内容和模板生成静态网站：2026-11-01 官方仓库查阅记录。
- [[golang-protobuf-go-official-research]] — 旧版 Go Protocol Buffers 绑定：2026-11-01 官方仓库查阅记录。
- [[golangci-asciicheck-go-official-research]] — 检查 Go 标识符中的非 ASCII 字符：2026-11-01 官方仓库查阅记录。
- [[golangci-canonicalheader-go-official-research]] — 检查 HTTP header 名称的规范大小写：2026-11-01 官方仓库查阅记录。
- [[golangci-dupl-go-official-research]] — 检测重复的 Go 代码片段：2026-11-01 官方仓库查阅记录。
- [[golangci-go-printf-func-name-go-official-research]] — 检查 printf 风格函数名称：2026-11-01 官方仓库查阅记录。
- [[golangci-gofmt-go-official-research]] — 将 gofmt 检查集成到 golangci 工具链：2026-11-01 官方仓库查阅记录。
- [[golangci-golines-go-official-research]] — 格式化过长的 Go 源码行：2026-11-01 官方仓库查阅记录。
- [[golangci-misspell-go-official-research]] — 检查英文拼写错误：2026-11-01 官方仓库查阅记录。
- [[golangci-plugin-module-register-go-official-research]] — 提供 golangci 插件模块的注册包：2026-11-01 官方仓库查阅记录。
- [[golangci-revgrep-go-official-research]] — 只显示变更行上的静态分析结果：2026-11-01 官方仓库查阅记录。
- [[golangci-rowserrcheck-go-official-research]] — 检查 SQL 查询循环后是否读取 Rows.Err：2026-11-01 官方仓库查阅记录。
- [[golangci-swaggoswag-go-official-research]] — 供 golangci 集成的 swaggo/swag 维护分支：2026-11-01 官方仓库查阅记录。
- [[golangci-unconvert-go-official-research]] — 检查不必要的 Go 类型转换：2026-11-01 官方仓库查阅记录。
- [[google-go-cmp-go-official-research]] — 比较 Go 值并给出结构化差异：2026-11-01 官方仓库查阅记录。
- [[gordonklaus-ineffassign-go-official-research]] — 检测无效赋值：2026-11-01 官方仓库查阅记录。
- [[gostaticanalysis-analysisutil-go-official-research]] — 为 go/analysis 分析器提供辅助函数：2026-11-01 官方仓库查阅记录。
- [[gostaticanalysis-comment-go-official-research]] — 为静态分析提供 ast.CommentMap 辅助工具：2026-11-01 官方仓库查阅记录。
- [[gostaticanalysis-forcetypeassert-go-official-research]] — 检测未检查的 Go 类型断言：2026-11-01 官方仓库查阅记录。
- [[gostaticanalysis-nilerr-go-official-research]] — 检测检查 error 后仍返回 nil 的错误分支：2026-11-01 官方仓库查阅记录。
- [[hashicorp-go-immutable-radix-go-official-research]] — 提供泛型不可变 radix tree：2026-11-01 官方仓库查阅记录。
- [[hashicorp-go-version-go-official-research]] — 解析和比较语义版本及约束：2026-11-01 官方仓库查阅记录。
- [[hashicorp-golang-lru-go-official-research]] — 提供线程安全的泛型 LRU 缓存：2026-11-01 官方仓库查阅记录。
- [[hashicorp-hcl-go-official-research]] — 解析和生成结构化配置语言：2026-11-01 官方仓库查阅记录。

## Concepts 概念

- [[latency-percentiles]] — 延迟分位数的定义、用途、样本窗口与三个点不能重建完整分布的边界。
- [[distributed-quantiles]] — 全局 P99 不能平均各实例 P99；Histogram 聚合与可合并摘要的证据边界。
- [[emotional-control-at-work]] — 压力和异议沟通的具体做法，以及文章观点的证据边界。
- [[rust-interior-mutability]] — Cell、RefCell、OnceCell、LazyCell 和 UnsafeCell 的选择线索。
- [[sqlite-filter-clause]] — SQLite 普通聚合 FILTER 自 3.30.0 起支持；与 2018 年资料的矛盾。
- [[llm-wiki]] — 核心模式：LLM 增量维护的持久化 wiki；三层架构 + ingest/query/lint 三操作。
- [[retrieval-augmented-generation]] — RAG：查询时检索切片生成答案，无知识积累。
- [[memex]] — 桌面式私人「文件与图书馆」(1945)：微缩胶片 + 投影屏 + 关联路径。
- [[associative-trails]] — 关联索引/路径：memex 的核心机制；超链接与交叉引用的思想原点。
- [[command-line-interface]] — 命令行界面（CLI）：终端（那扇窗）≠ shell（那个程序）；本地 AI 工具链的执行层。

## Entities 实体

- [[andrej-karpathy]] — AI 研究者；LLM Wiki 模式作者。（stub）
- [[vannevar-bush]] — OSRD 主任（1945）；memex 构想提出者。
- [[obsidian]] — 本地优先的 markdown 知识管理应用；本库的浏览 IDE。
- [[qmd]] — 本地 markdown 搜索引擎（BM25 + 向量 + LLM 重排）。（stub）
- [[claude-code]] — Anthropic 的终端 agent；本库的维护者（「LLM 是程序员」中的程序员）。
- [[runoob]] — 发布本库首份中文教程来源的公众号。（stub）
- [[windows-terminal]] — 微软现代终端模拟器：把 CMD / PowerShell / WSL 装进同一窗口的标签与窗格。
- [[command-prompt]] — Windows 传统命令行 `cmd.exe`：`.bat` 脚本与基础操作。（stub）
- [[powershell]] — 微软现代命令行与脚本环境；AI 工具链在 Windows 上的默认落点。（stub）
- [[wsl]] — Windows Subsystem for Linux：本地 AI 工具（`apt` / `python` / `ollama`）的栖息地。（stub）
- [[winget]] — Windows 命令行包管理器：让「装个新外壳」变成一行可复制的命令。（stub）
- [[guangying-niukou]] — 发布「AI 时代命令行」连载的公众号（署名「凡哥哥」）。（stub）
- [[penpot]] — 可自托管的协作设计平台；本库目前记录其一次 Docker 部署快照。
- [[gophernotes-go]] — Jupyter 的 Go kernel：用途、两个典型代码单元、补全与 Windows 限制。
- [[chi-go]] — Go `net/http` 路由库 chi v5：安装、路径参数、关键限制与作者。
- [[peter-kieltyka]] — chi 作者；索引其在本库已摄入的库及官方资料可核实的其他项目。
- [[google-uuid-go]] — Go UUID 库：生成、解析、格式与随机池的关键限制。
- [[paul-borman]] — google/uuid 贡献者及历史版本发布参与者；索引其账号下的其他 Go 库。
- [[pgx-go]] — PostgreSQL 的 Go 驱动与工具集：基础查询、连接池选用及 v5.12.0 修复。
- [[jack-christensen]] — pgx 原始署名者和近期发布参与者；索引其关联的 PostgreSQL 工具。
- [[koanf-toml-v2-go]] — koanf 的独立 TOML v2 parser 模块：安装、加载配置与关键边界。
- [[kailash-nadh]] — koanf 原始版权署名者和近期发布参与者；索引其账号下的其他 Go 库。

- [[koanf-rawbytes-go]] — 把内存中的 []byte 作为 koanf 配置源；常与 JSON、TOML 等 parser 配合。
- [[koanf-v2-go]] — 从多种 provider 与 parser 加载、合并和读取配置。
- [[zerolog-go]] — 链式 API 输出结构化 JSON 日志，适合低分配的服务日志。
- [[do-go]] — 使用泛型注册、解析服务及管理依赖注入生命周期。
- [[etcd-client-pkg-v3-go]] — etcd 客户端共享基础包的模块集合，例如 types、fileutil。
- [[etcd-server-v3-go]] — 运行 etcd 服务端及嵌入式服务的模块集合。
- [[zap-go]] — Uber Go 的结构化日志库，以强类型字段记录日志。
- [[protobuf-go]] — Protocol Buffers 的 Go 运行时、反射与代码生成生态。
- [[perks-go]] — 提供流式近似分位数 quantile 等 Go 工具包。
- [[xxhash-v2-go]] — 计算快速的 XXH64 非密码学哈希。
- [[go-figure-go]] — 把文本渲染为终端 ASCII 字画。
- [[go-semver-go]] — 解析和比较 SemVer 版本号。
- [[huma-v2-go]] — 以 Go 类型定义 HTTP API 并生成 OpenAPI 文档与验证逻辑。
- [[fsnotify-go]] — 跨平台文件系统变更通知。
- [[mapstructure-v2-go]] — 将 map 解码到 Go struct，常用于配置处理。
- [[pgerrcode-go]] — 给 PostgreSQL SQLSTATE 错误码提供命名常量。
- [[pgpassfile-go]] — 解析 PostgreSQL .pgpass 密码文件并查找匹配密码。
- [[pgservicefile-go]] — 解析 PostgreSQL .pg_service.conf 服务配置。
- [[puddle-v2-go]] — 以泛型提供最小化的并发资源池。
- [[koanf-maps-go]] — 供 koanf 使用的嵌套 map 复制、合并、展开等工具。
- [[koanf-file-go]] — 从磁盘读取配置文件原始字节，配合 parser 加载并可监听变更。

- [[olivier-poitrey]] — Olivier Poitrey 的身份、已摄入库和其他经官方账号核实的项目。

- [[samuel-berthe]] — Samuel Berthe 的身份、已摄入库和其他经官方账号核实的项目。

- [[caleb-spare]] — Caleb Spare 的身份、已摄入库和其他经官方账号核实的项目。

- [[daniel-deutsch]] — Daniel Deutsch 的身份、已摄入库和其他经官方账号核实的项目。

- [[daniel-g-taylor]] — Daniel G. Taylor 的身份、已摄入库和其他经官方账号核实的项目。

- [[etcd-io]] — etcd-io 项目组织：本库模块及经官方账号核实的其他项目。

- [[uber-go]] — uber-go 项目组织：本库模块及经官方账号核实的其他项目。

- [[protocolbuffers]] — protocolbuffers 项目组织：本库模块及经官方账号核实的其他项目。

- [[fsnotify-project]] — fsnotify 项目组织：本库模块及经官方账号核实的其他项目。

- [[go-viper]] — go-viper 项目组织：本库模块及经官方账号核实的其他项目。

- [[coreos]] — coreos 项目组织：本库模块及经官方账号核实的其他项目。

- [[bjorn-rabenstein]] — perks 当前仓库账号的公开身份与已摄入库。
- [[blake-mizerany]] — perks 原始版权署名者与已摄入库。

- [[go-colorable-go]] — 在 Windows 终端处理 ANSI 色彩输出；适合需要跨平台彩色日志的程序。
- [[go-isatty-go]] — 检测文件描述符是否连接终端，用于决定颜色、交互提示等输出。
- [[copystructure-go]] — 递归复制包含 map、slice、指针等引用值的 Go 数据。
- [[reflectwalk-go]] — 按反射方式遍历复杂 Go 值，并通过 walker 接口处理节点。
- [[goautoneg-go]] — 根据 HTTP Accept 请求头从候选媒体类型中选择响应 Content-Type。
- [[go-toml-v2-go]] — 把 TOML 文本解码为 Go 结构，也可将结构编码为 TOML。
- [[prometheus-client-golang-go]] — 在 Go 服务中创建和收集 Prometheus 指标。
- [[prometheus-client-model-go]] — Prometheus Go 指标数据模型的 protobuf 类型；供 client_golang 等组件交换指标。
- [[prometheus-common-go]] — Prometheus 组件共享的 Go 包；expfmt 处理指标文本与格式协商。
- [[prometheus-procfs-go]] — 读取 Linux /proc 的进程和内核统计数据。
- [[probing-go]] — 通过 HTTP 健康端点持续探测目标，统计丢包和往返时间。
- [[etcd-api-v3-go]] — etcd v3 的协议和数据模型包，供客户端、服务端共享。
- [[etcd-pkg-v3-go]] — etcd 内部和周边使用的通用工具包集合。
- [[yaml-v2-go]] — 将 YAML 编解码为 Go 值，提供严格解码以发现未知字段和重复键。
- [[x-sync-go]] — 补充 Go 并发原语；errgroup 汇聚 goroutine 错误并传播取消。
- [[x-sys-go]] — 提供 Go 标准库之外的系统调用绑定，按操作系统分子包。
- [[x-text-go]] — 提供国际化、Unicode、字符编码、语言区域等文本处理子包。
- [[x-time-go]] — 提供时间相关辅助包；rate 用 token bucket 限制事件速率。

- [[yasuhiro-matsumoto]] — go-colorable 与 go-isatty README 署名作者及其他项目线索。
- [[mitchell-hashimoto]] — copystructure、reflectwalk 账号关联及归档状态。
- [[thomas-pelletier]] — go-toml 项目账号身份及 v1/v2 模块关系。
- [[prometheus-project]] — 本库四个 Prometheus Go 模块的项目组织索引。
- [[gustavo-niemeyer]] — go-yaml 原始开发者及项目停止维护声明。

- [[gci-go]] — 按可配置分组确定性整理 Go import，适合代码风格检查。
- [[golangci-lint-v2-go]] — 聚合多种 Go linter 并统一配置、运行，适合项目和 CI。
- [[mage-go]] — 用 Go 函数定义项目构建任务，适合替代部分 Makefile 脚本。
- [[gofumpt-go]] — 在 gofmt 基础上施加更严格的 Go 代码格式规则。
- [[gocheckcompilerdirectives-go]] — 检查 //go: 编译器指令注释是否有效，适合静态检查。
- [[gochecknoglobals-go]] — 检测 Go 包级全局变量，帮助限制可变全局状态。
- [[lipgloss-v2-go]] — 为终端 UI 文本和布局声明样式，适合 Charm 生态 TUI。
- [[garif-go]] — 构造、修改并输出 SARIF 2.1.0 静态分析结果日志。
- [[go-errorlint-go]] — 检查 Go 错误比较、类型断言与包装等用法，适合迁移至 errors.Is/As。
- [[mergo-go]] — 把源结构体或 map 的值合并到目标，常用于填入默认配置。
- [[exhaustruct-v5-go]] — 检查结构体字面量是否显式初始化全部字段。
- [[golib-gaijin-go]] — Gaijin 的通用 Go 子包集合，可按需使用构建信息等组件。
- [[tagalign-go]] — 对齐和整理 Go struct tag，适合格式检查与修复。
- [[dupword-go]] — 检查 Go 代码或注释中的重复单词。
- [[iota-mixing-go]] — 识别同一 const 块内把无关常量与 iota 枚举混写的风险。
- [[noinlineerr-go]] — 检查在 if 语句初始化部分内联声明 err 的写法。
- [[errname-go]] — 检查哨兵错误 Err 前缀和错误类型 Error 后缀命名。
- [[leigh-mcculloch]] — Leigh McCulloch 的项目与角色索引；区分仓库归属与个人作者。
- [[charmbracelet]] — Charmbracelet 的项目与角色索引；区分仓库归属与个人作者。
- [[dario-castane]] — Dario Castañé 的项目与角色索引；区分仓库归属与个人作者。
- [[gaijin-entertainment]] — Gaijin Entertainment 的项目与角色索引；区分仓库归属与个人作者。

- [[nilnil-go]] — 检查同时返回 nil 值和 nil error 的含糊结果。
- [[testifylint-go]] — 检查 testify 测试断言写法，减少含糊或错误的断言。
- [[burntsushi-toml-go]] — 把 TOML 文本解码到 Go 结构体并编码回 TOML。
- [[clickhouse-go-linter-go]] — 检查 ClickHouse 原生 Go API 中 rows.Err 和 batch.Close 遗漏。
- [[go-err113-go]] — 检查错误直接比较与动态新建错误等 Go 1.13 后错误处理风格。
- [[masterminds-semver-v3-go]] — 解析 Semantic Version 并检验版本约束。
- [[unqueryvet-go]] — 检查 SQL 查询中 SELECT * 等不显式选列的写法。
- [[depguard-v2-go]] — 按 allow/deny 规则检查 Go import。
- [[air-go]] — 开发时监听 Go 项目变更并自动重新构建、运行。
- [[chroma-v2-go]] — 以纯 Go lexer 和 formatter 给代码做语法高亮。
- [[go-check-sumtype-go]] — 检查 Go 模拟 sum type 的 switch 分支是否穷尽。
- [[nakedret-v2-go]] — 找出超过长度阈值的函数里的裸 return。
- [[prealloc-go]] — 提示可预分配容量的 slice 构造，减少扩容。
- [[alfatraining-structtag-go]] — 解析和检查 Go 结构体字段 tag。
- [[asasalint-go]] — 找出把 any slice 错误地作为单个 any 传入可变参数函数的情况。
- [[nilnesserr-go]] — 组合 nilness 与 nilerr 检查，找出不一致的 nil/error 返回。
- [[brotli-go]] — 纯 Go Brotli 编码与解码，适合 HTTP 压缩或文件流。
- [[forbidigo-v2-go]] — 按规则禁止特定 Go 标识符或调用，例如调试输出。
- [[makezero-v2-go]] — 检查先创建非零长度 slice 又 append 导致多出零值元素。
- [[godartsass-v2-go]] — 通过 Dart Sass Embedded 协议从 Go 编译 Sass/SCSS。
- [[golibsass-go]] — 从 Go 调用 LibSass 编译 SCSS。
- [[bitset-go]] — 用可扩展位集合存储非负整数的布尔状态。
- [[anton-telyshev]] — Anton Telyshev 的身份及 Go 项目索引。
- [[andrew-gallant]] — Andrew Gallant 的身份及 Go 项目索引。
- [[alec-thomas]] — Alec Thomas 的身份及 Go 项目索引。
- [[bjorn-erik-pedersen]] — Bjørn Erik Pedersen 的身份及 Go 项目索引。
- [[clickhouse]] — ClickHouse 的身份及 Go 项目索引。

- [[cyclop-go]] — 检测 Go 函数和包的圈复杂度。
- [[wsl-v5-go]] — 检查 Go 语句间的空行和分组风格。
- [[bidichk-go]] — 检测源码中可能改变显示顺序的危险双向 Unicode 控制符。
- [[errchkjson-go]] — 检查 JSON 编码的不可支持类型与可省略的错误处理。
- [[ireturn-go]] — 提示函数返回接口类型的设计选择。
- [[mirror-go]] — 提示可避免 string 与 []byte 转换的对应标准库调用。
- [[perfsprint-go]] — 找出可用 strconv 等更直接操作替代的 fmt 格式化调用。
- [[zxcvbn-go]] — 估计密码强度并识别常见词和模式。
- [[durationcheck-go]] — 检查两个 time.Duration 相乘的可疑写法。
- [[colorprofile-go]] — 检测终端色彩能力并自动降级颜色输出。
- [[ultraviolet-go]] — 提供终端 UI 的 cell 绘制、输入和差量渲染原语。
- [[charm-x-ansi-go]] — 解析、生成和清理 ANSI 终端控制序列。
- [[charm-x-term-go]] — 跨平台查询终端大小、TTY 状态及原始模式。
- [[charm-x-termios-go]] — 在 Unix 终端读取或设置 termios 与窗口尺寸。
- [[charm-x-windows-go]] — 封装 Charm 所需的 Windows Console 输入记录与系统调用。
- [[intrange-go]] — 找出可改用 Go 1.22 整数 range 的循环。
- [[displaywidth-go]] — 按 Unicode 字素簇计算等宽终端显示列宽。
- [[uax29-v2-go]] — 按 Unicode UAX #29 分割字素、单词和句子。
- [[bartlomiej-klimczak]] — Bartłomiej Klimczak 的已摄入 Go 项目索引。
- [[simon-sawert]] — Simon Sawert 的已摄入 Go 项目索引。
- [[lucas-bremgartner]] — Lucas Bremgartner 的已摄入 Go 项目索引。
- [[oleg-butuzov]] — Oleg Butuzov 的已摄入 Go 项目索引。
- [[catena-cyber]] — Catena cyber 的已摄入 Go 项目索引。
- [[cosmin-cojocar]] — Cosmin Cojocar 的已摄入 Go 项目索引。
- [[charith-ellawala]] — Charith Ellawala 的已摄入 Go 项目索引。
- [[clifton-kaznocha]] — Clifton Kaznocha 的已摄入 Go 项目索引。
- [[matt-sherman]] — Matt Sherman 的已摄入 Go 项目索引。

- [[curioswitch-go-reassign-go]] — 检查对其他包顶层变量的重新赋值；用法、限制与待验证角色见库页。
- [[dave-dst-go]] — 保留注释和间距地改写 Go 语法树；用法、限制与待验证角色见库页。
- [[denis-tingaikin-go-header-go]] — 检查 Go 源码的版权头；用法、限制与待验证角色见库页。
- [[dlclark-regexp2-go]] — 提供兼容 .NET 特性的回溯式正则引擎；用法、限制与待验证角色见库页。
- [[ettle-strcase-go]] — 转换 snake_case、camelCase 等命名形式；用法、限制与待验证角色见库页。
- [[fatih-color-go]] — 向终端输出 ANSI 颜色文本；用法、限制与待验证角色见库页。
- [[fatih-structtag-go]] — 解析和修改 Go struct 字段标签；用法、限制与待验证角色见库页。
- [[firefart-nonamedreturns-go]] — 检查函数签名中的命名返回值；用法、限制与待验证角色见库页。
- [[fzipp-gocyclo-go]] — 计算 Go 函数的圈复杂度；用法、限制与待验证角色见库页。
- [[ghostiam-protogetter-go]] — 检查 protobuf 嵌套字段的直接访问；用法、限制与待验证角色见库页。
- [[go-critic-go-critic-go]] — 运行可扩展的 Go 代码审查规则；用法、限制与待验证角色见库页。
- [[go-toolsmith-astcast-go]] — 安全地将 AST 节点转换为具体类型；用法、限制与待验证角色见库页。
- [[go-toolsmith-astequal-go]] — 比较 Go AST 结构是否相等；用法、限制与待验证角色见库页。
- [[go-toolsmith-astfmt-go]] — 以 fmt 风格格式化 Go AST 节点；用法、限制与待验证角色见库页。
- [[go-toolsmith-astp-go]] — 测试 AST 节点类型；用法、限制与待验证角色见库页。
- [[go-toolsmith-strparse-go]] — 将短字符串解析为 Go 表达式、语句或声明；用法、限制与待验证角色见库页。
- [[go-toolsmith-typep-go]] — 判断 go/types 类型的性质；用法、限制与待验证角色见库页。
- [[gobwas-glob-go]] — 编译并匹配 glob 模式；用法、限制与待验证角色见库页。
- [[godoc-lint-godoc-lint-go]] — 检查 Go 文档注释规范；用法、限制与待验证角色见库页。
- [[gofrs-flock-go]] — 提供文件锁及非阻塞获取；用法、限制与待验证角色见库页。
- [[gohugoio-hashstructure-go]] — 为 Go 值生成结构哈希；用法、限制与待验证角色见库页。
- [[gohugoio-hugo-go]] — 从内容和模板生成静态网站；用法、限制与待验证角色见库页。
- [[golang-protobuf-go]] — 旧版 Go Protocol Buffers 绑定；用法、限制与待验证角色见库页。
- [[golangci-asciicheck-go]] — 检查 Go 标识符中的非 ASCII 字符；用法、限制与待验证角色见库页。
- [[golangci-canonicalheader-go]] — 检查 HTTP header 名称的规范大小写；用法、限制与待验证角色见库页。
- [[golangci-dupl-go]] — 检测重复的 Go 代码片段；用法、限制与待验证角色见库页。
- [[golangci-go-printf-func-name-go]] — 检查 printf 风格函数名称；用法、限制与待验证角色见库页。
- [[golangci-gofmt-go]] — 将 gofmt 检查集成到 golangci 工具链；用法、限制与待验证角色见库页。
- [[golangci-golines-go]] — 格式化过长的 Go 源码行；用法、限制与待验证角色见库页。
- [[golangci-misspell-go]] — 检查英文拼写错误；用法、限制与待验证角色见库页。
- [[golangci-plugin-module-register-go]] — 提供 golangci 插件模块的注册包；用法、限制与待验证角色见库页。
- [[golangci-revgrep-go]] — 只显示变更行上的静态分析结果；用法、限制与待验证角色见库页。
- [[golangci-rowserrcheck-go]] — 检查 SQL 查询循环后是否读取 Rows.Err；用法、限制与待验证角色见库页。
- [[golangci-swaggoswag-go]] — 供 golangci 集成的 swaggo/swag 维护分支；用法、限制与待验证角色见库页。
- [[golangci-unconvert-go]] — 检查不必要的 Go 类型转换；用法、限制与待验证角色见库页。
- [[google-go-cmp-go]] — 比较 Go 值并给出结构化差异；用法、限制与待验证角色见库页。
- [[gordonklaus-ineffassign-go]] — 检测无效赋值；用法、限制与待验证角色见库页。
- [[gostaticanalysis-analysisutil-go]] — 为 go/analysis 分析器提供辅助函数；用法、限制与待验证角色见库页。
- [[gostaticanalysis-comment-go]] — 为静态分析提供 ast.CommentMap 辅助工具；用法、限制与待验证角色见库页。
- [[gostaticanalysis-forcetypeassert-go]] — 检测未检查的 Go 类型断言；用法、限制与待验证角色见库页。
- [[gostaticanalysis-nilerr-go]] — 检测检查 error 后仍返回 nil 的错误分支；用法、限制与待验证角色见库页。
- [[hashicorp-go-immutable-radix-go]] — 提供泛型不可变 radix tree；用法、限制与待验证角色见库页。
- [[hashicorp-go-version-go]] — 解析和比较语义版本及约束；用法、限制与待验证角色见库页。
- [[hashicorp-golang-lru-go]] — 提供线程安全的泛型 LRU 缓存；用法、限制与待验证角色见库页。
- [[hashicorp-hcl-go]] — 解析和生成结构化配置语言；用法、限制与待验证角色见库页。
- [[go-toolsmith]] — go-toolsmith 官方仓库账号及本库已摄入项目的索引；个人角色待核实。
- [[gostaticanalysis]] — gostaticanalysis 官方仓库账号及本库已摄入项目的索引；个人角色待核实。
- [[golangci]] — golangci 官方仓库账号及本库已摄入项目的索引；个人角色待核实。
- [[hashicorp]] — hashicorp 官方仓库账号及本库已摄入项目的索引；个人角色待核实。
- [[gohugoio]] — gohugoio 官方仓库账号及本库已摄入项目的索引；个人角色待核实。
- [[golang-org]] — golang 官方仓库账号及本库已摄入项目的索引；个人角色待核实。
- [[google-org]] — google 官方仓库账号及本库已摄入项目的索引；个人角色待核实。

## Topics 主题

- [[personal-knowledge-management]] — 个人知识管理：本库正在积累的主题总览（synthesis）。
- [[ai-era-command-line]] — AI 时代的命令行：非技术用户如何搭起本地 AI 工具环境（本轮新开主题 / 连载教程 hub）。
- [[penpot-self-hosting]] — Penpot 2.18 自托管实例的服务拓扑、数据卷与配置注意点。

## Comparisons 对比

- [[llm-wiki-vs-rag]] — 编译式知识 vs. 检索式问答。

## Answers 问答归档

（暂无——有值得留存的查询结果时归档到 `wiki/answers/`）

## Outputs 产物（output/）

- [2026-11-01 Lint 巡检报告](output/2026-11-01-lint.md) — 结构核对、P99 冲突复查、未摄入 raw 候选与验证缺口。

## Library inboxes 第三方库收件箱（raw/）

- [Go 第三方库收件箱](raw/golang-libs-inbox.md) — 每行一个库名；用户要求时再摄入。
- [Rust 第三方库收件箱](raw/rust-libs-inbox.md) — 每行一个库名；用户要求时再摄入。
- [JVM 第三方库收件箱](raw/jvm-libs-inbox.md) — Java / Kotlin 共用；每行一个库名，用户要求时再摄入。

## Backlog 待建页面

- （建议）Engelbart《Augmenting Human Intellect》(1962)：memex → 人机协同的直接后续
- （建议）超文本谱系：Nelson/Xanadu、H.G. Wells《World Brain》(1938)
- （建议）「预测 vs 实现」对照页：memex 的技术预言哪些成真
- （建议）Python / 解释器：「为什么 AI 都爱写 Python」——[[ai-era-command-line]] 系列预告篇（尚未剪藏）
- （建议）Windows Terminal 美化配置：`settings.json`、字体与配色方案（可作 `output/` 产物）
- （待验证）Penpot 实例的登录、文件创建、导出与 MCP 连接；以及其公网暴露、密钥和备份状态
- Obsidian Web Clipper 剪藏流程（方法页）
- Marp 幻灯片 / Dataview 查询用法（工具用法页）
- 搜索方案：qmd 集成评估（wiki 规模增长后再做）
- （评估）raw/ 子目录化（articles / papers）——待来源规模增长后再议（output/ 落盘已于 2026-10-01 采纳，见 schema v1.3）
- （待验证）chi 的当前维护者名单及各自角色；仅凭仓库归属不能推断。
- （待验证）google/uuid 的创始作者与当前维护者名单；Paul Borman 的具体角色已按官方证据限定。
- （待验证）pgx 的完整当前维护者名单，以及用户项目版本与 v5.12.0 安全修复的相关性。
- （待验证）koanf TOML parser v2 子模块的独立作者及完整当前维护者名单。
- （待验证）koanf file provider 子模块的具体创建者及完整当前维护者名单；监听回调事件行为按目标版本核对。
- （待验证）本批次剩余 Go 模块的个人创建者及当前维护者；Prometheus、etcd、Go x 包按项目归属记录，不能视为个人作者。
- （待验证）本轮新增 Go 库中，仅能核实组织或仓库账号的项目，其个人创建者和当前维护者；作者索引区分账号关联与个人贡献。
- （待验证）对 P99 单实例原始示例产出可编译修正版并实测；多实例场景按目标流量、窗口与精度要求验证 Histogram 或 t-digest 方案。
- （待验证）微信在指定平台与版本的聊天记录存储实现；现有 [[sqlite-2018-dialect-clipping]] 正文没有相关证据。
- （待补）Emotional Control 与团队心理安全、晋升结果之间的实证研究；现有 [[emotional-control-leadership-clipping]] 为个人观点。

- `github.com/daixiang0/gci`：个人创建者与当前维护者待验证；不得仅由仓库所属账号推断。
- `github.com/golangci/golangci-lint/v2`：个人创建者与当前维护者待验证；不得仅由仓库所属账号推断。
- `github.com/magefile/mage`：个人创建者与当前维护者待验证；不得仅由仓库所属账号推断。
- `mvdan.cc/gofumpt`：个人创建者与当前维护者待验证；不得仅由仓库所属账号推断。
- `codeberg.org/chavacava/garif`：个人创建者与当前维护者待验证；不得仅由仓库所属账号推断。
- `codeberg.org/polyfloyd/go-errorlint`：个人创建者与当前维护者待验证；不得仅由仓库所属账号推断。
- `github.com/4meepo/tagalign`：个人创建者与当前维护者待验证；不得仅由仓库所属账号推断。
- `github.com/Abirdcfly/dupword`：个人创建者与当前维护者待验证；不得仅由仓库所属账号推断。
- `github.com/AdminBenni/iota-mixing`：个人创建者与当前维护者待验证；不得仅由仓库所属账号推断。
- `github.com/AlwxSin/noinlineerr`：个人创建者与当前维护者待验证；不得仅由仓库所属账号推断。
- `github.com/Antonboom/errname`：个人创建者与当前维护者待验证；不得仅由仓库所属账号推断。

- `github.com/Djarvur/go-err113`：个人创建者及当前维护者待验证。
- `github.com/Masterminds/semver/v3`：个人创建者及当前维护者待验证。
- `github.com/MirrexOne/unqueryvet`：个人创建者及当前维护者待验证。
- `github.com/OpenPeeDeeP/depguard/v2`：个人创建者及当前维护者待验证。
- `github.com/air-verse/air`：个人创建者及当前维护者待验证。
- `github.com/alexkohler/nakedret/v2`：个人创建者及当前维护者待验证。
- `github.com/alexkohler/prealloc`：个人创建者及当前维护者待验证。
- `github.com/alfatraining/structtag`：个人创建者及当前维护者待验证。
- `github.com/alingse/asasalint`：个人创建者及当前维护者待验证。
- `github.com/alingse/nilnesserr`：个人创建者及当前维护者待验证。
- `github.com/andybalholm/brotli`：个人创建者及当前维护者待验证。
- `github.com/ashanbrown/forbidigo/v2`：个人创建者及当前维护者待验证。
- `github.com/ashanbrown/makezero/v2`：个人创建者及当前维护者待验证。
- `github.com/bits-and-blooms/bitset`：个人创建者及当前维护者待验证。
- （待验证）本批 18 个 Go 项目的个人创建与当前维护角色；已建身份页仅确认官方账号关联，不能据仓库所属推定唯一作者。
- （待验证）`github.com/charmbracelet/x/windows` 的目标 Windows 版本与独立最小运行示例；Charm x 子模块的 API 稳定性按实际版本复核。

- （待验证）本批 45 个 Go 项目的个人创建者和现任维护者；仓库账号页只确认归属，不推断个人角色。
- （待验证）[[golangci-plugin-module-register-go]]、[[golangci-swaggoswag-go]]、[[gostaticanalysis-analysisutil-go]] 与 [[gostaticanalysis-comment-go]] 的独立最小 API 示例。
- （待验证）本批 CLI 及 Go 示例在目标版本的实际编译和运行；尤其核对 golangci-lint v2 参数与 fork 模块路径。

## Stats

- 来源：**157** 份 ｜ wiki 页面：**377** ｜ Outputs：**1** ｜ 最近更新：2026-11-01
