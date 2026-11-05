---
title: "Rust 单元测试详解：使用 cargo test 保证代码质量"
source: "https://mp.weixin.qq.com/s?__biz=MzYzODE1NzUzMw==&mid=2247484537&idx=1&sn=df146fa63662053704c32ce96368d82c&chksm=f0e753cbc790daddac51d75f93f87f10d774294e8ac656980bf0669141f9422b85c57e77a8f6&cur_album_id=4602071361631748097&scene=189#wechat_redirect"
author:
published:
created: 2026-11-05
description: "《Rust 编程实战》系列第 29 篇在上一篇文章中，我们学习了 Rust 文档生成，了解了如何使用 ///"
tags:
  - "clippings"
---
程序员爱钓鱼 *Aug 3, 2026, 7:20 AM*

> 《Rust 编程实战》系列第 29 篇  
> 在上一篇文章中，我们学习了 Rust 文档生成，了解了如何使用 `///` 、 `//!`、 `cargo doc` 和文档测试编写可维护的 API 文档。本篇继续学习 Rust 自动化测试体系中最基础、最常用的一部分：单元测试。  
> 单元测试用于验证一个函数、一个模块或一段独立逻辑是否符合预期。例如：

- • 加法函数是否返回正确结果
- • 用户名为空时是否校验失败
- • 除数为零时是否返回错误
- • 商品价格计算是否正确
- • 某种非法状态是否会触发 panic  
	Rust 内置了测试框架，不需要额外安装测试库。只要使用 `#[test]` 标记测试函数，再执行：
```
cargo test
```

即可自动编译并运行测试。

## 什么是单元测试

单元测试通常针对程序中最小的可测试单元，例如一个函数或一个模块。  
假设有一个加法函数：

```
fn add(a: i32, b: i32) -> i32 {
    a + b
}
```

我们希望确认：

```
add(2,3)
```

一定返回：

```
5
```

可以编写测试：

```
#[test]
fn test_add() {
    let result = add(2, 3);
    assert_eq!(result, 5);
}
```

执行：

```
cargo test
```

如果测试通过，会看到类似：

```
test test_add ... ok
```

如果结果不符合预期，测试会失败并显示具体位置。

## 使用 #\[test\] 定义测试

普通函数不会被测试框架自动执行。  
只有添加：

```
#[test]
```

的函数才会被识别为测试函数。

```
#[test]
fn test_example() {
    println!("运行测试");
}
```

测试函数通常：

- • 不接收参数
- • 默认返回 `()`
- • 使用断言判断结果
- • 名称以 `test_` 开头或表达具体行为  
	推荐使用具有业务含义的测试名称：
```
#[test]
fn returns_sum_when_numbers_are_valid() {
}
```

比下面这种名称更清晰：

```
#[test]
fn test1() {
}
```

## 使用测试模块

单元测试通常放在当前源文件底部，并使用测试模块组织：

```
fn add(a: i32, b: i32) -> i32 {
    a + b
}

#[cfg(test)]
mod tests {
    use super::*;

    #[test]
    fn test_add() {
        assert_eq!(add(2, 3), 5);
    }
}
```

这里：

```
#[cfg(test)]
```

表示只有执行测试时才编译该模块。  
正常执行：

```
cargo run
```

时，测试代码不会被包含。

```
use super::*;
```

表示导入父模块中的内容，因此测试模块可以调用 `add()` 。

## 使用 assert!

`assert!` 用于判断一个布尔表达式是否为 `true` 。

```
fn is_adult(age: u32) -> bool {
    age >= 18
}

#[test]
fn adult_age_should_pass() {
    assert!(is_adult(20));
}
```

如果表达式为 `false` ，测试失败。  
还可以添加自定义说明：

```
#[test]
fn child_age_should_fail() {
    let age = 16;
    assert!(
        !is_adult(age),
        "年龄 {} 不应该通过成人校验",
        age
    );
}
```

`assert!` 适合测试：

- • 布尔返回值
- • 集合是否为空
- • 字符串是否包含内容
- • 条件是否成立

## 使用 assert\_eq!

`assert_eq!` 用于判断两个值是否相等。

```
#[test]
fn test_total_price() {
    let price = 100;
    let count = 3;
    assert_eq!(price * count, 300);
}
```

测试失败时，会输出左右两边的实际值，方便定位问题。  
例如：

```
assert_eq!(2 + 2, 5);
```

会显示类似：

```
left: 4
right: 5
```

被比较的类型通常需要实现：

```
PartialEq
Debug
```

## 使用 assert\_ne!

`assert_ne!` 用于判断两个值不相等。

```
#[test]
fn generated_id_should_not_be_zero() {
    let id = 1001;
    assert_ne!(id, 0);
}
```

常见使用场景：

- • 生成的编号不能为零
- • 加密前后内容不能相同
- • 修改后的状态不能等于旧状态

## 测试多个输入

一个函数通常需要测试多个场景。

```
fn square(value: i32) -> i32 {
    value * value
}

#[cfg(test)]
mod tests {
    use super::*;

    #[test]
    fn square_positive_number() {
        assert_eq!(square(5), 25);
    }

    #[test]
    fn square_zero() {
        assert_eq!(square(0), 0);
    }

    #[test]
    fn square_negative_number() {
        assert_eq!(square(-4), 16);
    }
}
```

不要只测试正常输入，还应该测试：

- • 零
- • 负数
- • 空字符串
- • 空集合
- • 最大值和最小值
- • 边界条件
- • 非法参数

## 测试 Result

很多业务函数返回：

```
Result<T,E>
```

例如：

```
fn divide(a: i32, b: i32) -> Result<i32, String> {
    if b == 0 {
        return Err(String::from("除数不能为0"));
    }
    Ok(a / b)
}
```

测试成功情况：

```
#[test]
fn divide_should_return_result() {
    let result = divide(10, 2);
    assert_eq!(result, Ok(5));
}
```

测试失败情况：

```
#[test]
fn divide_by_zero_should_fail() {
    let result = divide(10, 0);
    assert!(result.is_err());
}
```

也可以判断具体错误：

```
#[test]
fn divide_by_zero_should_return_message() {
    let result = divide(10, 0);
    assert_eq!(
        result,
        Err(String::from("除数不能为0"))
    );
}
```

## 测试 Option

例如查找第一个偶数：

```
fn first_even(values: &[i32]) -> Option<i32> {
    for &value in values {
        if value % 2 == 0 {
            return Some(value);
        }
    }
    None
}
```

测试：

```
#[test]
fn should_find_first_even_number() {
    let values = [1, 3, 4, 6];
    assert_eq!(first_even(&values), Some(4));
}

#[test]
fn should_return_none_when_no_even_number() {
    let values = [1, 3, 5];
    assert_eq!(first_even(&values), None);
}
```

## 测试 panic

如果某段代码在特定情况下应该触发 panic，可以使用：

```
#[should_panic]
```

例如：

```
fn get_first(values: &[i32]) -> i32 {
    if values.is_empty() {
        panic!("数组不能为空");
    }
    values[0]
}
```

测试：

```
#[test]
#[should_panic]
fn empty_values_should_panic() {
    get_first(&[]);
}
```

还可以判断 panic 信息：

```
#[test]
#[should_panic(expected = "数组不能为空")]
fn empty_values_should_panic_with_message() {
    get_first(&[]);
}
```

只有 panic 信息包含指定文本时，测试才通过。  
注意：普通业务错误通常应该返回 `Result` ，不要为了方便测试而滥用 panic。

## 测试函数返回 Result

测试函数本身也可以返回 `Result` ：

```
#[test]
fn parse_number_should_work()
    -> Result<(), Box<dyn std::error::Error>>
{
    let number = "123".parse::<i32>()?;
    assert_eq!(number, 123);
    Ok(())
}
```

这样可以在测试中使用：

```
?
```

传播错误。  
如果返回 `Err` ，测试失败；返回 `Ok(())` ，测试通过。

## 测试私有函数

单元测试模块通常位于被测试代码所在模块内部，因此可以测试私有函数。

```
fn normalize_name(name: &str) -> String {
    name.trim().to_lowercase()
}

#[cfg(test)]
mod tests {
    use super::*;

    #[test]
    fn normalize_name_should_clean_input() {
        assert_eq!(
            normalize_name("  TOM  "),
            "tom"
        );
    }
}
```

不需要为了测试而把内部函数改成 `pub` 。

## 忽略耗时测试

某些测试运行时间较长，例如：

- • 大文件处理
- • 性能测试
- • 网络请求
- • 数据库测试  
	可以使用：
```
#[ignore]
```

例如：

```
#[test]
#[ignore]
fn large_data_test() {
    // 耗时测试
}
```

普通执行：

```
cargo test
```

会跳过该测试。  
运行被忽略的测试：

```
cargo test -- --ignored
```

运行全部测试，包括被忽略的：

```
cargo test -- --include-ignored
```

## 运行指定测试

运行名称中包含 `divide` 的测试：

```
cargo test divide
```

运行一个完整名称：

```
cargo test divide_by_zero_should_fail
```

显示测试中的 `println!` 输出：

```
cargo test -- --nocapture
```

默认情况下，测试通过时标准输出会被隐藏。

## 单线程运行测试

Rust 测试默认可以并行执行。  
如果多个测试共同操作同一个文件、端口或全局资源，可能相互影响。  
可以单线程执行：

```
cargo test -- --test-threads=1
```

不过更好的方式是让每个测试使用独立资源，避免测试之间互相依赖。

## 实战：用户注册校验测试

```
#[derive(Debug, PartialEq)]
enum RegisterError {
    EmptyName,
    InvalidAge,
}

fn register(
    name: &str,
    age: u32,
) -> Result<(), RegisterError> {
    if name.trim().is_empty() {
        return Err(RegisterError::EmptyName);
    }
    if age < 18 {
        return Err(RegisterError::InvalidAge);
    }
    Ok(())
}

#[cfg(test)]
mod tests {
    use super::*;

    #[test]
    fn valid_user_should_register() {
        let result = register("Tom", 20);
        assert_eq!(result, Ok(()));
    }

    #[test]
    fn empty_name_should_fail() {
        let result = register("   ", 20);
        assert_eq!(
            result,
            Err(RegisterError::EmptyName)
        );
    }

    #[test]
    fn child_should_fail() {
        let result = register("Tom", 16);
        assert_eq!(
            result,
            Err(RegisterError::InvalidAge)
        );
    }
}
```

这里通过：

```
#[derive(PartialEq)]
```

让错误枚举可以使用 `assert_eq!` 比较。

## 常见错误

## 测试中滥用 unwrap

不推荐：

```
let value = result.unwrap();
```

如果测试目标是验证成功结果，可以使用：

```
assert_eq!(result, Ok(100));
```

如果确实要取值， `expect()` 通常比 `unwrap()` 更清楚：

```
let value = result.expect("这里应该成功");
```

## 测试之间相互依赖

错误思路：

```
测试A创建数据
测试B依赖测试A的数据
```

测试执行顺序不应该被依赖。每个测试应独立准备和清理数据。

## 只测试正常情况

只测试成功场景容易遗漏：

- • 空值
- • 非法输入
- • 越界
- • 重复数据
- • 错误分支

## 为了测试暴露私有实现

不要把私有函数全部改成 `pub` 。单元测试放在模块内部即可访问私有内容。

## 单元测试最佳实践

测试名称应表达行为：

```
empty_password_should_be_rejected
```

一个测试尽量只验证一个核心行为，失败时更容易定位。  
测试结构可以使用：

```
准备数据
执行操作
验证结果
```

例如：

```
#[test]
fn discount_should_apply_to_large_order() {
    let total = 500.0;
    let result = calculate_discount(total);
    assert_eq!(result, 50.0);
}
```

不要测试标准库本身，例如没有必要测试：

```
assert_eq!(2 + 2, 4);
```

测试重点应该是自己的业务逻辑。  
修复 Bug 时，应先为该 Bug 补充测试，防止以后再次出现。

## 本章小结

Rust 内置了完整的单元测试能力，不需要额外测试框架。  
本文学习了：

- • 使用 `#[test]` 定义测试
- • 使用 `#[cfg(test)]` 创建测试模块
- • 使用 `assert!` 验证布尔条件
- • 使用 `assert_eq!` 和 `assert_ne!` 比较结果
- • 测试 `Option` 和 `Result`
- • 使用 `#[should_panic]` 测试 panic
- • 让测试函数返回 `Result`
- • 测试私有函数
- • 使用 `#[ignore]` 忽略耗时测试
- • 运行指定测试
- • 显示测试输出
- • 单线程运行测试
- • 为成功、失败和边界场景分别编写测试  
	可以记住：

> 单元测试关注一个函数或一个模块内部的独立逻辑。  
> 测试不仅要验证正常流程，也要覆盖错误流程和边界条件。  
> 测试越独立、越明确，项目重构时就越安全。

## 下一篇预告

下一篇我们将学习：

## Rust 集成测试详解：测试多个模块协作与公共 API

内容包括：

- • 单元测试与集成测试的区别
- • `tests` 目录结构
- • 每个测试文件都是独立 Crate
- • 测试 Library Crate 公共接口
- • 公共测试辅助模块
- • 多文件集成测试
- • 命令行程序测试
- • 文件、数据库与 HTTP 测试思路
- • 集成测试最佳实践

Rust 编程实战 · Table of Contents