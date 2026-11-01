---
title: "github.com/prometheus/procfs"
type: entity
entity_type: tool
created: 2026-11-01
updated: 2026-11-01
tags: [go, library]
status: growing
sources: [raw/prometheus-procfs-go-official-research-2026-11-01.md]
---

# github.com/prometheus/procfs

## 用途与适用场景

读取 Linux /proc 的进程和内核统计数据。（[[prometheus-procfs-go-official-research]]）

## 依赖与版本

- Go 模块执行 `go get github.com/prometheus/procfs`；示例使用 `github.com/prometheus/procfs`。
- 查阅日期：2026-11-01；目标版本以项目 `go.mod` 为准。若模块根路径与示例 import 不同，使用上述子包路径。

## 作者与维护者

- [[prometheus-project]]：Prometheus 项目组织仓库；个人创建者及维护者名单待验证。
- 完整当前维护者名单待验证；不把仓库归属写成唯一作者。

## 典型用法

按官方包文档或 README 摘录；以下是教学片段，需补齐 import、上下文和运行条件，**尚未实际运行**。

```go
fs, err := procfs.NewDefaultFS()
if err != nil { panic(err) }
stat, err := fs.Stat()
if err != nil { panic(err) }
fmt.Println(stat)
```

## 关键限制

- 依赖可用的 Linux procfs；Windows 上不能据此获取本机 /proc 数据。部分旧 New* API 已弃用。

## 来源

- [[prometheus-procfs-go-official-research]]；本地查阅记录：`raw/prometheus-procfs-go-official-research-2026-11-01.md`。
- [官方仓库](https://github.com/prometheus/procfs)；[Go Packages](https://pkg.go.dev/github.com/prometheus/procfs)。
