---
title: "backtrace"
type: entity
entity_type: tool
created: 2026-11-01
updated: 2026-11-01
tags: [rust, library]
status: growing
sources: [raw/backtrace-rust-official-research-2026-11-01.md]
---

# backtrace

## 用途与适用场景

在运行时采集并解析调用栈。（[[backtrace-rust-official-research]]）

## 依赖与版本

- Rust / Cargo；`cargo add backtrace`。实际版本以项目 Cargo.lock 为准。
- 2026-11-01 查阅 docs.rs 的 0.3.77 文档；crate 名含连字符时，Rust import 通常将连字符写成下划线。

## 作者与维护者

- 创建者：待验证。
- 当前维护者：待验证。包 owner 或仓库归属本身不等于个人作者身份或完整维护者名单。

## 典型用法

以下片段依据官方文档公开 API 整理，需补足调用上下文、启用适当 feature 并按实际锁定版本编译；**未在本机运行**。

```rust
let trace = backtrace::Backtrace::new();
println!("{trace:?}");
```

## 关键限制

- 当前收件箱已由用户更正为 `backtrace`；先前 raw 查阅笔记保留了旧拼写 `bracktrace` 的历史记录。

## 来源

- [[backtrace-rust-official-research]]；本地查阅记录：`raw/backtrace-rust-official-research-2026-11-01.md`。
- [官方文档](https://docs.rs/backtrace/latest/backtrace/)；[crates.io](https://crates.io/crates/backtrace)。
