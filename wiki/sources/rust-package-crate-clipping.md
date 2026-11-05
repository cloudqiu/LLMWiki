---
title: "Rust Package 与 Crate 详解：理解 Rust 项目的基本组成"
type: source
created: 2026-11-05
updated: 2026-11-05
tags: [rust, rust-basics, cargo, modules]
status: growing
author: "程序员爱钓鱼（剪藏正文署名；作者身份待验证）"
source_url: "https://mp.weixin.qq.com/s?__biz=MzYzODE1NzUzMw==&mid=2247484520&idx=1&sn=3f4eba0e88425fca2353c5e0eb8e5b44&chksm=f0e753dac790dacc0e8a3d024eeedde6f2f3b723da79cc81504ba3eea4d444df54708abbb2fa&cur_album_id=4602071361631748097&scene=189#wechat_redirect"
raw_file: "raw/Rust Package 与 Crate 详解：理解 Rust 项目的基本组成.md"
format: article
---

# Rust Package 与 Crate 详解：理解 Rust 项目的基本组成

## 来源信息

- 《Rust 编程实战》第 26 篇；正文显示 2026-07-31，剪藏于 2026-11-05。原文件的 `author`、`published` 字段为空；署名及日期未在线核对。
- 原文：`raw/Rust Package 与 Crate 详解：理解 Rust 项目的基本组成.md`；网页地址见 frontmatter。

## 一句话概括

区分 Cargo package、Rust crate 与 module，并展示单 package 多 target 和 workspace 的项目布局。

## 核心要点

- crate 是 Rust 编译单元，主要分 binary 和 library；`src/main.rs` 与 `src/lib.rs` 分别可作为默认的 binary / library crate 根（“什么是 Crate？”至“Crate 的两种类型”）。
- package 由 `Cargo.toml` 描述，可以包含多个 binary crate 和至多一个 library crate；`src/bin/*.rs` 增加 binary target，`cargo run --bin` 选择运行目标（“什么是 Package？”至“一个 Package 多个 Crate”）。
- `lib.rs` 与 `main.rs` 可共存，把可复用逻辑放在 library target；workspace 则将多个 member package 放在共同的 Cargo 配置下（“Library + Binary 组合项目”至“什么是 Workspace？”）。
- 文章给出 `cargo package` / `cargo publish` 的发布路径，以及路径依赖的示意项目（“发布 Rust 库”至“实战：创建一个工具库”）。

## 与既有知识的关系

- 接续 [[rust-module-clipping]]；与 [[cargo-guide-clipping]]、[[rust-project-layout-clipping]] 互补。学习路径见 [[rust-programming-basics]]。
- 待验证：示例未在本次摄入时编译，发布命令也未执行。原文“每个 workspace member 都是独立 Crate”是教学简化：member 是 package，package 可包含多个 crate；“`src/bin` 或配置”也不能使额外的 `lib2.rs` 自动成为第二个 library target。文中的 package、crate、module 树形图只适合入门示意，不能代替 Cargo target 规则。

## 由本来源派生 / 更新的页面

- [[rust-programming-basics]]。
