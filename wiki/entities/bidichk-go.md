---
title: "github.com/breml/bidichk"
type: entity
entity_type: tool
created: 2026-11-01
updated: 2026-11-01
tags: [go, library]
status: growing
sources: [raw/bidichk-go-official-research-2026-11-01.md]
---

# github.com/breml/bidichk

## 用途与适用场景

检测源码中可能改变显示顺序的危险双向 Unicode 控制符。（[[bidichk-go-official-research]]）

## 依赖与版本

- 模块：`github.com/breml/bidichk`；安装或依赖声明：`go install github.com/breml/bidichk/cmd/bidichk@latest`。
- 查阅日期：2026-11-01；实际使用版本由项目锁定。

## 作者与维护者

- [[lucas-bremgartner]]：官方主页证实 Lucas Bremgartner 与账号关联；具体独立创建和现任维护角色待验证。

## 典型用法

以下是按官方资料整理的核心片段，**尚未在本机运行**。命令需在 Go 项目中执行；Go 代码需补齐 import、变量和外围函数。

```text
bidichk ./...
```

## 关键限制

- 仅检查配置定义的危险字符，不等于完整代码安全审计。

## 来源

- [[bidichk-go-official-research]]；[官方仓库](https://github.com/breml/bidichk)；[官方文档](https://github.com/breml/bidichk)。
- 本地查阅记录：`raw/bidichk-go-official-research-2026-11-01.md`。
