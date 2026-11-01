# webpki-roots 官方资料查阅记录

> 2026-11-01 查阅。本文为 Codex 根据 crate 发布文档整理的研究笔记，并非官方原文副本；示例未在本机运行。

## 名称与版本

- 收件箱名称与发布包名：`webpki-roots`。
- docs.rs 显示版本 1.0.11；目标项目须以 Cargo.lock 核对实际使用版本。
- [发布文档](https://docs.rs/webpki-roots/latest/webpki_roots/)；[crates.io 包页](https://crates.io/crates/webpki-roots)。查阅日期：2026-11-01。

## 用途

提供内置的 Mozilla 可信根证书集合。

## 典型入口

```rust
let roots = webpki_roots::TLS_SERVER_ROOTS;
```

以上为根据公开 API 整理的片段，可能需要外层函数、依赖、feature 或平台条件；未编译运行。

## 身份与边界

- 包所有者、仓库归属或发布账号不足以确认个人创建者及当前维护者；两者待验证。
- 内置根证书会随版本变化；应用需要考虑信任根更新策略。
