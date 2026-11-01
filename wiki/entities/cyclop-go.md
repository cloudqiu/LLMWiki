---
title: "github.com/bkielbasa/cyclop"
type: entity
entity_type: tool
created: 2026-11-01
updated: 2026-11-01
tags: [go, library]
status: growing
sources: [raw/cyclop-go-official-research-2026-11-01.md]
---

# github.com/bkielbasa/cyclop

## 用途与适用场景

检测 Go 函数和包的圈复杂度。（[[cyclop-go-official-research]]）

## 依赖与版本

- 模块：`github.com/bkielbasa/cyclop`；安装或依赖声明：`go get github.com/bkielbasa/cyclop/cmd/cyclop`。
- 查阅日期：2026-11-01；实际使用版本由项目锁定。

## 作者与维护者

- [[bartlomiej-klimczak]]：官方主页证实 Bartłomiej Klimczak 与账号关联；具体独立创建和现任维护角色待验证。

## 典型用法

以下是按官方资料整理的核心片段，**尚未在本机运行**。命令需在 Go 项目中执行；Go 代码需补齐 import、变量和外围函数。

```text
cyclop .
```

## 关键限制

- 官方 README 使用 cmd/cyclop 安装；复杂度阈值需按项目配置。

## 来源

- [[cyclop-go-official-research]]；[官方仓库](https://github.com/bkielbasa/cyclop)；[官方文档](https://github.com/bkielbasa/cyclop)。
- 本地查阅记录：`raw/cyclop-go-official-research-2026-11-01.md`。
