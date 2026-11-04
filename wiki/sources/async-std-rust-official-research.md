---
title: "async-std 官方资料查阅"
type: source
created: 2026-11-02
updated: 2026-11-04
tags: [rust, library]
status: stub
sources: [raw/async-std-rust-official-research-2026-11-02.md, "raw/Rust 异步生态futures，async_std, tokio.md"]
author: "crates.io 包元数据；Codex 整理"
source_url: "https://crates.io/crates/async-std"
raw_file: "raw/async-std-rust-official-research-2026-11-02.md"
format: notes
---

# async-std 官方资料查阅

## 来源信息

- [crates.io 官方包页](https://crates.io/crates/async-std)，2026-11-02 查阅；本地研究笔记：`raw/async-std-rust-official-research-2026-11-02.md`。
- [发布文档](https://docs.rs/async-std/latest/async_std/)；显示稳定版本：1.13.2。

## 一句话概括

> 官方摘要：Deprecated in favor of `smol` - Async version of the Rust standard library

## 核心要点

- 已核实发布名与注册表显示版本；具体 API 示例和身份信息待验证。
- 该包的官方摘要标为 deprecated 或 unmaintained；选用前须核对迁移建议。
> [!warning] 矛盾
> [[rust-async-ecosystem-conversation]] 将 `async-std` 作为可正常选择的生产运行时；[项目文档](https://docs.rs/async-std/latest/async_std/)写明已停止并建议迁移到 `smol`。

## 由本来源派生 / 更新的页面

- [[async-std-rust]]。
