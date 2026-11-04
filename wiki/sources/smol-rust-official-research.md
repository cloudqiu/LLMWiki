---
title: "smol Rust 官方资料查阅"
type: source
created: 2026-11-04
updated: 2026-11-04
tags: [rust, async, runtime, library]
status: growing
author: "smol-rs 项目；本地查阅笔记由 Codex 编写"
source_url: "https://docs.rs/smol/2.0.2/smol/"
raw_file: raw/smol-rust-official-research-2026-11-04.md
format: notes
---

# smol Rust 官方资料查阅

## 来源信息

- 出处：smol 官方文档、仓库 README 与 manifest；2026-11-04 查阅。
- 本地记录：`raw/smol-rust-official-research-2026-11-04.md`。
- 原始链接：[smol 2.0.2 文档](https://docs.rs/smol/2.0.2/smol/)、[官方仓库](https://github.com/smol-rs/smol)。

## 一句话概括

> smol 将执行器、I/O、计时器等较小的 Rust async crates 汇集成运行时入口；官方文档还说明 Tokio 库需要按类型使用 `async-compat` 适配。

## 核心要点

- 2.0.2 文档列出 `block_on`、`spawn`、`Executor`、`net`、`io` 等；`spawn` 的全局执行器默认单线程。
- manifest 将 Stjepan Glavina 列为作者；创建者与现任维护者的具体身份仍待验证。
- 仓库 manifest 与 README 的当前 MSRV 为 Rust 1.85；锁定版本仍须独立核对。

## 关键细节

- `raw/smol-rust-official-research-2026-11-04.md` 的「版本与能力」「作者与维护证据」「示例核对与限制」记录了各项官方 URL 与适用边界。

## 与既有知识的关系

- [[rust-async-runtime-boundaries]] 已依据 async-std 官方文档注明其停止并推荐 smol；本次补充 smol 自身能力与兼容边界。
- smol 与 [[async-executor-rust]] 相关，但 smol 是组合入口，async-executor 是执行器组件。
- 当前维护者及创建过程待验证，不能从仓库归属或 manifest 作者字段直接推断。

## 由本来源派生 / 更新的页面

- [[smol-rust]]、[[stjepan-glavina]]、[[async-executor-rust]]、[[rust-async-runtime-boundaries]]。
