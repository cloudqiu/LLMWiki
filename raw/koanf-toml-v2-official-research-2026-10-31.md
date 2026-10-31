# koanf TOML parser v2 官方资料查阅记录（2026-10-31）

本文件是 Codex 根据官方页面整理的定位笔记，**不是官方原文快照**。本机网络代理阻止直接下载；事实请回到所列链接核对。收件箱条目只用于确定待查模块。

## 1. 模块与 API

- Go Packages：https://pkg.go.dev/github.com/knadh/koanf/parsers/toml/v2 。2026-10-31 查阅时页面显示 v2.2.2，发布于 2026-08-04；不据此断言以后仍为最新版。
- 「Overview」「Parser」「Unmarshal」「Marshal」：此包实现 `koanf.Parser`，把 TOML 字节解析为 `map[string]any`，也可将配置 map 序列化为 TOML 字节。入口是 `toml.Parser()`；本包本身不是配置来源 provider，也不是 koanf 核心对象。
- 对应 tag 的官方源码：https://github.com/knadh/koanf/blob/parsers/toml/v2.2.2/parsers/toml/toml.go 。源码导入 `github.com/pelletier/go-toml/v2` 作为 TOML 编解码器。`Unmarshal` 在结果 map 为空时返回 `(nil, nil)`；`Marshal` 在输入 map 为空时返回 `(nil, nil)`。此处是 v2.2.2 源码行为。
- koanf 官方 README：https://github.com/knadh/koanf 。「Installation」和「List of installable Providers and Parsers」将核心 `github.com/knadh/koanf/v2`、TOML parser `github.com/knadh/koanf/parsers/toml/v2` 与各 provider 列为分别安装的模块；表格标明此 parser 使用 go-toml v2。README「Concepts」「Reading config from files」展示 `k.Load(file.Provider(...), parser.Parser())`、`koanf.New(".")` 与按分隔键读取配置的组合方式。

## 2. 作者与其他项目

- koanf 官方 LICENSE：https://github.com/knadh/koanf/blob/master/LICENSE ，版权行署名 Kailash Nadh（2019），并链接 `knadh` 账号。
- 本人 GitHub 主页：https://github.com/knadh ，显示姓名 Kailash Nadh；将 koanf 与 listmonk 等项目置顶。2026 年 10 月的 koanf 官方 releases：https://github.com/knadh/koanf/releases ，由 `knadh` 账号发布，支持其近期维护参与；不代表其为唯一维护者，也不确认 parser 子模块每一行的个人作者。
- 同账号下其他 Go 库：[goyesql](https://github.com/knadh/goyesql)（读取含命名查询的 SQL 文件）、[stuffbin](https://github.com/knadh/stuffbin)（将静态资源压缩嵌入 Go 程序）。仓库归属可作为项目线索，不能单独证明独立创作。两者尚未摄入。
- `koanf/v2`、`providers/rawbytes` 和 `maps` 也是 koanf 相关模块；收件箱已有对应名称或近似名称，摄入前需分别核实路径拼写和版本。

## 3. 待验证

- parser 子模块的独立作者、完整当前维护者名单；目前可确定的是 koanf 项目的版权署名与 `knadh` 近期发布参与。
- 用户项目的依赖版本；wiki 示例未在本机运行。
