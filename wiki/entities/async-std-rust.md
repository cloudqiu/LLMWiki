---
title: "async-std"
type: entity
entity_type: tool
created: 2026-11-02
updated: 2026-11-04
tags: [rust, library]
status: stub
sources: [raw/async-std-rust-official-research-2026-11-02.md, "raw/Rust 异步生态futures，async_std, tokio.md", raw/smol-rust-official-research-2026-11-04.md]
---

# async-std

## 用途与适用场景

官方摘要为“Deprecated in favor of `smol` - Async version of the Rust standard library”。此页记录版本与来源；迁移目标见 [[smol-rust]]，具体迁移步骤仍须按 API 核对。（[[async-std-rust-official-research]]）

## 依赖与版本

- Rust / Cargo：`cargo add async-std`。
- 2026-11-02 查阅 crates.io 显示稳定版本 1.13.2；实际依赖版本以 Cargo.lock 为准。

## 作者与维护者

- 创建者：待验证。
- 当前维护者：待验证。仓库归属和发布账号不足以证明身份。

## 典型用法

- 安装依赖后，按目标版本的 [发布文档](https://docs.rs/async-std/latest/async_std/) 选择 API；独立最小示例待补。**未在本机运行**。

## 关键限制

- 该包的官方摘要标为 deprecated 或 unmaintained；选用前须核对迁移建议。
> [!warning] 矛盾
> [[rust-async-ecosystem-conversation]] 将 `async-std` 描述为仍可选择的生产级运行时；[项目发布文档](https://docs.rs/async-std/latest/async_std/)明确写明已停止，并建议现有用户及依赖它的库转向 `smol`。


## 来源

- [[async-std-rust-official-research]]；本地研究笔记：`raw/async-std-rust-official-research-2026-11-02.md`。
- [crates.io](https://crates.io/crates/async-std)；[发布文档](https://docs.rs/async-std/latest/async_std/)。
- 对话摘录：[[rust-async-ecosystem-conversation]]；其选型建议与官方维护声明冲突。另见 [[rust-async-runtime-boundaries]]。
