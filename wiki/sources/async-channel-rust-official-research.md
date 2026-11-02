---
title: "async-channel 官方资料查阅"
type: source
created: 2026-11-02
updated: 2026-11-02
tags: [rust, library]
status: growing
sources: [raw/async-channel-rust-official-research-2026-11-02.md]
author: "docs.rs 发布文档；Codex 整理"
source_url: "https://docs.rs/async-channel/latest/async_channel/"
raw_file: "raw/async-channel-rust-official-research-2026-11-02.md"
format: notes
---

# async-channel 官方资料查阅

## 来源信息

- [docs.rs 发布文档](https://docs.rs/async-channel/latest/async_channel/)，查阅日期：2026-11-02。
- 本地研究笔记：`raw/async-channel-rust-official-research-2026-11-02.md`。

## 一句话概括

> 异步多生产者多消费者 channel，每条消息由一个接收者取得。

## 核心要点

- 文档显示版本 2.5.0；有界与无界 channel 的容量和背压行为不同。
- 创建者、当前维护者及独立最小调用示例待验证。

## 由本来源派生 / 更新的页面

- [[async-channel-rust]]。
