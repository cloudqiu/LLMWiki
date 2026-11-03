---
title: "Rust if let 与 while let 详解：简化模式匹配"
source: "https://mp.weixin.qq.com/s?__biz=MzYzODE1NzUzMw==&mid=2247484455&idx=1&sn=98edda2f7f33ed0eb2ab4ff0bea02f4a&chksm=f0e75395c790da83bd0a78f398bd7727041de96e49d1a07cdbccc84c440eef371042cb9ffccf&cur_album_id=4602071361631748097&scene=189#wechat_redirect"
author:
published:
created: 2026-11-03
description: "《Rust 编程实战》系列第 14 篇在上一篇文章中，我们学习了 Rust 的 match 模式匹配。"
tags:
  - "clippings"
---
程序员爱钓鱼 *Jul 19, 2026, 4:24 AM*

> 《Rust 编程实战》系列第 14 篇

在上一篇文章中，我们学习了 Rust 的 `match` 模式匹配。

`match` 非常强大，能够处理：

- • 枚举
- • 元组
- • 范围
- • `Option`
- • `Result`
- • 模式绑定
- • 匹配守卫

但在实际开发中，有些场景只关心其中一种情况。

例如：

- • 只关心 `Option` 是否为 `Some`
- • 只关心 `Result` 是否成功
- • 只处理某一个枚举成员
- • 只在匹配成功时执行代码

如果每次都使用完整的 `match` ，代码可能显得有些冗长。

Rust 为这种场景提供了两个更简洁的语法：

```
if let
```

和：

```
while let
```

本文将详细介绍：

- • `if let` 的基本语法
- • `if let else`
- • 使用 `if let` 处理 `Option`
- • 使用 `if let` 处理 `Result`
- • 使用 `if let` 匹配枚举
- • `while let` 的基本语法
- • 使用 `while let` 处理栈
- • 使用 `while let` 处理消息
- • `match` 、 `if let` 与 `while let` 的区别
- • 常见错误
- • 实战案例

---

## 为什么需要 if let？

先来看一个使用 `match` 的例子。

```
fn main() {
    let user_name = Some("Tom");

    match user_name {
        Some(name) => {
            println!("用户名：{}", name);
        },
        None => {},
    }
}
```

这段代码只关心：

```
Some(name)
```

对于：

```
None
```

不需要执行任何操作。

这时可以使用 `if let` 简化：

```
fn main() {
    let user_name = Some("Tom");

    if let Some(name) = user_name {
        println!("用户名：{}", name);
    }
}
```

输出：

```
用户名：Tom
```

代码更简洁，也更容易阅读。

---

## if let 的基本语法

基本语法如下：

```
if let 模式 = 值 {
    匹配成功时执行的代码
}
```

例如：

```
fn main() {
    let value = Some(100);

    if let Some(number) = value {
        println!("数字：{}", number);
    }
}
```

这里：

```
Some(number)
```

是模式。

```
value
```

是要匹配的值。

如果 `value` 是 `Some` ，其中的数据会绑定到 `number` 。

---

## if let 与 match 的关系

下面两段代码作用相同。

使用 `match` ：

```
match value {
    Some(number) => {
        println!("{}", number);
    },
    _ => {},
}
```

使用 `if let` ：

```
if let Some(number) = value {
    println!("{}", number);
}
```

可以理解为：

> `if let` 是只关心一个匹配分支时，对 `match` 的简化写法。

---

## 使用 if let 处理 Option

`Option<T>` 有两个成员：

```
Some(T)
None
```

例如：

```
fn find_user(id: u64) -> Option<&'static str> {
    if id == 1 {
        Some("Alice")
    } else {
        None
    }
}

fn main() {
    let result = find_user(1);

    if let Some(name) = result {
        println!("找到用户：{}", name);
    }
}
```

输出：

```
找到用户：Alice
```

如果：

```
find_user(100)
```

返回 `None` ，代码块不会执行。

---

## if let else

如果匹配失败时也需要执行代码，可以增加：

```
else
```

例如：

```
fn main() {
    let user_name: Option<&str> = None;

    if let Some(name) = user_name {
        println!("用户名：{}", name);
    } else {
        println!("用户名不存在");
    }
}
```

输出：

```
用户名不存在
```

它等价于：

```
match user_name {
    Some(name) => {
        println!("用户名：{}", name);
    },
    None => {
        println!("用户名不存在");
    },
}
```

---

## 使用 if let 匹配枚举

`if let` 不仅能处理 `Option` ，也可以匹配普通枚举。

例如：

```
enum Message {
    Text(String),
    Image(String),
    Quit,
}

fn main() {
    let message = Message::Text(
        String::from("Hello Rust"),
    );

    if let Message::Text(content) = message {
        println!("文本消息：{}", content);
    }
}
```

输出：

```
文本消息：Hello Rust
```

这里只关心：

```
Message::Text
```

所以使用 `if let` 比完整 `match` 更简洁。

---

## 使用 if let 处理 Result

`Result<T, E>` 有两个成员：

```
Ok(T)
Err(E)
```

只关心成功结果时，可以写：

```
fn main() {
    let result: Result<i32, &str> = Ok(100);

    if let Ok(value) = result {
        println!("操作成功：{}", value);
    }
}
```

输出：

```
操作成功：100
```

---

## 只处理错误

如果只关心失败情况，可以匹配：

```
Err(error)
```

例如：

```
fn main() {
    let result: Result<i32, &str> =
        Err("连接服务器失败");

    if let Err(error) = result {
        println!("发生错误：{}", error);
    }
}
```

输出：

```
发生错误：连接服务器失败
```

---

## if let 可以解构元组

例如：

```
fn main() {
    let point = Some((10, 20));

    if let Some((x, y)) = point {
        println!("坐标：({}, {})", x, y);
    }
}
```

输出：

```
坐标：(10, 20)
```

这里同时完成了两层匹配：

1. 1\. 匹配 `Some`
2. 2\. 解构其中的元组

---

## if let 可以解构结构体

定义一个结构体：

```
struct User {
    name: String,
    age: u8,
}
```

然后匹配：

```
fn main() {
    let user = Some(User {
        name: String::from("Tom"),
        age: 20,
    });

    if let Some(User { name, age }) = user {
        println!("姓名：{}", name);
        println!("年龄：{}", age);
    }
}
```

输出：

```
姓名：Tom
年龄：20
```

---

## 忽略不需要的字段

可以使用：

```
..
```

忽略其他字段。

例如：

```
struct User {
    id: u64,
    name: String,
    age: u8,
    enabled: bool,
}

fn main() {
    let user = Some(User {
        id: 1,
        name: String::from("Alice"),
        age: 22,
        enabled: true,
    });

    if let Some(User { name, .. }) = user {
        println!("用户名：{}", name);
    }
}
```

这里只提取 `name` ，其他字段全部忽略。

---

## if let 与匹配守卫

传统 `if let` 可以在代码块内部继续写条件判断：

```
fn main() {
    let value = Some(20);

    if let Some(number) = value {
        if number >= 18 {
            println!("数值大于等于 18");
        }
    }
}
```

现代 Rust 还支持 let chain，在一个条件中组合多个判断：

```
fn main() {
    let value = Some(20);

    if let Some(number) = value
        && number >= 18
    {
        println!("数值大于等于 18");
    }
}
```

这种写法能减少嵌套。

如果需要兼容较旧的 Rust 版本，可以继续使用嵌套 `if` 。

---

## 多个 if let 条件

例如，同时判断用户和权限：

```
fn main() {
    let user = Some("Tom");
    let role = Some("admin");

    if let Some(name) = user
        && let Some(user_role) = role
        && user_role == "admin"
    {
        println!("管理员用户：{}", name);
    }
}
```

这类写法适合多个可选值必须同时存在的场景。

---

## let else

除了 `if let` ，Rust 还提供：

```
let else
```

它适合匹配失败时提前退出函数。

例如：

```
fn print_user(user: Option<&str>) {
    let Some(name) = user else {
        println!("用户不存在");
        return;
    };

    println!("用户名：{}", name);
}

fn main() {
    print_user(Some("Alice"));
    print_user(None);
}
```

输出：

```
用户名：Alice
用户不存在
```

这种写法可以避免多层嵌套。

---

## if let 与 let else 的区别

`if let` ：

```
if let Some(name) = user {
    println!("{}", name);
}
```

适合匹配成功时执行某段逻辑。

`let else` ：

```
let Some(name) = user else {
    return;
};
```

适合匹配失败时提前返回，然后继续使用匹配到的数据。

例如：

```
fn process_user(user: Option<&str>) {
    let Some(name) = user else {
        println!("用户不存在");
        return;
    };

    println!("开始处理用户：{}", name);
    println!("加载用户权限");
    println!("加载用户订单");
}
```

---

## 什么是 while let？

`if let` 只匹配一次。

如果希望在模式持续匹配成功时不断循环，可以使用：

```
while let
```

基本语法：

```
while let 模式 = 值 {
    匹配成功时重复执行
}
```

当匹配失败时，循环自动结束。

---

## while let 基本示例

```
fn main() {
    let mut number = Some(3);

    while let Some(value) = number {
        println!("{}", value);

        if value == 1 {
            number = None;
        } else {
            number = Some(value - 1);
        }
    }

    println!("循环结束");
}
```

输出：

```
3
2
1
循环结束
```

只要 `number` 是：

```
Some(value)
```

循环就会继续。

当它变成：

```
None
```

循环结束。

---

## while let 与 loop + match

下面的代码使用 `loop` 和 `match` ：

```
fn main() {
    let mut stack = vec![1, 2, 3];

    loop {
        match stack.pop() {
            Some(value) => {
                println!("{}", value);
            },
            None => {
                break;
            },
        }
    }
}
```

可以简化为：

```
fn main() {
    let mut stack = vec![1, 2, 3];

    while let Some(value) = stack.pop() {
        println!("{}", value);
    }
}
```

输出：

```
3
2
1
```

---

## 使用 while let 处理栈

`Vec` 的：

```
pop()
```

方法会返回：

```
Option<T>
```

如果向量中有数据，返回：

```
Some(value)
```

如果为空，返回：

```
None
```

因此非常适合使用 `while let` 。

完整示例：

```
fn main() {
    let mut tasks = vec![
        String::from("生成报表"),
        String::from("发送邮件"),
        String::from("备份数据库"),
    ];

    while let Some(task) = tasks.pop() {
        println!("正在处理：{}", task);
    }

    println!("所有任务处理完成");
}
```

输出：

```
正在处理：备份数据库
正在处理：发送邮件
正在处理：生成报表
所有任务处理完成
```

注意， `pop()` 从向量尾部取数据，所以顺序是后进先出。

---

## 使用 while let 遍历迭代器

迭代器的：

```
next()
```

方法也返回：

```
Option<T>
```

因此可以使用 `while let` 。

例如：

```
fn main() {
    let numbers = vec![10, 20, 30];
    let mut iterator = numbers.into_iter();

    while let Some(number) = iterator.next() {
        println!("{}", number);
    }
}
```

输出：

```
10
20
30
```

不过，普通集合遍历通常更推荐使用 `for` ：

```
for number in numbers {
    println!("{}", number);
}
```

`while let` 更适合需要手动控制迭代过程的情况。

---

## 使用 while let 处理消息队列

假设有一个简单的消息队列：

```
enum Message {
    Text(String),
    Stop,
}
```

可以这样处理：

```
fn main() {
    let mut messages = vec![
        Message::Stop,
        Message::Text(String::from("第二条消息")),
        Message::Text(String::from("第一条消息")),
    ];

    while let Some(message) = messages.pop() {
        match message {
            Message::Text(content) => {
                println!("收到消息：{}", content);
            },
            Message::Stop => {
                println!("收到停止命令");
                break;
            },
        }
    }
}
```

输出：

```
收到消息：第一条消息
收到消息：第二条消息
收到停止命令
```

这里：

- • `while let` 负责从队列中持续取数据
- • `match` 负责处理不同消息类型

---

## while let 只关心一种消息

如果只处理文本消息，可以写：

```
fn main() {
    let mut messages = vec![
        Message::Text(String::from("消息三")),
        Message::Text(String::from("消息二")),
        Message::Text(String::from("消息一")),
    ];

    while let Some(Message::Text(content)) = messages.pop() {
        println!("收到文本：{}", content);
    }
}
```

这里同时匹配：

- • 外层 `Some`
- • 内层 `Message::Text`

如果取出的值不是文本消息，循环会立即结束。

---

## while let 处理 Result

`while let` 也可以处理连续成功的操作。

例如：

```
fn main() {
    let mut values = vec!["30", "20", "10"];
    let mut index = 0;

    while let Some(text) = values.pop() {
        if let Ok(number) = text.parse::<i32>() {
            println!("解析成功：{}", number);
            index += 1;
        }
    }

    println!("成功解析 {} 个数字", index);
}
```

输出：

```
解析成功：10
解析成功：20
解析成功：30
成功解析 3 个数字
```

---

## 实战：处理可选用户

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
    let result = find_user(1);

    if let Some(user) = result {
        println!("用户编号：{}", user.id);
        println!("用户名：{}", user.name);
        println!("是否启用：{}", user.enabled);
    } else {
        println!("用户不存在");
    }
}
```

输出：

```
用户编号：1
用户名：Tom
是否启用：true
```

---

## 实战：读取配置端口

```
fn parse_port(value: Option<&str>) -> Option<u16> {
    if let Some(text) = value {
        if let Ok(port) = text.parse::<u16>() {
            return Some(port);
        }
    }

    None
}

fn main() {
    let config_port = Some("8080");

    if let Some(port) = parse_port(config_port) {
        println!("服务端口：{}", port);
    } else {
        println!("端口配置无效");
    }
}
```

输出：

```
服务端口：8080
```

可以使用 let chain 简化：

```
fn parse_port(value: Option<&str>) -> Option<u16> {
    if let Some(text) = value
        && let Ok(port) = text.parse::<u16>()
    {
        return Some(port);
    }

    None
}
```

---

## 实战：批量处理任务

```
#[derive(Debug)]
struct Task {
    id: u64,
    name: String,
}

fn main() {
    let mut tasks = vec![
        Task {
            id: 1,
            name: String::from("导入用户"),
        },
        Task {
            id: 2,
            name: String::from("生成报表"),
        },
        Task {
            id: 3,
            name: String::from("备份文件"),
        },
    ];

    while let Some(task) = tasks.pop() {
        println!(
            "开始处理任务 {}：{}",
            task.id,
            task.name
        );

        println!("任务处理完成");
    }

    println!("任务队列为空");
}
```

输出：

```
开始处理任务 3：备份文件
任务处理完成
开始处理任务 2：生成报表
任务处理完成
开始处理任务 1：导入用户
任务处理完成
任务队列为空
```

---

## 实战：订单查询与状态判断

```
#[derive(Debug)]
enum OrderStatus {
    Pending,
    Paid,
    Shipped,
    Completed,
}

struct Order {
    id: u64,
    status: OrderStatus,
}

fn find_order(id: u64) -> Option<Order> {
    if id == 1001 {
        Some(Order {
            id,
            status: OrderStatus::Paid,
        })
    } else {
        None
    }
}

fn main() {
    let result = find_order(1001);

    let Some(order) = result else {
        println!("订单不存在");
        return;
    };

    println!("订单编号：{}", order.id);

    if let OrderStatus::Paid = order.status {
        println!("订单已付款，可以安排发货");
    }
}
```

输出：

```
订单编号：1001
订单已付款，可以安排发货
```

---

## match、if let 和 while let 的区别

## match

适合处理多个分支。

```
match value {
    Some(value) => println!("{}", value),
    None => println!("没有数据"),
}
```

特点：

- • 可以处理所有情况
- • 支持穷尽性检查
- • 适合枚举和复杂模式
- • 分支较多时最清晰

---

## if let

适合只关心一种模式。

```
if let Some(value) = value {
    println!("{}", value);
}
```

特点：

- • 写法简洁
- • 不要求列出所有分支
- • 适合单一成功情况
- • 可配合 `else`

---

## while let

适合只要模式持续匹配，就不断循环。

```
while let Some(value) = stack.pop() {
    println!("{}", value);
}
```

特点：

- • 模式匹配成功时继续循环
- • 匹配失败时自动结束
- • 常用于 `Option`
- • 常用于迭代器、栈和消息队列

---

## 如何选择？

可以使用下面的规则：

| 场景 | 推荐语法 |
| --- | --- |
| 处理多个枚举成员 | `match` |
| 需要穷尽性检查 | `match` |
| 只关心一个匹配结果 | `if let` |
| 匹配失败时提前退出 | `let else` |
| 模式成功时持续循环 | `while let` |
| 普通集合遍历 | `for` |

---

## 常见错误

## 模式和值顺序写反

错误：

```
if let value = Some(number) {
}
```

正确语法是：

```
if let Some(number) = value {
}
```

左边是模式，右边是被匹配的值。

---

## 把 if let 当作普通等值判断

下面代码虽然可以编译，但不推荐：

```
let number = 10;

if let 10 = number {
    println!("等于 10");
}
```

对于简单数值比较，直接使用：

```
if number == 10 {
    println!("等于 10");
}
```

更加清晰。

`if let` 更适合解构复杂模式。

---

## if let 忽略了重要分支

例如：

```
if let Ok(value) = result {
    println!("{}", value);
}
```

这会静默忽略所有错误。

如果错误对业务很重要，应该使用：

```
match result {
    Ok(value) => println!("{}", value),
    Err(error) => println!("错误：{}", error),
}
```

或者：

```
if let Ok(value) = result {
    println!("{}", value);
} else {
    println!("操作失败");
}
```

---

## while let 中匹配值没有变化

例如：

```
fn main() {
    let value = Some(10);

    while let Some(number) = value {
        println!("{}", number);
    }
}
```

这会形成无限循环。

因为 `value` 永远都是：

```
Some(10)
```

`while let` 中必须确保被匹配的值会发生变化，或者循环内部存在 `break` 。

---

## while let 提前结束

例如：

```
enum Message {
    Text(String),
    Image(String),
}

fn main() {
    let mut messages = vec![
        Message::Text(String::from("第二条")),
        Message::Image(String::from("image.png")),
        Message::Text(String::from("第一条")),
    ];

    while let Some(Message::Text(content)) = messages.pop() {
        println!("{}", content);
    }
}
```

第一次取出文本消息后继续循环。

第二次取出图片消息时，模式匹配失败，整个循环立即结束。

剩余消息不会继续处理。

如果希望处理所有消息，应改成：

```
while let Some(message) = messages.pop() {
    match message {
        Message::Text(content) => {
            println!("文本：{}", content);
        },
        Message::Image(path) => {
            println!("图片：{}", path);
        },
    }
}
```

---

## 最佳实践

## 单分支匹配优先使用 if let

不推荐：

```
match value {
    Some(value) => {
        println!("{}", value);
    },
    _ => {},
}
```

推荐：

```
if let Some(value) = value {
    println!("{}", value);
}
```

---

## 多个重要分支使用 match

不推荐为了简短而写多个独立的 `if let` ：

```
if let Message::Text(content) = message {
}

if let Message::Image(path) = message {
}
```

这还可能涉及所有权移动问题。

推荐：

```
match message {
    Message::Text(content) => {},
    Message::Image(path) => {},
    Message::Quit => {},
}
```

---

## 匹配失败后无法继续时使用 let else

例如：

```
fn process_user(user: Option<User>) {
    let Some(user) = user else {
        return;
    };

    println!("{}", user.name);
}
```

这种写法比嵌套 `if let` 更清晰。

---

## while let 中明确数据如何变化

例如：

```
while let Some(task) = tasks.pop() {
    process_task(task);
}
```

这里每次 `pop()` 都会减少一个元素，因此循环最终会结束。

---

## 不要静默忽略关键错误

例如数据库写入失败、支付失败、文件保存失败，不应该只写：

```
if let Ok(_) = result {
    println!("成功");
}
```

更合适的是：

```
match result {
    Ok(_) => println!("成功"),
    Err(error) => println!("失败：{}", error),
}
```

---

## 完整练习：消息任务处理系统

下面实现一个简单的消息任务处理系统。

```
#[derive(Debug)]
enum Task {
    SendEmail {
        address: String,
        subject: String,
    },
    GenerateReport {
        name: String,
    },
    Backup {
        path: String,
    },
}

fn process_task(task: Task) {
    match task {
        Task::SendEmail {
            address,
            subject,
        } => {
            println!(
                "发送邮件到 {}，主题：{}",
                address,
                subject
            );
        },

        Task::GenerateReport { name } => {
            println!("生成报表：{}", name);
        },

        Task::Backup { path } => {
            println!("备份目录：{}", path);
        },
    }
}

fn main() {
    let mut tasks = vec![
        Task::Backup {
            path: String::from("/data"),
        },
        Task::GenerateReport {
            name: String::from("月度销售报表"),
        },
        Task::SendEmail {
            address: String::from("admin@example.com"),
            subject: String::from("任务完成通知"),
        },
    ];

    while let Some(task) = tasks.pop() {
        process_task(task);
    }

    println!("全部任务处理完成");
}
```

输出：

```
发送邮件到 admin@example.com，主题：任务完成通知
生成报表：月度销售报表
备份目录：/data
全部任务处理完成
```

这个案例综合使用了：

- • 枚举
- • 结构化枚举成员
- • `while let`
- • `match`
- • 模式解构
- • 任务队列

在实际项目中，这种模式可以用于：

- • 消息队列消费者
- • 后台任务处理
- • 文件批处理
- • 网络事件处理
- • 命令分发
- • 桌面软件任务队列

---

## 本章小结

`if let` 和 `while let` 都是建立在 Rust 模式匹配能力之上的简化语法。

通过本文，我们学习了：

- • `if let` 基本语法
- • `if let else`
- • 使用 `if let` 处理 `Option`
- • 使用 `if let` 处理 `Result`
- • 匹配普通枚举
- • 解构元组和结构体
- • `let else`
- • let chain
- • `while let` 基本语法
- • 使用 `while let` 处理栈
- • 使用 `while let` 处理迭代器
- • 使用 `while let` 处理任务队列
- • `match` 、 `if let` 和 `while let` 的区别
- • 常见错误与最佳实践

可以记住三个简单原则：

> 多种情况使用 `match` 。

> 只关心一种情况使用 `if let` 。

> 只要匹配成功就继续循环，使用 `while let` 。

---

## 下一篇预告

下一篇我们将学习 **Rust 所有权基础** ，包括：

- • 什么是所有权
- • 栈与堆
- • 变量作用域
- • `String` 的内存结构
- • 移动语义
- • `clone`
- • `Copy` 类型
- • 函数参数与所有权转移
- • 函数返回值与所有权
- • 常见所有权错误

Rust 编程实战 · Table of Contents