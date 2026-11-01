# anyhow_ext 官方资料查阅记录

> 2026-11-01 查阅。本文为 Codex 根据 crate 官方发布文档整理的研究笔记，并非官方原文副本；示例未在本机运行。

## 名称与版本

- 收件箱名称：anyhow_ext。
- 已核实 crate：`anyhow_ext`，docs.rs 显示版本 0.2.1；目标项目须以 Cargo.lock 核对实际使用版本。
- [官方发布文档](https://docs.rs/anyhow_ext/latest/anyhow_ext/)；[crates.io 包页](https://crates.io/crates/anyhow_ext)。查阅日期：2026-11-01。

## 用途

在 anyhow 错误链中添加源码位置与简短回溯。

## 典型入口

```rust
use anyhow_ext::{Context, Result};
fn read() -> Result<String> { Ok(std::fs::read_to_string("config.txt").dot()?) }
```

以上仅为按官方 API 整理的最小片段，可能需要外层函数、依赖或平台条件；未编译运行。

## 身份与边界

- 发布文档可验证 crate 用途与公开 API，但单凭包所有者、仓库归属或发布账号不能确认个人创建者与当前维护者；两者待验证。
- 具体 feature、平台要求和兼容版本须按目标项目锁定的版本核对。
