# Rust crate 依赖 re-export 官方资料查阅记录（2026-11-05）

本文件是查阅笔记，不是官网原文副本。问题：为什么 Rust crate 常把所依赖的第三方库 re-export？

## 查阅资料

- Rust Book，`pub use` 与公共 API：https://doc.rust-lang.org/book/ch07-04-bringing-paths-into-scope-with-the-use-keyword.html
- Rust Book，发布 crate 时重新导出依赖定义：https://doc.rust-lang.org/book/ch14-02-publishing-to-crates-io.html
- Rust Reference，`use` 声明与可见性：https://doc.rust-lang.org/reference/items/use-declarations.html
- Cargo Book，SemVer 兼容性：https://doc.rust-lang.org/cargo/reference/semver.html
- Cargo Book，依赖解析与多版本类型风险：https://doc.rust-lang.org/cargo/reference/resolver.html
- Cargo Book，dependency features 的重新导出：https://doc.rust-lang.org/cargo/reference/features-examples.html
- Rust API Guidelines，公开依赖的稳定性：https://rust-lang.github.io/api-guidelines/necessities.html
- smol 官方 API 文档：https://docs.rs/smol/2.0.2/smol/
- 本库原有 smol 官方研究：`raw/smol-rust-official-research-2026-11-04.md`。

## 核对结果

- `pub use` 可把另一个路径下的公开 item 作为本 crate 的公开名字提供，形成与内部模块结构不同的外部 API。Rust Book 还明确举出将依赖的定义纳入本 crate 公共 API 的情形。
- 官方 smol 文档明确说明该 crate 主要重新导出若干较小的 async crate；因此“facade / 统一入口”有具体实例。
- Cargo 的 SemVer 指南把移动或删除公开 item 视为破坏性变更；旧路径可借 `pub use` 保留。若公开 API 使用依赖的类型，该依赖也是 public dependency，升级风险须计入本 crate 的版本策略。
- Cargo resolver 文档说明同名 crate 的不兼容版本可能同时出现，其类型对编译器而言不同，即使名字相同。re-export 提供一个明确的类型路径，但不会自动合并依赖图里所有版本。
- Cargo Book 还说明可以在本 crate 的 feature 中转发依赖 feature，让使用者不必直接配置那个依赖；这与 `pub use` 重新导出 Rust item 是两种不同机制。

## 边界

- 统一入口、版本匹配和降低依赖配置负担是对这些官方机制与 smol 实例的归纳，不意味着所有 crate 都出于相同动机。
- 仅把内部实现依赖公开给用户，会扩大需要长期维护的 API 面；应优先选择用户确实要命名或配置的类型、trait、宏及 feature。
