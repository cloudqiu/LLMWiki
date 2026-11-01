# futures-util 官方资料查阅记录

> 2026-11-01 查阅。本文是 Codex 根据 crate 发布文档整理的研究笔记，并非官方原文副本；示例未在本机运行。

## 名称与版本

- 收件箱名称：`futures-util`。
- docs.rs 显示版本 0.3.34；目标项目须以 Cargo.lock 核对实际使用版本。
- [发布文档](https://docs.rs/futures-util/latest/futures_util/)；[crates.io 包页](https://crates.io/crates/futures-util)。查阅日期：2026-11-01。

## 用途

提供 Future、Stream、Sink 的组合器和扩展 trait。

## 典型入口

```rust
use futures_util::StreamExt;
let values = futures_util::stream::iter([1, 2, 3]).collect::<Vec<_>>().await;
```

以上为根据公开 API 整理的最小片段，可能需要外层函数、依赖或平台条件；未编译运行。

## 身份与边界

- 发布文档可验证用途与公开 API，但包所有者、仓库归属或发布账号不足以确认个人创建者及当前维护者；两者待验证。
- 此 crate 是生态中的组件；直接依赖前核对上层 crate 是否已重导出所需 API。
