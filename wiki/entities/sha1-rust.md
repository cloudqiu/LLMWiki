---
title: "sha1"
type: entity
entity_type: tool
created: 2026-11-01
updated: 2026-11-01
tags: [rust, library]
status: growing
sources: [raw/sha1-rust-official-research-2026-11-01.md]
---

# sha1

## 用途与适用场景

计算 SHA-1 摘要，主要用于旧协议兼容。（[[sha1-rust-official-research]]）

## 依赖与版本

- Rust / Cargo；`cargo add sha1`。实际版本以项目 Cargo.lock 为准。
- 2026-11-01 查阅 docs.rs 的 0.11.0 文档；包名与 Rust 模块名可能不同，具体以发布文档为准。

## 作者与维护者

- 创建者：待验证。
- 当前维护者：待验证。包 owner 或仓库归属本身不等于个人作者身份或完整维护者名单。

## 典型用法

以下片段依据发布文档公开 API 整理，需补足上下文、feature 和平台条件，并按锁定版本编译；**未在本机运行**。

```rust
use sha1::{Digest, Sha1};
let digest = Sha1::digest(b"legacy data");
```

## 关键限制

- `sha1-1` 无可核实同名 crate；这里只按 `sha1` 暂归档。SHA-1 不适合安全关键的新用途；实际包名和版本待 Cargo.lock 核对。

## 相关库

[[ring-rust]]、[[subtle-rust]]、[[digest-rust]]。

## 来源

- [[sha1-rust-official-research]]；本地查阅记录：`raw/sha1-rust-official-research-2026-11-01.md`。
- [发布文档](https://docs.rs/sha1/latest/sha1/)；[crates.io](https://crates.io/crates/sha1)。
