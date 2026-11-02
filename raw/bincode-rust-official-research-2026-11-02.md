# bincode 官方资料查阅记录

> 2026-11-02 查阅 crates.io 官方包元数据；本文为研究笔记，不是官方原文副本。API 示例未在本机运行。

## 名称与版本

- 收件箱名称：`bincode`。
- crates.io 发布名：`bincode`；显示稳定版本：3.0.0。项目实际版本以 Cargo.lock 为准。
- [官方包页](https://crates.io/crates/bincode)；[注册表 API](https://crates.io/api/v1/crates/bincode)；[3.0.0 发布页](https://docs.rs/crate/bincode/3.0.0)。

## 用途

- 官方英文摘要：A binary serialization / deserialization strategy for transforming structs into bytes and vice versa!
- 中文概括：此 crate 提供上述功能；更具体的适用场景与 API 入口待依据发布文档核实。

## 典型入口

- 3.0.0 仅含停止维护说明和编译错误，不能作为可用序列化 API；已有项目需核对锁定版本，旧版本示例待核实。

## 身份与边界

- 官方元数据列出的仓库：https://github.com/bincode-org/bincode。仓库归属不等于创建者或完整维护者名单。
- 创建者、当前维护者：待官方证据核实。
- [3.0.0 发布页](https://docs.rs/crate/bincode/3.0.0) 明确称项目停止维护，且该版 lib.rs 只有编译错误；不能仅凭 crates.io 摘要推断最新版本可用。
