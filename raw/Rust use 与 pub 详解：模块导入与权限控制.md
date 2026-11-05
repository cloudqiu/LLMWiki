---
title: "Rust use 与 pub 详解：模块导入与权限控制"
source: "https://mp.weixin.qq.com/s?__biz=MzYzODE1NzUzMw==&mid=2247484527&idx=1&sn=dbf965d54444ce552e00827c4944efbd&chksm=f0e753ddc790dacbf413264c45a2264d82fc6cfc9db5a2c2690ecaa370c8448f4a015b7245f3&cur_album_id=4602071361631748097&scene=189#wechat_redirect"
author:
published:
created: 2026-11-05
description:
tags:
  - "clippings"
---
程序员爱钓鱼 *Aug 1, 2026, 6:04 AM*

> 《Rust 编程实战》系列第 27 篇

在上一篇文章中，我们学习了：

- • Package
- • Crate
- • Module

了解了 Rust 项目的组织结构：

```
Package
    |
    └── Crate
            |
            └── Module
                    |
                    └── Function
```

但是在实际开发中，还有两个非常重要的问题：

1. 1\. 一个模块中的代码如何被另一个模块使用？
2. 2\. 哪些代码应该暴露给外部？

Rust 提供了两个关键字：

```
use
```

和：

```
pub
```

其中：

- • `use` 负责引入路径，简化代码调用
- • `pub` 负责控制访问权限，决定哪些内容可以被外部使用

本文将介绍：

- • use 基础用法
- • 多层路径导入
- • as 重命名
- • pub 权限控制
- • pub(crate)
- • pub(super)
- • re-export
- • 模块 API 设计
- • 实际项目应用

---

## use 的作用

Rust 中模块之间默认通过完整路径访问。

例如：

```
mod user {
    pub fn login() {
        println!("用户登录");
    }
}

fn main(){
    user::login();
}
```

如果模块层级较深：

```
app::user::service::login();
```

代码会变得很长。

这时候可以使用：

```
use
```

提前导入。

---

## 基础 use 使用

例如：

```
mod user {
    pub fn login(){
        println!(
            "登录成功"
        );
    }
}

use user::login;

fn main(){
    login();
}
```

执行：

```
登录成功
```

这里：

```
use user::login;
```

把函数引入当前作用域。

之后可以直接：

```
login();
```

---

## 导入模块

除了导入函数，也可以导入整个模块：

```
mod user {

    pub fn login(){

    }
    pub fn logout(){

    }

}

use user;

fn main(){
    user::login();
    user::logout();

}
```

---

## 使用多个导入

假设：

```
std::collections
```

中有：

```
HashMap
HashSet
```

传统写法：

```
use std::collections::HashMap;
use std::collections::HashSet;
```

可以简写：

```
use std::collections::{
    HashMap,
    HashSet,
};
```

这种方式在大型项目非常常见。

---

## 使用通配符 \*

可以导入模块所有公开内容：

```
use std::collections::*;
```

例如：

```
let map =
    HashMap::new();

let set =
    HashSet::new();
```

但是：

> 不推荐大量使用 `*`

原因：

- • 不知道引入了什么
- • 容易产生名称冲突
- • 降低代码可读性

通常只在：

- • 测试代码
- • 特殊场景

使用。

---

## 使用 as 重命名

如果两个模块存在同名类型：

例如：

```
use module_a::User;
use module_b::User;
```

会冲突。

可以使用：

```
as
```

重命名。

示例：

```
use module_a::User as AdminUser;

use module_b::User as CustomerUser;
```

使用：

```
let admin =
    AdminUser {};
let customer =
    CustomerUser {};
```

---

## 什么是 pub？

Rust 默认所有内容都是私有的：

例如：

```
mod user {
    fn login(){

    }
}
```

外部无法访问：

```
user::login();
```

因为：

```
login()
```

默认私有。

---

## 使用 pub 暴露内容

添加：

```
pub
```

即可公开：

```
mod user {
    pub fn login(){
        println!(
            "登录"
        );
    }
}

fn main(){
    user::login();
}
```

---

## pub 可以修饰什么？

## 函数

```
pub fn login(){

}
```

---

## 结构体

```
pub struct User {

}
```

---

## 字段

结构体字段默认也是私有：

```
pub struct User {
    pub name:String,
    age:u32,
}
```

外部：

可以：

```
user.name
```

不能：

```
user.age
```

---

## 枚举

枚举公开后：

所有成员默认公开：

```
pub enum Status {
    Success,
    Failed,
}
```

可以：

```
Status::Success
```

---

## pub(crate)

有时候：

我们不希望整个外部项目访问。

只希望：

当前 Crate 内使用。

使用：

```
pub(crate)
```

例如：

```
pub(crate) fn internal(){

}
```

访问范围：

```
当前 Crate
```

不可被外部依赖项目使用。

适合：

- • 项目内部工具
- • 内部服务
- • 私有实现

---

## pub(super)

表示：

父模块可以访问。

例如：

```
mod user {
    fn check(){

    }
    mod auth {
        pub(super) fn verify(){

        }
    }
}
```

这里：

```
verify()
```

只有：

```
user
```

模块可以访问。

---

## pub(in path)

更细粒度权限：

```
pub(in crate::user)
fn test(){

}
```

表示：

只有：

```
crate::user
```

路径下可以访问。

实际开发中较少使用。

---

## use 与 pub 结合

大型项目中经常：

内部结构：

```
user
 |
 ├── model.rs
 |
 ├── service.rs
 |
 └── repository.rs
```

外部只需要：

```
user::UserService
```

而不是：

```
user::service::UserService
```

可以使用：

```
pub use
```

重新导出。

---

## pub use（重新导出）

例如：

model.rs：

```
pub struct User {
    pub name:String,
}
```

user/mod.rs：

```
mod model;

pub use model::User;
```

外部：

原来：

```
user::model::User
```

现在：

```
user::User
```

更加简洁。

---

## 实战：设计公共 API

假设项目：

```
shop

src

├── lib.rs

└── user

    ├── mod.rs

    ├── model.rs

    └── service.rs
```

---

model.rs：

```
pub struct User {
    pub name:String,
}
```

---

service.rs：

```
use super::model::User;

pub fn create_user(
    name:String
)
-> User {
    User {
        name
    }
}
```

---

user/mod.rs：

```
mod model;

mod service;

pub use model::User;

pub use service::create_user;
```

---

外部调用：

```
use shop::user::{
    User,
    create_user,
};

fn main(){

    let user =
        create_user(
            String::from("Tom")
        );

    println!(
        "{}",
        user.name
    );

}
```

外部不需要知道内部文件结构。

这就是良好的模块设计。

---

## use 的作用域

注意：

```
use
```

只影响当前模块。

例如：

```
mod user {

    use std::collections::HashMap;

}
```

这个 HashMap 只能在：

```
user
```

模块内部使用。

外部无法使用。

---

## 常见错误

## 忘记 pub

错误：

```
mod user {
    fn login(){

    }
}
```

外部无法访问。

解决：

```
pub fn login(){

}
```

---

## 导入路径错误

例如：

```
use user::Login;
```

但是实际：

```
user::login
```

大小写错误会失败。

Rust 区分大小写。

---

## 过度 pub

不要：

```
pub fn every_internal_function(){

}
```

全部公开。

这样会：

- • 增加维护成本
- • 暴露实现细节
- • 降低安全性

推荐：

只公开必要 API。

---

## 大量使用 glob 导入

例如：

```
use crate::*;
```

大型项目中容易混乱。

推荐明确：

```
use crate::user::User;
```

---

## Rust 模块设计原则

## 1\. 默认私有

先写：

```
fn
```

需要外部访问时再：

```
pub
```

---

## 2\. 暴露业务接口

例如：

推荐：

```
pub fn login()
```

隐藏：

```
fn verify_password()
```

---

## 3\. 使用 pub use 简化调用

内部：

```
user/service/login
```

外部：

```
user::login()
```

提升 API 体验。

---

## 4\. 模块按照业务划分

推荐：

```
src
├── user
├── product
├── order
├── payment
└── common
```

不要：

```
utils.rs
```

塞入所有代码。

---

## 本章小结

Rust 中：

## use

负责：

- • 引入模块
- • 简化路径
- • 解决名称冲突

例如：

```
use crate::user::User;
```

---

## pub

负责：

- • 控制访问权限
- • 设计模块 API

包括：

```
pub
pub(crate)
pub(super)
pub use
```

---

大型 Rust 项目的核心思想：

> 内部实现隐藏，公共接口清晰。

通过：

```
Module
+
use
+
pub
```

可以构建清晰、安全、易维护的 Rust 项目结构。

---

## 下一篇预告

下一篇将学习：

## Rust 文档生成详解：cargo doc 与 API 文档

内容包括：

- • Rust 文档注释
- • /// 与 //!
- • Markdown 文档格式
- • cargo doc
- • cargo doc --open
- • 示例代码测试
- • 文档测试 doctest
- • 发布 Crates 文档
- • 实战：为 Rust 库编写完整文档

Rust 编程实战 · Table of Contents