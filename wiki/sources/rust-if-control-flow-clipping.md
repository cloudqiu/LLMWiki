---
title: "Rust 控制流 if 详解：条件判断与 if 表达式"
type: source
created: 2026-11-03
updated: 2026-11-03
tags: [rust, rust-basics, control-flow]
status: growing
author: "程序员爱钓鱼（剪藏正文署名；作者身份待验证）"
source_url: "https://mp.weixin.qq.com/s?__biz=MzYzODE1NzUzMw==&mid=2247484443&idx=1&sn=611794f33130565158a37c73024c8a19&chksm=f0e753a9c790dabf18fe78cc3b54812cfbfa10a0351b763d3191288104b9b6c8b2fefcf51282&cur_album_id=4602071361631748097&scene=189#wechat_redirect"
raw_file: "raw/Rust 控制流 if 详解：条件判断与 if 表达式.md"
format: article
---

# Rust 控制流 if 详解：条件判断与 if 表达式

## 来源信息

- 作者 / 出处：剪藏正文署名“程序员爱钓鱼”；《Rust 编程实战》系列第 11 篇。原文件 frontmatter 的 author、published 为空。
- 发表时间：正文显示 2026-07-16；未与网页在线核对。剪藏创建于 2026-11-03。
- 本地原文：`raw/Rust 控制流 if 详解：条件判断与 if 表达式.md`；[网页原址](https://mp.weixin.qq.com/s?__biz=MzYzODE1NzUzMw==&mid=2247484443&idx=1&sn=611794f33130565158a37c73024c8a19&chksm=f0e753a9c790dabf18fe78cc3b54812cfbfa10a0351b763d3191288104b9b6c8b2fefcf51282&cur_album_id=4602071361631748097&scene=189#wechat_redirect)。

## 一句话概括

解释 `if`、`else if`、布尔条件、逻辑运算与 `if` 表达式，并用订单计算展示条件顺序。

## 核心要点

- `if` 和 `while` 的条件须为 `bool`；`else if` 自上而下选择首个成立分支（“条件必须是 bool 类型”、“条件顺序很重要”）。
- `&&`、`||` 有短路行为；`if` 可作为表达式，分支结果须有兼容类型（“短路求值”、“if 是表达式”）。
- 以提前返回减少嵌套；订单例子说明先折扣再判断免邮会改变结果（“减少过深嵌套”、“完整练习”）。

## 与既有知识的关系

- 关联：[[rust-programming-basics]], [[rust-functions-return-values-clipping]], [[rust-loops-clipping]]。
- 待验证：“完整练习”先列 `订单实付：96.00`，随后正文自行更正为 `106.00`；按给定代码与规则应为 106.00，不能引用前一结果。金额使用 `f64` 仅作语法演示，示例未实机运行。

## 由本来源派生 / 更新的页面

- [[rust-programming-basics]]。
