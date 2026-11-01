---
title: "equivalent"
type: entity
entity_type: tool
created: 2026-11-01
updated: 2026-11-01
tags: [rust, library]
status: growing
sources: [raw/equivalent-rust-official-research-2026-11-01.md]
---

# equivalent

## 用途与适用场景

为映射查找定义跨类型键等价和比较 trait。（[[equivalent-rust-official-research]]）

## 依赖与版本

- Rust / Cargo；`cargo add equivalent`。实际版本以项目 Cargo.lock 为准。
- 2026-11-01 查阅 docs.rs 的 1.0.2 文档；crate 名含连字符时，Rust import 通常将连字符写成下划线。

## 作者与维护者

- 创建者：待验证。
- 当前维护者：待验证。包 owner 或仓库归属本身不等于个人作者身份或完整维护者名单。

## 典型用法

以下片段依据官方文档公开 API 整理，需补足调用上下文、启用适当 feature 并按实际锁定版本编译；**未在本机运行**。

```rust
use equivalent::Equivalent;
let equal = "hello".equivalent(&String::from("hello"));
```

## 关键限制

- 平台、feature 与版本边界须按实际项目核对。

## 来源

- [[equivalent-rust-official-research]]；本地查阅记录：`raw/equivalent-rust-official-research-2026-11-01.md`。
- [官方文档](https://docs.rs/equivalent/latest/equivalent/)；[crates.io](https://crates.io/crates/equivalent)。
