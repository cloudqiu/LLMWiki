# Tokio 系统学习指南：官方资料查阅记录

查阅日期：2026-11-04。本文件是查阅笔记，不是官方文档副本；学习计划和练习验收标准由 Codex 综合设计。

## 官方资料

- Rust Book 异步编程章：https://doc.rust-lang.org/book/ch17-00-async-await.html — Future、async/await 与并发基础。
- Tokio 教程目录：https://tokio.rs/tokio/tutorial — 依次覆盖 setup、Hello Tokio、spawning、shared state、channels、I/O、framing、async in depth、select、streams。
- Tokio 教程 setup：https://tokio.rs/tokio/tutorial/setup — 以 Mini-Redis 客户端和服务端为贯穿项目；建议读者已有 Rust 基础；Mini-Redis 用于教学，不是生产 Redis 库。
- Tokio API 文档：https://docs.rs/tokio/latest/tokio/ — 查阅时显示 1.54.1；`full` 便于入门，但不含 `test-util`，之后可按用到的 API 收窄 features。
- Tokio spawning：https://tokio.rs/tokio/tutorial/spawning 与 https://docs.rs/tokio/latest/tokio/task/fn.spawn.html — `spawn` 的 Future 和输出需满足 `Send + 'static`；任务与线程不同。
- Tokio shared state：https://tokio.rs/tokio/tutorial/shared-state — 简单数据可用短时的 `std::sync::Mutex` 临界区；涉及异步资源的共享更适合专属任务与消息传递；锁跨 `.await` 需特别谨慎。
- Tokio channels：https://tokio.rs/tokio/tutorial/channels — 以通道和资源所有者任务协调多个请求。
- Tokio I/O：https://tokio.rs/tokio/tutorial/io — `AsyncRead` / `AsyncWrite` 与扩展 trait。
- Tokio framing：https://tokio.rs/tokio/tutorial/framing — TCP 字节流到协议帧的边界处理。
- Tokio async in depth：https://tokio.rs/tokio/tutorial/async — Future、poll、waker 与执行模型。
- Tokio select：https://tokio.rs/tokio/tutorial/select 与 https://docs.rs/tokio/latest/tokio/macro.select.html — 同一任务中的分支并发、取消安全；需要并行时使用独立任务。
- Tokio streams：https://tokio.rs/tokio/tutorial/streams — `tokio-stream` 提供流适配；按需学习。
- Tokio runtime：https://docs.rs/tokio/latest/tokio/runtime/ — 多线程与 current-thread 调度器。
- Tokio spawn_blocking：https://docs.rs/tokio/latest/tokio/task/fn.spawn_blocking.html — 将阻塞操作放到允许阻塞的线程；大量 CPU 工作需限制并行度或使用更合适的执行器。
- Tokio graceful shutdown：https://tokio.rs/tokio/topics/shutdown — 停止条件、通知各部分、等待完成三个步骤。
- Tokio testing：https://tokio.rs/tokio/topics/testing — `#[tokio::test]` 和暂停时间；暂停时间需要 `test-util` feature。
- Tokio tracing：https://tokio.rs/tokio/topics/tracing — 为异步程序建立可追踪的事件与 span。
- Tokio bridging：https://tokio.rs/tokio/topics/bridging — 同步代码与 Tokio runtime 的边界。
- Tokio JoinSet：https://docs.rs/tokio/latest/tokio/task/struct.JoinSet.html — 管理一组任务并收集完成结果；集合被 drop 时会 abort 其中任务。

## 与本库的关系

- `raw/tokio-rust-official-research-2026-11-01.md`：此前的 Tokio 包资料和版本记录。
- `raw/Rust 异步生态futures，async_std, tokio.md`：用于理解用户已有问题，但其中对运行时兼容性及 futures 执行器的绝对化论断不能作为官方事实；冲突见 `wiki/concepts/rust-async-runtime-boundaries.md`。

## 版本与验证边界

- 以上网页在 2026-11-04 查阅；学习时以自己项目的 Cargo.lock、对应版本 API 和编译结果为准。
- 本指南里的最小练习代码未在本机编译执行；官方 Mini-Redis 项目也未在本机运行。
