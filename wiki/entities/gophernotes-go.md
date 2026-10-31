---
title: "gophernotes (Go)"
type: entity
entity_type: tool
created: 2026-10-31
updated: 2026-10-31
tags: [go, jupyter, gophernotes]
status: growing
sources: [raw/gophernotes-official-research-2026-10-31.md, raw/gophernotes-usage.md]
---

# gophernotes

## 用途与适用场景

gophernotes 是 Jupyter Notebook / nteract 的 Go kernel，用 `gomacro` 交互执行 Go。适合在 notebook 中讲解语言概念、试算数据、记录探索过程并分享带代码的文档；它不是普通 Go 项目的依赖包。（[[gophernotes-official-research]]；官方 README）

## 依赖与版本

- 生态：Go + Jupyter Notebook / nteract。
- 官方 README 的安装示例使用 `gophernotes@v0.7.5`；用户本地版本与安装方式待验证。
- 用户已报告本地启动成功，故此处不重复安装步骤。启动 Jupyter 后选择 **Go** kernel。（官方 README「Getting Started」）

## 典型用法

### 1. 运行 Go 代码单元

在 Go kernel 的代码单元粘贴，按 `Shift+Enter`。不需要写 `package main` 或 `func main()`。示例预期输出前十个 Fibonacci 数；尚未在用户本地 notebook 验证。（`raw/gophernotes-usage.md`「运行 Go 代码」）

```go
import "fmt"

a, b := 0, 1
for i := 0; i < 10; i++ {
    fmt.Print(a, " ")
    a, b = b, a+b
}
```

### 2. 查看 kernel 自带帮助

在单独的代码单元运行以下特殊命令，查看当前环境支持的命令；尚未在用户本地验证。（官方 README「Special commands」）

```text
%help
```

## 补全与关键限制

- 执行 `import "fmt"` 后，在新单元输入 `fmt.Pr` 并按 `Tab` 可测试补全。kernel 实现了 completion handler；键入时是否自动弹出候选与 Jupyter 前端有关，用户环境表现待验证。（官方 `complete.go`；`raw/gophernotes-usage.md`「补全」）
- 官方 README 指出：原生 Windows 下不能导入第三方包；需要此功能可在 Docker 中运行。解释执行还有其他边界，详见官方 README「Limitations」。

## 来源

- [[gophernotes-official-research]]：官方 README 与源码的本地查阅记录。
- [官方仓库及 README](https://github.com/gopherdata/gophernotes)
- [补全实现](https://github.com/gopherdata/gophernotes/blob/master/complete.go)
- 本地资料：`raw/gophernotes-official-research-2026-10-31.md`、`raw/gophernotes-usage.md`
