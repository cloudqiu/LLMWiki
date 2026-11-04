---
title: "Rust String 与 &str 详解：字符串所有权、借用与转换"
source: "https://mp.weixin.qq.com/s?__biz=MzYzODE1NzUzMw==&mid=2247484476&idx=1&sn=077e76194dfa713814aea46146faddc8&chksm=f0e7538ec790da98134be4a345fe7764a3b564a5f219a0ed9b48a750eadcbe7f813014a90087&cur_album_id=4602071361631748097&scene=189#wechat_redirect"
author:
published:
created: 2026-11-04
description: "《Rust 编程实战》系列第 18 篇字符串是编程中最常用的数据类型之一。在 Rust 中，字符串并不是只有一种类型。"
tags:
  - "clippings"
---
程序员爱钓鱼 *Jul 23, 2026, 7:36 AM*

> 《Rust 编程实战》系列第 18 篇

字符串是编程中最常用的数据类型之一。

在 Rust 中，字符串并不是只有一种类型。初学者最常见的两个字符串类型是：

```
String
```

和：

```
&str
```

它们看起来都能保存文本，但在所有权、内存分配和使用场景上有明显区别。

简单来说：

- • `String` 通常拥有字符串数据
- • `&str` 通常只是借用一段字符串数据

本文将介绍：

- • `String` 与 `&str` 的区别
- • 字符串字面量
- • 创建和修改 `String`
- • 字符串追加与拼接
- • 所有权移动与借用
- • `String` 和 `&str` 相互转换
- • 字符串比较与查找
- • UTF-8 与中文字符
- • 字符串遍历
- • 常见错误与实战案例

---

## 什么是 &str？

`&str` 称为字符串切片。

最常见的字符串字面量类型就是：

```
&str
```

例如：

```
fn main() {
    let language = "Rust";

    println!("{}", language);
}
```

这里的：

```
"Rust"
```

是字符串字面量，变量 `language` 的类型通常是：

```
&str
```

可以显式写出类型：

```
fn main() {
    let language: &str = "Rust";

    println!("{}", language);
}
```

字符串字面量通常被编译进程序的二进制文件中，在程序运行期间保持有效。

---

## 什么是 String？

`String` 是一个可增长、可修改、拥有所有权的 UTF-8 字符串类型。

创建 `String` ：

```
fn main() {
    let language = String::from("Rust");

    println!("{}", language);
}
```

也可以使用：

```
to_string()
```
```
fn main() {
    let language = "Rust".to_string();

    println!("{}", language);
}
```

这两种方式都会创建一个拥有字符串数据的 `String` 。

---

## String 与 &str 的核心区别

示例：

```
let first: &str = "Rust";
let second: String = String::from("Rust");
```

主要区别如下：

| 特性 | `String` | `&str` |
| --- | --- | --- |
| 是否拥有数据 | 通常拥有 | 通常借用 |
| 是否可增长 | 可以 | 不可以 |
| 是否可修改 | 可以声明为可变 | 不能改变长度 |
| 常见来源 | 动态创建、读取文件、用户输入 | 字符串字面量、 `String` 切片 |
| 常见函数参数 | 需要接管所有权时 | 只读取文本时 |

可以暂时记住：

> 需要创建、修改和长期保存字符串时，使用 `String` 。

> 只需要读取一段文本时，优先使用 `&str` 。

---

## 创建 String

## 使用 String::from()

```
fn main() {
    let message = String::from("Hello Rust");

    println!("{}", message);
}
```

## 使用 to\_string()

```
fn main() {
    let message = "Hello Rust".to_string();

    println!("{}", message);
}
```

## 使用 String::new()

创建空字符串：

```
fn main() {
    let message = String::new();

    println!("长度：{}", message.len());
}
```

输出：

```
长度：0
```

---

## 修改 String

`String` 默认不可变。

错误示例：

```
fn main() {
    let message = String::from("Hello");

    message.push('!');
}
```

如果需要修改，必须添加 `mut` ：

```
fn main() {
    let mut message = String::from("Hello");

    message.push('!');

    println!("{}", message);
}
```

输出：

```
Hello!
```

---

## 使用 push() 添加字符

`push()` 用于追加一个字符：

```
fn main() {
    let mut text = String::from("Rust");

    text.push('!');
    text.push('好');

    println!("{}", text);
}
```

输出：

```
Rust!好
```

`push()` 的参数类型是：

```
char
```

因此需要使用单引号。

正确：

```
text.push('A');
```

错误：

```
text.push("A");
```

---

## 使用 push\_str() 添加字符串

`push_str()` 用于追加字符串切片：

```
fn main() {
    let mut text = String::from("Hello");

    text.push_str(" Rust");

    println!("{}", text);
}
```

输出：

```
Hello Rust
```

`push_str()` 接收：

```
&str
```

它不会取得参数字符串的所有权。

```
fn main() {
    let mut first = String::from("Hello");
    let second = String::from(" Rust");

    first.push_str(&second);

    println!("{}", first);
    println!("{}", second);
}
```

`second` 在调用后仍然可以继续使用。

---

## 字符串拼接

## 使用 + 运算符

```
fn main() {
    let first = String::from("Hello");
    let second = String::from(" Rust");

    let result = first + &second;

    println!("{}", result);
}
```

输出：

```
Hello Rust
```

需要注意：

```
first + &second
```

会取得 `first` 的所有权。

拼接后不能再使用：

```
first
```

但是 `second` 只是被借用，因此仍然可以使用。

---

## 使用 format! 拼接

多个字符串拼接时，更推荐：

```
format!()
```

示例：

```
fn main() {
    let language = "Rust";
    let version = 2024;

    let message = format!(
        "{} Edition {}",
        language,
        version
    );

    println!("{}", message);
}
```

输出：

```
Rust Edition 2024
```

`format!()` 会返回新的 `String` ，通常不会取得参数的所有权。

```
fn main() {
    let first = String::from("Hello");
    let second = String::from("Rust");

    let result = format!("{} {}", first, second);

    println!("{}", result);
    println!("{}", first);
    println!("{}", second);
}
```

三个变量都可以继续使用。

---

## String 的所有权移动

`String` 没有实现 `Copy` 。

例如：

```
fn main() {
    let first = String::from("Rust");
    let second = first;

    println!("{}", second);
}
```

赋值后，字符串所有权从 `first` 移动到 `second` 。

此时不能继续使用：

```
println!("{}", first);
```

否则会出现所有权错误。

---

## 使用 clone() 复制 String

如果确实需要两份独立数据，可以使用：

```
clone()
```
```
fn main() {
    let first = String::from("Rust");
    let second = first.clone();

    println!("{}", first);
    println!("{}", second);
}
```

`clone()` 会复制堆上的字符串内容，因此存在额外开销。

不要为了绕过所有权问题而到处使用 `clone()` ，能够借用时通常优先借用。

---

## 借用 String

函数只需要读取字符串时，可以接收：

```
&str
```

例如：

```
fn print_message(message: &str) {
    println!("{}", message);
}

fn main() {
    let text = String::from("Hello Rust");

    print_message(&text);

    println!("{}", text);
}
```

这里：

```
&text
```

会自动转换为 `&str` 。

函数没有取得 `text` 的所有权，所以调用后仍然可以使用原字符串。

---

## 为什么函数参数优先使用 &str？

下面的函数接收 `String` ：

```
fn print_message(message: String) {
    println!("{}", message);
}
```

调用时：

```
let text = String::from("Hello");

print_message(text);
```

所有权会移动进函数，之后不能继续使用 `text` 。

如果函数只需要读取内容，更推荐：

```
fn print_message(message: &str) {
    println!("{}", message);
}
```

这样既可以传入 `String` ：

```
print_message(&text);
```

也可以传入字符串字面量：

```
print_message("Hello");
```

因此 `&str` 参数更加通用。

---

## String 转换为 &str

最常见的方法是借用：

```
fn main() {
    let text = String::from("Hello Rust");

    let slice: &str = &text;

    println!("{}", slice);
}
```

也可以显式调用：

```
as_str()
```
```
fn main() {
    let text = String::from("Hello Rust");

    let slice = text.as_str();

    println!("{}", slice);
}
```

还可以获取部分字符串切片：

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

---

## &str 转换为 String

可以使用：

```
String::from()
```
```
fn main() {
    let text: &str = "Rust";

    let owned = String::from(text);

    println!("{}", owned);
}
```

也可以使用：

```
to_string()
```
```
let owned = text.to_string();
```

或者：

```
to_owned()
```
```
let owned = text.to_owned();
```

三种方式都可以从 `&str` 创建拥有数据的 `String` 。

---

## 获取字符串长度

```
fn main() {
    let text = String::from("Rust");

    println!("{}", text.len());
}
```

输出：

```
4
```

但是需要注意：

> `len()` 返回的是 UTF-8 字节长度，不是字符数量。

例如：

```
fn main() {
    let text = String::from("你好");

    println!("{}", text.len());
}
```

输出通常是：

```
6
```

因为一个中文字符通常占 3 个 UTF-8 字节。

---

## 统计字符数量

如果需要计算字符数量，可以使用：

```
chars().count()
```
```
fn main() {
    let text = "你好Rust";

    let count = text.chars().count();

    println!("字符数量：{}", count);
}
```

输出：

```
字符数量：6
```

这里包含：

```
你、好、R、u、s、t
```

---

## Rust 字符串不能直接使用数字索引

错误示例：

```
fn main() {
    let text = String::from("Rust");

    println!("{}", text[0]);
}
```

Rust 不允许直接通过索引访问字符串字符。

原因是字符串使用 UTF-8 编码，不同字符占用的字节数可能不同。

例如：

```
R 占 1 个字节
你 通常占 3 个字节
```

因此 `text[0]` 的含义并不明确：是第一个字节，还是第一个字符？

---

## 遍历字符串字符

可以使用：

```
chars()
```
```
fn main() {
    let text = "你好Rust";

    for character in text.chars() {
        println!("{}", character);
    }
}
```

输出：

```
你
好
R
u
s
t
```

---

## 遍历字符串字节

如果需要处理原始字节，可以使用：

```
bytes()
```
```
fn main() {
    let text = "Rust";

    for byte in text.bytes() {
        println!("{}", byte);
    }
}
```

输出的是每个字符对应的 UTF-8 字节值。

普通文本处理中通常使用 `chars()` ，网络协议、编码或二进制处理中可能使用 `bytes()` 。

---

## 字符串切片与 UTF-8 边界

下面的英文字符串切片是安全的：

```
fn main() {
    let text = String::from("Hello Rust");

    let hello = &text[0..5];

    println!("{}", hello);
}
```

但是中文字符串需要特别小心：

```
fn main() {
    let text = String::from("你好");

    let value = &text[0..1];

    println!("{}", value);
}
```

这段代码会发生 panic，因为索引 `1` 位于中文字符的 UTF-8 编码中间。

下面的范围通常是有效的：

```
let value = &text[0..3];
```

但实际开发中不要靠猜测字节数处理 Unicode 文本。

更安全的方式是使用：

```
chars()
```

---

## 字符串常用方法

## 判断是否为空

```
fn main() {
    let text = String::new();

    println!("{}", text.is_empty());
}
```

## 判断是否包含内容

```
fn main() {
    let text = "学习 Rust 编程";

    println!("{}", text.contains("Rust"));
}
```

## 判断开头和结尾

```
fn main() {
    let filename = "main.rs";

    println!("{}", filename.starts_with("main"));
    println!("{}", filename.ends_with(".rs"));
}
```

## 去除首尾空白

```
fn main() {
    let text = "  Hello Rust  ";

    println!("原内容：|{}|", text);
    println!("处理后：|{}|", text.trim());
}
```

## 替换内容

```
fn main() {
    let text = "Hello Java";

    let result = text.replace("Java", "Rust");

    println!("{}", result);
}
```

输出：

```
Hello Rust
```

---

## 字符串分割

可以使用：

```
split()
```

例如：

```
fn main() {
    let text = "apple,banana,orange";

    for fruit in text.split(',') {
        println!("{}", fruit);
    }
}
```

输出：

```
apple
banana
orange
```

`split()` 返回的每一部分通常是：

```
&str
```

它们借用了原始字符串数据。

---

## 将字符串解析为数字

可以使用：

```
parse()
```
```
fn main() {
    let text = "123";

    match text.parse::<i32>() {
        Ok(number) => {
            println!("数字：{}", number);
        }
        Err(error) => {
            println!("解析失败：{}", error);
        }
    }
}
```

解析结果类型是：

```
Result<T, E>
```

因此必须处理成功和失败两种情况。

---

## 实战：清理用户输入

下面实现一个简单用户名清理函数：

```
fn clean_username(input: &str) -> String {
    input
        .trim()
        .to_lowercase()
        .replace(' ', "_")
}

fn main() {
    let input = "  Rust User  ";

    let username = clean_username(input);

    println!("{}", username);
}
```

输出：

```
rust_user
```

这个函数：

1. 1\. 使用 `trim()` 去除首尾空格
2. 2\. 使用 `to_lowercase()` 转为小写
3. 3\. 使用 `replace()` 替换中间空格
4. 4\. 返回新的 `String`

---

## 实战：解析商品数据

假设商品数据格式为：

```
商品名称,价格,库存
```

实现解析函数：

```
fn parse_product(
    input: &str,
) -> Result<(String, f64, u32), String> {
    let parts: Vec<&str> =
        input.split(',').collect();

    if parts.len() != 3 {
        return Err(
            String::from("商品数据格式错误"),
        );
    }

    let name = parts[0].trim().to_string();

    let price = parts[1]
        .trim()
        .parse::<f64>()
        .map_err(|_| {
            String::from("商品价格无效")
        })?;

    let stock = parts[2]
        .trim()
        .parse::<u32>()
        .map_err(|_| {
            String::from("库存数量无效")
        })?;

    Ok((name, price, stock))
}

fn main() {
    let data = "机械键盘,299.0,20";

    match parse_product(data) {
        Ok((name, price, stock)) => {
            println!("商品：{}", name);
            println!("价格：{:.2}", price);
            println!("库存：{}", stock);
        }
        Err(error) => {
            println!("解析失败：{}", error);
        }
    }
}
```

输出：

```
商品：机械键盘
价格：299.00
库存：20
```

---

## 常见错误

## push() 和 push\_str() 混淆

错误：

```
text.push("Rust");
```

`push()` 只能接收一个 `char` 。

正确：

```
text.push('R');
```

追加字符串应该使用：

```
text.push_str("Rust");
```

---

## 使用 + 后继续访问左侧 String

错误：

```
let first = String::from("Hello");
let second = String::from("Rust");

let result = first + &second;

println!("{}", first);
```

`first` 的所有权已经移动。

多个字符串拼接时，可以优先使用：

```
format!()
```

---

## 函数只读字符串却接收 String

不推荐：

```
fn print_text(text: String) {
    println!("{}", text);
}
```

如果函数不需要取得所有权，更推荐：

```
fn print_text(text: &str) {
    println!("{}", text);
}
```

---

## 直接索引字符串

错误：

```
let text = String::from("Rust");

println!("{}", text[0]);
```

需要遍历字符时，应使用：

```
text.chars()
```

---

## 错误切割中文字符串

错误：

```
let text = "你好";

let value = &text[0..1];
```

切片边界必须位于合法 UTF-8 字符边界。

---

## 最佳实践

## 只读参数优先使用 &str

推荐：

```
fn validate_name(name: &str) -> bool {
    !name.trim().is_empty()
}
```

这样既能接收字符串字面量，也能接收 `String` 引用。

---

## 需要保存和修改时使用 String

```
let mut message = String::new();

message.push_str("Hello");
message.push('!');
```

需要拥有数据、动态增长或返回新字符串时，应使用 `String` 。

---

## 多个字符串拼接优先使用 format!

```
let message = format!(
    "用户 {} 的积分是 {}",
    username,
    score
);
```

相比连续使用 `+` ， `format!()` 通常更清晰。

---

## Unicode 文本使用 chars()

需要按字符处理中文、日文或表情符号时，应使用：

```
chars()
```

不要直接按照猜测的字节位置切片。

---

## 本章小结

`String` 和 `&str` 都可以表示 UTF-8 文本，但用途不同。

通过本文，我们学习了：

- • 字符串字面量的类型通常是 `&str`
- • `String` 拥有并管理字符串数据
- • `String::from()` 和 `to_string()`
- • `push()` 与 `push_str()`
- • `+` 和 `format!()` 字符串拼接
- • `String` 的所有权移动
- • 使用引用避免移动
- • `String` 与 `&str` 相互转换
- • `len()` 返回字节长度
- • 使用 `chars()` 遍历字符
- • UTF-8 字符串不能直接数字索引
- • 字符串查找、替换、分割与解析
- • 函数参数优先使用 `&str`

可以记住：

> `String` 适合拥有、保存和修改文本。

> `&str` 适合借用和读取文本。

在实际 Rust 项目中，一个常见原则是：

```
函数内部需要创建结果时使用 String，
函数参数只需要读取时使用 &str。
```

---

## 下一篇预告

下一篇我们将学习 **Rust Vec 动态数组详解** ，包括：

- • 什么是 `Vec<T>`
- • 创建动态数组
- • `vec![]` 宏
- • `push()` 与 `pop()`
- • 元素访问与安全访问
- • 修改和删除元素
- • 遍历 `Vec`
- • `len()` 与 `capacity()`
- • 动态扩容
- • `Vec` 与数组、切片的区别
- • `Vec<String>` 所有权问题
- • 排序、查找和去重
- • 实战：商品列表与任务队列

![](https://wst.wxapp.tc.qq.com/161/20304/snscosdownload/SH/reserved/68abe2010005665d0aeda70c85f71715000000a100004f50?imageView2/1/w/800/h/800/q/50)

Go语言\*课 go编程语言 Go语言开发 高并发设计 编程范式 工程实践

先用后付

假一赔三

7天无理由

¥79.8

![](https://res.wx.qq.com/shop/public/2024-10-17/fae7be51-beb6-4e61-aad8-4c1f7ccfab83.png)

人民邮电出版社书店

![](https://mmec.wxqcloud.qq.com.cn/shop/public/2026-07-13/1ade7f7a-528a-437d-a83b-b640764d8f70.png) ![](https://res.wx.qq.com/t/components/icons/base/arrow_down_regular.svg) 收起

使用手机微信

扫码了解商品信息

Rust 编程实战 · Table of Contents