---
title: Penpot
type: entity
entity_type: tool
created: 2026-10-21
updated: 2026-10-21
tags: [penpot, design-tools, self-hosting]
status: growing
sources: [raw/Dissecting penpot.md]
---

# Penpot

## 简介

Penpot 是可自行部署的协作设计平台。本库目前掌握的是一份 Docker Compose 安装与镜像检查快照，不能据此概括其全部产品功能或内部实现。见 [[dissecting-penpot]]。

## 关键事实

- 此快照以 `penpotapp/frontend`、`backend`、`admin-console`、`mcp`、`exporter` 五个 Penpot 镜像，加 PostgreSQL、Valkey、MailCatcher 组成实例。`PENPOT_VERSION` 默认 tag `2.18`，所检查 Penpot 镜像的构建标签为 `2.18.3`。见原文 L181–L579、L726–L1391。
- 浏览器入口配置为 `http://localhost:9001`。原文提供的是容器启动输出，没有应用层验收结果。见 L65–L69、L580–L598。
- 此实例的数据持久化依赖 PostgreSQL 卷与素材卷；具体服务关系见 [[penpot-self-hosting]]。

## 在本库中的角色

首个以实际部署记录为中心的设计工具实体；后续可继续积累使用体验、MCP 接口和版本升级的证据。

## 相关页面

- [[dissecting-penpot]]
- [[penpot-self-hosting]]

## 来源

- `raw/Dissecting penpot.md`，Compose 与镜像检查部分。
