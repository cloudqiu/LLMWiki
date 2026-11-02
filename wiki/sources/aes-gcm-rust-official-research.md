---
title: "aes-gcm 官方资料查阅"
type: source
created: 2026-11-02
updated: 2026-11-02
tags: [rust, library]
status: growing
sources: [raw/aes-gcm-rust-official-research-2026-11-02.md]
author: "docs.rs 发布文档；Codex 整理"
source_url: "https://docs.rs/aes-gcm/latest/aes_gcm/"
raw_file: "raw/aes-gcm-rust-official-research-2026-11-02.md"
format: notes
---

# aes-gcm 官方资料查阅

## 来源信息

- [docs.rs 发布文档](https://docs.rs/aes-gcm/latest/aes_gcm/)，查阅日期：2026-11-02。
- 本地研究笔记：`raw/aes-gcm-rust-official-research-2026-11-02.md`。

## 一句话概括

> AES-GCM 认证加密实现，提供机密性与完整性保护。

## 核心要点

- 文档显示版本 0.11.1；nonce 不可在同一密钥下重复；实际调用需核对官方安全说明。
- 创建者、当前维护者及独立最小调用示例待验证。

## 由本来源派生 / 更新的页面

- [[aes-gcm-rust]]。
