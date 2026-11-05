---
title: "Rust Module 模块系统详解：组织大型项目代码"
source: "https://mp.weixin.qq.com/s?__biz=MzYzODE1NzUzMw==&mid=2247484516&idx=1&sn=b9a0237c62a77b63f0b6f693edc34d25&chksm=f0e753d6c790dac0c77a4bbc94d55d468afe346edf0347771ad1a3e08df3593a5ed16232a4d4&cur_album_id=4602071361631748097&scene=189#wechat_redirect"
author:
published:
created: 2026-11-05
description: "《Rust 编程实战》系列第 25 篇随着 Rust 项目越来越复杂，把所有代码写在一个：main.rs文件"
tags:
  - "clippings"
---
程序员爱钓鱼 *Jul 30, 2026, 7:30 AM*

> 《Rust 编程实战》系列第 25 篇

随着 Rust 项目越来越复杂，把所有代码写在一个：

```
main.rs
```

文件中会变得非常难以维护。

例如一个 Web 项目可能包含：

```
用户模块
商品模块
订单模块
数据库模块
认证模块
配置模块
```

如果全部放在一个文件：

```
main.rs
```

最终会变成几千甚至几万行代码。

Rust 提供了模块系统：

```
Module
```

用于：

- • 拆分代码
- • 管理命名空间
- • 控制访问权限
- • 组织大型项目结构

本文将介绍：

- • 什么是 Module
- • mod 关键字
- • 模块嵌套
- • pub 权限控制
- • use 引入模块
- • super 和 self
- • 多文件模块结构
- • 实战项目组织方式

---

## 什么是 Module？

Module（模块）是 Rust 组织代码的基本单位。

它可以包含：

- • 函数
- • 结构体
- • 枚举
- • 常量
- • Trait
- • 子模块

例如：

```
mod user {
    fn login() {
        println!("用户登录");
    }
}
```

这里创建了一个：

```
user
```

模块。

---

## 使用 mod 创建模块

基本语法：

```
mod 模块名 {
    //代码
}
```

例如：

```
fn main() {
    user::login();
}

mod user {
    pub fn login() {
        println!("登录成功");
    }
}
```

输出：

```
登录成功
```

---

## 模块默认私有

Rust 默认：

> 模块内部内容对外不可访问。

例如：

```
mod user {
    fn login(){
        println!("login");
    }
}

fn main(){
    user::login();
}
```

会报错：

```
function \`login\` is private
```

因为：

```
login()
```

默认是私有函数。

---

## 使用 pub 暴露内容

如果希望外部访问，需要：

```
pub
```

例如：

```
mod user {
    pub fn login(){
        println!(
            "用户登录"
        );
    }
}

fn main(){
    user::login();
}
```

输出：

```
用户登录
```

---

## pub 控制访问权限

Rust 有不同级别：

## 私有

默认：

```
fn test(){}
```

只能当前模块使用。

---

## pub

公开：

```
pub fn test(){}
```

外部模块可以访问。

---

## pub(crate)

当前 crate 内可访问：

```
pub(crate) fn test(){}
```

适合项目内部共享。

---

## pub(super)

父模块可访问：

```
pub(super) fn test(){}
```

---

## 模块嵌套

模块可以包含子模块。

例如：

```
mod shop {

    pub mod product {

        pub fn list(){
            println!(
                "商品列表"
            );
        }
    }

}
```

调用：

```
fn main(){

    shop::product::list();

}
```

输出：

```
商品列表
```

结构：

```
shop
 |
 └── product
        |
        └── list()
```

---

## 使用 use 简化路径

如果模块路径很长：

```
shop::product::list();
```

可以使用：

```
use
```

引入。

例如：

```
mod shop {
    pub mod product {
        pub fn list(){
            println!(
                "商品列表"
            );
        }
    }
}

use shop::product;

fn main(){

    product::list();

}
```

---

## 使用 as 重命名

可以给导入内容设置别名：

```
use std::collections::HashMap
    as Map;

fn main(){
    let users:
        Map<String,i32>
        =
        Map::new();
}
```

这样可以避免名称冲突。

---

## self、super 和 crate

Rust 模块中经常使用：

```
self
super
crate
```

---

## self

表示当前模块。

例如：

```
mod user {

    pub fn login(){}

    pub fn test(){

        self::login();

    }

}
```

等价：

```
login();
```

---

## super

表示父模块。

例如：

```
mod app {

    fn config(){
    
    }

    mod user {

        fn login(){
            super::config();
        }
    }
}
```

这里：

```
super::config()
```

访问父模块：

```
app
```

中的函数。

---

## crate

表示当前项目根模块。

例如：

```
crate::config::load();
```

表示：

从项目根目录开始查找。

---

## 文件模块结构

实际项目不会把模块全部写在：

```
main.rs
```

里面。

推荐拆分：

例如：

```
src
 |
 ├── main.rs
 |
 ├── user.rs
 |
 ├── product.rs
 |
 └── db.rs
```

---

## 创建文件模块

user.rs：

```
pub fn login(){
    println!(
        "用户登录"
    );
}
```

main.rs：

```
mod user;

fn main(){
    user::login();
}
```

Rust 会自动加载：

```
user.rs
```

---

## 文件夹模块

大型项目通常：

```
src
 |
 ├── main.rs
 |
 └── user
       |
       ├── mod.rs
       ├── login.rs
       └── profile.rs
```

user/mod.rs：

```
pub mod login;
pub mod profile;
```

login.rs：

```
pub fn login(){
    println!(
        "登录"
    );
}
```

main.rs：

```
mod user;

fn main(){
    user::login::login();
}
```

---

## Rust 2018 新模块方式

新版 Rust 推荐：

```
src
 |
 ├── user.rs
 |
 └── user
       └── login.rs
```

不一定需要：

```
mod.rs
```

例如：

```
mod user;
```

会自动寻找：

```
user.rs
```

或者：

```
user/mod.rs
```

---

## 模块最佳实践

## 一个模块负责一个领域

例如：

不推荐：

```
utils.rs
```

里面放：

- • 用户
- • 商品
- • 数据库
- • 文件

推荐：

```
src
├── user
├── product
├── order
├── database
└── config
```

---

## 实战：简单后台项目结构

例如：

```
shop-system
src
├── main.rs
├── config.rs
├── database.rs
├── user
│   ├── mod.rs
│   ├── login.rs
│   └── register.rs
├── product
│   ├── mod.rs
│   └── service.rs
└── order
    ├── mod.rs
    └── service.rs
```

---

main.rs：

```
mod config;
mod database;
mod user;
mod product;
mod order;

fn main(){
    println!(
        "系统启动"
    );
}
```

---

user/mod.rs：

```
pub mod login;
pub mod register;
```

---

user/login.rs：

```
pub fn login(){
    println!(
        "用户登录"
    );
}
```

调用：

```
user::login::login();
```

---

## 模块与权限设计

大型项目中：

内部实现：

```
fn check_password(){

}
```

不应该暴露。

只暴露：

```
pub fn login(){

}
```

例如：

```
pub mod user {

    pub fn login(){
        check_password();
    }

    fn check_password(){
        println!(
            "检查密码"
        );
    }
}
```

外部只能：

```
user::login();
```

不能：

```
user::check_password();
```

这样可以隐藏实现细节。

---

## Module 与面向对象思想

Rust 没有传统类：

```
class
```

但是可以通过：

```
module
+
struct
+
impl
```

实现类似组织方式。

例如：

```
mod user {

    pub struct User {
        pub name:String,
    }

    impl User {

        pub fn login(&self){
            println!(
                "{} 登录",
                self.name
            );
        }
    }
}
```

调用：

```
let user =
    user::User{
        name:String::from("Tom")
    };
user.login();
```

---

## 常见错误

## 忘记 pub

错误：

```
mod user {
    fn login(){}
}
```

外部无法调用。

解决：

```
pub fn login(){}
```

---

## 模块名称冲突

例如：

```
mod user;

mod user;
```

重复定义会报错。

---

## 循环依赖

例如：

```
user
 ↓
order
 ↓
user
```

容易造成结构混乱。

应该重新设计公共模块。

---

## 本章小结

Rust Module 是管理大型项目代码的重要工具。

通过本文，我们学习了：

- • 创建模块
- • mod 关键字
- • 模块嵌套
- • pub 权限控制
- • use 导入
- • self、super、crate
- • 文件模块结构
- • 多文件项目组织
- • 实际项目目录设计

可以记住：

> Module 负责代码组织。

> pub 负责控制访问权限。

> 一个模块应该负责一个明确领域。

良好的模块设计，是开发大型 Rust 项目的基础。

---

## 下一篇预告

下一篇将学习：

## Rust Package 与 Crate 详解

内容包括：

- • 什么是 Package
- • 什么是 Crate
- • Binary Crate 与 Library Crate
- • Cargo 项目结构
- • Cargo.toml 作用
- • workspace 工作空间
- • 多 Crate 项目管理
- • 发布自己的 Rust 库
- • 实战：创建模块化项目

Rust 编程实战 · Table of Contents