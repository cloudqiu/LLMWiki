# Rust `Box::leak(input.to_owned().into_boxed_str())` 官方资料查阅记录（2026-11-05）

本文件是官方资料查阅笔记，不是官网原文副本。问题：此调用链的每一步做什么？

## 查阅资料

- `ToOwned` 文档：https://doc.rust-lang.org/std/borrow/trait.ToOwned.html
- `String::into_boxed_str` 文档：https://doc.rust-lang.org/std/string/struct.String.html
- `Box::leak` 文档：https://doc.rust-lang.org/std/boxed/struct.Box.html

## 核对结果

- `input: &str` 是借用；`input.to_owned()` 生成拥有文本的 `String`，复制输入字节，使结果不再依赖输入的生命周期。
- `String::into_boxed_str(self)` 消费 `String` 并返回 `Box<str>`。它会丢弃多余容量，标准库明确提示这一步可能重新分配并复制字节，不能保证零拷贝。
- `Box::leak(boxed)` 消费 `Box<str>`，返回 `&mut str`，在类型允许时可取 `'static` 生命周期；函数返回 `&'static str` 时可从可变引用强制转换为共享引用。
- 被泄漏的分配不再由 `Box` 正常释放。每次调用都可能保留一份分配；普通函数通常应直接返回 `String`，该链主要用于确有意图保留数据到程序结束的场景。
