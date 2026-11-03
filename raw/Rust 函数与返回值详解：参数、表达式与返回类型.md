---
title: "Rust 函数与返回值详解：参数、表达式与返回类型"
source: "https://mp.weixin.qq.com/s?__biz=MzYzODE1NzUzMw==&mid=2247484435&idx=1&sn=61713186a75582aaa9d6630a4554aafb&chksm=f0e753a1c790dab7a623218a0e0945f61048a93265ddd62d9fa0bbfa7768e50fec63e01a94d5&cur_album_id=4602071361631748097&scene=189#wechat_redirect"
author:
published:
created: 2026-11-03
description: "《Rust 编程实战》系列第 9 篇在前面的文章中，我们已经学习了变量、数据类型、常量和静态变量。"
tags:
  - "clippings"
---
程序员爱钓鱼 *Jul 14, 2026, 4:13 AM*

> 《Rust 编程实战》系列第 9 篇

在前面的文章中，我们已经学习了变量、数据类型、常量和静态变量。

接下来，我们需要解决一个非常重要的问题：

> 如何把一段功能独立出来，并在程序中的多个地方重复使用？

答案就是： **函数（Function）** 。

函数是组织 Rust 程序最基本的方式之一。无论是命令行工具、Web 服务、桌面软件还是企业级项目，最终都会由大量函数共同组成。

本文将详细介绍：

- • 如何定义函数
- • 如何传递参数
- • 如何声明参数类型
- • 如何返回数据
- • Rust 中语句和表达式的区别
- • `return` 与隐式返回的区别
- • 单元类型 `()`
- • 函数的常见错误和最佳实践

---

## 什么是函数？

函数可以理解为一段完成特定任务的代码。

例如：

```
fn say_hello() {
    println!("Hello, Rust!");
}
```

这里定义了一个名为：

```
say_hello
```

的函数。

它的功能是输出：

```
Hello, Rust!
```

函数定义后不会自动执行，必须调用它。

完整代码如下：

```
fn main() {
    say_hello();
}

fn say_hello() {
    println!("Hello, Rust!");
}
```

运行结果：

```
Hello, Rust!
```

---

## fn 关键字

Rust 使用：

```
fn
```

定义函数。

基本语法如下：

```
fn 函数名() {
    // 函数体
}
```

例如：

```
fn print_message() {
    println!("正在学习 Rust");
}
```

调用函数：

```
print_message();
```

函数名通常使用蛇形命名法，也就是：

```
snake_case
```

例如：

```
fn get_user_name() {}

fn calculate_total_price() {}

fn save_order_data() {}
```

不推荐：

```
fn GetUserName() {}
```

---

## main 函数

每个 Rust 可执行程序都需要一个入口函数：

```
fn main() {
}
```

程序启动时，会首先执行 `main` 函数。

例如：

```
fn main() {
    println!("程序开始运行");
}
```

对于普通可执行项目来说， `main` 函数是必须存在的。

不过，库项目通常使用：

```
src/lib.rs
```

而不需要 `main` 函数。

---

## 函数可以定义在 main 后面吗？

可以。

例如：

```
fn main() {
    say_hello();
}

fn say_hello() {
    println!("Hello");
}
```

也可以写在 `main` 前面：

```
fn say_hello() {
    println!("Hello");
}

fn main() {
    say_hello();
}
```

Rust 不要求函数必须先定义再调用。

只要函数位于当前模块中，编译器就可以找到它。

---

## 函数参数

函数可以接收外部传入的数据，这些数据称为参数。

例如：

```
fn greet(name: &str) {
    println!("你好，{}！", name);
}
```

调用：

```
fn main() {
    greet("Tom");
    greet("Alice");
}
```

输出：

```
你好，Tom！
你好，Alice！
```

这里：

```
name: &str
```

表示函数接收一个名为 `name` 的参数，类型是 `&str` 。

---

## Rust 函数参数必须指定类型

Rust 不允许省略函数参数类型。

错误写法：

```
fn greet(name) {
    println!("{}", name);
}
```

编译器无法知道 `name` 的类型。

正确写法：

```
fn greet(name: &str) {
    println!("{}", name);
}
```

这是 Rust 与部分动态语言不同的地方。

变量可以通过初始值推导类型：

```
let age = 18;
```

但函数参数必须明确写出类型：

```
fn show_age(age: i32) {
    println!("{}", age);
}
```

---

## 多个函数参数

函数可以接收多个参数。

例如：

```
fn print_user(name: &str, age: u8) {
    println!("姓名：{}，年龄：{}", name, age);
}
```

调用：

```
fn main() {
    print_user("Tom", 20);
}
```

输出：

```
姓名：Tom，年龄：20
```

每个参数都必须指定类型：

```
fn print_user(name: &str, age: u8)
```

参数之间使用逗号分隔。

---

## 参数顺序必须一致

例如：

```
fn print_user(name: &str, age: u8) {
    println!("{} {}", name, age);
}
```

正确调用：

```
print_user("Alice", 18);
```

错误调用：

```
print_user(18, "Alice");
```

因为参数位置和类型不匹配。

Rust 会在编译阶段报错，而不是等程序运行时才发现问题。

---

## 函数返回值

函数除了执行操作，也可以返回结果。

例如：

```
fn add(a: i32, b: i32) -> i32 {
    a + b
}
```

这里：

```
-> i32
```

表示函数返回一个 `i32` 类型的值。

调用：

```
fn main() {
    let result = add(10, 20);

    println!("{}", result);
}
```

输出：

```
30
```

---

## 返回值语法

Rust 函数返回值的语法如下：

```
fn 函数名(参数) -> 返回类型 {
    返回值
}
```

例如：

```
fn get_age() -> u8 {
    18
}
```

调用：

```
fn main() {
    let age = get_age();

    println!("{}", age);
}
```

输出：

```
18
```

---

## 为什么返回值后面没有分号？

这是 Rust 初学者最容易困惑的地方。

正确写法：

```
fn add(a: i32, b: i32) -> i32 {
    a + b
}
```

错误写法：

```
fn add(a: i32, b: i32) -> i32 {
    a + b;
}
```

区别就在于最后的分号。

在 Rust 中：

```
a + b
```

是表达式，会产生一个值。

而：

```
a + b;
```

加上分号后，就变成了语句，不再返回这个值。

---

## 语句与表达式

理解函数返回值，必须理解 Rust 中的两个概念：

- • 语句（Statement）
- • 表达式（Expression）

## 语句

语句执行操作，但通常不返回有意义的值。

例如：

```
let x = 10;
```

这是一个语句。

再例如：

```
println!("Hello");
```

也是一个语句。

---

## 表达式

表达式会计算并产生一个值。

例如：

```
10 + 20
```

结果是：

```
30
```

再例如：

```
{
    let x = 10;
    x + 1
}
```

整个代码块的值是：

```
11
```

---

## 代码块也可以返回值

Rust 中的大括号代码块本身也是表达式。

例如：

```
fn main() {
    let result = {
        let a = 10;
        let b = 20;

        a + b
    };

    println!("{}", result);
}
```

输出：

```
30
```

这里代码块最后一行：

```
a + b
```

没有分号，因此这个值成为整个代码块的结果。

---

## 使用 return 返回值

Rust 也支持 `return` 关键字。

例如：

```
fn add(a: i32, b: i32) -> i32 {
    return a + b;
}
```

注意：

使用 `return` 时，后面通常需要分号：

```
return a + b;
```

这与隐式返回不同。

隐式返回：

```
fn add(a: i32, b: i32) -> i32 {
    a + b
}
```

显式返回：

```
fn add(a: i32, b: i32) -> i32 {
    return a + b;
}
```

两种写法结果相同。

---

## 什么时候使用 return？

如果返回值位于函数最后一行，通常推荐使用隐式返回：

```
fn multiply(a: i32, b: i32) -> i32 {
    a * b
}
```

如果需要提前结束函数，则使用 `return` 。

例如：

```
fn get_level(score: i32) -> &'static str {
    if score < 0 {
        return "分数无效";
    }

    if score >= 90 {
        return "优秀";
    }

    if score >= 60 {
        return "及格";
    }

    "不及格"
}
```

这里多个分支都可能提前返回。

---

## if 也可以作为表达式

Rust 中的 `if` 不只是控制语句，也可以返回值。

例如：

```
fn get_status(age: u8) -> &'static str {
    if age >= 18 {
        "成年人"
    } else {
        "未成年人"
    }
}
```

调用：

```
fn main() {
    let status = get_status(20);

    println!("{}", status);
}
```

输出：

```
成年人
```

还可以直接赋值：

```
fn main() {
    let age = 20;

    let status = if age >= 18 {
        "成年人"
    } else {
        "未成年人"
    };

    println!("{}", status);
}
```

---

## if 各分支类型必须一致

例如：

```
let value = if true {
    10
} else {
    20
};
```

这是合法的，因为两个分支都是整数。

下面的代码会报错：

```
let value = if true {
    10
} else {
    "hello"
};
```

因为一个分支返回整数，另一个分支返回字符串。

Rust 无法为变量确定统一类型。

---

## 没有返回值的函数

有些函数只执行操作，不需要返回数据。

例如：

```
fn print_message() {
    println!("Hello");
}
```

这类函数实际上也有返回类型，只是返回的是：

```
()
```

它称为：

**单元类型（Unit Type）** 。

上面的函数也可以写成：

```
fn print_message() -> () {
    println!("Hello");
}
```

一般情况下不需要显式写出来。

---

## 单元类型 ()

`()` 表示没有实际数据的返回值。

例如：

```
fn do_nothing() -> () {
}
```

也可以：

```
fn do_nothing() {
}
```

两者等价。

单元类型在 Rust 中经常出现，例如：

- • 普通打印函数
- • 修改外部状态的函数
- • 没有返回数据的回调
- • `Result<(), E>` 中表示成功但不返回内容

例如：

```
fn save_data() -> Result<(), String> {
    println!("保存成功");

    Ok(())
}
```

这里：

```
Ok(())
```

表示操作成功，但没有额外数据需要返回。

---

## 返回多个值

Rust 函数只能返回一个值，但可以借助元组返回多个数据。

例如：

```
fn get_user() -> (&'static str, u8, bool) {
    ("Tom", 20, true)
}
```

调用：

```
fn main() {
    let user = get_user();

    println!("姓名：{}", user.0);
    println!("年龄：{}", user.1);
    println!("状态：{}", user.2);
}
```

也可以解构：

```
fn main() {
    let (name, age, active) = get_user();

    println!("{} {} {}", name, age, active);
}
```

---

## 实战：计算商品总价

下面写一个简单的函数，计算商品总价。

```
fn calculate_total(price: f64, quantity: u32) -> f64 {
    price * quantity as f64
}

fn main() {
    let total = calculate_total(29.9, 3);

    println!("商品总价：{:.2}", total);
}
```

输出：

```
商品总价：89.70
```

这里：

```
quantity as f64
```

把 `u32` 转换为 `f64` ，这样才能与价格相乘。

---

## 实战：计算折扣价格

```
fn calculate_discount_price(price: f64, discount: f64) -> f64 {
    if discount <= 0.0 || discount > 1.0 {
        return price;
    }

    price * discount
}

fn main() {
    let final_price = calculate_discount_price(100.0, 0.8);

    println!("折后价格：{:.2}", final_price);
}
```

输出：

```
折后价格：80.00
```

当折扣值无效时，函数会提前返回原价。

---

## 实战：判断数字是否为偶数

```
fn is_even(number: i32) -> bool {
    number % 2 == 0
}

fn main() {
    let result = is_even(10);

    println!("是否为偶数：{}", result);
}
```

输出：

```
是否为偶数：true
```

这里：

```
number % 2 == 0
```

本身就是一个布尔表达式，因此可以直接作为返回值。

不需要写成：

```
if number % 2 == 0 {
    true
} else {
    false
}
```

前一种写法更简洁。

---

## 函数参数与变量可变性

函数参数默认也是不可变的。

例如：

```
fn increase(number: i32) {
    number += 1;
}
```

会报错，因为 `number` 不可变。

可以改成：

```
fn increase(mut number: i32) {
    number += 1;

    println!("{}", number);
}
```

这里的 `mut` 只表示函数内部的参数变量可以修改。

完整示例：

```
fn increase(mut number: i32) {
    number += 1;

    println!("函数内部：{}", number);
}

fn main() {
    let number = 10;

    increase(number);

    println!("函数外部：{}", number);
}
```

输出：

```
函数内部：11
函数外部：10
```

为什么外部还是 10？

因为整数类型默认会复制一份传入函数。函数内部修改的是参数副本，不是外部变量。

这个问题与 Rust 的所有权和 `Copy` 类型有关，后续会详细学习。

---

## 函数调用必须匹配返回类型

例如：

```
fn get_age() -> i32 {
    "18"
}
```

会报错。

因为函数声明返回：

```
i32
```

实际却返回：

```
&str
```

正确写法：

```
fn get_age() -> i32 {
    18
}
```

Rust 会在编译阶段检查返回值类型。

---

## 常见错误

## 参数没有指定类型

错误：

```
fn add(a, b) {
    println!("{}", a + b);
}
```

正确：

```
fn add(a: i32, b: i32) {
    println!("{}", a + b);
}
```

---

## 返回表达式后加了分号

错误：

```
fn add(a: i32, b: i32) -> i32 {
    a + b;
}
```

正确：

```
fn add(a: i32, b: i32) -> i32 {
    a + b
}
```

或者：

```
fn add(a: i32, b: i32) -> i32 {
    return a + b;
}
```

---

## 返回值类型不一致

错误：

```
fn get_value(ok: bool) -> i32 {
    if ok {
        10
    } else {
        "error"
    }
}
```

两个分支必须返回相同类型。

正确：

```
fn get_value(ok: bool) -> i32 {
    if ok {
        10
    } else {
        0
    }
}
```

---

## 调用函数时参数数量不一致

函数定义：

```
fn add(a: i32, b: i32) -> i32 {
    a + b
}
```

错误调用：

```
add(10);
```

或者：

```
add(10, 20, 30);
```

参数数量必须完全一致。

---

## 把打印结果当作返回值

例如：

```
fn add(a: i32, b: i32) -> i32 {
    println!("{}", a + b);
}
```

`println!` 的返回值是 `()` ，不是 `i32` 。

正确写法：

```
fn add(a: i32, b: i32) -> i32 {
    a + b
}
```

打印应该放在调用位置：

```
fn main() {
    let result = add(10, 20);

    println!("{}", result);
}
```

---

## 函数设计最佳实践

## 一个函数只做一件事

不推荐把登录、保存数据、发送邮件和写日志全部放在一个函数里。

推荐拆分：

```
fn validate_user() {}

fn save_user() {}

fn send_email() {}

fn write_log() {}
```

这样代码更容易测试和维护。

---

## 函数名要表达意图

不推荐：

```
fn do_it() {}
```

推荐：

```
fn calculate_order_total() {}

fn find_user_by_id() {}

fn create_access_token() {}
```

看到函数名就能理解它的用途。

---

## 参数不要过多

如果一个函数有大量参数：

```
fn create_user(
    name: String,
    age: u8,
    email: String,
    phone: String,
    city: String,
    address: String,
) {
}
```

后续可以考虑使用结构体：

```
struct CreateUserRequest {
    name: String,
    age: u8,
    email: String,
    phone: String,
    city: String,
    address: String,
}
```

然后函数只接收一个参数：

```
fn create_user(request: CreateUserRequest) {
}
```

---

## 优先返回结果，而不是在函数内部直接打印

不推荐：

```
fn add(a: i32, b: i32) {
    println!("{}", a + b);
}
```

更推荐：

```
fn add(a: i32, b: i32) -> i32 {
    a + b
}
```

这样调用方可以决定如何使用结果：

```
let result = add(10, 20);

println!("{}", result);
```

也可以继续参与计算：

```
let total = add(10, 20) * 2;
```

---

## 完整练习

下面是一个简单的订单金额计算程序。

```
fn calculate_subtotal(price: f64, quantity: u32) -> f64 {
    price * quantity as f64
}

fn calculate_discount(subtotal: f64, discount_rate: f64) -> f64 {
    if discount_rate <= 0.0 || discount_rate > 1.0 {
        return subtotal;
    }

    subtotal * discount_rate
}

fn calculate_shipping(final_price: f64) -> f64 {
    if final_price >= 99.0 {
        0.0
    } else {
        10.0
    }
}

fn main() {
    let price = 39.9;
    let quantity = 3;
    let discount_rate = 0.9;

    let subtotal = calculate_subtotal(price, quantity);
    let discounted_price = calculate_discount(subtotal, discount_rate);
    let shipping = calculate_shipping(discounted_price);
    let total = discounted_price + shipping;

    println!("商品小计：{:.2}", subtotal);
    println!("折后金额：{:.2}", discounted_price);
    println!("运费：{:.2}", shipping);
    println!("订单总额：{:.2}", total);
}
```

可能输出：

```
商品小计：119.70
折后金额：107.73
运费：0.00
订单总额：107.73
```

这个示例将不同功能拆分成多个函数：

- • `calculate_subtotal` ：计算商品小计
- • `calculate_discount` ：计算折扣金额
- • `calculate_shipping` ：计算运费

这就是函数最重要的价值： **拆分复杂逻辑，让代码更容易理解和复用。**

---

## 本章小结

函数是 Rust 程序组织代码的基础。

通过本文，我们学习了：

- • 使用 `fn` 定义函数
- • 函数命名规范
- • 函数参数和参数类型
- • 使用 `->` 声明返回类型
- • 隐式返回和 `return`
- • 语句与表达式的区别
- • 为什么返回表达式不能加分号
- • 单元类型 `()`
- • 使用元组返回多个值
- • `if` 表达式返回值
- • 函数参数的可变性
- • 常见错误与函数设计实践

其中最重要的一点是：

> Rust 函数体最后一个不带分号的表达式，会成为函数的返回值。

理解表达式和返回值之后，后面学习控制流、闭包、错误处理和所有权都会更加轻松。

---

## 下一篇预告

下一篇我们将学习 **Rust 注释与文档注释** ，包括：

- • 普通单行注释
- • 多行注释
- • 文档注释 `///`
- • 模块文档注释 `//!`
- • Markdown 文档
- • 文档代码示例
- • 使用 `cargo doc` 生成项目文档
- • 如何编写高质量的 Rust API 文档

Rust 编程实战 · Table of Contents