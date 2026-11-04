---
title: "async-executor"
type: entity
entity_type: tool
created: 2026-11-02
updated: 2026-11-04
tags: [rust, library]
status: stub
sources: [raw/async-executor-rust-official-research-2026-11-02.md, raw/smol-rust-official-research-2026-11-04.md]
---

# async-executor

## 用途与适用场景

提供异步任务执行器，运行由 future 构成的任务。（[[async-executor-rust-official-research]]）

## 依赖与版本

- Rust / Cargo：`cargo add async-executor`。
- 2026-11-02 查阅 docs.rs 版本 1.14.0；实际依赖版本以 Cargo.lock 为准。

## 作者与维护者

- manifest 署名作者：[[stjepan-glavina|Stjepan Glavina]] 与 John Nunley，依据官方 `Cargo.toml` 的 `authors` 字段；创建者的具体角色待验证。
- 当前维护者：待验证。

## 典型用法

- `cargo add async-executor` 安装依赖；公开 API 的独立最小示例待按锁定版本核实。**未在本机运行**。

## 关键限制

- 任务调度和阻塞行为需与运行环境匹配。

## 来源

- [[async-executor-rust-official-research]]；`raw/async-executor-rust-official-research-2026-11-02.md`。
- [官方发布文档](https://docs.rs/async-executor/latest/async_executor/)。
- [官方 manifest](https://github.com/smol-rs/async-executor/blob/master/Cargo.toml) 的作者署名见 `raw/smol-rust-official-research-2026-11-04.md`；此库也是 [[smol-rust|smol]] 的组成组件之一。
