---
title: "Rust 文档生成详解：使用 rustdoc 与 cargo doc 编写 API 文档"
type: source
created: 2026-11-05
updated: 2026-11-05
tags: [rust, rust-basics, documentation, testing]
status: growing
author: "程序员爱钓鱼（剪藏正文署名；作者身份待验证）"
source_url: "https://mp.weixin.qq.com/s?__biz=MzYzODE1NzUzMw==&mid=2247484531&idx=1&sn=b3f001e30a06aac48bdb528262811a3b&chksm=f0e753c1c790dad7d434bf80ba2907cfa5ffd676959bc2871cc39fe257f14a9125192b526d34&cur_album_id=4602071361631748097&scene=189#wechat_redirect"
raw_file: "raw/Rust 文档生成详解：使用 rustdoc 与 cargo doc 编写 API 文档.md"
format: article
---

# Rust 文档生成详解：使用 rustdoc 与 cargo doc 编写 API 文档

## 来源信息

- 《Rust 编程实战》第 28 篇；正文显示 2026-08-02，剪藏于 2026-11-05。原文件的 `author`、`published` 字段为空；署名及日期未在线核对。
- 原文：`raw/Rust 文档生成详解：使用 rustdoc 与 cargo doc 编写 API 文档.md`；网页地址见 frontmatter。

## 一句话概括

介绍 `///`、`//!` 文档注释、rustdoc 的 HTML 输出，以及可编译的文档示例与 doctest。

## 核心要点

- `///` 描述下一项，`//!` 描述当前模块或 crate；文档注释可写 Markdown、代码块及内部链接（“普通注释与文档注释”至“文档注释支持 Markdown”、“文档中的链接”）。
- `cargo doc` 生成 HTML；`--open` 打开结果，`--no-deps` 跳过依赖文档，`--document-private-items` 包含私有项（“生成项目文档”至“生成私有内容文档”）。
- `cargo test` 可执行文档中的 Rust 示例；隐藏行 `#` 参与测试，`no_run` 编译但不运行，`compile_fail` 验证不能编译的示例（“文档测试 Doctest”至“标记不运行的代码”）。
- 公共 API 的说明应涵盖行为、错误和 panic 边界，并让示例随 API 更新（“为函数编写完整文档”、“Rust 文档最佳实践”）。

## 与既有知识的关系

- 接续 [[rust-use-pub-clipping]]，与 [[rust-comments-rustdoc-clipping]] 交叉；后续是 [[rust-unit-testing-clipping]]。学习路径见 [[rust-programming-basics]]。
> [!warning] 矛盾
> 本文“为函数编写完整文档”和“实战：为数学工具库生成文档”对除数为零返回 `Result::Err`；[[rust-error-handling-best-practices-clipping]] 的“3. 程序逻辑错误使用 panic”却直接为同类除零情况调用 `panic!`。需按输入来源和函数契约判断；两篇原说法不能合成一条无条件规则。

- 待验证：文中 `add(...)`、`safe_divide(...)` 的若干 doctest 片段没有导入 crate 路径，不能因展示为代码块就认定可编译；内部链接示例提及未在同片段定义的 `User::disable`。本次未运行 `cargo test` / `cargo doc`；网页署名和发表时间未在线核对。

## 由本来源派生 / 更新的页面

- [[rust-programming-basics]]、[[rust-error-handling-best-practices-clipping]]。
