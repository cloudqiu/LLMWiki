# arrayvec 官方资料查阅记录

> 2026-11-02 查阅 docs.rs 发布文档；本文为研究笔记，并非官方原文副本。示例尚未编译运行。

## 名称与版本

- 收件箱名称：`arrayvec`。
- docs.rs 显示版本：0.7.8；项目实际版本须按 Cargo.lock 核对。
- 官方发布文档：https://docs.rs/arrayvec/latest/arrayvec/

## 用途

提供以内联数组存储内容的 ArrayVec 与 ArrayString。

## 典型入口

- 安装：`cargo add arrayvec`。
- 公开 API 与可运行示例需继续按锁定版本补核；本页暂不提供未经核实的调用片段。

## 身份与边界

- 创建者与当前维护者：待官方身份依据核实；不能仅凭发布账号推断。
- 容量固定；超出容量时需按 API 处理。
