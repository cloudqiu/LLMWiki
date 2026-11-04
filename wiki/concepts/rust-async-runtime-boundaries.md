---
title: "Rust 异步抽象与运行时边界"
type: concept
created: 2026-11-04
updated: 2026-11-04
tags: [rust, async, futures, runtimes]
status: growing
sources:
  - "raw/Rust 异步生态futures，async_std, tokio.md"
  - "raw/futures-rust-official-research-2026-11-01.md"
  - "raw/tokio-rust-official-research-2026-11-01.md"
  - "raw/async-std-rust-official-research-2026-11-02.md"
  - "raw/smol-rust-official-research-2026-11-04.md"
---

# Rust 异步抽象与运行时边界

## 定义

`std::future::Future` 描述可被轮询的异步计算；`futures` 提供相关工具与可选执行器；完整运行时还可提供调度、I/O 驱动、计时器及运行时特定 API。不同 Future 是否能跨运行时执行，取决于它实际调用的能力。参见 [标准库 Future](https://doc.rust-lang.org/std/future/trait.Future.html)、[futures](https://docs.rs/futures/latest/futures/) 和 [Tokio](https://docs.rs/tokio/latest/tokio/)。

## 为什么重要 / 解决什么问题

写异步库时应区分“只返回 Future”和“依赖某个运行时的 I/O、timer 或任务 API”，避免向调用者暗示不存在的运行时兼容性。应用可根据所依赖库实际支持的运行时选择执行环境。

## 机制 / 要点

| 组件 | 当前可核实的角色 | 注意 |
| --- | --- | --- |
| [[futures-rust|futures]] | `FutureExt`、`Stream`、`Sink`、channel、`block_on` 等；执行器模块也有 `ThreadPool` | `ThreadPool` 受 feature 控制；该库本身不等同于完整网络 I/O 运行时 |
| [[tokio-rust|Tokio]] | 运行时、任务调度、I/O 驱动、定时器及网络 API | `net`、`time`、`rt` 等能力按 feature 启用 |
| [[async-std-rust|async-std]] | 历史上提供类 `std` 的异步 API 与运行时 | [项目文档](https://docs.rs/async-std/latest/async_std/)已声明停止，建议用户转向 `smol` |
| [[smol-rust|smol]] | 将执行器、网络、I/O 与 timer 等较小 async crates 汇集为运行时入口 | 全局 `spawn` 默认单线程；Tokio 库接入需核对 `async-compat` 适配 |

- 若库只组合 `Future` / `Stream` 且不用特定运行时服务，接口可以保持较强的运行时独立性。要调用 `tokio::net`、`tokio::time` 等，则应明确 Tokio 依赖及 feature；仅实现标准 `Future` 不保证底层 I/O 在其他执行器中可运行。
- 原文的双 crate 示例是纯计算与字符串格式化演示；`my_lib` 可返回 Future，由 `my_app` 的 Tokio 执行。代码未在本次摄入时运行，且示意目录未包含实际 workspace 根 manifest。

## 边界与争议

> [!warning] 矛盾
> [[rust-async-ecosystem-conversation]] 把 `async-std` 描述为可与 Tokio 平行选择的生产运行时；[[async-std-rust-official-research]] 和 [官方发布文档](https://docs.rs/async-std/latest/async_std/)写明已停止并建议改用 `smol`。

> [!warning] 矛盾
> 对话称 `futures::executor` 只有单线程；[官方执行器文档](https://docs.rs/futures/latest/futures/executor/)同时列有 `ThreadPool` 与 `LocalPool`。

- “只用 futures 绝不能生产使用”不是普遍规则；需先定义应用是否需要外部 I/O、定时器、任务调度和目标平台。不同项目的性能与兼容性也不能从单一对话断言。

## 相关页面

- [[rust-async-ecosystem-conversation]]、[[futures-rust]]、[[tokio-rust]]、[[async-std-rust]]、[[smol-rust]]、[[rust-crate-selection]]。

## 来源

- 本页 frontmatter 所列 raw 文件；其中对话摘录不是官方事实来源。官方查阅笔记及上列发布文档用于核对当前状态。
