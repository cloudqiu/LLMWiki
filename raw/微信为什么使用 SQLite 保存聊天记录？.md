---
title: "微信为什么使用 SQLite 保存聊天记录？"
source: "https://mp.weixin.qq.com/s/genD-1mZyrm27CVwW76wtw"
author:
published:
created: 2026-10-07
description:
tags:
  - "clippings"
---
将 小哈学Java设为“ **星标** **⭐** ”

第一时间收到文章更新

![图片](https://mmbiz.qpic.cn/mmbiz_png/sTnayibHfVq7iaS1l2f7sxwxXEZHKcpjJmib6F5tDxnEqMTGCVubyGa9dUzA7ib8IffsH2dIicNEicfIQMc2ykdRF3qg/640?wx_fmt=png&random=0.7342939506927444&wxfrom=5&wx_lazy=1&tp=webp#imgIndex=0) 来源：https://modern-sql.com/blog/2019-01/sqlite-in-2018

**在线 Java 面试刷题（已更新334题，图文并茂）：https://www.quanxiaoha.com/java-interview**

> “
> 
> SQLite 是一个被大家低估的数据库，但有些人认为它是一个不适合生产环境使用的玩具数据库。事实上，SQLite 是一个非常可靠的数据库，它可以处理 TB 级的数据，但它没有网络层。接下来，本文将与大家共同探讨 SQLite 在过去一年中最新的 SQL 功能。

SQLite "只是"一个库，它不是传统意义上的服务器。因此，在某些场合下，它确实不合适。但是，在相当多的其他场合，它却是最合适的选择。SQLite 号称是部署和使用最广泛的数据库引擎。我认为这很有可能，因为 SQLite 没有版权的限制。无论何时，只要开发者想使用 SQL 在文件中存储结构化的数据，SQLite 应是首选方案。

SQLite 的 SQL 方言也非常强大。它比 MySQL 早四年就开始支持 with 语句。最近，它还实现了对于窗口函数的支持，这仅仅比 MySQL 晚五个月。

接下来，本文将介绍 SQLite 在 2018 年新增加的 SQL 功能，也就是 SQLite 从版本 3.22.0 到 3.26.0 所新增加的 SQL 功能。

具体内容包括：

1. 布尔字面量和判断
2. 窗口函数
3. Filter 子句
4. Insert … on conflict（"Upsert"）
5. 重命名列
6. 在 Modern-SQL.com 上接下来

## 布尔变量和判断

SQLite 支持"假"布尔值：它接受 Boolean 作为类型的名称，但它将其当作整数看待（这一点非常类似于 MySQL）。真值 true 和 false 分别由数值 1 和 0 表示（这一点和 C 语言一样）。

从版本 3.23.0 开始，SQLite 将关键字 true 和 false 分别用数字 1 和 0 表示，并支持 is \[not\] true | false 的判断语句。现在，它不再支持关键字 unknown。开发者可以使用空值 null 来代替，因为 unknown 和 null 的布尔值是一样的。

在 INSERT 和 UPDATE 语句中，字面量 true 和 false 可以大大提高 values 和 set 子句的可读性。

is \[not\] true | false 这个判断语句很有用，它与比较操作的含义不一样：

我们来比较一下

```
WHERE c <> FALSE
```

和

```
WHERE c IS NOT FALSE
```

在上面的例子中，如果 c 是 null，那么 c <> false 的结果是 unknown。

这是因为 WHERE 子句只接受结果为 true 的值，它会过滤掉结果为 false 或 unknown 的值。这样，它就会把对应的行从结果中去掉。

与此相对应，如果 c 是 null，那么，c is not false 的判断结果是 true。因此，第二个 WHERE 子句也将包含 c 是 null 的行。

要达到同样的效果，您可以采用的另外一种方法是增加单独处理 null 值的子句。也就是使用语句:

```
WHERE c <> FALSE
   OR c IS NULL
```

这种形式的语句更长并且有一些冗余语句（c 被使用了两次）。长话短说，可以使用 is not false 判断来替代这个 or…is-null 的语句。更详细的内容，请参考 "Binary Decisions Based on Three-Valued Results"。

SQLite 中对布尔字面量和布尔判断的支持现在和其他开源数据库接近，唯一的差距是 SQLite 不支持 is\[not\] unknown（你可以使用 is \[not\] null 来代替）。有趣的是，这些功能在下面提到的商用产品中还不可用。

![各数据库布尔字面量支持情况对比](https://mmbiz.qpic.cn/mmbiz_png/sTnayibHfVq7iaS1l2f7sxwxXEZHKcpjJmXsL28BsFcd6KXH9kM3u0AGTBPZM38ibFZWUsticVeWn5oR4X8Gak3dkg/640?wx_fmt=png&tp=webp&wxfrom=5&wx_lazy=1#imgIndex=1)

各数据库布尔字面量支持情况对比

- 0：只支持 true，false。不支持 notknown，如果需要，用 null 代替
- 1：不支持 is \[not\] unknown，如果需要，用 is \[not\] null 代替

## 窗口函数

SQLite 3.25.0 引入了窗口函数。如果你知道窗口函数，那么也知道这是一件大事。如果你不了解窗口功能，请你自己学习如何使用。这篇文章不会具体解释窗口函数，但请相信：它是最重要的"现代"SQL 特性。

SQLite 对 over 子句的支持与其他数据库非常接近。唯一值得注意的限制是 range 语句不支持数字或间隔距离（仅支持 current row 和 unbounded preceding|following）。在发布 sqlite 3.25.0 时，SQL Server 和 PostgreSQL 具有同样的限制。PostgreSQL 11 消除了这一限制。

![各数据库 over 子句支持情况对比](https://mmbiz.qpic.cn/mmbiz_png/sTnayibHfVq7iaS1l2f7sxwxXEZHKcpjJmactBLj2BKMwiacpnC9XwV179WQs8PO5Szlb211YrZjFq22NYkucpRjw/640?wx_fmt=png&tp=webp&wxfrom=5&wx_lazy=1#imgIndex=2)

各数据库 over 子句支持情况对比

- 0：没有变化
- 1：Range 范围定义不支持 datetime 类型
- 2：Range 范围不接受关键字（只支持 unbounded 和 current row）

SQLite 对于窗口函数的支持在业界是领先的。它不支持的功能在其他一些主要产品中也同样不支持（在聚合中语句中的 distinct，width\_bucket，respect|ignore nulls 和 from first|last 等语句）。

![各数据库窗口函数支持情况对比](https://mmbiz.qpic.cn/mmbiz_png/sTnayibHfVq7iaS1l2f7sxwxXEZHKcpjJm2gRRhzhXSkbu8X2so4JAcRFTjl5SaMHPKRFyTODvpVcgnW4aj6kVxQ/640?wx_fmt=png&tp=webp&wxfrom=5&wx_lazy=1#imgIndex=3)

各数据库窗口函数支持情况对比

- 0：同样没有 ORDER BY 语句
- 1：不允许负偏移量，nulls 的特定处理：lead(, 'IGNORE NULLS')，这里是字符串参数
- 2：没有缺省值（第三个参数），不支持 respect|ignore nulls 语句
- 3：不允许负偏移量，不支持 ignore nulls 语句
- 4：不允许负偏移量
- 5：不支持 respect|ignore nulls 语句
- 6：不允许负偏移量，不支持 respect|ignore nulls 语句
- 7：nulls 的特定处理：first\_value(, 1, null, 'IGNORE NULLS')，这里是字符串参数。
- 8：不支持 ignore nulls 语句
- 9：不支持 ignore nulls 语句和 from last 语句

## 过滤语句

虽然 filter 语句只是语法糖——你也可以很容易地使用表达式来获得相同的结果——我认为它也是必不可少的语法糖，因为它能使人们更加容易地学习和理解 SQL 语句。

看看下面的 select 子句，您觉得哪一个更容易理解？

```
SELECT SUM(revenue) total_revenue
     , SUM(CASE WHEN product = 1
                THEN revenue
            END
          ) prod1_revenue
   ...
```

和

```
SELECT SUM(revenue) total_revenue
     , SUM(revenue) FILTER(WHERE product = 1) prod1_revenue
   ...
```

此示例很好地总结了 filter 子句的作用：它是聚合函数的后缀，可以在进行聚合之前根据特定条件，过滤掉相应的行。pivot 技术是 filter 子句最常见的用例。这包括将实体属性值（EAV）模型中的属性转换为表格的列，如果想了解更多的内容，可以参考链接 "filter-Selective Aggregates"（https://modern-sql.com/feature/filter）。

SQLite 从版本 3.25.0 开始，在使用 over 子句的聚合函数中支持了 filter 子句，但是在使用 group by 子句的聚合函数中还不支持。不幸的是，这意味着您仍然无法在 SQLite 中使用 filter 语句来处理上述情况。你必须像以前一样使用 case 表达式。我真的希望 SQLite 在这一点上能尽快做到。

![各数据库 filter 子句支持情况对比](https://mmbiz.qpic.cn/mmbiz_png/sTnayibHfVq7iaS1l2f7sxwxXEZHKcpjJm2ehf4xQIB9HqN1hbygnGPX9iaTrZ3rK71ia4WM81BicsrwG9Jib4ujURfg/640?wx_fmt=png&tp=webp&wxfrom=5&wx_lazy=1#imgIndex=4)

各数据库 filter 子句支持情况对比

## Insert … on conflict（"Upsert"）

SQLite 从版本 3.24.0 开始，引入了 "upsert" 概念：它是一个 insert 语句，可以优雅地处理主键和唯一约束的冲突。您可以选择忽略这些冲突（在 on conflict 语句中什么都不做）或者更新当前行（在 on conflict 语句中执行更新操作）。

这是一个特有的 SQL 扩展，即它不是标准 SQL 的一部分，因此在下面的矩阵中是灰色的。但是，SQLite 遵守与 PostgreSQL 相同的语法来实现此功能 0。该标准提供了对 merge 语句的支持。

与 PostgreSQL 不同，SQLite 在以下语句中存在问题。

```
INSERT INTO target
SELECT *
  FROM source
    ON CONFLICT (id)
    DO UPDATE SET val = excluded.val
```

根据说明文档，这是因为解析器无法判断关键字 ON 是 SELECT 语句的连接约束还是 upsert 子句的开头。你可以通过向查询中添加子句来解决，例如 where true。

```
INSERT INTO target
SELECT *
  FROM source
 WHERE true
    ON CONFLICT (id)
    DO UPDATE SET val = excluded.val
```
![各数据库 Upsert 支持情况对比](https://mmbiz.qpic.cn/mmbiz_png/sTnayibHfVq7iaS1l2f7sxwxXEZHKcpjJmILK6qjXYVNIp3UafTJ9W37Qr4kIb002SdXgogy8Vb9OLs2Ml2dJVqg/640?wx_fmt=png&tp=webp&wxfrom=5&wx_lazy=1#imgIndex=5)

各数据库 Upsert 支持情况对比

- 0：同样记录 insert、update、delete 和 merge 操作的错误信息（"DML error logging"）
- 1：On conflict 语句不能紧挨查询的 from 语句，如果需要，可以添加 where true 语句来分隔。

## 重命名列

SQLite 引入的另一个特有功能是重命名基准数据库表中的列 1。标准的 SQL 不支持此类功能 2。

SQLite 遵循其他产品常用的语法来重命名列：

> “
> 
> ALTER TABLE … RENAME COLUMN … TO

![各数据库重命名列支持情况对比](https://mmbiz.qpic.cn/mmbiz_png/sTnayibHfVq7iaS1l2f7sxwxXEZHKcpjJmaEuib4qHNZo2SFsgFuDBZpBfm0icDnQ84Ip7AdUjic9v6NDx2KFlO9nvA/640?wx_fmt=png&tp=webp&wxfrom=5&wx_lazy=1#imgIndex=6)

各数据库重命名列支持情况对比

- 0：请查阅 sp\_rename。

## 其他消息

在 2018 年，SQLite 除了在 SQL 语法上的变化，还有一些应用程序接口（API）的变化。你可以查阅 sqlite.com（https://www.sqlite.org/news.html）上的新闻部分来了解更详细的消息。

## 脚标

- 0：SQLite 通常遵循 PostgreSQL 语法，Richard Hipp 将此称为 PostgreSQL 会怎么做（WWPD）。
- 1：基准数据库表是指用 Create table 语句创建的数据库表。派生的数据库表（如 Select 语句返回的查询结果集）中的列名可以通过 SELECT 语句、FROM 语句或 WITH 语句来进行改变
- 2：据我所知，也许可以通过可更新视图或派生的列来模拟该功能。

> “
> 
> 原文：https://modern-sql.com/blog/2019-01/sqlite-in-2018
> 
> 作者简介：Markus Winand 提供高效的 SQL 培训。他出版的著作《SQL Performance Explained》已经成为开发人员的标准读物。

，你将获得: **专属的项目实战（4个项目） / 1v1 提问 / 简历修改 / **Java 学习路线 /** 社群讨论 / **学习打卡 / 每月赠书****

- 《仿小红书（微服务架构）》 已完结，基于 Spring Cloud Alibaba + Spring Boot 3.x + JDK 17..., ；演示地址：http://116.62.199.48:7070/
- 《Spring AI 应用（RAG 智能客服）》已完结, 基于 Spring AI + Spring Boot 3.x + JDK 21
- 《秒杀系统设计》正在更新中，单体到微服务高并发架构演进
- **《前后端分离博客项目（全栈开发）》** 已完结,演示链接：http://116.62.199.48/
- 项目阅读地址：https://quanxiaoha.com/column

截止目前， **累计输出 150w+ 字，讲解图 4013+ 张，还在持续爆肝中..** [戳我加入学习，解锁全部项目，已有4900+小伙伴加入](https://mp.weixin.qq.com/s?__biz=MzU4MDUyMDQyNQ==&mid=2247566317&idx=1&sn=ede64496766addace122dd32f6cfbdcf&scene=21#wechat_redirect)

![图片](https://mmbiz.qpic.cn/mmbiz_gif/sTnayibHfVq6k58yrsWFU0zS4MhOFVPH9ib8lFF40iahdfmiaz8IicbvIfia8icp3F3Y5OG1BJAKthCic72w2IiboDVBicYA/640?wx_fmt=gif&from=appmsg&wxfrom=5&wx_lazy=1&randomid=65h7dnft&tp=webp#imgIndex=1)

```
1. 我的私密学习小圈子，从0到1手撸企业实战项目~2. 面试难题：分布式 Session 实现难点，这篇就够！3. Java 生成各种 PDF 实战方案（图片、模板、表格）4. 消息重试框架 Spring-Retry 和 Guava-Retry，这个框架有点意思
```
```
最近面试BAT，整理一份面试资料《Java面试BATJ通关手册》，覆盖了Java核心技术、JVM、Java并发、SSM、微服务、数据库、数据结构等等。获取方式：点“在看”，关注公众号并回复 Java 领取，更多内容陆续奉上。PS：因公众号平台更改了推送规则，如果不想错过内容，记得读完点一下“在看”，加个“星标”，这样每次新文章推送才会第一时间出现在你的订阅列表里。点“在看”支持小哈呀，谢谢啦
```

Read more