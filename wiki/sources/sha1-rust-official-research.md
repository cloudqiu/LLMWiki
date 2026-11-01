---
title: "sha1 官方资料查阅"
type: source
created: 2026-11-01
updated: 2026-11-01
tags: [rust, library]
status: growing
sources: [raw/sha1-rust-official-research-2026-11-01.md]
author: "docs.rs 发布文档；Codex 整理"
source_url: "https://docs.rs/sha1/latest/sha1/"
raw_file: "raw/sha1-rust-official-research-2026-11-01.md"
format: notes
---

# sha1 官方资料查阅

## 来源信息

- 2026-11-01 查阅 [docs.rs 文档](https://docs.rs/sha1/latest/sha1/)；本地笔记 `raw/sha1-rust-official-research-2026-11-01.md` 并非官方原文副本。

## 一句话概括

> 计算 SHA-1 摘要，主要用于旧协议兼容。

## 核心要点

- docs.rs 显示版本：0.11.0；实际依赖版本须由 Cargo.lock 确定。
- 典型入口与使用条件见 raw「典型入口」；身份与边界见 raw「身份与边界」。

## 与既有知识的关系

- 收件箱 `sha1-1` 暂按 `sha1` 消歧。

## 由本来源派生 / 更新的页面

- [[sha1-rust]]。
