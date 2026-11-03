---
title: "Rust 函数与返回值详解：参数、表达式与返回类型"
type: source
created: 2026-11-03
updated: 2026-11-03
tags: [rust, rust-basics]
status: growing
author: "程序员爱钓鱼（剪藏正文署名；作者身份待验证）"
source_url: "https://mp.weixin.qq.com/s?__biz=MzYzODE1NzUzMw==&mid=2247484435&idx=1&sn=61713186a75582aaa9d6630a4554aafb&chksm=f0e753a1c790dab7a623218a0e0945f61048a93265ddd62d9fa0bbfa7768e50fec63e01a94d5&cur_album_id=4602071361631748097&scene=189#wechat_redirect"
raw_file: "raw/Rust 函数与返回值详解：参数、表达式与返回类型.md"
format: article
---

# Rust 函数与返回值详解：参数、表达式与返回类型

## 来源信息

- 作者 / 出处：剪藏正文署名“程序员爱钓鱼”；《Rust 编程实战》系列第 9 篇。原文件 frontmatter 的 author、published 为空。
- 发表时间：正文显示 2026-07-14；未与网页在线核对。剪藏创建于 2026-11-03。
- 本地原文：`raw/Rust 函数与返回值详解：参数、表达式与返回类型.md`；[网页原址](https://mp.weixin.qq.com/s?__biz=MzYzODE1NzUzMw==&mid=2247484435&idx=1&sn=61713186a75582aaa9d6630a4554aafb&chksm=f0e753a1c790dab7a623218a0e0945f61048a93265ddd62d9fa0bbfa7768e50fec63e01a94d5&cur_album_id=4602071361631748097&scene=189#wechat_redirect)。

## 一句话概括

解释函数参数类型、表达式返回、`return`、`if` 表达式、单元类型及元组返回。

## 核心要点

- 函数参数需类型标注；返回类型用 `->` 指定，尾表达式不加分号时可作为返回值（“函数参数”、“函数返回值”、“为什么返回值后面没有分号？”）。
- 区分语句和表达式；代码块及 `if` 可产生值，各分支须满足类型要求（“语句与表达式”至“if 各分支类型必须一致”）。
- 说明 `return` 提前返回、`()` 单元类型、元组返回多个字段及参数绑定 `mut`（相应小节）。

## 与既有知识的关系

- 关联：[[rust-programming-basics]], [[rust-variables-mutability-clipping]]。
- 待验证：文中价格计算使用 `f64` 仅作语法练习，涉及真实金额时还需另行考虑精度；示例未在本次摄入时编译运行。

## 由本来源派生 / 更新的页面

- [[rust-programming-basics]]。
