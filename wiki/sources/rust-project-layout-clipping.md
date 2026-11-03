---
title: "Rust 项目目录结构详解：从 Hello World 到企业级项目"
type: source
created: 2026-11-03
updated: 2026-11-03
tags: [rust, rust-basics]
status: growing
author: "程序员爱钓鱼（剪藏正文署名；作者身份待验证）"
source_url: "https://mp.weixin.qq.com/s?__biz=MzYzODE1NzUzMw==&mid=2247484419&idx=1&sn=2441030ef1f0487331fd1db2da6e2ccb&chksm=f0e753b1c790daa73d2ff17f215bf32af430a7c77b1fcd6016f1bfd7bf89aff2a5632e4ac800&cur_album_id=4602071361631748097&scene=189#wechat_redirect"
raw_file: "raw/Rust 项目目录结构详解：从 Hello World 到企业级项目.md"
format: article
---

# Rust 项目目录结构详解：从 Hello World 到企业级项目

## 来源信息

- 作者 / 出处：剪藏正文署名“程序员爱钓鱼”；《Rust 编程实战》系列第 5 篇。原文件 frontmatter 的 author、published 为空。
- 发表时间：正文显示 2026-07-10；未与网页在线核对。剪藏创建于 2026-11-03。
- 本地原文：`raw/Rust 项目目录结构详解：从 Hello World 到企业级项目.md`；[网页原址](https://mp.weixin.qq.com/s?__biz=MzYzODE1NzUzMw==&mid=2247484419&idx=1&sn=2441030ef1f0487331fd1db2da6e2ccb&chksm=f0e753b1c790daa73d2ff17f215bf32af430a7c77b1fcd6016f1bfd7bf89aff2a5632e4ac800&cur_album_id=4602071361631748097&scene=189#wechat_redirect)。

## 一句话概括

解释 Cargo 项目的常见文件和目标目录，并展示一种应用分层目录建议。

## 核心要点

- 描述 manifest、锁文件、`src/main.rs`、`src/lib.rs` 和 `target/` 的角色（“创建一个新项目”至“lib.rs”）。
- 展示 `src/bin`、`examples`、`tests`、`benches` 对应的多二进制、示例、集成测试和基准测试用途（各同名小节）。
- 提出 config/router/handler/service/repository/model 等目录的企业应用分层范例（“企业级项目目录”）。

## 与既有知识的关系

- 关联：[[rust-programming-basics]], [[cargo-guide-clipping]]。
- 待验证：末段目录树是作者建议，不是 Cargo 要求；不能把每种项目都必须有 `main.rs`、`Cargo.lock` 或 `benches` 当作通则。

## 由本来源派生 / 更新的页面

- [[rust-programming-basics]]。
