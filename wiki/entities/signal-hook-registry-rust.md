---
title: "signal-hook-registry"
type: entity
entity_type: tool
created: 2026-11-01
updated: 2026-11-01
tags: [rust, library]
status: stub
sources: [raw/signal-hook-registry-rust-official-research-2026-11-01.md]
---

# signal-hook-registry

## 用途与适用场景

为 signal-hook 提供低层信号回调注册后端。（[[signal-hook-registry-rust-official-research]]）

## 依赖与版本

- Rust / Cargo；`cargo add signal-hook-registry`。实际版本以项目 Cargo.lock 为准。
- 2026-11-01 查阅 docs.rs 的 1.4.8 文档；包名与 Rust 模块名可能不同，具体以发布文档为准。

## 作者与维护者

- 创建者：待验证。
- 当前维护者：待验证。包 owner 或仓库归属本身不等于个人作者身份或完整维护者名单。

## 典型用法

独立的最小 API 用法未从发布文档可靠确认；从 [API 列表](https://docs.rs/signal-hook-registry/latest/signal_hook_registry/) 查阅相应类型或宏。此页待补示例。

## 关键限制

- 此 crate 是 signal-hook 的底层后端，直接使用需遵守异步信号安全要求。

## 来源

- [[signal-hook-registry-rust-official-research]]；本地查阅记录：`raw/signal-hook-registry-rust-official-research-2026-11-01.md`。
- [发布文档](https://docs.rs/signal-hook-registry/latest/signal_hook_registry/)；[crates.io](https://crates.io/crates/signal-hook-registry)。
