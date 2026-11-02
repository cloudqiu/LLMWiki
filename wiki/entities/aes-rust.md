---
title: "aes"
type: entity
entity_type: tool
created: 2026-11-02
updated: 2026-11-02
tags: [rust, library]
status: stub
sources: [raw/aes-rust-official-research-2026-11-02.md]
---

# aes

## 用途与适用场景

AES 分组密码的纯 Rust 实现，用于构建更高层的加密方案。（[[aes-rust-official-research]]）

## 依赖与版本

- Rust / Cargo：`cargo add aes`。
- 2026-11-02 查阅 docs.rs 版本 0.9.3；实际依赖版本以 Cargo.lock 为准。

## 作者与维护者

- 创建者：待验证。
- 当前维护者：待验证。

## 典型用法

- `cargo add aes` 安装依赖；公开 API 的独立最小示例待按锁定版本核实。**未在本机运行**。

## 关键限制

- 官方明确标记低层密码原语，不应直接用于应用数据加密。

## 来源

- [[aes-rust-official-research]]；`raw/aes-rust-official-research-2026-11-02.md`。
- [官方发布文档](https://docs.rs/aes/latest/aes/)。
