# cfg-if 官方资料查阅记录

> 2026-11-01 查阅。本文为 Codex 根据 crate 官方发布文档整理的研究笔记，并非官方原文副本；示例未在本机运行。

## 名称与版本

- 收件箱名称：cfg-if。
- 已核实 crate：`cfg-if`，docs.rs 显示版本 1.0.5；目标项目须以 Cargo.lock 核对实际使用版本。
- [官方发布文档](https://docs.rs/cfg-if/latest/cfg_if/)；[crates.io 包页](https://crates.io/crates/cfg-if)。查阅日期：2026-11-01。

## 用途

按 cfg 条件选择首个匹配的代码块。

## 典型入口

```rust
cfg_if::cfg_if! { if #[cfg(unix)] { const OS: &str = "unix"; } else { const OS: &str = "other"; } }
```

以上仅为按官方 API 整理的最小片段，可能需要外层函数、依赖或平台条件；未编译运行。

## 身份与边界

- 发布文档可验证 crate 用途与公开 API，但单凭包所有者、仓库归属或发布账号不能确认个人创建者与当前维护者；两者待验证。
- 具体 feature、平台要求和兼容版本须按目标项目锁定的版本核对。
