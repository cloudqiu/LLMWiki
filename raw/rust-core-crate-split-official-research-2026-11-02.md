# Rust crate 的 -core 拆分：time 例证查阅记录

> 2026-11-02 查阅。本文为官方文档和仓库配置的研究笔记，不是官方原文副本。

## 官方依据

- [Cargo Workspaces](https://doc.rust-lang.org/cargo/reference/workspaces.html)：workspace 管理多个 package，共享 lockfile、构建目录和配置；它本身不决定公开 API 边界。
- [Rust Reference: Procedural macros](https://doc.rust-lang.org/reference/procedural-macros.html)：过程宏必须定义在 `proc-macro` 类型 crate 中。
- [time 仓库根 Cargo.toml](https://github.com/time-rs/time/blob/main/Cargo.toml)：workspace 成员包括 `time`、`time-core`、`time-macros`。
- [time/Cargo.toml](https://github.com/time-rs/time/blob/main/time/Cargo.toml)：`time-core` 是普通依赖；`time-macros` 是可选依赖，由 `macros` feature 启用；`large-dates` feature 传给 `time-core`。
- [time-macros/Cargo.toml](https://github.com/time-rs/time/blob/main/time-macros/Cargo.toml)：声明 `proc-macro = true`，并依赖 `time-core`。2026-11-02 直接核对 main 分支，版本字段为 0.2.32。
- [time-core 文档](https://docs.rs/time-core/latest/time_core/)：说明它是 `time` 的实现细节，不建议直接依赖；公开模块含 `unit` 与 `util`。

## 推论边界

- 就 `time` 而言，`time-core` 在普通库与过程宏之间放置共用基础组件，是从实际依赖关系推得的设计作用。不能据此断言所有 `-core` crate 都有同样目的。
- `-core` 是项目命名约定，不等同于 Rust 标准库 `core`，也不自动保证 `no_std`、小体积或稳定公共 API。
