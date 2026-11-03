---
title: "第一个 Rust 程序 Hello World"
source: "https://mp.weixin.qq.com/s?__biz=MzYzODE1NzUzMw==&mid=2247484411&idx=1&sn=8923bc203d375524929a4d906570bbbd&chksm=f0e75449c790dd5f764a60256eb09d1820e3738c25da9f34ec97c7d4af853eb0c123643a021b&cur_album_id=4602071361631748097&scene=189#wechat_redirect"
author:
published:
created: 2026-11-03
description: "《Rust 编程实战》系列第 3 篇在上一篇文章中，我们完成了 Rust 开发环境的安装，并成功安装了 ru"
tags:
  - "clippings"
---
程序员爱钓鱼 *Jul 8, 2026, 7:22 AM*

> 《Rust 编程实战》系列第 3 篇

在上一篇文章中，我们完成了 Rust 开发环境的安装，并成功安装了 `rustc` 和 `Cargo` 。

从这一篇开始，我们正式编写第一个 Rust 程序——经典的 **Hello, World!**。

虽然这个程序只有一行输出，但它能帮助我们了解 Rust 项目的基本结构、Cargo 的工作方式以及程序是如何编译和运行的。

---

## 为什么每门语言都从 Hello World 开始？

几乎所有编程语言的第一课都是输出一句：

```
Hello, World!
```

它的目的不是学习输出，而是验证：

- • 开发环境是否安装成功
- • 编译器是否可以正常工作
- • IDE 是否配置正确
- • 程序能够成功编译和运行

对于 Rust 来说，Hello World 还能帮助我们认识 Cargo 创建的项目结构。

---

## 创建第一个 Rust 项目

打开终端（Windows 可以使用 PowerShell，macOS 和 Linux 使用 Terminal）。

执行：

```
cargo new hello_rust
```

如果一切正常，会看到类似输出：

```
Creating binary (application) \`hello_rust\` package
```

这表示 Cargo 已经帮我们创建好了一个完整的 Rust 项目。

进入项目目录：

```
cd hello_rust
```

---

## 查看项目结构

执行：

```
tree
```

如果没有安装 `tree` 命令，也可以直接查看目录。

项目结构如下：

```
hello_rust/
├── Cargo.toml
└── src
    └── main.rs
```

这是一个最简单的 Rust 项目。

各个文件的作用如下：

| 文件 | 作用 |
| --- | --- |
| Cargo.toml | 项目配置文件 |
| src/main.rs | 程序入口 |
| target | 编译后的文件（首次编译后生成） |

第一次创建时还没有 `target` 目录。

当执行 `cargo build` 或 `cargo run` 后，Cargo 会自动创建。

---

## Cargo.toml 是什么？

打开：

```
Cargo.toml
```

默认内容类似：

```
[package]
name = "hello_rust"
version = "0.1.0"
edition = "2024"

[dependencies]
```

这里包含了项目的重要信息。

## package

描述项目基本信息。

例如：

```
name = "hello_rust"
```

项目名称。

---

```
version = "0.1.0"
```

当前版本。

通常遵循：

```
主版本.次版本.修订版本
```

例如：

```
1.0.0
```

---

```
edition = "2024"
```

Rust 使用 Edition（版本规范）来保证新特性与旧项目兼容。

目前常见版本包括：

- • 2018
- • 2021
- • 2024

新项目建议使用最新稳定 Edition。

---

## dependencies

用于管理第三方依赖。

目前为空：

```
[dependencies]
```

以后学习数据库、Web 开发时，都会在这里添加依赖。

例如：

```
serde = "1.0"
tokio = "1"
axum = "0.8"
```

Cargo 会自动下载并管理这些库。

---

## main.rs

打开：

```
src/main.rs
```

默认内容如下：

```
fn main() {
    println!("Hello, world!");
}
```

程序虽然只有两行，却包含了 Rust 最基本的语法。

---

## 认识 main 函数

第一行：

```
fn main() {
```

其中：

```
fn
```

表示定义函数（Function）。

---

```
main
```

表示程序入口。

每个 Rust 可执行程序都有一个：

```
fn main()
```

程序运行时，会首先执行这里面的代码。

---

## println! 宏

第二行：

```
println!("Hello, world!");
```

很多初学者会问：

为什么不是：

```
println()
```

而是：

```
println!()
```

因为：

`println!` 不是普通函数。

它是 **宏（Macro）** 。

宏可以在编译期间生成代码，因此比普通函数更加灵活。

以后还会接触：

```
vec!

format!

panic!

assert!

dbg!
```

它们都是 Rust 提供的常用宏。

---

## 修改输出内容

把代码改成：

```
fn main() {
    println!("你好，Rust！");
}
```

保存后重新运行：

```
cargo run
```

输出：

```
你好，Rust！
```

说明修改已经生效。

---

## 输出多个内容

例如：

```
fn main() {
    println!("欢迎学习 Rust");
    println!("这是第一天");
    println!("Hello Rust");
}
```

输出：

```
欢迎学习 Rust
这是第一天
Hello Rust
```

Rust 会按照代码顺序依次执行。

---

## 使用变量输出

例如：

```
fn main() {
    let name = "Rust";

    println!("Hello {}", name);
}
```

输出：

```
Hello Rust
```

这里的：

```
{}
```

表示占位符。

后面的：

```
name
```

会替换进去。

---

也可以输出多个变量：

```
fn main() {
    let language = "Rust";
    let year = 2026;

    println!("{} 发布于 {}", language, year);
}
```

输出：

```
Rust 发布于 2026
```

---

## Cargo run 做了什么？

执行：

```
cargo run
```

实际上 Cargo 完成了两件事情：

第一步：

编译程序。

相当于：

```
cargo build
```

第二步：

运行程序。

因此：

```
cargo run
```

等价于：

```
cargo build

./target/debug/hello_rust
```

Windows 下：

```
target\debug\hello_rust.exe
```

---

## Cargo build

如果只想编译：

```
cargo build
```

编译成功后：

项目会新增：

```
target/
```

里面存放所有编译结果。

例如：

```
target
└── debug
    └── hello_rust
```

---

## Release 模式

默认：

```
cargo run
```

属于 Debug 模式。

如果需要发布正式版本：

执行：

```
cargo build --release
```

Cargo 会进行更多优化。

生成：

```
target/release/
```

性能会更高。

---

## 常见错误

## cargo: command not found

说明 Cargo 没有安装成功。

可以检查：

```
cargo --version
```

如果没有输出版本号，请重新安装 Rust 或检查环境变量。

---

## rustc: command not found

说明编译器没有加入环境变量。

重新打开终端：

或者执行：

```
source ~/.cargo/env
```

---

## 找不到 Cargo.toml

例如：

```
could not find Cargo.toml
```

说明没有进入项目目录。

正确做法：

```
cd hello_rust
cargo run
```

---

## 本章小结

通过本文，我们完成了第一个 Rust 程序的编写，并认识了 Rust 项目的基本结构。

我们学习了：

- • 如何使用 `cargo new` 创建项目
- • `Cargo.toml` 的作用
- • `src/main.rs` 是程序入口
- • `fn main()` 的意义
- • `println!` 宏的使用
- • `cargo run` 、 `cargo build` 和 `cargo build --release` 的区别
- • Rust 项目的编译流程

虽然 Hello World 非常简单，但它已经包含了 Rust 项目的核心组成部分。

在接下来的文章中，我们将进一步学习 Cargo 包管理器，了解它如何管理依赖、构建项目以及帮助我们高效开发 Rust 应用。

---

## 下一篇预告

下一篇我们将深入学习 **Cargo 包管理器详解** ，包括：

- • Cargo 常用命令
- • 添加第三方依赖
- • 编译与运行
- • Release 与 Debug 的区别
- • Cargo.lock 和 Cargo.toml 的作用
- • Rust 项目的最佳实践

掌握 Cargo 后，你将能够更加高效地开发和管理 Rust 项目。

Rust 编程实战 · Table of Contents