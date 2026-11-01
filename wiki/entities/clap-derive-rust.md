---
title: "clap_derive"
type: entity
entity_type: tool
created: 2026-11-01
updated: 2026-11-01
tags: [rust, library]
status: growing
sources: [raw/clap-derive-rust-official-research-2026-11-01.md]
---

# clap_derive

## 用途与适用场景

clap 的派生宏实现组件。（[[clap-derive-rust-official-research]]）

## 依赖与版本

- Rust / Cargo；`cargo add clap_derive`。实际版本以项目 Cargo.lock 为准。
- 2026-11-01 查阅 docs.rs 的 4.6.7 文档；crate 名含连字符时，Rust import 通常将连字符写成下划线。

## 作者与维护者

- 创建者：待验证。
- 当前维护者：待验证。包 owner 或仓库归属本身不等于个人作者身份或完整维护者名单。

## 典型用法

以下片段依据官方文档公开 API 整理，需补足调用上下文、启用适当 feature 并按实际锁定版本编译；**未在本机运行**。

```rust
#[derive(clap::Parser)] struct Cli { #[arg(long)] verbose: bool }
```

## 关键限制

- 平台、feature 与版本边界须按实际项目核对。

## 相关库

[[clap-rust]]、[[clap-builder-rust]]。

## 来源

- [[clap-derive-rust-official-research]]；本地查阅记录：`raw/clap-derive-rust-official-research-2026-11-01.md`。
- [官方文档](https://docs.rs/clap_derive/latest/clap_derive/)；[crates.io](https://crates.io/crates/clap_derive)。
