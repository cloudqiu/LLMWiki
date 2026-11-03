---
title: "Rust 编程入门"
type: topic
created: 2026-11-03
updated: 2026-11-03
tags: [rust, rust-basics]
status: growing
sources:
  - "raw/为什么学习 Rust？Rust 能做什么？.md"
  - "raw/Rust 开发环境安装（WindowsmacOSLinux）.md"
  - "raw/第一个 Rust 程序 Hello World.md"
  - "raw/Cargo 包管理器详解：Rust 开发必会工具.md"
  - "raw/Rust 项目目录结构详解：从 Hello World 到企业级项目.md"
  - "raw/Rust 变量与不可变性：为什么默认不能修改变量？.md"
  - "raw/Rust 数据类型详解：整数、浮点数、布尔、字符、元组和数组.md"
  - "raw/Rust 函数与返回值详解：参数、表达式与返回类型.md"
  - "raw/Rust 注释与文档注释详解：从代码说明到 cargo doc.md"
---

# Rust 编程入门

## 概述

《Rust 编程实战》系列已摄入第 1–7、9–10 篇。阅读路径从语言定位与环境安装开始，经过 Hello World、Cargo 和项目结构，再进入变量、基础类型、函数与 rustdoc。第 8 篇（常量与静态变量）尚无原始资料，不能根据前后篇补写。

这些页面归档的是教程作者的讲解。涉及工具链现状、性能、治理和代码正确性时，仍需官方文档或实机验证。

## 学习脉络

1. [[why-learn-rust-clipping|为什么学习 Rust]]：了解作者提出的动机和应用场景。
2. [[rust-installation-clipping|安装]] → [[rust-hello-world-clipping|Hello World]]：准备工具链，认识最小可执行项目。
3. [[cargo-guide-clipping|Cargo]] → [[rust-project-layout-clipping|项目结构]]：区分 manifest、锁文件、构建产物与源文件布局。
4. [[rust-variables-mutability-clipping|变量与不可变性]] → [[rust-data-types-clipping|数据类型]] → [[rust-functions-return-values-clipping|函数与返回值]]：从绑定和类型进入表达式、参数与返回值。
5. [[rust-comments-rustdoc-clipping|注释与 rustdoc]]：为公开 API 写文档并用 doctest 核查示例。

## 与已有知识的连接

- [[rust-interior-mutability]] 补充“绑定不可变”和“内部可变性”的区别；不能把教程中“不可变对象天然线程安全”照搬为通则。
- 本库已有的 Rust crate 实体页可供继续探索第三方依赖；库的 API 用法仍以各自官方证据为准。

## 开放问题

- 第 8 篇原文在哪里？补齐后再接入本学习路径。
- 对安装命令、Cargo 行为与 doctest 示例，按目标工具链版本核对并实际运行。
- 作者关于 Rust Foundation、性能和广泛采用的判断，需要独立可靠证据。

## 来源

- 本页 frontmatter 所列九份 raw 剪藏；各篇的出处、发表日期与证据边界见对应来源页。
