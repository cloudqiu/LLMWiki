---
title: "github.com/pkg/errors"
type: entity
entity_type: tool
created: 2026-11-02
updated: 2026-11-02
tags: [go, library]
status: growing
sources: [raw/pkg-errors-go-official-research-2026-11-02.md]
---

# github.com/pkg/errors

## 用途与适用场景

包装错误并附加调用栈或上下文。（[[pkg-errors-go-official-research]]）

## 依赖与版本

- Go：`go get github.com/pkg/errors@v0.9.1`；实际版本以项目 go.mod/go.sum 为准。
- 查阅日期：2026-11-02；相关导入路径：`github.com/pkg/errors`。

## 作者与维护者

- 创建者：待验证。
- 当前维护者：待验证。

## 典型用法

- `errors.Wrap(err, "context")`（示意调用，需放入完整程序并按锁定版本编译）。 **未在本机运行**。

## 关键限制

- 具体平台、子包和版本约束需按目标项目核对。

## 来源

- [[pkg-errors-go-official-research]]；`raw/pkg-errors-go-official-research-2026-11-02.md`。
- [官方包文档](https://pkg.go.dev/github.com/pkg/errors)。
