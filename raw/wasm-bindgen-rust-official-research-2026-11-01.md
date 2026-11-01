# wasm-bindgen 官方资料查阅记录

> 2026-11-01 查阅。本文为 Codex 根据 crate 发布文档整理的研究笔记，并非官方原文副本；示例未在本机运行。

## 名称与版本

- 收件箱名称与发布包名：`wasm-bindgen`。
- docs.rs 显示版本 0.2.130；目标项目须以 Cargo.lock 核对实际使用版本。
- [发布文档](https://docs.rs/wasm-bindgen/latest/wasm_bindgen/)；[crates.io 包页](https://crates.io/crates/wasm-bindgen)。查阅日期：2026-11-01。

## 用途

连接 Rust/Wasm 与 JavaScript 值和函数。

## 典型入口

```rust
use wasm_bindgen::prelude::*;
#[wasm_bindgen] pub fn greet() -> String { "hello".into() }
```

以上为根据公开 API 整理的片段，可能需要外层函数、依赖、feature 或平台条件；未编译运行。

## 身份与边界

- 包所有者、仓库归属或发布账号不足以确认个人创建者及当前维护者；两者待验证。
- 具体 feature、平台要求和兼容版本须按目标项目锁定版本核对。
