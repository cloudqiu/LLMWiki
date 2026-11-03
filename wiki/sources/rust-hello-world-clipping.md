---
title: "第一个 Rust 程序 Hello World"
type: source
created: 2026-11-03
updated: 2026-11-03
tags: [rust, rust-basics]
status: growing
author: "程序员爱钓鱼（剪藏正文署名；作者身份待验证）"
source_url: "https://mp.weixin.qq.com/s?__biz=MzYzODE1NzUzMw==&mid=2247484411&idx=1&sn=8923bc203d375524929a4d906570bbbd&chksm=f0e75449c790dd5f764a60256eb09d1820e3738c25da9f34ec97c7d4af853eb0c123643a021b&cur_album_id=4602071361631748097&scene=189#wechat_redirect"
raw_file: "raw/第一个 Rust 程序 Hello World.md"
format: article
---

# 第一个 Rust 程序 Hello World

## 来源信息

- 作者 / 出处：剪藏正文署名“程序员爱钓鱼”；《Rust 编程实战》系列第 3 篇。原文件 frontmatter 的 author、published 为空。
- 发表时间：正文显示 2026-07-08；未与网页在线核对。剪藏创建于 2026-11-03。
- 本地原文：`raw/第一个 Rust 程序 Hello World.md`；[网页原址](https://mp.weixin.qq.com/s?__biz=MzYzODE1NzUzMw==&mid=2247484411&idx=1&sn=8923bc203d375524929a4d906570bbbd&chksm=f0e75449c790dd5f764a60256eb09d1820e3738c25da9f34ec97c7d4af853eb0c123643a021b&cur_album_id=4602071361631748097&scene=189#wechat_redirect)。

## 一句话概括

用 Cargo 创建二进制项目，解释 `Cargo.toml`、`main.rs`、`println!` 与 debug/release 构建。

## 核心要点

- `cargo new hello_rust` 生成 manifest 与 `src/main.rs`，首次构建后出现 `target/`（“创建第一个 Rust 项目”、“查看项目结构”）。
- `fn main()` 是此示例的入口，`println!` 是宏，`cargo run` 构建并运行（“认识 main 函数”、“println! 宏”、“Cargo run 做了什么？”）。
- 介绍 `Cargo.toml` 的 package/dependencies 与 `cargo build --release`（“Cargo.toml 是什么？”、“Release 模式”）。

## 与既有知识的关系

- 关联：[[rust-programming-basics]], [[cargo-guide-clipping]]。
- 待验证：示例 `println!("{} 发布于 {}", language, year)` 把 2026 写作 Rust 发布年，属于示例值，不能据此记为历史事实；`cargo run` 与单独 build 后运行的过程也只是概念化说明。

## 由本来源派生 / 更新的页面

- [[rust-programming-basics]]。
