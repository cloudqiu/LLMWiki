---
title: "Rust Option 详解：安全处理“可能存在，也可能不存在”的值"
source: "https://mp.weixin.qq.com/s?__biz=MzYzODE1NzUzMw==&mid=2247484494&idx=1&sn=67fe318ff6788ddbcf36e985a7f55215&chksm=f0e753fcc790daea6ed25bd9b55dbe4c004bdc372e73a09971cfe95eec76ddd0c433d980ca92&cur_album_id=4602071361631748097&scene=189#wechat_redirect"
author:
published:
created: 2026-11-05
description: "《Rust 编程实战》系列第 21 篇在上一篇文章中，我们学习了 HashMap。"
tags:
  - "clippings"
---
程序员爱钓鱼 *Jul 26, 2026, 6:45 AM*

> 《Rust 编程实战》系列第 21 篇

在上一篇文章中，我们学习了 `HashMap` 。

在使用 `HashMap` 查询数据时，经常会看到这样的代码：

```
map.get("Tom")
```

它的返回值并不是直接返回某个值，而是：

```
Option<&V>
```

为什么？

因为指定的键可能存在，也可能不存在。

Rust 使用：

```
Option<T>
```

来表示这种“可能有值，也可能没有值”的情况。

它是 Rust 中最重要的枚举类型之一。

本文将介绍：

- • 什么是 `Option<T>`
- • `Some` 与 `None`
- • 为什么 Rust 不依赖传统空值
- • `match` 处理 Option
- • `if let`
- • `unwrap()` 与 `expect()`
- • 默认值处理
- • `map()` 、 `and_then()`
- • 函数返回 Option
- • 实战案例
- • 常见错误与最佳实践

---

## 什么是 Option？

`Option<T>` 的定义可以简单理解为：

```
enum Option<T> {
    Some(T),
    None,
}
```

它只有两种状态。

有值：

```
Some(value)
```

没有值：

```
None
```

例如：

```
fn main() {
    let first = Some(100);
    let second: Option<i32> = None;

    println!("{:?}", first);
    println!("{:?}", second);
}
```

输出：

```
Some(100)
None
```

---

## 为什么需要 Option？

假设我们要查询一个用户年龄。

用户可能存在：

```
20
```

也可能不存在。

一些语言可能使用：

```
null
```

表示没有值。

但如果忘记检查空值，就可能产生运行时错误。

Rust 更倾向于把“可能不存在”明确写进类型：

```
Option<i32>
```

这意味着：

> 调用者必须意识到这个值有可能不存在。

---

## Some 与 None

有值时使用：

```
Some()
```

例如：

```
let age = Some(20);
```

它的类型通常是：

```
Option<i32>
```

没有值时：

```
let age: Option<i32> = None;
```

这里通常需要明确类型，因为单独一个 `None` 无法告诉编译器内部应该是什么类型。

---

## Option 与 T 不同

下面两个变量类型完全不同：

```
let age: i32 = 20;

let optional_age: Option<i32> =
    Some(20);
```

不能直接这样相加：

```
let result = age + optional_age;
```

因为：

```
i32
```

和：

```
Option<i32>
```

不是同一种类型。

必须先把 `Option` 中的值安全地取出来。

---

## 使用 match 处理 Option

最完整的处理方式是：

```
match
```

例如：

```
fn main() {
    let score = Some(90);

    match score {
        Some(value) => {
            println!("成绩：{}", value);
        }
        None => {
            println!("没有成绩");
        }
    }
}
```

输出：

```
成绩：90
```

这里必须处理：

```
Some
```

和：

```
None
```

两个分支。

---

## 函数返回 Option

假设我们实现一个查找函数：

```
fn find_user(id: u64)
    -> Option<&'static str>
{
    match id {
        1 => Some("Tom"),
        2 => Some("Alice"),
        _ => None,
    }
}

fn main() {
    match find_user(2) {
        Some(name) => {
            println!("用户：{}", name);
        }
        None => {
            println!("用户不存在");
        }
    }
}
```

当用户存在时：

```
Some("Alice")
```

不存在时：

```
None
```

这种设计比返回一个特殊字符串：

```
"不存在"
```

更加明确。

---

## 使用 if let 简化 Option

如果只关心 `Some` ，可以使用：

```
if let
```
```
fn main() {
    let username = Some("Tom");

    if let Some(name) = username {
        println!("用户名：{}", name);
    }
}
```

相当于只处理：

```
Some
```

而忽略 `None` 。

如果还需要处理 `None` ：

```
if let Some(name) = username {
    println!("用户名：{}", name);
} else {
    println!("用户名不存在");
}
```

---

## 使用 unwrap() 获取值

可以使用：

```
unwrap()
```

直接获取内部值：

```
fn main() {
    let number = Some(100);

    let value = number.unwrap();

    println!("{}", value);
}
```

输出：

```
100
```

但是如果：

```
let number: Option<i32> = None;
```

再执行：

```
number.unwrap();
```

程序会 panic。

因此：

> 不确定一定有值时，不要随意使用 unwrap()。

---

## 使用 expect()

`expect()` 与 `unwrap()` 类似，但可以指定错误信息。

```
fn main() {
    let config = Some("127.0.0.1");

    let host = config.expect(
        "服务器地址不能为空"
    );

    println!("{}", host);
}
```

如果为 `None` ，错误信息会更加明确。

在测试代码或程序启动阶段，如果某个值理论上必须存在， `expect()` 通常比 `unwrap()` 更容易排查问题。

---

## 使用 unwrap\_or() 设置默认值

如果值不存在，可以提供默认值：

```
fn main() {
    let score: Option<i32> = None;

    let value = score.unwrap_or(0);

    println!("{}", value);
}
```

输出：

```
0
```

如果：

```
let score = Some(90);
```

则得到：

```
90
```

---

## unwrap\_or\_else()

如果默认值需要通过计算获得，可以使用：

```
unwrap_or_else()
```
```
fn default_name() -> String {
    String::from("游客")
}

fn main() {
    let username: Option<String> = None;

    let name = username
        .unwrap_or_else(default_name);

    println!("{}", name);
}
```

只有在 `None` 时，才会调用默认值函数。

---

## 使用 map() 转换 Option

假设：

```
let value = Some(10);
```

想把内部数字乘以 2。

可以使用：

```
map()
```
```
fn main() {
    let value = Some(10);

    let result =
        value.map(|number| number * 2);

    println!("{:?}", result);
}
```

输出：

```
Some(20)
```

如果原值是：

```
None
```

则结果仍然是：

```
None
```

所以 `map()` 可以理解为：

> 有值就处理，没有值就继续保持 None。

---

## Option 与字符串处理

例如：

```
fn main() {
    let username =
        Some(String::from("tom"));

    let result = username.map(|name| {
        name.to_uppercase()
    });

    println!("{:?}", result);
}
```

输出：

```
Some("TOM")
```

---

## 使用 and\_then()

有时候一次操作之后，仍然可能没有值。

例如：

```
fn parse_age(text: &str)
    -> Option<u32>
{
    text.parse::<u32>().ok()
}
```

进一步处理：

```
fn valid_age(age: u32)
    -> Option<u32>
{
    if age <= 150 {
        Some(age)
    } else {
        None
    }
}
```

可以组合：

```
fn main() {
    let result = parse_age("20")
        .and_then(valid_age);

    println!("{:?}", result);
}
```

输出：

```
Some(20)
```

如果输入：

```
abc
```

或者年龄超过限制，都会得到：

```
None
```

---

## 使用 Option 查询 Vec

`Vec::get()` 返回：

```
Option<&T>
```

示例：

```
fn main() {
    let numbers = vec![10, 20, 30];

    match numbers.get(5) {
        Some(value) => {
            println!("值：{}", value);
        }
        None => {
            println!("索引不存在");
        }
    }
}
```

相比：

```
numbers[5]
```

`get()` 不会因为越界直接 panic。

---

## 使用 Option 查询 HashMap

```
use std::collections::HashMap;

fn main() {
    let mut users = HashMap::new();

    users.insert("Tom", 100);

    if let Some(score) = users.get("Tom") {
        println!("积分：{}", score);
    }
}
```

`get()` 返回：

```
Option<&i32>
```

因为对应的键可能不存在。

---

## 实战：查找最高成绩

```
fn find_max(scores: &[i32])
    -> Option<i32>
{
    if scores.is_empty() {
        return None;
    }

    let mut max = scores[0];

    for &score in scores {
        if score > max {
            max = score;
        }
    }

    Some(max)
}

fn main() {
    let scores = [80, 95, 72, 100];

    match find_max(&scores) {
        Some(max) => {
            println!("最高分：{}", max);
        }
        None => {
            println!("没有成绩");
        }
    }
}
```

如果切片为空：

```
[]
```

返回：

```
None
```

这样比返回：

```
0
```

更合理，因为 `0` 本身可能就是合法成绩。

---

## 实战：查询商品价格

```
use std::collections::HashMap;

fn find_price(
    products: &HashMap<String, f64>,
    name: &str,
) -> Option<f64> {
    products.get(name).copied()
}

fn main() {
    let mut products = HashMap::new();

    products.insert(
        String::from("键盘"),
        299.0,
    );

    products.insert(
        String::from("鼠标"),
        99.0,
    );

    match find_price(&products, "键盘") {
        Some(price) => {
            println!("价格：{:.2}", price);
        }
        None => {
            println!("商品不存在");
        }
    }
}
```

这里：

```
products.get(name)
```

得到：

```
Option<&f64>
```

调用：

```
copied()
```

可以转换为：

```
Option<f64>
```

因为 `f64` 实现了 `Copy` 。

---

## 常见错误

## 把 Option 当成普通值使用

错误：

```
let value = Some(10);

println!("{}", value + 1);
```

必须先处理 `Option` ：

```
if let Some(number) = value {
    println!("{}", number + 1);
}
```

---

## 滥用 unwrap()

不推荐：

```
let user = map.get("Tom").unwrap();
```

如果 `Tom` 不存在，程序会 panic。

更推荐：

```
match map.get("Tom") {
    Some(user) => {
        println!("{:?}", user);
    }
    None => {
        println!("用户不存在");
    }
}
```

---

## 用特殊值表示“没有数据”

例如：

```
fn find_score() -> i32 {
    -1
}
```

问题是：

```
-1
```

到底表示真实数据，还是不存在？

更加明确的设计是：

```
fn find_score() -> Option<i32>
```

---

## 最佳实践

如果值可能不存在，优先考虑：

```
Option<T>
```

例如：

```
fn find_user(id: u64)
    -> Option<User>
```

不要随意使用：

```
unwrap()
```

可以优先考虑：

```
match
if let
unwrap_or()
map()
and_then()
```

函数只需要表达“有没有值”时， `Option` 非常合适。

但如果不仅要告诉调用者失败，还需要说明：

> 为什么失败？

那么就应该使用：

```
Result<T, E>
```

---

## Option 和 Result 的区别

`Option` ：

```
Some(value)
None
```

表达：

```
有值 / 没值
```

例如：

```
HashMap::get()
Vec::get()
```

而 `Result` ：

```
Ok(value)
Err(error)
```

表达：

```
成功 / 失败，并携带错误原因
```

例如读取文件：

```
成功 -> 文件内容
失败 -> 文件不存在、权限不足等错误信息
```

可以简单理解：

> 不需要解释为什么没有值，使用 Option。

> 需要说明为什么失败，使用 Result。

---

## 本章小结

`Option<T>` 用来安全表达一个值可能存在，也可能不存在。

它包含：

```
Some(T)
```

和：

```
None
```

通过本文，我们学习了：

- • 什么是 `Option<T>`
- • `Some` 与 `None`
- • 为什么值不能直接与 `Option<T>` 混用
- • 使用 `match` 处理 Option
- • 使用 `if let` 简化代码
- • `unwrap()` 与 `expect()`
- • `unwrap_or()` 和 `unwrap_or_else()`
- • 使用 `map()` 转换值
- • 使用 `and_then()` 组合操作
- • `Vec::get()` 返回 Option
- • `HashMap::get()` 返回 Option
- • 使用 Option 设计安全的函数返回值
- • Option 和 Result 的区别

可以记住：

> `Option<T>` 不是一个需要绕开的麻烦，而是 Rust 强迫我们显式处理“没有数据”这种真实情况。

---

## 下一篇预告

下一篇我们将学习 **Rust Result 详解：错误处理的核心机制** ，包括：

- • 什么是 `Result<T, E>`
- • `Ok` 与 `Err`
- • 使用 `match` 处理错误
- • `unwrap()` 与 `expect()`
- • `unwrap_or()` 与默认值
- • `?` 运算符
- • 错误传播
- • `Option` 与 `Result` 的区别
- • `parse()` 错误处理
- • 文件读取错误处理
- • 自定义错误
- • 实战：配置解析与业务校验

Rust 编程实战 · Table of Contents