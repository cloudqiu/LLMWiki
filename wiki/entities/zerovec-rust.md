---
title: "zerovec"
type: entity
entity_type: tool
created: 2026-11-01
updated: 2026-11-01
tags: [rust, library]
status: stub
sources: [raw/zerovec-rust-official-research-2026-11-01.md]
---

# zerovec

## 用途与适用场景

把结构化数据以零拷贝方式存于字节切片。（[[zerovec-rust-official-research]]）

## 依赖与版本

- Rust / Cargo；`cargo add zerovec`。实际版本以项目 Cargo.lock 为准。
- 2026-11-01 查阅 docs.rs 的 0.11.9 文档；包名与 Rust 模块名可能不同，具体以发布文档为准。

## 作者与维护者

- 创建者：待验证。
- 当前维护者：待验证。包 owner 或仓库归属本身不等于个人作者身份或完整维护者名单。

## 典型用法

独立的最小 API 用法未从发布文档可靠确认；从 [API 列表](https://docs.rs/zerovec/latest/zerovec/) 查阅相应类型或宏。此页待补示例。

## 关键限制

- 具体 feature、平台要求和兼容版本须按目标项目锁定版本核对。

## 相关库

[[yoke-rust]]、[[yoke-derive-rust]]、[[zerofrom-rust]]、[[zerofrom-derive-rust]]、[[zerovec-derive-rust]]、[[zerotrie-rust]]、[[writeable-rust]]、[[icu-provider-rust]]。

## 来源

- [[zerovec-rust-official-research]]；本地查阅记录：`raw/zerovec-rust-official-research-2026-11-01.md`。
- [发布文档](https://docs.rs/zerovec/latest/zerovec/)；[crates.io](https://crates.io/crates/zerovec)。
