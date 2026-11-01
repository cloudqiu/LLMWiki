---
title: "github.com/mattn/go-isatty"
type: entity
entity_type: tool
created: 2026-11-01
updated: 2026-11-01
tags: [go, library]
status: growing
sources: [raw/go-isatty-go-official-research-2026-11-01.md]
---

# github.com/mattn/go-isatty

## 用途与适用场景

检测文件描述符是否连接终端，用于决定颜色、交互提示等输出。（[[go-isatty-go-official-research]]）

## 依赖与版本

- Go 模块执行 `go get github.com/mattn/go-isatty`；示例使用 `github.com/mattn/go-isatty`。
- 查阅日期：2026-11-01；目标版本以项目 `go.mod` 为准。若模块根路径与示例 import 不同，使用上述子包路径。

## 作者与维护者

- [[yasuhiro-matsumoto]]：README 明列 Yasuhiro Matsumoto 为作者。
- 完整当前维护者名单待验证；不把仓库归属写成唯一作者。

## 典型用法

按官方包文档或 README 摘录；以下是教学片段，需补齐 import、上下文和运行条件，**尚未实际运行**。

```go
terminal := isatty.IsTerminal(os.Stdout.Fd())
fmt.Println(terminal)
```

## 关键限制

- 检测的是给定文件描述符；Cygwin/MSYS2 终端有单独的 IsCygwinTerminal 路径。

## 来源

- [[go-isatty-go-official-research]]；本地查阅记录：`raw/go-isatty-go-official-research-2026-11-01.md`。
- [官方仓库](https://github.com/mattn/go-isatty)；[Go Packages](https://pkg.go.dev/github.com/mattn/go-isatty)。
