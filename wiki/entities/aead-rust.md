---
title: "aead"
type: entity
entity_type: tool
created: 2026-11-02
updated: 2026-11-02
tags: [rust, library]
status: stub
sources: [raw/aead-rust-official-research-2026-11-02.md]
---

# aead

## 用途与适用场景

AEAD 加密算法的公共 trait 与类型，供具体算法实现使用。（[[aead-rust-official-research]]）

## 依赖与版本

- Rust / Cargo：`cargo add aead`。
- 2026-11-02 查阅 docs.rs 版本 0.6.1；实际依赖版本以 Cargo.lock 为准。

## 作者与维护者

- 创建者：待验证。
- 当前维护者：待验证。

## 典型用法

- `cargo add aead` 安装依赖；公开 API 的独立最小示例待按锁定版本核实。**未在本机运行**。

## 关键限制

- 接口 crate；应用应选择具体 AEAD 实现。

## 来源

- [[aead-rust-official-research]]；`raw/aead-rust-official-research-2026-11-02.md`。
- [官方发布文档](https://docs.rs/aead/latest/aead/)。
