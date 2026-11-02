---
title: "aes-gcm"
type: entity
entity_type: tool
created: 2026-11-02
updated: 2026-11-02
tags: [rust, library]
status: stub
sources: [raw/aes-gcm-rust-official-research-2026-11-02.md]
---

# aes-gcm

## 用途与适用场景

AES-GCM 认证加密实现，提供机密性与完整性保护。（[[aes-gcm-rust-official-research]]）

## 依赖与版本

- Rust / Cargo：`cargo add aes-gcm`。
- 2026-11-02 查阅 docs.rs 版本 0.11.1；实际依赖版本以 Cargo.lock 为准。

## 作者与维护者

- 创建者：待验证。
- 当前维护者：待验证。

## 典型用法

- `cargo add aes-gcm` 安装依赖；公开 API 的独立最小示例待按锁定版本核实。**未在本机运行**。

## 关键限制

- nonce 不可在同一密钥下重复；实际调用需核对官方安全说明。

## 来源

- [[aes-gcm-rust-official-research]]；`raw/aes-gcm-rust-official-research-2026-11-02.md`。
- [官方发布文档](https://docs.rs/aes-gcm/latest/aes_gcm/)。
