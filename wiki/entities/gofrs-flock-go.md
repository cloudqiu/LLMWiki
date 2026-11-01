---
title: "github.com/gofrs/flock"
type: entity
entity_type: tool
created: 2026-11-01
updated: 2026-11-01
tags: [go, library]
status: growing
sources: [raw/gofrs-flock-go-official-research-2026-11-01.md]
---

# github.com/gofrs/flock

## 用途与适用场景

提供文件锁及非阻塞获取。（[[gofrs-flock-go-official-research]]）

## 依赖与版本

- Go 模块：`github.com/gofrs/flock`；在项目中执行 `go get github.com/gofrs/flock`。
- 官方资料查阅日期：2026-11-01；具体版本由项目锁定。

## 作者与维护者

- 作者待验证；仓库归属账号不等于已核实的个人创建者。
- 具体创建者与当前维护者待验证。

## 典型用法

以下是对照官方仓库资料整理的最小片段，**尚未在本机运行**。Go 片段需要补齐 import、变量或外围函数。

```go
lock := flock.New("/tmp/app.lock"); ok, err := lock.TryLock(); _, _ = ok, err
```

## 关键限制

- 锁路径和文件系统语义因平台而异；成功后须 Unlock。

## 来源

- [[gofrs-flock-go-official-research]]；[官方仓库](https://github.com/gofrs/flock)；[所查 README 或仓库说明](https://raw.githubusercontent.com/gofrs/flock/master/README.md)。
- 本地查阅记录：`raw/gofrs-flock-go-official-research-2026-11-01.md`。
