---
title: "Cargo 包管理器详解：Rust 开发必会工具"
source: "https://mp.weixin.qq.com/s?__biz=MzYzODE1NzUzMw==&mid=2247484415&idx=1&sn=aeadd7a178b9b0bce99bdb7bdd9e7c4b&chksm=f0e7544dc790dd5b68e6febaf33003d770a72f23ff5ab711517cee116cb15371d18448410b15&cur_album_id=4602071361631748097&scene=189#wechat_redirect"
author:
published:
created: 2026-11-03
description: "《Rust 编程实战》系列第 4 篇在前面的文章中，我们已经成功安装了 Rust，并编写了第一个 Hello"
tags:
  - "clippings"
---
程序员爱钓鱼 *Jul 9, 2026, 4:41 AM*

> 《Rust 编程实战》系列第 4 篇

在前面的文章中，我们已经成功安装了 Rust，并编写了第一个 `Hello, World!` 程序。

如果说 **Rust 是发动机** ，那么 **Cargo 就是整辆汽车的中控系统** 。

学习 Rust，几乎每天都会使用 Cargo。

它不仅负责 **编译代码** ，还负责：

- • 创建项目
- • 管理依赖
- • 下载第三方库
- • 编译程序
- • 运行程序
- • 测试程序
- • 发布项目
- • 生成文档

可以说，Rust 的开发体验之所以优秀，Cargo 功不可没。

本文将全面介绍 Cargo 的常用功能，为后续学习打下基础。

---

## 什么是 Cargo？

Cargo 是 Rust 官方提供的包管理器（Package Manager）和构建工具（Build Tool）。

它类似于：

| 语言 | 包管理工具 |
| --- | --- |
| Rust | Cargo |
| Go | Go Modules |
| Node.js | npm / pnpm |
| Python | pip |
| Java | Maven / Gradle |
| PHP | Composer |

Cargo 已经随 Rust 一起安装，无需额外下载。

查看版本：

```
cargo --version
```

例如：

```
cargo 1.90.0
```

---

## 创建项目

Cargo 可以快速创建一个完整项目。

创建二进制程序：

```
cargo new hello_rust
```

进入目录：

```
cd hello_rust
```

查看目录：

```
hello_rust
├── Cargo.toml
└── src
    └── main.rs
```

其中：

- • `Cargo.toml` ：项目配置
- • `src` ：源代码
- • `main.rs` ：程序入口

---

## 创建库项目

除了可执行程序，还可以创建库（Library）。

例如：

```
cargo new math --lib
```

目录变成：

```
math
├── Cargo.toml
└── src
    └── lib.rs
```

可以发现：

没有：

```
main.rs
```

而是：

```
lib.rs
```

库项目用于：

- • 工具库
- • SDK
- • 公共组件
- • 第三方 Crate

以后发布到 crates.io 的，大多数都是库项目。

---

## Cargo.toml

Cargo 的核心配置文件。

例如：

```
[package]
name = "hello_rust"
version = "0.1.0"
edition = "2024"

[dependencies]
```

它主要包含：

- • 项目名称
- • 版本
- • 作者（可选）
- • Edition
- • 依赖
- • Feature
- • 发布配置

以后几乎所有第三方库都会写到：

```
[dependencies]
```

例如：

```
[dependencies]
serde = "1.0"
tokio = "1"
axum = "0.8"
```

Cargo 会自动下载。

---

## Cargo 常用命令

Rust 开发中，最常用的几个命令如下。

---

## cargo run

编译并运行程序。

```
cargo run
```

它实际上执行了两步：

第一步：

```
cargo build
```

第二步：

运行：

```
target/debug/项目名称
```

因此：

```
cargo run
```

最适合开发阶段。

---

## cargo build

只编译，不运行。

```
cargo build
```

编译成功后：

生成：

```
target/debug/
```

里面就是可执行文件。

---

## cargo build --release

发布版本。

```
cargo build --release
```

Cargo 会开启优化。

生成：

```
target/release/
```

发布软件时，一般都使用 Release 版本。

它：

- • 更快
- • 更小
- • 优化更多

---

## cargo check

很多开发者每天都会使用。

```
cargo check
```

它：

**只检查代码。**

不会真正生成可执行文件。

因此速度非常快。

适合：

- • 写代码
- • 检查错误
- • IDE 自动调用

VS Code 中的 rust-analyzer 就大量使用了这个命令。

---

## cargo test

运行测试。

```
cargo test
```

以后写：

```
#[test]
fn add_test() {
    assert_eq!(2 + 2, 4);
}
```

Cargo 会自动执行所有测试。

---

## cargo clean

删除编译缓存。

```
cargo clean
```

会删除：

```
target/
```

如果：

- • 编译异常
- • 空间太大

可以执行一次。

下一次 Cargo 会重新编译。

---

## cargo doc

生成文档。

```
cargo doc --open
```

Cargo 会自动生成：

HTML 文档。

浏览器打开即可查看。

很多大型 Rust 项目都使用这种方式生成 API 文档。

---

## cargo fmt

格式化代码。

需要安装：

```
rustup component add rustfmt
```

然后：

```
cargo fmt
```

代码会自动统一格式。

团队开发几乎都会使用。

---

## cargo clippy

Rust 最受欢迎的静态检查工具。

安装：

```
rustup component add clippy
```

运行：

```
cargo clippy
```

它不仅检查错误。

还会告诉你：

- • 有没有更好的写法
- • 有没有性能问题
- • 有没有多余代码

建议每次提交代码前都运行一次。

---

## Cargo 下载依赖

例如：

修改：

```
[dependencies]
rand = "0.9"
```

然后：

```
cargo build
```

Cargo 会：

① 下载源码

② 编译

③ 放入缓存

以后其它项目再次使用：

不会重复下载。

---

## Cargo 缓存在哪里？

默认：

Windows：

```
C:\Users\用户名\.cargo
```

macOS：

```
~/.cargo
```

Linux：

```
~/.cargo
```

编译缓存：

```
target/
```

下载缓存：

```
~/.cargo/registry
```

Git 仓库：

```
~/.cargo/git
```

因此第二次编译通常会快很多。

---

## Cargo.lock

很多新手都会问：

为什么有：

```
Cargo.toml
```

还有：

```
Cargo.lock
```

区别如下：

## Cargo.toml

描述：

**我要什么。**

例如：

```
tokio = "1"
```

意思是：

需要 Tokio 1.x。

---

## Cargo.lock

记录：

**实际安装了什么。**

例如：

```
tokio 1.47.1
```

因此：

多人开发时：

每个人安装的版本一致。

避免：

"我这里可以运行。"

"你那里不能运行。"

---

## 添加第三方库

推荐使用：

```
cargo add serde
```

如果没有：

安装：

```
cargo install cargo-edit
```

然后：

```
cargo add tokio
```

Cargo 自动修改：

```
[dependencies]
tokio = "1"
```

非常方便。

---

## Cargo 发布项目

以后可以发布自己的库：

```
cargo publish
```

发布到：

crates.io

供全球开发者使用。

例如：

```
serde

tokio

clap

axum
```

都是这样发布的。

---

## Cargo 工作流程

一个典型的 Rust 开发流程如下：

```
创建项目
      │
      ▼
cargo new
      │
      ▼
编写代码
      │
      ▼
cargo check
      │
      ▼
cargo run
      │
      ▼
cargo test
      │
      ▼
cargo fmt
      │
      ▼
cargo clippy
      │
      ▼
cargo build --release
```

如果养成这个习惯，代码质量通常会比较高。

---

## 常见问题

## 下载依赖很慢

可以配置 Cargo 镜像源。

例如，在 `~/.cargo/config.toml` 中配置国内镜像（如字节、清华、中科大等），可以显著提升下载速度。

---

## Cargo.toml 写错

例如：

```
serde = 1.0
```

正确：

```
serde = "1.0"
```

版本号需要使用字符串。

---

## cargo run 找不到 Cargo.toml

原因：

没有进入项目目录。

例如：

```
cd hello_rust
cargo run
```

---

## target 太大

正常现象。

Release 编译后：

几百 MB 都可能出现。

可以：

```
cargo clean
```

重新生成。

---

## 本章小结

Cargo 是 Rust 开发中最重要的工具之一，它集包管理、项目构建、测试、文档生成和发布于一体，让开发者能够专注于业务代码，而无需手动管理复杂的构建流程。

通过本文，你已经掌握了：

- • 什么是 Cargo
- • 创建二进制项目和库项目
- • Cargo.toml 与 Cargo.lock 的作用
- • 常用命令（run、build、check、test、fmt、clippy 等）
- • 第三方依赖管理
- • Cargo 的工作流程
- • 常见问题及解决方法

随着后续学习深入，你会发现 Cargo 不只是一个包管理器，更是整个 Rust 工程化开发的核心工具。

---

## 下一篇预告

下一篇我们将学习 **Rust 项目目录结构详解** ，包括：

- • `src` 目录的作用
- • `main.rs` 与 `lib.rs` 的区别
- • `mod` 模块组织方式
- • `tests` 、 `examples` 、 `benches` 目录
- • 企业级 Rust 项目推荐目录结构

学完之后，你将能够看懂绝大多数 Rust 开源项目的组织方式，并为后续的大型项目开发做好准备。

Rust 编程实战 · Table of Contents