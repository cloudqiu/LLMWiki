---
title: "js-sys"
type: entity
entity_type: tool
created: 2026-11-01
updated: 2026-11-01
tags: [rust, library]
status: stub
sources: [raw/js-sys-rust-official-research-2026-11-01.md]
---

# js-sys

## 用途与适用场景

在 wasm-bindgen 中调用 JavaScript 内建对象和 API。（[[js-sys-rust-official-research]]）

## 依赖与版本

- Rust / Cargo；`cargo add js-sys`。实际版本以项目 Cargo.lock 为准。
- 2026-11-01 查阅 docs.rs 的 0.3.106 文档；crate 名含连字符时，Rust import 通常将连字符写成下划线。

## 作者与维护者

- 创建者：待验证。
- 当前维护者：待验证。包 owner 或仓库归属本身不等于个人作者身份或完整维护者名单。

## 典型用法

独立的最小 API 用法未从发布文档可靠确认；从 [API 列表](https://docs.rs/js-sys/latest/js_sys/) 查阅相应类型或宏。此页待补示例。

## 关键限制

- 平台、feature 与版本边界须按实际项目核对。

## 来源

- [[js-sys-rust-official-research]]；本地查阅记录：`raw/js-sys-rust-official-research-2026-11-01.md`。
- [发布文档](https://docs.rs/js-sys/latest/js_sys/)；[crates.io](https://crates.io/crates/js-sys)。
