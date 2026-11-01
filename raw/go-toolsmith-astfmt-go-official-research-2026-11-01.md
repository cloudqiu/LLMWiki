# github.com/go-toolsmith/astfmt 官方资料查阅记录

> 2026-11-01 查阅。本文是 Codex 的中文研究笔记，不是官方原文副本；代码片段尚未在本机运行。

## 官方来源

- 收件箱原条目：`github.com/go-toolsmith/astformat`；官方项目实际为 `github.com/go-toolsmith/astfmt`，原文未修改。
- [项目仓库](https://github.com/go-toolsmith/astfmt)；[所查 README 或仓库说明](https://github.com/go-toolsmith/astfmt)。
- [Go Packages 入口](https://pkg.go.dev/github.com/go-toolsmith/astfmt)（具体 API 以目标版本为准）。
- 仓库归属账号：`go-toolsmith`；归属不等于个人创建者或现任维护者。

## 核心事实与用法

- 用途：以 fmt 风格格式化 Go AST 节点。
- 模块依赖：`go get github.com/go-toolsmith/astfmt`。
- 官方 README 的最小用法：

```go
astfmt.Println(strparse.Expr(`x+1`))
```

## 边界

- 示例还需导入 `github.com/go-toolsmith/strparse`。
- 示例未在本机编译或运行；若为命令行工具，执行前核对目标版本的命令与参数。
- 创建者与现任维护者的具体身份待验证；不由仓库所有者直接推断。
