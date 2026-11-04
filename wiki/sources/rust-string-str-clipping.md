---
title: "Rust String 与 &str 详解：字符串所有权、借用与转换"
type: source
created: 2026-11-04
updated: 2026-11-04
tags: [rust, rust-basics, strings]
status: growing
author: "程序员爱钓鱼（剪藏正文署名；作者身份待验证）"
source_url: "https://mp.weixin.qq.com/s?__biz=MzYzODE1NzUzMw==&mid=2247484476&idx=1&sn=077e76194dfa713814aea46146faddc8&chksm=f0e7538ec790da98134be4a345fe7764a3b564a5f219a0ed9b48a750eadcbe7f813014a90087&cur_album_id=4602071361631748097&scene=189#wechat_redirect"
raw_file: "raw/Rust String 与 &str 详解：字符串所有权、借用与转换.md"
format: article
---

# Rust String 与 &str 详解：字符串所有权、借用与转换

## 来源信息

- 作者 / 出处：剪藏正文署名“程序员爱钓鱼”；《Rust 编程实战》系列第 18 篇。原文件 frontmatter 的 author、published 为空。
- 发表时间：正文显示 2026-07-23；未与网页在线核对。剪藏创建于 2026-11-04。
- 本地原文：`raw/Rust String 与 &str 详解：字符串所有权、借用与转换.md`；原始链接见 frontmatter。文末有剪藏带入的商品广告，不作为教程内容。

## 一句话概括

对比拥有 UTF-8 文本的 `String` 与借用文本的 `&str`，说明修改、转换、所有权和字符边界。

## 核心要点

- `String` 可拥有和增长文本；`&str` 借用文本，字符串字面量也是 `&str`。只读函数参数用 `&str` 可接收字面量和 `String` 的借用（“什么是 &str？”至“String 与 &str 的核心区别”、“为什么函数参数优先使用 &str？”）。
- `push()` 添加字符，`push_str()` 添加字符串；`+` 消耗左侧 `String`，而 `format!` 创建新字符串。`String` 赋值会移动所有权，需要独立副本时可 `clone()`（“修改 String”至“使用 format! 拼接”、“String 的所有权移动”至“使用 clone() 复制 String”）。
- 借用或 `as_str()` 可得到 `&str`；`String::from()`、`to_string()`、`to_owned()` 可从 `&str` 创建 `String`（“借用 String”至“&str 转换为 String”）。
- `len()` 返回 UTF-8 字节数，不能用 `text[0]` 取得字符；`chars()` 遍历 Unicode 标量值，`bytes()` 遍历字节。字符串切片必须落在合法 UTF-8 边界（“获取字符串长度”至“字符串切片与 UTF-8 边界”）。

## 与既有知识的关系

- 关联：[[rust-programming-basics]]、[[rust-slice-clipping]]、[[rust-vec-clipping]]。
- 待验证：代码示例未在本次摄入时编译运行；正文署名和发表时间未在线核对。`chars()` 不保证按用户感知的字形簇分割，且示例中的 CSV 式 `split(',')` 不处理引号或转义（“实战：解析商品数据”）。

## 由本来源派生 / 更新的页面

- [[rust-programming-basics]]、[[rust-slice-clipping]]。
