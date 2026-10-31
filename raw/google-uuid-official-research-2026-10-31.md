# google/uuid 官方资料查阅记录（2026-10-31）

本文件是 Codex 阅读官方页面后的定位笔记，**不是官方原文快照**。本机网络代理阻止了直接下载；事实请回到链接所指的官方页面核对。收件箱条目仅用于确定待查库。

## 1. 项目及版本

- 官方仓库与 README：https://github.com/google/uuid 。README「uuid」「Install」：用于生成和检查 UUID，安装命令 `go get github.com/google/uuid`；项目说明它基于先前的 `github.com/pborman/uuid`，两者的 UUID 类型不同：此库为 16 字节数组，上游旧库为字节切片。
- Go Packages：https://pkg.go.dev/github.com/google/uuid 。2026-10-31 查阅时页面显示 v1.6.0（发布于 2024-01-23）；API 描述以这一显示版本为准，不断言它是最新版本。
- 「Documentation / Overview」：`UUID` 是 `[16]byte`，可作为 map key 或直接比较。
- 「NewString」「NewRandom」：`NewString()` 生成随机 v4 UUID 字符串，但随机数源失败时会 panic；需要显式处理错误时用 `NewRandom()`，其返回 `(UUID, error)`。
- 「Parse」「Validate」：`Parse` 返回 `(UUID, error)`，接受标准形式，也接受无连字符的十六进制字符串和带花括号的形式；官方明确说不要将 `Parse` 用作只接受标准形式的校验。`Validate` 同样允许文档列出的多种格式。
- 「EnableRandPool」：可提升 v4 生成吞吐，但随机池放在 Go heap，不适合某些安全敏感场景；启用和关闭操作不是线程安全的，只应在没有并发生成时调用。

## 2. 作者、贡献者与关联库

- 官方 `CONTRIBUTORS`：https://github.com/google/uuid/blob/master/CONTRIBUTORS ，首列 `Paul Borman`，另列其他贡献者；文件并未指定唯一作者或当前维护者。
- 官方 LICENSE：https://github.com/google/uuid/blob/master/LICENSE 与 `uuid.go` 源码版权行注明 Google Inc.；版权持有人和 GitHub 组织归属不能直接等同于具体作者或维护者。
- 官方 releases：https://github.com/google/uuid/releases ，历史 v1.1–v1.3 等版本由 GitHub 账号 `pborman` 发布；2024 年 v1.6.0 使用 `release-please` 发布。由此只能确认历史发布参与，不能推断目前由谁维护。
- 先前版本：https://github.com/pborman/uuid ，该仓库 README 确认 `google/uuid` 基于先前版本；两者是不同的库，不能把上游库直接登记为本次已摄入。
- `pborman` 的 GitHub 主页：https://github.com/pborman ，列有 `pborman/uuid`、`pborman/getopt` 等库。`getopt` 官方仓库 https://github.com/pborman/getopt 的 README 称其为 Go 命令行选项解析库。仓库归属仅证明其账号下的项目，不证明独立创作。

## 3. 待验证

- `google/uuid` 的明确创始作者及当前维护者名单；Paul Borman 是官方列名的贡献者及历史发布参与者，不能据此断言他是该仓库唯一作者或当前维护者。
- 用户项目中使用的版本；下列 wiki 示例未在本机运行。
