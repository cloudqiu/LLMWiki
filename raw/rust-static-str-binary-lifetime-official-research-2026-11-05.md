# Rust `&'static str` 与 binary 官方资料查阅记录（2026-11-05）

本文件是官方资料查阅笔记，不是官网原文副本。问题：返回 `&'static str` 是否意味着函数或文本必须在编译时已进入 binary？

## 查阅资料

- Rust 标准库 `reference`：https://doc.rust-lang.org/std/primitive.reference.html
- Rust Book 生命周期章节：https://doc.rust-lang.org/book/ch10-03-lifetime-syntax.html
- Rust Reference 字符串字面量：https://doc.rust-lang.org/reference/expressions/literal-expr.html
- Rust 标准库 `Box::leak`：https://doc.rust-lang.org/std/boxed/struct.Box.html
- Rust 标准库 `include_str!`：https://doc.rust-lang.org/std/macro.include_str.html

## 核对结果

- `&'static str` 约束被引用的字符串数据可在程序剩余生命周期内保持有效，不表示数据一定在编译时已知。字符串**字面量**是典型来源，Rust 官方文档说其文本存于程序 binary。
- `include_str!` 在编译时包含文件文本，表达式也得到 `&'static str`。
- `Box::leak(input.to_owned().into_boxed_str())` 可以从运行时输入生成 `&'static str`，因为分配的内存被有意保留，不在正常作用域结束时释放；这有永久占用内存的代价，不应仅为消除生命周期错误而使用。
- `fn greeting() -> &'static str { "hello" }` 的函数字节码可能被普通编译器优化内联或移除；返回类型的生命周期规则不规定函数必须以独立符号存在于 binary。

## 验证

- 使用本机 `rustc --edition=2021` 编译运行字面量与 `Box::leak` 两种返回值的最小程序；断言均通过。测试程序在临时目录，未加入知识库。
