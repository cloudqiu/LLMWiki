---
title: "Cargo 包管理器详解：Rust 开发必会工具"
type: source
created: 2026-11-03
updated: 2026-11-03
tags: [rust, rust-basics]
status: growing
author: "程序员爱钓鱼（剪藏正文署名；作者身份待验证）"
source_url: "https://mp.weixin.qq.com/s?__biz=MzYzODE1NzUzMw==&mid=2247484415&idx=1&sn=aeadd7a178b9b0bce99bdb7bdd9e7c4b&chksm=f0e7544dc790dd5b68e6febaf33003d770a72f23ff5ab711517cee116cb15371d18448410b15&cur_album_id=4602071361631748097&scene=189#wechat_redirect"
raw_file: "raw/Cargo 包管理器详解：Rust 开发必会工具.md"
format: article
---

# Cargo 包管理器详解：Rust 开发必会工具

## 来源信息

- 作者 / 出处：剪藏正文署名“程序员爱钓鱼”；《Rust 编程实战》系列第 4 篇。原文件 frontmatter 的 author、published 为空。
- 发表时间：正文显示 2026-07-09；未与网页在线核对。剪藏创建于 2026-11-03。
- 本地原文：`raw/Cargo 包管理器详解：Rust 开发必会工具.md`；[网页原址](https://mp.weixin.qq.com/s?__biz=MzYzODE1NzUzMw==&mid=2247484415&idx=1&sn=aeadd7a178b9b0bce99bdb7bdd9e7c4b&chksm=f0e7544dc790dd5b68e6febaf33003d770a72f23ff5ab711517cee116cb15371d18448410b15&cur_album_id=4602071361631748097&scene=189#wechat_redirect)。

## 一句话概括

汇总 Cargo 的项目创建、依赖、构建、测试、文档、格式化、检查和发布命令。

## 核心要点

- 比较 `cargo new` 和 `cargo new --lib`，并介绍 manifest 的 package/dependencies 区（“创建项目”、“创建库项目”、“Cargo.toml”）。
- 依次介绍 run、build、check、test、clean、doc、fmt、clippy、add 与 publish 的用途（“Cargo 常用命令”至“Cargo 发布项目”）。
- 区分依赖声明 `Cargo.toml` 和依赖解析锁定文件 `Cargo.lock`，给出常见开发流程（“Cargo.lock”、“Cargo 工作流程”）。

## 与既有知识的关系

- 关联：[[rust-programming-basics]], [[rust-project-layout-clipping]]。
- 待验证：`Cargo.lock` 记录解析出的依赖版本，不等同于机器上“实际安装了什么”；`cargo add` 的可用方式与版本、缓存目录及命令选项应以当前 Cargo 官方文档核对。代码命令未在本次摄入时运行。

## 由本来源派生 / 更新的页面

- [[rust-programming-basics]]。
