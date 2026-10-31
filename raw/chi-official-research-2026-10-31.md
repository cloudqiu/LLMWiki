# chi v5 官方资料查阅记录（2026-10-31）

本文件是 Codex 根据下列官方页面整理的定位笔记，**不是官方网页原文快照**。本机网络代理阻止了直接下载；引用与事实请回到链接所指页面核对。收件箱条目 `github.com/go-chi/chi/v5` 只用于指定待查库。

## 1. Go Packages：chi v5.5.0

- 页面：https://pkg.go.dev/github.com/go-chi/chi/v5
- 查阅日期：2026-10-31。页面显示版本 v5.5.0，发布于 2026-10-14；本文只对该查阅版本作 API 说明，不断言它是最新版本。
- 「README / Install」「Features」「Examples」：模块路径 `github.com/go-chi/chi/v5`；`go get github.com/go-chi/chi/v5`；轻量、可组合，兼容标准库 `net/http` 的 handler 和 middleware；核心无外部依赖。示例使用 `chi.NewRouter()`、`r.Get()`、`r.Use()`。
- 「Documentation / Overview」「URL patterns」：`{name}` 参数通过 `chi.URLParam(r, "name")` 获取；路由路径须以 `/` 开始，尾部 `/` 要明确处理。文档称支持最近四个 Go 主版本；不在此转换为固定 Go 最低版本。
- 「README / Middlewares / Choosing a ClientIP middleware」：旧 `middleware.RealIP` 已标废弃，因 IP 欺骗风险；应按代理架构选择 `ClientIPFrom*` 系列。该条只作为选型提醒。
- 「README / License」：版权行署名 Peter Kieltyka（2015-present）。

## 2. 官方 GitHub 项目与作者

- chi 仓库及 README：https://github.com/go-chi/chi 。「License」同样署名 Peter Kieltyka；仓库位于 `go-chi` 组织下，不能单凭组织归属推断实际维护者。README「Extra middlewares & packages」列出组织的相关包，这些包不自动归于 Peter 个人。
- Peter Kieltyka 的 GitHub 主页：https://github.com/pkieltyka 。该账号将 `go-chi/chi`、`webrpc/webrpc` 和 `pkieltyka/go-llm` 列为 pinned repositories；pinned 只证明其主动展示，不单独证明作者身份。
- Peter 的 GitHub Sponsors 自述：https://github.com/sponsors/pkieltyka 。自称 `go-chi` 和 `webrpc` 的 author，可用于确认其作者角色。
- webrpc 官方 README：https://github.com/webrpc/webrpc ，「Authors」明确列 Peter Kieltyka、José Carlos Nieto、Vojtech Vitek；因此将 Peter 记为**共同作者**，不记为唯一作者。此项目尚未摄入。
- go-llm 官方仓库：https://github.com/pkieltyka/go-llm ，项目位于 Peter 个人账号下且由本人置顶；记作其账号下的其他 Go 库，不凭此断言其独立创作或当前维护状态。此项目尚未摄入。

## 3. 尚待核实

- chi 当前维护者的明确名单及各自角色：查过 README、项目主页、作者主页，未见可据以确认名单的官方声明。Peter 的作者身份明确，不能仅据作者或仓库归属推断他是唯一的当前维护者。
- 本笔记未验证用户本地的 chi 版本，也未运行示例。
