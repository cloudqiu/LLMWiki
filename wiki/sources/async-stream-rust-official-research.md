---
title: "async-stream 官方资料查阅"
type: source
created: 2026-11-01
updated: 2026-11-01
tags: [rust, library]
status: growing
sources: [raw/async-stream-rust-official-research-2026-11-01.md]
author: "docs.rs 发布文档；Codex 整理"
source_url: "https://docs.rs/async-stream/latest/async_stream/"
raw_file: "raw/async-stream-rust-official-research-2026-11-01.md"
format: notes
---

# async-stream 官方资料查阅

## 来源信息

- 2026-11-01 查阅 [docs.rs 文档](https://docs.rs/async-stream/latest/async_stream/) 与 [crates.io 包页](https://crates.io/crates/async-stream)。
- 本地研究笔记：`raw/async-stream-rust-official-research-2026-11-01.md`，并非官方原文副本。

## 一句话概括

> 用 stream! 与 try_stream! 宏创建异步流。

## 核心要点

- docs.rs 显示版本：0.3.6；实际依赖版本须由 Cargo.lock 确定。
- 典型入口与使用条件见 raw「典型入口」；身份与边界见 raw「身份与边界」。

## 与既有知识的关系

- 与 [[async-stream-rust]] 相关。

## 由本来源派生 / 更新的页面

- [[async-stream-rust]]。
