---
title: "Rust 元组 Tuple 详解：组合不同类型的数据"
source: "https://mp.weixin.qq.com/s?__biz=MzYzODE1NzUzMw==&mid=2247484463&idx=1&sn=cce568238bbbd8d525f6ae948bf88b8c&chksm=f0e7539dc790da8bf6bd0eb0bac8393fad65f57cdb3d4f5f78cd1527aa0e4752cd5db992d10f&cur_album_id=4602071361631748097&scene=189#wechat_redirect"
author:
published:
created: 2026-11-04
description: "《Rust 编程实战》系列第 16 篇在上一篇文章中，我们学习了 Rust 数组 Array。"
tags:
  - "clippings"
---
程序员爱钓鱼 *Jul 21, 2026, 9:04 AM*

> 《Rust 编程实战》系列第 16 篇

在上一篇文章中，我们学习了 Rust 数组 `Array` 。

数组可以在一个变量中保存多个数据，但数组有一个重要限制：

> 数组中的所有元素必须是相同类型。

例如：

```
let scores = [80, 90, 100];
```

这里的元素都是整数。

但在实际开发中，我们经常需要把不同类型的数据组合在一起。例如一个用户可能包含：

- • 用户编号：整数
- • 用户名：字符串
- • 是否启用：布尔值
- • 账户余额：浮点数

这些数据不能直接放进同一个数组。Rust 为这种场景提供了元组：

```
Tuple
```

元组可以把多个不同类型的值组合成一个整体。

本文将介绍：

- • 元组的定义
- • 元组类型
- • 元素访问
- • 元组修改
- • 元组解构
- • 元组作为函数参数和返回值
- • 嵌套元组
- • 元组模式匹配
- • 单元素元组
- • 单元类型 `()`
- • 元组与数组的区别
- • 常见错误与实战案例

---

## 什么是元组？

元组是一种复合数据类型，可以把多个值组合成一个值。

元组中的每个元素可以拥有不同类型。

```
fn main() {
    let user = (1, "Tom", true, 99.5);

    println!("{:?}", user);
}
```

输出：

```
(1, "Tom", true, 99.5)
```

这个元组包含四个元素：

```
1
"Tom"
true
99.5
```

它们的类型分别可能是：

```
i32
&str
bool
f64
```

---

## 元组的基本语法

元组使用圆括号定义：

```
let 元组名 = (元素1, 元素2, 元素3);
```

例如：

```
fn main() {
    let product = (
        1001,
        "机械键盘",
        299.0,
        true,
    );

    println!("{:?}", product);
}
```

输出：

```
(1001, "机械键盘", 299.0, true)
```

打印整个元组时，可以使用调试格式：

```
{:?}
```

---

## 元组可以保存不同类型

```
fn main() {
    let data = (
        100,
        3.14,
        true,
        'R',
        "Rust",
    );

    println!("{:?}", data);
}
```

这个元组同时保存了：

- • 整数
- • 浮点数
- • 布尔值
- • 字符
- • 字符串切片

这正是元组与数组最大的区别。

数组要求元素类型相同，而元组允许每个位置拥有不同类型。

---

## 显式声明元组类型

可以明确写出每个元素的类型：

```
fn main() {
    let user: (u64, &str, bool, f64) =
        (1, "Alice", true, 1000.5);

    println!("{:?}", user);
}
```

元组类型写作：

```
(u64, &str, bool, f64)
```

类型的数量和顺序必须与值完全一致。

下面的写法会报错：

```
let user: (u64, bool, &str) =
    (1, "Alice", true);
```

因为第二个位置声明为 `bool` ，实际却传入了字符串。

---

## 元组长度和类型固定

元组创建后，元素数量不能增加或减少。

```
let user = (1, "Tom", true);
```

这个元组始终拥有三个元素。

元组没有下面这些方法：

```
push()
pop()
remove()
```

每个位置的类型也已经确定。

例如：

```
let mut user = (1, "Tom", true);

user.0 = 100;
```

这是允许的，因为 `user.0` 原本就是整数。

但是下面的写法不允许：

```
user.0 = "one";
```

因为不能把整数位置修改成字符串。

---

## 访问元组元素

元组通过点号和数字索引访问元素：

```
元组变量.索引
```

示例：

```
fn main() {
    let user = (1, "Tom", true, 99.5);

    println!("用户编号：{}", user.0);
    println!("用户名：{}", user.1);
    println!("是否启用：{}", user.2);
    println!("账户余额：{}", user.3);
}
```

输出：

```
用户编号：1
用户名：Tom
是否启用：true
账户余额：99.5
```

元组索引从 `0` 开始。

假设：

```
let data = (10, "Rust", true);
```

对应关系如下：

| 索引 | 元素 |
| --- | --- |
| `.0` | `10` |
| `.1` | `"Rust"` |
| `.2` | `true` |

注意数组和元组的访问方式不同：

```
array[0]
tuple.0
```

---

## 为什么元组不能动态索引？

数组可以这样访问：

```
let index = 1;
println!("{}", numbers[index]);
```

但元组不能写成：

```
let index = 1;
println!("{}", user[index]);
```

原因是元组的每个位置可能拥有不同类型。

例如：

```
let user = (1, "Tom", true);
```

其中：

```
user.0 是整数
user.1 是字符串
user.2 是布尔值
```

编译器必须在编译阶段明确知道访问哪个位置，才能确定结果类型。

---

## 修改元组元素

元组默认不可变。

错误示例：

```
fn main() {
    let user = (1, "Tom", true);

    user.2 = false;
}
```

如果需要修改，必须使用 `mut` ：

```
fn main() {
    let mut user = (1, "Tom", true);

    user.2 = false;

    println!("{:?}", user);
}
```

输出：

```
(1, "Tom", false)
```

再看一个商品示例：

```
fn main() {
    let mut product = (
        1001,
        "机械键盘",
        299.0,
        10,
    );

    product.2 = 259.0;
    product.3 = 20;

    println!("{:?}", product);
}
```

输出：

```
(1001, "机械键盘", 259.0, 20)
```

---

## 元组解构

除了使用 `.0` 、`.1` 访问元素，还可以把元组拆分成多个变量。

这种操作称为：

```
解构
```

示例：

```
fn main() {
    let user = (1, "Tom", true);

    let (id, name, enabled) = user;

    println!("用户编号：{}", id);
    println!("用户名：{}", name);
    println!("是否启用：{}", enabled);
}
```

输出：

```
用户编号：1
用户名：Tom
是否启用：true
```

这里：

```
let (id, name, enabled) = user;
```

把元组中的三个元素分别绑定给三个变量。

---

## 解构数量必须一致

错误示例：

```
fn main() {
    let user = (1, "Tom", true);

    let (id, name) = user;
}
```

元组有三个元素，但左侧只有两个变量，因此无法完成匹配。

正确写法：

```
let (id, name, enabled) = user;
```

如果不需要某个值，可以使用 `_` 忽略。

---

## 使用 \_ 忽略元素

```
fn main() {
    let user = (1, "Tom", true);

    let (_, name, _) = user;

    println!("用户名：{}", name);
}
```

输出：

```
用户名：Tom
```

这里忽略了用户编号和启用状态。

也可以使用以下划线开头的变量：

```
let (_id, name, _enabled) = user;
```

区别在于：

- • `_` 完全忽略值
- • `_id` 仍然会绑定值，只是不提示未使用警告

确定不需要某个值时，优先使用 `_` 。

---

## 使用.. 忽略多个元素

可以使用 `..`忽略多个连续元素：

```
fn main() {
    let data = (10, 20, 30, 40, 50);

    let (first, .., last) = data;

    println!("第一个元素：{}", first);
    println!("最后一个元素：{}", last);
}
```

输出：

```
第一个元素：10
最后一个元素：50
```

---

## 可变解构

可以让解构得到的变量可变：

```
fn main() {
    let point = (10, 20);

    let (mut x, mut y) = point;

    x += 5;
    y += 10;

    println!("x = {}, y = {}", x, y);
}
```

输出：

```
x = 15, y = 30
```

这里修改的是新变量 `x` 和 `y` ，并不是原来的 `point` 。

---

## 嵌套元组

元组内部还可以包含另一个元组：

```
fn main() {
    let user = (
        1,
        "Tom",
        ("Tokyo", "Japan"),
    );

    println!("{:?}", user);
}
```

它的类型可以表示为：

```
(i32, &str, (&str, &str))
```

访问嵌套元组：

```
fn main() {
    let user = (
        1,
        "Tom",
        ("Tokyo", "Japan"),
    );

    println!("编号：{}", user.0);
    println!("姓名：{}", user.1);
    println!("城市：{}", user.2.0);
    println!("国家：{}", user.2.1);
}
```

输出：

```
编号：1
姓名：Tom
城市：Tokyo
国家：Japan
```

也可以直接解构：

```
fn main() {
    let user = (
        1,
        "Tom",
        ("Tokyo", "Japan"),
    );

    let (
        id,
        name,
        (city, country),
    ) = user;

    println!("{} {} {} {}", id, name, city, country);
}
```

---

## 元组作为函数参数

可以把整个元组传给函数：

```
fn print_user(user: (u64, &str, bool)) {
    println!("编号：{}", user.0);
    println!("姓名：{}", user.1);
    println!("启用：{}", user.2);
}

fn main() {
    let user = (1, "Alice", true);

    print_user(user);
}
```

还可以在函数内部解构：

```
fn print_user(user: (u64, &str, bool)) {
    let (id, name, enabled) = user;

    println!("编号：{}", id);
    println!("姓名：{}", name);
    println!("启用：{}", enabled);
}
```

相比频繁使用 `.0` 和 `.1` ，解构后的变量名通常更容易理解。

---

## 元组作为函数返回值

Rust 函数只能直接返回一个值，但这个值可以是元组。

因此可以使用元组返回多个结果。

例如，同时返回两个数字的和与积：

```
fn calculate(
    first: i32,
    second: i32,
) -> (i32, i32) {
    let sum = first + second;
    let product = first * second;

    (sum, product)
}

fn main() {
    let result = calculate(10, 5);

    println!("和：{}", result.0);
    println!("积：{}", result.1);
}
```

输出：

```
和：15
积：50
```

更推荐直接解构返回值：

```
fn main() {
    let (sum, product) = calculate(10, 5);

    println!("和：{}", sum);
    println!("积：{}", product);
}
```

变量名比 `.0` 、`.1` 更清晰。

---

## 返回最大值和最小值

```
fn find_min_max(
    numbers: &[i32],
) -> Option<(i32, i32)> {
    if numbers.is_empty() {
        return None;
    }

    let mut min = numbers[0];
    let mut max = numbers[0];

    for &number in numbers {
        if number < min {
            min = number;
        }

        if number > max {
            max = number;
        }
    }

    Some((min, max))
}

fn main() {
    let numbers = [12, 5, 88, 32, 1];

    match find_min_max(&numbers) {
        Some((min, max)) => {
            println!("最小值：{}", min);
            println!("最大值：{}", max);
        }
        None => {
            println!("没有数据");
        }
    }
}
```

输出：

```
最小值：1
最大值：88
```

返回类型：

```
Option<(i32, i32)>
```

表示：

- • 有数据时返回包含最小值和最大值的元组
- • 没有数据时返回 `None`

---

## 元组与 match 模式匹配

元组非常适合配合 `match` 使用。

例如根据坐标判断位置：

```
fn main() {
    let point = (0, 10);

    match point {
        (0, 0) => {
            println!("位于原点");
        }
        (0, y) => {
            println!("位于 Y 轴，y = {}", y);
        }
        (x, 0) => {
            println!("位于 X 轴，x = {}", x);
        }
        (x, y) => {
            println!("普通坐标：({}, {})", x, y);
        }
    }
}
```

输出：

```
位于 Y 轴，y = 10
```

元组模式可以同时判断多个状态：

```
fn main() {
    let status = (true, false);

    match status {
        (false, _) => {
            println!("用户尚未登录");
        }
        (true, true) => {
            println!("进入管理员后台");
        }
        (true, false) => {
            println!("进入普通用户中心");
        }
    }
}
```

输出：

```
进入普通用户中心
```

---

## 使用 if let 匹配元组

只关心一种模式时，可以使用 `if let` ：

```
fn main() {
    let point = (0, 20);

    if let (0, y) = point {
        println!("位于 Y 轴，y = {}", y);
    }
}
```

输出：

```
位于 Y 轴，y = 20
```

---

## 元组与 Option 组合

元组经常放在 `Option` 中，用来返回多个可选值。

```
fn find_user(
    id: u64,
) -> Option<(u64, &'static str)> {
    match id {
        1 => Some((1, "Tom")),
        2 => Some((2, "Alice")),
        _ => None,
    }
}

fn main() {
    if let Some((id, name)) = find_user(2) {
        println!("用户编号：{}", id);
        println!("用户名：{}", name);
    } else {
        println!("用户不存在");
    }
}
```

输出：

```
用户编号：2
用户名：Alice
```

---

## 单元素元组

把一个值放进圆括号，并不会自动变成元组。

```
let value = (10);
```

这里的 `value` 仍然是普通整数。

单元素元组必须添加逗号：

```
let value = (10,);
```

其类型是：

```
(i32,)
```

示例：

```
fn main() {
    let normal = (10);
    let tuple = (10,);

    println!("普通值：{:?}", normal);
    println!("单元素元组：{:?}", tuple);
}
```

输出：

```
普通值：10
单元素元组：(10,)
```

---

## 空元组与单元类型

不包含任何元素的元组写作：

```
()
```

它被称为单元类型：

```
Unit Type
```

`()` 既是一个类型，也是该类型唯一的值。

例如：

```
fn print_message() -> () {
    println!("Hello Rust");
}
```

返回类型可以省略：

```
fn print_message() {
    println!("Hello Rust");
}
```

两种写法作用相同。

许多只执行操作、不返回业务数据的代码，结果都是 `()` 。

例如：

```
fn main() {
    let result = println!("Hello");

    println!("{:?}", result);
}
```

输出：

```
Hello
()
```

---

## 元组的所有权

元组是否实现 `Copy` ，取决于其中所有元素是否实现 `Copy` 。

例如整数元组：

```
fn main() {
    let first = (10, 20);
    let second = first;

    println!("{:?}", first);
    println!("{:?}", second);
}
```

整数实现了 `Copy` ，因此 `first` 仍然可以使用。

如果元组包含 `String` ：

```
fn main() {
    let first = (
        1,
        String::from("Tom"),
    );

    let second = first;

    println!("{:?}", second);
}
```

赋值后， `String` 的所有权会移动到 `second` ，不能再使用完整的 `first` 。

如果不希望移动，可以传递引用：

```
fn print_user(user: &(u64, String)) {
    println!("编号：{}", user.0);
    println!("姓名：{}", user.1);
}

fn main() {
    let user = (
        1,
        String::from("Alice"),
    );

    print_user(&user);

    println!("{:?}", user);
}
```

所有权将在后续章节中详细讲解。

---

## 元组与数组的区别

数组：

```
let numbers = [10, 20, 30];
```

元组：

```
let user = (1, "Tom", true);
```

主要区别如下：

| 特性 | Tuple | Array |
| --- | --- | --- |
| 元素类型 | 可以不同 | 必须相同 |
| 元素数量 | 固定 | 固定 |
| 访问方式 | `.0`  、`.1` | `[0]`  、 `[1]` |
| 动态索引 | 不支持 | 支持 |
| `len()` | 不支持 | 支持 |
| `for`  遍历 | 不能直接遍历 | 支持 |
| 主要用途 | 组合不同数据 | 保存同类数据 |

元组不能直接使用 `for` 遍历，因为元组中的元素可能拥有不同类型。

如果需要顺序遍历一组同类型数据，应使用：

- • 数组
- • `Vec`
- • 切片

---

## 元组与结构体的选择

元组适合临时组合少量数据：

```
let point = (10, 20);
```
```
let result = (true, "操作成功");
```

但是，如果字段较多，元组可读性会迅速下降。

例如：

```
let user = (
    1,
    "Tom",
    20,
    true,
    1000.0,
    "Tokyo",
);
```

看到：

```
user.4
```

很难知道它代表什么。

这时更适合使用结构体：

```
struct User {
    id: u64,
    name: String,
    age: u8,
    enabled: bool,
    balance: f64,
    city: String,
}
```

通常可以遵循以下原则：

> 临时组合两个或三个值，可以使用元组。

> 数据需要长期维护，或者字段含义明确，应该使用结构体。

---

## 实战：商品价格计算

函数返回：

- • 商品原价
- • 优惠金额
- • 最终价格
```
fn calculate_price(
    price: f64,
    discount_rate: f64,
) -> (f64, f64, f64) {
    let discount_amount =
        price * discount_rate;

    let final_price =
        price - discount_amount;

    (
        price,
        discount_amount,
        final_price,
    )
}

fn main() {
    let (
        original_price,
        discount_amount,
        final_price,
    ) = calculate_price(200.0, 0.2);

    println!("商品原价：{:.2}", original_price);
    println!("优惠金额：{:.2}", discount_amount);
    println!("最终价格：{:.2}", final_price);
}
```

输出：

```
商品原价：200.00
优惠金额：40.00
最终价格：160.00
```

---

## 实战：订单金额分析

要求：

- • 计算商品总额
- • 计算优惠金额
- • 计算运费
- • 返回最终金额
```
fn analyze_order(
    prices: &[f64],
) -> (f64, f64, f64, f64) {
    let mut subtotal = 0.0;

    for price in prices {
        if *price > 0.0 {
            subtotal += price;
        }
    }

    let discount_rate =
        if subtotal >= 500.0 {
            0.1
        } else if subtotal >= 200.0 {
            0.05
        } else {
            0.0
        };

    let discount_amount =
        subtotal * discount_rate;

    let discounted_total =
        subtotal - discount_amount;

    let shipping =
        if discounted_total >= 99.0 {
            0.0
        } else {
            10.0
        };

    let final_total =
        discounted_total + shipping;

    (
        subtotal,
        discount_amount,
        shipping,
        final_total,
    )
}

fn main() {
    let prices = [
        199.0,
        88.0,
        59.0,
        299.0,
    ];

    let (
        subtotal,
        discount,
        shipping,
        final_total,
    ) = analyze_order(&prices);

    println!("商品总额：{:.2}", subtotal);
    println!("优惠金额：{:.2}", discount);
    println!("运费：{:.2}", shipping);
    println!("最终金额：{:.2}", final_total);
}
```

输出：

```
商品总额：645.00
优惠金额：64.50
运费：0.00
最终金额：580.50
```

这个案例综合使用了：

- • 数组切片
- • `for` 循环
- • `if` 表达式
- • 元组返回值
- • 元组解构
- • 订单业务规则

---

## 常见错误

## 使用方括号定义元组

错误：

```
let user = [1, "Tom", true];
```

方括号用于数组，元组应该使用圆括号：

```
let user = (1, "Tom", true);
```

---

## 使用数组方式访问元组

错误：

```
println!("{}", user[0]);
```

正确：

```
println!("{}", user.0);
```

---

## 解构数量不一致

错误：

```
let point = (10, 20);

let (x, y, z) = point;
```

正确：

```
let (x, y) = point;
```

---

## 忘记单元素元组的逗号

错误：

```
let value = (10);
```

正确：

```
let value = (10,);
```

---

## 修改不可变元组

错误：

```
let point = (10, 20);

point.0 = 100;
```

正确：

```
let mut point = (10, 20);

point.0 = 100;
```

---

## 过度使用元组

下面的元组字段太多：

```
let product = (
    1001,
    "电脑",
    5999.0,
    10,
    true,
    "数码产品",
);
```

访问 `product.4` 时，字段含义不清楚。

这种业务数据更适合定义结构体。

---

## 最佳实践

## 返回少量结果时使用元组

```
fn calculate() -> (i32, i32) {
    (10, 20)
}
```

返回两个或三个紧密相关的值时，元组简单实用。

---

## 尽量立即解构返回值

不推荐：

```
let result = calculate();

println!("{}", result.0);
println!("{}", result.1);
```

推荐：

```
let (sum, product) = calculate();

println!("{}", sum);
println!("{}", product);
```

---

## 多个状态组合可以使用元组匹配

```
match (logged_in, is_admin) {
    (false, _) => println!("未登录"),
    (true, true) => println!("管理员"),
    (true, false) => println!("普通用户"),
}
```

这种写法通常比嵌套多个 `if` 更清晰。

---

## 字段较多时使用结构体

如果元组包含多个具有明确含义的字段，应优先使用结构体。

结构体字段有名称，更容易阅读、维护和扩展。

---

## 本章小结

元组是 Rust 中用于组合不同类型数据的复合类型。

通过本文，我们学习了：

- • 元组使用圆括号定义
- • 元组元素可以拥有不同类型
- • 元组长度和每个位置的类型固定
- • 使用 `.0` 、`.1` 访问元素
- • 使用 `mut` 修改元组
- • 元组解构
- • 使用 `_` 和 `..`忽略数据
- • 嵌套元组
- • 元组作为函数参数
- • 元组作为函数返回值
- • 使用元组返回多个结果
- • 元组与 `match` 、 `if let`
- • 单元素元组必须添加逗号
- • 单元类型 `()`
- • 元组与所有权的关系
- • 元组、数组与结构体的区别

可以记住：

> 数组用于保存相同类型的一组数据。

> 元组用于临时组合不同类型的多个数据。

> 字段较多或业务含义明确时，应使用结构体。

---

## 下一篇预告

下一篇我们将学习 **Rust 切片 Slice 详解** ，包括：

- • 什么是切片
- • 数组切片 `&[T]`
- • 字符串切片 `&str`
- • 范围语法 `..`与 `..=`
- • 切片的开始位置和长度
- • 切片与所有权
- • 可变切片 `&mut [T]`
- • 使用 `get()` 安全获取切片
- • 切片作为函数参数
- • 数组、 `Vec` 与切片的关系
- • UTF-8 字符串切片注意事项
- • 实战：批量数据处理与字符串解析

Rust 编程实战 · Table of Contents