# Rust 字符串返回类型官方资料查阅记录（2026-11-05）

本文件是官方资料查阅笔记，不是原文副本。问题：函数返回字符串时应选 `String` 还是 `&str`？

## 查阅资料

- Rust Book，所有权与返回值：https://doc.rust-lang.org/book/ch04-01-what-is-ownership.html
- Rust Book，字符串切片与从输入借用的返回值：https://doc.rust-lang.org/book/ch04-03-slices.html
- Rust Book，返回引用的生命周期与局部值限制：https://doc.rust-lang.org/book/ch10-03-lifetime-syntax.html
- Rust 官方错误解释 E0515（不得返回局部值引用）：https://doc.rust-lang.org/error_codes/E0515.html
- Rust Reference，生命周期省略规则：https://doc.rust-lang.org/reference/lifetime-elision.html
- Rust 标准库 `str`（字面量的 `'static` 生命周期）：https://doc.rust-lang.org/std/primitive.str.html
- Rust 标准库 `Cow`（借用或拥有）：https://doc.rust-lang.org/std/borrow/enum.Cow.html

## 核对结果

- `String` 拥有文本；返回它把所有权交给调用者。返回已有 `String` 的 move 不要求克隆其堆内容。
- `&str` 是借用视图。若返回输入的切片，输出引用的有效期受输入约束。只有一个输入引用的简单签名通常可省略显式生命周期标注；多个可能来源时须明确关系。
- 局部创建的 `String` 在函数退出时析构，不能返回指向它的 `&str`；生命周期标注不能延长局部值。
- 字符串字面量可以返回为 `&'static str`。`Cow<'a, str>` 可表示结果有时借自输入、有时需要拥有新字符串。

## 边界

- 此处给出通用 API 选择原则，具体返回类型还取决于调用方是否需要跨越源数据生命周期、是否已有可转移的 `String`、以及是否要求只读视图。
- 本次未编译自写示例；答案中的代码按官方规则整理，目标项目仍应运行编译器核对。
