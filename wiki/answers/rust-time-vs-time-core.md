---
title: "time 和 time-core 分别包含什么？应用该依赖谁？"
type: answer
created: 2026-11-02
updated: 2026-11-02
tags: [rust, cargo, date-time]
status: growing
sources: [raw/time-vs-time-core-official-research-2026-11-02.md, raw/time-rust-official-research-2026-11-01.md, raw/time-core-rust-official-research-2026-11-01.md]
---

# time 和 time-core 分别包含什么？

> 归档自 2026-11-02 的后续查询；前一问见 [[rust-crate-core-split]]。

## 回答

| crate | 具体内容 | 面向谁 |
| --- | --- | --- |
| [[time-rust]] | `Date`、`Time`、`PlainDateTime`、`OffsetDateTime`、`UtcOffset`、`SignedDuration`、`Month`、`Weekday` 等日期时间类型；按 feature 提供宏、格式化、解析和 serde 支持。 | 应用与其他库的主要入口 |
| [[time-core-rust]] | `unit` 模块中的时间单位换算，以及 `util` 中的辅助函数。 | `time` 等同项目 crate 的内部实现 |

`time-core` 官方文档明确说它是实现细节，不建议直接依赖。应用若在自己的代码中使用 `time::...`，通常只需在 `Cargo.toml` 声明 `time`；Cargo 会解析并编译它所需的 `time-core`。例如：

```toml
[dependencies]
time = "0.3"
```

```rust
let now = time::OffsetDateTime::now_utc();
```

如果使用 `time::macros`、格式化或解析接口，需按文档启用相应 feature，例如 `time = { version = "0.3", features = ["macros", "formatting", "parsing"] }`。以上示例未在本机编译；具体可用 API 取决于项目锁定的版本和 feature。若应用源码不直接引用 `time`，只是其他依赖在内部使用它，则应用无需为此再声明 `time`。

## 依据

- `raw/time-vs-time-core-official-research-2026-11-02.md`「time 的公开内容」「time-core 的公开内容及定位」「依赖声明」。
- [[time-rust]]、[[time-core-rust]]；前一问 [[rust-crate-core-split]]。

## 后续

- 需要 `no_std`、`local-offset`、serde 或较大年份范围时，按当前发布版本核对 feature 与平台条件。
