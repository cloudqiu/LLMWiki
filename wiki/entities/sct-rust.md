---
title: "sct"
type: entity
entity_type: tool
created: 2026-11-01
updated: 2026-11-01
tags: [rust, library]
status: stub
sources: [raw/sct-rust-official-research-2026-11-01.md]
---

# sct

## 用途与适用场景

提供证书透明度相关类型与验证支持。（[[sct-rust-official-research]]）

## 依赖与版本

- Rust / Cargo；`cargo add sct`。实际版本以项目 Cargo.lock 为准。
- 2026-11-01 查阅 docs.rs 的 0.7.1 文档；包名与 Rust 模块名可能不同，具体以发布文档为准。

## 作者与维护者

- 创建者：待验证。
- 当前维护者：待验证。包 owner 或仓库归属本身不等于个人作者身份或完整维护者名单。

## 典型用法

独立的最小 API 用法未从发布文档可靠确认；从 [API 列表](https://docs.rs/sct/latest/sct/) 查阅相应类型或宏。此页待补示例。

## 关键限制

- 这是证书透明度相关的旧组件；与当前 rustls 的配套版本须核实。

## 相关库

[[rustls-rust]]、[[rustls-pki-types-rust]]、[[rustls-webpki-rust]]、[[tokio-rustls-rust]]。

## 来源

- [[sct-rust-official-research]]；本地查阅记录：`raw/sct-rust-official-research-2026-11-01.md`。
- [发布文档](https://docs.rs/sct/latest/sct/)；[crates.io](https://crates.io/crates/sct)。
