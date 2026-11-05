---
title: "Rust Package 与 Crate 详解：理解 Rust 项目的基本组成"
source: "https://mp.weixin.qq.com/s?__biz=MzYzODE1NzUzMw==&mid=2247484520&idx=1&sn=3f4eba0e88425fca2353c5e0eb8e5b44&chksm=f0e753dac790dacc0e8a3d024eeedde6f2f3b723da79cc81504ba3eea4d444df54708abbb2fa&cur_album_id=4602071361631748097&scene=189#wechat_redirect"
author:
published:
created: 2026-11-05
description: "《Rust 编程实战》系列第 26 篇在上一篇文章中，我们学习了 Rust 的：Module模块系统。"
tags:
  - "clippings"
---
程序员爱钓鱼 *Jul 31, 2026, 8:26 AM*

> 《Rust 编程实战》系列第 26 篇

在上一篇文章中，我们学习了 Rust 的：

```
Module
```

模块系统。

Module 主要解决：

> 如何在一个项目内部组织代码。

例如：

```
用户模块
商品模块
订单模块
数据库模块
```

但是，一个完整 Rust 项目不仅只有 Module。

Rust 还有两个非常重要的概念：

```
Package
Crate
```

很多初学者容易混淆：

- • Package 是什么？
- • Crate 是什么？
- • Module 和 Crate 有什么区别？
- • 一个项目为什么可以有多个 Crate？

理解这些概念，对于开发大型 Rust 项目非常重要。

本文将介绍：

- • 什么是 Package
- • 什么是 Crate
- • Binary Crate 与 Library Crate
- • Package 与 Crate 的关系
- • Cargo.toml 的作用
- • src 目录结构
- • 多 Crate 项目
- • Workspace 工作空间
- • 发布 Rust 库

---

## 什么是 Crate？

Crate 是 Rust 编译的基本单位。

简单理解：

> Crate 是 Rust 编译器一次处理的代码集合。

一个 Crate 可以包含：

- • Rust 源代码
- • Module
- • 函数
- • 结构体
- • Trait

例如：

```
src
 |
 └── main.rs
```

这里：

```
main.rs
```

就是一个：

```
Binary Crate
```

---

## Crate 的两种类型

Rust 中主要有两种 Crate：

## 1\. Binary Crate

二进制程序。

最终生成：

```
.exe
```

或者：

```
可执行文件
```

例如：

```
fn main(){
    println!(
        "Hello Rust"
    );
}
```

编译：

```
cargo build
```

生成：

```
target/debug/app
```

这就是 Binary Crate。

常见用途：

- • Web 服务
- • 命令行工具
- • 桌面程序
- • 游戏程序

---

## 2\. Library Crate

库 Crate。

不会直接运行。

主要用于：

> 提供代码给其他项目使用。

例如：

创建：

```
cargo new utils --lib
```

生成：

```
utils

src
└── lib.rs
```

lib.rs：

```
pub fn hello(){
    println!(
        "Hello Library"
    );
}
```

其他项目可以引用：

```
use utils::hello;
```

---

## 什么是 Package？

Package 是 Cargo 管理项目的单位。

简单理解：

> Package 是一个完整的 Rust 工程。

它包含：

- • Cargo.toml
- • 一个或多个 Crate

例如：

```
my-project
├── Cargo.toml
└── src
    └── main.rs
```

这是一个 Package。

---

## Package 与 Crate 的关系

关系：

```
Package
   |
   |
   +---- Binary Crate
   |
   |
   +---- Library Crate
```

一个 Package：

至少包含：

```
一个 Crate
```

最多可以包含：

```
多个 Binary Crate
+
一个 Library Crate
```

---

## Cargo 创建项目

创建 Binary Package：

```
cargo new hello
```

生成：

```
hello

├── Cargo.toml
└── src
    └── main.rs
```

其中：

```
Package:
hello

Crate:
main.rs
```

---

创建 Library Package：

```
cargo new utils --lib
```

生成：

```
utils

├── Cargo.toml
└── src
    └── lib.rs
```

其中：

```
Package:
utils

Crate:
lib.rs
```

---

## Cargo.toml 的作用

Cargo.toml 是 Package 配置文件。

例如：

```
[package]
name = "hello"
version = "0.1.0"
edition = "2024"

[dependencies]
serde = "1"
```

包含：

## 项目信息

```
name
version
edition
```

---

## 依赖管理

例如：

```
[dependencies]

serde="1"

tokio="1"
```

表示：

当前 Package 依赖：

- • serde
- • tokio

---

## 编译配置

例如：

```
[profile.release]

opt-level=3
```

---

## 一个 Package 多个 Crate

例如：

```
my-app
├── Cargo.toml
└── src
    ├── main.rs
    └── bin

        ├── tool1.rs

        └── tool2.rs
```

这里：

```
main.rs
```

是：

```
Binary Crate
```

同时：

```
tool1.rs
tool2.rs
```

也是：

```
Binary Crate
```

执行：

```
cargo run --bin tool1
```

运行：

```
tool1
```

---

## Library + Binary 组合项目

大型项目经常这样设计：

```
my-server
├── Cargo.toml
└── src
    ├── lib.rs
    └── main.rs
```

其中：

```
lib.rs
```

负责：

业务逻辑。

例如：

```
pub fn start_server(){

}
```

---

main.rs：

负责：

启动程序。

```
use my_server::start_server;

fn main(){

    start_server();

}
```

优点：

- • 业务代码可以测试
- • 可以被其他程序复用
- • main.rs 保持简单

这是 Rust 服务端常见结构。

---

## 什么是 Workspace？

当项目非常大时，一个 Package 不够。

例如：

一个电商系统：

```
shop

├── user-service
├── order-service
├── payment-service
└── common
```

每个都是独立 Crate。

可以使用：

```
Workspace
```

统一管理。

---

Workspace 示例：

目录：

```
shop
├── Cargo.toml
├── user
│   └── Cargo.toml
├── order
│   └── Cargo.toml
└── common
    └── Cargo.toml
```

根 Cargo.toml：

```
[workspace]

members = [
"user",
"order",
"common"
]
```

这样：

```
cargo build
```

可以同时编译所有项目。

---

## Package、Crate、Module 区别

这是最容易混淆的三个概念。

| 名称 | 作用 | 示例 |
| --- | --- | --- |
| Package | 一个完整项目 | 一个 Cargo 工程 |
| Crate | 编译单位 | main.rs、lib.rs |
| Module | 代码组织单位 | mod user |

关系：

```
Package

  └── Crate
        └── Module
              └── Function
```

例如：

```
shop项目
Package
↓
main.rs
Crate
↓
mod user
Module
↓
fn login()

函数
```

---

## 发布 Rust 库

如果开发一个通用库：

例如：

```
http-client
```

可以发布到：

```
crates.io
```

流程：

## 登录

```
cargo login TOKEN
```

---

## 检查

```
cargo package
```

---

## 发布

```
cargo publish
```

其他人：

```
[dependencies]

http-client="1.0"
```

即可使用。

---

## 实战：创建一个工具库

创建：

```
cargo new my-utils --lib
```

结构：

```
my-utils
src
└── lib.rs
```

lib.rs：

```
pub fn add(
    a:i32,
    b:i32
)
->i32{
    a+b
}
```

其他项目：

Cargo.toml：

```
[dependencies]

my-utils={
path="../my-utils"
}
```

使用：

```
use my_utils::add;

fn main(){
    let result =
        add(1,2);
    println!(
        "{}",
        result
    );
}
```

输出：

```
3
```

---

## 常见错误

## 一个 Package 创建多个 lib.rs

错误：

```
src
├── lib.rs
└── lib2.rs
```

Cargo 不会自动认为：

```
lib2.rs
```

也是 Library Crate。

需要：

```
src/bin
```

或者配置。

---

## 混淆 Package 和 Crate

例如：

错误理解：

> 一个项目就是一个 Crate。

实际上：

一个项目：

```
Package
```

里面可以有：

```
多个 Crate
```

---

## 过度拆分 Crate

不是所有模块都需要独立 Crate。

例如：

用户模块：

```
user
```

订单模块：

```
order
```

通常 Module 就够了。

只有：

- • 独立发布
- • 独立编译
- • 大型服务

才考虑拆成 Crate。

---

## Rust 项目结构建议

中小型项目：

```
src
├── main.rs
├── config.rs
├── database.rs
├── user.rs
└── order.rs
```

---

大型项目：

```
src
├── main.rs
├── lib.rs
├── user
├── order
├── database
└── common
```

---

微服务：

```
workspace
├── gateway
├── user-service
├── order-service
├── payment-service
└── common
```

---

## 本章小结

Rust 中：

## Package

表示：

> 一个 Cargo 项目。

负责：

- • 项目管理
- • 依赖管理
- • 编译配置

---

## Crate

表示：

> Rust 编译单元。

包括：

- • Binary Crate
- • Library Crate

---

## Module

表示：

> Crate 内部代码组织方式。

三者关系：

```
Package
 ↓
Crate
 ↓
Module
 ↓
Function
```

理解 Package、Crate 和 Module，是开发大型 Rust 项目的基础。

---

## 下一篇预告

下一篇将学习：

## Rust use 与 pub 详解：模块导入与权限控制

内容包括：

- • use 的各种写法
- • pub 权限规则
- • pub(crate)
- • pub(super)
- • re-export
- • super 与 crate
- • 模块 API 设计
- • 实战：设计一个 Rust 项目公共接口

Rust 编程实战 · Table of Contents