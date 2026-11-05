---
title: "Rust HashMap 详解：键值存储、查询、更新与统计"
source: "https://mp.weixin.qq.com/s?__biz=MzYzODE1NzUzMw==&mid=2247484488&idx=1&sn=32f7c0080926ab4747f259c9e51e6a57&chksm=f0e753fac790daec218dc8f6fef5d899934c49dbd33e9eb108ff8b0914bb4b5529d86cc5accf&cur_album_id=4602071361631748097&scene=189#wechat_redirect"
author:
published:
created: 2026-11-05
description: "《Rust 编程实战》系列第 20 篇在上一篇文章中，我们学习了动态数组 Vec\x26lt;T\x26gt;。"
tags:
  - "clippings"
---
程序员爱钓鱼 *Jul 25, 2026, 8:36 AM*

> 《Rust 编程实战》系列第 20 篇

在上一篇文章中，我们学习了动态数组 `Vec<T>` 。

`Vec` 适合按照顺序保存一组相同类型的数据，例如：

```
let products = vec![
    "键盘",
    "鼠标",
    "显示器",
];
```

访问元素时，通常需要使用数字索引：

```
products[0]
```

但在实际开发中，很多数据更适合通过一个具有明确含义的键进行查询。

例如：

- • 通过用户名查询用户积分
- • 通过商品编号查询库存
- • 通过单词查询出现次数
- • 通过配置名称查询配置值
- • 通过城市名称查询天气数据

Rust 标准库提供了：

```
HashMap<K, V>
```

`HashMap` 通常称为哈希表、散列表或键值映射。

它使用“键”和“值”保存数据：

```
键 -> 值
```

例如：

```
"Tom" -> 100
"Alice" -> 200
```

本文将介绍：

- • 什么是 `HashMap`
- • 创建哈希表
- • 插入键值
- • 查询和修改数据
- • 删除键值
- • 遍历 `HashMap`
- • `entry()` API
- • 单词计数
- • 所有权问题
- • `HashMap` 与 `Vec` 的区别
- • 常见错误
- • 实战案例

---

## 什么是 HashMap？

`HashMap` 是一种通过键查找值的集合。

它的完整类型是：

```
HashMap<K, V>
```

其中：

- • `K` 表示键的类型
- • `V` 表示值的类型

例如：

```
HashMap<String, i32>
```

表示：

- • 键是 `String`
- • 值是 `i32`

可以保存这样的数据：

```
"Tom" -> 100
"Alice" -> 95
"Bob" -> 88
```

与 `Vec` 不同， `HashMap` 不是通过连续数字索引访问元素，而是通过键访问。

---

## 导入 HashMap

`HashMap` 位于 Rust 标准库的集合模块中。

使用前需要导入：

```
use std::collections::HashMap;
```

完整示例：

```
use std::collections::HashMap;

fn main() {
    let scores: HashMap<String, i32> =
        HashMap::new();

    println!("{:?}", scores);
}
```

输出：

```
{}
```

---

## 创建 HashMap

最常见的创建方式是：

```
HashMap::new()
```

例如：

```
use std::collections::HashMap;

fn main() {
    let mut scores = HashMap::new();

    scores.insert("Tom", 90);
    scores.insert("Alice", 100);

    println!("{:?}", scores);
}
```

Rust 可以根据插入的数据推断类型。

这里的类型通常是：

```
HashMap<&str, i32>
```

由于需要调用 `insert()` 修改集合，因此必须使用：

```
mut
```

---

## 显式声明类型

创建空 `HashMap` 时，也可以明确声明键和值的类型：

```
use std::collections::HashMap;

fn main() {
    let mut users:
        HashMap<String, u32> =
        HashMap::new();

    users.insert(
        String::from("Tom"),
        100,
    );

    println!("{:?}", users);
}
```

这里：

```
HashMap<String, u32>
```

表示用户名为 `String` ，积分为 `u32` 。

---

## 使用 insert() 插入数据

`insert()` 用于插入键值对。

语法：

```
map.insert(key, value);
```

示例：

```
use std::collections::HashMap;

fn main() {
    let mut prices = HashMap::new();

    prices.insert("键盘", 299.0);
    prices.insert("鼠标", 99.0);
    prices.insert("显示器", 1599.0);

    println!("{:?}", prices);
}
```

`HashMap` 中的所有键必须是相同类型，所有值也必须是相同类型。

下面这种写法不允许：

```
map.insert("name", "Tom");
map.insert("age", 20);
```

因为第一个值是字符串，第二个值是整数。

---

## 相同键会覆盖旧值

一个 `HashMap` 中不能同时存在两个完全相同的键。

```
use std::collections::HashMap;

fn main() {
    let mut scores = HashMap::new();

    scores.insert("Tom", 80);
    scores.insert("Tom", 100);

    println!("{:?}", scores);
}
```

最终只会保留：

```
"Tom" -> 100
```

第二次插入会覆盖第一次的值。

---

## insert() 的返回值

`insert()` 会返回被替换的旧值。

返回类型是：

```
Option<V>
```

示例：

```
use std::collections::HashMap;

fn main() {
    let mut scores = HashMap::new();

    let first = scores.insert("Tom", 80);
    let second = scores.insert("Tom", 100);

    println!("第一次：{:?}", first);
    println!("第二次：{:?}", second);
}
```

输出：

```
第一次：None
第二次：Some(80)
```

第一次插入时没有旧值，因此返回 `None` 。

第二次插入覆盖了 `80` ，因此返回 `Some(80)` 。

---

## 使用 get() 查询数据

可以通过键查询值：

```
use std::collections::HashMap;

fn main() {
    let mut scores = HashMap::new();

    scores.insert("Tom", 90);
    scores.insert("Alice", 100);

    let result = scores.get("Tom");

    println!("{:?}", result);
}
```

输出：

```
Some(90)
```

`get()` 返回：

```
Option<&V>
```

因为指定的键可能不存在。

---

## 使用 match 处理查询结果

```
use std::collections::HashMap;

fn main() {
    let mut scores = HashMap::new();

    scores.insert("Tom", 90);

    match scores.get("Alice") {
        Some(score) => {
            println!("成绩：{}", score);
        }
        None => {
            println!("没有找到该用户");
        }
    }
}
```

这样可以安全处理键不存在的情况。

---

## 使用 if let 查询

只关心查询成功的情况时，可以使用：

```
if let
```
```
use std::collections::HashMap;

fn main() {
    let mut scores = HashMap::new();

    scores.insert("Tom", 90);

    if let Some(score) = scores.get("Tom") {
        println!("Tom 的成绩：{}", score);
    }
}
```

---

## 判断键是否存在

可以使用：

```
contains_key()
```
```
use std::collections::HashMap;

fn main() {
    let mut users = HashMap::new();

    users.insert("Tom", true);

    println!("{}", users.contains_key("Tom"));
    println!("{}", users.contains_key("Alice"));
}
```

输出：

```
true
false
```

---

## 使用 get\_mut() 修改值

如果需要修改已经存在的值，可以使用：

```
get_mut()
```
```
use std::collections::HashMap;

fn main() {
    let mut scores = HashMap::new();

    scores.insert("Tom", 90);

    if let Some(score) = scores.get_mut("Tom") {
        *score += 10;
    }

    println!("{:?}", scores);
}
```

输出：

```
{"Tom": 100}
```

`get_mut()` 返回可变引用，因此需要通过：

```
*score
```

修改实际值。

---

## 使用 remove() 删除数据

```
use std::collections::HashMap;

fn main() {
    let mut users = HashMap::new();

    users.insert("Tom", 100);
    users.insert("Alice", 200);

    let removed = users.remove("Tom");

    println!("删除结果：{:?}", removed);
    println!("剩余数据：{:?}", users);
}
```

`remove()` 返回：

```
Option<V>
```

如果键存在，会删除并返回对应的值。

---

## 获取 HashMap 长度

使用：

```
len()
```
```
use std::collections::HashMap;

fn main() {
    let mut map = HashMap::new();

    map.insert("a", 1);
    map.insert("b", 2);

    println!("长度：{}", map.len());
}
```

判断是否为空：

```
map.is_empty()
```

清空全部数据：

```
map.clear()
```

---

## 遍历 HashMap

可以使用 `for` 遍历键和值：

```
use std::collections::HashMap;

fn main() {
    let mut scores = HashMap::new();

    scores.insert("Tom", 90);
    scores.insert("Alice", 100);
    scores.insert("Bob", 85);

    for (name, score) in &scores {
        println!("{}：{}", name, score);
    }
}
```

需要注意：

> `HashMap` 默认不保证遍历顺序。

每次运行时，输出顺序都可能不同。

不要依赖 `HashMap` 的遍历顺序。

---

## 只遍历键

可以使用：

```
keys()
```
```
for key in scores.keys() {
    println!("{}", key);
}
```

---

## 只遍历值

可以使用：

```
values()
```
```
for value in scores.values() {
    println!("{}", value);
}
```

如果需要修改所有值，可以使用：

```
values_mut()
```
```
use std::collections::HashMap;

fn main() {
    let mut scores = HashMap::new();

    scores.insert("Tom", 80);
    scores.insert("Alice", 90);

    for score in scores.values_mut() {
        *score += 5;
    }

    println!("{:?}", scores);
}
```

---

## 使用 entry() 插入默认值

很多场景需要实现：

> 如果键不存在就插入，存在则保留原值。

可以使用：

```
entry()
```

示例：

```
use std::collections::HashMap;

fn main() {
    let mut scores = HashMap::new();

    scores.insert("Tom", 90);

    scores
        .entry("Tom")
        .or_insert(100);

    scores
        .entry("Alice")
        .or_insert(100);

    println!("{:?}", scores);
}
```

结果中：

- • `Tom` 已存在，仍然是 `90`
- • `Alice` 不存在，被插入为 `100`

---

## 使用 entry() 进行计数

`HashMap` 非常适合统计单词出现次数。

```
use std::collections::HashMap;

fn main() {
    let text = "rust go rust java rust go";

    let mut counts = HashMap::new();

    for word in text.split_whitespace() {
        let count = counts
            .entry(word)
            .or_insert(0);

        *count += 1;
    }

    println!("{:?}", counts);
}
```

统计结果类似：

```
{
    "rust": 3,
    "go": 2,
    "java": 1
}
```

这里：

```
or_insert(0)
```

在单词第一次出现时插入 `0` 。

返回的是可变引用：

```
&mut i32
```

所以使用：

```
*count += 1;
```

增加计数。

---

## or\_insert\_with()

如果默认值需要通过函数或复杂计算获得，可以使用：

```
or_insert_with()
```
```
use std::collections::HashMap;

fn main() {
    let mut users:
        HashMap<String, Vec<String>> =
        HashMap::new();

    users
        .entry(String::from("Tom"))
        .or_insert_with(Vec::new)
        .push(String::from("Rust"));

    println!("{:?}", users);
}
```

当键不存在时，才会调用：

```
Vec::new
```

创建空动态数组。

---

## 从 Vec 创建 HashMap

可以结合 `zip()` 和 `collect()` 创建哈希表。

```
use std::collections::HashMap;

fn main() {
    let names = vec!["Tom", "Alice", "Bob"];
    let scores = vec![90, 100, 85];

    let result: HashMap<_, _> =
        names
            .into_iter()
            .zip(scores.into_iter())
            .collect();

    println!("{:?}", result);
}
```

`zip()` 会将两组数据按位置组合：

```
("Tom", 90)
("Alice", 100)
("Bob", 85)
```

然后使用 `collect()` 收集为 `HashMap` 。

---

## HashMap 的所有权

将拥有所有权的值插入 `HashMap` 时，所有权通常会移动。

```
use std::collections::HashMap;

fn main() {
    let key = String::from("Tom");
    let value = String::from("管理员");

    let mut users = HashMap::new();

    users.insert(key, value);

    println!("{:?}", users);
}
```

插入后，不能继续使用：

```
key
value
```

因为所有权已经移动到 `HashMap` 中。

如果插入的是实现了 `Copy` 的类型，例如整数，值会被复制。

---

## 使用引用作为键和值

也可以把引用插入 `HashMap` ：

```
use std::collections::HashMap;

fn main() {
    let key = String::from("Tom");
    let value = String::from("管理员");

    let mut users = HashMap::new();

    users.insert(&key, &value);

    println!("{:?}", users);
    println!("{} {}", key, value);
}
```

此时 `HashMap` 借用了外部数据。

需要保证外部数据的生命周期至少和 `HashMap` 一样长。

初学阶段，如果数据需要长期保存在集合中，使用拥有所有权的 `String` 通常更简单。

---

## String 键的查询

假设键类型是：

```
String
```

查询时通常不需要创建新的 `String` 。

```
use std::collections::HashMap;

fn main() {
    let mut users:
        HashMap<String, i32> =
        HashMap::new();

    users.insert(
        String::from("Tom"),
        100,
    );

    println!("{:?}", users.get("Tom"));
}
```

虽然键是 `String` ，但可以直接使用 `&str` 查询。

这样可以避免为了查询而额外创建字符串。

---

## HashMap 与 Vec 的区别

| 特性 | `Vec<T>` | `HashMap<K, V>` |
| --- | --- | --- |
| 数据形式 | 元素列表 | 键值对 |
| 访问方式 | 数字索引 | 键 |
| 顺序 | 保持元素顺序 | 不保证顺序 |
| 重复 | 可以重复 | 键不能重复 |
| 适合场景 | 顺序数据 | 快速按键查询 |
| 示例 | 商品列表 | 商品库存表 |

例如，保存文章列表可以使用：

```
Vec<Article>
```

通过文章编号查询文章，可以考虑：

```
HashMap<u64, Article>
```

实际项目中，两者经常配合使用。

---

## 实战：商品库存管理

```
use std::collections::HashMap;

fn main() {
    let mut stocks = HashMap::new();

    stocks.insert(
        String::from("键盘"),
        20,
    );

    stocks.insert(
        String::from("鼠标"),
        50,
    );

    stocks.insert(
        String::from("显示器"),
        10,
    );

    let product = "键盘";
    let buy_count = 3;

    match stocks.get_mut(product) {
        Some(stock) => {
            if *stock >= buy_count {
                *stock -= buy_count;

                println!("购买成功");
                println!("剩余库存：{}", stock);
            } else {
                println!("库存不足");
            }
        }
        None => {
            println!("商品不存在");
        }
    }
}
```

这个案例完成了：

- • 商品库存保存
- • 按商品名查询
- • 获取可变引用
- • 判断库存
- • 扣减库存

---

## 实战：用户登录次数统计

```
use std::collections::HashMap;

fn record_login(
    records: &mut HashMap<String, u32>,
    username: &str,
) {
    let count = records
        .entry(username.to_string())
        .or_insert(0);

    *count += 1;
}

fn main() {
    let mut records = HashMap::new();

    record_login(&mut records, "Tom");
    record_login(&mut records, "Alice");
    record_login(&mut records, "Tom");

    for (username, count) in &records {
        println!(
            "{} 登录了 {} 次",
            username,
            count
        );
    }
}
```

`entry()` API 可以避免先查询再插入，让代码更加简洁。

---

## 实战：统计最高频单词

```
use std::collections::HashMap;

fn main() {
    let text =
        "rust is fast and rust is safe";

    let mut counts = HashMap::new();

    for word in text.split_whitespace() {
        *counts.entry(word).or_insert(0) += 1;
    }

    let most_common = counts
        .iter()
        .max_by_key(|(_, count)| *count);

    match most_common {
        Some((word, count)) => {
            println!(
                "出现最多的单词：{}，次数：{}",
                word,
                count
            );
        }
        None => {
            println!("没有单词");
        }
    }
}
```

输出：

```
出现最多的单词：rust，次数：2
```

---

## 常见错误

## 忘记导入 HashMap

错误：

```
let map = HashMap::new();
```

如果没有导入，会找不到类型。

正确：

```
use std::collections::HashMap;
```

---

## 忘记声明 mut

错误：

```
let map = HashMap::new();

map.insert("Tom", 100);
```

正确：

```
let mut map = HashMap::new();
```

---

## 直接假设键一定存在

不推荐：

```
let value = map.get("Tom").unwrap();
```

如果键不存在，程序会 panic。

更安全的方式是使用：

```
match
```

或：

```
if let
```

---

## 遍历时依赖顺序

`HashMap` 不保证元素顺序。

如果业务要求排序，可以把数据收集到 `Vec` 后排序，或者使用其他有序映射结构。

---

## 插入 String 后继续使用原变量

```
let name = String::from("Tom");

map.insert(name, 100);

println!("{}", name);
```

如果 `name` 作为拥有所有权的键插入，之后不能继续使用它。

可以插入：

```
name.clone()
```

但不要无意义地滥用 `clone()` 。

---

## 先查询再插入导致代码重复

不推荐：

```
if map.contains_key("Tom") {
    let value = map.get_mut("Tom").unwrap();
    *value += 1;
} else {
    map.insert("Tom", 1);
}
```

推荐使用：

```
*map.entry("Tom").or_insert(0) += 1;
```

---

## 最佳实践

## 不确定键是否存在时使用 get()

```
if let Some(value) = map.get(key) {
    println!("{}", value);
}
```

避免直接使用 `unwrap()` 。

---

## 统计和默认值优先使用 entry()

```
*counts.entry(word).or_insert(0) += 1;
```

这是 `HashMap` 最常见、最实用的写法之一。

---

## 字符串查询尽量使用 &str

当键是 `String` 时，查询通常可以直接使用：

```
map.get("Tom")
```

不需要写成：

```
map.get(&String::from("Tom"))
```

这样可以减少不必要的内存分配。

---

## 不依赖 HashMap 的遍历顺序

如果需要按键排序：

```
let mut items: Vec<_> =
    map.iter().collect();

items.sort_by_key(|(key, _)| *key);
```

排序需求应该显式实现。

---

## 复杂业务数据使用结构体

例如：

```
struct Product {
    name: String,
    price: f64,
    stock: u32,
}
```

然后使用：

```
HashMap<u64, Product>
```

通过商品编号快速查找完整商品信息。

---

## 本章小结

`HashMap<K, V>` 是 Rust 中常用的键值集合。

通过本文，我们学习了：

- • 导入和创建 `HashMap`
- • 使用 `insert()` 插入数据
- • 相同键覆盖旧值
- • 使用 `get()` 安全查询
- • `contains_key()` 判断键是否存在
- • 使用 `get_mut()` 修改值
- • 使用 `remove()` 删除数据
- • 遍历键和值
- • `keys()` 、 `values()` 和 `values_mut()`
- • 使用 `entry()` 插入默认值
- • 使用 `or_insert()` 完成计数
- • 从 `Vec` 创建 `HashMap`
- • `String` 插入时的所有权移动
- • `HashMap` 与 `Vec` 的区别
- • 商品库存、登录次数和单词统计案例

可以记住：

> `Vec` 适合按照顺序保存数据。

> `HashMap` 适合通过键快速查询数据。

> 当键可能不存在时，查询结果需要使用 `Option` 处理。

---

## 下一篇预告

下一篇我们将学习 **Rust Option 详解** ，包括：

- • 什么是 `Option<T>`
- • `Some` 与 `None`
- • Rust 为什么没有传统空指针
- • 使用 `match` 处理 `Option`
- • 使用 `if let` 简化判断
- • `unwrap()` 与 `expect()`
- • `unwrap_or()` 与默认值
- • `map()` 、 `and_then()` 和组合操作
- • `Option` 与函数返回值
- • `Option` 与所有权
- • 实战：安全查询、用户信息和配置读取

Rust 编程实战 · Table of Contents