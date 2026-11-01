---
title: "anstream"
type: entity
entity_type: tool
created: 2026-11-01
updated: 2026-11-01
tags: [rust, library]
status: growing
sources: [raw/anstream-rust-official-research-2026-11-01.md]
---

# anstream

## 用途与适用场景

让 ANSI 彩色输出适应终端能力的 stdout/stderr 流。（[[anstream-rust-official-research]]）

## 依赖与版本

- Rust / Cargo；`cargo add anstream`。实际版本以项目 Cargo.lock 为准。
- 2026-11-01 查阅 docs.rs 的 1.0.0 文档；crate 名含连字符时，Rust import 通常将连字符写成下划线。

## 作者与维护者

- 创建者：待验证。
- 当前维护者：待验证。包 owner 或仓库归属本身不等于个人作者身份或完整维护者名单。

## 典型用法

以下片段依据官方文档公开 API 整理，需补足调用上下文、启用适当 feature 并按实际锁定版本编译；**未在本机运行**。

```rust
anstream::println!("hello");
```

## 关键限制

- 平台、feature 与版本边界须按实际项目核对。

## 相关库

[[anstyle-rust]]、[[anstyle-query-rust]]、[[anstyle-wincon-rust]]。

## 来源

- [[anstream-rust-official-research]]；本地查阅记录：`raw/anstream-rust-official-research-2026-11-01.md`。
- [官方文档](https://docs.rs/anstream/latest/anstream/)；[crates.io](https://crates.io/crates/anstream)。
