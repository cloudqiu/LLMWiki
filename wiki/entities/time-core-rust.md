---
title: "time-core"
type: entity
entity_type: tool
created: 2026-11-01
updated: 2026-11-02
tags: [rust, library]
status: stub
sources: [raw/time-core-rust-official-research-2026-11-01.md, raw/rust-core-crate-split-official-research-2026-11-02.md, raw/time-vs-time-core-official-research-2026-11-02.md]
---

# time-core

## 用途与适用场景

time crate 的内部基础组件；公开的 `unit` 模块负责时间单位换算，`util` 模块提供辅助函数。官方文档不建议应用直接依赖。详见 [[rust-time-vs-time-core]]。（[[time-core-rust-official-research]]）

## 依赖与版本

- 应用通常声明 `time`，由 Cargo 解析其 `time-core` 依赖；实际版本以项目 Cargo.lock 为准。
- 2026-11-01 查阅 docs.rs 的 0.1.9 文档；包名与 Rust 模块名可能不同，具体以发布文档为准。

## 作者与维护者

- 创建者：待验证。
- 当前维护者：待验证。包 owner 或仓库归属本身不等于个人作者身份或完整维护者名单。

## 典型用法

独立的最小 API 用法未从发布文档可靠确认；从 [API 列表](https://docs.rs/time-core/latest/time_core/) 查阅相应类型或宏。此页待补示例。

## 关键限制

- 本 crate 是 `time` 的实现细节；具体 feature、平台要求和兼容版本须按目标项目锁定版本核对。

## 相关库

[[time-rust]]、[[time-macros-rust]]、[[powerfmt-rust]]、[[num-conv-rust]]。

官方文档将本 crate 定位为 `time` 的实现细节；拆分背景见 [[rust-crate-core-split]]。

## 来源

- [[time-core-rust-official-research]]；本地查阅记录：`raw/time-core-rust-official-research-2026-11-01.md`。
- [发布文档](https://docs.rs/time-core/latest/time_core/)；[crates.io](https://crates.io/crates/time-core)。
