---
title: "Rust 切片 Slice 详解：安全访问连续数据"
source: "https://mp.weixin.qq.com/s?__biz=MzYzODE1NzUzMw==&mid=2247484470&idx=1&sn=84610b55c727021a891db950dd0e8725&chksm=f0e75384c790da929457da33a7b93955ee0012e986407618439f026a4aaeaf5bc5f9f07db6b7&cur_album_id=4602071361631748097&scene=189#wechat_redirect"
author:
published:
created: 2026-11-04
description: "《Rust 编程实战》系列第 17 篇在上一篇文章中，我们学习了元组 Tuple。"
tags:
  - "clippings"
---
程序员爱钓鱼 *Jul 22, 2026, 6:17 AM*

> 《Rust 编程实战》系列第 17 篇

在上一篇文章中，我们学习了元组 `Tuple` 。

这一篇继续学习 Rust 中非常重要的数据类型：

```
Slice
```

中文通常称为切片。

切片本身不拥有数据，而是对一段连续数据的引用。它可以指向：

- • 数组的一部分
- • `Vec` 的一部分
- • 字符串的一部分
- • 整个集合

切片的核心作用是：

> 在不复制数据的情况下，安全地访问一段连续内容。

本文将介绍：

- • 什么是切片
- • 数组切片 `&[T]`
- • 切片范围语法
- • 切片访问与遍历
- • 可变切片
- • 切片作为函数参数
- • 数组、 `Vec` 与切片的关系
- • 字符串切片 `&str`
- • UTF-8 字符串切片注意事项
- • 常见错误与实战案例

---

## 什么是切片？

先定义一个数组：

```
let numbers = [10, 20, 30, 40, 50];
```

如果只需要访问中间三个元素，可以创建切片：

```
fn main() {
    let numbers = [10, 20, 30, 40, 50];

    let slice = &numbers[1..4];

    println!("{:?}", slice);
}
```

输出：

```
[20, 30, 40]
```

这里：

```
&numbers[1..4]
```

表示借用数组中索引 `1` 到索引 `4` 之前的数据。

包含：

```
1、2、3
```

不包含索引 `4` 。

---

## 切片的类型

整数切片类型写作：

```
&[i32]
```

字符串切片类型写作：

```
&str
```

例如：

```
fn main() {
    let numbers = [10, 20, 30];

    let slice: &[i32] = &numbers[0..2];

    println!("{:?}", slice);
}
```

需要注意：

```
[i32; 3]
```

表示长度固定为 3 的数组。

而：

```
[i32]
```

表示一段长度不固定的连续整数数据。

切片通常不能单独存在，需要通过引用使用：

```
&[i32]
```

---

## 常见范围语法

假设数组如下：

```
let numbers = [10, 20, 30, 40, 50];
```

获取索引 1 到 3：

```
let slice = &numbers[1..4];
```

结果：

```
[20, 30, 40]
```

从开头到索引 2：

```
let slice = &numbers[..3];
```

结果：

```
[10, 20, 30]
```

从索引 2 到结尾：

```
let slice = &numbers[2..];
```

结果：

```
[30, 40, 50]
```

获取全部元素：

```
let slice = &numbers[..];
```

也可以使用包含结束位置的范围：

```
let slice = &numbers[1..=3];
```

结果同样是：

```
[20, 30, 40]
```

---

## 切片不会复制数据

创建切片时，不会重新复制一份数组数据。

```
fn main() {
    let numbers = [10, 20, 30, 40];

    let slice = &numbers[1..3];

    println!("原数组：{:?}", numbers);
    println!("切片：{:?}", slice);
}
```

切片通常可以理解为保存了：

- • 数据开始位置
- • 数据长度

因此创建切片的成本很低。

不过，切片依赖原始数据存在。如果原始数据失效，切片也不能继续使用。

Rust 编译器会通过借用检查保证这种关系安全。

---

## 获取切片长度

切片可以调用：

```
len()
```

例如：

```
fn main() {
    let numbers = [10, 20, 30, 40, 50];
    let slice = &numbers[1..4];

    println!("切片长度：{}", slice.len());
}
```

输出：

```
切片长度：3
```

还可以判断切片是否为空：

```
println!("{}", slice.is_empty());
```

---

## 访问切片元素

切片也可以使用索引访问：

```
fn main() {
    let numbers = [10, 20, 30, 40];
    let slice = &numbers[1..3];

    println!("{}", slice[0]);
    println!("{}", slice[1]);
}
```

输出：

```
20
30
```

需要注意，切片拥有自己的索引。

虽然 `slice` 来源于原数组的索引 `1..3` ，但在切片内部：

```
20 的索引是 0
30 的索引是 1
```

---

## 使用 get() 安全访问

直接使用索引时，如果越界会发生 panic。

```
let value = slice[10];
```

如果索引不确定，推荐使用：

```
get()
```

示例：

```
fn main() {
    let numbers = [10, 20, 30];
    let slice = &numbers[..];

    match slice.get(5) {
        Some(value) => {
            println!("找到元素：{}", value);
        }
        None => {
            println!("索引超出范围");
        }
    }
}
```

`get()` 返回：

```
Option<&T>
```

这样可以避免程序因为索引越界而直接崩溃。

---

## 使用 get() 安全创建切片

切片范围也可能越界。

错误示例：

```
let slice = &numbers[1..100];
```

可以使用 `get()` ：

```
fn main() {
    let numbers = [10, 20, 30, 40];

    match numbers.get(1..3) {
        Some(slice) => {
            println!("{:?}", slice);
        }
        None => {
            println!("切片范围无效");
        }
    }
}
```

输出：

```
[20, 30]
```

---

## 遍历切片

切片可以使用 `for` 遍历：

```
fn main() {
    let numbers = [10, 20, 30, 40];
    let slice = &numbers[1..];

    for number in slice {
        println!("{}", number);
    }
}
```

输出：

```
20
30
40
```

如果同时需要索引，可以使用：

```
fn main() {
    let numbers = [10, 20, 30];

    for (index, value) in numbers.iter().enumerate() {
        println!("{}：{}", index, value);
    }
}
```

---

## 可变切片

普通切片只能读取数据：

```
&[T]
```

如果需要修改原始数据，可以使用可变切片：

```
&mut [T]
```

示例：

```
fn main() {
    let mut numbers = [10, 20, 30, 40];

    let slice = &mut numbers[1..3];

    slice[0] = 200;
    slice[1] = 300;

    println!("{:?}", numbers);
}
```

输出：

```
[10, 200, 300, 40]
```

修改切片中的值，会直接修改原数组中的对应数据。

---

## 批量修改切片

```
fn double_values(numbers: &mut [i32]) {
    for number in numbers {
        *number *= 2;
    }
}

fn main() {
    let mut numbers = [10, 20, 30, 40];

    double_values(&mut numbers[1..3]);

    println!("{:?}", numbers);
}
```

输出：

```
[10, 40, 60, 40]
```

这里只修改了数组中间两个元素。

---

## 切片作为函数参数

假设函数只接收固定长度数组：

```
fn calculate(numbers: [i32; 3]) -> i32 {
    numbers[0] + numbers[1] + numbers[2]
}
```

这个函数只能接收长度为 3 的数组。

更通用的写法是使用切片：

```
fn calculate(numbers: &[i32]) -> i32 {
    let mut total = 0;

    for number in numbers {
        total += number;
    }

    total
}

fn main() {
    let first = [10, 20, 30];
    let second = [1, 2, 3, 4, 5];

    println!("{}", calculate(&first));
    println!("{}", calculate(&second));
}
```

参数：

```
&[i32]
```

可以接收任意长度的整数切片。

---

## 数组、Vec 与切片

切片既可以来自数组，也可以来自 `Vec` 。

数组切片：

```
fn main() {
    let numbers = [10, 20, 30, 40];

    let slice = &numbers[1..3];

    println!("{:?}", slice);
}
```

`Vec` 切片：

```
fn main() {
    let numbers = vec![10, 20, 30, 40];

    let slice = &numbers[1..3];

    println!("{:?}", slice);
}
```

函数接收切片后，不需要关心数据原来来自数组还是 `Vec` ：

```
fn print_numbers(numbers: &[i32]) {
    println!("{:?}", numbers);
}

fn main() {
    let array = [1, 2, 3];
    let vector = vec![4, 5, 6, 7];

    print_numbers(&array);
    print_numbers(&vector);
}
```

因此，切片参数非常适合编写通用函数。

---

## 字符串切片 &str

除了数组切片，Rust 中还有字符串切片：

```
&str
```

字符串字面量本身就是字符串切片：

```
fn main() {
    let language: &str = "Rust";

    println!("{}", language);
}
```

也可以从 `String` 中创建切片：

```
fn main() {
    let text = String::from("Hello Rust");

    let hello = &text[0..5];

    println!("{}", hello);
}
```

输出：

```
Hello
```

这里 `hello` 并不拥有新的字符串数据，只是引用 `text` 的一部分。

---

## UTF-8 字符串切片

Rust 字符串使用 UTF-8 编码。

这意味着中文字符通常占用多个字节。

例如：

```
fn main() {
    let text = String::from("你好Rust");

    println!("字节长度：{}", text.len());
}
```

`len()` 返回的是字节数，而不是字符数量。

因此下面的代码可能发生 panic：

```
let slice = &text[0..1];
```

因为索引 `1` 可能位于中文字符的中间。

正确做法是保证切片边界位于合法 UTF-8 字符边界上。

例如：

```
fn main() {
    let text = String::from("你好Rust");

    let slice = &text[0..3];

    println!("{}", slice);
}
```

通常一个中文字符占 3 个 UTF-8 字节，因此这里可以得到：

```
你
```

但实际开发中，不建议通过猜测字节数处理中文字符。

如果要按字符遍历，应使用：

```
chars()
```

例如：

```
fn main() {
    let text = "你好Rust";

    for character in text.chars() {
        println!("{}", character);
    }
}
```

---

## 使用 char\_indices() 获取字符位置

如果需要字符和字节索引，可以使用：

```
char_indices()
```
```
fn main() {
    let text = "你好Rust";

    for (index, character) in text.char_indices() {
        println!("字节索引 {}：{}", index, character);
    }
}
```

输出类似：

```
字节索引 0：你
字节索引 3：好
字节索引 6：R
字节索引 7：u
字节索引 8：s
字节索引 9：t
```

这说明字符串索引本质上是字节索引，而不是字符序号。

---

## 实战：计算切片统计数据

下面实现一个函数，同时计算总和、最大值和最小值：

```
fn analyze(
    numbers: &[i32],
) -> Option<(i32, i32, i32)> {
    if numbers.is_empty() {
        return None;
    }

    let mut total = 0;
    let mut min = numbers[0];
    let mut max = numbers[0];

    for &number in numbers {
        total += number;

        if number < min {
            min = number;
        }

        if number > max {
            max = number;
        }
    }

    Some((total, min, max))
}

fn main() {
    let numbers = [12, 30, 5, 88, 16];

    match analyze(&numbers[1..4]) {
        Some((total, min, max)) => {
            println!("总和：{}", total);
            println!("最小值：{}", min);
            println!("最大值：{}", max);
        }
        None => {
            println!("没有数据");
        }
    }
}
```

传入的切片是：

```
[30, 5, 88]
```

输出：

```
总和：123
最小值：5
最大值：88
```

---

## 常见错误

## 切片范围越界

错误：

```
let slice = &numbers[1..100];
```

范围超过原集合长度时会 panic。

范围不确定时，可以使用：

```
numbers.get(1..100)
```

---

## 开始位置大于结束位置

错误：

```
let slice = &numbers[4..2];
```

切片开始位置不能大于结束位置。

---

## 修改只读切片

错误：

```
let slice = &numbers[1..3];

slice[0] = 100;
```

只读切片不能修改数据。

需要使用：

```
let slice = &mut numbers[1..3];
```

同时原数组也必须声明为 `mut` 。

---

## 中文字符串按字符序号切片

错误思路：

```
let text = "你好";
let first = &text[0..1];
```

Rust 字符串索引是字节索引， `1` 可能处在字符内部。

处理 Unicode 字符时，应优先使用：

```
chars()
```

---

## 返回局部数组的切片

下面的思路是错误的：

```
fn create_slice() -> &[i32] {
    let numbers = [1, 2, 3];

    &numbers[..]
}
```

函数结束后，局部数组会被销毁，不能返回指向它的切片。

可以返回数组或 `Vec` ，也可以让函数借用外部数据后返回其中的切片。

---

## 最佳实践

## 函数参数优先使用切片

相比：

```
fn print(numbers: [i32; 5])
```

更推荐：

```
fn print(numbers: &[i32])
```

这样函数能够接收不同长度的数组和 `Vec` 。

---

## 不确定范围使用 get()

```
if let Some(slice) = numbers.get(start..end) {
    println!("{:?}", slice);
}
```

这比直接切片更加安全。

---

## 修改数据时使用可变切片

```
fn reset(values: &mut [i32]) {
    values.fill(0);
}
```

这样既不会取得整个集合的所有权，也能修改指定数据。

---

## 字符串参数优先考虑 &str

函数只需要读取文本时，通常使用：

```
fn print_text(text: &str)
```

而不是强制要求：

```
fn print_text(text: String)
```

`&str` 可以接收字符串字面量，也可以接收 `String` 的切片。

---

## 本章小结

切片是对连续数据的一段引用，它本身不拥有数据。

通过本文，我们学习了：

- • 数组切片 `&[T]`
- • 字符串切片 `&str`
- • 范围语法 `..`和 `..=`
- • 切片长度与索引
- • `get()` 安全访问
- • 切片遍历
- • 可变切片 `&mut [T]`
- • 切片作为函数参数
- • 数组、 `Vec` 和切片的关系
- • UTF-8 字符串切片的注意事项
- • 使用 `chars()` 处理 Unicode 字符

可以记住：

> 数组和 `Vec` 负责拥有数据。

> 切片负责借用并访问一部分数据。

切片是 Rust 借用机制中非常重要的一部分，后续在字符串、集合、函数参数和网络数据处理中都会频繁使用。

---

## 下一篇预告

下一篇我们将学习 **Rust String 与 &str 详解** ，包括：

- • `String` 与 `&str` 的区别
- • 字符串字面量
- • 创建和修改 `String`
- • `push()` 与 `push_str()`
- • 字符串拼接
- • 所有权与借用
- • `String` 转换为 `&str`
- • `&str` 转换为 `String`
- • UTF-8 与中文字符
- • 字符串遍历
- • 字节、字符和字形的区别
- • 实战：文本清洗与命令解析

Rust 编程实战 · Table of Contents