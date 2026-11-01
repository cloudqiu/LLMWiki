# autocfg 官方资料查阅记录

> 2026-11-01 查阅。本文为 Codex 根据 crate 官方发布文档整理的研究笔记，并非官方原文副本；示例未在本机运行。

## 名称与版本

- 收件箱名称：autocfg。
- 已核实 crate：`autocfg`，docs.rs 显示版本 1.5.1；目标项目须以 Cargo.lock 核对实际使用版本。
- [官方发布文档](https://docs.rs/autocfg/latest/autocfg/)；[crates.io 包页](https://crates.io/crates/autocfg)。查阅日期：2026-11-01。

## 用途

在 build.rs 中检测 rustc 功能并发出 cfg。

## 典型入口

```rust
let ac = autocfg::new();
ac.emit_has_type("i128");
```

以上仅为按官方 API 整理的最小片段，可能需要外层函数、依赖或平台条件；未编译运行。

## 身份与边界

- 发布文档可验证 crate 用途与公开 API，但单凭包所有者、仓库归属或发布账号不能确认个人创建者与当前维护者；两者待验证。
- 具体 feature、平台要求和兼容版本须按目标项目锁定的版本核对。
