---
title: "sync_wrapper 官方资料查阅"
type: source
created: 2026-11-01
updated: 2026-11-01
tags: [rust, library]
status: growing
sources: [raw/sync-wrapper-rust-official-research-2026-11-01.md]
author: "docs.rs 发布文档；Codex 整理"
source_url: "https://docs.rs/sync_wrapper/latest/sync_wrapper/"
raw_file: "raw/sync-wrapper-rust-official-research-2026-11-01.md"
format: notes
---

# sync_wrapper 官方资料查阅

## 来源信息

- 2026-11-01 查阅 [docs.rs 文档](https://docs.rs/sync_wrapper/latest/sync_wrapper/)；本地笔记 `raw/sync-wrapper-rust-official-research-2026-11-01.md` 并非官方原文副本。

## 一句话概括

> 用静态类型约束包装不直接满足并发 trait 的值。

## 核心要点

- docs.rs 显示版本：1.0.2；实际依赖版本须由 Cargo.lock 确定。
- 典型入口与使用条件见 raw「典型入口」；身份与边界见 raw「身份与边界」。

## 与既有知识的关系

- 相关依赖及角色见库页；创建者与现任维护者待官方证据核实。

## 由本来源派生 / 更新的页面

- [[sync-wrapper-rust]]。
