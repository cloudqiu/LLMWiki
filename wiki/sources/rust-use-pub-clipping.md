---
title: "Rust use 与 pub 详解：模块导入与权限控制"
type: source
created: 2026-11-05
updated: 2026-11-05
tags: [rust, rust-basics, modules, visibility]
status: growing
author: "程序员爱钓鱼（剪藏正文署名；作者身份待验证）"
source_url: "https://mp.weixin.qq.com/s?__biz=MzYzODE1NzUzMw==&mid=2247484527&idx=1&sn=dbf965d54444ce552e00827c4944efbd&chksm=f0e753ddc790dacbf413264c45a2264d82fc6cfc9db5a2c2690ecaa370c8448f4a015b7245f3&cur_album_id=4602071361631748097&scene=189#wechat_redirect"
raw_file: "raw/Rust use 与 pub 详解：模块导入与权限控制.md"
format: article
---

# Rust use 与 pub 详解：模块导入与权限控制

## 来源信息

- 《Rust 编程实战》第 27 篇；正文显示 2026-08-01，剪藏于 2026-11-05。原文件的 `author`、`published` 字段为空；署名及日期未在线核对。
- 原文：`raw/Rust use 与 pub 详解：模块导入与权限控制.md`；网页地址见 frontmatter。

## 一句话概括

解释 `use` 的路径绑定、`pub` 的可见性范围和 `pub use` 的公开 API 重新导出。

## 核心要点

- `use` 将路径绑定引入当前作用域；可以导入项、使用分组路径与 `as` 别名。glob 导入在较大模块中容易造成名称冲突（“use 的作用”至“使用 as 重命名”）。
- 子项及结构体字段默认私有；`pub`、`pub(crate)`、`pub(super)`、`pub(in path)` 分别控制不同范围，公开项的可达性还取决于祖先模块路径（“什么是 pub？”至“pub(in path)”）。
- `pub use` 可以从私有内部模块重新导出公开类型或函数，减少调用方对文件布局的依赖（“use 与 pub 结合”至“实战：设计公共 API”）。
- 文章建议默认保持私有，只公开稳定的业务接口（“常见错误”至“Rust 模块设计原则”）。

## 与既有知识的关系

- 细化 [[rust-module-clipping]] 和 [[rust-package-crate-clipping]] 的模块路径与公开 API 设计；学习路径见 [[rust-programming-basics]]。
- 待验证：示例未在本次摄入时编译。“导入模块”中的 `mod user { ... }` 与 crate 根的 `use user;` 同名，可能造成重复定义；`pub use model::User` 示例将 `model` 设为私有，因此文中所谓外部“原来 `user::model::User`”并不是可用的公开路径。实战示例的 `lib.rs` 须实际声明并公开 `user` 模块，原文目录图未展示该行。

## 由本来源派生 / 更新的页面

- [[rust-programming-basics]]。
