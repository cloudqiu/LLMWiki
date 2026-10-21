---
title: Penpot 自托管
type: topic
created: 2026-10-21
updated: 2026-10-21
tags: [penpot, docker, self-hosting]
status: growing
sources: [raw/Dissecting penpot.md]
---

# Penpot 自托管

## 概述

本页归纳 [[dissecting-penpot]] 中 Penpot 2.18 实例的部署结构。它是一份 2026-10-21 摄入的配置快照，不代表所有版本或当前运行状态。

## 服务与数据路径

| 部分 | 此快照中的作用与连接 |
| --- | --- |
| frontend | 通过主机 `9001` 提供入口；依赖 backend、admin-console、mcp、exporter。 |
| backend | 连接 PostgreSQL、Valkey；配置素材文件系统存储与 SMTP。 |
| admin-console | 使用同一数据库与 `PENPOT_SECRET_KEY`，并连接 frontend 内部地址。 |
| mcp、exporter | 独立服务；exporter 依赖 Valkey，mcp 被 frontend 列为依赖。具体协议与调用路径，原文未展示。 |
| PostgreSQL、Valkey | PostgreSQL 持久化数据库；Valkey 的 URI 被 backend 与 exporter 使用，配置注释称其用于 WebSocket 通知。 |
| MailCatcher | 接收示例 SMTP 邮件，Web 界面映射主机 `1080`。 |

上述拓扑来自原文 L181–L579。不能仅凭 `depends_on` 推断所有实际请求路径。

## 配置与运维边界

- `PENPOT_FLAGS` 同时启用 SMTP、prepl、MCP、admin-console，并关闭邮件验证与安全会话 Cookie；这些是快照中的实际示例值。见原文 L55–L61。
- 快照中的 `PENPOT_SECRET_KEY` 和 PostgreSQL 密码是示例值。对外部署前应生成独立密钥、设置实际数据库凭据，启用 HTTPS 并重新检查注册与邮件验证策略。原文 L83–L111 有密钥说明；[Penpot 官方安装指南](https://help.penpot.app/technical-guide/getting-started/docker/)也明确建议 HTTPS，并说明默认卷需备份。
- 需备份 `penpot_postgres_v15` 和 `penpot_assets`。仅看到容器 `Started` / `Healthy` 不足以确认用户文件、登录与导出功能。见 L121–L127、L580–L598。
- 原文是剪藏式笔记，Compose 代码块含非标准空格；如要实际执行，应获取并检查原始 `docker-compose.yaml`，不要直接从笔记复制。

## 页面地图

| 页面 | 类型 | 一句话 |
| --- | --- | --- |
| [[dissecting-penpot]] | source | 此次部署和镜像检查的原始记录摘要。 |
| [[penpot]] | entity | Penpot 在本库中已有证据支持的事实。 |

## 开放问题

- 本地实例是否完成登录、创建文件、导出及 MCP 连接的实际测试？
- 这份快照对应的实例是否只在本机使用？其密钥、密码和邮件策略是否已另行覆盖？
- 若升级，admin-console 与其他服务的版本、备份和迁移步骤应如何核对？

## 来源

- `raw/Dissecting penpot.md`，尤其 L55–L111、L181–L598。
- [Penpot 官方 Docker 安装指南](https://help.penpot.app/technical-guide/getting-started/docker/)（2026-10-21 核对部署、HTTPS 与备份说明）。
