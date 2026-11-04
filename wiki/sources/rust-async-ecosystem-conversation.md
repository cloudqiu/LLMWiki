---
title: "Rust 异步生态：futures、async-std、Tokio 对话摘录"
type: source
created: 2026-11-04
updated: 2026-11-04
tags: [rust, async, futures, runtimes]
status: growing
author: "未标明（AI 对话摘录，含生成过程文字）"
source_url: ""
raw_file: "raw/Rust 异步生态futures，async_std, tokio.md"
format: notes
---

# Rust 异步生态：futures、async-std、Tokio 对话摘录

## 来源信息

- 作者 / 出处：本地 AI 对话摘录；包含三个连续问题、回答及“Deep thinking completed”生成过程文字，未标明作者、模型、原始链接或日期。生成过程只是摘录内容，不作事实证据。
- 获取日期：文件于 2026-11-04 加入 `raw/`；本地原文：`raw/Rust 异步生态futures，async_std, tokio.md`。
- 核对日期：2026-11-04；本次还查阅了 [futures 文档](https://docs.rs/futures/latest/futures/)、[执行器模块](https://docs.rs/futures/latest/futures/executor/)、[Tokio 文档](https://docs.rs/tokio/latest/tokio/) 和 [async-std 文档](https://docs.rs/async-std/latest/async_std/)。

## 一句话概括

对话用“异步抽象/工具”与“运行时”解释三库分工，并演示一个依赖 `futures` 的库由 Tokio 应用执行。

## 核心要点

- `Future` trait 目前由标准库定义；`futures` 提供 `Stream`、`Sink`、组合子、I/O trait 及执行器工具；Tokio 提供任务调度、I/O 驱动和定时器。摘录的总体分层可作入门模型，但不能据此断定所有异步库的依赖图（开头比较与“三者关系”；[标准库 Future](https://doc.rust-lang.org/std/future/trait.Future.html)；[futures](https://docs.rs/futures/latest/futures/)；[Tokio](https://docs.rs/tokio/latest/tokio/)）。
- `futures::executor::block_on` 能在当前线程驱动适合的 Future。摘录末尾的 `my_lib` / `my_app` 示例展示 `Ready`、`FutureExt::map`、`BoxFuture` 与 Tokio `#[tokio::main]` 的组合；该示例没有网络、文件或定时器，因此没有证明一般 I/O Future 可在任意运行时直接互换（“只用 futures 能做什么？”、“项目结构”至“为什么这样能工作？”）。
- 需要 Tokio 的 `net`、`time` 等具体能力的库，不能仅靠返回标准 `Future` 就宣称运行时无关；依赖及 feature 应按所用 API 选择（“什么时候需要引入 tokio 到库里？”；[Tokio 文档的库作者与 feature 小节](https://docs.rs/tokio/latest/tokio/)）。

## 与既有知识的关系

- 关联：[[rust-async-runtime-boundaries]]、[[futures-rust]]、[[tokio-rust]]、[[async-std-rust]]、[[futures-rust-official-research]]、[[tokio-rust-official-research]]、[[async-std-rust-official-research]]。
> [!warning] 矛盾
> 摘录把 `async-std` 作为仍可推荐的生产运行时，并称它“生产级”；[async-std 发布文档](https://docs.rs/async-std/latest/async_std/)明确说项目已停止，建议迁移到 `smol`。此冲突也记录在 [[async-std-rust]]。
> [!warning] 矛盾
> 摘录称 `futures::executor` 只有单线程、无法利用多核；[futures 执行器文档](https://docs.rs/futures/latest/futures/executor/)列出 `ThreadPool`（需相应 feature）及 `LocalPool`。此冲突也记录在 [[futures-rust]]。
- 其他待验证：摘录的“不能在生产环境只用 futures”“所有主流库都必须依赖 Tokio”“Tokio 可以驱动任何 Future”等均过于绝对；适用性取决于具体 Future 是否要求 I/O driver、timer 或其他运行时服务。摘录提到 `futures::time::sleep`，本次查阅的 `futures` 文档未见该模块，应按目标版本核对。示例未在本次摄入时编译或运行。

## 由本来源派生 / 更新的页面

- [[rust-async-runtime-boundaries]]、[[futures-rust]]、[[async-std-rust]]、[[futures-rust-official-research]]、[[async-std-rust-official-research]]。
