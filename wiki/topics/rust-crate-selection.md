---
title: "Rust crate 发现与选型"
type: topic
created: 2026-11-04
updated: 2026-11-04
tags: [rust, crates, selection]
status: growing
sources:
  - "raw/10 Rust Crates Every Developer Should Know in 2026.md"
  - "raw/Crate List.md"
  - "raw/Rust Crates - Best rust crates by topic & Highest rated rust crates.md"
---

# Rust crate 发现与选型

## 概述

这三份剪藏都是第三方发现和推荐材料。它们能帮助按用途列出候选，不能单独证明当前版本、API、维护者或适用性。选定候选后，应查项目官方文档、仓库和 crates.io；本库已有的库页也要回溯各自所引的官方来源。

## 来源地图

| 来源 | 适合使用的部分 | 证据边界 |
| --- | --- | --- |
| [[rustify-ten-crates-2026-clipping|Rustify 十个 crate]] | 了解常见项目功能所对应的候选 | 排名、下载量、普及率和示例未独立复核 |
| [[blessed-rs-crate-list-clipping|blessed.rs 清单]] | 按任务类别比较候选和替代项 | 未标发布日期；偏好与维护状态可能变化 |
| [[crates-dev-discovery-clipping|crates.dev 首页]] | 获取若干 crate 名称 | 自称的测试审查与部分术语定义缺乏可靠依据 |

## 从场景到已有库页

- 数据交换：[[serde-rust]]；异步执行：[[tokio-rust]]；错误处理：[[anyhow-rust]]、[[thiserror-rust]]。
- CLI 和并行：[[clap-rust]]、[[rayon-rust]]；HTTP 客户端与 Web 服务：[[reqwest-rust]]、[[axum-rust]]。
- 诊断与数据库：[[tracing-rust]]、[[sqlx-rust]]；日期时间：[[time-rust]]、[[chrono-rust]]，另将 jiff 作为待核查候选。

## 开放问题

- 对具体项目确定最低 Rust 版本、目标平台、功能开关和许可证后，逐一核对候选 crate 的官方文档与维护现状。
- Rustify 的量化与普及率断言需有可重复的数据来源；blessed.rs 对 chrono 的状态判断需核对项目公告。
- 这三份来源没有触发对其所列全部 crate 的逐个摄入；新增库页仍按本库第三方库流程核实官方资料、作者和示例。

## 来源

- 本页 frontmatter 所列三份 raw 剪藏；各来源页记录了具体推荐及可信度边界。
