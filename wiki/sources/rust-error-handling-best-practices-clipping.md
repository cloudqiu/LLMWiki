---
title: "Rust 错误处理最佳实践：构建可靠的应用程序"
type: source
created: 2026-11-05
updated: 2026-11-05
tags: [rust, rust-basics, error-handling]
status: growing
author: "程序员爱钓鱼（剪藏正文署名；作者身份待验证）"
source_url: "https://mp.weixin.qq.com/s?__biz=MzYzODE1NzUzMw==&mid=2247484512&idx=1&sn=6f496e4f5c1f0096085135e2ed853e67&chksm=f0e753d2c790dac4601b3e9d18f0d41672cab7f0a503cd2a5c4c22a052167ca0e386ebdf32da&cur_album_id=4602071361631748097&scene=189#wechat_redirect"
raw_file: "raw/Rust 错误处理最佳实践：构建可靠的应用程序.md"
format: article
---

# Rust 错误处理最佳实践：构建可靠的应用程序

## 来源信息

- 《Rust 编程实战》第 24 篇；正文显示 2026-07-29，剪藏于 2026-11-05。原文件的 `author`、`published` 字段为空；署名及日期未在线核对。
- 原文：`raw/Rust 错误处理最佳实践：构建可靠的应用程序.md`；网页地址见 frontmatter。第 23 篇原文尚未摄入。

## 一句话概括

将 `Option`、`Result`、`panic!` 放入应用错误处理流程，讨论类型化错误、传播、分层转换及 `thiserror` / `anyhow` 的常见分工。

## 核心要点

- 文中主张可预期失败用 `Result`、单纯缺失用 `Option`、程序不变量破坏才考虑 `panic!`（“错误处理三原则”、“不要滥用 panic”）。
- 枚举错误类型比统一的 `String` 更利于分支处理；`From` 和 `?` 可连接底层与上层错误（“不要使用 String 作为所有错误”至“错误转换”）。
- 文中将 `thiserror` 用于定义结构化错误、`anyhow` 用于应用级错误传播；这是场景建议，具体依赖版本和 API 应以官方资料核对（“thiserror：推荐用于库项目”至“thiserror 和 anyhow 区别”）。
- Web 层应将内部错误转换为对外响应；日志示例提及 `tracing`，但原文未提供完整的隐私或敏感字段处理规则（“Web 服务错误设计”、“日志记录错误”）。

## 与既有知识的关系

- 接续 [[rust-option-clipping]]、[[rust-result-clipping]]；相关 crate 见 [[thiserror-rust]]、[[anyhow-rust]]。学习顺序见 [[rust-programming-basics]]。
> [!warning] 矛盾
> “3. 程序逻辑错误使用 panic”把 `divide(a, b)` 的 `b == 0` 直接设为 panic；同文“不要滥用 panic”又要求将可预期用户输入错误返回 `Result`。后续 [[rust-rustdoc-cargo-doc-clipping]] 与 [[rust-unit-testing-clipping]] 也把除零作为 `Result::Err` 分支。若 `b` 来自调用方输入，除零应按 API 契约和使用场景设计，不能一律视作内部 bug。本条也记录在 [[rust-programming-basics]]。

- 待验证：`thiserror = "2"`、`anyhow = "1"` 及示例未按目标 Cargo.lock 或本机编译核对；来源署名和发表时间未在线核对。文中记录“用户信息”的日志建议必须结合隐私和最小化原则审视。

## 由本来源派生 / 更新的页面

- [[rust-programming-basics]]。
