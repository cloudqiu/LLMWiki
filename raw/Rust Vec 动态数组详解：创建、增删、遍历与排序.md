---
title: "Rust Vec 动态数组详解：创建、增删、遍历与排序"
source: "https://mp.weixin.qq.com/s?__biz=MzYzODE1NzUzMw==&mid=2247484482&idx=1&sn=ae6a33e13c5d5caf5d145e1bf5ace454&chksm=f0e753f0c790dae660d76f944291bce465f73912924a78ac1c6c2e68d7667184073b94481639&cur_album_id=4602071361631748097&scene=189#wechat_redirect"
author:
published:
created: 2026-11-04
description: "《Rust 编程实战》系列第 19 篇在上一篇文章中，我们学习了 String 与 \x26amp;str。"
tags:
  - "clippings"
---
程序员爱钓鱼 *Jul 24, 2026, 8:24 AM*

> 《Rust 编程实战》系列第 19 篇

在上一篇文章中，我们学习了 `String` 与 `&str` 。

这一篇继续学习 Rust 中最常用的集合类型之一：

```
Vec<T>
```

`Vec` 通常称为动态数组，也叫向量。

与普通数组不同， `Vec` 的长度可以在程序运行过程中变化。我们可以动态添加、删除和修改元素。

例如：

```
let mut numbers = vec![10, 20, 30];

numbers.push(40);
```

执行后， `numbers` 变成：

```
[10, 20, 30, 40]
```

本文将介绍：

- • 什么是 `Vec`
- • 创建动态数组
- • 添加和删除元素
- • 访问和修改元素
- • 遍历 `Vec`
- • `len()` 与 `capacity()`
- • 排序、查找和去重
- • `Vec<String>` 的所有权
- • `Vec` 、数组和切片的区别
- • 常见错误
- • 实战案例

---

## 什么是 Vec？

`Vec<T>` 是 Rust 标准库提供的可增长集合。

它具有以下特点：

- • 所有元素必须是相同类型
- • 元素按照插入顺序排列
- • 长度可以动态变化
- • 数据通常存储在堆上
- • 支持添加、删除、排序和查找

例如：

```
fn main() {
    let numbers = vec![10, 20, 30];

    println!("{:?}", numbers);
}
```

输出：

```
[10, 20, 30]
```

这里 `numbers` 的类型通常是：

```
Vec<i32>
```

---

## 使用 vec! 宏创建 Vec

最常用的创建方式是：

```
vec![]
```

例如：

```
fn main() {
    let fruits = vec!["苹果", "香蕉", "橙子"];

    println!("{:?}", fruits);
}
```

也可以显式声明类型：

```
fn main() {
    let scores: Vec<i32> = vec![80, 90, 100];

    println!("{:?}", scores);
}
```

Rust 通常可以根据元素自动推断类型。

---

## 创建空 Vec

可以使用：

```
Vec::new()
```

例如：

```
fn main() {
    let numbers: Vec<i32> = Vec::new();

    println!("{:?}", numbers);
}
```

创建空 `Vec` 时，通常必须指定元素类型，因为编译器无法从空集合推断。

也可以写成：

```
let numbers = Vec::<i32>::new();
```

---

## 使用 Vec::with\_capacity()

如果提前知道大概会保存多少元素，可以预先分配容量：

```
fn main() {
    let numbers: Vec<i32> =
        Vec::with_capacity(100);

    println!("长度：{}", numbers.len());
    println!("容量：{}", numbers.capacity());
}
```

输出类似：

```
长度：0
容量：100
```

这不会创建 100 个元素，只会提前准备容纳 100 个元素的空间。

---

## 使用重复值创建 Vec

可以使用：

```
vec![值; 数量]
```

例如：

```
fn main() {
    let numbers = vec![0; 5];

    println!("{:?}", numbers);
}
```

输出：

```
[0, 0, 0, 0, 0]
```

这种写法适合初始化状态、计数器或缓冲区。

---

## 使用 push() 添加元素

`Vec` 默认不可变。

如果需要添加元素，必须使用 `mut` ：

```
fn main() {
    let mut numbers = vec![10, 20];

    numbers.push(30);
    numbers.push(40);

    println!("{:?}", numbers);
}
```

输出：

```
[10, 20, 30, 40]
```

`push()` 会把元素添加到末尾。

新元素类型必须与原有元素类型一致。

---

## 使用 pop() 删除末尾元素

`pop()` 会删除并返回最后一个元素。

```
fn main() {
    let mut numbers = vec![10, 20, 30];

    let value = numbers.pop();

    println!("删除结果：{:?}", value);
    println!("剩余数据：{:?}", numbers);
}
```

输出：

```
删除结果：Some(30)
剩余数据：[10, 20]
```

`pop()` 返回：

```
Option<T>
```

因为空 `Vec` 没有元素可以删除。

```
if let Some(value) = numbers.pop() {
    println!("删除了：{}", value);
}
```

---

## 使用 insert() 插入元素

可以在指定索引位置插入元素：

```
fn main() {
    let mut numbers = vec![10, 30, 40];

    numbers.insert(1, 20);

    println!("{:?}", numbers);
}
```

输出：

```
[10, 20, 30, 40]
```

原来索引 `1` 及其后面的元素会向后移动。

如果插入位置超过长度，程序会 panic。

---

## 使用 remove() 删除指定元素

```
fn main() {
    let mut fruits =
        vec!["苹果", "香蕉", "橙子"];

    let removed = fruits.remove(1);

    println!("删除：{}", removed);
    println!("剩余：{:?}", fruits);
}
```

输出：

```
删除：香蕉
剩余：["苹果", "橙子"]
```

`remove()` 会移动后面的元素，因此频繁从开头或中间删除可能成本较高。

---

## 使用 swap\_remove() 快速删除

如果不关心元素顺序，可以使用：

```
swap_remove()
```
```
fn main() {
    let mut numbers = vec![10, 20, 30, 40];

    let removed = numbers.swap_remove(1);

    println!("删除：{}", removed);
    println!("剩余：{:?}", numbers);
}
```

输出可能是：

```
删除：20
剩余：[10, 40, 30]
```

它会把最后一个元素移动到删除位置，因此速度更快，但会改变顺序。

---

## 访问 Vec 元素

可以使用索引访问：

```
fn main() {
    let numbers = vec![10, 20, 30];

    println!("{}", numbers[0]);
    println!("{}", numbers[1]);
}
```

索引从 `0` 开始。

如果访问越界索引：

```
println!("{}", numbers[10]);
```

程序会 panic。

---

## 使用 get() 安全访问

当索引不确定时，推荐使用：

```
get()
```
```
fn main() {
    let numbers = vec![10, 20, 30];
    let index = 5;

    match numbers.get(index) {
        Some(value) => {
            println!("元素：{}", value);
        }
        None => {
            println!("索引超出范围");
        }
    }
}
```

`get()` 返回：

```
Option<&T>
```

因此不会因为越界直接崩溃。

---

## 获取第一个和最后一个元素

```
fn main() {
    let numbers = vec![10, 20, 30];

    println!("{:?}", numbers.first());
    println!("{:?}", numbers.last());
}
```

输出：

```
Some(10)
Some(30)
```

两者都返回 `Option<&T>` ，因为集合可能为空。

---

## 修改 Vec 元素

```
fn main() {
    let mut numbers = vec![10, 20, 30];

    numbers[1] = 200;

    println!("{:?}", numbers);
}
```

输出：

```
[10, 200, 30]
```

也可以使用：

```
get_mut()
```

安全获得可变引用：

```
fn main() {
    let mut numbers = vec![10, 20, 30];

    if let Some(value) = numbers.get_mut(1) {
        *value = 200;
    }

    println!("{:?}", numbers);
}
```

---

## 遍历 Vec

最常见的方式是使用 `for` ：

```
fn main() {
    let numbers = vec![10, 20, 30];

    for number in &numbers {
        println!("{}", number);
    }

    println!("{:?}", numbers);
}
```

使用：

```
&numbers
```

可以借用集合，遍历后原 `Vec` 仍然可以使用。

---

## 遍历并修改元素

使用可变引用：

```
fn main() {
    let mut numbers = vec![10, 20, 30];

    for number in &mut numbers {
        *number *= 2;
    }

    println!("{:?}", numbers);
}
```

输出：

```
[20, 40, 60]
```

循环变量是可变引用，因此需要使用：

```
*number
```

进行解引用。

---

## 获取索引和值

可以使用：

```
enumerate()
```
```
fn main() {
    let fruits =
        vec!["苹果", "香蕉", "橙子"];

    for (index, fruit) in
        fruits.iter().enumerate()
    {
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

---

## len() 与 is\_empty()

获取当前元素数量：

```
numbers.len()
```

判断是否为空：

```
numbers.is_empty()
```

示例：

```
fn main() {
    let numbers = vec![10, 20, 30];

    println!("长度：{}", numbers.len());
    println!("是否为空：{}", numbers.is_empty());
}
```

---

## 长度与容量的区别

`Vec` 有两个重要概念：

```
长度 len
容量 capacity
```

长度表示当前实际元素数量。

容量表示当前已分配空间最多可以容纳多少个元素，而不需要重新分配内存。

```
fn main() {
    let mut numbers = Vec::new();

    println!(
        "长度：{}，容量：{}",
        numbers.len(),
        numbers.capacity()
    );

    for number in 1..=10 {
        numbers.push(number);

        println!(
            "长度：{}，容量：{}",
            numbers.len(),
            numbers.capacity()
        );
    }
}
```

当长度超过容量时， `Vec` 会自动申请更大的内存空间。

具体扩容策略属于实现细节，不应该依赖固定倍数。

---

## 预留和释放容量

可以使用：

```
reserve()
```

提前增加容量：

```
numbers.reserve(100);
```

如果想尽量释放多余容量，可以使用：

```
shrink_to_fit()
```
```
fn main() {
    let mut numbers =
        Vec::with_capacity(100);

    numbers.push(10);
    numbers.push(20);

    numbers.shrink_to_fit();

    println!("{}", numbers.capacity());
}
```

不过频繁调整容量也有成本，通常不需要手动干预。

---

## 清空 Vec

使用：

```
clear()
```
```
fn main() {
    let mut numbers = vec![10, 20, 30];

    numbers.clear();

    println!("{:?}", numbers);
    println!("长度：{}", numbers.len());
}
```

`clear()` 会删除所有元素，但已分配容量通常会保留，以便以后继续使用。

---

## 判断是否包含元素

```
fn main() {
    let numbers = vec![10, 20, 30];

    println!("{}", numbers.contains(&20));
    println!("{}", numbers.contains(&99));
}
```

输出：

```
true
false
```

---

## 查找元素位置

可以结合迭代器和 `position()` ：

```
fn main() {
    let numbers = vec![10, 20, 30, 20];

    let position = numbers
        .iter()
        .position(|value| *value == 20);

    println!("{:?}", position);
}
```

输出：

```
Some(1)
```

只返回第一个匹配位置。

---

## 保留符合条件的元素

可以使用：

```
retain()
```
```
fn main() {
    let mut numbers =
        vec![1, 2, 3, 4, 5, 6];

    numbers.retain(|number| {
        number % 2 == 0
    });

    println!("{:?}", numbers);
}
```

输出：

```
[2, 4, 6]
```

`retain()` 会保留闭包返回 `true` 的元素。

---

## 排序 Vec

整数升序排序：

```
fn main() {
    let mut numbers = vec![30, 10, 50, 20];

    numbers.sort();

    println!("{:?}", numbers);
}
```

输出：

```
[10, 20, 30, 50]
```

降序排序：

```
numbers.sort_by(|a, b| b.cmp(a));
```

完整示例：

```
fn main() {
    let mut numbers = vec![30, 10, 50, 20];

    numbers.sort_by(|a, b| b.cmp(a));

    println!("{:?}", numbers);
}
```

---

## 浮点数排序

浮点数不能直接使用普通 `sort()` ，因为其中可能存在 `NaN` 。

可以使用：

```
sort_by()
```
```
fn main() {
    let mut prices =
        vec![29.9, 10.5, 88.0, 35.6];

    prices.sort_by(|a, b| {
        a.partial_cmp(b).unwrap()
    });

    println!("{:?}", prices);
}
```

正式项目中需要考虑 `NaN` ，避免随意使用 `unwrap()` 。

---

## 去除重复元素

`dedup()` 只会删除相邻的重复元素。

```
fn main() {
    let mut numbers =
        vec![1, 2, 2, 3, 1, 1];

    numbers.dedup();

    println!("{:?}", numbers);
}
```

结果：

```
[1, 2, 3, 1]
```

如果要删除所有重复值，可以先排序：

```
fn main() {
    let mut numbers =
        vec![3, 1, 2, 3, 2, 1];

    numbers.sort();
    numbers.dedup();

    println!("{:?}", numbers);
}
```

输出：

```
[1, 2, 3]
```

---

## 使用 append() 合并 Vec

```
fn main() {
    let mut first = vec![1, 2, 3];
    let mut second = vec![4, 5, 6];

    first.append(&mut second);

    println!("first：{:?}", first);
    println!("second：{:?}", second);
}
```

输出：

```
first：[1, 2, 3, 4, 5, 6]
second：[]
```

`append()` 会把 `second` 中的元素移动到 `first` 。

---

## 使用 extend() 添加多个元素

```
fn main() {
    let mut numbers = vec![1, 2];

    numbers.extend([3, 4, 5]);

    println!("{:?}", numbers);
}
```

输出：

```
[1, 2, 3, 4, 5]
```

---

## Vec 与切片

`Vec<T>` 可以方便地借用为：

```
&[T]
```

例如：

```
fn calculate_total(numbers: &[i32]) -> i32 {
    numbers.iter().sum()
}

fn main() {
    let numbers = vec![10, 20, 30];

    println!("{}", calculate_total(&numbers));
}
```

函数只需要读取数据时，使用切片参数比直接接收 `Vec` 更通用。

同一个函数既可以接收数组，也可以接收 `Vec` ：

```
let array = [1, 2, 3];
let vector = vec![4, 5, 6];

calculate_total(&array);
calculate_total(&vector);
```

---

## Vec 与所有权

`Vec` 可以保存 `String` ：

```
fn main() {
    let names = vec![
        String::from("Tom"),
        String::from("Alice"),
    ];

    println!("{:?}", names);
}
```

不能直接把元素从索引位置移动出来：

```
let name = names[0];
```

因为索引操作通常返回引用位置，而不能破坏集合结构。

可以借用：

```
let name = &names[0];
```

也可以克隆：

```
let name = names[0].clone();
```

或者通过 `remove()` 取得所有权：

```
fn main() {
    let mut names = vec![
        String::from("Tom"),
        String::from("Alice"),
    ];

    let name = names.remove(0);

    println!("{}", name);
}
```

---

## 数组、Vec 与切片的区别

| 特性 | Array | Vec | Slice |
| --- | --- | --- | --- |
| 长度 | 固定 | 动态 | 由引用范围决定 |
| 是否拥有数据 | 是 | 是 | 否 |
| 添加元素 | 不支持 | 支持 | 不支持 |
| 删除元素 | 不支持 | 支持 | 不支持 |
| 常见类型 | `[T; N]` | `Vec<T>` | `&[T]` |
| 使用场景 | 固定数量 | 动态集合 | 借用连续数据 |

可以简单理解：

> Array 是固定长度容器。

> Vec 是动态长度容器。

> Slice 是对容器中一段数据的借用。

---

## 实战：商品列表管理

定义一个商品名称列表，支持添加、删除和查找：

```
fn main() {
    let mut products = vec![
        String::from("键盘"),
        String::from("鼠标"),
        String::from("显示器"),
    ];

    products.push(
        String::from("耳机"),
    );

    if let Some(position) = products
        .iter()
        .position(|name| name == "鼠标")
    {
        let removed = products.remove(position);

        println!("删除商品：{}", removed);
    }

    for (index, product) in
        products.iter().enumerate()
    {
        println!(
            "{}. {}",
            index + 1,
            product
        );
    }
}
```

输出：

```
删除商品：鼠标
1. 键盘
2. 显示器
3. 耳机
```

---

## 实战：成绩统计

```
fn analyze_scores(
    scores: &[i32],
) -> Option<(i32, f64, i32, i32)> {
    if scores.is_empty() {
        return None;
    }

    let total: i32 = scores.iter().sum();
    let average =
        total as f64 / scores.len() as f64;

    let min = *scores.iter().min()?;
    let max = *scores.iter().max()?;

    Some((total, average, min, max))
}

fn main() {
    let mut scores = vec![88, 59, 95, 76];

    scores.push(100);
    scores.retain(|score| *score >= 60);
    scores.sort_by(|a, b| b.cmp(a));

    match analyze_scores(&scores) {
        Some((total, average, min, max)) => {
            println!("成绩：{:?}", scores);
            println!("总分：{}", total);
            println!("平均分：{:.2}", average);
            println!("最低分：{}", min);
            println!("最高分：{}", max);
        }
        None => {
            println!("没有成绩数据");
        }
    }
}
```

输出：

```
成绩：[100, 95, 88, 76]
总分：359
平均分：89.75
最低分：76
最高分：100
```

---

## 实战：简单任务队列

```
fn main() {
    let mut tasks = vec![
        String::from("学习 Vec"),
        String::from("编写练习"),
    ];

    tasks.push(
        String::from("复习所有权"),
    );

    println!("当前任务：");

    for (index, task) in
        tasks.iter().enumerate()
    {
        println!("{}. {}", index + 1, task);
    }

    if !tasks.is_empty() {
        let finished = tasks.remove(0);

        println!("完成任务：{}", finished);
    }

    println!("剩余任务：{:?}", tasks);
}
```

需要频繁从队列开头删除元素时，实际项目通常更适合使用：

```
VecDeque
```

因为 `Vec::remove(0)` 会移动后面的所有元素。

---

## 常见错误

## 忘记声明 mut

错误：

```
let numbers = vec![1, 2, 3];

numbers.push(4);
```

正确：

```
let mut numbers = vec![1, 2, 3];

numbers.push(4);
```

---

## 空 Vec 没有指定类型

错误：

```
let values = Vec::new();
```

如果后面没有足够信息帮助推断类型，编译器会报错。

正确：

```
let values: Vec<i32> = Vec::new();
```

---

## 使用索引访问越界元素

错误：

```
let numbers = vec![1, 2, 3];

println!("{}", numbers[10]);
```

不确定索引是否合法时，应使用：

```
numbers.get(10)
```

---

## 遍历时同时修改 Vec 结构

下面的思路通常会产生借用冲突：

```
for number in &numbers {
    numbers.push(*number);
}
```

遍历期间已经不可变借用了 `numbers` ，不能同时进行可变修改。

可以先收集新元素，再统一添加。

---

## 误以为 dedup() 会删除所有重复值

```
let mut values = vec![1, 2, 1];

values.dedup();
```

结果仍然是：

```
[1, 2, 1]
```

因为重复值不相邻。

如果不关心原顺序，可以先排序再去重。

---

## 频繁 remove(0)

```
values.remove(0);
```

每次都会移动后面的元素。

如果业务是先进先出的队列，应考虑：

```
VecDeque
```

---

## 最佳实践

## 函数只读集合时使用切片

推荐：

```
fn print_values(values: &[i32]) {
    println!("{:?}", values);
}
```

而不是：

```
fn print_values(values: &Vec<i32>) {
}
```

切片参数更通用。

---

## 已知数据量时预分配容量

```
let mut records =
    Vec::with_capacity(1000);
```

可以减少扩容次数，但不需要为很小的数据过度优化。

---

## 不确定索引时使用 get()

```
if let Some(value) = values.get(index) {
    println!("{}", value);
}
```

---

## 不关心顺序时使用 swap\_remove()

```
values.swap_remove(index);
```

它通常比 `remove()` 更高效，但会改变元素顺序。

---

## 多个业务字段优先使用结构体

不推荐长期使用：

```
Vec<(u64, String, f64, bool)>
```

更清晰的写法是：

```
struct Product {
    id: u64,
    name: String,
    price: f64,
    enabled: bool,
}
```

然后使用：

```
Vec<Product>
```

---

## 本章小结

`Vec<T>` 是 Rust 中最常用的动态集合之一。

通过本文，我们学习了：

- • 使用 `vec![]` 创建动态数组
- • 使用 `Vec::new()` 创建空集合
- • `push()` 、 `pop()` 、 `insert()` 和 `remove()`
- • 使用索引和 `get()` 访问元素
- • 使用 `get_mut()` 修改元素
- • 遍历和可变遍历
- • `len()` 、 `capacity()` 和动态扩容
- • `clear()` 、 `retain()` 和 `contains()`
- • 排序、查找与去重
- • `append()` 和 `extend()`
- • `Vec<String>` 的所有权问题
- • `Vec` 与数组、切片的区别
- • 商品列表、成绩统计和任务队列案例

可以记住：

> 固定数量的数据使用数组。

> 动态变化的数据使用 `Vec` 。

> 函数只需要读取集合时，参数优先使用切片 `&[T]` 。

---

## 下一篇预告

下一篇我们将学习 **Rust HashMap 哈希表详解** ，包括：

- • 什么是 `HashMap`
- • 创建哈希表
- • 插入和更新键值
- • 通过键查询数据
- • `get()` 与安全访问
- • 删除键值
- • 遍历 `HashMap`
- • `entry()` API
- • `or_insert()` 与计数统计
- • `String` 所有权问题
- • `HashMap` 与 `Vec` 的区别
- • 实战：用户信息、商品库存和单词统计

![](https://wst.wxapp.tc.qq.com/161/20304/snscosdownload/SH/reserved/6a4b558400068d461cecff05e3351f15000000a100004f50?imageView2/1/w/800/h/800/q/50)

Rust编程思维 从C++到Rust的平滑过渡 黄祥 机械工业出版社9787

运费险

先用后付

7天无理由

¥109

![](https://res.wx.qq.com/shop/public/2024-10-17/fae7be51-beb6-4e61-aad8-4c1f7ccfab83.png)

义博图书甄选店

![](https://res.wx.qq.com/t/components/icons/base/arrow_down_regular.svg) 收起

使用手机微信

扫码了解商品信息

Rust 编程实战 · Table of Contents