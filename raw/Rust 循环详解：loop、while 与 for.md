---
title: "Rust 循环详解：loop、while 与 for"
source: "https://mp.weixin.qq.com/s?__biz=MzYzODE1NzUzMw==&mid=2247484447&idx=1&sn=802b0f1a33592f0e6d9915d687478a39&chksm=f0e753adc790dabba39c783154628ca44671a0735951ed0e3ba4eabb1398adbfc934684ea3de&cur_album_id=4602071361631748097&scene=189#wechat_redirect"
author:
published:
created: 2026-11-03
description: "《Rust 编程实战》系列第 12 篇在上一篇文章中，我们学习了 if 条件判断。"
tags:
  - "clippings"
---
程序员爱钓鱼 *Jul 17, 2026, 7:20 AM*

> 《Rust 编程实战》系列第 12 篇

在上一篇文章中，我们学习了 `if` 条件判断。

`if` 可以让程序根据条件选择不同的执行路径，而循环则可以让程序重复执行某段代码。

例如：

- • 重复输出一段内容
- • 遍历数组
- • 批量处理文件
- • 统计商品数量
- • 不断读取用户输入
- • 轮询服务器状态
- • 重试网络请求
- • 持续监听消息

Rust 提供了三种主要循环方式：

- • `loop`
- • `while`
- • `for`

本文将详细介绍这三种循环的使用方法，以及：

- • `break`
- • `continue`
- • 循环返回值
- • 范围语法
- • 倒序遍历
- • 循环标签
- • 常见错误
- • 实战案例

---

## 什么是循环？

循环可以理解为：

> 在满足一定条件时，重复执行一段代码。

例如，我们希望输出 1 到 5。

如果不使用循环，可以写成：

```
fn main() {
    println!("1");
    println!("2");
    println!("3");
    println!("4");
    println!("5");
}
```

虽然可以运行，但代码重复很多。

使用循环后：

```
fn main() {
    for number in 1..=5 {
        println!("{}", number);
    }
}
```

代码会更加简洁。

输出：

```
1
2
3
4
5
```

---

## Rust 的三种循环

Rust 提供：

```
loop
```

表示无限循环。

```
while
```

表示条件循环。

```
for
```

表示遍历循环。

它们适合不同场景。

| 循环 | 适用场景 |
| --- | --- |
| `loop` | 不确定循环次数，需要主动退出 |
| `while` | 条件成立时持续执行 |
| `for` | 遍历数组、集合或数字范围 |

---

## loop 无限循环

`loop` 会无限重复执行代码。

基本语法：

```
loop {
    // 重复执行的代码
}
```

例如：

```
fn main() {
    loop {
        println!("正在运行");
    }
}
```

这段程序会不断输出：

```
正在运行
正在运行
正在运行
...
```

除非手动终止程序，否则不会停止。

在终端中一般可以按：

```
Ctrl + C
```

停止运行。

---

## 使用 break 退出 loop

无限循环通常需要配合：

```
break
```

退出。

例如：

```
fn main() {
    let mut count = 1;

    loop {
        println!("{}", count);

        if count >= 5 {
            break;
        }

        count += 1;
    }
}
```

输出：

```
1
2
3
4
5
```

当：

```
count >= 5
```

成立时，执行：

```
break;
```

循环立即结束。

---

## break 会结束当前循环

例如：

```
fn main() {
    let mut number = 0;

    loop {
        number += 1;

        if number == 3 {
            break;
        }

        println!("{}", number);
    }

    println!("循环结束");
}
```

输出：

```
1
2
循环结束
```

当 `number` 等于 3 时， `break` 直接结束循环，因此不会输出 3。

---

## loop 可以返回值

Rust 中的 `loop` 是表达式，可以通过 `break` 返回一个值。

例如：

```
fn main() {
    let mut count = 0;

    let result = loop {
        count += 1;

        if count == 5 {
            break count * 10;
        }
    };

    println!("结果：{}", result);
}
```

输出：

```
结果：50
```

这里：

```
break count * 10;
```

不仅退出循环，还把：

```
count * 10
```

作为整个 `loop` 表达式的结果。

---

## loop 返回值的类型必须一致

例如：

```
fn main() {
    let result = loop {
        break 100;
    };

    println!("{}", result);
}
```

这里 `result` 的类型是 `i32` 。

如果循环中有多个 `break` ，它们返回的类型必须一致。

错误示例：

```
fn main() {
    let enabled = true;

    let result = loop {
        if enabled {
            break 100;
        } else {
            break "error";
        }
    };

    println!("{:?}", result);
}
```

一个分支返回整数，一个分支返回字符串，Rust 无法确定统一类型。

---

## continue 跳过当前循环

`continue` 不会结束整个循环。

它只会跳过本次循环剩余代码，直接进入下一次循环。

例如：

```
fn main() {
    let mut number = 0;

    loop {
        number += 1;

        if number == 3 {
            continue;
        }

        println!("{}", number);

        if number >= 5 {
            break;
        }
    }
}
```

输出：

```
1
2
4
5
```

当 `number` 等于 3 时，执行：

```
continue;
```

所以：

```
println!("{}", number);
```

不会执行。

---

## 使用 loop 模拟重试

`loop` 非常适合实现重试逻辑。

例如：

```
fn main() {
    let mut retry_count = 0;

    loop {
        retry_count += 1;

        println!("第 {} 次尝试连接服务器", retry_count);

        let connected = retry_count == 3;

        if connected {
            println!("连接成功");
            break;
        }

        if retry_count >= 5 {
            println!("超过最大重试次数");
            break;
        }

        println!("连接失败，准备重试");
    }
}
```

输出：

```
第 1 次尝试连接服务器
连接失败，准备重试
第 2 次尝试连接服务器
连接失败，准备重试
第 3 次尝试连接服务器
连接成功
```

---

## while 条件循环

`while` 会在条件为 `true` 时持续执行。

基本语法：

```
while 条件 {
    // 循环代码
}
```

例如：

```
fn main() {
    let mut number = 1;

    while number <= 5 {
        println!("{}", number);

        number += 1;
    }
}
```

输出：

```
1
2
3
4
5
```

执行过程是：

1. 1\. 判断 `number <= 5`
2. 2\. 条件成立，执行循环体
3. 3\. 修改 `number`
4. 4\. 再次判断条件
5. 5\. 条件不成立时退出

---

## while 条件必须是 bool

和 `if` 一样， `while` 后面的条件必须是布尔值。

错误示例：

```
fn main() {
    let number = 1;

    while number {
        println!("执行");
    }
}
```

Rust 不会自动把整数转换成布尔值。

正确写法：

```
fn main() {
    let mut number = 1;

    while number != 0 {
        println!("{}", number);

        number -= 1;
    }
}
```

---

## 使用 while 倒计时

```
fn main() {
    let mut count = 5;

    while count > 0 {
        println!("{}", count);

        count -= 1;
    }

    println!("开始！");
}
```

输出：

```
5
4
3
2
1
开始！
```

---

## while 适合什么场景？

`while` 适合：

- • 条件未知何时结束
- • 读取数据直到为空
- • 重试直到成功
- • 倒计时
- • 等待某个状态变化
- • 按索引处理数据

例如：

```
fn main() {
    let numbers = [10, 20, 30, 40];
    let mut index = 0;

    while index < numbers.len() {
        println!("{}", numbers[index]);

        index += 1;
    }
}
```

输出：

```
10
20
30
40
```

不过，遍历数组时通常更推荐使用 `for` 。

---

## for 遍历循环

`for` 是 Rust 中最常用的循环。

基本语法：

```
for 变量 in 可迭代对象 {
    // 循环代码
}
```

例如：

```
fn main() {
    let numbers = [10, 20, 30, 40];

    for number in numbers {
        println!("{}", number);
    }
}
```

输出：

```
10
20
30
40
```

每次循环时，数组中的一个元素会被赋值给：

```
number
```

---

## 为什么遍历数组推荐 for？

虽然可以使用 `while` 和索引：

```
fn main() {
    let numbers = [10, 20, 30];
    let mut index = 0;

    while index < numbers.len() {
        println!("{}", numbers[index]);

        index += 1;
    }
}
```

但推荐：

```
fn main() {
    let numbers = [10, 20, 30];

    for number in numbers {
        println!("{}", number);
    }
}
```

原因是：

- • 写法更简洁
- • 不需要手动管理索引
- • 不容易数组越界
- • 代码更符合 Rust 风格

---

## 数字范围

Rust 可以使用范围生成连续数字。

例如：

```
1..5
```

表示：

```
1、2、3、4
```

不包含 5。

示例：

```
fn main() {
    for number in 1..5 {
        println!("{}", number);
    }
}
```

输出：

```
1
2
3
4
```

---

## 包含结束值的范围

使用：

```
1..=5
```

表示包含 5。

例如：

```
fn main() {
    for number in 1..=5 {
        println!("{}", number);
    }
}
```

输出：

```
1
2
3
4
5
```

两种范围的区别：

| 写法 | 结果 |
| --- | --- |
| `1..5` | 1、2、3、4 |
| `1..=5` | 1、2、3、4、5 |

---

## 倒序遍历

可以使用：

```
rev()
```

反转范围。

例如：

```
fn main() {
    for number in (1..=5).rev() {
        println!("{}", number);
    }

    println!("开始！");
}
```

输出：

```
5
4
3
2
1
开始！
```

需要给范围加括号：

```
(1..=5).rev()
```

---

## 使用 step\_by 设置步长

可以使用：

```
step_by()
```

跳跃遍历。

例如：

```
fn main() {
    for number in (0..=10).step_by(2) {
        println!("{}", number);
    }
}
```

输出：

```
0
2
4
6
8
10
```

适合处理：

- • 偶数
- • 分页
- • 固定间隔的数据
- • 分块任务

---

## for 遍历字符串字符

可以使用：

```
chars()
```

遍历字符串中的字符。

例如：

```
fn main() {
    let text = "Rust编程";

    for ch in text.chars() {
        println!("{}", ch);
    }
}
```

输出：

```
R
u
s
t
编
程
```

Rust 字符串不能直接通过整数索引访问，但可以使用 `chars()` 遍历 Unicode 字符。

---

## for 遍历字节

如果需要查看字符串的 UTF-8 字节，可以使用：

```
bytes()
```

例如：

```
fn main() {
    let text = "Rust";

    for byte in text.bytes() {
        println!("{}", byte);
    }
}
```

输出：

```
82
117
115
116
```

---

## 使用 enumerate 获取索引

遍历数据时，如果还需要索引，可以使用：

```
enumerate()
```

例如：

```
fn main() {
    let fruits = ["苹果", "香蕉", "橙子"];

    for (index, fruit) in fruits.iter().enumerate() {
        println!("{}：{}", index, fruit);
    }
}
```

输出：

```
0：苹果
1：香蕉
2：橙子
```

如果希望编号从 1 开始：

```
fn main() {
    let fruits = ["苹果", "香蕉", "橙子"];

    for (index, fruit) in fruits.iter().enumerate() {
        println!("{}：{}", index + 1, fruit);
    }
}
```

---

## iter、iter\_mut 与 into\_iter

遍历集合时，经常会看到：

```
iter()
```
```
iter_mut()
```
```
into_iter()
```

它们的区别与所有权有关。

## iter

只读借用元素：

```
fn main() {
    let numbers = vec![10, 20, 30];

    for number in numbers.iter() {
        println!("{}", number);
    }

    println!("{:?}", numbers);
}
```

循环结束后， `numbers` 仍然可以使用。

---

## iter\_mut

可变借用元素：

```
fn main() {
    let mut numbers = vec![10, 20, 30];

    for number in numbers.iter_mut() {
        *number += 1;
    }

    println!("{:?}", numbers);
}
```

输出：

```
[11, 21, 31]
```

这里：

```
*number += 1;
```

修改了集合中的原始元素。

---

## into\_iter

获取集合元素的所有权：

```
fn main() {
    let names = vec![
        String::from("Tom"),
        String::from("Alice"),
    ];

    for name in names.into_iter() {
        println!("{}", name);
    }
}
```

对于不能复制的类型，遍历结束后原集合通常不能继续使用。

这部分与所有权关系密切，后续会详细讲解。

---

## for 中使用 break

`for` 循环也可以使用 `break` 。

例如，查找第一个大于 50 的数字：

```
fn main() {
    let numbers = [10, 30, 60, 80];

    for number in numbers {
        if number > 50 {
            println!("找到：{}", number);
            break;
        }
    }
}
```

输出：

```
找到：60
```

找到目标后，循环立即结束。

---

## for 中使用 continue

例如，跳过偶数，只输出奇数：

```
fn main() {
    for number in 1..=10 {
        if number % 2 == 0 {
            continue;
        }

        println!("{}", number);
    }
}
```

输出：

```
1
3
5
7
9
```

---

## 循环嵌套

一个循环中可以包含另一个循环。

例如：

```
fn main() {
    for row in 1..=3 {
        for column in 1..=3 {
            println!("行：{}，列：{}", row, column);
        }
    }
}
```

输出：

```
行：1，列：1
行：1，列：2
行：1，列：3
行：2，列：1
...
```

这种写法称为嵌套循环。

常用于：

- • 二维数组
- • 表格
- • 矩阵
- • 九九乘法表
- • 多层数据处理

---

## 循环标签

在嵌套循环中，普通 `break` 只会退出当前最内层循环。

例如：

```
fn main() {
    for row in 1..=3 {
        for column in 1..=3 {
            if row == 2 && column == 2 {
                break;
            }

            println!("{} {}", row, column);
        }
    }
}
```

当条件成立时，只退出内层循环，外层循环仍然继续。

如果希望退出指定循环，可以使用循环标签。

语法：

```
'标签名: loop {
}
```

例如：

```
fn main() {
    'outer: for row in 1..=3 {
        for column in 1..=3 {
            if row == 2 && column == 2 {
                break 'outer;
            }

            println!("行：{}，列：{}", row, column);
        }
    }

    println!("全部循环结束");
}
```

输出：

```
行：1，列：1
行：1，列：2
行：1，列：3
行：2，列：1
全部循环结束
```

标签名称前面要带：

```
'
```

例如：

```
'outer
```

---

## 带标签的 continue

`continue` 也可以指定循环标签。

例如：

```
fn main() {
    'outer: for row in 1..=3 {
        for column in 1..=3 {
            if column == 2 {
                continue 'outer;
            }

            println!("行：{}，列：{}", row, column);
        }
    }
}
```

当 `column == 2` 时，会直接进入外层循环的下一次迭代。

输出：

```
行：1，列：1
行：2，列：1
行：3，列：1
```

---

## 实战：计算 1 到 100 的和

```
fn main() {
    let mut total = 0;

    for number in 1..=100 {
        total += number;
    }

    println!("结果：{}", total);
}
```

输出：

```
结果：5050
```

---

## 实战：统计偶数数量

```
fn main() {
    let numbers = [12, 7, 18, 21, 30, 5];
    let mut count = 0;

    for number in numbers {
        if number % 2 == 0 {
            count += 1;
        }
    }

    println!("偶数数量：{}", count);
}
```

输出：

```
偶数数量：3
```

---

## 实战：查找最大值

```
fn main() {
    let numbers = [12, 45, 7, 88, 34];
    let mut max = numbers[0];

    for number in numbers {
        if number > max {
            max = number;
        }
    }

    println!("最大值：{}", max);
}
```

输出：

```
最大值：88
```

---

## 实战：九九乘法表

```
fn main() {
    for row in 1..=9 {
        for column in 1..=row {
            print!(
                "{}×{}={}\t",
                column,
                row,
                column * row
            );
        }

        println!();
    }
}
```

输出类似：

```
1×1=1
1×2=2  2×2=4
1×3=3  2×3=6  3×3=9
...
```

这里使用：

```
print!
```

表示输出后不自动换行。

每完成一行后，再使用：

```
println!();
```

换行。

---

## 实战：模拟分页处理

假设有 23 条数据，每页处理 5 条。

```
fn main() {
    let total_items = 23;
    let page_size = 5;
    let mut start = 0;

    while start < total_items {
        let end = (start + page_size).min(total_items);

        println!(
            "处理第 {} 到 {} 条数据",
            start + 1,
            end
        );

        start += page_size;
    }
}
```

输出：

```
处理第 1 到 5 条数据
处理第 6 到 10 条数据
处理第 11 到 15 条数据
处理第 16 到 20 条数据
处理第 21 到 23 条数据
```

这种逻辑常用于：

- • 批量读取数据库
- • 分页调用 API
- • 批量处理文件
- • 分批发送消息

---

## 实战：密码输入次数限制

```
fn main() {
    let correct_password = "rust123";
    let inputs = ["123456", "admin", "rust123"];
    let mut attempts = 0;

    for input in inputs {
        attempts += 1;

        println!("第 {} 次尝试", attempts);

        if input == correct_password {
            println!("密码正确");
            break;
        }

        println!("密码错误");

        if attempts >= 3 {
            println!("尝试次数过多");
        }
    }
}
```

输出：

```
第 1 次尝试
密码错误
第 2 次尝试
密码错误
第 3 次尝试
密码正确
```

---

## loop、while、for 如何选择？

## 使用 loop

当循环次数不确定，并且需要在内部主动退出时：

```
loop {
    if condition {
        break;
    }
}
```

常见场景：

- • 服务器监听
- • 消息消费
- • 不断读取用户输入
- • 自动重试
- • 游戏主循环

---

## 使用 while

当循环依赖明确条件时：

```
while condition {
}
```

常见场景：

- • 倒计时
- • 条件重试
- • 按索引遍历
- • 数据不为空时持续处理

---

## 使用 for

当遍历范围或集合时：

```
for item in items {
}
```

常见场景：

- • 遍历数组
- • 遍历 Vec
- • 遍历字符串字符
- • 数字范围
- • 文件列表
- • 数据库查询结果

一般来说：

> 能使用 `for` 时，优先使用 `for` 。

---

## 常见错误

## 忘记修改 while 条件变量

错误：

```
fn main() {
    let mut number = 1;

    while number <= 5 {
        println!("{}", number);
    }
}
```

`number` 永远不会发生变化，因此会形成无限循环。

正确：

```
fn main() {
    let mut number = 1;

    while number <= 5 {
        println!("{}", number);

        number += 1;
    }
}
```

---

## 范围结束值理解错误

```
for number in 1..5 {
    println!("{}", number);
}
```

不会输出 5。

需要包含 5 时使用：

```
1..=5
```

---

## continue 导致更新代码无法执行

错误示例：

```
fn main() {
    let mut number = 0;

    while number < 5 {
        if number == 2 {
            continue;
        }

        number += 1;
    }
}
```

当 `number == 2` 时，会不断执行 `continue` ，而无法执行：

```
number += 1;
```

最终形成无限循环。

正确写法：

```
fn main() {
    let mut number = 0;

    while number < 5 {
        number += 1;

        if number == 2 {
            continue;
        }

        println!("{}", number);
    }
}
```

---

## 数组索引越界

错误：

```
fn main() {
    let numbers = [10, 20, 30];
    let mut index = 0;

    while index <= numbers.len() {
        println!("{}", numbers[index]);

        index += 1;
    }
}
```

因为最后一次：

```
index == numbers.len()
```

已经越界。

正确：

```
while index < numbers.len()
```

或者直接使用：

```
for number in numbers
```

---

## 嵌套循环 break 退出错层级

普通：

```
break;
```

只退出最近一层循环。

如果需要退出外层循环，应使用标签：

```
break 'outer;
```

---

## 最佳实践

## 遍历集合优先使用 for

不推荐：

```
let mut index = 0;

while index < numbers.len() {
    println!("{}", numbers[index]);

    index += 1;
}
```

推荐：

```
for number in numbers {
    println!("{}", number);
}
```

---

## 循环条件要简单清晰

不推荐在 `while` 中写过于复杂的表达式。

可以先拆成变量：

```
let should_continue =
    connected &&
    retry_count < max_retries &&
    !cancelled;

while should_continue {
}
```

不过需要注意，如果条件依赖循环中的变量，应在每次循环时重新计算。

---

## 尽早使用 break

找到结果后及时退出循环，避免无意义计算。

例如：

```
for user in users {
    if user.id == target_id {
        println!("找到用户");
        break;
    }
}
```

---

## 谨慎使用无限循环

`loop` 很强大，但要确保存在明确退出条件，或者它本来就是长期运行任务。

例如服务器：

```
loop {
    // 接收并处理连接
}
```

这类无限循环是合理的。

---

## 避免在循环中重复做昂贵操作

例如：

```
for item in items {
    let config = load_config();
}
```

如果配置不需要每次重新加载，应移动到循环外：

```
let config = load_config();

for item in items {
    process(item, &config);
}
```

这样性能更好。

---

## 完整练习：商品订单统计

下面使用循环统计一组商品价格。

要求：

- • 计算总价
- • 统计大于等于 100 元的商品数量
- • 查找最高价格
- • 跳过价格小于等于 0 的无效数据
```
fn main() {
    let prices = [
        29.9,
        199.0,
        -1.0,
        88.0,
        399.0,
        0.0,
        59.9,
    ];

    let mut total = 0.0;
    let mut expensive_count = 0;
    let mut max_price = 0.0;

    for price in prices {
        if price <= 0.0 {
            continue;
        }

        total += price;

        if price >= 100.0 {
            expensive_count += 1;
        }

        if price > max_price {
            max_price = price;
        }
    }

    println!("有效商品总价：{:.2}", total);
    println!("高价商品数量：{}", expensive_count);
    println!("最高商品价格：{:.2}", max_price);
}
```

输出：

```
有效商品总价：775.80
高价商品数量：2
最高商品价格：399.00
```

这个案例综合使用了：

- • `for`
- • `if`
- • `continue`
- • 累加
- • 计数
- • 最大值查找

这些都是实际业务开发中非常常见的循环操作。

---

## 本章小结

循环是程序处理重复任务的核心工具。

通过本文，我们学习了：

- • `loop` 无限循环
- • 使用 `break` 退出循环
- • 使用 `continue` 跳过当前循环
- • `loop` 作为表达式返回值
- • `while` 条件循环
- • `for` 遍历数组和范围
- • `..` 与 `..=` 的区别
- • `rev()` 倒序遍历
- • `step_by()` 设置步长
- • `enumerate()` 获取索引
- • `iter()` 、 `iter_mut()` 和 `into_iter()`
- • 嵌套循环
- • 循环标签
- • 常见错误与最佳实践

选择循环时可以记住：

- • 不确定结束时间：使用 `loop`
- • 根据条件循环：使用 `while`
- • 遍历集合或范围：使用 `for`

在大多数日常开发场景中， `for` 是最安全、最清晰，也是最常用的选择。

---

## 下一篇预告

下一篇我们将学习 **Rust 的 match 模式匹配** ，包括：

- • `match` 基本语法
- • 匹配多个值
- • 范围匹配
- • 通配符 `_`
- • 绑定变量
- • `Option` 匹配
- • match 作为表达式返回值
- • 穷尽性检查
- • 实战：订单状态与用户权限处理

![](https://wst.wxapp.tc.qq.com/161/20304/snscosdownload/SH/reserved/68f82ad60007ef6e2cf9858cc13e0315000000a100004f50?imageView2/1/w/800/h/800/q/50)

Rust游戏开发实战 \[美\]赫伯·沃尔弗森 邮电出版社97871156

运费险

先用后付

7天无理由

¥99.8

![](https://res.wx.qq.com/shop/public/2024-10-17/fae7be51-beb6-4e61-aad8-4c1f7ccfab83.png)

蓝墨水图书店

![](https://res.wx.qq.com/t/components/icons/base/arrow_down_regular.svg) 收起

使用手机微信

扫码了解商品信息

Rust 编程实战 · Table of Contents