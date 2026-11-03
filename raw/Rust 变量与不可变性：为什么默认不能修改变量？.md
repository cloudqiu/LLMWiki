---
title: "Rust 变量与不可变性：为什么默认不能修改变量？"
source: "https://mp.weixin.qq.com/s?__biz=MzYzODE1NzUzMw==&mid=2247484423&idx=1&sn=a99f9a5ab204d5412299d1487965ce1f&chksm=f0e753b5c790daa30b06ef29317734208a1579445e24f6451f7ae763b35820c76472fae93896&cur_album_id=4602071361631748097&scene=189#wechat_redirect"
author:
published:
created: 2026-11-03
description: "《Rust 编程实战》系列第 6 篇在学习任何一门编程语言时，变量都是最基础也是最重要的知识。"
tags:
  - "clippings"
---
程序员爱钓鱼 *Jul 11, 2026, 7:06 AM*

> 《Rust 编程实战》系列第 6 篇

在学习任何一门编程语言时，变量都是最基础也是最重要的知识。

如果你学过 C、C++、Java、Go 或 Python，你会发现这些语言定义变量后，通常都可以随时修改变量的值。

例如，在 Go 中：

```
package main

import "fmt"

func main() {
    age := 18
    age = 20
    fmt.Println(age)
}
```

程序可以正常运行。

但是，在 Rust 中，如果写出类似代码：

```
fn main() {
    let age = 18;

    age = 20;

    println!("{}", age);
}
```

编译器会直接报错。

为什么？

因为 **Rust 默认所有变量都是不可变（Immutable）的** 。

这是 Rust 保证内存安全和并发安全的重要设计之一。

本文将详细介绍 Rust 的变量、不可变性、可变变量以及变量遮蔽（Shadowing）。

---

## 什么是变量？

变量（Variable）可以理解为：

> **用于保存数据的一个名字。**

例如：

```
fn main() {
    let name = "Rust";
    let age = 10;

    println!("{}", name);
    println!("{}", age);
}
```

输出：

```
Rust
10
```

这里：

```
let name = "Rust";
```

表示：

定义一个名字叫：

```
name
```

它保存：

```
Rust
```

同样：

```
let age = 10;
```

保存：

```
10
```

以后需要使用时：

直接写变量名即可。

---

## let 关键字

Rust 使用：

```
let
```

定义变量。

语法：

```
let 变量名 = 值;
```

例如：

```
let name = "Tom";

let age = 18;

let score = 99.5;
```

每条语句最后都要有：

```
;
```

这与 Go 不同。

---

## Rust 默认不可变

来看一个例子。

```
fn main() {

    let age = 18;

    age = 20;

    println!("{}", age);

}
```

编译：

```
cargo run
```

得到错误：

```
cannot assign twice to immutable variable
```

意思是：

> 无法再次给不可变变量赋值。

原因就在于：

```
let
```

默认创建的是：

**不可变变量。**

也就是说：

创建之后：

不能修改。

---

## 为什么 Rust 默认不可变？

很多初学者都会问：

> 为什么 Rust 不像其他语言一样允许修改变量？

原因有三个。

## 一、避免意外修改

例如：

```
let price = 100;
```

程序运行几千行之后：

突然：

```
price = 1;
```

如果项目很大。

很难找到是谁修改了它。

默认不可变可以避免很多这种 Bug。

---

## 二、更容易推导代码

例如：

```
let id = 1001;
```

只要看到：

```
id
```

开发者就知道：

它永远都是：

```
1001
```

阅读代码更加轻松。

---

## 三、更安全

不可变对象：

天然线程安全。

因此：

Rust 更容易实现高性能并发。

---

## 可变变量

如果确实需要修改变量。

Rust 允许：

使用：

```
mut
```

例如：

```
fn main() {

    let mut age = 18;

    age = 20;

    println!("{}", age);

}
```

输出：

```
20
```

这里：

```
mut
```

表示：

Mutable（可变）。

语法：

```
let mut 变量 = 值;
```

例如：

```
let mut count = 0;

count += 1;
```

完全合法。

---

## 修改多次

例如：

```
fn main() {

    let mut num = 1;

    num = 2;

    num = 3;

    num = 100;

    println!("{}", num);

}
```

输出：

```
100
```

Rust 没有限制修改次数。

只要：

变量是：

```
mut
```

即可。

---

## 不可变与可变对比

不可变：

```
let name = "Rust";
```

可以：

```
println!("{}", name);
```

不能：

```
name = "Go";
```

---

可变：

```
let mut name = "Rust";
```

可以：

```
name = "Go";
```

也可以：

```
println!("{}", name);
```

---

## 一次定义多个变量

Rust 可以连续定义多个变量。

例如：

```
fn main() {

    let name = "Alice";

    let age = 20;

    let city = "Beijing";

    println!("{}", name);

    println!("{}", age);

    println!("{}", city);

}
```

输出：

```
Alice
20
Beijing
```

---

## 类型自动推导

Rust 能自动推导变量类型。

例如：

```
let age = 18;
```

编译器自动认为：

```
i32
```

再例如：

```
let pi = 3.14;
```

自动推导：

```
f64
```

因此：

很多时候：

无需写：

```
let age: i32 = 18;
```

直接：

```
let age = 18;
```

即可。

---

## 显式指定类型

当然。

也可以：

自己指定。

例如：

```
let age: i32 = 18;

let score: f64 = 98.5;

let ok: bool = true;
```

语法：

```
let 变量: 类型 = 值;
```

---

## 变量遮蔽（Shadowing）

Rust 有一个非常有特色的功能：

Shadowing。

例如：

```
fn main() {

    let x = 5;

    let x = x + 1;

    let x = x * 2;

    println!("{}", x);

}
```

输出：

```
12
```

这里：

并不是修改变量。

而是：

重新定义了一个新的：

```
x
```

旧变量已经被新的变量遮蔽（Shadow）了。

---

## Shadowing 与 mut 有什么区别？

来看两个例子。

使用：

```
mut
```
```
let mut x = 5;

x = 6;
```

这里：

只有一个：

```
x
```

只是修改了它。

---

使用：

```
let x = 5;

let x = 6;
```

这里：

实际上有两个变量。

第二个：

遮蔽了第一个。

---

## Shadowing 可以改变类型

这是：

`mut`

做不到的。

例如：

```
let space = "100";

let space = space.len();

println!("{}", space);
```

输出：

```
3
```

第一次：

```
space
```

是：

```
&str
```

第二次：

变成：

```
usize
```

如果：

使用：

```
mut
```

则会报错。

因为：

类型不能改变。

---

## 常见错误

## 忘记写 mut

例如：

```
let count = 0;

count += 1;
```

错误：

```
cannot assign twice to immutable variable
```

解决：

```
let mut count = 0;
```

---

## 修改类型

例如：

```
let mut name = "Rust";

name = 100;
```

错误：

类型不一致。

Rust 是静态类型语言。

变量一旦确定类型。

不能修改。

---

## Shadowing 误认为修改变量

例如：

```
let x = 5;

let x = 6;
```

很多初学者认为：

修改了：

```
x
```

实际上：

不是。

而是：

创建了：

新的变量。

---

## 最佳实践

开发中建议遵循以下原则：

- • 默认使用不可变变量。
- • 只有真正需要修改时，才使用 `mut` 。
- • 类型转换优先考虑 Shadowing，而不是强行修改变量。
- • 缩小可变变量的作用范围，减少意外修改的可能性。
- • 给变量起有意义的名字，例如 `user_name` 、 `total_price` ，避免使用 `a` 、 `b` 、 `tmp` 等难以理解的名称。

这样不仅代码更安全，也更容易维护。

---

## 本章小结

变量是 Rust 编程中最基础的概念，而 **默认不可变** 则是 Rust 与许多其他语言最大的不同之一。

本文学习了：

- • 什么是变量
- • `let` 定义变量
- • Rust 默认不可变
- • `mut` 可变变量
- • 类型自动推导
- • 显式类型声明
- • Shadowing（变量遮蔽）
- • `mut` 与 Shadowing 的区别
- • 常见错误和最佳实践

掌握变量和不可变性的设计思想后，你会发现 Rust 鼓励开发者编写更加安全、可预测的代码，这也是它在大型项目和高并发场景中备受青睐的重要原因。

---

## 下一篇预告

下一篇我们将学习 **Rust 数据类型（Data Types）** ，包括：

- • 整数类型
- • 浮点数类型
- • 布尔类型
- • 字符类型
- • 元组（Tuple）
- • 数组（Array）
- • 类型转换
- • 类型推导

学完之后，你将能够正确选择和使用 Rust 中各种基础数据类型，为后续学习函数、所有权和结构体打下坚实基础。

Rust 编程实战 · Table of Contents