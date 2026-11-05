---
title: "Rust 集成测试详解：验证多个模块与公共 API 的协作"
source: "https://mp.weixin.qq.com/s?__biz=MzYzODE1NzUzMw==&mid=2247484541&idx=1&sn=d49cca7236fa6bafc03fc12d4a6d1db7&chksm=f0e753cfc790dad91e46e61a70a3b2776a7b8200e8df483f785ec08871cea2da65d22cf2ed84&cur_album_id=4602071361631748097&scene=189#wechat_redirect"
author:
published:
created: 2026-11-05
description: "《Rust 编程实战》系列第 30 篇在上一篇文章中，我们学习了 Rust 单元测试，了解了如何使用 #[t"
tags:
  - "clippings"
---
程序员爱钓鱼 *Aug 4, 2026, 8:13 AM*

> 《Rust 编程实战》系列第 30 篇  
> 在上一篇文章中，我们学习了 Rust 单元测试，了解了如何使用 `#[test]` 、 `assert!`、 `assert_eq!`、 `#[should_panic]` 和 `cargo test` 验证函数或模块内部逻辑。  
> 单元测试通常关注较小范围，例如：

- • 一个函数的返回值是否正确
- • 一个私有函数是否正常工作
- • 一个模块的错误分支是否完整  
	但真实项目通常由多个模块共同完成业务。例如用户注册可能同时涉及：
- • 参数校验模块
- • 用户服务模块
- • 数据存储模块
- • 错误处理模块  
	只测试单个函数，并不能保证这些模块组合后仍然正确。Rust 为此提供了集成测试。  
	集成测试主要用于验证：

> 多个模块组合后，程序的公共接口是否按照预期工作。  
> 本文将介绍：

- • 什么是集成测试
- • 单元测试与集成测试的区别
- • `tests` 目录结构
- • 测试 Library Crate
- • 多文件集成测试
- • 公共测试辅助模块
- • 测试文件操作
- • 测试命令行程序
- • 集成测试最佳实践

## 什么是集成测试

集成测试从项目外部调用公共 API，模拟其他程序使用当前 Crate 的方式。  
例如一个数学库提供：

```
pub fn add(a: i32, b: i32) -> i32 {
    a + b
}
```

集成测试不会直接放在 `src/lib.rs` 中，而是放在项目根目录的：

```
tests
```

目录。  
项目结构：

```
math-utils
├── Cargo.toml
├── src
│   └── lib.rs
└── tests
    └── math_test.rs
```

`tests/math_test.rs` ：

```
use math_utils::add;

#[test]
fn add_should_return_sum() {
    assert_eq!(add(10, 20), 30);
}
```

执行：

```
cargo test
```

Cargo 会自动发现并运行 `tests` 目录中的测试。

## 单元测试与集成测试的区别

单元测试通常写在源代码文件内部：

```
#[cfg(test)]
mod tests {
    use super::*;

    #[test]
    fn test_add() {
        assert_eq!(add(1, 2), 3);
    }
}
```

集成测试写在独立文件中：

```
use math_utils::add;

#[test]
fn test_add() {
    assert_eq!(add(1, 2), 3);
}
```

主要区别如下：

| 对比项 | 单元测试 | 集成测试 |
| --- | --- | --- |
| 位置 | `src`  文件内部 | `tests`  目录 |
| 测试范围 | 函数或模块 | 多模块协作 |
| 私有内容 | 可以测试 | 不能直接访问 |
| 公共 API | 可以测试 | 主要测试目标 |
| 编译方式 | 当前 Crate 内部 | 独立测试 Crate |
| 可以简单理解： |  |  |

> 单元测试站在模块内部检查实现。  
> 集成测试站在项目外部检查公共接口。

## 每个测试文件都是独立 Crate

`tests` 目录中的每一个 `.rs` 文件都会被 Cargo 当成独立的测试 Crate。  
例如：

```
tests
├── user_test.rs
├── product_test.rs
└── order_test.rs
```

Cargo 会分别编译：

- • `user_test`
- • `product_test`
- • `order_test`  
	因此每个测试文件都需要单独导入项目中的公共内容：
```
use shop::user::create_user;
```

一个测试文件中的普通函数不能直接被另一个测试文件调用，除非将公共辅助代码组织成模块。

## 为什么集成测试更适合 Library Crate

假设项目只有：

```
src/main.rs
```

那么它主要是 Binary Crate。集成测试通常更容易测试 Library Crate，因为库中的公共函数可以被外部导入。  
推荐结构：

```
src
├── lib.rs
└── main.rs
```

`src/lib.rs` ：

```
pub fn calculate_total(
    price: f64,
    count: u32,
) -> f64 {
    price * count as f64
}
```

`src/main.rs` ：

```
use shop::calculate_total;

fn main() {
    let total = calculate_total(99.0, 2);
    println!("总金额：{}", total);
}
```

`tests/order_test.rs` ：

```
use shop::calculate_total;

#[test]
fn total_should_be_calculated() {
    let result = calculate_total(99.0, 2);
    assert_eq!(result, 198.0);
}
```

这样业务逻辑既能被主程序使用，也能被集成测试直接测试。

## 测试公共 API

集成测试只能正常访问公开内容。  
例如：

```
pub fn create_user() {
}
```

可以被测试。  
但下面的私有函数：

```
fn validate_password() {
}
```

不能直接从 `tests` 目录访问。  
这正是集成测试的重要意义：

> 它只关心用户真正能够使用的公共 API，而不依赖内部实现。  
> 即使以后重构私有函数，只要公共接口行为没有改变，集成测试仍然可以通过。

## 实战：用户注册集成测试

`src/lib.rs` ：

```
pub mod user;
```

`src/user.rs` ：

```
#[derive(Debug, PartialEq)]
pub struct User {
    pub name: String,
    pub age: u32,
}

#[derive(Debug, PartialEq)]
pub enum RegisterError {
    EmptyName,
    InvalidAge,
}

pub fn register(
    name: &str,
    age: u32,
) -> Result<User, RegisterError> {
    if name.trim().is_empty() {
        return Err(RegisterError::EmptyName);
    }
    if age < 18 {
        return Err(RegisterError::InvalidAge);
    }
    Ok(User {
        name: name.trim().to_string(),
        age,
    })
}
```

`tests/user_test.rs` ：

```
use shop::user::{
    register,
    RegisterError,
};

#[test]
fn valid_user_should_register() {
    let result = register("Tom", 20);
    let user = result.expect("注册应该成功");
    assert_eq!(user.name, "Tom");
    assert_eq!(user.age, 20);
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
```

这里从外部完整测试了用户模块的公开行为。

## 运行指定集成测试文件

运行全部测试：

```
cargo test
```

只运行某个集成测试文件：

```
cargo test --test user_test
```

这里的：

```
user_test
```

对应：

```
tests/user_test.rs
```

运行文件中名称包含 `empty` 的测试：

```
cargo test --test user_test empty
```

显示测试输出：

```
cargo test --test user_test -- --nocapture
```

## 多文件集成测试

大型项目可以按业务拆分：

```
tests
├── user_test.rs
├── product_test.rs
├── order_test.rs
└── common
    └── mod.rs
```

这样不同业务拥有独立测试文件，结构更清晰。

## 公共测试辅助模块

多个测试可能需要重复创建数据，例如：

- • 创建测试用户
- • 创建临时配置
- • 创建测试商品
- • 初始化测试数据库  
	可以把公共代码放在：
```
tests/common/mod.rs
```

内容：

```
use shop::user::User;

pub fn create_test_user() -> User {
    User {
        name: String::from("Test User"),
        age: 20,
    }
}
```

在测试文件中使用：

```
mod common;

#[test]
fn test_user_data() {
    let user = common::create_test_user();
    assert_eq!(user.age, 20);
}
```

建议使用：

```
tests/common/mod.rs
```

而不是：

```
tests/common.rs
```

因为 `tests/common.rs` 会被 Cargo 当成一个独立集成测试 Crate，即使里面没有测试，也会被单独编译。

## 测试文件操作

文件测试应该使用独立临时文件，避免修改真实业务数据。  
示例：

```
use std::fs;

#[test]
fn file_should_be_written_and_read() {
    let path = std::env::temp_dir()
        .join("rust_test_data.txt");

    fs::write(&path, "Hello Rust")
        .expect("写入测试文件失败");

    let content = fs::read_to_string(&path)
        .expect("读取测试文件失败");

    assert_eq!(content, "Hello Rust");

    fs::remove_file(&path)
        .expect("删除测试文件失败");
}
```

测试完成后应清理临时数据。  
如果多个测试可能同时运行，文件名最好包含唯一编号，避免并发冲突。

## 测试数据库

数据库集成测试通常验证：

- • 数据能否插入
- • 数据能否查询
- • 数据能否更新
- • 事务失败时是否回滚  
	测试数据库不应该直接使用生产数据库。  
	推荐：
```
开发数据库
测试数据库
生产数据库
```

相互分离。  
每个测试可以遵循：

```
准备测试数据
执行数据库操作
验证结果
清理数据
```

对于支持事务的数据库，可以在测试开始时开启事务，测试结束后回滚，从而保持环境干净。

## 测试 HTTP 接口

Web 项目的集成测试通常模拟完整请求：

```
HTTP 请求
→ 路由
→ 业务逻辑
→ 数据库
→ HTTP 响应
```

例如验证：

- • 状态码是否为 200
- • JSON 字段是否正确
- • 参数错误是否返回 400
- • 未登录是否返回 401
- • 数据不存在是否返回 404  
	集成测试不应该只判断请求成功，还应该验证响应内容和错误格式。

## 测试命令行程序

命令行程序可以测试：

- • 退出状态码
- • 标准输出
- • 标准错误
- • 命令参数
- • 文件生成结果  
	简单示例：
```
use std::process::Command;

#[test]
fn program_should_print_help() {
    let output = Command::new(
        env!("CARGO_BIN_EXE_my_app")
    )
    .arg("--help")
    .output()
    .expect("程序启动失败");

    assert!(output.status.success());

    let stdout =
        String::from_utf8_lossy(&output.stdout);

    assert!(stdout.contains("Usage"));
}
```

`CARGO_BIN_EXE_my_app` 可以获得 Cargo 构建出的测试程序路径。

## 测试环境配置

集成测试可能需要不同配置，例如：

```
APP_ENV=test
DATABASE_URL=测试数据库
LOG_LEVEL=debug
```

测试中可以读取环境变量：

```
let database_url =
    std::env::var("TEST_DATABASE_URL")
        .expect("缺少测试数据库配置");
```

不要把生产密码、令牌或数据库地址直接写进测试代码。

## 并行测试问题

Rust 默认并行运行测试。  
如果两个测试同时操作：

- • 相同文件
- • 相同数据库记录
- • 相同端口
- • 全局环境变量  
	可能互相影响。  
	临时解决方法：
```
cargo test -- --test-threads=1
```

但更推荐让测试资源彼此隔离，例如：

- • 使用不同临时文件
- • 使用唯一用户编号
- • 使用独立数据库事务
- • 随机分配端口

## 集成测试常见错误

## 测试私有函数

错误：

```
use shop::user::validate_password;
```

如果函数不是 `pub` ，集成测试不能访问。  
不要仅为了测试而随意公开内部函数。私有逻辑应该由单元测试验证，集成测试关注公共行为。

## 测试依赖执行顺序

错误思路：

```
测试A创建用户
测试B修改用户
测试C删除用户
```

测试顺序不保证固定。每个测试应该独立创建所需数据。

## 使用生产环境资源

不要在测试中连接生产数据库、修改真实文件或调用真实支付接口。

## 只验证状态码

例如接口返回 200，并不代表业务一定正确，还应该验证返回数据。

## 测试结束后不清理资源

未清理的文件和数据库记录会导致后续测试结果不稳定。

## 集成测试最佳实践

## 单元测试和集成测试配合

推荐：

```
大量快速单元测试
+
少量关键集成测试
```

单元测试覆盖内部逻辑，集成测试覆盖模块协作和关键业务流程。

## 测试公共行为

集成测试应关注：

- • 输入什么
- • 返回什么
- • 状态如何变化  
	不要过度依赖内部实现。

## 每个测试保持独立

测试应该能够：

- • 单独运行
- • 任意顺序运行
- • 重复运行

## 使用真实但隔离的环境

数据库、文件和 HTTP 测试应尽量接近真实环境，但必须与生产环境隔离。

## 为 Bug 添加回归测试

发现线上问题后，应先编写能够复现问题的集成测试，再修复代码，防止相同问题再次出现。

## 本章小结

Rust 集成测试用于从项目外部验证多个模块和公共 API 是否能够正确协作。  
本文学习了：

- • 单元测试与集成测试的区别
- • 使用 `tests` 目录创建集成测试
- • 每个测试文件都是独立 Crate
- • 集成测试只能访问公共 API
- • 使用 `cargo test --test` 运行指定测试
- • 使用 `tests/common/mod.rs` 共享辅助代码
- • 测试文件、数据库、HTTP 和命令行程序
- • 隔离测试环境和测试数据
- • 处理并行测试资源冲突
- • 保持测试独立和可重复  
	可以记住：

> 单元测试验证内部逻辑。  
> 集成测试验证公共接口和模块协作。  
> 高质量项目通常同时包含单元测试与集成测试。

## 下一篇预告

下一篇我们将进入 Rust 最核心的知识：

## Rust 所有权 Ownership 详解

内容包括：

- • 什么是所有权
- • 栈与堆
- • 所有权三条规则
- • 变量作用域
- • String 的内存结构
- • Move 所有权移动
- • Clone 深拷贝
- • Copy Trait
- • 函数参数与所有权
- • 函数返回值转移所有权
- • 所有权与内存安全
- • 常见编译错误与实战案例

Rust 编程实战 · Table of Contents