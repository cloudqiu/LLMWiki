---
title: "github.com/alecthomas/chroma/v2"
type: entity
entity_type: tool
created: 2026-11-01
updated: 2026-11-01
tags: [go, library]
status: growing
sources: [raw/chroma-v2-go-official-research-2026-11-01.md]
---

# github.com/alecthomas/chroma/v2

## 用途与适用场景

以纯 Go lexer 和 formatter 给代码做语法高亮。（[[chroma-v2-go-official-research]]）

## 依赖与版本

- 模块：`github.com/alecthomas/chroma/v2`；安装或依赖声明：`go get github.com/alecthomas/chroma/v2`。
- 查阅日期：2026-11-01。具体版本由目标项目锁定。

## 作者与维护者

- [[alec-thomas]]：官方个人或组织账号关联此仓库；具体创建与当前维护角色待验证。

## 典型用法

以下是按官方资料整理的最小片段，**尚未在本机运行**。Go 片段需要相应 import、变量和外围函数；文字步骤须按目标项目配置执行。

```go
err := quick.Highlight(os.Stdout, "package main", "go", "html", "monokai"); _ = err
```

## 关键限制

- 找不到 lexer、formatter 或 style 时可能返回 nil；应有回退处理。

## 来源

- [[chroma-v2-go-official-research]]；[官方资料](https://pkg.go.dev/github.com/alecthomas/chroma/v2)；[Go Packages](https://pkg.go.dev/github.com/alecthomas/chroma/v2)。
- 本地研究笔记：`raw/chroma-v2-go-official-research-2026-11-01.md`。
