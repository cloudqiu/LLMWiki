---
title: "Rust 项目目录结构详解：从 Hello World 到企业级项目"
source: "https://mp.weixin.qq.com/s?__biz=MzYzODE1NzUzMw==&mid=2247484419&idx=1&sn=2441030ef1f0487331fd1db2da6e2ccb&chksm=f0e753b1c790daa73d2ff17f215bf32af430a7c77b1fcd6016f1bfd7bf89aff2a5632e4ac800&cur_album_id=4602071361631748097&scene=189#wechat_redirect"
author:
published:
created: 2026-11-03
description: "《Rust 编程实战》系列第 5 篇在上一篇文章中，我们学习了 Cargo 包管理器，知道了如何创建 Rus"
tags:
  - "clippings"
---
程序员爱钓鱼 *Jul 10, 2026, 8:28 AM*

> 《Rust 编程实战》系列第 5 篇

在上一篇文章中，我们学习了 Cargo 包管理器，知道了如何创建 Rust 项目、管理依赖以及编译程序。

不过，当我们执行 `cargo new` 创建项目后，会发现 Rust 项目的目录非常简单，甚至比很多语言都要简洁。

那么：

- • 每个文件夹有什么作用？
- • `main.rs` 和 `lib.rs` 有什么区别？
- • `src` 为什么如此重要？
- • 企业级 Rust 项目又是如何组织目录的？

本文将带你全面了解 Rust 项目的目录结构。

---

## 创建一个新项目

首先创建一个新的 Rust 项目：

```
cargo new hello_rust
```

进入项目目录：

```
cd hello_rust
```

查看目录结构：

```
hello_rust
├── Cargo.toml
├── Cargo.lock
├── src
│   └── main.rs
└── target
```

其中：

| 文件 | 作用 |
| --- | --- |
| Cargo.toml | 项目配置文件 |
| Cargo.lock | 依赖锁定文件 |
| src | 源代码目录 |
| target | 编译输出目录 |

刚创建项目时：

- • 没有 Cargo.lock（第一次编译后生成）
- • 没有 target（第一次编译后生成）

---

## Cargo.toml

整个 Rust 项目的核心。

例如：

```
[package]
name = "hello_rust"
version = "0.1.0"
edition = "2024"

[dependencies]
```

Cargo 会根据这里的信息：

- • 下载依赖
- • 编译项目
- • 发布项目
- • 生成文档

以后几乎所有第三方库都会写在：

```
[dependencies]
```

例如：

```
tokio = "1"
serde = "1"
axum = "0.8"
```

---

## Cargo.lock

很多初学者会忽略这个文件。

其实它非常重要。

Cargo.toml：

```
我要安装什么
```

Cargo.lock：

```
实际安装了什么
```

例如：

Cargo.toml：

```
tokio = "1"
```

Cargo 可能实际安装：

```
tokio 1.47.1
```

Cargo 会把最终版本记录到：

```
Cargo.lock
```

这样团队开发时：

所有人的依赖版本都一致。

---

## src 目录

Rust 所有源码默认都放在：

```
src/
```

例如：

```
src
└── main.rs
```

随着项目越来越大：

这里会变成：

```
src
├── main.rs
├── config.rs
├── db.rs
├── router.rs
├── handler.rs
├── service.rs
├── model.rs
├── utils.rs
└── middleware.rs
```

所有业务代码通常都放在这里。

---

## main.rs

如果项目是：

**可执行程序（Binary）**

那么一定有：

```
src/main.rs
```

例如：

```
fn main() {
    println!("Hello Rust");
}
```

程序启动时：

首先执行：

```
fn main()
```

它就是整个程序的入口。

---

## lib.rs

如果项目是：

```
cargo new math --lib
```

目录变成：

```
src
└── lib.rs
```

这里没有：

```
main.rs
```

因为：

它不是应用程序。

而是：

**Rust 库（Library）。**

例如：

```
pub fn add(a: i32, b: i32) -> i32 {
    a + b
}
```

以后其它项目可以直接引用。

很多知名 Rust 库：

- • serde
- • tokio
- • axum
- • clap

都有：

```
lib.rs
```

---

## 一个项目可以同时拥有 main.rs 和 lib.rs

很多大型项目都会这样。

例如：

```
src
├── main.rs
└── lib.rs
```

其中：

`main.rs`

负责：

启动程序。

例如：

```
fn main() {
    println!("Server Start...");
}
```

而：

`lib.rs`

负责：

真正的业务逻辑。

例如：

```
pub mod router;
pub mod service;
pub mod model;
```

这是企业项目最常见的组织方式。

---

## bin 目录

如果一个项目需要多个可执行程序：

可以：

```
src
├── main.rs
└── bin
    ├── server.rs
    ├── client.rs
    └── admin.rs
```

运行：

```
cargo run --bin server
```

或者：

```
cargo run --bin client
```

很多工具类项目都会这样设计。

---

## examples

官方推荐放：

示例程序。

例如：

```
examples
├── basic.rs
├── websocket.rs
└── upload.rs
```

运行：

```
cargo run --example basic
```

很多开源项目都有：

几十甚至上百个 Example。

方便学习。

---

## tests

存放：

集成测试。

例如：

```
tests
├── api.rs
├── login.rs
└── user.rs
```

运行：

```
cargo test
```

Cargo 自动执行。

---

## benches

性能测试。

例如：

```
benches
└── benchmark.rs
```

用于：

- • Benchmark
- • 压力测试
- • 算法比较

大型项目都会有。

---

## target

编译输出目录。

例如：

```
target
├── debug
└── release
```

Debug：

```
cargo build
```

Release：

```
cargo build --release
```

这里通常：

**不要提交 Git。**

一般都会加入：

```
.gitignore
```

---

## 企业级项目目录

随着项目越来越大。

通常会组织成：

```
src
├── main.rs
├── config
├── router
├── handler
├── middleware
├── model
├── entity
├── service
├── repository
├── utils
├── common
├── errors
├── dto
├── vo
└── api
```

例如：

## config

配置读取。

```
config/
```

负责：

- • 数据库
- • Redis
- • JWT
- • 日志

---

## router

路由。

例如：

```
Router::new()
```

统一放这里。

---

## handler

控制器。

例如：

```
GET /users
```

对应：

```
get_user()
```

---

## service

业务逻辑。

例如：

```
登录

注册

支付

订单
```

全部放：

```
service/
```

---

## repository

数据库访问。

例如：

```
CRUD
```

统一管理。

---

## model

数据结构。

例如：

```
struct User
```

---

## dto

请求对象。

例如：

```
LoginRequest
```

---

## vo

返回对象。

例如：

```
UserVO
```

---

## middleware

中间件。

例如：

- • JWT
- • 日志
- • CORS

---

## utils

工具类。

例如：

- • JWT
- • UUID
- • 时间
- • Hash
- • 加密

---

## 推荐目录（适合中小项目）

```
project
├── Cargo.toml
├── src
│   ├── main.rs
│   ├── config.rs
│   ├── router.rs
│   ├── handler.rs
│   ├── service.rs
│   ├── model.rs
│   └── utils.rs
├── tests
├── examples
└── target
```

这种结构简单清晰，适合学习和中小型项目。

---

## 推荐目录（适合企业项目）

```
project
├── Cargo.toml
├── src
│   ├── main.rs
│   ├── lib.rs
│   ├── config
│   ├── router
│   ├── handler
│   ├── middleware
│   ├── service
│   ├── repository
│   ├── model
│   ├── entity
│   ├── dto
│   ├── vo
│   ├── utils
│   └── common
├── tests
├── examples
├── benches
└── target
```

后续我们开发 Axum 后台管理系统、CMS、博客系统时，都将采用这种组织方式。

---

## 本章小结

Rust 项目的目录虽然简洁，但每个目录都有明确的职责。

本文学习了：

- • Cargo.toml 与 Cargo.lock 的区别
- • `src` 目录的作用
- • `main.rs` 与 `lib.rs` 的区别
- • `examples` 、 `tests` 、 `benches` 的用途
- • `target` 编译目录
- • 企业级 Rust 项目的推荐目录结构

理解项目结构后，你在阅读 Rust 开源项目时会更加轻松，也能为后续的大型项目开发打下基础。

---

## 下一篇预告

下一篇我们将正式学习 Rust 的第一个核心语法—— **变量与不可变性（Variables & Mutability）** 。

你将了解：

- • 如何定义变量
- • 为什么 Rust 默认不可变
- • `let` 与 `let mut` 的区别
- • Shadowing（变量遮蔽）
- • 常见错误及最佳实践

这是理解 Rust 所有权系统之前必须掌握的基础知识。

![](https://wst.wxapp.tc.qq.com/161/20304/snscosdownload/SH/reserved/6a4f44ca0006f5ad5f9f01a10996d80e000000a000004f50?imageView2/1/w/800/h/800/q/50)

Rust编程思维：从C++到Rust的平滑过渡

假一赔三

7天无理由

¥81.8

![](https://res.wx.qq.com/shop/public/2024-10-17/fae7be51-beb6-4e61-aad8-4c1f7ccfab83.png)

机械工业出版社官方旗舰店

![](https://mmec.wxqcloud.qq.com.cn/shop/public/2026-07-13/1ade7f7a-528a-437d-a83b-b640764d8f70.png) ![](https://res.wx.qq.com/t/components/icons/base/arrow_down_regular.svg) 收起

使用手机微信

扫码了解商品信息

Rust 编程实战 · Table of Contents