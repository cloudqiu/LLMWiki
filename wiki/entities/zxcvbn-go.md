---
title: "github.com/ccojocar/zxcvbn-go"
type: entity
entity_type: tool
created: 2026-11-01
updated: 2026-11-01
tags: [go, library]
status: growing
sources: [raw/zxcvbn-go-official-research-2026-11-01.md]
---

# github.com/ccojocar/zxcvbn-go

## 用途与适用场景

估计密码强度并识别常见词和模式。（[[zxcvbn-go-official-research]]）

## 依赖与版本

- 模块：`github.com/ccojocar/zxcvbn-go`；安装或依赖声明：`go get github.com/ccojocar/zxcvbn-go`。
- 查阅日期：2026-11-01；实际使用版本由项目锁定。

## 作者与维护者

- [[cosmin-cojocar]]：官方主页证实 Cosmin Cojocar 与账号关联；具体独立创建和现任维护角色待验证。

## 典型用法

以下是按官方资料整理的核心片段，**尚未在本机运行**。命令需在 Go 项目中执行；Go 代码需补齐 import、变量和外围函数。

```go
strength := zxcvbn.PasswordStrength("example-password", []string{"username"}); _ = strength
```

## 关键限制

- 这是已归档 nbutton23 版本的活跃 fork；评分是估计，不是密码安全保证。

## 来源

- [[zxcvbn-go-official-research]]；[官方仓库](https://github.com/ccojocar/zxcvbn-go)；[官方文档](https://github.com/ccojocar/zxcvbn-go)。
- 本地查阅记录：`raw/zxcvbn-go-official-research-2026-11-01.md`。
