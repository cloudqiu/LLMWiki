---
title: "github.com/beorn7/perks"
type: entity
entity_type: tool
created: 2026-10-31
updated: 2026-11-01
tags: [go, library]
status: growing
sources: [raw/perks-go-official-research-2026-10-31.md, raw/单实例模拟P99.md, raw/多实例P99例子.md]
---

# github.com/beorn7/perks

## 用途与适用场景

提供流式近似分位数 quantile 等 Go 工具包。（[[perks-go-official-research]]）

## 依赖与版本

- Go 模块项目执行 `go get github.com/beorn7/perks`；示例使用 `github.com/beorn7/perks/quantile`。
- 查阅日期：2026-10-31。具体版本由项目 `go.mod` 锁定；本机未下载或编译。模块根路径与实际 import 不同时，以示例子包为准。

## 作者与维护者

- 作者索引：[[blake-mizerany]]（原始版权）、[[bjorn-rabenstein]]（当前仓库账号）。
- 原始 README 版权署名 Blake Mizerany；beorn7 的个人身份与当前维护角色待验证。
- 其他相关项目：暂无已核实的同账号其他独立库。这些项目尚未摄入；作者/组织关系详见可用的作者页或原始查阅记录。

## 典型用法

以下是按官方包文档整理的最小核心片段；需要补齐相应 import、外部对象或运行环境，**尚未实际运行**。

```go
q := quantile.NewTargeted(map[float64]float64{0.9: 0.01})
for _, v := range []float64{1,2,3,4,5} { q.Insert(v) }
fmt.Println(q.Query(0.9))
```

## 关键限制

- 根模块不是 quantile 包；Stream 文档称非线程安全。原始 README 版权署名 Blake Mizerany，当前 beorn7 仓库维护角色待验证。
- `Stream.Count()` 返回已观察样本数；`NewTargeted` 的 epsilon 限制分位位置的绝对误差，不是延迟值的百分比。并发 `Insert`/`Query`/`Count` 需同步。（[[single-instance-p99-simulation]]）

> [!warning] 原始多实例示例与官方文档矛盾
> `raw/多实例P99例子.md` 第 5–7、78–103、183–189、254–271、312–319 行把 `Stream.Merge` 当作少量实例可用的全局 P99 方案；[官方包文档](https://pkg.go.dev/github.com/beorn7/perks/quantile)明确标注该方法损坏且不产生正确结果。不要用于跨实例分位数聚合；详见 [[distributed-quantiles]]。

## 来源

- [[perks-go-official-research]]
- [官方仓库](https://github.com/beorn7/perks)；[Go Packages](https://pkg.go.dev/github.com/beorn7/perks)；[示例 API](https://pkg.go.dev/github.com/beorn7/perks/quantile)。
- 本地查阅记录：`raw/perks-go-official-research-2026-10-31.md`。
- 新摄入材料：`raw/单实例模拟P99.md`、`raw/多实例P99例子.md`；[[single-instance-p99-simulation]]、[[multi-instance-p99-examples]]。
