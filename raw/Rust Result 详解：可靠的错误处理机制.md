---
title: "Rust Result 详解：可靠的错误处理机制"
source: "https://mp.weixin.qq.com/s?__biz=MzYzODE1NzUzMw==&mid=2247484500&idx=1&sn=0c48a17aa50263056d94e636fcb64a76&chksm=f0e753e6c790daf0e40a70dfe8e8fd5f36f74edba6ac4550e070c300d6187206c9d451ce9cda&cur_album_id=4602071361631748097&scene=189#wechat_redirect"
author:
published:
created: 2026-11-05
description: "《Rust 编程实战》系列第 22 篇在上一篇文章中，我们学习了：Option\x26lt;T\x26gt;它用于表示：一个值可能存"
tags:
  - "clippings"
---
程序员爱钓鱼 *Jul 27, 2026, 5:05 AM*

> 《Rust 编程实战》系列第 22 篇

在上一篇文章中，我们学习了：

```
Option<T>
```

它用于表示：

> 一个值可能存在，也可能不存在。

例如：

```
HashMap::get()
Vec::get()
```

返回：

```
Some(value)
None
```

但是实际开发中，很多问题不仅仅是“有没有值”，还需要知道：

> 为什么失败？

例如：

- • 文件不存在
- • 数据格式错误
- • 网络连接失败
- • 数据库查询失败
- • 用户输入非法
- • 权限不足

这时候 Rust 提供了：

```
Result<T, E>
```

它是 Rust 错误处理的核心类型。

本文将介绍：

- • 什么是 Result
- • Ok 与 Err
- • 使用 match 处理错误
- • unwrap 与 expect
- •? 运算符
- • 错误传播
- • Option 与 Result 区别
- • 自定义错误
- • 实战案例

---

## 什么是 Result？

`Result` 是 Rust 标准库中的枚举类型。

定义类似：

```
enum Result<T, E> {
    Ok(T),
    Err(E),
}
```

其中：

- • `T` 表示成功时返回的数据类型
- • `E` 表示失败时错误类型

例如：

成功：

```
Ok("文件内容")
```

失败：

```
Err("文件不存在")
```

---

## Result 的基本使用

示例：

```
fn divide(
    a: i32,
    b: i32,
) -> Result<i32, String> {

    if b == 0 {
        return Err(
            String::from("不能除以0")
        );
    }

    Ok(a / b)
}

fn main() {

    let result = divide(10, 2);

    println!("{:?}", result);
}
```

输出：

```
Ok(5)
```

如果：

```
divide(10, 0)
```

返回：

```
Err("不能除以0")
```

---

## 使用 match 处理 Result

最完整的处理方式：

```
fn main() {

    let result = divide(10, 0);

    match result {

        Ok(value) => {
            println!(
                "结果：{}",
                value
            );
        }

        Err(error) => {
            println!(
                "错误：{}",
                error
            );
        }
    }
}
```

输出：

```
错误：不能除以0
```

Rust 强制要求处理成功和失败两种情况。

---

## Result 与 Option 的区别

Option：

```
Some(value)
None
```

表示：

```
有数据 / 没数据
```

例如：

```
map.get()
```

---

Result：

```
Ok(value)
Err(error)
```

表示：

```
成功 / 失败
```

并且失败时携带原因。

例如：

文件读取：

成功：

```
Ok("hello")
```

失败：

```
Err("文件不存在")
```

简单理解：

| 类型 | 用途 |
| --- | --- |
| Option | 可能没有值 |
| Result | 可能发生错误 |

---

## 使用 unwrap()

如果确定一定成功，可以使用：

```
unwrap()
```

例如：

```
fn main() {

    let result: Result<i32, &str>
        = Ok(100);

    let value = result.unwrap();

    println!("{}", value);
}
```

输出：

```
100
```

但是如果：

```
let result: Result<i32, &str>
    = Err("失败");
```

执行：

```
result.unwrap();
```

程序会 panic。

因此：

> unwrap 适合测试代码，不适合处理用户输入和外部数据。

---

## 使用 expect()

`expect()` 与 `unwrap()` 类似，但可以提供错误说明。

```
fn main() {

    let value =
        "123"
        .parse::<i32>()
        .expect(
            "数字解析失败"
        );

    println!("{}", value);
}
```

如果失败：

错误信息：

```
数字解析失败
```

相比：

```
unwrap()
```

更容易定位问题。

---

## 使用 unwrap\_or()

提供默认值：

```
fn main() {

    let result:
        Result<i32, &str>
        = Err("失败");

    let value =
        result.unwrap_or(0);

    println!("{}", value);
}
```

输出：

```
0
```

如果成功：

```
Ok(100)
```

则返回：

```
100
```

---

## 使用? 运算符

Rust 中处理错误最常见的方式：

```
?
```

它可以自动传播错误。

例如：

```
use std::fs;

fn read_file()
    -> Result<String, std::io::Error>
{

    let content =
        fs::read_to_string(
            "data.txt"
        )?;

    Ok(content)
}
```

这段代码：

```
?
```

会自动完成：

如果成功：

```
Ok(content)
```

继续执行。

如果失败：

```
Err(error)
```

立即返回。

---

## 不使用? 的写法

上面的代码等价于：

```
use std::fs;

fn read_file()
    -> Result<String, std::io::Error>
{

    let result =
        fs::read_to_string(
            "data.txt"
        );

    match result {

        Ok(content) => {
            Ok(content)
        }

        Err(error) => {
            Err(error)
        }
    }
}
```

可以看到：

`?`

只是 Rust 提供的错误传播简写。

---

## 多个错误操作

实际项目中，经常有多个可能失败的步骤：

例如：

1. 1\. 读取文件
2. 2\. 解析数字
3. 3\. 计算结果

使用：

```
?
```

代码会更加清晰：

```
use std::fs;

fn calculate()
    -> Result<i32, Box<dyn std::error::Error>>
{

    let text =
        fs::read_to_string(
            "number.txt"
        )?;

    let number:
        i32 =
        text.trim()
            .parse()?;

    Ok(number * 2)
}
```

每一步失败都会自动返回错误。

---

## Result 与 Option 转换

有时候需要在两者之间转换。

## Result 转 Option

```
let result:
    Result<i32, String>
    = Ok(100);

let option =
    result.ok();
```

得到：

```
Some(100)
```

如果是：

```
Err(...)
```

得到：

```
None
```

---

## Option 转 Result

```
let option:
    Option<i32>
    = Some(100);

let result =
    option.ok_or(
        "没有数据"
    );
```

得到：

```
Ok(100)
```

---

## 自定义错误类型

实际项目中，不建议所有错误都使用：

```
String
```

通常会定义自己的错误类型。

例如：

```
#[derive(Debug)]
enum AppError {

    UserNotFound,

    InvalidPassword,

    DatabaseError,
}
```

函数：

```
fn login(
    username: &str
)
-> Result<(), AppError>
{

    if username.is_empty() {

        return Err(
            AppError::UserNotFound
        );
    }

    Ok(())
}
```

这样错误类型更加明确。

---

## 实战：用户注册校验

```
#[derive(Debug)]
enum RegisterError {

    EmptyName,

    InvalidAge,
}

fn register(
    name: &str,
    age: u32,
)
-> Result<(), RegisterError>
{

    if name.is_empty() {

        return Err(
            RegisterError::EmptyName
        );
    }

    if age < 18 {

        return Err(
            RegisterError::InvalidAge
        );
    }

    Ok(())
}

fn main() {

    match register(
        "Tom",
        20
    ) {

        Ok(_) => {
            println!(
                "注册成功"
            );
        }

        Err(error) => {
            println!(
                "注册失败：{:?}",
                error
            );
        }
    }
}
```

输出：

```
注册成功
```

---

## 实战：解析配置文件

假设配置：

```
port=8080
```

解析：

```
fn parse_port(
    text: &str
)
-> Result<u16, String>
{

    let parts:
        Vec<&str>
        =
        text.split('=')
            .collect();

    if parts.len() != 2 {

        return Err(
            String::from(
                "配置格式错误"
            )
        );
    }

    let port =
        parts[1]
        .parse::<u16>()
        .map_err(|_| {

            String::from(
                "端口格式错误"
            )

        })?;

    Ok(port)
}

fn main() {

    match parse_port(
        "port=8080"
    ) {

        Ok(port) => {
            println!(
                "端口：{}",
                port
            );
        }

        Err(error) => {
            println!(
                "{}",
                error
            );
        }
    }
}
```

输出：

```
端口：8080
```

---

## 常见错误

## 滥用 unwrap()

错误：

```
let user =
    find_user()
    .unwrap();
```

如果数据来自：

- • 用户输入
- • 网络请求
- • 文件
- • 数据库

不要直接 unwrap。

---

## 用错误字符串代替错误类型

不推荐：

```
Result<User, String>
```

大型项目更推荐：

```
Result<User, UserError>
```

错误类型更加明确。

---

## 忽略 Result

例如：

```
file.write(data);
```

编译器会提醒：

```
unused Result
```

因为写入可能失败。

应该处理：

```
file.write(data)?;
```

或者：

```
match file.write(data) {
    Ok(_) => {}
    Err(e) => {}
}
```

---

## 最佳实践

## 库代码优先返回 Result

例如：

```
fn load_config()
 -> Result<Config, ConfigError>
```

让调用者决定如何处理错误。

---

## 应用入口可以处理最终错误

例如：

```
fn main()
 -> Result<(), Box<dyn std::error::Error>>
{
    run()?;

    Ok(())
}
```

---

## 使用? 简化错误传播

推荐：

```
let data = read_file()?;
```

而不是大量：

```
match
```

嵌套。

---

## 自定义业务错误

大型项目建议：

```
enum Error {
    Database,
    Network,
    Permission,
}
```

便于统一管理。

---

## 本章小结

`Result<T, E>` 是 Rust 错误处理的核心。

通过本文，我们学习了：

- • Result 的结构
- • Ok 和 Err
- • match 处理错误
- • unwrap 和 expect
- • unwrap\_or 默认值
- •? 错误传播
- • Option 与 Result 转换
- • 自定义错误类型
- • 配置解析和注册校验案例

可以记住：

> Option 解决“有没有值”。

> Result 解决“成功还是失败，以及为什么失败”。

Rust 不隐藏错误，而是要求程序明确处理错误，这也是 Rust 程序稳定、安全的重要原因。

---

## 下一篇预告

下一篇将学习：

## Rust panic 详解：不可恢复错误与程序崩溃处理

内容包括：

- • 什么是 panic
- • panic! 宏
- • panic 发生场景
- • backtrace 调试
- • unwrap 引发 panic
- • panic 与 Result 的区别
- • recover 思想
- • abort 与 unwind
- • 什么时候应该 panic
- • 实战错误定位

Rust 编程实战 · Table of Contents