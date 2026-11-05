---
title: "Rust 函数返回字符串时选 String 还是 &str？"
type: answer
created: 2026-11-05
updated: 2026-11-05
tags: [rust, strings, ownership, borrowing, lifetimes]
status: growing
sources:
  - raw/rust-string-return-ownership-official-research-2026-11-05.md
  - raw/rust-static-str-binary-lifetime-official-research-2026-11-05.md
  - raw/Rust String 与 &str 详解：字符串所有权、借用与转换.md
  - raw/Rust 所有权 Ownership 详解：理解内存安全的核心机制.md
---

# Rust 函数返回字符串时选 `String` 还是 `&str`？

> 归档自 2026-11-05 的查询；关联 [[rust-string-str-clipping]] 与 [[rust-ownership-clipping]]。

## 回答

看**结果的所有权来自哪里**：

| 情况 | 返回类型 | 原因 |
| --- | --- | --- |
| 结果是输入文本的一段或原样借用 | `&str` | 借用输入，不制造独立拥有者；调用者不能比输入活得更久。 |
| 函数创建、拼接、转换文本并交给调用者持有 | `String` | 新文本由调用者拥有，可以独立于输入存在。 |
| 返回固定字面量 | `&'static str` | 字面量在程序运行期间有效。 |
| 有时借用输入、有时需要生成新文本 | `Cow<'a, str>` | 统一表达借用和拥有；有额外 API 复杂度。 |

借用输入的示例：

```rust
fn first_word(s: &str) -> &str {
    s.split_whitespace().next().unwrap_or("")
}
```

这里只有一个输入引用，输出生命周期可由规则省略；效果相当于 `fn first_word<'a>(s: &'a str) -> &'a str`。返回值借自 `s`，所以不能在原字符串失效后使用它。[Rust Book：切片](https://doc.rust-lang.org/book/ch04-03-slices.html)、[生命周期](https://doc.rust-lang.org/book/ch10-03-lifetime-syntax.html)。

新建结果的示例：

```rust
fn label(name: &str) -> String {
    format!("用户：{name}")
}
```

这里返回的是新建的文本；调用者获得所有权。若函数**已经拥有**一个 `String`，直接返回它也是所有权转移，不必为了返回而 `clone()`。[Rust Book：返回值与所有权](https://doc.rust-lang.org/book/ch04-01-what-is-ownership.html)。

### 有时借用、有时新建：`Cow<'a, str>`

下面只演示替换 `&`，不是完整的 HTML 转义器：

```rust
use std::borrow::Cow;

fn escape_ampersands(input: &str) -> Cow<'_, str> {
    if input.contains('&') {
        Cow::Owned(input.replace('&', "&amp;"))
    } else {
        Cow::Borrowed(input)
    }
}

fn main() {
    let plain = escape_ampersands("Rust");
    let escaped = escape_ampersands("A&B");
    assert!(matches!(plain, Cow::Borrowed("Rust")));
    assert!(matches!(escaped, Cow::Owned(_)));
    assert_eq!(escaped, "A&amp;B");
}
```

`"Rust"` 不含 `&`，结果直接借用输入，没有为结果复制文本；`"A&B"` 需要替换，`replace` 新建 `String`，由 `Cow::Owned` 持有。`Cow<'_, str>` 让两个分支共用一个返回类型；借用分支仍受输入生命周期约束。调用者如需无论哪个分支都独立持有，可调用 `.into_owned()`，借用分支届时才复制。这个示例已用本机 `rustc --edition=2021` 编译运行，断言通过。[标准库 `Cow`](https://doc.rust-lang.org/std/borrow/enum.Cow.html)。

`Cow` 是 **Clone on Write** 的缩写，即“写入时才克隆”。它可以先持有借用数据；若调用 `to_mut()` 请求可变访问，借用分支才克隆成拥有的数据。已经是 `Cow::Owned` 时不需再次克隆。上面的 `escape_ampersands` 示例通过条件分支直接构造 `Borrowed` / `Owned`，没有调用 `to_mut()`，但使用的是同一个可借用或拥有的类型。[标准库 `Cow`](https://doc.rust-lang.org/std/borrow/enum.Cow.html)。

不能返回局部 `String` 的借用：

```rust
// 错误示意：
fn bad() -> &'static str {
    let s = String::from("hello");
    s.as_str()
}
```

`s` 在函数结束时被释放；返回引用会悬空。把返回类型改成 `String` 并返回 `s`，才把数据交给调用者。给 `&str` 补生命周期标注也不能让局部 `s` 活得更久。[Rust E0515](https://doc.rust-lang.org/error_codes/E0515.html)。

## 易混边界

- 返回字面量可写 `fn status() -> &'static str { "ok" }`；这不适用于函数中新建的 `String`。[标准库 `str`](https://doc.rust-lang.org/std/primitive.str.html)。
- 若要在两个输入中返回其一，通常需显式标注输出和输入的生命周期关系；不能让签名凭空承诺结果活得比所借数据更久。[Rust Book：生命周期](https://doc.rust-lang.org/book/ch10-03-lifetime-syntax.html)。
- 调用者需要独立保存一个借来的结果时，可在边界处用 `.to_owned()` 转成 `String`；若接口经常在借用与新建之间切换，可考虑 `Cow<'a, str>`。[标准库 `Cow`](https://doc.rust-lang.org/std/borrow/enum.Cow.html)。
- 函数**参数**只读时通常优先 `&str`；函数**返回值**需要按所有权来源判断，两者不必对称。`raw/Rust String 与 &str 详解：字符串所有权、借用与转换.md` 的“为什么函数参数优先使用 &str？”讨论的是参数。

### `&'static str` 是否一定来自 binary？

字符串**字面量**如 `"ok"` 在编译时已知，官方资料说明其文本存于程序 binary；函数调用时返回的是指向该文本的 `&str` 视图。`include_str!` 也在编译时把文件内容纳入程序。[Rust Reference](https://doc.rust-lang.org/reference/expressions/literal-expr.html)、[标准库 `include_str!`](https://doc.rust-lang.org/std/macro.include_str.html)。

但 `&'static` 说的是**被引用数据的有效期**，不要求文本本身编译时已知。例如下面的字符串来自运行时输入：

```rust
fn keep_forever(input: &str) -> &'static str {
    Box::leak(input.to_owned().into_boxed_str())
}
```

`Box::leak` 让这份堆分配在程序剩余时间内保持有效，所以能返回 `&'static str`；代价是内存不会按正常作用域释放。它是说明生命周期含义的反例，普通业务函数通常应返回 `String`，而非故意泄漏内存。该示例已用本机 `rustc --edition=2021` 编译运行。[标准库 `Box::leak`](https://doc.rust-lang.org/std/boxed/struct.Box.html)。

函数本身像普通 Rust 函数一样参与编译与链接；是否保留为 binary 中独立的函数体由优化和链接决定，**不是** `&'static str` 返回类型的要求。

## 依据

- `raw/rust-string-return-ownership-official-research-2026-11-05.md`：“查阅资料”与“核对结果”。
- `raw/rust-static-str-binary-lifetime-official-research-2026-11-05.md`：“核对结果”与“验证”。
- `raw/Rust String 与 &str 详解：字符串所有权、借用与转换.md`：“什么是 &str？”至“String 与 &str 的核心区别”、“借用 String”至“&str 转换为 String”。
- `raw/Rust 所有权 Ownership 详解：理解内存安全的核心机制.md`：“函数返回值转移所有权”、“只读参数优先借用”。

## 后续

- 若有具体函数签名和调用方式，可按返回值是否需要脱离输入独立存活来确定类型。
