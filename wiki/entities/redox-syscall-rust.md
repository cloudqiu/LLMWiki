---
title: "redox_syscall"
type: entity
entity_type: tool
created: 2026-11-01
updated: 2026-11-01
tags: [rust, library]
status: stub
sources: [raw/redox-syscall-rust-official-research-2026-11-01.md]
---

# redox_syscall

## 用途与适用场景

提供 Redox OS 系统调用号、类型与原始调用封装。（[[redox-syscall-rust-official-research]]）

## 依赖与版本

- Rust / Cargo；`cargo add redox_syscall`。实际版本以项目 Cargo.lock 为准。
- 2026-11-01 查阅 docs.rs 的 0.9.4 文档；包名与 Rust 模块名可能不同，具体以发布文档为准。

## 作者与维护者

- 创建者：待验证。
- 当前维护者：待验证。包 owner 或仓库归属本身不等于个人作者身份或完整维护者名单。

## 典型用法

独立的最小 API 用法未从发布文档可靠确认；从 [API 列表](https://docs.rs/redox_syscall/latest/syscall/) 查阅相应类型或宏。此页待补示例。

## 关键限制

- 主要供 Redox 内核及 relibc 使用；普通应用直接调用不建议，系统调用 ABI 可能变化。

## 来源

- [[redox-syscall-rust-official-research]]；本地查阅记录：`raw/redox-syscall-rust-official-research-2026-11-01.md`。
- [发布文档](https://docs.rs/redox_syscall/latest/syscall/)；[crates.io](https://crates.io/crates/redox_syscall)。
