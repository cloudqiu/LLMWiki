---
title: "github.com/OpenPeeDeeP/depguard/v2"
type: entity
entity_type: tool
created: 2026-11-01
updated: 2026-11-01
tags: [go, library]
status: growing
sources: [raw/depguard-v2-go-official-research-2026-11-01.md]
---

# github.com/OpenPeeDeeP/depguard/v2

## 用途与适用场景

按 allow/deny 规则检查 Go import。（[[depguard-v2-go-official-research]]）

## 依赖与版本

- 模块：`github.com/OpenPeeDeeP/depguard/v2`；安装或依赖声明：`go get github.com/OpenPeeDeeP/depguard/v2`。
- 查阅日期：2026-11-01。具体版本由目标项目锁定。

## 作者与维护者

- 仓库账号 OpenPeeDeeP；个人创建者和当前维护者待验证。

## 典型用法

以下是按官方资料整理的最小片段，**尚未在本机运行**。Go 片段需要相应 import、变量和外围函数；文字步骤须按目标项目配置执行。

```text
在 .depguard.yml 定义规则后运行 depguard ./...
```

## 关键限制

- 独立 CLI 的官方 README 安装命令仍指向无 /v2 的子路径，实际版本须核对；配置默认匹配规则需审阅。

## 来源

- [[depguard-v2-go-official-research]]；[官方资料](https://github.com/OpenPeeDeeP/depguard/blob/v2/README.md)；[Go Packages](https://pkg.go.dev/github.com/OpenPeeDeeP/depguard/v2)。
- 本地研究笔记：`raw/depguard-v2-go-official-research-2026-11-01.md`。
