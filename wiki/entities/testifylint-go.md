---
title: "github.com/Antonboom/testifylint"
type: entity
entity_type: tool
created: 2026-11-01
updated: 2026-11-01
tags: [go, library]
status: growing
sources: [raw/testifylint-go-official-research-2026-11-01.md]
---

# github.com/Antonboom/testifylint

## 用途与适用场景

检查 testify 测试断言写法，减少含糊或错误的断言。（[[testifylint-go-official-research]]）

## 依赖与版本

- 模块：`github.com/Antonboom/testifylint`；安装或依赖声明：`go install github.com/Antonboom/testifylint@latest`。
- 查阅日期：2026-11-01。具体版本由目标项目锁定。

## 作者与维护者

- [[anton-telyshev]]：官方个人或组织账号关联此仓库；具体创建与当前维护角色待验证。

## 典型用法

以下是按官方资料整理的最小片段，**尚未在本机运行**。Go 片段需要相应 import、变量和外围函数；文字步骤须按目标项目配置执行。

```text
testifylint ./...
```

## 关键限制

- --fix 会改写源码，官方提示修复后可能留下未使用 import。

## 来源

- [[testifylint-go-official-research]]；[官方资料](https://github.com/Antonboom/testifylint)；[Go Packages](https://pkg.go.dev/github.com/Antonboom/testifylint)。
- 本地研究笔记：`raw/testifylint-go-official-research-2026-11-01.md`。
