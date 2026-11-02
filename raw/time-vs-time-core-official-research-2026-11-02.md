# time 与 time-core 的具体内容：官方资料查阅记录

> 2026-11-02 查阅。本文为研究笔记，不是官方原文副本；代码示例未在本机编译。

## time 的公开内容

- [time 0.3.55 文档](https://docs.rs/time/latest/time/) 的「Structs / Enums」：`Date`、`Time`、`PlainDateTime`、`OffsetDateTime`、`UtcDateTime`、`UtcOffset`、`SignedDuration`、`Timestamp`、`Month`、`Weekday`；`Duration` 与 `PrimitiveDateTime` 为旧名称的类型别名。
- 同一文档的「Modules」：错误、扩展 trait、时间单位与工具；`format_description`、`formatting`、`parsing`、`macros`、`serde` 等模块受相应 feature 控制。
- 同一文档的「Feature flags」：默认启用 `std`（从而启用 `alloc`）；`macros`、`formatting`、`parsing` 等按需启用。

## time-core 的公开内容及定位

- [time-core 0.1.9 文档](https://docs.rs/time-core/latest/time_core/) 明确说这是 `time` 的实现细节，不建议直接依赖。公开列表主要是 `unit`（时间单位之间换算）和 `util`（辅助函数）模块。
- 它不提供 `time::Date`、`time::OffsetDateTime` 等应用常用入口。

## 依赖声明

- [time/Cargo.toml](https://github.com/time-rs/time/blob/main/time/Cargo.toml)：`time-core` 是 `time` 的普通依赖；`time-macros` 是可选依赖，由 `macros` feature 启用。
- 因而直接在应用源码使用 `time::...` 时，应用声明 `time` 依赖；Cargo 会解析其内部依赖，无需同时声明 `time-core`。若用 `time::macros` 或格式化/解析接口，启用对应 feature。
