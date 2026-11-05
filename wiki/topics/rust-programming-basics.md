---
title: "Rust 编程入门"
type: topic
created: 2026-11-03
updated: 2026-11-05
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
  - "raw/Rust 控制流 if 详解：条件判断与 if 表达式.md"
  - "raw/Rust 循环详解：loop、while 与 for.md"
  - "raw/Rust match 模式匹配详解：比 if 更强大的条件分支.md"
  - "raw/Rust if let 与 while let 详解：简化模式匹配.md"
  - "raw/Rust 数组 Array 详解：定义、访问、遍历与切片.md"
  - "raw/Rust 元组 Tuple 详解：组合不同类型的数据.md"
  - "raw/Rust 切片 Slice 详解：安全访问连续数据.md"
  - "raw/Rust String 与 &str 详解：字符串所有权、借用与转换.md"
  - "raw/Rust Vec 动态数组详解：创建、增删、遍历与排序.md"
  - "raw/Rust HashMap 详解：键值存储、查询、更新与统计.md"
  - "raw/Rust Option 详解：安全处理“可能存在，也可能不存在”的值.md"
  - "raw/Rust Result 详解：可靠的错误处理机制.md"
  - "raw/Rust 错误处理最佳实践：构建可靠的应用程序.md"
  - "raw/Rust Module 模块系统详解：组织大型项目代码.md"
  - "raw/Rust Package 与 Crate 详解：理解 Rust 项目的基本组成.md"
  - "raw/Rust use 与 pub 详解：模块导入与权限控制.md"
---

# Rust 编程入门

## 概述

《Rust 编程实战》系列已摄入第 1–7、9–22、24–27 篇。阅读路径从语言定位与环境安装开始，经过 Hello World、Cargo 和项目结构，再进入变量、基础类型、函数、rustdoc、控制流与模式匹配，接着学习数组、元组、切片、字符串、`Vec`、`HashMap`、可选值与错误处理，最后进入模块、package、crate 和公开 API 的组织。第 8 篇（常量与静态变量）和第 23 篇（panic）尚无原始资料，不能根据前后篇补写。

这些页面归档的是教程作者的讲解。涉及工具链现状、性能、治理和代码正确性时，仍需官方文档或实机验证。

## 学习脉络

1. [[why-learn-rust-clipping|为什么学习 Rust]]：了解作者提出的动机和应用场景。
2. [[rust-installation-clipping|安装]] → [[rust-hello-world-clipping|Hello World]]：准备工具链，认识最小可执行项目。
3. [[cargo-guide-clipping|Cargo]] → [[rust-project-layout-clipping|项目结构]]：区分 manifest、锁文件、构建产物与源文件布局。
4. [[rust-variables-mutability-clipping|变量与不可变性]] → [[rust-data-types-clipping|数据类型]] → [[rust-functions-return-values-clipping|函数与返回值]]：从绑定和类型进入表达式、参数与返回值。
5. [[rust-comments-rustdoc-clipping|注释与 rustdoc]]：为公开 API 写文档并用 doctest 核查示例。
6. [[rust-if-control-flow-clipping|if]] → [[rust-loops-clipping|循环]]：用条件分支与三种循环组织控制流；注意短路、分支次序、退出和范围边界。
7. [[rust-match-patterns-clipping|match]] → [[rust-if-let-while-let-clipping|if let / while let]]：从穷尽式匹配走向单分支和持续匹配；明确未处理分支及容器取值顺序。
8. [[rust-array-clipping|数组]] → [[rust-tuple-clipping|元组]] → [[rust-slice-clipping|切片]]：比较固定长度同类型数据与固定位置混合类型数据；用切片借用数组、`Vec` 或字符串的一部分，注意范围和 UTF-8 字节边界。
9. [[rust-string-str-clipping|String / &str]] → [[rust-vec-clipping|Vec]]：区分拥有与借用、复制与移动；对动态文本和动态集合分别学习增长、访问、容量及迭代。
10. [[rust-hashmap-clipping|HashMap]] → [[rust-option-clipping|Option]]：按键组织、查询和更新数据，理解 `get()` 返回可选引用；缺失值通过匹配或组合子处理。
11. [[rust-result-clipping|Result]] → [[rust-error-handling-best-practices-clipping|错误处理实践]]：让错误携带原因，以 `?` 传播并设计分层错误；第 23 篇 panic 原文仍缺。
12. [[rust-module-clipping|Module]]：用 `mod`、路径和可见性组织多文件项目；区分 crate 根与 package/workspace。
13. [[rust-package-crate-clipping|Package 与 Crate]] → [[rust-use-pub-clipping|use 与 pub]]：认识 Cargo package、编译 target 与 workspace，再设计模块可见性和 `pub use` 对外接口。

## 与已有知识的连接

- [[rust-interior-mutability]] 补充“绑定不可变”和“内部可变性”的区别；不能把教程中“不可变对象天然线程安全”照搬为通则。
- 本库已有的 Rust crate 实体页可供继续探索第三方依赖；库的 API 用法仍以各自官方证据为准。

> [!warning] 矛盾
> [[rust-error-handling-best-practices-clipping]] 把除数为零直接用作 `panic!` 示例，同篇又要求可预期的用户输入错误使用 `Result`。应按输入来源与函数契约判断，不能把除零一律当作内部逻辑错误。

## 开放问题

- 第 8 篇原文在哪里？补齐后再接入本学习路径。
- 第 23 篇 panic 原文尚缺；补齐后核对它与第 24 篇的错误边界。
- 对安装命令、Cargo 行为与 doctest 示例，按目标工具链版本核对并实际运行。
- 第 11 篇的订单输出先写 96.00 后更正为 106.00；第 12 篇预计算的循环条件不可当作动态条件；第 14 篇 let chain 需按目标工具链版本核对。
- 第 15–17 篇的示例尚未编译运行；尤其需要复核数组遍历的所有权影响、切片范围越界行为及 UTF-8 字符边界。
- 第 18–19 篇示例尚未编译运行；`chars()` 返回 Unicode 标量值而非完整字形簇，`partial_cmp(...).unwrap()` 不能直接用于可能含 `NaN` 的数据。
- 第 20–22、24–25 篇的示例未在本次摄入时编译；特别核对错误层的 `?` 转换、`thiserror` / `anyhow` 版本、`crate` 根的含义和日志敏感字段。
- 第 26–27 篇的示例未在本次摄入时编译；workspace member 是 package 而不必只有一个 crate，`use user;` 的同名导入、私有 `model` 的所谓原公开路径及实战中缺少 `pub mod user;` 均需复核。
- 作者关于 Rust Foundation、性能和广泛采用的判断，需要独立可靠证据。

## 来源

- 本页 frontmatter 所列二十五份 raw 剪藏；各篇的出处、发表日期与证据边界见对应来源页。
