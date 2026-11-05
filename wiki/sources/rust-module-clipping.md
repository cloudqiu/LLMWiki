---
title: "Rust Module 模块系统详解：组织大型项目代码"
type: source
created: 2026-11-05
updated: 2026-11-05
tags: [rust, rust-basics, modules]
status: growing
author: "程序员爱钓鱼（剪藏正文署名；作者身份待验证）"
source_url: "https://mp.weixin.qq.com/s?__biz=MzYzODE1NzUzMw==&mid=2247484516&idx=1&sn=b9a0237c62a77b63f0b6f693edc34d25&chksm=f0e753d6c790dac0c77a4bbc94d55d468afe346edf0347771ad1a3e08df3593a5ed16232a4d4&cur_album_id=4602071361631748097&scene=189#wechat_redirect"
raw_file: "raw/Rust Module 模块系统详解：组织大型项目代码.md"
format: article
---

# Rust Module 模块系统详解：组织大型项目代码

## 来源信息

- 《Rust 编程实战》第 25 篇；正文显示 2026-07-30，剪藏于 2026-11-05。原文件的 `author`、`published` 字段为空；署名及日期未在线核对。
- 原文：`raw/Rust Module 模块系统详解：组织大型项目代码.md`；网页地址见 frontmatter。

## 一句话概括

介绍用 `mod`、`pub` 和路径组织 Rust 代码，并展示内联、文件和目录模块的布局。

## 核心要点

- `mod` 声明模块；子项默认私有，`pub`、`pub(crate)`、`pub(super)` 控制可见范围（“什么是 Module？”至“pub 控制访问权限”）。
- `use` 缩短路径，`as` 设别名；`self`、`super`、`crate` 分别指当前、父级和 crate 根的路径位置（“使用 use 简化路径”至“crate”）。
- `mod user;` 可从 `user.rs` 或 `user/mod.rs` 引入文件模块；Rust 2018 风格可以用 `user.rs` 配合 `user/login.rs`，无需一律写 `mod.rs`（“文件模块结构”至“Rust 2018 新模块方式”）。
- 文章以后台项目展示按领域拆分模块和只暴露必要 API 的思路（“模块最佳实践”至“模块与权限设计”）。

## 与既有知识的关系

- 与 [[rust-project-layout-clipping]]、[[cargo-guide-clipping]] 互补；接续 [[rust-error-handling-best-practices-clipping]]。学习顺序见 [[rust-programming-basics]]。
- 待验证：示例未在本次摄入时编译。原文把 `crate` 说成“项目根模块/项目根目录”，更精确的语义是当前 **crate** 的根；同一个 package 或 workspace 可能有多个 crate。模块的 `pub` 可达性还受祖先模块可见性约束。

## 由本来源派生 / 更新的页面

- [[rust-programming-basics]]。
