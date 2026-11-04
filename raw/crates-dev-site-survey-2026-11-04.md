# crates.dev 站点查阅记录（2026-11-04）

> 这是本次查询的查阅笔记，不是原站逐字副本。网页内容可能更新；本站既不是 crates.io，也不是各 crate 的官方文档。原始首页剪藏见 `raw/Rust Crates - Best rust crates by topic & Highest rated rust crates.md`。

## 范围

- 查阅 [首页](https://crates.dev/)及其导航直接链接的 23 个不同站内页面：8 篇单库评论、11 篇主题清单、3 篇通用指南、1 篇运行时比较。首页导航有重复链接，这里按不同 URL 去重。
- 另尝试访问 `/sitemap.xml` 与 `/robots.txt`，浏览工具未能取得；不能证明站点只有这 24 页。外部推广站点与嵌入视频不计入本次站内阅读。

## 单库评论（8）

- [Hyper](https://crates.dev/article/Rust_crate_review_Hyper.html)：HTTP 客户端/服务端；示例使用旧式 `hyper::rt::run` 等接口。
- [Actix-web](https://crates.dev/article/Rust_crate_review_Actixweb.html)：Web 框架、路由、中间件与异步。
- [Tokio](https://crates.dev/article/Rust_crate_review_Tokio.html)：异步运行时、socket、定时器、channel。
- [rustls](https://crates.dev/article/Rust_crate_review_Rustls.html)：TLS；代码混用旧配置 API 和其他版本类型。
- [Diesel](https://crates.dev/article/Rust_crate_review_Diesel.html)：ORM、查询构建、schema；命令与示例未经验证。
- [Rocket](https://crates.dev/article/Rust_crate_review_Rocket.html)：Web 框架；示例写 `rocket = "0.5.0-rc.1"` 却仍使用旧 `rocket::ignite()` 和 nightly feature。
- [Serde](https://crates.dev/article/Rust_crate_review_Serde.html)：序列化、反序列化、derive 与字段属性；示例版本和 feature 需复核。
- [Iron](https://crates.dev/article/10_Rust_crate_review_Iron.html)：旧 Web 框架与 middleware、路由示例；没有当前维护证据。

## 主题清单（11）

- [密码学](https://crates.dev/article/Top_5_Rust_Crates_for_Cryptography.html)：RustCrypto、sodiumoxide、ring、rustls 和名称含糊的 Crypto。
- [游戏开发](https://crates.dev/article/Top_10_Rust_Crates_for_Game_Development.html)：引擎、ECS、图形、窗口、音频、数学和资源处理混列。
- [Web 开发 A](https://crates.dev/article/Top_10_Rust_crates_for_web_development.html)、[Web 开发 B](https://crates.dev/article/Top_10_Rust_Crates_for_Web_Development.html)：两个不同 URL 的十项清单，框架、HTTP、模板、序列化、TLS 和数据库混列；名单并不相同。
- [数据科学](https://crates.dev/article/Top_10_Rust_Crates_for_Data_Science.html)：ndarray、csv、serde、rayon、统计、绘图和线性代数等。
- [GUI](https://crates.dev/article/Top_10_Rust_Crates_for_GUI_Development.html)：GTK、Qt、Iced 等，也把绑定项目与 GUI toolkit 混称为 crate。
- [网络](https://crates.dev/article/Top_5_Rust_Crates_for_Networking.html)：Tokio、Hyper、rustls、Actix、Quiche；其中 Quiche 被称为 TLS 库，分类需要复核。
- [机器学习](https://crates.dev/article/Top_5_Rust_Crates_for_Machine_Learning.html)：ndarray、tch-rs、rusty-machine 等；具体名称与现行状态待核实。
- [机器人](https://crates.dev/article/Top_5_Rust_Crates_for_Robotics.html)：GPIO、embedded HAL、ROS 与模拟；`rust-embedded-hal` 等名字需和注册表核对。
- [图像处理](https://crates.dev/article/Top_10_Rust_Crates_for_Image_Processing.html)：image、imageproc 与若干名称未核实的项目，混入 OpenGL 渲染库。
- [音频](https://crates.dev/article/Top_5_Rust_Crates_for_Audio_Processing.html)：RustFFT、Hound、CPAL、rodio、rust-portaudio；Hound 的格式支持声明需核实。

## 通用指南与比较（4）

- [crate 管理入门](https://crates.dev/article/A_beginners_guide_to_Rust_crate_management.html)：Cargo.toml、版本、锁文件、更新；把 rustup 与 Cargo 一并称作包管理器。
- [如何选 crate](https://crates.dev/article/How_to_choose_the_right_Rust_crate_for_your_project.html)：建议检查文档、测试、兼容性、性能、维护活跃度与社区。
- [如何贡献](https://crates.dev/article/How_to_contribute_to_Rust_crates_and_improve_the_community.html)：从使用反馈、报 issue、PR、文档到维护者工作。
- [Tokio 与 async-std](https://crates.dev/article/Rust_crate_comparison_Tokio_vs_asyncstd.html)：泛泛比较性能与易用性；无基准、版本或当前维护证据。

## 证据核对

- 首页声称 crates.io 对所有发布的 crate 提供评分与评论、站内每个推荐都经过测试审查，但页面没有展示可复核的方法或逐库报告。
- [Rust 官方《Packages and Crates》](https://doc.rust-lang.org/stable/book/ch07-01-packages-and-crates.html)区分 package 与 crate；首页和一些文章将两者混称。
- [rustup 官方书](https://rust-lang.github.io/rustup/)将 rustup 定义为工具链安装/切换工具；包依赖由 Cargo 管理。
- [Rocket 官方 v0.5 升级说明](https://rocket.rs/guide/v0.5/upgrading/)明确移除旧 feature、以 `rocket::build()` 取代 `ignite()`；本站 Rocket 评论的“0.5”示例不能按字面复用。
- [rustls 当前 ConfigBuilder 文档](https://docs.rs/rustls/latest/rustls/struct.ConfigBuilder.html)采用 `ServerConfig::builder()` / `ClientConfig::builder()`；本站 rustls 评论的 `0.19.0` 片段不代表当前 API。
- [Hyper v1 升级指南](https://hyper.rs/guides/1/upgrading/)说明 v1 的客户端/服务端接入方式；本站 Hyper 评论中的旧式 runtime 示例不能当作现行用法。

## 结论

可把该站用于发现关键词和待比较的方向；选型、版本、功能、安全、维护、作者与 API 示例，应回到 crates.io、项目官方文档/仓库及目标版本测试。上述页面均未作为单个库的官方 ingest 来源。
