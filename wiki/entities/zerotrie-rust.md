---
title: "zerotrie"
type: entity
entity_type: tool
created: 2026-11-01
updated: 2026-11-01
tags: [rust, library]
status: stub
sources: [raw/zerotrie-rust-official-research-2026-11-01.md]
---

# zerotrie

## 用途与适用场景

以零拷贝 trie 存储和查询字节字符串。（[[zerotrie-rust-official-research]]）

## 依赖与版本

- Rust / Cargo；`cargo add zerotrie`。实际版本以项目 Cargo.lock 为准。
- 2026-11-01 查阅 docs.rs 的 0.2.5 文档；包名与 Rust 模块名可能不同，具体以发布文档为准。

## 作者与维护者

- 创建者：待验证。
- 当前维护者：待验证。包 owner 或仓库归属本身不等于个人作者身份或完整维护者名单。

## 典型用法

独立的最小 API 用法未从发布文档可靠确认；从 [API 列表](https://docs.rs/zerotrie/latest/zerotrie/) 查阅相应类型或宏。此页待补示例。

## 关键限制

- 零拷贝布局不支持就地修改；更新需要重建数据结构。

## 相关库

[[yoke-rust]]、[[yoke-derive-rust]]、[[zerofrom-rust]]、[[zerofrom-derive-rust]]、[[zerovec-rust]]、[[zerovec-derive-rust]]、[[writeable-rust]]、[[icu-provider-rust]]。

## 来源

- [[zerotrie-rust-official-research]]；本地查阅记录：`raw/zerotrie-rust-official-research-2026-11-01.md`。
- [发布文档](https://docs.rs/zerotrie/latest/zerotrie/)；[crates.io](https://crates.io/crates/zerotrie)。
