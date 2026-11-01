---
title: "io-uring 官方资料查阅"
type: source
created: 2026-11-01
updated: 2026-11-01
tags: [rust, library]
status: growing
sources: [raw/io-uring-rust-official-research-2026-11-01.md]
author: "docs.rs 发布文档；Codex 整理"
source_url: "https://docs.rs/io-uring/latest/io_uring/"
raw_file: "raw/io-uring-rust-official-research-2026-11-01.md"
format: notes
---

# io-uring 官方资料查阅

## 来源信息

- 2026-11-01 查阅 [docs.rs 文档](https://docs.rs/io-uring/latest/io_uring/)；本地笔记 `raw/io-uring-rust-official-research-2026-11-01.md` 并非官方原文副本。

## 一句话概括

> 封装 Linux io_uring 异步 I/O 接口。

## 核心要点

- docs.rs 显示版本：0.7.15；实际依赖版本须由 Cargo.lock 确定。
- 典型入口与使用条件见 raw「典型入口」；身份与边界见 raw「身份与边界」。

## 与既有知识的关系

- 创建者与现任维护者待官方证据核实。

## 由本来源派生 / 更新的页面

- [[io-uring-rust]]。
