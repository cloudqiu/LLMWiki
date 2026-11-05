---
title: "Rust 所有权 Ownership 详解：理解内存安全的核心机制"
source: "https://mp.weixin.qq.com/s?__biz=MzYzODE1NzUzMw==&mid=2247484549&idx=1&sn=7c6901dc88a8cea5e6ad2c47282759dd&chksm=f0e75337c790da21c87e0dd37b1331f4d9aea1509caabf9c37a25e0aa478d531e2ffc548b1ee&cur_album_id=4602071361631748097&scene=189#wechat_redirect"
author:
published:
created: 2026-11-05
description: "《Rust 编程实战》系列第 31 篇在上一篇文章中，我们学习了 Rust 集成测试。"
tags:
  - "clippings"
---
程序员爱钓鱼 *Aug 5, 2026, 7:52 AM*

> 《Rust 编程实战》系列第 31 篇  
> 在上一篇文章中，我们学习了 Rust 集成测试。本篇将进入 Rust 最核心、也是最重要的知识之一：

```
Ownership
```

中文通常称为所有权。  
很多初学者第一次接触 Rust 时，会对下面的代码感到困惑：

```
fn main() {
    let name = String::from("Rust");
    let new_name = name;
    println!("{}", name);
}
```

这段代码无法通过编译，因为 `name` 的所有权已经转移给了 `new_name` 。  
在其他语言中，变量赋值通常只是复制一个值，但 Rust 会根据数据类型决定：

- • 复制数据
- • 转移所有权
- • 借用数据  
	所有权系统让 Rust 在没有垃圾回收器的情况下，仍然可以保证内存安全。  
	本文将介绍：
- • 什么是所有权
- • 栈与堆
- • 所有权三条规则
- • 变量作用域
- • String 的内存结构
- • 所有权移动
- • Clone 与 Copy
- • 函数参数和返回值中的所有权
- • 所有权与内存安全
- • 常见错误和最佳实践

## 什么是所有权

所有权可以理解为：

> 每一块内存数据，都由某个变量负责管理。  
> 当这个变量离开作用域时，Rust 会自动释放它拥有的数据。  
> 例如：

```
fn main() {
    let message = String::from("Hello Rust");
    println!("{}", message);
}
```

变量 `message` 拥有字符串数据。当 `main` 函数结束时， `message` 离开作用域，Rust 自动释放字符串占用的内存。  
开发者不需要手动调用：

```
free()
```

也不需要等待垃圾回收器扫描内存。

## 所有权三条规则

Rust 所有权系统可以总结为三条规则。  
第一条：

> Rust 中的每一个值都有一个所有者。  
> 例如：

```
let name = String::from("Tom");
```

字符串 `"Tom"` 的所有者是变量 `name` 。  
第二条：

> 一个值在同一时间只能有一个所有者。  
> 例如：

```
let first = String::from("Rust");
let second = first;
```

执行后，字符串数据的所有者从 `first` 变成 `second` 。  
第三条：

> 当所有者离开作用域时，值会被自动释放。

```
{
    let text = String::from("Hello");
    println!("{}", text);
}
```

代码块结束后， `text` 被销毁，它拥有的字符串内存也被释放。

## 变量作用域

作用域表示变量在程序中有效的范围。

```
fn main() {
    {
        let language = String::from("Rust");
        println!("{}", language);
    }
}
```

变量 `language` 只在内部代码块中有效。  
下面的代码会报错：

```
fn main() {
    {
        let language = String::from("Rust");
    }
    println!("{}", language);
}
```

因为变量已经离开作用域。  
Rust 在变量离开作用域时，会自动调用：

```
drop
```

释放对应资源。

## 栈与堆

理解所有权之前，需要简单了解栈和堆。  
栈适合保存：

- • 固定大小的数据
- • 生命周期较短的数据
- • 可以快速复制的数据  
	例如：
```
let age: i32 = 20;
let enabled: bool = true;
```

这些数据大小在编译阶段已经确定，通常直接存储在栈上。  
堆适合保存：

- • 大小可能变化的数据
- • 运行时动态创建的数据  
	例如：
```
let name = String::from("Rust");
```

`String` 的实际文本内容通常存储在堆上。

## String 的内存结构

一个 `String` 变量本身通常包含三部分信息：

```
指针
长度
容量
```

例如：

```
let text = String::from("Rust");
```

可以简单理解为：

```
text
├── 指针：指向堆上的字符串数据
├── 长度：4
└── 容量：4或更大
```

真正的字符数据：

```
Rust
```

存储在堆上。  
变量本身保存的是管理这段堆内存的信息。

## 所有权移动

看下面的代码：

```
fn main() {
    let first = String::from("Rust");
    let second = first;
    println!("{}", second);
}
```

这段代码可以运行。  
但下面的代码会报错：

```
fn main() {
    let first = String::from("Rust");
    let second = first;
    println!("{}", first);
}
```

原因是：

```
let second = first;
```

并没有完整复制堆上的字符串数据，而是把所有权从 `first` 转移给了 `second` 。  
这个过程称为：

```
Move
```

移动后：

```
first 失效
second 成为新所有者
```

## Rust 为什么要让原变量失效

假设 `first` 和 `second` 都可以继续使用，并且都认为自己拥有同一块堆内存。  
当作用域结束时：

```
first 释放一次
second 再释放一次
```

就会产生重复释放：

```
double free
```

这可能导致：

- • 程序崩溃
- • 内存破坏
- • 安全漏洞  
	Rust 通过让旧变量立即失效，从编译阶段避免重复释放。

## Clone 深拷贝

如果确实需要复制一份独立的堆数据，可以使用：

```
clone()
```

示例：

```
fn main() {
    let first = String::from("Rust");
    let second = first.clone();
    println!("{}", first);
    println!("{}", second);
}
```

此时内存中存在两份独立字符串：

```
first  -> Rust
second -> Rust
```

两者可以分别使用和释放。  
不过 `clone()` 需要复制堆数据，可能存在性能开销。  
因此不要为了逃避所有权问题而大量使用 `clone()` 。

## Copy 类型

有些类型在赋值时不会移动，而是直接复制。  
例如：

```
fn main() {
    let first = 100;
    let second = first;
    println!("{}", first);
    println!("{}", second);
}
```

这段代码可以正常运行。  
因为整数实现了：

```
Copy
```

常见 Copy 类型包括：

- • 整数
- • 浮点数
- • 布尔值
- • 字符
- • 只包含 Copy 类型的元组  
	例如：
```
let point = (10, 20);
let new_point = point;
println!("{:?}", point);
```

仍然可以使用 `point` 。

## Move 与 Copy 的区别

`Copy` ：

```
let a = 10;
let b = a;
```

结果：

```
a 有效
b 有效
```

`Move` ：

```
let a = String::from("Rust");
let b = a;
```

结果：

```
a 失效
b 有效
```

可以简单记住：

> 栈上的简单类型通常可以 Copy。  
> 拥有堆资源的类型通常会 Move。

## 函数参数中的所有权

把一个 `String` 传入函数时，所有权通常会移动。

```
fn print_name(name: String) {
    println!("{}", name);
}

fn main() {
    let name = String::from("Tom");
    print_name(name);
}
```

调用后， `name` 不能继续使用：

```
println!("{}", name);
```

会报错。  
因为：

```
main 中的 name
    ↓
移动到 print_name
```

函数结束后，参数 `name` 被销毁，字符串数据也被释放。

## Copy 类型传入函数

如果传入的是 Copy 类型，则原变量仍然有效。

```
fn print_age(age: u32) {
    println!("{}", age);
}

fn main() {
    let age = 20;
    print_age(age);
    println!("{}", age);
}
```

因为 `u32` 实现了 Copy，传入函数时只是复制。

## 函数返回值转移所有权

函数可以把所有权返回给调用者。

```
fn create_name() -> String {
    String::from("Rust")
}

fn main() {
    let name = create_name();
    println!("{}", name);
}
```

这里字符串所有权从函数内部转移到变量 `name` 。  
也可以接收一个值后再返回：

```
fn return_name(name: String) -> String {
    name
}

fn main() {
    let name = String::from("Tom");
    let name = return_name(name);
    println!("{}", name);
}
```

虽然可以这样处理，但频繁传入再返回会让代码很繁琐。  
Rust 为此提供了借用机制，后续章节会详细讲解。

## 实战：商品名称处理

下面的函数取得商品名称所有权并进行处理：

```
fn normalize_product_name(name: String) -> String {
    name.trim().to_lowercase()
}

fn main() {
    let product = String::from("  Rust Book  ");
    let product = normalize_product_name(product);
    println!("{}", product);
}
```

输出：

```
rust book
```

第一次声明：

```
let product = String::from(...)
```

调用函数后，原所有权被移动。  
随后使用同名变量接收新字符串，这种写法称为变量遮蔽：

```
let product = normalize_product_name(product);
```

## 实战：创建用户

```
#[derive(Debug)]
struct User {
    name: String,
    age: u32,
}

fn create_user(name: String, age: u32) -> User {
    User { name, age }
}

fn main() {
    let name = String::from("Alice");
    let user = create_user(name, 20);
    println!("{:?}", user);
}
```

调用后：

```
name
```

的所有权已经移动到 `User` 结构体中。  
不能继续访问原变量：

```
println!("{}", name);
```

## 结构体字段的所有权

结构体可以拥有自己的数据：

```
struct Product {
    name: String,
    price: f64,
}
```

创建结构体：

```
let name = String::from("Keyboard");
let product = Product {
    name,
    price: 299.0,
};
```

此时 `name` 的所有权移动到：

```
product.name
```

结构体被销毁时，字段拥有的数据也会自动释放。

## 部分移动

如果从结构体中取出一个拥有所有权的字段，可能发生部分移动。

```
struct User {
    name: String,
    age: u32,
}

fn main() {
    let user = User {
        name: String::from("Tom"),
        age: 20,
    };
    let name = user.name;
    println!("{}", name);
    println!("{}", user.age);
}
```

这里：

```
user.name
```

被移动，但 `user.age` 是 Copy 类型，因此仍然可以访问。  
不过不能再整体使用：

```
println!("{:?}", user);
```

因为结构体已经发生部分移动。

## 所有权与集合

把 `String` 放入 `Vec` 时，所有权会移动到集合中。

```
fn main() {
    let name = String::from("Tom");
    let mut names = Vec::new();
    names.push(name);
    println!("{:?}", names);
}
```

此时不能继续使用原来的 `name` 。  
因为集合现在负责管理字符串数据。

## drop 提前释放数据

通常变量在离开作用域时自动释放。  
也可以使用：

```
drop()
```

提前释放：

```
fn main() {
    let text = String::from("Hello");
    println!("{}", text);
    drop(text);
}
```

调用 `drop(text)` 后， `text` 不能继续使用。  
`drop()` 常用于：

- • 提前释放锁
- • 提前关闭资源
- • 缩短借用范围  
	普通字符串通常不需要手动调用。

## 所有权如何保证内存安全

所有权系统可以避免：

- • 使用已经释放的内存
- • 重复释放内存
- • 悬空指针
- • 多个位置同时修改同一数据  
	这些问题在 C 和 C++ 中通常需要开发者手动管理。  
	Rust 在编译阶段检查所有权规则，因此很多内存错误无法通过编译。

## 常见错误

## Move 后继续使用变量

错误：

```
let first = String::from("Rust");
let second = first;
println!("{}", first);
```

解决方式包括：

- • 使用 `second`
- • 使用 `clone()`
- • 使用引用借用数据

## 把 String 传入函数后继续使用

错误：

```
let name = String::from("Tom");
print_name(name);
println!("{}", name);
```

如果函数只需要读取，应改为借用：

```
fn print_name(name: &str) {
    println!("{}", name);
}
```

## 滥用 clone

不推荐：

```
let second = first.clone();
```

仅仅为了消除编译错误。  
应该先判断：

- • 是否真的需要两份数据
- • 是否可以借用
- • 是否可以重新设计所有权关系

## 混淆 Copy 和 Clone

`Copy` 是隐式复制：

```
let b = a;
```

`Clone` 是显式复制：

```
let b = a.clone();
```

拥有堆数据的类型通常不能 Copy，但可以 Clone。

## 所有权最佳实践

## 明确谁负责拥有数据

例如业务实体通常拥有自己的字段：

```
struct User {
    name: String,
}
```

函数只读取数据时，不应该轻易取得所有权。

## 只读参数优先借用

不推荐：

```
fn print_name(name: String)
```

更通用：

```
fn print_name(name: &str)
```

## 确实需要独立数据时再 clone

例如数据需要分别保存到两个长期存在的对象中，可以使用 `clone()` 。

## 让所有权关系保持简单

避免一个值在多个函数之间反复移动和返回。合理使用结构体和借用，可以让代码更清晰。

## 本章小结

所有权是 Rust 内存安全的核心。  
本文学习了：

- • 每个值都有一个所有者
- • 同一时间只能有一个所有者
- • 所有者离开作用域时数据自动释放
- • 栈和堆的基本区别
- • `String` 的指针、长度和容量
- • 所有权移动 Move
- • `clone()` 深拷贝
- • Copy 类型
- • 函数参数和返回值中的所有权转移
- • 结构体与集合中的所有权
- • 部分移动
- • `drop()` 提前释放资源
- • 所有权如何避免重复释放和悬空指针  
	可以记住：

> Rust 不是禁止变量赋值，而是要求明确数据由谁负责管理。  
> 简单类型通常复制，拥有资源的类型通常移动。  
> 所有权让 Rust 在没有垃圾回收器的情况下，仍然能够自动并安全地管理内存。

## 下一篇预告

下一篇我们将继续学习：

## Rust Move 详解：所有权移动与变量失效

内容包括：

- • Move 的完整执行过程
- • String 为什么会移动
- • Move 与浅拷贝的区别
- • 函数调用中的 Move
- • 结构体字段移动
- • 模式匹配中的 Move
- • 集合中的 Move
- • 如何避免不必要的 Move
- • Clone、Copy 与 Borrow 的选择
- • 常见所有权错误分析

Rust 编程实战 · Table of Contents