# smol Rust 官方资料查阅记录（2026-11-04）

本文件是对官方页面的查阅笔记，不是官网原文副本。收件箱输入：`raw/rust-libs-inbox.md` 中的 `smol`；未改动收件箱。

## 查阅资料

- smol 2.0.2 API 文档：https://docs.rs/smol/2.0.2/smol/
- smol 官方仓库与 README：https://github.com/smol-rs/smol
- smol 官方 manifest：https://github.com/smol-rs/smol/blob/master/Cargo.toml
- async-executor 官方 manifest：https://github.com/smol-rs/async-executor/blob/master/Cargo.toml
- async-std 发布文档：https://docs.rs/async-std/latest/async_std/

## 版本与能力

- 查阅时 docs.rs 提供 smol 2.0.2 文档，仓库 manifest 也标注 2.0.2；实际项目依赖版本以 Cargo.lock 为准。
- 官方文档称 smol 为小型异步运行时，主要重新导出更小的 async crates；公开 `block_on`、`spawn`、`Executor`、网络、I/O、文件系统、计时器等 API。
- 官方文档的 HTTP 示例用 `smol::block_on` 驱动 `smol::net::TcpStream` 与异步写入。`spawn` 文档摘要注明全局执行器默认单线程；需要多线程设置可看 `smol-macros` 或自定义 Executor。
- 官方 README 要求 Tokio 库与 smol 配合时，对 future 与 I/O 类型使用 `async-compat` 适配器。不能仅凭两者都用标准 Future 就假定 I/O 兼容。
- 当前仓库 README 的 MSRV 政策及 manifest `rust-version` 均指向 Rust 1.85；这是查阅时的仓库状态，目标版本需按实际依赖核对。

## 作者与维护证据

- smol 官方 manifest `authors` 明确写 `Stjepan Glavina <stjepang@gmail.com>`。这支持其为 manifest 署名作者；不能单凭该字段确定独立创建者或现任维护者。
- 已摄入的 async-executor 官方 manifest 同样把 Stjepan Glavina 列为作者，另列 John Nunley；因此可在 Stjepan 的作者页关联此已摄入库，但不据此推断其现任维护角色。
- smol-rs 仓库归属只说明组织托管，不足以确定个人或组织的当前维护职责。创建者的具体角色与当前维护者均待验证。

## 示例核对与限制

- `smol = "2"` 可作为 Cargo.toml 依赖声明；`smol::block_on(async { ... })` 与 `smol::spawn(async { ... })` 对应官方公开 API。本文及派生库页的示例未在本机编译运行。
- 官方项目示例涉及 HTTP 明文连接；不能把该示例误当 TLS/HTTPS 客户端。
- async-std 发布文档明确写已停止并建议转向 smol；这只支持项目迁移建议，不表示二者 API 完全相同。
