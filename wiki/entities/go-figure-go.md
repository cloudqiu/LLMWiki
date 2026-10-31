---
title: "github.com/common-nighthawk/go-figure"
type: entity
entity_type: tool
created: 2026-10-31
updated: 2026-10-31
tags: [go, library]
status: growing
sources: [raw/go-figure-go-official-research-2026-10-31.md]
---

# github.com/common-nighthawk/go-figure

## 用途与适用场景

把文本渲染为终端 ASCII 字画。（[[go-figure-go-official-research]]）

## 依赖与版本

- Go 模块项目执行 `go get github.com/common-nighthawk/go-figure`；示例使用 `github.com/common-nighthawk/go-figure`。
- 查阅日期：2026-10-31。具体版本由项目 `go.mod` 锁定；本机未下载或编译。模块根路径与实际 import 不同时，以示例子包为准。

## 作者与维护者

- 作者索引：[[daniel-deutsch]]。
- 仓库账号 common-nighthawk；个人姓名与其他库待验证。
- 其他相关项目：暂无可可靠核实的其他库。。这些项目尚未摄入；作者/组织关系详见可用的作者页或原始查阅记录。

## 典型用法

以下是按官方包文档整理的最小核心片段；需要补齐相应 import、外部对象或运行环境，**尚未实际运行**。

```go
fig := figure.NewFigure("Hello", "standard", true)
fig.Print()
```

## 关键限制

- 字体名和空格支持有边界；项目 TODO 明示更完整空格支持未完成。

## 来源

- [[go-figure-go-official-research]]
- [官方仓库](https://github.com/common-nighthawk/go-figure)；[Go Packages](https://pkg.go.dev/github.com/common-nighthawk/go-figure)；[示例 API](https://pkg.go.dev/github.com/common-nighthawk/go-figure)。
- 本地查阅记录：`raw/go-figure-go-official-research-2026-10-31.md`。
