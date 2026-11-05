---
title: "Rust Option 详解：安全处理可能缺失的值"
type: source
created: 2026-11-05
updated: 2026-11-05
tags: [rust, rust-basics, error-handling]
status: growing
author: "程序员爱钓鱼（剪藏正文署名；作者身份待验证）"
source_url: "https://mp.weixin.qq.com/s?__biz=MzYzODE1NzUzMw==&mid=2247484494&idx=1&sn=67fe318ff6788ddbcf36e985a7f55215&chksm=f0e753fcc790daea6ed25bd9b55dbe4c004bdc372e73a09971cfe95eec76ddd0c433d980ca92&cur_album_id=4602071361631748097&scene=189#wechat_redirect"
raw_file: "raw/Rust Option 详解：安全处理“可能存在，也可能不存在”的值.md"
format: article
---

# Rust Option 详解：安全处理可能缺失的值

## 来源信息

- 《Rust 编程实战》第 21 篇；正文显示 2026-07-26，剪藏于 2026-11-05。原文件的 `author`、`published` 字段为空；署名及日期未在线核对。
- 原文：`raw/Rust Option 详解：安全处理“可能存在，也可能不存在”的值.md`；网页地址见 frontmatter。

## 一句话概括

用 `Some(T)` / `None` 表达值可能缺失，并展示匹配、默认值、映射与链式处理。

## 核心要点

- `Option<T>` 与 `T` 是不同类型；`match`、`if let` 显式处理 `Some` 和 `None`，适合查找函数与 `Vec::get()` / `HashMap::get()`（“Option 与 T 不同”至“使用 if let 简化 Option”、“使用 Option 查询 Vec”至“使用 Option 查询 HashMap”）。
- `unwrap()` / `expect()` 在 `None` 时 panic；`unwrap_or()`、`unwrap_or_else()` 可提供默认值，后者只在需要时计算（“使用 unwrap() 获取值”至“unwrap_or_else()”）。
- `map()` 转换已有值；`and_then()` 串接仍可能返回 `Option` 的步骤。教程将解析失败经 `.ok()` 转为 `None`，这会丢掉错误原因（“使用 map() 转换 Option”至“使用 and_then()”）。
- 与 [[rust-result-clipping]] 对照：只需表达有无时可用 `Option`，需要携带失败原因时用 `Result`（“Option 和 Result 的区别”）。

## 与既有知识的关系

- 接续 [[rust-hashmap-clipping]]、[[rust-vec-clipping]]；与 [[rust-match-patterns-clipping]]、[[rust-if-let-while-let-clipping]] 互补。学习顺序见 [[rust-programming-basics]]。
- 待验证：示例未在本次摄入时编译；来源署名和发表时间未在线核对。`.ok()` 抹去错误细节，只适合不需区分原因的调用方。

## 由本来源派生 / 更新的页面

- [[rust-programming-basics]]。
