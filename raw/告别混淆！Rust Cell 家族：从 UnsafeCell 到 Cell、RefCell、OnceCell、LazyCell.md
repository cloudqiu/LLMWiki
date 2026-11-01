---
title: "告别混淆！Rust Cell 家族：从 UnsafeCell 到 Cell、RefCell、OnceCell、LazyCell"
source: "https://mp.weixin.qq.com/s/7jZdthg4EHeOy8_Acf4iUQ"
author:
  - "[[锈铁匠]]"
published:
created: 2026-11-01
description: "Rust 的内部可变性都建立在 UnsafeCell 之上。Cell、RefCell、OnceCell、LazyCell 分别适合什么场景？"
tags:
  - "clippings"
---
锈铁匠 锈铁匠铺 *Oct 28, 2026, 8:31 PM*

以Cell为代表的封装类型是Rust内部可变性的代表，它的出现和可变借用只能存在一份的限制有关。有句顺口溜，“可变不共享，共享不可变”形象地表达了这个限制。在复杂场景中，程序员有时希望创建一个变量的多个引用，还要通过这些引用安全地修改这个变量。而Rust的可变引用和不可变引用不能共存，所以常规的引用语法无法达到这个目的。面对此类问题，Rust的一贯策略是提供一个全新的封装类型Wrapper，一旦对类型T进行封装，就意味着对T的访问多了一道手续，就像从一个专门的入口进去才能完成访问。而类型封装的秘密就存在于这道手续中，此手续是否安全可靠由封装的设计者做出承诺。

## 一、UnsafeCell封装

针对“可变不共享”这个强加的限制，Rust自身又提供了Cell系列封装类型来解除这个限制，从而使被封装的内部数据可变，这种性质叫作内部可变性，具备内部可变性的数据类型叫作内部可变类型。Cell家族类型是内部可变性的代表，而UnsafeCell\<T>是这些安全类型的底层类型。换句话说，如果一个类型内部定义了UnsafeCell\<T>，那么这个类型就是内部可变类型。标准库源代码对Cell相关类型的定义在文件core/src/cell.rs中，UnsafeCell\<T>定义如下：

![Image](https://mmbiz.qpic.cn/mmbiz_png/vRuscQFQcKwOqU9ElgqTWCR0Z80Y5LQ8diaXWiatO1v67UrQdMTEMRJuiczblDUmIfq0Q5YFY4BwAhTSOlazItFe5Zkk12kaHE8icicJ2QHRwP4k/640?wx_fmt=png&from=appmsg&watermark=1&tp=webp&wxfrom=5&wx_lazy=1#imgIndex=0)

UnsafeCell\<T>通常不在用户代码中直接出现，因为它明确告知了Unsafe。对用户更有价值的类型是Cell\<T>、RefCell\<T>、OnceCell\<T>和LazyCell\<T>封装。

## 二、Cell封装

Cell是一个结构体类型, 内部封装了一个类型T的值字段。为了写这个值，Cell提供了专门的set()方法，因为这是标准库的定义，标准库的设计者——顶级程序员，对外号称保证set()方法操作的安全性，用户无需担心，尤其是Linux源码为Rust语言提供了值得信赖的背书。

![Image](https://mmbiz.qpic.cn/sz_mmbiz_png/vRuscQFQcKxRgicrtSIMCOLKR93t3AjWLmQeLmAApyCjpbWniaSgfG7viabb8qs0ZODBqUmJAq01ZaI491eKBYib1joQhur8ZX3NhNjtjaWRsho/640?wx_fmt=png&from=appmsg&watermark=1&tp=webp&wxfrom=5&wx_lazy=1#imgIndex=1)

struct Cell是最外一层封装，内部字段value类型为UnsafeCell，或者说Cell的底层封装为UnsafeCell封装。Cell在UnsafeCell的基础之上，提供安全修改内部变量的方法。然而Cell的实现部分并没有提供对内部值的引用，因此仅仅通过Cell无法调用内部变量的方法，自然Cell的可使用场景就受到了一些限制。

![Image](https://mmbiz.qpic.cn/mmbiz_png/vRuscQFQcKyaSThkE3mxK5uic4qVBrqNpy9LvCN2qFbUBMDyByqAH6pwSr0sIOhFKcEdp7MGM1icXD6ibbptOPfRGXZNOLTcTItewibHjWtljGw/640?wx_fmt=png&from=appmsg&watermark=1&tp=webp&wxfrom=5&wx_lazy=1#imgIndex=2)

## 三、RefCell封装

因为Cell没有提供内部变量的安全引用，才有了RefCell封装类型。RefCell的实现依赖于Cell和UnsafeCell，还是在文件core/src/cell.rs中，其源代码定义如下：

![Image](https://mmbiz.qpic.cn/mmbiz_png/vRuscQFQcKx1ryLcFGWQbmFHyNvMT3mRBf1stCH48NMibxRib33uxCgynNUicIorAmKttibkhzlGrZ5sWSCfsA8B3dZOr1YExGjCuOS7abedvg4/640?wx_fmt=png&from=appmsg&watermark=1&tp=webp&wxfrom=5&wx_lazy=1#imgIndex=3)

RefCell实现了Borrow和BorrowMut特征，用户据此可以获取内部变量的不可变引用和可变引用，相当于找到一个可读写的句柄，从而得以使用内部变量类型提供的各种方法。从某种角度看，RefCell封装类型显得更加务实，它是内部可变类型的典型代表。

UnsafeCell、CellRefCell在Rust1.0版本时已就绪，后续演进版本又提供了OnceCell和LazyCell封装。

## 四、OnceCell封装

OnceCell: 2023年6月的Rust 1.70引入，Once一词和FnOnce类型闭包中闭包只能被执行一次含义相同，OnceCell封装意味着只能对内部值进行一次写操作。

![Image](https://mmbiz.qpic.cn/sz_mmbiz_png/vRuscQFQcKyGNAGKxVaKedusp07hscEau2DBwc7XdUKM93LfeWf4Jqysic99kOS8FVvy50dEg8M8nnrNYpTliaIZEnfcpXIsqFdK24ymmlPl8/640?wx_fmt=png&from=appmsg&watermark=1&tp=webp&wxfrom=5&wx_lazy=1#imgIndex=4)

## 五、LazyCell封装

LazyCell: 2024年7月的Rust 1.80引入，Lazy一词表示懒惰，我们可以再次和迭代器闭包操作联系起来，迭代器状态推进是惰性的，只在有消费需求的时候才会把生产朝前推进一步。被LazyCell封装的值，只在LazyCell被首次访问时才执行初始化。为此文件core/src/cell/lazy.rs还单独定义了enum State来追踪状态。如果想自己写一个初始化状态机逻辑，LazyCell.rs的实现是很好的参考代码。

![Image](https://mmbiz.qpic.cn/sz_mmbiz_png/vRuscQFQcKzIxMhibpOlCAUG6tmYzw1TSMictf6SMOUdfJFVzocnGVegUzgkEcXhDtS33nMkds3lHbeNfm3AUsXDibA4wHicr0aOuk9Vt5ymaak/640?wx_fmt=png&from=appmsg&watermark=1&tp=webp&wxfrom=5&wx_lazy=1#imgIndex=5)

## 总结

综合Cell、RefCell以及后来的OnceCell和LazyCell，它们都是在UnsafeCell基础上的进一步封装，这些封装类型的相互依赖关系如下：

![Image](https://mmbiz.qpic.cn/sz_mmbiz_png/vRuscQFQcKzf07qdcibbtyC3gyppkD5g0iaJSOo9tMGvMMLchZRx0NBVTia7l9SFZziaxtyvy3UvqOVRACibXa0R4ndLfZg2rO9OWysicwnLqx0FU/640?wx_fmt=png&from=appmsg&watermark=1&tp=webp&wxfrom=5&wx_lazy=1#imgIndex=7)

从这一连串的设计中还可以体会到Rust设计的良苦用心，传统编程中变量初始化在多线程中给程序员带来的挑战，到了Rust这里都逐一进行了拆解，以尝试寻求更优解，直至写入标准库来方便广大程序员。从稳定版本1.70到1.80，在一年出头的时间里就能完成，可以说稳定的新feature都在第一时间推送给了用户，因此保持更新Rust到最新版本对这门语言的学习是有很多好处的。

往期回顾 · Table of Contents