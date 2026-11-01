---
title: "github.com/ckaznocha/intrange"
type: entity
entity_type: tool
created: 2026-11-01
updated: 2026-11-01
tags: [go, library]
status: growing
sources: [raw/intrange-go-official-research-2026-11-01.md]
---

# github.com/ckaznocha/intrange

## 用途与适用场景

找出可改用 Go 1.22 整数 range 的循环。（[[intrange-go-official-research]]）

## 依赖与版本

- 模块：`github.com/ckaznocha/intrange`；安装或依赖声明：`go get github.com/ckaznocha/intrange`。
- 查阅日期：2026-11-01；实际使用版本由项目锁定。

## 作者与维护者

- [[clifton-kaznocha]]：官方主页证实 Clifton Kaznocha 与账号关联；具体独立创建和现任维护角色待验证。

## 典型用法

以下是按官方资料整理的核心片段，**尚未在本机运行**。命令需在 Go 项目中执行；Go 代码需补齐 import、变量和外围函数。

```text
通过 golangci-lint 启用 intrange 检查项目
```

## 关键限制

- 目标项目的 Go 版本须至少 1.22；独立 CLI 用法待验证。

## 来源

- [[intrange-go-official-research]]；[官方仓库](https://github.com/ckaznocha/intrange)；[官方文档](https://github.com/ckaznocha/intrange)。
- 本地查阅记录：`raw/intrange-go-official-research-2026-11-01.md`。
