---
title: "fd-lock"
type: entity
entity_type: tool
created: 2026-11-01
updated: 2026-11-01
tags: [rust, library]
status: growing
sources: [raw/fd-lock-rust-official-research-2026-11-01.md]
---

# fd-lock

## 用途与适用场景

为文件提供建议式读写锁，适合多进程协调访问。（[[fd-lock-rust-official-research]]）

## 依赖与版本

- Rust / Cargo；`cargo add fd-lock`。实际版本以项目 Cargo.lock 为准。
- 2026-11-01 查阅 docs.rs 的 4.0.4 文档；crate 名含连字符时，Rust import 通常将连字符写成下划线。

## 作者与维护者

- 创建者：待验证。
- 当前维护者：待验证。包 owner 或仓库归属本身不等于个人作者身份或完整维护者名单。

## 典型用法

以下片段依据发布文档公开 API 整理，需补足上下文、启用适当 feature 并按实际锁定版本编译；**未在本机运行**。

```rust
let file = std::fs::File::open("data.txt")?;
let mut locked = fd_lock::RwLock::new(file);
let reader = locked.read()?;
```

## 关键限制

- 平台、feature 与版本边界须按实际项目核对。

## 来源

- [[fd-lock-rust-official-research]]；本地查阅记录：`raw/fd-lock-rust-official-research-2026-11-01.md`。
- [发布文档](https://docs.rs/fd-lock/latest/fd_lock/)；[crates.io](https://crates.io/crates/fd-lock)。
