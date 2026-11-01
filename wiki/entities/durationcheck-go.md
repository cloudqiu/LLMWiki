---
title: "github.com/charithe/durationcheck"
type: entity
entity_type: tool
created: 2026-11-01
updated: 2026-11-01
tags: [go, library]
status: growing
sources: [raw/durationcheck-go-official-research-2026-11-01.md]
---

# github.com/charithe/durationcheck

## 用途与适用场景

检查两个 time.Duration 相乘的可疑写法。（[[durationcheck-go-official-research]]）

## 依赖与版本

- 模块：`github.com/charithe/durationcheck`；安装或依赖声明：`go get github.com/charithe/durationcheck/cmd/durationcheck`。
- 查阅日期：2026-11-01；实际使用版本由项目锁定。

## 作者与维护者

- [[charith-ellawala]]：官方主页证实 Charith Ellawala 与账号关联；具体独立创建和现任维护角色待验证。

## 典型用法

以下是按官方资料整理的核心片段，**尚未在本机运行**。命令需在 Go 项目中执行；Go 代码需补齐 import、变量和外围函数。

```text
durationcheck ./...
```

## 关键限制

- 规则针对可疑乘法，不能覆盖所有时间单位错误。

## 来源

- [[durationcheck-go-official-research]]；[官方仓库](https://github.com/charithe/durationcheck)；[官方文档](https://github.com/charithe/durationcheck)。
- 本地查阅记录：`raw/durationcheck-go-official-research-2026-11-01.md`。
