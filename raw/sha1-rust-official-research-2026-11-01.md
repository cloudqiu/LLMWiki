# sha1 官方资料查阅记录

> 2026-11-01 查阅。本文为 Codex 根据 crate 发布文档整理的研究笔记，并非官方原文副本；示例未在本机运行。

## 名称与版本

- 收件箱名称：`sha1-1`；暂对应正式 crate `sha1`，原文未改。
- docs.rs 显示版本 0.11.0；目标项目须以 Cargo.lock 核对实际使用版本。
- [发布文档](https://docs.rs/sha1/latest/sha1/)；[crates.io 包页](https://crates.io/crates/sha1)。查阅日期：2026-11-01。

## 用途

计算 SHA-1 摘要，主要用于旧协议兼容。

## 典型入口

```rust
use sha1::{Digest, Sha1};
let digest = Sha1::digest(b"legacy data");
```

以上为根据公开 API 整理的片段，可能需要外层函数、依赖、feature 或平台条件；未编译运行。

## 身份与边界

- 包所有者、仓库归属或发布账号不足以确认个人创建者及当前维护者；两者待验证。
- `sha1-1` 无可核实同名 crate；这里只按 `sha1` 暂归档。SHA-1 不适合安全关键的新用途；实际包名和版本待 Cargo.lock 核对。
