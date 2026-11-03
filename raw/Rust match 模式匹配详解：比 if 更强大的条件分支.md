---
title: "Rust match 模式匹配详解：比 if 更强大的条件分支"
source: "https://mp.weixin.qq.com/s?__biz=MzYzODE1NzUzMw==&mid=2247484451&idx=1&sn=7747c613035210aea1ad036dabfe868b&chksm=f0e75391c790da87727ab3f0f92579a627f353f064604f825572054604e7c3634a9e44fcbc9e&cur_album_id=4602071361631748097&scene=189#wechat_redirect"
author:
published:
created: 2026-11-03
description: "《Rust 编程实战》系列第 13 篇在上一篇文章中，我们学习了 Rust 的三种循环：• loop• wh"
tags:
  - "clippings"
---
程序员爱钓鱼 *Jul 18, 2026, 8:15 AM*

> 《Rust 编程实战》系列第 13 篇

在上一篇文章中，我们学习了 Rust 的三种循环：

- • `loop`
- • `while`
- • `for`

这一篇将学习 Rust 最具代表性的语法之一： **模式匹配（Pattern Matching）** 。

Rust 使用 `match` 进行模式匹配。

它看起来有点像其他语言中的 `switch` ，但实际上比传统的 `switch` 强大得多。

`match` 不仅可以匹配数字和字符串，还可以匹配：

- • 枚举
- • 范围
- • 元组
- • 结构体
- • `Option`
- • `Result`
- • 引用
- • 变量
- • 嵌套数据

此外，Rust 编译器还会检查所有可能情况是否都被处理，这称为 **穷尽性检查** 。

本文将详细介绍：

- • `match` 的基本语法
- • 匹配多个值
- • 通配符 `_`
- • 范围匹配
- • 模式绑定
- • 匹配守卫
- • `match` 返回值
- • 元组匹配
- • 枚举匹配
- • `Option` 模式匹配
- • 常见错误
- • 实战案例

---

## 什么是模式匹配？

模式匹配可以理解为：

> 把一个值与多个模式进行比较，找到第一个匹配的模式，然后执行对应代码。

例如，根据数字输出星期名称：

```
fn main() {
    let day = 3;

    match day {
        1 => println!("星期一"),
        2 => println!("星期二"),
        3 => println!("星期三"),
        4 => println!("星期四"),
        5 => println!("星期五"),
        6 => println!("星期六"),
        7 => println!("星期日"),
        _ => println!("无效日期"),
    }
}
```

输出：

```
星期三
```

程序会把 `day` 依次与每个模式进行匹配。

当匹配到：

```
3 => println!("星期三")
```

时，就会执行对应代码。

---

## match 的基本语法

基本语法如下：

```
match 要匹配的值 {
    模式1 => 表达式1,
    模式2 => 表达式2,
    模式3 => 表达式3,
    _ => 默认表达式,
}
```

其中每一个：

```
模式 => 表达式
```

称为一个匹配分支，也称为：

```
match arm
```

例如：

```
fn main() {
    let number = 2;

    match number {
        1 => println!("一"),
        2 => println!("二"),
        3 => println!("三"),
        _ => println!("其他数字"),
    }
}
```

---

## match 分支之间使用逗号

每个匹配分支通常使用逗号分隔：

```
match number {
    1 => println!("一"),
    2 => println!("二"),
    _ => println!("其他"),
}
```

如果分支使用大括号包含多条语句，结尾逗号可以省略，但为了统一风格，通常建议保留。

例如：

```
fn main() {
    let number = 1;

    match number {
        1 => {
            println!("匹配到数字 1");
            println!("执行第一组逻辑");
        },
        2 => {
            println!("匹配到数字 2");
        },
        _ => {
            println!("其他数字");
        },
    }
}
```

---

## match 会从上到下匹配

`match` 会按照分支顺序，从上到下查找第一个符合条件的模式。

一旦匹配成功，后面的分支不会继续执行。

例如：

```
fn main() {
    let number = 5;

    match number {
        1..=10 => println!("1 到 10"),
        5 => println!("数字 5"),
        _ => println!("其他"),
    }
}
```

这段代码中， `5` 会先匹配：

```
1..=10
```

因此后面的：

```
5 => println!("数字 5")
```

不会执行。

编译器还可能提示后面的模式永远无法匹配。

正确顺序应该是：

```
fn main() {
    let number = 5;

    match number {
        5 => println!("数字 5"),
        1..=10 => println!("1 到 10"),
        _ => println!("其他"),
    }
}
```

---

## match 的穷尽性检查

Rust 要求 `match` 必须覆盖所有可能情况。

例如：

```
fn main() {
    let enabled = true;

    match enabled {
        true => println!("已经启用"),
    }
}
```

这段代码无法通过编译。

因为 `bool` 有两个可能值：

```
true
false
```

但代码只处理了 `true` 。

正确写法：

```
fn main() {
    let enabled = true;

    match enabled {
        true => println!("已经启用"),
        false => println!("尚未启用"),
    }
}
```

这种机制可以避免开发者漏掉某些情况。

---

## 使用通配符 \_

当我们不想逐一处理所有剩余情况时，可以使用：

```
_
```

它表示匹配任何未被前面分支匹配的值。

例如：

```
fn main() {
    let number = 10;

    match number {
        1 => println!("一"),
        2 => println!("二"),
        _ => println!("其他数字"),
    }
}
```

这里 `_` 会匹配除 1 和 2 以外的所有数字。

---

## 忽略剩余情况

如果对剩余情况不需要进行任何操作，可以写：

```
_ => (),
```

例如：

```
fn main() {
    let number = 8;

    match number {
        1 => println!("匹配到 1"),
        2 => println!("匹配到 2"),
        _ => (),
    }
}
```

`()` 是单元值，表示不做任何处理。

也可以使用空代码块：

```
_ => {}
```

---

## 匹配多个值

可以使用竖线：

```
|
```

表示“或者”。

例如：

```
fn main() {
    let number = 2;

    match number {
        1 | 2 | 3 => println!("数字在 1 到 3 之间"),
        4 | 5 => println!("数字是 4 或 5"),
        _ => println!("其他数字"),
    }
}
```

输出：

```
数字在 1 到 3 之间
```

这比重复写多个分支更加简洁。

---

## 范围匹配

可以使用：

```
..=
```

匹配包含边界的范围。

例如：

```
fn main() {
    let score = 85;

    match score {
        90..=100 => println!("优秀"),
        80..=89 => println!("良好"),
        60..=79 => println!("及格"),
        0..=59 => println!("不及格"),
        _ => println!("分数无效"),
    }
}
```

输出：

```
良好
```

这里必须使用：

```
..=
```

因为模式中的范围通常需要明确包含结束值。

---

## 字符范围匹配

范围匹配也可以用于字符。

例如：

```
fn main() {
    let ch = 'G';

    match ch {
        'a'..='z' => println!("小写英文字母"),
        'A'..='Z' => println!("大写英文字母"),
        '0'..='9' => println!("数字字符"),
        _ => println!("其他字符"),
    }
}
```

输出：

```
大写英文字母
```

---

## match 是表达式

和 `if` 一样， `match` 也是表达式，可以返回值。

例如：

```
fn main() {
    let status = 2;

    let message = match status {
        0 => "待处理",
        1 => "处理中",
        2 => "已完成",
        _ => "未知状态",
    };

    println!("{}", message);
}
```

输出：

```
已完成
```

这里整个 `match` 的结果被赋值给了：

```
message
```

---

## 各分支返回类型必须一致

正确示例：

```
fn main() {
    let status = 1;

    let message = match status {
        0 => "关闭",
        1 => "开启",
        _ => "未知",
    };

    println!("{}", message);
}
```

所有分支都返回 `&str` 。

错误示例：

```
fn main() {
    let status = 1;

    let value = match status {
        0 => 100,
        1 => "开启",
        _ => 0,
    };

    println!("{:?}", value);
}
```

一个分支返回整数，一个分支返回字符串，因此无法通过编译。

---

## 分支中执行多条语句

如果一个分支需要执行多条语句，可以使用代码块：

```
fn main() {
    let status = 1;

    match status {
        0 => {
            println!("当前状态：关闭");
            println!("请联系管理员开启");
        },
        1 => {
            println!("当前状态：正常");
            println!("可以继续操作");
        },
        _ => {
            println!("未知状态");
        },
    }
}
```

如果 `match` 需要返回值，代码块最后一个不带分号的表达式就是该分支的结果。

例如：

```
fn main() {
    let score = 92;

    let level = match score {
        90..=100 => {
            println!("成绩很好");
            "优秀"
        },
        60..=89 => {
            println!("成绩合格");
            "及格"
        },
        _ => {
            println!("需要继续努力");
            "不及格"
        },
    };

    println!("最终等级：{}", level);
}
```

---

## 模式绑定

`match` 不仅可以判断值，还可以把匹配到的内容绑定到变量。

例如：

```
fn main() {
    let number = 15;

    match number {
        value => println!("匹配到的值是：{}", value),
    }
}
```

这里的：

```
value
```

会绑定到 `number` 的值。

不过，这种写法会匹配所有情况，因此后面不能再写其他分支。

例如下面的代码是错误的：

```
match number {
    value => println!("{}", value),
    10 => println!("十"),
}
```

第一个 `value` 已经能匹配所有值，后面的分支永远无法执行。

---

## 使用 @ 进行绑定

Rust 可以使用：

```
@
```

在匹配范围的同时，把实际值绑定到变量。

例如：

```
fn main() {
    let age = 16;

    match age {
        value @ 0..=12 => {
            println!("{} 岁，属于儿童阶段", value);
        },
        value @ 13..=17 => {
            println!("{} 岁，属于青少年阶段", value);
        },
        value @ 18..=59 => {
            println!("{} 岁，属于成年人阶段", value);
        },
        value => {
            println!("{} 岁，属于其他年龄阶段", value);
        },
    }
}
```

输出：

```
16 岁，属于青少年阶段
```

`value @ 13..=17` 表示：

- • 匹配 13 到 17
- • 把实际值保存到 `value`

---

## 匹配守卫

模式匹配后还可以增加额外条件，称为：

```
Match Guard
```

语法：

```
模式 if 条件 => 表达式
```

例如：

```
fn main() {
    let number = 10;

    match number {
        value if value % 2 == 0 => {
            println!("{} 是偶数", value);
        },
        value => {
            println!("{} 是奇数", value);
        },
    }
}
```

输出：

```
10 是偶数
```

---

## 匹配守卫示例

根据用户年龄和会员状态判断权限：

```
fn main() {
    let age = 20;
    let is_member = true;

    match age {
        value if value >= 18 && is_member => {
            println!("成年会员");
        },
        value if value >= 18 => {
            println!("成年非会员");
        },
        _ => {
            println!("未成年用户");
        },
    }
}
```

匹配守卫适合处理模式本身无法直接表达的复杂条件。

---

## 匹配元组

`match` 可以直接匹配元组。

例如：

```
fn main() {
    let point = (0, 5);

    match point {
        (0, 0) => println!("位于原点"),
        (0, y) => println!("位于 Y 轴，y = {}", y),
        (x, 0) => println!("位于 X 轴，x = {}", x),
        (x, y) => println!("普通坐标：({}, {})", x, y),
    }
}
```

输出：

```
位于 Y 轴，y = 5
```

这里：

```
(0, y)
```

表示：

- • 第一个值必须是 0
- • 第二个值绑定到变量 `y`

---

## 忽略元组中的部分数据

可以使用 `_` 忽略不需要的值。

例如：

```
fn main() {
    let user = ("Tom", 20, true);

    match user {
        (name, _, true) => {
            println!("已启用用户：{}", name);
        },
        (name, _, false) => {
            println!("已禁用用户：{}", name);
        },
    }
}
```

这里年龄使用 `_` 忽略。

---

## 使用.. 忽略多个值

当元组或结构中有很多字段时，可以使用：

```
..
```

忽略剩余部分。

例如：

```
fn main() {
    let data = (10, 20, 30, 40, 50);

    match data {
        (first, .., last) => {
            println!("第一个：{}", first);
            println!("最后一个：{}", last);
        },
    }
}
```

输出：

```
第一个：10
最后一个：50
```

---

## 枚举与 match

`match` 最常见、最强大的使用场景是处理枚举。

先定义一个订单状态枚举：

```
enum OrderStatus {
    Pending,
    Paid,
    Shipped,
    Completed,
    Cancelled,
}
```

然后使用 `match` ：

```
fn print_order_status(status: OrderStatus) {
    match status {
        OrderStatus::Pending => {
            println!("订单待付款");
        },
        OrderStatus::Paid => {
            println!("订单已付款");
        },
        OrderStatus::Shipped => {
            println!("订单已发货");
        },
        OrderStatus::Completed => {
            println!("订单已完成");
        },
        OrderStatus::Cancelled => {
            println!("订单已取消");
        },
    }
}

fn main() {
    let status = OrderStatus::Paid;

    print_order_status(status);
}
```

输出：

```
订单已付款
```

---

## 枚举可以携带数据

Rust 枚举的成员可以保存数据。

例如：

```
enum Message {
    Quit,
    Text(String),
    Move(i32, i32),
}
```

使用 `match` 提取数据：

```
fn handle_message(message: Message) {
    match message {
        Message::Quit => {
            println!("退出程序");
        },
        Message::Text(content) => {
            println!("文本消息：{}", content);
        },
        Message::Move(x, y) => {
            println!("移动到坐标：({}, {})", x, y);
        },
    }
}

fn main() {
    let message = Message::Text(
        String::from("Hello Rust"),
    );

    handle_message(message);
}
```

输出：

```
文本消息：Hello Rust
```

这里：

```
Message::Text(content)
```

不仅匹配了枚举成员，还把其中的字符串提取到 `content` 。

---

## Option 与 match

`Option<T>` 是 Rust 中非常重要的枚举，用于表示某个值可能存在，也可能不存在。

它的定义可以简单理解为：

```
enum Option<T> {
    Some(T),
    None,
}
```

例如：

```
fn find_user(id: u64) -> Option<&'static str> {
    if id == 1 {
        Some("Tom")
    } else {
        None
    }
}
```

调用时可以使用 `match` ：

```
fn main() {
    let user = find_user(1);

    match user {
        Some(name) => {
            println!("找到用户：{}", name);
        },
        None => {
            println!("用户不存在");
        },
    }
}
```

输出：

```
找到用户：Tom
```

---

## 使用 match 处理 Option

再看一个数组查找示例：

```
fn main() {
    let numbers = [10, 20, 30];

    let result = numbers.get(1);

    match result {
        Some(value) => {
            println!("找到元素：{}", value);
        },
        None => {
            println!("索引超出范围");
        },
    }
}
```

输出：

```
找到元素：20
```

如果改成：

```
let result = numbers.get(10);
```

则输出：

```
索引超出范围
```

使用 `get()` 不会因为数组越界而直接 panic，而是返回 `Option` 。

---

## match 与 if else 的区别

下面的代码使用 `if else` ：

```
fn get_status(status: u8) -> &'static str {
    if status == 0 {
        "待付款"
    } else if status == 1 {
        "已付款"
    } else if status == 2 {
        "已发货"
    } else {
        "未知状态"
    }
}
```

使用 `match` ：

```
fn get_status(status: u8) -> &'static str {
    match status {
        0 => "待付款",
        1 => "已付款",
        2 => "已发货",
        _ => "未知状态",
    }
}
```

当判断同一个值的多个固定情况时， `match` 通常更加清晰。

---

## 什么时候使用 if？

适合复杂布尔条件：

```
if age >= 18 && logged_in && !blocked {
    println!("允许访问");
}
```

---

## 什么时候使用 match？

适合：

- • 同一个值有多个可能情况
- • 处理枚举
- • 处理 `Option`
- • 处理 `Result`
- • 解构元组和结构体
- • 需要编译器检查分支是否完整

---

## 实战：订单状态处理

```
#[derive(Debug)]
enum OrderStatus {
    Pending,
    Paid,
    Shipped,
    Completed,
    Cancelled,
}

fn get_status_message(status: &OrderStatus) -> &'static str {
    match status {
        OrderStatus::Pending => "订单等待付款",
        OrderStatus::Paid => "订单已经付款，等待发货",
        OrderStatus::Shipped => "订单已经发货",
        OrderStatus::Completed => "订单已经完成",
        OrderStatus::Cancelled => "订单已经取消",
    }
}

fn can_cancel(status: &OrderStatus) -> bool {
    match status {
        OrderStatus::Pending | OrderStatus::Paid => true,
        OrderStatus::Shipped
        | OrderStatus::Completed
        | OrderStatus::Cancelled => false,
    }
}

fn main() {
    let status = OrderStatus::Paid;

    println!("状态：{:?}", status);
    println!("说明：{}", get_status_message(&status));
    println!("能否取消：{}", can_cancel(&status));
}
```

输出：

```
状态：Paid
说明：订单已经付款，等待发货
能否取消：true
```

---

## 实战：HTTP 状态码处理

```
fn get_http_message(code: u16) -> &'static str {
    match code {
        200 => "请求成功",
        201 => "创建成功",
        400 => "请求参数错误",
        401 => "未登录或登录已过期",
        403 => "没有访问权限",
        404 => "资源不存在",
        500..=599 => "服务器内部错误",
        _ => "未知状态码",
    }
}

fn main() {
    let code = 404;

    println!("{}：{}", code, get_http_message(code));
}
```

输出：

```
404：资源不存在
```

---

## 实战：根据用户角色判断权限

```
enum UserRole {
    Guest,
    User,
    Editor,
    Admin,
}

fn get_permissions(role: UserRole) -> &'static str {
    match role {
        UserRole::Guest => "只能浏览公开内容",
        UserRole::User => "可以浏览和评论",
        UserRole::Editor => "可以编辑和发布文章",
        UserRole::Admin => "拥有全部管理权限",
    }
}

fn main() {
    let role = UserRole::Editor;

    println!("{}", get_permissions(role));
}
```

输出：

```
可以编辑和发布文章
```

---

## 实战：简单计算器

```
fn calculate(
    left: f64,
    operator: char,
    right: f64,
) -> Option<f64> {
    match operator {
        '+' => Some(left + right),
        '-' => Some(left - right),
        '*' => Some(left * right),
        '/' if right != 0.0 => Some(left / right),
        '/' => None,
        _ => None,
    }
}

fn main() {
    let result = calculate(10.0, '/', 2.0);

    match result {
        Some(value) => {
            println!("计算结果：{}", value);
        },
        None => {
            println!("无法完成计算");
        },
    }
}
```

输出：

```
计算结果：5
```

这里使用了：

- • 字符匹配
- • 匹配守卫
- • `Option`
- • `match` 解构

---

## 实战：处理用户查询结果

```
struct User {
    id: u64,
    name: String,
    enabled: bool,
}

fn find_user(id: u64) -> Option<User> {
    match id {
        1 => Some(User {
            id: 1,
            name: String::from("Tom"),
            enabled: true,
        }),
        2 => Some(User {
            id: 2,
            name: String::from("Alice"),
            enabled: false,
        }),
        _ => None,
    }
}

fn main() {
    let result = find_user(2);

    match result {
        Some(user) if user.enabled => {
            println!(
                "用户 {} 可以正常使用系统",
                user.name
            );
        },
        Some(user) => {
            println!(
                "用户 {} 已被禁用",
                user.name
            );
        },
        None => {
            println!("用户不存在");
        },
    }
}
```

输出：

```
用户 Alice 已被禁用
```

---

## 常见错误

## 没有覆盖所有情况

错误：

```
fn main() {
    let enabled = true;

    match enabled {
        true => println!("开启"),
    }
}
```

正确：

```
match enabled {
    true => println!("开启"),
    false => println!("关闭"),
}
```

或者：

```
match enabled {
    true => println!("开启"),
    _ => println!("关闭"),
}
```

---

## 把通配符写在前面

错误：

```
match number {
    _ => println!("其他"),
    1 => println!("一"),
}
```

`_` 已经匹配所有值，因此后面的分支无法执行。

通配符通常应该放在最后。

---

## 分支返回类型不同

错误：

```
let result = match number {
    1 => 100,
    2 => "two",
    _ => 0,
};
```

所有分支必须返回相同类型。

---

## 范围分支顺序错误

错误：

```
match score {
    0..=100 => println!("有效分数"),
    90..=100 => println!("优秀"),
    _ => println!("无效"),
}
```

第二个分支永远不会匹配。

应该把范围更小、更具体的分支放前面。

---

## 模式变量覆盖外部变量

例如：

```
fn main() {
    let value = 10;
    let number = 20;

    match number {
        value => println!("{}", value),
    }
}
```

这里模式中的 `value` 创建了一个新变量，并没有与外部的 `value = 10` 比较。

如果想匹配固定值，更适合直接写字面量、常量，或者使用匹配守卫。

例如：

```
fn main() {
    let expected = 10;
    let number = 20;

    match number {
        value if value == expected => {
            println!("匹配成功");
        },
        _ => {
            println!("匹配失败");
        },
    }
}
```

---

## 最佳实践

## 处理枚举时尽量列出全部成员

例如：

```
match status {
    OrderStatus::Pending => {},
    OrderStatus::Paid => {},
    OrderStatus::Shipped => {},
    OrderStatus::Completed => {},
    OrderStatus::Cancelled => {},
}
```

这样以后给枚举增加新成员时，编译器会提醒你更新相关代码。

如果直接使用：

```
_ => {}
```

编译器可能无法帮助你发现遗漏的业务逻辑。

---

## 通配符只用于确实不关心的情况

例如：

```
match number {
    1 => println!("一"),
    _ => {},
}
```

如果剩余情况对业务很重要，就不应该简单忽略。

---

## 固定值判断优先使用 match

例如：

```
match status {
    0 => "待处理",
    1 => "处理中",
    2 => "已完成",
    _ => "未知",
}
```

通常比多个 `else if` 更容易阅读。

---

## 复杂条件使用匹配守卫

例如：

```
match age {
    value if value >= 18 && is_member => {
        println!("成年会员");
    },
    value if value >= 18 => {
        println!("成年用户");
    },
    _ => {
        println!("未成年用户");
    },
}
```

---

## 不要让单个 match 过于庞大

如果每个分支包含大量业务逻辑，可以把逻辑拆成函数。

例如：

```
match status {
    OrderStatus::Pending => handle_pending(),
    OrderStatus::Paid => handle_paid(),
    OrderStatus::Shipped => handle_shipped(),
    OrderStatus::Completed => handle_completed(),
    OrderStatus::Cancelled => handle_cancelled(),
}
```

这样更加容易维护和测试。

---

## 完整练习：订单操作处理系统

下面实现一个简单的订单操作系统。

```
#[derive(Debug)]
enum OrderStatus {
    Pending,
    Paid,
    Shipped,
    Completed,
    Cancelled,
}

enum OrderAction {
    Pay,
    Ship,
    Confirm,
    Cancel,
}

fn process_order(
    status: OrderStatus,
    action: OrderAction,
) -> OrderStatus {
    match (status, action) {
        (OrderStatus::Pending, OrderAction::Pay) => {
            println!("订单付款成功");
            OrderStatus::Paid
        },

        (OrderStatus::Pending, OrderAction::Cancel) => {
            println!("订单取消成功");
            OrderStatus::Cancelled
        },

        (OrderStatus::Paid, OrderAction::Ship) => {
            println!("订单发货成功");
            OrderStatus::Shipped
        },

        (OrderStatus::Paid, OrderAction::Cancel) => {
            println!("付款订单已取消，准备退款");
            OrderStatus::Cancelled
        },

        (OrderStatus::Shipped, OrderAction::Confirm) => {
            println!("确认收货成功");
            OrderStatus::Completed
        },

        (current_status, _) => {
            println!("当前状态不支持该操作");
            current_status
        },
    }
}

fn main() {
    let status = OrderStatus::Pending;

    let status = process_order(
        status,
        OrderAction::Pay,
    );

    println!("当前状态：{:?}", status);

    let status = process_order(
        status,
        OrderAction::Ship,
    );

    println!("当前状态：{:?}", status);

    let status = process_order(
        status,
        OrderAction::Confirm,
    );

    println!("最终状态：{:?}", status);
}
```

输出：

```
订单付款成功
当前状态：Paid
订单发货成功
当前状态：Shipped
确认收货成功
最终状态：Completed
```

这个例子综合使用了：

- • 枚举
- • 元组匹配
- • 模式绑定
- • 通配符
- • `match` 返回值
- • 变量遮蔽
- • 订单状态流转

这类状态流转逻辑非常适合使用 `match` 实现。

---

## 本章小结

`match` 是 Rust 中最强大的控制流工具之一。

通过本文，我们学习了：

- • `match` 的基本语法
- • 匹配分支 `match arm`
- • 穷尽性检查
- • 通配符 `_`
- • 匹配多个值
- • 范围匹配
- • 字符范围
- • `match` 作为表达式返回值
- • 模式绑定
- • `@` 绑定
- • 匹配守卫
- • 元组解构
- • 忽略部分数据
- • 枚举模式匹配
- • `Option` 模式匹配
- • 常见错误与最佳实践

与普通 `switch` 相比，Rust 的 `match` 不只是值判断工具，更是一个强大的数据解构和状态处理系统。

在实际 Rust 项目中， `match` 会频繁用于：

- • 处理枚举状态
- • 处理 `Option`
- • 处理 `Result`
- • 解析命令
- • 处理网络消息
- • 状态机
- • 错误分类
- • 业务流程控制

---

## 下一篇预告

下一篇我们将学习 **Rust 的 `if let` 与 `while let`** ，包括：

- • 为什么需要 `if let`
- • 使用 `if let` 简化单分支匹配
- • `if let else`
- • 使用 `while let` 持续匹配数据
- • 遍历栈和队列
- • `match` 、 `if let` 与 `while let` 的选择
- • 实战：处理可选用户与消息队列

Rust 编程实战 · Table of Contents