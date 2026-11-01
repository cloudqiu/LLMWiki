---
title: "byteorder-lite"
type: entity
entity_type: tool
created: 2026-11-01
updated: 2026-11-01
tags: [rust, library]
status: growing
sources: [raw/byteorder-lite-rust-official-research-2026-11-01.md]
---

# byteorder-lite

## 用途与适用场景

byteorder 的禁止 unsafe 变体，删去部分需要 unsafe 的方法。（[[byteorder-lite-rust-official-research]]）

## 依赖与版本

- Rust / Cargo；`cargo add byteorder-lite`。实际版本以项目 Cargo.lock 为准。
- 2026-11-01 查阅 docs.rs 的 0.1.0 文档；crate 名含连字符时，Rust import 通常将连字符写成下划线。

## 作者与维护者

- 创建者：待验证。
- 当前维护者：待验证。包 owner 或仓库归属本身不等于个人作者身份或完整维护者名单。

## 典型用法

以下片段依据官方文档公开 API 整理，需补足调用上下文、启用适当 feature 并按实际锁定版本编译；**未在本机运行**。

```rust
use byteorder_lite::{BigEndian, ByteOrder};
let value = BigEndian::read_u32(&[0, 0, 0, 1]);
```

## 关键限制

- 该 fork 不提供原 crate 的全部方法；`read_*_into` 系列被移除。

## 相关库

[[byteorder-rust]]。

## 来源

- [[byteorder-lite-rust-official-research]]；本地查阅记录：`raw/byteorder-lite-rust-official-research-2026-11-01.md`。
- [官方文档](https://docs.rs/byteorder-lite/latest/byteorder_lite/)；[crates.io](https://crates.io/crates/byteorder-lite)。
