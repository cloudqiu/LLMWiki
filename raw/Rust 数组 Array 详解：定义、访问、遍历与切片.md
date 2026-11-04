---
title: "Rust 数组 Array 详解：定义、访问、遍历与切片"
source: "https://mp.weixin.qq.com/s?__biz=MzYzODE1NzUzMw==&mid=2247484459&idx=1&sn=5d58aace2c52ded990f5b3a74648b4d6&chksm=f0e75399c790da8f52a29f25515b6016e8072a6a41182581aeeeb8959e890c01019ad0b4244c&cur_album_id=4602071361631748097&scene=189#wechat_redirect"
author:
published:
created: 2026-11-04
description: "《Rust 编程实战》系列第 15 篇在前面的文章中，我们已经学习了条件判断、循环和模式匹配。"
tags:
  - "clippings"
---
程序员爱钓鱼 *Jul 20, 2026, 7:23 AM*

> 《Rust 编程实战》系列第 15 篇

在前面的文章中，我们已经学习了条件判断、循环和模式匹配。

从这一篇开始，我们将学习 Rust 中常用的数据集合类型。

首先介绍数组：

```
Array
```

数组可以在一个变量中保存多个数据，例如：

- • 一周 7 天的温度
- • 12 个月的销售额
- • RGB 三个颜色值
- • 固定数量的考试成绩
- • 固定长度的配置数据
- • 游戏地图中的固定坐标

Rust 数组有两个重要特点：

1. 1\. 数组中的所有元素必须是相同类型
2. 2\. 数组创建后长度不能改变

本文将详细介绍：

- • 数组的定义
- • 数组类型
- • 数组长度
- • 重复值初始化
- • 数组索引
- • 数组修改
- • 数组遍历
- • 安全访问
- • 数组切片
- • 多维数组
- • 数组函数参数
- • 数组与 `Vec` 的区别
- • 常见错误
- • 实战案例

---

## 什么是数组？

数组是一组按照顺序排列的相同类型数据。

例如：

```
fn main() {
    let numbers = [10, 20, 30, 40, 50];

    println!("{:?}", numbers);
}
```

输出：

```
[10, 20, 30, 40, 50]
```

这里：

```
numbers
```

是数组变量名。

数组中包含 5 个整数：

```
10、20、30、40、50
```

打印整个数组时，可以使用调试格式：

```
{:?}
```

---

## 数组的基本语法

数组的基本语法如下：

```
let 数组名 = [元素1, 元素2, 元素3];
```

例如：

```
fn main() {
    let fruits = ["苹果", "香蕉", "橙子"];

    println!("{:?}", fruits);
}
```

输出：

```
["苹果", "香蕉", "橙子"]
```

Rust 会自动推断数组的元素类型和长度。

---

## 数组元素类型必须相同

正确示例：

```
fn main() {
    let numbers = [10, 20, 30, 40];
}
```

所有元素都是整数。

错误示例：

```
fn main() {
    let values = [10, 20.5, true];
}
```

这里包含：

- • 整数
- • 浮点数
- • 布尔值

Rust 数组不允许保存不同类型的数据。

如果需要把不同类型的数据组合在一起，可以使用下一篇将要学习的元组：

```
Tuple
```

---

## 数组长度固定

数组一旦创建，长度就不能改变。

例如：

```
let numbers = [10, 20, 30];
```

这个数组长度固定为 3。

不能执行类似下面的操作：

```
numbers.push(40);
```

因为普通数组没有 `push()` 方法。

如果需要动态添加或删除数据，应使用：

```
Vec<T>
```

数组适合数据数量固定的场景。

---

## 显式声明数组类型

Rust 数组类型的写法是：

```
[元素类型; 数组长度]
```

例如：

```
fn main() {
    let numbers: [i32; 5] = [10, 20, 30, 40, 50];

    println!("{:?}", numbers);
}
```

这里：

```
[i32; 5]
```

表示：

- • 每个元素的类型是 `i32`
- • 数组一共有 5 个元素

注意，类型与长度之间使用分号：

```
;
```

---

## 数组长度是类型的一部分

下面两个数组的类型不同：

```
fn main() {
    let first: [i32; 3] = [1, 2, 3];
    let second: [i32; 4] = [1, 2, 3, 4];

    println!("{:?}", first);
    println!("{:?}", second);
}
```

它们的类型分别是：

```
[i32; 3]
```

和：

```
[i32; 4]
```

即使元素类型相同，只要长度不同，数组类型也不同。

---

## 数组长度必须与元素数量一致

错误示例：

```
fn main() {
    let numbers: [i32; 3] = [10, 20, 30, 40];
}
```

声明的长度是 3，但实际提供了 4 个元素，因此无法通过编译。

正确写法：

```
fn main() {
    let numbers: [i32; 4] = [10, 20, 30, 40];

    println!("{:?}", numbers);
}
```

---

## 使用重复值初始化数组

如果所有元素初始值相同，可以使用：

```
[初始值; 数量]
```

例如：

```
fn main() {
    let numbers = [0; 5];

    println!("{:?}", numbers);
}
```

输出：

```
[0, 0, 0, 0, 0]
```

这里：

```
[0; 5]
```

表示创建 5 个值为 0 的元素。

---

## 重复值初始化示例

创建 10 个布尔值：

```
fn main() {
    let flags = [false; 10];

    println!("{:?}", flags);
}
```

创建 4 个满分成绩：

```
fn main() {
    let scores = [100; 4];

    println!("{:?}", scores);
}
```

输出：

```
[100, 100, 100, 100]
```

这种写法常用于：

- • 初始化计数器
- • 创建固定缓冲区
- • 初始化状态数组
- • 创建棋盘或地图

---

## 访问数组元素

数组通过索引访问元素。

语法：

```
数组名[索引]
```

例如：

```
fn main() {
    let fruits = ["苹果", "香蕉", "橙子"];

    println!("{}", fruits[0]);
    println!("{}", fruits[1]);
    println!("{}", fruits[2]);
}
```

输出：

```
苹果
香蕉
橙子
```

---

## 数组索引从 0 开始

Rust 数组的第一个元素索引是：

```
0
```

例如：

```
let numbers = [10, 20, 30, 40];
```

元素和索引的对应关系是：

| 索引 | 元素 |
| --- | --- |
| `0` | `10` |
| `1` | `20` |
| `2` | `30` |
| `3` | `40` |

数组最后一个有效索引是：

```
数组长度 - 1
```

---

## 获取数组长度

使用：

```
len()
```

可以获得数组长度。

例如：

```
fn main() {
    let numbers = [10, 20, 30, 40, 50];

    println!("数组长度：{}", numbers.len());
}
```

输出：

```
数组长度：5
```

---

## 访问第一个和最后一个元素

直接通过索引访问：

```
fn main() {
    let numbers = [10, 20, 30, 40];

    let first = numbers[0];
    let last = numbers[numbers.len() - 1];

    println!("第一个元素：{}", first);
    println!("最后一个元素：{}", last);
}
```

输出：

```
第一个元素：10
最后一个元素：40
```

---

## 使用 first() 获取第一个元素

数组提供：

```
first()
```

方法。

它返回：

```
Option<&T>
```

示例：

```
fn main() {
    let numbers = [10, 20, 30];

    if let Some(first) = numbers.first() {
        println!("第一个元素：{}", first);
    }
}
```

输出：

```
第一个元素：10
```

这种方式比直接使用索引更加安全。

---

## 使用 last() 获取最后一个元素

```
fn main() {
    let numbers = [10, 20, 30];

    if let Some(last) = numbers.last() {
        println!("最后一个元素：{}", last);
    }
}
```

输出：

```
最后一个元素：30
```

---

## 数组索引越界

如果访问不存在的索引，程序会发生 panic。

例如：

```
fn main() {
    let numbers = [10, 20, 30];

    println!("{}", numbers[5]);
}
```

数组只有三个元素，有效索引是：

```
0、1、2
```

访问索引 5 会导致数组越界。

错误信息通常包含：

```
index out of bounds
```

---

## 使用 get() 安全访问数组

如果索引来自用户输入、配置文件或外部数据，推荐使用：

```
get()
```

例如：

```
fn main() {
    let numbers = [10, 20, 30];
    let index = 5;

    match numbers.get(index) {
        Some(value) => {
            println!("找到元素：{}", value);
        }
        None => {
            println!("索引 {} 超出数组范围", index);
        }
    }
}
```

输出：

```
索引 5 超出数组范围
```

`get()` 返回：

```
Option<&T>
```

索引有效时返回：

```
Some(&value)
```

索引无效时返回：

```
None
```

---

## 索引访问与 get() 的区别

直接索引：

```
numbers[index]
```

特点：

- • 写法简单
- • 返回具体元素
- • 越界时程序 panic

安全访问：

```
numbers.get(index)
```

特点：

- • 返回 `Option`
- • 越界时不会直接崩溃
- • 适合处理不确定索引

在实际项目中，外部传入的索引通常应该使用 `get()` 。

---

## 修改数组元素

数组默认不可变。

错误示例：

```
fn main() {
    let numbers = [10, 20, 30];

    numbers[0] = 100;
}
```

如果需要修改数组，必须使用：

```
mut
```

正确写法：

```
fn main() {
    let mut numbers = [10, 20, 30];

    numbers[0] = 100;

    println!("{:?}", numbers);
}
```

输出：

```
[100, 20, 30]
```

---

## 批量修改数组元素

```
fn main() {
    let mut scores = [60, 70, 80];

    scores[0] += 10;
    scores[1] += 10;
    scores[2] += 10;

    println!("{:?}", scores);
}
```

输出：

```
[70, 80, 90]
```

---

## 使用 for 遍历数组

`for` 是遍历数组最常用的方式。

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

每次循环都会把一个数组元素赋值给：

```
number
```

---

## 使用引用遍历数组

也可以借用整个数组：

```
fn main() {
    let numbers = [10, 20, 30, 40];

    for number in &numbers {
        println!("{}", number);
    }

    println!("原数组：{:?}", numbers);
}
```

这里：

```
&numbers
```

表示借用数组。

后续学习所有权和借用时，会详细解释这种写法。

---

## 使用 iter() 遍历

```
fn main() {
    let numbers = [10, 20, 30];

    for number in numbers.iter() {
        println!("{}", number);
    }
}
```

`iter()` 会产生一个只读迭代器。

循环变量 `number` 是元素引用。

---

## 使用 enumerate() 获取索引

如果遍历时还需要元素索引，可以使用：

```
enumerate()
```

示例：

```
fn main() {
    let fruits = ["苹果", "香蕉", "橙子"];

    for (index, fruit) in fruits.iter().enumerate() {
        println!("索引 {}：{}", index, fruit);
    }
}
```

输出：

```
索引 0：苹果
索引 1：香蕉
索引 2：橙子
```

如果希望序号从 1 开始：

```
fn main() {
    let fruits = ["苹果", "香蕉", "橙子"];

    for (index, fruit) in fruits.iter().enumerate() {
        println!("第 {} 个水果：{}", index + 1, fruit);
    }
}
```

---

## 使用 while 遍历数组

数组也可以通过索引和 `while` 遍历。

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

不过，如果只需要顺序读取所有元素，通常更推荐 `for` 。

原因是：

- • 写法更简洁
- • 不需要维护索引
- • 不容易越界
- • 更符合 Rust 风格

---

## 使用 iter\_mut() 修改所有元素

如果希望遍历并修改数组中的元素，可以使用：

```
iter_mut()
```

示例：

```
fn main() {
    let mut numbers = [10, 20, 30];

    for number in numbers.iter_mut() {
        *number += 5;
    }

    println!("{:?}", numbers);
}
```

输出：

```
[15, 25, 35]
```

这里的 `number` 是可变引用。

所以修改原始元素时，需要使用：

```
*number
```

进行解引用。

---

## 使用 fill() 填充数组

可以使用：

```
fill()
```

把数组中的所有元素修改为同一个值。

```
fn main() {
    let mut numbers = [1, 2, 3, 4];

    numbers.fill(0);

    println!("{:?}", numbers);
}
```

输出：

```
[0, 0, 0, 0]
```

适合：

- • 重置数组
- • 清空状态
- • 初始化缓冲区
- • 重置游戏地图数据

---

## 判断数组是否包含某个元素

可以使用：

```
contains()
```

例如：

```
fn main() {
    let numbers = [10, 20, 30, 40];

    println!("{}", numbers.contains(&20));
    println!("{}", numbers.contains(&99));
}
```

输出：

```
true
false
```

注意需要传入元素的引用：

```
&20
```

---

## 数组切片 Slice

切片表示数组中的一部分数据。

切片通常以引用形式出现：

```
&[T]
```

例如：

```
fn main() {
    let numbers = [10, 20, 30, 40, 50];

    let slice = &numbers[1..4];

    println!("{:?}", slice);
}
```

输出：

```
[20, 30, 40]
```

范围：

```
1..4
```

包含索引：

```
1、2、3
```

不包含索引 4。

---

## 常见切片范围

假设数组如下：

```
let numbers = [10, 20, 30, 40, 50];
```

获取索引 1 到 3：

```
let slice = &numbers[1..4];
```

结果：

```
[20, 30, 40]
```

从开头到索引 2：

```
let slice = &numbers[..3];
```

结果：

```
[10, 20, 30]
```

从索引 2 到结尾：

```
let slice = &numbers[2..];
```

结果：

```
[30, 40, 50]
```

获取整个数组：

```
let slice = &numbers[..];
```

使用包含结束位置的范围：

```
let slice = &numbers[1..=3];
```

结果也是：

```
[20, 30, 40]
```

---

## 切片不会复制数组

切片只是引用原数组中的一段连续数据。

```
fn main() {
    let numbers = [10, 20, 30, 40];

    let slice = &numbers[1..3];

    println!("原数组：{:?}", numbers);
    println!("切片：{:?}", slice);
}
```

输出：

```
原数组：[10, 20, 30, 40]
切片：[20, 30]
```

切片通常只保存：

- • 数据开始位置
- • 数据长度

因此创建切片的成本很低。

---

## 切片也可能越界

错误示例：

```
fn main() {
    let numbers = [10, 20, 30];

    let slice = &numbers[1..10];

    println!("{:?}", slice);
}
```

数组长度只有 3，结束索引却是 10，因此程序会 panic。

如果切片范围来自外部输入，应先进行范围校验，或者使用：

```
get()
```

例如：

```
fn main() {
    let numbers = [10, 20, 30, 40];
    let range = 1..3;

    match numbers.get(range) {
        Some(slice) => println!("{:?}", slice),
        None => println!("切片范围无效"),
    }
}
```

---

## 数组作为函数参数

可以把固定长度数组直接作为参数。

```
fn print_numbers(numbers: [i32; 3]) {
    println!("{:?}", numbers);
}

fn main() {
    let numbers = [10, 20, 30];

    print_numbers(numbers);
}
```

参数类型：

```
[i32; 3]
```

表示函数只能接收长度为 3 的整数数组。

下面的数组不能传入：

```
let numbers = [10, 20, 30, 40];
```

因为它的类型是：

```
[i32; 4]
```

---

## 使用切片作为函数参数

实际项目中，更推荐使用切片参数：

```
fn print_numbers(numbers: &[i32]) {
    for number in numbers {
        println!("{}", number);
    }
}

fn main() {
    let first = [10, 20, 30];
    let second = [1, 2, 3, 4, 5];

    print_numbers(&first);
    print_numbers(&second);
}
```

参数：

```
&[i32]
```

可以接收任意长度的整数数组切片。

这样函数更加通用。

---

## 计算数组总和

```
fn calculate_total(numbers: &[i32]) -> i32 {
    let mut total = 0;

    for number in numbers {
        total += number;
    }

    total
}

fn main() {
    let numbers = [10, 20, 30, 40];

    let total = calculate_total(&numbers);

    println!("数组总和：{}", total);
}
```

输出：

```
数组总和：100
```

---

## 计算数组平均值

```
fn calculate_average(numbers: &[f64]) -> Option<f64> {
    if numbers.is_empty() {
        return None;
    }

    let mut total = 0.0;

    for number in numbers {
        total += number;
    }

    Some(total / numbers.len() as f64)
}

fn main() {
    let scores = [80.0, 90.0, 75.0, 95.0];

    match calculate_average(&scores) {
        Some(average) => {
            println!("平均分：{:.2}", average);
        }
        None => {
            println!("数组为空，无法计算平均分");
        }
    }
}
```

输出：

```
平均分：85.00
```

---

## 查找数组最大值

```
fn find_max(numbers: &[i32]) -> Option<i32> {
    if numbers.is_empty() {
        return None;
    }

    let mut max = numbers[0];

    for &number in numbers {
        if number > max {
            max = number;
        }
    }

    Some(max)
}

fn main() {
    let numbers = [12, 45, 8, 99, 31];

    match find_max(&numbers) {
        Some(max) => println!("最大值：{}", max),
        None => println!("数组为空"),
    }
}
```

输出：

```
最大值：99
```

这里：

```
for &number in numbers
```

表示直接从引用中取出整数值。

因为 `i32` 实现了 `Copy` ，所以可以直接复制。

---

## 查找数组最小值

```
fn find_min(numbers: &[i32]) -> Option<i32> {
    let mut iterator = numbers.iter();

    let first = iterator.next()?;
    let mut min = *first;

    for &number in iterator {
        if number < min {
            min = number;
        }
    }

    Some(min)
}

fn main() {
    let numbers = [12, 45, 8, 99, 31];

    if let Some(min) = find_min(&numbers) {
        println!("最小值：{}", min);
    }
}
```

输出：

```
最小值：8
```

---

## 空数组

Rust 允许创建长度为 0 的数组。

```
fn main() {
    let numbers: [i32; 0] = [];

    println!("{:?}", numbers);
    println!("长度：{}", numbers.len());
    println!("是否为空：{}", numbers.is_empty());
}
```

输出：

```
[]
长度：0
是否为空：true
```

数组是否为空可以通过：

```
is_empty()
```

判断。

---

## 多维数组

数组的元素也可以是另一个数组。

例如二维数组：

```
fn main() {
    let matrix = [
        [1, 2, 3],
        [4, 5, 6],
        [7, 8, 9],
    ];

    println!("{:?}", matrix);
}
```

它的类型是：

```
[[i32; 3]; 3]
```

表示：

- • 外层有 3 个元素
- • 每个元素都是长度为 3 的整数数组

---

## 访问二维数组元素

```
fn main() {
    let matrix = [
        [1, 2, 3],
        [4, 5, 6],
        [7, 8, 9],
    ];

    println!("{}", matrix[0][0]);
    println!("{}", matrix[1][2]);
}
```

输出：

```
1
6
```

其中：

```
matrix[1][2]
```

表示：

- • 获取索引为 1 的行
- • 再获取这一行中索引为 2 的元素

也就是第二行第三列。

---

## 遍历二维数组

```
fn main() {
    let matrix = [
        [1, 2, 3],
        [4, 5, 6],
        [7, 8, 9],
    ];

    for row in matrix {
        for value in row {
            print!("{}\t", value);
        }

        println!();
    }
}
```

输出：

```
1    2    3
4    5    6
7    8    9
```

多维数组常用于：

- • 表格
- • 矩阵
- • 棋盘
- • 地图
- • 图像像素
- • 游戏关卡
- • 固定网格数据

---

## 字符串切片数组

数组可以保存多个字符串切片：

```
fn main() {
    let names = ["Tom", "Alice", "Jack"];

    for name in names {
        println!("{}", name);
    }
}
```

数组类型可以表示为：

```
[&str; 3]
```

---

## String 数组

数组也可以保存拥有所有权的 `String` ：

```
fn main() {
    let names = [
        String::from("Tom"),
        String::from("Alice"),
        String::from("Jack"),
    ];

    println!("{:?}", names);
}
```

遍历 `String` 数组时，可以使用引用，避免移动所有权：

```
fn main() {
    let names = [
        String::from("Tom"),
        String::from("Alice"),
    ];

    for name in &names {
        println!("{}", name);
    }

    println!("原数组：{:?}", names);
}
```

后续学习所有权时，会详细分析这里的区别。

---

## 使用 array::from\_fn 创建数组

如果每个元素需要根据索引计算，可以使用：

```
std::array::from_fn
```

例如：

```
fn main() {
    let numbers: [usize; 5] =
        std::array::from_fn(|index| index * 10);

    println!("{:?}", numbers);
}
```

输出：

```
[0, 10, 20, 30, 40]
```

这里闭包会依次接收到索引：

```
0、1、2、3、4
```

然后根据索引生成元素。

---

## 数组解构

数组也可以通过模式匹配进行解构。

```
fn main() {
    let numbers = [10, 20, 30];

    let [first, second, third] = numbers;

    println!("{}", first);
    println!("{}", second);
    println!("{}", third);
}
```

输出：

```
10
20
30
```

解构变量数量必须与数组长度一致。

---

## 在 match 中匹配数组

```
fn main() {
    let numbers = [10, 20, 30];

    match numbers {
        [10, second, third] => {
            println!("第一个元素是 10");
            println!("第二个元素：{}", second);
            println!("第三个元素：{}", third);
        }
        _ => {
            println!("不匹配");
        }
    }
}
```

数组模式匹配常用于固定格式数据。

---

## 数组与 Vec 的区别

数组：

```
let numbers = [1, 2, 3];
```

动态数组：

```
let numbers = vec![1, 2, 3];
```

主要区别如下：

| 特性 | Array | Vec |
| --- | --- | --- |
| 长度 | 固定 | 可动态变化 |
| 添加元素 | 不支持 | 支持 `push()` |
| 删除元素 | 不支持 | 支持 `pop()` 、 `remove()` |
| 类型是否包含长度 | 包含 | 不包含 |
| 数据存储 | 通常直接存储 | 元素通常存储在堆上 |
| 适用场景 | 固定数量数据 | 动态数量数据 |

适合使用数组的场景：

- • RGB 三个颜色值
- • 一周七天
- • 固定坐标
- • 固定长度缓冲区
- • 固定配置
- • 矩阵和棋盘

适合使用 `Vec` 的场景：

- • 用户列表
- • 商品列表
- • 文件列表
- • 数据库查询结果
- • 动态任务队列
- • 网络消息集合

---

## 实战：统计一周温度

假设记录一周七天的温度：

```
fn main() {
    let temperatures = [
        25.5,
        27.0,
        26.5,
        29.0,
        30.5,
        28.0,
        24.5,
    ];

    let mut total = 0.0;
    let mut highest = temperatures[0];
    let mut lowest = temperatures[0];

    for temperature in temperatures {
        total += temperature;

        if temperature > highest {
            highest = temperature;
        }

        if temperature < lowest {
            lowest = temperature;
        }
    }

    let average = total / temperatures.len() as f64;

    println!("平均温度：{:.2}℃", average);
    println!("最高温度：{:.2}℃", highest);
    println!("最低温度：{:.2}℃", lowest);
}
```

输出：

```
平均温度：27.29℃
最高温度：30.50℃
最低温度：24.50℃
```

---

## 实战：学生成绩统计

要求：

- • 计算总分
- • 计算平均分
- • 查找最高分
- • 查找最低分
- • 统计及格人数
```
fn main() {
    let scores = [86, 59, 92, 75, 48, 100];

    let mut total = 0;
    let mut highest = scores[0];
    let mut lowest = scores[0];
    let mut passed_count = 0;

    for score in scores {
        total += score;

        if score > highest {
            highest = score;
        }

        if score < lowest {
            lowest = score;
        }

        if score >= 60 {
            passed_count += 1;
        }
    }

    let average = total as f64 / scores.len() as f64;

    println!("总分：{}", total);
    println!("平均分：{:.2}", average);
    println!("最高分：{}", highest);
    println!("最低分：{}", lowest);
    println!("及格人数：{}", passed_count);
}
```

输出：

```
总分：460
平均分：76.67
最高分：100
最低分：48
及格人数：4
```

---

## 实战：商品价格处理

要求：

- • 跳过无效价格
- • 计算有效商品总价
- • 统计高价商品数量
- • 查找最高价格
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
    let mut valid_count = 0;
    let mut expensive_count = 0;
    let mut max_price = 0.0;

    for price in prices {
        if price <= 0.0 {
            continue;
        }

        total += price;
        valid_count += 1;

        if price >= 100.0 {
            expensive_count += 1;
        }

        if price > max_price {
            max_price = price;
        }
    }

    println!("有效商品数量：{}", valid_count);
    println!("有效商品总价：{:.2}", total);
    println!("高价商品数量：{}", expensive_count);
    println!("最高商品价格：{:.2}", max_price);
}
```

输出：

```
有效商品数量：5
有效商品总价：775.80
高价商品数量：2
最高商品价格：399.00
```

---

## 实战：简单井字棋棋盘

使用二维数组保存井字棋棋盘：

```
fn main() {
    let board = [
        ['X', 'O', 'X'],
        [' ', 'X', 'O'],
        ['O', ' ', 'X'],
    ];

    for row in board {
        for cell in row {
            print!(" {} ", cell);
        }

        println!();
    }
}
```

输出类似：

```
X  O  X
   X  O
O     X
```

二维数组非常适合保存固定大小的游戏棋盘。

---

## 常见错误

## 数组元素类型不一致

错误：

```
let values = [10, "Rust", true];
```

数组只能保存相同类型的元素。

需要组合不同类型时，可以使用元组。

---

## 声明长度与实际长度不一致

错误：

```
let numbers: [i32; 3] = [1, 2, 3, 4];
```

应修改为：

```
let numbers: [i32; 4] = [1, 2, 3, 4];
```

---

## 数组索引越界

错误：

```
let numbers = [10, 20, 30];

println!("{}", numbers[3]);
```

最后一个有效索引是 2。

索引不确定时，应使用：

```
numbers.get(index)
```

---

## 忘记使用 mut

错误：

```
let numbers = [1, 2, 3];

numbers[0] = 100;
```

正确：

```
let mut numbers = [1, 2, 3];

numbers[0] = 100;
```

---

## 把数组当作动态集合

错误思路：

```
let mut numbers = [1, 2, 3];

numbers.push(4);
```

数组长度固定，不支持 `push()` 。

需要动态长度时使用：

```
let mut numbers = vec![1, 2, 3];

numbers.push(4);
```

---

## while 遍历条件写错

错误：

```
while index <= numbers.len() {
    println!("{}", numbers[index]);
}
```

当：

```
index == numbers.len()
```

时已经越界。

正确条件：

```
while index < numbers.len()
```

---

## 切片范围越界

错误：

```
let slice = &numbers[1..100];
```

切片结束位置不能超过数组长度。

可以使用：

```
numbers.get(1..100)
```

安全检查。

---

## 最佳实践

## 固定数量数据使用数组

例如：

```
let rgb = [255, 128, 64];
```

RGB 永远只有三个值，适合使用数组。

---

## 动态数量数据使用 Vec

例如商品列表：

```
let mut products = Vec::new();

products.push("手机");
products.push("电脑");
```

商品数量可能变化，因此更适合 `Vec` 。

---

## 函数参数优先使用切片

不推荐把函数限制为固定长度：

```
fn calculate(numbers: [i32; 5]) {
}
```

更通用的写法：

```
fn calculate(numbers: &[i32]) {
}
```

这样可以接收不同长度的数据。

---

## 不确定索引使用 get()

如果索引来自用户输入，应使用：

```
if let Some(value) = numbers.get(index) {
    println!("{}", value);
}
```

避免程序因为越界而崩溃。

---

## 遍历数组优先使用 for

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

只有确实需要索引控制时，才使用 `while` 。

---

## 修改所有元素使用 iter\_mut()

```
for number in numbers.iter_mut() {
    *number *= 2;
}
```

相比手动编写多个索引，代码更加简洁。

---

## 完整练习：月度销售数据分析

假设保存一家公司 12 个月的销售额。

要求：

- • 计算全年销售额
- • 计算月平均销售额
- • 查找最高销售额
- • 查找最低销售额
- • 找出最高销售额所在月份
- • 统计超过平均值的月份数量
```
fn main() {
    let monthly_sales = [
        12000.0,
        13500.0,
        11800.0,
        14200.0,
        15600.0,
        14900.0,
        16200.0,
        17100.0,
        15800.0,
        18000.0,
        19500.0,
        22000.0,
    ];

    let mut total = 0.0;
    let mut highest = monthly_sales[0];
    let mut lowest = monthly_sales[0];
    let mut highest_month = 0;

    for (index, sales) in monthly_sales.iter().enumerate() {
        total += sales;

        if *sales > highest {
            highest = *sales;
            highest_month = index;
        }

        if *sales < lowest {
            lowest = *sales;
        }
    }

    let average = total / monthly_sales.len() as f64;
    let mut above_average_count = 0;

    for sales in monthly_sales {
        if sales > average {
            above_average_count += 1;
        }
    }

    println!("全年销售额：{:.2}", total);
    println!("月平均销售额：{:.2}", average);
    println!("最高月销售额：{:.2}", highest);
    println!("最低月销售额：{:.2}", lowest);
    println!("最高销售额月份：{} 月", highest_month + 1);
    println!(
        "超过平均销售额的月份数量：{}",
        above_average_count
    );
}
```

输出：

```
全年销售额：190600.00
月平均销售额：15883.33
最高月销售额：22000.00
最低月销售额：11800.00
最高销售额月份：12 月
超过平均销售额的月份数量：5
```

这个案例综合使用了：

- • 固定长度数组
- • `for` 遍历
- • `iter()`
- • `enumerate()`
- • 累加计算
- • 最大值和最小值
- • 数组长度
- • 类型转换
- • 条件统计

---

## 本章小结

数组是 Rust 中用于保存固定数量、相同类型数据的集合。

通过本文，我们学习了：

- • 数组的定义
- • 数组元素类型必须相同
- • 数组长度固定
- • 数组类型 `[T; N]`
- • 重复值初始化 `[value; N]`
- • 数组索引
- • `len()` 和 `is_empty()`
- • `first()` 和 `last()`
- • `get()` 安全访问
- • 可变数组
- • `for` 、 `iter()` 和 `iter_mut()`
- • `enumerate()` 获取索引
- • 数组切片
- • 多维数组
- • 数组作为函数参数
- • 使用切片编写通用函数
- • 数组解构和模式匹配
- • 数组与 `Vec` 的区别
- • 常见错误与最佳实践

可以记住：

> 数组适合保存数量固定、类型相同的数据。

如果数据数量需要动态变化，则应该使用：

```
Vec<T>
```

---

## 下一篇预告

下一篇我们将学习 **Rust 元组 Tuple 详解** ，包括：

- • 什么是元组
- • 元组的定义
- • 元组可以保存不同类型
- • 元组类型声明
- • 通过索引访问元组
- • 元组解构
- • 元组作为函数返回值
- • 返回多个结果
- • 单元类型 `()`
- • 嵌套元组
- • 元组与数组的区别
- • 实战：返回用户信息和计算结果

Rust 编程实战 · Table of Contents