# github.com/beorn7/perks 官方资料查阅记录

> 2026-10-31 查阅。本文是 Codex 对官方页面的研究笔记，并非官方原文副本。收件箱原文保留不动；API 示例未在本机运行。

## 1. 模块与用途

- 收件箱条目：`github.com/beorn7/perks`。
- 官方模块 / import：`github.com/beorn7/perks`；示例导入 `github.com/beorn7/perks/quantile`。
- 用途：提供流式近似分位数 quantile 等 Go 工具包。
- Go Packages：[模块页面](https://pkg.go.dev/github.com/beorn7/perks)；[示例包页面](https://pkg.go.dev/github.com/beorn7/perks/quantile)。查阅日期：2026-10-31。具体版本以项目 go.mod 锁定；本地未下载依赖，未核对用户项目版本。

## 2. 典型 API

官方包文档显示如下调用方式；示例为教学片段，所需 import 和外部对象需按项目补齐，未运行：

```go
q := quantile.NewTargeted(map[float64]float64{0.9: 0.01})
for _, v := range []float64{1,2,3,4,5} { q.Insert(v) }
fmt.Println(q.Query(0.9))
```

## 3. 作者与关联项目

- 官方仓库：https://github.com/beorn7/perks。
- 角色判断：原始 README 版权署名 Blake Mizerany；beorn7 的个人身份与当前维护角色待验证。
- 同一账号或组织的其他可查项目：暂无已核实的同账号其他独立库。仓库归属不自动证明个人独立创作，清单也不代表全部作品。

## 4. 选用边界与待验证

- 根模块不是 quantile 包；Stream 文档称非线程安全。原始 README 版权署名 Blake Mizerany，当前 beorn7 仓库维护角色待验证。
- 需在目标 Go 版本、操作系统和用户项目中编译运行；本轮无法从本机直接获取模块。

## 5. 个人身份核对

- [beorn7 账号](https://github.com/beorn7)显示 Björn Rabenstein；[bmizerany 账号](https://github.com/bmizerany)及原始 perks 仓库、当前 README 版权署名显示 Blake Mizerany。两人角色应区分，当前维护分工待验证。
