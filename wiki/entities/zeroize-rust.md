---
title: "zeroize"
type: entity
entity_type: tool
created: 2026-11-01
updated: 2026-11-01
tags: [rust, library]
status: growing
sources: [raw/zeroize-rust-official-research-2026-11-01.md]
---

# zeroize

## 用途与适用场景

清除敏感内存并降低编译器优化掉清除操作的风险。（[[zeroize-rust-official-research]]）

## 依赖与版本

- Rust / Cargo；`cargo add zeroize`。实际版本以项目 Cargo.lock 为准。
- 2026-11-01 查阅 docs.rs 的 1.9.1 文档；包名与 Rust 模块名可能不同，具体以发布文档为准。

## 作者与维护者

- 创建者：待验证。
- 当前维护者：待验证。包 owner 或仓库归属本身不等于个人作者身份或完整维护者名单。

## 典型用法

以下片段依据发布文档公开 API 整理，需补足上下文、feature 和平台条件，并按锁定版本编译；**未在本机运行**。

```rust
use zeroize::Zeroize;
let mut secret = vec![1u8, 2, 3];
secret.zeroize();
```

## 关键限制

- 具体 feature、平台要求和兼容版本须按目标项目锁定版本核对。

## 相关库

[[zerocopy-rust]]、[[zerocopy-derive-rust]]。

## 来源

- [[zeroize-rust-official-research]]；本地查阅记录：`raw/zeroize-rust-official-research-2026-11-01.md`。
- [发布文档](https://docs.rs/zeroize/latest/zeroize/)；[crates.io](https://crates.io/crates/zeroize)。
