# async-channel 官方资料查阅记录

> 2026-11-02 查阅 docs.rs 发布文档；本文为研究笔记，并非官方原文副本。示例尚未编译运行。

## 名称与版本

- 收件箱名称：`async-channel`。
- docs.rs 显示版本：2.5.0；项目实际版本须按 Cargo.lock 核对。
- 官方发布文档：https://docs.rs/async-channel/latest/async_channel/

## 用途

异步多生产者多消费者 channel，每条消息由一个接收者取得。

## 典型入口

- 安装：`cargo add async-channel`。
- 公开 API 与可运行示例需继续按锁定版本补核；本页暂不提供未经核实的调用片段。

## 身份与边界

- 创建者与当前维护者：待官方身份依据核实；不能仅凭发布账号推断。
- 有界与无界 channel 的容量和背压行为不同。
