---
title: "futures 官方资料查阅"
type: source
created: 2026-11-01
updated: 2026-11-04
tags: [rust, library]
status: growing
sources: [raw/futures-rust-official-research-2026-11-01.md, "raw/Rust 异步生态futures，async_std, tokio.md"]
author: "docs.rs 发布文档；Codex 整理"
source_url: "https://docs.rs/futures/latest/futures/"
raw_file: "raw/futures-rust-official-research-2026-11-01.md"
format: notes
---

# futures 官方资料查阅

## 来源信息

- 2026-11-01 查阅 [docs.rs 文档](https://docs.rs/futures/latest/futures/)；本地笔记 `raw/futures-rust-official-research-2026-11-01.md` 并非官方原文副本。

## 一句话概括

> 提供异步编程的 Future、Stream 与组合工具。

## 核心要点

- docs.rs 显示版本：0.3.34；实际依赖版本须由 Cargo.lock 确定。
- 典型入口与使用条件见 raw「典型入口」；身份与边界见 raw「身份与边界」。

## 与既有知识的关系

- 创建者与现任维护者待官方证据核实。
> [!warning] 矛盾
> 新摄入的 [[rust-async-ecosystem-conversation]] 称 `futures::executor` 仅有单线程执行器；[模块文档](https://docs.rs/futures/latest/futures/executor/)还列有 `ThreadPool`（需 `thread-pool` feature）。

## 由本来源派生 / 更新的页面

- [[futures-rust]]。
