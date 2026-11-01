---
title: "cfg-if"
type: entity
entity_type: tool
created: 2026-11-01
updated: 2026-11-01
tags: [rust, library]
status: growing
sources: [raw/cfg-if-rust-official-research-2026-11-01.md]
---

# cfg-if

## 用途与适用场景

按 cfg 条件选择首个匹配的代码块。（[[cfg-if-rust-official-research]]）

## 依赖与版本

- Rust / Cargo；`cargo add cfg-if`。实际版本以项目 Cargo.lock 为准。
- 2026-11-01 查阅 docs.rs 的 1.0.5 文档；crate 名含连字符时，Rust import 通常将连字符写成下划线。

## 作者与维护者

- 创建者：待验证。
- 当前维护者：待验证。包 owner 或仓库归属本身不等于个人作者身份或完整维护者名单。

## 典型用法

以下片段依据官方文档公开 API 整理，需补足调用上下文、启用适当 feature 并按实际锁定版本编译；**未在本机运行**。

```rust
cfg_if::cfg_if! { if #[cfg(unix)] { const OS: &str = "unix"; } else { const OS: &str = "other"; } }
```

## 关键限制

- 官方文档提示 Rust 新版已有相近内置宏；具体替代需核对最低 Rust 版本。

## 来源

- [[cfg-if-rust-official-research]]；本地查阅记录：`raw/cfg-if-rust-official-research-2026-11-01.md`。
- [官方文档](https://docs.rs/cfg-if/latest/cfg_if/)；[crates.io](https://crates.io/crates/cfg-if)。
