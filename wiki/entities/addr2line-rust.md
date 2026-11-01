---
title: "addr2line"
type: entity
entity_type: tool
created: 2026-11-01
updated: 2026-11-01
tags: [rust, library]
status: growing
sources: [raw/addr2line-rust-official-research-2026-11-01.md]
---

# addr2line

## 用途与适用场景

从 DWARF 调试信息按地址查源文件、行号和函数名。（[[addr2line-rust-official-research]]）

## 依赖与版本

- Rust / Cargo；`cargo add addr2line`。实际版本以项目 Cargo.lock 为准。
- 2026-11-01 查阅 docs.rs 的 0.27.1 文档；crate 名含连字符时，Rust import 通常将连字符写成下划线。

## 作者与维护者

- 创建者：待验证。
- 当前维护者：待验证。包 owner 或仓库归属本身不等于个人作者身份或完整维护者名单。

## 典型用法

以下片段依据官方文档公开 API 整理，需补足调用上下文、启用适当 feature 并按实际锁定版本编译；**未在本机运行**。

```rust
let loader = addr2line::Loader::new("app")?;
let location = loader.find_location(0x1234)?;
```

## 关键限制

- 平台、feature 与版本边界须按实际项目核对。

## 来源

- [[addr2line-rust-official-research]]；本地查阅记录：`raw/addr2line-rust-official-research-2026-11-01.md`。
- [官方文档](https://docs.rs/addr2line/latest/addr2line/)；[crates.io](https://crates.io/crates/addr2line)。
