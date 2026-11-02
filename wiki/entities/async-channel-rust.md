---
title: "async-channel"
type: entity
entity_type: tool
created: 2026-11-02
updated: 2026-11-02
tags: [rust, library]
status: stub
sources: [raw/async-channel-rust-official-research-2026-11-02.md]
---

# async-channel

## 用途与适用场景

异步多生产者多消费者 channel，每条消息由一个接收者取得。（[[async-channel-rust-official-research]]）

## 依赖与版本

- Rust / Cargo：`cargo add async-channel`。
- 2026-11-02 查阅 docs.rs 版本 2.5.0；实际依赖版本以 Cargo.lock 为准。

## 作者与维护者

- 创建者：待验证。
- 当前维护者：待验证。

## 典型用法

- `cargo add async-channel` 安装依赖；公开 API 的独立最小示例待按锁定版本核实。**未在本机运行**。

## 关键限制

- 有界与无界 channel 的容量和背压行为不同。

## 来源

- [[async-channel-rust-official-research]]；`raw/async-channel-rust-official-research-2026-11-02.md`。
- [官方发布文档](https://docs.rs/async-channel/latest/async_channel/)。
