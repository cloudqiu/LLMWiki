---
title: "Rust 错误处理最佳实践：构建可靠的应用程序"
source: "https://mp.weixin.qq.com/s?__biz=MzYzODE1NzUzMw==&mid=2247484512&idx=1&sn=6f496e4f5c1f0096085135e2ed853e67&chksm=f0e753d2c790dac4601b3e9d18f0d41672cab7f0a503cd2a5c4c22a052167ca0e386ebdf32da&cur_album_id=4602071361631748097&scene=189#wechat_redirect"
author:
published:
created: 2026-11-05
description: "《Rust 编程实战》系列第 24 篇在前面的章节中，我们学习了 Rust 的三种错误处理方式：Option"
tags:
  - "clippings"
---
程序员爱钓鱼 *Jul 29, 2026, 7:57 AM*

> 《Rust 编程实战》系列第 24 篇

在前面的章节中，我们学习了 Rust 的三种错误处理方式：

```
Option<T>
```

表示：

> 一个值可能存在，也可能不存在。

例如：

```
HashMap::get()
Vec::get()
```

---

```
Result<T, E>
```

表示：

> 一个操作可能成功，也可能失败。

例如：

```
文件读取
网络请求
数据库查询
```

---

```
panic!
```

表示：

> 程序遇到了无法继续安全运行的问题。

例如：

```
数组越界
违反内部逻辑
不可恢复错误
```

实际开发中，如何合理组合这些方式，决定了 Rust 项目的稳定性。

本文将介绍：

- • Rust 错误处理设计原则
- • Option、Result、panic 使用场景
- • 自定义错误类型
- • 错误传播
- • anyhow 与 thiserror
- • Web 项目错误处理方案
- • 生产环境最佳实践

---

## 错误处理三原则

在 Rust 项目中，可以遵循：

## 1\. 可预期错误使用 Result

例如：

读取配置：

```
use std::fs;

fn load_config()
    -> Result<String, std::io::Error>
{
    let content =
        fs::read_to_string(
            "config.toml"
        )?;

    Ok(content)
}
```

文件不存在属于正常失败情况：

```
Err(文件不存在)
```

程序可以处理。

---

## 2\. 不存在的数据使用 Option

例如：

查询用户：

```
fn find_user(
    id:u64
)
-> Option<String>
{
    match id {

        1 => Some(
            String::from("Tom")
        ),

        _ => None,

    }
}
```

用户不存在不是错误，只是没有查询结果。

---

## 3\. 程序逻辑错误使用 panic

例如：

```
fn divide(
    a:i32,
    b:i32
)
->i32{

    if b==0 {

        panic!(
            "除数不能为0"
        );

    }

    a/b
}
```

这里：

```
b=0
```

违反函数设计规则。

---

## 不要使用 String 作为所有错误

初学 Rust 时，经常这样写：

```
Result<User,String>
```

例如：

```
fn login()
-> Result<(),String>
{

    Err(
        String::from(
            "密码错误"
        )
    )

}
```

小项目可以。

但是大型项目会产生问题：

- • 无法区分错误类型
- • 无法统一处理
- • 不方便日志记录
- • 不方便国际化

更推荐：

```
enum AppError {

    UserNotFound,

    PasswordWrong,

    DatabaseError,

}
```

---

## 自定义错误类型

示例：

```
#[derive(Debug)]
enum UserError {

    NotFound,

    InvalidPassword,

    DatabaseFailure,

}
```

函数：

```
fn login(
    username:&str
)
-> Result<(),UserError>
{

    if username.is_empty(){

        return Err(
            UserError::NotFound
        );

    }

    Ok(())

}
```

调用：

```
match login("") {

    Ok(_) => {
        println!("登录成功");
    }

    Err(error)=>{
        println!(
            "{:?}",
            error
        );
    }

}
```

这样错误结构更加清晰。

---

## 使用? 简化错误传播

传统写法：

```
let result =
    read_file();

match result {

    Ok(data)=>{

    }

    Err(error)=>{

        return Err(error);

    }

}
```

代码比较冗长。

Rust 推荐：

```
let data =
    read_file()?;
```

完整示例：

```
fn process()
-> Result<String,std::io::Error>
{

    let text =
        std::fs::read_to_string(
            "data.txt"
        )?;

    Ok(text)

}
```

`?` 会自动：

成功：

```
Ok(value)
```

继续执行。

失败：

```
Err(error)
```

直接返回。

---

## 错误转换

实际项目中，一个函数可能调用多个模块：

例如：

```
HTTP接口
    |
业务层
    |
数据库
    |
文件系统
```

每层都有自己的错误。

例如数据库：

```
DatabaseError
```

文件：

```
IoError
```

最终统一：

```
AppError
```

示例：

```
enum AppError {

    Io(
        std::io::Error
    ),

    Database(
        String
    ),

}
```

转换：

```
impl From<std::io::Error>
for AppError {

    fn from(
        error:std::io::Error
    )
    -> Self {

        AppError::Io(error)

    }
}
```

之后：

```
read_file()?
```

可以自动转换错误类型。

---

## thiserror：推荐用于库项目

大型 Rust 项目通常使用：

```
thiserror
```

创建清晰错误类型。

Cargo.toml：

```
[dependencies]
thiserror="2"
```

示例：

```
use thiserror::Error;

#[derive(Error,Debug)]
enum UserError {

    #[error("用户不存在")]
    NotFound,

    #[error("数据库错误")]
    DatabaseError,

}
```

使用：

```
return Err(
    UserError::NotFound
);
```

优势：

- • 自动实现 Error trait
- • 错误信息统一
- • 适合长期维护

---

## anyhow：推荐用于应用程序

如果开发：

- • 命令行工具
- • 后台服务
- • Web 应用

可以使用：

```
anyhow
```

Cargo.toml：

```
[dependencies]
anyhow="1"
```

示例：

```
use anyhow::Result;

fn run()
-> Result<()>
{

    let data =
        std::fs::read_to_string(
            "config.txt"
        )?;

    println!("{}", data);

    Ok(())

}
```

anyhow 自动处理错误链。

适合：

应用层。

---

## thiserror 和 anyhow 区别

| 类型 | thiserror | anyhow |
| --- | --- | --- |
| 主要用途 | 库开发 | 应用开发 |
| 错误类型 | 明确定义 | 动态包装 |
| 是否暴露错误 | 是 | 通常隐藏 |
| 适合场景 | SDK、框架 | 服务端程序 |

实际项目常见组合：

```
底层库
 ↓
thiserror

业务应用
 ↓
anyhow
```

---

## Web 服务错误设计

例如 Rust Web 项目：

```
Controller
    |
Service
    |
Repository
    |
Database
```

推荐：

数据库层：

```
DatabaseError
```

业务层：

```
BusinessError
```

接口层：

转换成：

```
{
    "code":400,
    "message":"用户不存在"
}
```

不要直接返回数据库错误。

---

## 日志记录错误

错误处理不能只有：

```
println!
```

生产环境推荐：

```
tracing
```

例如：

```
tracing::error!(
    "database error: {:?}",
    error
);
```

记录：

- • 错误类型
- • 请求ID
- • 用户信息
- • 调用位置

方便线上排查。

---

## 不要滥用 panic

错误：

```
fn create_user(
    name:String
){

    if name.is_empty(){

        panic!(
            "用户名为空"
        );

    }

}
```

用户名为空属于业务错误。

应该：

```
fn create_user(
    name:String
)
-> Result<(),UserError>
{

    if name.is_empty(){

        return Err(
            UserError::InvalidName
        );

    }

    Ok(())

}
```

---

## 错误处理流程设计

一个成熟项目通常：

```
用户输入
   |
   v
Result
   |
业务校验
   |
Result
   |
数据库
   |
Result
   |
统一错误转换
   |
HTTP响应
```

不要：

```
用户输入错误
       |
       panic
       |
       服务崩溃
```

---

## 实战：统一业务错误

```
use thiserror::Error;

#[derive(Error,Debug)]
enum AppError {

    #[error("用户不存在")]
    UserNotFound,

    #[error("权限不足")]
    PermissionDenied,

    #[error("数据库错误")]
    DatabaseError,

}

fn delete_user(
    id:u64
)
-> Result<(),AppError>
{

    if id==0 {

        return Err(
            AppError::UserNotFound
        );

    }

    Ok(())

}

fn main(){

    match delete_user(0){

        Ok(_)=>{
            println!("删除成功");
        }

        Err(e)=>{
            println!("{}",e);
        }

    }

}
```

输出：

```
用户不存在
```

---

## 错误处理最佳实践总结

## 普通业务错误

使用：

```
Result<T,E>
```

例如：

- • 登录失败
- • 参数错误
- • 数据不存在

---

## 查询不到数据

使用：

```
Option<T>
```

例如：

- • 用户查询
- • 配置查询
- • 缓存查询

---

## 不可恢复错误

使用：

```
panic!
```

例如：

- • 程序内部 bug
- • 不可能状态

---

## 项目错误设计

推荐：

```
底层库
    thiserror

业务应用
    anyhow

接口层
    统一转换
```

---

## 本章小结

Rust 的错误处理核心思想：

> 错误不是异常，而是程序状态的一部分。

通过本文，我们学习了：

- • Result、Option、panic 的职责
- • 自定义错误类型
- • 错误传播
- •? 运算符
- • thiserror
- • anyhow
- • Web 项目错误设计
- • 生产环境错误处理规范

掌握错误处理后，Rust 程序不仅安全，而且更容易维护。

---

## 下一篇预告

下一篇进入 Rust 项目组织：

## Rust Module 模块系统详解

内容包括：

- • 什么是 Module
- • mod 关键字
- • 文件模块结构
- • pub 权限控制
- • use 引入
- • crate 与 package
- • super 与 self
- • 多文件项目组织
- • 实战：创建项目模块结构

Rust 编程实战 · Table of Contents