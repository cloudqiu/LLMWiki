---
title: "github.com/dlclark/regexp2/v2"
type: entity
entity_type: tool
created: 2026-11-01
updated: 2026-11-01
tags: [go, library]
status: growing
sources: [raw/dlclark-regexp2-go-official-research-2026-11-01.md]
---

# github.com/dlclark/regexp2/v2

## 用途与适用场景

提供兼容 .NET 特性的回溯式正则引擎。（[[dlclark-regexp2-go-official-research]]）

## 依赖与版本

- Go 模块：`github.com/dlclark/regexp2/v2`；在项目中执行 `go get github.com/dlclark/regexp2/v2`。
- 官方资料查阅日期：2026-11-01；具体版本由项目锁定。

## 作者与维护者

- 作者待验证；仓库归属账号不等于已核实的个人创建者。
- 具体创建者与当前维护者待验证。

## 典型用法

以下是对照官方仓库资料整理的最小片段，**尚未在本机运行**。Go 片段需要补齐 import、变量或外围函数。

```go
re, err := regexp2.Compile(`a+`, 0); _ = re; _ = err
```

## 关键限制

- 回溯匹配不保证 regexp 包的线性时间；v2 最低 Go 版本需核对。

## 来源

- [[dlclark-regexp2-go-official-research]]；[官方仓库](https://github.com/dlclark/regexp2)；[所查 README 或仓库说明](https://raw.githubusercontent.com/dlclark/regexp2/master/README.md)。
- 本地查阅记录：`raw/dlclark-regexp2-go-official-research-2026-11-01.md`。
