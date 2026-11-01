---
title: "futures"
type: entity
entity_type: tool
created: 2026-11-01
updated: 2026-11-01
tags: [rust, library]
status: growing
sources: [raw/futures-rust-official-research-2026-11-01.md]
---

# futures

## 用途与适用场景

提供异步编程的 Future、Stream 与组合工具。（[[futures-rust-official-research]]）

## 依赖与版本

- Rust / Cargo；`cargo add futures`。实际版本以项目 Cargo.lock 为准。
- 2026-11-01 查阅 docs.rs 的 0.3.34 文档；crate 名含连字符时，Rust import 通常将连字符写成下划线。

## 作者与维护者

- 创建者：待验证。
- 当前维护者：待验证。包 owner 或仓库归属本身不等于个人作者身份或完整维护者名单。

## 典型用法

以下片段依据发布文档公开 API 整理，需补足上下文、启用适当 feature 并按实际锁定版本编译；**未在本机运行**。

```rust
let result = futures::executor::block_on(async { 42 });
```

## 关键限制

- 平台、feature 与版本边界须按实际项目核对。

## 相关库

[[futures-channel-rust]]、[[futures-core-rust]]、[[futures-executor-rust]]、[[futures-io-rust]]、[[futures-macro-rust]]、[[futures-sink-rust]]、[[futures-task-rust]]、[[futures-util-rust]]。

## 来源

- [[futures-rust-official-research]]；本地查阅记录：`raw/futures-rust-official-research-2026-11-01.md`。
- [发布文档](https://docs.rs/futures/latest/futures/)；[crates.io](https://crates.io/crates/futures)。
