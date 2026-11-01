---
title: "SQLite 聚合 FILTER 子句的版本边界"
type: concept
created: 2026-11-01
updated: 2026-11-01
tags: [sqlite, sql, aggregate]
status: growing
sources: ["raw/微信为什么使用 SQLite 保存聊天记录？.md"]
---

# SQLite 聚合 FILTER 子句的版本边界

## 定义

`FILTER (WHERE ...)` 让聚合只处理满足条件的输入行。2018 年的 [[sqlite-2018-dialect-clipping]] 把它用于窗口聚合；[现行 SQLite 聚合函数文档](https://www.sqlite.org/lang_aggfunc.html)同样支持普通聚合。

## 机制 / 要点

```sql
SELECT SUM(revenue) FILTER (WHERE product = 1) AS product_revenue
FROM sales;
```

该示例面向 SQLite 3.30.0 及之后支持普通聚合 `FILTER` 的版本；尚未在本机执行。

> [!warning] 矛盾：旧资料的版本限制
> `raw/微信为什么使用 SQLite 保存聊天记录？.md` 115–140 行说普通 `GROUP BY` 聚合不支持 `FILTER`；这在该文讨论的 2018 年版本范围内成立，但[SQLite 3.30.0 官方发布说明](https://www.sqlite.org/releaselog/3_30_0.html)已明确新增聚合函数 `FILTER`。[[sqlite-2018-dialect-clipping]] 同时记录此处过时结论。

## 边界

- 应先确认运行环境的 SQLite 版本；不能把 2018 年跨数据库支持矩阵当作当前能力表。
- 剪藏文件标题中的“微信聊天记录”没有得到正文支持；不能据此推断微信的存储实现。

## 相关页面

- [[sqlite-2018-dialect-clipping]]
