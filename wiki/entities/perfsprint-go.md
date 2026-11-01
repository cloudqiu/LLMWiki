---
title: "github.com/catenacyber/perfsprint"
type: entity
entity_type: tool
created: 2026-11-01
updated: 2026-11-01
tags: [go, library]
status: growing
sources: [raw/perfsprint-go-official-research-2026-11-01.md]
---

# github.com/catenacyber/perfsprint

## 用途与适用场景

找出可用 strconv 等更直接操作替代的 fmt 格式化调用。（[[perfsprint-go-official-research]]）

## 依赖与版本

- 模块：`github.com/catenacyber/perfsprint`；安装或依赖声明：`go install github.com/catenacyber/perfsprint@latest`。
- 查阅日期：2026-11-01；实际使用版本由项目锁定。

## 作者与维护者

- [[catena-cyber]]：官方主页证实 Catena cyber 与账号关联；具体独立创建和现任维护角色待验证。

## 典型用法

以下是按官方资料整理的核心片段，**尚未在本机运行**。命令需在 Go 项目中执行；Go 代码需补齐 import、变量和外围函数。

```text
perfsprint ./...
```

## 关键限制

- 部分重写改变 nil 错误等边界行为；--fix 前需审阅。

## 来源

- [[perfsprint-go-official-research]]；[官方仓库](https://github.com/catenacyber/perfsprint)；[官方文档](https://github.com/catenacyber/perfsprint)。
- 本地查阅记录：`raw/perfsprint-go-official-research-2026-11-01.md`。
