---
title: "wasm-bindgen-shared"
type: entity
entity_type: tool
created: 2026-11-01
updated: 2026-11-01
tags: [rust, library]
status: stub
sources: [raw/wasm-bindgen-shared-rust-official-research-2026-11-01.md]
---

# wasm-bindgen-shared

## 用途与适用场景

在 wasm-bindgen 与其 CLI 之间共享内部定义。（[[wasm-bindgen-shared-rust-official-research]]）

## 依赖与版本

- Rust / Cargo；`cargo add wasm-bindgen-shared`。实际版本以项目 Cargo.lock 为准。
- 2026-11-01 查阅 docs.rs 的 0.2.129 文档；包名与 Rust 模块名可能不同，具体以发布文档为准。

## 作者与维护者

- 创建者：待验证。
- 当前维护者：待验证。包 owner 或仓库归属本身不等于个人作者身份或完整维护者名单。

## 典型用法

独立的最小 API 用法未从发布文档可靠确认；从 [API 列表](https://docs.rs/crate/wasm-bindgen-shared/latest) 查阅相应类型或宏。此页待补示例。

## 关键限制

- 这是 wasm-bindgen 内部依赖，通常不直接在应用中使用。

## 相关库

[[wasm-bindgen-rust]]、[[wasm-bindgen-backend-rust]]、[[wasm-bindgen-futures-rust]]、[[wasm-bindgen-macro-rust]]、[[wasm-bindgen-macro-support-rust]]、[[js-sys-rust]]、[[web-sys-rust]]、[[wasm-streams-rust]]、[[web-time-rust]]。

## 来源

- [[wasm-bindgen-shared-rust-official-research]]；本地查阅记录：`raw/wasm-bindgen-shared-rust-official-research-2026-11-01.md`。
- [发布文档](https://docs.rs/crate/wasm-bindgen-shared/latest)；[crates.io](https://crates.io/crates/wasm-bindgen-shared)。
