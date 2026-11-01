# codeberg.org/chavacava/garif 官方资料查阅记录

> 2026-11-01 查阅。本文为 Codex 研究笔记，不是官方原文副本。收件箱未改动；示例未在本机运行。

## 模块与用途

- 收件箱：`codeberg.org/chavacava/garif`。
- 官方模块：`codeberg.org/chavacava/garif`。
- 用途：构造、修改并输出 SARIF 2.1.0 静态分析结果日志。
- [官方项目或文档](https://pkg.go.dev/codeberg.org/chavacava/garif)；[Go Packages](https://pkg.go.dev/codeberg.org/chavacava/garif)。

## 安装与典型用法

```go
go get codeberg.org/chavacava/garif
```

```go
rule := garif.NewRule("example")
driver := garif.NewDriver("my-analyzer").WithRules(rule)
_ = driver
```

## 身份与边界

- 身份：Codeberg 账号 chavacava；个人身份与当前维护者待验证。
- 限制：Go Packages 的 README 示例仍写旧 GitHub import；实际依赖应使用 Codeberg 模块路径，具体迁移兼容性待验证。
- 具体版本由目标项目锁定，未下载、编译或运行；以上为 2026-11-01 的资料状态。
