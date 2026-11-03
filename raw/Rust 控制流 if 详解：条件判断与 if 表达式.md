---
title: "Rust 控制流 if 详解：条件判断与 if 表达式"
source: "https://mp.weixin.qq.com/s?__biz=MzYzODE1NzUzMw==&mid=2247484443&idx=1&sn=611794f33130565158a37c73024c8a19&chksm=f0e753a9c790dabf18fe78cc3b54812cfbfa10a0351b763d3191288104b9b6c8b2fefcf51282&cur_album_id=4602071361631748097&scene=189#wechat_redirect"
author:
published:
created: 2026-11-03
description: "《Rust 编程实战》系列第 11 篇在前面的文章中，我们已经学习了变量、数据类型、函数和注释。"
tags:
  - "clippings"
---
程序员爱钓鱼 *Jul 16, 2026, 8:05 AM*

> 《Rust 编程实战》系列第 11 篇

在前面的文章中，我们已经学习了变量、数据类型、函数和注释。

到目前为止，我们编写的程序大多是从上到下依次执行。

但真实程序不可能永远只执行固定逻辑。

例如：

- • 用户是否已经登录
- • 商品库存是否充足
- • 分数是否及格
- • 订单金额是否满足免邮条件
- • 年龄是否达到注册要求
- • 文件是否存在

程序需要根据不同条件，执行不同代码。

这就是控制流。

Rust 中最常用的条件控制语句是：

```
if
```

本文将详细介绍：

- • `if`
- • `else`
- • `else if`
- • 比较运算符
- • 逻辑运算符
- • 嵌套判断
- • `if` 表达式
- • 条件分支返回值
- • 常见错误
- • 实战案例

---

## 什么是控制流？

控制流可以理解为：

> 控制程序按照不同条件，选择不同的执行路径。

例如：

```
fn main() {
    let age = 20;

    if age >= 18 {
        println!("已经成年");
    }
}
```

运行结果：

```
已经成年
```

程序会先判断：

```
age >= 18
```

如果结果为：

```
true
```

就执行大括号中的代码。

如果结果为：

```
false
```

则跳过这段代码。

---

## if 的基本语法

Rust 中 `if` 的基本语法如下：

```
if 条件 {
    条件成立时执行的代码
}
```

例如：

```
fn main() {
    let score = 90;

    if score >= 60 {
        println!("考试及格");
    }
}
```

这里的条件是：

```
score >= 60
```

因为 `90 >= 60` 为真，所以输出：

```
考试及格
```

---

## 条件必须是 bool 类型

Rust 对条件表达式要求非常严格。

`if` 后面的条件必须是：

```
bool
```

也就是：

```
true
```

或者：

```
false
```

正确示例：

```
fn main() {
    let logged_in = true;

    if logged_in {
        println!("欢迎回来");
    }
}
```

错误示例：

```
fn main() {
    let number = 1;

    if number {
        println!("执行");
    }
}
```

这段代码会报错。

因为 Rust 不会像 C、JavaScript 或 Python 那样，自动把数字转换成布尔值。

正确写法应该是：

```
fn main() {
    let number = 1;

    if number != 0 {
        println!("执行");
    }
}
```

Rust 要求开发者明确表达条件，避免隐式转换造成逻辑错误。

---

## else 分支

如果希望条件不成立时执行另一段代码，可以使用：

```
else
```

例如：

```
fn main() {
    let age = 16;

    if age >= 18 {
        println!("已经成年");
    } else {
        println!("尚未成年");
    }
}
```

输出：

```
尚未成年
```

完整语法：

```
if 条件 {
    条件成立时执行
} else {
    条件不成立时执行
}
```

---

## else if 多条件判断

当程序需要判断多个条件时，可以使用：

```
else if
```

例如：

```
fn main() {
    let score = 85;

    if score >= 90 {
        println!("优秀");
    } else if score >= 80 {
        println!("良好");
    } else if score >= 60 {
        println!("及格");
    } else {
        println!("不及格");
    }
}
```

输出：

```
良好
```

程序会按照从上到下的顺序判断。

当某个条件成立后，后面的分支不会继续执行。

---

## 条件顺序很重要

来看一个错误示例：

```
fn main() {
    let score = 95;

    if score >= 60 {
        println!("及格");
    } else if score >= 90 {
        println!("优秀");
    }
}
```

输出：

```
及格
```

虽然分数是 95，但第一个条件：

```
score >= 60
```

已经成立。

因此程序不会继续判断：

```
score >= 90
```

正确写法应该从更严格的条件开始：

```
fn main() {
    let score = 95;

    if score >= 90 {
        println!("优秀");
    } else if score >= 60 {
        println!("及格");
    } else {
        println!("不及格");
    }
}
```

---

## 比较运算符

`if` 中经常使用比较运算符。

| 运算符 | 含义 |
| --- | --- |
| `==` | 等于 |
| `!=` | 不等于 |
| `>` | 大于 |
| `<` | 小于 |
| `>=` | 大于等于 |
| `<=` | 小于等于 |

例如：

```
fn main() {
    let age = 20;

    println!("{}", age == 20);
    println!("{}", age != 18);
    println!("{}", age > 18);
    println!("{}", age < 30);
}
```

输出：

```
true
true
true
true
```

---

## 逻辑运算符

复杂条件通常需要逻辑运算符。

Rust 中常用的逻辑运算符有：

| 运算符 | 含义 |
| --- | --- |
| `&&` | 并且 |
| \` |  |
| `!` | 取反 |

---

## && 并且

只有两边条件都成立，结果才是 `true` 。

例如：

```
fn main() {
    let age = 20;
    let has_id_card = true;

    if age >= 18 && has_id_card {
        println!("允许进入");
    }
}
```

这里必须同时满足：

- • 年龄达到 18 岁
- • 已携带身份证

才会执行。

---

## || 或者

只要任意一个条件成立，结果就是 `true` 。

例如：

```
fn main() {
    let is_admin = false;
    let is_manager = true;

    if is_admin || is_manager {
        println!("可以进入管理后台");
    }
}
```

虽然 `is_admin` 是 `false` ，但 `is_manager` 是 `true` ，因此条件成立。

---

## ! 取反

`!` 可以反转布尔值。

例如：

```
fn main() {
    let logged_in = false;

    if !logged_in {
        println!("请先登录");
    }
}
```

这里：

```
!false
```

等于：

```
true
```

所以会输出：

```
请先登录
```

---

## 组合多个条件

例如，判断用户是否可以领取优惠券：

```
fn main() {
    let logged_in = true;
    let total_price = 120.0;
    let already_received = false;

    if logged_in && total_price >= 100.0 && !already_received {
        println!("可以领取优惠券");
    } else {
        println!("暂不满足领取条件");
    }
}
```

---

## if 可以嵌套

一个 `if` 中还可以继续写另一个 `if` 。

例如：

```
fn main() {
    let logged_in = true;
    let is_admin = false;

    if logged_in {
        println!("用户已登录");

        if is_admin {
            println!("进入管理员后台");
        } else {
            println!("进入普通用户中心");
        }
    } else {
        println!("请先登录");
    }
}
```

这种写法称为嵌套判断。

不过，嵌套层级过多会降低代码可读性。

---

## 减少过深嵌套

不推荐：

```
fn check_user(logged_in: bool, enabled: bool, is_admin: bool) {
    if logged_in {
        if enabled {
            if is_admin {
                println!("允许访问");
            }
        }
    }
}
```

更清晰的写法：

```
fn check_user(logged_in: bool, enabled: bool, is_admin: bool) {
    if !logged_in {
        println!("用户未登录");
        return;
    }

    if !enabled {
        println!("账号已禁用");
        return;
    }

    if !is_admin {
        println!("没有管理员权限");
        return;
    }

    println!("允许访问");
}
```

这种方式称为提前返回。

它可以减少嵌套，让代码更容易阅读。

---

## if 是表达式

Rust 中非常重要的一点是：

> `if` 不仅可以控制流程，还可以返回一个值。

例如：

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

输出：

```
成年人
```

这里整个 `if` 表达式的结果被赋值给了：

```
status
```

---

## if 表达式的语法

```
let 变量 = if 条件 {
    值1
} else {
    值2
};
```

例如：

```
fn main() {
    let number = 10;

    let result = if number % 2 == 0 {
        "偶数"
    } else {
        "奇数"
    };

    println!("{}", result);
}
```

输出：

```
偶数
```

---

## 各分支返回类型必须一致

下面的代码是正确的：

```
fn main() {
    let enabled = true;

    let value = if enabled {
        100
    } else {
        0
    };

    println!("{}", value);
}
```

因为两个分支都返回整数。

下面的代码会报错：

```
fn main() {
    let enabled = true;

    let value = if enabled {
        100
    } else {
        "关闭"
    };

    println!("{}", value);
}
```

因为：

- • 一个分支返回 `i32`
- • 一个分支返回 `&str`

Rust 无法确定 `value` 的统一类型。

---

## if 表达式末尾不要加分号

正确：

```
let result = if true {
    10
} else {
    20
};
```

错误：

```
let result = if true {
    10;
} else {
    20;
};
```

加上分号后，分支返回的是：

```
()
```

也就是单元类型，而不是整数。

---

## if 与函数返回值

`if` 表达式非常适合直接作为函数返回值。

例如：

```
fn get_user_level(score: u32) -> &'static str {
    if score >= 1000 {
        "黄金会员"
    } else if score >= 500 {
        "白银会员"
    } else {
        "普通会员"
    }
}
```

调用：

```
fn main() {
    let level = get_user_level(800);

    println!("{}", level);
}
```

输出：

```
白银会员
```

---

## 实战：判断用户年龄

```
fn get_age_status(age: u8) -> &'static str {
    if age < 12 {
        "儿童"
    } else if age < 18 {
        "青少年"
    } else if age < 60 {
        "成年人"
    } else {
        "老年人"
    }
}

fn main() {
    let age = 35;

    println!("年龄阶段：{}", get_age_status(age));
}
```

输出：

```
年龄阶段：成年人
```

---

## 实战：订单免邮判断

```
fn calculate_shipping(total: f64) -> f64 {
    if total >= 99.0 {
        0.0
    } else {
        10.0
    }
}

fn main() {
    let total = 88.0;
    let shipping = calculate_shipping(total);

    println!("商品金额：{:.2}", total);
    println!("运费：{:.2}", shipping);
}
```

输出：

```
商品金额：88.00
运费：10.00
```

---

## 实战：根据会员等级计算折扣

```
fn get_discount(level: &str) -> f64 {
    if level == "gold" {
        0.8
    } else if level == "silver" {
        0.9
    } else {
        1.0
    }
}

fn main() {
    let level = "gold";
    let price = 200.0;

    let discount = get_discount(level);
    let final_price = price * discount;

    println!("会员等级：{}", level);
    println!("原价：{:.2}", price);
    println!("折后价：{:.2}", final_price);
}
```

输出：

```
会员等级：gold
原价：200.00
折后价：160.00
```

---

## 实战：登录权限判断

```
fn check_access(
    logged_in: bool,
    account_enabled: bool,
    is_admin: bool,
) -> &'static str {
    if !logged_in {
        return "请先登录";
    }

    if !account_enabled {
        return "账号已被禁用";
    }

    if !is_admin {
        return "没有管理员权限";
    }

    "允许访问后台"
}

fn main() {
    let message = check_access(true, true, false);

    println!("{}", message);
}
```

输出：

```
没有管理员权限
```

这里使用提前返回，避免了多层嵌套。

---

## 实战：判断闰年

闰年规则：

- • 能被 400 整除，是闰年
- • 不能被 400 整除，但能被 4 整除且不能被 100 整除，也是闰年

实现如下：

```
fn is_leap_year(year: u32) -> bool {
    if year % 400 == 0 {
        true
    } else if year % 100 == 0 {
        false
    } else {
        year % 4 == 0
    }
}

fn main() {
    let year = 2028;

    if is_leap_year(year) {
        println!("{} 是闰年", year);
    } else {
        println!("{} 不是闰年", year);
    }
}
```

还可以简化为：

```
fn is_leap_year(year: u32) -> bool {
    year % 400 == 0 || year % 4 == 0 && year % 100 != 0
}
```

---

## 条件运算中的优先级

逻辑表达式中：

```
!
```

优先级高于：

```
&&
```

而：

```
&&
```

优先级高于：

```
||
```

例如：

```
let result = true || false && false;
```

会先计算：

```
false && false
```

然后再计算：

```
true || false
```

结果为：

```
true
```

为了提高可读性，复杂条件建议加括号：

```
let result = true || (false && false);
```

---

## 短路求值

Rust 的 `&&` 和 `||` 支持短路求值。

例如：

```
fn main() {
    let logged_in = false;

    if logged_in && check_permission() {
        println!("允许访问");
    }
}

fn check_permission() -> bool {
    println!("检查权限");
    true
}
```

因为：

```
logged_in
```

已经是 `false` ，整个 `&&` 表达式一定为 `false` 。

因此：

```
check_permission()
```

不会执行。

同样，使用 `||` 时，如果左边已经是 `true` ，右边也不会继续执行。

---

## 常见错误

## 把赋值写成判断

错误：

```
if age = 18 {
    println!("成年");
}
```

赋值使用：

```
=
```

相等比较使用：

```
==
```

正确：

```
if age == 18 {
    println!("年龄正好是 18");
}
```

---

## 使用数字作为条件

错误：

```
if 1 {
    println!("执行");
}
```

正确：

```
if 1 != 0 {
    println!("执行");
}
```

---

## if 分支类型不一致

错误：

```
let result = if true {
    10
} else {
    "error"
};
```

正确：

```
let result = if true {
    10
} else {
    0
};
```

---

## 忘记 else 分支

如果 `if` 用作赋值表达式，一般需要 `else` 。

错误：

```
let result = if true {
    10
};
```

因为条件不成立时，程序不知道应该返回什么值。

正确：

```
let result = if true {
    10
} else {
    0
};
```

---

## 条件范围写错

例如：

```
if score >= 60 {
    println!("及格");
} else if score >= 90 {
    println!("优秀");
}
```

应该把更严格的条件放前面：

```
if score >= 90 {
    println!("优秀");
} else if score >= 60 {
    println!("及格");
}
```

---

## 最佳实践

## 简单布尔值不要重复比较

不推荐：

```
if logged_in == true {
    println!("已登录");
}
```

推荐：

```
if logged_in {
    println!("已登录");
}
```

判断为假时：

```
if !logged_in {
    println!("未登录");
}
```

---

## 避免过深嵌套

优先使用提前返回：

```
fn process_user(enabled: bool) {
    if !enabled {
        println!("用户已禁用");
        return;
    }

    println!("处理用户");
}
```

---

## 复杂条件拆成变量

不推荐：

```
if logged_in && enabled && total >= 100.0 && !blocked {
    println!("允许下单");
}
```

可以写成：

```
let can_order =
    logged_in &&
    enabled &&
    total >= 100.0 &&
    !blocked;

if can_order {
    println!("允许下单");
}
```

这样更容易理解和调试。

---

## 多个固定值判断时考虑 match

如果条件只是判断同一个变量的多个固定值：

```
if status == 0 {
    println!("待支付");
} else if status == 1 {
    println!("已支付");
} else if status == 2 {
    println!("已发货");
}
```

后续可以使用更适合的：

```
match
```

`match` 是 Rust 非常强大的模式匹配工具，将在后面的文章中详细介绍。

---

## 完整练习：订单优惠计算

下面编写一个完整的订单优惠程序。

规则如下：

- • 普通会员不打折
- • 白银会员打九折
- • 黄金会员打八折
- • 订单满 99 元免运费
- • 账号被禁用时不能下单

代码如下：

```
fn get_discount(level: &str) -> f64 {
    if level == "gold" {
        0.8
    } else if level == "silver" {
        0.9
    } else {
        1.0
    }
}

fn calculate_shipping(total: f64) -> f64 {
    if total >= 99.0 {
        0.0
    } else {
        10.0
    }
}

fn calculate_order(
    account_enabled: bool,
    member_level: &str,
    original_price: f64,
) -> f64 {
    if !account_enabled {
        println!("账号已被禁用，无法下单");
        return 0.0;
    }

    let discount = get_discount(member_level);
    let discounted_price = original_price * discount;
    let shipping = calculate_shipping(discounted_price);

    discounted_price + shipping
}

fn main() {
    let account_enabled = true;
    let member_level = "gold";
    let original_price = 120.0;

    let total = calculate_order(
        account_enabled,
        member_level,
        original_price,
    );

    println!("会员等级：{}", member_level);
    println!("商品原价：{:.2}", original_price);
    println!("订单实付：{:.2}", total);
}
```

输出：

```
会员等级：gold
商品原价：120.00
订单实付：96.00
```

需要注意：

折后金额为 96 元，不满足 99 元免邮条件，因此还应加上 10 元运费。

最终正确结果应为：

```
106.00
```

程序实际输出也会是：

```
订单实付：106.00
```

这个例子体现了实际开发中一个常见问题：

> 业务规则的执行顺序会直接影响最终结果。

先打折再判断免邮，与先判断免邮再打折，可能得到不同结果。因此编写业务逻辑时，必须明确规则顺序。

---

## 本章小结

`if` 是 Rust 中最常用的控制流工具。

通过本文，我们学习了：

- • `if` 的基本语法
- • `else` 和 `else if`
- • 条件必须是 `bool`
- • 比较运算符
- • `&&` 、 `||` 和 `!`
- • 嵌套条件判断
- • 提前返回
- • `if` 作为表达式返回值
- • 分支返回类型必须一致
- • 短路求值
- • 常见错误
- • 条件判断最佳实践

其中最重要的特点是：

> Rust 中的 `if` 是表达式，可以直接产生一个值。

理解这一点后，后面学习 `match` 、 `if let` 、循环表达式和错误处理都会更加容易。

---

## 下一篇预告

下一篇我们将学习 **Rust 循环控制：loop、while 与 for** ，包括：

- • 无限循环 `loop`
- • 使用 `break` 退出循环
- • 使用 `continue` 跳过当前循环
- • 从 `loop` 返回值
- • `while` 条件循环
- • `for` 遍历数组和范围
- • `range` 范围语法
- • 循环标签
- • 实战：统计、查找和批量处理数据

Rust 编程实战 · Table of Contents